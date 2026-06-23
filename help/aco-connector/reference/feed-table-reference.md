---
title: 摘要表格結構描述參考
description: 瞭解 [!DNL Adobe Commerce Optimizer Connector] 用來追蹤摘要專案狀態、匯出狀態和錯誤詳細資訊的摘要資料表結構描述。
autotag-review: '2026-06-23T00:00:00.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="僅限PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案（Adobe管理的PaaS基礎結構）和內部部署專案的Adobe Commerce 。"
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 19de20caafd45e3a00896d0d4b29b7e96dfe94e1
workflow-type: tm+mt
source-wordcount: 324
ht-degree: 0%

---


# 摘要表格結構描述參考

每個摘要在[!DNL Adobe Commerce]資料庫中都有一個專用的MySQL資料表。 所有摘要表格會共用相同的欄結構。

## 支援的摘要

如需API端點、批次限制、索引器名稱和摘要表格名稱等支援摘要的完整清單，請參閱[聯結器模組與摘要端點](connector-reference.md#supported-feeds)。

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
| `status` | INT | 上次匯出嘗試的提交狀態代碼。 請參閱[摘要提交與錯誤處理](../connector-sync-pipeline.md#feed-submission-and-error-handling)。 |
| `errors` | 文字 | 此專案的[!DNL Commerce Optimizer] API傳回的JSON編碼錯誤詳細資料 |
| `metadata` | JSON | 匯出框架使用的內部同步標幟和鎖定中繼資料資訊 |

## 常見診斷查詢

使用下列SQL查詢直接檢查摘要表格狀態。 `feed_data`欄以[!DNL Adobe Commerce Optimizer] API格式儲存資料。 將預留位置值（例如`<SKU>`、`<ATTRIBUTE_CODE>`、`<SLUG>`和`<PRICE_BOOK_ID>`）取代為您環境中的實際值。

**產品摘要 — 依SKU：**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.sku') AS 'SKU',
       JSON_EXTRACT(f.feed_data, '$.source.locale') AS 'locale',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_products_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.sku') IN ('<SKU>');
```

**產品屬性摘要 — 依屬性代碼：**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.code') AS 'code',
       JSON_EXTRACT(f.feed_data, '$.source.locale') AS 'locale',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_product_attributes_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.code') IN ('<ATTRIBUTE CODE>');
```

**類別摘要 — 依URL路徑：**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.slug') AS 'slug',
    JSON_EXTRACT(f.feed_data, '$.source.locale') AS 'locale',
    f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_categories_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.slug') IN ('<SLUG>');
```

**價格摘要 — 依SKU：**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.sku') AS 'SKU',
       JSON_EXTRACT(f.feed_data, '$.priceBookId') AS 'price book ID',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_product_prices_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.sku') IN ('<SKU>');
```

**價格手冊摘要 — 依價格手冊識別碼：**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.priceBookId') AS 'price book ID',
    JSON_EXTRACT(f.feed_data, '$.name') AS 'name',
    JSON_EXTRACT(f.feed_data, '$.parentId') AS 'parent price book ID',
    JSON_EXTRACT(f.feed_data, '$.currency') AS 'currency',
    f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_price_books_feed f
WHERE JSON_UNQUOTE(JSON_EXTRACT(f.feed_data, '$.priceBookId'))  IN ('<PRICE_BOOK_ID>');
```

>[!MORELIKETHIS]
>
>- [聯結器模組和饋送端點](connector-reference.md)
>- [聯結器同步管道](../connector-sync-pipeline.md)
>- [管理同步處理](../data-sync-manage.md)
>- [聯結器摘要的欄位對應](field-mapping.md)
