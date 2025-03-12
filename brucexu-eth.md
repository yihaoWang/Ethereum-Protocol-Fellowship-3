---
timezone: UTC+13
---


# 你的名字

## 自我介绍  
**Bruce**，以太坊狂战士，密码朋克传销专家，极度残酷无情地人行 LLM 建设者。  

## 你认为你会完成本次残酷学习吗？  
✅ **那必须的！**  

## 你的联系方式（推荐 Telegram）  
- 📬 **Telegram**：[t.me/brucexu_eth](https://t.me/brucexu_eth)  
- 🐦 **Twitter/X**：[x.com/brucexu_eth](https://x.com/brucexu_eth)  

---

# Notes

<!-- Content_START -->

# 2025.03.11

## Test https://epf.wiki/#/eps/week4

测试还是很关键的，如果几个客户端输出的不一致，就会出现分叉了。一般测试需要构造一些参数和内容，比如：

- Pre-state： accounts 和 balances、nonces、code 和 storage
- Environment：timestamp、previous RANDAO、block number 等等
- Txs：具体的 tx messages
- Post-state：预期的 state or accounts

Fuzzy state testing，可以创建随机的 smart contract code 来测试可能出现的意外情况。

上面主要是 EVM 测试。Blockchain 的测试就是多加一些 blocks，然后检查 chain head 和 post-state。需要添加一些 invalid block 然后测试失败的情况。

通用的测试用例在这里：https://github.com/ethereum/tests 测试的工具是：https://github.com/ethereum/retesteth。

一些客户端会引用这些测试用例到自己的仓库进行测试，例如：`go-ethereum (Go): Docs, Test location: tests/testdata`。

![image](https://github.com/user-attachments/assets/a78bb472-d1b7-4242-a7bc-04ad589cc451)

基本上就是一些 data 相关的，可能是从真实区块链上面拿到的，然后放在这里用于做单元测试使用。

TODO 看到 ethereum/execution-spec-tests 了 Week.4.EPFsg.Test.Security.Overview.pdf

# 2025.03.12

## 深度看看 Pectra 升级 https://gist.github.com/Thegaram/64b5d43144d5740f01907b48d986b8e7

一般通过类似这样的 EIP-7600 来整理和汇总包含进来的升级，比如这个是在 2024-01-18 创建的，等待了一年 https://eips.ethereum.org/EIPS/eip-7600 准备 last call 了。

### EVM

- EIP-7702: Set EOA account code (https://eips.ethereum.org/EIPS/eip-7702)
  - Add a new tx type that sets the code for an EOA 支持通过 EOA 发送
- EIP-2537: Precompile for BLS12-381 curve operations (https://eips.ethereum.org/EIPS/eip-2537)
- EIP-2935: Save historical block hashes in state (https://eips.ethereum.org/EIPS/eip-2935)

### Blobs & Calldata

- EIP-7691: Blob throughput increase (https://eips.ethereum.org/EIPS/eip-7691)
- EIP-7840: Add blob schedule to EL config files (https://eips.ethereum.org/EIPS/eip-7840)
- EIP-7623: Increase calldata cost (https://eips.ethereum.org/EIPS/eip-7623)

### CL & Staking

- EIP-7685: General purpose execution layer requests (https://eips.ethereum.org/EIPS/eip-7685)
- EIP-6110: Supply validator deposits on chain (https://eips.ethereum.org/EIPS/eip-6110)
- EIP-7002: Execution layer triggerable exits (https://eips.ethereum.org/EIPS/eip-7002)
- EIP-7251: Increase the MAX_EFFECTIVE_BALANCE (https://eips.ethereum.org/EIPS/eip-7251)
- EIP-7549: Move committee index outside Attestation (https://eips.ethereum.org/EIPS/eip-7549)

### EIP-7702 Notes


```
# At first, account is an EOA with no code
> cast code "$alice"
0x

# Set delegated code
> cast send --from "$alice" --private-key "$alice_pk" --auth "$multicall" $(cast az)

# Account now has a special code delegation, stored persistently in state
> cast code "$alice"
0xef0100ca11bde05977b3631167028862be2a173976ca11
```

0xef0100 这是一个特殊前缀，用来表示“给 EOA 地址写入 delegated code”的操作。EIP-7702 让包含这一前缀的 code 被解释成“这段地址在执行时要将调用委托给后面指定的合约”。

MultiCall 是一种智能合约功能，允许在一个交易中执行多个合约调用。

```
> calls=()

> calldata=$(cast calldata "approve(address,uint256)" "$erc20_gateway" "$amount")
> calls+=("($usdt, false, 0, $calldata)")

> calldata=$(cast calldata "depositERC20(address,uint256,uint256)" "$usdt" "$amount" "$gas")
> calls+=("($erc20_gateway, false, $fee, $calldata)")

# ...

> cast send "$alice" "aggregate3Value((address,bool,uint256,bytes)[] calldata calls)" \
    "[${calls[1]}, ${calls[2]}}]" \
     --value $fee \
    --from "$alice" --unlocked
```

之后就可以合并成一个 call 去触发。不然需要分开多个 EOA 签名和 call。

执行以下相关命令进一步测试（https://gist.github.com/Thegaram/51a49a829b2a13ebc88990894a30912b）：

```
# set to an L1 node RPC
eth_rpc="https://eth.llamarpc.com"

# run 7702-enabled local forked network
anvil --fork-url "$eth_rpc" --auto-impersonate --odyssey
```

新开一个窗口：

```
# Anvil dev account
alice="0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266"
alice_pk="0xac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80"

# contracts
usdt="0xdac17f958d2ee523a2206206994597c13d831ec7"
multicall="0xcA11bde05977b3631167028862bE2a173976CA11"
scroll_erc20_gateway="0xd8a791fe2be73eb6e6cf1eb0cb3f36adc9b3f8f9"
scroll_message_queue="0x0d7E906BD9cAFa154b048cFa766Cc1E54E39AF9B"

# message configs
amount="1"
gas_limit="200000"

# estimate cross-layer message fee
fee=$(cast call "$scroll_message_queue" "estimateCrossDomainMessageFee(uint256 _gasLimit)(uint256)" "$gas_limit" --json | jq -r '.[]')

# pre-fund account with ETH
cast rpc anvil_setBalance "$alice" 10000000000000000000

# pre-fund account with USDT
export issuer=$(cast call "$usdt" "owner()(address)")
cast send --from "$issuer" --unlocked "$usdt" "transfer(address to, uint value)" "$alice" "$(( 10 * $amount ))"


```

输出：

```
blockHash            0xab049cfa97ad8326a73c54794562b309ee87d6f7642f9c907c9eaa197665b23d
blockNumber          22028120
contractAddress      
cumulativeGasUsed    63173
effectiveGasPrice    573246114
from                 0xC6CDE7C39eB2f0F0095F41570af89eFC2C1Ea828
gasUsed              63173
logs                 [{"address":"0xdac17f958d2ee523a2206206994597c13d831ec7","topics":["0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef","0x000000000000000000000000c6cde7c39eb2f0f0095f41570af89efc2c1ea828","0x000000000000000000000000f39fd6e51aad88f6f4ce6ab8827279cfffb92266"],"data":"0x000000000000000000000000000000000000000000000000000000000000000a","blockHash":"0xab049cfa97ad8326a73c54794562b309ee87d6f7642f9c907c9eaa197665b23d","blockNumber":"0x1501f58","blockTimestamp":"0x67d100e1","transactionHash":"0x47c0198c5beae7286e3ee98e9f8cc39c0768b66e79ec16e689ec65ea2ba1828b","transactionIndex":"0x0","logIndex":"0x0","removed":false}]
logsBloom            0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000010000000000000000000004000000000000000000000000000000000008000000000000040000000000000000000000000000000000200000000000000100000000000000000000000000000010000000000000000000000000000000000000000000000000000000000000000000100000000000000000000000000080000000000000000000000000000000000000000000000002000000200000000000000000000000002000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
root                 
status               1 (success)
transactionHash      0x47c0198c5beae7286e3ee98e9f8cc39c0768b66e79ec16e689ec65ea2ba1828b
transactionIndex     0
type                 2
blobGasPrice         5663462761
blobGasUsed          
authorizationList    
to                   0xdAC17F958D2ee523a2206206994597C13D831ec7
```

TODO 跑到 Deposit without EIP-7702 https://gist.github.com/Thegaram/51a49a829b2a13ebc88990894a30912b https://gist.github.com/Thegaram/64b5d43144d5740f01907b48d986b8e7




<!-- Content_END -->
