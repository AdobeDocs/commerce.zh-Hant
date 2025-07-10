---
title: 將媒體檔案移轉至AEM
description: 將媒體檔案從Adobe Commerce或外部來源移轉至AEM Assets DAM。
feature: CMS, Media, Integration
exl-id: ccb13e90-8b18-4f1e-94ce-f0dacea2f617
source-git-commit: 995fb071953ddad6cb2076207910679905bb0347
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 0%

---

# 將媒體檔案移轉至AEM Assets DAM

Adobe Commerce和Adobe Experience Manager (AEM)皆提供內建功能，可簡化從Commerce到AEM Assets **數位資產管理系統(DAM)**&#x200B;的媒體檔案移轉。 您也可以從其他來源移轉媒體檔案。

## 先決條件

| 類別 | 需求 |
|----------|-------------|
| **系統需求** | <ul><li>已布建AEM Assets的AEM as a Cloud Service環境</li><li>足夠的儲存容量</li><li>大型檔案傳輸的網路頻寬</li></ul> |
| **必要的存取權和許可權** | <ul><li>AEM Assets as a Cloud Service的管理員存取權</li><li>存取儲存媒體檔案的來源系統(Adobe Commerce或外部系統)</li><li>存取雲端儲存服務的適當許可權</li></ul> |
| **雲端儲存空間帳戶** | <ul><li>AWS S3或Azure Blob儲存帳戶</li><li>私人容器/貯體設定</li><li>驗證認證</li></ul> |
| **Source內容** | <ul><li>可移轉的已整理媒體檔案</li><li>AEM Assets<a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/file-format-support#image-formats">支援的</a>格式影像和視訊檔案。</li><li>乾淨的重複資產</li></li> |
| **中繼資料準備** | <ul><li>為AEM Assets資產設定的<a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/aem-asset-management/getting-started/aem-assets-configure-aem">Commerce中繼資料設定檔</a></li><li>每個資產的對應中繼資料值</li><li>CSV檔案編輯器(例如Microsoft Excel)</li></ul> |

## 移轉最佳實務

1. 移轉前可透過移除未使用和重複的內容來組織資產。

1. 依大小、格式或使用案例以邏輯方式組織資產。

1. 請考慮將大型移轉分成較小的批次。

1. 排程非尖峰時間耗用大量資源的匯入。

1. 在完整匯入之前驗證中繼資料對應。

## 移轉工作流程

依照移轉工作流程從Adobe Commerce或其他外部系統匯出媒體檔案，並將其匯入AEM Assets DAM。

### 步驟1：從現有的資料來源匯出內容

僅[!BADGE 個PaaS]{type=Informative tooltip="僅適用於雲端專案上的Adobe Commerce (Adobe管理的PaaS基礎結構)。"}

對Adobe Commerce商家而言，**遠端儲存模組**&#x200B;可方便媒體檔案匯入和匯出。 此模組可讓企業使用AWS S3等遠端儲存服務來儲存和管理媒體檔案。 若要設定Commerce執行個體的遠端儲存空間，請參閱[Commerce設定指南](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/storage/remote-storage/remote-storage-aws-s3)中的&#x200B;**設定遠端儲存空間**。

如果您將媒體檔案儲存在Adobe Commerce外部，請直接將它們上傳到AEM as a Cloud Service支援的[資料來源](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/bulk-import-assets-view#prerequisites)之一。

### 步驟2：建立中繼資料對應的CSV檔案

匯出媒體檔案後，請建立CSV檔案，以使用自動化所需的中繼資料對應這些資產。 CSV應包含&#x200B;**產品**、**位置**&#x200B;和&#x200B;**角色對應**&#x200B;的欄位，以確保與[AEM Assets中繼資料設定檔](configure-aem.md#configure-a-metadata-profile)一致。

對於您計畫移轉的每個媒體檔案，請為Commerce資產[的](configure-aem.md)AEM Assets中繼資料設定檔中包含的中繼資料欄位提供值，如下表所述。

| 中繼資料 | 說明 | 值 |
|-------|-------------|--------|
| 資產路徑 | 資產將儲存於AEM Assets存放庫中的完整路徑。<br><br>使用路徑建立子資料夾以整理Commerce資產，例如`content/dam/commerce/<brand>/<type>`。 | `/content/dam/commerce/<sub-folder>/..<filename>` |
| commerce：positions | 資產在產品相簿中的位置/順序 | 多個以縱線分隔的數值（請參閱csv檔案） |
| commerce：isCommerce | 表示資產是否用於商業的旗標 | `Yes` |
| commerce：sku | 與此資產相關聯的產品SKU | 多個以縱線分隔的字串值（請參閱csv檔案） |
| commerce：roles | 資產的角色或影像型別（例如，`thumbnail`、`main image`、`swatch`） | 多個值以分號分隔（例如「thumbnail； image； swatch_image； small_image」） |

+++CSV程式碼

使用這個範例CSV程式碼，在程式碼編輯器或試算表應用程式(如Microsoft Excel)中建立檔案。

```csv
assetPath,commerce:positions{{Number: multi}},commerce:isCommerce{{String}},commerce:skus{{String: multi}},commerce:roles{{String: multi}}
/content/dam/commerce/sample1.jpg,1,Yes,sku1,thumbnail; image; swatch_image; small_image
/content/dam/commerce/sample2.jpg,1|1|1,Yes,sku1|sku2|sku3,thumbnail; image; swatch_image; small_image|image|image; small_change
```

+++

### 步驟3：將Assets大量匯入AEM Assets

建立中繼資料對應檔案後，請使用AEM Assets大量匯入工具來匯入您的資產。

以下是使用該工具的高層級概觀。

1. [登入您的AEM Assets as a Cloud Service作者環境](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/aem-users#login-aem)。

1. 從Experience Manager工具檢視中，選取&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL Bulk Import]**。

   ![AEM Assets製作](../assets/aem-assets-bulk-import-selection.png){width="600" zoomable="yes"}

1. 從大量匯入設定中，選取&#x200B;**[!UICONTROL Create]**&#x200B;以開啟設定表單。

   ![AEM Assets製作](../assets/aem-assets-bulk-import-configuration.png){width="600" zoomable="yes"}

1. 設定並儲存組態。

   您將需要：

   * 您的資料來源的驗證認證
   * AEM Assets中儲存匯入檔案的目標資料夾
   * 選填。 關於自訂匯入組態的MIME型別、檔案大小和其他引數的資訊
   * 中繼資料對應CSV檔案的路徑，您已上傳至雲端儲存空間執行個體。

   如需詳細步驟，請參閱[AEM Assets as a Cloud Service使用手冊](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/add-assets#configure-bulk-ingestor-tool)中的&#x200B;*設定大量匯入工具*。

1. 儲存組態後，請使用大量匯入工具來測試及執行匯入作業。

>[!MORELIKETHIS]
>
> [大量匯入工具影片示範](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/add-assets#asset-bulk-ingestor)
> &#x200B;> [秘訣、最佳實務和限制](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/add-assets#tips-limitations)
> &#x200B;> [使用API上傳或內嵌資產](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/admin/developer-reference-material-apis#asset-upload)
