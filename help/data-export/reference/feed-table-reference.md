---
title: 摘要表格結構描述參考
description: 瞭解 [!DNL SaaS Data Export] 用來追蹤摘要專案狀態、匯出狀態和錯誤詳細資訊的摘要資料表結構描述。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Services
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088bid: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: cc250cf1-34eb-4863-80d0-d170d45ea067
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: c70c1643afbf8e9633df89a613d6798416c8eb44
workflow-type: tm+mt
source-wordcount: 429
ht-degree: 0%

---


# 摘要表格結構描述參考

每個摘要在[!DNL Adobe Commerce]資料庫中都有一個專用的MySQL資料表。 所有摘要表格會共用相同的欄結構。 下表列出每個摘要及其CLI摘要名稱、索引器ID和摘要表格名稱。

## 支援的摘要

實際的摘要清單取決於已安裝的[!DNL SaaS Data Export]封裝。


| 摘要(`--feed`) | 用途 | 索引子ID | 摘要表格 | 匯出模式 |
| --- | ------------------------------------------------------------------- | --- | --- | --- |
| `products` | 產品目錄（屬性、類別、影像等） | `catalog_data_exporter_products` | `cde_products_feed` | 立即 |
| `productAttributes` | 屬性定義和中繼資料。 用於定義搜尋結構描述。 | `catalog_data_exporter_product_attributes` | `cde_product_attributes_feed` | 立即 |
| `categories` | 類別資料 | `catalog_data_exporter_categories` | `cde_categories_feed` | 立即 |
| `prices` | 產品價格與客戶群組價格及層級價格 | `catalog_data_exporter_product_prices` | `cde_product_prices_feed` | 立即 |
| `variants` | 可設定的產品變體 | `catalog_data_exporter_product_variants` | `cde_product_variants_feed` | 立即 |
| `scopesWebsite` | 具有商店檢視代碼的網站 | `scopes_website_data_exporter` | `scopes_website_data_exporter` | 舊版 |
| `scopesCustomerGroup` | 客戶群組定義 | `scopes_customergroup_data_exporter` | `scopes_customergroup_data_exporter` | 舊版 |
| `productOverrides` | 計算出的產品許可權 | `catalog_data_exporter_product_overrides` | `cde_product_overrides_feed` | 立即 |
| `categoryPermissions` *(EE)* | 原始類別許可權資料 | `catalog_data_exporter_category_permissions` | `cde_category_permissions_feed` | 立即 |
| `orders` | 銷售訂單狀態 | `sales_order_data_exporter_v2` | `sales_data_exporter_orders_v2` | 舊版 |

**匯出模式**&#x200B;資料行指出每個摘要收集和提交資料的方式：

- **立即模式摘要** — 收集資料、使用內容雜湊略過未變更的專案（雜湊重複資料刪除），並在相同的索引器執行中送出更新。
- **舊版模式摘要** (`scopesWebsite`， `scopesCustomerGroup`， `orders`) — 請先將組合資料儲存在摘要資料表中，然後透過個別的cron工作送出。

請參閱[同步處理模式](../sync-overview.md#synchronization-modes)。

## 結構描述

| 欄 | 型別 | 說明 |
| --- | --- | ---------------- |
| `id` | 整數(PK) | 自動增加主索引鍵 |
| `source_entity_id` | INT | 來自Commerce來源表格的實體ID （例如，`catalog_product_entity.entity_id`） |
| `feed_id` | VARCHAR | 摘要專案的唯一識別碼。 計算為專案識別欄位的雜湊（例如，`sku + storeViewCode`），而不是自動增加值。 |
| `feed_data` | JSON | 此專案的摘要裝載。 僅填入實體識別碼和範圍的最小資訊。 設定`PERSIST_EXPORTED_FEED=1`時，會儲存完整裝載。 |
| `feed_hash` | VARCHAR | 用於變更偵測的內容雜湊。 從承載中計算，排除時間戳記(`modifiedAt`， `updatedAt`)。 如果雜湊符合前一個匯出，則不會重新提交專案。 |
| `is_deleted` | TINYINT | 軟刪除標籤。 在Commerce中刪除實體時，設為`1`。 |
| `modified_at` | 時間戳記 | 上次修改此摘要專案的時間 |
| `status` | INT | 上次匯出嘗試的提交狀態代碼。 請參閱[摘要提交與HTTP錯誤處理](../sync-overview.md#feed-submission-and-http-error-handling)。 |
| `errors` | 文字 | SaaS服務針對此專案傳回的JSON編碼錯誤詳細資料 |
| `metadata` | JSON | 匯出框架使用的內部同步標幟和鎖定中繼資料資訊 |

## 常見診斷查詢

使用下列SQL查詢直接檢查摘要表格狀態。 將預留位置值（例如`<SKU>`、`<ATTRIBUTE_CODE>`和`<CATEGORY_ID>`）取代為您環境中的實際值。 如需資料表名稱的完整清單，請參閱[支援的摘要](#supported-feeds)。

**產品摘要 — 依SKU：**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.sku') AS 'SKU',
       JSON_EXTRACT(f.feed_data, '$.storeViewCode') AS 'store view code',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_products_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.sku') IN ('<SKU>');
```

**產品屬性摘要 — 依屬性代碼：**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.attributeCode') AS 'code',
       JSON_EXTRACT(f.feed_data, '$.storeViewCode') AS 'store view code',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_product_attributes_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.attributeCode') IN ('<ATTRIBUTE_CODE>');
```

**價格摘要 — 依SKU：**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.sku') AS 'SKU',
       JSON_EXTRACT(f.feed_data, '$.websiteCode') AS 'website code',
       JSON_EXTRACT(f.feed_data, '$.customerGroupCode') AS 'customer group code',
       IFNULL(cg.customer_group_code, '-- (base price)') AS 'AC customer group',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_product_prices_feed f
LEFT JOIN customer_group cg
       ON sha1(cg.customer_group_id) = JSON_EXTRACT(f.feed_data, '$.customerGroupCode')
WHERE JSON_EXTRACT(f.feed_data, '$.sku') IN ('<SKU>');
```

**產品覆寫摘要 — 依SKU：**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.sku') AS 'SKU',
       JSON_EXTRACT(f.feed_data, '$.websiteCode') AS 'website code',
       JSON_EXTRACT(f.feed_data, '$.customerGroupCode') AS 'customer group code',
       IFNULL(cg.customer_group_code, 'NA (deleted)') AS 'AC customer group',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_product_overrides_feed f
LEFT JOIN customer_group cg
       ON sha1(cg.customer_group_id) = JSON_EXTRACT(f.feed_data, '$.customerGroupCode')
WHERE JSON_EXTRACT(f.feed_data, '$.sku') IN ('<SKU>');
```

**類別摘要 — 依類別識別碼：**

```sql
SELECT JSON_EXTRACT(feed_data, '$.categoryId') AS 'Category ID',
       JSON_EXTRACT(f.feed_data, '$.storeViewCode') AS 'store view code',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_categories_feed f
WHERE JSON_EXTRACT(feed_data, '$.categoryId') IN (<CATEGORY_ID>);
```

**變體摘要 — 依可設定的產品SKU：**

```sql
SELECT JSON_EXTRACT(feed_data, '$.parentSku') AS 'configurable SKU',
       JSON_EXTRACT(feed_data, '$.productSku') AS 'Variant SKU',
       JSON_EXTRACT(f.feed_data, '$.optionValues') AS 'options',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_product_variants_feed f
WHERE JSON_EXTRACT(feed_data, '$.parentSku') = '<SKU>';
```


>[!MORELIKETHIS]
>
>- [使用SaaS資料匯出同步處理資料](../sync-overview.md)
>- [檢視和管理同步處理](../data-sync-manage.md)
>- [使用Commerce CLI同步摘要](../data-export-cli-commands.md)
