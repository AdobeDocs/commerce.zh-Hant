---
title: 在 [!DNL Payment Services]簽出
description: 自訂 [!DNL Payment Services] 結帳以符合客戶需求。
feature: Payments, Checkout
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---


# 在[!DNL Payment Services]中籤出

您可以設定Adobe Commerce [!DNL Payment Services]的結帳，以最符合購物者的需要。 [訂單自動作廢](#order-auto-voided-if-error)和[信用卡存放](#credit-card-vaulting)等功能，確保您的購物者擁有順暢的使用者體驗。

## 訂單在錯誤時自動失效

如果結帳期間發生錯誤，[!DNL Payment Services]會自動使訂單失效/取消訂單。

購物者的結帳頁面上會顯示錯誤訊息。 訊息可能會有所不同。

![簽出](assets/user-checkout-error.png "時發生錯誤"){width="600" zoomable="yes"}

針對特定[訂單](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/order-management/orders/orders.html?lang=en)，管理員中也會顯示有關已取消訂單的註解。

![已取消訂單的訂單註解](assets/admin-checkout-error.png "已取消訂單的訂單註解"){width="600" zoomable="yes"}

如果購物者取得訂單授權，但並未建立訂單並轉換為`Capture`，該訂單會自動失效。 此程式可確保購物者的信用卡上不會預留任何信用額度，並避免在標準29天期間結束時授權失效時產生的付款提供者費用。

>[!NOTE]
>
>只有當客戶使用設定為`Authorize`模式（而非`Authorize and Capture`模式）的付款方式時，才會發生訂單自動作廢。

## 從產品頁面結帳

當客戶使用PayPal或[!DNL Pay Later]按鈕直接從產品頁面結帳時，只會購買目前產品頁面上呈現的專案。 已位於客戶購物車的專案不會新增至結帳流程，也不會購買。

此功能可讓客戶快速購買目前檢視的專案，同時保留先前新增至購物車的專案。
如果客戶取消訂單，目前產品頁面中的專案會新增到客戶的購物車。

當客戶從產品頁面進入結帳流程時，結帳頁面就會簡化，此檢視畫面只會顯示與訂單相關的資料和選項。

## 信用卡保險存放

購物者可以儲存或「儲存」他們的信用卡資訊，以供日後在網站層級（相同商家帳戶內的任何商店）購買。

如需詳細資訊，請參閱[信用卡存放](vaulting.md)
