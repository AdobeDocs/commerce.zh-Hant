---
title: '[!DNL Payment Services]指南'
description: 這些 [!DNL Payment Services] 的 [!DNL Adobe Commerce] 檔案目標對象。
seo-title: Adobe Commerce Payments Services Audience
seo-description: Describes contents of the [!DNL Payment Services] for Adobe Commerce documentation
exl-id: 30b23f26-9aac-4a24-a607-2431455fc935
feature: Payments, Checkout, Paas, Saas
recommendations: noCatalog
source-git-commit: b75cad4fd71b5ab9c0199ca47800c36cbd1ae76c
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---


# [!DNL Payment Services]指南

Adobe Commerce和Magento Open Source的[!DNL Payment Services]是完全整合的支付解決方案，可讓您從單一位置(您的Commerce儀表板)有效監管所有店面的付款和訂單資料。

透過簡單的部署、自動更新及直覺式介面，管理付款變得前所未有的輕鬆。  此簡化系統不僅降低營運複雜性，更提供快速、可靠且安全的付款選項，提升客戶體驗。 利用[!DNL Payment Services]，商戶可專注於發展業務，同時為客戶提供順暢且值得信賴的結帳體驗。

本指南提供[!DNL Payment Services]功能與優勢的概觀，以及基本入門與實作資訊，包括服務設定與管理的詳細指示。

本指南涵蓋：

![檢查](assets/icon-check.png)目的、優點及主要功能的概述，例如報告功能與安全性法規遵循。

![支票](assets/icon-check.png)相容性和可用的付款體驗選項（由地區決定）以及支援的付款方式。

![檢查](assets/icon-check.png)上線、設定選項、沙箱設定（用於測試）和生產設定（用於處理即時付款）的逐步檔案。

![支票](assets/icon-check.png)管理及監控付款的工具，包括財務報告、退款處理及作廢。

![檢查](assets/icon-check.png)其他資源，例如最佳實務、支援頻道和版本注意事項，以取得持續更新。

## 探索[!DNL Payment Services]檔案

如果您想瞭解[!DNL Payment Services]如何轉換您的商務作業，或需要更多有關Adobe Commerce和Magento Open Source的[!DNL Payment Services]技術指南，本指南已涵蓋您。

如需現成付款解決方案（包括功能和優點）的概觀，請從[主要優點](introduction.md)開始。 如需實作的逐步指示，請跳到[上線](onboard.md)。

<table style="table-layout:fixed">
<tr style="border: 0;">
<td valign="top" style="text-align: center;">
   <div>
      <a href="introduction.md">
      <img alt="付款服務" src="assets/benefits.jpg">
      <strong >主要優點</strong>
      </a>
   </div>
   <p>
      <em>瞭解付款服務如何轉換您的業務。 進一步瞭解主要功能和優點</em>
   </p>
</td>
<td valign="top" style="text-align: center;">
   <div>
      <a href="compatibility.md">
      <img alt="付款服務" src="assets/compatibility.jpg">
      <strong>相容性</strong>
      </a>
   </div>
   <p>
      <em>探索市場可用性、支援的付款方式，以及Adobe的安全性與法規遵循標準</em>
   </p>
</td>
<td valign="top" style="text-align: center;">
   <div>
      <a href="onboard.md">
      <img alt="付款服務" src="assets/onboard.jpg">
      <strong>上線</strong>
      </a>
   </div>
   <p>
      <em>檢視逐步指南和技術檔案，協助您設定和上線</em>
   </p>
</td>
<tr style="border: 0;">
<td valign="top" style="text-align: center;">
   <div>
      <a href="configure-admin.md">
      <img alt="付款服務" src="assets/configuration.jpg">
      <strong>組態</strong>
      </a>
   </div>
   <p>
      <em>自訂設定並測試您的結帳體驗，以開始處理即時付款</em>
   </p>
</td>
<td valign="top" style="text-align: center;">
   <div>
      <a href="reporting.md">
      <img alt="付款服務" src="assets/reporting.jpg">
      <strong>報告</strong>
      </a>
   </div>
   <p>
      <em>存取報告以管理所有訂單與付款方式的作業與追蹤效能</em>
   </p>
</td>
<td valign="top" style="text-align: center;">
   <div>
      <a href="release-notes.md">
      <img alt="付款服務" src="assets/resources.jpg">
      <strong>資源</strong>
      </a>
   </div>
   <p>
      <em>瀏覽如何連絡客戶支援的實用連結、影片教學課程和指示</em>
   </p>
</td>
</table>

>[!MORELIKETHIS]
>
> * [[!DNL Adobe Commerce] 2.4使用手冊](https://experienceleague.adobe.com/docs/commerce-admin/user-guides/home.html?lang=zh-Hant) — 同時針對[!DNL Adobe Commerce]和[!DNL Magento Open Source]以商家為中心的檔案
> * [[!DNL Adobe Commerce] 2.4使用手冊](https://experienceleague.adobe.com/docs/commerce-admin/user-guides/home.html?lang=zh-Hant) — 用來建置和自訂[!DNL Adobe Commerce]或[!DNL Magento Open Source]的開發人員專用檔案
> * [發行說明](release-notes.md) — 進一步瞭解即將發行的版本、產品詳細資料，以及哪些Adobe Commerce版本支援[!DNL Payment Services]擴充功能
> * [說明中心](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/overview.html?lang=zh-Hant) — 在知識庫中搜尋[!DNL Payment Services]相關的疑難排解文章
> * [支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=zh-Hant#submit-ticket)—Commerce客戶可以提交票證，以取得其他協助

## 支援

如果您需要資訊或本指南未涵蓋有關[!DNL Payment Services]的問題，請連絡您的[!DNL Payment Services]銷售代表，或使用[!DNL Payment Services]首頁中的可用資源：

>[!VIDEO](https://video.tv.adobe.com/v/3447836)

檢視[哪個 [!DNL Payment Services] 選項適合您？](compatibility.md#which-payment-services-option-is-right-for-you)要檢查哪個選項最適合您的[!DNL Payment Services]主題。
