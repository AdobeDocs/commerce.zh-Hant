---
source-git-commit: b6b737220a6dadf55b03da54e8d74226ed578cd0
workflow-type: tm+mt
source-wordcount: '1639'
ht-degree: 0%
---
# 受限制的存取金鑰

受限制的存取金鑰可讓授權的使用者端應用程式存取[私人目錄檢視](private-catalog-view.md) — 只有從指派的金鑰中攜帶有效已簽署權杖的請求才能擷取目錄資料。 所有其他請求都遭到拒絕，包括來自無法明確存取此目錄檢視的購物者的請求，以及探索Adobe Commerce Merchandising Services API的指令碼。

受限存取金鑰的布建方式為下列兩種方式之一：

- **自動，針對B2B共用目錄** — 系統布建並指派與B2B共用目錄關聯的目錄檢視的初始金鑰。 接著，您可以從Commerce管理員管理金鑰和金鑰指派。 請參閱&#x200B;*Commerce管理指南*&#x200B;中的[目錄檢視驗證](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/b2b/shared-catalogs/catalog-views-manage)。 自動布建可在下列部署中使用：

  - 適用於Adobe Commerce B2B的&#x200B;**具有CCDM**&#x200B;的Adobe Commerce as a Cloud Service。
  - **雲端或內部部署上的Adobe Commerce**，已透過[!DNL Adobe Commerce Optimizer Connector for B2B]與Adobe Commerce Optimizer整合。 需要聯結器的B2B擴充功能。

- **手動，針對任何目錄檢視** — 若要自行保護目錄檢視 — 例如，針對合作夥伴入口網站或發行前預覽 — 請遵循本主題中的步驟，從[建立受限制的存取金鑰](#create-a-restricted-access-key)開始。

## 限制存取的關鍵使用案例

**[!UICONTROL Price Book ID]**&#x200B;會決定請求會看到哪些價格 — 其範圍是定價，而非誰可以提出請求。 任何知道目錄檢視ID和價格簿ID的使用者端都可透過Merchandising ServicesAPI擷取該資料。 限制存取金鑰可新增個別的補充控制：限制存取金鑰可限定存取目錄檢視的使用者範圍，且不受價格簿所套用。

受限制的存取金鑰通常用於：

- **合約式B2B定價** — 限制連結至議價價格簿的目錄檢視，以便只有適用它的買方可以查詢它。 其他購買機構和公眾則不能。 若為B2B共用目錄，此專案會自動設定。 請參閱[金鑰管理和輪換](#key-management-and-rotation)。
- **合作夥伴與經銷商入口網站** — 將目錄的子集限製為直接與銷售服務API整合的已核准合作夥伴。
- **發行前預覽** — 讓受信任的內部或合作夥伴系統先預覽即將推出的產品，然後再公開顯示。

## 受限制的存取金鑰如何運作

受限制的存取金鑰是RSA金鑰組的公開元件。 您的使用者端應用程式會產生並使用此金鑰來證明其已獲得讀取私人目錄檢視的授權。 在此內容中，_使用者端應用程式_&#x200B;是指可驗證購物者的後端系統，例如，[!DNL Adobe Commerce]上的自訂邏輯或協力廠商後端，而不是店面前端本身。

下列步驟說明金鑰組與簽署的權杖如何從建立移動到驗證不屬於B2B共用目錄一部分的目錄檢視。

1. 您的使用者端應用程式會產生RSA金鑰組並保留私密金鑰。
1. 您在系統中將&#x200B;**公用**&#x200B;金鑰註冊為受限制的存取金鑰。
1. 您的使用者端應用程式會使用私密金鑰簽署JSON Web權杖(JWT)，並將其隨每個對私密目錄檢視的請求納入。

   系統會根據已登入的公開金鑰來驗證權杖的簽章，並傳回要求的目錄資料（如果有效）。

## 存取受限制的存取金鑰工作區

如何開啟受限制的存取金鑰工作區取決於您使用的產品：

- **Adobe Commerce管理員** (Adobe Commerce as a Cloud Service) — 選取&#x200B;*系統* > *資料傳輸* > **受限存取金鑰**。
- **Adobe Commerce Optimizer Studio** — 選取&#x200B;*存放區設定* > **受限制的存取金鑰**。

## 建立受限制的存取金鑰

>[!NOTE]
>
>本節及接下來的兩個章節說明管理受限制存取金鑰的手動程式。 對於具有自動金鑰布建的B2B共用目錄，請從Commerce管理員管理金鑰。 請參閱[受限制的存取金鑰](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/systems/data-transfer/data-sync/catalog-view-sync/restricted-access-keys)。

### 新增受限制的存取金鑰

選取您用來管理金鑰之工具的索引標籤： Commerce Admin或Adobe Commerce Optimizer Studio。

>[!BEGINTABS]

>[!TAB Adobe Commerce管理員]

客戶透過CCDM使用Adobe Commerce as a Cloud Service，或透過聯結器連線至Adobe Commerce的Adobe Commerce Optimizer，可以從Commerce管理員產生RSA金鑰組。 請參閱[管理受限制的存取金鑰](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/systems/data-transfer/data-sync/catalog-view-sync/restricted-access-keys)。

>[!TAB Adobe Commerce Optimizer Studio — 手動金鑰管理]

使用Adobe Commerce Optimizer Studio的客戶必須產生和管理自己的RSA金鑰組，然後將公開金鑰新增到系統中。 這是具有第三方後端的Adobe Commerce Optimizer的必要工作流程。 使用聯結器的客戶也可以使用此工作流程，而不使用Commerce管理員。

**產生RSA金鑰組**

若要初次測試私人目錄檢視，請使用[!DNL OpenSSL]之類的工具產生金鑰組。 保守私密金鑰的秘密。 只有公開金鑰才會作為限制存取金鑰上傳至系統。

```bash
openssl genrsa -out private-key.pem 2048
openssl rsa -in private-key.pem -pubout -out public-key.pem
```

金鑰大小必須介於2048到8192位元之間。 `public-key.pem`包含您貼到下列&#x200B;**[!UICONTROL Public key]**&#x200B;欄位中的值。

**將公開金鑰新增至系統**

1. 在[限制存取]金鑰工作區中，按一下&#x200B;**[!UICONTROL Add Restricted Access Key]**。

   ![限制存取金鑰清單，包含[新增限制存取金鑰]按鈕](/help/assets/ccdm-shared/setup/restricted-access-keys.png){width="70%" zoomable="yes"}

1. 輸入金鑰詳細資料：

   ![新增限制存取金鑰表單，包含[標題]、[到期日]和[公開金鑰]欄位](/help/assets/ccdm-shared/setup/restricted-access-keys-add.png){width="70%" zoomable="yes"}

   - **[!UICONTROL Title]** — 識別索引鍵的標籤，顯示在索引鍵清單和目錄檢視索引鍵選擇器中，例如`ACME Corp wholesale portal — Tier 1 pricing`。
   - **[!UICONTROL Expiration date]** — 停止接受金鑰的日期和時間(UTC)，即使對於尚未過期的權杖亦然。
   - **[!UICONTROL Public key]** — 主體公開金鑰資訊(SPKI)格式的PEM編碼RSA公開金鑰，包括`-----BEGIN PUBLIC KEY-----`和`-----END PUBLIC KEY-----`標籤。 在整個環境中必須是唯一的。

1. 按一下&#x200B;**[!UICONTROL Save]**。

>[!ENDTABS]

建立後，金鑰便不可變動。 若要變更任何值，請刪除索引鍵並建立新值。 請參閱[旋轉金鑰](#rotate-a-key)以在沒有存取中斷的情況下完成此操作。

## 將索引鍵指派給目錄檢視

受限存取金鑰只有在指派給啟用&#x200B;**[!UICONTROL Catalog Protection]**&#x200B;的目錄檢視後，才會驗證存取權。 如需設定步驟，請參閱[保護目錄檢視](private-catalog-view.md#protect-a-catalog-view)。

## 刪除金鑰

1. 在&#x200B;**[!UICONTROL Restricted access keys]**&#x200B;工作區中，尋找您要移除的金鑰並將其刪除。

   如果將索引鍵指派給一或多個目錄檢視，則會出現警告，說明依賴該索引鍵的使用者端應用程式會失去存取權。 目錄檢視本身仍受到保護 — 它們不會公開存取。

1. 確認刪除。

## 金鑰管理和輪換

受限存取金鑰的管理方式為下列兩種之一，視您使用目錄保護的方式而定：

- **自動，針對B2B共用目錄** — 對於使用具有CCDM的銷售服務的Adobe Commerce B2B部署，以及透過[!DNL Adobe Commerce Optimizer Connector for B2B]整合的Adobe Commerce Optimizer部署（需要B2B擴充功能），在建立目錄檢視時，服務會自動產生並指派第一個受限制的存取金鑰。 每個目錄檢視都有各自的索引鍵。 之後，您可以從「共用目錄」或「公司帳戶」頁面管理每個金鑰。 您也可以從Commerce Admin **受限存取金鑰**&#x200B;頁面（**系統** > **資料傳輸**）檢視及管理金鑰。 請參閱[管理目錄檢視組態](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/b2b/shared-catalogs/catalog-views-manage)。

  共用目錄和存放區檢視的每個組合都會投影為個別的目錄檢視。 投影是目錄檢視、政策、價格簿參考和限制存取金鑰組態資料，會匯出至該組合的「銷售服務」資料層。 因此，指派給多個存放區檢視的共用目錄會產生多個目錄檢視，每個檢視都有自己的索引鍵。 編輯或旋轉某個目錄檢視的金鑰，而不會影響其他目錄檢視。

  金鑰預設為較長的到期期間。 如果您需要輪換金鑰，請在「管理員」中新增替代金鑰，並讓兩者保持作用中狀態，直到您將舊金鑰移除為止。

- **針對任何目錄檢視**&#x200B;手動 — 您如何產生和管理金鑰取決於您的產品內容。 無論是哪種情況，都會由負責驗證購物者的後端使用者端在代號上簽名。

  - **Commerce Admin （具有CCDM的Adobe Commerce as a Cloud Service或具有聯結器的Adobe Commerce Optimizer）** — 在Commerce Admin中產生RSA金鑰組，並在&#x200B;**受限存取金鑰**&#x200B;頁面上建立、指派和刪除金鑰。 Adobe Commerce不會自動旋轉按鍵。 若要旋轉按鍵，請參閱[旋轉按鍵](#rotate-a-key)。
  - **Adobe Commerce Optimizer Studio**—Studio未產生金鑰。 這是具有第三方後端的Adobe Commerce Optimizer的必要工作流程，聯結器客戶也可以使用。 使用您的使用者端應用程式來產生RSA金鑰組、保留私密金鑰，並將公開金鑰新增為受限制的存取金鑰。 使用本主題中之前的步驟來建立、新增和刪除金鑰。 若要旋轉按鍵，請參閱[旋轉按鍵](#rotate-a-key)。

### 旋轉索引鍵

若要在不中斷存取的情況下旋轉金鑰，請注意，目錄檢視最多可同時指派三個金鑰：

選取您用來管理金鑰之工具的索引標籤： Commerce Admin或Adobe Commerce Optimizer Studio。

>[!BEGINTABS]

>[!TAB Adobe Commerce管理員]

請參閱[鍵選取與輪換](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/systems/data-transfer/data-sync/catalog-view-sync/restricted-access-keys#key-selection-and-rotation)。 這適用於具有CDM的Adobe Commerce as a Cloud Service，以及透過Adobe Commerce Optimizer聯結器與Adobe Commerce Optimizer整合的Adobe Commerce專案。

>[!TAB Adobe Commerce Optimizer Studio （手動金鑰管理）]

具有第三方後端的Adobe Commerce Optimizer需要此程式。 使用聯結器的客戶也可以改用它，而不使用Commerce管理員。

1. 產生新的金鑰組，並將新的公開金鑰新增為新的受限制存取金鑰。
1. 將新索引鍵與現有索引鍵一起指派給目錄檢視。
1. 開始使用新的私密金鑰簽署新權杖以完成金鑰變換。
1. 在新金鑰上確認所有使用者端應用程式後，請移除並刪除舊金鑰。

>[!ENDTABS]

## 限制

檢視[目錄檢視和原則限制](https://experienceleague.adobe.com/zh-hant/docs/commerce/optimizer/boundaries-limits)。

## 更多相關資訊

- [私人目錄檢視](private-catalog-view.md) — 瞭解如何使用受限制的存取金鑰保護目錄檢視。
