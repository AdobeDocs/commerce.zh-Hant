---
title: SaaS價格索引
description: 使用SaaS價格索引來改善效能
autotag-review: '2026-06-17T15:08:59.000Z'
seo-title: Adobe SaaS Price Indexing
seo-description: Price indexing give performance improvements using SaaS infrastructure
exl-id: d1bf3879-3e86-4665-a55c-494963c87f90
TQID: https://experienceleague.adobe.com/dfZjgp5wR6H4c7WkNNhjLYUgKNTPIqPWxKiShlTU1yA
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
last-update: 2026-07-29
source-git-commit: 7ce47d7abf7519a7e3ecd436faabf4089005cd63
workflow-type: tm+mt
source-wordcount: 491
ht-degree: 0%

---

# SaaS價格索引

SaaS定價索引可藉由將資源密集的作業（例如索引和價格計算）從Commerce應用程式解除安裝到Adobe的雲端基礎架構，以最佳化網站效能。 此方式可讓商戶快速擴充資源，以加快價格指數化時間，並更快速地提供店面價格更新和連線Commerce服務。

下圖顯示當Commerce使用Commerce應用程式中包含的[價格索引](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers)程式時，指向SaaS服務的索引資料流程：

![預設資料流程](assets/old_way.png)

啟用SaaS價格索引後，資料流程會變更。 使用[Commerce SaaS資料匯出](../data-export/sync-overview.md)執行價格索引。

![SaaS價格索引資料流程](assets/new_way.png)

所有商戶都可以從使用SaaS價格索引中受益，但擁有以下特性專案的商戶可獲得最大的收益：

* **不變價格變更** — 需要重複變更價格以符合策略性目標（例如頻繁促銷、季節性折扣或存貨減價）的商家。
* **多個網站和/或客戶群組** — 跨多個網站（網域/品牌）和/或客戶群組共用產品目錄的商家。
* **跨網站或客戶群組的許多獨特價格** — 具有廣泛共用產品目錄的商家，其中包含跨網站或客戶群組的獨特價格。 例如B2B商傢俱有預先議價的價格，或品牌具有不同的定價策略。

## 使用SaaS價格索引

安裝Adobe Commerce Services時，會自動啟用SaaS價格索引。 它支援所有內建Adobe Commerce產品型別的價格計算。

### 需求

* [Adobe Commerce](https://business.adobe.com/products/magento/magento-commerce.html) 2.4.4+。 如需詳細資訊，請參閱[系統需求](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/system-requirements){target="_blank"}。

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

## 監視同步處理進度

{{$include /help/_includes/data-export/verify-commerce-service-data-sync.md}}

必要時使用[Commerce CLI](../data-export/data-export-cli-commands.md)手動重新同步摘要。 如需重新同步選項及其他疑難排解步驟，請參閱&#x200B;_SaaS Data Export Guide_&#x200B;中的[Manage synchronization](../data-export/data-sync-manage.md)。

>[!NOTE]
>
>若要在Commerce雲端或內部部署的Commerce管理員中無法使用資料摘要同步狀態頁面時將其啟用，請依照[擴充功能安裝指示](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status#install-the-extension)操作。

## 自訂產品型別的價格

自訂產品型別（例如，基本、特殊、群組和目錄規則價格）支援價格計算。

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
