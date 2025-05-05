---
title: 使用 [!DNL Commerce] 事件資料在Real-Time CDP中建立對象
description: 瞭解如何使用 [!DNL Commerce] 事件資料在Real-Time CDP中建立對象
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 0%

---

# 使用[!DNL Commerce]事件資料在Real-Time CDP中建立對象

使用從您的[!DNL Commerce]存放區擷取的事件資料，在Real-Time CDP中建立對象。 擷取的資料會根據瀏覽行為、過去的購買、設定檔屬性、轉換或流失的傾向、忠誠度狀態、高和低客戶價值等。

## 我應考慮使用哪些資料？

使用店面、後台和設定檔事件的資料，在Real-Time CDP中建立對象。

| 資料型別 | 店面資料（行為事件） | 後台資料（伺服器端事件） | 客戶設定檔和區段資料 |
|---|---|---|---|
| **定義** | 客戶在您網站上採取的點按或動作。 | 生命週期相關資訊和每個訂單（過去和目前）的詳細資訊。 | 您的購物者是誰，以及他們符合哪些區段的資格。 |
| 由Adobe Commerce擷取的&#x200B;**個事件** | [productPageView](events.md#productpageview)<br>[addToCart](events.md#addtocart) | [placeOrder](events.md#completecheckout)<br>[orderplaced](events-backoffice.md#orderplaced)<br>[orderLineItemRefolled](events-backoffice.md#orderlineitemrefunded)<br>[訂單已取消](events-backoffice.md#ordercancelled)<br>[訂單歷史記錄](connect-data.md#send-historical-order-data) | [createAccount](events.md#createaccount)<br>[editAccount](events.md#editaccount)<br>[設定檔記錄](events-profilerecord.md) |

## 其他客戶都取得了哪些成就？

Adobe [!DNL Commerce]客戶透過啟用Real-Time CDP中建置的受眾並將其部署至其[!DNL Commerce]執行個體，已取得顯著的業務影響。

一家全球多品牌服裝零售商達成：

- 擁有數百萬個統一客戶設定檔的單一信任來源
- 建立40多個「高意圖客戶」的不重複受眾，以跨管道參與

一家全球飲料公司收集到：

- 來自100多個國家/地區的9,800萬個客戶設定檔

## 讓我們開始吧

在本文中，您將瞭解如何：

- 根據事件收集的[!DNL Commerce]資料在Real-Time CDP中建立對象
- 啟用您[!DNL Commerce]存放區的對象
- 在[!DNL Commerce]中使用對象來通知購物車價格規則

>[!IMPORTANT]
>
>使用您的[!DNL Commerce]沙箱環境完成本文所述的工作。 這可確保您傳送至Experience Platform的店面和後台事件資料不會稀釋您的生產事件資料。

### 先決條件

開始之前，請確定：

- 您已布建為可使用Real-Time CDP。 如果您不確定，請洽詢您的系統整合商或管理專案和環境的開發團隊。
- 您[已安裝](install.md)且[已設定](connect-data.md) [!DNL Commerce]中的[!DNL Data Connection]延伸模組。
- 您[已確認](connect-data.md#confirm-that-event-data-is-collected)您的[!DNL Commerce]事件資料已送達Experience Platform Edge。

### 1.建立對象

受眾是一組具有類似行為或特徵的客戶。 在本練習中，您會建立受眾，使對您商店中特定產品感興趣的人員符合資格。

若要簡化此練習，請使用[productPageView](events.md#productpageview)事件的事件資料。 此事件會擷取有關已檢視產品的詳細資訊，例如產品名稱、SKU、價格等。

使用此事件資料可指定對象包含至少有一個「產品檢視」事件的個人，其中SKU （產品識別碼）等於網站上的特定產品，且該事件發生在前一天。&#x200B;URL

1. 開啟Experience Platform，然後從左側導覽選單中選取&#x200B;**[!UICONTROL Audiences]**。

   ![對象儀表板](assets/audience-left-rail.png)

1. 按一下&#x200B;**[!UICONTROL Create Audience]**。

   ![建立對象](assets/browse-create-audience.png)

   **區段產生器**&#x200B;工作區隨即顯示。

1. 在&#x200B;**區段產生器**&#x200B;工作區中，選取&#x200B;**建置規則**&#x200B;建立方法。

   ![建置規則](assets/build-rule.png)

   **區段產生器**&#x200B;工作區是您為對象定義規則和條件的地方&#x200B;。 這些規則和條件以您Commerce存放區中的事件和設定檔資料為基礎，並定義判斷使用者是否符合對象資格的條件。 例如，您可以建立規則，納入已檢視特定產品的使用者，或在特定時間範圍內購買的使用者。 深入瞭解[區段產生器](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/segmentation/ui/segment-builder)以及規則和條件。

1. 選取[事件](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/segmentation/ui/segment-builder#events)標籤。

   ![事件標籤](assets/audience-events-tab.png)

1. 搜尋「產品檢視」事件型別。 然後，將其拖放至&#x200B;**區段產生器**&#x200B;工作區。

1. 返回&#x200B;**事件**&#x200B;索引標籤並搜尋「SKU」，這是`productListItems`欄位下的資料欄位。 將其拖放至&#x200B;**區段產生器**&#x200B;工作區的&#x200B;**產品檢視**&#x200B;事件上。

   **事件規則**&#x200B;區段隨即顯示，您可以在其中指定要用來建立對象的特定產品。

   ![選取SKU](assets/audience-addsku.png)

1. 按一下&#x200B;**任何時間**&#x200B;並選取值為&#x200B;*1*&#x200B;的&#x200B;*在最後*&#x200B;內，將時間間隔設定為一天。

   建立對象時，您可以指定擷取最近活動的時間間隔。 設定時間間隔可讓您根據使用者在特定時間範圍內最近的互動或行為來鎖定使用者。

1. 在工作區右側的&#x200B;**對象屬性**&#x200B;區段中，提供對象的名稱、說明和評估方法來設定對象屬性。

1. 若要儲存對象，請按一下&#x200B;**[!UICONTROL Save and Close]**。

   您對象的詳細資訊會顯示在&#x200B;**對象**&#x200B;儀表板上。

### 2.對[!DNL Commerce]目的地啟用對象

您透過為[!DNL Commerce]目的地啟用對象，使其可在[!DNL Commerce]中使用。

>[!IMPORTANT]
>
>如果您尚未將[!DNL Commerce]設定為可接收資料的可用目的地，請參閱[Adobe [!DNL Commerce] 連線](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/destinations/catalog/personalization/adobe-commerce)主題。

1. 在您對象的&#x200B;**詳細資料**&#x200B;標籤中，按一下&#x200B;**啟用至目的地**。

1. 選取您的[!DNL Commerce]目的地。 然後，按一下&#x200B;**下一步**。

1. 按一下&#x200B;**[!UICONTROL Finish]**&#x200B;完成啟動程式。

## 3.在「對象控制面板」中檢視對象

在[!DNL Commerce]中，您可以使用&#x200B;**Real-Time CDP Audiences**&#x200B;儀表板，檢視可為您的[!DNL Commerce]執行個體個人化的所有[作用中](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations)對象。

若要存取&#x200B;**Real-Time CDP Audiences**&#x200B;儀表板，請前往&#x200B;_管理員_&#x200B;側邊欄，然後前往&#x200B;**[!UICONTROL Customers]** > **[!UICONTROL Real-time CDP Audience]**。

在控制面板中，尋找您建立的對象。 請注意，購物車價格規則或動態區塊中並未使用它。 在下一節中，您會將對象連結至購物車價格規則。

![Real-Time CDP受眾控制面板](assets/real-time-cdp-dashboard.png)

### 4.根據對象建立購物車價格規則

本節說明如何根據新對象建立購物車價格規則。

1. 確認您的新對象顯示在&#x200B;**Real-Time CDP Audiences**&#x200B;儀表板中。
1. [建立購物車價格規則](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-create)。
1. [使用您的新對象設定購物車價格規則的條件](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-create#use-real-time-cdp-audiences-to-set-a-condition)。
1. [設定當產品加入購物車時要發生的動作](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-create#step-3-define-the-actions)。
1. 繼續設定購物車價格規則。
1. 前往沙箱執行個體的客戶檢視。
1. 將您根據對象的產品新增至購物車。 請注意，購物車價格規則已啟用。

## 總結

在本練習中，您已在Real-Time CDP中建立受眾，並將其啟動至[!DNL Commerce]目的地。 然後，在[!DNL Commerce]管理員中，您根據該對象建立了購物車價格規則，並在您的沙箱環境中啟用了規則。
