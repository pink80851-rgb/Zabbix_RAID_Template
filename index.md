
# 🚀 Zabbix RAID 自動化監控模組 (StorCLI 版)
* 將傳統 MIS 的「人肉巡檢」轉化為「Code-Driven」的自動化監控系統。

* 本專案提供了一套完整的 Zabbix 模板與配置腳本，專門用於監控 Windows Server 環境下的 LSI/Broadcom RAID 陣列狀態。

# 📖 專案深度解析 (Project Breakdown)
為了讓您更了解本系統的設計思維與實作細節，我將內容拆解為以下四個階段：

* 1. 🔍 專案簡介與目標 (Introduction)
為什麼選擇 StorCLI？

監控的核心價值與 ISO 27001 合規性。

2. 🏗️ 系統架構與邏輯 (Architecture)
內含 Mermaid 流程圖。

解釋數據如何從硬體層流轉至 Zabbix 告警層。

3. 📉 舊有模式與痛點分析 (Legacy Mode)
紀錄傳統 RDP + MSM UI 巡檢的低效率。
<img width="1473" height="816" alt="螢幕擷取畫面 2026-03-23 090350" src="https://github.com/user-attachments/assets/260203b1-66fb-47d9-9df3-c8289c68b89d" />
<img width="725" height="789" alt="螢幕擷取畫面 2026-03-23 085103" src="https://github.com/user-attachments/assets/33d378e9-3fec-4110-8323-f300b84223ed" />


分析人工巡檢造成的資訊斷層。

4. ⚡ 現行自動化成果 (Current Solution)
 展示 Zabbix 自動化後的即時數據與告警機制。
<img width="1882" height="836" alt="螢幕擷取畫面 2026-03-23 090503" src="https://github.com/user-attachments/assets/3ff1af09-7ca6-433a-9341-27d670c89f8f" />
<img width="1863" height="797" alt="螢幕擷取畫面 2026-03-23 090511" src="https://github.com/user-attachments/assets/44d43d84-8484-4c56-8886-0a5e2d03a55b" />


導入後的運維效率提升對比。

🛠️ 快速開始 (Quick Start)
如果您想在您的環境中部署這套監控，請參考以下步驟：

1. 前置作業
確認伺服器已安裝 LSI/Broadcom RAID 卡。
![Uploading 螢幕擷取畫面 2026-03-23 085103.png…]()

下載 storcli64.exe 並放置於 C:\storcli64\ 路徑下。

2. 部署 Agent 設定
將本倉庫中的 zabbix_agentd.d/raid.conf 內容加入您的 Windows Zabbix Agent 設定檔中並重啟服務。

3. 匯入模板
在 Zabbix Server 網頁介面匯入 By_users_Raid_only.yaml，並將其連結 (Link) 至目標主機。

🌟 為什麼這個專案值得關注？
零手動介入：利用 LLD (磁碟自動發現) 技術，新增硬碟自動上線監控。

低系統負載：避開沉重的 MSM GUI，僅透過輕量級 CLI 採集數據。

SRE 思維：不僅僅是監控，更是將維運流程「代碼化」的實踐。

## 📖 專案目錄 (Project Sections)
* [Step 1: 專案簡介與目標](./01_intro.md)
* [Step 2: 系統架構與邏輯](./02_architecture.mmd)
* [Step 3: 舊有模式與痛點分析](./03_legacy.md)
* [Step 4: 優化後的自動化方案](./04_optimized.md)
