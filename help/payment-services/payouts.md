---
title: 支付報表
description: 使用「付款」報表，可完全透明地顯示付款金額、已處理數量，以及財務調節之交易層次的詳細報表。
role: User
level: Intermediate
exl-id: f3f99474-cd28-4c8f-b0ea-dca8e014b108
feature: Payments, Checkout, Paas, Saas
source-git-commit: a0f9ddbf3d0f291855cb51fd70a782c48b8efc6c
workflow-type: tm+mt
source-wordcount: '1303'
ht-degree: 0%

---

# 支付報表

[!DNL Payment Services]和[!DNL Adobe Commerce]的[!DNL Magento Open Source]為您提供完整的報告，以便您清楚瞭解商店的交易、訂單和付款。

有兩個可用的「付款」報表檢視表，可讓您檢視所有付款的深入資訊：

* **[付款資料視覺化檢視表](#payouts-data-visualization-view)** — 付款服務首頁上可用的圖表，以視覺化方式呈現付款報表檢視表中的每日彙總金額
* **[付款報表檢視](#payouts-report-view)** — 付款中可用的報表，可顯示所有交易的詳細付款資訊

「付款」檢視表一目瞭然地顯示完整的付款資訊，可讓您完全透明地顯示付款金額、已處理的數量，以及財務調節之交易層次的詳細報表。

您可以[以.csv檔案格式下載支付交易](#download-transactions)，以用於現有的會計或訂單管理軟體。

>[!NOTE]
>
>付款報表只會顯示擷取的訂單（付款動作設定為[`Authorize and Capture`](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/production.html?lang=zh-Hant#set-payment-services-as-payment-method)） — 或[標籤為`Invoiced`](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice)。

## 支付資料視覺效果檢視

支付資料視覺化檢視可在支付服務首頁取得。 這是從詳細的表格[支付報告檢視](#payouts-report-view)以視覺化方式呈現每日彙總金額。

在&#x200B;_管理員_&#x200B;側邊欄上，前往&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**&#x200B;檢視信用與借項的資料視覺化圖表，以及一段時間的移動平均值。

在管理員中![支付資料視覺效果](assets/payouts-report.png){width="800" zoomable="yes"}

按一下&#x200B;**[!UICONTROL View Report]**&#x200B;以瀏覽至詳細的表格[支付報告檢視](#payouts-report-view)。

### 自訂交易時間範圍

依預設，會顯示30天的交易。

從「付款資料」視覺效果檢視中，您可以選取日期範圍，以自訂您要檢視之付款交易的時間範圍：

1. 在&#x200B;_管理員_&#x200B;側邊欄上，移至&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**。 「付款」資料視覺效果檢視會顯示在「付款」區段中。
1. 按一下&#x200B;**[!UICONTROL Range]**&#x200B;選取器篩選器。
1. 選擇適用的日期範圍 — 30天、15天或7天。
1. 檢視指定日期的交易資訊。

### 交易資訊

所選日期範圍的交易金額會顯示在「付款」資料視覺化檢視的左側。 所選日期範圍的日期會顯示在檢視的底部。 如果特定日期沒有付款，該日期將不會顯示。

「付款」資料視覺效果檢視包含下列資訊。

| 資料 | 說明 |
| ------------ | -------------------- |
| [!UICONTROL Transaction amount] | 指定時間範圍內交易的金額範圍；Y軸上的資料（左側） |
| 日期範圍 | 指定時間範圍的日期範圍；X軸（底部）上的資料 |
| 來源 | 指定時間範圍的付款 |
| 借方 | 指定時間範圍內的借方（退款） |
| 移動平均 | 表示指定時間範圍內每個日期的平均派息 |
| 範圍的淨值 | 指定時間範圍（範圍）的淨支付金額 |

## 支付報表檢視

「付款服務」的「付款」檢視表中提供「付款」報表檢視表。 其中包含有關您商店付款的所有可用資訊。

在&#x200B;_Admin_&#x200B;側邊欄上，前往&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** > _[!UICONTROL Payouts]_>**[!UICONTROL View Report]**&#x200B;檢視詳細的表格式支付報告檢視。

管理員中的![付款交易](assets/payouts-report-new.png){width="800" zoomable="yes"}

您可以根據本主題中的章節設定此檢視，以最理想的方式呈現您想要檢視的資料。

請參閱此報表中的連結Commerce訂單與交易ID、交易金額、每筆交易的付款方式及其他。

您可以[以.csv檔案格式下載支付交易](#download-transactions)，以用於現有的會計或訂單管理軟體。

>[!NOTE]
>
>此資料表中顯示的資料預設使用`DESC`以遞減順序(`TRANS DATE`)排序。 `TRANS DATE`是啟動交易的日期和時間。

### 選取資料來源

在「付款」報表檢視中，您可以選取您要檢視其報表結果的資料來源 — **[!UICONTROL Live]**&#x200B;或&#x200B;**[!UICONTROL Sandbox]**。

![資料來源選擇](assets/datasource.png){width="300" zoomable="yes"}

如果&#x200B;_[!UICONTROL Live]_&#x200B;是選取的資料來源，您可以看到生產模式中存放區的報表資訊。 如果&#x200B;_[!UICONTROL Sandbox]_&#x200B;是選取的資料來源，您會看到以沙箱模式儲存的報告資訊。

資料來源選取專案的工作方式如下：

* 如果您沒有任何處於即時模式的存放區，資料來源選項會預設為&#x200B;_[!UICONTROL Sandbox]_。
* 如果您在即時模式中有任何存放區（一或多個），資料來源選項會預設為&#x200B;_[!UICONTROL Live]_。
* 報表匯出一律遵循資料來源選擇。

若要選取「訂單付款狀態」報表的資料來源，請執行下列步驟：

1. 在&#x200B;_管理員_&#x200B;側邊欄上，前往&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** > _[!UICONTROL Payouts]_>**[!UICONTROL View Report]**。
1. 按一下&#x200B;**[!UICONTROL Data source]**&#x200B;並選取&#x200B;**[!UICONTROL Live]**&#x200B;或&#x200B;**[!UICONTROL Sandbox]**。

   報表結果會根據選取的資料來源重新產生。

### 檢視交易

依預設，會顯示30天的交易。

搜尋中傳回或顯示在預設30天交易中的列數，會與「交易日期」行事曆選取器篩選器一起顯示在「付款」檢視網格上方。

向左及向右捲動，檢視每日報表中每個支付交易[的](#column-descriptions)資訊，包括交易日期、參考ID、商業發票號碼及付款方式詳細資料。

#### 自訂交易時間範圍

在「付款報表」檢視中，您可以輸入特定日期或從日期選擇器選取日期範圍，以自訂您要檢視之付款交易的時間範圍：

1. 在&#x200B;_管理員_&#x200B;側邊欄上，前往&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** > _[!UICONTROL Payouts]_>**[!UICONTROL View Report]**。
1. 按一下&#x200B;_[!UICONTROL Transaction dates]_&#x200B;行事曆選擇器篩選器。
1. 選擇適用的日期範圍。
1. 檢視網格中指定日期的付款狀態。

### 顯示和隱藏欄

依預設，「付款」報表檢視會顯示大部分可用的資訊欄。 不過，您可以自訂您在報表中看到的欄。

1. 在&#x200B;_管理員_&#x200B;側邊欄上，前往&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Payouts]_>**[!UICONTROL View Report]**。
1. 按一下&#x200B;_欄設定_&#x200B;圖示（![欄設定圖示](assets/column-settings.png){width="20" zoomable="yes"}）。
1. 若要自訂您在報表中看到的欄，請核取或取消核取清單中的欄。

   「付款」報表檢視會立即顯示您在「欄設定」功能表中所做的任何變更。 欄偏好設定將會儲存，而且如果您離開報表檢視，偏好設定將維持有效。

### 下載交易

您可以下載一個.csv檔案，其中包含「付款」檢視格線中顯示的所有交易。

1. 在&#x200B;_管理員_&#x200B;側邊欄上，前往&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** > _[!UICONTROL Payouts]_>**[!UICONTROL View Report]**。
1. [自訂交易的日期範圍時間範圍](#customize-transactions-timeframe)。
1. 按一下「_下載_」（「![下載」圖示](assets/icon-download.png){width="20" zoomable="yes"}）圖示。

您的付款交易會以.csv格式下載。

### 欄說明

支付報表包含下列資訊。

| 欄 | 說明 |
| ------------ | -------------------- |
| [!UICONTROL Provider] | 付款提供者 |
| [!UICONTROL Provider trans] | 交易ID |
| [!UICONTROL Trans date] | 啟動交易的日期和時間 |
| [!UICONTROL Type] | 交易型別 — *[!UICONTROL PAYMENT]*，*[!UICONTROL BONUS]*，*[!UICONTROL CHARGEBACK]*，*[!UICONTROL CORRECTION]*，*[!UICONTROL CURRENCY_CONVERSATION]*，*[!UICONTROL DEPOSIT]*，*[!UICONTROL DISBURSEMENT]*，*[!UICONTROL DISPUTE]*，*[!UICONTROL FEES]*，*[!UICONTROL HOLD]*，*[!UICONTROL HOLD_RELEASE]*，*[!UICONTROL INCENTIVES]*，*[!UICONTROL OTHERS]*，*[!UICONTROL RECOUP]*，*[!UICONTROL REFUND]*，*[!UICONTROL REVERSAL]*，*[!UICONTROL WITHDRAWAL]* <br> <br>如需詳細資訊，請參閱[交易型別](#transaction-types)。 |
| [!UICONTROL Status] | 交易的目前狀態 — *[!UICONTROL SUCCESS]*， *[!UICONTROL DENIED]*， *[!UICONTROL PENDING]* |
| [!UICONTROL Code] | 表示貸方(*CR*)或借方(*DR*)的交易代碼 |
| [!UICONTROL Reference ID] | 與此事件相關的原始交易ID |
| [!UICONTROL Invoice] | 交易的商業發票ID （每張訂單一個） |
| [!UICONTROL Commerce order] | Commerce訂單ID <br> <br>若要檢視相關的[訂單資訊](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/stores-sales/order-management/orders/orders)，請按一下ID。 |
| [!UICONTROL Commerce trans] | Commerce交易ID |
| [!UICONTROL Pay method] | 信用卡型別 — *[!UICONTROL BANK]*、*[!UICONTROL PAYPAL]*、*[!UICONTROL CREDIT_CARD]* — 和相關聯的卡片提供者（例如&#x200B;*Visa*&#x200B;或&#x200B;*MasterCard*） |
| [!UICONTROL TRANS AMT] | 交易金額 |
| [!UICONTROL CUR] | 交易金額的貨幣單位 |
| [!UICONTROL PENDING] | 尚未支付的金額 |
| [!UICONTROL CUR] | 暫緩金額的貨幣單位 |
| [!UICONTROL SELLER AMT] | 轉給客戶或從客戶轉出的資金金額<br> <br>從賣家帳戶移出的基金會顯示破折號(-)首碼。 |
| [!UICONTROL CUR] | 賣家金額的貨幣單位 |
| [!UICONTROL PARTNER FEE] | 與交易<br>相關的夥伴費用 <br>從合作夥伴費用帳戶移出的基金會顯示破折號(-)首碼。 |
| [!UICONTROL CUR] | 合作夥伴費用的貨幣單位 |
| [!UICONTROL PROV FEES] | 與交易<br>相關的費用 <br>資金移出提供者的費用帳戶會顯示破折號(-)前置詞。 |
| [!UICONTROL CUR] | 提供者費用的貨幣單位 |
| [!UICONTROL FEE %] | 收取費用的交易金額百分比 |
| [!UICONTROL FIXED FEE] | 固定提供者費用金額 |
| [!UICONTROL CHBK FEE] | 與交易<br>相關的借項衝回費用 <br>破折號(-)首碼表示已迴轉借項衝回費用。 |
| [!UICONTROL CUR] | 借項衝回費用的貨幣單位 |
| [!UICONTROL HOLD AMT] | 保留金額或解除保留金額<br> <br>破折號(-)首碼表示正在核發保留資金。 |
| [!UICONTROL CUR] | 保留金額的幣別單位 |
| [!UICONTROL RECOUP AMT] | 從回收帳戶<br>中回收的金額 <br>從回收帳戶移出的基金會顯示破折號(-)首碼。 |
| [!UICONTROL CUR] | 扣除金額的貨幣單位 |

### 交易型別

這些交易型態可能會在支付交易中註明。

| 報告 | 說明 |
| ------------ | -------------------- |
| [!UICONTROL PAYMENT] | 訂單的金額在買方和賣方之間移動 |
| [!UICONTROL AUTH] | 授權和授權作廢交易 |
| [!UICONTROL BONUS] | — |
| [!UICONTROL CHARGEBACK] | 借項衝回費用與借項衝回費用迴轉交易 |
| [!UICONTROL CORRECTION] | — |
| [!UICONTROL CURRENCY_CONVERSION] | — |
| [!UICONTROL DEPOSIT] | — |
| [!UICONTROL DISBURSEMENT] | — |
| [!UICONTROL DISPUTE] | — |
| [!UICONTROL FEES] | 合作夥伴費用、付款費用和費用迴轉交易 |
| [!UICONTROL HOLD] | — |
| [!UICONTROL HOLD_RELEASE] | — |
| [!UICONTROL INCENTIVES] | — |
| [!UICONTROL OTHERS] | — |
| [!UICONTROL RECOUP] | 從銀行或虧損帳戶收回 |
| [!UICONTROL REFUND] | — |
| [!UICONTROL REVERSAL] | — |
| [!UICONTROL WITHDRAWAL] | — |
