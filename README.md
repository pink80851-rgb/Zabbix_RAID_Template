📊 Zabbix RAID Monitoring Template (SRE-Oriented)
📌 專案目標 (Project Objective)

本專案提供一套以 Zabbix 6.0 為基礎的 RAID 監控模板，專注於：

🔍 自動化 RAID 狀態監控
🔁 透過 LLD (Low-Level Discovery) 減少人工維護成本
⚠️ 即時異常偵測與告警
🧩 模組化設計，便於擴展與重用
🎯 解決的核心問題
傳統 RAID 監控需手動逐顆設定 disk item
無法即時掌握 RAID 卡溫度與磁碟狀態
重複性維運操作（RDP / CLI 檢查）效率低

👉 本模板將上述流程 完全自動化 + 標準化

🏗️ 技術架構 (Technical Architecture)

本模板採用 Zabbix 原生功能，結合多種 preprocessing 與 discovery 技術：

🔧 核心組件
Zabbix Template
RAID 卡溫度監控 (raid.roc.temp)
RAID 總體狀態 (raid.vd.status)
Low-Level Discovery (LLD)
自動發現 RAID Disk Slot (raid.pd.discovery)
動態生成以下監控項目：
Disk Capacity
Disk Serial Number
Disk State
Item Preprocessing
JSONPATH：解析 RAID CLI JSON 結構
JavaScript：自訂 Slot 解析邏輯
REGEX：擷取狀態與容量資訊
📊 架構流程
RAID CLI / API
      ↓
   JSON Output
      ↓
[ Zabbix Preprocessing ]
  - JSONPATH
  - JavaScript
  - REGEX
      ↓
 Low-Level Discovery (LLD)
      ↓
 Item Prototypes
      ↓
 Trigger Prototypes
      ↓
 Alert / Monitoring
🚀 擴展性 (Scalability & Extensibility)

本專案設計時已考慮 SRE 實務中的擴展需求：

🔌 可擴展方向
✅ 支援多品牌 RAID Controller（LSI / MegaRAID / Dell PERC）
✅ 可延伸至：
CPU / Memory / NIC 監控
Storage (SSD / NVMe)
✅ 可整合：
Prometheus Exporter
Grafana Dashboard
AlertManager / Webhook
🧱 模組化設計
每個監控項目皆為 獨立 item prototype
可快速複製並套用至其他硬體監控場景
Trigger 與 Item 解耦，方便調整告警策略
💡 技術亮點 (Technical Highlights)
🔍 1. LLD 自動化監控
自動偵測 RAID Disk Slot
無需手動新增磁碟
適用於動態變更環境（熱插拔 / 擴充）
🧠 2. JavaScript + JSONPATH 組合解析
var input = JSON.parse(value);
var output = [];

input.forEach(function(item) {
    var slot = item["EID:Slt"].split(":")[1];
    output.push({ "{#SLOT}": slot });
});

return JSON.stringify(output);
精準解析 RAID CLI JSON 結構
動態產生 LLD Macro {#SLOT}
提高資料抽取彈性
🧹 3. 高效資料清洗 (Preprocessing Pipeline)
使用 REGEX：
擷取容量 (TB / GB)
擷取狀態 (Onln / Fail / Rebuild)
減少不必要資料寫入 Zabbix DB
提升效能與可讀性
🚨 4. 智慧告警設計
RAID 溫度告警：

75°C 觸發

< 70°C 自動恢復
Disk 狀態告警：
非 Onln / GHS 即觸發 WARNING

👉 避免誤報（False Positive），提高告警品質

🔖 5. Tag-based 分類設計
使用 Tag：
DiskSlot
Raid
STATUS

🧭 SRE 實務價值 (SRE Perspective)

本專案符合 SRE 核心理念：

📉 降低 Toil（重複性勞務）
⚙️ 自動化監控流程
📊 提高系統可觀測性 (Observability)
🚨 改善 Incident Response 時間
📎 未來優化方向 (Future Improvements)
 加入 RAID rebuild 進度監控
 整合 Grafana 視覺化 Dashboard
 建立 Alert 分級（Critical / Warning / Info）
 支援多 Controller aggregation
 與 CMDB / Asset 系統整合
