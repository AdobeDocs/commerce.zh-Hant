---
title: '[!DNL SaaS Data Export Extension]發行說明'
description: 適用於Adobe Commerce的 [!DNL Data Export Extension] 的最新發行資訊。
feature: Services, Release Notes
recommendations: noCatalog
exl-id: 8ae51d3d-8c12-4607-b7e5-985033143a84
source-git-commit: bb9300c621ceac618c51e4dd787527ac1e960dd8
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 0%

---

# [!DNL SaaS Data Export]擴充功能發行說明

下列發行說明說明[!DNL SaaS data export]擴充功能的最新版本。 支援目前的主要發行版本。 舊版的發行說明僅供參考。

更新包括：

![新](../assets/new.svg)新功能
![修正](../assets/fix.svg)修正和改良
![錯誤](../assets/bug.svg)已知問題


>[!NOTE]
>
>SaaS資料匯出擴充功能是隨「即時搜尋」、「產品建議」和「目錄服務」自動安裝的模組集合。 您可以使用Composer檢查系統上安裝的版本。 在某些情況下，您可能會想要升級系統上的資料匯出擴充功能，以取得修正或新功能，而不更新Commerce服務版本。

## 目前的主要版本

## 103.4.2版

![修正](../assets/fix.svg)已新增在使用包含`EXPORTER_EXTENDED_LOG=1`環境變數的`saas:resync --dry-run`命令執行測試重新同步時，在`saas-export.log`中收集實體裝載的功能。<!--MDEE-1023-->

## 103.4.1版

![Fix](../assets/fix.svg)已在QueryXml快取索引鍵中新增首碼，以防止與其他模組發生命名衝突。<!--MDEE-1019-->

## 103.4.0版

![修正](../assets/fix.svg)若產品未指派至類別，產品覆寫摘要將不再傳送許可權。<!--MDEE-449-->

## 103.3.21版

![修正](../assets/new.svg)已新增功能，以根據指定的產品SKU清單來部分同步`products`、`productOverrides`和`productAttributes`摘要。 將`--by-ids`選項新增至resync CLI命令以使用新功能： <!--MDEE-606-->

```shell
bin/magento saas:resync --feed=<FEED_NAME> --by-ids='<SKU1>,<SKU2>,<SKU3>
```

![修正](../assets/fix.svg)解決已棄用的功能，減少與PHP 8.4之間的潛在相容性問題。<!--MDEE-1002-->

## 103.3.20版

![修正](../assets/fix.svg)透過改善與Catalog Data Export cron作業失敗相關的錯誤訊息，修正`cron.log`中無法追蹤的`BulkException`錯誤。<!--MDEE-966-->
![修正](../assets/fix.svg)已改善產品重新同步化程式在擁有大量存放區檢視的執行個體上的效能。<!--MDEE-974-->

## 103.3.19版

![修正](../assets/fix.svg)已更新資料匯出擴充功能，以提升摘要擴充性。 <!--MDEE-936-->
![修正](../assets/fix.svg)資料匯出處理器現在會在完全重新同步之前驗證索引器狀態，以避免摘要資料表中意外遺失資料。

## 103.3.18版

產品與類別實體的![修正](../assets/fix.svg)測試更新現在已在資料匯出資料更新上正確觸發。<!--MDEE-963-->

## 103.3.17版

![修正](../assets/fix.svg)已新增PHP 8.4的相容性。<!--MDEE-941-->

## 103.3.16版

針對多個商店檢視的可設定產品，![Fix](../assets/fix.svg)選項值可以空白。<!--MDEE-926-->

## 103.3.15版

![修正](../assets/fix.svg)已確保在舊組態上穩定執行整合測試。 <!--MDEE-869-->
![修正](../assets/fix.svg)停止傳播不必要的屬性選項。 <!--MDEE-882-->
![修正](../assets/fix.svg)修正當資料序列化失敗時，傳送至資料匯出記錄檔的錯誤訊息。 <!--MDEE-913-->
![修正](../assets/fix.svg)透過額外的測試涵蓋範圍來增強簡單產品更新的可靠性。<!--MDEE-886-->

## 103.3.14版

![修正](../assets/fix.svg)匯出工具索引器現在會維持相依索引器的正確狀態。 以前，這些索引錯誤地失效，需要進行額外的檢查和驗證，以減緩索引效能。<!--MDEE-866-->

## 103.3.13版本

![修正](../assets/fix.svg)為屬性選項資料新增本機快取，以改善資料同步處理程式的效能。<!--MDEE-864-->

## 103.3.12版

![修正](../assets/fix.svg)解決增加簡單與虛擬產品同步處理時間的問題。<!--MDEE-861-->

## 103.3.11版

![修正](../assets/fix.svg)資料匯出服務現在會以百分比傳送套件組合產品的特殊價格資料，以更正先前傳送為最終價格的問題。 <!--MDEE-854-->
![Fix](../assets/fix.svg)已更新與Monolog 3相容的Monolog實作。<!--MDEE-858-->

## 103.3.10版

![修正](../assets/fix.svg)修正產品自訂選項摘要的多重商店檢閱過濾。 <!--MDEE-842-->
![修正](../assets/fix.svg)在摘要的雜湊值變更之前，不會重新提交無效的摘要。<!--MDEE-848-->

## 103.3.9版

![修正](../assets/fix.svg)刪除實體時，會針對網站(`scopesWebsite`)和客戶群組(`scopesCustomerGroup`)的範圍設定服務摘要傳播`deleted`旗標。<!--MDEE-839-->

## 103.3.8版本

![修正](../assets/fix.svg)已停用的組態選項已不再匯出為作用中選項。<!--MDEE-812-->
![Fix](../assets/fix.svg)變更子產品時，現在會在可設定的產品上更新選項和值。 <!--MDEE-835-->
![新](../assets/new.svg)已新增在產品屬性摘要中包含其他系統屬性資料的功能。

## 103.3.7版

![修正](../assets/fix.svg)從InventoryDataExporter模組移除不必要的相依性。
![修正](../assets/fix.svg)已變更CatalogInventoryDataExporter模組中所含存貨模組的必要版本，以支援Adobe Commerce 2.4.4版。

## 103.3.6版

![修正](../assets/fix.svg)修正多執行緒模式中摘要重新索引期間發生的死結。 查詢現在分成插入和更新操作。
![修正](../assets/fix.svg)已針對有許多網站的大型目錄最佳化價格查詢。
![New](../assets/new.svg)已新增重試邏輯，以便在發生死結時重新執行失敗的交易。

## 103.3.5版

![修正](../assets/fix.svg)設定SaaS一般模組最新相容資料匯出版本的相依性。

![修正](../assets/fix.svg)已將`ScopeConfig`執行個體取代為`ServiceConfigInterface`以支援不同的服務設定。

## 103.3.4版

![修正](../assets/fix.svg)新增支援資料傳輸稽核記錄，方法是在每次從Commerce執行個體傳輸資料至Commerce服務<!--MDEE-785-->時，新增傳送`data_sent_outside`事件的機制

## 103.3.3版本

![新](../assets/new.svg) SaaS資料匯出現在會快取屬性中繼資料查詢的Entity-Attribute-Value (EAV)屬性。

![修正](../assets/fix.svg)修正產品被刪除時，`InventoryStockStatus`摘要未在重試時儲存的問題。

## 103.3.2版

![修正](../assets/fix.svg)修正移除的實體摘要中缺少`modifiedAt`欄位的問題。

## 103.3.1版

![修正](../assets/fix.svg)修正安裝Page Builder時，產品摘要重新索引期間出現`Invalid Template File`訊息的問題。

## 103.3.0版

![新](../assets/new.svg)已移轉立即匯出摘要資料表至統一結構：
`id`、`source_entity_id`、`feed_id`、`modified_at`、`is_deleted`、`status`、`feed_data`、`feed_hash`、`errors`

![新](../assets/new.svg)已將目錄和詳細目錄摘要移轉至立即匯出解決方案。

![新](../assets/new.svg)已將立即匯出摘要cron-job重新命名為`*_feed_resend_failed_items`。

![新](../assets/new.svg)已重新命名立即匯出摘要、索引器檢視ID和變更記錄表。
- 摘要表格（和索引子檢視ID）：
   - `catalog_data_exporter_products` -> `cde_products_feed`
   - `catalog_data_exporter_product_attributes` -> `cde_product_attributes_feed`
   - `catalog_data_exporter_categories` -> `cde_categories_feed`
   - `catalog_data_exporter_product_prices` -> `cde_product_prices_feed`
   - `catalog_data_exporter_product_variants` -> `cde_product_variants_feed`
   - `inventory_data_exporter_stock_status` -> `inventory_data_exporter_stock_status_feed`
- 變更記錄表名稱 — 遵循與摘要表相同的命名模式，但變更記錄表名稱會新增`_cl`尾碼。  例如`catalog_data_exporter_products_cl`-> `cde-products_feed_cl`
如果您的自訂程式碼會參考任何這些實體，請以新名稱更新參考，以確保您的程式碼繼續正常運作。

![修正](../assets/fix.svg)在摘要資料中設定`modified_at`欄位，但僅限於需要它的摘要。

![修正](../assets/fix.svg)修改`productAttributes`查詢以僅擷取產品屬性。

## 103.2.6版

![修正](../assets/fix.svg)修正當資料表有首碼時，無法重新索引摘要的問題。

## 103.2.5版

![修正](../assets/fix.svg)已最佳化價格查詢。

## 103.2.4版

![修正](../assets/fix.svg)修正啟用Commerce Inventory management時，產品顯示的不正確庫存狀態。

## 103.2.3版本

![修正](../assets/fix.svg)修正網站層級特殊定價。
![修正](../assets/fix.svg)已針對所有處理的摘要新增Mutex。


## 103.2.2版

![修正](../assets/fix.svg)已改善大型目錄的摘要批次處理策略。 批次表格現在會填入有限數量的ID，以減少記憶體使用量。

![修正](../assets/fix.svg)消除了CommerceInventoryDataExporter對MSI模組的硬性相依性。

![修正](../assets/fix.svg)已改善`commerce-data-exporter`記錄檔，以收集更多資訊，並依不同的匯出階段加以組織。

## 103.2.1版

- 已發行更新版本。

## 103.2.0版

- 新增產品和價格的多執行緒資料同步。
