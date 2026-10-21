---
title: 店面
description: 瞭解Adobe Commerce店面選項，包括由Edge Delivery Services支援的Commerce店面和自訂Headless實作。
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T01:12:22.967Z'
TQID: 'https://experienceleague.adobe.com/1mQm2s3UGzr7S4j9RMZAaRoUVtzu93N1IFbOypR8vkA'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
feature_v2:
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
subfeature_v2:
  - id: e396cff5-f586-484c-89f0-7f1da3308f92
    internal-label: GraphQL
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%
---

# 店面

店面與Commerce後端和API層分開。 根據選取的架構，店面可透過API Mesh、App Builder或其他整合機制，從Commerce Foundation API、Storefront Services API、[!DNL Adobe Commerce Optimizer] Merchandising Services API或連線系統擷取資料。 請參閱[架構選項](../architecture-options/overview.md)，瞭解每個店面如何與Commerce後端配對。

## 由Edge Delivery Services提供支援的Commerce店面

由[!DNL Edge Delivery Services]提供支援的Commerce店面是以Adobe Commerce展示板上建置的面向客戶的店面選項，使用插入式元件和內容區塊。 它與[架構概觀](../architecture-options/overview.md)的任一專案相容，可依據後端連線到Commerce Foundation、Storefront Services或[!DNL Adobe Commerce Optimizer]銷售服務。 檢視[Adobe Commerce店面總覽](https://experienceleague.adobe.com/en/tools/commerce-storefront/)。

## 店面服務

[!DNL Storefront Services]是搭配[!DNL Adobe Commerce]使用的店面導向服務。 服務API可提供對以下功能的最佳化存取：

- [!DNL Catalog Service]
- [!DNL Live Search]
- [!DNL Product Recommendations]

雲端或內部部署（設定時）上的[!DNL Adobe Commerce]和[!DNL Adobe Commerce as a Cloud Service]都使用Storefront服務。 它們不是[!DNL Adobe Commerce as a Cloud Service]的專屬專案，不應該做為兩個[!DNL Adobe Commerce]平台選項之間的識別標籤。 請參閱[Storefront Services GraphQL結構描述](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/)。

## 自訂Headless店面

依據Commerce店面以外的[!DNL Edge Delivery Services]支援的店面選項包括[!DNL Luma]、[!DNL PWA Studio]或自訂Headless店面（視平台支援和實施需求而定）。 自訂Headless店面會根據選取的[架構選項](../architecture-options/overview.md)連線到與任何其他店面選項相同的API系列 — Commerce Foundation、Storefront Services或Commerce Optimizer Merchandising Services。

## 購物車與結帳整合

處理購物車和結帳交易的位置取決於Commerce後端，而不是店面技術：

- 當[!DNL Adobe Commerce] Commerce Foundation是後端時，店面會使用Commerce Foundation API進行購物車、結帳、客戶和訂單作業，以及設定的付款、稅捐、送貨和履行整合。
- 當協力廠商商務平台作為後端（如同獨立[!DNL Adobe Commerce Optimizer]）時，店面會透過API Mesh、App Builder或直接整合連線至該平台的購物車、結帳、客戶、訂單、付款、稅務、送貨和履行服務。

## 相關指引

- [架構概覽](../architecture-options/overview.md)
- [API](../apis/commerce-apis.md)
