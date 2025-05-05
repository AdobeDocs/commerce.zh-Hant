---
title: 入門
description: 瞭解 [!DNL Product Recommendations]中的需求與支援平台。
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---

# 入門

[!DNL Product Recommendations]的上線流程需要存取伺服器的命令列，且包含下列步驟。 如果您不熟悉如何使用命令列，請向開發人員或系統整合商尋求協助。

- [實作工作流程](implementation-workflow.md)
- [安裝與設定](install-configure.md)
- [設定](settings.md)
- [驗證](verify.md)
- [中繼環境](staging-environment.md)

## 需求

- Adobe Commerce 2.4.4+
- PHP 8.1、8.2
- Composer 2

### 支援平台

- Adobe Commerce內部部署(EE) ：2.4.4+
- 雲端上的Adobe Commerce (ECE) ： 2.4.4+

## 端點

[!DNL Product Recommendations]透過`https://catalog-service.adobe.io/graphql`的端點通訊。

### 頁面產生器支援

[!DNL Product Recommendations]可以新增到頁面作為頁面產生器內容型別。 若要將頁面產生器支援新增至產品建議，請參閱[安裝與設定](install-configure.md)。

請參閱[[!DNL Page Builder] 整合](page-builder.md)，瞭解如何將[!DNL Product Recommendations]新增至[!DNL Page Builder]內容的指示。

### SaaS價格索引

產品推薦客戶可以使用[SaaS價格索引](../price-index/price-indexing.md)，提供更快的價格變更更新和同步化時間。

### B2B支援 {#b2bsupport}

B2B店面通常需要複雜的邏輯，這些邏輯會指定每個購物者或客戶群組的產品可見度和價格。 [!DNL Product Recommendations]現在[支援](release-notes.md)此功能，接受[類別許可權](https://experienceleague.adobe.com/docs/commerce-admin/catalog/categories/category-permissions.html?lang=zh-Hant)、[共用目錄](https://experienceleague.adobe.com/docs/commerce-admin/b2b/shared-catalogs/catalog-shared.html?lang=zh-Hant)和[客戶群組特定定價](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html?lang=zh-Hant)。 例如，如果您隱藏零售客戶區段中的某些類別，則該區段中的購物者不會看到這些類別中產品的建議。 此外，當您為特定客戶群組和公司定義共用目錄時，這些購物者只會看到他們可存取之產品的建議。 所有建議產品都會根據每位購物者的客戶群組，反映正確的客戶群組特定價格。

>[!NOTE]
>
>商戶可以使用[目錄服務](../catalog-service/overview.md)店面API來自訂和擴充Widget或店面元素，但任何自訂都超出了Adobe支援團隊的範圍。
