---
title: 發行說明
description: ' [!DNL Adobe Commerce Optimizer]的最新發行資訊。'
role: Admin, Developer, User, Leader
recommendations: noCatalog
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和 [!DNL Adobe Commerce Optimizer] 專案（Adobe管理的SaaS基礎結構）。"
exl-id: e420d461-9ea2-4e32-aa37-230b14a297d7
source-git-commit: d0967674d05018f13dc6c8a562005d65d44e42ab
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---

# 發行說明

下列發行說明包含[!DNL Adobe Commerce Optimizer]的更新。

## 2026年4月

**發行日期**： 2026年4月7日

>[!BEGINSHADEBOX]

### 目錄規則

銷售規則現在包含[類別規則](./merchandising/rules/add.md)，因此您可以使用與搜尋相同的智慧型排名和手動動作（釘選、提升、隱藏），鎖定一或多個類別並控制類別頁面上的產品順序。

### 價格篩選

建議篩選器現在支援[價格篩選器](./merchandising/recommendations/filters.md#price)，您可以使用它來設定產品的最低與最高價格範圍。

### 其他發行說明

[!DNL Adobe Commerce Optimizer]使用最新版的AEM Assets整合、Commerce Optimizer聯結器及[!DNL Adobe Commerce Storefront]。 使用下列連結檢視每個區域的發行說明：

| 擴充性 | 店面 |
| --- | --- |
| [AEM Assets整合](../aem-assets-integration/release-notes.md)<br>[Commerce Optimizer聯結器](../aco-connector/release-notes.md) | [店面版本資訊](https://experienceleague.adobe.com/developer/commerce/storefront/releases/?lang=zh-Hant)<br>[店面變更記錄檔](https://experienceleague.adobe.com/developer/commerce/storefront/releases/changelog/?lang=zh-Hant) |

>[!ENDSHADEBOX]

## 2026年2月

**發行日期**：2026年2月19日

>[!BEGINSHADEBOX]

新增在您[建立建議單位](./merchandising/recommendations/create.md)或[銷售規則](./merchandising/rules/add.md)時指定目錄檢視的功能。

### 其他發行說明

[!DNL Adobe Commerce Optimizer]使用最新版的AEM Assets整合、Commerce Optimizer聯結器及[!DNL Adobe Commerce Storefront]。 使用下列連結檢視每個區域的發行說明：

| 擴充性 | 店面 |
| --- | --- |
| [AEM Assets整合](../aem-assets-integration/release-notes.md)<br>[Commerce Optimizer聯結器](../aco-connector/release-notes.md) | [店面版本資訊](https://experienceleague.adobe.com/developer/commerce/storefront/releases/?lang=zh-Hant)<br>[店面變更記錄檔](https://experienceleague.adobe.com/developer/commerce/storefront/releases/changelog/?lang=zh-Hant) |

>[!ENDSHADEBOX]

## 2025年12

**發行日期**：2025年12月10日

>[!BEGINSHADEBOX]

### 機會

AI支援的網站最佳化建議現在可透過[Adobe Sites Optimizer整合](./manage-results/opportunities.md)取得。 此功能可協助銷售人員透過自動化偵測和智慧型建議，識別及解決影響商業網站效能的問題。

### 目錄圖層

已新增[目錄層](./setup/catalog-layer.md)，以便在不變更來源資料的情況下修改產品資料，包括層級優先順序管理以及與Adobe Sites Optimizer自動修正功能的整合。

### 其他發行說明

[!DNL Adobe Commerce Optimizer]使用最新版的AEM Assets整合、Commerce Optimizer聯結器及[!DNL Adobe Commerce Storefront]。 使用下列連結檢視每個區域的發行說明：

| 擴充性 | 店面 |
| --- | --- |
| [AEM Assets整合](../aem-assets-integration/release-notes.md)<br>[Commerce Optimizer聯結器](../aco-connector/release-notes.md) | [店面版本資訊](https://experienceleague.adobe.com/developer/commerce/storefront/releases/?lang=zh-Hant)<br>[店面變更記錄檔](https://experienceleague.adobe.com/developer/commerce/storefront/releases/changelog/?lang=zh-Hant) |

>[!ENDSHADEBOX]

## 2025年10

**發行日期**：2025年10月14日

>[!BEGINSHADEBOX]

### Commerce Optimizer Salesforce Commerce聯結器

[!DNL Commerce Optimizer Salesforce Commerce Connector]是新的App Builder整合入門套件，可讓Commerce管理員和開發人員順暢地將Salesforce B2C Commerce目錄資料與[!DNL Commerce Optimizer]連線。<!--COMOPT-536-->

管理員的&#x200B;**：**

* Salesforce中的目錄更新（產品、價格、中繼資料、價目表）會自動與Commerce Optimizer同步，無需手動干預。
* 此整合獨立於Adobe Commerce運作，可降低複雜性和可能的失敗點。
* 管理員可以依賴定期排程更新，以確保Commerce Optimizer中的目錄資料準確，進而改善銷售和產品建議。

開發人員的&#x200B;**：**

* 入門套件提供簡化且可擴充的架構，可將Salesforce目錄資料擷取至SaaS銷售服務。
* 參考實作、設計檔案和程式碼範例可用來加速自訂整合或疑難排解。<!--COMOPT-536-->

### 分層搜尋

* 下列進階搜尋功能的GA版本：使用`startsWith`和`contains`的分層搜尋。 [了解更多](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#layered-search-and-expansion-of-search-types)。

### 類別API

新類別REST API現已推出，可讓管理員和開發人員以程式設計方式建立、更新及管理導覽和產品分組的多個類別樹狀結構。 此API支援全域和通道專屬設定，專為高擴充性而設計，最高可支援10,000個類別樹狀結構和500個類別（每個樹狀結構）。 如需詳細資訊，請參閱[Merchandising Services開發人員指南](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/#categories)中的&#x200B;_類別_。<!--DCAT-2649-->

### 其他發行說明

[!DNL Adobe Commerce Optimizer]使用最新版的AEM Assets整合、Commerce Optimizer聯結器及[!DNL Adobe Commerce Storefront]。 使用下列連結檢視每個區域的發行說明：

| 擴充性 | 店面 |
| --- | --- |
| [AEM Assets整合](../aem-assets-integration/release-notes.md)<br>[Commerce Optimizer聯結器](../aco-connector/release-notes.md) | [店面版本資訊](https://experienceleague.adobe.com/developer/commerce/storefront/releases/?lang=zh-Hant)<br>[店面變更記錄檔](https://experienceleague.adobe.com/developer/commerce/storefront/releases/changelog/?lang=zh-Hant) |

>[!ENDSHADEBOX]

## 2025年8月

**發行日期**： 2025年8月28日

>[!BEGINSHADEBOX]

### 歐盟區域現已推出

現已推出客戶IMS組織的歐盟地區(eu1)支援。 在Cloud Manager中&#x200B;**新增Commerce Optimizer執行個體**&#x200B;時，您現在可以選取&#x200B;**歐盟**&#x200B;作為[地區](./get-started.md#step-1-create-an-instance)。 歐盟區域僅適用於生產環境。

歐盟區域的基本生產URL為：

* 管理員： `https://eu1.admin.commerce.adobe.com`
* REST和GraphQL： `https://eu1.api.commerce.adobe.com`

![建立執行個體](./assets/create-instance.png){width="600" align="center" zoomable="yes"}

### 其他發行說明

[!DNL Adobe Commerce Optimizer]使用最新版的AEM Assets整合、Commerce Optimizer聯結器及[!DNL Adobe Commerce Storefront]。 使用下列連結檢視每個區域的發行說明：

| 擴充性 | 店面 |
| --- | --- |
| [AEM Assets整合](../aem-assets-integration/release-notes.md)<br>[Commerce Optimizer聯結器](../aco-connector/release-notes.md) | [店面版本資訊](https://experienceleague.adobe.com/developer/commerce/storefront/releases/?lang=zh-Hant)<br>[店面變更記錄檔](https://experienceleague.adobe.com/developer/commerce/storefront/releases/changelog/?lang=zh-Hant) |

>[!ENDSHADEBOX]
