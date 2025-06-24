---
title: Adobe Commerce SaaS與PaaS的比較
description: 比較Adobe Commerce SaaS與PaaS模型，判斷符合您業務需求的最佳實作方法。
role: Architect
exl-id: c8c9a0b4-f47c-46ec-bc9d-39dee9641f59
source-git-commit: 0eb74c1e70ac2c7073f8f9387baec4f6d3e90a86
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 0%

---

# 功能比較

Adobe Commerce提供三種部署模式：

- 僅[!BADGE SaaS]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案(Adobe管理的SaaS基礎結構)。"} [Adobe Commerce as a Cloud Service](overview.md) (SaaS)
- 僅[!BADGE PaaS]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案(Adobe管理的PaaS基礎結構)和內部部署專案的Adobe Commerce 。"} [雲端上的Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/overview) (PaaS)
- [Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/overview) （內部部署）

這項比較的重點在於軟體即服務(SaaS)和平台即服務(PaaS)模型之間的差異，這兩種模型提供不同等級的自訂性、擴充性以及商業實作的控制權。

>[!NOTE]
>
>內部部署模型與PaaS模型具有類似功能，因此這項比較也適用於考量SaaS與內部部署實作的情況。

## 商店管理功能

[Commerce管理UI](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/guide-overview)是存取功能的主要介面，可管理後端商店作業、庫存、定價、促銷和客戶互動。 但是，[!DNL Adobe Commerce as a Cloud Service]提供獨特的解決方案，取代了Adobe Commerce雲端和內部部署專案中某些著名的功能。

下表說明[!DNL Adobe Commerce as a Cloud Service]中可用的功能和取代解決方案：

<table>
    <thead>
        <tr>
            <th>Adobe Commerce PaaS模型[!BADGE PaaS only]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案(Adobe管理的PaaS基礎結構)和內部部署專案。"}</th>
            <th>SaaS模型[!BADGE SaaS only]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案(Adobe管理的SaaS基礎結構)。"}</th>
            <th>詳細資料</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/wysiwyg/gallery/media-gallery-asset-management">數位資產管理</a></td>
            <td><a href="../product-visuals/overview.md">產品視覺效果</a></td>
            <td>健全的數位資產管理(DAM)系統與Adobe Experience Manager整合，用於管理多媒體內容。 或者，預設的數位檔案和資產管理功能提供儲存和管理數位資產的基本資產管理工具。</td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/guide-overview">內容管理系統(CMS)</a></td>
            <td rowspan="3"><a href="https://experienceleague.adobe.com/developer/commerce/storefront/merchants/get-started/">店面建置器</a></td>
            <td rowspan="3">CMS可讓使用者使用檔案製作或視覺化編輯器輕鬆建立和管理店面內容，並包含原生實驗功能。</td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/page-builder/guide-overview">頁面產生器</a></td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/seo/url-rewrites/url-rewrite">URL重新寫入</a></td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/staging/content-staging">內容分段</a></td>
            <td rowspan="2"><a href="../catalog-service/overview.md">目錄服務</a></td>
            <td rowspan="2">多樣化檢視模型（唯讀）服務，用於管理目錄資料及呈現產品相關的店面體驗。</td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/merchandising/visual-merch/visual-merchandiser">Visual Merchandiser</a></td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/payments/payments">付款</a></td>
            <td><a href="../payment-services/guide-overview.md">付款服務</a></td>
            <td>整合的支付服務，可促進安全且有效率的交易。</td>
        </tr>
    </tbody>
</table>

## 擴充功能和平台功能

下表比較平台功能與擴充功能，協助您瞭解差異，並在開始實作前，針對最適合您業務需求的模式，做出明智的決策。

<table>
    <thead>
        <tr>
            <th>功能</th>
            <th>Adobe Commerce PaaS模型[!BADGE PaaS only]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案(Adobe管理的PaaS基礎結構)和內部部署專案。"}</th>
            <th>SaaS模型[!BADGE SaaS only]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案(Adobe管理的SaaS基礎結構)。"}</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>平台功能</strong></td>
        </tr>
        <tr>
            <td>B2B功能</td>
            <td>安裝後即可使用完整的B2B功能</td>
            <td>已預先安裝核心B2B功能<sup>1</sup></td>
        </tr>
        <tr>
            <td>實驗</td>
            <td>適用於特定階層的附加元件</td>
            <td>A/B測試可最佳化參與和轉換</td>
        </tr>
        <tr>
            <td>功能與安全性更新</td>
            <td>需要手動升級和修補</td>
            <td>自動部署</td>
        </tr>
        <tr>
            <td>託管基礎結構</td>
            <td>單一租使用者</td>
            <td>多租使用者</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Commerce管理員自訂</strong></td>
        </tr>
        <tr>
            <td>可延伸的核心管理畫面</td>
            <td>完整的版面配置與功能自訂</td>
            <td>預設濾鏡，可見度控制項</td>
        </tr>
        <tr>
            <td>可延伸的新管理員畫面</td>
            <td>標準管理員UI整合和外部應用程式插入(管理員UI SDK)</td>
            <td>外部應用程式插入(管理員UI SDK)</td>
        </tr>
        <tr>
            <td>可自訂的管理主題</td>
            <td>可延伸主題化架構</td>
            <td>無主題化架構</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>擴充性</strong></td>
        </tr>
        <tr>
            <td>擴充性模型</td>
            <td>處理中（PHP自訂）和處理外(API、事件、App Builder)</td>
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
            <td>核心和B2B實體的自訂屬性<sup>2</sup></td>
        </tr>
        <tr>
            <td>技術</td>
            <td>CSS、CLI、HTML、JS、PHP、XML</td>
            <td>CSS、CLI、HTML、JS、節點</td>
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
            <td>App Builder狀態程式庫（僅限檔案）<sup>3</sup></td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td colspan="3">
                <sup>1</sup>核心<a href="https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/guide-overview">B2B功能</a> （例如公司管理和報價）可在SaaS中立即使用。 不過，產業專屬的自訂可能需要額外的實施考量因素。
                <br><br>
                <sup>2</sup> SaaS中的資料模型擴充性支援<a href="https://developer.adobe.com/commerce/webapi/graphql/schema/attributes/mutations/">擴充核心實體</a>，超出產品和客戶範圍，包括B2B實體。 不過，產業特定的資料模型（例如經銷商特定的屬性）可能需要額外的架構考量。
                <br><br>
                <sup>3</sup> Adobe正在積極處理Document DB整合，以滿足SaaS的持續儲存需求。 目前，需要長期資料儲存的實作可能需要布建和維護額外的基礎架構。
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
>- 請考慮使用API Mesh來擴充API功能。
>- 監控Adobe的持續平台演化和新功能發行。
>- 根據可用的擴充性選項評估特定產業資料模型的需求。
>- 考慮採用由管道和原則支援的[銷售服務](../optimizer/setup/catalog-view.md)。
