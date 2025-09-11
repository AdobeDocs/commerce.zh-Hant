---
title: 建立自訂事件
description: 瞭解如何建立自訂事件，將您的Adobe Commerce資料連線至其他Adobe DX產品。
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: db782c0a-8f13-4076-9b17-4c5bf98e9d01
source-git-commit: 25d796da49406216f26d12e3b1be01902dfe9302
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# 建立自訂事件

您可以建立自己的店面活動來收集產業獨有的資料，以擴充[事件平台](events.md)。 當您建立和設定自訂事件時，會傳送到[Adobe Commerce事件收集器](https://github.com/adobe/commerce-events/tree/main/packages/storefront-events-collector)。

## 處理自訂事件

僅支援Adobe Experience Platform的自訂事件。 自訂資料不會轉送到Adobe Commerce儀表板和量度追蹤器。

對於任何`custom`事件，收集器：

- 將具有`identityMap`的`ECID`新增為主要身分
- 在`email`中包含`identityMap`以作為次要身分&#x200B;_如果_ `personalEmail.address`已設定在事件中
- 在轉送至Edge之前，先包裝`xdm`物件內的完整事件

範例：

透過Adobe Commerce Events SDK發佈的自訂事件：

```javascript
mse.publish.custom({
    commerce: {
        saveForLaters: {
            value: 1,
        },
    },
});
```

在Experience Platform Edge中：

```javascript
{
  xdm: {
    identityMap: {
      ECID: [
        {
          id: 'ecid1234',
          primary: true
        }
      ],
      email: [
        {
          id: "runs@safari.ke",
          primary: false
        }
      ]
    },
    commerce: {
        saveForLaters: {
            value: 1
        }
    }
  }
}
```

>[!NOTE]
>
> 使用自訂事件可能會影響預設的Adobe Analytics報表。

## 處理事件覆寫（自訂屬性）

對於使用`customContext`設定的任何事件，收集器會覆寫或延伸`custom context`中欄位之事件裝載中的欄位。 覆寫的使用案例是當開發人員想要重複使用和擴充由頁面其他部分在已支援的事件中設定的內容時。

事件覆寫僅適用於轉送至Experience Platform時。 它們不會套用至Adobe Commerce和Sensei分析事件。 Adobe Commerce事件收集器[README](https://github.com/adobe/commerce-events/blob/e34bcfc0deca8d5ac1f9310fc1ee4c1becf4ffbb/packages/storefront-events-collector/README.md)提供其他資訊。

>[!NOTE]
>
>使用Experience Platform事件裝載中的自訂屬性增加`productListItems`時，請使用SKU比對產品。 此要求不適用於`product-page-view`個事件。

### 使用情況

```javascript
const mse = window.magentoStorefrontEvents;

mse.publish.productPageView(customCtx);
```

### 範例1 — 新增`productCategories`

```javascript
magentoStorefrontEvents.publish.productPageView({
    productListItems: [
        {
            productCategories: [
                {
                    categoryID: "cat_15",
                    categoryName: "summer pants",
                    categoryPath: "pants/mens/summer",
                },
            ],
        },
    ],
});
```

### 範例2 — 在發佈事件前新增自訂內容

```javascript
const mse = window.magentoStorefrontEvents;

mse.context.setCustom({
  productListItems: [
    {
      productCategories: [
        {
          categoryID: "cat_15",
          categoryName: "summer pants",
          categoryPath: "pants/mens/summer",
        },
      ],
    },
  ],
});

mse.publish.productPageView();
```

### 範例3 — 在發佈程式中設定的自訂內容會覆寫先前在Adobe Client Data Layer中設定的自訂內容。

在此範例中，`pageView`事件在&#x200B;**欄位中會有**&#x200B;自訂頁面名稱2`web.webPageDetails.name`。

```javascript
const mse = window.magentoStorefrontEvents;

mse.context.setCustom({
  web: {
    webPageDetails: {
      name: 'Custom Page Name 1'
    },
  },
});

mse.publish.pageView({
  web: {
    webPageDetails: {
      name: 'Custom Page Name 2'
    },
  },
});
```

### 範例4 — 使用具有多個產品的事件將自訂內容新增至`productListItems`

```javascript
const mse = window.magentoStorefrontEvents;

mse.context.setCustom({
  productListItems: [
    {
      SKU: "24-WB01", //Match SKU to override correct product in event payload
      productCategory: "Hand Bag", //Custom attribute added to event payload
      name: "Strive Handbag (CustomName)" //Override existing attribute with custom value in event payload
    },
    {
      SKU: "24-MB04",
      productCategory: "Backpack Bag",
      name: "Strive Backpack (CustomName)"
    },
  ],
});

mse.publish.shoppingCartView();
```

>[!NOTE]
>
> 使用自訂屬性覆寫事件可能會影響預設的Adobe Analytics報表。
