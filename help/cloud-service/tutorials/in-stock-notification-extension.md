---
title: 庫存通知擴充功能教學課程
description: 瞭解如何使用App Builder、Edge Delivery Services和AI輔助開發工具，為Adobe Commerce as a Cloud Service建立庫存通知擴充功能。
solution: Commerce
feature: App Builder, Cloud
feature-set: Commerce
role: Developer
level: Intermediate
type: Tutorial
hide: true
hidefromtoc: true
source-git-commit: ce8882b8af21198a7bc57bc58124e8a2d1491a50
workflow-type: tm+mt
source-wordcount: '2599'
ht-degree: 0%

---

# 庫存通知擴充功能教學課程

本教學課程會引導您使用[!DNL Adobe Commerce as a Cloud Service]和AI輔助開發工具，為[!DNL Adobe App Builder]建立庫存通知擴充功能。 此擴充功能可讓購物者訂閱無庫存的產品，並在產品補充庫存時收到通知。

您建置兩個部分：

- **App Builder擴充功能** — REST API可管理無庫存訂閱（建立、讀取、刪除），具有事件導向且排程的庫存回訪偵測。
- **店面整合** — 產品詳細資料頁面(PDP)上的訂閱表單，僅在所選產品或變體無存貨時顯示。

>[!NOTE]
>
>AI代理程式是不確定的。 本教學課程中的提示、問題和輸出為範例。 您的代理程式可能會產生不同的問題、需求或架構提案。 使用本教學課程中的範例，引導代理程式取得類似結果。

開始之前，請先完成[必要條件](./tutorial-prerequisites.md)。 此教學課程使用&#x200B;**整合入門套件**。 確認您已複製該檔案，並完成必要條件頁面上所述的設定步驟。

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

- 您有一個包含產品資料的[!DNL Adobe Commerce as a Cloud Service]執行個體。 請參閱[Commerce Cloud服務執行個體](https://experienceleague.adobe.com/zh-hant/docs/commerce/cloud-service/overview){target="_blank"}。
- 您有一個店面專案連線到您的[!DNL Commerce]執行個體。 如果沒有店面，請依照[建立店面](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/?lang=zh-Hant){target="_blank"}中的步驟操作。
- 已安裝`aem` CLI：

  ```bash
  npm install -g @adobe/aem-cli
  ```

## 擴充功能開發

本節將引導您使用AI輔助開發工具，為[!DNL Adobe Commerce as a Cloud Service]開發庫存通知擴充功能。 此擴充功能提供用於訂閱管理的REST API，並偵測產品何時透過Commerce事件和排程檢查重新補充庫存。

1. 導覽至編碼代理程式中的MCP設定。

   例如，在游標中，移至&#x200B;**[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**。 確認`commerce-extensibility`工具集已啟用且沒有錯誤。 如果您看到錯誤，請關閉和開啟工具集。

   >[!NOTE]
   >
   >使用AI輔助開發工具時，代理程式產生的程式碼和回應會有自然變化。
   >如果您遇到任何程式碼問題，請要求代理程式協助您進行偵錯。

1. 如果您有任何檔案新增到Cursor的內容中，請將其停用。

   導覽至「**[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Indexing & Docs]**」並刪除任何列出的檔案。

### 步驟1：提供初始提示

提示AI代理程式開始實作。 告訴代理程式停止並詢問問題，可協助您及早掌控實施方向。

在代理程式的聊天視窗中輸入下列提示：

```shell-session
Implement an Adobe Commerce as a Cloud Service extension to handle out-of-stock notifications for products.

The service should provide REST API endpoints for basic create, read, update, and delete (CRUD) operations on out-of-stock notifications, allowing storefronts to manage notifications for specific product SKUs.

Back-in-stock is detected by an inventory or product event or a scheduled action that checks Commerce API and then calls the REST API to send the notification.

STOP and ask me any clarifying questions you have about the requirements before you do any work.
```

>[!TIP]
>
>在繼續操作前通知代理程式停止操作並詢問問題，可協助您及早引導實作。 此程式可確保及早識別關鍵假設和遺漏的需求，並需要在本教學課程中啟動引導式工作流程。

### 步驟2：回答代理程式的問題

代理程式返回時會提出一系列必要的問題，然後才能開始形成解決方案。 下列範例顯示典型的問題和答案。 您的代理可能會問不同的問題，但主題通常相同。

**代理程式問題範例：**

1. **REST API — 主機和消費者** — CRUD REST API是否應為儲存區域呼叫的此App Builder應用程式的一部分（例如Adobe I/O Runtime上的Web動作）？ 誰會將其命名為（EDS Storefront、自訂/Headless店面或兩者）？ 您需要CORS、公開（未驗證）存取，還是來電者會使用API金鑰、OAuth或Commerce權杖？
1. **資料模型** — 一個「通知」應該代表什麼？ 客戶識別碼（僅限電子郵件或客戶ID）？ 產品識別碼（僅限SKU或SKU +商店檢視）？ 相同客戶可以多次訂閱相同的SKU嗎？或是應該對訂閱進行重複資料刪除？
1. **庫存偵測 — 事件與已排程** — 您想要事件導向偵測（對Commerce的存貨/產品事件做出反應）、已排程偵測（定期檢查庫存的已排程動作）或兩者皆要嗎？ 「傳送通知」是什麼意思（呼叫外部webhook、傳送電子郵件或記錄）？
1. **補充庫存 — Commerce來源** — 您是否有偏好的事件名稱，或是設計應使用Commerce提供的任何庫存/庫存更新事件？ 對於已排程的檢查，哪個API應該用來透過SKU取得庫存狀態？
1. **持續性與多租用** — `aio-lib-state`是持續訂閱的正確位置，還是您有外部存放區？ 設計應假設是多租使用者還是單一租使用者？
1. **CRUD語意與生命週期** — 「刪除」是否表示取消訂閱？ 您需要「更新」嗎？ 在傳送補貨通知後，訂閱是否應自動移除或標籤為已通知？
1. **無法運作** — 要強制執行的任何速率限制或訂閱上限？ 是否有任何法規遵循需求（雙重選擇加入、同意標幟）？

**範例答案：**

```shell-session
1. The CRUD REST API should be part of thie App Builder app. It will be called by the EDS Storefront. For this implementation there is no need for API keys or security tokens.
2. For this initial implementation the customer identifier will be the email, product is identified by SKU, customer emails should not be able to subscribe to the same SKU multiple times.
3. Implement both. For now instead of sending the notification, log it so I can audit in the Adobe Developer Console.
4. Research and use what the best event to use that commerce already provides. Research the simplest way to get the stock status by SKU.
5. Use the aio-lib-state. Single tenant for now
6. Delete means cancel subscription. Skip Update, it does not apply for this service. After subscription is sent, it should be marked as notified or removed so it won't send again until the user subscribes again.
7. No limits. Implement minimal compliance requirements.
```

>[!NOTE]
>
>您的代理可能會詢問不同的問題。 使用這些答案作為指引，引導代理程式取得相同的功能結果：具有電子郵件和SKU訂閱的REST API、事件導向和排程的庫存偵測、`aio-lib-state`持續性以及記錄型通知。

### 步驟3：檢閱需求和架構

代理程式會產生需求和架構檔案，供您檢閱。 確認需求與您提供的答案相符，以及架構涵蓋：

- 訂閱CRUD的REST API動作（建立、讀取、更新和刪除）
- 由Commerce詳細目錄事件觸發的事件導向後備庫存處理常式
- 作為遞補專案的已排程支票存量動作
- 使用`aio-lib-state`的持續性

>[!NOTE]
>
>AI代理是不確定的，其行為會因模型和IDE而異。 您可能會收到一組不同的問題，產生一組不同的需求和架構。 若是如此，請嘗試將代理程式引導至與本教學課程中呈現內容最相符的方向上，然後再繼續。

### 步驟4：選取實作計畫

代理程式可讓您選擇建立詳細的實作計畫，或完成直接實作。

- 如果您想要可檢視計畫，而且可以在階段中執行並具有更多控制權的計畫，請選取第一個選項。
- 如果您希望代理程式以最小的介入完成完整實作，請選取第二個選項。

### 步驟5：部署、上線並訂閱事件

代理程式完成實作後，會提供後續步驟，讓您使用下列命令部署應用程式、將Commerce執行個體加入及訂閱事件：

1. 部署擴充功能：

   ```bash
   aio app deploy
   ```

1. 執行上線指令碼，向Commerce註冊事件提供者：

   ```bash
   npm run onboard
   ```

1. 訂閱Commerce事件：

   ```bash
   npm run commerce-event-subscribe
   ```

1. 驗證事件訂閱。

   導覽至您的Commerce執行個體並開啟&#x200B;**[!UICONTROL System]** > **[!UICONTROL Event Subscriptions]**。

   您應該會看到事件記錄表格。

   ![Commerce管理功能表醒目提示事件訂閱區段](../assets/in-stock-event-subscriptions.png){width="600" zoomable="yes"}

   ![具有已登入事件專案的事件訂閱資料表](../assets/in-stock-event-table.png){width="600" zoomable="yes"}

### 步驟6：測試擴充

要求代理程式提供測試步驟。 由於這是API服務，您可以請求命令列指示：

```shell-session
Give me step by step instructions to test the API service from the command line.
```

請依照代理程式提供的步驟進行。 下列範例顯示典型的測試命令。

**訂閱SKU：**

```bash
API_URL="https://<your-runtime-url>/api/v1/web/notify-out-of-stock/api"; curl -X POST "$API_URL" \
  -H "Content-Type: application/json" \
  -d '{"email":"test@example.com","sku":"ADB153"}'
```

回應看起來類似於：

```json
{
  "createdAt": "2026-03-06T22:11:00.308Z",
  "email": "test@example.com",
  "id": "b3353bf5-1007-4b10-989d-430892dd4a66",
  "sku": "ADB153"
}
```

**列出所有訂閱：**

```bash
curl -X GET "$API_URL"
```

回應會傳回所有作用中訂閱的清單：

```json
{
  "subscriptions": [
    {
      "createdAt": "2026-03-06T22:11:00.308Z",
      "email": "test@example.com",
      "id": "b3353bf5-1007-4b10-989d-430892dd4a66",
      "sku": "ADB153"
    }
  ]
}
```

**測試庫存回收流程：**

1. 從您的Commerce執行個體，編輯您已為其建立訂閱的產品。
1. 將產品庫存狀態設定為&#x200B;**[!UICONTROL Out of Stock]**。
1. 等候約一分鐘，然後將庫存狀態切換回&#x200B;**[!UICONTROL In Stock]**。

   ![Commerce管理員產品編輯頁面顯示「庫存狀態」下拉式清單，其中包含「有庫存」和「無庫存」選項](../assets/in-stock-product-stock-status-toggle.png){width="600" zoomable="yes"}

1. 等候約五分鐘，讓事件觸發並傳送至您的服務。

1. 從[!DNL Adobe Developer Console]，導覽至App Builder記錄區段。

   ![Adobe Developer Console App Builder記錄區段](../assets/in-stock-developer-console-logs.png){width="600" zoomable="yes"}

1. 在記錄中，確認是否有專案確認已處理事件，且已識別正確的電子郵件 — SKU訂閱配對。

   ![App Builder記錄專案顯示庫存事件處理](../assets/in-stock-log-entries.png){width="600" zoomable="yes"}

>[!TIP]
>
>您可以詢問代理程式在記錄中尋找什麼，以確認已成功記錄通知動作。 您也可以複製並貼上記錄專案，讓代理程式執行驗證。

在補貨事件處理後，請求訂閱清單應少傳回一個專案，因為通知的訂閱已移除。

### 建立服務合約

現在服務實作已經完成，請要求代理程式建立店面工作的服務合約：

```shell-session
Create an API service contract for the Out of Stock notification service and its endpoints. Ensure that the service contract is clear and detailed enough for a frontend developer to implement the storefront UI integration without needing to ask additional questions about the API. Name this file OUT_OF_STOCK_NOTIFICATION_CONTRACT.md
```

將此檔案複製到您的店面專案中，以便店面代理程式可以參考它。

## 連線到店面

本節將引導您使用[!DNL Edge Delivery Services]和AI輔助開發工具來實施庫存通知擴充功能的店面部分。 您將訂閱表單新增到產品詳細資料頁面(PDP)，僅在所選產品或變體無存貨時顯示。

>[!NOTE]
>
>提供的提示是起點。 雖然您可以在不修改的情況下使用它們，但請考慮與代理進行自然交談。
>
>使用AI輔助開發工具時，代理程式產生的程式碼和回應一律會有自然變異。
>
>如果您遇到任何程式碼問題，請要求代理程式協助您進行偵錯。

### 店面必要條件

在開始店面整合之前，請確認您具備下列條件：

- 連線到您[!DNL Commerce]執行個體的店面專案
- 使用CLI安裝的Commerce storefront AI工具[&#128279;](./tutorial-prerequisites.md#install-the-storefront-ai-tools)
- `OUT_OF_STOCK_NOTIFICATION_CONTRACT.md`檔案已複製到您的店面專案

### 步驟1：驗證環境

開啟您的`config.json`檔案，並驗證`commerce-core-endpoint`和`commerce-endpoint`的值是否指向您的[!DNL Adobe Commerce as a Cloud Service] GraphQL端點。

```json
"commerce-core-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
"commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
```

### 步驟2：提供初始提示

服務合約已在您的專案中時，提示代理程式在產品詳細資訊頁面中建立UI。 若您的代理程式中有可用的，請使用&#x200B;**計畫**&#x200B;模式，以防止代理程式在沒有計畫的情況下繼續進行。

```shell-session
Analyze @OUT_OF_STOCK_NOTIFICATION_CONTRACT.md. Add a form for subscribing to a notification for when a product is back in stock. Place this form on the product details page, underneath the add to cart and wishlist button. The form only displays when a product is out of stock. 

Use the project manager skill to plan this implementation.
```

>[!TIP]
>
>特別要求使用專案經理技能會觸發分階段工作流程，協助您在流程初期引導實施。 此程式可確保儘早識別關鍵假設和遺漏的需求，讓代理商有機會向您提供您原本可能未想在原始提示中提供的詳細資訊和需求。

### 步驟3：回答規劃問題

代理程式傳回時需回答一系列問題，然後才能開始形成解決方案。 下列範例顯示典型的問題和答案。 您的代理可能會問不同的問題，但主題通常相同。

**代理程式問題範例：**

1. **API基底URL** — 店面應該如何取得通知無庫存API基底URL？ 選項可能包括設定區塊（例如，具有`out-of-stock-api-base-url`的表格）、全域預留位置或環境變數，或其他方法。
1. **副本** — 實作應該使用預留位置來取得成功和錯誤訊息（例如，針對本地化），還是使用靜態英文來進行此實作？
1. **成功訂閱後** — 表單是否應隱藏並僅顯示「您已訂閱」(A)、保持表單可見但已停用，並在其上方顯示成功訊息(B)或其他行為(C)？
1. **可設定的產品** — 表單的可見度是否應該以所選變體的`inStock`值為基礎，以便讓表單顯示所選變體何時無庫存？

**範例答案：**

```shell-session
1. Global placeholder with baseurl value of `https://<your-runtime-url>/api/v1/web/notify-out-of-stock/api`
2. Use placeholders with static English fallback
3. B
4. Use selected variant's inStock value
```

>[!NOTE]
>
>將`<your-runtime-url>`取代為您App Builder部署中的實際[!DNL Adobe I/O Runtime] URL。
>
>您的代理可能會詢問不同的問題。 請使用下列答案作為指引：
>
>- API基底URL使用全域預留位置，以便在無需修改程式碼的情況下進行變更。
>- 針對以靜態英文作為遞補的使用者複製使用預留位置。
>- 成功訂閱後，保持表單可見但停用，並在其上方顯示成功訊息。
>- 對於可設定的產品，請使用所選變體的`inStock`值來控制表單可見性。

### 步驟4：檢閱需求和架構

代理程式會更新需求檔案以供您檢閱。 確認：

- 只有在產品或選取的變體無庫存時，表單才會出現。
- 表單位於PDP上的加入購物車和願望清單按鈕下方。
- API整合使用來自全域預留位置的基底URL。
- 成功和錯誤狀態會根據合約來處理(201、409、400、503/500)。

>[!NOTE]
>
>AI代理是不確定的，其行為會因模型和IDE而異。 您可能會收到一組不同的問題，產生一組不同的需求和架構。 若是如此，請嘗試將代理程式引導至與本教學課程中呈現內容最相符的方向上，然後再繼續。

在&#x200B;**階段2 （架構規劃）**&#x200B;期間，代理程式會先研究檔案和您的程式碼基底，再提出架構。 預期代理程式會：

- 搜尋[!DNL Commerce]的PDP下拉式容器、槽和事件裝載檔案。
- 掃描您的`blocks`目錄和`scripts/initializers/`資料夾以取得現有的PDP相關程式碼。
- 探索可用容器和槽內容圖形的TypeScript定義。

接著，代理程式會顯示架構選項。 檢閱計畫並指示代理程式繼續。

### 步驟5：選取實作計畫

代理程式可讓您選擇建立詳細的實作計畫，或完成直接實作。

- 如果您想要可檢視計畫，而且可以在階段中執行並具有更多控制權的計畫，請選取第一個選項。
- 如果您希望代理程式以最小的介入完成完整實作，請選取第二個選項。

在&#x200B;**階段4 （實作）**&#x200B;期間，代理程式會根據選取的架構產生程式碼。 根據方法，代理程式會使用數種專門技能：

- **內容模式：**&#x200B;如果需要新區塊，代理程式會設計作者友善的內容結構。
- **區塊開發：**&#x200B;代理程式會依照[!DNL Edge Delivery Services]慣例建立區塊檔案，包括JavaScript裝飾函式、設定範圍的CSS樣式、協助工具的ARIA標籤，以及載入和錯誤狀態處理。
- **插入式自訂：**&#x200B;如果架構使用插槽自訂，代理程式會匯入正確的容器、使用產品標題附近的驗證插槽，以及訂閱目前SKU的產品資料事件。

觀察產生的程式碼，如有需要，詢問問題或重新導向代理程式。

### 步驟6：啟動伺服器並測試

代理程式完成實作後，請啟動開發伺服器並測試表單。

1. 啟動本機開發伺服器：

   ```bash
   npm run start
   ```

1. 在瀏覽器中，導覽至無庫存產品頁面。 例如：

   ```shell-session
   http://localhost:3000/products/<out-of-stock-product-slug>/<sku>
   ```

1. 確認訂閱表單出現在加入購物車和願望清單按鈕的下方。

您可以執行手動測試，或要求代理程式使用其瀏覽器功能來為您測試：

```shell-session
Run complete browser testing. Use the following out of stock product 'http://localhost:3000/products/<out-of-stock-product-slug>/<sku>'
```

![產品詳細資訊頁面，在加入購物車按鈕下方顯示補貨通知表單](../assets/in-stock-notification-form.png){width="600" zoomable="yes"}

### 步驟7：清除

在您略過或完成測試之後，代理程式會提示您繼續最終&#x200B;**清理**&#x200B;階段。 確認後，代理程式會封存實施期間建立的所有檔案成品。

## 疑難排解

若在教學課程中遇到問題，請使用下列提示：

- **API錯誤：**&#x200B;使用CLI直接傳送要求給API以驗證行為。 例如，使用`curl`獨立測試每個端點。
- **代理程式錯誤：**&#x200B;將錯誤訊息複製並貼到代理程式聊天工作階段以協助您偵錯問題。 代理程式可以診斷常見問題，例如缺少環境變數或動作設定錯誤。
- **事件管道：**&#x200B;如果補貨事件未觸發，請確認您已完成入門和事件訂閱步驟。 檢查`workspace.json`是否位於正確的位置，以及是否已啟用Commerce事件模組。
- **Stock狀態承載：** Commerce可能會將`is_in_stock`以字串(`"1"`)傳送，而非布林值(`true`)。 如果未觸發庫存回覆處理常式，請要求代理程式檢查消費者程式碼是否包含嚴格型別比較，並更新以處理兩種格式。

## 教學課程回顧

以下是本教學課程中涵蓋的主題摘要：

- **擴充功能開發：**&#x200B;說明AI代理程式的新功能，並使用[!DNL App Builder]產生CRUD作業的有效的REST API。
- **事件導向架構：**&#x200B;正在設定Commerce事件和排程動作，以偵測產品何時恢復庫存。
- **本機測試和部署：**&#x200B;使用`curl`測試API並使用[!DNL Adobe I/O CLI]部署。
- **服務合約：**&#x200B;正在建立橋接後端擴充功能與店面實作的API合約。
- **分階段店面整合：**&#x200B;使用AI輔助的技能處理需求、架構和實作。
- **插入式整合：**&#x200B;使用[!DNL Adobe Commerce]插入式容器和插槽，將訂閱表單新增至PDP。

## 後續步驟

使用下列建議來延長您的庫存通知服務：

- **傳送實際通知：**&#x200B;以電子郵件服務（例如[!DNL Adobe Campaign]或協力廠商提供者）取代以記錄檔為基礎的通知。
- **新增訂閱管理頁面：**&#x200B;建立購物者可以檢視及取消使用中訂閱的店面頁面。
- **支援多租使用者部署：**&#x200B;擴充狀態管理，以便在單一App Builder應用程式中支援多個Commerce租使用者。
- **新增速率限制：**&#x200B;在訂閱API上實作速率限制以防止濫用。
