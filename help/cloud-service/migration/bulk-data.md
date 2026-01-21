---
title: 批量資料遷移工具
description: 學習如何使用批量資料遷移工具，將你現有的 Adobe Commerce on Cloud 實例資料遷移到 [!DNL Adobe Commerce as a Cloud Service]其他平台。
feature: Cloud
badgeSaas: label="僅限 SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於 Adobe Commerce as a Cloud Service 及 Adobe Commerce Optimizer 專案（Adobe 管理的 SaaS 基礎設施）。"
role: Developer
level: Intermediate
exl-id: 81522de9-df54-4651-b8ed-58956376af86
source-git-commit: e582ce85b58b57922a8cdd63dbe32bd0f08c64f9
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 0%

---

# 批量資料遷移工具

該大規模資料遷移工具採用分散式架構，確保從 PaaS 環境安全且高效地遷移資料到 SaaS 環境。 此工具協助解決方案實作者將資料從現有的 Adobe Commerce 雲端實例（PaaS）遷移到 [!DNL Adobe Commerce as a Cloud Service] （SaaS）。 欲了解更多遷移流程資訊，請參閱 [遷移概覽](./overview.md)。

>[!NOTE]
>
>批量資料遷移工具僅支援遷移第一方核心商務資料。 目前不支援自訂資料遷移。

下圖詳細說明使用大量資料移轉工具的架構和關鍵元件。

![大量資料移轉工具架構圖，顯示PaaS至SaaS資料流程](../assets/bulk-data-diagram.png){zoomable="yes"}

## 移轉工作流程

大量資料移轉工作流程包含下列步驟：

1. 設定新的遷移環境。
1. 從舊系統複製你的資料。
1. 把你的資料移到新系統。
1. 讓您的產品目錄在新系統中公開。
1. 確認你的資料是否正確遷移。

以下各節會詳細說明這些步驟。

## 存取大量資料移轉工具

批量資料遷移工具的可用性如下：

- **2026** 年第一季（尚未提供）-批量資料遷移工具初次釋出後，您可以透過提交支援工單來存取。
- **2026** 年第一季（尚未提供）-在大量資料遷移工具公開發布後，將可從此頁面存取。

## 創造目標環境

解決方案實作者（SI）建立遷移的目標環境。 此環境儲存從來源實例遷移的資料。

首先，建立 [一個新的 [!DNL Adobe Commerce as a Cloud Service] （SaaS）實例](../getting-started.md#create-an-instance)。

### 設定擷取工具

使用擷取工具從來源實例擷取資料。

1. 從 Adobe 提供的連結下載解壓工具。
1. 在擷取工具中設定以下環境變數：
   - 您現有MySQL資料庫的連線詳細資料
   - 您的[!DNL Adobe Commerce as a Cloud Service]執行個體的目標租使用者ID
   - 您的IMS憑證，包括：
      - 使用者端ID
      - 使用者端密碼
      - IMS範圍
      - IMS URL - 基本網址。 例如， `https://ims-na1.adobelogin.com/`。
      - IMS組織ID

   針對IMS範圍和其他值，請在&#x200B;**Adobe Developer Console**&#x200B;中專案內的[認證](https://developer.adobe.com/console/)區段中選取您的OAuth型別。 在擷取工具隨附的`.example.env`檔案中提供詳細資訊。

### 擷取資料

在執行擷取工具前，解決方案實作者必須先建立一條 SSH 隧道，連接至 PaaS 資料庫，方法包括：

```bash
magento-cloud tunnel:open
```

接著執行擷取工具，它會：

1. 連接 PaaS 資料庫，分析其結構，並與 SaaS 租戶結構細節做比較。
1. 根據 PaaS 與 SaaS 之間的共通架構元素，產生擷取與轉型計畫。
1. 使用目錄資料管理服務（CDMS）擷取資料。

### 載重資料

執行Adobe提供的載入資料工具。 此工具將：

1. 使用移轉帳戶連線至SaaS租使用者資料庫。
1. 產生載入計畫。
1. 執行計畫，將資料批次移至SaaS租使用者資料庫。
1. 處理目錄媒體並將其傳輸到目標環境。
1. 清除 SaaS Redis 快取並使租戶的資料庫索引失效。

### 目錄資料擷取

資料載入後，目錄資料會自動從 SaaS 租戶資料庫流向目錄服務。

目錄服務會將這些資料與即時搜尋及產品推薦共享。 此程式不需要手動介入。 資料一旦擷取完成，所有服務都能取得。

### 資料完整性驗證

遷移後，CDMS 會執行以下自動資料完整性檢查，以確保遷移資料的準確性與完整性：

**基於 API 的驗證**

在驗證過程中，CDMS 會將先前查詢的 REST 與 GraphQL API 回應，與目標實例的對應紀錄進行比較。 任何差異都會在遷移狀態中顯示。

**資料庫層級驗證**

在驗證過程中，CDMS 會計算擷取紀錄的數量，並將其與載入的紀錄數量進行比較。

**按需驗證（可選）**

您也可以手動觸發對所有系統紀錄的全面驗證：

>[!NOTE]
>
>此過程資源密集，僅應用於沙盒環境。

完整驗證包括：

- 完整的基於 API 的驗證，使用所有預先擷取的 REST 與 GraphQL API 回應
- 找到任何不一致的詳細報告
