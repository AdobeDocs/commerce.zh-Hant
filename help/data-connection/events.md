---
title: 行為事件
description: 瞭解每個行為事件擷取哪些資料。
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: bcabccc9-8a2e-4045-9306-1d999bb75624
source-git-commit: 631dfacd26a333e70a70f354d191d256d90d946f
workflow-type: tm+mt
source-wordcount: '402'
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

店面事件會從購物者在網站上的互動擷取資料，並包含`addToCart`、`pageView`、`createAccount`、`editAccount`、`startCheckout`、`completeCheckout`、`signIn`、`signOut`等事件。 店面事件僅適用於簡單且可設定的產品。

請參閱[開發人員檔案](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection)，深入瞭解店面活動。

## 客戶設定檔事件

從店面擷取的設定檔事件包含帳戶資訊，例如`signIn`、`signOut`、`createAccount`和`editAccount`。 此資料可用於協助填入重要客戶詳細資訊，以更好地定義區段或執行行銷活動，例如傳送註冊折扣優惠、帳戶變更確認等。

請參閱[開發人員檔案](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection)，深入瞭解客戶設定檔事件。

## 搜尋事件

搜尋事件會提供與購物者意圖相關的資料。 insight迎合購物者的意圖，可協助商家瞭解購物者如何搜尋商品、他們點選了什麼，最終購買或放棄。 此資料如何使用的範例是，如果您想要鎖定搜尋您最熱門產品但從未購買產品的現有購物者。 您必須安裝[[!DNL Live Search]](../live-search/install.md)擴充功能才能存取這些事件。

使用在`searchRequest.id`和`searchResponse.id`事件中找到的`searchRequestSent`和`searchResponseReceived`欄位，以互動參照搜尋要求至對應的搜尋回應。

請參閱[開發人員檔案](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection)，深入瞭解搜尋事件。

## B2B事件

Adobe Commerce的![B2B](../assets/b2b.svg)針對B2B商家，您必須[安裝](install.md#install-the-b2b-extension) `experience-platform-connector-b2b`擴充功能才能存取這些事件。

B2B事件包含[請購單清單](https://experienceleague.adobe.com/docs/commerce-admin/b2b/requisition-lists/requisition-lists.html)資訊，例如，請購單清單是否已建立、新增或刪除。 透過追蹤請購單清單的特定事件，您可以檢視客戶經常購買哪些產品，並根據該資料建立行銷活動。

請參閱[開發人員檔案](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection)，深入瞭解B2B事件。
