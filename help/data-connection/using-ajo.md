---
title: 使用Adobe Journey Optimizer傳送捨棄的購物車電子郵件
description: 瞭解如何使用Adobe Journey Optimizer傳送捨棄的購物車電子郵件。
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1262'
ht-degree: 0%

---

# 使用Adobe Journey Optimizer傳送捨棄的購物車電子郵件

瞭解如何在購物車或瀏覽器工作階段已放棄時傳遞個人化重新參與電子郵件或通知。 在本文中，您會使用客戶產生的資料，這些客戶已檢視許多產品和類別、參與產品或花費在頁面上。

## 我應考慮使用哪些資料？

使用店面和後台事件的資料，建立捨棄的購物車、瀏覽電子郵件或通知。

| 資料型別 | 店面資料（行為事件） | 後台資料（伺服器端事件） |
|---|---|---|
| **定義** | 客戶在您網站上採取的點按或動作。 | 生命週期相關資訊和每個訂單（過去和目前）的詳細資訊。 |
| 由Adobe Commerce擷取的&#x200B;**個事件** | [pageView](https://experienceleague.adobe.com/zh-hant/docs/commerce/data-connection/event-forwarding/events#pageview)<br>[productPageView](https://experienceleague.adobe.com/zh-hant/docs/commerce/data-connection/event-forwarding/events)<br>[addToCart](https://experienceleague.adobe.com/zh-hant/docs/commerce/data-connection/event-forwarding/events#addtocart)<br>[openCart](https://experienceleague.adobe.com/zh-hant/docs/commerce/data-connection/event-forwarding/events#opencart)<br>[startCheckout](https://experienceleague.adobe.com/zh-hant/docs/commerce/data-connection/event-forwarding/events#startcheckout)<br>[completeCheckout](https://experienceleague.adobe.com/zh-hant/docs/commerce/data-connection/event-forwarding/events#completecheckout) | [orderPlaced](https://experienceleague.adobe.com/zh-hant/docs/commerce/data-connection/event-forwarding/events-backoffice#orderplaced)<br>[訂單歷史記錄](https://experienceleague.adobe.com/zh-hant/docs/commerce/data-connection/fundamentals/connect-data#send-historical-order-data) |

### 其他客戶都取得了哪些成就？

Adobe [!DNL Commerce]客戶透過Adobe [!DNL Commerce]、Adobe [!DNL Journey Optimizer]和Adobe [!DNL Real-Time CDP]實作個人化的放棄行銷活動，已取得顯著的業務影響。

一家全球多品牌服裝零售商達成：

- 來自新行銷活動的1.9倍點選轉換
- 來自全頻道放棄歷程的收入增加57%
- 重新參與行銷活動的轉換率增加41%
- 每週有1000多名新購物者參與

一家全球飲料公司達成：

- 36%重新參與電子郵件開啟率
- 點進率提升21%
- 轉換率提升8.5%
- 89%的重新參與放棄者轉換

## 讓我們開始吧

此特定使用案例著重於使用您[!DNL Commerce]執行個體的資料來建立捨棄的購物車電子郵件，並將其傳送至Adobe [!DNL Journey Optimizer]。

### 什麼是Adobe Journey Optimizer？

[Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=zh-Hant)可協助您為購物者打造個人化的商務體驗。 例如，您可以使用Journey Optimizer建立並傳送排程行銷活動（例如零售商店的每週促銷活動），或如果客戶將產品加入購物車但未完成結帳程式，則產生放棄的購物車電子郵件。

在此主題中，您將瞭解如何藉由聆聽從您的[!DNL Commerce]執行個體產生的`checkout`事件並在Journey Optimizer中回應該事件，建置捨棄的購物車電子郵件。

>[!IMPORTANT]
>
>為了示範，請使用您的[!DNL Commerce]沙箱環境，這樣您就不會因為傳送至Experience Platform的店面和後台事件資料而稀釋生產事件資料。

### 先決條件

開始這些步驟之前，請確定：

- 您已布建為使用Adobe [!DNL Journey Optimizer]。 如果您不確定，請洽詢您的系統整合商或管理專案和環境的開發團隊。
- 您[已安裝](install.md)且[已設定](connect-data.md) [!DNL Commerce]中的[!DNL Data Connection]延伸模組。
- 您[已確認](connect-data.md#confirm-that-event-data-is-collected)您的[!DNL Commerce]事件資料已送達Experience Platform Edge。

## 步驟1：在您的[!DNL Commerce]沙箱環境中建立使用者

在您的沙箱環境中建立使用者，並確認該使用者帳戶資訊會顯示在Experience Platform中。 請確認您指定的電子郵件有效，如同稍後在本節中用來傳送捨棄的購物車電子郵件一樣。

1. 在您的[!DNL Commerce]沙箱環境中登入或建立帳戶。

   ![登入您的測試帳戶](assets/sign-in-account.png){width="700" zoomable="yes"}

   在安裝及設定[!DNL Data Connection]擴充功能後，此帳戶資訊會以設定檔傳送至Experience Platform。

1. 確認您的使用者帳戶資訊會顯示在Experience Platform的&#x200B;**[!UICONTROL Profile]**&#x200B;區段中。

   前往Adobe Experience Platform中的&#x200B;**[!UICONTROL Profiles]**。 按一下設定檔中的&#x200B;**[!UICONTROL Detail]**&#x200B;以檢視您建立的設定檔。

   ![確認設定檔](assets/check-event-profile.png){width="700" zoomable="yes"}

## 步驟2：在Journey Optimizer中檢視事件

在您的[!DNL Commerce]沙箱環境中，檢視產品頁面、將專案新增至購物車並完成購物者將執行的各種其他活動，以觸發店面上的事件。 然後，確認這些事件正在流入Journey Optimizer。

1. 啟動[Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/user-interface.html?lang=zh-Hant)。
1. 選取&#x200B;**[!UICONTROL Profiles]**。
1. 將&#x200B;**[!UICONTROL Identity namespace]**&#x200B;設為`Email`。
1. 將&#x200B;**[!UICONTROL Identity value]**&#x200B;設定為您的電子郵件地址。
1. 選取您的設定檔，然後選取「**[!UICONTROL Events]**」標籤。

   ![檢查事件詳細資料](assets/check-event-details.png){width="700" zoomable="yes"}

   尋找`commerce.checkouts`事件並檢查事件裝載：

   ```json
   "personID": "84281643067178465783746543501073369488", 
   "eventType": "commerce.checkouts", 
   "_id": "4b41703f-e42e-485b-8d63-7001e3580856-0", 
   "commerce": { 
       "cart": {}, 
       "checkouts": { 
           "value": 1 
       } 
   ```

   如您所見，完整的事件裝載包含豐富的事件資料。 在下一節中，您將設定Journey Optimizer中的事件以接聽並回應從您的[!DNL Commerce]店面產生的`commerce.checkouts`事件。

## 步驟3：在Journey Optimizer中設定事件

在Journey Optimizer中設定兩個事件：一個事件監聽Commerce的`commerce.checkouts`事件，另一個是基本逾時事件，會等待經過特定時間後再觸發捨棄的購物車電子郵件。

### 建立監聽器事件

1. 啟動[Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/user-interface.html?lang=zh-Hant)。

1. 按一下左窗格&#x200B;**[!UICONTROL Administration]**&#x200B;區段下的&#x200B;**[!UICONTROL Configurations]**。

1. 在&#x200B;**[!UICONTROL Events]**&#x200B;圖磚中，按一下&#x200B;**[!UICONTROL Manage]**。

   ![Journey Optimizer事件設定](assets/ajo-config.png){width="700" zoomable="yes"}

1. 在&#x200B;**[!UICONTROL Events]**&#x200B;頁面上，按一下&#x200B;**[!UICONTROL Create Event]**。

1. 在右側導覽區域中，設定您的事件，如下所示：

   1. 將&#x200B;**[!UICONTROL Name]**&#x200B;設為： `firstname_lastname_checkout`。
   1. 將&#x200B;**[!UICONTROL Type]**&#x200B;設為&#x200B;**[!UICONTROL Unitary]**。
   1. 將&#x200B;**[!UICONTROL Event id typ]e**&#x200B;設為&#x200B;**[!UICONTROL Rule based]**。
   1. 將&#x200B;**[!UICONTROL Schema]**&#x200B;設定為您的[!DNL Commerce] [結構描述](update-xdm.md)。
   1. 選取&#x200B;**[!UICONTROL Fields]**&#x200B;以開啟&#x200B;**[!UICONTROL Fields]**&#x200B;頁面。 然後，選取對此事件有用的欄位。 例如，選取&#x200B;**[!UICONTROL Product list items]**、**[!UICONTROL Commerce]**、**[!UICONTROL eventType]**&#x200B;和&#x200B;**[!UICONTROL Web]**&#x200B;下的所有欄位。
   1. 按一下&#x200B;**[!UICONTROL OK]**&#x200B;以儲存選取的欄位。
   1. 在&#x200B;**[!UICONTROL Event id condition]**&#x200B;欄位內按一下。 然後，建立條件： `eventType`等於`commerce.checkouts`，`personalEmail.address`等於您在上一節建立設定檔時使用的電子郵件地址。

      ![Journey Optimizer設定條件](assets/ajo-set-condition.png){width="700" zoomable="yes"}

   1. 按一下&#x200B;**[!UICONTROL OK]**。
   1. 按一下&#x200B;**[!UICONTROL Save]**&#x200B;以儲存您的事件。

### 建立逾時事件

1. 在Journey Optimizer中建立事件，就像您之前做的那樣。

1. 在右側導覽區域中，設定您的事件，如下所示：

   1. 將&#x200B;**[!UICONTROL Name]**&#x200B;設為： `firstname_lastname_timeout`。
   1. 將&#x200B;**[!UICONTROL Type]**&#x200B;設為&#x200B;**[!UICONTROL Unitary]**。
   1. 將&#x200B;**[!UICONTROL Event id type]**&#x200B;設為&#x200B;**[!UICONTROL Rule based]**。
   1. 將&#x200B;**[!UICONTROL Schema]**&#x200B;設定為您的[!DNL Commerce] [結構描述](update-xdm.md)。
   1. 將&#x200B;**[!UICONTROL Schema]**、**[!UICONTROL Fields]**&#x200B;和&#x200B;**[!UICONTROL Event id condition]**&#x200B;設定為與上述相同。
   1. 按一下&#x200B;**[!UICONTROL Save]**&#x200B;以儲存您的事件。

在設定這兩個事件後，建立傳送捨棄購物車電子郵件的歷程。

## 步驟4：建立結帳歷程

建立監聽`commerce.checkouts`事件的歷程，然後在經過指定時間後傳送捨棄的購物車電子郵件。

1. 在Journey Optimizer中，選取&#x200B;**J[!UICONTROL OURNEY MANAGEMENT]**&#x200B;下的&#x200B;**[!UICONTROL Journeys]**。
1. 按一下&#x200B;**[!UICONTROL Create Journey]**。
1. 指定歷程的名稱。
1. 按一下&#x200B;**[!UICONTROL OK]**&#x200B;以儲存歷程。
1. 在左側導覽列中的&#x200B;**[!UICONTROL EVENTS]**&#x200B;區段下，搜尋您先前建立的結帳事件： `firstname_lastname_checkout`並將其拖放到畫布上。

   >[!TIP]
   >
   >連按兩下事件會自動將其新增至畫布。

1. 搜尋逾時事件並將其新增至畫布。
1. 按兩下逾時事件。

   1. 在&#x200B;**[!UICONTROL Timeout]**&#x200B;區段中，選取&#x200B;**[!UICONTROL Define the event time]**&#x200B;核取方塊。
   1. 在&#x200B;**[!UICONTROL Wait for]**&#x200B;欄位中輸入`1`和`Minute`。
   1. 選取&#x200B;**[!UICONTROL Set a timeout path]**&#x200B;核取方塊。

   透過此逾時設定，執行結帳但未在一分鐘內完成訂單的購物者會觸發此逾時分支。 在實際生產環境中，您可以設定較長的時間，例如24小時。

1. 在&#x200B;**[!UICONTROL ACTIONS]**&#x200B;下的左側導覽中，將&#x200B;**[!UICONTROL Email]**&#x200B;動作新增至逾時分支。 您的歷程應如下所示：

   ![Journey Optimizer畫布](assets/ajo-canvas.png){width="700" zoomable="yes"}

### 建立捨棄的購物車電子郵件

建立捨棄的購物車電子郵件，在偵測到捨棄的購物車時傳送。

1. 在您上述建立的歷程中，按兩下畫布上的&#x200B;**[!UICONTROL Email]**&#x200B;圖示。

1. 依照Journey Optimizer指南中的[步驟](https://experienceleague.adobe.com/docs/journey-optimizer/using/content-management/personalization/personalization-use-cases/personalization-use-case-helper-functions.html?lang=zh-Hant#configure-email)建立捨棄的購物車電子郵件。

您現在在Journey Optimizer中有一個從您的[!DNL Commerce]商店監聽`commerce.checkouts`事件的歷程，以及一個一段時間後傳送的捨棄購物車電子郵件。 下一節將說明如何測試歷程。

## 步驟5：即時觸發結帳事件

在本節中，您將即時測試事件。

1. 在Journey Optimizer中，切換為測試模式。

   ![啟用測試模式](assets/ajo-enable-test.png){width="700" zoomable="yes"}

1. 若要即時測試此歷程，請開啟另一個瀏覽器分頁，然後前往您沙箱環境中的[!DNL Commerce]網站。

   1. 新增產品至購物車。
   1. 前往結帳頁面。
   1. 從結帳頁面，返回首頁面或關閉標籤以捨棄購物車。

      歷程現在已觸發。 若要確認，請在Journey Optimizer中開啟擁有您歷程的標籤。 您應該會看到綠色箭頭，顯示使用者瀏覽的路徑。

1. 檢查您的收件匣中是否有電子郵件。
