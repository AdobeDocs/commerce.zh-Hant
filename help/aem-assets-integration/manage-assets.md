---
title: 管理資產
description: 使用適用於Commerce的AEM Assets整合，管理店面的媒體資產。
feature: CMS, Media
exl-id: 40ca36e0-d617-4814-852d-bc60ff53b2b3
source-git-commit: a0eaaf0de53962b37c7b52f3e7e13aac4c62e372
workflow-type: tm+mt
source-wordcount: '982'
ht-degree: 0%

---

# 管理Commerce媒體資產

<!--In ACAP-844, this topic was linked to from the Commerce Admin products images and videos when the Assets integration is enabled. If the URL to the topic changes, be sure to add a redirect.-->

在Commerce的AEM Assets整合啟用後，您可以管理下列媒體型別：

* 產品影像
* 內容影像
* 產品視頻
* 類別影像

**正在更新產品映像？**

產品影像通過匹配規則連結：

* 若要瞭解如何在AEM Assets中新增或更新產品資產（中繼資料、SKU連結、核准），請參閱[預設自動比對](synchronize/default-match.md)。
* 如需類別影像或頁面產生器內容，請參閱[手動選取資產](synchronize/asset-selector-integration.md)。

## 產品影像

啟用整合後，影像管理可在數位資產管理系統(DAM)中集中管理。 接著Adobe Commerce就會成為重要的參與管道，確保各店面只會使用獲得核准的高品質影像。 此設定可增強品牌一致性、將手動工作減到最少，並簡化內容更新，讓商家無須在Adobe Commerce中手動上傳或管理影像。

### 在Adobe Commerce中檢視產品影像

系統會根據預先設定的比對規則，自動從AEM Assets提取產品影像：

1. 在&#x200B;_管理員_&#x200B;側邊欄上，瀏覽至&#x200B;**[!UICONTROL Catalog]** > **[!UICONTROL Products]**。

1. 選取產品。

1. 開啟&#x200B;**影像和影片**&#x200B;區段。

   ![產品影像](assets/product-image.png){width="600" zoomable="yes"}

   >[!NOTE]
   >
   > 訊息會指出整合已啟用，使這成為&#x200B;**唯讀**&#x200B;區段，因為影像管理集中於DAM中。

   若要設定產品資產（將影像連結至SKU），請開啟您的AEM Assets作者執行個體，然後從主檢視按一下&#x200B;**Assets**。 請參閱中繼資料組態步驟的[預設自動比對](synchronize/default-match.md)。

### 在AEM Assets中管理產品影像

若要管理產品相關影像，所有變更必須直接在&#x200B;**AEM Assets**&#x200B;中進行。 此程式已完全自動化，可確保將任何變更同步至Adobe Commerce，無需手動干預。

要瞭解如何將資產連結到AEM Assets的產品（包括元資料配置和批准），請參閱以下主題：

* [預設自動匹配](synchronize/default-match.md)
* [自定義自動匹配](synchronize/custom-match.md)。

### 同步SLA

有關同步計時的資訊，請參閱[同步SLA](get-started/setup-synchronization.md#synchronization-sla)主題。

## 內容影像

Adobe Commerce為未使用CMS (Adobe Experience Manager)工具集的商家提供Page Builder做為&#x200B;**內容管理系統(AEM)**。 為了增強內容建立功能，我們的整合採用[AEM Asset Selector](synchronize/asset-selector-integration.md)，讓行銷人員可直接從&#x200B;**DAM**&#x200B;順暢存取及內嵌影像。 如此可確保內容建立時只使用經過核准且高品質的影像，而無須在Adobe Commerce中備援儲存空間。

### 在頁面產生器中使用AEM資產選擇器

僅[!BADGE PaaS]{type=Informative tooltip="僅適用於雲端專案上的Adobe Commerce （Adobe管理的PaaS基礎結構）。"}若要使用&#x200B;**AEM資產選擇器**&#x200B;嵌入影像：

1. 使用&#x200B;**頁面產生器**&#x200B;導覽至`content enrichment`Adobe Commerce Admin **中支援**&#x200B;的任何區段。

1. 開啟[頁面產生器](https://developer.adobe.com/commerce/frontend-core/page-builder/){target=_blank}。

   將會提供名為&#x200B;**AEM資產**&#x200B;的新媒體型別。

1. 將AEM資產媒體型別拖放至內容區塊中。

1. 出現提示時，提供存取DAM的認證。

1. 從DAM選取影像，並將其直接插入內容中。

與選取影像的關聯將會儲存到Adobe Commerce中，做為指向&#x200B;**Dynamic Media**&#x200B;的直接URL，確保：

* 影像檔案不需要儲存在Adobe Commerce中。

* 營銷人員只與DAM的批准資產合作。

* 所有客戶接觸點的內容保持一致和最新。

>[!TIP]
>
> [DA.live（文檔創作）](https://experienceleague.adobe.com/developer/commerce/storefront/merchants/storefront-builder/#dalive-document-authoring){target=_blank}還提供了資產選擇器以豐富資料。

## 產品視頻

Adobe Commerce是數位資產的重要參與管道。 啟用AEM Assets整合後，視訊管理會集中於&#x200B;**DAM**&#x200B;中，確保各商務店面的一致性、法規遵循及最佳化傳送。

### 管理產品影片

1. 在&#x200B;_管理員_&#x200B;側邊欄上，瀏覽至&#x200B;**[!UICONTROL Catalog]** > **[!UICONTROL Products]**。

1. 選取產品。

1. 開啟&#x200B;**影像和影片**&#x200B;區段。

   ![產品影像](assets/product-image.png){width="600" zoomable="yes"}

   >[!NOTE]
   >
   > 訊息指出整合已啟用，使此區段&#x200B;**成為唯讀**，因為視訊是在AEM Assets中控制。

### 在AEM Assets中關聯影片

1. 在AEM Assets中，導覽至您要與產品相關聯的影片。

1. 將影片連結至Adobe Commerce中的一或多個產品。

1. 整合會自動同步關聯，直接在店面顯示Dynamic Media視訊播放器。 如此一來，商家就不需要管理視訊播放設定。

### 僅支援API優先視訊

目前，整合可透過API支援影片，讓合作夥伴能以程式設計方式擷取影片。

>[!WARNING]
>
> 依預設，視訊尚未整合至現有的Adobe Commerce店面解決方案。

這項整合可確保商戶能以可擴充且最佳化的方式輕鬆管理產品影片，同時利用AEM Assets和Dynamic Media實現順暢的傳送。

### 同步SLA

如需同步處理時間的相關資訊，請參閱[同步SLA](get-started/setup-synchronization.md#synchronization-sla)主題。

## 類別影像

Adobe Commerce使商戶能夠將影像與產品類別關聯起來，幫助建立一個視覺上令人著迷的店面。 AEM Assets整合利AEM用資產選擇器，使營銷商能夠直接從&#x200B;**數字資產管理系統(DAM)**&#x200B;無縫選擇資產。 這確保只使用經批准的映像，並消除了將其儲存在Adobe Commerce的需要，從而跨所有項目渠道保持一致性和效率。

### 將資AEM產選擇器用於類別影像

設定[AEM Asset Selector](synchronize/asset-selector-integration.md)後，您就可以用它來將資產新增至目錄類別內容。

1. 在&#x200B;_管理員_&#x200B;側邊欄上，瀏覽至&#x200B;**[!UICONTROL Catalog]** > **[!UICONTROL Categories]**。

1. 選取要更新的類別。

1. 展開![區段中的](../assets/icon-display-expand.png)擴充選擇器&#x200B;**[!UICONTROL Content]**。

1. 在&#x200B;**[!UICONTROL Content]**&#x200B;區段中，找出與類別相關聯的&#x200B;*影像欄位*。

   ![類別內容](assets/category-asset.png){width="600" zoomable="yes"}

1. 按一下&#x200B;**[!UICONTROL Select from Assets]**&#x200B;以變更類別影像。

   ![類別內容](assets/asset-view.png){width="600" zoomable="yes"}

1. 從「AEM資產選擇器」中選擇影像。

   ![類別內容](assets/select-image.png){width="600" zoomable="yes"}

1. 按一下&#x200B;**[!UICONTROL Save]**&#x200B;並繼續。

   如需建立類別的詳細資訊，請參閱[Commerce Catalog Management Guide](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/categories/create/category-create#step-3-complete-the-category-content)中的&#x200B;**完成類別內容**。

## 更新資產

當您在AEM Assets中更新並核准資產後，系統會自動使用自動比對功能將更新傳送至Adobe Commerce。 此程式會在資產核準時觸發。 為確保包括所有最終變更和中繼資料更新，在核准資產之前，請務必重新處理資產。

若要讓Commerce端工作流程透過中繼資料將資產連結至產品，請參閱[預設自動比對](synchronize/default-match.md)主題。

如需AEM Assets程式的相關資訊，請參閱下列檔案：

* [正在重新處理數位資產](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/reprocessing)

* [批准資產](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/approve-assets)
