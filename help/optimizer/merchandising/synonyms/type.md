---
title: 同義字型別
description: 瞭解 [!DNL Adobe Commerce Optimizer]中不同型別的同義字。
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案(Adobe管理的SaaS基礎結構)。"
source-git-commit: 3131cc27a25d1bf958071b973f1d4bf1a68be152
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# 同義字的型別

單向和雙向同義字會擴展關鍵字的定義。 有些可與關鍵字互換，有些則代表關鍵字的子集。

## 雙向

雙向同義字具有相同涵義，並傳回相同的搜尋結果。 在下列範例中，以粗體顯示的第一個字是目錄中所使用的關鍵字，後面跟著與原始關鍵字具有相同含義的字詞。 您可以為相同關鍵字建立一對簡單的雙向同義字，或是多個雙向同義字的鏈結。

**夾克** ![雙向選擇器](../../assets/btn-two-way.png)外套
**褲子** ![雙向選擇器](../../assets/btn-two-way.png)短褲![雙向選擇器](../../assets/btn-two-way.png)褲子

## 單向

單向同義字是關鍵字的子集，但具有更明確的含義。 例如，羊毛衫和短褲都是短褲，但並非所有短褲都是羊毛衫或短褲。 搜尋短褲包括卡布衫和短褲。 不過，搜尋短褲不會傳回Capris。

**運動衫** ![單向選擇器](../../assets/btn-one-way.png)連帽衫
**褲子** ![單向選擇器](../../assets/btn-one-way.png)卡普里斯![多個單向選擇器](../../assets/btn-multiple-one-way.png)小腿長褲![多個單向選擇器](../../assets/btn-multiple-one-way.png)兜售推手

## 多字同義字行為

對於多字同義字，[!DNL Adobe Commerce Optimizer]會將該同義字視為片語。 例如，若您建立雙向同義字&#x200B;**餐桌** ![雙向選擇器](../../assets/btn-two-way.png) **餐桌** ![雙向選擇器](../../assets/btn-two-way.png) **餐桌**，則[!DNL Adobe Commerce Optimizer]會搜尋所有設定為可搜尋的欄位，以尋找&#x200B;**餐桌**&#x200B;或&#x200B;**餐桌**&#x200B;或&#x200B;**餐桌**&#x200B;的出現位置。

如果未建立同義字，且購物者搜尋&#x200B;**kitchen table**，則[!DNL Adobe Commerce Optimizer]會在可搜尋欄位中的任何位置尋找字詞，甚至跨不同的欄位，例如名稱欄位中的&#x200B;**table**&#x200B;和中繼關鍵字中的&#x200B;**kitchen**。

建立同義字後，搜尋行為會變更，以尋找確切的片語&#x200B;**廚房表**。 這樣可能會減少結果的數量，因為系統只會顯示含有精確片語的產品。

如果您想要像之前一樣分別搜尋字詞，您可以[建立支援票證](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide)。 如果有足夠的需求，[!DNL Adobe Commerce Optimizer]將會考慮在未來版本中將此功能新增至產品。
