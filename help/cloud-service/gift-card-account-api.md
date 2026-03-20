---
title: 禮卡帳戶REST端點
description: 瞭解如何使用禮卡帳戶REST API，以程式設計方式在 [!DNL Adobe Commerce as a Cloud Service]中建立、更新、刪除和查詢禮卡帳戶。
role: Admin, Developer
level: Experienced
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案（Adobe管理的SaaS基礎結構）。"
source-git-commit: 160180d9d779514f6faee3c7de46531ebf191c7d
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 0%

---

# 禮卡帳戶API

{{accs-sandbox-experimental}}

禮卡帳戶REST端點可在帳戶層級（而非購物車或報價層級）提供禮卡帳戶的程式化管理。 使用此API來建立、擷取、更新和刪除禮卡帳戶，或透過JSON匯入端點大量布建禮卡帳戶。

這些端點專為：

* 管理員管理禮卡方案
* 從外部系統（例如ERP、CRM和行銷平台）提供禮品卡的協力廠商整合
* 大量禮卡建立的自動化工作流程

## Authentication

所有端點都需要管理員或整合持有人權杖。 權杖必須與包含`Magento_GiftCardAccount::giftcardaccount`存取控制清單(ACL)資源的角色相關聯。

對於大量匯入作業，角色也必須包含`Magento_ImportExport::import_api` ACL資源。

## 網站和商店內容

網站和商店檢視值是從HTTP要求標題解析，而不是從要求內文解析。 傳遞下列其中一個標頭給每個請求：

* `Store: <store_view_code>`
* `Magento-Website-Code: <website_code>`

API會自動從這些標題解析網站。 請勿在REST要求裝載中包含`website_id`。

>[!NOTE]
>
>大量匯入端點是一個例外狀況。 由於匯入作業大量進行，且可能以特定網站為目標，因此匯入裝載中的每一列都需要明確的`website_id`值。

## REST API參考

API在`/V1/giftcardaccounts`底下公開下列作業，全部由`Magento_GiftCardAccount::giftcardaccount` ACL資源保護：

| 方法 | URL | 說明 |
|--------|-----|-------------|
| POST | `/rest/V1/giftcardaccounts` | 建立禮品卡帳戶 |
| GET | `/rest/V1/giftcardaccounts` | 列出帳戶（支援searchCriteria） |
| GET | `/rest/V1/giftcardaccounts/:id` | 依ID取得帳戶 |
| GET | `/rest/V1/giftcardaccounts/code/:code` | 依程式碼取得帳戶 |
| PUT | `/rest/V1/giftcardaccounts/:id` | 更新帳戶（合併語意） |
| DELETE | `/rest/V1/giftcardaccounts/:id` | 刪除帳戶 |

### 欄位參考

| 欄位 | 型別 | 有效值 | REST建立 | 匯入 |
|---|---|---|---|---|
| `code` | 字串 | 最多255個字元 | 必填 | 必填 |
| `balance` | 浮點數 | >= 0 | 必填 | 必填 |
| `status` | int | `0` （已停用），`1` （已啟用） | 選擇性，預設為`1` | 選擇性，預設為`1` |
| `state` | int | `0` （可用）、`1` （已使用）、`2` （已兌換）、`3` （已過期） | 選擇性，預設為`0` | 選擇性，預設為`0` |
| `is_redeemable` | int | `0`或`1` | 選擇性，預設為`1` | 選擇性，預設為`1` |
| `date_expires` | 字串 | `YYYY-MM-DD`或null | 可選 | 可選 |
| `date_created` | 字串 | `YYYY-MM-DD` | 自動設定 | 選填，若省略則自動設定 |
| `website_id` | int | 有效的網站ID | 不接受（從標題自動解析） | 必填 |

### 建立禮品卡帳戶

建立具有重複代碼偵測的新禮品卡帳戶。

| 專案 | 值 |
|---|---|
| **方法** | `POST` |
| **URL** | `/V1/giftcardaccounts` |

**要求內文：**

```json
{
  "giftcardAccount": {
    "code": "GIFT-1234-ABCD",
    "balance": 100.00,
    "status": 1,
    "state": 0,
    "is_redeemable": 1,
    "date_expires": "2027-12-31"
  }
}
```

**回應(200)：**

```json
{
  "account_id": 42,
  "code": "GIFT-1234-ABCD",
  "balance": 100,
  "status": 1,
  "state": 0,
  "is_redeemable": 1,
  "date_expires": "2027-12-31",
  "date_created": "2026-03-12"
}
```

### 依ID擷取禮卡帳戶

| 專案 | 值 |
|---|---|
| **方法** | `GET` |
| **URL** | `/V1/giftcardaccounts/:id` |

**回應(200)：**

傳回單一禮品卡帳戶物件。

### 依代碼擷取禮品卡帳戶

| 專案 | 值 |
|---|---|
| **方法** | `GET` |
| **URL** | `/V1/giftcardaccounts/code/:code` |

>[!IMPORTANT]
>
>如果禮卡代碼是純數值（例如，`12345`），則對`/V1/giftcardaccounts/12345`的請求符合ID路由，而不是代碼路由。 當程式碼可以是數值時，請一律使用`/V1/giftcardaccounts/code/12345`進行程式碼型查詢。

**回應(200)：**

傳回單一禮品卡帳戶物件。

### 列出具有搜尋條件的禮品卡帳戶

| 專案 | 值 |
|---|---|
| **方法** | `GET` |
| **URL** | `/V1/giftcardaccounts` |

以查詢引數的形式傳遞搜尋條件。 下列範例會傳回`status`等於`1` （已啟用）的禮品卡帳戶：

```text
GET /V1/giftcardaccounts?searchCriteria[filterGroups][0][filters][0][field]=status&searchCriteria[filterGroups][0][filters][0][value]=1&searchCriteria[pageSize]=10&searchCriteria[currentPage]=1
```

**回應(200)：**

```json
{
  "items": [
    {
      "account_id": 42,
      "code": "GIFT-1234-ABCD",
      "balance": 100,
      "status": 1,
      "state": 0,
      "is_redeemable": 1,
      "date_expires": "2027-12-31",
      "date_created": "2026-03-12"
    }
  ],
  "search_criteria": { ... },
  "total_count": 1
}
```

### 更新禮品卡帳戶

使用合併語意更新現有的禮品卡帳戶。 僅套用請求中的非空欄位。 `code`欄位不可修改。 傳遞不同的程式碼會傳回驗證錯誤。

| 專案 | 值 |
|---|---|
| **方法** | `PUT` |
| **URL** | `/V1/giftcardaccounts/:id` |

**要求內文：**

```json
{
  "giftcardAccount": {
    "balance": 75.00,
    "status": 1
  }
}
```

**回應(200)：**

傳回更新的禮品卡帳戶物件。

### 刪除禮品卡帳戶

| 專案 | 值 |
|---|---|
| **方法** | `DELETE` |
| **URL** | `/V1/giftcardaccounts/:id` |

**回應(200)：**

```json
true
```

## 透過JSON大量匯入

可以使用實體型別為`POST /V1/import/json`的`giftcardaccount`大量布建禮品卡帳戶。 除了禮品卡帳戶ACL之外，此端點還需要`Magento_ImportJsonApi::import_api`存取控制清單(ACL)資源。

### 支援的行為

| 行為 | 說明 |
|---|---|
| `append` | 建立新的禮品卡帳戶。 如果程式碼已存在，該列會失敗，而匯入會繼續其餘列。 |
| `replace` | 依代碼更新及插入禮品卡帳戶。 如果代碼不存在，則建立帳戶，如果代碼不存在，則取代帳戶。 |
| `delete` | 依代碼移除禮品卡帳戶。 |

### 請求範例

```json
{
  "source": {
    "entity": "giftcardaccount",
    "behavior": "append",
    "validation_strategy": "validation-stop-on-errors",
    "allowed_error_count": "10",
    "items": [
      {
        "code": "BULK-001",
        "balance": 50.00,
        "website_id": 1,
        "status": 1,
        "state": 0,
        "is_redeemable": 1,
        "date_expires": "2027-06-30"
      },
      {
        "code": "BULK-002",
        "balance": 25.00,
        "website_id": 1
      }
    ]
  }
}
```

### 匯入行為詳細資料

* 匯入承載中的每一列都需要明確的`website_id`，這與REST端點從要求標題推斷網站不同。
* 每一列會分別驗證。 無效列會產生每列錯誤，而不會影響相同批次中的有效列。
* 偵測到相同批次中的重複程式碼，並將其報告為每列錯誤，而非導致交易回覆。
* 直接將寫入資料匯入資料庫以取得效能，並略過廠商模型的儲存生命週期。 匯入期間不會建立餘額變更歷史記錄專案。
* REST建立作業會拒絕過去的到期日。 匯入依設計接受過期的日期，以支援歷史資料移轉。

## 錯誤處理

API會傳回標準HTTP狀態代碼：

| 狀態代碼 | 條件 |
|---|---|
| `400` | 驗證錯誤。 遺失必要欄位、無效值或REST建立時的過期日期。 |
| `401` | 缺少持有人權杖或持有人權杖無效。 |
| `403` | 權杖缺少必要的ACL資源。 |
| `404` | 找不到禮品卡帳戶。 |
| `409` | 禮品卡代碼重複。 |

輸入驗證涵蓋必要欄位、值範圍（狀態必須為`0`或`1`、狀態必須為`0`-`3`、餘額必須為非負數）、日期格式以及型別安全性。 數值欄位的非數值會遭到拒絕。
