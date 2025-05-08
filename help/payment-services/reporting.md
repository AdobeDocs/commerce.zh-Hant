---
title: 報告
description: 使用「交易」報表來瞭解交易授權率及交易趨勢。
role: User
level: Intermediate
exl-id: dd1d80f9-5983-4181-91aa-971522eb56fa
source-git-commit: 4482c1f93a424c73497b88c707d0ab93a694c957
workflow-type: tm+mt
source-wordcount: '1270'
ht-degree: 0%

---

# 報告

[!DNL Adobe Commerce]和[!DNL Magento Open Source]的[!DNL Payment Services]為您提供完整的報告，以便您清楚瞭解商店的交易、訂單和付款。

![交易報告](assets/transactions-report.png){width="700" zoomable="yes"}

「交易」報表可顯示交易授權率及負面的交易趨勢，因此您可以有效監控商店的健康狀況，並預先識別及解決任何交易問題。

檢視店面訂單的個別交易及其付款方式、結果、付款回應代碼等。

「交易」報表中提供的資訊僅供商家使用。 請勿與客戶或其他潛在的詐騙者共用此資訊。 交易資訊可用於略過安全性檢查或下單導致借項衝回。

您可以下載.csv檔案格式的「交易」報表，以於現有的會計或訂單管理軟體中使用。

>[!NOTE]
>
>如果您尚未為[!DNL Payment Services]上線並啟動即時模式[&#128279;](production.md#enable-live-payments)，則無法檢視財務報表。

## 交易報表檢視

「交易」報表檢視可在「付款服務」的「交易」檢視中使用。 其中包含您商店中所有可用的交易資訊。

在&#x200B;_Admin_&#x200B;側邊欄上，前往&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** > _[!UICONTROL Transactions]_>**[!UICONTROL View Report]**&#x200B;檢視詳細的表格式交易報告檢視。

![交易報告檢視](assets/transactions-report-view.png){width="800" zoomable="yes"}

您可以根據本主題中的章節設定此檢視，以最理想的方式呈現您想要檢視的資料。

請參閱此報表中的連結Commerce訂單與PayPal交易ID、交易金額、每筆交易的付款方式等。

並非所有支付方法都提供相同的資訊粒度。 例如，信用卡交易會提供回應、AVS和CCV代碼，以及「交易」報表中卡片的最後四位數；PayPal付款按鈕則否。

您可以[以.csv檔案格式](#download-transactions)下載交易，以用於現有的會計或訂單管理軟體。

>[!WARNING]
>
> 交易報告不會包含任何在[!DNL Payment Services]以外進行的擷取。

### 選取資料來源

在「交易」報表檢視中，您可以選取您要檢視其報表結果的資料來源 — **[!UICONTROL Live]**&#x200B;或&#x200B;**[!UICONTROL Sandbox]**。

![資料來源選擇](assets/datasource.png){width="300" zoomable="yes"}

如果&#x200B;_[!UICONTROL Live]_&#x200B;是選取的資料來源，您可以看到在生產模式中使用[!DNL Payment Services]之存放區的報表資訊。 如果&#x200B;_[!UICONTROL Sandbox]_&#x200B;是選取的資料來源，您可以看到沙箱模式的報告資訊。

資料來源選取專案的工作方式如下：

* 如果您沒有任何以生產模式使用[!DNL Payment Services]的存放區，資料來源選項會預設為&#x200B;_[!UICONTROL Sandbox]_。
* 如果您有任何儲存（一或多個）在生產模式中使用[!DNL Payment Services]，資料來源選項會預設為&#x200B;_[!UICONTROL Live]_。
* 報表匯出一律遵循資料來源選擇。

若要選取[!UICONTROL Transactions]報表的資料來源：

1. 在&#x200B;_管理員_&#x200B;側邊欄上，前往&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Transactions]_>**[!UICONTROL View Report]**。
1. 按一下&#x200B;**[!UICONTROL Data source]**&#x200B;並選取&#x200B;**[!UICONTROL Live]**&#x200B;或&#x200B;**[!UICONTROL Sandbox]**。

   報表結果會根據選取的資料來源重新產生。

### 自訂日期時間範圍

從「交易」報表檢視中，您可以選取特定日期，以自訂您要檢視的交易的時間範圍。 依預設，網格中會顯示30天的交易。

1. 在&#x200B;_管理員_&#x200B;側邊欄上，前往&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Transactions]_>**[!UICONTROL View Report]**。
1. 按一下&#x200B;**[!UICONTROL Transaction dates]**&#x200B;行事曆選擇器篩選器。
1. 選擇適用的日期範圍。
1. 在網格中檢視指定日期的交易。

### 篩選報表資訊

從「交易」報表檢視中，您可以選取篩選條件，以篩選您要檢視的狀態結果。

1. 在&#x200B;_管理員_&#x200B;側邊欄上，前往&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Transactions]_>**[!UICONTROL View Report]**。
1. 按一下&#x200B;**[!UICONTROL Filter]**&#x200B;選取器。
1. 切換&#x200B;_[!UICONTROL Transaction Result]_&#x200B;選項，只檢視所選訂單交易的報表結果。
1. 切換&#x200B;_[!UICONTROL Payment Method]_&#x200B;選項以檢視用於交易的付款型別的報告結果。
1. 切換&#x200B;_[!UICONTROL Payment Detail]_&#x200B;選項，檢視使用的付款型別的其他資訊（可用時）。
1. 輸入&#x200B;_最小訂單金額_&#x200B;或&#x200B;_最大訂單金額_&#x200B;以檢視該訂單金額範圍內的報表結果。
1. 輸入&#x200B;_[!UICONTROL Order ID]_&#x200B;以搜尋特定交易。
1. 介紹&#x200B;_[!UICONTROL Card Last Four]_&#x200B;以搜尋特定的信用卡或扣帳卡。
1. 輸入&#x200B;_[!UICONTROL Customer ID]_&#x200B;以顯示特定客戶的所有交易。
1. 輸入&#x200B;_[!UICONTROL Customer Email]_&#x200B;以篩選該電子郵件的交易。
1. 按一下&#x200B;**[!UICONTROL Hide filters]**&#x200B;以隱藏篩選器。

### 顯示和隱藏欄

依預設，「交易」報表會顯示所有可用的資訊欄。 不過，您可以自訂您在報表中看到的欄。

1. 在&#x200B;_管理員_&#x200B;側邊欄上，前往&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Transactions]_>**[!UICONTROL View Report]**。
1. 按一下&#x200B;**[!UICONTROL Column settings]**&#x200B;圖示![欄設定圖示](assets/column-settings.png){width="20" zoomable="yes"}。
1. 若要自訂您在報表中看到的欄，請核取或取消核取清單中的欄。

   「交易」報表會立即顯示您在「欄設定」功能表中所做的任何變更。 欄偏好設定會儲存，如果您離開報表檢視，偏好設定仍會維持有效。

### 更新報表資料

交易報告檢視會顯示&#x200B;_[!UICONTROL Last updated]_&#x200B;時間戳記，顯示上次更新報告資訊的時間。 依預設，交易報告資料每三小時自動重新整理一次。

您也可以手動強制重新整理報表資料，以檢視最新的報表資訊。

1. 在&#x200B;_管理員_&#x200B;側邊欄上，前往&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Transactions]_>**[!UICONTROL View Report]**。
1. 按一下&#x200B;_重新整理_&#x200B;圖示（![重新整理圖示](assets/refresh-button-med.png){width="20" zoomable="yes"}）。

   已重新整理交易報表資料，並顯示&#x200B;*[!UICONTROL Update complete]*&#x200B;確認訊息，而且格線中顯示最新資訊。

### 下載交易

您可以下載.csv檔案，其中包含交易檢視格線中顯示的所有交易，無論您是檢視預設的30天交易還是自訂的時間範圍。

1. 在&#x200B;_管理員_&#x200B;側邊欄上，移至&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > **[!UICONTROL Transactions]**。
1. 如果您想要檢視過去30天以外時間範圍的交易，請[自訂您狀態的日期範圍時間範圍](#customize-dates-timeframe)。
1. 按一下&#x200B;_下載_ ![下載圖示](assets/icon-download.png){width="20" zoomable="yes"}圖示。

您的交易會以.csv格式下載。

### 欄說明

「交易」報表包含下列資訊。

| 欄 | 說明 |
| ------------ | -------------------- |
| [!UICONTROL Order ID] | Commerce訂單ID （僅包含成功交易的值，且被拒絕的交易為空白）<br> <br>若要檢視相關的[訂單資訊](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/stores-sales/order-management/orders/orders){target="_blank"}，請按一下ID。 |
| [!UICONTROL PayPal Transaction ID] | 付款提供者提供的交易ID；僅包含成功交易的值，並包含拒絕交易的破折號。 您可以按一下此ID以存取PayPal交易詳細資訊頁面。 |
| [!UICONTROL Customer ID] | 訂單的Commerce客戶ID<br> <br>如需詳細資訊，請參閱[客戶資訊](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/customers/customer-accounts/account-create){target="_blank"}主題。 |
| [!UICONTROL Transaction Date] | 交易日期時間戳記 |
| [!UICONTROL Payment Method] | 用於交易的付款型別，包含有關品牌和卡片型別的資訊。 如需詳細資訊，請參閱[卡片型別](https://developer.paypal.com/docs/api/orders/v2/#definition-card_type)；適用於Payment Services 1.6.0或更新版本 |
| [!UICONTROL Payment Detail] | 提供交易所用付款型別的額外資訊（可用時）。 |
| [!UICONTROL Card Last Four] | 用於交易的信用卡或借記卡的最後4位數 |
| [!UICONTROL Result] | 交易的結果 — *[!UICONTROL OK]* （成功交易）、*[!UICONTROL Rejected by Payment Provider]* （由PayPal拒絕）、*[!UICONTROL Rejected by Bank]* （由發行卡的銀行拒絕） |
| [!UICONTROL Response Code] | 提供付款提供者或銀行拒絕原因的錯誤碼；請參閱[`Rejected by Bank`狀態](https://developer.paypal.com/docs/api/orders/v2/#definition-processor_response)和[`Rejected by Payment Provider`狀態](https://developer.paypal.com/api/rest/reference/orders/v2/errors/)的可能回應代碼清單和說明。 |
| [!UICONTROL AVS Code] | 地址驗證服務代碼；付款請求的處理器回應資訊。 如需詳細資訊，請參閱[可能的程式碼和說明清單](https://developer.paypal.com/docs/api/orders/v2/#definition-processor_response)。 |
| [!UICONTROL CVV Code] | 信用卡與借記卡的卡片驗證值代碼；如需詳細資訊，請參閱[可能的代碼清單與說明](https://developer.paypal.com/docs/api/orders/v2/#definition-processor_response)。 |
| [!UICONTROL Amount] | 交易的訂單金額 |
| [!UICONTROL Currency] | 用於交易訂單的貨幣 |
| [!UICONTROL Type] | [交易 — `Authorize`或`Authorize and Capture`的付款動作](../payment-services/production.md#set-payment-services-as-payment-method) |

### 錯誤回應代碼

_回應代碼_&#x200B;欄顯示與交易相關的特定錯誤或成功代碼。 您可能會看到的一些常見錯誤代碼包括：

* `PAYMENT_DENIED`—PayPal已拒絕交易，因為它懷疑是詐騙。
* `INTERNAL_SERVER_ERROR` — 交易被PayPal拒絕，並發生PayPal伺服器錯誤。 可以重試交易。
* `INSTRUMENT_DECLINED`—PayPal已根據選取的付款方式拒絕客戶。 可以使用不同的付款方式重試交易。
* `9500` — 關聯銀行拒絕交易，因為它懷疑是詐騙。
* `5120` — 關聯銀行拒絕交易，因為客戶沒有足夠的資金進行付款。
* `5650` — 關聯銀行拒絕交易，因為銀行需要強大的客戶驗證([3DS](security.md#3ds))。

2023年6月1日以後交易的失敗交易有詳細的錯誤回應代碼。 2023年6月1日之前發生的交易會顯示部分報表資料。
