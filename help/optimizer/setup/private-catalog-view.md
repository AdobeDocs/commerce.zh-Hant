---
title: 私人目錄檢視
description: 瞭解私人目錄檢視如何限制目錄資料存取、自動為B2B共用目錄建立或手動設定目錄保護。
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和[!DNL Adobe Commerce Optimizer]個專案（Adobe管理的SaaS基礎結構）。"
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
    internal-label: Optimization
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
source-git-commit: f93bd673624c58050696da772ce733874ce594e5
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 0%
---
# 私人目錄檢視

依預設，[目錄檢視](catalog-view.md)是公用的。 限制對目錄檢視的存取，以便只有具有有效簽署權杖的請求才能擷取其資料。

目錄檢視會透過下列兩種方式之一變成私人：

- [!BADGE Private Beta]{type=Caution tooltip="需要Adobe Commerce Optimizer Connector B2B擴充功能，目前為私人測試版。"} **自動，針對B2B共用目錄** — 針對使用[!DNL Adobe Commerce Optimizer Connector]與B2B擴充功能整合的Commerce部署，會根據[!DNL Adobe Commerce]中的共用目錄組態，自動為您建立和設定私人目錄檢視。 請參閱[B2B共用目錄的自動私人目錄檢視](#automatic-private-catalog-views-for-b2b-shared-catalogs)。

- **手動，針對任何目錄檢視** — 若要限制存取原本為公開的目錄檢視，包括B2C目錄檢視，請依照[保護目錄檢視](#protect-a-catalog-view)中的步驟操作。 請參閱[受限存取金鑰使用案例](restricted-access-keys.md#restricted-access-key-use-cases)以取得範例，例如合作夥伴入口網站和發行前預覽。

目錄保護僅套用至選取的目錄檢視。 它不會變更檢視的原則或圖層。 它會將檢視限製為單一價格簿 — 請參閱私人目錄檢視上的[價格簿限制](#price-book-restriction-on-private-catalog-views)。

## 瞭解保護界限

目錄保護僅適用於啟用它的目錄檢視。 它可保護目錄和搜尋請求，但不會變更檢視的原則或層、保護其他目錄檢視，或保護購物車、結帳或訂單操作。

連線的商務後端必須獨立強制執行購買資格。

## 私人目錄檢視的價格簿限制

私人目錄檢視只能參考一個價格簿。 這與公用型錄檢視不同，後者可以使用多個價格簿。

啟用[!UICONTROL Catalog Protection]時，目錄檢視表表單上的價格簿選擇器會從多選控制項切換為單選（選項按鈕）控制項。

![私人目錄檢視價格簿限制](../assets/catalog-view-private-pricebook-restrictions.png)

- 如果您在已指派多個價格簿的型錄檢視上啟用[!UICONTROL Catalog Protection]，則您必須移除除一個價格簿以外的所有價格簿，才能儲存檢視。
- 如果您先前儲存的私人型錄檢視具有在此限制存在之前的多個價格簿指定，則型錄檢視組態不會自動變更。 不過，下次編輯檢視表時，您必須先移除所有價目表（僅一個價目表除外），才能儲存更新。

在這些案例中，[!DNL Adobe Commerce Optimizer]會顯示下列驗證訊息： `A protected catalog view can use only one price book. Select 'Single price book only' to continue.`

公開目錄檢視不受此限制影響，並可繼續參考多個價格簿。

## B2B共用目錄的自動私人目錄檢視

[!BADGE Private Beta]{type=Caution tooltip="需要Adobe Commerce Optimizer Connector B2B擴充功能，目前為私人測試版。"}

對於與[!DNL Adobe Commerce Optimizer Connector for B2B]整合以支援共用目錄的部署，擴充功能會根據[!DNL Adobe Commerce]中的共用目錄組態，自動建立及設定私人目錄檢視。 此設定包括目錄檢視、原則、初始限制存取金鑰和價格簿參考。 使用此設定，您可以從Commerce管理員&#x200B;**受限存取金鑰**&#x200B;頁面（**系統** > **資料傳輸**）管理受限存取金鑰。 如需詳細資訊，請參閱&#x200B;*[!DNL Adobe Commerce Optimizer Connector]整合指南*&#x200B;中的[B2B共用目錄變更](/help/aco-connector/get-started.md#monitor-b2b-shared-catalog-changes)。

如果您未使用B2B共用目錄，例如，為了保護合作夥伴入口網站的目錄檢視或發行前預覽，請使用[保護目錄檢視](#protect-a-catalog-view)中的指示來手動設定一個目錄。

## 保護目錄檢視

>[!NOTE]
>
>針對與[!DNL Adobe Commerce Optimizer Connector for B2B]所管理的B2B共用目錄相關聯的目錄檢視，略過此程式。 請參閱[B2B共用目錄的自動私人目錄檢視](#automatic-private-catalog-views-for-b2b-shared-catalogs)。

開始之前，請從使用者端應用程式產生的公開金鑰[建立限制存取金鑰](restricted-access-keys.md)。

1. 在目錄檢視建立或編輯表單上，將&#x200B;**[!UICONTROL Catalog Protection]**&#x200B;切換為&#x200B;**[!UICONTROL Enabled]**。

1. 在&#x200B;**[!UICONTROL Restricted Access Keys]**&#x200B;底下，選取最多三個[受限制的存取金鑰](restricted-access-keys.md)以指派給此目錄檢視。

   ![目錄檢視編輯表單上已啟用目錄保護，並指派受限制的存取金鑰](../assets/catalog-view-protected.png){width="70%" zoomable="yes"}

1. 按一下&#x200B;**[!UICONTROL Save catalog view]**。

   目錄檢視現在受到保護。 只有從指派的金鑰中攜帶有效已簽署權杖的請求，才能擷取其資料。

   >[!NOTE]
   >
   >允許目錄保護組態變更生效最多五分鐘。

## 驗證存取權是否已強制執行

若要確認私人目錄檢視拒絕未授權的要求，請使用下列標頭，使用及不使用已簽署的權杖呼叫其[GraphQL端點](../get-started.md#get-instance-details)：

| 頁首 | 用途 |
| --- | --- |
| `AC-View-ID` | 要查詢的目錄檢視。 |
| `AC-Price-Book-ID` | 要套用的價格簿。 |
| `AC-Catalog-View-Access-Token` | 已簽署的目錄檢視的JWT證明授權。 |

沒有有效Token的要求會傳回GraphQL錯誤，而非目錄資料，例如：

```json
{
  "errors": [
    {
      "message": "Access key validation failed: Missing token",
      "extensions": { "x-commerce-exception": "access-key-invalid" }
    }
  ]
}
```

要求所攜帶的權杖由指派的未過期金鑰簽署，會如預期傳回目錄資料。 如需簽署JWT和呼叫Merchandising API的詳細資訊，請參閱[開發人員檔案](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api#authentication)。

## 管理受限制的存取金鑰

如果[!UICONTROL Catalog Protection]已啟用，且所有指派的索引鍵都已過期，則目錄檢視將無法存取。 依賴此目錄檢視的店面無法從中提供資料。 指派新的未過期金鑰以還原存取權。 如需指示，請參閱[旋轉鍵](restricted-access-keys.md#rotate-a-key)。

>[!NOTE]
>
>對於與[!DNL Adobe Commerce Optimizer Connector for B2B]擴充功能整合的部署，您可以從Commerce管理員&#x200B;**受限存取金鑰**&#x200B;頁面（**系統** > **資料傳輸**）管理存取金鑰。 如需詳細資訊，請參閱&#x200B;*[!DNL Adobe Commerce Optimizer Connector]整合指南*&#x200B;中的[限制存取金鑰管理](../../aco-connector/restricted-access-keys.md)。

## 更多相關資訊

- [目錄檢視](catalog-view.md) — 瞭解目錄檢視如何依業務結構、原則和定價組織您的產品目錄。
- [受限制的存取金鑰](restricted-access-keys.md) — 建立、指派及旋轉用於簽署目錄保護權杖的金鑰。
