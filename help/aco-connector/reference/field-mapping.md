---
title: ' [!DNL Adobe Commerce Optimizer Connector] 摘要的欄位對應'
description: 瞭解所有摘要的 [!DNL Adobe Commerce Optimizer Connector] 欄位從 [!DNL Adobe Commerce] 目錄資料對應到 [!DNL Adobe Commerce Optimizer] 擷取API格式。
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="僅限PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案（Adobe管理的PaaS基礎結構）和內部部署專案的Adobe Commerce 。"
autotag-review: '2026-06-09T15:49:03.934Z'
TQID: 'https://experienceleague.adobe.com/SOWOnguudhqzX-r66nGUqc-WKet5qq6GRV11ADx0Me4'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
  - id: c32adafa-ed01-4b31-997e-2413013911b0
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: b23e006f-0a29-4f1d-8fd0-77aa56f3d12b
source-git-commit: 1f901b4a72c10dc4e710742b98c03e88cbc8739f
workflow-type: tm+mt
source-wordcount: 465
ht-degree: 0%

---


# 聯結器摘要的欄位對應

此頁面記錄了[!DNL Adobe Commerce Optimizer Connector]如何將[!DNL Adobe Commerce]目錄欄位轉換為[!DNL Commerce Optimizer] [!DNL Catalog Data Ingestion API]所需的格式。 如需支援的摘要及其API端點的清單，請參閱[聯結器參考](connector-reference.md#supported-feeds)。

## 產品

| [!DNL Adobe Commerce]欄位 | [!DNL Commerce Optimizer] API欄位 | 附註 |
| ----------------------------------------------- | -------------- | ------- |
| `sku` | `sku` | |
| `storeViewCode` | `source/locale` | |
| `name` | `name` | |
| `urlKey` | `slug` | |
| `productId` | `externalIds[0].id` | `origin`已修正至`"AdobeCommerce"` |
| `status` | `status` | 大寫；針對未指定子項的複合產品，設定為`DISABLED` |
| `description` | `description` | |
| `shortDescription` | `shortDescription` | |
| `visibility` | `visibleIn` | 以逗號分隔的值已分割並對應： `Catalog`→`CATALOG`， `Search`→`SEARCH`；已捨棄未對應的值 |
| `metaTitle` | `metaTags/title` | |
| `metaDescription` | `metaTags/description` | |
| `metaKeyword` | `metaTags/keywords` | 以換行分隔的字串分割為陣列 |
| `inStock`, `lowStock`, `weight`, `weightUnit` | `attributes[].code = "aco_ac_attributes"` | JSON編碼物件`{inStock, lowStock, weight, weightType}`；一律顯示為第一個屬性專案 |
| `attributes[]` | `attributes[]` | 每個對應至`{code, values[], variantReferenceId}`；`inStock`、`lowStock`、`weight`、`weightType`的專案均已排除（它們會進入`aco_ac_attributes`） |
| `images[]` | `images[]` | `url`， `label`；標準角色對應： `image`→`BASE`， `small_image`→`SMALL`， `thumbnail`→`THUMBNAIL`， `swatch_image`→`SWATCH`；非標準角色移至`customRoles[]` |
| `categoryData[].categoryPath` | `routes[].path` | |
| `categoryData[].productPosition` | `routes[].position` | |
| `links[].type` + `links[].sku` | `links[]` | `type`個大寫；捨棄不含`sku`的專案 |
| `parents[].productType` + `parents[].sku` | `links[]` | 對應的型別： `configurable`→`VARIANT_OF`，`bundle`/`bundle_fixed`→`IN_BUNDLE` |
| `configurable options` | `configurations[]` | `id`→`attributeCode`，`label`；設定`swatchType`時選項型別`SWATCH`，否則`CONFIGURABLE`；來自`isDefault`的預設變體；值包括`variantReferenceId`，`label`，`colorHex`，`imageUrl` |
| `bundle options` | `bundles[]` | `label`→`group`；`required`；`renderType` `checkbox`/`multi`→`multiSelect: true`；來自`isDefault`的預設SKU；專案包括`sku`、`qty`、`userDefinedQty` (`qtyMutability`) |

## 產品屬性中繼資料

| [!DNL Adobe Commerce]欄位 | [!DNL Commerce Optimizer] API欄位 | 附註 |
| --------------- | -------------- | ------- |
| `attributeCode` | `code` | |
| `storeViewCode` | `source/locale` | |
| `label` | `label` | |
| `dataType` + `frontendInput` | `dataType` | 請參閱下方的轉換表格 |
| `visible` | `visibleIn: "PRODUCT_DETAIL"` | 在`true`時新增至陣列 |
| `visibleInSearch` | `visibleIn: "SEARCH_RESULTS"` | 在`true`時新增至陣列 |
| `visibleInListing` | `visibleIn: "PRODUCT_LISTING"` | 在`true`時新增至陣列 |
| `visibleInCompareList` | `visibleIn: "PRODUCT_COMPARE"` | 在`true`時新增至陣列 |
| `filterable` | `filterable` | |
| `sortable` | `sortable` | |
| `searchable` | `searchable` | |
| `searchWeight` | `searchWeight` | |
| `searchTypes` | `searchTypes` | |

**資料型別轉換：**

| [!DNL Adobe Commerce] `dataType` | [!DNL Adobe Commerce] `frontendInput` | [!DNL Commerce Optimizer] API `dataType` |
| -------------------- | -------------------------- | ------------------- |
| `int` | `boolean` | `BOOLEAN` |
| `int` | `text`或`select` | `TEXT` |
| `int` | 任何其他 | `INTEGER` |
| `decimal` | - | `DECIMAL` |
| `text`, `varchar`, `static`, `datetime` | - | `TEXT` |
| `OBJECT` | - | `OBJECT` |
| 任何其他 | - | `TEXT` |

## 價格簿

與其他聯結器摘要不同，[!DNL Adobe Commerce]中的[!DNL SaaS Data Export]索引器不會收集`priceBooks`摘要。 聯結器會從Admin的網站和客戶群組設定產生此摘要。

每個網站建立一個&#x200B;**基本價格簿**，加上每個網站 — 客戶群組配對一個&#x200B;**子價格簿**。

**價格簿識別碼公式：**

- **基準** （一般價格）： `priceBookId = websiteCode`
- **子項** （客戶群組或共用目錄）： `priceBookId = websiteCode::sha1(customerGroupId)`，其中`sha1(customerGroupId)`是客戶群組整數識別碼的SHA-1十六進位摘要

價格摘要在解析價格專案所屬的價格簿時，會使用相同的公式。 如需店面如何解析客戶工作階段的`priceBookId`，請參閱[無頭店面整合](../headless-storefront.md#graphql-commerceoptimizer-query)。

| 產生的欄位 | [!DNL Commerce Optimizer] API欄位 | 附註 |
| ---------------- | -------------- | ------- |
| `websiteCode`, `customerGroupId` | `priceBookId` | |
| 網站名稱 | `name` | 基本價格簿：網站名稱。 子項： `"Group Name (Website Name)"` |
| `websiteCode` | `parentId` | 僅出現在子價格簿上；指向基本價格簿 |
| 網站基本貨幣 | `currency` | 僅存在於基礎價格簿上；由子項繼承 |

## 價格

| [!DNL Adobe Commerce]欄位 | [!DNL Commerce Optimizer] API欄位 | 附註 |
| --------------- | -------------- | ------------------------------------------------------------------------------- |
| `sku` | `sku` | |
| `websiteCode`, `customerGroupId` | `priceBookId` | |
| `regular` | `regular` | |
| `discounts[]` | `discounts[]` | 折扣範例：特殊價格、型錄規則價格、共用型錄價格 |
| `tierPrices[]` | `tierPrices[]` | |

## 類別

含有空白`urlPath` （邏輯根類別）的專案會被略過，且永遠不會提交。

| [!DNL Adobe Commerce]欄位 | [!DNL Commerce Optimizer] API欄位 | 附註 |
| --------------- | -------------- | ------- |
| `storeViewCode` | `source/locale` | |
| `name` | `name` | |
| `urlPath` | `slug` | |
| `description` | `description` | |
| `metaTitle` | `metaTags/title` | |
| `metaDescription` | `metaTags/description` | |
| `metaKeywords` | `metaTags/keywords` | 以換行分隔的字串分割為陣列 |
| `image` | `images[].url` | 單一元素陣列； `roles: ["BASE"]` |
| `isActive` + `includeInMenu` | `families` | `["top_menu"]`若兩者皆為`true`，否則`[]` |

>[!MORELIKETHIS]
>
> - [使用資料擷取API擷取產品和價格資料](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/){target="_blank"} — 瞭解中繼資料、產品、類別、價格手冊和價格的目錄資料模型
> - [目錄資料擷取REST API參考](https://developer.adobe.com/commerce/services/reference/rest/){target="_blank"} — 檢閱每個摘要端點的要求與回應結構
> - [如何搭配 [!DNL Adobe Commerce]](../overview.md#how-the-connector-works-with-adobe-commerce)使用 [!DNL Commerce Optimizer Connector]  — 瞭解商店檢視、網站和客戶群組如何對應至目錄來源和價格簿
> - [在 [!DNL Commerce Optimizer]](/help/optimizer/setup/pricebooks.md)中的價格簿 — 管理聯結器匯出所建立的價格簿
> - [無頭店面整合](../headless-storefront.md#graphql-commerceoptimizer-query) — 解決客戶工作階段的`priceBookId`
