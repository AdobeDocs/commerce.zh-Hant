---
title: 銷售規則
description: '[!DNL Adobe Commerce Optimizer]銷售規則結合邏輯與動作，以塑造購物體驗。'
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案(Adobe管理的SaaS基礎結構)。"
source-git-commit: 356b10704c9e7c7329d3e9c0e10baa15d5142ec0
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---

# 銷售規則

銷售規則是指一組規則，這些規則結合邏輯與動作，可影響購物者在您商店中的搜尋體驗。 您可以使用銷售規則來提升、隱藏、釘選或隱藏產品，以即時校正搜尋結果，支援您的業務目標。

每個規則有三個主要元件：

- 條件 — 觸發動作的條件。
- 事件 — 當滿足條件時發生的動作。
- 詳細資訊 — 規則名稱，以及選擇性的時間範圍和說明。

您可以結合多個條件和動作，並排程規則在期間內為作用中。 您也可以設定即使未設定搜尋字詞，也會套用的預設規則。

## 需求

簡單搜尋規則可以有單一條件和單一事件，而複雜規則最多可以有十個條件，以觸發最多25個事件。
規則可以有：

- 最多10個條件
- 最多25個事件

查詢文字可以包含：

- 英數字元（字母和數字）
- 大小寫字元。 將忽略大小寫。

## 邏輯運運算元

邏輯運運算元`AND`和`OR`結合兩個條件並傳回不同的結果。 在具有多個條件的規則中使用的所有邏輯運運算元都是相同的。 無法在相同規則中同時使用`AND`和`OR`。

### 比對運運算元

Match運運算元`All`和`Any`決定用來聯結規則中多個條件的邏輯運運算元，而且可用來變更現有的運運算元。

- `All` — 使用`AND`邏輯運運算元聯結多個條件。 使用`All` Match運運算元的規則只能有一個`Search query is`條件。
- `Any` — 使用`OR`邏輯運運算元聯結多個條件。

構成複雜規則時，可以協助您以縮排寫出規則，以描述傳回想要達到的結果所需的條件、關聯事件和產品名稱或SKU。 然後，建立規則並測試結果。

## 預設規則

您可以設定預設規則，此規則在沒有提供搜尋字詞或無法套用其他搜尋規則時套用。 如果您將預設規則設為「最常購買」，則所有查詢都會預設為該排名型別，除非以更具體的搜尋字詞超越。 預設規則無法設定搜尋字詞。

## 多個規則的優先順序

一次只對一個搜尋字詞套用一個搜尋規則。
如果發現多個規則適用於搜尋片語，則會套用所有這些規則。 如果兩個規則（`rule 1`會增加SKU1，但`rule 2`會隱藏相同的SKU）之間發生衝突，則優先使用最近套用的規則(`rule 2`)。

- 規則會依「上次修改」時間戳記排序。 最近修改的規則會依時間戳記順序先套用，之後則套用較舊的規則。
- `query is`條件優先於其他條件。 如果較新的規則包含`query contains`條件，但較舊的規則有`query is`條件，則套用`query is`規則。

### 店面請求

如果包含`query is`條件的作用中規則符合搜尋字詞，則會套用該規則。 如果有多個具有`query is`條件的相符規則，則會套用最近更新的作用中規則。
否則，會套用最近更新的使用中規則。

### 預覽請求

在[!DNL Adobe Commerce Optimizer]中提出的要求運作方式略有不同。 預覽[!DNL Adobe Commerce Optimizer]時，會套用所有規則，包括已到期和已排程的規則。

- 如果正在預覽的規則具有`query is`條件，則會套用它。
- 如果正在預覽的規則沒有`query is`條件，但找到具有`query is`條件的後續作用中相符規則，則會套用`query is`規則。
- 如果正在預覽的規則沒有`query is`條件，而且找不到具有`query is`條件的其他規則，則會套用正在預覽的規則。
