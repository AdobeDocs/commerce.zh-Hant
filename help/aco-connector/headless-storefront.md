---
title: '[!DNL Adobe Commerce Optimizer Connector] Headless店面整合'
description: 瞭解如何將Headless店面與 [!DNL Adobe Commerce Optimizer Connector] GraphQL API、價格手冊ID和套件組合加到購物車編碼整合。
feature: Storefront, Integration, GraphQL
badgePaas: label="僅限PaaS" type="Informative" url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案（Adobe管理的PaaS基礎結構）和內部部署專案的Adobe Commerce 。"
autotag-review: '2026-06-09T16:27:30.102Z'
TQID: 'https://experienceleague.adobe.com/Orif1rROglTQ-3ZkRj5LMF90Y-AdpfTnOgPmJXQjYgc'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: c32adafa-ed01-4b31-997e-2413013911b0
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: d378ca77-2da1-4f39-ad92-1917fe974a38
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 237
ht-degree: 0%

---

# Headless店面整合

`CommerceAdapter`模組延伸[!DNL Adobe Commerce]以橋接Headless店面與[!DNL Adobe Commerce Optimizer]之間的間隙。 它提供GraphQL查詢來解析客戶價格簿內容，並強制執行[!DNL Adobe Commerce Optimizer] GraphQL API預期的套件組合產品編碼。

如需高階店面設定指示，請參閱[!DNL Adobe Commerce Optimizer Connector]概觀中的[設定銷售與店面](./overview.md#merchandising-storefronts)。

## GraphQL： `commerceOptimizer`查詢 {#graphql-commerceoptimizer-query}

Headless店面呼叫`commerceOptimizer` GraphQL查詢以擷取目前客戶工作階段的`priceBookId`。 擷取價格時將此值傳遞至[[!DNL Adobe Commerce Optimizer] GraphQL API](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api){target="_blank"}。

```graphql
{
  commerceOptimizer {
    priceBookId
  }
}
```

範例回應：

```json
{
  "data": {
    "commerceOptimizer": {
      "priceBookId": "base::a94a8fe5ccb19ba61c4c0873d391e987982fbbd3"
    }
  }
}
```

如何解析`priceBookId`：

| 工作階段狀態 | `priceBookId` |
|-----------------------|---------------------------------------------------------------------|
| 來賓（未登入） | `websiteCode::sha1(0)`，其中`0`是訪客客戶群組ID |
| 已登入的客戶 | `websiteCode::sha1(customerGroupId)` |

`Store`要求標頭會決定網站範圍，因此會決定`websiteCode`元件。 `sha1(customerGroupId)`元件符合資料同步處理期間使用的價格簿識別碼公式。 請參閱[價格手冊](reference/field-mapping.md#price-books)。

## 套件組合產品：加入購物車格式 {#bundle-products-add-to-cart-format}

允許購物者將捆綁產品從Headless店面新增到購物車，每個選取的捆綁選項只有`SKU`和`qty`。

每個選取或輸入的選項值都必須以下列格式進行base64編碼：

```text
base64("bundle_item/" + JSON.stringify({"sku": "<child_sku>", "qty": "<qty>"}))
```

所有選項中相同的子SKU可能只會出現一次。

範例([!DNL JavaScript])：

```javascript
const encodedOption = btoa(
  'bundle_item/' + JSON.stringify({ sku: 'child-product-sku', qty: '1' })
);
```
