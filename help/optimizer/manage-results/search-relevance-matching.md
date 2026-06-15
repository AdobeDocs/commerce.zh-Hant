---
title: 搜尋比對和排名
description: 瞭解 [!DNL Adobe Commerce Optimizer] 如何排定精確和接近符合、相同欄位符合和跨欄位符合的優先順序，以及排名如何與搜尋權重、智慧型排名和銷售規則互動。
role: Admin, Leader, User
recommendations: noCatalog
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和 [!DNL Adobe Commerce Optimizer] 專案（Adobe管理的SaaS基礎結構）。"
hide: true
autotag-review: '2026-06-12T19:49:25.241Z'
TQID: 'https://experienceleague.adobe.com/GBfssL1pTVx4FKjsi45mDsTx2XyCr0aViexH3OpPjVo'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
subfeature_v2:
  - id: faf75e43-5608-48b8-8169-3f8a9b8a5caf
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: d378ca77-2da1-4f39-ad92-1917fe974a38
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: 717ecbc9c6aa41f8a504579de8ce55f514cc4307
workflow-type: tm+mt
source-wordcount: 946
ht-degree: 0%

---

# 搜尋比對和排名

>[!IMPORTANT]
>
>下列功能位於[私人測試版](https://experienceleague.adobe.com/en/docs/commerce-operations/release/beta)。

[!DNL Adobe Commerce Optimizer]排名結果，讓購物者能先看到最相關的產品。 此服務對目錄文字&#x200B;**與購物者型別最符合**&#x200B;的產品提供最強勁的提升，然後偏好以有意義的方式一起出現查詢字詞的符合，最後包括更廣泛的符合（包括支援自動完成樣式比對的行為）。

## 相符專案的優先順序如何

在高層次，相關性使用三個相符強度的層（除了下面描述的其他評分因素外）：

1. **精確和接近的片語相符** — 完整搜尋片語符合目錄文字，或是在正規化後接近的相符專案，例如字乾等（例如，單數與複數形式會解析成相同的根）。 這些相符專案會獲得最高的相關性提升。

1. **相同欄位中的所有字詞** — 查詢中的每個字詞都出現在可搜尋的屬性中（例如，產品&#x200B;**名稱**&#x200B;中的`red`和`pants`）。 此層會獲得次高的提升。

1. **跨不同欄位的字詞** — 查詢字詞出現在不同的可搜尋屬性中（例如，**色彩**&#x200B;中的`red`和&#x200B;**名稱**&#x200B;中的`pants`）。 這是最廣泛的相符層，關聯性提升最低。 它也可以符合自動完成所使用的部分查詢 — 例如，當購物者於完成`pants`前輸入`red pan`時。 如需德文目錄，請參閱[Decompounding (German)](#decompounding-german)。

### 範例

針對`red pants`之類的查詢：

- 包含精確片語&#x200B;**紅色褲子** （或相近變體）的產品排名&#x200B;**前**。
- **紅色**&#x200B;和&#x200B;**褲子**&#x200B;出現在&#x200B;**相同欄位** （例如，**名稱**）排名下方的產品。
- 字詞出現在&#x200B;**不同欄位** （例如，**色彩**&#x200B;和&#x200B;**名稱**）的產品如下。

### 分解符號（德文） {#decompounding-german}

德文目錄使用許多複合字詞。 例如，**spulbecken**&#x200B;和&#x200B;**spul becken**&#x200B;可以分解成&#x200B;**spul**&#x200B;和&#x200B;**beck** （字串後）等權杖，所以搜尋&#x200B;**spul becken**&#x200B;的購物者仍然可以找到&#x200B;**Spulbecken**。 在這個圖層中，複合字詞的取消複合子字必須出現在相同欄位中。 其他查詢詞在不同的欄位中可能相符。

此&#x200B;**AND**&#x200B;需求篩選器與只有一個子字的不相關相符。 例如，當只有部份複合物符合時，搜尋&#x200B;**Brauseschlauch**&#x200B;不再傳回&#x200B;**Schlauchstuck**。 對&#x200B;**spulbecken**&#x200B;的搜尋仍可符合&#x200B;**spulbeckventil**，因為較長的字包含所有預期的語彙基元。

>[!NOTE]
>
>精確和接近片語比對及相同欄位比對會使用上述規則，而不會解壓縮。

#### 範例

搜尋片語（如`Brauseschlauch chrom`）：

- **精確和接近的字片語相符** — 尋找完整字詞&#x200B;**brauseschlauch chrom**&#x200B;做為輸入字詞，但不進行解壓縮（字詞串仍然適用）。
- **相同欄位中的所有字詞** — 在&#x200B;**same**&#x200B;可搜尋屬性中尋找&#x200B;**brauseschlauch**&#x200B;和&#x200B;**chrom**，仍然沒有解壓縮（例如，兩者都在&#x200B;**name**&#x200B;中）。
- 跨不同欄位的&#x200B;**字** — 將&#x200B;**Brauseschlauch**&#x200B;解複合成&#x200B;**Brause**&#x200B;和&#x200B;**Schlauch**。 這些Token必須出現在&#x200B;**相同**&#x200B;欄位中（不一定是相鄰的片語）。 **chrom**&#x200B;可在&#x200B;**不同**&#x200B;欄位中符合（例如，**name**，**chrom** **color**&#x200B;中的&#x200B;**brause**&#x200B;和&#x200B;**schlauch**）。

在[設定](../settings.md)中的[語言](../settings.md#language)索引標籤上將&#x200B;**語言**&#x200B;設定為&#x200B;**德文**，因此會套用分解規則。 在生產環境中啟用變更之前，請先在預備店面驗證高價值德文查詢。

分解是以規則為基礎，可以在此圖層新增邊緣大小寫。 如果字典中遺漏子字，則代碼化可能會不完整，並傳回比您預期更廣的相符專案，例如，**gaszahler**&#x200B;中遺漏的&#x200B;**gas**&#x200B;可能只產生&#x200B;**zahl**，或是&#x200B;**thermostat**&#x200B;中遺漏的&#x200B;**stat**。 字乾也會產生未預期的根（例如，**schrauber**&#x200B;字乾至&#x200B;**schraub**，或&#x200B;**schelle**&#x200B;至&#x200B;**schell**）。 Adobe會針對已識別問題的已知案例更新字典和詞幹覆寫。

## 其他哪些會影響排名

關聯性並非僅由片語比對決定。 數個訊號會互動：

- 從&#x200B;**精確/近**&#x200B;個字詞比對增加
- 當&#x200B;**所有查詢詞**&#x200B;出現在&#x200B;**相同**&#x200B;欄位中時提升
- **智慧型排名** （啟用時），將文字關聯性與行為訊號融合在一起 — 請參閱[智慧型排名計分的運作方式](../merchandising/rules/add.md#how-intelligent-ranking-scoring-works-search)
- **[搜尋每個屬性的權重](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search-results)**&#x200B;以及其他文字關聯性因素（例如，詞匯出現的頻率以及名稱或描述長度）。 在&#x200B;*設定*&#x200B;中，設定哪些屬性參與關鍵字搜尋，以及它們的相對&#x200B;**[關鍵字搜尋權重](../settings.md)**。
- **[銷售規則](../merchandising/rules/overview.md)**，例如pin、boost和bury

由於這些訊號會互動，只有在最廣泛的層級符合的產品有時可以排在較緊的詞語符合項之上 — 例如，當&#x200B;**搜尋權重**&#x200B;或高權重欄位中的詞語頻率超過其他位置較弱的詞語符合項時。

**範例：**&#x200B;如果&#x200B;**紅色褲子**&#x200B;在&#x200B;**描述**&#x200B;中顯示為具有&#x200B;**搜尋權重= 1**&#x200B;的片語，但&#x200B;**紅色**&#x200B;和&#x200B;**褲子**&#x200B;分別出現在&#x200B;**名稱**&#x200B;和&#x200B;**顏色**，具有&#x200B;**搜尋權重= 10**，則&#x200B;**描述**&#x200B;中的片語相符項可能不會超過分割相符項，視整體分數而定。

手動&#x200B;**圖釘**&#x200B;和&#x200B;**bury**&#x200B;規則仍為強式；**提升**&#x200B;規則可能需要調整以克服新片語與相同欄位提升。 變更權重或規則後驗證重要查詢。

### 搜尋權重1和組合索引

以&#x200B;**最小搜尋權數** （權數&#x200B;**1**）和針對特殊比對模式（例如包含或開頭為）設定的&#x200B;**非**&#x200B;設定的屬性，可以在搜尋索引中合併成單一內部欄位(`defaultSearchField`)，以減少欄位對應負荷。 將其視為&#x200B;**相同欄位**&#x200B;相符的可搜尋表面：僅登陸在這些合併的低權重欄位中的權杖會一起評估，而不是作為個別的個別屬性欄位。 Adobe可能會隨著比對的發展來調整此最佳化。

## 相關主題

- [設定](../settings.md)
- [搜尋績效](search-performance.md)
- [銷售規則概觀](../merchandising/rules/overview.md)
- [新增搜尋規則](../merchandising/rules/add.md)
- [同義字概觀](../merchandising/synonyms/overview.md)
