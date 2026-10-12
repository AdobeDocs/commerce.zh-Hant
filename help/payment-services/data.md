---
title: 可用資料
description: 使用Financial Reporting資料來協調報表與非Commerce系統。
role: User
level: Intermediate
exl-id: dbf41ce9-01f9-45d0-b651-e4c499e83822
feature: Payments, Checkout, Data Import/Export, Paas, Saas
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 601e4abe-d9bf-58de-a779-32ed6794dcbe
    internal-label: Data Import/Export
  - id: 00451af3-7b97-5414-9992-3a6c269e413f
    internal-label: Paas
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
source-git-commit: 76e77db86adecdbd3be76040970c0d0899c34cdc
workflow-type: tm+mt
source-wordcount: '167'
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

* [`purchase_unit`，其中`custom_id`與`invoice_id`位在](https://developer.paypal.com/docs/api/orders/v2/#definition-purchase_unit)
* [顯示訂單詳細資料](https://developer.paypal.com/docs/api/orders/v2/#orders_get)
