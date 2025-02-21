---
title: 第2級和第3級處理
description: ' [!DNL Payment Services] 筆交易中的卡片付款處理層級。'
role: Admin
feature: Payments
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---

# 第2級和第3級處理

透過[!DNL Payment Services]有三個可用的卡片處理層級：

* 層級1是最常見的，需要較少的資訊，因此通常比使用層級2或層級3資料處理的交易產生較高的交換費用，這些資料通常與公司和購買信用卡有關。

* 使用層級2和層級3，接受大量購買卡或公司卡交易的[!DNL Payment Services]客戶在交換加上(IC++)定價時，可能會因為允許[!DNL Payment Services]傳送更多交易相關資訊而收到較低的處理率。 如果交易符合資格，則根據卡片網路需求，商家可能會收到特定交易的較低處理率。

>[!NOTE]
>
>層級2與層級3訂價僅適用於Visa與MasterCard交易。 American Express只提供第2層定價。 Discover不提供第2級或第3級定價。 如需詳細資訊，請參閱PayPal開發人員檔案中的[付款處理](https://developer.paypal.com/docs/checkout/advanced/processing/){target=_blank}。

檢視[什麼是IC++?PayPal開發人員檔案中的](https://www.paypal.com/us/brc/article/what-is-interchange-plus-plus){target=_blank}以取得詳細資訊。

第2級與第3級處理資料可讓商家降低其IC++定價，前提是他們提供購買的其他細節，以降低處理器風險，並提供有利的方面：

* 提供這項處理資料，大型客戶的費用將會降低。

* 客戶不太可能遇到詐騙情況，因為訂單具有更多資訊。

不過，卡片網路（如Visa和Mastercard）最終會決定交易是否符合第2級或第3級處理的資格：

* 第2層資料包含其他資訊，例如訂單的稅捐金額、客戶代碼或採購單編號。

* 第3層資料更瞭解有關銷售的詳細資訊，這有助於取得相較於第2層更低的交換率。 第3層資料包含採購料號摘要、採購單位數量、訂購料號的單位及其他特定明細等資訊。

[!DNL Payment Services]會收集這項資料，並提供付款交易的詳細報表。

## [!DNL Payment Services]中的第2級與第3級卡片付款交易

要符合第2級或第3級處理的資格，商家必須傳送先前的資訊，不過最終決定交易在處理時符合哪個層級的資訊是卡片網路。

如需詳細資訊，請參閱PayPal開發人員檔案中的[付款處理常見問題集](https://www.paypal.com/us/cshelp/article/ts2278?_ga=1.131773126.875104296.1712843492){target=_blank}。

[!DNL Payment Services]個商店層級的商家預設停用層級2與層級3處理。

如果您已使用IC++訂價，便可使用第2級與第3級處理。 若要啟用此功能，您可以透過[命令列介面(CLI](configure-cli.md))執行此操作。

>[!IMPORTANT]
>
>如有任何問題，請洽詢您的[!DNL Payment Services]帳戶管理員。
