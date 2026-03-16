---
title: 管理您的應用程式
description: 將App Builder應用程式與您的Commerce執行個體建立關聯、設定和取消關聯。
feature: App Builder, Extensibility, Integration
source-git-commit: 4a5174d074a020f6199ed121e0289939612bc5c2
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---


# 管理您的應用程式

應用程式管理員會將App Builder應用程式與其Commerce執行個體建立關聯。 設定表單會根據應用程式的架構動態轉譯，因此不需要自訂管理員UI開發。 應用程式管理員會透過Commerce自動產生的表單來配置設定。

![應用程式管理](assets/app-management-view.png){width="500" zoomable="yes"}

## 先決條件

建立應用程式關聯之前，請確定您具備下列條件：

| 需求 | 說明 |
|-------------|-------------|
| **管理員存取權** | 具有[!DNL App Management]許可權的Commerce管理員 |
| **已部署的應用程式** | App Builder應用程式已部署到您的組織並準備好連線 |
| **組織存取權** | 存取已部署應用程式的Adobe組織 |

## 教學課程

觀看此影片，瞭解如何將應用程式與Commerce執行個體建立關聯並設定設定。

>[!VIDEO](https://video.tv.adobe.com/v/3478966?captions=chi_hant)

## 關聯應用程式

關聯程式會從Commerce匯入網站、商店和商店檢視，以及在應用程式和您的Commerce執行個體之間建立連結。

若要將您的App Builder應用程式連結至Commerce執行個體：

1. 導覽至&#x200B;**[!UICONTROL Apps]** > **[!UICONTROL App Management]**。

1. 按一下&#x200B;**[!UICONTROL Associate App]**。

   ![關聯應用程式](assets/associate-app.png){width="500" zoomable="yes"}

1. 從清單中選取&#x200B;**[!UICONTROL Project]**。

1. 選取&#x200B;**[!UICONTROL Workspace]**。

1. 按一下&#x200B;**[!UICONTROL Associate]**。

   ![應用程式詳細資料](assets/app-details.png){width="500" zoomable="yes"}

>[!WARNING]
>
>如果範圍同步失敗，關聯仍會完成。 您稍後可以從關聯應用程式組態中的&#x200B;**[!UICONTROL Manage Scopes]**&#x200B;檢視手動同步範圍。

## 設定設定

在[!DNL App Management]檢視中建立應用程式關聯後，請透過表單設定其設定：

1. 按一下關聯應用程式上的&#x200B;**[!UICONTROL Configure]**。

1. 表單會顯示應用程式可設定的設定。

1. 視需要修改值。

1. 按一下&#x200B;**[!UICONTROL Save]**。

### 範圍特定設定

當不同的網站、商店或商店檢視需要唯一的設定時，請使用範圍特定的設定。 例如，僅針對特定區域或商店檢視啟用功能，或針對每個品牌使用不同的設定。 較低範圍的設定會覆寫較高範圍的設定。

覆寫特定範圍層級的全域值：

1. 按一下&#x200B;**[!UICONTROL Change Scope]**。

1. 從清單中選取範圍。

1. 修改此範圍的值。

1. 按一下&#x200B;**[!UICONTROL Save]**。

## 管理範圍

從應用程式詳細資訊畫面存取&#x200B;**[!UICONTROL Manage Scopes]**&#x200B;以管理您應用程式的範圍階層。

![管理範圍](assets/manage-scopes.png){width="500" zoomable="yes"}

| 動作 | 說明 |
|--------|-------------|
| **[!UICONTROL Add root scope]** | 新增僅套用至應用程式的範圍。 |
| **[!UICONTROL Sync Commerce scopes]** | 新增或變更網站、商店和商店檢視後，從Commerce重新整理清單。 |
| **[!UICONTROL Import scopes]** | 從檔案大量匯入範圍。 |

## 取消關聯應用程式

當您不再需要應用程式連線至您的Commerce執行個體時，請取消關聯應用程式。 例如，您可能需要淘汰整合、切換到不同的工作區或清除測試設定。

>[!WARNING]
>
> 取消關聯會移除此執行處理的所有組態值。 此動作無法還原。

若要從Commerce例項移除應用程式：

1. 導覽至&#x200B;**[!UICONTROL Apps]** > **[!UICONTROL App Management]**。

1. 按一下應用程式上的&#x200B;**[!UICONTROL Unassociate]**。

1. 確認動作。

## 相關檔案

* [疑難排解 [!DNL App Management]](troubleshooting.md) — 解決應用程式關聯和設定的常見問題。
