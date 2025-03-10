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

<!-- Content_END -->
