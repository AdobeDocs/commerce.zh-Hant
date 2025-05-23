---
title: 篩選產品
description: 定義包含或排除不將產品用作建議的條件。
exl-id: 140bf047-4f6a-48da-b536-d96e78ae3d17
source-git-commit: 59aa4ae67a1a8a853b72d78cd65a6cc44a6bc662
workflow-type: tm+mt
source-wordcount: '800'
ht-degree: 0%

---

# 篩選產品

Adobe Commerce會自動將無法設定的預設篩選器套用至建議單位。 如果您將多個建議單位部署至頁面，Adobe Commerce會篩選掉單位中重複的任何產品。 系統只會使用重複產品的第一次參考，以便給其他建議的產品騰出空間。 Adobe Commerce也會篩選掉任何先前購買過的產品和購物車中的產品。

當您[建立](create.md)建議單位時，您可以定義篩選器來控制哪些產品可以顯示在建議中。 這些篩選器是根據您定義的一組包含或排除條件。 只有符合所有包含條件的產品才會出現在建議中。 不建議使用符合任何排除條件的產品。

您可以設定多個篩選器，並只啟用您想要的篩選器，方法是選取每個篩選器頁面上的切換按鈕。 這可讓您建立篩選草稿以供日後使用。 每個標籤上會顯示已啟用的篩選器的數目。

## 條件

條件可以是靜態或動態。

- 靜態條件會使用現有的產品屬性來決定哪些產品可以出現在單位中。 例如，您可以指定只有價格超過$25的庫存產品才會出現在單位中。 靜態條件適用於所有頁面型別。

- 一個動態條件可關閉購物者目前的內容，例如目前檢視的類別或產品。 例如，建立要在產品詳細資料頁面上部署的產品建議時，您可以建立條件，以僅建議目前檢視之產品相對價格範圍內的產品。 除了首頁之外，動態條件可用於每個頁面型別，也可用於搭配Page Builder放置且具有建議的頁面。

### 邏輯運運算元

邏輯運運算元`AND`和`OR`用於聯結多個條件。 如果同時使用包含和排除篩選器，系統會先評估包含專案，以判斷所有可能的建議產品，然後從清單中移除符合任何排除篩選器的產品。

- `AND` — 加入兩個包含篩選條件
- `OR` — 加入兩個排除篩選條件

>[!NOTE]
>
> 包含和排除篩選器會取代`magento/product-recommendations`模組3.2.2版及更新版本中的舊版類別排除。 請參閱[發行說明](release-notes.md)以進一步瞭解Adobe Commerce發行版本。

## 篩選器型別 {#filtertypes}

![篩選器](assets/rec-conditions.png)

### 類別

僅[!BADGE 個PaaS]{type=Informative url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案(Adobe管理的PaaS基礎結構)和內部部署專案的Adobe Commerce 。"}

根據產品類別來篩選產品。 類別篩選器使用直接類別指派及其子類別。 例如，啟用類別`Gear`的排除條件會排除指派給`Gear`的產品及其所有子類別，例如`Gear/Bags`或`Gear/Fitness Equipment`。 這同樣適用於類別上的包含篩選器。 例如，啟用類別`Gear`的包含條件，會包含指派給`Gear`的產品及其所有子類別，例如`Gear/Bags`或`Gear/Fitness Equipment`。

類別欄位會顯示屬於目前商店的類別。

>[!NOTE]
>
>對於B2B商家，類別篩選器會遵守您已設定的任何[客戶特定產品類別](https://experienceleague.adobe.com/docs/commerce-admin/catalog/categories/category-permissions.html?lang=zh-Hant)。

當您將建議部署至頁面型別時，Adobe Commerce建議您使用以下類別篩選設定：

| 頁面 | 篩選依據 |
|---|---|
| 首頁 | 不要篩選產品。 |
| 類別 | 篩選特定類別中的產品。 |
| 產品詳細資料 | 篩選相同類別中的產品。 |
| 購物車 | 篩選購物車中的產品類別。 |
| 訂單確認 | 篩選購買的產品類別。 |

### 產品

產品篩選器會指定哪些特定產品符合或不符合條件，以便顯示在建議中。 您無法選取已停用或無法個別顯示的產品，因為這些產品永遠無法出現在建議中。

>[!NOTE]
>
>可設定產品的子產品不會顯示在建議單位中，因為這些子產品具有&#x200B;_不個別顯示_&#x200B;的可見性。

### 型別

僅[!BADGE 個PaaS]{type=Informative url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案(Adobe管理的PaaS基礎結構)和內部部署專案的Adobe Commerce 。"}

根據產品型別的篩選器會包含或排除特定型別的所有產品。 支援的型別包括&#x200B;_簡單_、_可設定_、_虛擬_、_可下載_&#x200B;或&#x200B;_禮卡_。 不支援&#x200B;_套件_、_群組_&#x200B;和自訂產品型別。

### 可見度

僅[!BADGE 個PaaS]{type=Informative url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案(Adobe管理的PaaS基礎結構)和內部部署專案的Adobe Commerce 。"}

根據可見度篩選產品，例如： _目錄_、_搜尋_&#x200B;或兩者。

### 價格

根據產品價格的篩選器會使用最終價格來執行比較。 最終價格包含匿名購物者可使用的任何折扣或特殊價格。 針對B2B商家，顯示的價格會反映您已設定的[客戶特定群組價格](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html?lang=zh-Hant)。

### 庫存狀態

下列排除篩選器可用於根據庫存狀態篩選產品：

- 無庫存 — （僅限排除）排除無庫存的產品。
- 庫存低 — （僅供排除）排除庫存低的產品。 低庫存狀態是以[詳細目錄組態](https://experienceleague.adobe.com/docs/commerce-admin/config/catalog/inventory.html?lang=zh-Hant)中的&#x200B;_僅X剩餘Threshold_&#x200B;值為基礎。
