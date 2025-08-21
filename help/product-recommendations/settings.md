---
title: 設定
description: 瞭解如何變更 [!DNL Product Recommendations] 資料的來源，以及如何啟用視覺化建議。
exl-id: fe37624d-c53e-40cd-b182-10f62cba74c0
source-git-commit: 7d5e3faeef2fb16779d1558027a0b76ff3fe3a38
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# 設定

當您[為Recommendations設定SaaS資料空間](../landing/saas.md#saas-configuration)時，SaaS資料空間會收集目錄資料和店面行為資料。 [Adobe Sensei](https://www.adobe.com/sensei.html)會分析該資料，並計算用於提供產品推薦的產品關聯。

測試或測試的非生產環境通常沒有店面行為資料的數量或品質，無法提供逼真的產品建議。 實際購物者行為規模化只能在生產環境中擷取。 為解決此問題，Adobe Commerce可讓您將生產環境中的產品建議與其他非生產SaaS資料空間搭配使用。 在非生產環境中使用實際的店面資料，可讓您預覽購物者看到的建議，並實驗不同的建議型別和放置位置。 購物者可以預覽來自不同SaaS資料空間的建議，但無法點選。

使用暫存`environmentId`記錄暫存訂單。 它不會影響生產資料。 使用`alternateEnvironmentId`擷取生產資料。

>[!NOTE]
>
>透過REST使用產品建議時，`alternateEnvironmentId`引數可用來指定其他資料空間。 透過[GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/)使用產品建議時，此引數無法使用。

## 選擇建議來源

若要變更產品建議資料的來源，請選擇包含您要使用之行為資料的SaaS資料空間。 開始之前，請確定：

- 店面資料收集必須[針對您的生產環境設定並啟用](install-configure.md)，且[已驗證](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/verify/)行為資料正在傳送至Adobe Commerce。
- 您的非生產環境目錄應該與生產目錄基本上相同。 使用類似的目錄可確保產品推薦單位的回報與生產單位非常類似。

1. 登入您的非生產Adobe Commerce環境的管理員。

1. 在&#x200B;_管理員_&#x200B;側邊欄上，前往&#x200B;**行銷** > _促銷活動_ > **產品建議**。

1. 按一下&#x200B;**設定**。

   ![產品推薦設定](assets/settings.png)
   _設定_

1. 在&#x200B;_建議來源_&#x200B;區段中，啟用&#x200B;**從其他SaaS資料空間擷取建議**&#x200B;選項。 _Recommendations來源_&#x200B;區段只會出現在非生產環境中。

   _可用SaaS資料空間_&#x200B;的清單隨即顯示。

   ![產品推薦設定](assets/settings-select-saas.png)
   _設定_

1. 選取具有您要使用的購物者資料的SaaS資料空間。

1. 按一下&#x200B;**儲存變更**。

   Adobe Commerce現在會從選取的資料空間擷取建議。

   >[!NOTE]
   >
   > 雖然您可以檢視從非生產用店面上的其他SaaS資料空間擷取的建議，但您無法按一下這些建議。

### 設定新的SaaS資料空間

1. 在[Recommendations來源]區段中，按一下[編輯組態]。****

1. 依照指示設定新的[[!DNL Commerce] 服務](/help/landing/saas.md)。

## 啟用視覺化建議

如果已安裝[Visual Product Recommendations](install-configure.md)模組，您必須啟用Visual Recommendations才能使用[Visual Similarity](type.md#visualsim)建議型別。

在&#x200B;_視覺建議_&#x200B;區段中，將&#x200B;**啟用視覺建議**&#x200B;設定為作用中的位置。
