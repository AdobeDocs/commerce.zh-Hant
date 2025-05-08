---
title: 顯著的防欺詐功能
description: 啟用 [!DNL Payment Services] 的自動詐騙保護(Signifyd)。
role: Admin, User
level: Intermediate
feature: Payments, Checkout, Configuration, Security, Paas, Saas
exl-id: 440296bb-a6ff-408b-8195-3027916e4f84
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---

# 有效保護詐騙

您可以使用[Signifyd延伸模組](https://commercemarketplace.adobe.com/signifyd-module-connect.html)為[!DNL Payment Services]啟用自動詐騙保護。

Adobe Commerce支援Signifyd 5.4.0和更新版本。 [!DNL Payment Services]支援驗證前和驗證後簽署流程。

Signifyd/[!DNL Payment Services]整合提供信用卡、借記卡、保管卡、透過Admin結帳，以及PayPal和Apple Pay付款方式的涵蓋範圍。 雖然部分交易的細節並未在支付服務和Signifyd之間分享，但Signifyd為所有支付方式提供全面的風險保障，確保最大限度的保護。

請參閱[簽署檔案](https://community.signifyd.com/support/s/article/magento-2-extension-install-guide?language=en_US#downloadandinstallingmagento2extension)，瞭解如何安裝和設定擴充功能。

## 入門

您必須直接與Signifyd通訊，才能將擴充功能上線以與[!DNL Payment Services]搭配使用，不需要設定[!DNL Payment Services]。 安裝後，您就可以在Admin中設定Signifyd擴充功能。 與此擴充功能相關的任何支援將由Signfyd管理。

使用Signid上線時，您必須：

1. 連絡代理人以設定新帳戶。
1. 依預設，Signifyd是[已加入允許清單](https://github.com/signifyd/magento2/blob/main/docs/RESTRICT-PAYMENTS.md)，以確保Signifyd不會觸發其目前不支援的其他付款選項。 若要禁止特定付款方式，您必須進行變更。
1. 向Signifyd確認PayPal不會拒絕可能由Signifyd核准的訂單，方法是透過Paypal中的商家詐騙保護設定。
1. 啟用Signifyd延伸以與[!DNL Payment Services]相容：
   * 在&#x200B;_即時_&#x200B;模式下使用[!DNL Payment Services]時，Signifyd必須處於生產模式。
   * 在&#x200B;_沙箱_&#x200B;模式中使用[!DNL Payment Services]時，Signifyd必須處於測試模式。

## 設定

因為Signifyd會對您的訂單採取某些動作，所以必須設定擴充功能，以根據您為[!DNL Payment Services]設定的付款動作適當地執行動作。

這些設定選項與支付服務和Signifyd整合不相容：

* 當[!DNL Payment Services]設定為`Authorize`付款動作&#x200B;_且_ Signifyd處於`PostAuth`模式，且&#x200B;_[!UICONTROL Decline Guarantees]_選項設定為&#x200B;**建立銷退折讓單**時。

  原因： [!DNL Payment Services]建立授權交易，表示然後嘗試退款。


* [!DNL Payment Services]已使用`Authorize and Capture`付款動作&#x200B;_設定，且_ Signifyd處於`PostAuth`模式，且&#x200B;_[!UICONTROL Decline Guarantees]_選項設定為&#x200B;**取消訂單**。

  原因： [!DNL Payment Services]建立擷取交易，表示之後嘗試作廢。


請參閱Signifyd檔案以取得[設定擴充功能](https://community.signifyd.com/support/s/article/magento-2-extension-install-guide?language=en_US#configuringmagento2extension)的相關資訊。

請參閱[深入瞭解訂單工作流程](https://community.signifyd.com/support/s/article/magento-2-extension-install-guide?language=en_US#howmagento2works)的重要檔案。
