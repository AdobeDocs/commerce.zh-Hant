---
title: 設定AEM Assets專案
description: 透過新增整合所需的中繼資料，啟用Adobe Commerce與AEM Assets之間的無縫資產同步。
feature: CMS, Media, Integration
exl-id: a5d2cbab-5ea1-446b-8ab2-2c638128a40c
source-git-commit: 6cd37fda03bb51a1375b0e9dc542f9e02d3c6e54
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 0%

---

# 設定AEM Assets專案以支援Commerce中繼資料

若要在AEM Assets中管理Commerce資產檔案，請完成下列步驟，以使用所需的程式碼和中繼資料設定AEM Assets專案，以便從AEM製作環境管理Commerce資產。

* **步驟1：**&#x200B;安裝含有樣版程式碼的AEM專案範本，將Commerce名稱空間和中繼資料結構描述資源新增至Experience Manager Assets as a Cloud Service環境設定。
* **步驟2：**&#x200B;設定要套用至Commerce資產檔案的中繼資料設定檔

## 將程式碼加入您的AEM專案

Adobe提供AEM Commerce範本`assets-commerce`，將Commerce名稱空間和中繼資料結構描述資源新增至Experience Manager Assets as a Cloud Service環境設定。 將此程式碼作為&#x200B;**Maven**&#x200B;套件部署至您的環境。 然後，在AEM Assets製作環境中設定Commerce中繼資料，以完成設定。

範本將下列資源新增至AEM Assets製作環境：

* [自訂名稱空間](https://github.com/ankumalh/assets-commerce/blob/main/ui.config/jcr_root/apps/commerce/config/org.apache.sling.jcr.repoinit.RepositoryInitializer~commerce-namespaces.cfg.json)，`Commerce`可識別Commerce相關屬性。

   * 具有標籤`commerce:isCommerce`的自訂中繼資料型別`Eligible for Commerce`可標籤與Adobe Commerce專案相關聯的Commerce資產。

   * 自訂中繼資料型別`commerce:skus`與對應的UI元件以新增&#x200B;**[!UICONTROL Product Data]**&#x200B;屬性。 產品資料包含中繼資料屬性，以將Commerce資產與產品SKU建立關聯。

     ![自訂產品資料UI控制項](../assets/aem-commerce-sku-metadata-fields-from-template.png){width="600" zoomable="yes"}

   * 自訂中繼資料型別`commerce:roles`和`commerce:positions`屬性，用於顯示Commerce中資產的視覺化方式。

* 中繼資料結構表單具有Commerce索引標籤，其中包含用於標籤Commerce資產的`Eligible for Commerce`和`Product Data`欄位。 此表單也提供在AEM Assets UI中顯示或隱藏`roles`和`position`欄位的選項。

  AEM Assets中繼資料結構表單的![Commerce索引標籤](../assets/assets-configure-metadata-schema-form-editor.png){width="600" zoomable="yes"}

* [範例已標籤並核准Commerce資產](https://github.com/ankumalh/assets-commerce/blob/main/ui.content/src/main/content/jcr_root/content/dam/wknd/en/activities/hiking/equipment_6.jpg/.content.xml) `equipment_6.jpg`，以支援初始資產同步化。 只有已核准的Commerce資產才能從AEM Assets同步到Adobe Commerce。

>[!NOTE]
>
> 請參閱[readme](https://github.com/ankumalh/assets-commerce)頁面，以取得有關&#x200B;**AEM Commerce樣板**&#x200B;的詳細資訊。

### 先決條件

您需要下列資源和許可權，才能將`commerce-assets`套件部署至AEM Assets as a Cloud Service AEM環境：

* [存取具有計畫和部署管理員角色的AEM Assets Cloud Manager計畫和環境](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager#access-sysadmin-bo)。

* [本機AEM開發環境](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview)，而且熟悉AEM本機開發程式。

* 瞭解[AEM專案結構](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure)以及如何使用Cloud Manager部署自訂內容套件。

### 安裝`commerce-assets`封裝

1. 如有需要，可從AEM Cloud Manager建立AEM Assets專案的生產和中繼環境。

1. 視需要設定部署管道。

1. 從GitHub，從[AEM Commerce範本](https://github.com/ankumalh/assets-commerce)下載程式碼。

1. 從您的[本機AEM開發環境](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview)，將自訂程式碼作為Maven套件安裝在您的AEM Assets環境設定中，或手動將程式碼複製到現有的專案設定中。

1. 提交變更，並將本機開發分支推送到Cloud Manager Git存放庫。

1. 從AEM Cloud Manager [部署您的程式碼以更新AEM環境](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code#deploying-code-with-cloud-manager)。

## 選填。 設定中繼資料設定檔

在AEM Assets製作環境中，透過建立中繼資料設定檔，設定Commerce資產中繼資料的預設值。 然後，將新設定檔套用至AEM資產資料夾，以自動使用這些預設值。 此設定可減少手動步驟，以簡化資產處理。

設定中繼資料設定檔時，您只需要設定下列元件：

* 新增Commerce索引標籤。 此索引標籤會啟用範本新增的Commerce特定組態設定
* 將`Eligible for Commerce`欄位新增至Commerce索引標籤。

產品資料UI元件會根據範本自動新增。

### 定義中繼資料設定檔

1. 登入Adobe Experience Manager作者環境。

1. 在Adobe Experience Manager工作區中，按一下Adobe Experience Manager圖示以前往AEM Assets的作者內容管理工作區。

   ![AEM Assets製作](../assets/aem-assets-authoring.png){width="600" zoomable="yes"}

1. 選取槌子圖示，開啟「管理員」工具。

   ![AEM作者管理員管理中繼資料設定檔](../assets/aem-manage-metadata-profiles.png){width="600" zoomable="yes"}

1. 按一下&#x200B;**[!UICONTROL Metadata Profiles]**&#x200B;開啟設定檔設定頁面。

1. **[!UICONTROL Create]** Commerce整合的中繼資料設定檔。

   ![AEM作者管理員新增中繼資料設定檔](../assets/aem-create-metadata-profile.png){width="600" zoomable="yes"}

1. 新增Commerce中繼資料的索引標籤。

   1. 按一下左側的&#x200B;**[!UICONTROL Settings]**。

   1. 按一下索引標籤區段中的&#x200B;**[!UICONTROL +]**，然後指定&#x200B;**[!UICONTROL Tab Name]**、`Commerce`。

1. 將`Eligible for Commerce`欄位新增至表單。

   ![AEM作者管理員將中繼資料欄位新增至設定檔](../assets/aem-edit-metadata-profile-fields.png){width="600" zoomable="yes"}

   * 按一下&#x200B;**[!UICONTROL Build form]**。

   * 將`Single Line text`欄位拖曳至表單。

   * 按一下`Eligible for Commerce`新增標籤的&#x200B;**[!UICONTROL Field Label]**&#x200B;文字。

   * 在[設定]索引標籤上，將標籤文字新增至&#x200B;**欄位標籤**。

   * 將預留位置文字設定為`yes`。

   * 在&#x200B;**[!UICONTROL Map to Property]**&#x200B;欄位中，複製並貼上下列值

     ```terminal
     ./jcr:content/metadata/commerce:isCommerce
     ```

1. 選填。 若要自動同步處理上傳至AEM Assets環境的已核准Commerce資產，請在&#x200B;_[!UICONTROL Review Status]_&#x200B;索引標籤上將`Basic`欄位的預設值設為`approved`。

1. 儲存更新。

#### 將中繼資料設定檔套用至Commerce資產來源檔案夾

1. 從[!UICONTROL &#x200B; Metadata Profiles]頁面，選取Commerce整合設定檔。

1. 從動作功能表中選取&#x200B;**[!UICONTROL Apply Metadata Profiles to Folders]**。

1. 選取包含Commerce資產的資料夾。

   建立Commerce資料夾（如果沒有）。

1. 按一下&#x200B;**[!UICONTROL Apply]**。

## 後續步驟

僅[!BADGE PaaS]{type=Informative tooltip="僅適用於雲端專案上的Adobe Commerce (Adobe管理的PaaS基礎結構)。"} [安裝Adobe Commerce套件](configure-commerce.md)

**設定您的Commerce店面** — 若要搭配使用AEM Assets與由Edge Delivery Services支援的Commerce店面，請完成[EDS AEM Assets設定](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/)主題中所述的店面設定。
