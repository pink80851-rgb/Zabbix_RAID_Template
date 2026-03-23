##04. 現行自動化監控方案 (Current Automation Solution)為了徹底解決人工巡檢的低效率與資訊斷層，我開發了一套基於 Zabbix + StorCLI 的自動化監控架構。
#  這套系統實現了「無須登入、主動告警、自動紀錄」的目標。
#  🏗️ 系統架構與技術棧 (Architecture)數據採集：使用 storcli64.exe 命令列工具，避開沉重的 MSM UI 負擔。
#  傳輸通道：透過 Zabbix Agent (Active/Passive) 將硬體狀態推播至監控中心。
#  自動化邏輯：LLD (Low-Level Discovery)：自動偵測伺服器上的實體碟數量與 Slot 位置。
#  JavaScript 預處理：在 Zabbix 端即時解析 JSON 數據，提取關鍵欄位。
#  視覺化：整合 Grafana (或 Zabbix Dashboard) 呈現即時與歷史狀態。

### 🛠️ 核心監控指標 (Key Monitoring Metrics)監控項目執行方式預期效益RAID 總體狀態raid.vd.status發生降級 (Degraded) 時，1 分鐘內觸發 Email 告警。
#  磁碟自動發現raid.pd.discovery自動抓取 Slot 編號，新增硬碟不須手動修改設定。
#  硬碟詳細資訊raid.pd.sn / size自動紀錄 SN 序號與容量，取代手動 Excel 登記。
#  硬體健康度raid.roc.temp監控 RAID 卡晶片溫度，預防因機房空調故障導致的硬體損毀。
