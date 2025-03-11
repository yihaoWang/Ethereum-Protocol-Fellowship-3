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



# 2025.07.12

<!-- Content_END -->
