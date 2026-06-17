---
title: 預估資料量和同步處理時間
description: 瞭解如何估計 [!DNL Adobe Commerce Optimizer Connector] 摘要的資料量和同步處理時間，以規劃目錄同步並避免中斷。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="僅限PaaS" type="Informative" url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案（Adobe管理的PaaS基礎結構）和內部部署專案的Adobe Commerce 。"
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c32adafa-ed01-4b31-997e-2413013911b0
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 469
ht-degree: 0%

---


# 預估資料量和同步處理時間

Adobe建議您在開始任何摘要同步處理前，先預估資料量和同步處理時間，以確保順暢的排程並避免網站作業中斷。 這在規劃初始同步或大規模目錄更新（例如大量價格變更）時尤其重要。

依預設，聯結器會以單螺紋模式處理進給。 摘要提交程式沒有平行化。 內嵌API每秒最多可接受2個請求。 不過，[!DNL Adobe Commerce Optimizer]擷取速率的基底配置會將輸送量限製為下列專案：

- 每分鐘最多1,000種產品（產品是包含特定商店檢視中屬性的SKU）。 如需基底配置詳細資訊，請參閱[限制和邊界](../../optimizer/boundaries-limits.md)。
- 最高每分鐘50,000個價格

## 影響同步時間的因素

下列的估計假設條件如下：

- 執行緒計數： 1 （預設）
- 摘要接受率：每秒2個要求（每個要求0.5秒）
- 所有產品都會指派至所有現有網站

實際傳輸速度視要求裝載大小和Commerce應用程式伺服器上的目前負載而定。

## 計算每個摘要的同步時間

使用下表來預估每個聯結器資訊源的記錄數、請求數和同步時間。 批次大小值反映[支援的摘要](connector-reference.md#supported-feeds)參考中定義的限制。

>[!NOTE]
>
>產品同步時間以每分鐘1,000個產品的基本配置限製為基礎。 對於其他摘要，計算則以每秒2個要求的傳輸率為基礎。 實際速度視裝載大小和伺服器負載而定。
>
>預估價格會假設所有客戶群組都有獨特的價格。

| 摘要 | 資料範例 | 公式 | 預測的要求 | 預測的同步處理時間 |
| ---- | ------------ | ------- | ------------------ | ------------------- |
| 產品 | 產品(P)：10,000，商店檢視(SV)：4 | P × SV = 40,000筆記錄 | 40,000 ÷批次大小(100) = 400 | 40,000 ÷ 1,000筆記錄/分鐘= **40分鐘** |
| 類別 | 類別(C)：500，商店檢視(SV)：4 | C × SV = 2,000筆記錄 | 2,000 ÷批次大小(100) = 20 | （20 × 0.5秒） ÷ 60 = **~10 s** |
| 產品屬性 | 屬性(A)：200，存放區檢視(SV)：4 | A × SV = 800筆記錄 | 800 ÷批次大小(100) = 8 | （8 × 0.5秒） ÷ 60 = **~4 s** |
| 價格 | 產品(P)：10,000、網站(WS)：2、客戶群組(CG)：6 | P × WS × CG = 120,000筆記錄 | 120,000 ÷批次大小(500) = 240 | （240 × 0.5秒） ÷ 60 = **2分鐘** |
| 價格簿 | 網站(WS)：2、客戶群組(CG)：6 | WS × CG = 12筆記錄 | 12 ÷批次大小(500) = 1 | （1 × 0.5秒） ÷ 60 = **&lt; 1 s** |

>[!MORELIKETHIS]
>
> - [聯結器模組和摘要端點](connector-reference.md) — 檢閱批次限制和支援的摘要
> - [管理同步](../data-sync-manage.md) — 監視同步狀態並觸發手動重新同步
> - [聯結器同步管道](../connector-sync-pipeline.md) — 瞭解cron排程和自動同步如何運作
