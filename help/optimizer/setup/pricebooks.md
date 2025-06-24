---
title: 價格手冊
description: 瞭解如何在 [!DNL Adobe Commerce Optimizer]中管理價格簿。
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案(Adobe管理的SaaS基礎結構)。"
source-git-commit: 553490762ef10e43ccce1654acec59aeb83bb5f9
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---

# 價格手冊

本文會說明如何定義價格簿，並將其指定給具有適當資料控管控制的目錄檢視表。

請參閱[開發人員檔案](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/api-reference/#tag/Price-Books)，瞭解如何使用價格手冊API將協力廠商系統的價格手冊資訊擷取到[!DNL Adobe Commerce Optimizer]。

透過價格簿，您可以定義定價目錄來源，以管理不同客戶層級和市場的產品價格。 價格簿支援階層式模型，允許每個基本價格簿下最多三個層級的巢狀子價格簿。 每個價格簿都可以參考上階價格簿，以構成訂價型錄來源的樹狀結構。

基準價格簿會定義其本身及其所有子價格簿的幣別。 子價格簿會繼承此幣別，且無法覆寫它。

## 重要概念

| 詞語 | 說明 |
|------|-------------|
| **價格簿** | 定義價格型錄來源的邏輯群組；例如，特定區域或客戶層，用來管理產品價格。 |
| **遞補價格手冊** | 階層中最上層的價格簿。 它沒有父代，而且是&#x200B;*僅*&#x200B;價格簿，定義其本身及其所有子系價格簿的貨幣。<br/><br/>如果在建立價格簿期間（透過API）未定義上階，則會建立新的備援價格簿。 |
| **父價格簿** | 較高層級的價格簿，若未明確設定子項價格，則子項價格簿可從中繼承價格。 |
| **階層深度** | 最多3個層級(備援→子項→孫項)<br/><br/>在內嵌時未強制執行。 |
| **貨幣** | 僅定義於遞補價格簿。 由所有子系繼承，價格手冊。<br/><br/>如果在建立備援價格簿期間未指定貨幣（透過API），則貨幣預設為USD。 |
| **產品價格** | 指定給特定價格簿中之產品(SKU)的特定價格。 |
| **折扣** | 折扣在產品價格中定義。 未繼承。 |
