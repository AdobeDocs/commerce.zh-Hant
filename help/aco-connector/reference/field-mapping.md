---
title: '[!DNL Adobe Commerce Optimizer Connector]摘要的欄位對應'
description: 瞭解從[!DNL Adobe Commerce]目錄資料對應到所有摘要之[!DNL Adobe Commerce Optimizer]擷取API格式的[!DNL Adobe Commerce Optimizer Connector]欄位對應。
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="僅限PaaS" type="Informative" url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案（Adobe管理的PaaS基礎結構）和內部部署專案的Adobe Commerce 。"
autotag-review: '2026-06-09T15:49:03.934Z'
TQID: 'https://experienceleague.adobe.com/SOWOnguudhqzX-r66nGUqc-WKet5qq6GRV11ADx0Me4'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
  - id: b23e006f-0a29-4f1d-8fd0-77aa56f3d12b
    internal-label: Data modeling
source-git-commit: 1e34df4f07f9043675104fce55c58e0617463b33
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 2%
---

# 聯結器摘要的欄位對應

此頁面記錄了[!DNL Adobe Commerce Optimizer Connector]如何將[!DNL Adobe Commerce]目錄欄位轉換為[!DNL Commerce Optimizer] [!DNL Catalog Data Ingestion API]所需的格式。 如需支援的摘要及其API端點的清單，請參閱[聯結器參考](connector-reference.md#supported-feeds)。

## 產品

`products`摘要傳送資料至[產品端點](https://developer.adobe.com/commerce/services/reference/rest/#tag/Products){target="_blank"}。

| [!DNL Adobe Commerce]欄位 | [!DNL Commerce Optimizer] API欄位 | 對應詳細資料 |
| ----------------------------------------------- | -------------- | ------- |
| `sku` | `sku` | |
| `storeViewCode` | `source/locale` | |
| `name` | `name` | |
| `urlKey` | `slug` | |
| `productId` | `externalIds[0].id` | 將`origin`設為`"AdobeCommerce"` |
| `status` | `status` | 將狀態轉換為大寫。 如果狀態遺失，或如果可設定或組合產品沒有選項值，則使用`DISABLED`。 |
| `description` | `description` | 如果缺少說明，則使用空字串。 |
| `shortDescription` | `shortDescription` | 如果缺少簡短說明，則使用空字串。 |
| `visibility` | `visibleIn` | 分割逗號分隔值並將`Catalog`對應至`CATALOG`並將`Search`對應至`SEARCH`。 捨棄其他值。 |
| `metaTitle` | `metaTags/title` | |
| `metaDescription` | `metaTags/description` | |
| `metaKeyword` | `metaTags/keywords` | 將換行分隔的關鍵字分割成陣列，並修剪空白字元。 |
| `inStock`, `lowStock`, `weight`, `weightUnit` | `attributes[].code = "aco_ac_attributes"` | 一律新增`aco_ac_attributes`專案作為第一個屬性。 其JSON值包含`inStock`和`lowStock`做為字串。 當這些值可用時，它包含`weight`和`weightType`。 |
| `attributes[]` | `attributes[]` | 將每個專案對應至其屬性程式碼、字串值，以及相符的變數參考ID （可用時）。 略過`inStock`、`lowStock`、`categories`、`weight`和`weightType`。 與存貨相關的值包含在`aco_ac_attributes`中。 類別會匯出為路由。 |
| `images[]` | `images[]` | 略過沒有URL的影像。<br>匯出`url`、`label` （如果遺漏則為空白）和`sortOrder` （整數，預設為`0`）。<br>依`sortOrder`遞增順序排序影像。<br>對應標準角色：`image`到`BASE`、`small_image`到`SMALL`、`thumbnail`到`THUMBNAIL`和`swatch_image`到`SWATCH`。 將其他角色匯出為`customRoles[]`。 |
| `categoryData[].categoryPath` | `routes[].path` | 略過具有空白類別路徑的專案。 |
| `categoryData[].productPosition` | `routes[].position` | 如果缺少產品位置，則使用`0`。 |
| `links[].type` + `links[].sku` | `links[]` | `type`個大寫；捨棄不含`sku`的專案 |
| `parents[].productType` + `parents[].sku` | `links[]` | 將`configurable`對應至`VARIANT_OF`，並將`bundle`或`bundle_fixed`對應至`IN_BUNDLE`。 將其他產品型別轉換為大寫。 略過沒有SKU的父母。 |
| `configurable options` | `configurations[]` | 匯出具有ID和至少一個值的選項。<br>將`id`對應至`attributeCode`。 當`swatchType`存在時，將`type`設定為`SWATCH`，否則設定為`CONFIGURABLE`。<br>使用預設值的識別碼做為`defaultVariantReferenceId`。<br>將每個值對應到`variantReferenceId`、`label`、`colorHex`和`imageUrl`。 |
| `bundle options` | `bundles[]` | 匯出至少包含一個專案的選項。<br>使用選項標籤做為`group`，如果標籤是空的，則使用`Bundle group`。 將`required`複製到輸出。<br>將`checkbox`和`multi`轉譯器型別的`multiSelect`設為`true`。<br>列出`defaultItemSkus`中的預設SKU。 每個專案包含`sku`、`qty` （預設為`0`）和`userDefinedQty` （從`qtyMutability`，預設為`false`）。 |

## 產品屬性中繼資料

`productAttributes`摘要傳送資料至[中繼資料端點](https://developer.adobe.com/commerce/services/reference/rest/#tag/Metadata){target="_blank"}。

| [!DNL Adobe Commerce]欄位 | [!DNL Commerce Optimizer] API欄位 | 對應詳細資料 |
| --------------- | -------------- | ------- |
| `attributeCode` | `code` | |
| `storeViewCode` | `source/locale` | |
| `label` | `label` | |
| `dataType` + `frontendInput` | `dataType` | 請參閱下方的轉換表格 |
| `dataType`和`frontendInput` | `dataType` | 使用下列轉換規則。 |
| `visible`, `visibleInSearch`, `visibleInListing`, `visibleInCompareList` | `visibleIn[]` | 當旗標為`true`時，會將其對應的值加入： <br>`visible` → `PRODUCT_DETAIL`<br>`visibleInSearch` → `SEARCH_RESULTS`<br>`visibleInListing` → `PRODUCT_LISTING`<br>`visibleInCompareList` → `PRODUCT_COMPARE` |
| `filterable` | `filterable` | |
| `sortable` | `sortable` | |
| `searchable` | `searchable` | |
| `searchWeight` | `searchWeight` | |
| `searchTypes` | `searchTypes` | |

### 資料型別轉換

當`dataType`為`int`時，聯結器會檢查`frontendInput`。 對於其他資料型別，`frontendInput`不會影響轉換。

| 輸入`dataType` | 輸入`frontendInput` | 輸出`dataType` |
| ---------------- | --------------------- | ----------------- |
| `int` | `boolean` | `BOOLEAN` |
| `int` | `text`或`select` | `TEXT` |
| `int` | 任何其他值，包括缺少的值 | `INTEGER` |
| `decimal` | 未使用 | `DECIMAL` |
| `text`, `varchar`, `static`, `datetime` | 未使用 | `TEXT` |
| `OBJECT` | 未使用 | `OBJECT` |
| 任何其他值 | 未使用 | `TEXT` |

>[!NOTE]
>
>當屬性使用`OBJECT`資料型別時，[Products API](https://developer.adobe.com/commerce/services/reference/graphql/#products){target="_blank"}會嘗試將其儲存的值剖析為JSON。 如果剖析成功，API會傳回值作為巢狀物件。 針對無法以單一值表示的結構化屬性資料，請使用`OBJECT`。 如需指示，請參閱[動態新增產品屬性](../../data-export/add-attribute-dynamically.md)。

## 價格簿

`priceBooks`摘要傳送資料至[價格簿端點](https://developer.adobe.com/commerce/services/reference/rest/#tag/Price-Books){target="_blank"}。

與其他聯結器摘要不同，[!DNL Adobe Commerce]中的[!DNL SaaS Data Export]索引器不會收集`priceBooks`摘要。 聯結器會從Admin的網站和客戶群組設定產生此摘要。

聯結器會針對每個網站，為每個客戶群組建立一個基本價格簿和一個子價格簿。

對`priceBookId`使用這些公式：

- 一般價格的基準價格簿： `priceBookId = websiteCode`。
- 客戶群組的子價格簿： `priceBookId = websiteCode::sha1(customerGroupId)`，其中`sha1(customerGroupId)`是客戶群組的整數ID的SHA-1十六進位摘要。

價格摘要會使用相同的公式，將每個價格專案指定至價格簿。 如需店面如何針對客戶工作階段解析`priceBookId`的相關資訊，請參閱[無頭店面整合](../headless-storefront.md#graphql-commerceoptimizer-query)。


| Source欄位或值 | [!DNL Commerce Optimizer] API欄位 | 對應詳細資料 |
| ---------------- | -------------- | ------- |
| `websiteCode` | `parentId` | 將此欄位新增至子價格簿。 其值可識別基本價格簿。 |
| 網站名稱 | `name` | 使用基本價格簿的網站名稱。 對子價格簿使用`Customer group name (Website name)`。 |
| `websiteCode` | `parentId` | 僅出現在子價格簿上；指向基本價格簿 |
| 網站基本貨幣 | `currency` | 僅包含基本價格簿的此欄位。 兒童價格簿會省略它。 |

## 價格

`prices`摘要傳送[!DNL Adobe Commerce]資料至[價格端點](https://developer.adobe.com/commerce/services/reference/rest/#tag/Prices){target="_blank"}。

| 摘要輸入欄位 | [!DNL Commerce Optimizer] API欄位 | 對應詳細資料 |
| --------------- | -------------- | ------------------------------------------------------------------------------- |
| `sku` | `sku` | 以未變更的方式傳遞SKU。 |
| `websiteCode`, `customerGroupCode` | `priceBookId` | 將`websiteCode`與`customerGroupCode`中客戶群組識別碼的SHA-1雜湊結合。 如果`customerGroupCode`是`0`，則會單獨使用`websiteCode`。 |
| `regular` | `regular` | 以不變的價格傳遞一般價格。 |
| `discounts[]` | `discounts[]` | 如果來源值為`null`，會匯出空白陣列。<br>若專案的`code`設為`special_price`且`percentage`，當值介於`0`與`100`之間時，將`percentage`設為`100 - percentage`。 設定為`0` （位於或超出該範圍）。<br>將其他專案（包括價格特別價格）通過未變更。 |
| `tierPrices[]` | `tierPrices[]` | 如果來源值遺失或`null`，則使用空白陣列。 |

## 類別

`categories`摘要傳送[!DNL Adobe Commerce]資料至[類別端點](https://developer.adobe.com/commerce/services/reference/rest/#tag/Categories){target="_blank"}。

含有空白`urlPath` （邏輯根類別）的專案會被略過，且永遠不會提交。

| [!DNL Adobe Commerce]欄位 | [!DNL Commerce Optimizer] API欄位 | 對應詳細資料 |
| --------------- | -------------- | ------- |
| `storeViewCode` | `source/locale` | |
| `name` | `name` | |
| `urlPath` | `slug` | |
| `description` | `description` | |
| `position` | `position` | 匯出出現時的類別位置。 缺少欄位時省略該欄位。 |
| `metaTitle` | `metaTags/title` | |
| `metaDescription` | `metaTags/description` | |
| `metaKeywords` | `metaTags/keywords` | 以換行分隔的字串分割為陣列 |
| `image` | `images[].url` | 單一元素陣列； `roles: ["BASE"]` |
| `isActive` + `includeInMenu` | `families` | `["top_menu"]`若兩者皆為`true`，否則`[]` |

| `metaKeywords` | `metaTags/keywords` |將換行分隔的關鍵字分割成陣列，並修剪空白字元。 |
| `image` | `images[].url` |當`image`存在時，會匯出具有`BASE`角色的一個影像。 當影像空白或遺失時，匯出空白陣列。 |
| `isActive` + `includeInMenu` | `families` |只有在兩個值都是`true`時才新增`top_menu`。 否則，會匯出空白陣列。 |
| `attributes[]` | `attributes[]` |將具有非空白`attributeCode`的專案匯出為`{code, values[]}`。 將值轉換為字串。 不存在符合條件的專案時，省略`attributes`。 |

>[!MORELIKETHIS]
>
> - [使用資料擷取API擷取產品和價格資料](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/){target="_blank"} — 瞭解中繼資料、產品、類別、價格手冊和價格的目錄資料模型
> - [目錄資料擷取REST API參考](https://developer.adobe.com/commerce/services/reference/rest/){target="_blank"} — 檢閱每個摘要端點的要求與回應結構
> - [如何搭配 [!DNL Adobe Commerce]](../overview.md#how-the-connector-works-with-adobe-commerce)使用 [!DNL Commerce Optimizer Connector]  — 瞭解商店檢視、網站和客戶群組如何對應至目錄來源和價格簿
> - [在 [!DNL Commerce Optimizer]](/help/optimizer/setup/pricebooks.md)中的價格簿 — 管理聯結器匯出所建立的價格簿
> - [無頭店面整合](../headless-storefront.md#graphql-commerceoptimizer-query) — 解決客戶工作階段的`priceBookId`
