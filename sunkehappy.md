---
timezone: UTC+8
---

> 请在上边的 timezone 添加你的当地时区(UTC)，这会有助于你的打卡状态的自动化更新，如果没有添加，默认为北京时间 UTC+8 时区


# Calvin Sun

1. 自我介绍: 我來自中国，是一名前端开发工程师，目前在上海工作
2. 你认为你会完成本次残酷学习吗？   会
3. 你的联系方式（推荐 Telegram）  https://t.me/calvinsun_hk

## Notes

<!-- Content_START -->

### 2025.03.10

#### 以太坊的设计
想要明白以太坊的设计，我们就得了解下他的先驱还有文化。Unix的模块化对以太坊的影响很大，以太坊的模块化设计也是受到了Unix的影响。自由软件运动对以太坊的影响也很大，以太坊的智能合约就是受到了自由软件运动的影响。非对称加密开启了加密货币的时代，以太坊的智能合约也是受到了非对称加密的影响。

#### 以太坊协议的设计
以太坊从比特币，还有别的背景（上面有，比如Unix，自由软件行动等）出汲取灵感，这些在黄皮书中有。[执行规范](https://github.com/ethereum/execution-specs), 还有[共识规范](https://github.com/ethereum/consensus-specs)，目前都是用Python实现的。

#### 以太坊的实现与开发
一个以太坊客户端会实现共识层还有执行层，运行了这个客户端并且联网的，我们称之为节点。以太坊里面不限制开发语言。

#### 以太坊里面里面的测试

以太坊里面会有各种各样的改动，还有各种技术实现的客户端，所以需要各种各样的测试。有一些是在测试客户端，还有些是在模拟测试网络。

#### 协调
一般协调是由[PM repo](https://github.com/ethereum/pm)定期会议发起的，社区的idea还有proposal，是通过[EIP process](https://eips.ethereum.org/EIPS/eip-1)来协调的。

#### 额外的学习和练习
1. [以太坊解谜](https://ethereum.org/quizzes)
2. [Absolute Essentials of Ethereum](https://www.routledge.com/Absolute-Essentials-of-Ethereum/Dylan-Ennis/p/book/9781032334189)
3. [Mastering Ethereum](https://github.com/ethereumbook/ethereumbook)

#### 额外的笔记
质押：从2022年the merge开始，以太坊从PoW转向了PoS。质押是验证者为了保护网络，还有获得收益而采取的行动。验证者会锁定一定数量的ETH，然后运行一个全节点，然后验证交易。如果验证者诚实的去验证交易，那么他们就可以获得奖励。如果他们作恶，或者长期离线，那么他们就会被惩罚。

有了质押之后，以太坊就不需要像比特币那样需要大量的算力来保证网络安全了，这样也降低了能源的消耗，减少对环境的影响。

<!-- Content_END -->
