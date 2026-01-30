---
title: Adobe Commerce SaaS與PaaS的比較
description: 比較Adobe Commerce SaaS與PaaS模型，判斷符合您業務需求的最佳實作方法。
feature: App Builder, GraphQL, Integration, Saas
role: Developer, Admin, Leader
level: Intermediate
exl-id: c8c9a0b4-f47c-46ec-bc9d-39dee9641f59
source-git-commit: 5e4481dfd7259a07bda58a1e945b086e9f1c1805
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 0%

---

# 功能比較

Adobe Commerce提供三種部署模式：

- 僅[!BADGE SaaS]{type=Positive url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案(Adobe管理的SaaS基礎結構)。"} [Adobe Commerce as a Cloud Service](overview.md) (SaaS)
- 僅[!BADGE PaaS]{type=Informative url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案(Adobe管理的PaaS基礎結構)和內部部署專案的Adobe Commerce 。"} [雲端上的Adobe Commerce](https://experienceleague.adobe.com/zh-hant/docs/commerce-on-cloud/user-guide/overview) (PaaS)
- [Adobe Commerce](https://experienceleague.adobe.com/zh-hant/docs/commerce-operations/installation-guide/overview) （內部部署）

這項比較著重於軟體即服務(SaaS)和平台即服務(PaaS)模式之間的差異。 這些模型提供不同等級的自訂性、擴充性，以及對Commerce實作的控制。

>[!NOTE]
>
>內部部署模型與PaaS模型具有類似功能，因此這項比較也適用於考量SaaS與內部部署實作的情況。

## 商店管理功能

[Commerce管理UI](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/systems/guide-overview)是存取功能的主要介面，可管理後端商店作業、庫存、定價、促銷和客戶互動。 但是，[!DNL Adobe Commerce as a Cloud Service]提供獨特的解決方案，取代[!DNL Adobe Commerce on Cloud]和內部部署專案中某些已知的功能。

下表說明[!DNL Adobe Commerce as a Cloud Service]中可用的功能和取代解決方案：

<table>
    <thead>
        <tr>
            <th>功能</th>
            <th>Adobe Commerce PaaS模型[!BADGE PaaS only]{type=Informative url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案(Adobe管理的PaaS基礎結構)和內部部署專案。"}</th>
            <th>SaaS模型[!BADGE SaaS only]{type=Positive url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案(Adobe管理的SaaS基礎結構)。"}</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>數位資產管理</td>
            <td><a href="https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/content-design/wysiwyg/gallery/media-gallery-asset-management">媒體集</a></td>
            <td><a href="../aem-assets-integration/overview.md">產品視覺效果</a></td>
        </tr>
        <tr>
            <td>內容管理</td>
            <td><a href="https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/content-design/guide-overview">內容管理系統(CMS)</a>，<a href="https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/page-builder/guide-overview">頁面產生器</a>，<a href="https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/marketing/seo/url-rewrites/url-rewrite">URL重寫</a></td>
            <td><a href="https://experienceleague.adobe.com/developer/commerce/storefront/merchants/get-started/?lang=zh-Hant">店面建置器</a></td>
        </tr>
        <tr>
            <td>目錄銷售</td>
            <td><a href="https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/content-design/staging/content-staging">內容暫存</a>，<a href="https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/marketing/merchandising/visual-merch/visual-merchandiser">Visual Merchandiser</a></td>
            <td><a href="../catalog-service/overview.md">目錄服務</a></td>
        </tr>
        <tr>
            <td>付款</td>
            <td><a href="https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/stores-sales/payments/payments">支付解決方案</a></td>
            <td><a href="../payment-services/guide-overview.md">付款服務</a></td>
        </tr>
        <tr>
            <td>B2B功能</td>
            <td>安裝後即可使用完整的B2B功能</td>
            <td>已預先安裝核心B2B功能<sup>1</sup></td>
        </tr>
        <tr>
            <td>實驗</td>
            <td>適用於特定階層的附加元件</td>
            <td>原生A/B測試可最佳化參與和轉換</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td colspan="3">
                <sup>1</sup>核心<a href="https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/b2b/guide-overview">B2B功能</a> （例如公司管理和報價）可在SaaS中立即使用。 不過，產業專屬的自訂可能需要額外的實施考量因素。
            </td>
        </tr>
    </tfoot>
</table>

## 擴充功能和平台功能

下表比較平台功能與擴充功能，協助您瞭解差異，並在開始實作前決定最適合您業務需求的模式。

<table>
    <thead>
        <tr>
            <th>功能</th>
            <th>Adobe Commerce PaaS模型[!BADGE PaaS only]{type=Informative url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案(Adobe管理的PaaS基礎結構)和內部部署專案。"}</th>
            <th>SaaS模型[!BADGE SaaS only]{type=Positive url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案(Adobe管理的SaaS基礎結構)。"}</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>平台功能</strong></td>
        </tr>
        <tr>
            <td>功能與安全性更新</td>
            <td>需要手動升級和修補。 每年提供6個修補程式版本和1個次要版本。</td>
            <td>Adobe透過無版本SaaS模型自動升級</td>
        </tr>
        <tr>
            <td>託管基礎結構</td>
            <td>單一租使用者</td>
            <td>多租使用者</td>
        </tr>
        <tr>
            <td>效能與擴充性</td>
            <td>可縮放架構的水準自動縮放。 針對網頁層級推出垂直自動縮放，以供所有商家提早存取，包括非縮放架構。</td>
            <td>跨棧疊完整自動縮放的多租使用者雲端原生應用程式</td>
        </tr>
        <tr>
            <td>可觀察性</td>
            <td>[!DNL New Relic] 供客戶監控和管理環境的存取權</td>
            <td>Adobe已管理。 客戶可以將[!DNL OpenTelemetry]用於[!DNL App Builder]應用程式，並將RUM儀表板用於店面。 未包含[!DNL New Relic]授權。 客戶可以設定[!DNL API Mesh]和[!DNL App Builder]將資料傳送至自己的[!DNL New Relic]帳戶。</td>
        </tr>
        <tr>
            <td>CDN</td>
            <td>[!DNL Fastly] 已包含</td>
            <td>完整管理的Edge CDN與Commerce店面緊密結合。 也支援BYO-CDN。</td>
        </tr>
        <tr>
            <td>安全性與合規性</td>
            <td>SOC2、PCI、各託管提供者的ISO認證、HIPAA</td>
            <td>SOC2、PCI、ISO、GDPR。 HIPAA目前無法使用。</td>
        </tr>
        <tr>
            <td>災難回覆與SLA</td>
            <td>99.99%基礎架構、99.9%應用程式(Managed Services)</td>
            <td>99.9% （基礎結構和應用程式），更快的RPO/RTO</td>
        </tr>
        <tr>
            <td>託管區域</td>
            <td>Azure （24個位置）、AWS （22個位置）、GCP （8個位置，非標準）</td>
            <td>全域皆可使用。 如需您所在地區生產環境的詳細資訊，請聯絡您的客戶服務代表。 根據需求推出其他地點。</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Commerce管理員自訂</strong></td>
        </tr>
        <tr>
            <td>Admin Console擴充性</td>
            <td>PHP自訂和主題設定、App Builder擴充性（建議）</td>
            <td>App Builder擴充性</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>擴充性</strong></td>
        </tr>
        <tr>
            <td>擴充性模型</td>
            <td>處理中（PHP自訂）及處理外(建議：API、事件、App Builder)</td>
            <td>僅限處理序外(API、事件、App Builder)</td>
        </tr>
        <tr>
            <td>可延伸的Web API</td>
            <td>原生REST/GraphQL擴充功能和API網狀功能與自訂解析器</td>
            <td>使用自訂解析器的API網格</td>
        </tr>
        <tr>
            <td>資料模型擴充性</td>
            <td>完整的資料模型自訂</td>
            <td>核心和B2B實體的自訂屬性<sup>1</sup></td>
        </tr>
        <tr>
            <td>技術</td>
            <td>CSS、CLI、HTML、JS、PHP、XML</td>
            <td>CSS、CLI、HTML、JS、節點</td>
        </tr>
        <tr>
            <td>應用程式市集</td>
            <td>[!DNL Magento Marketplace]應用程式的[[!DNL Exchange Marketplace]](https://marketplace.magento.com/) （PHP延伸模組）和[[!DNL App Builder]](https://commercemarketplace.adobe.com) （建議使用）</td>
            <td>[!DNL App Builder] 來自[[!DNL Exchange Marketplace]](https://commercemarketplace.adobe.com)的應用程式</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>資料與儲存</strong></td>
        </tr>
        <tr>
            <td>搜尋索引自訂</td>
            <td>原生搜尋自訂</td>
            <td>需要協力廠商解決方案</td>
        </tr>
        <tr>
            <td>自訂電子郵件型別</td>
            <td>完整的電子郵件自訂</td>
            <td>僅限標準電子郵件範本</td>
        </tr>
        <tr>
            <td>自訂資料儲存</td>
            <td>資料庫、檔案、快取、佇列</td>
            <td>App Builder狀態程式庫（僅限檔案）<sup>2 - <a href="https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/storage/database">App Builder的資料庫儲存體</a>目前正在搶先存取。</sup></td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td colspan="3">
                SaaS中的<sup>1</sup>資料模型擴充性支援<a href="https://developer.adobe.com/commerce/webapi/graphql/schema/attributes/mutations/">擴充核心實體</a>，超出產品和客戶範圍，包括B2B實體。 不過，產業特定的資料模型（例如經銷商特定的屬性）可能需要額外的架構考量。
                <br><br>
                <sup>2</sup> Adobe正在積極處理Document DB整合，以滿足SaaS的持續儲存需求。 目前，需要長期資料儲存的實作可能需要布建和維護額外的基礎架構。
            </td>
        </tr>
    </tfoot>
</table>

>[!NOTE]
>
>在考慮移轉至SaaS時，Adobe建議您：
>
>- 儘可能將適當的功能移至「程式外」擴充性。
>- 減少需要轉接的曲面面積。
>- 請考慮使用[!DNL API Mesh]來擴充API功能。
>- 監控Adobe的持續平台演化和新功能發行。
>- 根據可用的擴充性選項評估特定產業資料模型的需求。
>- 請考慮採用由目錄檢視和原則[支援的](../optimizer/setup/catalog-view.md)銷售服務。
