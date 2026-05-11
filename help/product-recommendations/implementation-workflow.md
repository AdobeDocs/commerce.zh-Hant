---
title: 實作工作流程
description: 瞭解在您的店面成功實作 [!DNL Product Recommendations] 的步驟。
exl-id: 4a784d04-8be6-473f-afb3-264af06c850a
TQID: https://experienceleague.adobe.com/-nvORlxBNwoCcZb6s-OvaX8TtIh28Q-fjeUxsDXpe9E
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: c4147b6e-073b-4d3c-9ab1-d60f2f4434efid: d3cdead0-685a-4489-9250-4bb709942f66id: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 563
ht-degree: 0%

---

# 實作工作流程

[!DNL Product Recommendations]同時使用行為和目錄資料：

- 行為 — 購物者在您網站上的參與度資料，例如產品檢視、新增到購物車的專案以及購買。 Adobe Commerce和Adobe AI不會收集個人識別資訊。

- 目錄 — 產品中繼資料，例如名稱、價格和可用性。

安裝`magento/product-recommendations module`時，Adobe AI會彙總行為和目錄資料，並為每個建議型別建立[!DNL Product Recommendations]。 然後[!DNL Product Recommendations]服務會將這些建議部署至您的店面。 為協助您在店面實作產品推薦，請使用以下工作流程：

>[!NOTE]
>
> 如果您的店面是使用PWA Studio實作，請參閱[PWA檔案](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/)。 如果您使用自訂前端技術，例如React或Vue JS，請瞭解如何[整合](headless.md) [!DNL Product Recommendations]到您的Headless店面。

## 工作流程

1. **將資料收集部署至生產環境**

   部署[!DNL Product Recommendations]需要兩個主要[資料來源](type.md)：目錄和行為。 由於生產是擷取和分析購物者動作的唯一環境，因此請儘早在生產上開始收集資料。 [瞭解](events.md) Adobe AI如何訓練產生更高品質建議的機器學習模型。 額外好處是，當您開始收集生產環境的行為資料時，可以在非生產環境中作業時，根據此生產資料[擷取建議](staging-environment.md#fetch-recommendations-from-production-environment-recommended)。 接著，您可以測試和實驗不同的建議，這些建議是根據實際生產中收集的購物者資料計算而得。

   若要將資料收集部署至生產環境，您必須[藉由提供[API金鑰](https://experienceleague.adobe.com/docs/commerce/user-guides/integration-services/saas.html)來](install-configure.md)安裝並設定[!DNL Product Recommendations]模組。

   >[!TIP]
   >
   > 部署資料彙集不會變更您的店面外觀或購物者的體驗。 只有建立和部署建議單位，才會改變店面的客戶體驗。 請務必先在非生產環境中測試，然後再部署到生產環境。 此外，在您自訂範本之前，請勿建立建議單位。 請參閱下一步。

1. **自訂範本以符合您的樣式**

   您的店面代表您的品牌，因此請務必修改產品推薦範本以符合您的網站主題。

   >[!TIP]
   >
   > 透過自訂範本，您可以指定樣式表、覆寫建議單位在頁面上的顯示位置等等。

   請參閱開發人員檔案中的[自訂](https://experienceleague.adobe.com/docs/commerce/product-recommendations/developer/customize.html)，瞭解如何完成此步驟。

1. **在您的非生產環境中測試建議**

   在將技術部署到生產環境之前，最好的做法永遠是在非生產環境中測試新技術。 在非生產環境中測試建議可讓您使用不同的建議單位型別、定位和頁面。 您可以在非生產環境中測試時，根據生產上已收集的行為資料提取建議，讓建議結果以實際客戶的購物行為為基礎。

   >[!TIP]
   >
   > 確認您的非生產環境目錄與生產環境目錄大致相同。 使用類似的目錄可確保建議單位中傳回的產品與生產時的產品非常類似。

   請參閱從生產環境擷取[1}行為資料，以瞭解如何完成此步驟。](staging-environment.md)

1. **建立建議並部署至您的生產店面**

   現在您已在生產環境中部署行為資料收集、修改產品建議範本，以及使用實際購物者行為來測試建議，您已準備好將所有程式碼提升至生產環境，並[建立](create.md)即時產品建議。
