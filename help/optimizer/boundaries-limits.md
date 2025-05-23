---
title: 邊界和限制
description: 瞭解 [!DNL Adobe Commerce Optimizer] 的界限和限制，以確保其符合您的業務需求。
role: Admin, Developer
exl-id: 58d94da9-8d48-4513-8b6a-8e8c7c27a2a5
source-git-commit: 149b87fc822e5d07eed36f3d6a38c80e7b493214
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# 邊界和限制

>[!NOTE]
>
>本檔案說明提早存取開發的界限和限制，並未反映可供一般使用的所有功能。

下列專案提供Adobe Commerce Optimizer的邊界和限制。

## 目錄

- 目錄擷取的保證率為：每分鐘1000項產品，每分鐘5000項價格
- 每日產品更新的基礎數量為1,000,000。
- 單一執行個體中允許的SKU總數為250,000。 
- 範圍的最大數量為50。
- 每個產品的變數數量為10,000。
- 產品大小不得超過200kb。

## 價格

- 價格簿的數量上限為1,000。

## 搜尋和店面

- 單一搜尋請求可傳回的產品數量為100個。
- 可篩選屬性的最大數量為200
- 可搜尋屬性的數量上限為200
- 可排序屬性的最大數量為50
- 多面的最大數量為100。 所有Facet都必須是可篩選的屬性。
- 單一Facet cat傳回的選項數上限為100，支援請求可增加該數量。

## 管道和原則

- 每個租使用者的管道數上限為1000。
- 指派給一個管道的政策數量上限為10個。
- 原則中使用的屬性值數量上限為100。 

## 產品探索和建議

- 對於產品探索，不支援基於屬性的銷售和價格設定。
- 對於建議：

   - [!DNL Adobe Commerce Optimizer]支援&#x200B;_最近檢視的_&#x200B;建議型別以便提早存取。
   - 不支援類別或屬性包含或排除專案。
   - 您無法在[!DNL Adobe Commerce Optimizer]中預覽建議。
