---
title: SaaS價格索引
description: 使用SaaS價格索引來改善效能
seo-title: Adobe SaaS Price Indexing
seo-description: Price indexing give performance improvements using SaaS infrastructure
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%

---

# SaaS價格索引

SaaS定價索引可藉由將資源密集的作業（例如索引和價格計算）從Commerce應用程式解除安裝到Adobe的雲端基礎架構，以最佳化網站效能。 此方式可讓商家快速擴充資源，以加快價格指數化時間，並更快速地提供店面價格更新和連線Commerce服務。

下圖顯示當Commerce使用Commerce應用程式中包含的[價格索引](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers)程式時，指向SaaS服務的索引資料流程：

![預設資料流程](assets/old_way.png)

啟用SaaS價格索引後，資料流程會變更。 使用[Commerce SaaS資料匯出](../data-export/data-synchronization.md)執行價格索引。

![SaaS價格索引資料流程](assets/new_way.png)

所有商戶都可以從使用SaaS價格索引中受益，但擁有以下特性專案的商戶可獲得最大的收益：

* **價格持續變動**&#x200B;需要重複變更價格以符合策略性目標的商家，例如頻繁促銷活動、季節性折扣或存貨減價。
* **多個網站和/或客戶群組** — 跨多個網站（網域/品牌）和/或客戶群組共用產品目錄的商家。
* **多個網站或客戶群組的許多不重複價格** — 具有廣泛共用產品目錄的商家，其中包含多個網站或客戶群組的不重複價格。 例如B2B商傢俱有預先議價的價格，或品牌具有不同的定價策略。

## 使用SaaS價格索引

安裝Adobe Commerce Services時，會自動啟用SaaS價格索引。 它支援所有內建Adobe Commerce產品型別的價格計算。

### 需求

* Adobe Commerce 2.4.4+

### 先決條件

* 下列其中一個Commerce服務必須搭配最新版的Commerce擴充功能安裝：

   * [目錄服務](../catalog-service/overview.md)
   * [即時搜尋](../live-search/overview.md)
   * [產品推薦](../product-recommendations/guide-overview.md)


>[!NOTE]
>
>如有需要，可以使用[目錄配接器](catalog-adapter.md)停用Commerce應用程式中的預設價格索引器。

## 將價格與SaaS價格索引同步

為Adobe Commerce啟用SaaS價格索引後，同步新摘要以更新店面和Commerce Services中的價格：

```bash
bin/magento saas:resync --feed=scopesCustomerGroup
bin/magento saas:resync --feed=scopesWebsite
bin/magento saas:resync --feed=prices
```

### 自訂產品型別的價格

自訂產品型別支援價格計算，例如基本價格、特殊價格、群組價格、目錄規則價格等。

如果您的自訂產品型別使用特定公式來計算最終價格，您可以擴充產品價格摘要的行為。

1. 在`Magento\ProductPriceDataExporter\Model\Provider\ProductPrice`類別上建立外掛程式。

   ```xml
   <config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:noNamespaceSchemaLocation="urn:magento:framework:ObjectManager/etc/config.xsd">
       <type name="Magento\ProductPriceDataExporter\Model\Provider\ProductPrice">
           <plugin name="custom_type_price_feed" type="YourModule\CustomProductType\Plugin\UpdatePriceFromFeed" />
       </type>
   </config>
   ```

1. 使用自訂公式建立方法：

   ```php
   class UpdatePriceFromFeed
   {
       /**
       * @param ProductPrice $subject
       * @param array $result
       * @param array $values
       *
       * @return array
       */
       public function afterGet(ProductPrice $subject, array $result, array $values) : array
       {
           // Override the output $result with your data for the corresponding products (see original method for details) 
           return $result;
       }
   }
   ```

