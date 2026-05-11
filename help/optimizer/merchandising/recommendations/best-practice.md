---
title: Recommendations最佳作法
description: 瞭解您可以在網站的各個頁面上放置建議，以及針對每種建議型別的常用標籤提供建議。
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和 [!DNL Adobe Commerce Optimizer] 專案（Adobe管理的SaaS基礎結構）。"
exl-id: 08d7aeff-8b86-4fa3-93e6-4b72dc1ab117
TQID: https://experienceleague.adobe.com/J4vSJ4EMfSTeL7rVEv9bTr998wvU5DR4S-hXQ3HCSGg
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
topic_v2:
  - id: bcc5edb5-84c3-4940-9f84-ed88b6c16274
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 360
ht-degree: 0%

---

# Recommendations最佳作法

Adobe建議您在使用Recommendations時遵循下列准則：

- 讓您的建議型別多樣化。 如果客戶一再建議相同的產品，就會開始忽略建議。

- 請勿將相同的建議部署至購物車頁面和訂單確認頁面。 請考慮將`Most Added to Cart`用於購物車頁面，並將`Bought This, Bought That`用於訂單確認頁面。

- 保持網站整潔。 請勿在同一頁面上部署超過三個建議單位。

- 如果您的商店銷售服裝，`More like this`建議可能會建議與檢視產品性別不符的性別特定產品。 請考慮僅針對非服裝類別使用此建議型別。

## 產品建議放置環境

有這麼多建議型別可供選擇，您應在每個頁面上使用哪一種？ 如果您不確定從何處開始，請嘗試下列步驟：

| 頁面 | 建議型別 |
|---|---|
| 首頁 | `Recommended for you` |
| 產品頁面 | `Viewed this, viewed that` |
| 購物車 | `Bought this, bought that` |

您可以追蹤[量度](../../manage-results/recommendation-performance.md)，並視需要加以調整。 請記住，實驗是關鍵。

## 建議標籤

指定給店面中推薦的標籤會影響購物者如何解讀其與他們的相關性。 以下標籤經常用於每種型別的建議。

| 建議型別 | 建議的標籤 |
|---|---|
| 檢視次數最多<br>加入購物車的次數最多<br>購買次數最多<br>轉換（檢視到購物車）<br>轉換（檢視到購買） | 最受歡迎<br>熱門專案<br>趨勢<br>目前最受歡迎<br>最近最受歡迎<br>受此專案啟發的熱門專案(PDP)<br>最暢銷商品<br>您可能有興趣 |
| 為您推薦 | 正適合您<br>為您推薦<br>靈感來自您的購物趨勢 |
| 已檢視這個專案，已檢視那個專案 | 檢視此專案的客戶也檢視了<br>客戶也檢視了<br>相關專案 |
| 已檢視此專案，但購買了其他專案 | 瀏覽過此專案的客戶最終購買<br>客戶最終購買<br>其他人瀏覽此專案後會購買什麼？ |
| 購買了此專案，也購買了其他專案 | 取得您所需要的一切<br>別忘了這些<br>經常一起購買 |
| 更多相關資訊 | 其他類似專案<br>類似專案 |
| 通用 | 您可能也會喜歡<br>購物者也喜歡<br>類似的選項<br>相關專案 |
| 趨勢 | 趨勢<br>目前趨勢<br>最近趨勢<br>熱門專案<br>趨勢相關產品(PDP) |
| 最近檢視的專案 | 最近檢視的專案<br>請再檢視一次 |
