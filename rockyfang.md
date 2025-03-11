---
timezone: UTC+8
---

> 请在上边的 timezone 添加你的当地时区(UTC)，这会有助于你的打卡状态的自动化更新，如果没有添加，默认为北京时间 UTC+8 时区


# RockyFang

1. 自我介绍: 我叫rocky，來自深圳，目前在一家知名交易所从事后端开发工作，平时的工作也会跟链打交道，希望能在这里学到更多链上相关的知识。感谢提供学习机会。
笔记按内容整理链接：https://github.com/rockyfang2024/Web3Learn/tree/main/ETH%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0
2. 你认为你会完成本次残酷学习吗？   会
3. 你的联系方式（推荐 Telegram）  https://t.me/rockyfang2024
## Notes

<!-- Content_START -->

### 2025.03.10

笔记内容


#### 一、水龙头

视频资源
- [如何获得以太坊Sepolia测试网络的ETH. Sepolia测试水龙头推荐](https://www.bilibili.com/video/BV1Vm411o7xS/?spm_id_from=333.337.search-card.all.click&vd_source=9e7f96609fdf67741d9bbf68913badca)

错误提示：The faucet denied starting a session because your wallet does not meet the minimum passport score.

遇到“水龙头拒绝启动会话，因为您的钱包不符合最低护照积分”这种错误提示，通常是指您的钱包（或账户）未达到某种要求的评分或条件。这种情况通常与使用水龙头（faucet）相关，水龙头为用户提供小额的加密货币，作为测试或开发的目的。

#### 二、以太坊节点类型及其区别

以太坊网络中有多种类型的节点，每种节点承担不同的角色和功能。以下是主要节点类型及其特点：

##### 1. 全节点 (Full Node)
- **定义**：全节点存储以太坊区块链的完整历史记录，包括所有交易和智能合约。
- **功能**：
  - 验证和存储所有交易与区块。
  - 提供网络的安全性，通过对交易进行验证来防止欺诈。
  - 可以直接与其他节点进行交互，参与矿池或验证者。
- **优势**：
  - 具有完整的数据，能够参与网络的所有活动。
- **缺点**：
  - 存储需求大，下载区块链数据占用较多的存储空间。

##### 2. 轻节点 (Light Node)
- **定义**：轻节点只存储区块头信息，而不存储完整的交易记录。
- **功能**：
  - 通过请求其他全节点获取所需信息（如交易状态和区块数据）。
  - 适合低功耗和存储限制的设备（如手机和嵌入式设备）。
- **优势**：
  - 启动速度快，存储需求低。
- **缺点**：
  - 依赖全节点提供数据，无法独立验证交易，安全性相对较低。

##### 3. 矿工节点 (Miner Node)
- **定义**：矿工节点是全节点的一种，专门用于挖矿（即创造新区块）。
- **功能**：
  - 通过解决复杂的数学问题来验证交易并打包到新区块中。
  - 赚取区块奖励和交易费用。
- **优势**：
  - 参与区块生产，可以获得经济收益。
- **缺点**：
  - 对计算能力和电力消耗的要求较高。

##### 4. 归档节点 (Archive Node)
- **定义**：归档节点是一种特殊类型的全节点，存储所有历史状态数据。
- **功能**：
  - 保存每个区块的状态，包括所有账户的余额、合约的存储等。
  - 允许查询任意时间点的状态。
- **优势**：
  - 能够提供详细的状态历史，用于数据分析和审计。
- **缺点**：
  - 存储需求极高，通常只有大型服务提供商或开发者使用。

##### 5. 验证者节点 (Validator Node)
- **定义**：在以太坊 2.0 的权益证明（PoS）机制中，验证者节点负责验证交易并创建新区块。
- **功能**：
  - 质押（staking）一定数量的 ETH 作为验证保证，参与新区块的验证。
- **优势**：
  - 相较于矿工，不需要高额的计算资源，节能环保。
- **缺点**：
  - 参与质押需要一定数量的 ETH，可能对普通用户造成门槛。

##### 总结
不同类型的以太坊节点在网络中扮演着各自独特的角色，用户可以根据其需求选择相应的节点类型。全节点提供更高的安全性和自主性，而轻节点和归档节点则为特定用途提供便利。

#### 三、Solidity

视频资源
-[（32 小时最全课程）区块链，智能合约 & 全栈 Web3 开发](https://www.bilibili.com/video/BV1Ca411n7ta?spm_id_from=333.788.videopod.episodes&vd_source=9e7f96609fdf67741d9bbf68913badca&p=14)


##### Remix

[Remix](https://remix.ethereum.org/)

视频资源
- [10分钟学会使用Remix创建、编译、部署、调试智能合约](https://www.bilibili.com/video/BV1WT411a7N7/?spm_id_from=333.337.search-card.all.click&vd_source=9e7f96609fdf67741d9bbf68913badca)

文件类型
- .ts  TypeScript
- .sol Solidity

快捷键
- cmd + S 编译代码
##### 定义license和分享规则

```
// SPDX-License-Identifier: GPL-3.0
```

##### 约定版本号

约定版本号 大于0.4.22且小于0.9.0

```
pragma solidity >=0.4.22 <0.9.0;
```
或者
```
pragma solidity 0.8.7;
```
或者
```
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.7; // 任何比0.8.7更新的版本都可以
```
##### 定义合约

```
contract name {}
```

##### 基础数据类型

[官方文档](https://docs.soliditylang.org/en/v0.8.14/types.html)

基础数据类型
- bool
- uint
    - unit8 // 8个bit
    - unit256 // 256个bit
- int
- address
- bytes


### 2025.03.11



获取API KEY

https://developer.metamask.io/

#### 获取最新区块号

```js
const { ethers } = require("ethers");

// 连接到以太坊主网
const provider = new ethers.JsonRpcProvider("https://mainnet.infura.io/v3/your-infura-api-key");

async function main() {
    // 获取最新区块号
    const blockNumber = await provider.getBlockNumber();
    console.log(`Latest block number: ${blockNumber}`);
}

main();

```

#### 获取钱包余额

```js
const { ethers } = require("ethers");

// 使用 Infura 的提供器
const provider = new ethers.JsonRpcProvider("https://mainnet.infura.io/v3/YOUR_INFURA_PROJECT_ID");

// 查询钱包余额
async function getWalletBalance(address) {
    const balance = await provider.getBalance(address);
    console.log(`Balance of ${address}: ${ethers.formatEther(balance)} ETH`);
}

const walletAddress = "Your walletAddress"; // 示例地址
getWalletBalance(walletAddress);

```

官方文档
https://docs.metamask.io/services/reference/ethereum/

#### 使用测试网络发起交易

```js
// 导入 ethers.js
const { ethers } = require("ethers");

// 配置 Infura 的 Sepolia 连接信息
const INFURA_API_KEY = "INFURA_API_KEY";  // 替换为你的 Infura API Key
const provider = new ethers.JsonRpcProvider(`https://sepolia.infura.io/v3/${INFURA_API_KEY}`);

// 私钥 (不要在生产环境中暴露真实的私钥!)
const privateKey = "Your Private Key"; // 替换为你的钱包私钥
const wallet = new ethers.Wallet(privateKey, provider); // 使用私钥和提供者连接钱包

// 接收方地址和转账金额
const recipient = "Accept Address"; // 替换为目标接收地址
const amountInEth = "0.01"; // 要发送的金额 (Sepolia ETH)

async function sendTransaction() {
    try {
        // 构造并发送一笔交易
        const tx = await wallet.sendTransaction({
            to: recipient,
            value: ethers.parseEther(amountInEth), // 将 ETH 转换为 Wei
        });

        console.log(`Transaction sent! Hash: ${tx.hash}`);

        // 等待交易确认
        const receipt = await tx.wait();
        console.log("Transaction confirmed:", receipt);

    } catch (error) {
        console.error("Error sending transaction:", error);
    }
}

// 调用函数
sendTransaction();


```

结果返回

```
Transaction sent! Hash: xxxxxxxx
Transaction confirmed: TransactionReceipt {
  provider: JsonRpcProvider {},
  to: 'xxxxx',
  from: 'xxxxxx',
  contractAddress: null,
  hash: 'xxxxxxxx',
  index: 170,
  blockHash: 'xxxxx',
  blockNumber: 7879017,
  logsBloom: '0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000',
  gasUsed: 21000n,
  blobGasUsed: null,
  cumulativeGasUsed: 15194128n,
  gasPrice: 12331105n,
  blobGasPrice: null,
  type: 2,
  status: 1,
  root: undefined
}

```

#### 测试网浏览器

- Sepolia 测试网
    - 区块链浏览器： https://sepolia.etherscan.io
-  Goerli 测试网
    - 区块链浏览器： https://goerli.etherscan.io
- 主网（Mainnet）
    - https://etherscan.io

免费测试币：
    - https://www.alchemy.com/faucets/ethereum-sepolia


#### web3.js 和 ethers.js
**`web3.js`** 和 **`ethers.js`** 是与以太坊网络交互的两个常见 JavaScript 库，它们各有优点和适用场景。两者的主要功能类似，但在设计、易用性、模块化、安全性等方面存在一些重要区别。

 **适用场景**

| 场景                          | web3.js                                                                            | ethers.js                                                                          |
| ----------------------------- | ----------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| **小型轻量的前端 DApp**       | 不推荐，功能臃肿，体积较大。                                                       | 推荐，体积小（大约 88kB），加载速度快。                                           |
| **复杂的后端应用程序**        | 比较适合，历史悠久，功能全面。（但仍需对接其他模块完成细化工作）                     | 更推荐，模块化设计使得分层解耦较容易，工具链完整且稳定。                           |
| **离线钱包或签名功能**        | 支持较初级的离线签名功能，但不够完善。                                              | 推荐，内置支持离线交易构造、签名，还有更强的密钥管理工具和硬件钱包集成支持。       |
| **老项目迭代/维护**           | 如果早期项目基于 web3.js 开发，直接扩展可以降低学习成本。                          | 如果重写或升级为目标，可选择更轻量的 ethers.js，与现代开发理念更贴合。             |
| **多链扩展（EVM 兼容链）**    | 支持但集成起来较繁琐。                                                             | 更推荐，对多链支持较好，API 结构更加灵活易扩展。                                   |

---


| 指标               | **web3.js**                                | **ethers.js**                              |
| ------------------ | ------------------------------------------ | ------------------------------------------ |
| **体积**          | 较大                                      | 较小                                      |
| **模块化设计**    | 无模块化，代码臃肿                        | 模块化，按需加载                          |
| **API 设计**      | API 较老，存在兼容性问题                  | 现代化 API，设计简洁易用                   |
| **私钥管理**      | 无内置密钥工具                            | 提供完整的密钥管理工具                     |
| **多链支持**      | 支持多链但有一定开发成本                  | 支持更灵活的多链环境优化                   |
| **适用场景**      | 历史项目或者初级开发                      | 现代 DApp 和复杂系统开发更适合             |

**总体建议：**
- **web3.js**：适合维护老项目，或者在熟悉其原有生态情况下轻松开发。
- **ethers.js**：更推荐用于现代项目，它更轻量、更安全、模块化，且开发体验更好。






<!-- Content_END -->
