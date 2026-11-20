---
title: 預設自動比對
description: 瞭解預設的自動比對規則如何實現Adobe Commerce與AEM Assets整合之間的無縫同步，確保資產自動連結到正確的銷售實體。
feature: CMS, Media, Integration
exl-id: 8a18639b-f508-456e-8d22-18e3e0fdd515
TQID: 'https://experienceleague.adobe.com/z7vpuhsVJnKohiU-bKNrcGnoIQ5WAwcwiccYlvawN0U'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: ddbd0f6e-b569-5a04-8a70-55058777c373
    internal-label: CMS
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
source-git-commit: 5e9c42e5c93ac81604aa38bf3e55c5df729650a0
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%
---
# 預設自動比對

Commerce的AEM Assets整合提供以&#x200B;**AEM Assets**&#x200B;中繼資料組態為基礎的預設自動比對機制(**[!UICONTROL Match by product SKU]**)。 此規則可讓您在&#x200B;**Adobe Commerce**&#x200B;與&#x200B;**AEM Assets**&#x200B;之間無縫同步，確保資產會自動連結至正確的銷售實體。

## 設定自動比對機制

1. 從Commerce Admin導覽至&#x200B;**[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**。

1. 指定&#x200B;**[!UICONTROL Match by product SKU]**&#x200B;作為比對規則。

   ![依產品SKU規則和中繼資料屬性名稱比對](../assets/ootb-matching-rule.png){width="700" zoomable="yes"}

1. 在&#x200B;**[!UICONTROL Match by product SKU attribute name]**&#x200B;中，輸入在AEM Assets中儲存產品SKU的[中繼資料屬性名稱](../metadata.md)，而非實際的SKU值。

   >[!NOTE]
   >
   > 如果遵循了標準上線流程，此值應設為`commerce:skus`。

## 自動比對機制的運作方式

在Commerce Admin中設定&#x200B;**[!UICONTROL Match by product SKU]**&#x200B;相符規則後，Commerce資產檔案會根據為每個檔案設定的資產中繼資料，自動從AEM Assets同步至您的Commerce專案。 您可在&#x200B;**AEM作者**&#x200B;環境中，從AEM Assets **Commerce**&#x200B;索引標籤設定中繼資料：

1. 開啟您的AEM Assets編寫執行個體（此URL已針對您的專案布建在與Adobe Commerce相同的IMS組織中）。

1. 從主導覽畫面中按一下&#x200B;**Assets**&#x200B;以存取數位資產管理(DAM)介面。

1. 在AEM Assets中，將`Eligible for Commerce`欄位設定為`Yes`來更新影像中繼資料，以新增Adobe Commerce關聯。

   ![範例中繼資料](../assets/metadata-commerce-yes.png){width="600" zoomable="yes"}

1. 設定將資產連結至相關產品SKU的中繼資料（[!UICONTROL SKU]、[!UICONTROL position]和[!UICONTROL role]）。

   四個標準角色是`image`、`small_image`、`thumbnail`和`swatch_image`。 使用AEM Assets整合擴充功能1.4.6版或更新版本，您也可以輸入自訂影像角色，例如`hero`或`custom_role_1`。 如需詳細資訊，請參閱[自訂自動比對](custom-match.md)。

   >[!NOTE]
   >
   > 如果資產用於多個產品，請為每個關聯的SKU設定中繼資料。

1. 在`Basic`索引標籤中，將&#x200B;_[!UICONTROL Review Status]_欄位的預設值設定為`approved`。

   ![範例中繼資料](../assets/metadata-review-status.png){width="600" zoomable="yes"}

核准資產後，[確認產品關聯、同步化結果，以及店面顯示](../get-started/setup-synchronization.md#verify-the-integration)。 如果資產未出現，請檢閱[同步處理狀態](../get-started/sync-status.md)。 對於Adobe Commerce Optimizer，請改用[最佳化工具驗證工作流程](../get-started/configure-aco.md#match-by-sku-workflow-example)；無法使用同步處理狀態。

僅[!BADGE PaaS]{type=Informative tooltip="僅適用於雲端專案上的Adobe Commerce （Adobe管理的PaaS基礎結構）。"}如需其他同步化疑難排解，請檢閱[整合記錄檔](../get-started/logs.md)。
