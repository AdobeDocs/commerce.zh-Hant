---
title: 同義字最佳作法
description: 瞭解在存放區中實作同義字的最佳實務。
role: Admin, Developer
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案(Adobe管理的SaaS基礎結構)。"
source-git-commit: 54b300ed89f830c2fe5258ec889302a59decd59f
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# 同義字最佳作法

以下提供建立同義字時的最佳實務清單。

- [!DNL Adobe Commerce Optimizer]預設會管理錯誤拼字。 您可以設定同義字，以納入購物者可能會使用的字詞，這些字詞與您目錄中指定的字詞不同。 您不想因為某人正在尋找「沙發」，而您的產品卻被列為「沙發」而失去銷售機會。 您可以輸入客戶可能會用來尋找您的產品的所有可能字詞，以擷取廣泛的搜尋字詞。 您可以[將同義字設定為單向或雙向](add.md#step-2-define-the-synonym-by-type)以改善結果。

- 將品牌名稱和縮寫對應至其全名，例如「HP」對應至「Hewlett-Packard」，以及常用產品暱稱，例如「iPhone」對應至「Apple iPhone」。

- 加入特定產業的行話和購物者可互換使用的術語，例如「運動鞋」和「跑鞋」。

- 根據新的搜尋趨勢、產品新增和購物者行為，定期更新同義字清單。

- 分析搜尋結果和購物者回饋，以測試同義字對應的有效性。 調整對應以改善正確性和關聯性。

- 避免使用停用詞，因為它們不會讓同義字更有意義，但會增加必須處理的資料量。 [!DNL Adobe Commerce Optimizer]會從同義字中篩選出常用英文「停用詞」，例如：

  a、an、and、are、as、at、be、but、by、for、if、in、into、is、it、no、not、of、on、or、such、that、the、their、then、there、these、they、this、to、was、will、with

- 不需要將單字的單數與複數形式都定義為同義字。 如果您的目錄中有單數與複數混合的詞語，搜尋會尋找正確的產品組合。 例如，如果您在產品名稱中使用「pant」一詞，而購物者搜尋「pants」，則會傳回正確的產品組合，並提供單一單詞「pant」作為建議。 單詞「pant」通常用於時尚產業，有時也用於零售業，儘管複數形式的「pants」在某些領域更常使用。 （技術上來說，「褲子」一詞是指服裝中遮住一條腿的部分，因此您需要用一條褲子遮住兩條腿。）

- 與目錄中術語的使用方式一致。 請記住，使用方式上可能有所地區差異，有時會產業內部有所差異。
