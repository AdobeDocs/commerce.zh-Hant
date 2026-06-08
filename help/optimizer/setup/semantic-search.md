---
title: 語意搜尋
description: 從[設定]啟用 [!DNL Adobe Commerce Optimizer] 中的AI語意搜尋。 不需要屬性設定或店面變更。
role: Admin, User
recommendations: noCatalog
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和 [!DNL Adobe Commerce Optimizer] 專案（Adobe管理的SaaS基礎結構）。"
source-git-commit: 015f88e540fe5bf7acc4469d7c91b4f606709809
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 0%

---

# 語意搜尋

語意搜尋會使用AI來瞭解購物者的意思，而不只是他們鍵入的字詞。 即使您的目錄未使用相關片語，如「沙灘婚禮的禮服」或「一整天都穿著舒服的鞋子」等查詢仍可傳回相關產品。

[!DNL Adobe Commerce Optimizer]在一個搜尋體驗中結合關鍵字比對和語意比對。 您不會在店面管理個別的關鍵字和語意模式。 在Admin中，移至[設定](../settings.md#advanced-search)工作區以管理語意搜尋，並可選擇調整&#x200B;**[!UICONTROL Advanced search]**&#x200B;標籤上的進階控制項。

## 優點

- **更少的空白搜尋頁面** — 當購物者的文字與目錄文字不符時，購物者會尋找產品。
- **更好的比對方式** — 自然、描述性的查詢會傳回有用的結果。
- **少一些同義字維護** — 常見的字詞變化（例如，沙發和沙發）通常不需要手動同義字清單即可處理。
- **沒有店面或開發人員工作** — 語意搜尋預設為啟用，不需要主題代碼、下拉式清單或API變更。

## 運作方式

啟用語意搜尋時，[!DNL Adobe Commerce Optimizer]會使用系統選擇的預先定義目錄屬性（例如產品名稱和說明），將查詢含義與傳統關鍵字搜尋一併解譯。 您不會在「管理員」中選取或排列屬性的優先順序。

例如：

- 搜尋「皮沙發」會傳回標示為「皮沙發」的產品。
- 即使產品名稱中沒有「春天」，「春天連身裙」也可以出現季節性連身裙。
- 「步道跑鞋」可搭配越野或登山鞋類產品。

## 當您啟用語意搜尋時會發生什麼事

語意搜尋可與您現有的[!DNL Adobe Commerce Optimizer]搜尋設定搭配使用。 您沒有取代關鍵字搜尋或重新設定店面。

語意搜尋作用中時：

- 您現有的[銷售規則](../merchandising/rules/overview.md)、[同義字](../merchandising/synonyms/overview.md)、[面向](../merchandising/facets/overview.md)、提升和篩選器會繼續套用。
- 語意搜尋可新增AI支援的購物者意圖理解，以隨著關鍵字比對改善結果相關性。
- 預先定義的目錄屬性會自動編制索引。 您不選取屬性或發佈個別的設定。

## 在管理員中管理語意搜尋

語意搜尋預設為&#x200B;**為符合資格的英文目錄啟用**。 移至&#x200B;**[!UICONTROL Settings]** > **[!UICONTROL Advanced search]**&#x200B;以確認設定或進行變更：

1. 在Admin中，移至&#x200B;**[!UICONTROL Settings]**。
1. 在&#x200B;**[!UICONTROL Advanced search]**&#x200B;標籤上，檢閱&#x200B;**[!UICONTROL Enable semantic search]**。

   啟用後，搜尋會根據含義和內容比對產品，藉此產生更相關的結果、較少的空白搜尋頁面，並改善轉換。

1. 如果您變更切換或調整控制項，請按一下&#x200B;**[!UICONTROL Save]**。

   索引完成之後會更新搜尋結果。 對於中型型錄，編制索引最多可能需要半小時。 若為包含數百萬項產品的大型目錄，則可能需要數小時的時間。

>[!NOTE]
>
> 語意搜尋僅適用於&#x200B;**英文**&#x200B;目錄。 如果您將&#x200B;**[!UICONTROL Language]**&#x200B;變更為非英文目錄，**[!UICONTROL Enable semantic search]**&#x200B;會自動停用。

儲存後，您不需要發佈單獨的組態或變更店面設定。

## 啟用後驗證

語意搜尋作用中且索引完成之後，Adobe建議驗證搜尋效能。 使用[搜尋效能](../manage-results/search-performance.md)頁面來檢閱對您業務而言重要的度量和測試查詢。

1. 檢閱您在&#x200B;**唯一搜尋**&#x200B;報表中搜尋最多的辭彙。
1. 從店面的&#x200B;**零結果**&#x200B;報告測試歷史零結果查詢。
1. 比較啟用前後相同查詢的搜尋結果。
1. 監控搜尋轉換和參與量度，包括點進率、轉換率和零結果率。

## 選擇性調整

在&#x200B;**[!UICONTROL Advanced search]**&#x200B;索引標籤上，您可以調整語意搜尋啟用後搜尋的行為方式：

- **[!UICONTROL Semantic boost]** — 增加或減少強式含意比對影響排名。 例如，假設透過語意搜尋擷取的產品相符專案顯示在結果結尾。 加入提升會將其在結果中向上移動。
- **[!UICONTROL Similarity threshold]** — 設定產品出現之前相符專案必須接近的程度。 值越低，顯示的結果越多；值越高，顯示的符合越少、越嚴格。
- **[!UICONTROL Fuzzy search]**&#x200B;和&#x200B;**[!UICONTROL Fuzzy search similarity threshold]** — 當查詢包含小型拼字差異時，協助購物者尋找產品。

如需控制項說明和逐步指導，請參閱[進階搜尋](../settings.md#advanced-search)。

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
