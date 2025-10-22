---
title: 同步資料與SaaS資料匯出
description: 瞭解 [!DNL SaaS Data Export] 如何在Adobe Commerce執行個體和連線的SaaS服務之間收集及同步資料。
role: Admin, Developer
exl-id: 2ca7c92a-fb52-4055-ae16-11e99b38d161
source-git-commit: 5dd290a4e10bdbd1f6c96b67ab6c9ba1598705dc
workflow-type: tm+mt
source-wordcount: '880'
ht-degree: 0%

---

# 與SaaS資料匯出同步資料

當您安裝需要資料匯出的Commerce服務（例如「目錄服務」、「即時搜尋」或「產品建議」）時，將會安裝Saas資料匯出模組的集合，以管理資料收集和同步程式。

SaaS資料匯出會持續將產品資料從Adobe Commerce執行個體移至Commerce Services平台，以保持資料在最新狀態。 例如，產品建議需要目前的目錄資訊，才能正確地傳回具有正確名稱、價格和可用性的建議。 使用[資料管理儀表板](https://experienceleague.adobe.com/en/docs/commerce/user-guides/data-services/catalog-sync)來觀察和管理同步化程式，或是使用命令列介面來觸發同步化並重新索引產品資料，以供Commerce服務使用。

下圖顯示SaaS資料匯出流程。

Adobe Commerce的![SaaS資料匯出集合與同步流程](assets/data-export-flow.png){width="900" zoomable="yes"}

SaaS資料匯出流程的主要元件包括：

- SaaS資料匯出模組會從Adobe Commerce收集摘要資料、組合摘要專案、監聽更新，並保留摘要狀態。
- SaaS匯出模組，可匯出資料、設定路由，以及將摘要發佈至連線的服務。
- Adobe Commerce服務會管理資料擷取程式，以驗證傳入的摘要並保留連線服務的更新。

>[!NOTE]
>
>為了確保順暢的排程並避免網站作業中斷，Adobe建議在開始任何資料摘要同步處理之前，先預估資料量和同步處理時間。 在計畫初始同步或大規模目錄更新（例如大量價格變更）時，此預估很重要。 如需詳細資訊，請參閱[估算資料同步處理的資料量和傳輸時間](estimate-data-volume-sync-time.md)

## 同步模式

SaaS資料匯出有兩種模式可處理實體摘要：

- **立即匯出模式** — 在此模式中，會收集資料並在單一反複專案中立即傳送至Commerce服務。 此模式可加快將實體更新傳送至Commerce服務的速度，並降低摘要表格的儲存大小。

- **舊版匯出模式** — 在此模式中，資料會以單一程式收集。 然後，cron作業會將收集的資料傳送至連線的商務服務。 在資料匯出記錄專案中，使用舊版模式的摘要會標示為`(legacy)`。

## 同步型別

SaaS資料匯出支援三種同步型別：完全同步、部分同步和重試失敗專案同步。

### 完全同步

將Adobe Commerce執行個體連線至Commerce服務後，執行完整同步以將實體摘要資料從Adobe Commerce傳送至連線的服務。

>[!NOTE]
>
>完全同步主要適用於上線階段。 請避免正常使用，以防止資料庫超過負荷。 初始同步後，會使用部分同步自動同步進行中的變更。

### 部分同步

透過部分同步，SaaS資料匯出會自動從Commerce應用程式將更新（例如產品名稱變更或價格更新）傳送至連線的商務服務。

資料匯出程式會使用下列cron作業來自動化部分同步作業。

- 「索引」cron群組工作：
   - `indexer_reindex_all_invalid`工作會重新索引所有無效的摘要。 這是標準的Adobe Commerce cron工作。
   - `saas_data_exporter`工作適用於舊版匯出摘要。
   - `sales_data_exporter`工作特定於銷售資料匯出摘要。

這些工作每分鐘執行一次。

為了讓部分同步運作，Commerce應用程式需要下列設定：

- [已透過cron工作啟用工作排程](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/configuration.html)

- 所有SaaS資料匯出索引子都是以`Update by Schedule`模式設定。

  在SaaS資料匯出103.1.0版和更新版本中，`Update by Schedule`模式預設為啟用。 您可以使用Commerce CLI命令`bin/magento indexer:show-mode | grep -i feed`來驗證伺服器上的索引組態

### 重試失敗的專案同步

「重試失敗的專案」同步會使用個別程式來重新傳送因同步處理期間發生錯誤（例如應用程式錯誤、網路中斷或SaaS服務錯誤）而無法同步的專案。 此同步的實作也以cron作業為基礎。

- `resync_failed_feeds_data_exporter` cron群組工作：
   - `<feed name>_feed_resend_failed_feeds_items`工作會重新傳送無法同步處理的專案，例如`products_feed_resend_failed_items`。

### 檢視及管理同步化程式

大多數同步化活動會根據應用程式組態自動處理。 不過，SaaS資料匯出也提供管理程式的工具。

- 管理員使用者可以檢視及追蹤同步處理進度，並從[資料管理儀表板](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard)取得資料的相關資訊。

- 具有Commerce應用程式伺服器存取權的開發人員、系統整合經銷商或管理員，可以使用Adobe Commerce命令列工具(CLI)管理同步流程和資料摘要。 請參閱[使用Commerce CLI管理同步作業](data-export-cli-commands.md)。

### 驗證Commerce應用程式設定

部分同步和重試失敗專案同步僅在Commerce執行個體已正確設定時運作。 通常，設定會在設定Commerce服務時完成。 如果資料匯出無法正常運作，請檢查下列設定。

- [確認cron工作正在執行](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues)。

- 請確認索引子是從[Admin](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management)執行，或使用Commerce CLI命令`bin/magento indexer:info`執行。

- 確認下列摘要的索引子已設定為`Update by Schedule`：目錄屬性、產品、產品覆寫和產品變體。 您可以在Admin中或使用CLI ([)從](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management)索引管理`bin/magento indexer:show-mode | grep -i feed`檢查索引子。

### 資料傳輸記錄的事件管理器通知

在103.3.4版或更新版本中，從Commerce執行個體傳送資料給Adobe Commerce服務時，SaaS Data Export會傳送`data_sent_outside`事件。

```php
$this->eventManager->dispatch(
   "data_sent_outside",
   [
       "timestamp" => time(),
       "type" => $metadata->getFeedName(),
       "data" => $data
   ]
);
```

>[!NOTE]
>
>如需關於事件以及如何訂閱事件的資訊，請參閱Adobe Commerce開發人員檔案中的[事件和觀察者](https://developer.adobe.com/commerce/php/development/components/events-and-observers)。
