---
title: 將Commerce資料連線至Adobe Experience Platform
description: 瞭解如何將Commerce資料連結至Adobe Experience Platform。
feature: Personalization, Integration, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '2910'
ht-degree: 0%

---

# 將Commerce資料連線至Adobe Experience Platform

安裝[!DNL Data Connection]擴充功能時，在Commerce _Admin_&#x200B;的&#x200B;**服務**&#x200B;下的&#x200B;**系統**&#x200B;功能表中會出現兩個新的設定頁面。

- Commerce服務聯結器
- [!DNL Data Connection]

若要將您的Adobe Commerce執行個體連線到Adobe Experience Platform，您必須設定這兩個聯結器，從Commerce服務聯結器開始，然後以[!DNL Data Connection]擴充功能完成。

## 設定Commerce服務聯結器

如果您先前已安裝Adobe Commerce服務，表示您可能已設定Commerce服務聯結器。 如果沒有，則您必須在[Commerce服務聯結器](../landing/saas.md)頁面上完成下列工作：

1. 登入您的Commerce帳戶以[擷取您的生產和沙箱API金鑰](../landing/saas.md#credentials)。
1. 選取[SaaS資料空間](../landing/saas.md#saas-configuration)。
1. 登入您的Adobe帳戶以[擷取您的組織ID](../landing/saas.md#ims-organization-optional)。

設定Commerce Services聯結器後，再設定[!DNL Data Connection]擴充功能。

## 設定[!DNL Data Connection]擴充功能

在本節中，您將瞭解如何設定[!DNL Data Connection]擴充功能。

### 新增服務帳戶和認證詳細資料

如果您計畫收集並傳送[歷史訂單資料](#send-historical-order-data)或[客戶設定檔資料](#send-customer-profile-data)，您必須新增服務帳戶與認證詳細資料。 此外，若您正在設定[Audience Activation](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html?lang=zh-Hant)擴充功能，則必須完成這些步驟。

如果您只收集和傳送店面或後台資料，您可以跳至[一般](#general)區段。

#### 步驟1：在Adobe Developer Console中建立專案

在Adobe Developer Console中建立可驗證Commerce的專案，以便進行Experience Platform API呼叫。

若要建立專案，請依照[驗證及存取Experience Platform API](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=zh-Hant)教學課程中概述的步驟進行。

進行教學課程的過程中，請確定您的專案具備下列專案：

- 存取下列[產品設定檔](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=zh-Hant#select-product-profiles)： **預設的生產所有存取權**&#x200B;和&#x200B;**AEP預設的所有存取權**。
- 已設定正確的[角色和許可權](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=zh-Hant#assign-api-to-a-role)。
- 如果您決定使用JSON Web權杖(JWT)作為伺服器對伺服器的驗證方法，您也必須上傳私密金鑰。

此步驟的結果會建立您在下一步中使用的組態檔。

#### 步驟2：下載設定檔

下載[工作區組態檔](https://developer.adobe.com/commerce/extensibility/events/project-setup/#download-the-workspace-configuration-file)。 將此檔案的內容複製並貼到Commerce管理員的&#x200B;**服務帳戶/認證詳細資料**&#x200B;頁面。

1. 在Commerce管理員中，瀏覽至&#x200B;**商店** >設定> **設定** > **服務** > **[!DNL Data Connection]**。

1. 選取您從&#x200B;**Adobe Developer Authorization Type**&#x200B;功能表實作的伺服器對伺服器授權方法。 Adobe建議使用OAuth。 已棄用JWT。 [深入瞭解](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)。

1. （僅限JWT）將`private.key`檔案的內容複製並貼到&#x200B;**使用者端密碼**&#x200B;欄位。 使用下列指令來複製內容。

   ```bash
   cat config/private.key | pbcopy
   ```

   請參閱[服務帳戶(JWT)驗證](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/)，以取得有關`private.key`檔案的詳細資訊。

1. 將`<workspace-name>.json`檔案的內容複製到&#x200B;**服務帳戶/認證詳細資料**&#x200B;欄位。

   ![[!DNL Data Connection]管理員組態](./assets/epc-admin-config.png){width="700" zoomable="yes"}

1. 按一下&#x200B;**儲存設定**。

1. 按一下&#x200B;**[!UICONTROL Test connection]**&#x200B;按鈕，確定您輸入的服務帳戶與認證資訊正確無誤。

### 一般

1. 在Admin中，移至&#x200B;**系統** >服務> **[!DNL Data Connection]**。

   ![[!DNL Data Connection]設定](./assets/epc-settings.png){width="700" zoomable="yes"}

1. 在「**一般**」下的「**設定**」標籤上，確認與您的Adobe Experience Platform帳戶相關聯的ID (如[Commerce Services Connector](../landing/saas.md#organizationid)中所設定)。 組織ID為全域。 每個Adobe Commerce例項只能關聯一個組織ID。

1. 在&#x200B;**領域**&#x200B;下拉式清單中，將內容設定為&#x200B;**網站**。

1. （選用）如果您已將[AEP Web SDK (alloy)](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=zh-Hant)部署至您的網站，請啟用核取方塊並新增AEP Web SDK的名稱。 否則，請將這些欄位留空，[!DNL Data Connection]擴充功能會為您部署一個擴充功能。

   >[!NOTE]
   >
   >如果您指定自己的AEP Web SDK，[!DNL Data Connection]擴充功能會使用與該SDK相關聯的資料流ID，而非此頁面上指定的資料流ID （如果有的話）。

### 資料收集

您可以在此段落中指定您要收集並傳送至Experience Platform Edge的資料型別。 有三種型別的資料：

- **行為** （使用者端資料）是在店面擷取的資料。 這包括購物者互動，例如`View Page`、`View Product`、`Add to Cart`和[請購單清單](events.md#b2b-events)資訊（適用於B2B商家）。

- **後台** （伺服器端資料）是在Commerce伺服器中擷取的資料。 這包括訂單狀態的相關資訊，例如，訂單是否已下達、取消、退款、出貨或完成。 其中也包含[歷史訂單資料](#send-historical-order-data)。

- **設定檔**&#x200B;是與購物者設定檔資訊相關的資料。 瞭解[更多](#send-customer-profile-data)。

若要確保您的Adobe Commerce執行個體可以開始資料收集，請檢閱[必要條件](overview.md#prerequisites)。

請參閱活動主題以進一步瞭解[店面](events.md#storefront-events)、[後台](events-backoffice.md)和[設定檔](events-backoffice.md#customer-profile-events-server-side)活動。

>[!NOTE]
>
>**資料彙集**&#x200B;區段中的所有欄位都套用至&#x200B;**網站**&#x200B;範圍或更新版本。

1. 若要傳送店面行為資料，請選取&#x200B;**店面活動**。

1. 如果您要傳送訂單狀態資訊，例如訂單已下達、已取消、已退款或已出貨，請選取&#x200B;**後台事件**。

   >[!NOTE]
   >
   >如果您選取&#x200B;**後台事件**，所有後台資料都會傳送到Experience Platform Edge。 如果購物者選擇退出資料收集，您必須在Experience Platform中明確設定購物者的隱私權偏好設定。 這與店面事件不同，店面事件收集器已根據購物者偏好設定處理同意。 深入瞭解[在Experience Platform中設定購物者的隱私權偏好設定](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/consent/adobe/dataset.html?lang=zh-Hant)。

1. (如果您使用自己的AEP Web SDK，請略過此步驟。) [在Adobe Experience Platform中建立](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=zh-Hant#create)資料流，或選取您要用於收集的現有資料流。 在&#x200B;**資料流識別碼**&#x200B;欄位中輸入該資料流識別碼。

1. 輸入您要包含Commerce資料的&#x200B;**資料集識別碼**。 若要尋找資料集ID：

   1. 開啟Experience Platform UI，然後在左側導覽中選取&#x200B;**資料集**&#x200B;以開啟&#x200B;**資料集**&#x200B;儀表板。 控制面板會列出貴組織的所有可用資料集。 系統會顯示每個列出資料集的詳細資料，包括其名稱、資料集所遵守的結構描述，以及最近一次擷取執行的狀態。
   1. 開啟與資料流相關聯的資料集。
   1. 在右側窗格中，檢視資料集的詳細資訊。 複製資料集ID

1. 若要確保根據[cron](https://experienceleague.adobe.com/docs/commerce-admin/systems/tools/cron.html?lang=zh-Hant)工作的排程更新後台事件資料，您必須將`Sales Orders Feed`索引變更為`Update by Schedule`。

   1. 在&#x200B;_管理員_&#x200B;側邊欄上，移至&#x200B;**[!UICONTROL System]** > _[!UICONTROL Tools]_>**[!UICONTROL Index Management]**。

   1. 選取`Sales Orders Feed`索引器的核取方塊。

   1. 將&#x200B;**[!UICONTROL Actions]**&#x200B;設為`Update by Schedule`。

   1. 如果您是第一次啟用後台資料，請執行以下命令來重新索引並觸發重新同步。 只要[cron](https://experienceleague.adobe.com/docs/commerce-admin/systems/tools/cron.html?lang=zh-Hant)工作設定正確，後續的重新同步就會自動發生。

      ```bash
      bin/magento index:reindex sales_order_data_exporter_v2
      ```

      ```bash
      bin/magento saas:resync --feed orders
      ```

#### 欄位說明

| 欄位 | 說明 |
|--- |--- |
| 範圍 | 您要套用組態設定的特定網站。 |
| 組織ID （全域） | 屬於購買Adobe DX產品的組織的ID。 此ID會將您的Adobe Commerce執行個體連結至Adobe Experience Platform。 |
| AEP Web SDK是否已部署至您的網站 | 如果您已將自己的AEP Web SDK部署到網站，請選取此核取方塊 |
| AEP Web SDK名稱（全域） | 如果您已將Experience Platform Web SDK部署至網站，請在此欄位中指定該SDK的名稱。 這可讓店面事件收集器和店面事件SDK使用您的Experience Platform Web SDK，而非[!DNL Data Connection]擴充功能部署的版本。 如果您未將Experience Platform Web SDK部署至您的網站，請將此欄位留空，而[!DNL Data Connection]擴充功能會為您部署一個擴充功能。 |
| 店面活動 | 只要組織ID和資料流ID有效，就會預設勾選。 店面活動會在購物者瀏覽您的網站時，從他們那裡收集匿名的行為資料。 |
| 後台活動 | 若勾選，事件裝載會包含匿名處理的訂單狀態資訊，例如訂單是否已下達、取消、退款或出貨。 |
| 資料串流ID （網站） | 可讓資料從Adobe Experience Platform流向其他Adobe DX產品的ID。 此ID必須與您特定Adobe Commerce執行個體中的特定網站相關聯。 如果您指定自己的Experience Platform Web SDK，請勿在此欄位中指定資料串流ID。 [!DNL Data Connection]擴充功能會使用與該SDK相關聯的資料串流ID，並忽略此欄位中指定的任何資料串流ID （如果有的話）。 |
| 資料集ID （網站） | 包含您Commerce資料的資料集ID。 除非您已取消選取&#x200B;**店面事件**&#x200B;或&#x200B;**後台事件**&#x200B;核取方塊，否則此欄位為必要欄位。 此外，如果您使用自己的Experience Platform Web SDK，因此沒有指定資料串流ID，您還是必須新增與資料串流相關聯的資料集ID。 否則，您無法儲存此表單。 |

上線後，店面資料開始流入Experience Platform Edge。 後端辦公室資料大約需要5分鐘才會顯示在邊緣。 後續更新會根據cron排程顯示在邊緣。

### 傳送客戶設定檔資料

有兩種型別的設定檔資料可傳送至Experience Platform：設定檔記錄和時間序列設定檔事件。

個人資料記錄包含購物者在Commerce執行個體中建立個人資料時所儲存的資料，例如購物者的姓名。 當您的結構描述和資料集[已正確設定](profile-data.md)時，設定檔記錄會傳送至Experience Platform並轉送至Adobe的設定檔管理和細分服務： [Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=zh-Hant)。

時間序列設定檔事件包含購物者設定檔資訊的相關資料，例如是否他們在您的網站上建立、編輯或刪除帳戶。 將設定檔事件資料傳送至Experience Platform時，該資料會位於資料集中，以供其他DX產品使用。

1. 請確定您已提供[個](#add-service-account-and-credential-details)服務帳戶和認證詳細資料。

1. 確定您有為[設定檔記錄資料擷取](profile-data.md)和[時間序列設定檔事件資料擷取](update-xdm.md#time-series-profile-event-data)指定的結構描述和資料集。

1. 如果您想要將設定檔資料傳送至Experience Platform，請在&#x200B;**客戶設定檔**&#x200B;核取方塊中加上核取記號。

1. 輸入&#x200B;**設定檔資料集識別碼**。

   個人檔案記錄資料使用的資料集必須與您目前用於行為和後台事件資料的資料集不同。

1. 如果您不想透過用於行為和後台資料的相同資料流ID串流設定檔事件，請透過相同的資料流ID **從**&#x200B;串流客戶設定檔中移除核取記號，然後輸入您要改用的資料流ID。

在Real-Time CDP中使用設定檔記錄大約需要10分鐘。 設定檔事件會立即開始串流。

>[!TIP]
>
>若未在Experience Platform中看到設定檔資料，請參閱[Commerce知識庫](https://experienceleague.adobe.com/zh-hant/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/data-connection-customer-profiles-not-exported)以取得疑難排解建議。

#### 欄位說明

| 欄位 | 說明 |
|--- |--- |
| 客戶設定檔 | 如果您想要收集並傳送客戶設定檔記錄，請選取此核取方塊。 |
| 設定檔資料集ID | 個人資料記錄所使用的資料集，必須與行為與後台事件所使用的資料集不同。 |
| 透過相同的資料流ID串流客戶設定檔 | 決定是否想要使用目前用於行為與後台事件的相同資料流。 |
| 客戶設定檔的資料流 | 指定客戶設定檔記錄特定的資料流。 |

### 傳送歷史訂單資料

Adobe Commerce最多會收集五年的[歷史訂單資料和狀態](events-backoffice.md#back-office-events)。 您可以使用[!DNL Data Connection]擴充功能將該歷史資料傳送至Experience Platform，讓您的客戶設定檔更為豐富，並根據這些過去的訂單來個人化客戶體驗。 資料會儲存在Experience Platform的資料集中。

雖然Commerce已收集歷史訂單資料，但您必須完成數個步驟，才能將該資料傳送至Experience Platform。

觀看此影片以進一步瞭解歷史訂單，然後完成下列步驟以實施歷史訂單收集。

>[!VIDEO](https://video.tv.adobe.com/v/3424672)

#### 設定Order Sync服務

訂單同步服務使用[Message Queue Framework](https://developer.adobe.com/commerce/php/development/components/message-queues/)和RabbitMQ。 完成這些步驟後，訂單狀態資料可以同步至SaaS，這只有在傳送至Experience Platform之前是必要的。

1. 請確定您已提供[個](#add-service-account-and-credential-details)服務帳戶和認證詳細資料。

1. [啟用](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/service/rabbitmq.html?lang=zh-Hant) RabbitMQ。

   >[!NOTE]
   >
   >RabbitMQ已設定為Commerce 2.4.7版及更新版本，但您必須啟用消費者。

1. 使用`CRON_CONSUMERS_RUNNER`環境變數，透過`.magento.env.yaml`中的cron工作啟用訊息佇列消費者。

   ```yaml
      stage:
        deploy:
          CRON_CONSUMERS_RUNNER:
            cron_run: true
   ```

   >[!NOTE]
   >
   >請參閱[部署變數檔案](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-deploy.html?lang=zh-Hant#cron_consumers_runner)以瞭解所有可用的設定選項。

啟用訂單同步服務後，您就可以在&#x200B;**[!UICONTROL [!DNL Data Connection]]**&#x200B;頁面中指定歷史訂單日期範圍。

#### 指定訂單歷史記錄日期範圍

指定您要傳送至Experience Platform的歷史訂單日期範圍。

1. 在Admin中，移至&#x200B;**系統** >服務> **[!DNL Data Connection]**。

1. 選取「**訂單歷史記錄**」標籤。

   ![[!DNL Data Connection]訂單歷史記錄](./assets/epc-order-history.png){width="700" zoomable="yes"}

1. 在&#x200B;**訂單歷程記錄同步**&#x200B;下，**從設定複製資料集ID**&#x200B;核取方塊已經啟用。 這可確保您使用的資料集與&#x200B;**設定**&#x200B;索引標籤中指定的資料集相同。

1. 在&#x200B;**From**&#x200B;與&#x200B;**To**&#x200B;欄位中，指定您要傳送之歷史訂單資料的日期範圍。 您無法選取超過五年的日期範圍。

1. 選取&#x200B;**[!UICONTROL Start Sync]**&#x200B;以觸發同步處理開始。 歷史訂單資料是批次處理資料，而非使用串流資料的店面和後台資料。 批次資料需約45分鐘才能送達Experience Platform。

##### 欄位說明

| 欄位 | 說明 |
|--- |--- |
| 從設定複製資料集ID | 複製您在&#x200B;**設定**&#x200B;索引標籤上輸入的資料集ID。 |
| 資料集ID （網站） | 包含您Commerce資料的資料集ID。 除非您已取消選取&#x200B;**店面事件**&#x200B;或&#x200B;**後台事件**&#x200B;核取方塊，否則此欄位為必要欄位。 此外，如果您使用自己的Experience Platform Web SDK，因此沒有指定資料串流ID，您還是必須新增與資料串流相關聯的資料集ID。 否則，您無法儲存此表單。 |
| 從 | 您要開始收集訂單歷史記錄資料的日期。 |
| 至 | 您要結束收集訂單歷史記錄資料的開始日期。 |
| 開始同步 | 開始將訂單歷史記錄資料同步至Experience Platform Edge的程式。 如果&#x200B;**[!UICONTROL Dataset ID]**&#x200B;欄位空白或資料集ID無效，此按鈕會停用。 |

### 資料自訂

在&#x200B;**資料自訂**&#x200B;索引標籤上，您可以檢視[!DNL Commerce]中設定並傳送至Experience Platform的任何自訂屬性。

![[!DNL Data Connection]資料自訂](./assets/epc-data-customization.png){width="700" zoomable="yes"}

>[!IMPORTANT]
>
>確定您在&#x200B;**資料彙集**&#x200B;索引標籤上[指定的](#data-collection)資料串流ID符合連結至結構描述以擷取自訂屬性的ID。

建立訂單的自訂屬性並將其傳送至Experience Platform時，Commerce中的屬性名稱必須與Experience Platform上[!DNL Commerce]結構描述中的屬性名稱相符。 如果兩者不符，就很難辨識差異。 如果名稱不相符，**自訂訂單屬性**&#x200B;表格可協助解決問題。

**自訂訂單屬性**&#x200B;表格可顯示[!DNL Commerce]後台與Experience Platform中的[!DNL Commerce]結構描述之間的自訂訂單屬性組態與對應。 此表格可讓您檢視不同來源的訂單層次與訂單料號層次自訂屬性，讓您更容易識別遺失或不對齊的屬性。 它也會顯示資料集ID，以協助區分即時和歷史資料集，因為每個資料集都可以有自己的自訂屬性。

如果您在表格中的自訂屬性名稱旁邊沒有看到綠色核取記號，表示來源中的屬性名稱不符。 在一個來源中更正屬性名稱，將會出現綠色核取記號，表示名稱現在相符。

- 如果屬性名稱在Experience Platform的結構描述中更新，您必須將設定儲存在&#x200B;**資料自訂**&#x200B;索引標籤上，才能觸發Experience Platform結構描述變更。 當您按一下&#x200B;**[!UICONTROL Refresh]**&#x200B;按鈕時，此變更將會反映在&#x200B;**自訂訂單屬性**&#x200B;表格中。
- 如果屬性名稱在[!DNL Commerce]中更新，則必須產生訂單事件以更新&#x200B;**自訂訂單屬性**&#x200B;資料表中的名稱。 此變更將在60分鐘左右反映出來。

深入瞭解如何[設定自訂屬性](custom-attributes.md)。

#### 欄位說明

| 欄位 | 說明 |
|--- |--- |
| 資料集 | 顯示包含自訂屬性的資料集。 即時和歷史資料集可以有自己的自訂屬性。 |
| Adobe Commerce | 顯示在[!DNL Commerce]後台中建立的任何自訂屬性。 |
| Experience Platform | 顯示在Experience Platform中[!DNL Commerce]結構描述中指定的任何自訂屬性。 |
| 重新整理 | 從Experience Platform中的[!DNL Commerce]結構描述擷取任何自訂屬性名稱。 |

## 確認已收集事件資料

若要確認正在從您的Commerce存放區收集資料，請使用[Adobe Experience Platform Debugger](https://experienceleague.adobe.com/docs/experience-platform/debugger/home.html?lang=zh-Hant)來檢查您的Commerce網站。 確認資料正在收集後，您可以執行查詢，從您建立的[資料集](overview.md#prerequisites)傳回資料，以確認店面和後台事件資料是否出現在邊緣。

1. 在Experience Platform的左側導覽中選取&#x200B;**查詢**，然後按一下[!UICONTROL Create Query]。

   ![查詢編輯器](assets/query-editor.png)

1. 當查詢編輯器開啟時，輸入從資料集中選取資料的查詢。

   ![建立查詢](assets/create-query.png)

   例如，您的查詢可能如下所示：

   ```sql
   SELECT * from `your_dataset_name` ORDER by TIMESTAMP DESC
   ```

1. 查詢執行之後，結果會顯示在&#x200B;**主控台**&#x200B;標籤旁邊的&#x200B;**結果**&#x200B;標籤中。 此檢視顯示查詢的表格輸出。

   ![查詢編輯器](assets/query-results.png)

在此範例中，您會看到來自[`commerce.productListAdds`](events.md#addtocart)、[`commerce.productViews`](events.md#productpageview)、[`web.webpagedetails.pageViews`](events.md#pageview)等的事件資料。 此檢視可讓您驗證Commerce資料是否到達邊緣。

如果結果不符合您的預期，請開啟您的資料集並尋找任何失敗的批次匯入。 深入瞭解[疑難排解批次匯入](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/troubleshooting.html?lang=zh-Hant)。

### 驗證設定檔資料是否出現在Experience Platform中

若未在Experience Platform中看到設定檔資料，請參閱[Commerce知識庫](https://experienceleague.adobe.com/zh-hant/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/data-connection-customer-profiles-not-exported)以取得疑難排解建議。

## 後續步驟

將Commerce資料傳送至Experience Platform Edge時，其他Adobe Experience Cloud產品(例如Adobe Journey Optimizer)可使用該資料。 例如，您可以設定Journey Optimizer監聽特定事件，並根據該事件資料為首次使用者或如果有捨棄的購物車時，觸發電子郵件。 瞭解如何透過在Journey Optimizer中[建立客戶歷程](using-ajo.md)來擴充您的Commerce平台。
