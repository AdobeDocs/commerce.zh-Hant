---
title: 檢閱記錄檔並進行疑難排解
description: 瞭解如何使用資料匯出和saas-export記錄檔來疑難排解 [!DNL data export] 錯誤。
feature: Services
exl-id: d022756f-6e75-4c2a-9601-31958698dc43
source-git-commit: 22c74c12ddfccdb4e6c4e02c3a15557e1020d5ef
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 0%

---

# 檢閱記錄檔並進行疑難排解

[!DNL data export]擴充功能提供記錄檔以追蹤資料收集和同步處理程式。

## 記錄檔

記錄檔位於Commerce應用程式伺服器上的`var/log`目錄中。

| 記錄檔名稱 | 檔案名稱 | 說明 |
|-----------------| ----------| -------------|
| SaaS資料匯出記錄 | `commerce-data-export.log` | 提供有關資料匯出活動的資訊，例如實體事件和完整重新同步觸發器。  每個記錄都有特定的結構，並提供有關摘要、作業、狀態、經歷時間、處理序識別碼和呼叫者的資訊。 |
| SaaS資料匯出錯誤記錄 | `data-export-errors.log` | 提供資料同步處理過程中發生的錯誤訊息和棧疊追蹤。 |
| SaaS匯出記錄 | `saas-export.log` | 提供關於傳送至Commerce SaaS服務的資料資訊。 |
| SaaS匯出錯誤記錄 | `saas-export-errors.log` | 提供將資料傳送至Commerce SaaS服務時發生錯誤的相關資訊。 |

如果您沒有看到Adobe Commerce服務的預期資料，請使用資料匯出擴充功能的錯誤記錄檔，以判斷發生問題的位置。 此外，您也可以使用其他資料來擴充記錄檔，以進行追蹤和疑難排解。 請參閱[延伸記錄](#extended-logging)。

### 記錄格式

每個記錄檔記錄都有以下結構。

```
[<log record datetime>] report.<log level>:
{
   "feed": "<feed name>",
   "operation": "<executed operation>",
   "status": "<status of operation>",
   "elapsed": "<time elapsed from script run>",
   "pid": "<process id that executed `operation`>",
   "caller": "<who called this `operation`>"
} [] []
```

>[!NOTE]
>
>JSON型字串經過美化，可更容易閱讀。

下表說明可記錄在記錄中的作業型別。

| 作業 | 說明 | 呼叫者範例 |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| 完全同步 | 收集特定摘要的所有資料並傳送至SaaS。 | `bin/magento saas:resync --feed=products` |
| 部分重新索引 | 收集特定摘要中更新的實體資料並將資料傳送至SaaS。 只有在更新的實體存在時，此記錄才會出現。 | `bin/magento cron:run --group=index` |
| 重試失敗的專案 | 如果先前的同步作業因Commerce應用程式或伺服器錯誤而失敗，請重新傳送指定摘要的專案至SaaS。 只有存在失敗的專案時，才會出現此記錄。 | `bin/magento cron:run --group=saas_data_exporter` (任何「*_data_exporter」cron群組) |
| 完整同步（舊版） | 在舊版匯出模式中，收集指定摘要的所有資料並傳送至SaaS。 | `bin/magento saas:resync --feed=categories` |
| 部分重新索引（舊版） | 在舊版匯出模式中，針對指定摘要將更新的實體傳送至SaaS。 只有在更新的實體存在時，此記錄才會出現。 | `bin/magento cron:run --group=index` |
| 部分同步（舊版） | 在舊版匯出模式中，針對指定摘要將更新的實體傳送至SaaS。 只有在更新的實體存在時，此記錄才會出現。 | `bin/magento cron:run --group=saas_data_exporter` (任何「*_data_exporter」cron群組) |


### 記錄範例

在完全重新同步期間，預設會每30秒追蹤並記錄一次進度。 紀錄專案範例如下。

```json
{
   "feed": "prices",
   "operation": "full sync",
   "status": "Progress: 2/5, processed: 200, synced: 100",
   "elapsed": "00:00:00 190 ms",
   "pid": "12824",
   "caller": "bin/magento saas:resync --feed=products"
}
```

在此範例中，`status`值提供同步作業的相關資訊：

- **`"Progress 2/5"`**&#x200B;表示已完成5個反複專案中的2個。 版序的數目取決於匯出的圖元數目。
- **`"processed: 200"`**&#x200B;表示已處理200個專案。
- **`"synced: 100"`**&#x200B;表示已傳送100個專案至SaaS。 預期`"synced"`不等於`"processed"`。 範例如下：
   - **`"synced" < "processed"`**&#x200B;表示與先前同步版本相比，摘要資料表未偵測到專案中的任何變更。 同步作業期間會忽略此類專案。
   - **`"synced" > "processed"`**&#x200B;相同的實體ID （例如，`Product ID`）可以在不同的範圍中有多個值。 例如，一個產品可指派至五個網站。 在此情況下，您可能會有「1個已處理」專案和「5個已同步」專案。

+++ **範例：價格摘要的完整重新同步記錄檔**

```
Price feed full resync:

[2024-03-05T21:00:51.754687+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Initialize","elapsed":"383 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:51.803178+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Creating batch table `catalog_data_exporter_product_prices_index_batches`. Start position: 30515","elapsed":"434 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:51.851878+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Batch table `catalog_data_exporter_product_prices_index_batches` created. Total Items: 500, batches: ~1","elapsed":"482 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:51.852548+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"start processing `500` items in `1` threads with `500` batch size","elapsed":"483 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:52.288369+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Progress 1\/1, processed 500, synced 0","elapsed":"919 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:53.994249+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Progress 1\/1, processed 500, synced 100","elapsed":"00:00:02 625 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:53.995168+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Complete","elapsed":"00:00:02 626 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
```

+++

## 使用New Relic檢視及疑難排解記錄

如果您將Adobe Commerce記錄檔儲存在New Relic中，可以新增剖析規則以改善可讀性和查詢體驗。

1. 登入New Relic。

1. 移至`Logs => Parsing`。

1. 按一下`Create parsing rule`。

1. 新增下列值以設定剖析規則。

   - **根據NRQL**&#x200B;篩選記錄檔

     `filePath LIKE '%commerce-data-export%.log'`

   - **剖析規則**

     `\[%{DATA:timestamp}\] report.%{DATA:logLevel} %{GREEDYDATA:feed:json}`

此範例新增規則，可讓您依特定摘要型別、操作等查詢New Relic記錄。

**查詢字串範例**—`feed.feed:"products" and feed.status:"Complete"`

## 疑難排解

如果Commerce Services中的資料遺失或不正確，請檢查記錄檔中是否有在從Adobe Commerce同步至Commerce Services平台期間發生錯誤的相關訊息。 如有需要，請使用擴充記錄功能，在記錄檔中新增其他資訊以進行疑難排解。

- 資料匯出錯誤記錄(`commerce-data-export-errors.log`)會擷取收集階段發生的錯誤。
- SaaS匯出錯誤記錄(`saas-export-errors.log`)會擷取傳輸階段發生的錯誤。

如果您看到與設定或協力廠商擴充功能無關的錯誤，請儘可能提交[支援票證](https://experienceleague.adobe.com/zh-hant/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide)並提供更多資訊。

### 解決目錄同步問題 {#resolvesync}

觸發資料重新同步時，最多可能需要一小時的時間才會更新資料，並反映在UI元件（例如即時搜尋和建議單位）中。 如果您仍然看到目錄與Commerce店面上的資料不一致，或目錄同步失敗，請參閱以下內容：

#### 資料差異

1. 在搜尋結果中顯示相關產品的詳細檢視。
1. 複製JSON輸出，並確認內容符合您在[!DNL Commerce]目錄中的內容。
1. 如果內容不符，請對目錄中的產品進行微幅變更，例如新增空格或句點。
1. 等候重新同步或[觸發手動重新同步](#resync)。

#### 同步處理未執行

如果同步未依排程執行，或未同步任何專案，請參閱此[知識庫](https://experienceleague.adobe.com/zh-hant/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/troubleshoot-product-recommendations-module-in-magento-commerce)文章。

#### 同步失敗

如果目錄同步處理的狀態為&#x200B;**失敗**，請提交[支援票證](https://experienceleague.adobe.com/zh-hant/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket)。

## 延伸記錄

使用環境變數來擴充記錄檔，並包含其他資料用於追蹤和疑難排解。 執行資料匯出CLI命令時，將環境變數新增至命令列，如下列範例所示。

### 檢查摘要裝載

當您重新同步摘要時，新增`EXPORTER_EXTENDED_LOG=1`環境變數，將摘要裝載包含在SaaS匯出記錄中。

```shell script
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed=products
```

作業完成後，摘要承載可在SaaS匯出記錄檔(`var/.log/saas-export.log`)中檢視。

### 保留摘要索引表格中的裝載

對於Commerce SaaS資料匯出擴充功能(`magento/module-data-exporter`) 103.3.0和更新版本，立即匯出摘要只會保留索引表格中最低限度的必要資料。 摘要包含所有目錄和庫存狀態摘要。

不建議在生產環境中保留索引表中的裝載資料，但在開發人員環境中可能會很有用。 當您重新同步摘要時，新增`PERSIST_EXPORTED_FEED=1`環境變數，以在索引中包含摘要裝載。

```shell script
PERSIST_EXPORTED_FEED=1 bin/magento saas:resync --feed=products
```

### 執行Profiler以疑難排解效能緩慢的問題

如果特定摘要的重新索引程式耗時過長，請執行效能評測器以收集可能對支援團隊有用的其他資料。

執行reindex命令時新增`EXPORTER_PROFILER=1`環境變數，以執行Profiler。

```
EXPORTER_PROFILER=1 bin/magento indexer:reindex catalog_data_exporter_products
```

效能分析工具資料會以下列格式儲存在資料匯出記錄檔(`var/log/commerce-data-export.log`)中：

```
<Provider class name>, <# of processed entities>, <execution time im ms>, <memory consumption in Mb>
```
