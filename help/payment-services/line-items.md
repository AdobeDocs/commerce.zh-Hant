---
title: ' [!DNL Payment Services]的行專案'
description: 瞭解 [!DNL Payment Services] 的行專案，以及如何檢視商家儀表板中的行專案。
feature: Payments, Paas, Saas
role: User
exl-id: f690ff94-f83d-4525-9d52-1dea25a71060
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---

# [!DNL Payment Services]的行專案

[!DNL Payment Services]的行專案是訂單中包含的專案。 這些明細專案會提供下列資訊：

* 產品詳細資料
* 數量
* 價格（包括稅金、折扣及其他相關資訊）

此資訊對於客戶服務、訂單管理和適當的帳單相當實用。

此功能預設為[!DNL Payment Services]啟用。 若要檢視行專案，請執行下列動作：

1. 導覽至您的[PayPal商家儀表板](https://www.paypal.com/merchant/){target=_blank}。

1. 按一下&#x200B;**活動** > **所有交易**。

1. 選取想要的訂單並檢視其明細專案：

   > 購物者儀表板檢視中的條列專案範例

   ![行專案檢視](assets/paypal-shopper-dashboard-line-items-view.png){width="500" zoomable="yes"}

## 明細專案屬性

透過Adobe Commerce下訂單時會產生明細專案，並將資訊傳送至PayPal，其屬性如下：

| 屬性 | 資料型別 | 說明 |
| --- | --- | --- |
| `name` | 字串！ | 專案名稱。 如果料號因多重數量或稅捐舍入發放而擁有多個明細行，則所有明細行的料號名稱都會相同，但顯示的價格可能會因舍入而稍有不同。 |
| `unit_amount` | 物件！ | 每單位的料號價格或費率。 包含下列屬性： `currency_code`和`value`。 |
| `tax` | 物件 | 每個單位的料號稅捐。 包含下列屬性： `currency_code`和`value`。 |
| `quantity` | 字串！ | 料號數量。 將會是整數。 |
| `description` | 字串 | 詳細的料號摘要。 |
| `sku` | 字串 | 料號的庫存單位（或SKU）。 |
| `url` | 字串 | 要購買的專案的`URL`。 對購買者可見，並用於購買者體驗。 |
| `upc` | 物件 | 專案的通用產品代碼（或UPC）。 |
| `category` | 字串 | 料號分型別態。 |

### `unit_amount`屬性

`unit_amount`物件包含下列屬性：

| 屬性 | 資料型別 | 說明 |
| --- | --- | --- |
| `currency_code` | 字串！ | 識別貨幣的[三字元ISO-4217貨幣代碼](https://developer.paypal.com/api/rest/reference/currency-codes/)。 |
| `value` | 字串！ | 表示專案的值。 `currency_code`會決定所需的小數位數（若有的話）。 |

### `tax`屬性

`tax`物件包含下列屬性：

| 屬性 | 資料型別 | 說明 |
| --- | --- | --- |
| `currency_code` | 字串！ | 識別貨幣的[三字元ISO-4217貨幣代碼](https://developer.paypal.com/api/rest/reference/currency-codes/)。 |
| `value` | 字串！ | 表示專案的值。 取決於每個`currency_code`的所需小數位數。 |

### `upc`屬性

`upc`物件包含下列屬性：

| 屬性 | 資料型別 | 說明 |
| --- | --- | --- |
| `type` | 字串！ | UPC型別。 |
| `code` | 字串！ | 專案的UPC產品代碼。 |

+++條列專案範例

```json
{
    "name": "Crown Summit Backpack - 1",
    "unit_amount": {
        "currency_code": "USD",
        "value": "38.50"
    },
    "tax": {
        "currency_code": "USD"
        "value": "3.13"
    },
    "quantity": "1",
    "description": "The Crown Summit Backpack is equally at home in a gym locker, study cube or a pup tent, so be sure yours is packed with books,",
    "sku": "24-MB03",
    "url": "https://magento.test/crown-summit-backpack.html",
    "upc": {
        "type": "UPC-A",
        "code": "000003"
    },
    "category": "PHYSICAL_GOODS"
},
{
    "name": "Crown Summit Backpack - 2",
    "unit_amount": {
        "currency_code": "USD",
        "value": "38.50"
    },
    "tax": {
        "currency_code": "USD",
        "value": "3.14"
    },
    "quantity": "1",
    "description": "The Crown Summit Backpack is equally at home in a gym locker, study cube or a pup tent, so be sure yours is packed with books,",
    "sku": "24-MB03",
    "url": "https://magento.test/crown-summit-backpack.html",
    "upc": {
        "type": "UPC-A",
        "code": "000003"
    },
    "category": "PHYSICAL_GOODS"
}
```

+++

如需這些欄位及其限制的詳細資訊，請參閱明細專案[&#128279;](https://developer.paypal.com/docs/api/orders/v2/#definition-line_item){target=_blank}的PayPal開發人員檔案。

## 管理條列專案

Adobe Commerce [會根據各資料列](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/taxes/taxes#warning-messages){target=_blank}的總金額來計算稅捐，如果訂購了相同料號的多重數量，或目錄中顯示含稅價格，則可能會導致舍入問題。 在這種情況下，總數量可能會分成兩行，但數量會等於訂購的料號總計。

> 商戶儀表板檢視中具有舍入問題的明細行專案範例

![行專案檢視](assets/line-items-example.png){width="600" zoomable="yes"}

+++Adobe Commerce如何計算行專案中的舍入問題

[!DNL Payment Services]的行專案會平衡此舍入問題，因此`unit_amount`或`unit_tax`值與訂單的總金額相對應。 料號可以分割成兩個明細行，以解決此舍入問題：

* 當舍入問題出現在`unit_amount`上時，商家應該會看到此額外明細行的價格差異。
* 當舍入問題出現在`unit_tax`上時，個別行專案上不會顯示差異，因為`tax`未顯示在網格中，但只顯示在底部的總計。

+++
