---
source-git-commit: 10a91a91337778648e99078bcbf0c9ef25a49f86
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---
# Commerce代碼片段

## 資料摘要同步狀態擴充功能的安裝注意事項 {#install-data-sync-feed-status}

>[!NOTE]
>
>如果雲端或內部部署的Commerce的Commerce Admin中沒有資料摘要同步狀態頁面，請依照[擴充功能安裝指示](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status#install-the-extension){target="_blank"}加以啟用。


## Adobe Commerce Optimizer整合環境校準 {#aco-integration-environment-alignment}

>[!IMPORTANT]
>
>一律將沙箱Optimizer執行個體連線到非生產環境，將生產執行個體連線到生產環境。 不相符的環境會導致不一致的目錄資料、搜尋結果和推薦。


## Optimizer的銷售服務 {#aco-merchandising-services}

>[!NOTE]
>
>針對使用Adobe Commerce Optimizer或Adobe Commerce Optimizer Connector的Commerce解決方案，請使用[銷售服務GraphQL API](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api/)，而不要使用目錄服務GraphQL API。

## Optimizer的資料同步檢查 {#aco-data-sync-verification}

>[!NOTE]
>
>對於使用[[!DNL Adobe Commerce Optimizer Connector]](../aco-connector/overview.md)將目錄資料匯出至[!DNL Adobe Commerce Optimizer]的部署，請使用Commerce管理員中的[資料摘要同步處理狀態頁面](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status)以及[!DNL Adobe Commerce Optimizer Studio]中的[資料同步處理頁面](../optimizer/setup/data-sync.md) （而非[資料管理儀表板](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)）來驗證目錄資料同步處理。

## 適用於API更新的Adobe Commerce Optimizer下拉式注意事項 {#aco-api-updates-and-dropins}

>[!NOTE]
>
>[!DNL Commerce Storefront on Edge Delivery Services]的[外掛元件](https://experienceleague.adobe.com/developer/commerce/storefront/dropins/all/introduction/?lang=zh-Hant)會自動擷取最新的GraphQL變更（新欄位、限制和查詢行為）。

## ACCS搶先使用 {#accs-early-access}

>[!NOTE]
>
>本檔案說明提早存取開發中的產品，並未反映所有可供一般使用的功能。

<!--
## Nav hack ACCS {#nav-hack-accs}

>[!BEGINSHADEBOX]

<table style="table-layout:fixed">
  <tr>
    <td style="vertical-align: middle;"><a href="https://developer.adobe.com/commerce/webapi/"><img alt="Developers" src="../assets/icons/developers.svg" /> <strong>Developers</strong></a></td>
    <td style="vertical-align: middle;"><a href="https://experienceleague.adobe.com/developer/commerce/storefront/?lang=zh-Hant"><img alt="Storefront" src="../assets/icons/storefront.svg" /> <strong>Storefront</strong></a></td>
    <td style="vertical-align: middle;"><a href="../cloud-service/overview.md"><img alt="Merchants" src="../assets/icons/merchants.svg" /> <strong>Merchants</strong></a></td>
    <td style="vertical-align: middle;"><a href="https://experienceleague.adobe.com/zh-hant/docs/commerce-learn/tutorials/getting-started/commerce-as-a-cloud-service/overview"><img alt="Videos" src="../assets/icons/videos.svg" /> <strong>Videos</strong></a></td>
    <td style="vertical-align: middle;"><a href="https://experienceleague.adobe.com/developer/commerce/storefront/playgrounds/commerce-services/?lang=zh-Hant"><img alt="Playgrounds" src="../assets/icons/playgrounds.svg" /> <strong>Playgrounds</strong></a></td>
  </tr>
</table>

>[!ENDSHADEBOX]
-->

## ACCS僅沙箱實驗功能 {#accs-sandbox-experimental}

>[!IMPORTANT]
>
>此功能為實驗性質，僅適用於[!DNL Adobe Commerce as a Cloud Service]的沙箱環境。
>
>此功能可能會有所變更，恕不另行通知。

[!BADGE 沙箱]{type=Caution tooltip="列出的專案目前僅在沙箱環境中可用。 Adobe會先在沙箱環境中推出新版本，讓您可以在生產環境中使用該版本之前有時間測試即將推出的變更。"}

## AEM Assets執行個體對應 {#aem-assets-instance-mapping}

>[!NOTE]
>
>將[!DNL Adobe Commerce as a Cloud Service]連線至[!DNL AEM Assets]時，您的[!DNL AEM Assets] Stage執行個體會對應至您的沙箱[!DNL Adobe Commerce as a Cloud Service]執行個體和任何其他非生產環境。 您的[!DNL AEM Assets]生產執行個體對應到您的[!DNL Adobe Commerce as a Cloud Service]生產執行個體。

## IMS身分和單一登入資訊 {#ims-identity-and-sso-config}

Adobe Commerce身分管理和驗證由Adobe Identity Management系統(IMS)透過Adobe Admin Console管理。

如需有關身分設定選項（包括Adobe ID、Enterprise ID和Federated ID）的資訊，以及設定單一登入(SSO)以安全存取Adobe應用程式的指示，請參閱&#x200B;*企業Admin Console*&#x200B;檔案中的[設定身分和單一登入](https://helpx.adobe.com/tw/enterprise/using/set-up-identity.html)。

## ACCS服務與擴充功能發行說明 {#accs-release}

### 其他發行說明

[!DNL Adobe Commerce as a Cloud Service]包含最新版本的銷售服務、付款服務及擴充版本。 使用下列連結檢視各版本的發行說明：

| 服務 | 擴充性 | 店面 |
| --- | --- | --- |
| <ul><li>[目錄服務](../catalog-service/release-notes.md)</li><li>[即時搜尋](../live-search/release-notes.md)</li><li>[付款服務](../payment-services/release-notes.md)</li><li>[產品建議](../product-recommendations/release-notes.md)</li><li>[SaaS資料匯出](../data-export/release-notes.md)</li></ul> | <ul><li>[管理UI SDK](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/release-notes/)</li><li>[API網格](https://developer.adobe.com/graphql-mesh-gateway/mesh/release)</li><li>[個活動](https://developer.adobe.com/commerce/extensibility/events/release-notes/)</li><li>[Webhooks](https://developer.adobe.com/commerce/extensibility/webhooks/release-notes/)</li></ul> | <ul><li>[發行資訊](https://experienceleague.adobe.com/developer/commerce/storefront/releases/?lang=zh-Hant)</li><li>[變更記錄檔](https://experienceleague.adobe.com/developer/commerce/storefront/releases/changelog/?lang=zh-Hant)</li></ul> |

## Adobe Commerce Optimizer服務發行說明 {#aco-release}

### 其他發行說明

[!DNL Adobe Commerce Optimizer]使用最新版的AEM Assets整合、Commerce Optimizer聯結器及[!DNL Adobe Commerce Storefront]。 使用下列連結檢視每個區域的發行說明：

| 服務 | 店面 |
| --- | --- |
| [AEM Assets整合](../aem-assets-integration/release-notes.md)<br>[Commerce Optimizer聯結器](../aco-connector/release-notes.md) | [店面版本資訊](https://experienceleague.adobe.com/developer/commerce/storefront/releases/?lang=zh-Hant)<br>[店面變更記錄檔](https://experienceleague.adobe.com/developer/commerce/storefront/releases/changelog/?lang=zh-Hant) |
