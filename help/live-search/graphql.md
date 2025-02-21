---
title: GraphQL
description: ' [!DNL Live Search] GraphQL工作區可讓您使用您的即時資料建立查詢。'
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '39'
ht-degree: 0%

---

# GraphQL

*GraphQL*&#x200B;工作區可讓管理員使用自己的資料建置和測試GraphQL查詢。

此工作區支援[`productSearch`](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/)和[`attributeMetadata`](https://developer.adobe.com/commerce/services/graphql/live-search/attribute-metadata/)查詢。

![GraphQL工作區](assets/graphql.png)

```graphql
query productSearch {
  productSearch(phrase: "a306") {
    total_count
    items {
      product {
        sku
		name
      }
    }
    facets {
      title
    }
  }
}
```

變數：

```json
{
  "Magento-Environment-Id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
  "Magento-Website-Code": "base",
  "Magento-Store-Code": "base",
  "Magento-Store-View-Code": "default",
  "X-Api-Key": "search_gql"
}
```

