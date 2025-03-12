---
timezone: UTC+8
---

> 请在上边的 timezone 添加你的当地时区(UTC)，这会有助于你的打卡状态的自动化更新，如果没有添加，默认为北京时间 UTC+8 时区


# 你的名字

1. 自我介绍
   Ray，一个准备深入学习以太坊的人
3. 你认为你会完成本次残酷学习吗？
   会的
5. 你的联系方式（推荐 Telegram）
   TG：@rayoo_eth

## Notes

<!-- Content_START -->

### 2025.03.10
这次共学用来研究 go-ethereum 代码，代码版本：https://github.com/ethereum/go-ethereum/commit/4cdd7c86314e5f5a98fa68e928deaa99c026f40d。

go-ethereum 代码结构及各个模块功能如下：
- accounts：管理以太坊账户，包括公私钥对的生成、签名验证、地址派生等
- beacon：处理与以太坊信标链（Beacon Chain）的交互逻辑，支持权益证明（PoS）共识的合并（The Merge）后功能
- build：构建脚本和编译配置（如 Dockerfile、跨平台编译支持）
- cmd：命令行工具入口，包含多个子命令
- common：通用工具类，如字节处理、地址格式转换、数学函数
- consensus：定义共识 API，包括之前的工作量证明（Ethash）和单机权益证明（Clique）以及 Beacon engine 等
- console：提供交互式 JavaScript 控制台，允许用户通过命令行直接与以太坊节点交互（如调用 Web3 API、管理账户、查询区块链数据）
- core：区块链核心逻辑，处理区块/交易的生命周期管理、状态机、Gas计算等
- crypto：加密算法实现，包括椭圆曲线（secp256k1）、哈希（Keccak-256）、签名验证
- docs：文档（如设计规范、API 说明）
- eth：以太坊协议的完整实现，包括节点服务、区块同步（如快速同步、归档模式）、交易广播等
- ethclient：实现以太坊客户端库，封装 JSON-RPC 接口，供 Go 开发者与以太坊节点交互（如查询区块、发送交易、部署合约）
- ethdb：数据库抽象层，支持 LevelDB、内存数据库等，存储区块链数据（区块、状态、交易）
- ethstats：收集并上报节点运行状态到统计服务，用于监控网络健康状态
- event：实现事件订阅与发布机制，支持节点内部模块间的异步通信（如新区块到达、交易池更新）
- graphql：提供 GraphQL 接口，支持复杂查询（替代部分 JSON-RPC 功能）
- internal：内部工具或限制外部访问的代码
- log：日志系统，支持分级日志输出、上下文日志记录
- mertrics：性能指标收集（Prometheus 支持）
- miner：挖矿相关逻辑，生成新区块并打包交易（PoW 场景下）
- node：节点服务管理，整合 P2P、RPC、数据库等模块的启动与配置
- p2p：点对点网络协议实现，支持节点发现（如Kademlia）、数据传输、加密通信
- params：定义以太坊网络参数（主网、测试网、创世区块配置）
- rlp：实现以太坊专用的数据序列化协议 RLP（Recursive Length Prefix），用于编码/解码区块、交易等数据结构
- rpc：实现 JSON-RPC 和 IPC 接口，供外部程序与节点交互
- signer：交易签名管理（硬件钱包集成）
- tests：集成测试和状态测试，验证协议兼容性
- trie & triedb：默克尔帕特里夏树（Merkle Patricia Trie）的实现，用于高效存储和验证账户状态、合约存储


### 2025.03.11
geth 节点是如何启动的？

TL;DR：geth 的启动的入口是在 cmd/geth 下，在启动时，会初始化交易池、后端 RPC 服务、p2p 模块、状态数据库、链区块数据库等模块，等待这些模块都初始化之后，节点启动完成。 


geth 程序入口在 cmd/geth/main.go 中实现， 使用了 https://github.com/urfave/cli 库来定义程序的入口，这个定义在 main.go 中的 init 方法中定义了 Action 是 geth 函数：
![image](https://github.com/user-attachments/assets/965b788b-289c-4bb1-8be0-5d3d2eba25e1)

在 geth 函数中会做一系列的准备，并启动 node，其中准备工作是在 makeFullNode 函数中来实现的：
![image](https://github.com/user-attachments/assets/11e304cb-0287-4d6a-acd6-1f8e5bcce845)

在这个函数中去注册和实现以太坊真正的需要实现的一些服务，比如下面的 utils.RegisterEthService 就是启动以太坊节点抽象的实现：
![image](https://github.com/user-attachments/assets/c602d45a-d945-4e5d-807e-a2b120025cd9)

通过 New 函数来实现以太坊节点：
![image](https://github.com/user-attachments/assets/b44ac0ab-8be4-40d5-9c4c-7a35072bb088)

geth 整个节点被抽象成一个 Ethereum 的结构体，在 eth/backend.go 中，eth.New() 就是实例化这个 Ethereum 节点的函数：
```Go
type Ethereum struct {
	// core protocol objects
	config         *ethconfig.Config
	txPool         *txpool.TxPool
	localTxTracker *locals.TxTracker
	blockchain     *core.BlockChain

	handler *handler
	discmix *enode.FairMix

	// DB interfaces
	chainDb ethdb.Database // Block chain database
   //....
}
```

`eth.New` 主要用来实现 Ethereum 的初始化，其中会有一些参数和当前节点状态的检查，也会执行一些初始化的操作.

初始化链数据库：
![image](https://github.com/user-attachments/assets/0d66a953-a2c1-4c95-822b-af9012228183)

初始化 BlockChain：
![image](https://github.com/user-attachments/assets/357e6e53-ec24-4e05-9d81-c3d399f9c360)

初始化交易池：分为 blob 交易的交易池和其他交易的交易池：
![image](https://github.com/user-attachments/assets/0fc0dbb6-944d-4d06-9675-2c12152eed1d)

初始化 handler，handler 代表 Ethereum 协议的入口，用来同步节点数据、接受 p2p 交易消息广播、并将新的交易添加到交易池中：
![image](https://github.com/user-attachments/assets/6af7bc78-bf24-42db-bae8-6a8d72782613)

实例化 RPC 的服务端，并注册 gasPrice 的预言机：
![image](https://github.com/user-attachments/assets/493b1bd3-5af0-4283-aa3a-35a7eba42d18)

RPC 会在 node 中启动，RPC 接口通过注册的方式注册到 node.go 中：

初始化配置
```Go
func New(conf *Config) (*Node, error) {
    //.....
    // Register built-in APIs.
    node.rpcAPIs = append(node.rpcAPIs, node.apis()...)
    // Configure RPC servers.
	node.http = newHTTPServer(node.log, conf.HTTPTimeouts)
	node.httpAuth = newHTTPServer(node.log, conf.HTTPTimeouts)
	node.ws = newHTTPServer(node.log, rpc.DefaultHTTPTimeouts)
	node.wsAuth = newHTTPServer(node.log, rpc.DefaultHTTPTimeouts)
	node.ipc = newIPCServer(node.log, conf.IPCEndpoint())
    //.....
}
```
启动节点
```Go
func (n *Node) Start() error {
    // .....
	// open networking and RPC endpoints
	// 这里会去启动 rpc 服务
	err := n.openEndpoints()
    //.....
}
```

然后 client 就可以连接节点，开始访问 RPC，RPC 的实现细节在 `internal` 包中实现，比如 eth namespace 在 inernal/ethapi 下实现，所有的接口定义在 backend.go 中。

注册 api:

```Go
func GetAPIs(apiBackend Backend) []rpc.API {
	nonceLock := new(AddrLocker)
	return []rpc.API{
		{
			Namespace: "eth",
			Service:   NewEthereumAPI(apiBackend),
		}, {
			Namespace: "eth",
			Service:   NewBlockChainAPI(apiBackend),
		}, {
			Namespace: "eth",
			Service:   NewTransactionAPI(apiBackend, nonceLock),
		}, {
			Namespace: "txpool",
			Service:   NewTxPoolAPI(apiBackend),
		}, {
			Namespace: "debug",
			Service:   NewDebugAPI(apiBackend),
		}, {
			Namespace: "eth",
			Service:   NewEthereumAccountAPI(apiBackend.AccountManager()),
		}, {
			Namespace: "personal",
			Service:   NewPersonalAccountAPI(apiBackend, nonceLock),
		},
	}
}
```

### 2025.03.12
交易是如何被节点处理的（1）

向以太坊节点发送交易的方式由两种：

- `SendTransaction`
- `SendRawTransaction`

SendTransaction 需要节点本身有对应的私钥来对签名交易，SendRawTransaction 则是需要提前对交易签名，然后将签好名的交易提交到节点，这种方式更常用，使用 Metamask 等钱包使用的就是这种方式。

在这里以 SendRawTransaction 为例，在节点启动之后，节点会启动以一个 API 模块，用来处理外部的各类 API 请求，SendRawTransaction 就是其中的一个 API，源代码在 `internal/ethapi/api.go` :
```Go
func (api *TransactionAPI) SendRawTransaction(ctx context.Context, input hexutil.Bytes) (common.Hash, error) {
	tx := new(types.Transaction)
	if err := tx.UnmarshalBinary(input); err != nil {
		return common.Hash{}, err
	}
	return SubmitTransaction(ctx, api.b, tx)
}
```

当前以太坊总共支持五类交易，通过 `tx.UnmarshalBinary` 方法，将对应的交易类型解析出来，并且将交易数据反序列化。

五类交易：

- LegacyTxType
- AccessListTxType
- DynamicFeeTxType
- BlobTxType
- SetCodeTxType

在完成交易的反序列化之后，就会调用 `SubmitTransaction` 函数向交易池提交交易，SendTransaction 和 SendRawTransaction 都会使用这个函数来向交易池提交交易。

检查 gas fee 是否合理：
![image](https://github.com/user-attachments/assets/c31c4b78-18ec-4acf-8e2d-e8ece01ed6cb)

EIP-155 通过在交易签名中引入 chainID 参数，解决了跨链交易重放问题。该检查确保当节点配置开启 EIP155Required 时，所有通过 RPC 提交的交易都必须符合这个标准。
![image](https://github.com/user-attachments/assets/8293518e-24ce-4d35-9341-3c3c30d339dc)

提交交易到交易池：
![image](https://github.com/user-attachments/assets/14e12d3a-7dc5-4c2c-8617-5eaa7aca6b12)

![image](https://github.com/user-attachments/assets/80b12d41-34df-4263-bb50-519c2c638b65)

在交易池中，会根据对应的交易类型来匹配对应的交易池，如果是 blob 交易，那么就会放入 BlobPool ，否则放入LegacyPool 。
![image](https://github.com/user-attachments/assets/fe592681-3ccc-4500-a219-db0e569534dc)

到这里，用户提交的交易就处理完成了，后续的步骤会由节点来处理。

如果在交易打包之前，重新发送了一笔交易，新的交易设置了新的 gasPrice 和 gasLimit，就会把原来交易池中的交易删除，替换成了新的 gasPrice 和 gasLimit 之后重新返回到交易池中。
![image](https://github.com/user-attachments/assets/fd852ae3-ed64-4814-8d99-d8ebcd7aaebc)


<!-- Content_END -->
