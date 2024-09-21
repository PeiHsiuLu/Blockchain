# Blockchain
台大薛智文教授：區塊鍊導論課程學習筆記

# Blockchain的 Hello World
[build OurChain line by lineLinks to an external site.](https://hackmd.io/Bo8C0LogQfmq_eSuOExr0w)  
# 期末專題

# 參考書籍
[1.Mastering Bitcoin 2nd Edition - 繁中](https://github.com/cypherpunks-core/bitcoinbook_2nd_zh)  
[2.Mastering Ethereum - 繁中](https://github.com/ChenPoWei/ethereumbook_zh/)  
[3.區塊鏈原理設計與應用](https://poweichen.gitbook.io/blockchain-guide-zh)  

# 上課筆記&學習紀錄
[1.9/16筆記](#916筆記)  
[2.9/23筆記](#923筆記)  
[3.9/30筆記](#930筆記)

-----
## 9/16筆記

### 1. 區塊鏈結構
區塊ID鏈接：每個區塊包含上一個區塊的ID（通常是哈希值），這種鏈接形成了區塊鏈，確保了順序和完整性。
### 2. 算力與挖礦
* 算力（Hash Rate）：衡量礦工解決PoW問題的計算能力，算力越高，挖出新區塊的速度越快。
* 礦池（Mining Pool）：多位礦工合力集中算力，以加快找到新區塊的機會。
### 3. 工作量證明（PoW）
* 工作量證明（PoW）：要求礦工進行大量計算以找到符合條件的哈希值。算力越高，找到哈希值的速度越快。
* 哈希值目標：共識算法設定哈希目標，礦工需找到比目標小的哈希值。
### 4. 礦工的角色與哈希值
* 礦工角色：礦工運算以尋找符合目標的哈希值，成功後才能打包交易並生成新區塊。
### 5. 區塊鏈共識算法與貝斯定理
* 貝斯定理：應用於區塊鏈共識算法，幫助節點達成一致。
### 6. 區塊鏈應用問題
* 區塊鏈儲存與利息問題：區塊鏈上挖到礦後如何儲存與分配資金，以及貨幣過量的風險問題。
### 7. 區塊鏈應用
* 智能合約：當交易變得複雜時，這些交易便成為智能合約。
* ID與身分驗證：在區塊鏈應用中，ID與第三方驗證至關重要。
### 8. 比特幣挖礦競賽
* PoW機制：確保交易安全和去中心化。礦工競爭解決複雜數學問題以挖出區塊，並獲得比特幣獎勵。
* 競賽目的：保障交易的安全性、新比特幣發行及系統去中心化。
### 9. 比特幣交易過程
* 交易輸入與輸出：比特幣交易涉及輸入與輸出，輸出腳本限制了誰可以提取比特幣。
* 找零機制：輸入需完全消耗，找零會自動返回給發起人。
* 交易費用：手續費由用戶自訂，礦工獲取這些費用作為報酬。
### 10. 挖礦機制與區塊確認
* 交易確認：越早被確認的交易越安全，並能防止雙重支付。
* 交易優先級與失敗風險：支付較高手續費可提升交易優先處理，減少等待和失敗風險。

## 9/23筆記
### bitcoinbook_2nd_zh 第三章學習筆記
如果要開發比特幣，必須先在linux環境創建 BitcoinCore 的開發環境。  
開發環境以後，可以使用 bitcoind --help 尋找到對自己有幫助的指令。 
以下是幾個常見的好用指令： 
- 將bitcoin core 作為後端運行的指令(很重要，許多指令開始之前必須先用到這個指令
  ```bash
  bitcoind -daemon
  ```

- 查閱節點的進程和運行狀態  
```bash
bitcoin-cli getblockchaininfo
```
範例：  
```json
{
  "chain": "main",  
  "blocks": 0,  
  "headers": 83999,  
  "bestblockhash": "000000000019d6689c085ae165831e934ff763ae46a2a6c172b3f1b60a8ce26f",  
  "difficulty": 1,  
  "mediantime": 1231006505,  
  "verificationprogress": 3.783041623201835e-09,  
  "chainwork": "0000000000000000000000000000000000000000000000000000000100010001",  
  "pruned": false,  
  [...]  
}
```
這展示了區塊鏈高度為0個區塊，有83999個區塊頭的節點。節點先獲取最長鏈的區塊頭，然後繼續下載完整區塊。 
- 檢查區塊
```bash
bitcoin-cli getblockhash (欲查閱的第幾個區塊)
```
這時候，會返回區塊的雜湊值    
- 查閱該區塊的資訊
```
 bitcoin-cli getblock (該區塊的雜湊值)
```
這時候，會返回一個 json 檔，返回該區塊的所有資訊  
示例如下：  
```json
{
  "hash": "00000000839a8e6886ab5951d76f411475428afc90947ee320161bbf18eb6048",
  "confirmations": 158577,
  "height": 1,
  "version": 1,
  "versionHex": "00000001",
  "merkleroot": "0e3e2357e806b6cdb1f70b54c3a3a17b6714ee1f0e68bebb44a74b1efd512098",
  "time": 1231469665,
  "mediantime": 1231469665,
  "nonce": 2573394689,
  "bits": "1d00ffff",
  "difficulty": 1,
  "chainwork": "0000000000000000000000000000000000000000000000000000000200020002",
  "nTx": 1,
  "previousblockhash": "000000000019d6689c085ae165831e934ff763ae46a2a6c172b3f1b60a8ce26f",
  "nextblockhash": "000000006a625f06636b8bb6ac7b960a8d03705d1ace08b1a19da3fdcc99ddbd",
  "strippedsize": 215,
  "size": 215,
  "weight": 860,
  "tx": [
    "0e3e2357e806b6cdb1f70b54c3a3a17b6714ee1f0e68bebb44a74b1efd512098"
  ]
}
```
該如何解讀該區塊呢？  
#### 基本信息
- **hash**: `00000000839a8e6886ab5951d76f411475428afc90947ee320161bbf18eb6048`
  - 這是該區塊的區塊哈希值，區塊哈希是區塊內容的加密摘要，並且是該區塊在區塊鏈中唯一的識別符號。
  
- **confirmations**: `158577`
  - 該區塊在區塊鏈上已被確認了 158,577 次，表示它在區塊鏈的歷史深度，越多確認代表該區塊位置越深、越難被修改。

- **height**: `1`
  - 該區塊的高度是 `1`，這表示它是比特幣區塊鏈的第二個區塊（第一個區塊是創世區塊，區塊高度為 0）。

- **version**: `1`
  - 區塊的版本號，指示該區塊使用的比特幣協議版本。

- **versionHex**: `00000001`
  - 區塊版本的十六進制表示法。

#### Merkle Root
- **merkleroot**: `0e3e2357e806b6cdb1f70b54c3a3a17b6714ee1f0e68bebb44a74b1efd512098`
  - 這是區塊中所有交易的 Merkle 樹根哈希，它用來驗證區塊中所有交易的完整性。

#### 時間相關
- **time**: `1231469665`
  - 區塊的時間戳，這是以 Unix 時間格式表示的秒數，對應的時間是 2009-01-09 02:54:25 UTC。

- **mediantime**: `1231469665`
  - 這是該區塊的中位時間戳，代表過去 11 個區塊的中間時間。它有助於防止時間操縱。

#### 其他區塊屬性
- **nonce**: `2573394689`
  - 區塊挖掘過程中的隨機數，礦工透過不斷變動此數字來尋找滿足工作量證明的有效哈希值。

- **bits**: `1d00ffff`
  - 表示難度目標的壓縮表示法，與難度直接相關。

- **difficulty**: `1`
  - 區塊的挖掘難度，這裡顯示的是最早期區塊的最低難度。

- **chainwork**: `0000000000000000000000000000000000000000000000000000000200020002`
  - 這是鏈上總的工作量，表示區塊鏈中所有區塊進行計算的總和。

#### 交易數據
- **nTx**: `1`
  - 區塊中包含的交易數量，這裡顯示為 1 筆交易。

- **tx**: `0e3e2357e806b6cdb1f70b54c3a3a17b6714ee1f0e68bebb44a74b1efd512098`
  - 這是該區塊中唯一的交易 ID，這筆交易是創幣交易（coinbase），用於支付給礦工的區塊獎勵。

#### 區塊大小
- **strippedsize**: `215`
  - 區塊移除簽名數據後的大小，以字節為單位。

- **size**: `215`
  - 區塊的總大小，以字節為單位。

- **weight**: `860`
  - 區塊的權重，用於 SegWit（隔離見證）後的區塊大小計算。

#### 區塊鏈連接
- **previousblockhash**: `000000000019d6689c085ae165831e934ff763ae46a2a6c172b3f1b60a8ce26f`
  - 前一個區塊的哈希值，這是比特幣創世區塊的哈希。

- **nextblockhash**: `000000006a625f06636b8bb6ac7b960a8d03705d1ace08b1a19da3fdcc99ddbd`
  - 下一個區塊的哈希值，區塊鏈中每個區塊都與前後區塊相連，形成區塊鏈。






-----   
### 上課筆記：
## 9/30筆記
