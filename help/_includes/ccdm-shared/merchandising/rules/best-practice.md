---
source-git-commit: e3be9274ca8db80d3559b24a5c8be36f5d61b2ba
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 0%
---
<!--
SOURCE OF TRUTH: Edit this file in the commerce.en repo:
https://github.com/Adobe-Enterprise-Docs/commerce.zh-Hant/blob/main/help/_includes/ccdm-shared/merchandising/rules/best-practice.md

This content is shared by the Adobe Commerce Optimizer Guide (commerce.en) and the
Merchandising Services with CCDM Guide (commerce-admin.en). Changes made in commerce.en
are synced automatically to commerce-admin.en, so do not edit the copy in that repo.
This includes related images in help/assets/ccdm-shared/.
-->

# 銷售規則最佳實務

若要最佳化轉換和收入，請實作有效的&#x200B;**搜尋規則**、強大的&#x200B;**預設清單**&#x200B;規則和&#x200B;**[類別規則](https://experienceleague.adobe.com/zh-hant/docs/commerce/optimizer/merchandising/rules/add#rule-types)**。 使用銷售資料、庫存、促銷活動和[智慧型排名](https://experienceleague.adobe.com/zh-hant/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking)調整排名。

只有在符合的購物者查詢必須傳回零個產品時，才使用[搜尋隱藏規則](https://experienceleague.adobe.com/zh-hant/docs/commerce/optimizer/merchandising/rules/overview#search-suppression-rules)，而不是當產品需要不同的排名時。

建立深思熟慮的&#x200B;**預設規則**&#x200B;至關重要。 您的[預設規則](https://experienceleague.adobe.com/zh-hant/docs/commerce/optimizer/merchandising/rules/overview#default-rule)會決定搜尋結果在未套用特定搜尋規則時的初始排序方式，這可以改善探索和購買的可能性。 請定期檢閱，以符合購物者需求和行銷活動。

## 最佳化搜尋規則的提示

- 釘選或提升高銷量或近期銷售活動的產品。
- 優先處理高評等和正面評論的產品。
- 確保庫存專案排名較高。
- 稍微優先處理利潤率較高的產品，而不會影響關聯性。
- 標示在銷售中或屬於特別促銷的產品。
- 使用促銷期間的日期範圍，在促銷期間或銷售期間自動設定搜尋規則。
- 根據使用[智慧型排名](https://experienceleague.adobe.com/zh-hant/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking)的個別購物者行為量身打造搜尋結果，例如「為您推薦」、「檢視次數最多」等。
- 當選取&#x200B;**無**&#x200B;以外的智慧策略時，針對每個規則調整&#x200B;**[智慧排名提升](https://experienceleague.adobe.com/zh-hant/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking-boost)**，並在發佈前於&#x200B;**測試您的規則**&#x200B;進行驗證。
- 請一律使用「測試規則」面板來預覽您的智慧排名策略如何影響不同查詢的實際搜尋結果。

## 類別規則的提示

- 在高流量或高利潤的&#x200B;**類別頁面**&#x200B;上使用[類別規則](https://experienceleague.adobe.com/zh-hant/docs/commerce/optimizer/merchandising/rules/add#rule-types)，其中已組織的訂單與搜尋一樣重要，例如，季節性系列或精選部門。
- 將&#x200B;**智慧型排名** （例如，趨勢、檢視次數最多）與購物者瀏覽該類別的方式對齊；類別頁面不會像搜尋規則那樣使用搜尋查詢文字。 請參閱[智慧型排名](https://experienceleague.adobe.com/zh-hant/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking)。 對於&#x200B;**無**&#x200B;以外的智慧型方法，請使用&#x200B;**[智慧型排名提升](https://experienceleague.adobe.com/zh-hant/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking-boost)**&#x200B;和類別預覽，以調整該類別規則的行為強度。
- 套用&#x200B;**圖釘**、**提升**&#x200B;和&#x200B;**埋藏**&#x200B;的方式與您的行銷活動計劃一致；請記住，只有當購物者對清單使用&#x200B;**預設排序**&#x200B;時，才會套用手動位置。 請參閱[手動排名](https://experienceleague.adobe.com/zh-hant/docs/commerce/optimizer/merchandising/rules/add#manual-ranking)。
- 在編輯器中預覽&#x200B;**類別**&#x200B;規則流程，並在發佈後在店面進行驗證，這與您在搜尋時「測試您的規則」面板使用的規則相同。

## 搜尋隱藏最佳實務和使用案例 {#search-suppression-best-practices}

搜尋隱藏規則會封鎖符合其條件的查詢結果，所以店面會顯示不含產品的搜尋結果頁面。 規則編輯器不提供隱藏規則的預覽。 使用符合限制的最窄條件，然後遵循[建立和管理搜尋隱藏規則](https://experienceleague.adobe.com/zh-hant/docs/commerce/optimizer/merchandising/rules/add#search-suppression-rules)。 規則啟動後，請驗證店面中相符和不相符的搜尋。 檢查店面的實際無結果簡報。

| 使用案例 | 建議的設定 | 檢查內容 |
| --- | --- | --- |
| 搜尋的法規遵循 | 將規則範圍設定為受影響的目錄檢視，並比對受限制的搜尋字詞。 | 向您的合規團隊確認條款。 單是搜尋隱藏不會阻止透過類別導覽、銷售頁面、建議或直接產品URL進行存取。 |
| 品牌限制 | 當受限品牌名稱必須封鎖較長的查詢時，請使用&#x200B;**查詢包含**。 | 規則啟動後，請檢查包含類似文字的不相關店面查詢，以避免隱藏合法的搜尋。 |
| 防止特定搜尋字詞傳回結果 | 使用&#x200B;**Query is**&#x200B;取得應該不會傳回任何產品的精確片語。 | 請個別檢查相關片語。 完全相符條件不會封鎖包含該片語的每個查詢。 |
| 查詢首碼或尾碼的限制 | 當限制文字的位置很重要時，使用&#x200B;**查詢開頭為**&#x200B;或&#x200B;**查詢結尾為**。 | 規則啟動後，請檢查店面查詢，並以開頭、中間和結尾的文字確認預期的範圍。 |
| 暫時搜尋限制 | 設定時間限制限制的開始和結束日期。 | 確認排程和啟用狀態，並檢閱限制結束後是否仍需要規則。 |

- 為每個規則指定一個描述性名稱，並在其說明中記錄限制的原因。
- 發佈變更前請先檢閱查詢條件。 規則生效後，請檢查應封鎖的店面查詢以及仍應傳回產品的查詢。 快取查詢結果最多可能需要15分鐘才能重新整理。
- 檢閱店面的無結果狀態，並確定購物者有實用方式繼續瀏覽，例如修訂查詢或導覽至店面支援的類別。
- 請勿使用查詢隱藏作為產品層級排除的替代項。 若要跨搜尋結果、搜尋建議及自動完成排除產品，請使用手動排除或&#x200B;**以屬性為基礎的銷售事件**，並在&#x200B;**預設搜尋規則**&#x200B;中以&#x200B;**隱藏**&#x200B;動作進行。
- 定期檢閱作用中隱藏規則。 停用不再需要的規則，或在限制變更時進行編輯和發佈。
