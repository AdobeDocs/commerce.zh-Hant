---
title: 連線 [!DNL Adobe Commerce] 至 [!DNL Adobe LLM Optimizer]
description: 啟用必要的Commerce服務、設定LLM Optimizer連線、驗證目錄存取權，以及在檢視商機或部署更新之前確認租使用者整備程度。
role: Admin, User
recommendations: noCatalog
badgePaas: label="僅限PaaS" type="Informative" url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案（Adobe管理的PaaS基礎結構）和內部部署專案的Adobe Commerce 。"
source-git-commit: 47348a44ff7c5f890c10594f44cae6e771be046f
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 0%

---

# 將[!DNL Adobe Commerce]連線至[!DNL Adobe LLM Optimizer]

>[!IMPORTANT]
>
>存取此整合受到限制。 如需詳細資訊，請聯絡您的技術客戶經理。

本文說明如何連線您可用於LLM Optimizer的[!DNL Adobe Commerce]目錄。

>[!NOTE]
>
>本文主要介紹整合的Commerce方面。 如需LLM Optimizer的一般資訊，請參閱[LLM Optimizer產品檔案](https://experienceleague.adobe.com/zh-hant/docs/llm-optimizer/using/home)。

## 啟用必要的Commerce服務 {#enable-commerce-services}

請與您的Commerce管理員或實作合作夥伴合作，確認下列事項：

- 根據您的架構（包括部署中的任何SaaS資料匯出工具或聯結器），LLM Optimizer必須讀取的目錄資料為&#x200B;**匯出或同步化**。
- API存取、認證和環境URL （沙箱與生產環境）符合您打算在LLM Optimizer中使用的&#x200B;**租使用者**。

## 在LLM Optimizer中設定Commerce連線 {#configure-commerce-connection}

**若要設定Commerce連線：**

1. 在[!DNL Adobe LLM Optimizer] UI中，開啟&#x200B;**客戶組態**，然後選取&#x200B;**[!UICONTROL Commerce]**&#x200B;索引標籤。

   在[客戶設定]索引標籤上的![Commerce設定](../assets/llmo-commerce-config.png)

1. 按一下&#x200B;**[!UICONTROL Add Store View]**&#x200B;以建立新列，或展開現有的存放區檢視專案以編輯它。
1. 輸入&#x200B;**[!UICONTROL Store View URL]** （必要）。

   使用該存放區檢視的店面URL，包括任何地區設定或路徑前置詞（例如，`https://brand.example.com/`或`https://brand.example.com/fr/`）。

1. 輸入&#x200B;**[!UICONTROL Environment ID]** （必要） — LLM Optimizer應連線之Adobe Commerce環境的識別碼。
1. 輸入&#x200B;**[!UICONTROL Website Code]**、**[!UICONTROL Store Code]**&#x200B;和&#x200B;**[!UICONTROL Store View Code]** （必要）。

   這些值必須與您Commerce管理員中連線的網站、商店和商店檢視的程式碼相符。

1. 可選：如果值與URL不同，請以Commerce執行個體的主機名稱（例如`www.example.com`）輸入&#x200B;**[!UICONTROL Host Name]**。
1. 輸入&#x200B;**[!UICONTROL Adobe Commerce Endpoint]** — 用於API存取之Adobe Commerce執行個體的基底URL。
1. 輸入或貼上用來向Commerce API驗證請求的&#x200B;**[!UICONTROL API Key]**。

   如果您需要在其他位置安全地複製金鑰，請按一下欄位旁的&#x200B;**[!UICONTROL Copy]**。

1. 按一下&#x200B;**[!UICONTROL Save]**&#x200B;以儲存組態。

儲存後，請等待任何&#x200B;**初始同步**&#x200B;或驗證工作完成，然後再為該存放區檢視依賴目錄或稽核結果。

若要移除存放區檢視設定，請開啟該專案，然後按一下&#x200B;**[!UICONTROL Delete]**。

### 欄位說明 {#commerce-connection-fields}

| 欄位 | 說明 |
| --- | --- |
| 存放區檢視URL | LLM Optimizer應將存放區檢視的公用URL視為目錄和稽核工作流程的範圍。 |
| 環境ID | Commerce環境識別碼(來自您的雲端或部署檔案，或管理員（如適用）。 |
| 網站程式碼 | 擁有目錄之網站的Commerce **[!UICONTROL Website Code]**。 |
| 存放區代碼 | 在該網站下的商店使用Commerce **[!UICONTROL Store Code]**。 |
| 存放區檢視代碼 | 商店檢視的Commerce **[!UICONTROL Store View Code]** （例如，`default`）。 |
| 主機名稱 | 表單除了其他URL外還會要求時Commerce店面或執行個體的主機名稱。 |
| Adobe Commerce端點 | LLM Optimizer用來存取Commerce API的例項URL。 |
| API金鑰 | API驗證的秘密金鑰；將其視為任何生產認證。 |

## 確認租使用者和環境整備 {#confirm-tenant-readiness}

- 除非是有意為之，否則請確認連線的&#x200B;**沙箱**&#x200B;專案未與&#x200B;**生產** Commerce資料混合。
- 調整Experience Cloud和Commerce中的&#x200B;**使用者角色**，讓核准部署動作的人員同時擁有適當的許可權。

## 後續步驟 {#next-steps}

[搭配使用LLM Optimizer與Adobe Commerce](use-llmo-with-commerce.md)以檢閱商機、部署目錄更新，並瞭解覆寫行為。
