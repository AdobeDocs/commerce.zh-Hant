---
title: 設定您的店面
description: 瞭解如何將您的Edge Delivery Services店面連線到AEM Assets整合。
feature: CMS, Media, Integration
TQID: https://experienceleague.adobe.com/gl0Y2UNs3sYkXE9QYwLtAltyX1dxE699y23ey-y0KUU
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
subfeature_v2: id: ae62cf09-5996-4921-bda8-fbe67b62e470
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2: id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: 7f901cec90291e264376e3f93e6ebaaccf7c15f0
workflow-type: tm+mt
source-wordcount: 610
ht-degree: 0%

---

# 設定您的店面

## 從AEM Assets啟用產品影像顯示 {#enable-product-images}

AEM Assets整合會顯示AEM Assets而不是Adobe Commerce的產品影像，以啟用進階最佳化、裁切和CDN傳送。

若要啟用Edge Delivery Services所支援之Commerce店面中的整合，請新增`"commerce-assets-enabled": true`引數至店面設定檔(`config.json`)。

```json
{
  "public": {
    "default": {
      "commerce-assets-enabled": true
    }
  }
}
```

Commerce下拉式清單會自動偵測`commerce-assets-enabled`設定，並據此調整影像處理。

如需將AEM Assets與Edge Delivery Services支援的Commerce店面搭配使用的詳細資訊，請參閱&#x200B;*AEM Assets店面*&#x200B;檔案中的[Adobe Commerce整合](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/)主題。

>[!TIP]
>
>若要讓作者瀏覽並將AEM Assets插入靜態內容頁面，請參閱[將AEM Assets連線至Da.live以進行靜態內容製作](#connect-aem-assets-authoring)。

## 將AEM Assets連線至Da.live以進行靜態內容製作 {#connect-aem-assets-authoring}

>[!NOTE]
>
>此設定獨立於AEM Assets整合擴充功能。 它由[Da.live](https://da.live){target="_blank"}提供，可讓作者透過[!UICONTROL Library]面板和[!UICONTROL Content Advisor]瀏覽AEM Assets，並將其插入靜態內容頁面（例如，登陸頁面或內容區塊）。 透過AEM Assets整合約步化的產品影像是使用`commerce-assets-enabled`設定個別設定的。

使用下列步驟將AEM Assets連線至Document Authoring (Da.live)店面，讓作者在編輯靜態內容時可以瀏覽並插入&#x200B;**[!UICONTROL Content Advisor]**&#x200B;的AEM Assets。

>[!NOTE]
>
>如需詳細的設定指示，請參閱Da.live檔案中的[設定AEM Assets](https://docs.da.live/administrators/guides/setup-aem-assets){target=_blank}和AEM Assets檔案中的[為Edge Delivery Services編寫AEM Assets內容時整合](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/integrate-aem-assets-edge-delivery-services/integrate-aem-assets-edge-delivery-services){target=_blank}。

### 步驟1：在Da.live中開啟您的網站設定

1. 從[Da.live](https://da.live){target=_blank}，找到並開啟您的店面。

1. 在階層連結導覽中，選取網站名稱旁的&#x200B;**[!UICONTROL Settings]**&#x200B;圖示，開啟網站設定試算表。

### 步驟2：複製您的AEM存放庫URL

1. 在新標籤中，前往[experience.adobe.com](https://experience.adobe.com){target=_blank}並導覽至&#x200B;**[!UICONTROL Experience Manager]**。

1. 開啟Adobe Experience Manager Assets：捲動至&#x200B;**[!UICONTROL My Authoring]**&#x200B;區段，然後選取&#x200B;**[!UICONTROL Production]**&#x200B;環境旁的&#x200B;**[!UICONTROL Assets]**。

1. 從瀏覽器位址列，複製開頭為`author`直到（包括） `.com`的區段，例如`author-p107634-e1009805.adobeaemcloud.com`。

### 步驟3：將存放庫ID新增至您的設定

1. 若要設定您的網站，請返回Da.live並在您的網站設定中選取&#x200B;**[!UICONTROL data]**。

1. 依照下列步驟完成試算表：

   | 儲存格 | 值 |
   |---|---|
   | A1 | `key` |
   | B1 | `value` |
   | A2 | `aem.repositoryId` |
   | B2 | 您在步驟2複製的URL |

1. 選取「**[!UICONTROL Save]**」，然後選取網站名稱旁的「上一步」箭頭，以返回網站根目錄。

   >[!NOTE]
   >
   > `author-`首碼主機會從製作層級瀏覽資產。 若要改為透過Dynamic Media傳送資產，請使用`delivery-`前置主機。 如需所有`aem.repositoryId`選項，請參閱[設定AEM Assets](https://docs.da.live/administrators/guides/setup-aem-assets){target=_blank}。

### 步驟4：透過程式庫連線AEM Assets

1. 從網站根目錄中，選取&#x200B;**[!UICONTROL index]**&#x200B;資料夾以開啟。

1. 在編輯器中，開啟&#x200B;**[!UICONTROL Library]**&#x200B;面板並選取&#x200B;**[!UICONTROL AEM Assets]**。

   **[!UICONTROL Content Advisor]**&#x200B;彈出視窗會開啟，並顯示您的AEM Assets資料夾和檔案。

您的店面現在已連線至AEM Assets。 您可以直接從&#x200B;**[!UICONTROL Content Advisor]**&#x200B;瀏覽及插入資產。

## 相關檔案

* *AEM Assets店面*&#x200B;檔案中的[Adobe Commerce整合](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/){target=_blank} — 店面設定和影像處理行為。

* 在&#x200B;*AEM Assets*&#x200B;檔案中為Edge Delivery Services](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/integrate-aem-assets-edge-delivery-services/integrate-aem-assets-edge-delivery-services){target=_blank}製作內容時，請[整合AEM Assets。

* 在Da.live檔案中[設定AEM Assets](https://docs.da.live/administrators/guides/setup-aem-assets){target=_blank}和[使用媒體](https://docs.da.live/authors/guides/adding-media){target=_blank}。
