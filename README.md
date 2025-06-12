# 🛡️ 詐騙檢舉平台 Demo

一個基於區塊鏈技術的詐騙檢舉平台，使用以太坊智能合約儲存檢舉記錄，並透過模擬 IPFS 系統管理檢舉內容。

## 📋 專案概述

此平台允許用戶通過 MetaMask 錢包連接，提交詐騙檢舉並將記錄永久保存在區塊鏈上。檢舉內容通過模擬的 IPFS 系統進行管理，支援多種詐騙類型標籤分類，提供完整的檢舉記錄管理功能。

## 🏗️ 系統架構

```
scam-report-demo/
├── backend/                    # 後端 API 服務
│   ├── .env.example           # 環境變數範例文件
│   ├── index.js               # 主要後端邏輯與 API 端點
│   ├── package.json           # 後端依賴管理
│   └── ReportRegistryABI.json # 智能合約 ABI 定義
├── frontend/                  # 前端介面
│   ├── improved-index.html    # 主要檢舉平台介面
│   └── test-reports.html      # 檢舉記錄測試與管理頁面
├── .gitignore                 # Git 忽略文件配置
└── README.md                  # 專案說明文件
```

## ⚡ 快速開始

### 前置需求

- **Node.js 18+** - JavaScript 執行環境
- **MetaMask** - 瀏覽器錢包擴展
- **Sepolia 測試網 ETH** - 用於支付 Gas 費用

### 1. 克隆專案

```bash
git clone <your-repo-url>
cd scam-report-demo
```

### 2. 後端設置

```bash
cd backend
npm install
```

複製並設置環境變數：

```bash
cp .env.example .env
```

編輯 `.env` 文件，配置以下參數：

```env
# 以太坊 Sepolia 測試網路 RPC 端點
NETWORK_URL=https://eth-sepolia.public.blastapi.io

# 部署者私鑰（⚠️ 僅用於測試，請勿使用真實私鑰）
PRIVATE_KEY=your_test_private_key_here

# 已部署的智能合約地址
CONTRACT_ADDRESS=0x18b72bfa680eec68e0fce91b810de8140c54b916

# 後端服務端口
PORT=3000

# IPFS API（Demo 模式可保持預設值）
IPFS_API_URL=https://ipfs.infura.io:5001
```

### 3. 啟動後端服務

```bash
# 正常啟動
npm start

# 開發模式（自動重載）
npm run dev
```

後端服務將在 `http://localhost:3000` 上運行

### 4. 啟動前端

直接在瀏覽器中開啟 HTML 文件：

- **主要平台**: `frontend/improved-index.html`
- **管理後台**: `frontend/test-reports.html`

## 🎯 主要功能

### 📝 檢舉提交功能
- **錢包連接**: 透過 MetaMask 進行身份驗證
- **多標籤分類**: 支援 11 種詐騙類型標籤選擇
- **內容管理**: 模擬 IPFS 內容儲存與 CID 生成
- **區塊鏈記錄**: 檢舉記錄永久保存在智能合約中

### 📊 檢舉記錄管理
- **即時統計**: 顯示總檢舉數與今日檢舉統計
- **標籤篩選**: 依據詐騙類型標籤篩選檢舉記錄
- **詳細資訊**: 包含檢舉人、時間、內容預覽等完整資訊
- **歷史查詢**: 支援完整檢舉記錄瀏覽與搜尋

### 🔧 開發者工具
- **API 測試**: 驗證後端 API 服務可用性
- **連線診斷**: 測試區塊鏈連接與智能合約互動
- **數據驗證**: 確保檢舉記錄的完整性和準確性

## 🛠️ 技術棧

### 前端技術
- **HTML5/CSS3/JavaScript**: 基礎網頁技術
- **Ethers.js v5.7.2**: 以太坊區塊鏈互動庫
- **MetaMask Integration**: 錢包連接與交易簽名
- **Responsive Design**: 響應式設計支援各種裝置

### 後端技術
- **Node.js + Express**: RESTful API 服務框架
- **Ethers.js v6.14.3**: 智能合約互動庫
- **CORS**: 跨域資源共享支援
- **模擬 IPFS**: 內容雜湊與分散式儲存模擬

### 區塊鏈技術
- **Ethereum Sepolia**: 測試網路環境
- **Smart Contract**: 檢舉記錄儲存與管理
- **Web3 Integration**: 去中心化應用互動

## 📡 API 文檔

### 檢舉管理端點

#### 提交檢舉
```http
POST /submit
Content-Type: application/json

{
  "content": "檢舉詳細內容",
  "tags": ["網路詐騙", "投資詐騙"]
}
```

**回應:**
```json
{
  "success": true,
  "cid": "QmXxxxxxxxxxx..."
}
```

#### 獲取所有檢舉
```http
GET /reports
```

**回應:**
```json
{
  "success": true,
  "reports": [
    {
      "reporter": "0x...",
      "cid": "QmXxx...",
      "timestamp": 1672531200,
      "content": "檢舉內容",
      "tags": ["網路詐騙"]
    }
  ]
}
```

#### 獲取特定檢舉
```http
GET /reports/:index
```

#### 獲取檢舉內容
```http
GET /content/:cid
```

### 統計資訊端點

#### 獲取平台統計
```http
GET /stats
```

**回應:**
```json
{
  "success": true,
  "stats": {
    "total": 150,
    "today": 5,
    "lastUpdated": "2024-01-15T10:30:00Z"
  }
}
```

## 🏷️ 詐騙類型標籤

平台支援以下詐騙類型分類：

| 標籤 | 描述 | 圖示 |
|------|------|------|
| 網路詐騙 | 一般網路相關詐騙行為 | 🌐 |
| 投資詐騙 | 虛假投資、理財詐騙 | 💰 |
| 加密貨幣 | 虛擬貨幣相關詐騙 | ₿ |
| 電話詐騙 | 電話騷擾、詐騙電話 | 📞 |
| 簡訊詐騙 | 詐騙簡訊、釣魚簡訊 | 📱 |
| 釣魚網站 | 偽造官方網站 | 🎣 |
| 假冒身份 | 冒充他人身份 | 👤 |
| 購物詐騙 | 網購、交易詐騙 | 🛒 |
| 愛情詐騙 | 感情詐騙、交友詐騙 | 💕 |
| 求職詐騙 | 虛假工作機會 | 💼 |
| 其他 | 其他類型詐騙 | ❓ |

## 🔧 開發說明

### 智能合約介面

智能合約 ABI 定義在 `backend/ReportRegistryABI.json`，包含以下主要功能：

- `submitReport(string cid)`: 提交檢舉記錄
- `getReport(uint256 index)`: 獲取特定檢舉記錄
- `getReportCount()`: 獲取檢舉總數

### 模擬 IPFS 系統

為了簡化 Demo 流程，本專案使用模擬 IPFS 系統：

```javascript
const generateMockCID = (content) => {
  const hash = crypto.createHash('sha256').update(content).digest('hex');
  return `Qm${hash.substring(0, 44)}`;
};
```

### 環境設置

1. **測試網路設置**: 在 MetaMask 中添加 Sepolia 測試網路
2. **測試 ETH**: 從 [Sepolia Faucet](https://sepoliafaucet.com/) 獲取測試代幣
3. **智能合約**: 使用 Remix IDE 部署智能合約

## 🚀 部署指南

### 本地開發環境

1. 啟動後端服務：`npm start`
2. 開啟前端頁面：在瀏覽器中打開 HTML 文件
3. 連接 MetaMask 並切換到 Sepolia 測試網

### 生產環境部署

**後端部署:**
```bash
# 使用 PM2 管理進程
npm install -g pm2
pm2 start index.js --name "scam-report-backend"
```

**前端部署:**
- 將 HTML 文件部署到任何靜態網站託管服務
- 確保 API 端點配置正確

## 🔍 故障排除

### 常見問題

**Q: MetaMask 連接失敗**
A: 確保已安裝 MetaMask 並切換到 Sepolia 測試網路

**Q: 交易失敗**
A: 檢查測試 ETH 餘額是否足夠支付 Gas 費用

**Q: API 連接錯誤**
A: 確認後端服務正在運行且端口配置正確

**Q: 智能合約互動失敗**
A: 驗證合約地址和 ABI 配置是否正確

### 日誌查看

```bash
# 查看後端日誌
tail -f backend/logs/app.log

# 檢查 PM2 狀態
pm2 status
pm2 logs scam-report-backend
```

## 📝 開發計畫

### 即將推出功能
- [ ] 使用者身份驗證系統
- [ ] 檢舉記錄評分機制
- [ ] 進階搜尋與篩選功能
- [ ] 資料匯出功能
- [ ] 多語言支援

### 技術改進
- [ ] 整合真實 IPFS 網路
- [ ] 資料庫持久化儲存
- [ ] 效能最佳化
- [ ] 單元測試覆蓋
- [ ] Docker 容器化

## 🤝 貢獻指南

歡迎參與專案開發！請遵循以下步驟：

1. Fork 此專案
2. 創建功能分支：`git checkout -b feature/新功能`
3. 提交更改：`git commit -m '新增某功能'`
4. 推送分支：`git push origin feature/新功能`
5. 提交 Pull Request

## 📄 授權條款

本專案採用 ISC 授權條款 - 詳見 [LICENSE](LICENSE) 文件

## 👥 開發團隊

- **專案維護者**: [您的名字]
- **技術顧問**: [顧問名字]

## 📞 聯絡資訊

- **專案首頁**: [GitHub Repository URL]
- **問題回報**: [GitHub Issues URL]
- **技術討論**: [Discord/Telegram Channel]

---

⭐ 如果這個專案對您有幫助，請給我們一個 Star！

🛡️ **讓我們一起打擊詐騙，保護每一個人的數位安全！**
