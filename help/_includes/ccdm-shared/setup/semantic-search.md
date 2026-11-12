---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%
---
語意搜尋會使用AI來瞭解購物者的意思，而不只是他們鍵入的字詞。 即使您的目錄未使用相關片語，如「沙灘婚禮的禮服」或「一整天都穿著舒服的鞋子」等查詢仍可傳回相關產品。

產品探索系統將關鍵字比對和語意比對結合在一個搜尋體驗中。 您不會在店面管理個別的關鍵字和語意模式。

## 設定語意搜尋

語意搜尋預設為&#x200B;**為符合資格的英文目錄啟用**。 您可以在[設定](../settings.md#advanced-search)工作區的&#x200B;**[!UICONTROL Advanced search]**&#x200B;標籤上管理它，您可以在此確認或變更設定，並選擇性調整語意提升、相似度臨界值和模糊搜尋。 請參閱[設定](../settings.md#access-the-settings-workspace)，瞭解如何開啟工作區。

儲存後，您不需要發佈單獨的組態或變更店面設定。

## 優點

- **更少的空白搜尋頁面** — 當購物者的文字與目錄文字不符時，他們就會尋找產品。
- **更好的比對方式** — 自然、描述性的查詢會傳回有用的結果。
- **少一些同義字維護** — 常見的字詞變化（例如，沙發和沙發）通常不需要手動同義字清單即可處理。
- **沒有店面或開發人員工作** — 語意搜尋預設為啟用，不需要主題代碼、下拉式清單或API變更。

## 運作方式

啟用語意搜尋時，系統會使用預先定義的目錄屬性（例如產品名稱和說明）來解譯與傳統關鍵字搜尋並列的查詢含義。 您不會在「設定」中選取屬性或排列其優先順序。

例如：

- 搜尋「皮沙發」會傳回標示為「皮沙發」的產品。
- 即使產品名稱中沒有「春天」，「春天連身裙」也可以出現季節性連身裙。
- 「步道跑鞋」可搭配越野或登山鞋類產品。

## 當您啟用語意搜尋時會發生什麼事

語意搜尋可與您現有的搜尋設定搭配使用。 您沒有取代關鍵字搜尋或重新設定店面。

語意搜尋作用中時：

- 您現有的[銷售規則](../merchandising/rules/overview.md)、[同義字](../merchandising/synonyms/overview.md)、[面向](../merchandising/facets/overview.md)、提升和篩選器會繼續套用。
- 語意搜尋可新增AI支援的購物者意圖理解，以隨著關鍵字比對改善結果相關性。
- 預先定義的目錄屬性會自動編制索引。 您不選取屬性或發佈個別的設定。

## 啟用後驗證

語意搜尋作用中且索引完成之後，Adobe建議驗證搜尋效能。 使用[搜尋效能](../manage-results/search-performance.md)頁面來檢閱對您業務而言重要的度量和測試查詢。

1. 檢閱您在&#x200B;**唯一搜尋**&#x200B;報表中搜尋最多的辭彙。
1. 從店面的&#x200B;**零結果**&#x200B;報告測試歷史零結果查詢。
1. 比較啟用前後相同查詢的搜尋結果。
1. 監控搜尋轉換和參與量度，包括點進率、轉換率和零結果率。

## 最佳實務

- 使用清楚的描述性產品名稱和說明（最好是50-100個字），讓關鍵字和語意比對都有強大的目錄文字可供使用。
- 從預設&#x200B;**[!UICONTROL Enable semantic search]**&#x200B;設定開始，然後只有在結果範圍太廣或太窄時才調整&#x200B;**[!UICONTROL Semantic boost]**&#x200B;或&#x200B;**[!UICONTROL Similarity threshold]**。
- 保留特定品牌或高度技術性的[同義字](../merchandising/synonyms/overview.md)，其中語意搜尋可能不包含專用字詞。

## 疑難排解

| 問題 | 該做什麼 |
| --- | --- |
| 儲存後店面沒有變更 | 等待索引完成。 大型目錄可能需要更長的時間。 |
| 結果過於寬泛 | 在&#x200B;**[!UICONTROL Advanced search]**&#x200B;索引標籤上提高&#x200B;**[!UICONTROL Similarity threshold]**&#x200B;或降低&#x200B;**[!UICONTROL Semantic boost]**。 |
| 結果感覺太窄 | 降低&#x200B;**[!UICONTROL Similarity threshold]**&#x200B;或提高&#x200B;**[!UICONTROL Semantic boost]**。 |
| 語意搜尋無法使用 | 確認&#x200B;**[!UICONTROL Language]**&#x200B;已設定為&#x200B;**英文**。 |

## 限制 {#semantic-search-limitations}

- **目錄語言：**&#x200B;語意搜尋僅適用於&#x200B;**英文**&#x200B;語言目錄。

## 有關此主題的更多說明

- [進階搜尋](../settings.md#advanced-search)
- [同義字](../merchandising/synonyms/overview.md)
- [搜尋績效](../manage-results/search-performance.md)
