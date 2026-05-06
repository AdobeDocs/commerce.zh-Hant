---
title: 整合限制和邊界
description: 瞭解使用Commerce的協力廠商目錄、自動修正涵蓋範圍、抓取必要條件、企業規模考量事項以及LLM Optimizer的受限制測試版存取限制等範圍限制。
role: Admin, User, Leader
recommendations: noCatalog
badgePaas: label="僅限PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案（Adobe管理的PaaS基礎結構）和內部部署專案的Adobe Commerce 。"
source-git-commit: 47348a44ff7c5f890c10594f44cae6e771be046f
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# 整合限制和邊界

>[!IMPORTANT]
>
>存取此整合受到限制。 如需詳細資訊，請聯絡您的技術客戶經理。

使用此主題來設定[!DNL Adobe Commerce]和[!DNL Adobe LLM Optimizer]整合可以自動化的期望、您仍然負責的位置以及仍在發展的限制。

## 協力廠商目錄限制 {#third-party-catalog}

當目錄&#x200B;**不在[!DNL Adobe Commerce]中上線時：**

- 根據您的設定，LLM Optimizer仍可使用映象或匯入的目錄資料來識別問題並提出改善建議。
- **直接將自動修正**&#x200B;寫入商戶的商務平台與寫入商戶的來源目錄不同。 您可能需要映象目錄、匯出/匯入或合作夥伴自動化才能套用變更。

若為Commerce託管的目錄，核准的名稱和說明更新會移至Commerce記錄系統。 請參閱[搭配Adobe Commerce使用LLM Optimizer](get-started/use-llmo-with-commerce.md)。

## 規模和技術限制 {#scale-limits}

大型目錄和高URL數可能會使抓取、分析和邊緣部署模式變得緊張。

## 抓取和機器人可讀性 {#crawling}

有意義的目錄和PDP深入分析假設與LLM相關的&#x200B;**機器人可以存取**&#x200B;您關心的URL，且頁面結構化，自動化分析是可靠的。 機器人規則、驗證、地理封鎖和重度個人化可能會減少涵蓋範圍。

## 相關主題

- [整合概述](overview.md)
- [將Adobe Commerce連線至LLM Optimizer](get-started/connect-to-llmo.md)
- [搭配Adobe Commerce使用LLM Optimizer](get-started/use-llmo-with-commerce.md)
