---
title: COMMERCE API
description: 比較Adobe Commerce API系列，包括Commerce Foundation、Storefront Services、Commerce Optimizer Merchandising Services和Data Ingestion。
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T01:36:11.529Z'
TQID: 'https://experienceleague.adobe.com/JBpnpCy9QITdcYtKnL2btd9grmgIk1prYaCNasgWkok'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: ef0c45ae-6bee-4821-a65e-e1e118e8a01c
    internal-label: Commerce Optimizer
feature_v2:
  - id: 22bad240-8308-569b-a9d5-578f1ff890ca
    internal-label: Customers
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 72863f3c-9d27-5dda-afe1-d9f934b1fba0
    internal-label: Extensibility
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: c4f010fa-1478-4300-a88d-706fbc036a7a
    internal-label: APIs and SDKs
subfeature_v2:
  - id: e396cff5-f586-484c-89f0-7f1da3308f92
    internal-label: GraphQL
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: da3860b0-d637-47df-bef0-273751180266
    internal-label: Digital asset management
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%
---

# API

| API系列 | 主要用途 | 使用者 |
| --- | --- | --- |
| **Commerce Foundation GraphQL API** | 核心商務和交易式功能，例如，目錄操作、購物車、結帳、客戶和訂單 | 雲端上的[!DNL Adobe Commerce]、內部部署上的[!DNL Adobe Commerce]以及[!DNL Adobe Commerce as a Cloud Service] |
| **Storefront Services GraphQL API** | 透過[!DNL Catalog Service]、[!DNL Live Search]和[!DNL Product Recommendations]以店面為導向的目錄、搜尋和建議體驗 | 雲端或內部部署上的[!DNL Adobe Commerce]已設定服務，以及[!DNL Adobe Commerce as a Cloud Service] |
| **Commerce Optimizer銷售服務GraphQL API** | 擷取Optimizer管理的目錄、目錄檢視、價格內容、搜尋、建議和銷售結果 | 在雲端或內部部署使用Optimizer Connector的[!DNL Adobe Commerce]，以及獨立式[!DNL Adobe Commerce Optimizer] |
| **Commerce Optimizer Data Ingestion REST API** | 將目錄和價格資料新增至獨立的[!DNL Adobe Commerce Optimizer]實作 | 獨立[!DNL Adobe Commerce Optimizer]已連線至外部資料來源 |

## Commerce Foundation GraphQL API

包括目錄、購物車、結帳、客戶和訂單在內的核心商務功能。 由[!DNL Adobe Commerce]在雲端、[!DNL Adobe Commerce]在內部部署和[!DNL Adobe Commerce as a Cloud Service]使用。 檢視[Commerce GraphQL API](https://developer.adobe.com/commerce/webapi/graphql/)。

## Storefront Services GraphQL API

透過[!DNL Catalog Service]、[!DNL Live Search]和[!DNL Product Recommendations]以店面為導向的目錄、搜尋和建議體驗。 由[!DNL Adobe Commerce]在雲端、內部部署和[!DNL Adobe Commerce as a Cloud Service]上使用。 請參閱[Storefront Services GraphQL結構描述](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/)。

## Commerce Optimizer銷售服務GraphQL API

擷取Optimizer管理的目錄、目錄檢視、價格內容、搜尋、建議和銷售結果。 由[!DNL Adobe Commerce]在雲端、具有[!DNL Adobe Commerce Optimizer Connector]的內部部署和獨立[!DNL Adobe Commerce Optimizer]上使用。 請參閱[Commerce Optimizer銷售服務](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/)。

## Commerce Optimizer資料擷取REST API

從外部資料來源將目錄和價格資料新增至獨立的[!DNL Adobe Commerce Optimizer]實作。 請參閱[Commerce Optimizer資料擷取](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/)。

## Commerce Optimizer整合

[!DNL Adobe Commerce Optimizer]透過數個整合路徑連線至其他系統，這取決於它是與[!DNL Adobe Commerce]配對還是與協力廠商後端配對。

### Adobe Commerce Optimizer聯結器

將雲端或內部部署上[!DNL Adobe Commerce]的目錄和價格資料同步到[!DNL Adobe Commerce Optimizer]，保留[!DNL Adobe Commerce]做為交易系統，而Optimizer提供探索和銷售。 請參閱[Commerce Optimizer整合](/help/optimizer/integrations/integrations-overview.md)。

### 協力廠商商務整合

透過資料擷取REST API，將來自協力廠商商務平台、PIM、ERP或其他來源的目錄和價格資料擷取至獨立[!DNL Adobe Commerce Optimizer]，而協力廠商平台則維持交易記錄系統。

### API Mesh和App Builder

使用API Mesh以協調具有私人或第三方API的Adobe Commerce API。 使用Adobe Developer App Builder建置自訂應用程式和整合。 如需相關的Commerce擴充性指引，請參閱[API網格](https://developer.adobe.com/graphql-mesh-gateway/)和[Adobe Commerce擴充性](https://developer.adobe.com/commerce/extensibility/)。

如需具體說明的事件導向整合，請參閱[適用於Adobe Commerce的Adobe I/O Events](https://experienceleague.adobe.com/zh-hant/docs/commerce-learn/tutorials/extensibility/adobe-developer-app-builder/io-events/getting-started-io-events)。


### 購物車和結帳移交

對於具有外部後端的獨立[!DNL Adobe Commerce Optimizer]，店面會使用Merchandising Services GraphQL API提供產品體驗，然後透過API Mesh、App Builder或直接整合，將購物車、結帳、客戶、訂單、付款、稅務、送貨和履行作業交到後端。

### AEM Assets

AEM Assets是選用的跨領域數位資產管理整合，可新增到任何Commerce或Optimizer架構，而不是其自己的獨立整合路徑。 請參閱[Commerce的AEM Assets整合](../aem-assets/aem-assets-integration.md)。

## 相關指引

- [架構概覽](../architecture-options/overview.md)
- [店面](../storefronts/overview.md)
- [Commerce的AEM Assets整合](../aem-assets/aem-assets-integration.md)
