---
title: 新增同義字
description: 新增 [!DNL Live Search] 同義字以改善搜尋要求的回應。
exl-id: 2dc535ea-35a3-45a8-8171-901005223cc9
source-git-commit: 81bde302463a70e41318b494565694929703dff9
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 0%

---

# 新增同義字

新增您自己的[!DNL Live Search]同義字組織清單，以提高客戶參與度。 [!DNL Live Search]可以管理每個`Data Space ID`最多200個同義字。

![[!DNL Live Search]同義字](assets/synonym-workspace.png)

## 步驟1：新增同義字

1. 在Admin中，前往&#x200B;**行銷** > SEO與搜尋> **[!DNL Live Search]**。
1. 針對多個存放區，將&#x200B;**領域**&#x200B;設定為套用同義字設定的[存放區檢視](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html#scope-settings)。
1. 按一下&#x200B;**同義字**&#x200B;索引標籤。
1. 按一下&#x200B;**新增同義字**&#x200B;按鈕。

## 步驟2：依型別定義同義字

請依照您要建立的[同義字](synonyms-type.md)型別的指示操作。

### 雙向同義字

1. 接受預設的&#x200B;**雙向**&#x200B;選項。

   ![新增雙向同義字](assets/synonym-add-two-way.png)

1. 輸入要比對的&#x200B;**關鍵字**&#x200B;詞語或片語。
1. 輸入您想要新增為關鍵字同義字的&#x200B;**擴增**字詞。 請使用逗號分隔多個詞語。
在此範例中，要比對的關鍵字是「pants」，而擴充辭彙集是「trousers， slacks」。

   ![雙向同義字範例](assets/synonym-add-two-way-example.png)

1. 完成時，按一下&#x200B;**儲存**。
同義字集合會顯示在清單中，每個辭彙之間會有一個雙向箭頭，表示辭彙可以互換。

   ![雙向同義字](assets/synonym-two-way.png)

### 單向同義字

1. 按一下&#x200B;**單向**&#x200B;同義字型別。

   ![新增單向同義字](assets/synonym-add-one-way.png)

1. 輸入&#x200B;**關鍵字**&#x200B;和&#x200B;**擴充**&#x200B;辭彙。 請使用逗號分隔多個詞語。

   ![單向同義字範例](assets/synonym-add-one-way-example.png)

   在此範例中，關鍵字是「pants」，而單向擴充辭彙「capris， pedle-pushers」是「pants」的子集，但具有特定含義。

1. 完成時，按一下&#x200B;**儲存**。
同義字集合出現在清單中，有一個從展開詞指向關鍵字的單向箭頭，指示該詞是關鍵字的子集。 每個擴充詞以加號分隔。

   ![單向同義字](assets/synonym-one-way.png)

## 步驟3：發佈變更

1. 當您的同義字完成時，按一下&#x200B;**發佈變更**。
1. 等候最多2小時，讓您的更新在店面中出現。

## 欄位說明

| 欄位 | 說明 |
|--- |--- |
| [型別](synonyms.md) | 判斷同義字與關鍵字的意義相同，或是關鍵字的子集。 選項：<br />雙向（預設） — 與關鍵字具有相同含義並傳回相同搜尋結果的字詞<br />單向 — 關鍵字的子集的字詞。 單向同義字會傳回特定產品的較窄清單。 |
| 關鍵字 | 通常與目錄中的一系列產品相關聯的字詞。 |
| 擴充 | 與關鍵字具有相同或類似含義的其他詞語。 |
