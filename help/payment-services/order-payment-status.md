---
title: 訂單付款狀態報表
description: 使用「訂單付款狀態」報表，可檢視訂單的付款狀態，並識別任何可能的問題。
role: User
level: Intermediate
exl-id: 192e47b9-d52b-4dcf-a720-38459156fda4
feature: Payments, Checkout, Orders, Paas, Saas
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '2045'
ht-degree: 0%

---

# 訂單付款狀態報表

[!DNL Adobe Commerce]和[!DNL Magento Open Source]的[!DNL Payment Services]提供您完整的報告，以便您可以清楚瞭解商店的[交易](reporting.md)、訂單和付款。

有兩個可用的「訂單」付款狀態報表檢視表，可讓您快速檢視訂單的付款狀態：

* **[訂單付款狀態視覺化檢視表](#order-payment-status-data-visualization-view)** — 付款服務首頁上可用的圖表，可透過訂單付款狀態報表檢視表以視覺化方式呈現每日彙總的付款狀態
* **[訂單付款狀態報表檢視](#order-payment-status-report-view)** — 以訂單付款狀態顯示所有交易的詳細付款、已開立商業發票、已出貨、退款及爭議狀態的可用報表

「訂單」付款狀態檢視表可協助您輕鬆瞭解特定訂單在訂單至現金處理流程中的位置。 這些報表可讓您根據訂單的付款狀態和付款日期快速檢視訂單，並識別任何潛在問題。

您可以[下載.csv檔案格式的訂單付款狀態](#download-order-payment-statuses)，以用於現有的會計或訂單管理軟體。

>[!NOTE]
>
>如果您尚未為[!DNL Payment Services]上線並啟動即時模式[&#128279;](production.md#enable-live-payments)，則無法檢視財務報表。

## 訂單付款狀態資料視覺效果檢視

付款服務首頁提供「訂單付款狀態」資料視覺化檢視。 這是詳細表格[訂單付款狀態報表檢視](#order-payment-status-report-view)中每日彙總付款狀態的視覺化表示。

在&#x200B;_管理員_&#x200B;側邊欄上，前往&#x200B;**銷售** > **付款服務** > _訂單_，檢視資料視覺效果[付款狀態圖表](#statuses-information)。

在管理員中![支付資料視覺效果](assets/orderpayment-dataviz.png){width="800" zoomable="yes"}

按一下&#x200B;**[!UICONTROL View Report]**&#x200B;以瀏覽至詳細的表格[訂單付款狀態報表檢視](#order-payment-status-report-view)。

### 自訂狀態時間範圍

依預設，會顯示30天的付款狀態。

從「訂單付款狀態」視覺效果檢視中，您可以選取日期範圍，以自訂您要檢視之付款狀態的時間範圍：

1. 在&#x200B;_管理員_&#x200B;側邊欄上，移至&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**。 訂單付款狀態資料視覺化檢視會顯示在&#x200B;_訂單_&#x200B;區段中。
1. 按一下&#x200B;**[!UICONTROL Range]**&#x200B;選取器篩選器。
1. 選擇適用的日期範圍 — 30天、15天或7天。
1. 檢視指定日期的狀態資訊。

### 狀態資訊

所選日期範圍的付款狀態會顯示在「訂單付款狀態」資料視覺效果檢視的左側。 所選日期範圍的日期會顯示在檢視的底部。 如果特定日期沒有訂單，該日期就不會出現。

「訂單付款狀態」資料視覺效果檢視包括下列資訊。

| 資料 | 說明 |
| ------------ | -------------------- |
| [!UICONTROL Orders] | 指定時間範圍內訂單的金額範圍；Y軸上的資料（左側） |
| 日期範圍 | 指定時間範圍的日期範圍；X軸（底部）上的資料 |
| 已授權 | 訂單已授權 |
| 已要求擷取 | 訂單要求的擷取 |
| 擷取已確認 | 訂單擷取完成 |
| 部分擷取 | 部分擷取的訂單 |
| 擷取失敗 | 訂單擷取失敗 |
| 已失效 | 訂單已失效 |

## 訂單付款狀態報表檢視

「付款服務」的「首頁」檢視中，提供「訂單」付款狀態報表檢視表。 其中包括所有交易的詳細狀態 — 付款、已開立商業發票、出貨、退款、爭議等等。

在&#x200B;_Admin_&#x200B;側邊欄上，前往&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**&#x200B;檢視詳細的表格式訂單付款狀態報告檢視。

![管理員中的訂單付款狀態交易](assets/orders-report-data.png){width="800" zoomable="yes"}

您可以根據本主題中的章節設定此檢視，以最理想的方式呈現您想要檢視的資料。

您可以[以.csv檔案格式下載支付交易](#download-order-payment-statuses)，以用於現有的會計或訂單管理軟體。

>[!NOTE]
>
>此資料表中顯示的資料預設使用`TRANS DATE`以遞減順序(`DESC`)排序。 `TRANS DATE`是啟動交易的日期和時間。

### 付款狀態更新

某些付款方法需要一段時間才能擷取付款。 [!DNL Payment Services]現在會依照下列方式偵測到訂單中付款交易的擱置狀態：

* 同步偵測`pending capture`個交易
* 非同步監視`pending capture`個交易

>[!NOTE]
>
>偵測訂單中付款交易的暫緩狀態，可防止在尚未收到付款時意外出貨訂單。 電子支票和PayPal交易可能會發生這種情況。

#### 同步偵測擱置中的擷取交易

自動偵測處於`Pending`狀態的擷取交易，並在偵測到此類交易時，防止訂單進入`Processing`狀態。

在客戶結帳期間或管理員為先前授權的付款建立發票時，[!DNL Payment Services]會自動偵測`Pending`狀態的擷取交易，並將對應的訂單轉換為`Payment Review`狀態。

#### 非同步監視擱置中的擷取交易

偵測暫止的擷取交易何時進入`Completed`狀態，讓商家可以繼續處理受影響的訂單。

為確保此程式可如預期運作，商家必須設定新的cron工作。 一旦工作設定為自動執行，商家就不需要進行其他干預。

請參閱[設定cron工作](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs.html)。 設定之後，新工作每30分鐘執行一次，以擷取處於`Payment Review`狀態的訂單的更新。

商戶可以透過「訂單付款狀態」報表檢視來檢查更新的付款狀態。

### 報告中使用的資料

[!DNL Payment Services]使用訂單資料，並將其與其他來源（包括PayPal）的彙總付款資料結合，以提供有意義且非常有用的報表。

訂單資料會匯出並保留在付款服務中。 當您[變更或新增訂單狀態](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-status#custom-order-status)或[編輯商店檢視](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/store-views#edit-a-store-view)、[商店](https://experienceleague.adobe.com/en/docs/commerce-admin/start/setup/store-details#store-information)或網站名稱時，該資料會與付款資料結合，而訂單付款狀態報表會填入結合資訊。

此程式包含兩個步驟：

1. 索引已變更資料`ON SAVE` （每次變更訂單資訊或存放區資訊時）或`BY SCHEDULE` （依預先設定的cron排程），視它在管理員的[索引管理](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management)中的設定方式而定。

   依預設，資料索引會發生`ON SAVE`，這表示每當順序、訂單狀態、商店檢視、商店或網站發生變更時，索引程式就會立即發生。

1. 已編制索引的資料會傳送至付款服務，然後填入「訂單」付款狀態報表。

為報表目的匯出和整理的唯一資料是「訂單付款狀態」報表所使用的資料。

>[!NOTE]
>
>此資料表中顯示的資料預設使用`ORDER DATE`以遞減順序(`DESC`)排序。 `ORDER DATE`是建立訂單的日期時間戳記。

#### 設定資料匯出

即使預設會在`ON SAVE`模式下重新索引，仍建議您在`BY SCHEDULE`模式下索引。 `BY SCHEDULE`索引會以1分鐘的cron排程執行，且任何變更的資料會在任何資料變更後的2分鐘內顯示在您的「訂單狀態」報表中。 這個排程的重新索引可幫助您減少商店上的任何負擔，尤其是如果您有大量傳入的訂單，因為這會按照排程進行（而不是每次下訂單時）。

您可以在管理員[&#128279;](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management#change-the-index-mode)中變更索引模式 — `ON SAVE`或`BY SCHEDULE`—。

若要瞭解如何設定資料匯出，請參閱[命令列組態](configure-cli.md#configure-data-export)。

### 選取資料來源

在「訂單付款狀態」報表檢視中，您可以選取您要檢視其報表結果的資料來源 — **[!UICONTROL Live]** _或&#x200B;**[!UICONTROL Sandbox]**。

![資料來源選擇](assets/datasource.png){width="300" zoomable="yes"}

如果&#x200B;_[!UICONTROL Live]_&#x200B;是選取的資料來源，您可以看到在生產模式中使用[!DNL Payment Services]之存放區的報表資訊。 如果&#x200B;_[!UICONTROL Sandbox]_&#x200B;是選取的資料來源，您可以看到沙箱模式的報告資訊。

資料來源選取專案的工作方式如下：

* 如果您沒有任何在即時模式下使用[!DNL Payment Services]的存放區，則資料來源選取專案會預設為&#x200B;_[!UICONTROL Sandbox]_。
* 如果您有任何在即時模式下使用[!DNL Payment Services]的存放區（一或多個），資料來源選項會預設為&#x200B;_[!UICONTROL Live]_。
* 報表匯出一律遵循資料來源選擇。

若要選取[!UICONTROL Order Payment Status]報表的資料來源：

1. 在&#x200B;_管理員_&#x200B;側邊欄上，前往&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > **[!UICONTROL Orders]** > **[!UICONTROL View Report]**。
1. 按一下&#x200B;_[!UICONTROL Data source]_&#x200B;選取器篩選器，然後選取&#x200B;**[!UICONTROL Live]**&#x200B;或&#x200B;**[!UICONTROL Sandbox]**。

   報表結果會根據選取的資料來源重新產生。

### 自訂訂單日期時間範圍

從「訂單付款狀態」報表檢視中，您可以選取特定日期，以自訂您要檢視之狀態結果的時間範圍。 依預設，30天的訂單付款狀態會顯示在網格中。

1. 在&#x200B;_管理員_&#x200B;側邊欄上，前往&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**。
1. 按一下&#x200B;_[!UICONTROL Order dates]_&#x200B;行事曆選擇器篩選器。
1. 選擇適用的日期範圍。
1. 檢視網格中指定日期的訂單付款狀態。

### 篩選報表資訊

從「訂單付款狀態」報表檢視中，您可以選取篩選條件，以篩選您要檢視的狀態結果。

1. 在&#x200B;_管理員_&#x200B;側邊欄上，前往&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**。
1. 按一下&#x200B;**[!UICONTROL Filter]**&#x200B;選取器。
1. 切換&#x200B;_付款狀態_&#x200B;選項，只檢視所選訂單付款狀態的報表結果。
1. 輸入&#x200B;_[!UICONTROL Min Order Amount]_&#x200B;或_[!UICONTROL Max Order Amount_]，檢視訂單金額範圍內的報表結果。
1. 按一下&#x200B;**[!UICONTROL Hide filters]**&#x200B;以隱藏篩選器。

### 顯示和隱藏欄

「訂單付款狀態」報表依預設會顯示所有可用的資訊欄位。 不過，您可以自訂您在報表中看到的欄。

1. 在&#x200B;_管理員_&#x200B;側邊欄上，前往&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**。
1. 按一下&#x200B;_欄設定_&#x200B;圖示（![欄設定圖示](assets/column-settings.png){width="20" zoomable="yes"}）。
1. 若要自訂您在報表中看到的欄，請核取或取消核取清單中的欄。

   「訂單付款狀態」報表會立即顯示您在「欄位設定」功能表中所做的任何變更。 欄偏好設定會儲存，如果您離開報表檢視，偏好設定仍會維持有效。

### 檢視狀態

「訂單付款狀態」報表檢視會顯示每張訂單的完整付款狀態資訊。

依預設，30天的訂單付款狀態會顯示在網格中。

向左向右捲動以檢視[訂單付款狀態資訊](#column-descriptions)，包括訂單日期、授權日期、已開立商業發票、已出貨、付款狀態等。

搜尋中傳回的列數，或顯示在預設30天訂單付款狀態的列數，會與「訂單日期」行事曆選取器篩選器一起顯示在「訂單付款」狀態檢視網格的上方。

#### 付款狀態

「付款狀態」欄位會顯示任何付款的目前狀態。 `Capture failed`筆付款顯示紅色警示狀態，而`Voided`筆付款顯示灰色警示狀態。

#### 退款狀態

「退款」狀態列位會顯示任何退款的目前狀態。 `Capture failed`筆付款顯示紅色警示狀態，而`Voided`筆付款顯示灰色警示狀態。

### 更新報表資料

「訂單付款狀態」報表檢視會顯示&#x200B;_[!UICONTROL Last updated]_&#x200B;時間戳記，顯示上次更新報表資訊的時間。 依預設，訂單付款狀態報表資料每三小時自動重新整理一次。

您也可以手動強制重新整理「訂單付款狀態」報表資料，以檢視最新的報表資訊。

1. 在&#x200B;_管理員_&#x200B;側邊欄上，前往&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**。
1. 按一下&#x200B;_重新整理_&#x200B;圖示（![重新整理圖示](assets/refresh-button-med.png){width="20" zoomable="yes"}）。

   已重新整理訂單付款狀態報表資料，並顯示&#x200B;*[!UICONTROL Update complete]*&#x200B;確認訊息，且格線中顯示最新資訊。

### 檢視爭議

您可以檢視商店訂單上的任何爭議，並從「訂單付款狀態」報表中切換作業選項至「PayPal解決中心」以對其採取行動。

1. 在&#x200B;_管理員_&#x200B;側邊欄上，前往&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**。
1. 導覽至&#x200B;**[!UICONTROL Disputes column]**。
1. 檢視特定訂單的任何爭議，並檢視[爭議狀態](#order-payment-status-information)。
1. 按一下以&#x200B;_PP-D-_&#x200B;開頭的爭議ID連結，檢閱[PayPal解決中心](https://www.paypal.com/us/cshelp/article/what-is-the-resolution-center-help246)的爭議詳細資料。
1. 視需要對爭議採取適當行動。

   若要依狀態排序順序爭議，請按一下[!UICONTROL Disputes]欄標題。

### 下載訂單付款狀態

您可以下載.csv檔案，其中包含所有顯示在「訂單付款」狀態檢視格線中的狀態，無論您檢視的是預設的30天狀態還是自訂的時間範圍。

1. 在&#x200B;_管理員_&#x200B;側邊欄上，前往&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**。
1. 如果您想要檢視過去30天以外時間範圍的狀態，請[自訂您狀態的日期範圍時間範圍](#customize-dates-timeframe)。
1. 按一下「_下載_」（![下載圖示](assets/icon-download.png){width="20" zoomable="yes"}）圖示。

您的訂單付款狀態會以.csv格式下載。

### 欄說明

訂單付款狀態報表包含下列資訊。

| 欄 | 說明 |
| ------------ | -------------------- |
| [!UICONTROL Order ID] | Commerce訂單ID<br> <br>若要檢視相關的[訂單資訊](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/orders){target="_blank"}，請按一下ID。 |
| [!UICONTROL Order Date] | 訂購日期時間戳記 |
| [!UICONTROL Authorized Date] | 付款授權的日期時間戳記 |
| [!UICONTROL Order Status] | 目前的Commerce [訂單狀態](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-status){target="_blank"} |
| [!UICONTROL Invoiced] | 訂單的商業發票狀態 — *[!UICONTROL No]*、*[!UICONTROL Partial]*&#x200B;或&#x200B;*[!UICONTROL Yes]* |
| [!UICONTROL Shipped] | 訂單的運送狀態 — *[!UICONTROL No]*、*[!UICONTROL Partial]*&#x200B;或&#x200B;*[!UICONTROL Yes]* |
| [!UICONTROL Order Amt] | 訂單的總金額 |
| [!UICONTROL Cur] | 訂單的貨幣型別 |
| [!UICONTROL Pay Status] | 特定訂單的付款狀態 |
| [!UICONTROL Paid Amt] | 訂單上的已付金額 |
| [!UICONTROL Cur] | 訂單付款金額的幣別型別 |
| [!UICONTROL Refund Status] | 訂單上的退款狀態（例如退貨、RMA及銷退折讓單的資訊） —    *[!UICONTROL Requires refund]*、*[!UICONTROL Refund requested]*、*[!UICONTROL Refunded]*、*[!UICONTROL Refund failed]*&#x200B;或&#x200B;*[!UICONTROL Voided]* |
| [!UICONTROL Refund Amount] | 訂單的已退款金額總計 |
| [!UICONTROL Cur] | 訂單退款金額的幣別型態 |
| [!UICONTROL Disputes] | 訂單上的任何爭議狀態（爭議和借項衝回的資訊） — *[!UICONTROL Open]*、*[!UICONTROL Waiting for buyer response]*、*[!UICONTROL Waiting for seller response]*、*[!UICONTROL Under review]*、*[!UICONTROL Resolved]*&#x200B;或&#x200B;*[!UICONTROL Other]* |
| [!UICONTROL Payment Method] | 訂單的Commerce交易中使用的付款方法 |
| [!UICONTROL Website] | 下訂單的網站 |
| [!UICONTROL Store] | 下訂單的存放區 |
| [!UICONTROL Store View] | 下訂單的存放區檢視 |
