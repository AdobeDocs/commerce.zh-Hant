---
title: 更新現有店面
description: 瞭解如何計畫從舊版Adobe Commerce店面到以Edge Delivery Services和下拉式元件為基礎的店面的漸進式遷移。
role: Developer, Leader
feature: Storefront
recommendations: noCatalog
autotag-review: '2026-10-20T11:09:14.812Z'
TQID: 'https://experienceleague.adobe.com/1OR7uwncjLw-NpwMMuwKjDjpASdh74sfu6s5rNClqxg'
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
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%
---

# 更新現有的店面

您可以逐步移轉舊版店面至Edge Delivery Services和Commerce下拉式元件，而非一次重建所有專案。

>[!NOTE]
>
>本指南適用於雲端基礎結構上的Adobe Commerce as a Cloud Service、Adobe Commerce，或使用店面服務或Adobe Commerce Optimizer Connector的內部部署。 也適用於具有現有或協力廠商後端的獨立Adobe Commerce Optimizer。 若要確認哪個選項適用於您的專案，請參閱[實作架構選項](../architecture-options/implementation-architectures.md)。

## 快速入門

1. 若要瞭解在Edge Delivery Services上建立的店面與您目前實作的比較，請檢閱[Adobe Commerce店面總覽](https://experienceleague.adobe.com/en/tools/commerce-storefront/)。

1. 使用[Storefront Developer Guide](https://experienceleague.adobe.com/en/tools/commerce-storefront/get-started/)來設定先移轉哪些頁面或流程的範圍。

1. 若為Adobe Commerce as a Cloud Service，請保留您現有的Commerce服務連線([!DNL Catalog Service]、[!DNL Live Search]、[!DNL Product Recommendations]、[!DNL Payment Services]) — 請參閱[設定Commerce服務](set-up-commerce-services.md)。

## 相關指引

- [建立新店面](build-new-storefront.md)
- [架構選項](../architecture-options/overview.md)
