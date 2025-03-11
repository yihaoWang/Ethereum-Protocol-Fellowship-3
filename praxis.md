---
timezone: UTC+8
---

# praxis

1. 自我介绍 
- 大家好，我叫praxis，目前在一家web3公司做基础设施,devops.主要负责区块链节点运维和以太坊质押，对以太坊协议底层技术有浓厚兴趣，希望能够跟大家一起学习进步。
2. 你认为你会完成本次残酷学习吗？   
- 会
3. 你的联系方式（推荐 Telegram）   
- @praxis_jw

## Notes

<!-- Content_START -->

### 2025.03.10

笔记内容
- 第一周笔记都会记录在这里，课程有些吃力，需要多花时间去理解才能输出。
- https://skrbug.notion.site/Week01-1b1ab1eba062806991eee219ea02acb1?pvs=4
<!-- Content_END -->

<!-- Content_START -->
### 2025.03.11
> 3.10 3.11 在看https://arxiv.org/pdf/2003.03052.pdf 这篇Gasper paper， 看的很慢，表示看到第四章开始有点吃力，需要多看几遍。 里面有太多关键字需要去查阅
> Gasper = GOHST + Cassper
- Gasper 
  - 由于 Casper 是一种确定性小工具，而不是完整的协议。 不同分支上的两个检查点不可能同时被确定，除非一组拥有超过一定总数的权益的验证者可证明违反了协议（因此可以被追究责任）。
  - 对应的是以太坊当中 epoch slot 等概念，以及对多签的slashed
- LMD GHOST 
  - The Greediest Heaviest Observed SubTree rule (GHOST) is a fork-choice rule introduced by Som-polinsky and Zohar
  - 以太坊POS进行修改，提出 `LMD GHOST`  Latest Message Driven Greediest Heaviest Observed SubTree 
  - LMD GHOST 核心:  哪边树所质押的eth最多，就以这棵子树作为标准

- 如何防止不诚实的验证者 出块
  - A dishonest validator can theoretically create a block with a duplicate slot number as an existing block, but we can suppose the digital signatures and the pseudorandom generator for block proposal selection are set up so such behavior would be verifiably caught.
  - 通过随机数和签名，其他验证者可以校验 

<!-- Content_END -->

