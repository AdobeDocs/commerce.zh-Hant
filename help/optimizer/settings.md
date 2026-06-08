---
title: 設定
description: 設定 [!DNL Adobe Commerce Optimizer]的設定。
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和 [!DNL Adobe Commerce Optimizer] 專案（Adobe管理的SaaS基礎結構）。"
exl-id: 6ac223de-8e03-4842-8b67-92ce321d323d
TQID: https://experienceleague.adobe.com/9-BMXoWad0bbvsnwgHQrs19ZC9ngGrVE9J7PszcX4Zc
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 015f88e540fe5bf7acc4469d7c91b4f606709809
workflow-type: tm+mt
source-wordcount: 867
ht-degree: 0%

---

# 設定

使用&#x200B;*設定*&#x200B;工作區來設定您店面的搜尋和產品探索。 可使用下列標籤：

- **價格Facet** — 設定價格範圍群組和間隔做為搜尋篩選器。
- **語言** — 設定用於索引和搜尋的目錄語言。
- **進階搜尋** — 啟用語意搜尋和模糊搜尋，並調整語意提升和相似度臨界值。

>[!BEGINTABS]

>[!TAB 價格Facet]

## 價格Facet {#price-facets}

您可以指定價格範圍群組的數量，以及價格值在群組之間的分配方式。 每個價格範圍會依序與上一個群組重疊。 例如，使用間隔為20的五個群組時，您會得到價格範圍，例如0-20、20-40、40-60、60-80和>80。 如果目錄中沒有足夠產品可填滿所有已定義的範圍，則會相應地調整可用群組的顯示。 例如：0-20、60-80、>80。

**設定價格Facet：**

1. 在&#x200B;**設定**&#x200B;工作區中，選取&#x200B;**[!UICONTROL Facets]**。
1. 在&#x200B;**價格Facet**&#x200B;區段中，執行下列動作：
   - 輸入可用的&#x200B;**[!UICONTROL Number of selections]**&#x200B;或價格群組。 最多可定義100個價格群組。
   - 輸入每個群組的&#x200B;**[!UICONTROL Interval value]**&#x200B;或價格範圍。 最大值為40,000,000。
1. 按一下&#x200B;**[!UICONTROL Save]**。

   更新後的設定約需15分鐘才能在店面提供。

### 欄位說明

| 欄位 | 說明 |
| --- | --- |
| 選擇數量 | 指定可在店面中作為搜尋篩選器使用的價格範圍群組數目。 預設值：8，最大值：100 |
| 間隔值 | 指定每個群組的價格範圍間隔。 例如，間隔值為20良品率群組0-20、20-40、40-60、60-80和>80的五種選擇。 預設值：5，最大值：40,000,000 |

>[!TAB 語言]

## 語言 {#language}

語言設定可告知[!DNL Adobe Commerce Optimizer]讀取目錄和寫入索引時預期的語言。

語言有不同的語法規則集：例如，如何分隔字詞、動詞句子和字詞形式。
語言設定可確保將正確的規則集套用到索引機制。

將語言設定設為目錄的主要語言。 當您變更索引的語言時，視目錄的大小和複雜度而定，可能需要5到60分鐘的時間才能將變更顯示在店面上。

| 語言 | 程式碼 |
|----|----|
| 阿拉伯文 | ar |
| 亞美尼亞文 | hy |
| 巴斯克語 | 歐盟 |
| 孟加拉文 | bn |
| 巴西文 | pt-br |
| 保加利亞文 | bg |
| 加泰隆尼亞文 | ca |
| 中文（簡體） | zh-cn |
| 中文（繁體） | zh-tw |
| 捷克文 | cs |
| 丹麥文 | da |
| 荷蘭文 | nl |
| 英文 | en |
| 愛沙尼亞文 | et |
| 芬蘭文 | fi |
| 法文 | fr |
| 加利西亞語 | gl |
| 德文 | de |
| 希臘文 | el |
| 北印度文 | 嗨 |
| 匈牙利文 | hu |
| 印尼文 | id |
| 愛爾蘭文 | ga |
| 義大利文 | it |
| 日文（片假名） | ja |
| 韓文 | ko |
| 拉脫維亞文 | lv |
| 立陶宛文 | lt |
| 挪威文 | 否 |
| 波斯文 | fa |
| 葡萄牙文 | pt |
| 羅馬尼亞文 | ro |
| 俄文 | ru |
| 索拉尼 | ku |
| 西班牙文 | es |
| 瑞典文 | sv |
| 土耳其文 | tr |
| 泰文 | th |

>[!TAB 進階搜尋]

## 進階搜尋 {#advanced-search}

使用&#x200B;**[!UICONTROL Advanced search]**&#x200B;索引標籤在一個位置管理搜尋。 [!DNL Adobe Commerce Optimizer]在店面提供整合式搜尋體驗；您沒有針對購物者分別設定關鍵字搜尋和語意搜尋。 根據預設，**[!UICONTROL Enable semantic search]**&#x200B;已為符合資格的英文目錄&#x200B;**啟用**。 語意搜尋可與您現有的設定搭配使用；會繼續套用[銷售規則](./merchandising/rules/overview.md)、[同義字](./merchandising/synonyms/overview.md)、[面向](./merchandising/facets/overview.md)、提升與篩選器。 系統會自動使用預先定義的目錄屬性 — 您不會在「管理員」中選取或排列屬性的優先順序。 不需要變更店面或開發人員。

![進階搜尋設定](./assets/advanced-search.png)

**若要管理語意搜尋：**

1. 在&#x200B;**設定**&#x200B;工作區上，選取&#x200B;**[!UICONTROL Advanced search]**&#x200B;索引標籤。
1. 在&#x200B;**[!UICONTROL Enable semantic search]**&#x200B;底下，確認已啟用語意搜尋，或如果您不想進行語意比對，請停用該功能。
1. 如果您變更切換或調整控制項，請按一下&#x200B;**[!UICONTROL Save]**。

   索引完成之後會更新搜尋結果。 對於中型型錄，編制索引最多可能需要半小時。 若為包含數百萬項產品的大型目錄，則可能需要數小時的時間。

### 選擇性調整

啟用語意搜尋後，您可在相同標籤上調整下列專案：

- **[!UICONTROL Semantic boost]** — 套用提升以優先處理排名中語義相關的結果。 當語意比對在結果集中應該加重時，請提高值；當結果感覺過於廣泛時，請降低值。
- **[!UICONTROL Similarity threshold]** — 設定語意比對的最低相似度分數（百分比）。 較低的值會傳回較多結果（較高的召回率），但可能包括較弱的符合專案。 值越高傳回的相符項越少，越嚴格（精確度越高）。

  >[!NOTE]
  >
  > 僅支援&#x200B;**英文**&#x200B;目錄的語意搜尋。 在&#x200B;**[語言](#language)**&#x200B;索引標籤上選取其他語言會停用&#x200B;**[!UICONTROL Enable semantic search]**。

- **[!UICONTROL Fuzzy search]** — 開啟&#x200B;**&#x200B;**&#x200B;以尋找搜尋查詢的近似相符專案，這有助於更正拼字和細微變化。
- **[!UICONTROL Fuzzy search similarity threshold]** — 設定出現模糊相符項所需的最小相似度（以百分比表示）。 較低的臨界值會傳回比較接近的相符專案；如果模糊結果範圍太廣，請提高臨界值。

如需優點、驗證指南、最佳實務、疑難排解及限制，請參閱[語意搜尋](setup/semantic-search.md)。

### 欄位說明

| 控制 | 說明 |
| --- | --- |
| 啟用語意搜尋 | 啟用後，搜尋會使用關鍵字比對的意義與內容。 預先定義的目錄屬性會自動使用；不需要在「管理員」中進行屬性設定。 已為[!DNL Adobe Commerce Optimizer]個客戶預設啟用。 |
| 語意提升 | 套用的提升功能可優先處理排名中語義相關的結果。 |
| 相似度臨界值 | 語意相符的最低相似度分數（百分比）。 較低的值有利於召回；較高的值有利於精確度。 |
| 模糊搜尋 | 當&#x200B;**在**&#x200B;時，搜尋會尋找接近相符的查詢（例如，次要變數）。 |
| 模糊搜尋相似度臨界值 | 必須符合最小相似性（百分比）模糊相符才能顯示在結果中。 |

>[!ENDTABS]
