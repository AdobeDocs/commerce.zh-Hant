---
title: 首頁
description: 使用管理員中的 [!DNL Payment Services] 首頁來上線（包括ACCS）、開啟交易報告、管理PaaS上的訂單和付款進入點，以及存取「學習」、「說明」和「設定」。
role: Admin, User
level: Intermediate
exl-id: d7a4c87f-33cb-446a-b442-3cdf05b518a2
feature: Payments, Checkout, Paas, Saas
source-git-commit: 14c4178338859d55a7391139033d51d1aa6f7678
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 1%

---

# [!DNL Payment Services]首頁

適用於Adobe Commerce和Magento Open Source的[!DNL Payment Services]提供您設定和使用擴充功能所需資訊的「首頁」檢視。 首頁頂端的選項取決於您的部署：雲端或內部部署(PaaS)上的Adobe Commerce，或[!DNL Adobe Commerce as a Cloud Service]或[!DNL Adobe Commerce Optimizer] (SaaS)。

在&#x200B;_管理員_&#x200B;側邊欄上，移至&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]**：

>[!BEGINTABS]

>[!TAB 雲端和內部部署上的 Adobe Commerce]

![首頁檢視](assets/home-view.png){width="700" zoomable="yes"}

>[!TAB Adobe Commerce as a Cloud Service和Commerce Optimizer]

在您完成上線之前，**[!UICONTROL Home]**&#x200B;將顯示&#x200B;**[!UICONTROL ACCS Onboarding Required]**。 通知連結至[設定沙箱服務](sandbox.md#sandbox-onboarding) （使用測試PayPal處理帳戶），或連結至[啟用即時付款](production.md#enable-live-payments) （如果您已在其他環境中測試）：

![支付服務首頁需要ACCS上線](assets/payment-services-home-accs-onboarding.png){width="700" zoomable="yes"}

上線完成後（或在已設定的執行個體上），**[!UICONTROL Home]**&#x200B;在表格式報告中顯示&#x200B;**[!UICONTROL Transactions]**&#x200B;和&#x200B;**[!UICONTROL View Report]**，以及&#x200B;**[!UICONTROL Learn]**&#x200B;和&#x200B;**[!UICONTROL Help]**&#x200B;區域：

![SaaS上的付款服務首頁](assets/payment-services-home-saas.png){width="700" zoomable="yes"}

>[!ENDTABS]

在此首頁檢視中，您可以存取&#x200B;_首頁_、_瞭解_&#x200B;關於[!DNL Payment Services]、設定擴充功能&#x200B;_設定_，或取得&#x200B;_說明_。 使用&#x200B;**[!UICONTROL View Report]** (SaaS)或&#x200B;**[!UICONTROL Orders]**&#x200B;和&#x200B;**[!UICONTROL Payouts]**&#x200B;進入點（雲端和內部部署上的Adobe Commerce）來開啟報告；請參閱[報告](reporting.md)。

## 首頁

僅[!BADGE 個PaaS]{type=Informative url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案（Adobe管理的PaaS基礎結構）和內部部署專案的Adobe Commerce 。"}

| 欄位 | 說明 |
|---|---|
| [!UICONTROL Orders] | 這些報表可讓您快速檢視訂單的付款狀態，並識別任何潛在問題。 |
| [!UICONTROL Payouts] | 「付款」報表會顯示完整的付款資訊，讓您對付款金額、已處理數量及財務調節之交易層次的詳細報表具有完全的透明度。 |

僅[!BADGE SaaS]{type=Positive url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案（Adobe管理的SaaS基礎結構）。"}

| 欄位 | 說明 |
|---|---|
| [!UICONTROL Transactions] | 彙總「交易」報表，協助您瞭解特定交易的結果。 按一下&#x200B;**[!UICONTROL View Report]**&#x200B;以開啟交易的網格（例如，訂單與PayPal交易ID、付款方式、結果和回應代碼）。 請參閱[交易報告檢視](reporting.md#transactions-report-view)。 |

## 瞭解

| 欄位 | 說明 |
|---|---|
| [!UICONTROL Read documentation] | 檢視[!DNL Payment Services]的最新使用者和開發人員檔案。 |
| [!UICONTROL How to onboard] | 尋找設定所需的一切，並開始使用[!DNL Payment Services]功能。 |
| [!UICONTROL Understand financial reports] | 在[!DNL Payment Services]中現金流量管理報告的深入說明。 |

## 說明

| 欄位 | 說明 |
|---|---|
| [!UICONTROL Visit help center] | [!DNL Adobe Commerce]說明中心有關於[!DNL Payment Services]的知識庫文章。 |
| [!UICONTROL Get support] | 請造訪[!DNL Adobe Commerce]支援入口網站以取得[!DNL Payment Services]的協助。 |

## 設定

在[首頁]檢視中，按一下&#x200B;**[!UICONTROL Settings]**。 如需詳細資訊，請參閱[[!DNL Payment Services] 組態](configure-admin.md)。

例如，當您收集支援的詳細資訊時，「付款服務」區域的頁尾將會顯示&#x200B;**付款服務**&#x200B;和&#x200B;**付款服務儀表板**&#x200B;版本標籤。
