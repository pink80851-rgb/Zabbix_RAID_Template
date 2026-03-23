
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
[內有舊版截圖] 紀錄傳統 RDP + MSM UI 巡檢的低效率。

分析人工巡檢造成的資訊斷層。

4. ⚡ 現行自動化成果 (Current Solution)
[內有成果截圖] 展示 Zabbix 自動化後的即時數據與告警機制。

導入後的運維效率提升對比。

🛠️ 快速開始 (Quick Start)
如果您想在您的環境中部署這套監控，請參考以下步驟：

1. 前置作業
確認伺服器已安裝 LSI/Broadcom RAID 卡。

下載 storcli64.exe 並放置於 C:\storcli64\ 路徑下。

2. 部署 Agent 設定
將本倉庫中的 zabbix_agentd.d/raid.conf 內容加入您的 Windows Zabbix Agent 設定檔中並重啟服務。

3. 匯入模板
在 Zabbix Server 網頁介面匯入 By_users_Raid_only.yaml，並將其連結 (Link) 至目標主機。

🌟 為什麼這個專案值得關注？
零手動介入：利用 LLD (磁碟自動發現) 技術，新增硬碟自動上線監控。

低系統負載：避開沉重的 MSM GUI，僅透過輕量級 CLI 採集數據。

SRE 思維：不僅僅是監控，更是將維運流程「代碼化」的實踐。
