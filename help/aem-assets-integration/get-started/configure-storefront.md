---
title: 設定您的店面
description: 瞭解如何將您的Edge Delivery Services店面連線到AEM Assets整合。
feature: CMS, Media, Integration
TQID: https://experienceleague.adobe.com/gl0Y2UNs3sYkXE9QYwLtAltyX1dxE699y23ey-y0KUU
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
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 137
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

如需如何使用AEM Assets搭配Edge Delivery Services支援的Commerce店面的詳細資訊，請完成&#x200B;*Adobe Commerce店面*&#x200B;檔案中[AEM Assets整合](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/)主題中所述的店面設定。
