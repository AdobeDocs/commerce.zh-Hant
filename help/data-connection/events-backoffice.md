---
title: 後台活動
description: 瞭解每個後台事件擷取哪些資料。
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: 65cf8150-1a14-4d4c-aa0c-1545109e4fe7
source-git-commit: 1750aee715946d3a871e021cbbee687f54d1ff09
workflow-type: tm+mt
source-wordcount: '3618'
ht-degree: 0%

---

# [!DNL Data Connection]個後台事件

以下列出您在安裝[!DNL Data Connection]擴充功能時可用的Commerce後台事件。 這些事件收集的資料會傳送至Adobe Experience Platform。 您也可以建立[自訂事件](custom-events.md)，以立即收集未提供的其他資料。

除了下列事件收集的資料之外，您也會取得Adobe Experience Platform Web SDK提供的[其他資料](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/automatic-information.html?lang=zh-Hant)。

後台事件包含伺服器端資料。 此資料包含[訂單狀態](#order-status)資訊，例如，訂單是否已下達、取消、退款、出貨或完成。 伺服器端資料也包含[客戶設定檔事件](#customer-profile-events)資訊，例如帳戶是否已建立、更新或刪除。

>[!NOTE]
>
>所有後台事件都包含[`identityMap`](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/identitymap.html?lang=zh-Hant)欄位，其中包括購物者的電子郵件地址（可用時）和ECID。

## 訂單狀態

訂單狀態資料會顯示購物者訂單的360度檢視。 此檢視可協助商家在開發行銷活動時，更妥善地鎖定目標或分析整個訂單狀態。 例如，您可以找出某些產品類別中在一年中不同時間表現良好的趨勢。 例如，在較冷的月份銷售較佳的冬季服飾，或購物者多年來感興趣的特定產品顏色。 此外，訂單狀態資料可協助您瞭解購物者根據先前訂單轉換的傾向，進而計算期限客戶值。

### orderPlaced

| 說明 | XDM事件名稱 |
|---|---|
| 購物者下訂單時觸發。 | `commerce.backofficeOrderPlaced` |

#### 從orderPlaced收集的資料

下表說明為此事件收集的資料。

| 欄位 | 說明 |
|---|---|
| `commerce.order` | 包含訂單的相關資訊。 |
| `commerce.order.purchaseID` | 賣家為此購買或合約所指派的唯一識別碼。 無法保證ID是唯一的。 |
| `commerce.order.payments` | 此訂單的付款清單。 |
| `commerce.order.payments.paymentTransactionID` | 此付款交易的唯一識別碼。 |
| `commerce.order.payments.paymentAmount` | 付款的值。 |
| `commerce.order.payments.paymentType` | 此訂單的付款方式。 已計算，允許自訂值。 |
| `commerce.order.payments.currencyCode` | 已使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)貨幣代碼，例如`USD`或`EUR`。 |
| `commerce.order.taxAmount` | 買方支付作為最終付款一部分的稅捐金額。 |
| `commerce.order.discountAmount` | 表示套用至整張訂單的折扣金額。 |
| `commerce.order.createdDate` | 在商務系統中建立新訂單的時間和日期。 例如，`2022-10-15T20:20:39+00:00`。 |
| `commerce.order.currencyCode` | 用於訂單總額的ISO 4217貨幣代碼。 |
| `commerce.shipping` | 一或多個產品的運送詳細資料。 |
| `commerce.shipping.shippingMethod` | 客戶選擇的配送方式，例如標準配送、加速配送、到店取貨等。 |
| `commerce.shipping.shippingAmount` | 客戶必須為運費支付的金額。 |
| `commerce.shipping.currencyCode` | 用於配送總額的ISO 4217貨幣代碼。 |
| `commerce.commerceScope` | 表示事件發生位置（商店檢視、商店、網站等）。 |
| `commerce.commerceScope.environmentID` | 環境識別碼。 32位數的英數字元ID，以連字型大小分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代碼。 每個網站可以有許多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的存放區檢視代碼。 每個商店可以有多個商店檢視。 |
| `commerce.commerceScope.websiteCode` | 不重複網站代碼。 一個環境中可以有許多網站。 |
| `commerce.billing.address` | 帳單郵寄地址。 |
| `commerce.billing.address.street1` | 主要街道層級資訊、公寓號碼、街道號碼和街道名稱 |
| `commerce.billing.address.street2` | 街道層級資訊的其他欄位。 |
| `commerce.billing.address.city` | 城市的名稱。 |
| `commerce.billing.address.state` | 狀態的名稱。 此為自由格式的欄位。 |
| `commerce.billing.address.postalCode` | 地點的郵遞區號。 郵遞區號並非適用於所有國家/地區。 在某些國家/地區，這僅包含郵遞區號的一部分。 |
| `commerce.billing.address.country` | 政府管理的領土的名稱。 除了`xdm:countryCode`，這是自由格式的欄位，可以有任何語言的國家名稱。 |
| `personalEmail` | 個人電子郵件地址。 |
| `personalEmail.address` | 技術地址，例如，RFC2822和後續標準中通常定義的`name@domain.com`。 |
| `productListItems` | 訂單中的一系列產品。 |
| `productListItems.id` | 此產品條目的明細專案識別碼。 |
| `productListItems.SKU` | 庫存單位。 產品的唯一識別碼。 |
| `productListItems.name` | 產品的顯示名稱或人類看得懂的名稱。 |
| `productListItems.priceTotal` | 產品明細專案的總價。 |
| `productListItems.quantity` | 購物車中的產品件數。 |
| `productListItems.discountAmount` | 表示套用的折扣金額。 |
| `productListItems.currencyCode` | 已使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)貨幣代碼，例如`USD`或`EUR`。 |
| `productListItems.selectedOptions` | 用於可設定產品的欄位。 |
| `productListItems.selectedOptions.attribute` | 識別可設定產品的屬性，例如`size`或`color`。 |
| `productListItems.selectedOptions.value` | 識別屬性的值，例如`small`或`black`。 |
| `productListItems.categories` | 包含有關產品類別的資訊。 |
| `productListItems.categories.id` | 類別的唯一識別碼。 |
| `productListItems.categories.name` | 類別的名稱。 |
| `productListItems.categories.path` | 類別的路徑。 |
| `productListItems.productImageUrl` | 產品的主要影像URL。 |

### orderInvoiced

| 說明 | XDM事件名稱 |
|---|---|
| 當商家提交商業發票以請求付款時觸發。 | `commerce.backofficeOrderInvoiced` |

#### 從orderInvoiced收集的資料

下表說明為此事件收集的資料。

| 欄位 | 說明 |
|---|---|
| `commerce.order` | 包含訂單的相關資訊。 |
| `commerce.order.purchaseID` | 賣家為此購買或合約所指派的唯一識別碼。 無法保證ID是唯一的。 |
| `commerce.order.priceTotal` | 此訂單套用所有折扣和稅金後的總價。 |
| `commerce.order.currencyCode` | 用於訂單總額的ISO 4217貨幣代碼。 |
| `commerce.order.purchaseOrderNumber` | 購買者為此購買或合約所指派的唯一識別碼。 |
| `commerce.order.payments` | 此訂單的付款清單。 |
| `commerce.order.payments.currencyCode` | 已使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)貨幣代碼，例如`USD`或`EUR`。 |
| `commerce.order.payments.paymentType` | 此訂單的付款方式。 已計算，允許自訂值。 |
| `commerce.order.payments.paymentAmount` | 付款的值。 |
| `commerce.shipping` | 一或多個產品的運送詳細資料。 |
| `commerce.shipping.shippingMethod` | 客戶選擇的配送方式，例如標準配送、加速配送、到店取貨等。 |
| `commerce.shipping.shippingAmount` | 客戶必須為運費支付的金額。 |
| `commerce.commerceScope` | 表示事件發生位置（商店檢視、商店、網站等）。 |
| `commerce.commerceScope.environmentID` | 環境識別碼。 32位數的英數字元ID，以連字型大小分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代碼。 每個網站可以有許多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的存放區檢視代碼。 每個商店可以有多個商店檢視。 |
| `commerce.commerceScope.websiteCode` | 不重複網站代碼。 一個環境中可以有許多網站。 |
| `personalEmail` | 個人電子郵件地址。 |
| `personalEmail.address` | 技術地址，例如，RFC2822和後續標準中通常定義的`name@domain.com`。 |
| `productListItems` | 訂單中的一系列產品。 |
| `productListItems.id` | 此產品條目的明細專案識別碼。 |
| `productListItems.SKU` | 庫存單位。 產品的唯一識別碼。 |
| `productListItems.name` | 產品的顯示名稱或人類看得懂的名稱。 |
| `productListItems.priceTotal` | 產品明細專案的總價。 |
| `productListItems.quantity` | 購物車中的產品件數。 |
| `productListItems.discountAmount` | 表示套用的折扣金額。 |
| `productListItems.categories` | 包含有關產品類別的資訊。 |
| `productListItems.categories.id` | 類別的唯一識別碼。 |
| `productListItems.categories.name` | 類別的名稱。 |
| `productListItems.categories.path` | 類別的路徑。 |

### orderItemsShipped

| 說明 | XDM事件名稱 |
|---|---|
| 在訂單出貨時觸發。 | `commerce.backofficeOrderItemsShipped` |

#### 從orderItemsShipped收集的資料

下表說明為此事件收集的資料。

| 欄位 | 說明 |
|---|---|
| `commerce.order` | 包含訂單的相關資訊。 |
| `commerce.order.purchaseID` | 賣家為此購買或合約所指派的唯一識別碼。 無法保證ID是唯一的。 |
| `commerce.order.payments` | 此訂單的付款清單。 |
| `commerce.order.payments.paymentTransactionID` | 此付款交易的唯一識別碼。 |
| `commerce.order.payments.paymentAmount` | 付款的值。 |
| `commerce.order.payments.paymentType` | 此訂單的付款方式。 已計算，允許自訂值。 |
| `commerce.order.payments.currencyCode` | 已使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)貨幣代碼，例如`USD`或`EUR`。 |
| `commerce.order.priceTotal` | 此訂單套用所有折扣和稅金後的總價。 |
| `commerce.order.purchaseOrderNumber` | 購買者為此購買或合約所指派的唯一識別碼。 |
| `commerce.order.currencyCode` | 已使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)貨幣代碼，例如`USD`或`EUR`。 |
| `commerce.order.lastUpdatedDate` | 商業系統中特定訂單記錄的上次更新時間。 |
| `commerce.shipping` | 一或多個產品的運送詳細資料。 |
| `commerce.shipping.shippingMethod` | 客戶選擇的配送方式，例如標準配送、加速配送、到店取貨等。 |
| `commerce.shipping.shippingAmount` | 客戶必須為運費支付的金額。 |
| `commerce.shipping.address` | 實際送貨地址。 |
| `commerce.shipping.address.street1` | 主要街道層級資訊、公寓號碼、街道號碼和街道名稱。 |
| `commerce.shipping.address.street2` | 選用的街道資訊第二行。 |
| `commerce.shipping.address.city` | 城市的名稱。 |
| `commerce.shipping.address.state` | 州名。 此為自由格式的欄位。 |
| `commerce.shipping.address.postalCode` | 地點的郵遞區號。 郵遞區號並非適用於所有國家/地區。 在某些國家/地區，這僅包含郵遞區號的一部分。 |
| `commerce.shipping.address.country` | 政府管理的領土的名稱。 除了`xdm:countryCode`，這是自由格式的欄位，可以有任何語言的國家名稱。 |
| `commerce.shipping.currencyCode` | 已使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)貨幣代碼，例如`USD`或`EUR`。 |
| `commerce.shipping.trackingNumber` | 出貨承運商為訂單料號出貨提供的追蹤編號。 |
| `commerce.shipping.trackingURL` | 追蹤訂單專案出貨狀態的URL。 |
| `commerce.shipping.shipDate` | 訂單中一或多個料號出貨的日期。 |
| `commerce.commerceScope` | 表示事件發生位置（商店檢視、商店、網站等）。 |
| `commerce.commerceScope.environmentID` | 環境識別碼。 32位數的英數字元ID，以連字型大小分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代碼。 每個網站可以有許多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的存放區檢視代碼。 每個商店可以有多個商店檢視。 |
| `commerce.commerceScope.websiteCode` | 不重複網站代碼。 一個環境中可以有許多網站。 |
| `commerce.billing.address` | 帳單郵寄地址。 |
| `commerce.billing.address.street1` | 主要街道層級資訊、公寓號碼、街道號碼和街道名稱 |
| `commerce.billing.address.street2` | 街道層級資訊的其他欄位。 |
| `commerce.billing.address.city` | 城市的名稱。 |
| `commerce.billing.address.state` | 狀態的名稱。 此為自由格式的欄位。 |
| `commerce.billing.address.postalCode` | 地點的郵遞區號。 郵遞區號並非適用於所有國家/地區。 在某些國家/地區，這僅包含郵遞區號的一部分。 |
| `commerce.billing.address.country` | 政府管理的領土的名稱。 除了`xdm:countryCode`，這是自由格式的欄位，可以有任何語言的國家名稱。 |
| `personalEmail` | 個人電子郵件地址。 |
| `personalEmail.address` | 技術地址，例如，RFC2822和後續標準中通常定義的`name@domain.com`。 |
| `productListItems` | 訂單中的一系列產品。 |
| `productListItems.SKU` | 庫存單位。 產品的唯一識別碼。 |
| `productListItems.name` | 產品的顯示名稱或人類看得懂的名稱。 |
| `productListItems.priceTotal` | 產品明細專案的總價。 |
| `productListItems.quantity` | 購物車中的產品件數。 |
| `productListItems.discountAmount` | 表示套用的折扣金額。 |
| `productListItems.currencyCode` | 已使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)貨幣代碼，例如`USD`或`EUR`。 |
| `productListItems.selectedOptions` | 用於可設定產品的欄位。 |
| `productListItems.selectedOptions.attribute` | 識別可設定產品的屬性，例如`size`或`color`。 |
| `productListItems.selectedOptions.value` | 識別屬性的值，例如`small`或`black`。 |
| `productListItems.categories` | 包含有關產品類別的資訊。 |
| `productListItems.categories.id` | 類別的唯一識別碼。 |
| `productListItems.categories.name` | 類別的名稱。 |
| `productListItems.categories.path` | 類別的路徑。 |

### orderCanceled

| 說明 | XDM事件名稱 |
|---|---|
| 購物者取消訂單時觸發。 | `commerce.backofficeOrderCancelled` |

#### 從orderCanceled收集的資料

下表說明為此事件收集的資料。

| 欄位 | 說明 |
|---|---|
| `commerce.order` | 包含訂單的相關資訊。 |
| `commerce.order.purchaseID` | 賣家為此購買或合約所指派的唯一識別碼。 無法保證ID是唯一的。 |
| `commerce.order.purchaseOrderNumber` | 購買者為此購買或合約所指派的唯一識別碼。 |
| `commerce.order.cancelDate` | 購物者取消訂單的日期和時間。 |
| `commerce.order.lastUpdatedDate` | 商業系統中特定訂單記錄的上次更新時間。 |
| `commerce.commerceScope` | 表示事件發生位置（商店檢視、商店、網站等）。 |
| `commerce.commerceScope.environmentID` | 環境識別碼。 32位數的英數字元ID，以連字型大小分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代碼。 每個網站可以有許多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的存放區檢視代碼。 每個商店可以有多個商店檢視。 |
| `commerce.commerceScope.websiteCode` | 不重複網站代碼。 一個環境中可以有許多網站。 |
| `personalEmail` | 個人電子郵件地址。 |
| `personalEmail.address` | 技術地址，例如，RFC2822和後續標準中通常定義的`name@domain.com`。 |

### orderLineItemRefreaded

| 說明 | XDM事件名稱 |
|---|---|
| 當購物者針對退回的料號退款時觸發。 | `commerce.backofficeCreditMemoIssued` |

#### 從orderLineItemRefreaded收集的資料

下表說明為此事件收集的資料。

| 欄位 | 說明 |
|---|---|
| `commerce.order` | 包含訂單的相關資訊。 |
| `commerce.order.purchaseID` | 賣家為此購買或合約所指派的唯一識別碼。 無法保證ID是唯一的。 |
| `commerce.order.lastUpdatedDate` | 商業系統中特定訂單記錄的上次更新時間。 |
| `commerce.order.purchaseOrderNumber` | 購買者為此購買或合約所指派的唯一識別碼。 |
| `commerce.refunds` | 此訂單的退款清單。 |
| `commerce.refunds.transactionID` | 此退款的唯一識別碼。 |
| `commerce.refunds.refundAmount` | 退款的值。 |
| `commerce.refunds.refundPaymentType` | 此訂單的付款方式。 已計算，允許自訂值。 |
| `commerce.refunds.currencyCode` | 已使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)貨幣代碼，例如`USD`或`EUR`。 |
| `personalEmail` | 個人電子郵件地址。 |
| `personalEmail.address` | 技術地址，例如，RFC2822和後續標準中通常定義的`name@domain.com`。 |
| `productListItems` | 訂單中的一系列產品。 |
| `productListItems.SKU` | 庫存單位。 產品的唯一識別碼。 |
| `productListItems.name` | 產品的顯示名稱或人類看得懂的名稱。 |
| `productListItems.priceTotal` | 產品明細專案的總價。 |
| `productListItems.quantity` | 購物車中的產品件數。 |
| `productListItems.discountAmount` | 表示套用的折扣金額。 |
| `productListItems.currencyCode` | 已使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)貨幣代碼，例如`USD`或`EUR`。 |
| `productListItems.selectedOptions` | 用於可設定產品的欄位。 |
| `productListItems.selectedOptions.attribute` | 識別可設定產品的屬性，例如`size`或`color`。 |
| `productListItems.selectedOptions.value` | 識別屬性的值，例如`small`或`black`。 |
| `productListItems.categories` | 包含有關產品類別的資訊。 |
| `productListItems.categories.id` | 類別的唯一識別碼。 |
| `productListItems.categories.name` | 類別的名稱。 |
| `productListItems.categories.path` | 類別的路徑。 |

### orderItemsReturnInitiated

| 說明 | XDM事件名稱 |
|---|---|
| 購物者要求傳回專案時觸發。 | `commerce.backofficeOrderItemsReturnInitiated` |

#### 從orderItemsReturnInitiated收集的資料

下表說明為此事件收集的資料。

| 欄位 | 說明 |
|---|---|
| `commerce.order` | 包含訂單的相關資訊。 |
| `commerce.order.purchaseID` | 賣家為此購買或合約所指派的唯一識別碼。 無法保證ID是唯一的。 |
| `commerce.order.returns` | 此訂單的RMA （退貨授權）資訊。 |
| `commerce.order.returns.returnID` | 此RMA （退貨授權）的唯一識別碼。 |
| `commerce.order.returns.returnStatus` | RMA （退貨授權）的狀態，例如「擱置中」、「已關閉」等。 |
| `commerce.commerceScope` | 表示事件發生位置（商店檢視、商店、網站等）。 |
| `commerce.commerceScope.environmentID` | 環境識別碼。 32位數的英數字元ID，以連字型大小分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代碼。 每個網站可以有許多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的存放區檢視代碼。 每個商店可以有多個商店檢視。 |
| `commerce.commerceScope.websiteCode` | 不重複網站代碼。 一個環境中可以有許多網站。 |
| `personalEmail` | 個人電子郵件地址。 |
| `personalEmail.address` | 技術地址，例如，RFC2822和後續標準中通常定義的`name@domain.com`。 |
| `productListItems` | 訂單中的一系列產品。 |
| `productListItems.SKU` | 庫存單位。 產品的唯一識別碼。 |
| `productListItems.name` | 產品的顯示名稱或人類看得懂的名稱。 |
| `productListItems.quantity` | 購物車中的產品件數。 |
| `productListItems.selectedOptions` | 用於可設定產品的欄位。 |
| `productListItems.selectedOptions.attribute` | 識別可設定產品的屬性，例如`size`或`color`。 |
| `productListItems.selectedOptions.value` | 識別屬性的值，例如`small`或`black`。 |
| `productListItems.categories` | 包含有關產品類別的資訊。 |
| `productListItems.categories.id` | 類別的唯一識別碼。 |
| `productListItems.categories.name` | 類別的名稱。 |
| `productListItems.categories.path` | 類別的路徑。 |
| `productListItems.returnItem` | 此料號的RMA （退貨授權）資訊。 |
| `productListItems.returnItem.returnStatus` | 傳回專案的狀態，例如「擱置中」、「已核准」等。 |
| `productListItems.returnItem.returnReason` | 要求此專案退貨的原因。 |
| `productListItems.returnItem.returnItemCondition` | 要求傳回的專案的條件。 |
| `productListItems.returnItem.returnResolution` | 要退回之專案的要求解決方式，例如「退款」、「兌換」等。 |
| `productListItems.returnItem.returnQuantityRequested` | 購物者要求傳回的此專案數。 |
| `productListItems.returnItem.returnQuantityAuthorized` | 已授權可傳回的此專案數。 |
| `productListItems.returnItem.eturnQuantityReceived` | 收到的傳回專案數。 |
| `productListItems.returnItem.returnQuantityApproved` | 此專案與傳回完全完成且已核准的編號。 |

### orderItemReturnCompleted

| 說明 | XDM事件名稱 |
|---|---|
| 購物者要求退貨的專案完成時觸發。 | `commerce.backofficeOrderItemsReturnCompleted` |

#### 從orderItemReturnCompleted收集的資料

下表說明為此事件收集的資料。

| 欄位 | 說明 |
|---|---|
| `commerce.order` | 包含訂單的相關資訊。 |
| `commerce.order.purchaseID` | 賣家為此購買或合約所指派的唯一識別碼。 無法保證ID是唯一的。 |
| `commerce.order.returns` | 此訂單的RMA （退貨授權）資訊。 |
| `commerce.order.returns.returnID` | 此RMA （退貨授權）的唯一識別碼。 |
| `commerce.order.returns.returnStatus` | RMA （退貨授權）的狀態，例如「擱置中」、「已關閉」等。 |
| `commerce.commerceScope` | 表示事件發生位置（商店檢視、商店、網站等）。 |
| `commerce.commerceScope.environmentID` | 環境識別碼。 32位數的英數字元ID，以連字型大小分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代碼。 每個網站可以有許多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的存放區檢視代碼。 每個商店可以有多個商店檢視。 |
| `commerce.commerceScope.websiteCode` | 不重複網站代碼。 一個環境中可以有許多網站。 |
| `personalEmail` | 個人電子郵件地址。 |
| `personalEmail.address` | 技術地址，例如，RFC2822和後續標準中通常定義的`name@domain.com`。 |
| `productListItems` | 訂單中的一系列產品。 |
| `productListItems.SKU` | 庫存單位。 產品的唯一識別碼。 |
| `productListItems.name` | 產品的顯示名稱或人類看得懂的名稱。 |
| `productListItems.selectedOptions` | 用於可設定產品的欄位。 |
| `productListItems.selectedOptions.attribute` | 識別可設定產品的屬性，例如`size`或`color`。 |
| `productListItems.selectedOptions.value` | 識別屬性的值，例如`small`或`black`。 |
| `productListItems.categories` | 包含有關產品類別的資訊。 |
| `productListItems.categories.id` | 類別的唯一識別碼。 |
| `productListItems.categories.name` | 類別的名稱。 |
| `productListItems.categories.path` | 類別的路徑。 |
| `productListItems.returnItem` | 此料號的RMA （退貨授權）資訊。 |
| `productListItems.returnItem.returnStatus` | 傳回專案的狀態，例如「擱置中」、「已核准」等。 |
| `productListItems.returnItem.returnReason` | 要求此專案退貨的原因。 |
| `productListItems.returnItem.returnItemCondition` | 要求傳回的專案的條件。 |
| `productListItems.returnItem.returnResolution` | 要退回之專案的要求解決方式，例如「退款」、「兌換」等。 |
| `productListItems.returnItem.returnQuantityRequested` | 購物者要求傳回的此專案數。 |
| `productListItems.returnItem.returnQuantityAuthorized` | 已授權可傳回的此專案數。 |
| `productListItems.returnItem.eturnQuantityReceived` | 收到的傳回專案數。 |
| `productListItems.returnItem.returnQuantityApproved` | 此專案與傳回完全完成且已核准的編號。 |

### orderShipmentCompleted

| 說明 | XDM事件名稱 |
|---|---|
| 在出貨完成時觸發。 | `commerce.backofficeOrderShipmentCompleted` |

#### 從orderShipmentCompleted收集的資料

下表說明為此事件收集的資料。

| 欄位 | 說明 |
|---|---|
| `commerce.order` | 包含訂單的相關資訊。 |
| `commerce.order.purchaseID` | 賣家為此購買或合約所指派的唯一識別碼。 無法保證ID是唯一的。 |
| `commerce.order.payments` | 此訂單的付款清單。 |
| `commerce.order.payments.paymentTransactionID` | 此付款交易的唯一識別碼。 |
| `commerce.order.payments.paymentAmount` | 付款的值。 |
| `commerce.order.payments.paymentType` | 此訂單的付款方式。 已計算，允許自訂值。 |
| `commerce.order.payments.currencyCode` | 已使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)貨幣代碼，例如`USD`或`EUR`。 |
| `commerce.order.taxAmount` | 買方支付作為最終付款一部分的稅捐金額。 |
| `commerce.order.createdDate` | 在商務系統中建立新訂單的時間和日期。 例如，`2022-10-15T20:20:39+00:00`。 |
| `commerce.shipping` | 一或多個產品的運送詳細資料。 |
| `commerce.shipping.shippingMethod` | 客戶選擇的配送方式，例如標準配送、加速配送、到店取貨等。 |
| `commerce.shipping.shippingAmount` | 客戶必須為運費支付的金額。 |
| `commerce.shipping.shipDate` | 訂單中一或多個料號出貨的日期。 |
| `commerce.shipping.address` | 實際送貨地址。 |
| `commerce.shipping.address.street1` | 主要街道層級資訊、公寓號碼、街道號碼和街道名稱。 |
| `commerce.shipping.address.street2` | 選用的街道資訊第二行。 |
| `commerce.shipping.address.city` | 城市的名稱。 |
| `commerce.shipping.address.state` | 州名。 此為自由格式的欄位。 |
| `commerce.shipping.address.postalCode` | 地點的郵遞區號。 郵遞區號並非適用於所有國家/地區。 在某些國家/地區，這僅包含郵遞區號的一部分。 |
| `commerce.shipping.address.country` | 政府管理的領土的名稱。 除了`xdm:countryCode`，這是自由格式的欄位，可以有任何語言的國家名稱。 |
| `commerce.billing.address` | 帳單郵寄地址。 |
| `commerce.billing.address.street1` | 主要街道層級資訊、公寓號碼、街道號碼和街道名稱 |
| `commerce.billing.address.street2` | 街道層級資訊的其他欄位。 |
| `commerce.billing.address.city` | 城市的名稱。 |
| `commerce.billing.address.state` | 狀態的名稱。 此為自由格式的欄位。 |
| `commerce.billing.address.postalCode` | 地點的郵遞區號。 郵遞區號並非適用於所有國家/地區。 在某些國家/地區，這僅包含郵遞區號的一部分。 |
| `commerce.billing.address.country` | 政府管理的領土的名稱。 除了`xdm:countryCode`，這是自由格式的欄位，可以有任何語言的國家名稱。 |
| `personalEmail` | 個人電子郵件地址。 |
| `personalEmail.address` | 技術地址，例如，RFC2822和後續標準中通常定義的`name@domain.com`。 |
| `productListItems` | 訂單中的一系列產品。 |
| `productListItems.SKU` | 庫存單位。 產品的唯一識別碼。 |
| `productListItems.name` | 產品的顯示名稱或人類看得懂的名稱。 |
| `productListItems.priceTotal` | 產品明細專案的總價。 |
| `productListItems.quantity` | 購物車中的產品件數。 |
| `productListItems.discountAmount` | 表示套用的折扣金額。 |
| `productListItems.currencyCode` | 已使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)貨幣代碼，例如`USD`或`EUR`。 |
| `productListItems.selectedOptions` | 用於可設定產品的欄位。 |
| `productListItems.selectedOptions.attribute` | 識別可設定產品的屬性，例如`size`或`color`。 |
| `productListItems.selectedOptions.value` | 識別屬性的值，例如`small`或`black`。 |
| `productListItems.categories` | 包含有關產品類別的資訊。 |
| `productListItems.categories.id` | 類別的唯一識別碼。 |
| `productListItems.categories.name` | 類別的名稱。 |
| `productListItems.categories.path` | 類別的路徑。 |

## 客戶設定檔事件

從伺服器端擷取的設定檔事件包含帳戶資訊，例如`accountCreated`、`accountUpdated`和`accountDeleted`。 此資料可用於協助填入重要客戶詳細資訊，以更好地定義區段或執行行銷活動，例如傳送註冊折扣優惠、帳戶變更確認等。 從[店面](events.md#customer-profile-events)擷取到類似的設定檔事件。

>[!NOTE]
>
>每個客戶設定檔事件也包含[`identityMap`](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/identitymap.html?lang=zh-Hant)欄位，其中包含系統產生的Commerce客戶ID作為設定檔的主要識別碼，以及當作次要識別碼使用的電子郵件ID。 [瞭解](custom-identities.md)如何建立自訂身分屬性來增強客戶設定檔識別。

### accountCreated

| 說明 | XDM事件名稱 |
|---|---|
| 購物者嘗試建立帳戶時觸發。 | `userAccount.backofficeCreateProfile` |

#### 從帳戶建立的資料收集

下表說明為此事件收集的資料。

| 欄位 | 說明 |
|---|---|
| `person` | 包含有關客戶的資訊。 |
| `person.name` | 包含客戶名稱的相關資訊。 |
| `person.name.firstName` | 包含客戶的名字。 |
| `person.name.lastName` | 包含客戶的姓氏。 |
| `personalEmail` | 個人電子郵件地址。 |
| `personalEmail.address` | 技術地址，例如，RFC2822和後續標準中通常定義的`name@domain.com`。 |
| `commerce.commerceScope` | 表示事件發生位置（商店檢視、商店、網站等）。 |
| `commerce.commerceScope.environmentID` | 環境識別碼。 32位數的英數字元ID，以連字型大小分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代碼。 每個網站可以有許多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的存放區檢視代碼。 每個商店可以有多個商店檢視。 |
| `commerce.commerceScope.websiteCode` | 不重複網站代碼。 一個環境中可以有許多網站。 |

### 帳戶已更新

| 說明 | XDM事件名稱 |
|---|---|
| 購物者嘗試編輯帳戶時觸發。 | `userAccount.backofficeUpdateProfile` |

#### 從帳戶收集的資料已更新

下表說明為此事件收集的資料。

| 欄位 | 說明 |
|---|---|
| `person` | 包含有關客戶的資訊。 |
| `person.name` | 包含客戶名稱的相關資訊。 |
| `person.name.firstName` | 包含客戶的名字。 |
| `person.name.lastName` | 包含客戶的姓氏。 |
| `personalEmail` | 個人電子郵件地址。 |
| `personalEmail.address` | 技術地址，例如，RFC2822和後續標準中通常定義的`name@domain.com`。 |
| `commerce.commerceScope` | 表示事件發生位置（商店檢視、商店、網站等）。 |
| `commerce.commerceScope.environmentID` | 環境識別碼。 32位數的英數字元ID，以連字型大小分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代碼。 每個網站可以有許多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的存放區檢視代碼。 每個商店可以有多個商店檢視。 |
| `commerce.commerceScope.websiteCode` | 不重複網站代碼。 一個環境中可以有許多網站。 |

### accountDeleted

| 說明 | XDM事件名稱 |
|---|---|
| 購物者嘗試刪除帳戶時觸發。 | `userAccount.backofficeDeleteProfile` |

#### 從帳戶收集的資料已刪除

下表說明為此事件收集的資料。

| 欄位 | 說明 |
|---|---|
| `person` | 包含有關客戶的資訊。 |
| `person.name` | 包含客戶名稱的相關資訊。 |
| `person.name.firstName` | 包含客戶的名字。 |
| `person.name.lastName` | 包含客戶的姓氏。 |
| `personalEmail` | 個人電子郵件地址。 |
| `personalEmail.address` | 技術地址，例如，RFC2822和後續標準中通常定義的`name@domain.com`。 |
| `commerce.commerceScope` | 表示事件發生位置（商店檢視、商店、網站等）。 |
| `commerce.commerceScope.environmentID` | 環境識別碼。 32位數的英數字元ID，以連字型大小分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代碼。 每個網站可以有許多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的存放區檢視代碼。 每個商店可以有多個商店檢視。 |
| `commerce.commerceScope.websiteCode` | 不重複網站代碼。 一個環境中可以有許多網站。 |
