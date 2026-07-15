---
title: 適用於Commerce的AEM Assets整合
description: 瞭解如何將Adobe Experience Manager Assets與您的 [!DNL Commerce] 執行個體整合，以建立和管理Commerce店面的媒體檔案。
feature: CMS, Media, Configuration, Integration
exl-id: f450752a-bef1-419e-ad14-ff8879ab204b
TQID: https://experienceleague.adobe.com/CTDmM7Ox2rQ-55F1BVTg-C8DPBEuEpzFxXGtWpnjXKs
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
subfeature_v2:
  - id: e91a50b1-0b31-436e-9033-00e4776e94cb
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: da3860b0-d637-47df-bef0-273751180266
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 0c2e50338cbf286704239b6d1f628180e85a3bef
workflow-type: tm+mt
source-wordcount: 1081
ht-degree: 1%

---

# 適用於Commerce的AEM Assets整合

在行銷預算受壓之際，對個人化內容的需求迅速增加。 受地區、季節和特定區段需求的驅動，零售商和品牌正在努力跟上產品影像變化需求的增長。

以包含1,000種產品的retailer為例。 在考慮不同地區、客戶區段和個人化工作時，所需數位資產的數量會大幅增加。 此狀況可能會導致大量的資產變數，高達數百萬個。

![總覽](assets/product-visuals-example.png){width="700" zoomable="yes"}

AEM Assets整合可自動化資產管理工作流程，解決此難題。 此整合會根據SKU或其他關鍵屬性，以動態方式將數位資產連結至適當的Adobe Commerce產品和類別。 此程式可透過啟用以下功能來簡化作業並提高效率：

* **順暢的安裝和設定** — 銷售團隊和開發人員可以使用熟悉的Adobe工具和工作流程快速設定整合。

* **動態資產更新** — 產品影像和行銷資產會自動反映AEM Assets的最新變更，保持店面正確且相關。

* **簡化的目錄管理** — 自動化資產重新整理和清理，將手動工作減至最少，並確保產品目錄維持一致且妥善維護。

## 使用整合的需求

若要將此整合與[產品視覺效果或AEM Assets](https://experienceleague.adobe.com/zh-hant/docs/commerce/cloud-service/overview#product-visuals-powered-by-aem-assets)搭配使用，企業必須符合下列要求：

>[!BEGINTABS]

>[!TAB 產品視覺效果]

[!BADGE 僅限SaaS]{type=Positive url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案（Adobe管理的SaaS基礎結構）。"}適用於Adobe Commerce、AEM Assets支援的產品視覺效果以及[AEM Dynamic Media](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/assets/dynamic/administering-dynamic-media)的有效授權（這些授權隨[!DNL Adobe Commerce as a Cloud Service]和[!DNL Adobe Commerce Optimizer]一起提供立即可用）。

>[!TAB AEM Assets]

[!BADGE 僅限SaaS]{type=Positive url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案（Adobe管理的SaaS基礎結構）。"}個Adobe Commerce、Adobe Experience Manager Assets和[AEM Dynamic Media](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/assets/dynamic/administering-dynamic-media)的有效授權。

僅[!BADGE PaaS]{type=Informative tooltip="僅適用於雲端專案上的Adobe Commerce （Adobe管理的PaaS基礎結構）。"} Adobe Commerce 2.4.5+

* PHP 8.1、8.2、8.3和8.4

* Composer 2.x

僅[!BADGE SaaS]{type=Positive url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案（Adobe管理的SaaS基礎結構）。"} Adobe Experience Manager已布建[Adobe Experience Manager Assets as a Cloud Service](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/assets/overview)

>[!ENDTABS]

設定整合的Adobe Commerce使用者必須擁有布建AEM Assets專案的[IMS組織](https://experienceleague.adobe.com/zh-hant/docs/core-services/interface/administration/organizations#concept_EA8AEE5B02CF46ACBDAD6A8508646255)的存取權。

>[!BEGINSHADEBOX]

## 主要業務優點

![支票](assets/icon-check.png) **無額外費用** — 此整合免費提供給符合授權要求的商家。

![檢查](assets/icon-check.png) **官方Adobe解決方案** — 由Adobe開發、維護及完全支援，確保穩定性並與未來的平台增強功能保持一致。

![檢查](assets/icon-check.png) **Adobe Managed支援模型** - Adobe會直接處理協助和疑難排解，提供可靠的支援及簡化的問題解決方案。

![檢查](assets/icon-check.png) **Adobe Storefront Builder功能** — 數位資產管理(DAM)解決方案允許使用[Storefront Builder](https://experienceleague.adobe.com/developer/commerce/storefront/merchants/storefront-builder/?lang=zh-Hant#userlabs-commerce-genai-product-visuals)上的影像、影片和其他媒體等資產。

>[!ENDSHADEBOX]

## 教學課程

若要瞭解如何設定和使用AEM Assets與Adobe Commerce的整合，請觀看這些影片。

>[!BEGINTABS]

>[!TAB 雲端或內部部署教學課程上的Adobe Commerce]

若要瞭解Adobe Commerce和AEM Assets如何共同作業來簡化內容工作流程，請觀看此影片：

>[!VIDEO](https://video.tv.adobe.com/v/3447900?captions=chi_hant)

>[!TAB Adobe Commerce as a Cloud Service教學課程]

瞭解如何使用Adobe Commerce as a Cloud Service與AEM Assets整合。

>[!VIDEO](https://video.tv.adobe.com/v/3478140?quality=12&learn=on)

>[!ENDTABS]

## 後續步驟

安裝和設定AEM Assets整合的程式取決於您的Adobe Commerce部署。 在所有情況下，您會先設定AEM Assets，然後將Commerce連線至該網站。

若要瞭解整合新增至您的AEM Assets環境的名稱空間、中繼資料結構描述和&#x200B;**[!UICONTROL Commerce]**&#x200B;標籤，請在開始前檢閱AEM Assets[&#128279;](metadata.md)中的Commerce中繼資料。

選取您的部署，依序依照必要步驟進行：

>[!BEGINTABS]

>[!TAB Adobe Commerce as a Cloud Service]

僅[!BADGE SaaS]{type=Positive tooltip="僅適用於Adobe Commerce as a Cloud Service專案（Adobe管理的SaaS基礎結構）。"}

1. 若要支援Commerce中繼資料，[請設定AEM Assets專案](get-started/configure-aem.md)。 在AEM版本`2026.5.26309`和更新版本上，使用[自助上線](get-started/configure-aem.md#enable-aem-commerce-self-service)；在舊版上，手動安裝`assets-commerce`套件。

1. [設定IMS使用者許可權](get-started/permissions.md)，以便資產選擇器和自動填入的&#x200B;**[!UICONTROL Program ID]**&#x200B;和&#x200B;**[!UICONTROL Environment ID]**&#x200B;欄位可供使用。

1. [在Commerce管理員中設定整合](get-started/setup-synchronization.md)。

1. 選填。 [啟用產品影像顯示](get-started/configure-storefront.md#enable-product-images)，讓Edge Delivery Services支援的店面可呈現AEM管理的產品影像。

>[!TAB 雲端上的Adobe Commerce (PaaS)]

僅[!BADGE 個PaaS]{type=Informative tooltip="僅適用於雲端專案上的Adobe Commerce （Adobe管理的PaaS基礎結構）。"}

1. 若要支援Commerce中繼資料，[請設定AEM Assets專案](get-started/configure-aem.md)。 在AEM版本`2026.5.26309`和更新版本上，使用[自助上線](get-started/configure-aem.md#enable-aem-commerce-self-service)；在舊版上，手動安裝`assets-commerce`套件。

1. [安裝Adobe Commerce套件](get-started/configure-commerce.md)以新增擴充功能並產生必要的認證和連線。

1. [設定IMS使用者許可權](get-started/permissions.md)，以便資產選擇器和自動填入的&#x200B;**[!UICONTROL Program ID]**&#x200B;和&#x200B;**[!UICONTROL Environment ID]**&#x200B;欄位可供使用。

1. [在Commerce管理員中設定整合](get-started/setup-synchronization.md)。

1. 選填。 [啟用產品影像顯示](get-started/configure-storefront.md#enable-product-images)，讓Edge Delivery Services支援的店面可呈現AEM管理的產品影像。

>[!TAB Adobe Commerce Optimizer]

僅[!BADGE SaaS]{type=Positive tooltip="僅適用於Adobe Commerce Optimizer專案。"}

[!DNL Adobe Commerce Optimizer]它沒有管理員設定UI。 Adobe支援會從您的入門票證設定整合，因此請先準備AEM Assets。

1. 若要支援Commerce中繼資料，[請設定AEM Assets專案](get-started/configure-aem.md)。 在AEM版本`2026.5.26309`和更新版本上，使用[自助上線](get-started/configure-aem.md#enable-aem-commerce-self-service)；在舊版上，手動安裝`assets-commerce`套件。

1. [使用您的租使用者ID、AEM方案ID、AEM環境ID、相符的規則、層級和區域設定，提交上線支援票證](get-started/configure-aco.md#onboarding)。

1. [使用您在票證中註冊的相同地區設定和圖層來設定您的目錄檢視](get-started/configure-aco.md#onboarding)。

1. 選填。 [啟用產品影像顯示](get-started/configure-storefront.md#enable-product-images)，讓Edge Delivery Services支援的店面可呈現AEM管理的產品影像。

   如需完整程式、限制和圖層指南，請參閱[設定Commerce Optimizer的AEM Assets](get-started/configure-aco.md)。

>[!ENDTABS]

## 支援

如果您需要本指南未涵蓋的資訊或問題，請聯絡您的AEM Assets整合銷售代表，或建立[支援票證](https://experienceleague.adobe.com/zh-hant/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#support-case)以取得其他協助。
