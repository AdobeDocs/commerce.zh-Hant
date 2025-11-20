---
title: 目錄同步
description: 瞭解如何將產品資料從 [!DNL Commerce] 伺服器匯出至 [!DNL Commerce Services]。
feature: Catalog Management, Data Import/Export, Catalog Service
exl-id: 99f96b93-b036-490c-8c57-40463a0de365
source-git-commit: ae672ed3f2693e2f14e8c7f379e59ef117a34fc3
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---

# 目錄同步

>[!NOTE]
>
> 「目錄同步」控制面板現在是「資料管理」控制面板。 此改版後的儀表板現在支援[[!DNL Product Recommendations]](../product-recommendations/guide-overview.md) v6.0.0+、[[!DNL Live Search]](../live-search/overview.md) v4.1.0+和[[!DNL Catalog Service]](../catalog-service/overview.md) v1.17+。 客戶可以更新至其中一項服務的最新版本，以取得資料管理控制面板。 請在[資料管理儀表板](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html?lang=zh-Hant)檔案中閱讀更多相關資訊。 目前這個主題仍適用於尚未升級且仍擁有目錄同步控制面板的使用者。

Adobe Commerce使用索引器將目錄資料編譯到表格中。 此程式會由[事件](https://experienceleague.adobe.com/docs/commerce-admin/systems/tools/index-management.html?lang=zh-Hant#events-that-trigger-full-reindexing)自動觸發，例如產品價格或存貨層次的變更。

目錄同步服務會持續將產品資料從[!DNL Adobe Commerce]執行個體移動到[!DNL Commerce Services]平台，以保持資料在最新狀態。 例如，[[!DNL Product Recommendations]](/help/product-recommendations/overview.md)需要目前的目錄資訊，才能正確傳回具有正確名稱、定價和可用性的建議。 使用&#x200B;_目錄同步_&#x200B;儀表板來觀察和管理同步處理或命令列介面以觸發目錄同步並重新索引產品資料以供[!DNL Commerce Services]使用。 請參閱[SaaS資料匯出](../data-export/data-export-cli-commands.md)指南中的&#x200B;_命令列介面參考_。

## 存取目錄同步控制面板

若要存取目錄同步處理儀表板，請選取&#x200B;**系統** > _資料傳輸_ > **目錄同步處理**。

使用&#x200B;**目錄同步**&#x200B;儀表板，您可以：

- 檢視同步處理狀態（**進行中**，**成功**，**失敗**）
- 檢視同步的產品總數
- 搜尋同步的產品以檢視其目前狀態
- 依名稱、SKU等搜尋商店目錄。
- 檢視JSON中的同步產品詳細資料，以協助診斷同步差異
- 重新起始同步處理作業

### 上次同步

報告下列專案的同步狀態：

- **Success** — 顯示同步處理成功的日期與時間以及更新的產品數目
- **失敗** — 顯示嘗試同步的日期和時間
- **進行中** — 顯示上次成功同步的日期和時間

目錄同步程式每小時會自動執行一次。 如果在店面沒有看到預期的產品，或產品未反映您最近所做的變更，您可以解決[目錄同步問題](#resolvesync)。

### 產品已同步

顯示從您的[!DNL Commerce]目錄同步的產品總數。 初次同步後，只應同步已變更的產品。

## 重新同步 {#resync}

如果必須在每小時排程同步發生之前啟動目錄重新同步，則可以強制進行重新同步。

>[!NOTE]
>
> 強制重新同步會觸發整個產品目錄的重新同步，而這會增加硬體資源的負載。

1. 從&#x200B;_目錄同步_&#x200B;儀表板，選取&#x200B;**設定**。

   _目錄同步處理設定_&#x200B;頁面就會顯示。

1. 在&#x200B;_重新同步資料_&#x200B;區段中，按一下[!UICONTROL Resync]。

   [!DNL Commerce]會在下一個排定的同步處理期間同步您的目錄。 視目錄大小而定，這項作業可能需要很長的時間。

## 同步的目錄產品

**同步目錄產品**&#x200B;表格會顯示下列資訊。

| 欄位 | 說明 |
|---|---|
| ID | 產品的唯一識別碼 |
| 名稱 | 產品的店面名稱 |
| 型別 | 識別產品型別，例如，簡單、可設定或可下載 |
| 上次匯出 | 上次成功從目錄中匯出產品的日期 |
| 上次修改時間 | 上次在目錄中修改產品的日期 |
| SKU | 顯示產品的庫存單位 |
| 價格 | 產品的價格 |
| 可見度 | 在[!DNL Commerce]目錄中定義的產品可見性設定 |

## 解決目錄同步問題 {#resolvesync}

請參閱[SaaS資料匯出指南](../data-export/troubleshooting-logging.md#troubleshooting)中的&#x200B;_記錄檔和疑難排解_。
