---
title: 設定您的店面
description: 瞭解如何設定您的 [!DNL Adobe Commerce Optimizer] 店面。
role: Developer
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案(Adobe管理的SaaS基礎結構)。"
source-git-commit: 3131cc27a25d1bf958071b973f1d4bf1a68be152
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 0%

---

# 設定您的店面

本教學課程示範如何設定及使用[Adobe Commerce Storefront (由Edge Delivery Services提供技術支援)](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/)，以建立效能、可擴充且安全的Commerce Storefront （由您[!DNL Adobe Commerce Optimizer]執行個體的資料提供技術支援）。


## 先決條件

- 確保您有可建立存放庫並設定為本機開發的GitHub帳戶(github.com)。

- 檢閱Adobe Edge Delivery Services店面檔案中的[概觀](https://experienceleague.adobe.com/developer/commerce/storefront/get-started)，瞭解在Adobe Commerce Edge Delivery Services上開發Commerce店面的概念和工作流程。
- 設定您的開發環境


### 設定您的開發環境

安裝Node.js以及在Edge Delivery Services上開發和測試您的[!DNL Adobe Commerce Optimizer]店面所需的Sidekick瀏覽器擴充功能。

#### 安裝節點.js

安裝Node Version Manager (NVM)和必要的Node.js版本(22.13.1 LTS)。

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

1. 驗證安裝。

   ```bash
   npm -v
   ```

>[!TIP]
>
>適用於Adobe Commerce ](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder)的[App Builder和適用於Adobe Developer App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/api-mesh/getting-started-api-mesh)的[API Mesh可提供擴充和自訂[!DNL Adobe Commerce Optimizer]解決方案的其他資源。 如需存取和使用資訊，請聯絡您的Adobe客戶代表。

#### 安裝Sidekick

安裝Sidekick瀏覽器擴充功能，以編輯、預覽和發佈內容至店面。 請參閱[Sidekick安裝指示](https://www.aem.live/docs/sidekick#installation)。

## 建立您的店面

您為[!DNL Adobe Commerce Optimizer]專案建立的店面使用Edge Delivery Services店面樣板上的自訂版Adobe Commerce。 樣板是一組檔案和資料夾，提供店面開發的起點。 此設定程式不同於Edge Delivery Services店面](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/)上[Adobe Commerce的標準設定程式。

>[!NOTE]
>
>本教學課程使用macOS、Chrome和Visual Studio Code作為開發環境。 畫面會擷取該設定，並提供相關指示。 您可以使用不同的作業系統、瀏覽器和程式碼編輯器，但您看到的UI和您採取的步驟會因此而有所不同。

### 工作流程概觀

請依照下列步驟設定與[!DNL Adobe Commerce Optimizer]搭配使用的店面。

1. **[建立程式碼存放庫](#step-1-create-site-code-repository)** — 從Adobe Commerce + Edge Delivery Services範本建立GitHub存放庫。 包含來源存放庫中的所有分支。
1. **[更新店面樣板](#step-2-update-the-storefront-boilerplate)** — 更新`aco`分支上的自訂樣板範本，以將您的內容資料夾連線到店面。
1. **[部署變更](#step-3-deploy-changes)** — 以`aco`分支的更新程式碼覆寫`main`分支上的程式碼。
1. **[新增CodeSync應用程式](#step-5-add-the-aem-code-sync-app)** — 將您的存放庫連線至Edge Delivery服務。 在完成原始程式碼自訂並將程式碼推送到`main`分支之前，請勿連執行緒式碼同步應用程式。
1. **[新增內容](#step-6-add-content)** — 使用示範內容複製工具，在託管於`https://da.live`的檔案製作環境中建立及初始化店面內容。
1. **[預覽示範網站](#step-7-preview-demo-site)** — 連線到您的店面網站以檢視[!DNL Adobe Commerce Optimizer]示範執行個體的範例內容和資料。
1. **[在本機環境中開發](#step-8-develop-in-your-local-environment)** — 安裝必要的相依性。 啟動本機開發伺服器，並更新店面設定，以連線至Adobe為您布建的[!DNL Adobe Commerce Optimizer]執行個體。
1. **[後續步驟](#next-steps)** — 進一步瞭解如何在店面管理和顯示內容和資料。


### 步驟1：建立網站程式碼存放庫

使用Edge Delivery Services + Adobe Commerce範本為您的店面建立網站範本程式碼的GitHub存放庫。

1. 登入您的GitHub帳戶。

1. 導覽至[aem-boilerplate-commerce](https://github.com/hlxsites/aem-boilerplate-commerce) GitHub存放庫。

1. 選取「**使用此範本**」，然後從下拉式功能表中選取「**建立新的存放庫**」。

   ![[!DNL Create github repo from storefront boilerplate template]](./assets/storefront-create-github-repo.png){width="700" zoomable="yes"}

   儲存區域組態頁面隨即顯示。

   ![[!DNL Configure github repo to pull all branches from boilerplate repo]](./assets/storefront-configure-github-repo.png){width="700" zoomable="yes"}

1. 使用下列詳細資料完成設定表單：

   - **存放庫範本**—`hlxsites/aem-boilerplate-commerce` （預設）。
   - **包含所有分支** — 選取包含所有分支的選項。
   - **所有者** — 您的組織或帳戶（必要）。
   - **存放庫名稱** — 您的新存放庫的唯一名稱（必填）。
   - **描述** — 存放庫的簡短描述（選擇性）。
   - **Public或Private**—Adobe建議使用public （預設）。

1. 選取&#x200B;**建立存放庫**。

   幾分鐘後，您的新存放庫會開啟。

   忽略GitHub使用者介面中顯示的任何提取請求通知。

### 步驟2：更新店面樣板

您需要下列資訊來更新店面樣板程式碼：

- 步驟2 **中的** GitHub存放庫URL— `github.com/{ORG}/{SITE}`
   - `{ORG}`是存放庫的組織名稱或使用者名稱
   - `{SITE}`是您的存放庫名稱
- 步驟1 **中的**&#x200B;內容資料夾URL— `https://drive.google.com/drive/folders/{YOUR_FOLDER_ID}`
   - `{YOUR_FOLDER_ID}`是您使用範例內容資料建立的資料夾識別碼。

#### 將存放庫連結至檔案作者環境

1. 將存放庫複製到本機電腦。

   ```bash
   git clone https://github.com/{ORG}/{SITE}.git
   ```

   如果您在複製存放庫時遇到錯誤，請參閱GitHub檔案中的[疑難排解複製錯誤](https://docs.github.com/en/repositories/creating-and-managing-repositories/troubleshooting-cloning-errors)。

1. 在終端機或IDE中開啟存放庫。

1. 檢視`aco`分支

   ```bash
   git checkout aco
   ```

1. 將`default-fstab.yaml`檔案複製到`fstab.yaml`以建立您的設定檔。

   ```bash
   cp default-fstab.yaml fstab.yaml
   ```

1. 更新店面設定檔案中的掛接點，以指向您的內容URL。

   1. 開啟[fstab.yaml](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/#vocabulary)設定檔。

      ```yaml
      mountpoints:
        /:
          url: https://content.da.live/{org}/{site}/
          type: markup
      
      folders:
       /products/: /products/default
      ```

   1. 將`{ORG}`和`{SITE}`字串取代為您為樣板程式碼建立的GitHub存放庫值。

      例如，更新的程式碼應如下所示。

      ```yaml
      mountpoints:
        /:
          url: https://content.da.live/owner-name/aco-storefront/
          type: markup
      ```

   1. 儲存檔案。

#### 設定Sidekick擴充功能

1. 新增Sidekick擴充功能的專案設定。 此設定可確保Sidekick可用於管理店面專案的內容。

>[!NOTE]
>
>請確定您已在瀏覽器中安裝[Sidekick擴充功能](https://www.aem.live/docs/sidekick#installation)。

1. 開啟`tools/sidekick/config.json`檔案。

   +++Sidekick設定檔

   ```json
   {
     "project": "Boilerplate",
     "plugins": [
       {
         "id": "cif",
         "title": "Commerce",
         "environments": [
           "edit"
         ],
         "url": "https://main--{SITE}--{ORG}.aem.live/tools/picker/dist/index.html",
         "isPalette": true,
         "paletteRect": "top: 54px; left: 5px; bottom: 5px; width: 300px; height: calc(100% - 59px); border-radius: var(--hlx-sk-button-border-radius); overflow: hidden; resize: horizontal;"
       },
       {
         "id": "personalisation",
         "title": "Personalisation",
         "environments": [
           "edit"
         ],
         "url": "https://main--{SITE}--{ORG}.aem.live/tools/segments/dist/index.html",
         "isPalette": true,
         "paletteRect": "top: 54px; left: 5px; bottom: 5px; width: 300px; height: calc(100% - 59px); border-radius: var(--hlx-sk-button-border-radius); overflow: hidden; resize: horizontal;"
       }
     ]
   }
   ```

   如需詳細資訊，請參閱[Sidekick資料庫檔案](https://www.aem.live/docs/sidekick-library)。

+++

1. 以您GitHub存放庫的值更新`url`機碼值。

   - 將`{ORG}`字串取代為您的存放庫的組織或使用者名稱。

   - 以存放庫名稱取代`{SITE}`字串

   +++更新組態檔的範例

   如果您的GitHub存放庫名稱為`aco-storefront`，而您的組織為`early-adopter`，則更新的URL應如下所示：

   ```json
   {
     "project": "Boilerplate",
     "plugins": [
       {
         "id": "cif",
         "title": "Commerce",
         "environments": [
           "edit"
         ],
         "url": "https://main--aco-storefront--early-adopter.aem.live/tools/picker/dist/index.html",
         "isPalette": true,
         "paletteRect": "top: 54px; left: 5px; bottom: 5px; width: 300px; height: calc(100% - 59px); border-radius: var(--hlx-sk-button-border-radius); overflow: hidden; resize: horizontal;"
       },
       {
         "id": "personalisation",
         "title": "Personalisation",
         "environments": [
           "edit"
         ],
         "url": "https://main--aco-storefront--early-adopter.aem.live/tools/segments/dist/index.html",
         "isPalette": true,
         "paletteRect": "top: 54px; left: 5px; bottom: 5px; width: 300px; height: calc(100% - 59px); border-radius: var(--hlx-sk-button-border-radius); overflow: hidden; resize: horizontal;"
       }
     ]
   }
   ```
