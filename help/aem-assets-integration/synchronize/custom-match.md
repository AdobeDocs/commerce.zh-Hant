---
title: 自訂自動比對
description: 瞭解自訂自動比對如何對具有複雜比對邏輯的商家，或依賴第三方系統(無法將中繼資料填入AEM Assets)的商戶特別有用。
feature: CMS, Media, Integration
exl-id: e7d5fec0-7ec3-45d1-8be3-1beede86c87d
source-git-commit: 7639422b237ad04cada366c541c041bc146ce085
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# 自訂自動比對

如果預設的自動比對策略（**OOTB自動比對**）不符合您的特定業務需求，請選取自訂比對選項。 此選項支援使用[Adobe Developer App Builder](https://experienceleague.adobe.com/zh-hant/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder)來開發自訂符合器應用程式，以處理複雜的符合邏輯，或來自無法將中繼資料填入AEM Assets的協力廠商系統的資產。

## 設定自訂自動比對

1. 從Commerce管理員中，導覽至「**[!UICONTROL Store]** >設定> **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**」。

1. 選取&#x200B;**[!UICONTROL Custom Matcher]**&#x200B;作為比對規則。

1. 當您選取此比對規則時，Admin會顯示其他欄位，以設定&#x200B;**端點**&#x200B;和自訂比對邏輯所需的&#x200B;**驗證引數**。

## 自訂比對器API端點

當您使用[App Builder](https://experienceleague.adobe.com/zh-hant/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder){target=_blank}建置自訂符合專案應用程式時，應用程式必須公開下列端點：

* **App Builder資產至產品URL**&#x200B;端點
* **App Builder產品至資產URL**&#x200B;端點

### App Builder資產至產品URL端點

此端點會擷取與指定資產相關聯的SKU清單：

#### 使用範例

```bash
const { Core } = require('@adobe/aio-sdk')
 
async function main (params) {
    // return the products that map to the assetId
    return {
        statusCode: 200,
        body: {
          asset_id: "urn:aaid:aem:1aa1d4a0-18b8-40a7-a228-e0ab588deee1",
          product_matches: [
            {
              product_sku: "SKU1",
              asset_roles: ["thumbnail"],
              asset_position: [1]
            }
          ]
        }
   }
}
 
exports.main = main
```

**要求**

```bash
GET https://your-app-builder-url/api/v1/web/app-builder-external-rule/asset-to-product
```

| 引數 | 資料型別 | 說明 |
| --- | --- | --- |
| `assetId` | 字串 | 代表更新的資產ID |

**回應**

```bash
{
  "asset_id": "{ASSET_ID}",
  "product_matches": [
    {
      "product_sku": "{PRODUCT_SKU_1}",
      "asset_roles": ["thumbnail","image"]
    },
    {
      "product_sku": "{PRODUCT_SKU_2}",
      "asset_roles": ["thumbnail"]
    }
  ]
}
```

### App Builder產品至資產URL端點

此端點會擷取與指定SKU相關聯的資產清單：

#### 使用範例

```bash
const { Core } = require('@adobe/aio-sdk')
 
async function main (params) {
    // return asset matches for a product
    return {
        statusCode: 200,
        body: {
          product_sku: params.productSku, //SKU-1
          asset_matches: [
            {
              asset_id: "urn:aaid:aem:1aa1d4a0-18b8-40a7-a228-e0ab588deee1",
              asset_roles: ["thumbnail","image"]
            }
          ]
        }
      }
}
 
exports.main = main
```

**要求**

```bash
GET https://your-app-builder-url/api/v1/web/app-builder-external-rule/product-to-asset
```

| 引數 | 資料型別 | 說明 |
| --- | --- | --- |
| `productSKU` | 字串 | 代表更新的產品SKU |

**回應**

```bash
{
  "product_sku": "{PRODUCT_SKU}",
  "asset_matches": [
    {
      "asset_id": "{ASSET_ID_1}",
      "asset_roles": ["thumbnail","image"]
    },
    {
      "asset_id": "{ASSET_ID_2}",
      "asset_roles": ["thumbnail"]
    }
  ]
}
```

>[!TIP]
>
> 在`asset_roles`金鑰中，使用支援的[Commerce資產角色](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/catalog/products/digital-assets/product-image#image-roles)，例如`thumbnail`、`image`、`small_image`和`swatch_image`。
