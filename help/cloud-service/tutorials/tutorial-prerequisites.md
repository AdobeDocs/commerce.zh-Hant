---
title: 教學課程必要條件
description: 瞭解Adobe Commerce as a Cloud Service教學課程的先決條件和設定步驟，包括擴充功能和店面開發工具。
solution: Commerce
feature: App Builder, Cloud
feature-set: Commerce
role: Developer
level: Intermediate
type: Tutorial
source-git-commit: 0ece7b58bdafd664297cbdee809c53ef2389fb12
workflow-type: tm+mt
source-wordcount: '1217'
ht-degree: 0%

---

# 教學課程必要條件

此頁面列出[!DNL Adobe Commerce as a Cloud Service]教學課程的先決條件和設定步驟，例如[評等延伸教學課程](./ratings-extension.md)和[送貨方法延伸教學課程](./shipping-method-extension.md)。

## 一般必要條件

在本教學課程中，擴充功能和店面開發都需要下列工具。

* [!DNL Node.js] （版本`22.x.x`）和npm （`9.0.0`或更新版本）：使用下列命令驗證您的安裝：

  ```bash
  node --version
  npm --version
  ```

* 安裝[Git](https://git-scm.com) — 確認您的安裝：

  ```bash
  git --version
  ```

* Bash shell
   * macOS/Linux：不需要安裝
   * Windows：使用[Git Bash](https://git-scm.com/install)或Linux (WSL) [的](https://learn.microsoft.com/en-us/windows/wsl/install)Windows子系統

* 下載AI輔助的IDE，例如[Cursor](https://cursor.com/download) （建議使用）。 也支援其他IDE，例如Claude Code、Gemini CLI或Copilot，但可能需要修改提示和教學課程中的其他步驟。

## [!DNL Adobe Commerce as a Cloud Service]必要條件

* 安裝[!DNL Adobe I/O CLI]

  ```bash
  npm install -g @adobe/aio-cli
  ```

* 安裝[Adobe I/O CLI Commerce](https://github.com/adobe-commerce/aio-cli-plugin-commerce)、[Adobe I/O CLI Runtime](https://github.com/adobe/aio-cli-plugin-runtime)和[App Builder CLI](https://github.com/adobe/aio-cli-plugin-app-dev)外掛程式：

  ```bash
  aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce @adobe/aio-cli-plugin-app-dev @adobe/aio-cli-plugin-runtime
  ```

安裝[!DNL Adobe I/O CLI]和必要的外掛程式之後，請設定您的擴充性工作區。 Adobe建議使用自動化設定，以獲得最快的體驗。

* **[自動設定](#automated-setup) （建議）** — 執行單一命令以自動設定您的工作區。
* **[手動設定](#manual-setup)** — 依照逐步指示個別設定每個元件。

### 自動化設定（建議） {#automated-setup}

>[!TIP]
>
>如果您遇到自動化安裝的問題，請遵循下列[手動安裝](#manual-setup)步驟。

`app-setup`命令會自動執行工作區設定程式，包括建立[!DNL Adobe Developer Console]專案、新增必要的API、設定[!DNL Adobe I/O CLI]、複製入門套件、連線本機工作區，以及安裝可擴充性的AI工具。

`app-setup`命令會引導您完成下列步驟：

* 選擇或建立具有必要API的[!DNL Adobe Developer Console]專案
* 使用您的組織、專案和工作區設定[!DNL Adobe I/O CLI]
* 複製適當的入門套件並設定專案
* 設定環境並將本機工作區連線到遠端工作區
* 安裝Commerce擴充性工具和編碼代理程式技能

執行以下命令，並遵循互動式提示：

```bash
aio commerce extensibility app-setup
```

命令完成後，瀏覽至您的專案目錄並重新啟動編碼代理程式，以載入新的MCP工具和技能。 如果您的教學課程需要店面，請重新執行命令並選取[!DNL AEM Boilerplate Commerce]入門套件。

以下範例安裝顯示簽出入門套件之互動式提示和輸出。

+++範例安裝（結帳入門套件）

```shell-session
aio commerce extensibility app-setup

🚀 Adobe Commerce Extensibility App Setup

✔ Logged in
📁 Working directory: /Users/username/projects/my-commerce-project

✔ Which starter kit would you like to use? Checkout Starter Kit
✔ Enter a name for your project directory: my-extension
✔ Which coding agent would you like to install the skills for? Cursor

📦 Cloning Checkout Starter Kit...
   ✔ Repository cloned
   Using npm (package-lock.json found)
   ✔ Dependencies installed

📋 Current Adobe I/O Console configuration:
   Org: My Organization (1234567)
   Project: My Commerce Project (1234567890123456789)
   Workspace: Stage (9876543210987654321)
✔ Do you want to continue with this configuration? (Answer "No" to select a different org/project/workspace)
No

🔧 Selecting Adobe I/O Console org, project, and workspace...

? Select Org: My Organization
Org selected My Organization
You are currently in:
1. Org: My Organization
2. Project: <no project selected>
3. Workspace: <no workspace selected>

? Select Project: My Commerce Project
Project selected : My Commerce Project
You are currently in:
1. Org: My Organization
2. Project: My Commerce Project
3. Workspace: <no workspace selected>

? Select Workspace: Stage
Workspace selected Stage
You are currently in:
1. Org: My Organization
2. Project: My Commerce Project
3. Workspace: Stage

✅ Console configured:
   Org: My Organization
   Project: My Commerce Project
   Workspace: Stage

🔐 Configuring workspace credentials and services...
   ✔ Workspace configuration loaded
   ✔ OAuth server-to-server credentials already configured
   ✔ All required services available in organization
   ✔ Subscribed to: Adobe Commerce as a Cloud Service

📋 Configuring Checkout Starter Kit...
   Creating .env from env.dist...
✔ Select tenant (type to search) My Commerce Instance:
https://<region>.api.commerce.adobe.com/<tenant-id>/graphql
   ✔ Commerce instance configured
✔ Enter the event prefix for your workspace: my-prefix
   ✔ Workspace IDs configured
   ✔ OAuth credentials configured
   ✔ Checkout Starter Kit configured

🔧 Installing Commerce Extensibility tools and agent skills...
   ✔ Commerce Extensibility tools installed

🎉 App setup complete!

📁 Project directory: /Users/username/projects/my-commerce-project/my-extension

Next steps:
   1. cd into your project directory
   2. Restart your coding agent to load the Commerce Extensibility tools and skills
```

+++

### 手動設定 {#manual-setup}

以下幾節將說明如何手動設定擴充性工作區的每個元件。 如果您偏好手動設定，或遇到[自動安裝程式](#automated-setup)的問題，請依照下列步驟進行。

### Adobe Developer Console必要條件

在Adobe Developer Console中設定具備必要API和憑證的專案。

1. 導覽至[Adobe Developer Console](https://developer.adobe.com/console){target="_blank"}。
1. 使用您的電子郵件和密碼登入。

#### 建立新專案

在Adobe Developer Console中建立App Builder專案，以託管您的擴充功能。

1. 導覽至[Adobe Developer Console](https://developer.adobe.com/)。
1. 按一下&#x200B;**[!UICONTROL Create project from a template]**。
1. 選取&#x200B;**[!UICONTROL App Builder]**&#x200B;範本。
1. 輸入&#x200B;**[!UICONTROL Project Title]**&#x200B;和&#x200B;**[!UICONTROL App Name]**。
1. 請確定已標示&#x200B;**[!UICONTROL Include Runtime]**&#x200B;核取方塊。

   ![已選取Adobe Developer Console範本的App Builder專案建立](../assets/app-builder-template.png){width="600" zoomable="yes"}

1. 按一下&#x200B;**[!UICONTROL Save]**。

#### 將API新增至工作區

將必要的API新增到您的Stage工作區，以進行事件管理和Commerce整合。

1. 按一下&#x200B;**[!UICONTROL Stage]**&#x200B;工作區，然後對每個API重複下列步驟。

   ![為API使用新增服務選項來暫存工作區](../assets/add-apis-workspace.png){width="600" zoomable="yes"}

1. 按一下&#x200B;**[!UICONTROL Add Service]**&#x200B;並選取&#x200B;**[!UICONTROL API]**。

1. 選取下列其中一個API。 請對下列每個API重複此程式：

   * **[!UICONTROL Adobe Services]**&#x200B;篩選器：
      * **[!UICONTROL I/O Management API]**
      * **[!UICONTROL I/O Events]** API
   * **[!UICONTROL Experience Cloud]**&#x200B;篩選器：
      * **[!UICONTROL Adobe I/O Events for Adobe Commerce]** API

1. 按一下&#x200B;**[!UICONTROL Next]**。

1. 按一下&#x200B;**[!UICONTROL Save configured API]**。

1. 重複上述步驟，直到您將所有API新增至工作區為止。

   ![Workspace顯示所有必要的API，已成功新增](../assets/apis-added.png){width="600" zoomable="yes"}

### 設定Adobe I/O CLI

將[!DNL Adobe I/O CLI]連線到您的組織、專案和工作區。

1. 清除任何現有設定：

   ```bash
   aio config clear
   ```

1. 使用[!DNL Adobe I/O CLI]登入：

   ```bash
   aio auth login -f
   ```

1. 使用下列每一個命令選取您的組織、專案和工作區：

   ```bash
   aio console org select
   ```

   ```bash
   aio console project select
   ```

   ```bash
   aio console workspace select
   ```

   ![終端機顯示Adobe I/O CLI組織專案和工作區選擇](../assets/cli-configuration.png){width="600" zoomable="yes"}

### 複製入門套件

為您正在建置的擴充功能複製以下Commerce starter kit存放庫之一，並準備您的專案：

整合入門套件：

```bash
git clone https://github.com/adobe/commerce-integration-starter-kit.git extension
cd extension
```

結帳入門套件：

```bash
git clone https://github.com/adobe/commerce-checkout-starter-kit.git extension
cd extension
```

>[!BEGINTABS]

>[!TAB 整合入門套件]

### 建立.env檔案

建立您的環境設定檔：

```bash
cp env.dist .env
```

在文字編輯器中開啟`.env`檔案，並新增下列OAuth認證：

```bash
OAUTH_CLIENT_ID=
OAUTH_CLIENT_SECRET=
OAUTH_TECHNICAL_ACCOUNT_ID=
OAUTH_TECHNICAL_ACCOUNT_EMAIL=
OAUTH_ORG_ID=
```

按一下工作區上的「**[!UICONTROL Credential details]**」索引標籤，從[Developer Console](https://developer.adobe.com/)的「**[!UICONTROL OAuth Server-to-Server]**」頁面複製這些值。

Adobe Developer Console中的![OAuth伺服器對伺服器認證頁面](../assets/oauth-credentials.png){width="600" zoomable="yes"}

#### 新增Commerce設定

將下列Commerce執行個體詳細資料新增至您的`.env`檔案：

```bash
COMMERCE_BASE_URL=
COMMERCE_GRAPHQL_ENDPOINT=
```

若要尋找這些值，請執行下列步驟：

1. 導覽至[Commerce Cloud服務執行個體](https://experience.adobe.com/#/@commerce/commerce/cloud-service/instances)。
1. 按一下執行個體旁的資訊圖示。
1. 將REST端點復製為`COMMERCE_BASE_URL`。
1. 將GraphQL端點復製為`COMMERCE_GRAPHQL_ENDPOINT`。

#### 設定事件前置詞

設定事件首碼的暫時值：

```bash
EVENT_PREFIX=test
```

### 下載工作區設定

執行以下命令來下載工作區組態檔：

```bash
aio console workspace download workspace.json
```

將工作區組態檔複製到`scripts`目錄：

```bash
cp workspace.json scripts/
```

### 將本機工作區連線到遠端工作區

將您的本機專案連結至遠端工作區：

```bash
aio app use workspace.json -m
```

![終端機顯示成功的工作區連線與aio應用程式使用命令](../assets/connect-workspace.png){width="600" zoomable="yes"}

>[!TAB 結帳入門套件]

### 將本機工作區連線到遠端工作區

將您的本機專案連結至遠端工作區。 從專案根目錄（`extension`資料夾），執行：

```bash
aio app use --merge
```

出現提示時，選擇使用您在設定Adobe I/O CLI時所選取之組織、專案和工作區的選項。 這會將工作區設定寫入您的應用程式中，以便部署和本機開發使用該工作區。

![終端機顯示成功的工作區連線與aio應用程式使用命令](../assets/connect-workspace.png){width="600" zoomable="yes"}

>[!ENDTABS]

### 安裝擴充性AI工具

此程式會建立MCP組態(`.<agent>/mcp.json`)、技能目錄(`.<agent>/skills/`)，並將`AGENTS.md`新增至專案根目錄。 系統會提示您選擇入門套件、編碼代理程式和封裝管理員。


1. 使用以下命令在`extension`資料夾中設定AI輔助開發工具：

   ```bash
   cd extension
   ```

   ```bash
   aio commerce extensibility tools-setup
   ```

   ![顯示AI擴充工具設定命令輸出的終端機](../assets/install-ai-tools.png){width="600" zoomable="yes"}

1. 安裝完成之後，請重新啟動編碼代理程式，讓它載入新的MCP工具和技能。 Commerce App Builder工具現在可在您的環境中使用。

   >[!NOTE]
   >
   >如果您看到開機套件找不到任何技能的警告，表示發生錯誤，這通常是因為安裝程式是在開機套件複製位置以外的資料夾中執行。 從`aio commerce extensibility tools-setup`資料夾（入門套件專案根目錄）執行`extension`，並在出現提示時選取適當的入門套件。

   ![終端機顯示設定了AI擴充性工具，並選取結帳啟動套件](../assets/tools-setup-checkout.png){width="600" zoomable="yes"}

## 店面手動設定

本節說明如何手動設定[Ratings擴充功能教學課程](./ratings-extension.md)和其他店面教學課程的店面。

若要自動設定店面，請執行`app-setup`自動化設定[區段中說明的](#automated-setup)命令，並選取[!DNL AEM Boilerplate Commerce]入門套件。

### 先決條件

若要完成[評等延伸教學課程](./ratings-extension.md#connect-to-the-storefront)的[店面](./ratings-extension.md)區段，並在您的商店中顯示產品評等，必須執行下列專案。

* [Google Chrome](https://www.google.com/chrome/) — 測試店面所需

* 連線到您[!DNL Commerce]執行個體的店面專案。 如果您沒有店面專案，請依照[建立店面](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/?lang=zh-Hant){target="_blank"}中的步驟進行，包括[連結商務資料的存放庫](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/?lang=zh-Hant#link-repo-to-commerce-data){target="_blank"}區段。

### 複製店面存放庫

開啟終端機並複製存放庫：

```bash
git clone https://github.com/hlxsites/aem-boilerplate-commerce.git storefront
cd storefront
```

### 安裝相依性

安裝專案相依性：

```bash
npm install
```

### 安裝店面AI工具

在`storefront`資料夾中設定AI輔助開發工具。

從樣板專案的根目錄執行以下命令。 命令會將`@adobe-commerce/commerce-extensibility-tools`套件安裝為開發相依性、將技能檔案複製到代理程式的技能目錄中，以及設定MCP （模型內容通訊協定），讓您的代理程式可以存取Commerce檔案搜尋工具。

```bash
aio commerce extensibility tools-setup
```

指令會引導您完成兩個提示：

1. **選取入門套件** — 選擇&#x200B;**AEM樣板Commerce**。

1. **選取編碼代理程式** — 從支援的代理程式清單中選擇您的代理程式。
