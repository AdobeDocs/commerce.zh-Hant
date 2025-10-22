---
title: 發行說明
description: Adobe Commerce中 [!DNL Data Connection] 擴充功能的最新發行資訊。
feature: Personalization, Integration, Release Notes
exl-id: f3b92632-947d-40cd-89b7-24ed0680be51
source-git-commit: 5dd290a4e10bdbd1f6c96b67ab6c9ba1598705dc
workflow-type: tm+mt
source-wordcount: '1290'
ht-degree: 1%

---

# 發行說明

>[!IMPORTANT]
>
>Experience Platform聯結器已重新命名為[!DNL Data Connection]。

下列發行說明包含[!DNL Data Connection]擴充功能的更新，並包含：

![新增](../assets/new.svg) — 新功能
![修正](../assets/fix.svg) — 修正和改良
![錯誤](../assets/bug.svg) — 已知問題

有關[!DNL Data Connection]擴充功能所使用的擴充功能的功能變更和修正，請參閱&#x200B;**支援的服務更新**。

請參閱[即將發行的版本](https://experienceleague.adobe.com/zh-hant/docs/commerce-operations/release/planning/schedule)，瞭解發行排程和支援。

請參閱開發人員檔案以[瞭解哪些Commerce版本支援此模組](https://experienceleague.adobe.com/zh-hant/docs/commerce-operations/release/product-availability)。

## 支援的服務更新

以下發行說明說明說明與[!DNL Data Connection]擴充功能所使用的擴充功能相關的功能變更和修正。

+++支援的服務更新

_2025年8月7日_

![新](../assets/new.svg) — 透過3.3.0版本，您現在可以新增[自訂屬性至設定檔](custom-identities.md)。

_2024年8月2日_

![Fix](../assets/fix.svg) — 當訂單總計設定為包含稅捐時，固定付款總金額。
![新](../assets/new.svg) — 已新增`taxAmount`欄位以訂購購買事件。
![新](../assets/new.svg) — 已新增新增將自訂資料新增至事件的功能。 有關[範例](https://github.com/adobe/commerce-events/blob/main/examples/events/custom-event-override.md)，請參閱下列內容。

_2024年1月24日_

![新](../assets/new.svg) — 已更新`data-services-b2b`擴充功能，針對B2B商家加入名為`deleteRequisitionList`的新請購單事件。

_2023年11月16日_

![修正](../assets/fix.svg) — 修正您下具有多個送貨地址的訂單時，錯誤訊息顯示不正確的問題。
![修正](../assets/fix.svg) — 修正`productPageView`事件中，在商店檢視上切換貨幣後，`productListItems.priceTotal`事件欄位未轉換價格的問題。
![修正](../assets/fix.svg) — 修正當商家切換商店檢視時，`productListItems`事件欄位中貨幣代碼未更新的問題。

_2023年10月10日_

![新增](../assets/new.svg) — 已新增訂單狀態事件：[已開立商業發票](events-backoffice.md#orderinvoiced)、[已起始訂單專案退貨](events-backoffice.md#orderitemsreturninitiated)，以及[已完成訂單專案退貨](events-backoffice.md#orderitemreturncompleted)。
![修正](../assets/fix.svg) — 修正重新整理快取後，貨幣設定變更未反映在事件中的問題。
![修正](../assets/fix.svg) — 修正啟用非同步下單時，未顯示訂單確認訊息的錯誤。
![新](../assets/new.svg) — 已將資料新增至[類別檢視]頁面上簡單產品的`addToRequisitionList`事件。
![修正](../assets/fix.svg) — 修正從訂購確認頁面新增產品時，`selectedOptions`事件中`addToRequisitionList`資料的問題。
![新增](../assets/new.svg) — 當產品從類別檢視頁面新增至請購單清單時，已將產品資料新增至`addToRequisitionList`事件。
![New](../assets/new.svg) — 當可設定的產品從「產品檢視」頁面新增至請購單清單時，已新增`addToRequisitionList`事件。
![新](../assets/new.svg) — 當產品數量增加和/或從請購單清單中減少時，新增`addToRequisitionList`和`removeFromRequisitionList`個事件。

_2023年6月10日_

![修正](../assets/fix.svg) — 修正`orderId`由於Commerce訂單識別碼中的首碼而未傳入內容的問題。
![修正](../assets/fix.svg) — 已更新內容安全性原則設定。

_2023年3月30日_

![New](../assets/new.svg) — 新增名為`data-services-b2b`的延伸模組，包含B2B商家的[請購單清單事件](events.md#b2b-events)。
![新](../assets/new.svg) — 已將`uniqueIdentifier`欄位新增至[搜尋](events.md#search-events)事件。 此新欄位可讓商家交叉參考搜尋要求與搜尋回應。

_2022年10月12日_

![新增](../assets/new.svg) — 新增兩個[店面活動](events.md)、`openCart`和`removeFromCart`至Adobe Commerce店面活動SDK和收集器。
![新](../assets/new.svg) — 已新增對[AEM店面](overview.md#aem-support)的支援。

+++

## 3.4.0

_2025年9月16日_

[!BADGE 相容性]{type=Informative tooltip="相容性"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg) [!DNL Data Connection]現在完全遵守Cookie限制模式，方法是在啟用限制時，防止在Cookie/本機儲存體中收集及儲存資料。

## 3.3.0

_2025年3月21日_

[!BADGE 相容性]{type=Informative tooltip="相容性"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg)已新增PHP 8.4支援。

## 3.2.1

_2025年1月17日_

[!BADGE 相容性]{type=Informative tooltip="相容性"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg) — 已將[HIPAA就緒的延伸](hipaa-readiness.md)新增至[!DNL Data Connection]，讓商家可以與Experience Platform共用[!DNL Commerce]個後台事件資料並維持HIPAA合規性。
![修正](../assets/fix.svg) — 修正[!DNL Data Connection]擴充功能覆寫`eventForwarding`資料並為所有客戶設定`HIPAA`標幟的問題。 現在，擴充功能只會為HIPAA客戶設定標幟。

## 3.2.0

_2024年10月7日_

[!BADGE 相容性]{type=Informative tooltip="相容性"} Adobe Commerce 2.4.4或更新版本

![新增](../assets/new.svg) — 已新增建立[自訂訂單屬性](custom-attributes.md)到後台資料的功能。
![新](../assets/new.svg) — 已新增新的[自訂訂單屬性](connect-data.md#data-customization)表格，協助您檢視[!DNL Commerce]中設定並傳送至Experience Platform的任何自訂屬性。
![新](../assets/new.svg) — 已新增[收集設定檔記錄](connect-data.md#send-customer-profile-data)和資料並傳送至Experience Platform的功能。

## 3.2.0-beta3

_2024年8月27日_

[!BADGE 相容性]{type=Informative tooltip="相容性"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg) — 如果您正在參與Beta版，請確定您的`composer.json`檔案在根層級有下列專案： `"minimum-stability": "beta"`。 此外，新增`composer require "magento/customers-connector: ^1.2.0"`以將客戶設定檔從您的Commerce執行個體傳送至SaaS。
![新](../assets/new.svg) — 此版本包含3.1.1、3.1.2、3.1.3和3.1.4中發行的修補程式。

## 3.1.4

_2024年8月9日_

[!BADGE 相容性]{type=Informative tooltip="相容性"} Adobe Commerce 2.4.4或更新版本

![修正](../assets/fix.svg) — 已更新`experience-platform-connector`中繼包以移除其他未使用的資料匯出工具和索引子。

## 3.1.3

_2024年7月22日_

[!BADGE 相容性]{type=Informative tooltip="相容性"} Adobe Commerce 2.4.4或更新版本

![修正](../assets/fix.svg) — 已更新`experience-platform-connector`中繼包以移除未使用的資料匯出工具和索引子。

## 3.1.2

_2024年6月5日_

[!BADGE 相容性]{type=Informative tooltip="相容性"} Adobe Commerce 2.4.4或更新版本

![修正](../assets/fix.svg) — 修正起始[歷史同步](connect-data.md#specify-order-history-date-range)時使用錯誤日期格式的問題。
![修正](../assets/fix.svg) — 修正Adobe Commerce 2.4.7未傳送`startCheckout`事件的問題。

## 3.1.1

_2024年4月4日_

[!BADGE 相容性]{type=Informative tooltip="相容性"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg) — 已新增所有[!DNL Data Connection]擴充功能對PHP 8.3的支援。
![新](../assets/new.svg) — 新增如何[整合](mobile-sdk-epc.md) Adobe Experience Platform Mobile SDK與Commerce的文章。

## 3.2.0-beta2

_2024年3月4日_

[!BADGE 相容性]{type=Informative tooltip="相容性"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg) — 如果您正在參與Beta版，請確定您的`composer.json`檔案在根層級有下列專案： `"minimum-stability": "beta"`。 此外，新增`composer require "magento/customers-connector: ^1.2.0"`以將客戶設定檔從您的Commerce執行個體傳送至SaaS。
![新](../assets/new.svg) — 已新增[新增自訂屬性](custom-attributes.md)的功能。
![新](../assets/new.svg) — 已新增[收集設定檔記錄](connect-data.md#send-customer-profile-data)和資料並傳送至Experience Platform的功能。

## 3.1.0

_2023年11月16日_

[!BADGE 相容性]{type=Informative tooltip="相容性"} Adobe Commerce 2.4.4或更新版本

![新](../assets/new.svg) - Experience Platform聯結器已重新命名為[!DNL Data Connection]。
![修正](../assets/fix.svg) — 新增在Adobe IMS無法產生存取權杖時記錄錯誤回應的功能。
![修正](../assets/fix.svg) — 如果您嘗試同步處理歷史訂單，但尚未指定帳戶認證，則已新增通知訊息。

## 3.0.0

_2023年10月10日_

[!BADGE 相容性]{type=Informative tooltip="相容性"} Adobe Commerce 2.4.4或更新版本

此為主要版本發行版本。 [編輯](install.md#update-the-data-connection)您專案的根composer.json檔案。

![新](../assets/new.svg) - [傳送歷史訂單](connect-data.md#send-historical-order-data)資料和狀態的一般可用性，給Experience Platform。
![新增](../assets/new.svg) — 當您[設定](connect-data.md#connect-commerce-data-to-adobe-experience-platform) [!DNL Data Connection]擴充功能時，已新增對OAuth 2.0的支援。
![新增](../assets/new.svg) — 已終止支援Adobe Commerce 2.4.3。

## 2.3.0

_2023年6月27日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.3或更新版本

![新增](../assets/new.svg) — 已新增[關閉傳送店面活動](connect-data.md#data-collection)至Experience Platform的功能。
![修正](../assets/fix.svg) — 已更新內容安全性原則設定。
![修正](../assets/fix.svg) — 修正Commerce 2.4.7版本對後台事件的支援。
![新](../assets/new.svg) — 新增當您儲存變更至[!DNL Data Connection]擴充功能表單時，有關快取失效的通知訊息。

## 3.0.0-beta1 （僅限內部）

_2023年6月13日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.3或更新版本

![新](../assets/new.svg) - (Beta)已新增[傳送歷史訂單](connect-data.md#beta-send-historical-order-data)資料和狀態至Experience Platform的功能。

## 2.2.0

_2023年3月30日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.3或更新版本

![新](../assets/new.svg) — 已搭配`commerce-data-export`和`saas-export`相依性與`experience-platform-connector`副檔名。 之前，您必須分別安裝這些相依性。 這些相依性加上商家設定，可啟用伺服器端處理[後台事件](events-backoffice.md)。
![新增](../assets/new.svg) — 已新增名為[`orderShipmentCompleted`](events-backoffice.md#ordershipmentcompleted)的後台事件。

## 2.1.1

_2023年2月28日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.3或更新版本

![新](../assets/new.svg) — 已新增所有[!DNL Data Connection]擴充功能對PHP 8.2的支援。

## 2.1.0

_2023年1月17日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.3或更新版本

![新](../assets/new.svg) — 已更新[[!DNL Data Connection] 擴充功能管理員](connect-data.md)，以便您可以指定自己的AEP Web SDK (alloy)。
![Fix](../assets/fix.svg)設定推送至邊緣之任何資料的主要身分時，已變更為使用`identityMap`而非`personID`。

## 2.0.1

_2022年11月10日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.3或更新版本

![修正](../assets/fix.svg) — 現在Adobe Experience Platform內容僅在Storefront事件收集器和店面事件SDK成功載入後才會設定。

## 2.0.0

_2022年10月12日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.3或更新版本

![新](../assets/new.svg) — 新增在[連線](connect-data.md)您的AEP執行個體至Experience Platform時，指定您自己的Adobe Commerce Web SDK的功能。
![修正](../assets/fix.svg) — 更新資料流範圍需求，因此資料流ID的範圍必須設定為網站而非儲存檢閱。

## 1.0.0

_2022年8月9日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.3或更新版本

![新](../assets/new.svg) — 一般可用性版本。
