---
title: 安全性架構和資料流程
description: 瞭解Adobe Commerce as a Cloud Service的安全性架構和資料流程。
role: Admin, Developer, Leader
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案（Adobe管理的SaaS基礎結構）。"
TQID: 'https://experienceleague.adobe.com/2yK-VVec98nFH9LPpfSe4kQ2YvQr2yy3G0Rym5-HCbI'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: ef32511703a96b5f4db32d54229e9a7cbe961f12
workflow-type: tm+mt
source-wordcount: 387
ht-degree: 0%

---


# 安全性架構和資料流程

下列範例說明資料通常如何在[!DNL Adobe Commerce as a Cloud Service]中流動：

![Adobe Commerce as a Cloud Service資料流程圖](../assets/data-flow-1.png)

## 資料流程敘述

**步驟1**：購物者在其瀏覽器中鍵入商家店面的URL，這會將URL傳送至Commerce店面的內容傳遞網路（外部CDN）。

**步驟2**：如果已快取網站URL，Storefront CDN會將其傳回給購物者。 如果尚未快取（若這是第一個資源請求就可能發生），外部CDN會將購物者的請求轉送至內部CDN，並快取後續請求的回應。

**步驟2a**：如果要求是針對影像或視訊，則會傳送給[!DNL Product Visuals]以進行履行，並返回店面。

**步驟3**：如果網站URL快取在內部CDN上，則會從該快取傳回。 如果沒有，則會傳送至[!DNL API Mesh]，並為後續要求快取回應。

**步驟4**： [!DNL API Mesh]充當協調層，並決定要傳送要求給[!DNL Adobe Commerce as a Cloud Service]或第三方系統以履行要求。

>[!NOTE]
>
>[!DNL API Mesh]只有在您已自訂您的網狀架構時，才會傳送要求給協力廠商系統。

**步驟5**：傳送至[!DNL Adobe Commerce as a Cloud Service]的要求會通過Web應用程式防火牆(WAF)，以封鎖可疑或惡意的要求。 如果請求的URL快取在[!DNL Commerce] CDN上，則會從該快取中傳送。 如果未快取，則會從一或多個[!DNL Adobe Commerce as a Cloud Service]微服務（例如foundation、search和recommendations）傳回它，然後快取以供未來的請求使用。

**步驟5a**：如果要求傳送至協力廠商系統，回應將會傳回[!DNL API Mesh]。

**步驟5b**：如果要求進行付款處理，付款提供者會將iframe轉譯至店面，讓購物者安全地輸入信用卡資訊，並完成付款交易。

**步驟6**： [!DNL API Mesh]收到來自[!DNL Adobe Commerce as a Cloud Service]或協力廠商服務的回應後，這些回應就會拼接成統一的圖形，並傳回[!DNL Commerce Storefront]以服務購物者的請求。
