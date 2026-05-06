---
title: 使用 [!DNL Adobe LLM Optimizer] 搭配 [!DNL Adobe Commerce]
description: 在LLM Optimizer中導覽Commerce商機、檢閱PDP和目錄擴充、將更新部署到 [!DNL Adobe Commerce]、在管理員和店面中驗證，以及瞭解如何覆寫和擷取標籤商機過時。
role: Admin, User
recommendations: noCatalog
badgePaas: label="僅限PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案（Adobe管理的PaaS基礎結構）和內部部署專案的Adobe Commerce 。"
source-git-commit: 47348a44ff7c5f890c10594f44cae6e771be046f
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 0%

---

# 搭配[!DNL Adobe Commerce]使用[!DNL Adobe LLM Optimizer]

>[!IMPORTANT]
>
>存取此整合受到限制。 如需詳細資訊，請聯絡您的技術客戶經理。

在[將Commerce連線到LLM Optimizer](connect-to-llmo.md)後，您主要在&#x200B;**[!DNL Adobe LLM Optimizer]** UI中工作，以在您準備就緒時檢閱機會並將核准的變更推送至目錄。 本文說明兩種以Commerce為中心的最佳化型別、如何使用&#x200B;**[!UICONTROL Opportunities]**、部署動作在[!DNL Adobe Commerce]中的行為方式，以及外部更新如何與LLM Optimizer建議互動。 如需整合的詳細資訊，請參閱[整合概述](../overview.md)。

## 瞭解LLM Optimizer中的Commerce最佳化 {#understand-optimizations}

對於Commerce支援的目錄，LLM Optimizer提供&#x200B;**[!UICONTROL Product Detail Page Enrichment]**&#x200B;和&#x200B;**[!UICONTROL Product Catalog Enrichment]**。

| 焦點 | 用途 |
| --- | --- |
| **[!UICONTROL Product Detail Page Enrichment]** （PDP擴充） | 可改善產品頁面閱讀AI驅動型探索的方式，而不需取代店面配置的建議。 |
| **[!UICONTROL Product Catalog Enrichment]** | 針對您可以檢閱、編輯（如有需要）以及套用至您的Commerce目錄的特定產品建議&#x200B;**產品名稱**&#x200B;和&#x200B;**產品說明**&#x200B;更新。 |

使用&#x200B;**[!UICONTROL Opportunities]**&#x200B;開啟產品或URL清單，並處理您所選型別的建議。

## 瀏覽Commerce商機 {#navigate-commerce-opportunities}

**若要開啟與Commerce相關的商機：**

1. 在左側邊欄中，按一下&#x200B;**[!UICONTROL Opportunities]**。
1. 按一下&#x200B;**[!UICONTROL Commerce Opportunity]**&#x200B;以顯示以您[!DNL Adobe Commerce]目錄為目標的最佳化型別。
1. 選取&#x200B;**[!UICONTROL Product Catalog Enrichment]**&#x200B;或&#x200B;**[!UICONTROL Product Detail Page Enrichment]**，視您要處理的專案而定。

![Commerce機會篩選和最佳化型別](../assets/llmo-opportunities.png)

### 瞭解機會量度 {#opportunity-metrics}

每個機會檢視都會總結影響，讓您能夠排定工作優先順序：

- **產品頁面**&#x200B;或&#x200B;**URL**：針對該最佳化型別評估的頁面或產品。
- **代理流量**：由AI代理程式發起的造訪與互動，可協助您先排定高影響力機會的優先順序。

### 瞭解建議狀態 {#suggestion-states}

這兩種擴充型別使用相同的工作流程檢視：

- **[!UICONTROL Current Suggestions]**：要檢閱的新專案或作用中專案。
- **[!UICONTROL Fixed Suggestions]**：您已部署或解析的專案。
- **[!UICONTROL Ignored Suggestions]**：您刻意從動作中排除的專案。

### 檢閱和部署PDP擴充 {#review-deploy-pdp}

PDP擴充適用於想要更清楚在AI驅動探索中傳送產品頁面訊息，同時保留您的銷售商設計的店面體驗的團隊。

**若要檢閱和部署PDP擴充：**

1. 從&#x200B;**[!UICONTROL Opportunities]**&#x200B;開啟&#x200B;**[!UICONTROL Product Detail Page Enrichment]**。
1. 在&#x200B;**[!UICONTROL URLs with Suggestions]**&#x200B;表格中，選取&#x200B;**[!UICONTROL Current Suggestions]**。
1. 若為URL或SKU，請按一下&#x200B;**[!UICONTROL Preview]**&#x200B;以檢閱AI分析和建議的擴充。
1. 可選：按一下&#x200B;**[!UICONTROL Copy]**&#x200B;將內容貼到外部編輯器中，或按一下&#x200B;**[!UICONTROL Edit suggestion]**&#x200B;就地編輯。
1. 可選：如果建議不符合您的策略，請將其移至&#x200B;**[!UICONTROL Ignored Suggestions]**。
1. 檢閱並核准後，請選取要更新的URL或SKU列，然後按一下&#x200B;**[!UICONTROL Deploy optimizations]**，再進行確認。

部署後，建議會移至LLM Optimizer中具有最佳化狀態的&#x200B;**[!UICONTROL Fixed Suggestions]**。

>[!NOTE]
>
>PDP擴充部署需要在LLM Optimizer中完成&#x200B;**在Edge**&#x200B;上線時最佳化。 如果上線不完整，UI會提示您先完成設定，然後再部署。

### 檢閱和部署產品目錄擴充 {#review-deploy-catalog}

目錄擴充適用於想要直接在Commerce中收緊產品名稱和完整說明的團隊，在儲存任何內容之前，您可以先檢閱建議。

**若要檢閱及部署產品目錄擴充：**

1. 從&#x200B;**[!UICONTROL Opportunities]**&#x200B;開啟&#x200B;**[!UICONTROL Product Catalog Enrichment]**。
1. 在&#x200B;**[!UICONTROL URLs with Suggestions]**&#x200B;表格中，選取&#x200B;**[!UICONTROL Current Suggestions]**。
1. 按一下URL或SKU列的展開控制項，以顯示建議的&#x200B;**產品名稱**&#x200B;和&#x200B;**產品說明**&#x200B;更新。
1. 可選：在部署之前，按一下編輯圖示可調整建議的名稱或說明。
1. 可選：如果建議不符合您的策略，請將其移至&#x200B;**[!UICONTROL Ignored Suggestions]**。
1. 檢閱並核准後，請選取要更新的URL或SKU列，然後按一下&#x200B;**[!UICONTROL Deploy optimizations]**，再進行確認。

核准的名稱和描述變更會像其他產品更新一樣儲存到您的[!DNL Adobe Commerce]目錄。

>[!IMPORTANT]
>
>將部署視為生產目錄變更。 使用您一般的變更控制、測試和QA實務。 唯有在銷售和SEO利害關係人就最終版本達成一致後部署。

部署後，建議會移至狀態為&#x200B;**已套用**&#x200B;的&#x200B;**[!UICONTROL Fixed Suggestions]**。

## 在Commerce管理員中驗證更新 {#verify-in-admin}

**若要驗證已部署的目錄擴充：**

1. 登入[!DNL Adobe Commerce] **管理員**。
1. 前往&#x200B;**[!UICONTROL Catalog]** > **[!UICONTROL Products]**。
1. 視需要使用篩選器和&#x200B;**存放區檢視**&#x200B;選擇器（例如&#x200B;**[!UICONTROL Default Store View]**），然後搜尋&#x200B;**SKU**。
1. 在編輯模式中開啟產品。

   產品表單顯示擴充的&#x200B;**產品名稱**。

   LLM Optimizer擴充後的![產品名稱欄位](../assets/llmo-admin-name.png)

1. 可選：如果您要保留手動輸入的名稱，請選取&#x200B;**[!UICONTROL Override LLM Optimizer provided Product Name]**。

手動覆寫會影響機會與目錄保持同步的方式；請參閱Admin[&#128279;](#manual-override-in-the-admin)中的手動覆寫。

1. 展開&#x200B;**[!UICONTROL Content]**&#x200B;區段並找到&#x200B;**說明**&#x200B;欄位。

   當您部署說明變更時，就會顯示擴充說明。

   LLM Optimizer擴充後的![說明欄位](../assets/llmo-admin-description.png)

1. 可選：如果您要保留手動輸入的描述，請選取&#x200B;**[!UICONTROL Override LLM Optimizer provided Description]**。

## 驗證店面的更新 {#verify-storefront}

在您的店面搜尋SKU並開啟PDP。 確認&#x200B;**名稱**&#x200B;和任何顯示長&#x200B;**描述**&#x200B;的區域皆反映您核准的內容。 也需確認任何使用相同目錄屬性的下游管道（與轉出相關的位置）。

<!--
## PDP enrichment rollback {#pdp-rollback}

If your project includes PDP enrichment opportunities, **rollback** behavior may support **bulk** or **per-URL** actions, depending on your LLM Optimizer release. Follow the in-product options for rollback. For **[!UICONTROL Product Catalog Enrichment]**, undoing a name or description in Commerce is effectively a new catalog edit or a follow-up opportunity, not a separate undo control in the Admin unless your team implements one.
-->

## 覆寫、擷取和陳舊的機會 {#overrides-ingestion}

在LLM Optimizer更新產品的名稱或說明後，其他擷取系統（例如REST API呼叫、CSV匯入、PIM摘要或類似程式）可能會變更相同欄位。 以下各節將說明在此情況下會發生的情況。

### 內嵌再次傳送原始目錄值

如果外部程式寫入原始名稱或說明（LLM Optimizer部署前存在的值），Commerce會根據整合規則，繼續遵循該欄位的LLM Optimizer部署值。 機會可能不會單獨根據該擷取自動回覆。

### 內嵌會傳送新值

如果外部程式傳送的新值不只是LLM Optimizer前版本的重複（例如，將「Red Shoes」重新命名為「Iconic Red Shoes」），則會接受該新目錄值，而相關的LLM Optimizer機會通常會在LLM Optimizer中標示為&#x200B;*過時*，因為即時目錄不再符合建議內容。

### 在管理員中手動覆寫 {#manual-override-in-the-admin}

如果您在[!DNL Adobe Commerce] *管理員*&#x200B;中手動編輯產品名稱或描述：

- *Admin*&#x200B;值會作為該手動變更的記錄系統而獲勝。
- LLM Optimizer機會標示為&#x200B;*過時*。
- 在LLM Optimizer中，UI會移回該機會的原始狀態，這樣就能重新基準化，或者在分析再次執行時接受新的建議。

這些規則可協助您知道LLM Optimizer、擷取摘要或&#x200B;*管理員*&#x200B;編輯在多個管道接觸同一SKU時是否具有權威性。

## 最佳實務

- **產品名稱和說明的檔案系統擁有權**，這樣PIM或摘要工作就不會無意間與LLM Optimizer的預期衝突。
- **在大量部署標題或說明之前，先與SEO和品牌團隊協調**。
- 主要目錄匯入後，**重新同步**&#x200B;或&#x200B;**重新分析**，以便機會反映目前的目錄狀態。

## 在示範中試用

使用Frescopa示範環境來檢視這兩種Commerce機會型別的運作情況：

- [檢視產品目錄擴充示範](https://play.llmo.now/org/demo-org/opportunities/commerce-product-catalog-enrichment/e5f2a854-7477-421c-820f-74d5dd595647?siteId=9ae8877a-bbf3-407d-9adb-d6a72ce3c5e3)
- [檢視產品詳細資料頁面擴充示範](https://play.llmo.now/org/demo-org/opportunities/commerce-product-page-enrichment/4e8b0428-0893-4864-a00e-fc1d77fb3372?siteId=9ae8877a-bbf3-407d-9adb-d6a72ce3c5e3)

## 相關主題

- [將Adobe Commerce連線至LLM Optimizer](connect-to-llmo.md)
- [整合概述](../overview.md)
- [整合限制和邊界](../boundaries-limits.md)
