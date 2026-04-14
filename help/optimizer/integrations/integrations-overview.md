---
title: Commerce Optimizer整合
description: 瞭解用於目錄同步、資產管理、店面最佳化和Salesforce Commerce Cloud連線的Adobe Commerce Optimizer整合。
solution: Commerce
feature: Integration, Catalog Management
role: Developer, Admin
level: Beginner
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於 [!DNL Adobe Commerce Optimizer] 個專案（Adobe管理的SaaS基礎結構）。"
exl-id: 8f3a2c1b-9d4e-5f6a-bc7d-1e2f3a4b5c6d
source-git-commit: d8cd6f543353e1b11f3aa14b3b97b02155d23809
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---


# [!DNL Adobe Commerce Optimizer]整合

[!DNL Adobe Commerce Optimizer]包含可讓您在雲端或內部部署上從Adobe Commerce同步資料、管理資產、改善店面體驗，以及連線外部系統的整合。 以下各節說明每個整合如何與[!DNL Adobe Commerce Optimizer]搭配運作。 請依照連結進行設定、設定和日常使用。

## Adobe Commerce Optimizer聯結器 {#aco-connector}

Adobe Commerce Optimizer聯結器是在Adobe Commerce （雲端或內部部署）和[!DNL Adobe Commerce Optimizer]之間同步目錄和定價資料的橋接器。 啟用聯結器後，Commerce仍會是產品資料的記錄系統，而[!DNL Adobe Commerce Optimizer]會支援產品探索、建議、銷售規則、分析和Headless店面體驗。

- [Adobe Commerce Optimizer聯結器總覽](../../aco-connector/overview.md){target="_blank"}
- [開始使用聯結器](../../aco-connector/get-started.md){target="_blank"}

## 透過AEM Assets呈現產品視覺效果 {#product-visuals}

產品視覺效果可讓您透過Adobe Experience Manager (AEM) Assets管理產品影像。 設定適用於Commerce Optimizer的AEM Assets以啟用產品視覺效果。 完成設定後，您可將AEM Assets設為產品影像的集中式數位資產管理解決方案，並透過自動化資產檢閱和管理工作流程，將影像與Commerce Optimizer目錄保持同步。 此整合會依SKU比對資產與產品。 更新會流經Adobe的整合服務，因此店面可反映最新媒體，無需手動重新上傳。

- [透過AEM Assets呈現產品視覺效果](../setup/product-visuals.md)
- [為Commerce Optimizer設定AEM Assets](../../aem-assets-integration/get-started/configure-aco.md){target="_blank"}

## Adobe Experience Manager Sites Optimizer {#aem-sites-optimizer}

Adobe Experience Manager Sites Optimizer會分析Commerce網站，並藉由呈現AI驅動的&#x200B;**[!UICONTROL Opportunities]**&#x200B;來改善效能 — 可協助您改善探索、參與和轉換的建議。

>[!AVAILABILITY]
>
>此功能需要&#x200B;**Ultima** Adobe Sites Optimizer授權。 您可以透過Adobe客戶技術顧問索取授權。 布建帳戶後，[!DNL Adobe Commerce Optimizer]介面中就會提供機會功能，您可以開始使用AI導向的深入分析來最佳化您的店面與銷售策略。

- [機會](../manage-results/opportunities.md)

## Commerce Salesforce聯結器 {#commerce-salesforce-connector}

Commerce Salesforce Connector （以Adobe App Builder為基礎）將Salesforce Commerce Cloud B2C的目錄和價格資料同步至[!DNL Adobe Commerce Optimizer]，因此您可以使用Adobe店面與銷售功能，而不需要重新部署Salesforce商務後端。 您可以使用Salesforce Commerce API排程同步、執行隨選更新及擴充整合。

- [Salesforce Commerce聯結器](../developer/salesforce-connector.md)

>[!MORELIKETHIS]
>
>- [Adobe Commerce Optimizer技術檔案](https://developer.adobe.com/commerce/services/optimizer/){target="_blank"}
>- [開始使用Adobe Commerce Optimizer](../get-started.md)
