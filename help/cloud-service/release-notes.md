---
title: '[!DNL Adobe Commerce as a Cloud Service]發行說明'
description: 瞭解 [!DNL Adobe Commerce as a Cloud Service]中的最新功能和改進專案。
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Developer, User, Leader
level: Beginner
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案(Adobe管理的SaaS基礎結構)。"
exl-id: cf06dec6-8d6b-413e-9977-df88373c188e
source-git-commit: b8a2ea53f686cc92e380afeb39c467338f91f991
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 0%

---

# 發行說明

下列發行說明包含[!DNL Adobe Commerce as a Cloud Service]的更新。

>[!NOTE]
>
>如果您正在雲端基礎結構上使用Adobe Commerce內部部署或Adobe Commerce，請參閱[Adobe Commerce發行說明](https://experienceleague.adobe.com/en/docs/commerce-operations/release/notes/overview)。

## 2026年1月 {#latest}

[!BADGE 生產]{type=Neutral tooltip="列出的專案目前可在生產環境中使用。"}

下列專案已於2026年1月20日發佈到[!DNL Adobe Commerce as a Cloud Service]的生產環境。

>[!BEGINSHADEBOX]

### 驗證增強功能

Adobe IMS管理員驗證的存取權杖現在只能透過POST請求接受。<!-- CCSAAS-4421 -->

### B2B下拉式清單

已對B2B下拉式元件進行下列變更：

* [!DNL Commerce Storefront on Edge Delivery Services]現在包含[B2B放置元件](http://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/)。 下列B2B下拉式清單現已可供使用：

   * **公司管理** — 啟用Adobe Commerce店面的公司設定檔管理和角色型許可權。
   * **公司切換器** — 提供使用者介面元件，讓使用者可在相關聯的多個公司之間切換。
   * **採購單** — 管理B2B交易的採購單工作流程、核准規則和採購單歷史記錄。
   * **報價管理** — 針對具有報價請求、議價及核准工作流程的B2B客戶，啟用可協商的報價。
   * **請購單清單** — 提供建立和管理重複購買及大量訂購的請購單清單的工具。

     >[!NOTE]
     >
     >此功能提升至生產環境時，將提供B2B下拉式元件的詳細檔案。

* 已發行B2B店面相容性套件。 此套件增強了[!DNL Adobe Commerce] B2B GraphQL結構描述，以協助改善B2B系統的開發。

<!-- 
* [!DNL Commerce Storefront on Edge Delivery Services] now includes [B2B drop-in components](http://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/). For a complete list of available B2B drop-in blocks, refer to the [storefront documentation](http://experienceleague.adobe.com/developer/commerce/storefront/merchants/b2b-commerce-blocks/).

* Released the [B2B Storefront Compatibility Package](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility-b2b/). This package enhances the [!DNL Adobe Commerce] B2B GraphQL schema to help improve development on B2B systems. -->

### 外部送貨追蹤器的可點按連結

透過[啟用自訂追蹤URL](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/delivery/shipping-settings#shipment-tracking-urls)，將購物者電子郵件中包含的出貨追蹤號碼從純文字轉換為可點按的連結。 USPS、UPS、FedEx和DHL支援此功能。<!-- See PR #716 in commerce-admin -->

### Google reCAPTCHA企業支援

[!DNL Adobe Commerce as a Cloud Service]個店面現在支援[reCAPTCHA Enterprise](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/captcha/security-google-recaptcha-enterprise)。 此功能透過使用適應性風險分析和機器學習來提供進階機器人保護，以便準確區分人類使用者與自動化機器人。 它可加強網站安全性、防止詐騙活動，並減少垃圾郵件和濫用，以維持受信任的購物體驗。<!-- CCSAAS-4242 -->

### 特定執行個體的管理員存取權

您現在可以[將使用者存取權](./user-management.md#add-users)指派給Admin Console中的個別[!DNL Adobe Commerce as a Cloud Service]執行個體。<!-- CCSAAS-4337 --><!-- See PR #332 -->

### 可觀察性

透過[!DNL Adobe Commerce as a Cloud Service]OpenTelemetry可觀察性[，更深入瞭解您的](https://developer.adobe.com/commerce/extensibility/observability/)執行個體，現在可自動使用。 OpenTelemetry提供量度、日誌和追蹤，協助您監控效能、更快地疑難排解問題，以及最佳化店面。 此功能可讓您主動深入分析系統健康狀況，並提升客戶的可靠性。

### 型錄價格規則的層級定價

您現在可以使用[目錄價格規則](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/pricing/product-price-tier#enable-tier-pricing-for-catalog-price-rules)，將階層式定價折扣與目錄規則折扣結合。 此增強功能可讓您建立更具活力和競爭力的定價策略，獎勵大宗採購，同時套用促銷折扣。 如此可增加吸引客戶、增加訂單價值及促進轉換的彈性。<!-- See PR #708 in commerce-admin -->

### 增強功能和錯誤修正

此版本中包含下列已選取的增強功能、最佳化和錯誤修正：

* 解決上傳檔案至S3時可能發生的錯誤。<!-- CCSAAS-4189 -->

* 解決登入Commerce Admin或存取REST API時可能出現的`User is not entitled to access this instance`錯誤。<!-- CCSAAS-4324 -->

* 修正從Newsletter範本格線預覽或佇列新聞稿時發生的錯誤。<!-- CCSAAS-4398 -->

* 修正按一下管理控制面板上的`404`重新載入資料&#x200B;[!UICONTROL **按鈕時所發生的**]&#x200B;錯誤。<!-- CCSAAS-4468 -->

* 解決啟用[!DNL AEM Assets integration]且產品具有影像時，無法透過REST API更新產品自訂屬性的問題。<!-- ACAP-1178 -->

* 各種效能和最佳化改進。<!-- CCSAAS-4255 --><!-- CCSAAS-4233 --><!-- CCSAAS-4220 --><!-- CCSAAS-4252 --><!-- CCSAAS-4330 --><!-- CCSAAS-3669 --><!-- CCSAAS-4462 -->

{{accs-release}}

>[!ENDSHADEBOX]

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
