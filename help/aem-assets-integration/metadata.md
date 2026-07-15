---
title: AEM Assets中的Commerce中繼資料
description: 瞭解Commerce整合新增至您的AEM Assets製作環境的AEM Assets名稱空間、中繼資料結構和替代文字。
feature: CMS, Media, Integration
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: da3860b0-d637-47df-bef0-273751180266
source-git-commit: 0c2e50338cbf286704239b6d1f628180e85a3bef
workflow-type: tm+mt
source-wordcount: 749
ht-degree: 0%

---

# AEM Assets中的Commerce中繼資料

Commerce中繼資料是AEM Assets與Commerce之間的合約。 它會告知Commerce哪些資產適用於Commerce、其所屬產品，以及應如何使用或顯示。 此中繼資料可讓AEM Assets整合正確對應及同步資產檔案。

Commerce中繼資料可啟用下列功能：

* **透過`commerce:isCommerce`欄位將資產標示為Commerce合格**。
* **透過`commerce:skus`欄位將資產與一個或多個產品SKU建立關聯**。
* **透過`commerce:roles`和`commerce:positions`欄位定義資產在Commerce**&#x200B;中的顯示方式。
* **透過`commerce:altTextStoreViews`和`commerce:altTextValues`欄位新增由商店檢視**&#x200B;鍵入的Commerce特定替代文字。
* **透過&#x200B;**&#x200B;[!UICONTROL Commerce]&#x200B;**索引標籤和結構描述表單，在AEM Assets屬性UI**&#x200B;中公開這些欄位。

>[!IMPORTANT]
>
>**Commerce專屬替代文字**&#x200B;功能尚未透過[自助上線](get-started/configure-aem.md#enable-aem-commerce-self-service)提供。 目前僅當您部署`assets-commerce`自訂程式碼套件時提供（請參閱[手動安裝assets-commerce套件](get-started/configure-aem.md#install-the-assets-commerce-package-manually)）。 已規劃為即將發行的AEM版本提供原生支援。

若要在您的AEM專案中設定這些資源，請參閱[設定AEM Assets專案](get-started/configure-aem.md)。 本主題的其他部分說明如何提供中繼資料。

## AEM Commerce assets-commerce套件內容

Adobe提供`assets-commerce` AEM Commerce程式碼套件，用於將Commerce名稱空間和中繼資料結構描述資源新增至Experience Manager Assets as a Cloud Service設定。

此套件程式碼會將下列資源新增至AEM Assets編寫環境：

* [自訂名稱空間](https://github.com/ankumalh/assets-commerce/blob/main/ui.config/jcr_root/apps/commerce/config/org.apache.sling.jcr.repoinit.RepositoryInitializer~commerce-namespaces.cfg.json)，`Commerce`可識別Commerce相關屬性。

   * 具有標籤`Eligible for Commerce`的自訂中繼資料型別`commerce:isCommerce`可標籤與Adobe Commerce專案相關聯的Commerce資產。

   * 自訂中繼資料型別`commerce:skus`與對應的UI元件以新增&#x200B;**[!UICONTROL Product Data]**&#x200B;屬性。 產品資料包含中繼資料屬性，以將Commerce資產與產品SKU建立關聯。

     ![自訂產品資料UI控制項](assets/aem-commerce-sku-metadata-fields-from-template.png){width="600" zoomable="yes"}

   * 自訂中繼資料型別`commerce:roles`和`commerce:positions`屬性會顯示資產在Commerce中的視覺化方式。

   * 替代文字多欄位(_[!UICONTROL Alt texts]_)中繼資料，讓編輯人員可以為每個Commerce存放區檢視程式碼輸入替代文字。 多欄位會持續存在於兩個索引對齊的`String[]`屬性中：

      * `commerce:altTextStoreViews` — 儲存每一列的檢視程式碼。
      * `commerce:altTextValues` — 在與`commerce:altTextStoreViews`中的每個專案相同的索引處比對替代文字。

     使用[外部比對器](synchronize/custom-match.md){target=_blank}的App Builder實作可在轉換資產裝載時攔截這些屬性。 這不會變更在目錄中指派產品影像或設定範圍的方式。 請參閱AEM Assets中繼資料[&#128279;](#localized-alt-text-in-aem-assets-metadata)中的本地化替代文字。

* 中繼資料結構表單具有Commerce索引標籤，其中包含用於標籤Commerce資產的`Eligible for Commerce`和`Product Data`欄位。 此表單也提供在AEM Assets UI中顯示或隱藏`roles`和`position`欄位的選項。

  AEM Assets中繼資料結構表單的![Commerce索引標籤](assets/assets-configure-metadata-schema-form-editor.png){width="600" zoomable="yes"}

* [範例已標籤並核准Commerce資產](https://github.com/ankumalh/assets-commerce/blob/main/ui.content/src/main/content/jcr_root/content/dam/wknd/en/activities/hiking/equipment_6.jpg/.content.xml) `equipment_6.jpg`，以支援初始資產同步化。 只有已核准的Commerce資產才能從AEM Assets同步到Adobe Commerce。

>[!NOTE]
>
> 請參閱GitHub上的[readme](https://github.com/ankumalh/assets-commerce)頁面，以取得有關&#x200B;**AEM Commerce封裝程式碼**&#x200B;的詳細資訊。

## AEM Assets中繼資料中的當地語系化替代文字

當您編輯符合資格的影像時，_[!UICONTROL Alt texts]_&#x200B;多欄位可在&#x200B;**[!UICONTROL Commerce]**&#x200B;索引標籤上的AEM Assets資產中繼資料編輯器中使用。

>[!IMPORTANT]
>
> 每個商店的檢視行為僅適用於替代文字。 AEM Assets整合不會針對每個Adobe Commerce商店檢視同步處理不同的產品影像。 來自AEM的產品影像會持續同步至Commerce，並且其相簿指派行為與此版發行前相同。

多欄位在每個Commerce存放區檢視中都包含一列。 每一列有兩個輸入：

* **[!UICONTROL Store View Code]** — 存放區檢視識別碼（例如`default`或`en_US`）。

* **[!UICONTROL Alt Text]** — 該商店檢視的替代文字，限製為255個字元。

選取&#x200B;**[!UICONTROL Add]**&#x200B;為其他存放區檢視新增更多列。 若要移除列，請選取該列上的&#x200B;**[!UICONTROL Delete]**&#x200B;圖示以將其移除。

![Alt文字多欄位，包含儲存區檢視碼和Alt文字輸入](assets/commerce-metadata-alt-texts-multifield.png){width="600" zoomable="yes"}

當您儲存時，如果任何資料列有空白的&#x200B;_[!UICONTROL Store View Code]_，或如果兩個資料列使用相同的存放區檢視代碼（不區分大小寫），使用者端驗證會封鎖提交。

替代文字專案會保留在JCR資產中繼資料中，作為兩個索引對齊的`String[]`屬性：

* `commerce:altTextStoreViews`：儲存每一列的檢視程式碼。
* `commerce:altTextValues`：在與`commerce:altTextStoreViews`中的每個專案相同的索引處比對替代文字。

當這些資產同步至Adobe Commerce時，每個商店的檢視替代文字會寫入產品媒體收藏館，以取得相符的商店檢視代碼。 基礎影像對應不會變更。
