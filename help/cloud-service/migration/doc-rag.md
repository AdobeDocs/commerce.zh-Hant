---
title: 檔案RAG服務
description: 瞭解如何使用AI支援的檔案搜尋服務來進行Adobe Commerce開發。
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案(Adobe管理的SaaS基礎結構)。"
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 28396828516645abec3b42a2c6874afe9134dfb8
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---

# 檔案RAG服務(Beta)

>[!NOTE]
>
>檔案RAG服務目前在Beta中，體驗可能會有所變更。

檔案RAG (Retrieval-Enhanced Generation)服務提供相關Adobe Commerce和App Builder檔案中的AI支援語意搜尋功能。

此RAG提供IDE介面來詢問有關Adobe Commerce的問題，並可提供開發應用程式和其他移轉工作的最佳實務建議。

RAG服務是[Commerce擴充性工具](./coding-tools.md) MCP （模型內容通訊協定）伺服器的一部分，該伺服器與Cursor和其他與MCP相容的AI助理整合。

## 可用檔案

下表說明RAG服務目前索引的檔案，以及可用來觸發搜尋關聯索引的關鍵字。 隨著我們開發RAG服務，隨附的檔案內容將會持續擴展。

| 類別 | 索引 | 包含的內容 | 關鍵字 |
|-------|---------|---------|------------------------|
| [店面](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=zh-Hant) | commerce-storefront-docs | Edge Delivery Services、下拉式清單、店面元件 | 店面、外掛程式、EDS、產品清單、結帳 |
| [擴充性](https://developer.adobe.com/commerce/extensibility/) | commerce-extensibility-docs | Webhook、活動、擴充功能、整合 | webhook，事件，擴充功能， API網格， GraphQL |
| [Commerce](https://experienceleague.adobe.com/zh-hant/docs/commerce/cloud-service/overview) | commerce-core-docs | 核心Commerce （目錄、客戶、訂單） | 目錄，產品，客戶，訂單，存貨 |
| [App Builder](https://developer.adobe.com/app-builder/docs/intro_and_overview/) | app-builder-docs | App Builder、執行階段動作、UI擴充功能 | 應用程式產生器，執行階段動作， React Spectrum |

如需索引選取的詳細資訊，請參閱[自動索引選取](#automatic-index-selection-recommended)和[明確索引選取](#explicit-index-selection)。

如需每個索引中所包含檔案的詳細資訊，請參閱[擷取的來源清單](https://github.com/adobe-commerce/azure-commerce-documentation-agent/blob/develop/docs/INGESTED_SOURCES.md)。

## 安全性與隱私權

* **IMS驗證** — 所有API呼叫都使用Adobe IMS OAuth2 Token。
* **沒有資料儲存體** - MCP伺服器未儲存任何認證或資料。
* **本機執行** — 所有工具都在您的電腦上本機執行。
* **安全通訊** — 檔案搜尋使用HTTPS搭配權杖驗證。

生產端點受[Azure前門](https://learn.microsoft.com/en-us/azure/frontdoor/front-door-overview)保護，包括下列保護：

* 具有Microsoft預設規則集2.1和機器人管理員規則集1.0的Web應用程式防火牆(WAF)
* 封鎖美國禁運地區（古巴、伊朗、朝鮮、敘利亞、克里米亞、盧甘斯克、頓涅茨克）的地理
* 邊緣的DDoS保護
* API管理後端已鎖定為僅接受來自前門的流量

針對不同的安全性需求，您可以使用自訂端點。 如需詳細資訊，請參閱[自訂前門端點](#custom-front-door-endpoint)。

## 先決條件

安裝之前，請確定您擁有：

* [Node.js](https://nodejs.org/en/download){target="_blank"} 18+ （建議使用LTS）
* [Cursor IDE](https://cursor.com/download){target="_blank"} （建議）或其他與MCP相容的IDE

  >[!NOTE]
  >
  >雖然支援其他MCP相容的IDE，但為獲得最佳體驗，建議使用Cursor。 如果您使用其他IDE，則需要修改檔案中的提示和其他步驟，才能使用您選取的IDE。

## 安裝

1. 全域安裝[Adobe I/O CLI](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/)：

   ```bash
   npm install -g @adobe/aio-cli
   ```

1. 使用Adobe IMS進行驗證：

   ```bash
   aio auth login
   ```

1. 複製Commerce擴充功能工具存放庫，並導覽至目錄：

   ```bash
   git clone https://github.com/adobe-commerce/commerce-extensibility-tools.git
   cd commerce-extensibility-tools
   ```

1. 安裝相依性：

   ```bash
   npm install
   ```

1. 在您的Commerce專案目錄中建立或更新`.cursor/mcp.json` （非全域）以包含`commerce-extensibility-tools` MCP伺服器：

   ```json
   {
     "mcpServers": {
       "commerce-extensibility-tools": {
         "command": "node",
         "args": [
           "/<your-project-directory>/commerce-extensibility-tools/index.js"
         ],
         "env": {
           "NODE_ENV": "production"
         }
       }
     }
   }
   ```

   請確定您將`<your-project-directory>`取代為您複製存放庫的實際路徑。

   >[!NOTE]
   >
   >在Windows上，如果您在提供專案目錄的路徑時遇到問題，請參閱[路徑問題疑難排解](#path-issues-windows)。

1. 重新啟動Cursor IDE以載入MCP伺服器。

1. 詢問AI助理以驗證安裝：

   ```shell-session
   Can you show me the available Adobe Commerce tools?
   ```

## 使用情況

安裝之後，您可以自動呼叫索引[&#128279;](#automatic-index-selection-recommended)或[明確](#explicit-index-selection)。 您也可以使用[`/search-commerce-docs`命令](#command-based-search)。

>[!NOTE]
>
>RAG服務會傳回前5個最相關的結果。

### 自動選取索引（建議）

若詢問您Commerce專案的自然語言問題，此工具會自動搜尋適當的檔案索引並提供相關資訊：

>[!BEGINSHADEBOX]

下列提示會自動選取`commerce-storefront-docs`索引：

```shell-session
"How do I use Edge Delivery Services drop-ins for product listing?"
```

下列提示會自動選取`commerce-extensibility-docs`索引：

```shell-session
"How do I create a webhook in Adobe Commerce?"
```

下列提示會自動選取`commerce-core-docs`索引：

```shell-session
"How to configure product catalog settings?"
```

下列提示會自動選取`app-builder-docs`索引：

```shell-session
"What are App Builder runtime action best practices?"
```

>[!ENDSHADEBOX]

### 明確選取索引

或者，您可以指定要在提示中使用的索引。

```shell-session
Search commerce-storefront-docs for authentication drop-in
```

```shell-session
Using app-builder-docs, how do I deploy runtime actions?
```

### 命令式搜尋

如果您要確保使用RAG服務，可以手動叫用`/search-commerce-docs` Cursor命令以搜尋包含提示字元的檔案：

```shell-session
/search-commerce-docs "How do I subscribe to Commerce events?"
```

## 自訂前門端點

依預設，檔案搜尋會使用具有WAF保護的生產[Azure Front Door](https://learn.microsoft.com/en-us/azure/frontdoor/front-door-overview)端點。 為了測試或開發目的，您可以使用`FRONT_DOOR_URL`環境變數覆寫此專案。

若要使用自訂端點，請將其新增至您的Cursor MCP設定：

```json
{
  "mcpServers": {
    "commerce-extensibility-tools": {
      "command": "node",
      "args": ["/<your-project-directory>/commerce-extensibility-tools/index.js"],
      "env": {
        "NODE_ENV": "production",
        "FRONT_DOOR_URL": "https://<custom-endpoint>.azurefd.net"
      }
    }
  }
}
```

>[!NOTE]
>
>大部分開發人員應該使用預設的生產端點，而不需要設定`FRONT_DOOR_URL`變數。

## 疑難排解

以下小節提供使用檔案RAG服務時可能遇到的常見問題的疑難排解提示。

### 驗證錯誤

檔案搜尋工具需要Adobe IMS驗證。 如果您遇到驗證錯誤，請使用下列步驟來疑難排解並解決問題。

1. 確認您已登入：

   ```bash
   aio where
   ```

1. 確認您可以看到您的IMS權杖：

   ```bash
   aio auth login --bare
   ```

1. 如果驗證錯誤持續存在，請嘗試登出並重新登入：

   ```bash
   aio auth logout
   aio auth login
   ```

### MCP伺服器未載入

如果MCP伺服器未連線，或您的代理程式指出無法連線到RAG，請使用下列步驟進行疑難排解並解決問題。

1. 使用&#x200B;**Cmd 、** (macOS)或&#x200B;**Ctrl 、** （Windows和Linux）開啟游標設定。

1. 搜尋「MCP」並確認已列出並啟用`commerce-extensibility-tools`。

1. 檢查MCP設定面板中的錯誤訊息。

1. 確認您的專案中有`mcp.json`檔案：

   ```bash
   cat .cursor/mcp.json
   ```

1. 驗證路徑正確且絕對：

   ```bash
   ls -la /<your-project-directory>/commerce-extensibility-tools/index.js
   ```

### 找不到工具

1. 結束游標並重新開啟。

1. 使用&#x200B;**Cmd+Shift+P** (macOS)或&#x200B;**Ctrl+Shift+P** (Windows/Linux)並搜尋「開發人員：開啟記錄檔資料夾」，在Cursor的開發者主控台中檢查MCP伺服器記錄。

1. 確認安裝：

   ```bash
   cd commerce-extensibility-tools
   npm install
   node index.js
   ```

   伺服器應該會在沒有錯誤的情況下啟動。

### 路徑問題(Windows)

在Windows上，使用正斜線`/`或逸出的反斜線`\\`：

```json
{
  "args": ["C:/Users/yourname/projects/commerce-extensibility-tools/index.js"]
}
```

```json
{
  "args": ["C:\\Users\\yourname\\projects\\commerce-extensibility-tools\\index.js"]
}
```

## 其他資源

* [Adobe Commerce開發人員檔案](https://developer.adobe.com/commerce/docs/){target="_blank"}
* [App Builder檔案](https://developer.adobe.com/app-builder/docs/){target="_blank"}
* [模型內容通訊協定](https://modelcontextprotocol.io/){target="_blank"}
* [資料指標IDE](https://cursor.sh/docs){target="_blank"}
