---
title: Headless
description: 瞭解如何將 [!DNL Product Recommendations] 整合到Headless店面。
exl-id: c40dac31-f87e-402a-ba50-e8aa4c1d66aa
source-git-commit: 1548b7e11249febc2cd8682581616619f80c052f
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---

# Headless

您可以使用[!DNL Product Recommendations]PWA Studio[或自訂前端技術（例如React或Vue JS）將](https://developer.adobe.com/commerce/pwa-studio/)整合到Headless店面。

自訂和Headless整合經銷商應參考這些Luma和PWA指示，作為建議的實作。 有許多方式可將產品建議實作到Headless解決方案中，本檔案未涵蓋所有案例。 整合經銷商必須為其實作提供事件、設計和測試服務。

[!DNL Product Recommendations]需要[行為和目錄資料](https://experienceleague.adobe.com/docs/commerce/product-recommendations/developer/development-overview.html?lang=zh-Hant)才能運作。 Headless實作中的目錄資料同步程式維持不變，但行為資料收集需要變更。

>[!NOTE]
>
>Headless執行個體必須實作事件以支援產品建議儀表板。

若要將[!DNL Product Recommendations]整合到Headless店面，您必須：

1. 將行為資料傳送至Adobe Sensei，以分析和計算產品推薦結果。 您也可以傳送其他資料以啟用產品推薦[量度報告](workspace.md)。

1. 擷取產品推薦結果並在頁面上呈現這些結果。

您可以使用可用的SDK來執行這兩個動作，如以下工作流程所述。

1. [安裝](install-configure.md) [!DNL Product Recommendations]模組。

1. 安裝並使用[Adobe Commerce店面活動SDK](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/)以引發[行為活動](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#product-recommendations)。

   傳回[!DNL Product Recommendations]個結果所需的最小事件數：

   | 事件 | 類別 |
   |--- | ---|
   | `view` | 產品 |
   | `add-to-cart` | 產品 |
   | `place-order` | 簽出 |

   若要啟用[量度報告](workspace.md)，需要下列額外事件：

   | 事件 | 類別 |
   |--- | ---|
   | `impression-render` | recommendation-unit |
   | `view` | recommendation-unit |
   | `rec-click` | recommendation-unit |
   | `rec-add-to-cart-click` | recommendation-unit （如果Recommendations範本中出現「加入購物車」按鈕） |

1. 觸發事件時，請使用[Adobe Commerce Storefront事件收集器](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/)來處理事件並將它們傳送到Adobe Sensei。

1. 收集行為資料後，您可以在Admin中[建立](create.md) [!DNL Product Recommendations]。

1. 使用[Recommendations SDK](https://developer.adobe.com/commerce/services/product-recommendations/)擷取店面上的推薦單位。 SDK會傳回必要的產品資料以轉譯頁面上的推薦單位。

1. 瞭解如何使用[`recommendations` GraphQL查詢](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/)，傳回指定SKU的產品建議區塊相關資訊等。
