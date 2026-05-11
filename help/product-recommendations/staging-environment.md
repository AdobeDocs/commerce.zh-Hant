---
title: 在中繼環境中測試
description: 瞭解如何在測試環境中使用生產環境中的 [!DNL Product Recommendations] 進行測試。
feature: Services, Recommendations, Staging
exl-id: 5b6d7615-6021-4419-98ea-006c8a299fe4
TQID: https://experienceleague.adobe.com/7e7e3T-vgkN-Pbqx6TwrBAWTEozhzS0h--tguOGe0yI
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 436
ht-degree: 0%

---

# 在中繼環境中測試

在將建議部署至生產環境之前，請在非生產環境中測試服務以確保一切都如預期般運作。

[!DNL Product Recommendations]根據從您的店面收集的[購物者行為資料](events.md)傳回產品。 不過，在非生產環境中，您可能沒有任何來自購物者的行為資料。 唯一可以在沒有行為資料的情況下測試的建議型別是`More like this`。 此建議型別不需要任何輸入資料，因為它使用直接內容相似度比對。

下列建議型別需要行為資料：

- 檢視次數最多
- 已檢視這個專案，已檢視那個專案
- 已購買此專案，已購買該專案

如何使用行為資料在非生產環境中測試建議？ 有幾個選項。

## 從生產環境擷取建議（建議）

Adobe Commerce可讓您從生產環境中擷取建議，並透過[切換](settings.md) SaaS資料空間而在非生產環境中預覽。

若要從生產環境擷取建議，您必須確定：

- Storefront資料收集在生產環境中[已設定並啟用](install-configure.md)。
- 您非生產環境中的目錄與生產環境中的目錄大致相同。 使用類似的目錄可確保建議單位中傳回的產品與生產環境中的產品非常類似。

## 在非生產環境中產生行為資料

1. 將`magento/product-recommendations`模組部署至目錄資料與您的生產目錄相似的非生產環境。

1. 在Admin中為[設定](../landing/saas.md#saas-configuration)使用其中一個非生產資料空間ID。

1. 在店面周圍按一下，自行產生資料，以模擬實際購物者的行為（或建立自動化指令碼）。 透過測試，您可在非生產環境中產生行為事件。 這些事件用於產生產品相關性，以支援建議。 為了進行測試，[!DNL Commerce]建議您與下列建議型別互動：

   - 檢視次數最多 — 只需要最少的輸入資料。 使用者必須檢視產品。
   - 已檢視這個專案，已檢視那個專案 — 需要多個使用者檢視多個產品。
   - 已購買此專案，已購買此專案 — 需要多位使用者購買多項產品。

### 警告

- 來自非生產[SaaS資料空間](../landing/saas.md#saas-configuration)的行為和目錄資料會識別隔離的環境，在其中產生的產品建議完全以關聯店面產生的行為資料為基礎。

- 因為您沒有大量的行為資料，所以用於計算產品關聯的輸入資料是稀疏的。 不過，這些資料仍會傳送至Sensei以電腦器學習模型，並根據此環境中產生的資料提供建議。
