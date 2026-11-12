---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 0%
---
依預設，[目錄檢視](catalog-view.md)是公用的。 限制對目錄檢視的存取，以便只有具有有效簽署權杖的請求才能擷取其資料。

目錄檢視會透過下列兩種方式之一變成私人：

- **自動，針對B2B共用目錄** — 對於使用銷售服務搭配可撰寫目錄資料模型(CCDM)的Adobe Commerce B2B部署，會根據[!DNL Adobe Commerce]中的共用目錄組態，自動為您建立和設定私人目錄檢視。 請參閱[B2B共用目錄的自動私人目錄檢視](#automatic-private-catalog-views-for-b2b-shared-catalogs)。

- **手動，針對任何目錄檢視** — 若要限制存取原本為公開的B2C目錄檢視，請依照[保護目錄檢視](#protect-a-catalog-view)中的步驟操作。 請參閱[受限存取金鑰使用案例](restricted-access-keys.md#restricted-access-key-use-cases)以取得範例，例如合作夥伴入口網站和發行前預覽。

目錄保護僅套用至選取的目錄檢視。 它不會變更檢視的原則或圖層。 它會將檢視限製為單一價格簿 — 請參閱私人目錄檢視上的[價格簿限制](#price-book-restriction-on-private-catalog-views)。

## 瞭解保護界限

目錄保護僅適用於啟用它的目錄檢視。 它可保護目錄和搜尋請求，但不會變更檢視的原則或層、保護其他目錄檢視，或保護購物車、結帳或訂單操作。

連線的商務後端必須獨立強制執行購買資格。

## 私人目錄檢視的價格簿限制

私人目錄檢視只能參考一個價格簿。 這與公用型錄檢視不同，後者可以使用多個價格簿。

啟用[!UICONTROL Catalog Protection]時，目錄檢視表表單上的價格簿選擇器會從多選控制項切換為單選（選項按鈕）控制項。

![私人目錄檢視價格簿限制](/help/assets/ccdm-shared/setup/catalog-view-private-pricebook-restrictions.png)

- 如果您在已指派多個價格簿的型錄檢視上啟用[!UICONTROL Catalog Protection]，則您必須移除除一個價格簿以外的所有價格簿，才能儲存檢視。
- 如果您先前儲存的私人型錄檢視具有在此限制存在之前的多個價格簿指定，則型錄檢視組態不會自動變更。 不過，下次編輯檢視表時，您必須先移除所有價目表（僅一個價目表除外），才能儲存更新。

在這些案例中，系統會顯示下列驗證訊息： `A protected catalog view can use only one price book. Select 'Single price book only' to continue.`

公開目錄檢視不受此限制影響，並可繼續參考多個價格簿。

## B2B共用目錄的自動私人目錄檢視

[!BADGE Private beta]{type=Caution tooltip="需要Adobe Commerce Optimizer Connector B2B擴充功能，目前為私人測試版。"}

針對使用銷售服務搭配CCDM的Adobe Commerce B2B部署，系統會根據[!DNL Adobe Commerce]中的共用目錄組態，自動建立及設定私人目錄檢視。 此設定包括目錄檢視、原則、初始限制存取金鑰和價格簿參考。 使用此設定，您可以從Commerce管理員&#x200B;**受限存取金鑰**&#x200B;頁面（**系統** > **資料傳輸**）管理受限存取金鑰。

如果您未使用B2B共用目錄，例如，為了保護合作夥伴入口網站的目錄檢視或發行前預覽，請使用[保護目錄檢視](#protect-a-catalog-view)中的指示來手動設定一個目錄。

## 保護目錄檢視

>[!NOTE]
>
>針對與[!DNL Adobe Commerce Optimizer Connector for B2B]所管理的B2B共用目錄相關聯的目錄檢視，略過此程式。 請參閱[B2B共用目錄的自動私人目錄檢視](#automatic-private-catalog-views-for-b2b-shared-catalogs)。

開始之前，請從使用者端應用程式產生的公開金鑰[建立限制存取金鑰](restricted-access-keys.md)。

1. 在目錄檢視建立或編輯表單上，將&#x200B;**[!UICONTROL Catalog Protection]**&#x200B;切換為&#x200B;**[!UICONTROL Enabled]**。

1. 在&#x200B;**[!UICONTROL Restricted Access Keys]**&#x200B;底下，選取最多三個[受限制的存取金鑰](restricted-access-keys.md)以指派給此目錄檢視。

   ![目錄檢視編輯表單上已啟用目錄保護，並指派受限制的存取金鑰](/help/assets/ccdm-shared/setup/catalog-view-protected.png){width="70%" zoomable="yes"}

1. 按一下&#x200B;**[!UICONTROL Save catalog view]**。

   目錄檢視現在受到保護。 只有從指派的金鑰中攜帶有效已簽署權杖的請求，才能擷取其資料。

   >[!NOTE]
   >
   >允許目錄保護組態變更生效最多五分鐘。

## 驗證存取權是否已強制執行

若要確認私人目錄檢視會拒絕未授權的請求，請使用以下標頭，使用和不使用已簽署的Token呼叫其GraphQL端點：

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

如果[!UICONTROL Catalog Protection]已啟用，且所有指派的索引鍵都已過期，則目錄檢視將無法存取。 依賴此目錄檢視的店面無法從中提供資料。 指派新的未過期金鑰以還原存取權。 如需指示，請參閱[旋轉索引鍵](restricted-access-keys.md#rotate-a-key)。

>[!NOTE]
>
>針對使用具有CCDM之銷售服務的Adobe Commerce B2B部署，您可以從Commerce管理員&#x200B;**受限制的存取金鑰**&#x200B;頁面（**系統** > **資料傳輸**）管理存取金鑰。 如需詳細資訊，請參閱&#x200B;*[!DNL Adobe Commerce Optimizer Connector]整合指南*&#x200B;中的[限制存取金鑰管理](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/systems/data-transfer/data-sync/catalog-view-sync/restricted-access-keys)。

## 更多相關資訊

- [目錄檢視](catalog-view.md) — 瞭解目錄檢視如何依業務結構、原則和定價組織您的產品目錄。
- [受限制的存取金鑰](restricted-access-keys.md) — 建立、指派及旋轉用於簽署目錄保護權杖的金鑰。
