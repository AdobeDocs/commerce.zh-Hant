---
title: 擴充功能的AI編碼工具
description: 瞭解如何使用AI工具來建立Commerce App Builder擴充功能。
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案(Adobe管理的SaaS基礎結構)。"
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 5dd290a4e10bdbd1f6c96b67ab6c9ba1598705dc
workflow-type: tm+mt
source-wordcount: '1454'
ht-degree: 0%

---

# 擴充功能的AI編碼工具

移轉至[!DNL Adobe Commerce as a Cloud Service]時，您可以使用AI編碼工具將現有的[!DNL Adobe Commerce] PHP擴充功能轉換為[!DNL Adobe Developer App Builder]擴充功能。 它也可以用來建立新的[!DNL App Builder]擴充功能。

使用AI編碼工具可提供下列優點：

* **增強型開發工作流程**：整合式Adobe Commerce開發工具。
* **AI支援的協助**：內容感知程式碼產生和偵錯。
* **Commerce特定功能**： Adobe Commerce App Builder開發的專用工具。
* **自動化工作流程**：簡化開發和部署程式。

## 先決條件

* 編碼代理程式，例如[Cursor](https://cursor.com/download)（建議）、[Github Copilot](https://github.com/features/copilot)、[Google Gemini CLI](https://github.com/google-gemini/gemini-cli)或[Claude Code](https://www.claude.com/product/claude-code)
* [Node.js](https://nodejs.org/en/download)： LTS版本
* 封裝管理員： [npm](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm)或[yarn](https://classic.yarnpkg.com/lang/en/docs/install/#mac-stable)
* [Git](https://github.com/git-guides/install-git)：用於存放庫複製和版本控制

## 安裝

1. 全域安裝最新的[Adobe I/O CLI](https://github.com/adobe/aio-cli)：

   ```bash
   npm install -g @adobe/aio-cli
   ```

1. 安裝[Adobe I/O CLI Commerce外掛程式](https://github.com/adobe-commerce/aio-cli-plugin-commerce)：

   ```bash
   aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce
   ```

1. 複製Commerce [整合入門套件](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/create-integration)：

   ```bash
   git clone git@github.com:adobe/commerce-integration-starter-kit.git
   ```

1. 導覽至入門套件目錄：

   ```bash
   cd commerce-integration-starter-kit
   ```

1. 執行互動式設定命令，安裝Commerce AI擴充性工具：

   ```bash
   aio commerce extensibility tools-setup
   ```

設定程式會提示您設定選項。 對於安裝位置，請選擇「目前的目錄」以在目前的工作區中安裝工具：

```terminal
? Where would you like to setup the tools?
❯ Current directory
  New directory
```

選取編碼代理程式時，Adobe建議選取`Cursor`以獲得最佳開發體驗：

```terminal
? Which coding agent would you like to use?
❯ Cursor
  Copilot
  Gemini CLI
  Claude Code
```

選取封裝管理員時，Adobe建議使用`npm`來維持一致性：

```terminal
? Which package manager would you like to use?
❯ npm
  yarn
```

1. 成功安裝編碼工具後，安裝程式會設定：

   * 適用於Adobe Commerce開發的MCP伺服器整合
   * 用於增強開發體驗的游標IDE規則
   * Commerce專屬的開發工具和工作流程

   下列檔案會新增至您的工作區：

   * MCP組態： `.cursor/mcp.json`
   * 規則目錄： `.cursor/rules/`

## 安裝後設定

1. 重新啟動Cursor IDE以載入新的MCP工具和組態。

1. 確認規則存在於`.cursor/rules/`資料夾下，以驗證安裝。

1. 啟用MCP伺服器：

   * 使用&#x200B;**Cmd+Shift+P** (macOS)或&#x200B;**Ctrl+Shift+P** （Windows和Linux）開啟「游標MCP設定」。
   * 型別&#x200B;**檢視：開啟MCP設定**
   * 在清單中找到&#x200B;**commerce-extensibility MCP伺服器**
   * 切換伺服器&#x200B;**開啟**&#x200B;以啟用編碼工具

1. 驗證伺服器狀態 — Commerce擴充性MCP伺服器應顯示為：

   ```terminal
   Status: Connected/Active
   Server: commerce-extensibility
   Configuration: Automatically configured via .cursor/mcp.json
   ```

## 範例提示

下列範例提示會建立擴充功能，以便在下訂單時傳送通知。

```terminal
Implement an Adobe Commerce SaaS extension that will send an ERP notification when a customer places an order. The ERP notification must be sent as a POST HTTP call to <ERP URL> with the following details in the request JSON body:

Order ID -> orderID
Order Total -> total
Customer Email ID -> emailID
Payment Type -> pType
```

## 最佳實務

Adobe建議您在使用AI編碼工具時，遵循下列最佳實務：

### 檢查清單

開始任何開發工作階段之前：

* 檢查`REQUIREMENTS.md`
* 驗證MCP工具是否正常運作
* 檢閱目前階段和目標
* 從範常式式碼或支架專案開始

開發期間：

* 信任四階段[通訊協定](#protocol)
* 請求複雜開發的實作計畫
* 使用MCP工具（可用時）
* 實施後測試每個功能
* 先在本機測試，然後再次部署和測試
* 運用編碼工具進行測試支援
* 問題不必要的複雜性
* 以漸進方式部署，加快開發速度

開始新聊天時：

* 提供正確的工作階段交接
* 具有`@`的參考金鑰檔案
* 設定作業階段的明確目標
* 使用以階段為基礎的邊界

### 工作流程

使用AI編碼工具進行開發時，請從範常式式碼或支架專案開始。 此方法可確保您以堅實的基礎為基礎進行建置，而不是從零開始，同時也會最佳化您的AI開發工作流程。

這也允許您利用Adobe的範本，並以經過驗證的模式和架構為基礎，同時保留既定的目錄結構和慣例。

請參閱下列資源，以開始使用：

* [整合入門套件](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/create-integration)
* [Adobe Commerce入門套件範本](https://github.com/adobe/adobe-commerce-samples/tree/main/starter-kit)
* [Adobe I/O Events入門範本](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/io-events/getting-started-io-events)
* [App Builder範例應用程式](https://developer.adobe.com/app-builder/docs/resources/sample_apps)

#### 為何應使用這些資源

* **已驗證的模式**：入門套件包含Adobe的最佳實務和架構決策
* **加快開發**：減少花費在樣版和設定上的時間
* **一致性**：確保您的擴充功能遵循既定的慣例
* **可維護性**：遵循標準模式時，更容易維護和更新
* **檔案**：入門套件附有範例和檔案
* **社群支援**：使用標準方式時更容易取得協助
* **AI內容效率**：使用熟悉的模式和結構來運作，減少大量說明的需求，並改善程式碼產生準確性
* **減少Token使用量**：參考現有的模式，而不是從頭開始產生所有內容，因此對話更有效率，內容摘要較少

### 通訊協定

規則系統會自動強制執行下列四個階段的通訊協定。 開發擴充功能時，工具應自動遵循此通訊協定：

* 第1階段：需求分析與釐清
   * 詢問澄清問題時，請提供完整的答案。
* 第2階段：架構規劃與使用者核准
   * 提出計畫時，請在核准前仔細檢閱計畫。
* 階段3：程式碼產生和實施
* 第4階段：檔案與驗證

### 請求複雜開發的實作計畫

對於涉及多個執行階段動作、接觸點或整合的複雜開發，會明確要求AI工具建立詳細的實作計畫。 當您在[階段2](#protocol)中看到包含多個元件的高階計畫時，請要求詳細的實作計畫，以將其細分為可管理的工作：

```terminal
Create a detailed implementation plan for this complex development.
```

複雜的Adobe Commerce擴充功能通常涉及：

* 多個執行階段動作
* 跨多個接觸點的事件設定
* 與外部系統整合
* 狀態管理需求
* 跨多個元件測試

### 使用MCP工具

工具預設為MCP工具，但在特定情況下，可以使用CLI指令代替。 如果您想要確保MCP工具的使用情況，請在提示中明確要求使用。

如果您看到正在使用CLI指令且想要改用MCP工具，請使用下列提示：

```terminal
Use only MCP tools and not CLI commands
```

* MCP工具： aio-app-deploy、aio-app-dev、aio-dev-invoke
* CLI命令： aio app deploy， aio app dev

CLI命令可用於下列情況：

* 複雜的部署案例
* 偵錯特定問題
* 當MCP工具具有限制時
* 不受MCP整合影響的一次性作業

### 開發

請務必質疑AI工具所造成的不必要的複雜性。

為簡單的唯讀端點新增不必要的檔案(`validator.js`、`transformer.js`、`sender.js`)時，請使用下列提示：

```terminal
Why do we need these files for a simple read-only endpoint?
Perform a root cause analysis before adding complexity
Verify if simpler solutions exist
```

### 測試

測試時請使用下列最佳實務：

#### 實施後測試每個功能

完成實作計畫中的功能開發後，請立即測試。 及早測試可避免複合問題，並簡化偵錯作業。

* 請勿等到所有功能都完成才使用
* 逐步測試以及早發現問題
* 在移到下一個功能之前驗證功能

#### 先在本機測試

一律先使用`aio-app-dev`工具在本機測試。 這可提供即時的意見反應，並允許更快的疊代週期、更輕鬆的偵錯，且沒有部署額外負荷。

1. 啟動本機開發伺服器：

   ```bash
   aio-app-dev
   ```

1. 本機測試動作：

   ```bash
   aio-dev-invoke action-name --parameters '{"test": "data"}'
   ```

#### 再次部署和測試

本機測試成功後，在執行階段環境中進行部署和測試。 執行階段環境的行為可能與本機開發不同。

1. 部署至執行階段：

   ```bash
   aio-app-deploy
   ```

1. 測試已部署的動作

1. 使用網頁瀏覽器或直接HTTP請求

1. 檢查啟動記錄檔以進行偵錯

#### 運用編碼工具進行測試支援

請求測試方面的協助。 這些工具可協助您針對特定執行階段動作進行除錯、記錄分析和建立適當的測試資料。

**測試執行階段動作**：

```terminal
Help me test the customer-created runtime action running locally
```

**偵錯失敗**：

```terminal
Why did the subscription-updated runtime action activation fail?
```

**檢查記錄**：

```terminal
Help me check the logs for the last stock-monitoring runtime action invocation
```

**建立測試承載**：

```terminal
Generate test data for this Commerce event
```

```terminal
Create a test payload for the customer_save_after event
```

**尋找執行階段端點**：

```terminal
What's the URL for this deployed action?
```

**處理驗證**：

```terminal
How do I authenticate with this external API?
```

**疑難排解**：

```terminal
Help me debug why this action is returning 500 errors
```

### 偵錯

停止並評估何時發生錯誤。 如果您遇到問題：

* 停止並評估 — 不要在中斷狀態中繼續
* 檢查記錄 — 使用啟用記錄來識別問題
* 簡化 — 移除複雜性以隔離問題
* 逐步測試 — 一次修正一個問題
* 驗證 — 繼續前先測試每個修正

### 部署

部署時請遵循下列最佳實務：

#### 逐步部署

僅部署已修改的動作以加速開發。 這樣就能降低中斷現有功能的風險，並更快速地提供變更意見回饋。 這也會降低中斷現有功能的風險。

* 使用MCP工具來部署特定動作

  ```bash
  aio-app-deploy --actions action-name
  ```

* 在本機測試後部署個別動作
* 以漸進方式部署，並避免在開發期間進行完整應用程式部署

#### 執行階段清理

進行重大變更後，請善用工具來清除孤立的動作。 讓AI工具系統地處理清理程式，它能夠有效地識別孤立的動作，驗證其狀態，並安全地移除它們而無需手動干預。

```terminal
Help me identify and clean up orphaned runtime actions
```

請求AI工具列出已部署的動作並識別未使用的動作

```terminal
List all deployed actions and identify which ones are no longer needed
```

讓AI工具使用適當的指令移除孤立的動作

```terminal
Remove the orphaned actions that are no longer part of the current implementation
```

### 監視

監視應用程式時，請使用下列最佳實務：

#### 留意內容品質指標

* **良好的內容**： AI會記住最近的決策，參考正確的檔案
* **不良內容**： AI要求先前提供的資訊，重複已解決的問題

#### 追蹤開發速度

* **高速**：進度清楚，需要最低限度的說明
* **低速度**：重複解釋、AI混淆、進度緩慢

#### 監控成本效益

追蹤權杖使用模式：

* **有效率**：權杖使用量低，內容摘要很少
* **低效率**：高語彙基元使用量、多重摘要、重複工作

## 避免什麼

使用AI編碼工具時，您應該避免以下反圖樣：

* **不要略過澄清階段** — 一律確保階段1在實施前完成。
* **在每個功能之後不要略過測試** — 逐步測試，不要等到所有功能都完成。
* **若沒有根本原因分析，請勿增加複雜性** — 詢問不必要的檔案新增問題，並要求進行適當的調查。
* **沒有實際資料測試就不要宣告成功** — 一律使用實際資料進行測試，而不僅僅是邊緣案例。
* **不要忘記執行階段清除** — 在重大變更後永遠清除孤立的動作。
