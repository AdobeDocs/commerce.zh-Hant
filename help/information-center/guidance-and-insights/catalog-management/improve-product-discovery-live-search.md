---
title: 使用Adobe Commerce Live Search改善產品探索
description: 瞭解如何使用搜尋效能見解和語意搜尋來協助購物者尋找相關產品。
audience: Merchandisers, commerce administrators, and store owners
autotag-review: '2026-10-21T12:57:39.807Z'
TQID: 'https://experienceleague.adobe.com/vUbbKdcd7RFb3YUNNjlW4u7AgtiXJKeZeRs9uJwxYyY'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 76cfaac4-e563-56dd-8938-708bf8b84956
    internal-label: Attributes
  - id: cdfd3bc1-dc23-5cf0-b965-d3c0c55cde67
    internal-label: Best Practices
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
    internal-label: Catalog management
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: 125c1f49-aefd-5f34-a252-288937f95f6b
    internal-label: Marketing Tools
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
topic_v2:
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
    internal-label: Insights
source-git-commit: f54c816fd23786ec519d5c890bc2664c3dcf8c6f
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 0%
---

# 使用Adobe Commerce Live Search改善產品探索

<table style="table-layout:auto">
<tr style="border: 0;">
   <td valign="middle" style="vertical-align: middle;"><img alt="桑德拉·岡薩雷斯·曼迦納肖像" src="../../assets/guidance-and-insights/live-search-author-avatar-sgonzalezmangana.png" width="96"><br><strong>Sandra Gonzalez Mangana</strong><br><em>資深產品經理</em></td>
</tr>
</table>

*透過搜尋效能分析和語意搜尋，協助購物者尋找他們需要的產品。*

在目錄中擁有正確的產品只是購物體驗的一部分。 購物者也需要能夠使用他們自然使用的字詞、詞句和問題來尋找這些產品。

Adobe Commerce即時搜尋提供搜尋效能深入分析，可幫助您找出探索問題並改善體驗。 使用這些見解來調查購物者遇到困難的位置，而不只是搜尋是否會傳回結果。

## 尋找搜尋效能中的訊號

在「即時搜尋效能」工作區中，檢閱量度，例如不重複搜尋、零結果搜尋、熱門結果、點進率、轉換率和平均點按位置等。 使用這些資訊來識別趨勢，並決定哪些查詢或產品需要注意。 [效能](https://experienceleague.adobe.com/zh-hant/docs/commerce/live-search/live-search-admin/performance)

![即時搜尋效能工作區會顯示不重複搜尋、平均點按位置、點進率、轉換率和零結果率，索引標籤會顯示不重複搜尋、零結果和熱門結果](../../assets/guidance-and-insights/live-search-performance-dashboard.png){width="800" zoomable="yes"}

*即時搜尋效能工作區會顯示要檢閱的量度。 顯示的值是範例資料。*

請考量下列訊號：

- **零結果搜尋：**&#x200B;沒有結果的查詢可能指向您的目錄、產品資訊或搜尋設定中的間隙。 目標是將零結果搜尋率保持在5%以下。 高於此臨界值的速率是值得研究的訊號。
- **低點進或弱點進位置：**&#x200B;購物者可能會看到不符合其需求的結果，或相關產品可能不夠突出。 為確保參與度，請至少將50%的搜尋設為目標，以便導致產品點選。
- **搜尋的低轉換率：**&#x200B;檢閱搜尋是否可協助購物者從查詢移至購買。 目標為超過3%的轉換率。

將它們視為基準和診斷訊號，而不是通用的通過或失敗。 效能會因產業、目錄複雜性、客戶行為及每個量度的測量方式而異。 建立存放區的基準，並比較一段時間內的效能。 結果可能會因您的目錄、購物者以及您測量結果的方式而異。

## 符合購物者意圖，而不僅僅是確切的字詞

購物者不一定會使用目錄中的術語來說明產品。 例如，搜尋「適合整天站立的舒適鞋子」的人，可能會對所謂的「緩衝式步行運動鞋」產品感興趣。

語意搜尋使用含意和內容加上關鍵字比對，有助於將自然語言查詢連線到相關產品，即使查詢與目錄字詞不完全相符。 即時搜尋將關鍵字和語意比對結合在一個搜尋體驗中。 [語意搜尋](https://experienceleague.adobe.com/zh-hant/docs/commerce/live-search/live-search-admin/semantic-search)

語意比對有助於探索性搜尋，但相關性仍取決於目錄中可用的產品和資訊。 對於包含精確模型、規格或相容性要求的搜尋，請檢查結果是否保持精確。

## 檢查部署的語意搜尋

設定取決於您使用的Adobe Commerce產品：

- **雲端基礎結構或內部部署上的Adobe Commerce：**&#x200B;即時搜尋語意搜尋可用於Adobe Commerce 2.4.4和更新版本。 在「管理員」中，前往「行銷> SEO和搜尋>即時搜尋」，開啟「設定」，啟用語意搜尋並儲存。 它支援英文目錄。 [設定 — 語意搜尋](https://experienceleague.adobe.com/zh-hant/docs/commerce/live-search/live-search-admin/settings)
- **Adobe Commerce as a Cloud Service：**&#x200B;系統預設會啟用語意搜尋。 它支援英文目錄。 [語意搜尋](https://experienceleague.adobe.com/zh-hant/docs/commerce/live-search/live-search-admin/semantic-search)
- **Adobe Commerce Optimizer：**&#x200B;系統預設會啟用語意搜尋。 您可以選擇調整控制項，例如語意提升和相似度臨界值。 這些設定也包含模糊搜尋選項。 [語意搜尋](https://experienceleague.adobe.com/zh-hant/docs/commerce/optimizer/setup/semantic-search) · [設定 — 選擇性調整](https://experienceleague.adobe.com/zh-hant/docs/commerce/optimizer/settings)

## 將搜尋深入分析轉化為行動

使用持續稽核週期來改善產品探索：

1. **尋找要調查的查詢。** 檢閱零結果搜尋、熱門查詢和低參與度的搜尋。
2. **檢查購物者想要什麼。** 判斷查詢是否指向遺失的產品、字詞不符或不清楚的產品資料。
3. **改善產品資訊。** 讓產品屬性和說明對於購物者使用的字詞準確而實用。 針對「即時搜尋」，Adobe建議設定適當的可搜尋屬性和權重，並確保屬性資料具有相關性。 [即時搜尋最佳實務](https://experienceleague.adobe.com/zh-hant/docs/commerce/live-search/best-practice)
4. **調整搜尋體驗。** 在適當的情況下，使用搜尋規則、同義字和Facet來協助購物者尋找及縮小相關結果。 [即時搜尋最佳實務](https://experienceleague.adobe.com/zh-hant/docs/commerce/live-search/best-practice)
5. **檢閱結果並重複。** 變更後，監控相同的查詢和效能訊號，然後根據購物者的做法進行調整。

## 將每個搜尋都列入計數

搜尋查詢是購物者想要的訊號。 將搜尋效能深入解析與相關的產品資訊和正確的搜尋功能配對，可以讓購物者更輕鬆地找到符合其需求的產品。

### 了解更多

- [什麼是Live Search？](../../../live-search/overview.md)
- [Live Search最佳作法](../../../live-search/best-practice.md)
- 雲端基礎結構上Adobe Commerce的[語意搜尋](../../../live-search/semantic-search.md)
- Adobe Commerce Optimizer的[語意搜尋](../../../optimizer/setup/semantic-search.md)
