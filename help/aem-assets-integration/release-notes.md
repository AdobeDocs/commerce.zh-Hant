---
title: AEM Assets整合發行說明
description: 如需所有AEM Assets整合發行版本的相關資訊，請參閱發行說明。
feature: CMS, Media, Release Notes
exl-id: 0d639565-812f-481a-afd6-6e6fa54ed70e
source-git-commit: 655d33ea7c4b75f81770490b2e229b1bec281fe1
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# AEM Assets整合發行說明

以下版本說明說明AEM Assets整合的初始版本，包括：

![新](../assets/new.svg)新功能
![已修正問題](../assets/fix.svg)修正和改良
![已知問題](../assets/bug.svg)已知問題

如需在功能發行版本之外發行的功能變更和修正，請檢閱&#x200B;_託管服務更新_&#x200B;區段。

深入瞭解即將發行的版本、產品支援，以及哪些Adobe Commerce版本支援AEM Assets整合擴充功能，請參閱Adobe Commerce [發行排程](https://experienceleague.adobe.com/zh-hant/docs/commerce-operations/release/planning/schedule)和[產品可用性](https://experienceleague.adobe.com/zh-hant/docs/commerce-operations/release/product-availability)主題。

## 託管服務更新

這些發行說明說明說明所發生的功能變更和修正，這些變更和修正是在託管服務的定期功能發行之外發行的。

+++託管服務更新

_2025年9月11日_

![新問題](../assets/new.svg)已更新具有新[屬性的](https://experienceleague.adobe.com/zh-hant/docs/commerce/aem-assets-integration/synchronize/custom-match){target=_blank}自訂自動比對`asset_matches`端點。

_2025年2月11日_

![新問題](../assets/new.svg)現在，商家可以同步產品與類別的影像。

+++

## v1.2.5

_2025年10月22日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.5版和更新版本。

![已修正問題](../assets/fix.svg)<!-- Issue ACAP-1161 -->已修正Adobe Commerce管理員中更新現有影像對應位置會導致PHP型別錯誤的問題。

## v1.2.4

_2025年10月17日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.5版和更新版本。

![已修正問題](../assets/fix.svg)<!-- Issue ACAP-1155 -->已改善自訂屬性的整體穩定性。 使用非同步API時，自訂屬性現在可以正確更新。

![已修正問題](../assets/fix.svg)<!-- Issue ACAP-1074 -->現在，定義基底連結URL時，[product-asset同步化](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/stores-sales/site-store/store-urls#configure-the-base-url){target=_blank}不會失敗。

## v1.2.3

_2025年10月2日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.5版和更新版本。

![已修正問題](../assets/fix.svg)<!-- Issue ACAP-1135 -->已修正更新產品屬性的問題。 產品屬性現在會依預期更新，且會在更新失敗時傳回適當的錯誤，而非200回應。

## v1.2.2

_2025年9月18日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.5版和更新版本。

![已修正問題](../assets/fix.svg)<!-- Issue ACAP-1110 -->改善迷你購物車、購物車和結帳頁面上的整體影像穩定性。 這些頁面上的影像現在已正確載入。

## v1.2.0

_2025年8月7日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.5版和更新版本。

![新問題](../assets/new.svg)<!-- Issue ACAP-1018 -->現在，商家可以在從管理員設定Assets整合時，選取[視覺效果擁有者](https://experienceleague.adobe.com/zh-hant/docs/commerce/aem-assets-integration/get-started/setup-synchronization){target=_blank}來選擇影像和媒體資產的來源。

![新問題](../assets/new.svg)<!-- Issue ACAP-1078 -->已更新具有新[屬性的](https://experienceleague.adobe.com/zh-hant/docs/commerce/aem-assets-integration/synchronize/custom-match){target=_blank}自訂自動比對`asset_matches`端點。 此變更可讓您實作自己的比對邏輯，以傳回與特定`productSku`相關聯的所有資產。

## v1.1.2

_2025年6月11日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.5版和更新版本。

![新問題](../assets/new.svg)<!-- Issue ACAP-1041 -->已新增Adobe Commerce 2.4.8和PHP 8.4的支援。

## v1.1.0

_2025年4月23日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.5版和更新版本。

![新問題](../assets/new.svg)<!-- Issue ACAP-955 -->現在，可以使用[自訂網域URL](https://experienceleague.adobe.com/zh-hant/docs/commerce/aem-assets-integration/get-started/setup-synchronization#optional-configure-the-custom-domain-url)，而不是AEM傳遞URL。 如果商家在其AEM儀表板中設定&#x200B;**自訂網域名稱**，則需要在Commerce中新增此&#x200B;**自訂網域URL**。

![已修正問題](../assets/fix.svg)<!-- Issue ACAP-987 -->已改善AEM Assets同步程式的整體記錄。

## v1.0.22

_2025年3月12日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.5版和更新版本。

![新問題](../assets/new.svg)<!-- Issue ACAP-xx -->現在，Assets選擇器需要[Assets選擇器IMS使用者端ID](https://experienceleague.adobe.com/zh-hant/docs/commerce/aem-assets-integration/get-started/setup-synchronization)，才能將AEM Assets影像與產品類別和頁面產生器產生的內容對應。

## v1.0.20

_2025年2月11日_

[!BADGE 支援]{type=Informative tooltip="支援"} Adobe Commerce 2.4.5版和更新版本。

![新](../assets/new.svg)<!-- Issue ACAP-xx -->一般可用性版本。
