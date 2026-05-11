---
title: '[!DNL Retrieve catalog data with GraphQL]'
description: 使用GraphQL查詢來擷取目錄資料，以支援Commerce體驗。
role: Admin, Developer
feature: Services, API Mesh, Catalog Service
exl-id: 49bbdb3b-bbe9-4777-8ea7-3bd25ae53889
TQID: https://experienceleague.adobe.com/ahutwotbB6Dxg7Tc3WMFd7S-WBMALvOYIUTmB5JKmyM
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 268
ht-degree: 0%

---

# 使用GraphQL擷取目錄資料 {#graphql-queries}

使用GraphQL查詢從Adobe Commerce目錄SaaS資料空間擷取產品、價格和其他資料，並使用它比原生Commerce GraphQL查詢更快地呈現Adobe Commerce體驗。

{{aco-merchandising-services}}

目錄服務提供下列查詢：

| 查詢 | 說明 | 使用情況 |
|-------|-------------|-------|
| `categories` | 傳回類別資料。 如果指定了子樹狀結構輸入物件，查詢會傳回有關子類別的詳細資訊。 | 對於呈現店面導覽和類別頁面很有用。 [檢視範例。](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) |
| `products` | 傳回指定為輸入之SKU的詳細資訊。 | 主要用於呈現產品詳細資料和產品比較頁面上的內容。 [檢視範例。](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) |
| `productSearch` | 傳回符合搜尋條件的產品清單。 | 用於根據搜尋輸入呈現搜尋結果和產品清單頁面。 [檢視範例。](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/) |
| `refineProduct` | 縮小針對複雜產品執行的產品查詢結果，以傳回有關產品變體的特定資訊。 | 當購物者選取產品選項時，對於呈現更新的產品詳細資料頁面非常有用。 [檢視範例。](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/) |
| `variants` | 傳回產品所有變體的詳細資訊。 | 對於在產品詳細資料或清單頁面上顯示變體影像而不提交多個API請求很有用。 [檢視範例。](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/product-variants/) |

如需使用這些查詢的詳細資訊，請參閱[Storefront Services GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/)。
