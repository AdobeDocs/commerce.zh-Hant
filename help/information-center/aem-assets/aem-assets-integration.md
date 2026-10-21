---
title: 適用於Commerce的AEM Assets整合
description: 瞭解如何將AEM Assets與Adobe Commerce、Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer整合，以集中管理產品影像和媒體。
role: Admin, Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T01:34:13.564Z'
TQID: 'https://experienceleague.adobe.com/v15DE37DoqpstrsWqnwd6DYpa5moT-BhQ80zDq2KP6I'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: ef0c45ae-6bee-4821-a65e-e1e118e8a01c
    internal-label: Commerce Optimizer
feature_v2:
  - id: 00451af3-7b97-5414-9992-3a6c269e413f
    internal-label: Paas
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 4%
---

# Commerce的AEM Assets整合

AEM Assets整合可啟用Adobe Commerce中的產品視覺效果功能，因此您可以在AEM Assets中集中管理產品影像、影片和其他媒體。 這是選用的附加元件，可與任何Commerce架構選項搭配使用，而非獨立的Commerce平台。

## 各架構的整合路徑

有兩個整合路徑。 路徑取決於您的Commerce架構。

| Commerce架構 | AEM Assets整合路徑 | 了解更多 |
| --- | --- | --- |
| 雲端或內部部署上的[!DNL Adobe Commerce] | Commerce的[!DNL AEM Assets]整合。 使用Commerce整合套件同步處理及管理[!DNL Adobe Commerce]與[!DNL AEM Assets]之間的產品影像、影片和其他媒體。 | 適用於Commerce的[AEM Assets整合](/help/aem-assets-integration/overview.md) |
| [!DNL Adobe Commerce as a Cloud Service] | 由[!DNL AEM Assets]提供支援的[!DNL Product Visuals] | [AEM Assets整合設定](/help/aem-assets-integration/overview.md#next-steps) |
| 獨立[!DNL Adobe Commerce Optimizer] | [!DNL Product Visuals]由[!DNL AEM Assets]提供。 基本目錄和價格資料會透過[最佳化程式資料擷取API](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/)送達。 | [使用AEM Assets的產品視覺效果](/help/optimizer/setup/product-visuals.md) |
| 具有[!DNL Adobe Commerce Optimizer Connector]的[!DNL Adobe Commerce] | [!DNL Product Visuals]由[!DNL AEM Assets]提供。 目錄和價格資料會由聯結器從[!DNL Adobe Commerce]同步處理。 | [Commerce Optimizer整合](/help/optimizer/integrations/integrations-overview.md) |

[!DNL Product Visuals]是Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer的整合路徑。 它會將AEM管理的產品影像同步到Commerce目錄層，並透過店面API將其提供給店面體驗。

## 選擇之前

- 雲端或內部部署路徑上的Commerce與Commerce as a Cloud Service或Adobe Optimizer [!DNL Product Visuals]路徑之間的設定和授權需求不同。 請先檢閱部署特定需求。
- [!DNL AEM Assets]管理數位資產。 它不會取代Commerce目錄、定價、購物車、結帳或訂購系統。
- 產品資產會使用SKU或其他記載的相符中繼資料來比對Commerce產品。
- 如果行銷和銷售團隊需要集中化的產品影像和資產工作流程，請選擇符合您Commerce架構的路徑。

## 相關資訊

- [Adobe Experience Manager Assets檔案](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/assets/overview)
- [架構概覽](../architecture-options/overview.md)
- [API](../apis/commerce-apis.md)
