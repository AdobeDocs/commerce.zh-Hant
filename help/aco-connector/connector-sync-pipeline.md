---
title: 目錄同步管道
description: 瞭解 [!DNL Adobe Commerce Optimizer Connector] 同步管道的運作方式，包括摘要轉換、cron排程、範圍控制和錯誤處理。
feature: Integration, Configuration
badgePaas: label="僅限PaaS" type="Informative" url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案（Adobe管理的PaaS基礎結構）和內部部署專案的Adobe Commerce 。"
autotag-review: '2026-06-09T16:21:52.214Z'
TQID: 'https://experienceleague.adobe.com/EXUQzAd0I6Hnq4twzhaBZZnv0jLjeGBuTx-QgQz-5MA'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: addc3a3a-2b1c-4fdf-aea4-4b1eb2931ba6
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 6d4493db5e0714577a8800007cc6d2c552578fa4
workflow-type: tm+mt
source-wordcount: 625
ht-degree: 1%

---

# 聯結器同步管道

**[!DNL Adobe Commerce Optimizer Connector]**&#x200B;以[[!DNL SaaS Data Export]](https://experienceleague.adobe.com/zh-hant/docs/commerce/saas-data-export/overview)建置，將[!DNL SaaS Data Export]索引子收集的資料對應至[!DNL Adobe Commerce Optimizer] [!DNL Catalog Data Ingestion API]所需的格式，並處理驗證、批次提交及範圍型同步控制。 以下各節將說明此同步的運作方式。

相關內容：

- 在[[!DNL Commerce Optimizer Connector] 總覽](overview.md)主題中瞭解整合的商業價值、主要功能和架構。

- 如需模組封裝名稱、摘要API端點和組態金鑰路徑，請參閱[聯結器參考](reference/connector-reference.md)

## 同步如何運作

下圖顯示透過[!DNL Adobe I/O Gateway]從[!DNL Adobe Commerce]到[!DNL Commerce Optimizer]的資料同步處理。

![Commerce Optimizer Connector高階同步圖表](assets/aco-connector-sync-high-level-diagram.png){width="800" zoomable="yes"}

當[!DNL Adobe Commerce]中的目錄資料變更時，同步處理會經過這些階段。

1. **實體變更偵測** — （每1分鐘） Cron工作(`indexer_reindex_all_invalid`)會偵測[!DNL Adobe Commerce]個實體變更並觸發[!DNL SaaS Data Export]，以組合摘要專案並追蹤其狀態。
1. **轉換** — [!DNL Commerce Optimizer Connector]會擷取組合摘要，將[!DNL Adobe Commerce]實體和範圍對應至[!DNL Commerce Optimizer] API所需的格式，並準備要傳輸的裝載。
1. **傳輸** — 轉換後的資料會透過[!DNL Adobe I/O Gateway]透過HTTP POST (`/v1/catalog/<feed name>`)傳送至[!DNL Commerce Optimizer]，以驗證並儲存傳入的摘要。
1. **失敗重試** （每5分鐘） — 單獨的cron工作(`*_resend_failed_items`)會偵測到任何失敗的摘要專案，並透過相同的管道重新提交它們。

### 排程的cron工作

兩個cron群組會按照固定計畫自動化管道。

| Cron群組 | 用途 | 排程 |
| ---------- | ------- | -------- |
| `indexer_reindex_all_invalid` | 接聽實體更新、組合摘要專案、保留摘要狀態 | 每1分鐘 |
| `*_resend_failed_items` | 檢查失敗的摘要專案，並將它們重新提交至[!DNL Commerce Optimizer] | 每5分鐘 |

**[!DNL SaaS Data Export]**&#x200B;擴充功能會處理摘要收集和狀態追蹤。 聯結器層將實體和範圍對應至[!DNL Commerce Optimizer] API所需的格式，並透過`POST /v1/catalog/<feed name>`提交它們。

#### 需求

- [Commerce cron必須執行](https://experienceleague.adobe.com/zh-hant/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues){target="_blank"}。
- 摘要索引子必須使用&#x200B;**[!UICONTROL Update by Schedule]**&#x200B;模式。 請參閱[驗證Commerce應用程式組態](../data-export/data-synchronization.md#verify-commerce-application-configuration){target="_blank"}。

## 範圍型同步控制

`CommerceOptimizerScopeMapper`模組會讀取每個網站和每個商店檢視的匯出設定，並在摘要收集和提交期間強制執行。

- **已啟用範圍**，以一般差異排程匯出資料。
- **已停用的領域**&#x200B;已從管道中排除。
先前同步的實體在下次cron執行時從[!DNL Commerce Optimizer]中移除。

如果同步問題只影響一個目錄來源或價格簿，請參閱[資料未同步](troubleshooting.md#data-not-syncing)。

如需自訂同步化範圍的詳細資訊，請參閱[自訂Commerce範圍匯出設定](get-started.md#customize-the-commerce-scopes-export-configuration)。

## 計時與監控

| 情境 | 一般計時 |
| -------- | -------------- |
| 例行目錄更新 | 1到2個差異同步週期（索引約1到2分鐘，加上提交） |
| 暫時性失敗 | 每5分鐘重試一次 |
| 完整同步或大型目錄 | 分鐘到小時 |

從Commerce管理員的[[!UICONTROL Data Feed Sync Status]](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status)頁面監視每個摘要的狀態。 請參閱[確認資料同步正在運作](./get-started.md#verify-that-the-data-sync-is-working)。

## 摘要提交和錯誤處理

`FeedSubmitter`處理序處理[!DNL Catalog Data Ingestion API]呼叫。

1. 將更新專案與刪除專案分開（不同的API端點）。
1. 呼叫會分別更新和刪除端點。
1. 將每個專案的狀態結果合併回單一回應。

### HTTP狀態代碼合併

當更新和刪除呼叫傳回不同的狀態代碼時，`FeedSubmitter`會以下列方式結合結果。

| 更新結果 | 刪除結果 | 最終結果 |
| --------------- | --------------- | ------------- |
| 200 | 200或無 | 200項成功 |
| 200 | 400 | 200包含刪除錯誤 |
| 400 | 400 | 400個合併錯誤 |
| 其他 | 其他 | 可重試 |

| 錯誤型別 | 行為 |
| ---------- | -------- |
| **400** | 回應`errors`欄位中列出的專案會出現在Admin中，需要注意。 批次中的其他專案會重試。 |
| **5xx** | 已由`resync_failed_feeds_data_exporter`群組中的摘要特定`*_feed_resend_failed_items` cron工作重試。 |

>[!MORELIKETHIS]
>
> - [聯結器總覽](overview.md) — 瞭解業務內容和範圍對應
> - [聯結器參考](reference/connector-reference.md) — 檢閱模組、API端點和組態金鑰
> - [自訂Commerce範圍匯出設定](./get-started.md#customize-the-commerce-scopes-export-configuration) — 設定每個範圍層級的摘要、啟用和停用行為，以及管理步驟
> - [疑難排解](troubleshooting.md) — 診斷同步處理失敗
