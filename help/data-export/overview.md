---
title: '[!DNL SaaS Data Export Guide]'
description: 瞭解如何將 [!DNL data export] 擴充功能用於Adobe Commerce SaaS服務，以在Adobe Commerce與連線的Commerce服務之間同步資料。
role: Admin, Developer
exl-id: 8a0067ba-90a4-48a6-8276-208d09abe6fc
TQID: https://experienceleague.adobe.com/OHE1GBUEd8hHFPwFlO9fJa3Y0wK2xZ0HOYnwUn0-DSk
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 569
ht-degree: 0%

---

# [!DNL SaaS Data Export] 指南

[!DNL SaaS data export]會在Adobe Commerce執行個體和連線的Commerce Services之間同步資料。 當您將Live Search、Product Recommendations或目錄服務新增至Adobe Commerce安裝時，[!DNL Data export]擴充功能會自動安裝。

>[!NOTE]
>
>如果您安裝Adobe Commerce Optimizer Connector，會使用相同的Data Export擴充功能，透過Composable Catalog Data Model (CCDM)將目錄和定價摘要傳送至Adobe Commerce Optimizer。 如需架構和組態詳細資訊，請參閱[Adobe Commerce Optimizer聯結器指南](../aco-connector/overview.md)。

SaaS資料匯出會收集並匯出各種型別的資料，稱為&#x200B;_摘要_，用於彙總特定型別的資訊。 視安裝的Commerce服務而定，SaaS資料匯出摘要包含：

- **目錄實體摘要**&#x200B;彙總產品資料。 資料包括產品、產品屬性、產品價格、產品變化、類別、類別許可權和產品許可權。
- **範圍摘要**&#x200B;會彙總客戶群組、網站、商店和商店檢視的資料。
- **銷售訂單摘要**&#x200B;會彙總訂單資料，包括其相關實體，例如商業發票、出貨、銷退折讓單等。
- **多Source庫存摘要**&#x200B;會彙總有關庫存狀態專案的資料。

SaaS資料匯出會以PHP擴充功能的形式提供。 它支援數種方法來啟動及管理資料同步流程。

- **從Admin或命令列手動同步處理**

   - Commerce Admin中的[資料管理儀表板](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)提供同步處理狀態的圖形檢視，顯示產品資料已成功同步至商務服務。 您可以使用儀表板對所有摘要執行完整重新同步（_完整同步_）。 不過，Adobe建議僅在第一次將Adobe Commerce連線至Commerce服務時，才執行完整同步。 請參閱[同步化程式](data-synchronization.md)。

     {{aco-data-sync-verification}}

   - [資料摘要同步狀態](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status)頁面會提供資料匯出摘要的健全狀況和效能的即時深入分析，這些摘要會將產品和類別資料從Commerce傳輸到外部服務，例如產品建議、即時搜尋和目錄服務或Adobe Commerce Optimizer。

   - [Adobe Commerce命令列工具](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/config-cli) (CLI)提供同步特定摘要的命令，並包含自訂摘要處理的其他選項。

- **與cron工作自動同步**

   - [部分資料同步](data-synchronization.md#partial-sync) — 當Commerce管理員使用者更新實體時，Cron工作會觸發部分資料同步。 資料匯出程式只會將這些更新傳送至連線的Commerce服務。 部分同步程式以MView機製為基礎，不需要管理員使用者或系統整合者執行任何動作。

   - [同步處理錯誤的自動重試](data-synchronization.md#retry-failed-items-sync) — 當資料同步處理期間發生錯誤時，Cron工作會觸發同步處理程式的自動重試。

- **匯出排程與效能**

   - 開發人員和系統整合經銷商能估計SaaS資料匯出所需的時間，以便在Adobe Commerce和連線的服務之間同步資料。 此預估可協助排程資料匯出處理，以防止網站中斷。 請參閱[估計資料量和傳輸時間](estimate-data-volume-sync-time.md)。

   - 在需要更快速進行同步的情況下，SaaS資料匯出可提供自訂選項來改善匯出處理效能。 請參閱[改善資料匯出效能](customize-export-processing.md)。

- **追蹤並疑難排解資料匯出活動** — 使用資料匯出和saas-export記錄檔，在同步和索引化程式期間檢閱同步狀態和摘要裝載。 請參閱[記錄及疑難排解](troubleshooting-logging.md)。
