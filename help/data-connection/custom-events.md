---
title: 建立自訂事件
description: 瞭解如何建立自訂事件，將您的Adobe Commerce資料連線至其他Adobe DX產品。
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: db782c0a-8f13-4076-9b17-4c5bf98e9d01
source-git-commit: 81fbcde11da6f5d086c2b94daeffeec60a9fdbcc
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 1%

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

僅Experience Platform支援標準事件的屬性覆寫。 自訂資料不會轉送到Commerce儀表板和量度追蹤器。

對於具有`customContext`的任何事件，收集器會覆寫在相關內容中設定的聯結欄位（欄位在`customContext`中）。 覆寫的使用案例是當開發人員想要重複使用和擴充由頁面其他部分在已支援的事件中設定的內容時。

### 範例

透過Adobe Commerce Events SDK發佈的具覆寫功能的產品檢視：

```javascript
mse.publish.productPageView({
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

在Experience Platform Edge中：

```javascript
{
  xdm: {
    eventType: 'commerce.productViews',
    identityMap: {
      ECID: [
        {
          id: 'ecid1234',
          primary: true,
        }
      ]
    },
    commerce: {
      productViews: {
        value : 1,
      }
    },
    productListItems: [{
        SKU: "1234",
        name: "leora summer pants",
        productCategories: [{
            categoryID: "cat_15",
            categoryName: "summer pants",
            categoryPath: "pants/mens/summer",
        }],
    }],
  }
}
```

Luma商店：

在Luma型存放區中，發佈事件會以原生方式實施。 因此，您可以延伸`customContext`來設定自訂資料。

例如：

```javascript
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
```

請參閱[自訂事件覆寫](https://github.com/adobe/commerce-events/blob/main/examples/events/custom-event-override.md)，深入瞭解如何處理自訂資料。

>[!NOTE]
>
> 使用自訂屬性覆寫事件可能會影響預設的Adobe Analytics報表。
