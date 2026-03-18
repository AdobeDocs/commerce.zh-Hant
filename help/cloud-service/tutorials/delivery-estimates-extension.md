---
title: 傳遞估計擴充功能教學課程
description: 瞭解如何使用App Builder、Edge Delivery Services和AI輔助開發工具，為Adobe Commerce as a Cloud Service建立傳遞日期估計擴充功能。
solution: Commerce
feature: App Builder, Cloud
feature-set: Commerce
role: Developer
level: Intermediate
type: Tutorial
hide: true
hidefromtoc: true
source-git-commit: 3fc8982613df7b1155cdfb08ac4b56de6d1ce4f6
workflow-type: tm+mt
source-wordcount: '3334'
ht-degree: 0%

---

# 傳遞估計擴充功能教學課程

本教學課程會使用[!DNL Adobe Commerce as a Cloud Service]、[!DNL Adobe App Builder]和AI輔助開發工具，引導您建立[!DNL Edge Delivery Services]的傳遞日期估計延伸。 此擴充功能會從外部API擷取運送時間和運送日期的預估值，並在整個店面顯示。

您建置兩個部分：

- **App Builder擴充功能** — 封裝外部傳遞預估API的後端對前端(BFF)動作、在結帳時提供包含傳遞日期的豐富送貨方法的webhook，以及管理設定而不需重新部署的管理UI設定頁面。
- **Storefront整合** — 傳遞日期估計顯示在產品詳細資料頁面(PDP)、購物車頁面，以及使用[!DNL Edge Delivery Services]下拉式元件和共用使用者端模組的結帳頁面。

>[!NOTE]
>
>AI代理程式是不確定的。 本教學課程中的提示、問題和輸出為範例。 您的代理程式可能會產生不同的問題、需求或架構提案。 使用本教學課程中的範例，引導代理程式取得類似結果。

開始之前，請先完成[必要條件](./tutorial-prerequisites.md)。 此教學課程使用&#x200B;**結帳入門套件**。 確認您已複製該檔案，並完成必要條件頁面上所述的設定步驟。

## 驗證先決條件

確認已安裝下列先決條件：

```bash
# Check Node.js version (should be 22.x.x)
node --version

# Check npm version (should be 9.0.0 or higher)
npm --version

# Check Git installation
git --version

# Check Bash shell installation
bash --version
```

如果上述任何命令未傳回預期的結果，請參閱[必要條件](./tutorial-prerequisites.md)以取得指引。

此外，請確認下列專案：

- 您有一個包含產品資料的[!DNL Adobe Commerce as a Cloud Service]執行個體。 請參閱[Commerce Cloud服務執行個體](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/overview){target="_blank"}。
- 您有一個店面專案連線到您的[!DNL Commerce]執行個體。 如果沒有店面，請依照[建立店面](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/){target="_blank"}中的步驟操作。
- 已安裝`aem` CLI：

  ```bash
  npm install -g @adobe/aem-cli
  ```

- 您有&#x200B;**購物者帳戶** — [!DNL Commerce]中的註冊客戶，其預設送貨地址已儲存。 PDP和購物車頁面上的估計傳送次數只會顯示給已登入的購物者。 結帳會顯示所有購物者的預估值（無論驗證狀態為何）。

>[!IMPORTANT]
>
>此教學課程使用&#x200B;**結帳入門套件** （不是整合入門套件）。 Checkout Starter Kit為付款、運送、稅金和活動提供以webhook為基礎的擴充功能。 請確定您是從簽出套件啟動。

## 設定模擬傳遞預估API

此擴充功能會呼叫外部傳遞估算API，以取得運送日期和時間估算。 在本教學課程中，您會使用模擬API，這樣就能在不使用真實電信業者帳戶的情況下執行完整流程。 有兩個可用選項：

- **選項A： Pipedream工作流程** — 免費套餐、快速設定，但有每月叫用限制。
- **選項B： App Builder執行階段動作** — 沒有在後端開發步驟中建立的外部相依性。

>[!TIP]
>
>在開發期間，如果您達到任意層級叫用配額，則可以從Pipedream （選項A）開始，然後切換至執行階段動作（選項B）。 這兩個選項都會實作相同的API合約。

### API規格

模型API接受POST請求，並傳回交貨日期預估，包括承運商、運輸天數、截止時間以及最佳預估。

**要求內文** （所有欄位都是模擬的選用欄位）：

```json
{
  "origin": { "country_code": "US", "postal_code": "90210", "city": "Beverly Hills" },
  "destination": { "country_code": "US", "postal_code": "10001", "city": "New York" },
  "ship_date": "2026-03-10",
  "carriers": ["standard", "express"],
  "service_levels": ["standard", "express"]
}
```

**回應(200 OK)：**

```json
{
  "estimates": [
    {
      "carrier_code": "standard",
      "service_code": "ground",
      "delivery_date": "2026-03-14",
      "safe_delivery_date": "2026-03-15",
      "transit_days": 4,
      "cutoff_datetime_utc": "2026-03-10T17:00:00.000Z"
    },
    {
      "carrier_code": "express",
      "service_code": "2day",
      "delivery_date": "2026-03-12",
      "safe_delivery_date": "2026-03-12",
      "transit_days": 2,
      "cutoff_datetime_utc": "2026-03-10T12:00:00.000Z"
    }
  ],
  "best_estimation": { "carrier_code": "express", "delivery_date": "2026-03-12", "transit_days": 2 }
}
```

**錯誤回應：** 401 （遺失/無效的API金鑰）、400 （無效的`ship_date`格式）、503 （模擬的停機時間）。

### 設定模型

>[!BEGINTABS]

>[!TAB Pipedream工作流程]

Pipedream選項使用持有人權杖驗證並接受對工作流程觸發器URL的POST請求。

| 專案 | 說明 |
|------|-------------|
| 基礎URL | 完整的Pipedream工作流程觸發程式URL （例如`https://<id>.m.pipedream.net`） |
| 驗證 | `Authorization: Bearer <API_KEY>` |
| 方法 | POST |

{style="table-layout:auto"}

**建立工作流程：**

1. 在[Pipedream](https://pipedream.com){target="_blank"} (**[!UICONTROL Workflows]** > **[!UICONTROL New Workflow]**)中建立新的工作流程。

1. 新增為POST設定的&#x200B;**HTTP / Webhook**&#x200B;觸發器。 Pipedream會指派webhook URL。

1. 新增&#x200B;**執行Node.js程式碼**&#x200B;步驟，並貼上下列處理常式程式碼：

   ```javascript
   const DEFAULT_CARRIERS = [
     { carrier_code: "standard", service_code: "ground", transit_days: 4 },
     { carrier_code: "express", service_code: "2day", transit_days: 2 },
     { carrier_code: "priority", service_code: "overnight", transit_days: 1 },
   ];
   
   const ISO_DATE = /^\d{4}-\d{2}-\d{2}$/;
   
   function parseShipDate(shipDate) {
     if (shipDate == null || typeof shipDate !== "string") return null;
     if (!ISO_DATE.test(shipDate)) return null;
     const d = new Date(shipDate + "T12:00:00.000Z");
     if (Number.isNaN(d.getTime())) return null;
     return shipDate;
   }
   
   function addBusinessDays(isoDate, days) {
     const d = new Date(isoDate + "T12:00:00.000Z");
     let added = 0;
     while (added < days) {
       d.setUTCDate(d.getUTCDate() + 1);
       const dow = d.getUTCDay();
       if (dow !== 0 && dow !== 6) added += 1;
     }
     return d.toISOString().slice(0, 10);
   }
   
   function cutoffUtc(isoDate, hour = 17) {
     return `${isoDate}T${String(hour).padStart(2, "0")}:00:00.000Z`;
   }
   
   function getBearerToken(headers) {
     const auth = headers?.Authorization ?? headers?.authorization ?? "";
     if (typeof auth !== "string" || !auth.startsWith("Bearer ")) return null;
     return auth.slice(7).trim() || null;
   }
   
   function handleDeliveryEstimate(body) {
     const shipDate = parseShipDate(body?.ship_date);
     const baseDate = shipDate ?? new Date().toISOString().slice(0, 10);
     let carriers = DEFAULT_CARRIERS;
     if (Array.isArray(body?.carriers) && body.carriers.length > 0) {
       const set = new Set(body.carriers.map((c) => String(c).toLowerCase()));
       carriers = DEFAULT_CARRIERS.filter((c) => set.has(c.carrier_code.toLowerCase()));
     }
     if (Array.isArray(body?.service_levels) && body.service_levels.length > 0) {
       const set = new Set(body.service_levels.map((s) => String(s).toLowerCase()));
       carriers = carriers.filter(
         (c) => set.has(c.service_code.toLowerCase()) || set.has(c.carrier_code.toLowerCase())
       );
     }
     if (carriers.length === 0) {
       return { status: 200, body: { estimates: [], best_estimation: null } };
     }
     const estimates = carriers.map((c) => {
       const delivery_date = addBusinessDays(baseDate, c.transit_days);
       const safe_delivery_date = addBusinessDays(baseDate, c.transit_days + 1);
       const cutoff_datetime_utc = cutoffUtc(baseDate, 17 - c.transit_days);
       return {
         carrier_code: c.carrier_code,
         service_code: c.service_code,
         delivery_date,
         safe_delivery_date,
         transit_days: c.transit_days,
         cutoff_datetime_utc,
       };
     });
     return { status: 200, body: { estimates, best_estimation: estimates[0] } };
   }
   
   export default defineComponent({
     async run({ steps, $ }) {
       const event = steps.trigger?.event ?? steps.trigger ?? {};
       const body = event.body ?? {};
       const headers = event.headers ?? {};
       const auth = getBearerToken(headers);
       const expectedKey =
         (typeof process.env.MOCK_API_KEY === "string" && process.env.MOCK_API_KEY.trim()) || null;
       if (expectedKey && (!auth || auth !== expectedKey)) {
         await $.respond({
           immediate: true,
           status: 401,
           headers: { "Content-Type": "application/json" },
           body: { error: "unauthorized", message: "Missing or invalid API key." },
         });
         return;
       }
       if (body?.ship_date != null && !parseShipDate(body.ship_date)) {
         await $.respond({
           immediate: true,
           status: 400,
           headers: { "Content-Type": "application/json" },
           body: { error: "bad_request", message: "Invalid ship_date; use YYYY-MM-DD." },
         });
         return;
       }
       const { status, body: responseBody } = handleDeliveryEstimate(body);
       await $.respond({
         immediate: true,
         status,
         headers: { "Content-Type": "application/json" },
         body: responseBody,
       });
     },
   });
   ```

1. （選用）在工作流程設定中新增`MOCK_API_KEY`環境變數，以強制執行持有人權杖驗證。 如果未設定，則會接受任何要求。

1. 部署工作流程。

   您的端點是webhook觸發程式URL。

**測試模型：**

```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer mock-api-key" \
  -d '{"destination": {"country_code": "US", "postal_code": "10001"}}' \
  "https://<your-endpoint>.m.pipedream.net"
```

>[!TAB App Builder執行階段動作]

App Builder Runtime動作選項會將模型部署為相同[!DNL App Builder]專案內的Runtime動作。 此方法沒有外部相依性和引動配額。

提示代理程式建立模擬動作：

```shell-session
Add a new runtime action to this project that implements the API in @docs/PIPEDREAM_API_SPEC.md
- Add it to a separate package
- Use the code in docs/pipedream as inspiration
```

代理程式使用與Pipedream選項相同的API合約建立`actions/mock-delivery-api/index.js`。 部署後，端點會是：

```shell-session
https://<namespace>.adobeioruntime.net/api/v1/web/mock-delivery-api/delivery-estimate
```

已根據`MOCK_API_KEY`中的`.env`環境變數驗證驗證。

>[!ENDTABS]

## 擴充功能開發

本節將引導您開發傳遞估計擴充功能的[!DNL App Builder]後端。 後端提供三個動作：

| 動作 | 型別 | 用途 |
|--------|------|---------|
| `delivery-estimates` | 獨立Web動作 | 店面的BFF — 針對傳送日期，PDP和購物車會呼叫此專案 |
| `shipping-methods` | Webhook動作 | 在結帳時於`additional_data`內提供運送費率 |
| `delivery-estimates-config` | 管理員後端動作 | 儲存在`aio-lib-state`中之設定的CRUD |

{style="table-layout:auto"}

1. 從編碼代理程式中的MCP設定中，確認`commerce-extensibility`工具集已啟用且沒有錯誤。

   例如，在游標中，移至&#x200B;**[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**。

   如果您看到錯誤，請關閉和開啟工具集。

   >[!NOTE]
   >
   >使用AI輔助開發工具時，代理程式產生的程式碼和回應會有自然變化。
   >如果您遇到任何程式碼問題，請要求代理程式協助您進行偵錯。

1. 如果您有任何檔案新增到Cursor的內容中，請將其停用。

   導覽至「**[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Indexing & Docs]**」並刪除任何列出的檔案。

### 步驟1：提供初始提示

為代理程式提供上下文的外部API規格，並提示其開始。 告訴代理程式停止並詢問問題，可協助您及早掌控實施方向。

在代理程式的聊天視窗中輸入下列提示：

```shell-session
I want to build an Adobe App Builder extension that extends the checkout with shipping date and time estimates taken from an external API described in @docs/API_SPEC.md.
Delivery dates for a product will be shown in the product details page and on the cart page.
Implement this feature by using the skills in this workspace for backend code, and a separate workspace with storefront skills. For this extension, focus on the backend skills and create an API_SPEC to hand work over to the storefront skills.

STOP and ask me clarifying questions about the requirements before you do any work.
```

>[!TIP]
>
>在提示中參考外部API規格檔案(`@docs/API_SPEC.md`)可提供代理程式有關第三方API合約的具體內容。 代理程式會使用它來設計BFF動作、共用的HTTP使用者端和管理員UI設定欄位。 告訴代理程式STOP並詢問問題，會觸發引導式工作流程，並幫助您及早掌控實施方向。

### 步驟2：回答代理程式的問題

代理程式返回時會提出一系列澄清問題，涵蓋例如目標環境（PaaS與SaaS）、範圍（獨立BFF動作、webhook擴充或兩者）、來源位址來源、快取策略和測試偏好設定等主題。 下列範例顯示典型的問題和答案。 您的代理可能會問不同的問題，但主題通常相同。

**代理程式問題範例：**

1. **目標環境** — 您是針對PaaS （內部部署）或SaaS (Adobe Commerce as a Cloud Service)建置嗎？
2. **範圍** — 這應該是一個獨立的BFF動作（店面會直接呼叫它）、webhook擴充（結帳時擴充送貨方法），或兩者皆是？
3. **管理員可設定性** — 是否應透過Commerce Admin設定API URL、API金鑰和來源位址等設定，或將其儲存在`.env`？
4. **來源地址** — 出貨地點（倉儲）地址來自何處？ 應該是靜態設定還是動態解析？
5. **快取** — 是否應在伺服器端快取傳遞預估，以減少對外部API的呼叫？ 如果是，什麼TTL？

**範例答案：**

```shell-session
Clarifications:
1. Let's build for SaaS
2. Let's do this:
(A) Can the PDP/cart call the 3rd party API directly — or are there any benefits of wrapping this call with a runtime action?
(B) Let's use the shipping-methods webhook
3. Let's use a Single-page application (SPA) that uses the Admin UI SDK to integrate with the admin. Since we are adding this config screen, let's make anything else that makes sense configurable to avoid redeployments when changing settings
4. Static configuration — origin address should be configurable in the Admin UI (e.g. warehouse address)
5. Yes, cache on the server side; suggest a TTL (e.g. 30 minutes) and make it configurable in the Admin UI
```

>[!TIP]
>
>詢問代理程式店面應該直接呼叫第三方API還是執行階段動作，會觸發有用的架構討論。 代理程式會說明BFF （前端後端）模式的好處：API金鑰會保留在伺服器端、CORS會處理、快取會集中處理，而且您會取得廠商摘要。 詢問管理員UI可設定性會推動代理程式將所有設定儲存在`aio-lib-state`中而非`.env`，如此一來，變更設定時便不會進行重新部署。

>[!NOTE]
>
>您的代理可能會詢問不同的問題。 使用這些答案作為指引，引導代理程式走向相同的功能結果：店面呼叫的BFF動作、擴充結帳的送貨方法webhook，以及儲存`aio-lib-state`中設定的Admin UI設定頁面。

### 步驟3：檢閱需求和架構

代理程式會產生需求和架構檔案，供您檢閱。 確認需求與您提供的答案相符，以及架構涵蓋：

- **BFF動作** (`delivery-estimates`) — 店面從PDP和購物車頁面呼叫的獨立網路動作。 它會從`aio-lib-state`讀取設定、呼叫外部傳遞預估API，並傳回格式化的預估。
- **webhook動作** (`shipping-methods`) — 在結帳期間，透過`additional_data`內的交貨日期來豐富運費。 使用`plugin.out_of_process_shipping_methods.api.shipping_rate_repository.get_rates` webhook方法。
- **管理員設定動作** (`delivery-estimates-config`) — 設定的CRUD （API URL、API金鑰、來源位址、電信業者、快取TTL）儲存在`aio-lib-state`中。
- **共用程式庫** — 外部API的HTTP使用者端和用於讀取及寫入`aio-lib-state`的設定模組。

>[!NOTE]
>
>AI代理是不確定的，其行為會因模型和IDE而異。 您可能會收到一組不同的問題，產生一組不同的需求和架構。 若是如此，請嘗試將代理程式引導至與本教學課程中呈現內容最相符的方向上，然後再繼續。

### 步驟4：選取實作計畫

代理程式可讓您選擇建立詳細的實作計畫或完成直接實作。

- 如果您想要可檢視計畫，而且可以在階段中執行並具有更多控制權的計畫，請選取第一個選項。
- 如果您希望代理程式以最小的介入完成完整實作，請選取第二個選項。

### 步驟5：清理和部署

代理程式完成實作後，就會繼續進行清除。 由於僅使用Shipping網域，代理程式會移除未使用的支架：

- 付款動作與設定(`validate-payment/`， `filter-payment/`， `payment-methods.yaml`)
- 稅捐動作與設定(`collect-taxes/`， `collect-adjustment-taxes/`， `tax-integrations.yaml`)
- 事件動作和設定(`commerce-events/`， `3rd-party-events/`， `events.config.yaml`)
- 通用支架(`generic/`)
- 其他網域的管理員UI SPA元件（例如稅捐相關頁面和鉤點）
- 未使用的指令碼、測試檔案和環境變數

>[!TIP]
>
>要求代理程式也在Admin UI SPA中檢查其他網域的剩餘專案。 起始套件支架中的「稅捐類別」頁面及其鉤點可能仍然存在，需要移除。

清除之後，請依此順序&#x200B;**使用這些步驟**&#x200B;進行部署：

```bash
# 1. Copy env template and fill in credentials.
cp env.dist .env

# 2. Select your App Builder workspace.
aio app use --merge

# 3. Sync OAuth credentials from workspace.
npm run sync-oauth-credentials

# 4. Deploy the extension.
aio app deploy

# 5. Register shipping carriers in Commerce.
npm run create-shipping-carriers
```

>[!IMPORTANT]
>
>請勿略過或重新排序步驟。 步驟1至3是部署的先決條件。 如果未設定認證，`aio app deploy`命令會失敗。

### 步驟6：設定webhook和管理UI

部署後，請設定送貨webhook。 代理程式可建立指令碼並以程式設計方式訂閱：

```bash
npm run subscribe-webhook
```

這個指令會使用下列設定來訂閱送貨webhook：

| 欄位 | 值 |
|-------|-------|
| Webhook方法 | `plugin.out_of_process_shipping_methods.api.shipping_rate_repository.get_rates` |
| Webhook型別 | `after` |
| 必填 | 選擇性（允許遞補為預設送貨） |
| 逾時 | 5000毫秒 |

{style="table-layout:auto"}

>[!NOTE]
>
>若為SaaS，webhook方法名稱會從路徑刪除`magento.`。 PaaS的webhook名稱為`plugin.magento.out_of_process_shipping_methods...`，而SaaS的webhook名稱為`plugin.out_of_process_shipping_methods...`。

接下來，設定管理員UI：

1. 啟用&#x200B;**Admin UI SDK** (**[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL Adobe Services]** > **[!UICONTROL Admin UI SDK]** > **[!UICONTROL Enable]** > **[!UICONTROL Yes]**)。

1. 選取您的[!DNL App Builder]工作區和擴充功能以設定擴充功能。

1. 按一下&#x200B;**[!UICONTROL Refresh registrations]**。

1. 導覽至&#x200B;**[!UICONTROL Apps]**&#x200B;側邊欄中的&#x200B;**[!UICONTROL Delivery Estimates]** > [!DNL Admin]。

1. 啟用功能並指定所需設定（包括API URL和API金鑰、來源位址、預設電信業者、快取TTL和電信業者代碼對應）以完成設定。

### 步驟7：測試擴充

直接測試傳遞估算BFF動作：

```bash
curl -s -X POST \
  -H "Content-Type: application/json" \
  -d '{"destination": {"country_code": "US", "postal_code": "10001"}}' \
  "https://<your-runtime-url>/api/v1/web/commerce-checkout-starter-kit/delivery-estimates" | jq .
```

回應應類似於：

```json
{
  "estimates": [
    {
      "carrier": "standard",
      "service_level": "ground",
      "delivery_date": "2026-03-12",
      "safe_delivery_date": "2026-03-13",
      "transit_days": 4,
      "cutoff_datetime_utc": "2026-03-06T18:00:00Z"
    },
    {
      "carrier": "express",
      "service_level": "2day",
      "delivery_date": "2026-03-10",
      "safe_delivery_date": "2026-03-10",
      "transit_days": 2,
      "cutoff_datetime_utc": "2026-03-06T20:00:00Z"
    }
  ],
  "best_estimation": {
    "carrier": "express",
    "delivery_date": "2026-03-10",
    "transit_days": 2
  }
}
```

### 建立服務合約

現在後端已完成，請要求代理程式建立店面工作的服務合約：

```shell-session
Produce a spec called STOREFRONT_API_SPEC that I can use in the storefront workspace with the corresponding agent. Also give me a prompt that I could use in that workspace.
```

代理程式會產生`docs/STOREFRONT_API_SPEC.md`，其中包含完整的BFF端點合約（要求與回應格式、範例承載、錯誤處理）以及店面工作區的現成提示。

開始店面開發步驟之前，請先將此檔案複製到您的店面專案中。

>[!TIP]
>
>讓代理程式產生另一個工作區的服務合約&#x200B;**和**&#x200B;提示，可確保後端和店面糰隊（或代理程式）之間的乾淨切換。 店面代理程式可以立即開始工作，而不需要詢問有關API的問題。

## 連線到店面

本節將引導您使用[!DNL Edge Delivery Services]和AI輔助開發工具來實作傳遞估計擴充功能的店面部分。 您將傳送日期估計新增到PDP、購物車頁面和結帳頁面。

>[!NOTE]
>
>提供的提示是起點。 雖然您可以在不修改的情況下使用它們，但請考慮與代理進行自然交談。
>
>使用AI輔助開發工具時，代理程式產生的程式碼和回應一律會有自然變異。
>
>如果您遇到任何程式碼問題，請要求代理程式協助您進行偵錯。

### 店面必要條件

開始店面整合之前，請確認您具備下列條件：

- 連線到您[!DNL Commerce]執行個體的店面專案
- 使用CLI安裝的Commerce storefront AI工具[&#128279;](./tutorial-prerequisites.md#install-the-storefront-ai-tools)
- `STOREFRONT_API_SPEC.md`檔案已複製到您的店面專案的`docs/`資料夾

### 步驟1：驗證環境

開啟您的`config.json`檔案，並驗證`commerce-core-endpoint`和`commerce-endpoint`的值是否指向您的[!DNL Adobe Commerce as a Cloud Service] GraphQL端點。

```json
"commerce-core-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
"commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
```

### 步驟2：提供初始提示

服務合約已在您的專案中時，提示代理程式實作店面整合。 若您的代理程式中有可用的，請使用&#x200B;**計畫**&#x200B;模式，以防止代理程式在沒有計畫的情況下繼續進行。

```shell-session
I need to implement delivery date estimates on the storefront for an Adobe Commerce (SaaS) store using Edge Delivery Services with storefront drop-ins. The backend is already built and deployed as an App Builder extension.

The full integration contract is in the `docs/STOREFRONT_API_SPEC.md` file— please read it first. It covers two integration points:

PDP and Cart pages — Call the delivery-estimates BFF action (HTTP POST) to fetch estimates for a destination and display the best delivery date.

Checkout shipping step — Delivery dates are already injected into each shipping method's `additional_data` by a webhook. No API call is needed. Just read `additional_data` from the shipping methods and display the delivery date next to each option.

Requirements:
- Show "Get it by [date]" on PDP using best_estimation.delivery_date
- Show a delivery date range on the cart page using delivery_date / safe_delivery_date
- Show delivery dates next to each shipping method at checkout, reading from additional_data
- Show "Order within X hours" countdown using cutoff_datetime_utc where appropriate
- Cache estimates client-side in sessionStorage to avoid redundant calls
- Never block the purchase flow — if estimates are unavailable, hide the UI silently

STOP and ask me any clarifying questions you have about the requirements before you do any work.
```

>[!TIP]
>
>提示會詳細說明，因為後端代理程式已提供完整API合約。 透過參考`@docs/STOREFRONT_API_SPEC.md`，代理程式可知道確切的端點URL、要求與回應格式，以及錯誤處理。 明確的需求清單會防止代理程式發明範圍。 具體而言，要求計畫模式會觸發分階段工作流程，協助您及早引導實施。

### 步驟3：回答澄清問題

代理程式傳回有關驗證範圍、簽出方法和樣式的問題。 下列範例顯示典型的問題和答案。

**代理程式問題範例：**

1. **匿名與登入的使用者** — 預估應顯示在所有購物者的PDP與購物車頁面上，還是僅顯示在已驗證的購物者頁面上？
2. **結帳方法** — ShippingMethods下拉式容器未公開`additional_data`，因此代理程式建議兩個選項：
   - **選項A：**&#x200B;在結帳和DOM插入傳遞日期時呼叫BFF （更簡單，與PDP/購物車一致）
   - **選項B：**&#x200B;透過`overrideGQLOperations`擴充結帳GraphQL片段以包含`additional_data`
3. **樣式** — 表情符號與現有設計權杖

**範例答案：**

```shell-session
1. Only for logged-in users — that way we can use the shopper's default shipping address and avoid a zip code input
2. Let's do Option A if feasible
3. Use anything that matches the current styling
```

>[!TIP]
>
>只顯示登入購物者的預估費用是個務實的選擇。 代理商可以自動（透過GraphQL）使用購物者的預設運送地址，因此無需輸入郵遞區號。 PDP和Cart上的匿名購物者需要輸入郵遞區號，這會增加摩擦。 結帳時，所有購物者都會看到交貨日期，因為已輸入運送地址。

>[!NOTE]
>
>您的代理可能會詢問不同的問題。 請使用下列答案作為指引：
>
>- 僅針對登入的購物者顯示PDP和購物車預估值（無需輸入郵遞區號）。
>- 若要結帳，請使用選項A （BFF呼叫+ DOM插入）以進行簡化。
>- 使用現有的設計代號來設定樣式。

### 步驟4：檢閱需求和架構

代理程式會設計共用模組架構。 確認其涵蓋：

| 元件 | 用途 |
|-----------|---------|
| `scripts/delivery-estimates.js` | 共用模組 — BFF使用者端、快取（sessionStorage，30分鐘TTL）、日期格式、倒數邏輯、客戶位址查詢、電信業者對應 |
| PDP整合 | 顯示「於[日期]前取得」，價格與說明之間有選擇性的倒數計時 |
| 購物車整合 | 在訂單摘要上方的右欄中顯示日期範圍（「週四，3月12日 — 週五，3月13日」） |
| 結帳整合 | 當出貨步驟作用中時呼叫BFF，DOM會透過`MutationObserver`插入傳遞日期 |

{style="table-layout:auto"}

要驗證的關鍵設計決策：

- 所有BFF呼叫都不會封鎖 — 頁面會先轉譯，預估會以非同步方式顯示。
- 所有失敗都是無訊息的 — 僅限`console.debug`，沒有購物者面對的錯誤。
- `CARRIER_MAP`將Commerce電信業者代碼(DPS、Fedex)對應至BFF電信業者代碼（標準、快速）。
- 動態`import()`將傳遞模組保留在關鍵轉譯路徑之外。

>[!NOTE]
>
>AI代理是不確定的，其行為會因模型和IDE而異。 您可能會收到一組不同的問題，產生一組不同的需求和架構。 若是如此，請嘗試將代理程式引導至與本教學課程中呈現內容最相符的方向上，然後再繼續。

### 步驟5：選取實作計畫

代理程式可讓您選擇建立詳細的實作計畫或完成直接實作。

- 如果您想要可檢視計畫，而且可以在階段中執行並具有更多控制權的計畫，請選取第一個選項。
- 如果您希望代理程式以最小的介入完成完整實作，請選取第二個選項。

在實作期間，代理程式會建立和修改下列檔案：

**新檔案：**

- `scripts/delivery-estimates.js` — 與`fetchDeliveryEstimates()`、`getCustomerShippingAddress()`、`formatDeliveryDate()`、`buildCountdownText()`、`findEstimateForCarrier()`共用模組

**已修改的檔案：**

- `blocks/product-details/product-details.js` + `.css` — 右欄中的傳遞預估div，主要轉譯後非同步擷取
- `blocks/commerce-cart/commerce-cart.js` + `.css` — 交貨預估div高於訂單摘要
- 送貨方法標籤的`blocks/commerce-checkout/commerce-checkout.js`、`containers.js`、`.css` — `MutationObserver`型DOM插入

觀察產生的程式碼，如有需要，詢問問題或重新導向代理程式。

### 步驟6：啟動伺服器並測試

代理程式完成實作後，請啟動開發伺服器並測試傳遞預估值。

1. 啟動本機開發伺服器：

   ```bash
   npm run start
   ```

1. 在瀏覽器中，登入您的購物者帳戶。

   PDP和購物車上的估計傳遞次數需要已儲存預設送貨地址的已驗證工作階段。

1. 導覽至產品頁面，然後驗證下列結果：

   | 頁面 | 預期結果 | 需要驗證 |
   |------|-----------------|---------------|
   | PDP | 「3月12日（星期四）前取得」搭配選用的倒數計時 | 是（僅限登入） |
   | 購物車 | 「預計送達：星期四，3月12日 — 星期五，3月13日」 | 是（僅限登入） |
   | 簽出 | 「預計送貨時間： 3月12日星期四」依送貨方式 | 否（結帳時輸入的地址） |

   {style="table-layout:auto"}

>[!NOTE]
>
>沒有相符承運商的送貨方法（例如，統一運費）不會顯示預估值。 這是刻意設計 — 只有`CARRIER_MAP`中對應的電信業者才能取得傳送日期。

您可以執行手動測試，或要求代理程式使用其瀏覽器功能來為您測試：

```shell-session
Run complete browser testing using the following product page 'http://localhost:3000/products/<product-slug>/<sku>'
```

### 步驟7：清除

在您跳過或完成測試後，代理程式會提示您繼續清除。 確認後，代理程式會封存實施期間產生的所有檔案成品。

## 疑難排解

如果在教學課程中遇到問題，請使用下列提示。

### 後端(App Builder)

| 症狀 | 原因 | 修正 |
|---------|-------|-----|
| 管理員UI設定動作傳回`400 Bad Request`並附上「要求定義不允許的引數（保留屬性）」 | 前端掛接正在要求內文中傳送`__ow_method`。 前置詞為`__ow_`的屬性會由OpenWhise保留，當動作有`final: true`時會遭到拒絕。 | 傳送自訂`method`屬性而非`__ow_method`。 後端動作會先讀取`params.method`，然後退回至`params.__ow_method` （執行階段會自動提供）。 |
| `aio app deploy`失敗，因為「productDependencies中需要maxVersion」 | CLI驗證需要`minVersion`產品相依性中的`maxVersion`和`app.config.yaml`。 | 將`maxVersion`值新增至`productDependencies`中的每個`app.config.yaml`專案。 |
| 部署命令失敗 | 部署前未設定認證。 `.env`、工作區選取和OAuth同步必須先發生。 | 請遵循正確的順序： `cp env.dist .env` > `aio app use --merge` > `npm run sync-oauth-credentials` > `aio app deploy`。 |

{style="table-layout:auto"}

### 店面(Edge Delivery Services)

| 症狀 | 原因 | 修正 |
|---------|-------|-----|
| 登入的購物者未出現PDP傳遞預估 | PDP區塊未初始化`account`下拉式清單，因此`getCustomerAddress()`無訊息失敗，且未擷取任何預估值。 | 直接使用`CORE_FETCH_GRAPHQL.fetchGraphQl()`查詢購物者地址，而非依賴帳戶外掛程式API。 這適用於任何頁面。 |
| GraphQL修正後PDP仍未顯示 | 使用了方法名稱中的錯字： `CORE_FETCH_GRAPHQL.fetch()`，而非`CORE_FETCH_GRAPHQL.fetchGraphQl()`。 | 使用正確的方法名稱： `fetchGraphQl` （大寫Q，小寫l）。 |
| 首次載入時未顯示結帳傳送日期 | `checkout/updated`事件接聽程式是在`checkout/initialized`觸發後註冊，因此遺漏了初始資料。 | 新增具有`checkout/initialized`的`{ eager: true }`接聽程式，以擷取註冊前發出的事件。 保留`checkout/updated`接聽程式以進行後續變更。 |
| 購物車傳遞預估未出現 | `block.appendChild(fragment)`將所有子系移出片段，因此`fragment.querySelector('.cart__delivery-estimate')`傳回null。 | 在附加作業後從`block`而不是`fragment`進行查詢。 |
| 統一運費在結帳時不會顯示交貨日期 | 依設計 — `CARRIER_MAP`僅將DPS對應至標準，並將Fedex對應至表示。 統一費率在外部API中沒有對應的電信業者。 | 不是錯誤。 若要新增其他電信業者的預估，請延伸`CARRIER_MAP`中的`scripts/delivery-estimates.js`，並在後端延伸中設定該電信業者。 |

{style="table-layout:auto"}

### Commerce SaaS沙箱

| 症狀 | 原因 | 修正 |
|---------|-------|-----|
| Webhook傳回`429 Too Many Requests` | [!DNL App Builder]工作區處於偵錯模式，具有嚴格的每分鐘速率限制。 [!DNL Commerce]在結帳期間經常重新計算運費，因此會耗盡配額。 | 部署至生產工作區（`aio app use`以切換，然後`aio app deploy`）。 生產工作區沒有偵錯率限制。 |
| Webhook軟性逾時警告（>1000毫秒） | 送貨方法webhook動作花費的時間超過[!DNL Commerce] 1000ms軟性逾時。 | 在`aio-lib-state`中更積極地啟用伺服器端快取，或在[!DNL Commerce Admin]中增加webhook逾時（Commerce Webhooks設定）。 |

{style="table-layout:auto"}

## 教學課程回顧

以下是本教學課程中涵蓋的主題摘要：

- **模擬API設定：**&#x200B;使用Pipedream或[!DNL App Builder]執行階段動作建立模擬傳遞預估API。
- **BFF模式：**&#x200B;正在建置封包外部API、保留認證伺服器端及集中快取的後端for-frontend動作。
- **Webhook擴充：**&#x200B;擴充送貨方法webhook，以在結帳時將交貨日期插入每個送貨選項。
- **管理員UI可設定性：**&#x200B;使用[!DNL Admin UI SDK]新增設定頁面，讓商家無需重新部署，即可管理API設定、來源地址及電信業者對應。
- **服務合約：**&#x200B;正在建立橋接後端擴充功能與店面實作的API合約。
- **店面整合：**&#x200B;使用共用使用者端模組，在PDP （「運送方式」）、購物車（日期範圍）和結帳（每種運送方式）上顯示預估的傳遞。
- **非封鎖UX：**&#x200B;確保傳遞估計絕不會封鎖購買流程 — 頁面會先轉譯，且估計會以非同步方式顯示。

## 後續步驟

使用下列建議來擴充您的傳遞預估服務：

- **連線實際電信業者API：**&#x200B;變更[!DNL Admin UI]中的服務URL和API金鑰，以即時出貨API （例如UPS、FedEx或USPS）取代模型。
- **支援匿名購物者：**&#x200B;在PDP和購物車頁面上新增郵遞區號輸入，讓未登入的購物者也能看到預估送貨量。
- **擴充電信業者對應：**&#x200B;新增更多電信業者代碼至`CARRIER_MAP`以顯示其他送貨方法的交貨日期。
- **新增伺服器端快取：**&#x200B;在BFF動作中實作`aio-lib-state`快取，以減少對重複來源和目的地配對之外部API的呼叫。
- **在訂單確認中顯示預估：**&#x200B;在訂單確認頁面和異動電子郵件中顯示預估的傳遞日期。
