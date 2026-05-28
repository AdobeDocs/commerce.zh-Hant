---
title: 設定整合
description: 瞭解如何連線您的Adobe Commerce專案和Experience Manager Assets專案，以啟用這兩個系統之間的資產同步。
feature: CMS, Media
exl-id: 3533d010-926f-4d78-935c-98a9b7040d27
TQID: https://experienceleague.adobe.com/MM-neGrH-N8xBcCwLgnsaIrIjhbX6uYL5kS41QdV79I
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: a6a91fbd6cc6907d070998f67eb0b9c8171dda23
workflow-type: tm+mt
source-wordcount: 948
ht-degree: 2%

---

# 設定整合

將Commerce連線至AEM Assets執行個體，並選取資產同步的比對策略，以設定整合。

識別AEM Assets專案後，選取在Adobe Commerce和AEM Assets之間同步資產的相符規則。

* **[!UICONTROL Match by product SKU]** — 符合資產中繼資料中的SKU與[Commerce產品SKU](https://experienceleague.adobe.com/zh-hant/docs/commerce-operations/implementation-playbook/glossary#sku)的預設規則，以確保資產與正確的產品相關聯。

* **[!UICONTROL Custom match]** — 符合規則，適用於需要自訂比對邏輯的較複雜案例或特定業務需求。 實作自訂比對需要在Adobe Developer App Builder中開發自訂程式碼，以定義資產與產品的比對方式。 即將推出更多詳細資料……

對於初始設定，請使用預設的&#x200B;*依產品SKU比對*&#x200B;規則。

## 需求

在設定AEM Assets整合之前，請確認您已完成下列步驟：

* [設定AEM Assets專案](configure-aem.md)

* 僅[!BADGE PaaS]{type=Informative tooltip="僅適用於雲端專案上的Adobe Commerce （Adobe管理的PaaS基礎結構）。"} [安裝Adobe Commerce套件](configure-commerce.md)以新增擴充功能，並產生使用擴充功能所需的認證和連線。

* [使用者許可權和IMS](permissions.md) — 需要「資產選擇器」和自動填入的設定欄位（方案ID、環境ID、網域對應）。

## 設定連線

1. 從「Commerce管理員」開啟AEM Assets整合設定。

   1. 移至「**[!UICONTROL Store]** >設定> **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**」。

      ![AEM Assets整合啟用整合](../assets/aem-assets-view.png){width="600" zoomable="yes"}

>[!INFO]
>
> AEM Assets整合僅支援全域（預設）範圍內的設定。 不支援網站層級設定。 當您嘗試在網站層級設定整合時，系統會忽略網站層級的設定，改用全域設定值。

1. 僅[!BADGE PaaS]{type=Informative tooltip="僅適用於雲端專案上的Adobe Commerce （Adobe管理的PaaS基礎結構）。"}輸入&#x200B;**[!UICONTROL Asset Selector IMS Client ID]**。

   需要此ID才能啟用資產選擇器，並自動填入方案ID和環境ID欄位的功能。 檢視[使用者許可權和IMS](permissions.md)以取得此ID。 如需「資產選擇器」的詳細資訊，請參閱[手動選取資產](../synchronize/asset-selector-integration.md)。

1. 從下拉式功能表中選取AEM Assets環境&#x200B;**[!UICONTROL Program ID]**&#x200B;和&#x200B;**[!UICONTROL Environment ID]**。

   當您的Commerce管理員使用者符合以下體驗的[使用者許可權和IMS](permissions.md#user-permissions-and-ims)時，就會出現選取器： **Adobe Commerce as a Cloud Service**、**Adobe Commerce Optimizer**&#x200B;和&#x200B;**Adobe Commerce on Cloud Infrastructure**&#x200B;整合功能可從您的IMS連結工作階段自動填入這些欄位，而非依賴貼上的ID。

   如果選取器無法使用，請從AEM Cloud Manager複製&#x200B;**[!UICONTROL Program ID]**&#x200B;和&#x200B;**[!UICONTROL Environment ID]**，或從您的作者URL衍生它們： `https://author-<ProgramID>-<EnvironmentID>.adobeaemcloud.com/` （將預留位置取代為您的識別碼）。

   在貼上或手動選取新值之前，清除任一欄位的&#x200B;**[!UICONTROL Use system value]**。

   ![AEM Assets整合表單，含方案ID和環境ID選取器](../assets/aem-assets-view.png){width="600" zoomable="yes"}

1. [!BADGE 僅限PaaS]{type=Informative tooltip="僅適用於雲端專案上的Adobe Commerce （Adobe管理的PaaS基礎結構）。"}選取[[!UICONTROL Commerce integration]](configure-commerce.md#add-the-integration-to-the-commerce-environment)以驗證Commerce與資產比對服務之間的要求。

1. 將&#x200B;**[!UICONTROL Synchronization enabled]**&#x200B;設為`Yes`以允許Commerce接受來自AEM Assets的傳入更新。

   啟用整合後，可使用其他設定選項來指定資產比對條件。

1. 從&#x200B;**[!UICONTROL Asset matching rule]**&#x200B;下拉式清單中選取其中一個資產比對規則以進行資產同步。

   * 選取[預設自動比對](../synchronize/default-match.md)的&#x200B;**[!UICONTROL Match by SKU]**，
   * 選取&#x200B;**[!UICONTROL Custom match]**&#x200B;進行[自訂自動比對](../synchronize/custom-match.md) （需要[Adobe Developer App Builder](https://experienceleague.adobe.com/zh-hant/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder)。）

1. 新增在&#x200B;**[!UICONTROL Match by product SKU attribute name]**&#x200B;欄位中為AEM Assets產品SKU定義的[Commerce中繼資料欄位名稱](configure-aem.md#define-the-metadata-profile)，預設為`commerce:skus`。

1. 選取&#x200B;**[!UICONTROL Save Config]**&#x200B;以套用更新並啟動資產同步處理。

   設定更新會觸發初始同步流程，允許Commerce接受來自AEM Assets的傳入更新。 同步所需的時間取決於資產數量和特定配置。 整合利用自動化程式，將同步所需的時間減至最少。

### 同步SLA

此整合可保證以下同步處理效能等級：

* `< 5 minutes for 99% of updates`

* `< 30 minutes for 99.9% of updates`

這可確保產品頁面一律顯示最新影像，讓店面內容保持精確且美觀。

### 設定視覺效果擁有者

**視覺化擁有者**&#x200B;設定會決定要提供整合中產品影像的系統：

* Adobe Commerce — 使用Commerce中託管的影像。

* AEM Assets — 使用與AEM同步的影像。

管理員會顯示該擁有者的可用影像，而其餘影像則會呈現灰色，並以&#x200B;**隱藏**&#x200B;標籤顯示。

如需影像顯示行為的詳細資訊，請參閱[設定影像詳細資料](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/catalog/products/digital-assets/product-image#set-image-details){target=_blank}主題。

>[!TIP]
>
> 從Commerce移轉至AEM Assets期間，請將&#x200B;**視覺效果擁有者**&#x200B;設定為Commerce以避免影像連結失效。 所有產品成功與AEM Assets同步後，請切換至AEM Assets擁有者以完成轉變。 這可確保整個程式中的連續影像可用性。

1. 導覽至「**[!UICONTROL Store]** >設定> **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**」。

   ![AEM Assets整合視覺化擁有者功能](../assets/visualization-owner-detail.png){width="400" zoomable="yes"}

1. 選取&#x200B;**視覺化擁有者**&#x200B;來源以顯示影像。

1. 按一下&#x200B;**[!UICONTROL Save Config]**&#x200B;以套用更新並啟動資產同步處理。

### 選填。 設定自訂網域URL

如果AEM Assets as a Cloud Service專案已使用[自訂網域名稱](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name){target=_blank}設定，您必須將網域名稱新增到Commerce存放區設定，好讓Commerce的AEM Assets整合能夠使用它。

1. 導覽至「**[!UICONTROL Store]** >設定> **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**」。

   ![AEM Assets整合啟用整合](../assets/aem-assets-view.png){width="700" zoomable="yes"}

1. 將&#x200B;**自訂網域URL**&#x200B;新增至&#x200B;**[!UICONTROL Asset Custom Domain]**&#x200B;欄位。

1. 按一下&#x200B;**[!UICONTROL Save Config]**&#x200B;以套用更新並啟動資產同步處理。

## 下一步

* **設定您的Commerce店面** — 若要搭配使用AEM Assets與由Edge Delivery Services支援的Commerce店面，請完成&#x200B;*Adobe Commerce店面檔案*&#x200B;中[AEM Assets整合](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/?lang=zh-Hant)主題中所述的店面設定。

* 設定Adobe Commerce與AEM Assets整合之間的[相符規則](../synchronize/default-match.md)。

* [管理Commerce資產](../manage-assets.md)。
