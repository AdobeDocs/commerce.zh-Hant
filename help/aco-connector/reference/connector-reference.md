---
title: '[!DNL Adobe Commerce Optimizer Connector]模組和摘要端點'
description: 瞭解 [!DNL Adobe Commerce]的 [!DNL Adobe Commerce Optimizer Connector] 模組、目錄摘要API端點、批次限制和core_config_data設定路徑。
feature: Integration, Configuration
badgePaas: label="僅限PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案（Adobe管理的PaaS基礎結構）和內部部署專案的Adobe Commerce 。"
autotag-review: '2026-06-09T15:48:19.494Z'
TQID: 'https://experienceleague.adobe.com/UM6Y-xoQpUDzWpaMe1GRPp4XoAtHBLBsHw388kumN8g'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 19de20caafd45e3a00896d0d4b29b7e96dfe94e1
workflow-type: tm+mt
source-wordcount: 301
ht-degree: 1%

---

# Adobe Commerce Optimizer聯結器的聯結器模組和饋送端點

此參考列出儲存在`core_config_data`中的[!DNL Adobe Commerce Optimizer Connector]模組套件、支援的摘要API端點和組態金鑰路徑。 若要瞭解這些元件在同步處理期間如何共同運作，請參閱[聯結器同步處理管道](../connector-sync-pipeline.md)。

## 模組

聯結器包含多個Magento模組，這些模組會收集目錄資料、將摘要資料對應至[!DNL Commerce Optimizer] API支援的格式，以及管理提交和範圍控制。 下表摘要列出每個模組及其角色。

| 模組 | 角色 |
| ------ | ---- |
| `DataExporterAdapter` | 將[!DNL Adobe Commerce]摘要對應至[!DNL Adobe Commerce Optimizer] API所需的格式。 覆寫摘要集區和結構描述設定。 |
| `SaasExportAdapter` | 將[!DNL Commerce Optimizer]摘要路由傳送到內嵌API，並封鎖不支援的摘要以供提交。 |
| `CommerceAcoExporter` | 管理[!DNL Commerce Optimizer]認證並提供CLI安裝命令 |
| `CommerceAdapter` | [!DNL Commerce Optimizer] API相容性層（GraphQL、套件附加購物車、設定UI） |
| `PriceBookDataExporter` | 依網站和客戶群組編制索引的價格簿摘要 |
| `SaasPriceBook` | 價格簿提交的SaaS基礎結構 |
| `CommerceOptimizerScopeMapper` | 每個網站和每個商店檢視的同步啟用 |

## 支援的摘要

聯結器將多個摘要型別提交至[!DNL Commerce Optimizer] [[!DNL Catalog Data Ingestion API]](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/){target="_blank"}。 下表列出每個摘要及其在[!DNL Adobe Commerce]中的端點、批次限制、索引器名稱和摘要表格。

| 摘要 | [!DNL Commerce Optimizer] API端點 | 批次限制 | AC索引名稱 | 摘要表格 |
| ---- | ----------------------------------- | ----------- | ------------- | ---------- |
| `products` | `POST /v1/catalog/products` | 100 | `catalog_data_exporter_products` | `cde_products_feed` |
| `categories` | `POST /v1/catalog/categories` | 100 | `catalog_data_exporter_categories` | `cde_categories_feed` |
| `productAttributes` | `POST /v1/catalog/products/metadata` | 100 | `catalog_data_exporter_product_attributes` | `cde_product_attributes_feed` |
| `prices` | `POST /v1/catalog/products/prices` | 500 | `catalog_data_exporter_product_prices` | `cde_product_prices_feed` |
| `priceBooks` | `POST /v1/catalog/price-books` | 500 | `data_exporter_price_books` | `cde_price_books_feed` |

[!DNL SaaS Data Export]索引子收集的`products`、`productAttributes`、`categories`和`prices`摘要會重複使用資料。 聯結器從網站和客戶群組設定產生`priceBooks`摘要，且不依賴[!DNL SaaS Data Export]索引器。

如需每個摘要的欄位層級對應詳細資訊，請參閱 [!DNL Commerce Optimizer Connector] 摘要[&#128279;](field-mapping.md)的欄位對應。
若要根據您的目錄大小預估同步處理所需的時間，請參閱[預估資料量和同步處理時間](estimate-data-volume-sync-time.md)。

## 設定路徑

[!DNL Commerce Optimizer Connector]認證與服務URL儲存在`aco_exporter/general/`路徑首碼下的`core_config_data`中。 執行`bin/magento aco:config:show`以檢閱目前的值。 命令不顯示使用者端密碼。

```text
aco_exporter/general/org_id
aco_exporter/general/tenant_id
aco_exporter/general/client_id
aco_exporter/general/client_secret       (encrypted)
aco_exporter/general/type
aco_exporter/general/ingestion_url
aco_exporter/general/optimizer_studio_url
```
