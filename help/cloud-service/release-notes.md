---
title: '[!DNL Adobe Commerce as a Cloud Service]發行說明'
description: 瞭解 [!DNL Adobe Commerce as a Cloud Service]中的最新功能和改進專案。
feature-set: Commerce
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Developer, User, Leader
level: Beginner
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案（Adobe管理的SaaS基礎結構）。"
exl-id: cf06dec6-8d6b-413e-9977-df88373c188e
source-git-commit: 9d4192bae09fce4f08baf4b3e2826302667cd55f
workflow-type: tm+mt
source-wordcount: '2091'
ht-degree: 0%

---

# 發行說明

下列發行說明包含[!DNL Adobe Commerce as a Cloud Service]的更新。

>[!NOTE]
>
>如果您正在雲端基礎結構上使用Adobe Commerce內部部署或Adobe Commerce，請參閱[Adobe Commerce發行說明](https://experienceleague.adobe.com/zh-hant/docs/commerce-operations/release/notes/overview)。

## 2026年3月 — 發行說#2 {#latest}


[!BADGE 生產]{type=Neutral tooltip="列出的專案目前可在生產環境中使用。"}

<!-- [!BADGE Sandbox]{type=Caution tooltip="The items listed are currently only available in Sandbox environments. Adobe makes new releases available in Sandbox environments first to provide time to test upcoming changes before the release is available on Production environments."} -->

以下專案已於2026年3月24日發佈到生產環境。

>[!BEGINSHADEBOX]

### 使用一次性程式碼以客戶身分登入

管理員現在可以透過[和REST API產生客戶模擬的](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/customers/customer-accounts/manage/login-as-customer)一次性程式碼[!DNL Commerce Admin]。 可透過`generateCustomerToken`或`exchangeOtpForCustomerToken`個GraphQL變動，以一次性代碼交換客戶存取權杖，讓無密碼的「以客戶身分登入」流程適用於賣家協助的購物情境。<!-- ACCS-404 -->

如需使用API實作此功能的指引，請參閱[REST API](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/login-as-customer/)和[GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/generate-token/)檔案。

### 透過REST API管理禮品卡帳戶

[現在可以透過REST API建立、更新、刪除及查詢](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/gift-card-accounts/)禮卡帳戶。 此外，透過`/V1/import/json`端點提供JSON大量匯入支援，啟用協力廠商整合以程式設計方式同步禮品卡。<!-- ACCS-476 -->

### 透過REST API觸發異動電子郵件

新的REST API端點(`POST /V1/custom-email/send`)可讓您指定電子郵件範本ID、收件者電子郵件和範本變數，隨時[觸發異動電子郵件](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/custom-email/)。 此API支援巢狀陣列作為複雜電子郵件內容的範本變數。<!-- ACCS-325, ACCS-481 -->

### 訂閱跨處理序送貨取得費率webhook

`plugin.out_of_process_shipping_methods.api.shipping_rate_repository.get_rates` webhook現在可在[!DNL Adobe Commerce as a Cloud Service]的Admin Webhook清單中使用。 使用它來實作[自訂送貨方法](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/shipping-use-cases/#shipping-methods)。<!-- ACCS-478 -->

### 透過產品屬性上傳PDF和其他檔案

新的「檔案」[屬性輸入型別](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/catalog/product-attributes/attributes-input-types)可讓您建立屬性集，以便上傳檔案（例如PDF）至個別產品。 您可以瀏覽至&#x200B;[!UICONTROL **商店**] > [!UICONTROL **設定**] > [!UICONTROL _目錄_] > [!UICONTROL **產品檔案屬性**]，以設定允許的副檔名和最大檔案大小。<!-- ACCS-535, ACCS-565 -->

### 設定公司自訂屬性

管理員現在可以在[!DNL Commerce Admin]的公司編輯頁面上管理公司自訂屬性。 可從[!DNL Adobe Commerce as a Cloud Service]的管理員UI設定、儲存及驗證自訂屬性。

若要設定公司自訂屬性，請瀏覽至&#x200B;[!UICONTROL **客戶**] > [!UICONTROL **公司**]，並選取要開啟編輯頁面的公司。 然後選取&#x200B;[!UICONTROL **自訂屬性**]&#x200B;索引標籤以新增屬性。
<!-- ACCS-294 -->

### 透過GraphQL訂閱價格和股票警報

EDS店面現在使用[價格與庫存警示](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/inventory/configuration/product-alerts/alert-setup)。<!-- ACCS-334 -->

此外，還有數種新的GraphQL變動可供訂閱和取消訂閱價格與股票警示：

+++新的GraphQL變動

```graphql
mutation {
  subscribeProductAlertStock(input: { sku: "ADB111" }) {
    success
    message
  }
}
```

```graphql
mutation {
  unsubscribeProductAlertStock(input: { sku: "ADB111" }) {
    success
    message
  }
}
```

```graphql
mutation {
  unsubscribeProductAlertStockAll {
    success
    message
  }
}
```

```graphql
mutation {
  subscribeProductAlertPrice(input: { sku: "ADB112" }) {
    success
    message
  }
}
```

```graphql
mutation {
  unsubscribeProductAlertPrice(input: { sku: "ADB115" }) {
    success
    message
  }
}
```

```graphql
mutation {
  unsubscribeProductAlertPriceAll {
    success
    message
  }
}
```

+++

### 增強功能和錯誤修正

此版本中包括下列選取的增強功能、最佳化和錯誤修正：

* [!UICONTROL Sales] > [!UICONTROL View Orders]公司角色現在可如預期運作。<!-- ACCS-604 -->

* `last_login_at`客戶擴充功能屬性現在可透過REST API使用，可讓整合功能擷取每位客戶的最新登入日期。<!-- ACCS-555 -->

* 修正[!DNL AEM Assets]整合表單建議的問題。<!-- ACCS-209 -->

* 修正共用目錄格線上的大量公司指派和取消指派動作可能會導致錯誤的問題。<!-- CCSAAS-4614 -->

* 修正當相同的產品再次以不同的數量或自訂價格新增到購物車時，自訂購物車定價遭到覆寫的問題。<!-- ACCS-529 -->

* 請購單清單專案UID現在與購物車及願望清單專案UID一致。<!-- ACCS-349 -->

* 修正大型共用目錄可能發生的產品編輯頁面逾時問題。<!-- CCSAAS-4657 -->

* 重新啟用GET `/V1/directory/countries`和GET `/V1/directory/countries/:countryId` REST API端點以進行管理員整合，讓使用者端可查詢有效的國家/地區資料。<!-- ACCS-518 -->

* 修正使用者擁有大型共用目錄時，REST API中可能發生的逾時問題。<!-- ACCS-4657 -->

* 修正封鎖的B2B公司仍可新增產品至購物車的問題。<!-- ACCS-552 -->

* 如果「客戶」或「公司」網格中有大量資料，則無法再使用匯出按鈕來避免錯誤。<!-- ACCS-320 -->

* 修正附加檔案大小未正確顯示的問題。<!-- ACCS-566 -->

* 修正在[!DNL Commerce Admin]中建立和刪除「檔案」屬性型別的問題。<!-- ACCS-605, ACCS-606 -->

{{accs-release}}

>[!ENDSHADEBOX]


## 2026年3月 — 發行說#1

[!BADGE 生產]{type=Neutral tooltip="列出的專案目前可在生產環境中使用。"}

下列專案已於2026年3月9日發佈到[!DNL Adobe Commerce as a Cloud Service]的生產環境。

>[!BEGINSHADEBOX]

### App Builder AI編碼工具和教學課程

您現在可以使用[AI編碼開發人員工具](./migration/coding-tools.md)來建立新的[!DNL App Builder]應用程式，並將現有的[!DNL Adobe Commerce] PHP擴充功能轉換成[!DNL App Builder]應用程式。 下列教學課程可示範如何使用工具：

* [教學課程必要條件](./tutorials/tutorial-prerequisites.md)
* [評等擴充功能教學課程](./tutorials/ratings-extension.md)
* [送貨方法擴充功能教學課程](./tutorials/shipping-method-extension.md)

### 透過管理員存取App Builder應用程式管理

[!DNL Commerce Admin]現在包含連結至[應用程式管理](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"}的功能表專案，此統一殼層用於管理與Commerce執行個體相關聯的[!DNL App Builder]個應用程式。 這項新增功能由最新的Admin UI SDK更新提供技術支援。<!-- CEXT-5755 -->

### 請求實體建立限制變更

網站、商店和商店檢視次數限制先前上限為50次。 您現在可以提交[支援要求](https://experienceleague.adobe.com/home?lang=zh-Hant&support-tab=home#support)來修改這些限制（如有必要）。<!-- ACCS-398 -->

### 使用結構化錯誤碼自訂店面驗證訊息

[`generateCustomerToken` GraphQL突變](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/generate-token/){target="_blank"}現在會連同錯誤訊息傳回輸入的錯誤碼，讓儲存區域能夠依據失敗原因顯示特定的UI訊息。 可用的錯誤碼包括： `CUSTOMER_MISSING_EMAIL`、`CUSTOMER_MISSING_PASSWORD`、`CUSTOMER_SIGN_IN_INCORRECT_OR_LOCKED`、`CUSTOMER_ACCOUNT_NOT_CONFIRMED`和`CUSTOMER_GENERIC_ERROR`。<!-- ACCS-301 -->

### 傳送購物車和願望清單閒置的自動電子郵件提醒

[電子郵件提醒模組](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/marketing/communications/email-reminders/email-reminder-rules) (`Magento_Reminder`)目前在[!DNL Adobe Commerce as a Cloud Service]中啟用，可讓商家建立自動提醒規則，以根據購物車和願望清單閒置狀態觸發傳送給客戶的電子郵件。<!-- CCSAAS-4597 -->

### 訂閱類別刪除事件webhook

`observer.catalog_category_delete_before` webhook現在可在[!DNL Adobe Commerce as a Cloud Service]中使用。 在刪除類別之前使用它來執行邏輯。<!-- CEXT-5862 -->

### 追蹤透過已註冊電子郵件下單的訪客訂單

新的選用商店層級設定可讓客戶[追蹤他們下單的客服訂單](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/stores-sales/point-of-purchase/checkout/checkout-guest#allow-guest-order-access-for-registered-emails) （若訂單使用的電子郵件地址符合註冊的客戶帳戶）。<!-- ACCS-289 -->

### 增強功能和錯誤修正

此版本中包括下列選取的增強功能、最佳化和錯誤修正：

* 修正某些組織管理員可能無每個租使用者權利而錯誤存取租使用者例項的問題。<!-- ACCS-335 -->

* 修正變更共用目錄時，可能會將使用者登出[!DNL Commerce Admin]的問題。<!-- ACCS-318 -->

* 修正造成部分Webhook欄位在[!DNL Commerce Admin] UI中顯示不正確的問題。<!-- CEXT-5874 -->

{{accs-release}}

>[!ENDSHADEBOX]

## 2026年2月 — 發行說#2

[!BADGE 生產]{type=Neutral tooltip="列出的專案目前可在生產環境中使用。"}

下列專案已於2026年2月24日發佈到[!DNL Adobe Commerce as a Cloud Service]的生產環境。

>[!BEGINSHADEBOX]

### 使用商務事件傳送內容欄位

[!DNL Adobe Commerce as a Cloud Service]現在在事件裝載中支援[內容欄位](https://developer.adobe.com/commerce/extensibility/events/context-fields/)，可讓您加入預設不屬於事件的資料。<!-- CEXT-5713 -->

### 使用新的webhook訂閱報價專案儲存事件

`observer.sales_quote_item_save_before` webhook現在可在[!DNL Adobe Commerce as a Cloud Service]中使用。 在儲存報價專案之前，使用它來執行邏輯。<!-- ACCS-346 -->

### 增強功能和錯誤修正

此版本中包括下列選取的增強功能、最佳化和錯誤修正：

* 修正可能導致[!DNL Commerce Admin]產品清單顯示問題的錯誤。 產品清單現在會限製為改善效能而顯示的共用目錄數量。<!-- CCSAAS-1242 -->

* 修正無法新增自訂禮品卡到購物車的GraphQL錯誤。<!-- ACCS-313 -->

{{accs-release}}

>[!ENDSHADEBOX]

## 2026年2月 — 發行說#1

[!BADGE 生產]{type=Neutral tooltip="列出的專案目前可在生產環境中使用。"}

下列專案已於2026年2月10日發佈到[!DNL Adobe Commerce as a Cloud Service]的生產環境。

>[!BEGINSHADEBOX]

### 自訂送貨方法並檢視管理員報表

已對[!DNL Commerce Admin]進行下列增強功能：

* 增強處理序外[出貨webhook裝載](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/shipping-use-cases/#payload)，以包含出貨地址自訂屬性。 這項變更可讓商家實作自訂送貨方法。<!-- ACCS-235 -->

* 已新增管理員報告的存取權，包括[客戶](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/start/reporting/customer-reports)、[行銷](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/start/reporting/marketing-reports)、[產品](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/start/reporting/product-reports)和[銷售](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/start/reporting/sales-reports)的報告。<!-- CCSAAS-3085 -->

>[!NOTE]
>
>在[!DNL Adobe Commerce as a Cloud Service]中無法使用的報告僅標籤為PaaS （僅[!BADGE PaaS]{type=Informative url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案（Adobe管理的PaaS基礎結構）和內部部署專案的Adobe Commerce 。"}）。

### 透過REST API擷取自訂商業發票金額

Invoice API現在支援使用擴充功能屬性的[自訂擷取金額](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/stores-sales/order-management/invoices#custom-capture-amounts)。<!-- ACCS-186, ACCS-197, ACCS-143 -->

>[!NOTE]
>
>由於法律限制，自訂擷取金額僅適用於北美(NA)地區和其他允許付款超額擷取的地區。

### 增強功能和錯誤修正

此版本中包括下列選取的增強功能、最佳化和錯誤修正：

* 修正抵用券格線篩選條件，以顯示透過API或匯入建立的所有自訂抵用券。<!-- CCSAAS-4509 -->

* 修正[!DNL Storefront Compatibility B2B Package]中`setNegotiableQuoteShippingAddress`突變未將手動輸入的地址儲存至客戶通訊錄的問題，即使`save_in_address_book`設定為`true`亦然。<!-- LYNX-1031 -->

<!-- The above change will also be covered by the B2B changelog published on February 13, 2026. -->

* 解決由於與資產角色相關的自訂屬性中[!DNL Edge Delivery Services]值損毀，`no_selection`中無法正確顯示產品影像的問題。<!-- ACAP-1206 -->

* 解決具有空名字或姓氏值的同盟使用者帳戶無法存取Commerce管理員的問題。<!-- ACCS-200 -->

* 簡化資產選擇器的設定，自動提供區域特定的IMS使用者端ID。 商戶不再需要提交支援票證來設定資產選擇器，以將產品類別影像與資產對應。 系統現在會根據Commerce地區，自動使用專屬的IMS使用者端ID。<!-- ACCS-175 -->

* 各種效能和最佳化改善專案。<!-- CCSAAS-4485, CCSAAS-4497, ACCS-196 -->

{{accs-release}}

>[!ENDSHADEBOX]

## 2026年1月

[!BADGE 生產]{type=Neutral tooltip="列出的專案目前可在生產環境中使用。"}

下列專案已於2026年1月20日發佈到[!DNL Adobe Commerce as a Cloud Service]的生產環境。

>[!BEGINSHADEBOX]

### B2B下拉式清單

已對B2B下拉式元件進行下列變更：

* [!DNL Commerce Storefront on Edge Delivery Services]現在包含[B2B放置元件](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/?lang=zh-Hant)。 下列B2B下拉式清單現已可供使用：

   * **[公司管理](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/company-management/?lang=zh-Hant)** — 啟用Adobe Commerce店面的公司設定檔管理和角色型許可權。
   * **[公司切換器](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/company-switcher/?lang=zh-Hant)** — 提供使用者介面元件，讓使用者可在相關聯的多個公司之間切換。
   * **[採購單](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/purchase-order/?lang=zh-Hant)** — 管理B2B交易的採購單工作流程、核准規則和採購單歷史記錄。
   * **[報價管理](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/quote-management/?lang=zh-Hant)** — 針對具有報價請求、議價及核准工作流程的B2B客戶，啟用可協商的報價。
   * **[請購單清單](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/requisition-list/?lang=zh-Hant)** — 提供建立和管理重複購買及大量訂購的請購單清單的工具。

* 已發行B2B店面相容性套件。 此套件增強了[!DNL Adobe Commerce] B2B GraphQL結構描述，以協助改善B2B系統的開發。

<!-- 
* [!DNL Commerce Storefront on Edge Delivery Services] now includes [B2B drop-in components](http://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/?lang=zh-Hant). For a complete list of available B2B drop-in blocks, refer to the [storefront documentation](http://experienceleague.adobe.com/developer/commerce/storefront/merchants/b2b-commerce-blocks/).

* Released the [B2B Storefront Compatibility Package](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility-b2b/?lang=zh-Hant). This package enhances the [!DNL Adobe Commerce] B2B GraphQL schema to help improve development on B2B systems. -->

### 外部送貨追蹤器的可點按連結

透過[啟用自訂追蹤URL](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/stores-sales/delivery/shipping-settings#shipment-tracking-urls)，將購物者電子郵件中包含的出貨追蹤號碼從純文字轉換為可點按的連結。 USPS、UPS、FedEx和DHL支援此功能。<!-- See PR #716 in commerce-admin -->

### Google reCAPTCHA企業支援

[!DNL Adobe Commerce as a Cloud Service]個店面現在支援[reCAPTCHA Enterprise](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/systems/security/captcha/security-google-recaptcha-enterprise)。 此功能透過使用適應性風險分析和機器學習來提供進階機器人保護，以便準確區分人類使用者與自動化機器人。 它可加強網站安全性、防止詐騙活動，並減少垃圾郵件和濫用，以維持受信任的購物體驗。<!-- CCSAAS-4242 -->

### 特定執行個體的管理員存取權

您現在可以[將使用者存取權](./user-management.md#add-users)指派給Admin Console中的個別[!DNL Adobe Commerce as a Cloud Service]執行個體。<!-- CCSAAS-4337 --><!-- See PR #332 -->

### 可觀察性

透過[!DNL App Builder]，您可以透過[!DNL Adobe Commerce as a Cloud Service]OpenTelemetry可觀察性[更深入瞭解您的](https://developer.adobe.com/commerce/extensibility/observability/)執行個體，現在可自動使用。 OpenTelemetry提供量度、日誌和追蹤，協助您監控效能、更快地疑難排解問題，以及最佳化店面。 此功能可讓您主動深入分析系統健康狀況，並提升客戶的可靠性。

>[!NOTE]
>
>OpenTelemetry可觀察性需要使用[!DNL App Builder]或其他處理序外擴充(OOPE)方案。

### 型錄價格規則的層級定價

您現在可以使用[目錄價格規則](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/catalog/products/pricing/product-price-tier#enable-tier-pricing-for-catalog-price-rules)，將階層式定價折扣與目錄規則折扣結合。 此增強功能可讓您建立更具活力和競爭力的定價策略，在獎勵大宗購買的同時套用促銷折扣。 如此可增加吸引客戶、增加訂單價值及促進轉換的彈性。<!-- See PR #708 in commerce-admin -->

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

* 新增使用[GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/uploads)和[REST](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/s3-uploads)中的預先簽署URL，將可轉讓的報價附件以及與客戶和客戶地址相關的檔案和影像上傳和擷取到Amazon S3的功能。 透過REST，您還可以上傳類別影像。<!-- CCSAAS-3250 -->

* 已將`POST /V1/customers`和`PUT /V1/customers/{customerId}`端點新增至[REST API](https://developer.adobe.com/commerce/webapi/rest/reference/)，以建立和更新客戶。 這些端點需要IMS授權。<!-- CCSAAS-3112 -->

* 新增[`exchangeOtpForCustomerToken`突變](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/exchange-otp-customer-token/) (需要購物者的電子郵件地址和一次性密碼(OTP))，並接收交換的客戶權杖。 此突變通常用於客戶需要使用傳送至其電子郵件或電話的OTP進行驗證的情況。

* 如果在Admin的&#x200B;[!UICONTROL **存放區電子郵件地址**]&#x200B;設定畫面中定義的位址包含結尾為`example.com`的值，Commerce不會傳送電子郵件至此位址。 系統會改為記錄未傳送電子郵件。 <!-- CCSAAS-3533 -->

#### 自訂訂單屬性

* 管理員使用者現在可以直接從「管理員」面板的「訂單檢視」、「編輯」和「建立」畫面檢視和編輯[自訂訂單屬性](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/stores-sales/order-management/orders/order-processing#custom-order-attributes)。 此增強功能可改善透過GraphQL建立的自訂訂單資料的管理。<!-- CEXT-5044 -->

>[!ENDSHADEBOX]
