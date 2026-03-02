---
title: 目錄圖層
description: 瞭解目錄圖層如何讓您修改產品資料而不變更原始來源資料，以便您可以安全地自訂並隨時還原變更。
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案(Adobe管理的SaaS基礎結構)。"
source-git-commit: bf1d88ef7daec25872678bb27bce0bb7c97fd296
workflow-type: tm+mt
source-wordcount: '1514'
ht-degree: 0%

---

# 目錄圖層

目錄圖層可讓您修改產品資料，而不變更原始來源資料。 圖層會透過在基本目錄上方建立圖層來套用變更至特定產品屬性，例如名稱、說明、影像、連結和中繼資料。 您的原始產品資料會維持不變，可讓您安全地自訂產品，並隨時還原變更。

![目錄圖層](../assets/catalog-layers.png)

## 目錄圖層的運作方式

當客戶檢視您的店面時，系統會將您的基本目錄資料與使用中的目錄圖層相結合，以顯示最終產品資訊。 以下是該程式的運作方式：

1. **圖層應用程式** — 使用管道ID和環境ID提出請求時，存放區服務會擷取相關的目錄檢視。

1. **資料合併** — 系統會根據圖層優先順序將目錄圖層套用至產品資料。

1. **欄位處理** — 不同的欄位型別處理方式不同：

   * **覆寫欄位** — 名稱、說明和中繼標題等文字欄位會取代為圖層中所定義的值，並以較高優先順序的圖層優先。
   * **合併欄位** — 從多個圖層合併影像、連結和屬性等陣列欄位，以提供統一的回應。

1. **優先順序解析度** — 順序欄位決定優先的圖層。 當多個圖層修改相同的欄位時，順序編號較低的圖層優先順序較高（例如，順序1是最高的）。

## 目錄層使用案例

目錄圖層通常用於：

* **SEO最佳化** — 根據[Sites Optimizer](../manage-results/opportunities.md)的AI建議覆寫產品中繼標題和說明。
* **季節性行銷活動** — 暫時更新促銷活動的產品名稱、說明或影像，而不變更來源資料。
* **地區自訂** — 根據地理位置或語言顯示不同的產品資訊。
* **A/B測試** — 測試不同的產品簡報，以最佳化轉換率。
* **多品牌管理** — 針對不同的品牌目錄檢視自訂產品屬性。
* **產品視覺效果** — 將AEM Assets的產品影像套用為基底目錄頂端的圖層。

## AEM-Assets層

當您啟用[產品視覺效果](product-visuals.md)時，AEM Assets整合會自動建立和管理專為AEM Assets內容使用的目錄層。 預設圖層名稱為`AEM-Assets`，不過您可以在AEM Assets整合[的](../../aem-assets-integration/get-started/configure-aco.md)上線期間指定自訂名稱。

此圖層包含與AEM Assets同步的產品影像。 如同其他目錄圖層，它是透過[產品圖層API](https://developer.adobe.com/commerce/services/reference/rest/#tag/Product-Layers){target=_blank}填入。 Assets整合服務會將AEM資產中繼資料和傳送URL轉換為API格式，並在AEM Assets核准資產時自動傳送資料。

整合支援每個租使用者一個來源（一個地區設定+一個圖層）。

>[!CAUTION]
>
> 將AEM-Assets圖層指派給目錄檢視。 如果未指定圖層，產品影像資料可能會意外覆寫。

### AEM-Assets圖層的運作方式

1. **自動建立**：圖層是在為您的[!DNL Commerce Optimizer]執行個體設定AEM Assets整合時建立的。

1. **影像同步**：當資產在AEM Assets中獲得核準時，Assets Integration Service會透過產品圖層API轉換資產資料並更新`AEM-Assets`圖層。

1. **圖層指派**：將`AEM-Assets`圖層指派給要顯示AEM Assets影像的目錄檢視。

### 將AEM-Assets圖層指派給目錄檢視

若要在店面顯示AEM Assets影像：

1. 瀏覽至&#x200B;_市集設定_，然後按一下&#x200B;**[!UICONTROL Catalog views]**。

1. 選取要套用圖層的目錄檢視。

1. 在目錄圖層區段中，找出&#x200B;**AEM-Assets**&#x200B;圖層。

1. 啟動圖層以為此目錄檢視啟用它。

1. 按一下&#x200B;**[!UICONTROL Save]**&#x200B;以套用變更。

指派後，店面API (目錄服務、即時搜尋、產品推薦和店面GraphQL API)會傳回產品的基本目錄影像和AEM Assets影像。

如需設定產品視覺效果的詳細資訊，請參閱[使用AEM Assets的產品視覺效果](product-visuals.md)。

## 透過資料擷取新增目錄層

您可以在資料擷取程式期間將目錄圖層新增至產品。 此方法適用於大量作業或自動化工作流程。

>[!NOTE]
>
>您使用擷取API匯入目錄圖層，但[使用UI完成圖層順序](#manage-layer-priorities)的設定。

**必要條件：**

* 具有存取資料擷取服務許可權的API認證
* 基礎目錄中已經存在的產品SKU

**步驟：**

1. 使用您要修改的產品屬性，以所需格式準備圖層資料。

1. 使用產品層API端點來擷取層資料。

1. 檢查目錄檢視組態，確認圖層已成功內嵌。

如需詳細的API規格和裝載範例，請參閱開發人員檔案中的[產品層](https://developer.adobe.com/commerce/services/reference/rest/#tag/Product-Layers){target=_blank}。

## 在UI中手動新增目錄圖層

>[!NOTE]
>
>此功能尚無法使用。

目錄檢視UI可讓您手動建立和管理圖層，這對產生AI支援的建議的Sites Optimizer等整合特別有用。

>[!NOTE]
>
>如果目錄檢視中沒有Sites Optimizer圖層，Sites Optimizer中的自動修正功能會自動建立一個圖層，並為其指定順序1 （最高優先順序）。 如果您刪除此圖層，則會在下次執行Sites Optimizer中的自動修復功能時重新建立該圖層，並將現有圖層移至較低順序的數字。 如果Sites Optimizer圖層已存在於不同的訂單編號，則自動修正功能不會變更其優先順序。

>[!TIP]
>
>若要進行大量圖層作業，請使用上述的資料擷取API方法[](#add-a-catalog-layer-via-data-ingestion)。

**若要建立手動圖層：**

1. 瀏覽至&#x200B;**存放區設定** > **目錄檢視**。

1. 選取要套用圖層的目錄檢視。

1. 在目錄圖層區段中，按一下&#x200B;**新增目錄圖層**。

1. 設定圖層屬性：

   * **圖層名稱** — 輸入描述性名稱以識別圖層用途。
   * **產品** — 選取要套用此圖層的產品。
   * **屬性** — 選擇要修改的產品屬性（名稱、說明、影像、中繼標籤等）。
   * **值** — 為每個選取的屬性輸入新值。

1. 按一下&#x200B;**儲存**&#x200B;以建立圖層。

新圖層會加入目錄檢視中，並自動指定下一個可用的訂單編號。

## 預覽圖層效果

>[!NOTE]
>
>此功能尚無法使用。

在啟動圖層或變更優先順序之前，您可以預覽它們對產品資料的影響。

**若要預覽圖層變更：**

1. 瀏覽至&#x200B;**存放區設定** > **目錄檢視**。

1. 選取包含要預覽圖層的型錄檢視。

1. 在目錄圖層區段中，選取特定產品或使用預覽功能。

1. 檢閱組合的產品資料，以顯示圖層如何修改基本型錄值。

1. 視需要調整圖層內容或優先順序。

## 啟動、停用或刪除圖層

您可以啟用或停用目錄圖層而不刪除它們，讓您控制何時套用特定的自訂。

**若要啟用或停用圖層：**

1. 瀏覽至&#x200B;**存放區設定** > **目錄檢視**。

1. 選取包含圖層的目錄檢視。

1. 在型錄圖層區段中，找出要切換的圖層。

1. 按一下啟動切換即可啟用或停用圖層。

   * **作用中** — 圖層已套用至產品資料。
   * **非使用中** — 圖層會保留，但不會套用至產品資料。

1. 此變更會立即在您的店面生效。

**若要刪除圖層：**

使用資料擷取API [刪除目錄層](https://developer.adobe.com/commerce/services/reference/rest/#operation/deleteProductLayers){target=_blank}。

## 管理圖層優先順序

套用圖層的順序決定了當多個圖層修改相同的產品屬性時，哪些值會出現在您的店面上。 管理優先順序可確保顯示正確的資料。

**瞭解優先順序：**

* 每個圖層都會指定順序編號（1、2、3等）
* 順序1的優先順序最高，並覆寫所有其他圖層
* 當多個圖層修改相同的欄位時，順序編號較低的圖層優先
* 優先順序僅適用於覆寫欄位（名稱、說明、中繼標籤）
* 合併欄位（影像、連結、屬性）以組合來自所有圖層的資料

**若要重新排序圖層優先順序：**

1. 瀏覽至&#x200B;**存放區設定** > **目錄檢視**。

1. 選取包含要重新排序之圖層的目錄檢視。

1. 在型錄圖層區段中，找出您要移動的圖層。

1. 拖放圖層以變更其位置，或使用重新排序控制項。

1. 系統會根據新順序自動更新訂單編號。

1. 按一下[儲存]以套用新的優先順序。****

>[!IMPORTANT]
>
>對圖層優先順序的變更會立即生效，並可能影響客戶在您店面看到的內容。 儲存前請先檢閱預覽，以確保套用正確的值（**尚未提供預覽**）。

## 最佳實務

使用目錄圖層時，請遵循下列建議：

* **使用描述性名稱** — 清楚地命名圖層以指示其用途（例如「Holiday 2025 Campaign」或「SEO最佳化 — 產品頁面」）。

* **限制圖層** — 雖然系統支援多個圖層，但使用太多可能會影響效能。 儘可能合併圖層。

<!--- **Test before activating**—Always preview layer effects before activating them on your live storefront. !!!REMOVE IF PREVIEW NOT AVAILABLE FOR GA!!!-->

* **檔案優先順序邏輯** — 追蹤哪些圖層應該優先處理，以避免意外覆寫。

* **檢閱Sites Optimizer圖層** — 使用Sites Optimizer的自動修復時，系統會建立最高優先順序的圖層。 在新增可能覆寫AI建議的手動圖層時請務必小心。 深入瞭解如何使用[Sites Optimizer](../manage-results/opportunities.md)。

* **監控效能** — 如果您發現產品頁面載入速度緩慢，請檢閱您的圖層組態，並考慮合併圖層。

## 更多相關資訊

* [目錄檢視](catalog-view.md) — 設定不同店面的目錄檢視
* [產品視覺效果](product-visuals.md) — 將AEM Assets用於產品影像
* [機會](../manage-results/opportunities.md) — 瞭解使用目錄層的AI支援的最佳化
