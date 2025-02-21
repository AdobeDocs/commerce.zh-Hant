---
title: '[!DNL Store Fulfillment by Walmart Commerce Technologies]發行說明'
description: 檢閱發行說明，瞭解所有 [!DNL Store Fulfillment by Walmart Commerce Technologies] 發行版本的相關資訊。
role: Admin, User, Leader
feature: Shipping/Delivery, Release Notes
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---

# 發行說明

這些版本說明說明[!DNL Store Fulfillment Services by Walmart Commerce Technologies]的初始版本，包括：

![新](../assets/new.svg)新功能
![已修正問題](../assets/fix.svg)修正和改良
![已知問題](../assets/bug.svg)已知問題

請參閱[即將發行的版本](https://experienceleague.adobe.com/docs/commerce-operations/release/planning/schedule.html)，瞭解發行排程和支援。

請參閱[產品可用性](https://experienceleague.adobe.com/docs/commerce-operations/release/product-availability.html)，瞭解哪些Adobe Commerce版本支援此擴充功能。

## v1.5.0

*2023年8月3日*

[!BADGE 支援]{type=Informative tooltip="支援"}[Adobe Commerce 2.4.4至2.4.6](https://experienceleague.adobe.com/docs/commerce-operations/release/product-availability.html)，包括2.4.6-p1、2.4.5-p3和2.4.4-p4安全性修補程式版本

此版本包含下列更新：

![新](../assets/fix.svg)更新擴充功能以支援[Adobe Commerce安全性修補程式發行版本](https://experienceleague.adobe.com/docs/commerce-operations/release/notes/security-patches/overview.html) 2.4.6-p1、2.4.5-p3和2.4.4-p4。

![新](../assets/new.svg)<!-- WMTP-918 -->已新增對銷售電子郵件的[非同步傳送](sales-emails.md)組態選項的支援。 升級至1.5.0版的商家可選擇立即傳送電子郵件（預設）或以非同步方式傳送。

![新](../assets/new.svg)<!-- WMTP-916-->已更新[來源組態](merchant-store-configuration.md)以支援國際電話號碼格式。

![新](../assets/new.svg)新增邏輯，以防止退款金額超過剩餘金額或開立商業發票的金額。

![新](../assets/new.svg)<!-- WMTP-882 -->已將`google.map.LatLng`物件取代為JSON常值，以支援與舊版[!DNL Google Maps]的相容性。

![已修正問題](../assets/fix.svg)<!-- WMTP- -->已更新建立`[!DNL Available for Store Pickup]`和`[!DNL Available for Home Delivery]`產品屬性的指令碼，以防止屬性類別衝突。

![已修正問題](../assets/fix.svg)<!-- WMTP-915 -->修正載入及儲存某些實體時，造成無限回圈的相容性問題。

![已修正問題](../assets/fix.svg)<!-- WMTP-921 -->修正當專案從產品詳細資料頁面(PDP)新增到購物車時，無法觸發[!DNL Ship to Store]報價驗證的問題。

![已修正問題](../assets/fix.svg)<!-- WMTP- 932 -->已修正允許客戶為不符合首頁傳送條件的專案選取首頁傳送方式的結帳問題。

![已修正問題](../assets/fix.svg)安裝更新：

- <!-- WMTP-880--> 修正安裝[!DNL Store Fulfillment]擴充功能時，傳回錯誤網站程式碼的問題。

- <!-- WMTP-878--> 修正SKU整數在安裝期間必須轉型為字串型別的問題。

![已修正問題](../assets/fix.svg)<!-- WMTP-915-->已修正遺失「簽入」錯誤碼所造成的失敗。

![已修正問題](../assets/fix.svg)<!-- WMTP-932 -->已修正分配作業期間與部分拒絕相關的錯誤。

![New](../assets/new.svg)<!-- WMTP-953 -->已更新Cancel API端點，將status引數作為選用物件使用。

![新](../assets/new.svg)<!-- WMTP-960 -->已改善Dispense API端點的記錄詳細資料。

## v1.4.0

*2023年4月13日*

[!BADGE 支援]{type=Informative tooltip="支援"}

![新](../assets/fix.svg) [!DNL Store Fulfillment]現在[與 [!DNL Adobe Commerce] 2.4.4至2.4.6](https://experienceleague.adobe.com/docs/commerce-operations/release/product-availability.html)相容。


## v1.3.0

*2023年2月27日*

[!BADGE 支援]{type=Informative tooltip="支援"}

此版本包含下列更新：

![新](../assets/fix.svg)<!-- WMTP-795 -->已新增功能，可將「系統組態」設定的預設範圍從網站變更為全域，以停用特定網站的「商店履行」解決方案。

## v1.2.0

*2022年9月27日*

[!BADGE 支援]{type=Informative tooltip="支援"}

此版本包含下列更新：

![新](../assets/fix.svg) [!DNL Store Fulfillment]現在[與 [!DNL Adobe Commerce] 2.4.4至2.4.5](https://experienceleague.adobe.com/docs/commerce-operations/release/product-availability.html)相容。


## v1.1.0

*2022年7月15日*

[!BADGE 支援]{type=Informative tooltip="支援"}

穩定性：一般可用性

![新增](../assets/fix.svg)<!-- WMTP-731 -->透過新增預設汽車造型和模型選擇，簡化Store Assist應用程式的[簽到體驗設定](check-in-experience-setup.md)。 在舊版中，商家必須手動設定汽車廠牌和模型選項。

## v1.0.0

*2022年3月4日*

[!BADGE 支援]{type=Informative tooltip="支援"}

穩定性：一般可用性

## 商店協助應用程式

如需Store Assist應用程式新發行版本的相關資訊，請參閱[Apple App Store](https://apps.apple.com/us/app/store-assist-by-walmart/id1609281539){target="_blank"}或[Google Play市集](https://play.google.com/store/apps/details?id=com.walmart.faas.storeassist){target="_blank"}中的應用程式資訊。
