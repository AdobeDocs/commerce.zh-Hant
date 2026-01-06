---
title: '[!DNL Adobe Commerce as a Cloud Service]發行說明'
description: 瞭解 [!DNL Adobe Commerce as a Cloud Service]中的最新功能和改進專案。
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Developer, User, Leader
level: Beginner
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案(Adobe管理的SaaS基礎結構)。"
exl-id: cf06dec6-8d6b-413e-9977-df88373c188e
source-git-commit: 1ce3b6b6b94b1b4e94c0d34c081dec2884d7f0f8
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---

# 發行說明

下列發行說明包含[!DNL Adobe Commerce as a Cloud Service]的更新。 如需其他產品的發行資訊，請參閱[Adobe Commerce Optimizer](../optimizer/release-notes.md)或[Adobe Commerce內部部署與雲端上的Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-operations/release/notes/overview)。

[!DNL Adobe Commerce as a Cloud Service]包含最新版本的銷售服務、付款服務和擴充功能版本。 使用下列連結檢視各版本的發行說明：

* 服務
   * [目錄服務](../catalog-service/release-notes.md)
   * [即時搜尋](../live-search/release-notes.md)
   * [付款服務](../payment-services/release-notes.md)
   * [產品推薦](../product-recommendations/release-notes.md)
   * [SaaS資料匯出](../data-export/release-notes.md)
* 擴充性
   * [管理UI SDK](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/release-notes/)
   * [API網格](https://developer.adobe.com/graphql-mesh-gateway/mesh/release)
   * [個活動](https://developer.adobe.com/commerce/extensibility/events/release-notes/)
   * [Webhooks](https://developer.adobe.com/commerce/extensibility/webhooks/release-notes/)

## 2025年11月

>[!BEGINSHADEBOX]

### 增強功能

* [使用者管理](./user-management.md) — 已變更Admin Console中的&#x200B;**產品管理員**&#x200B;角色，以自動更新使用者對Commerce管理員的存取權。<!-- CCSAAS-3012 -->

* 新增使用[GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/uploads)和[REST](https://developer.adobe.com/commerce/webapi/rest/modules/s3-uploads)中的預先簽署URL，將可轉讓的報價附件以及與客戶和客戶地址相關的檔案和影像上傳和擷取到Amazon S3的功能。 透過REST，您還可以上傳類別影像。<!-- CCSAAS-3250 -->

* 已將`POST /V1/customers`和`PUT /V1/customers/{customerId}`端點新增至[REST API](https://developer.adobe.com/commerce/webapi/rest/reference/)，以建立和更新客戶。 這些端點需要管理員授權。<!-- CCSAAS-3112 -->

* 新增[`exchangeOtpForCustomerToken`突變](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/exchange-otp-customer-token/) (需要購物者的電子郵件地址和一次性密碼(OTP))，並接收交換的客戶權杖。 此突變通常用於客戶需要使用傳送至其電子郵件或電話的OTP進行驗證的情況。

* 如果在Admin的&#x200B;[!UICONTROL **存放區電子郵件地址**]&#x200B;設定畫面中定義的位址包含結尾為`example.com`的值，Commerce不會傳送電子郵件至此位址。 系統會改為記錄未傳送電子郵件。 <!-- CCSAAS-3533 -->

#### 自訂訂單屬性

* 管理員使用者現在可以直接從「管理員」面板的「訂單檢視」、「編輯」和「建立」畫面檢視和編輯[自訂訂單屬性](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing#custom-order-attributes)。 此增強功能可改善透過GraphQL建立的自訂訂單資料的管理。<!-- CEXT-5044 -->

>[!ENDSHADEBOX]
