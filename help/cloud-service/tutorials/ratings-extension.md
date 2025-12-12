---
title: 評等擴充功能教學課程
description: 瞭解如何使用App Builder和AI輔助開發工具，為Adobe Commerce as a Cloud Service建立產品評等擴充功能。
role: Developer
hide: true
hidefromtoc: true
source-git-commit: d0b9fd3ebbf0c88abbbf12821c5c4825ffcf10f0
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# 評等擴充功能教學課程(Beta)

>[!NOTE]
>
>本教學課程中使用的AI工具目前在Beta中，可能包含錯誤或其他問題。

本教學課程會引導您使用[!DNL Adobe Commerce as a Cloud Service]和AI輔助開發工具，為[!DNL Adobe App Builder]建立產品評等延伸。

開始之前，請先完成[必要條件](./tutorial-prerequisites.md)。

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

如果上述任何命令未傳回預期的結果，請參閱[必要條件](tutorial-prerequisites.md)以取得指引。

## 擴充功能開發

本節將引導您使用AI輔助開發工具，為Adobe Commerce as a Cloud Service開發評等擴充功能的程式。

1. 導覽至「**[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**」，並驗證「`commerce-extensibility`」工具集已啟用且沒有錯誤。 如果您看到錯誤，請關閉和開啟工具集。

   ![資料指標設定](../assets/cursor-settings.png){width="600" zoomable="yes"}

   >[!NOTE]
   >
   >使用AI輔助開發工具時，代理程式產生的程式碼和回應會有自然的變化。
   >如果您在程式碼上遇到任何問題，可以隨時要求代理程式協助您進行偵錯。

1. 如果您有任何檔案新增到Cursor的內容中，請停用它：

   - 瀏覽至&#x200B;[!UICONTROL **Cursor**] > [!UICONTROL **設定**] > [!UICONTROL **Cursor設定**] > [!UICONTROL **索引與檔案**]，並刪除列出的任何檔案。

   ![停用檔案](../assets/disable-documentation.png){width="600" zoomable="yes"}

1. 產生產品評等擴充功能的程式碼：
   - 從游標中選取游標聊天路徑，選取&#x200B;**代理程式**&#x200B;模式。
   - 輸入下列提示：

   ```plain
   Implement an Adobe Commerce as a Cloud Service extension to handle Product Ratings.
   
   Implement a REST API to handle GET ratings requests.
   
   GET requests will have to support the following query parameters:
   
   sku -> product SKU
   ```

   >[!NOTE]
   >
   >如果代理程式要求搜尋檔案，請允許搜尋。

1. 請精確回答代理程式的問題，協助其產生最佳程式碼。

   ![在Cursor](../assets/enter-prompt.png){width="600" zoomable="yes"}中輸入提示

   ![代理程式詢問澄清問題](../assets/agent-questions.png){width="600" zoomable="yes"}

1. 使用下列範例文字來回答代理程式的問題，以設定隨機分級資料：

   ```plain
   Yes, this headless extension is for Adobe Commerce as a Cloud Service storefront,
   but we do not need any authentication for the GET API because guest users should be able to use it on the storefront.
   
   This extension will be called directly from the storefront, no async invocation, such as events or webhooks, is required.
   
   Start with just the GET API for now, we will implement other CRUD operations at a later time.
   
   We do not need a DB or storage mechanism right now, just return random ratings data between 1 and 5 and a ratings count between 1 and 1000.
   
   The API should only return the average rating for the product and the total number of ratings.
   We do not need to add tests right now.
   ```

   代理程式會建立`requirements.md`檔案，做為實作的信任來源。

   ![已建立需求檔案](../assets/requirements-file.png){width="600" zoomable="yes"}

1. 檢閱`requirements.md`檔案並驗證計畫。

   如果一切看起來正確，請指示代理程式移至&#x200B;**階段2 — 架構規劃**。
1. 檢閱架構計畫。
1. 指示代理程式繼續產生程式碼。

   代理程式會產生必要的程式碼，並提供您後續步驟的詳細摘要。

   ![架構規劃](../assets/architecture-planning.png){width="600" zoomable="yes"}

   ![程式碼產生摘要](../assets/code-generation-summary.png){width="600" zoomable="yes"}

   ![後續步驟](../assets/next-steps.png){width="600" zoomable="yes"}

### 本機測試

1. 請要求代理程式協助您在本機測試程式碼。

   ```plain
   Test the ratings API locally on a dev server using cURL.
   ```

1. 請依照代理程式的指示，並確認API是否在本機運作。

   ![本機測試](../assets/local-testing.png){width="600" zoomable="yes"}

   ![本機測試結果](../assets/local-testing-1.png){width="600" zoomable="yes"}

### 部署擴充功能

1. 驗證產生的程式碼後，請使用以下提示來部署擴充功能：

   ```plain
   Deploy the ratings API.
   ```

   代理程式會在部署前執行部署前準備程度評估。

   ![部署前評估](../assets/pre-deployment-assessment.png){width="600" zoomable="yes"}

1. 當您對評估結果有信心時，請指示代理程式繼續進行部署。

   代理程式會使用MCP工具組來自動驗證、建置和部署。

   ![部署](../assets/deployment-process.png){width="600" zoomable="yes"}

### 部署後

您可以先測試API，再將其整合至店面。 代理程式應提供新動作的位置和測試策略。

![測試策略](../assets/testing-strategy.png){width="600" zoomable="yes"}

您也可以在終端機中使用cURL手動測試API：

```bash
curl -s "https://<your-site>.adobeioruntime.net/api/v1/web/ratings/ratings?sku=TEST-SKU-123"
```

![cURL測試](../assets/curl-test.png){width="600" zoomable="yes"}

### 整合Edge Delivery Services

若要整合評等API與由[!DNL Adobe Commerce]提供支援的[!DNL Edge Delivery Services]店面，請要求代理程式建立具有評等API需求的服務合約：

```plain
Create a service contract for the ratings api that I can pass on to the storefront agent. Name it RATINGS_API_CONTRACT.md
```

![服務合約](../assets/create-contract.png){width="600" zoomable="yes"}

![服務合約詳細資料](../assets/contract.png){width="600" zoomable="yes"}
<!-- 
Return to the terminal and run the following command in the `extension` folder to copy the file to the `storefront` folder:

```bash
cp RATINGS_API_CONTRACT.md ../storefront
``` -->

### 後續步驟

現在您有了評等API合約，就可以開始建立評等延伸模組的店面（前端）部分了。

<!-- 
## Connect to the storefront

This section teaches you how to implement real storefront features and communicate effectively with AI agents when working with [!DNL Adobe Commerce] dropins and [!DNL Edge Delivery Services].

>[!NOTE]
>
>The prompts provided are starting points. Although you can use them without modification, consider having a natural conversation with the agent.
>
>When working with AI-assisted development tools, there are always natural variations in the code and responses generated by the agent.
>
>If you encounter any issues with your code, ask the agent to help you debug it.

### Ratings stars and review count implementation

1. Navigate to the `storefront` folder:

   ```bash
   cd storefront
   ```

1. Open the storefront folder in a new Cursor window.

    Alternatively, if you have the [Cursor CLI](https://cursor.com/docs/configuration/shell#installing-cli-commands) installed, open the window by using the following command in your terminal:

   ```bash
   cursor .
   ```

1. Start the local development server:

   ```bash
   npm run start
   ```

1. In a browser, navigate to the Apparel page:

   ```plain
   http://localhost:3000/apparel
   ```

1. Observe the boilerplate storefront UI layout and note the lack of visual product ratings.

1. Use the following prompt with your agent:

   ```plain
   Implement product ratings in the storefront.

   Add a 5-star rating display with a review count underneath each product name on the product list page, product details page, and product recommendations.

   Use the dropin slot system where available.

   Use @RATINGS_API_CONTRACT.md to understand how to use the ratings API.
   ```

1. Observe the changes in the codebase, and watch the Apparel page for updates.

   You should see the following changes in your development environment and browser:

   * A product rating "component" is automatically created.
   * The component is integrated into product-details, product-list-page, and product-recommendations blocks using [dropin slots](https://experienceleague.adobe.com/developer/commerce/storefront/dropins/customize/slots?lang=zh-Hant).
   * Stars display with proper fill proportions based on mock rating values.

![Product Ratings Implementation](../assets/product-ratings-implementation.png){width="600" zoomable="yes"}

## Tutorial recap

Here is a summary of the topics covered in this tutorial:

* **Feature implementation**: How to describe new functionality to an AI agent.
* **Iterative changes**: Making quick modifications to existing code.
* **Complex UI components**: Building interactive features with visual references.
* **Dropin integration**: Working with [!DNL Adobe Commerce] dropin containers and slots.
* **Component reusability**: Creating shared components used across multiple blocks.

## Next steps

For further experimentation with this tutorial, use the following suggestions to further customize your ratings extension, or create your own modifications:

### Change the star colors

Use the following prompt to your agent:

```plain
Change the star fill color to red.
```

**Expected outcome:**

The stars are changed to red.

![Red Star Colors](../assets/red-star-colors.png){width="600" zoomable="yes"}

### Add rating distribution modal

The following steps show how the agent handles complex UI features with visual references.

1. **Before starting:** Save the following mock image and paste it into the chat with your storefront agent.

   ![Rating Distribution Mockup](../assets/rating-distribution-mockup.png){width="600" zoomable="yes"}

1. Follow these steps to create the ratings distribution modal using the reference image as a guide:

   * Update the API to return additional data representing the ratings distribution.
   * Update the API Contract.
   * Update the contact in the storefront codebase.
   * Ask the storefront agent to use the reference image and updated API Contract to add the ratings distribution to the PDP page.

1. Observe the following changes in the codebase, and watch the Apparel page for updates:

   * How the agent interprets the visual mockup
   * Whether it uses appropriate HTML structure for accessibility
   * How it handles the positioning and interaction states

#### Troubleshooting

* If the modal does not appear, check the browser console for errors.
* If positioning is off, ask the agent to fix it using the following format:

   ```plain
   adjust the modal position to be...
   ```

![Rating Distribution Modal](../assets/rating-distribution-modal.png){width="600" zoomable="yes"}
 -->
