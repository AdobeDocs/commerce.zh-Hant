---
title: 透過REST觸發的電子郵件
description: 瞭解如何使用REST API，透過指定 [!DNL Adobe Commerce as a Cloud Service]的範本ID、收件者電子郵件和範本變數，隨選觸發異動電子郵件。
role: Admin
level: Experienced
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案（Adobe管理的SaaS基礎結構）。"
source-git-commit: 9661e368f7a0dc85edcd3e52a67ae2a98355d8b5
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 0%

---

# 透過REST API觸發的電子郵件

之前，您只能在事件觸發時傳送電子郵件，例如在客戶註冊或訂單購買期間。 在[!DNL Adobe Commerce as a Cloud Service]中，您可以指定範本ID、收件者電子郵件和範本變數，以透過REST API隨選傳送電子郵件。

>[!NOTE]
>
>目前，僅能傳送新建立的自訂範本。 不支援預先定義的和系統範本。

`V1/custom-email/send`端點可讓&#x200B;**協力廠商系統** （例如整合和外部服務）透過指定以下專案來隨選傳送電子郵件：

- **範本識別碼** — 電子郵件範本識別碼。
- **收件者電子郵件** — 此請求的目標電子郵件地址。
- **變數** - （選用）要插入範本的自訂已定義機碼值組，例如`customer_name`或`order_id`。

>[!NOTE]
>
>使用目前的存放區範圍和預設的&#x200B;**寄件者**&#x200B;電子郵件地址或範本定義的電子郵件地址，同步傳送電子郵件。

## REST合約

下節說明如何使用REST API隨選傳送異動電子郵件。

### 端點

- **URL** - `POST /rest/V1/custom-email/send`
- **授權** — 僅支援&#x200B;**服務對服務IMS授權**。 呼叫者必須能存取&#x200B;**透過API** (`Magento_CustomEmailSend::send_custom_email`)資源傳送自訂電子郵件。 如需詳細資訊，請參閱[REST驗證](https://developer.adobe.com/commerce/webapi/rest/authentication/)。
- **非同步使用方式** （建議） — 雖然此端點已同步實作，我們建議您使用&#x200B;**非同步REST API**&#x200B;呼叫它，讓使用者將要求排入佇列並處理，以避免長期HTTP連線。 在[!DNL Adobe Commerce as a Cloud Service]中，您可以在`/async`之後使用`V1`路由，例如： `POST https://<server>.api.commerce.adobe.com/<tenant-id>/V1/async/custom-email/send`。

  如需詳細資訊，請參考[非同步Web端點(SaaS)](https://developer.adobe.com/commerce/webapi/rest/use-rest/asynchronous-web-endpoints/)。

### 要求內文

- **templateId** （interger，必要） — 系統管理員在&#x200B;[!UICONTROL **行銷**] > [!UICONTROL _通訊_] > [!UICONTROL **電子郵件範本**]&#x200B;下定義的電子郵件範本ID。

- **recipientEmail** （字串，必要） — 目標電子郵件地址。 必須為有效的電子郵件格式。 缺少或空白值會觸發驗證錯誤。
- **變數** （物件，選擇性） — 以`UnstructuredArray`形式插入範本的機碼值對應。

  如果您未使用變數，請傳遞空白物件或忽略它。 在電子郵件範本內文和主旨中，使用變數語法來參考變數，例如`var order_id`。 主旨也支援在[支援的範本案例](#supported-template-scenarios)中說明的相同自訂變數和語法。

### 成功回應(HTTP 200)

成功傳送時API會傳回HTTP 200。

### 錯誤回應

- **HTTP 400 — 驗證錯誤**

  整合必須為每個要求提供有效的`templateId`和`recipientEmail`。

   - `"message": "Invalid recipient email format"` — 無效的或格式錯誤的收件者地址
   - `"message": "Recipient email is required."` — 遺失或空白`recipientEmail`
   - `"message": "Template ID must be a positive integer."` — 遺失、零或無效的`templateId`

- **HTTP 404 — 找不到範本**

  範例： `"message": "Email template with ID \"999\" does not exist."`

## 支援的範本案例

**電子郵件內文**&#x200B;和&#x200B;**範本主旨**&#x200B;皆支援下列範本功能：

>[!NOTE]
>
>範本主旨也支援自訂變數。 使用`var variableName`和其他語法，如下節所述。

- **包含指示詞** — 包含其他設計範本，例如電子郵件標頭。

  ```javascript
  {{template config_path="design/email/header_template"}}
  ```

- **簡單變數** — 使用`var variableName`，例如`var order_id`或`var g`。

  ```javascript
  {{var order.test}}
  {{var g}}
  {{var order_id}}
  ```

- **巢狀/點標籤法** — 對於在請求`variables`中傳遞的巢狀金鑰，在翻譯中使用以美元為前置詞的名稱，例如`$order_data.customer_name`、`$order.increment_id`或`$order_data.frontend_status_label`。

  ```javascript
  {{trans "%name," name=$order_data.customer_name}}
  {{trans "Your order #%increment_id has been updated with a status of **%order_status**." increment_id=$order.increment_id order_status=$order_data.frontend_status_label |raw}}
  ```

- **翻譯(trans)** — 引數化文字、具有多個預留位置的多行翻譯和HTML標籤。

  ```javascript
  {{trans "%name," name=$order_data.customer_name}}
  {{trans "Your order #%increment_id has been updated with a status of **%order_status**." increment_id=$order.increment_id order_status=$order_data.frontend_status_label |raw}}
  ```

- **原始輸出** — 當翻譯或變數內容包含HTML （例如`|raw`或`<strong>`）時，請使用`<a>`篩選器。

  ```javascript
  {{trans "Your order #%increment_id has been updated with a status of **%order_status**." increment_id=$order.increment_id order_status=$order_data.frontend_status_label |raw}}
  ```

- **URL協助程式** — 用於儲存翻譯內的URL。

  ```javascript
  {{trans 'You can check the status of your order by [logging into your account](%account_url).' account_url=$this.getUrl($store,'customer/account/',[_nosid:1]) |raw}}
  ```
