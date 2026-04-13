📌 專案概述 (Overview)

本專案基於 Zabbix 6.0 建立 RAID 監控與自動化觀測系統，目標是將傳統「人工 RAID 檢查流程」轉換為：

🔥 可觀測（Observability） + 自動化（Automation） + 可告警（Alerting）的一體化監控系統

🎯 解決的核心問題 (Problem Statement)

在傳統 RAID 維運中存在以下問題：

❌ RAID 狀態需手動登入主機或 UI 查詢
❌ Disk Slot / 狀態需逐顆人工確認
❌ RAID 異常依賴人為巡檢（非即時）
❌ 多機器環境下維運成本線性上升
❌ 無法標準化監控與告警邏輯
🧠 本專案解決的本質問題

🔥 將「RAID 人工檢查流程」轉換為「資料驅動監控系統」

核心改善：

減少人工巡檢（Toil Reduction）
降低遺漏與誤判風險
提升 RAID 異常反應速度（MTTR 降低）
建立標準化監控模型
🏗️ 系統架構 (Architecture)
RAID CLI / API
      ↓
JSON Output
      ↓
Zabbix Preprocessing Layer
  - JSONPATH
  - JavaScript
  - REGEX
      ↓
Low-Level Discovery (LLD)
      ↓
Item / Trigger Prototypes
      ↓
Alerting System
🔧 核心功能 (Core Features)
🟢 1. RAID 狀態監控
RAID 卡溫度監控 (raid.roc.temp)
RAID Virtual Disk 狀態監控 (raid.vd.status)
🟡 2. 自動化磁碟發現 (LLD)

透過 Zabbix LLD：

自動發現 Disk Slot
自動生成監控項目
Capacity
Serial Number
State

👉 無需人工新增 disk items

🔴 3. 異常告警機制
RAID 溫度 > 75°C → WARNING
RAID 狀態非 Onln / GHS → Trigger alert
Recovery 條件：
溫度 < 70°C 自動恢復

👉 降低 false alarm 與誤判率

🧹 4. 資料標準化處理（Preprocessing）

使用：

JSONPATH（結構解析）
REGEX（資料抽取）
JavaScript（slot mapping）

👉 效果：

📉 降低 Toil（重複人工檢查）
⏱️ 降低 MTTR（故障回應時間）
📡 提升可觀測性（Observability）
🚨 提升告警品質（Signal > Noise）
🧩 建立標準化監控模型
