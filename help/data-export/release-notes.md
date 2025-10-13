---
title: '[!DNL SaaS Data Export Extension]發行說明'
description: 適用於Adobe Commerce的 [!DNL Data Export Extension] 的最新發行資訊。
feature: Services, Release Notes
recommendations: noCatalog
exl-id: 8ae51d3d-8c12-4607-b7e5-985033143a84
source-git-commit: 9cca531a5f50850366a1c942fcda71eacecef5d0
workflow-type: tm+mt
source-wordcount: '1775'
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

## 103.4.14版

![修正](../assets/fix.svg)解決遺失[資料表時](https://developer.adobe.com/commerce/php/development/components/indexing/#mview)mview索引子`cde_product_overrides_feed_cl`工作可能失敗的問題。 此修正可確保穩定的重新索引，並防止多租使用者環境中與此資料表相關的工作失敗。&quot; <!--MDEE-1175-->

## 103.4.13版本

![修正](../assets/fix.svg)修正編輯Web組態設定導致產品摘要索引重設的問題。 <!--MDEE-1154-->
![修正](../assets/fix.svg)解決套件產品選項和變體可能多次出現在目錄服務回應中的問題，尤其是針對指派給多個商店或網站的產品。 透過此修正，每個產品每個套件選項/變體現在只會傳回一次，確保為商家和客戶提供精確且一致的店面顯示。<!--MDEE-1167-->

## 103.4.12版

![修正](../assets/fix.svg)修正存在客戶群組定價時，產品詳細資料頁面(PDP)未顯示目錄價格規則折扣的問題。 PDP現在正確顯示最低價格。<!--MDEE-1158-->

## 103.4.11版

僅![新](../assets/new.svg) [!BADGE PaaS]{type=Informative url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案(Adobe管理的PaaS基礎結構)和內部部署專案的Adobe Commerce 。"}
新增對其他產品屬性的支援，以在產品摘要中包含Commerce產品設定的稅種、屬性集和存貨資料。 如果客戶想要在產品匯出摘要中包含這些屬性，必須將「額外產品屬性」模組新增至其Adobe Commerce專案。 請參閱[新增稅捐類別、屬性集及存貨屬性](add-tax-attribute-set-inventory-attributes.md)。<!--MDEE-1135-->
![修正](../assets/fix.svg)解決在完整產品索引期間發生錯誤時，所刪除產品更新的同步處理不正確的問題。 現在，即使索引過程中發生錯誤，所有產品刪除仍會正確同步。<!--MDEE-1144-->

## 103.4.10版

![修正](../assets/fix.svg)修正某些動態建立的屬性傳回錯誤型別（`text`而非`OBJECT`）的問題。 現在，會一致地傳回正確的型別資訊，不需要手動重新同步或因應措施。<!--MDEE-1131-->
![修正](../assets/fix.svg)修正部分同步期間產品資料收集可能因LowStock庫存提供者發生錯誤而失敗的問題。 此修正可確保可靠匯出產品資料，且不會因為LowStock相關錯誤而略過任何產品ID。<!--MDEE-1132-->

## 103.4.9版

![修正](../assets/fix.svg)修正刪除產品或變更產品SKU時，未重新產生產品價格摘要的問題。<!--MDEE-1125-->
![修正](../assets/fix.svg)已改善產品更新處理，以確保在更新新建立的產品時，能正確反映變更，且新建立產品的SKU與先前已刪除的產品相同。 產品同步現在會正確使用更新的產品ID，確保準確可靠的資料匯出。<!--MDEE-1126-->
![修正](../assets/fix.svg)修正目錄服務可能透過確保在屬性刪除後發佈產品更新事件，傳回可設定產品過時變體資料的問題。<!--MDEE-1127-->

## 103.4.8版本

![新](../assets/new.svg)已新增層級價格資訊至價格摘要。 <!--MDEE-1070-->
![修正](../assets/fix.svg) Data Exporter擴充功能現在可正確匯出網站範圍的套件組合選擇價格，確保店面定價可根據「目錄價格範圍」設定反映準確的值。<!--MDEE-1115-->
![修正](../assets/fix.svg)之前，使用具有臨界值設定的Inventory management (多來源Inventory management)時，產品同步的`lowStock=true`狀態不正確。 此問題已修正，以確保低庫存報告的準確性。<!--MDEE-1113-->

## 103.4.7版

![修正](../assets/fix.svg)已移除儲存產品類別許可權的過時資料表。<!--MDEE-1065-->

## 103.4.6版

![修正](../assets/fix.svg)使用`ac_downloadable`屬性匯出Adobe Commerce可下載的產品資料以用於Adobe Commerce Optimizer。 <!--MDEE-1043-->
![修正](../assets/fix.svg) Adobe Commerce 2.4.4版的嚴重安裝錯誤修正。<!--MDEE-1074-->

## 103.4.5版

![新](../assets/new.svg) SaaS資料匯出現在支援Adobe Commerce `giftcard`產品型別。 在資料摘要中，禮品卡產品會匯出為產品屬性型別為`ac_giftcard`的簡單產品。 <!--MDEE-1042-->
![修正](../assets/fix.svg)已改善資料匯出錯誤報告。 記錄檔現在包含更詳細的錯誤訊息，包括原始技術細節，以便更輕鬆偵錯和追蹤錯誤。<!--MDEE-1064-->

## 103.4.4版

![New](../assets/new.svg)新增將`cleanup-feed`引數新增到`saas:resync` CLI命令時顯示的警告訊息。 `--cleanup-feed`選項應謹慎使用，且僅能在特定情況下使用，例如在環境清理後或與`--dry-run`選項搭配使用。 在其他情況下使用此外掛程式可能會導致資料遺失和同步問題。 <!--MDEE-1047-->
![Fix](../assets/fix.svg)已新增伺服器回應中的`x-request-id`，以改善追蹤能力。 <!--MDEE-1041-->
![修正](../assets/fix.svg)修正未儲存整個摘要批次的同步化狀態的問題，此問題會導致不必要的重新同步。 <!--MDEE-1049-->
![修正](../assets/fix.svg)修正當一個摘要包含錯誤時，同步處理期間會略過摘要批次中的所有摘要的問題。 <!--MDEE-976-->
![修正](../assets/fix.svg)已新增類別許可權索引器中維度的支援。<!--MDEE-654-->

## 103.4.3版本

![修正](../assets/fix.svg)解決在資料匯出程式期間因遺失EAV屬性而略過產品的問題。<!--MDEE-970-->

## 103.4.2版

![修正](../assets/fix.svg)已新增在使用包含`saas-export.log`環境變數的`saas:resync --dry-run`命令執行測試重新同步時，在`EXPORTER_EXTENDED_LOG=1`中收集實體裝載的功能。<!--MDEE-1023-->

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

![修正](../assets/fix.svg)透過改善與Catalog Data Export cron作業失敗相關的錯誤訊息，修正`BulkException`中無法追蹤的`cron.log`錯誤。<!--MDEE-966-->
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

![修正](../assets/fix.svg)刪除實體時，會針對網站(`deleted`)和客戶群組(`scopesWebsite`)的範圍設定服務摘要傳播`scopesCustomerGroup`旗標。<!--MDEE-839-->

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

![修正](../assets/fix.svg)新增支援資料傳輸稽核記錄，方法是在每次從Commerce執行個體傳輸資料至Commerce服務`data_sent_outside`時，新增傳送<!--MDEE-785-->事件的機制

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
