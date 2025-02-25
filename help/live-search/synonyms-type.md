---
title: 同義字的型別
description: 單向 [!DNL Live Search] 和雙向同義字會擴展關鍵字的定義。
exl-id: f5522428-c7cc-4627-a09b-d9148918c127
source-git-commit: 81bde302463a70e41318b494565694929703dff9
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 0%

---

# 同義字的型別

單向和雙向同義字會擴展關鍵字的定義。 有些可與關鍵字互換，有些則代表關鍵字的子集。

## 雙向

雙向同義字具有相同涵義，並傳回相同的搜尋結果。 在下列範例中，以粗體顯示的第一個字是目錄中所使用的關鍵字，後面跟著與原始關鍵字具有相同含義的字詞。 您可以為相同關鍵字建立一對簡單的雙向同義字，或是多個雙向同義字的鏈結。

**夾克** ![雙向選擇器](assets/btn-two-way.png)外套
**褲子** ![雙向選擇器](assets/btn-two-way.png)短褲![雙向選擇器](assets/btn-two-way.png)褲子

## 單向

單向同義字是關鍵字的子集，但具有更明確的含義。 例如，羊毛衫和短褲都是短褲，但並非所有短褲都是羊毛衫或短褲。 搜尋短褲包括卡布衫和短褲。 不過，搜尋短褲不會傳回Capris。

**運動衫** ![單向選擇器](assets/btn-one-way.png)連帽衫
**褲子** ![單向選擇器](assets/btn-one-way.png)卡普里斯![多個單向選擇器](assets/btn-multiple-one-way.png)小腿長褲![多個單向選擇器](assets/btn-multiple-one-way.png)兜售推手

## 最佳實務

請牢記以下最佳實務，以充份運用[!DNL Live Search]同義字。

### 避免「停用詞」

[!DNL Live Search]會從同義字中篩選出常用英文「停用詞」，例如：

a、an、and、are、as、at、be、but、by、for、if、in、into、is、it、no、not、of、on、or、such、that、the、their、then、there、these、they、this、to、was、will、with

停用詞不會使同義字更有意義，但會增加必須處理的資料量。

### 使用單數與複數

不需要將單字的單數與複數形式都定義為同義字。 如果您的目錄中有單數與複數混合的詞語，搜尋會尋找正確的產品組合。 例如，如果您在產品名稱中使用「pant」一詞，而購物者搜尋「pants」，則會傳回正確的產品組合，並提供單一單詞「pant」作為建議。 單詞「pant」通常用於時尚產業，有時也用於零售業，儘管複數形式的「pants」在某些領域更常使用。 （技術上來說，「褲子」一詞是指服裝中遮住一條腿的部分，因此您需要用一條褲子遮住兩條腿。）

### 一致性

與目錄中術語的使用方式一致。 請記住，使用方式上可能有所地區差異，有時會產業內部有所差異。

## 多字同義字行為

對於多字同義字，Commerce會將該同義字視為片語。 例如，若您建立雙向同義字&#x200B;**餐桌** ![雙向選擇器](assets/btn-two-way.png) **餐桌** ![雙向選擇器](assets/btn-two-way.png) **餐桌**，則Commerce會搜尋所有設為可搜尋的欄位，以尋找&#x200B;**餐桌**&#x200B;或&#x200B;**餐桌**&#x200B;或&#x200B;**餐桌**&#x200B;的出現位置。

如果未建立同義字，且購物者搜尋&#x200B;**kitchen table**，Commerce會在可搜尋欄位中的任何位置尋找字詞，甚至跨不同的欄位，例如名稱欄位中的&#x200B;**table**&#x200B;和中繼關鍵字中的&#x200B;**kitchen**。

建立同義字後，搜尋行為會變更，以尋找確切的片語&#x200B;**廚房表**。 這樣可能會減少結果的數量，因為系統只會顯示含有精確片語的產品。

如果您想要像之前一樣分別搜尋字詞，您可以[建立支援票證](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide)。 如果有足夠的需求，Commerce會考慮在未來版本中新增此功能至產品。
