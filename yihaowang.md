---
timezone: UTC+8
---


# Yihao

1. 自我介绍
  - full stack developer
  - 期待能參與 web3 開發學習和分享
2. 你认为你会完成本次残酷学习吗？
  - 會
  - 
3. 你的联系方式（推荐 Telegram）
  - zero5011@gmail.com

## Notes

<!-- Content_START -->

### 2025.03.10

### 2025.03.10

![image](https://github.com/user-attachments/assets/e6ae4706-c3b2-41f7-9f7a-8300c62ac288)

#### Consensus Layer(共識層)
- Validators(驗證者): 負責處理交易、提議和驗證區塊，確保區塊鏈的安全和完整性
- LMD-GHOST(最後投票決定): ETH2.0 採用的 Fork Choice 演算法
- Fork choice: 用來決定哪個分叉應該成為主鏈的一部分
- RANDAO: 負責隨機選出下一個 Proposer(提議者)
- Blobs: Binary Large Object 的縮寫，指的是一種專門設計的數據結構，用於存儲大量數據。在以太坊的上下文中，Blobs 是一種臨時存儲的數據塊，專門用於 Layer 2 解決方案（如 Optimistic Rollups 和 ZK-Rollups）將交易數據提交到以太坊主網。
  
#### Execution Layer(執行層)
- TXs (mempool): 交易首先進入 mempool（記憶池），等待驗證者打包進區塊
- EVM:
  - 執行 Ethereum 智能合約的核心環境
  - 解析智能合約的 opcode（操作碼） 並運行計算
  - 負責管理 Ethereum 的 Gas 消耗
- State (data)
  - 儲存所有帳戶資訊、智能合約狀態、餘額、Nonce 等
  - EVM 透過 State 來讀取與修改帳戶的狀態
- JSON-RPC API: 讓 使用者 或 Web3 應用 與 Ethereum 節點互動的 API


#### Consensus跟Execution之間的互動
共識層與執行層透過 Engine API 進行溝通，過程如下：
1. 驗證者 選擇新的區塊，並透過 Engine API 發送給執行層
2. 執行層 解析區塊中的交易，透過 EVM 執行，更新 State 並驗證區塊完整性
3. 若區塊合法，共識層會透過 LMD-GHOST 選擇最佳鏈，並通知其他驗證者

### 2025.03.11

<!-- Content_END -->
