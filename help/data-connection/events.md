---
title: 行為事件
description: 瞭解每個行為事件擷取哪些資料。
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: bcabccc9-8a2e-4045-9306-1d999bb75624
source-git-commit: 1750aee715946d3a871e021cbbee687f54d1ff09
workflow-type: tm+mt
source-wordcount: '4528'
ht-degree: 0%

---

# [!DNL Data Connection]行為事件

以下列出您在安裝[!DNL Data Connection]擴充功能時可用的Commerce行為事件。 這些事件收集的資料會傳送至Adobe Experience Platform。 您也可以建立[自訂事件](custom-events.md)，以立即收集未提供的其他資料。

除了下列事件收集的資料之外，您也會取得Adobe Experience Platform Web SDK提供的[其他資料](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/automatic-information.html)。

行為事件會在購物者瀏覽您的網站時，從他們那裡收集匿名的行為資料。 您可以使用這些事件收集到的資料，建立以特定購物者集為目標的促銷活動和行銷活動。

>[!NOTE]
>
>所有行為事件都包含[`identityMap`](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/identitymap.html)欄位，其中包括購物者的電子郵件地址（可用時）和ECID。

## 店面活動

店面事件會從購物者在網站上的互動擷取資料，並包含[`addToCart`](#addtocart)、[`pageView`](#pageview)、[`createAccount`](#createaccount)、[`editAccount`](#editaccount)、[`startCheckout`](#startcheckout)、[`completeCheckout`](#completecheckout)、[`signIn`](#signin)、[`signOut`](#signout)等事件。 店面事件僅適用於簡單且可設定的產品。

### addToCart

| 說明 | XDM事件名稱 |
|---|---|
| 當產品新增到購物車或購物車中的產品數量增加時觸發。 | `commerce.productListAdds` |

#### 從addToCart收集的資料

下表說明為此事件收集的資料。

| 欄位 | 說明 |
|---|---|
| `channel` | 包含資料來源的相關資訊。 `_id`和`_type`都包含[名稱空間值](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html)。 |
| `channel._id` | 管道的唯一識別碼，例如`"https://ns.adobe.com/xdm/channels/web"`。 |
| `channel._type` | 識別管道資料的來源，例如`"https://ns.adobe.com/xdm/channel-types/web"`。 |
| `commerce.productListAdds` | 表示是否已將產品新增至購物車。 值`1`表示已新增產品。 |
| `commerce.cart.cartID` | 識別客戶購物車的唯一ID。 |
| `commerce.commerceScope` | 表示事件發生位置（商店檢視、商店、網站等）。 |
| `commerce.commerceScope.environmentID` | 環境識別碼。 32位數的英數字元ID，以連字型大小分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代碼。 每個網站可以有許多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的存放區檢視代碼。 每個商店可以有多個商店檢視。 |
| `commerce.commerceScope.websiteCode` | 不重複網站代碼。 一個環境中可以有許多網站。 |
| `productListItems` | 加入購物車的一系列產品。 |
| `productListItems.SKU` | 庫存單位。 產品的唯一識別碼。 |
| `productListItems.name` | 產品的顯示名稱或人類看得懂的名稱。 |
| `productListItems.priceTotal` | 產品明細專案的總價。 |
| `productListItems.quantity` | 購物車中的產品件數。 |
| `productListItems.discountAmount` | 表示套用的折扣金額。 |
| `productListItems.currencyCode` | 已使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)貨幣代碼，例如`USD`或`EUR`。 |
| `productListItems.productImageUrl` | 產品的主要影像URL。 |
| `productListItems.selectedOptions` | 用於可設定產品的欄位。 |
| `productListItems.selectedOptions.attribute` | 識別可設定產品的屬性，例如`size`或`color`。 |
| `productListItems.selectedOptions.value` | 識別屬性的值，例如`small`或`black`。 |

### openCart

| 說明 | XDM事件名稱 |
|---|---|
| 建立新購物車時觸發，亦即將產品新增至空白購物車時。 | `commerce.productListOpens` |

#### 從openCart收集的資料

下表說明為此事件收集的資料。

| 欄位 | 說明 |
|---|---|
| `channel` | 包含資料來源的相關資訊。 `_id`和`_type`都包含[名稱空間值](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html)。 |
| `channel._id` | 管道的唯一識別碼，例如`"https://ns.adobe.com/xdm/channels/web"`。 |
| `channel._type` | 識別管道資料的來源，例如`"https://ns.adobe.com/xdm/channel-types/web"`。 |
| `commerce.productListOpens` | 指出是否已建立購物車。 值`1`表示已建立購物車。 |
| `commerce.cart.cartID` | 識別客戶購物車的唯一ID。 |
| `commerce.commerceScope` | 表示事件發生位置（商店檢視、商店、網站等）。 |
| `commerce.commerceScope.environmentID` | 環境識別碼。 32位數的英數字元ID，以連字型大小分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代碼。 每個網站可以有許多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的存放區檢視代碼。 每個商店可以有多個商店檢視。 |
| `commerce.commerceScope.websiteCode` | 不重複網站代碼。 一個環境中可以有許多網站。 |
| `productListItems` | 加入購物車的一系列產品。 |
| `productListItems.SKU` | 庫存單位。 產品的唯一識別碼。 |
| `productListItems.name` | 產品的顯示名稱或人類看得懂的名稱。 |
| `productListItems.priceTotal` | 產品明細專案的總價。 |
| `productListItems.quantity` | 購物車中的產品件數。 |
| `productListItems.discountAmount` | 表示套用的折扣金額。 |
| `productListItems.currencyCode` | 已使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)貨幣代碼，例如`USD`或`EUR`。 |
| `productListItems.productImageUrl` | 產品的主要影像URL。 |
| `productListItems.selectedOptions` | 用於可設定產品的欄位。 |
| `productListItems.selectedOptions.attribute` | 識別可設定產品的屬性，例如`size`或`color`。 |
| `productListItems.selectedOptions.value` | 識別屬性的值，例如`small`或`black`。 |

### removeFromCart

| 說明 | XDM事件名稱 |
|---|---|
| 每次移除產品或每次購物車中的產品數量減少時觸發。 | `commerce.productListRemovals` |

#### 從removeFromCart收集的資料

下表說明為此事件收集的資料。

| 欄位 | 說明 |
|---|---|
| `channel` | 包含資料來源的相關資訊。 `_id`和`_type`都包含[名稱空間值](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html)。 |
| `channel._id` | 管道的唯一識別碼，例如`"https://ns.adobe.com/xdm/channels/web"`。 |
| `channel._type` | 識別管道資料的來源，例如`"https://ns.adobe.com/xdm/channel-types/web"`。 |
| `commerce.productListRemovals` | 表示產品是否已從購物車移除。 值`1`表示產品已從購物車中移除。 |
| `commerce.cart.cartID` | 識別客戶購物車的唯一ID。 |
| `commerce.commerceScope` | 表示事件發生位置（商店檢視、商店、網站等）。 |
| `commerce.commerceScope.environmentID` | 環境識別碼。 32位數的英數字元ID，以連字型大小分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代碼。 每個網站可以有許多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的存放區檢視代碼。 每個商店可以有多個商店檢視。 |
| `commerce.commerceScope.websiteCode` | 不重複網站代碼。 一個環境中可以有許多網站。 |
| `productListItems` | 加入購物車的一系列產品。 |
| `productListItems.SKU` | 庫存單位。 產品的唯一識別碼。 |
| `productListItems.name` | 產品的顯示名稱或人類看得懂的名稱。 |
| `productListItems.priceTotal` | 產品明細專案的總價。 |
| `productListItems.quantity` | 購物車中的產品件數。 |
| `productListItems.discountAmount` | 表示套用的折扣金額。 |
| `productListItems.currencyCode` | 已使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)貨幣代碼，例如`USD`或`EUR`。 |
| `productListItems.productImageUrl` | 產品的主要影像URL。 |
| `productListItems.selectedOptions` | 用於可設定產品的欄位。 |
| `productListItems.selectedOptions.attribute` | 識別可設定產品的屬性，例如`size`或`color`。 |
| `productListItems.selectedOptions.value` | 識別屬性的值，例如`small`或`black`。 |

### shoppingCartView

| 說明 | XDM事件名稱 |
|---|---|
| 任何購物車頁面載入時觸發。 | `commerce.productListViews` |

#### 從shoppingCartView收集的資料

下表說明為此事件收集的資料。

| 欄位 | 說明 |
|---|---|
| `channel` | 包含資料來源的相關資訊。 `_id`和`_type`都包含[名稱空間值](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html)。 |
| `channel._id` | 管道的唯一識別碼，例如`"https://ns.adobe.com/xdm/channels/web"`。 |
| `channel._type` | 識別管道資料的來源，例如`"https://ns.adobe.com/xdm/channel-types/web"`。 |
| `commerce.productListViews` | 表示是否已檢視產品清單。 |
| `commerce.cart.cartID` | 識別客戶購物車的唯一ID。 |
| `commerce.commerceScope` | 表示事件發生位置（商店檢視、商店、網站等）。 |
| `commerce.commerceScope.environmentID` | 環境識別碼。 32位數的英數字元ID，以連字型大小分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代碼。 每個網站可以有許多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的存放區檢視代碼。 每個商店可以有多個商店檢視。 |
| `commerce.commerceScope.websiteCode` | 不重複網站代碼。 一個環境中可以有許多網站。 |
| `commerce.order` | 包含一或多個產品的擱置訂單相關資訊。 |
| `commerce.order.discountAmount` | 表示套用至整張訂單的折扣金額。 |
| `productListItems` | 加入購物車的一系列產品。 |
| `productListItems.SKU` | 庫存單位。 產品的唯一識別碼。 |
| `productListItems.name` | 產品的顯示名稱或人類看得懂的名稱。 |
| `productListItems.priceTotal` | 產品明細專案的總價。 |
| `productListItems.quantity` | 購物車中的產品件數。 |
| `productListItems.discountAmount` | 表示套用的折扣金額。 |
| `productListItems.currencyCode` | 已使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)貨幣代碼，例如`USD`或`EUR`。 |
| `productListItems.productImageUrl` | 產品的主要影像URL。 |
| `productListItems.selectedOptions` | 用於可設定產品的欄位。 |
| `productListItems.selectedOptions.attribute` | 識別可設定產品的屬性，例如`size`或`color`。 |
| `productListItems.selectedOptions.value` | 識別屬性的值，例如`small`或`black`。 |

### pageView

| 說明 | XDM事件名稱 |
|---|---|
| 任何頁面載入時觸發。 | `web.webpagedetails.pageViews` |

#### 從pageView收集的資料

下表說明為此事件收集的資料。

| 欄位 | 說明 |
|---|---|
| `channel` | 包含資料來源的相關資訊。 `_id`和`_type`都包含[名稱空間值](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html)。 |
| `channel._id` | 管道的唯一識別碼，例如`"https://ns.adobe.com/xdm/channels/web"`。 |
| `channel._type` | 識別管道資料的來源，例如`"https://ns.adobe.com/xdm/channel-types/web"`。 |
| `web.webPageDetails.pageViews` | 指出是否已載入頁面。 `value`的`1`表示頁面已載入。 |
| `web.webPageDetails.URL` | 網頁的規範或一般URL。 這可能是用來存取頁面的實際URL，將使用`Web Link`來記錄。 |
| `web.webPageDetails.name` | 網頁的規範名稱。 此名稱不一定是頁面標題或直接與頁面內容相關聯，但用於整理網站頁面以進行分類。 |
| `web.webReferrer.URL` | 購物者在點按您網站的連結前所造訪的網頁的URL。 |
| `commerce.commerceScope` | 表示事件發生位置（商店檢視、商店、網站等）。 |
| `commerce.commerceScope.environmentID` | 環境識別碼。 32位數的英數字元ID，以連字型大小分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代碼。 每個網站可以有許多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的存放區檢視代碼。 每個商店可以有多個商店檢視。 |
| `commerce.commerceScope.websiteCode` | 不重複網站代碼。 一個環境中可以有許多網站。 |

### productPageView

| 說明 | XDM事件名稱 |
|---|---|
| 任何產品頁面載入時觸發。 | `commerce.productViews` |

#### 從productPageView收集的資料

下表說明為此事件收集的資料。

| 欄位 | 說明 |
|---|---|
| `channel` | 包含資料來源的相關資訊。 `_id`和`_type`都包含[名稱空間值](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html)。 |
| `channel._id` | 管道的唯一識別碼，例如`"https://ns.adobe.com/xdm/channels/web"`。 |
| `channel._type` | 識別管道資料的來源，例如`"https://ns.adobe.com/xdm/channel-types/web"`。 |
| `commerce.productViews` | 表示是否已檢視產品。 |
| `commerce.commerceScope` | 表示事件發生位置（商店檢視、商店、網站等）。 |
| `commerce.commerceScope.environmentID` | 環境識別碼。 32位數的英數字元ID，以連字型大小分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代碼。 每個網站可以有許多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的存放區檢視代碼。 每個商店可以有多個商店檢視。 |
| `commerce.commerceScope.websiteCode` | 不重複網站代碼。 一個環境中可以有許多網站。 |
| `productListItems` | 加入購物車的一系列產品。 |
| `productListItems.SKU` | 庫存單位。 產品的唯一識別碼。 |
| `productListItems.name` | 產品的顯示名稱或人類看得懂的名稱。 |
| `productListItems.priceTotal` | 產品明細專案的總價。 |
| `productListItems.quantity` | 購物車中的產品件數。 |
| `productListItems.discountAmount` | 表示套用的折扣金額。 |
| `productListItems.currencyCode` | 已使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)貨幣代碼，例如`USD`或`EUR`。 |
| `productListItems.productImageUrl` | 產品的主要影像URL。 |
| `productListItems.selectedOptions` | 用於可設定產品的欄位。 |
| `productListItems.selectedOptions.attribute` | 識別可設定產品的屬性，例如`size`或`color`。 |
| `productListItems.selectedOptions.value` | 識別屬性的值，例如`small`或`black`。 |

### startCheckout

| 說明 | XDM事件名稱 |
|---|---|
| 購物者按一下結帳按鈕時觸發。 | `commerce.checkouts` |

#### 從startCheckout收集的資料

下表說明為此事件收集的資料。

| 欄位 | 說明 |
|---|---|
| `channel` | 包含資料來源的相關資訊。 `_id`和`_type`都包含[名稱空間值](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html)。 |
| `channel._id` | 管道的唯一識別碼，例如`"https://ns.adobe.com/xdm/channels/web"`。 |
| `channel._type` | 識別管道資料的來源，例如`"https://ns.adobe.com/xdm/channel-types/web"`。 |
| `commerce.checkouts` | 表示在結帳過程中是否發生動作。 |
| `commerce.cart.cartID` | 識別客戶購物車的唯一ID。 |
| `commerce.commerceScope` | 表示事件發生位置（商店檢視、商店、網站等）。 |
| `commerce.commerceScope.environmentID` | 環境識別碼。 32位數的英數字元ID，以連字型大小分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代碼。 每個網站可以有許多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的存放區檢視代碼。 每個商店可以有多個商店檢視。 |
| `commerce.commerceScope.websiteCode` | 不重複網站代碼。 一個環境中可以有許多網站。 |
| `productListItems` | 加入購物車的一系列產品。 |
| `productListItems.SKU` | 庫存單位。 產品的唯一識別碼。 |
| `productListItems.name` | 產品的顯示名稱或人類看得懂的名稱。 |
| `productListItems.priceTotal` | 產品明細專案的總價。 |
| `productListItems.quantity` | 購物車中的產品件數。 |
| `productListItems.discountAmount` | 表示套用的折扣金額。 |
| `productListItems.currencyCode` | 已使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)貨幣代碼，例如`USD`或`EUR`。 |
| `productListItems.productImageUrl` | 產品的主要影像URL。 |
| `productListItems.selectedOptions` | 用於可設定產品的欄位。 |
| `productListItems.selectedOptions.attribute` | 識別可設定產品的屬性，例如`size`或`color`。 |
| `productListItems.selectedOptions.value` | 識別屬性的值，例如`small`或`black`。 |

### completeCheckout

| 說明 | XDM事件名稱 |
|---|---|
| 購物者下訂單時觸發。 | `commerce.purchases` |

#### 從completeCheckout收集的資料

下表說明為此事件收集的資料。

| 欄位 | 說明 |
|---|---|
| `channel` | 包含資料來源的相關資訊。 `_id`和`_type`都包含[名稱空間值](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html)。 |
| `channel._id` | 管道的唯一識別碼，例如`"https://ns.adobe.com/xdm/channels/web"`。 |
| `channel._type` | 識別管道資料的來源，例如`"https://ns.adobe.com/xdm/channel-types/web"`。 |
| `commerce.purchases` | 表示是否已接受訂單。 |
| `commerce.order` | 包含一或多個產品已下訂單的相關資訊。 |
| `commerce.order.purchaseID` | 賣家為此購買或合約所指派的唯一識別碼。 無法保證ID是唯一的。 |
| `commerce.order.payments` | 此訂單的付款清單。 |
| `commerce.order.payments.paymentTransactionID` | 此付款交易的唯一識別碼。 |
| `commerce.order.payments.paymentAmount` | 付款的值。 |
| `commerce.order.payments.paymentType` | 此訂單的付款方式。 選項包括： `cash`、`credit_card`、`debit_card`、`gift_card`、`check`、`paypal`、`wire_transfer`、`credit_card_reference`、`other`。 |
| `commerce.order.payments.currencyCode` | 已使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)貨幣代碼，例如`USD`或`EUR`。 |
| `commerce.order.taxAmount` | 買方支付作為最終付款一部分的稅捐金額。 |
| `commerce.order.discountAmount` | 表示套用至整張訂單的折扣金額。 |
| `commerce.order.createdDate` | 在商務系統中建立新訂單的時間和日期。 例如，`2022-10-15T20:20:39+00:00`。 |
| `commerce.shipping` | 一或多個產品的運送詳細資料。 |
| `commerce.shipping.shippingMethod` | 客戶選擇的配送方式，例如標準配送、加速配送、到店取貨等。 |
| `commerce.shipping.shippingAmount` | 客戶必須為運費支付的金額。 |  | `shipping` | 一或多個產品的運送詳細資料。 |
| `commerce.shipping.currencyCode` | 已使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)貨幣代碼，例如`USD`或`EUR`。 |
| `commerce.commerceScope` | 表示事件發生位置（商店檢視、商店、網站等）。 |
| `commerce.commerceScope.environmentID` | 環境識別碼。 32位數的英數字元ID，以連字型大小分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代碼。 每個網站可以有許多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的存放區檢視代碼。 每個商店可以有多個商店檢視。 |
| `commerce.commerceScope.websiteCode` | 不重複網站代碼。 一個環境中可以有許多網站。 |
| `personalEmail` | 個人電子郵件地址。 |
| `personalEmail.address` | 技術地址，例如，RFC2822和後續標準中通常定義的`name@domain.com`。 |
| `productListItems` | 加入購物車的一系列產品。 |
| `productListItems.SKU` | 庫存單位。 產品的唯一識別碼。 |
| `productListItems.name` | 產品的顯示名稱或人類看得懂的名稱。 |
| `productListItems.priceTotal` | 產品明細專案的總價。 |
| `productListItems.quantity` | 購物車中的產品件數。 |
| `productListItems.discountAmount` | 表示套用的折扣金額。 |
| `productListItems.productImageUrl` | 產品的主要影像URL。 |
| `productListItems.selectedOptions` | 用於可設定產品的欄位。 |
| `productListItems.selectedOptions.attribute` | 識別可設定產品的屬性，例如`size`或`color`。 |
| `productListItems.selectedOptions.value` | 識別屬性的值，例如`small`或`black`。 |

## 客戶設定檔事件

從店面擷取的設定檔事件包含帳戶資訊，例如`signIn`、`signOut`、`createAccount`和`editAccount`。 此資料可用於協助填入重要客戶詳細資訊，以更好地定義區段或執行行銷活動，例如傳送註冊折扣優惠、帳戶變更確認等。 從[伺服器端](events-backoffice.md#customer-profile-events)擷取到類似的設定檔事件。

>[!NOTE]
>
>[瞭解](custom-identities.md)如何建立自訂身分屬性來增強客戶設定檔識別。

### 登入

| 說明 | XDM事件名稱 |
|---|---|
| 購物者嘗試登入時觸發。 | `userAccount.login` |

>[!NOTE]
>
> 嘗試特定動作時會觸發此事件。 這並不表示動作成功。

#### 從登入收集的資料

下表說明為此事件收集的資料。

| 欄位 | 說明 |
|---|---|
| `channel` | 包含資料來源的相關資訊。 `_id`和`_type`都包含[名稱空間值](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html)。 |
| `channel._id` | 管道的唯一識別碼，例如`"https://ns.adobe.com/xdm/channels/web"`。 |
| `channel._type` | 識別管道資料的來源，例如`"https://ns.adobe.com/xdm/channel-types/web"`。 |
| `person` | 個別執行者、聯絡人或擁有者。 |
| `person.accountID` | 擷取使用者帳戶ID。 |
| `person.accountType` | 擷取使用者帳戶型別，例如`Personal`或`Company` （如果適用）。 |
| `person.personalEmailID` | 技術地址，例如，RFC2822和後續標準中通常定義的`name@domain.com`。 |
| `personalEmail` | 擷取聯絡詳細資料 — 電子郵件和相關資訊。 |
| `personalEmail.address` | 技術地址，例如，RFC2822和後續標準中通常定義的`name@domain.com`。 |
| `userAccount` | 表示任何熟客方案細節、偏好設定、登入流程和其他帳戶偏好設定。 |
| `userAccount.login` | 表示訪客是否嘗試登入。 |
| `commerce.commerceScope` | 表示事件發生位置（商店檢視、商店、網站等）。 |
| `commerce.commerceScope.environmentID` | 環境識別碼。 32位數的英數字元ID，以連字型大小分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代碼。 每個網站可以有許多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的存放區檢視代碼。 每個商店可以有多個商店檢視。 |
| `commerce.commerceScope.websiteCode` | 不重複網站代碼。 一個環境中可以有許多網站。 |

### 登出

| 說明 | XDM事件名稱 |
|---|---|
| 購物者嘗試登出時觸發。 | `userAccount.logout` |

>[!NOTE]
>
> 嘗試特定動作時會觸發此事件。 這並不表示動作成功。

#### 從登出收集的資料

下表說明為此事件收集的資料。

| 欄位 | 說明 |
|---|---|
| `channel` | 包含資料來源的相關資訊。 `_id`和`_type`都包含[名稱空間值](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html)。 |
| `channel._id` | 管道的唯一識別碼，例如`"https://ns.adobe.com/xdm/channels/web"`。 |
| `channel._type` | 識別管道資料的來源，例如`"https://ns.adobe.com/xdm/channel-types/web"`。 |
| `userAccount` | 表示任何熟客方案細節、偏好設定、登入流程和其他帳戶偏好設定。 |
| `userAccount.logout` | 表示訪客是否嘗試登出。 |
| `commerce.commerceScope` | 表示事件發生位置（商店檢視、商店、網站等）。 |
| `commerce.commerceScope.environmentID` | 環境識別碼。 32位數的英數字元ID，以連字型大小分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代碼。 每個網站可以有許多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的存放區檢視代碼。 每個商店可以有多個商店檢視。 |
| `commerce.commerceScope.websiteCode` | 不重複網站代碼。 一個環境中可以有許多網站。 |

### createAccount

| 說明 | XDM事件名稱 |
|---|---|
| 購物者嘗試建立帳戶時觸發。 | `userAccount.createProfile` |

>[!NOTE]
>
> 嘗試特定動作時會觸發此事件。 這並不表示動作成功。

#### 從createAccount收集的資料

下表說明為此事件收集的資料。

| 欄位 | 說明 |
|---|---|
| `channel` | 包含資料來源的相關資訊。 `_id`和`_type`都包含[名稱空間值](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html)。 |
| `channel._id` | 管道的唯一識別碼，例如`"https://ns.adobe.com/xdm/channels/web"`。 |
| `channel._type` | 識別管道資料的來源，例如`"https://ns.adobe.com/xdm/channel-types/web"`。 |
| `person` | 個別執行者、聯絡人或擁有者。 |
| `person.accountID` | 擷取使用者帳戶ID。 |
| `person.accountType` | 擷取使用者帳戶型別，例如`Personal`或`Company` （如果適用）。 |
| `person.personalEmailID` | 技術地址，例如，RFC2822和後續標準中通常定義的`name@domain.com`。 |
| `personalEmail` | 擷取聯絡詳細資料 — 電子郵件和相關資訊。 |
| `personalEmail.address` | 技術地址，例如，RFC2822和後續標準中通常定義的`name@domain.com`。 |
| `userAccount` | 表示任何熟客方案細節、偏好設定、登入流程和其他帳戶偏好設定。 |
| `userAccount.updateProfile` | 指出使用者是否已更新其帳戶設定檔。 |
| `commerce.commerceScope` | 表示事件發生位置（商店檢視、商店、網站等）。 |
| `commerce.commerceScope.environmentID` | 環境識別碼。 32位數的英數字元ID，以連字型大小分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代碼。 每個網站可以有許多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的存放區檢視代碼。 每個商店可以有多個商店檢視。 |
| `commerce.commerceScope.websiteCode` | 不重複網站代碼。 一個環境中可以有許多網站。 |

### editAccount

| 說明 | XDM事件名稱 |
|---|---|
| 購物者嘗試編輯帳戶時觸發。 | `userAccount.updateProfile` |

>[!NOTE]
>
> 嘗試特定動作時會觸發此事件。 這並不表示動作成功。

#### 從editAccount收集的資料

下表說明為此事件收集的資料。

| 欄位 | 說明 |
|---|---|
| `channel` | 包含資料來源的相關資訊。 `_id`和`_type`都包含[名稱空間值](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html)。 |
| `channel._id` | 管道的唯一識別碼，例如`"https://ns.adobe.com/xdm/channels/web"`。 |
| `channel._type` | 識別管道資料的來源，例如`"https://ns.adobe.com/xdm/channel-types/web"`。 |
| `person` | 個別執行者、聯絡人或擁有者。 |
| `person.accountID` | 擷取使用者帳戶ID。 |
| `person.accountType` | 擷取使用者帳戶型別，例如`Personal`或`Company` （如果適用）。 |
| `person.personalEmailID` | 技術地址，例如，RFC2822和後續標準中通常定義的`name@domain.com`。 |
| `personalEmail` | 擷取聯絡詳細資料 — 電子郵件和相關資訊。 |
| `personalEmail.address` | 技術地址，例如，RFC2822和後續標準中通常定義的`name@domain.com`。 |
| `userAccount` | 表示任何熟客方案細節、偏好設定、登入流程和其他帳戶偏好設定。 |
| `userAccount.updateProfile` | 指出使用者是否已更新其帳戶設定檔。 |
| `commerce.commerceScope` | 表示事件發生位置（商店檢視、商店、網站等）。 |
| `commerce.commerceScope.environmentID` | 環境識別碼。 32位數的英數字元ID，以連字型大小分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代碼。 每個網站可以有許多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的存放區檢視代碼。 每個商店可以有多個商店檢視。 |
| `commerce.commerceScope.websiteCode` | 不重複網站代碼。 一個環境中可以有許多網站。 |

## 搜尋事件

搜尋事件會提供與購物者意圖相關的資料。 insight迎合購物者的意圖，可協助商家瞭解購物者如何搜尋商品、他們點選了什麼，最終購買或放棄。 此資料如何使用的範例是，如果您想要鎖定搜尋您最熱門產品但從未購買產品的現有購物者。 您必須安裝[[!DNL Live Search]](../live-search/install.md)擴充功能才能存取這些事件。

使用在`searchRequest.id`和`searchResponse.id`事件中找到的`searchRequestSent`和`searchResponseReceived`欄位，以互動參照搜尋要求至對應的搜尋回應。

### searchRequestSent

| 說明 | XDM事件名稱 |
|---|---|
| 在「輸入時搜尋」彈出視窗中由下列事件觸發：<br><br>按Enter，按一下&#x200B;_檢視全部_<br><br>&#x200B;由搜尋結果頁面上的下列事件觸發：<br><br>選取篩選器，變更排序順序（_排序依據_），變更排序方向（升序或降序），變更每頁的結果數（_每頁顯示次數_），導覽至下一頁，導覽至上一頁，導覽至其他頁面 | `searchRequest` |

>[!NOTE]
>
>已安裝B2B擴充功能的Adobe Commerce Enterprise Edition不支援搜尋事件。

#### 從searchRequestSent收集的資料

下表說明為此事件收集的資料。

| 欄位 | 說明 |
|---|---|
| `channel` | 包含資料來源的相關資訊。 `_id`和`_type`都包含[名稱空間值](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html)。 |
| `channel._id` | 管道的唯一識別碼，例如`"https://ns.adobe.com/xdm/channels/web"`。 |
| `channel._type` | 識別管道資料的來源，例如`"https://ns.adobe.com/xdm/channel-types/web"`。 |
| `searchRequest` | 表示是否已傳送搜尋要求。 |
| `searchRequest.id` | 此特定搜尋要求的唯一ID。 |
| `searchRequest.value` | 請求的可量化值。 |
| `siteSearch` | 包含搜尋的相關資訊。 |
| `siteSearch.filter` | 顯示是否套用任何篩選器以限制搜尋結果。 |
| `siteSearch.filter.attribute` （篩選器） | 用於確定是否將其納入搜尋結果的專案面向。 |
| `siteSearch.filter.isRange` | 為true時，值表示可接受值範圍的端點。 |
| `siteSearch.filter.value` | 用於確定搜尋結果中包含哪些專案的屬性值。 |
| `siteSearch.sort` | 指出搜尋結果的排序方式。 |
| `siteSearch.sort.attribute` （排序） | 用於對搜尋結果中的專案進行排序的屬性。 |
| `siteSearch.sort.order` | 傳回搜尋結果的順序。 |
| `siteSearch.query` | 搜尋的字詞。 |
| `commerce.commerceScope` | 表示事件發生位置（商店檢視、商店、網站等）。 |
| `commerce.commerceScope.environmentID` | 環境識別碼。 32位數的英數字元ID，以連字型大小分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代碼。 每個網站可以有許多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的存放區檢視代碼。 每個商店可以有多個商店檢視。 |
| `commerce.commerceScope.websiteCode` | 不重複網站代碼。 一個環境中可以有許多網站。 |

### searchResponseReceived

| 說明 | XDM事件名稱 |
|---|---|
| 當「即時搜尋」傳回「鍵入時搜尋」彈出視窗或搜尋結果頁面結果時觸發。 | `searchResponse` |

>[!NOTE]
>
>已安裝B2B擴充功能的Adobe Commerce Enterprise Edition不支援搜尋事件。

#### 從searchResponseReceived收集的資料

下表說明為此事件收集的資料。

| 欄位 | 說明 |
|---|---|
| `channel` | 包含資料來源的相關資訊。 `_id`和`_type`都包含[名稱空間值](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html)。 |
| `channel._id` | 管道的唯一識別碼，例如`"https://ns.adobe.com/xdm/channels/web"`。 |
| `channel._type` | 識別管道資料的來源，例如`"https://ns.adobe.com/xdm/channel-types/web"`。 |
| `searchResponse` | 表示是否已收到搜尋回應。 |
| `searchResponse.id` | 此特定搜尋回應的唯一ID。 |
| `searchResponse.value` | 回應的可量化值。 |
| `siteSearch.numberOfResults` | 傳回的產品數。 |
| `siteSearch.suggestions` | 字串陣列，其中包含存在於目錄中且與搜尋查詢類似的產品和類別名稱。 |
| `productListItems` | 加入購物車的一系列產品。 |
| `productListItems.SKU` | 庫存單位。 產品的唯一識別碼。 |
| `productListItems.name` | 產品的顯示名稱或人類看得懂的名稱。 |
| `productListItems.productImageUrl` | 產品的主要影像URL。 |
| `commerce.commerceScope` | 表示事件發生位置（商店檢視、商店、網站等）。 |
| `commerce.commerceScope.environmentID` | 環境識別碼。 32位數的英數字元ID，以連字型大小分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代碼。 每個網站可以有許多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的存放區檢視代碼。 每個商店可以有多個商店檢視。 |
| `commerce.commerceScope.websiteCode` | 不重複網站代碼。 一個環境中可以有許多網站。 |

## B2B事件

Adobe Commerce的![B2B](../assets/b2b.svg)針對B2B商家，您必須[安裝](install.md#install-the-b2b-extension) `experience-platform-connector-b2b`擴充功能才能存取這些事件。

B2B事件包含[請購單清單](https://experienceleague.adobe.com/docs/commerce-admin/b2b/requisition-lists/requisition-lists.html)資訊，例如，請購單清單是否已建立、新增或刪除。 透過追蹤請購單清單的特定事件，您可以檢視客戶經常購買哪些產品，並根據該資料建立行銷活動。

### createRequisitionList

| 說明 | XDM事件名稱 |
|---|---|
| 當購物者建立請購單清單時觸發。 | `commerce.requisitionListOpens` |

#### 從createRequisitionList收集的資料

下表說明為此事件收集的資料。

| 欄位 | 說明 |
|---|---|
| `channel` | 包含資料來源的相關資訊。 `_id`和`_type`都包含[名稱空間值](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html)。 |
| `channel._id` | 管道的唯一識別碼，例如`"https://ns.adobe.com/xdm/channels/web"`。 |
| `channel._type` | 識別管道資料的來源，例如`"https://ns.adobe.com/xdm/channel-types/web"`。 |
| `commerce.requisitionListOpens` | 指示初始化新的請購單清單。 |
| `commerce.requisitionList` | 客戶建立的請購單清單的屬性。 |
| `commerce.requisitionList.ID` | 請購單清單的唯一識別碼。 |
| `commerce.requisitionList.name` | 客戶指定的請購單清單名稱。 |
| `commerce.requisitionList.description` | 客戶指定的請購單清單摘要。 |
| `commerce.commerceScope` | 表示事件發生位置（商店檢視、商店、網站等）。 |
| `commerce.commerceScope.environmentID` | 環境識別碼。 32位數的英數字元ID，以連字型大小分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代碼。 每個網站可以有許多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的存放區檢視代碼。 每個商店可以有多個商店檢視。 |
| `commerce.commerceScope.websiteCode` | 不重複網站代碼。 一個環境中可以有許多網站。 |

### addToRequisitionList

| 說明 | XDM事件名稱 |
|---|---|
| 購物者將產品新增至現有請購單清單或建立清單時觸發。 | `commerce.requisitionListAdds` |

#### 從addToRequisitionList收集的資料

下表說明為此事件收集的資料。

| 欄位 | 說明 |
|---|---|
| `channel` | 包含資料來源的相關資訊。 `_id`和`_type`都包含[名稱空間值](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html)。 |
| `channel._id` | 管道的唯一識別碼，例如`"https://ns.adobe.com/xdm/channels/web"`。 |
| `channel._type` | 識別管道資料的來源，例如`"https://ns.adobe.com/xdm/channel-types/web"`。 |
| `commerce.requisitionListAdds` | 指示新增一或多個產品至請購單清單。 |
| `commerce.requisitionList` | 客戶建立的請購單清單的屬性。 |
| `commerce.requisitionList.ID` | 請購單清單的唯一識別碼。 |
| `commerce.requisitionList.name` | 客戶指定的請購單清單名稱。 |
| `commerce.requisitionList.description` | 客戶指定的請購單清單摘要。 |
| `commerce.commerceScope` | 表示事件發生位置（商店檢視、商店、網站等）。 |
| `commerce.commerceScope.environmentID` | 環境識別碼。 32位數的英數字元ID，以連字型大小分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代碼。 每個網站可以有許多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的存放區檢視代碼。 每個商店可以有多個商店檢視。 |
| `commerce.commerceScope.websiteCode` | 不重複網站代碼。 一個環境中可以有許多網站。 |
| `productListItems` | 已新增至請購單清單的產品陣列。 |
| `productListItems.SKU` | 庫存單位。 產品的唯一識別碼。 |
| `productListItems.name` | 產品的顯示名稱或人類看得懂的名稱。 |
| `productListItems.priceTotal` | 產品明細專案的總價。 |
| `productListItems.quantity` | 購物車中的產品件數。 |
| `productListItems.discountAmount` | 表示套用的折扣金額。 |
| `productListItems.currencyCode` | 已使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)貨幣代碼，例如`USD`或`EUR`。 |
| `productListItems.selectedOptions` | 用於可設定產品的欄位。 |
| `productListItems.selectedOptions.attribute` | 識別可設定產品的屬性，例如`size`或`color`。 |
| `productListItems.selectedOptions.value` | 識別屬性的值，例如`small`或`black`。 |

### removeFromRequisitionList

| 說明 | XDM事件名稱 |
|---|---|
| 當購物者從請購單清單移除產品時觸發。 | `commerce.requisitionListRemovals` |

#### 從removeFromRequisitionList收集的資料

下表說明為此事件收集的資料。

| 欄位 | 說明 |
|---|---|
| `channel` | 包含資料來源的相關資訊。 `_id`和`_type`都包含[名稱空間值](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html)。 |
| `channel._id` | 管道的唯一識別碼，例如`"https://ns.adobe.com/xdm/channels/web"`。 |
| `channel._type` | 識別管道資料的來源，例如`"https://ns.adobe.com/xdm/channel-types/web"`。 |
| `commerce.requsitionListRemovals` | 表示從請購單清單移除一或多個產品。 |
| `commerce.requisitionList` | 客戶建立的請購單清單的屬性。 |
| `commerce.requisitionList.ID` | 請購單清單的唯一識別碼。 |
| `commerce.requisitionList.name` | 客戶指定的請購單清單名稱。 |
| `commerce.requisitionList.description` | 客戶指定的請購單清單摘要。 |
| `commerce.commerceScope` | 表示事件發生位置（商店檢視、商店、網站等）。 |
| `commerce.commerceScope.environmentID` | 環境識別碼。 32位數的英數字元ID，以連字型大小分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代碼。 每個網站可以有許多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的存放區檢視代碼。 每個商店可以有多個商店檢視。 |
| `commerce.commerceScope.websiteCode` | 不重複網站代碼。 一個環境中可以有許多網站。 |
| `productListItems` | 已新增至請購單清單的產品陣列。 |
| `productListItems.SKU` | 庫存單位。 產品的唯一識別碼。 |
| `productListItems.name` | 產品的顯示名稱或人類看得懂的名稱。 |
| `productListItems.priceTotal` | 產品明細專案的總價。 |
| `productListItems.quantity` | 購物車中的產品件數。 |
| `productListItems.discountAmount` | 表示套用的折扣金額。 |
| `productListItems.currencyCode` | 已使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)貨幣代碼，例如`USD`或`EUR`。 |
| `productListItems.selectedOptions` | 用於可設定產品的欄位。 |
| `productListItems.selectedOptions.attribute` | 識別可設定產品的屬性，例如`size`或`color`。 |
| `productListItems.selectedOptions.value` | 識別屬性的值，例如`small`或`black`。 |

### deleteRequisitionList

| 說明 | XDM事件名稱 |
|---|---|
| 購物者刪除請購單清單時觸發。 | `commerce.requisitionListDeletes` |

#### 從deleteRequisitionList收集的資料

下表說明為此事件收集的資料。

| 欄位 | 說明 |
|---|---|
| `channel` | 包含資料來源的相關資訊。 `_id`和`_type`都包含[名稱空間值](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html)。 |
| `channel._id` | 管道的唯一識別碼，例如`"https://ns.adobe.com/xdm/channels/web"`。 |
| `channel._type` | 識別管道資料的來源，例如`"https://ns.adobe.com/xdm/channel-types/web"`。 |
| `commerce.requisitionListDeletes` | 指出已刪除請購單清單。 |
| `commerce.requisitionList` | 客戶建立的請購單清單的屬性。 |
| `commerce.requisitionList.ID` | 請購單清單的唯一識別碼。 |
| `commerce.requisitionList.name` | 客戶指定的請購單清單名稱。 |
| `commerce.requisitionList.description` | 客戶指定的請購單清單摘要。 |
| `commerce.commerceScope` | 表示事件發生位置（商店檢視、商店、網站等）。 |
| `commerce.commerceScope.environmentID` | 環境識別碼。 32位數的英數字元ID，以連字型大小分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代碼。 每個網站可以有許多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的存放區檢視代碼。 每個商店可以有多個商店檢視。 |
| `commerce.commerceScope.websiteCode` | 不重複網站代碼。 一個環境中可以有許多網站。 |
