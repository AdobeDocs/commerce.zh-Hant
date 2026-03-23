---
title: 以客戶身分登入，並提供一次性代碼
description: 瞭解如何使用「以客戶OTC身分登入」功能來產生 [!DNL Adobe Commerce as a Cloud Service]中客戶驗證的一次性代碼。
role: Admin
level: Intermediate
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案（Adobe管理的SaaS基礎結構）。"
source-git-commit: 2de1006ad3cee936d114bcf1b9a98b43a54d8c76
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 0%

---

# 客戶登入

{{accs-sandbox-experimental}}

以客戶OTC身分登入（一次性代碼）功能可讓管理員使用者為客戶產生短暫的單次使用代碼。 您可以透過GraphQL交換此程式碼以換取客戶存取權杖，讓無密碼的&#x200B;**登入成為銷售商協助購物情境的客戶**&#x200B;工作流程。

以客戶身分登入是由下列元件組成：

* **管理員UI** — 在客戶編輯頁面上，管理員可以要求一次性代碼(OTC)，而非以客戶身分直接登入。
* **REST API** - OTC產生的程式化端點，適用於管理指令碼和協力廠商整合。
* **GraphQL API** — 將OTC交換為店面或Headless商務流程的客戶存取權杖的變動。

## 從管理員產生一次性代碼

以Customer OTC登入將客戶編輯頁面上的標準登入方式按鈕取代為&#x200B;[!UICONTROL **取得客戶登入OTC**]&#x200B;按鈕。 然後，產生的一次性程式碼便可與店面或GraphQL搭配使用，以進行賣家輔助購物。

>[!NOTE]
>
>「訂單」、「發票」、「出貨」及「銷退折讓單」頁面上無法使用&#x200B;**以客戶身分登入**&#x200B;按鈕。

### 先決條件

您必須符合下列要求才能使用登入作為客戶功能：

* **管理員許可權** — 管理員使用者必須在其管理員角色中啟用`Magento_LoginAsCustomer::login`存取控制清單(ACL)許可權，才能以客戶身分登入。

* **客戶同意** — 客戶必須將`login_as_customer_assistance_allowed`擴充功能屬性設為&#x200B;**2**。 這可以在Admin的&#x200B;**編輯客戶**&#x200B;頁面上設定，或是在建立或編輯客戶時透過GraphQL設定。

  ![編輯客戶頁面上的客戶同意延伸屬性設定](./assets/customer-consent-attribute.png){width="600" zoomable="yes"}

* **啟用以客戶擴充功能登入** — 停用以客戶擴充功能登入時，將無法使用以客戶擴充功能登入。 若要確認擴充功能已啟用，請瀏覽至&#x200B;[!UICONTROL **商店**] > [!UICONTROL **組態**] > [!UICONTROL **客戶**] > [!UICONTROL **以客戶身分登入**] > [!UICONTROL **啟用擴充功能**]。

### 要求一次性代碼(OTC)

1. 導覽至&#x200B;[!UICONTROL **客戶**]，並選取要開啟編輯頁面的客戶。

1. 在[編輯客戶]頁面上，按一下[取得客戶登入OTC] [!UICONTROL **。**]

   在[編輯客戶]頁面上![取得客戶登入OTC按鈕](./assets/get-customer-login-otc-button.png){width="600" zoomable="yes"}

1. 輸入&#x200B;[!UICONTROL **原因**] （必要）並按一下&#x200B;[!UICONTROL **要求**]。

   ![原因欄位為](./assets/otc-reason-modal.png){width="600" zoomable="yes"}的OTC要求模組

   >[!NOTE]
   >
   >**原因**&#x200B;欄位為必填。 它會傳遞給OTP產生流程，並保留用於即將推出的稽核和事件日誌功能。

1. 產生的OTC會顯示在強制回應視窗中。 使用此程式碼搭配`generateCustomerToken`或`exchangeOtpForCustomerToken` GraphQL突變以取得客戶授權。

   ![已產生的OTC顯示在強制回應視窗中](./assets/otc-generated-code.png){width="300" zoomable="yes"}

>[!IMPORTANT]
>
>根據預設，所產生的一次性程式碼OTC的有效期限為30秒，且僅使用一次即可失效。 可透過提交[支援票證](https://experienceleague.adobe.com/home?lang=zh-Hant&support-tab=home#support)來設定TTL。

產生一次性程式碼後，您可以導覽至您的店面並使用以下憑證登入，以使用它：

* **電子郵件**：客戶的電子郵件地址
* **密碼**：產生的一次性代碼(OTC)

## 使用REST API產生一次性程式碼

POST `V1/customer/:customerId/otp`端點提供程式化方式為客戶產生OTC。 這對於需要持續觸發OTC發行的管理員UI、指令碼或協力廠商整合非常有用。

### REST合約

| 專案 | 值 |
|---|---|
| **方法** | POST |
| **URL** | `/rest/V1/customer/:customerId/otp` |
| **驗證** | 管理權杖（持有人）。 必要的ACL： `Magento_LoginAsCustomer::login`。 |
| **要求內文** | 包含選擇性`reason`欄位的JSON。 用於稽核和記錄。 |
| **成功回應** | HTTP 200、具有`otp`的JSON （32個字元的十六進位字串）。 |
| **錯誤回應** | 標準Web API錯誤（例如401、403）。 如果客戶的客戶協助登入功能遭停用，可能會顯示為500或對應的例外狀況。 |

### 請求範例

```text
POST /rest/V1/customer/:customerId/otp
Content-Type: application/json
```

```json
{"reason": "Support session"}
```

### 回應範例

```json
{"otp": "a1b2c3d4e5f6789012345678abcdef01"}
```

## 使用GraphQL交換客戶權杖的一次性程式碼

產生OTC （從Admin UI或REST API）後，使用下列GraphQL變動之一將其交換為客戶存取權杖。

### `generateCustomerToken`突變

`generateCustomerToken(email, password)`突變傳回客戶權杖。 `password`引數的評估順序如下：

1. **客戶密碼（預設）** — 客戶的帳戶密碼。
1. **客戶重設密碼權杖（一次使用）** - **忘記密碼**&#x200B;中的有效權杖（例如，`requestPasswordResetEmail`突變）。 在首次使用時消耗。
1. **管理員產生的OTC （一次性代碼）** — 管理員透過REST API或管理員UI為客戶產生的代碼。 單次使用、短期（預設為30秒）。

**結構描述：**

```graphql
type Mutation {
  generateCustomerToken(email: String!, password: String!): CustomerToken
}

type CustomerToken {
  token: String!
}
```

**範例：使用管理員OTC登入**

```graphql
mutation GenerateCustomerToken($email: String!, $password: String!) {
  generateCustomerToken(email: $email, password: $password) {
    token
  }
}
```

變數（使用OTC作為`password`）：

```json
{
  "email": "customer@example.com",
  "password": "<admin-generated-OTC>"
}
```

**範例：使用密碼登入**

```graphql
mutation GenerateCustomerToken($email: String!, $password: String!) {
  generateCustomerToken(email: $email, password: $password) {
    token
  }
}
```

變數：

```json
{
  "email": "customer@example.com",
  "password": "CustomerPassword123"
}
```

**範例：使用密碼重設權杖登入**

客戶要求重設密碼後（例如，`requestPasswordResetEmail`），透過電子郵件連結收到的重設權杖可在`password` （一次性使用）中當作`generateCustomerToken`。

```graphql
mutation GenerateCustomerToken($email: String!, $password: String!) {
  generateCustomerToken(email: $email, password: $password) {
    token
  }
}
```

變數（使用重設權杖做為`password`）：

```json
{
  "email": "customer@example.com",
  "password": "<reset-password-token-from-email-link>"
}
```

**範例回應：**

```json
{
  "data": {
    "generateCustomerToken": {
      "token": "<customer-access-token>"
    }
  }
}
```

### `exchangeOtpForCustomerToken`突變

`exchangeOtpForCustomerToken`突變會將管理員產生的密碼重設權杖或OTP交換給客戶存取權杖。 成功交換（一次性使用）後，OTP會失效。 此端點遵循reCAPTCHA設定。

**結構描述：**

```graphql
type Mutation {
  exchangeOtpForCustomerToken(
    email: String!
    otp: String!
  ): CustomerToken
}

type CustomerToken {
  token: String!
}
```

**範例要求：**

```graphql
mutation ExchangeOtpForCustomerToken($email: String!, $otp: String!) {
  exchangeOtpForCustomerToken(email: $email, otp: $otp) {
    token
  }
}
```

變數：

```json
{
  "email": "customer@example.com",
  "otp": "<one-time-password>"
}
```

**範例回應：**

```json
{
  "data": {
    "exchangeOtpForCustomerToken": {
      "token": "<customer-access-token>"
    }
  }
}
```

### 突變摘要

| 突變 | 使用案例 |
|---|---|
| `generateCustomerToken(email, password)` | 單一進入點：客戶密碼、密碼重設權杖、Admin OTC或OTP （在密碼/重設後嘗試）。 |
| `exchangeOtpForCustomerToken(email, otp)` | OTP或重設密碼權杖交換。 OTP （或重設密碼權杖）在使用後消耗。 |

密碼重設Token和Admin OTC都作為`password`引數傳遞給`generateCustomerToken`。 解析程式會偵測權杖型別並據此進行驗證。
