---
title: 建立新店面
description: 瞭解如何使用Edge Delivery Services、Adobe Commerce下拉式元件以及內容區塊和範本，規劃和建立新的Commerce店面。
role: Developer, Leader
feature: Storefront
recommendations: noCatalog
autotag-review: '2026-10-20T10:58:53.700Z'
TQID: 'https://experienceleague.adobe.com/z-PCoaJzaOyd7SlxjyWs-0tEVo3hpdHucdgq4cZSeQw'
product_v2:
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%
---

# 建立新店面

具有以下部署型別的Adobe Commerce客戶可以使用Edge Delivery Services、Commerce下拉式元件和內容區塊來建立新店面。

- Adobe Commerce as a Cloud Service
- Adobe Commerce Optimizer
- 雲端上的Adobe Commerce或使用不含Adobe Commerce Optimizer的Storefront Services的內部部署
- 使用Adobe Commerce Optimizer Connector的雲端或內部部署上的Adobe Commerce

使用Adobe Commerce範本提供可自訂並連線至您自己的Adobe Commerce或[!DNL Adobe Commerce Optimizer]執行個體的有效店面。

>[!NOTE]
>
>對於雲端基礎結構或內部部署的Adobe Commerce，透過聯結器採用Adobe Commerce Optimizer是一個店面現代化選項，並非必要條件。 如果您選擇此路徑，請使用[Luma Bridge](https://experienceleague.adobe.com/en/tools/commerce-storefront/setup/discovery/luma-bridge/)將您的Luma店面與Edge Delivery Services店面連線。

## 快速入門

1. 請檢閱[Adobe Commerce店面總覽](https://experienceleague.adobe.com/en/tools/commerce-storefront/merchants/quick-start/create-content/)和[店面架構](https://experienceleague.adobe.com/en/tools/commerce-storefront/get-started/architecture/)檔案，瞭解架構和可用的插入式元件。

1. 若要設定店面，請遵循店面檔案：

   - [建立店面](https://experienceleague.adobe.com/en/tools/commerce-storefront/get-started/create-storefront/)
   - [Storefront開發人員指南](https://experienceleague.adobe.com/en/tools/commerce-storefront/get-started/)以範圍、設定和啟動專案。

1. 將店面連線至您的Commerce後端。

   根據您的部署模式遵循指示。 如需詳細資訊，請參閱&#x200B;_店面開發人員指南_&#x200B;中的[後端選項](https://experienceleague.adobe.com/en/tools/commerce-storefront/get-started/backends/){target="_blank"}。

## 相關指引

- [Adobe Commerce店面總覽](https://experienceleague.adobe.com/en/tools/commerce-storefront/merchants/quick-start/create-content/)
- [啟用Adobe Commerce Optimizer](enable-aco.md)
- [Adobe Commerce Optimizer聯結器](../../aco-connector/overview.md)
- [連線AEM Assets](connect-aem-assets.md)
- [店面後端選項](https://experienceleague.adobe.com/en/tools/commerce-storefront/get-started/backends/){target="_blank"}
