---
title: 自訂自動比對
description: 瞭解自訂自動比對如何對具有複雜比對邏輯的商家，或依賴第三方系統（無法將中繼資料填入AEM Assets）的商戶特別有用。
feature: CMS, Media, Integration
exl-id: e7d5fec0-7ec3-45d1-8be3-1beede86c87d
TQID: https://experienceleague.adobe.com/RHRfW99iShMpajrEC8BhvoMEfQ-ABdipWTCdK-KaVH4
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
source-git-commit: 7ecedcc7c17abdeb64507d8f74ec6fc103b361cc
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%
---
# 自訂自動比對

如果預設的自動比對策略（**OOTB自動比對**）不符合您的特定業務需求，請選取自訂比對選項。 此選項支援使用[Adobe Developer App Builder](https://experienceleague.adobe.com/zh-hant/docs/commerce-learn/tutorials/extensibility/adobe-developer-app-builder/introduction-to-app-builder)來開發自訂符合器應用程式，以處理複雜的符合邏輯，或來自無法將中繼資料填入AEM Assets的協力廠商系統的資產。

## 設定自訂自動比對

1. 從Commerce管理員中，導覽至「**[!UICONTROL Store]** >設定> **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**」。

1. 選取&#x200B;**[!UICONTROL Custom Matcher]**&#x200B;作為比對規則。

1. 當您選取此比對規則時，Admin會顯示其他欄位，以設定&#x200B;**端點**&#x200B;和自訂比對邏輯所需的&#x200B;**驗證引數**。

### workspace.json

**[!UICONTROL Adobe I/O Workspace Configuration]**&#x200B;欄位透過匯入App Builder `workspace.json`設定檔，提供簡化的自訂比對器設定方式。

您可以從[Adobe Developer Console](https://developer.adobe.com/console)下載`workspace.json`檔案。 此檔案包含您App Builder工作區的所有認證和設定詳細資料。

+++範例`workspace.json`

```json
{
  "project": {
    "id": "project_id",
    "name": "project_name",
    "title": "title_name",
    "org": {
      "id": "id",
      "name": "Organization_name",
      "ims_org_id": "ims_id"
    },
    "workspace": {
      "id": "workspace_id",
      "name": "workspace_name_id",
      "title": "workspace_title_id",
      "action_url": "https://action_url.net",
      "app_url": "https://app_url.net",
      "details": {
        "credentials": [
          {
            "id": "credential_id",
            "name": "credential_name_id",
            "integration_type": "oauth_server_to_server",
            "oauth_server_to_server": {
              "client_id": "client_id",
              "client_secrets": ["secret"],
              "technical_account_email": "xx@technical_account_email.com",
              "technical_account_id": "technical_account_id",
              "scopes": [
                "AdobeID",
                "openid",
                "read_organizations",
                "additional_info.projectedProductContext",
                "additional_info.roles",
                "adobeio_api",
                "read_client_secret",
                "manage_client_secrets"
              ]
            }
          }
        ],
        "services": [
          {
            "code": "AdobeIOManagementAPISDK",
            "name": "I/O Management API"
          }
        ],
        "runtime": {
          "namespaces": [
            {
              "name": "namespace_name",
              "auth": "example_auth"
            }
          ]
        },
        "events": {
          "registrations": []
        },
        "mesh": {}
      }
    }
  }
}
```

+++

1. 將您的`workspace.json`檔案從App Builder專案拖放至&#x200B;**[!UICONTROL Adobe I/O Workspace Configuration]**&#x200B;欄位。 或者，您可以按一下瀏覽並選取檔案。

![Workspace設定](../assets/workspace-configuration.png){width="600" zoomable="yes"}

1. 系統自動：

   * 驗證JSON結構
   * 擷取及填入OAuth認證
   * 擷取工作區的可用執行階段動作
   * 填入&#x200B;**[!UICONTROL Product to Asset URL]**&#x200B;和&#x200B;**[!UICONTROL Asset to Product URL]**&#x200B;欄位的下拉式清單選項

1. 從每個流程的下拉式選單中選取適當的執行階段動作。

1. 按一下&#x200B;**[!UICONTROL Save Config]**。

## 非同步設定儲存

如果您的Commerce執行個體已啟用[非同步設定儲存](https://experienceleague.adobe.com/zh-hant/docs/commerce-operations/performance-best-practices/configuration#asynchronous-configuration-save)選項，則非同步取用者會將設定變更排入佇列並套用，而不會立即儲存在相同請求中。 若要在此模式中上傳自訂自動比對的`workspace.json`檔案，請依序完成下列步驟：

1. 確認Commerce非同步設定儲存已[啟用](https://experienceleague.adobe.com/zh-hant/docs/commerce-operations/performance-best-practices/configuration#asynchronous-configuration-save)。

1. 從Admin移至&#x200B;**[!UICONTROL Stores]** > [!UICONTROL Settings] > **[!UICONTROL Configuration]** > **[!UICONTROL Adobe Services]** > **[!UICONTROL AEM Assets Integration]**。

1. 上傳目前的App Builder `workspace.json`檔案。

1. 儲存設定。

1. 等候非同步設定取用者完成儲存處理。

1. 驗證OAuth值和相依的整合設定。

1. 驗證外部符合者註冊是否反映更新。

>[!NOTE]
>
>如果「非同步設定儲存」已停用，則會套用一般的同步儲存行為，而且您不需要等候佇列取用者。

### 疑難排解非同步設定儲存

| 症狀 | 該做什麼 |
| --- | --- |
| OAuth值在儲存後保持不變 | 確認您正在執行AEM Assets Integration擴充功能1.4.7版或更新版本，上傳新的`workspace.json`檔案，並等候佇列處理完成，然後再檢查值。 |
| 上傳無效後儲存失敗 | 驗證檔案是否為格式正確的`workspace.json`檔案，且包含預期的App Builder認證。 |
| 未上傳任何檔案 | 現有的已儲存組態保持不變。 |
| 外部比對器註冊不會更新 | 檢查佇列取用者是否已完成處理、檢閱Commerce記錄，並確認外部符合者註冊狀態。 |
| 停用非同步設定儲存 | 一般同步儲存行為適用；此疑難排解區段不適用。 |

>[!NOTE]
>
>如果您開發AEM Assets整合的設定觀察程式，就不需要依賴原始HTTP請求引數。 非同步設定儲存和其他程式化設定儲存可在沒有管理員請求內容的情況下執行觀察者。

## 自訂比對器API端點

當您使用[App Builder](https://experienceleague.adobe.com/zh-hant/docs/commerce-learn/tutorials/extensibility/adobe-developer-app-builder/introduction-to-app-builder){target=_blank}建置自訂符合專案應用程式時，應用程式必須公開下列端點：

* **App Builder資產至產品URL**&#x200B;端點
* **App Builder產品至資產URL**&#x200B;端點

### App Builder資產至產品URL端點

此端點會擷取與指定資產相關聯的SKU清單：

#### 使用範例

```javascript
const { Core } = require('@adobe/aio-sdk')

async function main(params) {

    // Build your own matching logic here to return the products that map to the assetId
    // var productMatches = [];
    // params.assetId
    // params.eventData.assetMetadata['commerce:isCommerce']
    // params.eventData.assetMetadata['commerce:skus'][i]
    // params.eventData.assetMetadata['commerce:roles']
    // params.eventData.assetMetadata['commerce:positions'][i]
    // ...
    // End of your matching logic

    // Set skip to true if the mapping hasn't changed
    const skipSync = false;

    return {
        statusCode: 200,
        body: {
            asset_id: params.assetId,
            product_matches: [
                {
                    product_sku: "<YOUR-SKU-HERE>",
                    asset_roles: ["thumbnail", "image", "swatch_image", "small_image"],
                    asset_position: 1
                }
            ],
            skip: skipSync
        }
    };
}

exports.main = main;
```

**要求**

```text
POST https://your-app-builder-url/api/v1/web/app-builder-external-rule/asset-to-product
```

| 引數 | 資料型別 | 說明 |
| --- | --- | --- |
| `assetId` | 字串 | 代表更新的資產ID。 |
| `eventData` | 物件 | 與資產相關聯的事件裝載（例如，符合專案從`eventData.assetMetadata`讀取的資產中繼資料）。 |

**回應**

```json
{
  "asset_id": "{ASSET_ID}",
  "product_matches": [
    {
      "product_sku": "{PRODUCT_SKU_1}",
      "asset_roles": ["thumbnail", "image"]
    },
    {
      "product_sku": "{PRODUCT_SKU_2}",
      "asset_roles": ["thumbnail"]
    }
  ],
  "skip": false
}
```

| 引數 | 資料型別 | 說明 |
| --- | --- | --- |
| `asset_id` | 字串 | 相符的資產ID。 |
| `product_matches` | 陣列 | 與資產相關聯的產品清單。 |
| `skip` | 布林值 | （選用）當`true`時，規則引擎會略過此資產的同步處理（無產品對應更新）。 當`false`或省略時，正常處理會執行。 請參閱[略過同步處理](#skip-sync-processing)。 |

### App Builder產品至資產URL端點

此端點會擷取與指定SKU相關聯的資產清單：

#### 使用範例

```javascript
const { Core } = require('@adobe/aio-sdk')

async function main(params) {
    // return asset matches for a product
    // Build your own matching logic here to return the assets that map to the productSku
    // var assetMatches = [];
    // params.productSku
    // ...
    // End of your matching logic

    // Set skip to true if the mapping hasn't changed
    const skipSync = false;

    return {
        statusCode: 200,
        body: {
            product_sku: params.productSku,
            asset_matches: [
                {
                    asset_id: "<YOUR-ASSET-ID-HERE>", // urn:aaid:aem:1aa1d5i2-17h8-40a7-a228-e3ur588deee1
                    asset_roles: ["thumbnail", "image", "swatch_image", "small_image"],
                    asset_format: "image", // can be "image" or "video"
                    asset_position: 1
                }
            ],
            skip: skipSync
        }
    };
}

exports.main = main;
```

**要求**

```text
POST https://your-app-builder-url/api/v1/web/app-builder-external-rule/product-to-asset
```

| 引數 | 資料型別 | 說明 |
| --- | --- | --- |
| `productSku` | 字串 | 代表更新的產品SKU。 |
| `eventData` | 物件 | 與產品相關聯的事件裝載（例如，符合專案從傳入事件使用的欄位）。 |

**回應**

```json
{
  "product_sku": "{PRODUCT_SKU}",
  "asset_matches": [
    {
      "asset_id": "{ASSET_ID_1}",
      "asset_roles": ["thumbnail", "image"],
      "asset_position": 1,
      "asset_format": "image"
    },
    {
      "asset_id": "{ASSET_ID_2}",
      "asset_roles": ["thumbnail"],
      "asset_position": 2,
      "asset_format": "image"
    }
  ],
  "skip": false
}
```

| 引數 | 資料型別 | 說明 |
| --- | --- | --- |
| `product_sku` | 字串 | 相符的產品SKU。 |
| `asset_matches` | 陣列 | 與產品相關聯的資產清單。 |
| `skip` | 布林值 | （選用）當`true`時，規則引擎會略過此產品的同步處理（無資產對應更新）。 當`false`或省略時，正常處理會執行。 請參閱[略過同步處理](#skip-sync-processing)。 |

`asset_matches`引數包含下列屬性：

| 屬性 | 資料型別 | 說明 |
| --- | --- | --- |
| `asset_id` | 字串 | 資產識別碼。 |
| `asset_roles` | 陣列 | 資產角色。 使用支援的[Commerce資產角色](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/catalog/products/digital-assets/product-image#image-roles)，例如`thumbnail`、`image`、`small_image`和`swatch_image`。 若使用AEM Assets整合擴充功能1.4.6和更新版本，也可接受自訂影像角色（例如`hero`或`custom_role_1`）。 |
| `asset_format` | 字串 | 資產格式。 可能的值為`image`和`video`。 |
| `asset_position` | 數字 | 資產在產品相簿中的位置。 |

## 略過同步處理

`skip`引數可讓您的自訂比對器略過特定資產或產品的同步處理。

當您的App Builder應用程式在回應中傳回`"skip": true`時，規則引擎不會傳送該資產或產品的更新或移除API請求給Commerce。 此最佳化可減少不必要的API呼叫並改善效能。
