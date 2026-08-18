---
source-git-commit: 1b8a6de3a35a626f211089955029207f8a88414c
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 0%

---
# MDEE記錄程式碼參考

記錄程式碼格式： `CDE<group_id>-<log_id>` （如`CDE01-02`）

來源： `commerce-data-export`、`commerce-data-export-ee`、`saas-export`

僅將代碼指派給`error`、`warning`和`critical`層級的記錄訊息。 已排除`info`、`notice`和`debug`層級訊息。

## 群組01 — 資料收集階段

與從來源實體（通常在資料提供者內）收集資料時發生的錯誤或警告相關的記錄代碼。
- 受影響的實體可能會使用部分資料進行處理，或如果發生錯誤則完全跳過。 如需詳細資訊，請參閱記錄訊息。
- 警告可能表示協力廠商模組與Data Export擴充功能的整合不正確；不過，同步作業通常會繼續。

| 記錄代碼 | 平準 | 訊息 |
|----------|---------|------------------------------------------------------------------------------------------------------------------------------------|
| CDE01-01 | 錯誤 | `CDE01-01 Failed to add stock info to "ac_inventory" attribute for ids "{ids}". Error: {exception_message}` |
| CDE01-02 | 警告 | `CDE01-02 Field "{field}" is missing in row {row_data}` |
| CDE01-03 | 警告 | `CDE01-03 Invalid field "{field}" requested from inventory config {config_data}` |
| CDE01-04 | 錯誤 | `CDE01-04 Was not able to add data to "ac_attribute_set" attribute for ids "{ids}". Error: {exception_message}` |
| CDE01-05 | 錯誤 | `CDE01-05 Unable to sync feed "{feed}" for ids "{ids}". Affected data provider: "{provider}". Error: {exception_message}` |
| CDE01-06 | 錯誤 | `CDE01-06 Unable to sync feed "{feed}" for ids "{ids}". Error: {exception_message}` |
| CDE01-07 | 錯誤 | `CDE01-07 Source entity id is null. Item sync was skip for feed "{feed}". field: "{field}", item: {item}` |
| CDE01-08 | 錯誤 | `CDE01-08 Cannot collect "inStock" for products "{product_ids}": no sales channel data for stores "{store_view_codes}"` |
| CDE01-09 | 錯誤 | `CDE01-09 Cannot get status attribute. Product variants ignore stock status. Error: {exception_message}` |
| CDE01-10 | 錯誤 | `CDE01-10 Unable to retrieve gift card product options for products "{values}". Error: {exception_message}` |
| CDE01-11 | 錯誤 | `CDE01-11 Unable to retrieve gift card shopper input options for products "{values}". Error: {exception_message}` |
| CDE01-12 | 警告 | `CDE01-12 Catalog Permissions: Global Configuration path was not found for path {path}. {config_dump}` |
| CDE01-13 | 錯誤 | `CDE01-13 Catalog Permissions: wrong state in global config. item: {item}, config: {config}` |
| CDE01-14 | 錯誤 | `CDE01-14 Failed to assign UUIDs for type: {type}, ids: {ids}` |
| CDE01-15 | 錯誤 | `CDE01-15 Failed to assign UUIDs for type: {type}, ids: {ids}. duplicates: {duplicates}` |
| CDE01-16 | 錯誤 | `CDE01-16 "{feed_name}" feed sync error: cannot build identifier for "{field}". Item skipped: {item}` |
| CDE01-17 | 警告 | `CDE01-17 Failed to create attribute "{attribute_code}". Will be retried on next sync. Error: {message}` |
| CDE01-18 | 警告 | `CDE01-18 Error on getting datetime for catalog price rule fetch. Using system time. website: "{website_id}", store: "{store_id}"` |
| CDE01-19 | 警告 | `CDE01-19 GiftCard {sku} does not have shopper input options` |
| CDE01-20 | 警告 | `CDE01-20 GiftCard {sku} doesn't have valid options: {options}` |
| CDE01-21 | 錯誤 | `CDE01-21 Unable to resolve url_path for category {id} with path "{path}", url_key "{urk_key}", store "{store}"` |
| CDE01-22 | 錯誤 | `CDE01-22 Unable to resolve url_path for category{id} with path "{path}" for store view "{store}"` |

## 群組02 — 傳送資料至SaaS階段

將摘要資料提交至SaaS端點時，所發生的錯誤或警告的相關記錄程式碼。
- 錯誤通常表示HTTP要求、回應處理或資料驗證期間發生失敗，導致資料無法被接受。
- 警告通常表示要求會自動重試的暫時性狀況（例如速率限制或伺服器錯誤）。

| 記錄代碼 | 平準 | 訊息 |
|-----------|---------|---------|
| CDE02-01 | 錯誤 | `CDE02-01 Application error on sending data to SaaS for feed "{feed_name}". Error: {error_message}` |
| CDE02-02 | 錯誤 | `CDE02-02 Unexpected error on sending data to SaaS for feed "{feed_name}". Error: {error_message}` |
| CDE02-03 | 警告 | `CDE02-03 Cannot parse the API response because the request was not successful.` |
| CDE02-04 | 錯誤 | `CDE02-04 Cannot obtain feed metadata for feed name "{feed_name}". Sync terminated. Error: {error_message}` |
| CDE02-05 | 錯誤 | `CDE02-05 Failed to submit feed batch for feed {feed_name}. Error: {error_message}` |
| CDE02-06 | 錯誤 | `CDE02-06 Failed to retry feed items submission for feed {feed_name}. Error: {error_message}` |
| CDE02-07 | 警告 | `CDE02-07 Feed "{feed_name}" sync error: too many requests (HTTP 429). Request will be retried.` |
| CDE02-08 | 警告 | `CDE02-08 Feed "{feed_name}" sync error: Server error (HTTP {http_status_code}). Request will be retried.` |
| CDE02-09 | 錯誤 | `CDE02-09 Feed "{feed_name}" sync error: data validation failed. Check logs. Request will not be retried.` |
| CDE02-10 | 警告 | `CDE02-10 Feed "{feed_name}" sync error: Client error (HTTP {http_status_code}). Request will be retried.` |
| CDE02-11 | 警告 | `CDE02-11 Feed "{feed_name}" sync error: application-level error. Request will be retried.` |
| CDE02-12 | 錯誤 | `CDE02-12 Feed "{feed_name}" sync error API request was not successful (status code: {status_code}).` |
| CDE02-13 | 警告 | `CDE02-13 The zlib-ext is not loaded. Request body can't be compressed and will proceed with regular json` |

## 群組03 — 排程實體更新時同步

與排程或觸發同步處理以回應實體變更時發生的錯誤或警告相關的記錄程式碼。
- 錯誤會導致無法排程增量同步，且通常需要完全或部分重新同步才能復原。
- 警告指出由於不支援的輸入、缺少識別碼或設定問題，同步作業已略過或延遲。

| 記錄代碼 | 平準 | 訊息 |
|----------|----------|----------------------------------------------------------------------------------------------------------------------------------|
| CDE03-01 | 錯誤 | `CDE03-01 Cannot schedule resync for feeds` |
| CDE03-02 | 警告 | `CDE03-02 Skipping product feed update scheduling. Category path "{category_path}" is wrongly formatted` |
| CDE03-03 | 錯誤 | `CDE03-03 Categories sync error on category "{category_id}" save. Run resync. Error: {error_message}` |
| CDE03-04 | 錯誤 | `CDE03-04 Product sync scheduling error on url key change ({old_url_key} -> {new_url_key}). Run resync. Error: {error_message}` |
| CDE03-05 | 錯誤 | `CDE03-05 Product sync scheduling error on category path change ({old_path} -> {new_path}). Run resync. Error: {error_message}` |
| CDE03-06 | 錯誤 | `CDE03-06 Product sync scheduling error on attribute "{attribute_code}" deletion. Run full resync. Error: {error_message}` |
| CDE03-07 | 警告 | `CDE03-07 Product sync scheduling error on inventory source save for SKUs: {product_skus}. Error: {error_message}` |
| CDE03-08 | 錯誤 | `CDE03-08 Product variants sync scheduling error on product "{sku_or_id}" save. Run resync. Error: {error_message}` |
| CDE03-09 | 警告 | `CDE03-09 The '{feed_name}' feed does not support partial resync by IDs, or an unsupported identifier type was specified.` |
| CDE03-10 | 警告 | `CDE03-10 There are no {id_field}s found to reindex for provided identifiers list: {identifiers}` |
| CDE03-11 | 錯誤 | `CDE03-11 Categories Permissions feed sync scheduling error on category "{category_id_and_name}" delete. Error: {error_message}` |
| CDE03-12 | 警告 | `CDE03-12 Product Overrides sync failed. Marked indexer as invalid. Error: {error_message}` |
| CDE03-13 | 錯誤 | `CDE03-13 Cannot invalidate indexers "{indexer_ids}" for event "{event_name}". Error: {error_message}` |
| CDE03-14 | 錯誤 | `CDE03-14 Failed to read config values. Indexer invalidation skipped. Error: {error_message}` |
| CDE03-15 | 錯誤 | `CDE03-15 Categories Permissions feed sync scheduling error on config save: {error_message}` |
| CDE03-16 | 錯誤 | `CDE03-16 Failed to reindex category permissions global configuration after full reindex: {error_message}` |
| CDE03-17 | 關鍵 | `CDE03-17 Failed to recreate product override view subscriptions on customer group save: {error_message}` |
| CDE03-18 | 關鍵 | `CDE03-18 Failed to recreate product override view subscriptions on customer group delete: {error_message}` |
| CDE03-19 | 錯誤 | `CDE03-19 Failed to remove product override view subscriptions during table maintenance: {error_message}` |
| CDE03-20 | 錯誤 | `CDE03-20 Failed to recreate product override view subscriptions after table maintenance: {error_message}` |
| CDE03-21 | 錯誤 | `CDE03-21 Product sync scheduling error on attribute {%s} option change. Run resync. Error: %s` |
| CDE03-22 | 警告 | `CDE03-22 StagedCategoryUrlKeyChangeDetector: no active row at version {version_id} for entity_id(s) [{entity_ids}]; skipping.` |
| CDE03-23 | 錯誤 | `CDE03-23 StagedCategoryUrlKeyChangeDetector: catalog_category url_key attribute not found; failing open.` |
| CDE03-24 | 錯誤 | `CDE03-24 InvalidateProductFeedOnCategoryUrlKeyChange: scheduler failed for path "{path}": {error_message}` |
| CDE03-25 | 錯誤 | `CDE03-25 InvalidateProductFeedOnCategoryUrlKeyChange: gate query failed: {error_message}` |
| CDE03-26 | 錯誤 | `CDE03-26 InvalidateProductFeedOnCategoryUrlKeyChange: unable to expand staged url_key category reindex scope: {error_message}` |
| CDE03-27 | 錯誤 | `CDE03-27 Failed to invalidate indexers after config "{config_section}" change. Error: {error_message}` |
| CDE03-28 | 警告 | `CDE03-28 StagedCategoryUrlKeyChangeDetector: catalog category staging schema is not present; skipping staged url_key change detection.` |

## 群組04 — 與索引或設定相關的一般錯誤

與索引處理期間或因設定錯誤而發生的錯誤相關的記錄程式碼。

| 記錄代碼 | 平準 | 訊息 |
|-----------|---------|---------|
| CDE04-02 | 錯誤 | `CDE04-02 Cannot set indexer to Update On Schedule mode for indexer {indexer_id}. Error: {message}` |
| CDE04-03 | 警告 | `CDE04-03 Partial sync failed for changelog "{changelog_name}". Should be retried. Error: {message}` |
| CDE04-04 | 錯誤 | `CDE04-04 Feed metadata does not contain indexer name. Check di.xml config` |
| CDE04-05 | 錯誤 | `CDE04-05 Cannot load feed indexer for feed` |
| CDE04-06 | 錯誤 | `CDE04-06 Failed to reset MView triggers for "{affected_views}" on index table switch. Run reindex. Error: {message}` |
| CDE04-07 | 錯誤 | `CDE04-07 Error on partial resync for feed "{feed_name}". Error: {message}` |
| CDE04-08 | 錯誤 | `CDE04-08 Error retrying failed items sync for feed "{feed_name}". Error: {message}` |
| CDE04-09 | 錯誤 | `CDE04-09 Error on full resync for feed "{feed_name}". Error: {message}` |
| CDE04-10 | 錯誤 | `CDE04-10 Error during full sync. Message: "{message}". The following IDs were skipped: [{ids}]` |
| CDE04-11 | 警告 | `CDE04-11 Feed "{feed_name}" sync failed. Resync will be run on next cron run. Error: {message}` |
| CDE04-12 | 警告 | `CDE04-12 Partial sync failed for feed "{feed_name}". Retry has been scheduled. Error: {message}` |
| CDE04-13 | 錯誤 | `CDE04-13 Sync completed, but failed to persist status to feed table for "{feed_name}" feed. Error: {message}` |
| CDE04-14 | 錯誤 | `CDE04-14 Cannot delete feed items for feed "{feed_name}" for ids: "{ids}". Error: {message}` |
| CDE04-15 | 警告 | `CDE04-15 Failed to serialize metadata after sync. Error: {message}` |
| CDE04-16 | 警告 | `CDE04-16 Batch table insert query "{query}" returned unexpected result. Expected: {expected_class}, Actual: {actual_type}` |
| CDE04-17 | 警告 | `CDE04-17 Failed to check indexer type when setting schedule mode: {message}` |
| CDE04-18 | 警告 | `CDE04-18 Fixture generator: failed to filter indexer changelog tables from fixture SQL: {message}` |
| CDE04-19 | 警告 | `CDE04-19 The identifier for a feed item is empty. Sync is skipped for the entity.` |
| CDE04-20 | 警告 | `CDE04-20 Unexpected call: feed "{feed_name}" is not locked, trace: {stack_trace}` |
| CDE04-21 | 錯誤 | `CDE04-21 Failed to clean up deleted feed items for feed "{feed_name}". Error: {error_message}` |
