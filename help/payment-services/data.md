---
title: 可用資料
description: 使用Financial Reporting資料來協調報表與非Commerce系統。
role: User
level: Intermediate
feature: Payments, Checkout, Data Import/Export
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# 可用資料

您可以使用一些訂單和付款資料，以便協調跨外部系統的Adobe Commerce Financial Reporting。

## 與ERP系統調解

您可以使用與特定訂單相關的增量ID，來調節Adobe Commerce Financial Reporting與非Adobe Enterprise Resource Planning (ERP)系統。

當付款服務傳送Commerce訂單給PayPal時，增量識別碼會包含在`invoice_id`中作為`custom_id` _和_ （也包含`increment_id`之後的隨機字串）。

ID可輕易地從付款的商家活動詳細資料和PayPal webhook中存取。

`invoice_id`與`custom_id`會顯示在付款的商家活動詳細資訊的底部附近：

商戶活動詳細資料![&#128279;](assets/merchant-activity-ids.png){width="600" zoomable="yes"}中的`custom_id`

PayPal的webhook詳細資料中的`custom_id`和`invoice_id`：

```json
   ...
   {
    "id": "4E855005GK253170H",
    "intent": "AUTHORIZE",
    "status": "COMPLETED",
    "payment_source": {
        ...
    },
    "purchase_units": [
        {
            ...
            "custom_id": "000001322",
            "invoice_id": "000001322-c01bd7c3-920f-4542-a900-738082177e92",
            ...
            "payments": {
                "authorizations": [
                    {
                       ...
                        "invoice_id": "000001322-c01bd7c3-920f-4542-a900-738082177e92",
                        "custom_id": "000001322",
                        ...
                    }
                ],
                "captures": [
                    {
                        ...
                        "invoice_id": "000001322-c01bd7c3-920f-4542-a900-738082177e92",
                        "custom_id": "000001322",
                        ...
                    }
                ]
            }
        }
    ],
    "payer": {
        ...
    },
    "create_time": "2022-09-12T14:59:01Z",
    "update_time": "2022-09-12T14:59:45Z",
    "links": [
        ...
    ]
}
   ...
```

如需詳細資訊，請參閱PayPal的REST API檔案：

* [`purchase_unit`，其中`custom_id`與`invoice_id`位於](https://developer.paypal.com/docs/api/orders/v2/#definition-purchase_unit)
* [顯示訂單詳細資料](https://developer.paypal.com/docs/api/orders/v2/#orders_get)
