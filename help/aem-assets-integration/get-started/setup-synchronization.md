---
title: 設定整合
description: 瞭解如何連線您的Adobe Commerce專案和Experience Manager Assets專案，以啟用這兩個系統之間的資產同步。
feature: CMS, Media
exl-id: 3533d010-926f-4d78-935c-98a9b7040d27
TQID: 'https://experienceleague.adobe.com/MM-neGrH-N8xBcCwLgnsaIrIjhbX6uYL5kS41QdV79I'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: ddbd0f6e-b569-5a04-8a70-55058777c373
    internal-label: CMS
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
    internal-label: Storefront configuration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: 5e9c42e5c93ac81604aa38bf3e55c5df729650a0
workflow-type: tm+mt
source-wordcount: '1355'
ht-degree: 1%
---
# 設定整合

將Commerce連線至AEM Assets執行個體，並選取資產同步的比對策略，以設定整合。

識別AEM Assets專案後，選取在Adobe Commerce和AEM Assets之間同步資產的相符規則。

* **[!UICONTROL Match by product SKU]** — 符合資產中繼資料中的SKU與[Commerce產品SKU](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/glossary#sku)的預設規則，以確保資產與正確的產品相關聯。

* **[!UICONTROL Custom match]** — 符合規則，適用於需要自訂比對邏輯的較複雜案例或特定業務需求。 實作自訂比對需要在Adobe Developer App Builder中開發自訂程式碼，以定義資產與產品的比對方式。 請參閱[自訂自動比對](../synchronize/custom-match.md)。

對於初始設定，請使用預設&#x200B;**[!UICONTROL Match by product SKU]**&#x200B;規則。

## 需求

在設定AEM Assets整合之前，請確認您已完成下列步驟：

* [設定AEM Assets專案](configure-aem.md)

* 僅[!BADGE PaaS]{type=Informative tooltip="僅適用於雲端專案上的Adobe Commerce （Adobe管理的PaaS基礎結構）。"} [安裝Adobe Commerce套件](configure-commerce.md)以新增擴充功能，並產生使用擴充功能所需的認證和連線。

* [使用者許可權和IMS](permissions.md) — 設定「資產選擇器」、「AEM環境選擇」和網域對應的必要許可權。

## 設定連線

![AEM Assets整合設定包含範例環境和網域值](../assets/aem-assets-view.png){width="900" zoomable="yes"}

1. 從Commerce Admin，前往&#x200B;**[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**。

>[!INFO]
>
> AEM Assets整合僅支援全域（預設）範圍內的設定。 不支援網站層級設定。 當您嘗試在網站層級設定整合時，系統會忽略網站層級的設定，改用全域設定值。

1. 僅[!BADGE PaaS]{type=Informative tooltip="僅適用於雲端專案上的Adobe Commerce （Adobe管理的PaaS基礎結構）。"}輸入&#x200B;**[!UICONTROL Asset Selector IMS Client ID]**。

   啟用資產選擇器需要此ID。 檢視[使用者許可權和IMS](permissions.md)以取得此ID。 如需「資產選擇器」的詳細資訊，請參閱[手動選取資產](../synchronize/asset-selector-integration.md)。

1. 從&#x200B;**[!UICONTROL AEM Environment]**&#x200B;中，選取在[設定AEM Assets專案](configure-aem.md)中設定的環境。

   此清單包括您的使用者擁有作者或傳遞產品設定檔的AEM環境。 如果缺少預期的環境，請檢閱[使用者許可權和IMS](permissions.md)。

   如果您的設定改為顯示單獨的&#x200B;**[!UICONTROL Program ID]**&#x200B;和&#x200B;**[!UICONTROL Environment ID]**&#x200B;欄位，請指定該環境的識別碼。 若是手動輸入，請從AEM Cloud Manager複製它們，或從您的作者URL衍生它們： `https://author-p<ProgramID>-e<EnvironmentID>.adobeaemcloud.com/`。 僅輸入數值識別碼，不含`p`和`e`首碼。

   針對具有&#x200B;**[!UICONTROL Use system value]**&#x200B;核取方塊的欄位，在覆寫預設值之前請清除該核取方塊。

1. 檢查&#x200B;**[!UICONTROL AEM Domain Mapping]**。 系統會根據選取的AEM環境自動載入可用網域。 如果您的專案使用自訂資產傳遞網域，請依照[設定自訂網域URL](#optional-configure-the-custom-domain-url)操作。

1. [!BADGE 僅限PaaS]{type=Informative tooltip="僅適用於雲端專案上的Adobe Commerce （Adobe管理的PaaS基礎結構）。"}選取[[!UICONTROL Commerce integration]](configure-commerce.md#add-the-integration-to-the-commerce-environment)以驗證Commerce與資產比對服務之間的要求。

1. 將&#x200B;**[!UICONTROL Synchronization enabled]**&#x200B;設為`Yes`以允許Commerce接受來自AEM Assets的傳入更新。

   啟用整合後，可使用其他設定選項來指定資產比對條件。

1. 從&#x200B;**[!UICONTROL Asset matching rule]**&#x200B;下拉式清單中選取其中一個資產比對規則以進行資產同步。

   * [預設自動比對](../synchronize/default-match.md)的Select **[!UICONTROL Match by product SKU]**。
   * 適用於[自訂自動比對](../synchronize/custom-match.md)的Select **[!UICONTROL Custom match]**。 此選項需要[Adobe Developer App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/extensibility/adobe-developer-app-builder/introduction-to-app-builder)。

1. 針對&#x200B;**[!UICONTROL Match by product SKU]**，在&#x200B;**[!UICONTROL Match by product SKU attribute name]**&#x200B;欄位中輸入[AEM Assets中繼資料屬性名稱](../metadata.md)。 預設值為`commerce:skus`。

   輸入屬性名稱，而非產品SKU值。 將實際產品SKU新增至AEM Assets中每個資產的&#x200B;**[!UICONTROL Product Data]**&#x200B;中繼資料，如[預設自動比對](../synchronize/default-match.md)中所述。

1. 檢閱[視覺化擁有者](#configure-the-visualization-owner)設定。 在移轉期間，保留&#x200B;**Adobe Commerce**&#x200B;所有權，直到資產同步處理完成。

1. 選取&#x200B;**[!UICONTROL Save Config]**&#x200B;以套用更新並啟動資產同步處理。

   設定更新會觸發初始同步流程，允許Commerce接受來自AEM Assets的傳入更新。 同步所需的時間取決於資產數量和特定配置。 整合利用自動化程式，將同步所需的時間減至最少。

### 同步SLA

用於整合的service level agreement (SLA)可保證以下同步處理效能等級：

* `< 5 minutes for 99% of updates`

* `< 30 minutes for 99.9% of updates`

此等級的服務可確保產品頁面一律顯示最新的影像，讓店面內容保持精確且美觀。

## 同步當地語系化替代文字

本地化的替代文字會使用現有的資產同步程式。 您不需要新的事件型別或單獨的同步設定。

1. 在AEM資產的&#x200B;**[!UICONTROL Commerce]**&#x200B;索引標籤中新增一或多個存放區檢視替代文字列。

1. 將資產與Commerce產品SKU建立關聯。

1. 在AEM Assets中核准資產。

1. 等待資產事件和同步程式完成。

1. 驗證Commerce管理員和店面回應中的當地語系化值。

如需欄位名稱、驗證規則和Commerce結果，請參閱AEM Assets中的[Commerce中繼資料](../metadata.md)。

## 設定視覺效果擁有者

**視覺化擁有者**&#x200B;設定會決定要提供整合中產品影像的系統：

* Adobe Commerce — 使用Commerce中託管的影像。

* AEM Assets — 使用與AEM同步的影像。

管理員會顯示該擁有者的可用影像，而其餘影像則會呈現灰色，並以&#x200B;**隱藏**&#x200B;標籤顯示。

如需影像顯示行為的詳細資訊，請參閱[設定影像詳細資料](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/digital-assets/product-image#set-image-details){target=_blank}主題。

>[!TIP]
>
> 從Commerce移轉至AEM Assets期間，請將&#x200B;**視覺效果擁有者**&#x200B;設定為Commerce以避免影像連結失效。 所有產品成功與AEM Assets同步後，請切換至AEM Assets擁有者以完成轉變。 這可確保整個程式中的連續影像可用性。

1. 導覽至&#x200B;**[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**。

   ![視覺效果擁有者設定為AEM Assets](../assets/visualization-owner-detail.png){width="700" zoomable="yes"}

1. Select **視覺化擁有者**&#x200B;來源以顯示影像。

1. 按一下&#x200B;**[!UICONTROL Save Config]**&#x200B;以套用更新。

   在切換至&#x200B;**AEM Assets**&#x200B;之前，[請確認資產與預期的產品](#verify-the-integration)相關聯。 然後[設定您的店面](configure-storefront.md)以顯示AEM Assets產品影像。

## 選填。 設定自訂網域URL

如果AEM Assets as a Cloud Service專案已使用[自訂網域名稱](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name){target=_blank}設定，您必須將網域名稱新增到Commerce存放區設定，好讓Commerce的AEM Assets整合能夠使用它。

向您的AEM管理員取得已設定的資產傳送自訂網域URL。 此設定會取代AEM傳遞URL；這不是用於識別方案ID和環境ID的AEM作者URL。 如果您的專案未使用自訂網域，請保持網域對應不變。

>[!NOTE]
>
>設定自訂網域URL不會更新先前同步資產的URL。 這些資產會保留其先前的URL，直到[在AEM Assets](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/reprocessing){target=_blank}中重新處理為止。 儲存自訂網域設定後，重新處理這些資產以更新其URL來使用自訂網域。

1. 導覽至&#x200B;**[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**。

1. 確認選取的&#x200B;**[!UICONTROL AEM Environment]**，然後從&#x200B;**[!UICONTROL AEM Domain Mapping]**&#x200B;中選取已設定的自訂網域。 系統會自動為選取的環境載入可用網域。

![AEM環境和網域選擇器，範例值為](../assets/aem-assets-environment-domain.png){width="700" zoomable="yes"}

    對於顯示&#x200B;**[!UICONTROL Asset Custom Domain]**&#x200B;文字欄位的設定，請在該欄位中輸入自訂網域URL。

1. 按一下&#x200B;**[!UICONTROL Save Config]**&#x200B;以套用更新。

## 驗證整合

>[!NOTE]
>
>Adobe Commerce Optimizer無法使用同步狀態。 請遵循[Commerce Optimizer驗證工作流程](configure-aco.md#match-by-sku-workflow-example)，而非下列Commerce管理員檢查。

1. 選擇現有的Commerce產品並記下其SKU。

1. 在AEM Assets中，將測試資產標示為&#x200B;**[!UICONTROL Eligible for Commerce]**、將其與該產品SKU建立關聯，並設定其角色和位置。 核准資產。 請參閱[預設自動比對](../synchronize/default-match.md)，或使用您設定的[自訂比對規則](../synchronize/custom-match.md)。

1. 同步完成後，請在Commerce管理員中開啟產品，並檢查其&#x200B;**[!UICONTROL Images And Videos]**&#x200B;區段以取得相關的資產、角色和位置。 請參閱[管理資產](../manage-assets.md)。

1. 檢閱[同步處理狀態](sync-status.md)以取得資產的同步處理結果。 如果同步化失敗，請檢閱&#x200B;**[!UICONTROL Error]**&#x200B;欄。

1. 選取&#x200B;**AEM Assets**&#x200B;作為視覺效果擁有者並完成[店面組態](configure-storefront.md)後，請開啟店面的產品並確認出現預期的影像。

僅[!BADGE PaaS]{type=Informative tooltip="僅適用於雲端專案上的Adobe Commerce （Adobe管理的PaaS基礎結構）。"}如需其他同步化疑難排解，請檢閱[整合記錄檔](logs.md)。

## 下一步

* [設定您的Commerce店面](configure-storefront.md)，以便使用Edge Delivery Services顯示AEM Assets的產品影像。

* 設定Adobe Commerce與AEM Assets整合之間的[相符規則](../synchronize/default-match.md)。

* [管理Commerce資產](../manage-assets.md)。
