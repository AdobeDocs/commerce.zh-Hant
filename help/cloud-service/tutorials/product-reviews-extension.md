---
title: 產品評論擴充功能教學課程
description: 瞭解如何使用App Builder、Edge Delivery Services和AI輔助開發工具，為Adobe Commerce as a Cloud Service建立產品評論和問答擴充功能。
solution: Commerce
feature: App Builder, Cloud
feature-set: Commerce
role: Developer
level: Intermediate
type: Tutorial
hide: true
hidefromtoc: true
source-git-commit: 9c76bae29c05909406a40ca03a2b3d242db05f3f
workflow-type: tm+mt
source-wordcount: '2470'
ht-degree: 0%

---

# 產品評論擴充功能教學課程

本教學課程會引導您建立擴充功能，讓客戶能夠使用[!DNL Adobe Commerce as a Cloud Service]和AI輔助開發工具，針對具有[!DNL Adobe App Builder]後端的店面提交產品檢閱和問答(Q&amp;A)內容。 此擴充功能為購物者提供REST API端點，以便檢視及提交產品評論和問答(Q&amp;A)內容，並將其顯示在產品詳細資料頁面(PDP)上。

您建置兩個部分：

- **App Builder擴充功能** — 具有GET和POST作業的REST API，可在`aio-lib-state`中建立和檢視具有驗證、分頁和持續性的產品檢閱和問答內容。
- **店面整合** — PDP上的產品評論區塊，可顯示評論和問答，提供購物者提交評論、問題和答案的表單。

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

- 您有一個包含產品資料的[!DNL Adobe Commerce as a Cloud Service]執行個體。 請參閱[Commerce Cloud服務執行個體](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/overview){target="_blank"}。
- 您有一個店面專案連線到您的[!DNL Commerce]執行個體。 如果沒有店面，請依照[建立店面](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/){target="_blank"}中的步驟操作。
- 已安裝`aem` CLI：

  ```bash
  npm install -g @adobe/aem-cli
  ```

## 擴充功能開發

本節將引導您開發擴充功能，以使用AI輔助開發工具針對具有[!DNL Adobe Commerce as a Cloud Service]後端的店面，提交及檢視產品評論和問答內容以進行擴充功能。 擴充功能提供REST API，可提交和檢視產品評論和問答內容，以及在PDP上顯示。

1. 導覽至編碼代理程式中的MCP設定。 例如，在游標中，移至&#x200B;**[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**。 確認`commerce-extensibility`工具集已啟用且沒有錯誤。 如果您看到錯誤，請關閉和開啟工具集。

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
I want to build an Adobe Commerce as a Cloud Service extension that allows shoppers to submit and view product review and question and answer (Q&A) content that displays on product detail pages (PDP).

## Product Reviews
The application has REST API endpoints that can be called by a storefront to retrieve and submit product reviews for a given SKU.

The GET endpoint accepts the following query parameters:
- sku (string, required): The SKU of the product to fetch reviews for
- limit (integer, optional): The maximum number of reviews to return (default: 10)
- offset (integer, optional): The number of reviews to skip for pagination (default: 0)

The POST endpoint accepts the following JSON body parameters:
- sku (string, required): The SKU of the product to submit a review for
- rating (integer, required): The rating for the product (1-5)
- review (string, optional): The text of the review
- user (string, optional): The name of the user submitting the review

The POST endpoint validates the input and returns appropriate error responses for invalid data. The reviews are stored and associated with the corresponding product SKU.

## Questions and Answers
The application has REST API endpoints that can be called by a storefront to retrieve and submit questions and answers for a given SKU.

The GET endpoint accepts the following query parameters:
- sku (string, required): The SKU of the product to fetch questions and answers for
- limit (integer, optional): The maximum number of questions and answers to return (default: 10)
- offset (integer, optional): The number of questions and answers to skip for pagination (default: 0)

The POST endpoint accepts the following JSON body parameters:
- sku (string, required): The SKU of the product to submit a question or answer for
- type (string, required): The type of submission ("question" or "answer")
- questionId (string, required if type is "answer"): The ID of the question being answered
- content (string, required): The text of the question or answer
- user (string, optional): The name of the user submitting the question or answer

The POST endpoint validates the input and returns appropriate error responses for invalid data. The questions and answers are stored and associated with the corresponding product SKU. Answers are also associated with the corresponding question.

Do not require Adobe IMS authentication for these endpoints. They will be called directly from the storefront.

STOP and ask me any clarifying questions you have about the requirements before you do any work.
```

>[!TIP]
>
>在繼續之前告訴代理程式停止操作並詢問問題，可協助您及早引導實作。 這可確保儘早識別關鍵假設和缺少的需求，以及啟動本教學課程中的引導式工作流程所需。

### 步驟2：回答代理程式的問題

代理程式傳回時需回答一系列問題，然後才能開始形成解決方案。 下列範例顯示典型的問題和答案。 您的代理可能會問不同的問題，但主題通常相同。

**代理程式問題範例：**

1. **REST API — 主機和消費者** — CRUD REST API是否應為儲存區域呼叫的此App Builder應用程式（Adobe I/O Runtime上的Web動作）的一部分？ 誰會將其命名為（EDS Storefront、自訂/Headless店面或兩者）？ 您需要CORS、公開（未驗證）存取，還是來電者會使用API金鑰或OAuth？
1. **資料模型** — 一個「評論」或「問題」代表什麼？ 客戶識別碼（僅限電子郵件或客戶ID）？ 產品識別碼（僅限SKU或SKU +商店檢視）？ 同一客戶是否可針對同一個SKU提交多個稽核？
1. **持續性** — `aio-lib-state`是持續稽核和問答的正確位置，還是您有外部存放區？ 設計應假設是多租使用者還是單一租使用者？
1. **分頁語意** — 針對GET問答集，`limit`是否僅適用於問題（含巢狀答案），或適用於問題加答案的總數？

**範例答案：**

```shell-session
1. The REST API should be part of this App Builder app. It will be called by the EDS Storefront. No authentication — public access for both GET and POST.
2. For reviews: sku, rating (1-5), optional review text, optional user name. For Q&A: sku, type (question or answer), content, optional user. Answers linked to questions via questionId. Allow multiple reviews per SKU from the same user.
3. Use aio-lib-state. Single tenant for now.
4. Pagination by question — limit and offset apply to questions; each question includes its nested answers.
```

>[!NOTE]
>
>您的代理可能會詢問不同的問題。 使用這些答案作為指引，引導代理程式取得相同的功能結果：具有評論和問答的公用REST API、`aio-lib-state`持續性以及無驗證。

### 步驟3：檢閱需求和架構

代理程式會產生需求和架構檔案，供您檢閱。 確認需求與您提供的答案相符，以及架構涵蓋：

- 四個Web動作： `reviews-get`、`reviews-post`、`qa-get`、`qa-post`
- 持續使用`aio-lib-state`搭配符合允許模式的金鑰（`[a-zA-Z0-9-_.]` — 無冒號）
- 狀態值儲存為JSON字串（非原始物件或陣列）
- 自含套件 — 在`product-reviews`套件內共用程式碼（util、常數），而不是透過逸出套件的`../../`路徑

>[!NOTE]
>
>AI代理是不確定的，其行為會因模型和IDE而異。 您可能會收到一組不同的問題，產生一組不同的需求和架構。 若是如此，請嘗試將代理程式導向，讓實作更符合本教學課程中的內容，然後再繼續。

### 步驟4：選取實作計畫

代理程式可讓您選擇建立詳細的實作計畫或完成直接實作。

- 如果您想要可檢視計畫，而且可以在階段中執行並具有更多控制權的計畫，請選取第一個選項。
- 如果您希望代理程式以最小的介入完成完整實作，請選取第二個選項。

### 步驟5：部署擴充功能

代理程式完成實作後，請部署擴充功能：

```bash
aio app deploy
```

如果代理程式將`require-adobe-auth: true`新增至動作，請要求它移除驗證，以便可以從店面直接呼叫端點：

```shell-session
Remove the requirement to provide a valid Adobe IMS access token from all product-reviews actions.
```

然後重新部署：

```bash
aio app deploy
```

### 步驟6：建立模型資料並預先填入以進行測試

建立模擬資料檔案，並使用curl預先填入API，好讓您可以在CLI和店面中擁有範例檢閱和問答內容以進行測試。

1. 使用範例資料建立檔案`docs/mock-product-reviews-data.json` （或類似檔案）。 例如：

   ```json
   {
     "reviews": [
       { "sku": "ADB153", "rating": 5, "review": "Great product, highly recommend!", "user": "shopper@example.com" },
       { "sku": "ADB153", "rating": 4, "review": "Good value for money.", "user": "buyer@example.com" }
     ],
     "questions": [
       { "sku": "ADB153", "type": "question", "content": "Does this come in other colors?", "user": "curious@example.com" }
     ]
   }
   ```

1. 使用curl將資料張貼至您已部署的API。

   將`<your-runtime-url>`取代為您的實際App Builder執行階段URL （例如，`https://1172492-prodreviewqa135-stage.adobeioruntime.net`）：

   ```bash
   API_URL="https://<your-runtime-url>/api/v1/web/product-reviews"
   
   # Submit reviews
   curl -s -X POST "$API_URL/reviews-post" \
     -H "Content-Type: application/json" \
     -d '{"sku":"ADB153","rating":5,"review":"Great product, highly recommend!","user":"shopper@example.com"}'
   
   curl -s -X POST "$API_URL/reviews-post" \
     -H "Content-Type: application/json" \
     -d '{"sku":"ADB153","rating":4,"review":"Good value for money.","user":"buyer@example.com"}'
   
   # Submit a question (save the returned id for the answer)
   curl -s -X POST "$API_URL/qa-post" \
     -H "Content-Type: application/json" \
     -d '{"sku":"ADB153","type":"question","content":"Does this come in other colors?","user":"curious@example.com"}'
   
   # Submit an answer (replace <QUESTION-UUID> with the id from the question response)
   curl -s -X POST "$API_URL/qa-post" \
     -H "Content-Type: application/json" \
     -d '{"sku":"ADB153","type":"answer","questionId":"<QUESTION-UUID>","content":"Yes, it comes in blue and red.","user":"seller@example.com"}'
   ```

1. 使用GET請求驗證資料：

   ```bash
   curl -s "$API_URL/reviews-get?sku=ADB153"
   curl -s "$API_URL/qa-get?sku=ADB153"
   ```

>[!TIP]
>
>針對包含評論和問答內容的產品使用SKU `ADB153`，針對沒有評論的產品，使用`ADB152`。 此資料設定可讓您測試店面中的填入和空白狀態。

### 步驟7：測試擴充

要求代理程式提供測試步驟，或使用上一步驟中的curl範例。 下列範例顯示典型的測試命令。

**送出評論：**

```bash
API_URL="https://<your-runtime-url>/api/v1/web/product-reviews"
curl -s -X POST "$API_URL/reviews-post" \
  -H "Content-Type: application/json" \
  -d '{"sku":"ADB153","rating":5,"review":"Excellent!","user":"test@example.com"}'
```

**清單評論：**

```bash
curl -s "$API_URL/reviews-get?sku=ADB153"
```

**提交問題：**

```bash
curl -s -X POST "$API_URL/qa-post" \
  -H "Content-Type: application/json" \
  -d '{"sku":"ADB153","type":"question","content":"Is this dishwasher safe?","user":"test@example.com"}'
```

**送出答案** （使用問題回應中的`id`作為`questionId`）：

```bash
curl -s -X POST "$API_URL/qa-post" \
  -H "Content-Type: application/json" \
  -d '{"sku":"ADB153","type":"answer","questionId":"<QUESTION-UUID>","content":"Yes, it is.","user":"support@example.com"}'
```

### 建立服務合約

現在服務實作已經完成，請要求代理程式建立店面工作的服務合約：

```shell-session
Create a service contract for the Product Review and Q&A application that defines the API endpoints, request and response formats, and any necessary data models. Ensure that the service contract is clear and detailed enough for a frontend developer to implement the storefront integration without needing to ask additional questions about the API. Name this file PRODUCT_REVIEW_QA_CONTRACT.md
```

將此檔案複製到您的店面專案中，以便店面代理程式可以參考它。

## 連線到店面

本節將指導您使用[!DNL Edge Delivery Services]和AI輔助開發工具來實施產品評論和問答擴充功能的店面部分。 您將產品評論區塊新增到PDP，其中會同時顯示評論和問答內容，並允許購物者提交新內容。

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
- `PRODUCT_REVIEW_QA_CONTRACT.md`檔案已複製到您的店面專案

### 步驟1：驗證環境

開啟您的`config.json`檔案，並驗證`commerce-core-endpoint`和`commerce-endpoint`的值是否指向您的[!DNL Adobe Commerce as a Cloud Service] GraphQL端點。

```json
"commerce-core-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
"commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
```

### 步驟2：提供初始提示

服務合約已在您的專案中時，提示代理程式實施產品評論區塊。 若您的代理程式中有可用的，請使用&#x200B;**計畫**&#x200B;模式，以防止代理程式在沒有計畫的情況下繼續進行。

```shell-session
Analyze @PRODUCT_REVIEW_QA_CONTRACT.md and build a product review block using the API specified in the contract. The block displays both reviews and Q&A content on the product detail page, with forms for shoppers to submit reviews, questions, and answers. Use the project manager skill to plan this implementation.
```

>[!TIP]
>
>明確要求使用專案經理技能會觸發分階段工作流程，協助您引導實施。 這可確保在流程早期識別關鍵假設和遺漏的需求。

### 步驟3：回答澄清問題

代理程式傳回時需回答一系列問題，然後才能開始形成解決方案。 下列範例顯示典型的問題和答案。 您的代理可能會問不同的問題，但主題通常相同。

**代理程式問題範例：**

1. **API基底URL** — 店面應該如何取得產品評論API基底URL？ 選項可能包括設定區塊（例如，具有`apiBaseUrl`的表格）、全域預留位置或其他方法。
1. **SKU來源** — 區塊應該從PDP內容（目前產品）或區塊組態讀取SKU嗎？
1. **表單行為** — 在成功提交後，表單應該隱藏、顯示成功訊息，或保持可見狀態但停用？

**範例答案：**

```shell-session
1. Block table config with apiBaseUrl (required). Each block instance can point to its own deployment.
2. From block table if set; otherwise use getProductSku() so it works on PDP without authoring a SKU.
3. Show a success message above the form; keep the form visible but disabled.
```

>[!NOTE]
>
>以您實際的App Builder執行階段URL （例如`https://1172492-prodreviewqa135-stage.adobeioruntime.net`）取代區塊設定中的預留位置。
>
>您的代理可能會詢問不同的問題。 請使用下列答案作為指引：
>
>- API基底URL應來自區塊表格，因此無需修改程式碼即可變更。
>- 區塊表格的SKU （若已設定）；否則來自PDP上的目前產品。
>- 成功提交後，顯示成功訊息並停用表單。

### 步驟4：檢閱需求和架構

代理程式會更新需求檔案以供您檢閱。 確認：

- 區塊會呈現評論（含評分、使用者、日期、文字）和問答（含巢狀答案的問題）。
- Forms可用於提交評論、問題和答案。
- 評論和問答內容都支援分頁。
- API整合使用區塊表格中的基底URL。
- 成功和錯誤狀態會根據合約處理。

>[!NOTE]
>
>AI代理是不確定的，其行為會因模型和IDE而異。 您可能會收到一組不同的問題，產生一組不同的需求和架構。 若是如此，請嘗試將代理程式導向，讓實作更符合本教學課程中的內容，然後再繼續。

### 步驟5：選取實作計畫

代理程式可讓您選擇建立詳細的實作計畫，或完成直接實作。

- 如果您想要可檢視計畫，而且可以在階段中執行並具有更多控制權的計畫，請選取第一個選項。
- 如果您希望代理程式以最小的介入完成完整實作，請選取第二個選項。

在實作期間，代理程式會建立和修改區塊檔案。 觀察產生的程式碼，如有需要，詢問問題或重新導向代理程式。 如果區塊未轉譯，請要求代理程式分析區段裝飾和區塊探索模式 — 區塊元素必須是區段的直接子系，架構才能找到它。

### 步驟6：在檔案製作中將區塊新增至產品頁面

將產品評論區塊新增至產品頁面範本，使其顯示在所有PDP上。 使用Document Authoring服務(da.live)來新增及設定區塊。

1. 開啟您的檔案編寫服務，例如[da.live](https://da.live/)

1. 按一下您的專案空間，開啟&#x200B;**產品**&#x200B;資料夾並選取&#x200B;**預設** (`products/default`)。

1. 新增區塊區段。

   在區塊表格中，新增區塊名稱為&#x200B;**product-review**&#x200B;的列（或您的代理程式建立的區塊名稱）。

1. 使用必要的設定來設定區塊：
   - **apiBaseUrl** — 您的App Builder執行階段URL （例如，`https://<namespace>-<app-name>-stage.adobeioruntime.net`）。
   - **sku** — 留空以在PDP上使用目前產品的SKU，或輸入特定的SKU以只顯示該產品的評論。

1. 按一下&#x200B;**[!UICONTROL Publish]**&#x200B;以發佈您的變更。

### 步驟7：啟動伺服器並測試

在「檔案製作」中將區塊新增至產品頁面後，請啟動開發伺服器並測試區塊。

1. 啟動本機開發伺服器：

   ```bash
   npm run start
   ```

1. 在瀏覽器中，導覽至已預先填入稽核和問答內容的產品頁面。 例如：

   ```shell-session
   http://localhost:3000/products/<product-slug>/ADB153
   ```

1. 確認產品稽核區塊顯示稽核和問答內容，並確認提交表單有效。

您可以執行手動測試，或要求代理程式使用其瀏覽器功能來為您測試：

```shell-session
Run complete browser testing. Use the following product page 'http://localhost:3000/products/<product-slug>/ADB153'
```

### 步驟8：清除

在您略過或完成測試之後，代理程式會提示您繼續最終&#x200B;**清理**&#x200B;階段。 確認後，代理程式會封存實施期間建立的所有檔案成品。

## 疑難排解

如果在教學課程中遇到問題，請使用下列提示。

### 後端(App Builder)

| 症狀 | 原因 | 修正 |
|---------|-------|-----|
| GET或POST傳回500「找不到模組」 | 產品評論動作使用`require("../../utils")`或`require("../../constants")`，可逸出套件組合。 部署套件時不包括這些檔案。 | 讓產品評論套件自成一體。 新增`actions/product-reviews/lib/constants.js`和`actions/product-reviews/lib/utils.js`，並從`../lib/...`而非`../../`更新所需的全部四個動作。 |
| GET傳回500且「金鑰必須符合模式」 | 狀態索引鍵使用冒號（例如，`reviews:ADB153`）。 `aio-lib-state`僅允許`[a-zA-Z0-9-_.]`。 | 將首碼從`reviews:`和`qa:`變更為`reviews.`和`qa.`。 新增`stateKey(prefix, sku)`協助程式以清除SKU （以`_`取代無效的字元）。 |
| POST傳回500且「值必須為字串」 | `aio-lib-state`只接受字串值。 程式碼會將陣列或物件傳遞至`state.put()`。 | 寫入時與`JSON.stringify()`序列化，讀取時與`JSON.parse()`序列化。 更新全部四個動作。 |

{style="table-layout:auto"}

### 店面(Edge Delivery Services)

| 症狀 | 原因 | 修正 |
|---------|-------|-----|
| 封鎖無法在測試頁面上呈現 | 區塊專案巢狀內嵌於額外的`div`中，因此`decorateSections`之後的區塊選取器(`div.section > div > div`)不相符。 | 將區塊設為區段的直接子項。 結構： `section > div.product-review` （或同等區塊類別）。 避免`section > div > div.product-review`。 |
| 無效的CSS權杖 | 區塊使用不存在於`styles/styles.css`中的設計權杖（例如，`--color-error-100`、`--type-detail-font-size`）。 | 要求代理程式根據專案的`styles/styles.css`驗證權杖，並將無效的權杖取代為現有的權杖（例如，`--color-alert-*`、`--type-details-caption-*`）。 |

{style="table-layout:auto"}

## 教學課程回顧

以下是本教學課程中涵蓋的主題摘要：

- **擴充功能開發：**&#x200B;說明在具有Adobe Commerce as a Cloud Service後端的店面上，使用AI代理程式建立和檢視產品評論及問答內容的功能，以及如何透過使用[!DNL App Builder]產生具有四個端點的有效REST API來實作此功能。
- **持續性：**&#x200B;使用具有正確金鑰格式和JSON序列化值的`aio-lib-state`。
- **模擬資料與預先填入：**&#x200B;建立模擬資料檔案，並使用curl預先填入API以進行CLI和店面測試。
- **服務合約：**&#x200B;正在建立橋接後端擴充功能與店面實作的API合約。
- **分階段店面整合：**&#x200B;使用AI輔助的技能處理需求、架構和實作。
- **PDP區塊：**&#x200B;新增產品評論區塊至PDP，PDP會顯示評論和問答以及提交表單和分頁。

## 後續步驟

使用下列建議來延伸您的產品檢閱服務：

- **新增稽核：**&#x200B;在發佈前實作稽核及問答內容的稽核工作流程。
- **新增驗證：**&#x200B;要求購物者登入才能提交評論或問答內容，並將提交內容與客戶帳戶建立關聯。
- **新增訂閱管理頁面：**&#x200B;建立購物者可以檢視和編輯評論的店面頁面。
- **支援多租使用者部署：**&#x200B;擴充狀態管理，以便在單一App Builder應用程式中支援多個Commerce租使用者。
- **新增速率限制：**&#x200B;在API上實作速率限制以防止濫用。
