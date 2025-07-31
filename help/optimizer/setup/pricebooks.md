---
title: 價格手冊
description: 瞭解如何在 [!DNL Adobe Commerce Optimizer]中管理價格簿。
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案(Adobe管理的SaaS基礎結構)。"
exl-id: a1849830-3d0e-4df9-ab73-380659c3f9dc
source-git-commit: 513ed97442bfffe74d64f4eb0484cfa8f25b5ecc
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# 價格手冊

價格手冊可讓您針對不同客戶層級和市場的目錄來源，定義產品價格。 價格簿支援階層式模型，允許每個基本價格簿下最多三個層級的巢狀子價格簿。 每個價格簿都可以參考上階價格簿，以構成訂價型錄來源的樹狀結構。

基準價格簿會定義其本身及其所有子價格簿的幣別。 子價格簿會繼承此幣別，且無法覆寫它。

請參閱[開發人員檔案](https://developer.adobe.com/commerce/services/reference/rest/)，瞭解如何使用價格簿API來建立、更新及刪除價格簿[!DNL Adobe Commerce Optimizer]。

## 重要概念

| 詞語 | 說明 |
|------|-------------|
| **價格簿** | 邏輯群組，定義型錄來源的價格；例如，特定區域或客戶階層，用來管理產品價格。 |
| **遞補價格手冊** | 階層中最上層的價格簿。 它沒有父代，而且是&#x200B;*僅*&#x200B;價格簿，定義其本身及其所有子系價格簿的貨幣。<br/><br/>如果在建立價格簿期間（透過API）未定義上階，則會建立新的備援價格簿。 |
| **父價格簿** | 較高層級的價格簿，若未明確設定子項價格，則子項價格簿可從中繼承價格。 |
| **階層深度** | 最多3個層級（備援 — >子項 — >子項）<br/><br/>在內嵌時未強制執行。 |
| **貨幣** | 僅針對遞補價格簿定義。 由所有下階價格簿繼承。<br/><br/>如果在建立備援價格簿期間未指定貨幣（透過API），則貨幣預設為USD。 |
| **產品價格** | 指定給特定價格簿中之產品(SKU)的特定價格。 |
| **折扣** | 折扣以產品價格定義。 未繼承。 |
