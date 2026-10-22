---
title: 設定Commerce服務
description: 瞭解如何使用Adobe Commerce服務聯結器將Commerce連線到銷售服務，以及將Magento Open Source連線到付款服務。
role: Admin, Developer
feature: Integration, Configuration
recommendations: noCatalog
autotag-review: '2026-10-20T11:14:04.410Z'
TQID: 'https://experienceleague.adobe.com/yyUDw1y5CYHxdLlC3bNo0DKK0byamPAKUjK-wwxVEX4'
product_v2:
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
subfeature_v2:
  - id: a1d22079-48b9-5e69-9ee6-eb236068ef34
    internal-label: Search
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%
---

# 設定Commerce服務

雲端基礎結構上的Adobe Commerce和內部部署專案會透過Commerce Services Connector連線到[!DNL Catalog Service]、[!DNL Live Search]、[!DNL Product Recommendations]和[!DNL Payment Services]之類的服務。 在[!DNL Adobe Commerce as a Cloud Service]，此連線已自動設定。

Magento Open Source使用[!DNL Payment Services]的Commerce服務聯結器。 [!DNL Catalog Service]、[!DNL Live Search]和[!DNL Product Recommendations]需要Adobe Commerce，因此不適用於Magento Open Source。

>[!NOTE]
>
>Adobe Commerce Optimizer以原生方式提供目錄和銷售功能，而不使用個別的[!DNL Live Search]、[!DNL Catalog Service]和[!DNL Product Recommendations]服務。 其目錄同步不需要使用Commerce Services Connector。 Commerce後端上的其他整合（例如[!DNL Payment Services]和[!DNL Data Connection]）仍需要聯結器。 請參閱[啟用Adobe Commerce Optimizer](enable-aco.md)以最佳化處理程式設定。


## 快速入門

1. 請檢閱[Commerce Services Connector](/help/landing/saas.md)檔案，以取得並設定您的API金鑰。

1. 如需透過聯結器取得的個別服務，請參閱[Adobe Commerce服務指南](/help/landing/home.md)。

## 相關指引

- [設定付款](configure-payments.md)
- [連線AEM Assets](connect-aem-assets.md)
- [整合Adobe Experience Platform](integrate-aep.md)
