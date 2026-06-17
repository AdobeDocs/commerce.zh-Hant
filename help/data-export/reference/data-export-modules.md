---
title: SaaS資料匯出模組
description: 瞭解 [!DNL SaaS Data Export] 中包含的Magento模組套件，及其在資料收集、轉換及提交至Adobe SaaS服務中的角色。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Developer
feature: Services
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088bid: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: cc250cf1-34eb-4863-80d0-d170d45ea067
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 111
ht-degree: 0%

---


# SaaS資料匯出模組

[!DNL SaaS Data Export]包含兩個模組群組：第一個用於資料收集和編制索引，第二個用於HTTP傳輸和提交。

這些模組會處理實體變更偵測、摘要索引、資料擷取和結構描述定義。
下表僅提供架構層級的模組；可用模組的完整清單視安裝的套裝程式而定。

| 模組 | 用途 | 金鑰類別 |
| --- | --- |--- |
| `DataExporter` | 核心架構：索引器、摘要表格、雜湊、重試、鎖定 | `FeedIndexer`, `FeedIndexMetadata`, `FeedMetadataPool`, `FeedLockManager` |
| `QueryXml` | 用於資料收集的XML型查詢DSL | `QueryFactory`, `QueryProcessor`, `SelectBuilder` |
| `SaaSCommon` | 共用HTTP傳輸、重試、CLI (`saas:resync`)、重新同步協調流程 | `ExportFeed`, `SubmitFeed`, `ResyncManager`, `ResyncManagerPool`, `ProgressBarManager` |

若要瞭解這些模組在同步處理期間如何共同運作，請參閱[SaaS資料匯出管道](../sync-overview.md)。

>[!MORELIKETHIS]
>
>- [同步化的運作方式](../sync-overview.md)
>- [摘要資料表結構描述](feed-table-reference.md)
>- [管理SaaS資料匯出擴充功能](../manage-extension.md)
