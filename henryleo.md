---
timezone: UTC+8
---

> 请在上边的 timezone 添加你的当地时区(UTC)，这会有助于你的打卡状态的自动化更新，如果没有添加，默认为北京时间 UTC+8 时区


# 你的名字

1. 自我介绍 hi，我是henryleo，生物信息工程师，开放科学/DeSci爱好者，同时也对代币经济学、隐私和区块链在社会治理中的作用很感兴趣。目前专注合成生物学工作。
2. 你认为你会完成本次残酷学习吗？ 我想我可以！
3. 你的联系方式 https://github.com/henrycyberbio/

## Notes

<!-- Content_START -->

### 2025.03.10

#### 用户交易的Gas费
Gas费=基础费用+优先费，这个费用不能低于Gas限额，Gas限额和基础费用由以太坊决定，优先费是给验证者的小费，由用户决定。这意味着用户只需要考虑优先费即可。
##### 第一种方式：完全手动设定

例如，Gas限额=21000Gwei，基础费用为100Gwei，优先费为10Gwei，则用户实际需要支付的费用为：
$$
Gas=GasLimit*(Base+Priority)=21000*(100+10)Gwei=2310000Gwei=0.00231ETH
$$
##### 第二种方式：设定最高收费
maxFeePerGas 最高收费

当用户设定的最高收费大于基础费用与优先费之和，则会退回多余部分：
$$
repay=maxFeePerGas-(BaseFee+Priority)
$$
当最高收费小于基础费用与优先费之和，则需要排队

##### 第三种方式：设定最高优先费
maxPriorityFeePerGas 最高优先费

当使用这种设置时，假设不需要排队，则收费肯定大于需要的费用：
$$maxFeePerGas>(BaseFee+Priority)$$
移项，即，当优先费小于最大费用与基础费用之差时，必然上链：
$$Priority<maxFeePerGas-BaseFee$$
那么为了节约Gas费或避免巨额Gas费的情况，可以设定最高优先费 maxPriorityFeePerGas：
$$Priority=min(maxPriorityFeePerGas, (maxFeePerGas-BaseFee))$$
这个公式意味着当网络不繁忙时（`maxFeePerGas-BaseFee`较小），选择立即成交的优先费用；当网络繁忙时，可以选择预期的最高优先费，开始排队。


### 2025.03.11

<!-- Content_END -->
