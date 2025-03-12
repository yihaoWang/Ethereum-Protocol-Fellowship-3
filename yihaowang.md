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

### 2025.03.12
共識層
- Validators(驗證者): 

#### Consensus跟Execution之間的互動
共識層與執行層透過 Engine API 進行溝通，過程如下：
1. 驗證者 選擇新的區塊，並透過 Engine API 發送給執行層
2. 執行層 解析區塊中的交易，透過 EVM 執行，更新 State 並驗證區塊完整性
3. 若區塊合法，共識層會透過 LMD-GHOST 選擇最佳鏈，並通知其他驗證者

### 2025.03.11
#### Consensus Layer(共識層)
Ethereum 的共識機制歷經了 工作量證明(PoW)到權益證明(PoS)的轉變

#### 拜占庭將軍問題(Byzantine Generals Problem, BGP)
是一個分散式系統中的容錯問題，描述了在不可靠的通訊環境下，如何讓多個節點就某個決策達成共識，即使其中部分參與者可能是惡意的。這個問題的核心在於 如何確保整個系統能夠在惡意行為的干擾下依然保持一致性（Consensus）

#### PoS(Proof of Stake, 權益證明)
以太坊在 2022 年 9 月 15 日 的 The Merge 升級後，正式由 PoW 轉為 PoS，取消了挖礦，改為由「驗證者（validator）」負責共識

PoS 的運作方式
1. 質押（Staking）
   - 想參與 PoS，需要 質押 32 ETH 成為「驗證者」
   - 這些 ETH 會被鎖定，作為參與共識的保證金
2. 隨機選擇出塊者
   - 以太坊 PoS 採用 Casper FFG + LMD GHOST 機制來選擇出塊者
   - Casper FFG（Finality Gadget）：確保交易的「最終性」（Finality）
   - LMD GHOST（Greedy Heaviest Observed Subtree）：決定哪條鏈是最重（最多驗證者支持），用來防止分叉攻擊
   - 在每個「slot」(12 秒)中，系統會隨機選擇1名驗證者 負責提議區塊
   - 其他驗證者會對該區塊進行投票，決定是否接受
3. 區塊驗證與共識
   - 選出的驗證者會打包交易，創建新的區塊，並廣播至網絡
   - 其他驗證者會檢查該區塊是否正確，然後投票
     - 若區塊通過 2/3 的驗證者投票，則區塊被確認，並成為最終區塊（Finalized）
     - 若驗證者惡意行為(例如提交無效區塊)，則會被懲罰，甚至沒收部分質押的 ETH（Slashing）
4. 區塊獎勵
   - 驗證者透過參與 PoS 來獲得獎勵，主要包括
     - 出塊獎勵(來自新鑄造的 ETH)
     - 交易手續費(但 PoS 下的手續費燃燒機制會減少發行量)
   - 若驗證者 離線或違規，則可能會被懲罰(例如損失部分 ETH)

#### 驗證者
以太坊會從這些驗證者中 隨機選擇 負責提議區塊與驗證交易

如何成為驗證者:
  1. 存入32ETH
  2. 運行驗證者節點，保持 24/7 在線
  3. 選擇運行方式
     - 自行架設節點
     - 使用 Staking 服務（如 Lido、Rocket Pool，這些允許小額質押）
     - 加入交易所的 Staking 計畫（如 Binance、Coinbase Staking）


#### Slot
- Slot（時間槽）是以太坊 PoS 中的一個時間單位，每個 Slot 持續 12 秒
- 在每個 Slot 中，一名驗證者(Validator) 會被隨機選中來 提議(propose)一個新的區塊(Block)
- 其他驗證者則負責 驗證與投票(Attestation)，確保區塊的正確性與共識
- 並非每個 Slot 都一定會產生區塊，有些 Slot 可能會「空缺(missed slot)」，導致該 Slot 沒有區塊


<!-- Content_END -->
