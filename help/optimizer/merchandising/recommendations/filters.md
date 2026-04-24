---
title: 建議篩選器
description: 瞭解如何使用篩選器來控制哪些產品出現在 [!DNL Adobe Commerce Optimizer] 建議中。
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和 [!DNL Adobe Commerce Optimizer] 專案（Adobe管理的SaaS基礎結構）。"
exl-id: f6100538-23c0-4e90-9834-a895d4707282
source-git-commit: ba445bf33ec9334c853245fce125af12cd244367
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 0%

---

# 篩選產品

[!DNL Adobe Commerce Optimizer]會自動將無法設定的預設篩選器套用至建議單位。 如果您將多個建議單位部署至一個頁面，[!DNL Adobe Commerce Optimizer]會篩選掉單位中重複的任何產品。 系統只會使用重複產品的第一次參考，以便給其他建議的產品騰出空間。 [!DNL Adobe Commerce Optimizer]也會篩選掉任何先前購買過的產品以及購物車中的產品。

當您[建立](create.md)建議單位時，您可以定義篩選器來控制哪些產品可以顯示在建議中。 這些篩選器是根據您定義的一組包含或排除條件。 只有符合所有包含條件的產品才會出現在建議中。 不建議使用符合任何排除條件的產品。

您可以設定多個篩選器，並只啟用您想要的篩選器，方法是選取每個篩選器頁面上的切換按鈕。 這可讓您建立篩選草稿以供日後使用。 每個標籤上會顯示已啟用的篩選器的數目。

## 條件

條件可以是靜態或動態。

- 靜態條件會使用現有的產品屬性來決定哪些產品可以出現在單位中。 例如，您可以指定只有價格超過$25的庫存產品才會出現在單位中。

- 一個動態條件可關閉購物者目前的內容，例如目前檢視的類別或產品。 例如，建立要在產品詳細資料頁面上部署的產品建議時，您可以建立條件，以僅建議目前檢視之產品相對價格範圍內的產品。

### 邏輯運運算元

邏輯運運算元`AND`和`OR`用於聯結多個條件。 如果同時使用包含和排除篩選器，系統會先評估包含專案，以判斷所有可能的建議產品，然後從清單中移除符合任何排除篩選器的產品。

- `AND` — 加入兩個包含篩選條件
- `OR` — 加入兩個排除篩選條件

## 篩選器型別

每種篩選型別都以目錄的不同層面為目標，例如產品和價格，因此您可以縮小或擴大哪些產品符合單位條件。 選擇符合銷售目標的型別，然後視需要結合包含和排除條件；以下子章節說明每個型別的行為方式以及[!DNL Adobe Commerce Optimizer]如何套用它。

>[!NOTE]
>
>只能建議符合&#x200B;**包含**&#x200B;篩選器的產品，而符合&#x200B;**排除**&#x200B;篩選器的任何產品都會被移除。

### 價格

>[!IMPORTANT]
>
>以下功能為測試版。

價格篩選會針對店面的&#x200B;**作用中價格簿**，使用每個產品的&#x200B;**最終計算價格**，也就是指派給呈現建議單位的店面的價格。 此值會反映在該價格簿中定義的折扣、促銷及特殊訂價，而不只是清單價格。 評估僅使用店面的價格簿；其他店面或價格簿不適用。 如何使用目錄和[價格簿](../../setup/pricebooks.md)設定來設定價格簿對應到店面。

#### 包含和排除規則如何使用價格

- **包含規則** — 只有最終價格&#x200B;**符合所有**&#x200B;定義的包含條件的產品，才符合資格。 這包含每個啟用的包含篩選器（例如，您的價格範圍加上任何其他包含規則）。
- **排除規則** — 將從建議中移除最終價格&#x200B;**符合任何**&#x200B;定義的排除條件的產品。

**顯示的價格** — 建議單位內產品上顯示的價格與該店面價格簿的&#x200B;**最終價格**&#x200B;相同，因此購物者看到的與篩選所用的值相符。

#### 設定價格篩選

1. 在[建立或編輯](create.md)建議單位時，請開啟&#x200B;**[!UICONTROL Filter products]** （或前往單位工作流程中的&#x200B;_篩選器_&#x200B;步驟）。
1. 選取「**[!UICONTROL Inclusions]**」或「**[!UICONTROL Exclusions]**」標籤，依據您僅允許價格範圍內的產品或封鎖價格範圍內的產品。 每個標籤上的徽章會顯示已啟用多少該型別的篩選器。
1. 在左側的清單中，選取&#x200B;**[!UICONTROL Price]**。
1. 開啟&#x200B;**[!UICONTROL Enable filter]**。

   價格值使用&#x200B;**網站的基本貨幣**，如頁面上所述。

1. 開啟&#x200B;**[!UICONTROL Include products based on]** （在&#x200B;**[!UICONTROL Inclusions]**&#x200B;標籤上）或&#x200B;**[!UICONTROL Exclusions]**&#x200B;標籤上的同等控制項，然後選擇&#x200B;**[!UICONTROL Set price range]**。
1. 使用貨幣符號旁的欄位來設定選用的&#x200B;**[!UICONTROL Min price]**&#x200B;和/或&#x200B;**[!UICONTROL Max price]**。 您可以輸入金額或使用&#x200B;**-**&#x200B;和&#x200B;**+**&#x200B;控制項來調整值。 如果您不需要最小值或最大值，請將繫結保留為空白。 系統會比較範圍與店面有效價格簿中每個產品的最終計算價格。
1. 完成建議單位的設定，然後如您平常一樣儲存或發佈，讓篩選器生效。

![價格篩選器](../../assets/filter-price.png)

### 產品

產品篩選依據&#x200B;**SKU**&#x200B;以個別目錄專案為目標。 您新增一或多個SKU，以僅允許這些產品（**包含**）或封鎖它們（**排除**），使用與[價格篩選器](#price)相同的&#x200B;**[!UICONTROL Filter products]**&#x200B;頁面。 您無法顯示已停用的產品或無法在推薦單位中個別顯示的產品；無論篩選條件為何，這些產品都不會出現在店面上。

#### 設定產品篩選

1. 在[建立或編輯](create.md)建議單位時，請開啟&#x200B;**[!UICONTROL Filter products]** （或前往單位工作流程中的&#x200B;_篩選器_&#x200B;步驟）。
1. 選取&#x200B;**[!UICONTROL Inclusions]**&#x200B;或&#x200B;**[!UICONTROL Exclusions]**&#x200B;索引標籤。 每個標籤上的徽章會顯示已啟用多少該型別的篩選器。
1. 在左側的清單中，選取&#x200B;**[!UICONTROL Product]**。
1. 開啟&#x200B;**[!UICONTROL Enable filter]**。

   右側面板標題會反映索引標籤，例如&#x200B;**[!UICONTROL Product inclusions]**&#x200B;或排除專案的同等專案。

1. 在&#x200B;**[!UICONTROL Product SKU]**&#x200B;中，輸入SKU並按一下&#x200B;**[!UICONTROL Add]**。 重複以上步驟以新增更多SKU。

   在&#x200B;**[!UICONTROL Product SKUs]**&#x200B;底下，每個SKU都會顯示為卸除式標籤。 按一下標籤上的&#x200B;**X**&#x200B;以移除該SKU，或按一下&#x200B;**[!UICONTROL Clear All]**&#x200B;以從清單中移除每個SKU。

1. 完成建議單位的設定，然後如您平常一樣儲存或發佈，讓篩選器生效。

對於&#x200B;**包含專案**，只能建議列出其SKU （且符合您其他已啟用的包含篩選器）的產品。 對於&#x200B;**排除專案**，不建議使用任何SKU已列出的產品，即使在其他情況下它符合資格。

![產品篩選器](../../assets/filter-product.png)

>[!NOTE]
>
>可設定產品的子產品不會顯示在建議單位中，因為這些子產品具有&#x200B;_不個別顯示_&#x200B;的可見性。

<!--
### Attribute

You can filter products based on attribute criteria, including attribute values. Selected values use OR logic to either include or exclude products when any of the specified values are found.
-->
