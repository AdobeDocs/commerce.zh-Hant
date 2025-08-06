---
title: 設定您的店面
description: 瞭解如何執行支架工具來設定您的 [!DNL Adobe Commerce as a Cloud Service] 店面。
role: Developer
exl-id: 02928dc4-1777-483e-b0ee-b04fc813864d
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案(Adobe管理的SaaS基礎結構)。"
source-git-commit: 47eb8ee55bb093767f76aa23df8bb347ee280aae
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 0%

---

# 設定您的店面

下列步驟示範如何使用`aio commerce init`命令快速設定由Edge Delivery支援的Adobe Commerce店面。 此程式會設定下列專案：

* [由Edge Delivery Services提供支援的Commerce店面](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/) — 由Adobe的Edge Delivery Services提供支援的效能、可擴充且安全的店面。
* [適用於Adobe Developer App Builder的API Mesh](https://developer.adobe.com/graphql-mesh-gateway/mesh/) — 這個API平台可讓開發人員將多個資料來源合併為單一GraphQL端點。 API Mesh透過單一閘道，使用Adobe API協調協力廠商API。 對單一GraphQL端點的一個查詢可以傳回來自多個來源的結果。
* [Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/) — 具有存取API、事件、執行階段函式和外掛程式的開發人員工具集合，您可以使用這些工具來建置Adobe應用程式的專案。
* [Adobe I/O Runtime](https://developer.adobe.com/runtime/docs/) — 用於部署自訂程式碼的無伺服器引擎，可回應事件並執行雲端中的函式。

## 先決條件

執行`aio commerce init`命令之前，您必須先完成下列必要條件：

1. 安裝節點版本管理員(NVM)。

   ```bash
   curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
   ```

1. 安裝Node.js和NPM。 如需詳細資訊，請參閱[Node.js](https://nodejs.org/en/)。

   ```bash
   nvm install 22
   ```

   ```bash
   npm install -g npm
   ```

1. 安裝[Adobe I/O Runtime CLI](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/)。

   ```bash
   npm install -g @adobe/aio-cli
   ```

1. 安裝Adobe I/O API網狀外掛程式。

   ```bash
   aio plugins:install @adobe/aio-cli-plugin-api-mesh
   ```

1. 安裝Adobe I/O Commerce外掛程式。

   ```bash
   aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce
   ```

1. 更新任何現有的外掛程式。

   ```bash
   aio plugins:update
   ```

1. 登入您的Adobe Experience Cloud帳戶。

   ```bash
   aio login
   ```

   如果`aio login`命令未啟動瀏覽器視窗，請參閱[疑難排解](#troubleshooting)區段。

1. 選取IMS組織、專案和工作區。 使用方向鍵並按&#x200B;**Enter**&#x200B;進行選擇。 如需`aio`命令的詳細資訊，請參閱[Adobe I/O CLI檔案](https://github.com/adobe/aio-cli-plugin-console?tab=readme-ov-file#commands)。

   ```bash
   aio console org select
   ```

   ```bash
   aio console project select
   ```

   ```bash
   aio console workspace select
   ```

1. 若尚未接受，請導覽至https://developer.adobe.com/console/home並按一下&#x200B;**「接受並繼續**」，以接受Adobe Developer主控台中的「開發人員使用條款」。

## 執行`aio commerce init`命令

執行以下命令，將為您的Commerce店面建立支架。 此支架是您建立和瞭解店面的絕佳起點。 如需使用店面的詳細資訊，請參閱[Adobe Commerce店面檔案](https://experienceleague.adobe.com/developer/commerce/storefront/)。


1. 執行`init`命令：

   ```bash
   aio commerce init
   ```

1. 如果您已登入GitHub，請輸入`Y`以在您的使用者名稱下建立存放庫。

1. 輸入您要建立的存放庫名稱。

1. 選取下列其中一個選項：

   * **使用示範Adobe Commerce租使用者** — 使用示範租使用者。
      * 如果選取此選項，系統會提示您於瀏覽器視窗中安裝AEM程式碼同步機器人。 您必須指定您建立的存放庫並授權機器人。 返回CLI並輸入`y`以確認AEM程式碼同步機器人安裝。
   * **挑選可用的Adobe Commerce租使用者** — 在選取的組織中選取現有的Commerce租使用者。
      * 如果選取此選項，則必須選取要在其中建立網格的專案和工作區。
   * **提供您自己的Adobe Commerce租使用者API URL** — 如果您是試用存取計畫參與者，請選取此選項。 輸入Adobe入門電子郵件中提供的API URL。

   >[!NOTE]
   >
   >如果您選取`Pick an available API (Mesh -> SaaS)`選項，則Adobe Developer Console中必須有現有的專案和Workspace。 [建立樣板化專案](https://developer.adobe.com/developer-console/docs/guides/projects/projects-template/)並選取App Builder會自動建立必要的工作區。

1. 程式完成後，您可以使用以下方法自訂店面：

   * 自訂您的程式碼： `https://github.com/<username or org>/<repo name>`
   * 編輯您的內容： `https://da.live/#/<username or org>/<repo name>`
   * 管理您的設定： `https://da.live/sheet#/<username or org>/<repo name>/configs-stage`
   * 預覽您的店面： `https://main--<repo name>--<username or org>.aem.page/`
   * 本機執行： `aio commerce:dev`

若要自訂您的店面，請參閱[Adobe Commerce店面檔案](https://experienceleague.adobe.com/developer/commerce/storefront/)。

## 疑難排解

如果您遇到`aio login`命令的問題，Adobe建議完全登出CLI和瀏覽器，然後重新登入。

1. 若要登出CLI，請執行：

   ```bash
   aio logout
   ```

1. 在您的瀏覽器中，導覽至[Adobe Developer Console](https://developer.adobe.com/console)，按一下右上角的設定檔圖示，然後選取&#x200B;**登出**。

1. 返回CLI並再次執行`aio login`命令，這會啟動瀏覽器視窗以登入。 然後，您可以繼續選取您的組織、專案和工作區。

   ```bash
   aio console org select
   ```

   ```bash
   aio console workspace select
   ```

   ```bash
   aio console project select
   ```

## 後續步驟

如需詳細資訊，請參閱下列文章：

* 若要進一步瞭解如何管理和顯示店面中的內容和資料，請參閱[更新店面內容](./use-cases.md#update-storefront-content)。
* 如需內容實驗功能的詳細資訊，請參閱[內容實驗](./use-cases.md#contextual-experimentation)。
* 如需使用Generative AI自動產生高品質內容的詳細資訊，請參閱[產生變數](./use-cases.md#generate-variations)。
* 若要進一步瞭解如何更新網站內容以及與Commerce前端元件和後端資料整合，請參閱[Adobe Commerce Storefront檔案](https://experienceleague.adobe.com/developer/commerce/storefront/)。
