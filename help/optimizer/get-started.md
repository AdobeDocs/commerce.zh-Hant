---
title: 開始使用 [!DNL Adobe Commerce Optimizer]
description: 瞭解如何開始使用 [!DNL Adobe Commerce Optimizer]。
hide: true
recommendations: noCatalog
exl-id: de57d93d-e156-45c1-86aa-de29a8c34bd2
source-git-commit: 9c3f5d1d5e7fd57d2306502d654a854bc5c66c71
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---

# 開始使用

>[!NOTE]
>
>本檔案說明提早存取開發中的產品，並未反映所有可供一般使用的功能。

本指南會逐步引導您建立及使用[!DNL Adobe Commerce Optimizer]執行個體。

<!--Click the tabs below to see high-level workflow overviews for the following user types:

- Administrators
- Merchants
- Developers

>[!BEGINTABS]

>[!TAB Administrator and merchant workflow]

This diagram provides a high-level overview of how administrators and merchants access and manage [!DNL Adobe Commerce Optimizer] instances. See the [Adobe Admin Console Guide](https://helpx.adobe.com/tw/enterprise/admin-guide.html) for more information about administrator workflows.

NEED DIAGRAM

>[!TAB Developer workflow]

This diagram provides a high-level overview of how developers create integrations for [!DNL Adobe Commerce Optimizer] using App Builder. See the [API documentation](https://developer.adobe.com/commerce/webapi/rest/) for more information.

NEED DIAGRAM

>[!ENDTABS]
-->

## 布建

在[!DNL Adobe Commerce Optimizer]執行個體準備就緒後，[!DNL Adobe Commerce Optimizer]布建團隊會提供您下列端點：

| 專案 | 範例URL | 用途 |
|---|---|---|
| [!DNL Adobe Commerce Optimizer] UI | `https://experience.adobe.com/#/@commerceprojectbeacon/commerce-optimizer-studio?tenant=<tenantId>` | 存取Commerce Optimizer UI以跨下列專案管理您的目錄： <br>1。 銷售規則（產品探索、產品推薦）。<br>2。 目錄管理（頻道和原則建立）。<br>3。 資料深入分析（檢視您的目錄資料擷取狀態）。 |
| 店面API | `https://na1-sandbox.api.commerce.adobe.com/<tenantId>/graphql` | 存取設定Edge Delivery Services支援的Commerce店面所需的API。 |
| 目錄資料擷取API | `https://na1-sandbox.api.commerce.adobe.com/<tenantId>/v1/catalog/<entity>` | 存取內嵌目錄資料所需的API。 |

>[!NOTE]
>
>請參閱[開發人員檔案](https://developer-stage.adobe.com/commerce/services/composable-catalog/)，深入瞭解店面設定和目錄擷取所需的API。

身為搶先體驗參與者，您將收到一封包含安全連結的電子郵件，連同您的IMS權杖，可讓您登入[!DNL Adobe Commerce Optimizer]或進行API呼叫。

## 設定店面

現在您已擁有[!DNL Adobe Commerce Optimizer]執行個體，您已準備好繼續[設定](./storefront.md)您的Commerce店面(由Edge Delivery Services提供技術支援)。

## 可供早期存取參與者使用的目錄資料

作為早期存取參與者，[!DNL Adobe Commerce Optimizer]執行個體包含以[Carvelo使用案例](./use-case/admin-use-case.md)為基礎的模擬目錄資料。 模擬資料以及一些預先設定的管道和原則，可協助您熟悉[!DNL Adobe Commerce Optimizer] UI。

<!--Ingest catalog data

By default, [!DNL Adobe Commerce Optimizer] instances do not include any product data.

See the [Ingestion API](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/using-the-api/) documentation to learn how you can import your catalog data into [!DNL Adobe Commerce Optimizer].

The catalog data that you ingest is visible in the [data insights](./insights-overview.md) page. Additionally, you can use the [Catalog](./catalog-overview.md) page to define the channels and policies.-->
