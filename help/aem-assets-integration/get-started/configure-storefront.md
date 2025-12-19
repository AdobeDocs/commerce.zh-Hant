---
title: 設定您的店面
description: 瞭解如何將您的Edge Delivery Services店面連線到AEM Assets整合。
feature: CMS, Media, Integration
source-git-commit: d426c7878f7a66fe1047673be7c5bf65ae1949a7
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---


# 設定您的店面

AEM Assets整合會顯示在AEM Assets中管理的產品影像，而非使用Adobe Commerce中託管的影像。 此整合可啟用進階影像管理功能，包括進階最佳化、裁切和透過Adobe內容傳遞網路(CDN)傳遞。

若要啟用Edge Delivery Services支援的Commerce店面整合，請更新店面設定檔案(`config.json`)以新增`"commerce-assets-enabled": true`引數。

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

如需如何使用AEM Assets搭配Edge Delivery Services支援的Commerce店面的詳細資訊，請完成[Adobe Commerce店面](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/?lang=zh-Hant)檔案中&#x200B;*AEM Assets整合*&#x200B;主題中所述的店面設定。
