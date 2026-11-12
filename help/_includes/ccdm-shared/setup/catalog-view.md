---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 0%
---
<!--This shared include file contains the conceptual and architecture overview of catalog views for Adobe Merchandising Services-->

目錄檢視會定義使用者端可擷取的產品和定價。 它結合目錄來源、目錄層、原則和價格手冊，以支援不同的品牌、地區、業務單位或管道。

## 什麼是目錄檢視？

目錄檢視會定義產品目錄的組織和顯示方式。 它們作為篩選條件來判斷：

- 根據業務結構（品牌、地區、經銷商）**可看見哪些產品**
- **透過連結的價格手冊顯示哪些價格**
- **如何使用原則（品牌、模型、類別等屬性）篩選產品**
- **使用哪些[目錄來源](/help/optimizer/setup/catalog-sources.md)**，根據地區設定等屬性
- **誰可以透過[目錄保護](private-catalog-view.md)和[受限制的存取金鑰](restricted-access-keys.md)存取檢視的資料**

例如，您可以為以下專案建立個別的目錄檢視：

- 品牌或業務單位
- 地理區域
- 經銷商或合作夥伴管道
- 具有特定定價的客戶區段

## 架構概覽

目錄檢視是Adobe Merchandising Services架構的一部分，可將Adobe Commerce基礎中使用的網站、商店、商店檢視架構更換為更靈活的模型：

![[!DNL Merchandising Services]架構](/help/assets/ccdm-shared/setup/merchandising-svcs-architecture.png)

### 運作方式

**1. 資料擷取**
來自Adobe Commerce後端或其他第三方後端（例如PIM或ERP）和其他系統的目錄資料會擷取到Adobe Merchandising Services資料層中。 每個SKU都包含對應至目錄檢視、原則及區域設定的區域設定資訊與產品屬性。 資料擷取程式取決於來源系統和整合方法：

- **Adobe Commerce後端** — 系統會匯出Commerce目錄摘要，將其對應至資料擷取REST API預期的格式，並將摘要資料同步至Adobe Merchandising Services資料層。 在此模型中，Adobe Commerce會管理初始同步和後續更新。 摘要包含產品、類別、產品屬性、價格和價格手冊。

- **協力廠商後端或來源系統** — 聯結器或整合服務會透過API、事件或匯出摘要從來源擷取目錄資料，然後對應及驗證可撰寫目錄資料模型(CCDM)結構描述，並使用資料擷取REST API將資料同步至Adobe Merchandising Services層。 整合負責初始載入及後續傳送變更。 平台專用聯結器（例如Adobe的[Salesforce Commerce Connector](https://experienceleague.adobe.com/zh-hant/docs/commerce/optimizer/developer/salesforce-connector)）可提供起點。

**2. 統一基礎目錄**
內嵌的資料會在目錄服務資料管道中建立統一的基本目錄。 此單一來源可消除業務單位間的資料重複。

**3. 目錄檢視**
多個目錄檢視代表不同的業務單位（例如，「Texas Retail」、「Texas Retail Secondural」）。 您可以跨目錄檢視共用地區、原則和價格簿，以取得彈性。

**4. 多頻道傳送**
經篩選的目錄資料會傳送至Edge Delivery Services、行銷場所、廣告平台和自訂微型店面等目的地。 如需目錄資料傳遞的詳細資訊，請參閱[開發人員檔案](https://developer.adobe.com/commerce/services/optimizer/)。

當目錄檢視啟用&#x200B;**[!UICONTROL Catalog Protection]**&#x200B;時，傳遞至該目的地需要指派的[受限制存取金鑰](restricted-access-keys.md)中的有效已簽署權杖；未獲授權的請求會遭拒，而非接收目錄資料。

### 主要元件

| 元件 | 用途 | 範例 |
|---|---|---|
| **目錄檢視** | 業務單位或分銷管道 | 經銷商網路、地區商店 |
| **原則** | 根據屬性的產品篩選器 | 品牌、型號、類別 |
| **地區設定** | 語言/地區設定 | en-US、fr-CA、es-MX |
| **價格簿** | 定價結構 | 零售、批發、員工 |
| **受限制的存取金鑰** | 可閘道受保護目錄檢視存取權的已簽署Token認證 | 合作夥伴入口網站金鑰、B2B定價金鑰 |

### 資料流程

1. **擷取** — 從Adobe Commerce後端擷取目錄資料
2. **處理序** — 套用目錄檢視、原則和定價
3. **傳遞** — 將篩選的目錄提供給店面、市場等等

## 主要功能

| 功能 | 優點 |
|---|---|
| **單一基底目錄** | 消除業務單位之間的資料重複 |
| **彈性定價** | 針對不同客戶區段，每個SKU有多個價格簿 |
| **可擴充** | 有效管理200M以上的SKU |
| **多頻道** | 將目錄提供給店面、市集和廣告平台 |
| **即時更新** | 快速更新促銷活動和行銷活動的目錄資料 |
| **私人目錄檢視** | 使用已簽署的權杖驗證將目錄檢視限製為授權使用者端 |

## 使用案例

### 多品牌企業集團

**挑戰**：管理多個品牌、國家/地區和語言<br>
**解決方案**：每個品牌/地區組合的單一目錄包含目錄檢視

### 汽車零件經銷商

**挑戰**： 3,000個產品相同但價格不同的經銷商<br>
**解決方案**：一個目錄，包含經銷商特定的目錄檢視和價格簿

### 多位置retailer

**挑戰**：每個地點的不同定價和詳細目錄<br>
**解決方案**：以位置為基礎的目錄檢視具有區域特定原則

>[!NOTE]
>
>如需目錄資料擷取與傳遞的詳細資訊，請參閱[開發人員檔案](https://developer.adobe.com/commerce/services/optimizer/)。
