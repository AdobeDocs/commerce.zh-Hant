---
title: '[!DNL SaaS Data Export Extension]發行說明'
description: 適用於Adobe Commerce的 [!DNL Data Export Extension] 的最新發行資訊。
feature: Services, Release Notes
recommendations: noCatalog
exl-id: 8ae51d3d-8c12-4607-b7e5-985033143a84
source-git-commit: efbcfcf29e37f06d0ccfabba2bfce81f9c935844
workflow-type: tm+mt
source-wordcount: '2495'
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

## 2026版本

### 103.4.23版本

_2026年4月20日_

![修正](../assets/fix.svg) **解決刪除靜態EAV屬性時的SQL錯誤** — 刪除靜態EAV屬性時，ProductAttributeDelete外掛程式不再產生SQL錯誤，確保更順暢的屬性管理並改善系統可靠性。 <!--MDEE-1336-->
![修正](../assets/fix.svg) **類別移動後修正類別路徑匯出** — 確保類別移至其他父級時，類別摘要能正確更新`url_path`，避免連線的Commerce服務遺失或過時的類別路徑。<!--MDEE-1331-->
![修正](../assets/fix.svg) **已改善相關產品的已排程類別更新** — 類別URL的已排程更新現在只會影響預期的類別，保留資料完整性並防止相關產品發生意外變更。 現在，排程的類別URL變更會正確反映在匯出的資料中，讓店面導覽和連結的服務與目前的目錄保持一致。
<!--MDEE-1321-->

### 103.4.22版

_2026年4月13日_

![修正](../assets/fix.svg) **已改善資料同步處理**

- 修正刪除期間無法使用匯出服務時，無法從連線的Commerce服務正確移除已刪除產品的問題。 重試和重新同步操作現在可確保已刪除的產品正確地反映在SaaS中。<!--MDEE-1319-->
- 目錄實體（產品和類別）現在可以匯出至已連線的Commerce服務，即使管理商店檢視缺少屬性值亦然。 這麼做可改善與協力廠商擴充功能的相容性，並減少因遺失預設值導致的匯出錯誤。<!--MDEE-1333-->

![修正](../assets/fix.svg)解決當摘要記錄包含非預期或遺失資料時，在資料摘要同步處理狀態頁面上可能發生的錯誤。 系統現在可順利處理這類案例，提升穩定性並避免當機。 如果您使用Adobe Commerce Optimizer Connector將資料從Adobe Commerce同步到Adobe Commerce Optimizer，請更新至[ACO Connector 1.0.11](https://experienceleague.adobe.com/en/docs/commerce/aco-optimizer-connector/release-notes)版或更新版本以修正此問題。<!--MDEE-1327-->

### 103.4.21版

_2026年4月2日_

![修正](../assets/fix.svg) **改善手動重新同步類別許可權索引器的可靠性** — 修正依特定順序執行索引器可能導致部分產品暫時無法顯示的問題。 系統現在會強制執行正確的順序，並在需要時自動觸發完全重新同步，以確保手動重新索引操作後所有產品仍可見。<!--MDEE-1332-->

### 103.4.20版

_2026年3月5日_

![修正](../assets/fix.svg)透過更新產品摘要索引程式，確保與未來PHP版本的相容性，以避免不建議使用null作為陣列位移。 這會改善索引期間的穩定性。<!--MDEE-1306-->

![修正](../assets/fix.svg)已改善類別資料的產品摘要同步化 — 現在，當您在Commerce管理UI中更新類別URL時，產品摘要會自動重新整理以反映新的類別路徑。 不需要手動動作，而且您的產品搜尋結果在類別URL變更後一律為最新。<!--MDEE-1294-->

### 103.4.19版

_2026年2月6日_

![修正](../assets/fix.svg)解決PHP 8.5上`di:compile`命令失敗的問題。編譯程式現在已順利完成，確保與最新PHP版本的相容性。<!--MDEE-1299-->

### 103.4.18版

_2026年2月2日_

![修正](../assets/fix.svg)修正更新期間專案批次可能超過允許限制，導致同步資料至`items_limit_exceeded`Commerce服務[或](https://experienceleague.adobe.com/en/docs/commerce/user-guides/home)Adobe Commerce Optimizer[時發生](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/data-sync)個錯誤的問題。<!--MDEE-1264-->

![修正](../assets/fix.svg)在組合產品選項收集期間新增邏輯以登入失敗的專案，藉此改善產品資料匯出的可靠性。<!--CCSAAS-4458-->

### 103.4.17版

_2026年1月5日_

![修正](../assets/fix.svg)已更新資料匯出延伸模組(`magento/module-data-exporter`)以移除不再必要的`magento/module-analytics`相依性。<!--MDEE-1260-->

![修正](../assets/fix.svg)修正更新產品的層級價格未移除舊值，導致重複或過時的層級價格專案的問題。 現在，更新後只會顯示目前的層級價格。<!--MDEE-1157-->

![修正](../assets/fix.svg)修正店面未免費顯示$0價格或100%折扣的產品的問題。 店面和購物車定價現在是一致的。<!--MDEE-1159-->

![修正](../assets/fix.svg) Symfony 7.4 LTS相容性已新增至資料匯出延伸模組，以支援未來的升級和整合。<!--MDEE-1272-->

## 較舊的版本

### 103.4.16版

_2025年11月24日_

![修正](../assets/fix.svg)解決某些索引子在安裝或升級期間因多個索引子中缺少ActionInterface實作而無法切換到`Update On Schedule`模式的問題。 此修正可確保擴充功能安裝與升級成功，不會發生索引子相關錯誤。<!--MDEE-1235-->

### 103.4.15版

_2025年10月22日_

![新](../assets/new.svg)已新增資料摘要同步狀態擴充功能的支援，以監視和疑難排解從Adobe Commerce到連線服務（目錄服務、即時搜尋和產品建議）的資料傳輸。 如需有關安裝及使用此擴充功能的詳細資訊，請參閱[Commerce管理指南](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status.html)中的&#x200B;*資料摘要同步狀態監視*。<!--MDEE-954-->

### 103.4.14版

_2025年10月10日_

![修正](../assets/fix.svg)解決遺失[資料表時](https://developer.adobe.com/commerce/php/development/components/indexing/#mview)mview索引子`cde_product_overrides_feed_cl`工作可能失敗的問題。 此修正可確保穩定地重新索引，並防止多租使用者環境中與此表格相關的工作失敗。<!--MDEE-1175-->

### 103.4.13版本

_2025年9月24日_

![修正](../assets/fix.svg)修正編輯Web組態設定導致產品摘要索引重設的問題。<!--MDEE-1154-->

![修正](../assets/fix.svg)解決套件產品選項和變體可能多次出現在目錄服務回應中的問題，尤其是針對指派給多個商店或網站的產品。 透過此修正，每個產品每個套件選項/變體現在只會傳回一次，確保為商家和客戶提供精確且一致的店面顯示。<!--MDEE-1167-->

### 103.4.12版

_2025年9月18日_

![修正](../assets/fix.svg)修正存在客戶群組定價時，產品詳細資料頁面(PDP)未顯示目錄價格規則折扣的問題。 PDP現在正確顯示最低價格。<!--MDEE-1158-->

### 103.4.11版

_2025年8月29日_

僅![新](../assets/new.svg) [!BADGE PaaS]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案（Adobe管理的PaaS基礎結構）和內部部署專案的Adobe Commerce 。"}
新增對其他產品屬性的支援，以在產品摘要中包含Commerce產品設定的稅種、屬性集和存貨資料。 如果客戶想要在產品匯出摘要中包含這些屬性，必須將「額外產品屬性」模組新增至其Adobe Commerce專案。 請參閱[新增稅捐類別、屬性集及存貨屬性](add-tax-attribute-set-inventory-attributes.md)。<!--MDEE-1135-->

![修正](../assets/fix.svg)解決在完整產品索引期間發生錯誤時，所刪除產品更新的同步處理不正確的問題。 現在，即使索引過程中發生錯誤，所有產品刪除仍會正確同步。<!--MDEE-1144-->

### 103.4.10版

_2025年8月18日_

![修正](../assets/fix.svg)修正某些動態建立的屬性傳回錯誤型別（`text`而非`OBJECT`）的問題。 現在，會一致地傳回正確的型別資訊，不需要手動重新同步或因應措施。<!--MDEE-1131-->

![修正](../assets/fix.svg)修正部分同步期間產品資料收集可能因LowStock庫存提供者發生錯誤而失敗的問題。 此修正可確保可靠匯出產品資料，且不會因為LowStock相關錯誤而略過任何產品ID。<!--MDEE-1132-->

### 103.4.9版

_2025年8月13日_

![修正](../assets/fix.svg)修正刪除產品或變更產品SKU時，未重新產生產品價格摘要的問題。<!--MDEE-1125-->

![修正](../assets/fix.svg)已改善產品更新處理，以確保在更新新建立的產品時，能正確反映變更，且新產品的SKU與先前已刪除的產品相同。 產品同步現在會正確使用更新的產品ID，以確保準確可靠的資料匯出。<!--MDEE-1126-->

![修正](../assets/fix.svg)修正目錄服務可能透過確保在屬性刪除後發佈產品更新事件，傳回可設定產品過時變體資料的問題。<!--MDEE-1127-->

### 103.4.8版本

_2025年8月6日_

![新](../assets/new.svg)已新增層級價格資訊至價格摘要。<!--MDEE-1070-->

![修正](../assets/fix.svg) Data Exporter擴充功能現在可正確匯出網站範圍的套件組合選取價格，確保店面定價可根據「目錄價格範圍」組態反映正確的值。<!--MDEE-1115-->

![修正](../assets/fix.svg)之前，使用具有臨界值設定的Inventory management （多來源Inventory management）時，產品同步處理的`lowStock=true`狀態不正確。 此問題已修正，以確保低庫存報告的準確性。<!--MDEE-1113-->

### 103.4.7版

_2025年7月22日_

![修正](../assets/fix.svg)已移除儲存產品類別許可權的過時資料表。<!--MDEE-1065-->

### 103.4.6版

_2025年6月20日_

![修正](../assets/fix.svg)使用`ac_downloadable`屬性匯出Adobe Commerce可下載的產品資料以用於Adobe Commerce Optimizer。<!--MDEE-1043-->

![修正](../assets/fix.svg) Adobe Commerce 2.4.4版的嚴重安裝錯誤修正。<!--MDEE-1074-->

### 103.4.5版

_2025年5月27日_

![新](../assets/new.svg) SaaS資料匯出現在支援Adobe Commerce `giftcard`產品型別。 在資料摘要中，禮品卡產品會匯出為產品屬性型別為`ac_giftcard`的簡單產品。<!--MDEE-1042-->

![修正](../assets/fix.svg)已改善資料匯出錯誤報告。 記錄檔現在包含更詳細的錯誤訊息，包括原始技術細節，以便更輕鬆偵錯和追蹤錯誤。<!--MDEE-1064-->

### 103.4.4版

_2025年5月15日_

![New](../assets/new.svg)新增將`cleanup-feed`引數新增到`saas:resync` CLI命令時顯示的警告訊息。 `--cleanup-feed`選項應謹慎使用，且僅能在特定情況下使用，例如在環境清理後或與`--dry-run`選項搭配使用。 在其他情況下使用此外掛程式可能會導致資料遺失和同步問題。<!--MDEE-1047-->

![Fix](../assets/fix.svg)已新增伺服器回應中的`x-request-id`，以改善可追蹤性。<!--MDEE-1041-->

![修正](../assets/fix.svg)修正未儲存整個摘要批次的同步化狀態的問題，此問題會導致不必要的重新同步。<!--MDEE-1049-->

![修正](../assets/fix.svg)修正當一個摘要包含錯誤時，同步處理期間會略過摘要批次中的所有摘要的問題。<!--MDEE-976-->

![修正](../assets/fix.svg)已新增類別許可權索引器中維度的支援。<!--MDEE-654-->

### 103.4.3版本

_2025年4月22日_

![修正](../assets/fix.svg)解決在資料匯出程式期間因遺失EAV屬性而略過產品的問題。<!--MDEE-970-->

### 103.4.2版

_2025年4月16日_

![修正](../assets/fix.svg)已新增在使用包含`saas-export.log`環境變數的`saas:resync --dry-run`命令執行測試重新同步時，在`EXPORTER_EXTENDED_LOG=1`中收集實體裝載的功能。<!--MDEE-1023-->

### 103.4.1版

_2025年4月10日_

![Fix](../assets/fix.svg)已在QueryXml快取索引鍵中新增首碼，以防止與其他模組發生命名衝突。<!--MDEE-1019-->

### 103.4.0版

_2025年3月31日_

![修正](../assets/fix.svg)若產品未指派至類別，產品覆寫摘要將不再傳送許可權。<!--MDEE-449-->

### 103.3.21版

_2025年3月11日_

![新](../assets/new.svg)已新增功能，以根據指定的產品SKU清單來部分同步`products`、`productOverrides`和`productAttributes`摘要。 將`--by-ids`選項新增至resync CLI命令以使用新功能： <!--MDEE-606-->

```shell
bin/magento saas:resync --feed=<FEED_NAME> --by-ids='<SKU1>,<SKU2>,<SKU3>
```

![修正](../assets/fix.svg)解決已棄用的功能，減少與PHP 8.4之間的潛在相容性問題。<!--MDEE-1002-->

### 103.3.20版

_2025年2月28日_

![修正](../assets/fix.svg)透過改善與Catalog Data Export cron作業失敗相關的錯誤訊息，修正`BulkException`中無法追蹤的`cron.log`錯誤。<!--MDEE-966-->

![修正](../assets/fix.svg)已改善產品重新同步處理在擁有大量存放區檢視的執行個體上的效能。<!--MDEE-974-->

### 103.3.19版

_2025年2月13日_

![修正](../assets/fix.svg)已更新資料匯出擴充功能，以提升摘要擴充性。<!--MDEE-936-->

![修正](../assets/fix.svg)資料匯出處理器現在會在完全重新同步之前驗證索引器狀態，以避免摘要資料表中意外遺失資料。

### 103.3.18版

_2025年1月28日_

產品與類別實體的![修正](../assets/fix.svg)測試更新現在已在資料匯出資料更新上正確觸發。<!--MDEE-963-->

### 103.3.17版

_2025年1月20日_

![修正](../assets/fix.svg)已新增PHP 8.4的相容性。<!--MDEE-941-->

### 103.3.16版

_2025年1月6日_

針對多個商店檢視的可設定產品，![Fix](../assets/fix.svg)選項值可以空白。<!--MDEE-926-->

### 103.3.15版

_2024年12月12日_

![修正](../assets/fix.svg)已確保在舊組態上穩定執行整合測試。<!--MDEE-869-->

![修正](../assets/fix.svg)停止傳播不必要的屬性選項。<!--MDEE-882-->

![修正](../assets/fix.svg)修正當資料序列化失敗時，傳送至資料匯出記錄檔的錯誤訊息。<!--MDEE-913-->

![修正](../assets/fix.svg)透過額外的測試涵蓋範圍來增強簡單產品更新的可靠性。<!--MDEE-886-->

### 103.3.14版

_2024年10月8日_

![修正](../assets/fix.svg)匯出工具索引器現在會維持相依索引器的正確狀態。 以前，這些索引錯誤地失效，需要進行額外的檢查和驗證，以減緩索引效能。<!--MDEE-866-->

### 103.3.13版本

_2024年10月1日_

![修正](../assets/fix.svg)為屬性選項資料新增本機快取，以改善資料同步處理程式的效能。<!--MDEE-864-->

### 103.3.12版

_2024年9月25日_

![修正](../assets/fix.svg)解決增加簡單與虛擬產品同步處理時間的問題。<!--MDEE-861-->

### 103.3.11版

_2024年9月9日_

![修正](../assets/fix.svg)資料匯出服務現在會以百分比傳送套件組合產品的特殊價格資料，以更正先前傳送為最終價格的問題。<!--MDEE-854-->

![Fix](../assets/fix.svg)已更新與Monolog 3相容的Monolog實作。<!--MDEE-858-->

### 103.3.10版

_2024年8月26日_

![修正](../assets/fix.svg)修正產品自訂選項摘要的多重商店檢閱過濾。<!--MDEE-842-->

![修正](../assets/fix.svg)在摘要的雜湊值變更之前，不會重新提交無效的摘要。<!--MDEE-848-->

### 103.3.9版

_2024年7月22日_

![修正](../assets/fix.svg)刪除實體時，會針對網站(`deleted`)和客戶群組(`scopesWebsite`)的範圍設定服務摘要傳播`scopesCustomerGroup`旗標。<!--MDEE-839-->

### 103.3.8版本

_2024年7月17日_

![修正](../assets/fix.svg)已停用的組態選項已不再匯出為作用中選項。<!--MDEE-812-->

![Fix](../assets/fix.svg)變更子產品時，可設定產品上的選項和值現在會更新。<!--MDEE-835-->

![新](../assets/new.svg)已新增在產品屬性摘要中包含其他系統屬性資料的功能。

### 103.3.7版

_2024年6月25日_

![修正](../assets/fix.svg)從InventoryDataExporter模組移除不必要的相依性。

![修正](../assets/fix.svg)已變更CatalogInventoryDataExporter模組中所含存貨模組的必要版本，以支援Adobe Commerce 2.4.4版。

### 103.3.6版

_2024年6月20日_

![修正](../assets/fix.svg)修正多執行緒模式中摘要重新索引期間發生的死結。 查詢現在分成插入和更新操作。

![修正](../assets/fix.svg)已針對有許多網站的大型目錄最佳化價格查詢。

![New](../assets/new.svg)已新增重試邏輯，以便在發生死結時重新執行失敗的交易。

### 103.3.5版

_2024年6月5日_

![修正](../assets/fix.svg)設定SaaS一般模組最新相容資料匯出版本的相依性。

![修正](../assets/fix.svg)已將`ScopeConfig`執行個體取代為`ServiceConfigInterface`以支援不同的服務設定。

### 103.3.4版

_2024年5月31日_

![修正](../assets/fix.svg)新增每當從Commerce執行個體將資料傳輸到Commerce服務時，透過傳送`data_sent_outside`事件的機制來支援資料傳輸稽核記錄。<!--MDEE-785-->

### 103.3.3版本

_2024年5月21日_

![新](../assets/new.svg) SaaS資料匯出現在會快取屬性中繼資料查詢的Entity-Attribute-Value (EAV)屬性。

![修正](../assets/fix.svg)修正產品被刪除時，`InventoryStockStatus`摘要未在重試時儲存的問題。

### 103.3.2版

_2024年5月14日_

![修正](../assets/fix.svg)修正移除的實體摘要中缺少`modifiedAt`欄位的問題。

### 103.3.1版

_2024年5月8日_

![修正](../assets/fix.svg)修正安裝Page Builder時，產品摘要重新索引期間出現`Invalid Template File`訊息的問題。

### 103.3.0版

_2024年4月30日_

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

- 變更記錄表名稱 — 遵循與摘要表相同的命名模式，但變更記錄表名稱會新增`_cl`尾碼。 例如`catalog_data_exporter_products_cl`-> `cde-products_feed_cl`

如果您的自訂程式碼會參考任何這些實體，請以新名稱更新參考，以確保您的程式碼繼續正常運作。

![修正](../assets/fix.svg)在摘要資料中設定`modified_at`欄位，但僅限於需要它的摘要。

![修正](../assets/fix.svg)修改`productAttributes`查詢以僅擷取產品屬性。

### 103.2.6版

_2024年4月23日_

![修正](../assets/fix.svg)修正當資料表有首碼時，無法重新索引摘要的問題。

### 103.2.5版

_2024年4月19日_

![修正](../assets/fix.svg)已最佳化價格查詢。

### 103.2.4版

_2024年4月12日_

![修正](../assets/fix.svg)修正啟用Commerce Inventory management時，產品顯示的不正確庫存狀態。

### 103.2.3版本

_2024年4月3日_

![修正](../assets/fix.svg)修正網站層級特殊定價。

![修正](../assets/fix.svg)已針對所有處理的摘要新增Mutex。

### 103.2.2版

_2024年3月14日_

![修正](../assets/fix.svg)已改善大型目錄的摘要批次處理策略。 批次表格現在會填入有限數量的ID，以減少記憶體使用量。

![修正](../assets/fix.svg)消除了CommerceInventoryDataExporter對MSI模組的硬性相依性。

![修正](../assets/fix.svg)已改善`commerce-data-exporter`記錄檔，以收集更多資訊，並依不同的匯出階段加以組織。

### 103.2.1版

_2024年3月5日_

- 已發行更新版本。

### 103.2.0版

_2024年2月21日_

- 新增產品和價格的多執行緒資料同步。


