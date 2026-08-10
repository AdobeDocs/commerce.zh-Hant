---
title: 私人目錄檢視
description: 瞭解如何透過啟用目錄保護來建立私人目錄檢視，以便只有具有有效已簽署Token的請求才能擷取其產品和定價資料。
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和 [!DNL Adobe Commerce Optimizer] 專案（Adobe管理的SaaS基礎結構）。"
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 38fa0734562a631fdcdd7510580571c5d37cb598
workflow-type: tm+mt
source-wordcount: 467
ht-degree: 0%

---

# 私人目錄檢視

依預設，[目錄檢視](catalog-view.md)是公用的。 在目錄檢視上啟用目錄保護，以限制對包含有效已簽署Token之要求的存取權。

目錄保護僅套用至選取的目錄檢視。 它不會變更檢視的原則、圖層或價格簿。

如需保護目錄檢視的時機範例，請參閱[受限制的存取金鑰使用案例](restricted-access-keys.md#restricted-access-key-use-cases)。

## 瞭解保護界限

目錄保護僅適用於啟用它的目錄檢視。 它可保護目錄和搜尋請求，但不變更檢視的原則或價格簿、保護其他目錄檢視，或保護購物車、結帳或訂單操作。

連線的商務後端必須獨立強制執行購買資格。

## 保護目錄檢視

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

如果[!UICONTROL Catalog Protection]已啟用，且所有指派的索引鍵都已過期，目錄檢視將無法存取，依賴此目錄檢視的儲存區域將無法從中提供資料。 指派新的未過期金鑰以還原存取權。 如需指示，請參閱[旋轉鍵](restricted-access-keys.md#rotate-a-key)。

>[!IMPORTANT]
>
>目前無法透過Adobe Commerce和Adobe Commerce Optimizer Connector自動建立和管理金鑰。

## 更多相關資訊

- [目錄檢視](catalog-view.md) — 瞭解目錄檢視如何依業務結構、原則和定價組織您的產品目錄。
- [受限制的存取金鑰](restricted-access-keys.md) — 建立、指派及旋轉用於簽署目錄保護權杖的金鑰。
