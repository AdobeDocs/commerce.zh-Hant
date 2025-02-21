---
title: 安全性與合規性
description: 檢閱您網站的安全與法規遵循需求。
feature: Payments, Checkout, Compliance
redirect_from: https://experienceleague.adobe.com/docs/commerce/payment-services/security.html
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 0%

---

# 安全性與合規性

安全性是[!DNL Payment Services]中最重要的考量，您的[!DNL Payment Services]沒有傳遞任何私人或支付卡產業(PCI)規範資訊。

## Commerce安全性

[!DNL Adobe Commerce]和[!DNL Magento Open Source]包含對數個安全性功能的支援。

請參閱核心使用手冊中的[安全性](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/security){target="_blank"}，以檢閱安全性最佳實務，並瞭解如何管理管理員工作階段和認證、實作驗證碼以及管理網站限制。

## PCI法規遵循

支付卡產業(PCI)針對接受透過網際網路以信用卡付款的企業建立了一套要求。 除了維護安全的環境之外，處理客戶信用卡資訊的商戶也應負責符合某些標準准則。

如需詳細資訊，請參閱[PCI法規遵循准則](https://experienceleague.adobe.com/en/docs/commerce-admin/start/compliance/payments/compliance-pci){target="_blank"}。

商戶可以完成[自我評估問卷(SAQ)](https://www.pcisecuritystandards.org/pci_security/completing_self_assessment){target="_blank"}，這是評估持卡人資料安全性的自我驗證工具。

### 信用卡欄位

若使用信用卡欄位，您的服務不會傳遞PCI管制的資料。 您不必儲存或維護這些資料，這大大降低了PCI法規遵循問題。

### 3DS

PCI 3-D Secure (3DS)可讓購買者線上上購買信用卡時，與其信用卡發行者進行驗證。 此額外的安全性層級有助於防止線上詐騙，是歐盟(EU)法規的必要專案。

[!UICONTROL Payment Services]提供3DS功能，讓商戶遵守歐盟法規，並保護客戶和商戶在他們的商店中免受欺詐活動。

如果您是歐盟或英國境內需要3DS法規遵循的商家，您必須在[設定](settings.md#credit-card-fields)中手動開啟3DS （預設為`Off`）。

>[!IMPORTANT]
>
>3DS規定適用於企業和持卡人的銀行位於[歐洲經濟區](https://www.efta.int/eea) (EEA)和英國的交易中。 美國商家不需要3DS，但可視需要為其交易啟用。

商家/店舖人員為買家下單的訂單未設定3DS合規性措施。

>[!MORELIKETHIS]
>
> * 如需詳細資訊，請參閱設定](settings.md#3ds)中的[3DS。
> * 請參閱PayPal開發人員檔案中的[測試卡](https://developer.paypal.com/docs/checkout/advanced/customize/3d-secure/test/)，以取得有關3DS測試之特定信用卡的詳細資訊。

### 卡片存放

當購物者[儲存（或「儲存」）其信用卡資訊](vaulting.md)以便日後在您的商店購買時，與購物者共用最小的信用卡資訊（最後四位數、卡片到期日及卡片品牌）。 信用卡資訊會與付款提供者一併儲存。 當卡片過期或不再需要儲存資訊時，可以刪除該Token，讓付款提供者不再儲存資訊。

如需詳細資訊，請參閱[信用卡存放](vaulting.md)。

### PayPal付款按鈕

使用PayPal付款按鈕，您的服務不會傳遞PCI管制的資料。 您不必儲存或維護這些資料，這大大降低了PCI法規遵循問題。

基於安全考量，PayPal在結帳時不會傳送帳單地址 — 國家/地區、電子郵件和名稱是唯一使用的帳單資訊。 您可以選擇啟用網站的PayPal結帳，連絡PayPal並完成審查程式，以傳回完整的帳單地址。

PayPal也整合了防欺詐功能，使用機器學習協助您對抗欺詐行為。 如需詳細資訊，請參閱PayPal的[賣家保護檔案](https://www.paypal.com/us/webapps/mpp/security/seller-protection)。

## 欺詐保護

您可以使用[Signifyd延伸模組](https://commercemarketplace.adobe.com/signifyd-module-connect.html)為付款服務啟用自動詐騙保護。 如需詳細資訊，請參閱[表示詐騙保護](fraud-protection.md)。

PayPal在其開發人員檔案中提供[詐騙保護](https://www.paypal.com/us/cshelp/article/what-is-fraud-protection-help1014){target=_blank}的其他選項：

* 如需詳細資訊，請參閱[進階詐騙保護](https://www.paypal.com/us/enterprise/fraud-protection-advanced#fraud-protection-advanced){target=_blank}。
* 如需詳細資訊，請參閱[借項衝回保護](https://www.paypal.com/us/cshelp/article/what-is-chargeback-protection-help608){target=_blank}。
