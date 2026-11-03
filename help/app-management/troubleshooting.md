---
title: 疑難排解[!DNL App Management]
description: 解決應用程式關聯、安裝、設定和升級的常見問題。
feature: App Builder, Extensibility, Integration
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 72863f3c-9d27-5dda-afe1-d9f934b1fba0
    internal-label: Extensibility
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
    internal-label: Developer tools
subfeature_v2:
  - id: a743e5dc-8f37-4b5d-a848-03c32ca30598
    internal-label: App Builder
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: a00b9e1654a572e1773b5b7e321683332882d86f
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 0%
---
# 疑難排解[!DNL App Management]

使用下列解決方案解決應用程式關聯、安裝、設定和升級的常見問題。

## 聯絡您的應用程式提供者之前

請依照以下針對您問題的步驟操作。 如果您需要應用程式開發人員或提供者的協助，請收集下列資訊：

* 應用程式名稱和已安裝的版本（如果可從應用程式卡上的&#x200B;**[!UICONTROL Manage]** > **[!UICONTROL Details]**&#x200B;取得）。
* 受影響的Commerce執行個體和Adobe組織。
* 失敗的作業，例如安裝或升級，以及失敗的步驟。
* 顯示的錯誤訊息和失敗熒幕擷圖（若有）。
* 失敗的大約時間，包括時區。
* 任何重試嘗試及其結果。

## 應用程式未顯示

如果部署後應用程式未出現在清單中，請檢查下列步驟：

1. 確認應用程式已部署並可於您的組織中使用。

1. 確認您已登入Developer Console中的正確Adobe組織。

1. 確認應用程式已準備好連線（您的應用程式開發人員或合作夥伴可確認）。

如果應用程式仍未顯示，請連絡您的應用程式開發人員，或參閱[Commerce擴充功能 [!DNL App Management]](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"}檔案以取得技術資訊。

## 範圍同步失敗

如果領域同步在關聯應用程式時失敗，請嘗試下列步驟：

1. 檢查您的Commerce執行個體是否可存取且上線。

1. 確認您的API認證有效且具有正確許可權。

1. 嘗試從應用程式設定中的&#x200B;**[!UICONTROL Manage Scopes]**&#x200B;手動同步。

## 設定未儲存

如果設定變更未儲存，請嘗試下列步驟：

1. 檢查所有必填欄位是否已填寫且有效。

1. 確保您擁有修改應用程式設定的正確許可權。

1. 請嘗試重新整理頁面並再次儲存。

如果問題仍然存在，請檢查您的瀏覽器主控台是否有錯誤，或聯絡您的應用程式開發人員。

## 安裝失敗

保持安裝頁面開啟而不重新整理，直到安裝完成。 關閉或重新整理它可能會使安裝無法正確完成。

如果安裝回報失敗：

1. 記下失敗的專案和任何顯示的錯誤訊息。

1. 檢查您是否已完成應用程式的預先安裝指示。

1. 請要求應用程式開發人員檢查失敗的步驟，並在再次嘗試安裝之前修正原因。

失敗的安裝可能會保留部分變更。 重試安裝時，會略過記錄為成功的自訂步驟；失敗或中斷的步驟可以再次執行。 要求您的開發人員檢查由部分執行建立的資源。

## 升級失敗

升級失敗可能會留下部分作業套用。 請勿將應用程式取消關聯並重新安裝作為例行復原步驟，因為取消關聯會移除設定，並可能執行破壞性的清理指令碼。

1. 識別失敗的步驟並記錄任何顯示的錯誤訊息。

1. 請您的應用程式開發人員檢查記錄、檢查是否已對Commerce或外部資源進行變更，並更正原因。

1. 在[!DNL App Management]中，選取&#x200B;**[!UICONTROL Retry Upgrade]**。 此動作適用於手動和自動升級模式。

每次重試都會從目前狀態建立新計畫。 記錄為成功的自訂安裝步驟會被跳過；失敗或中斷的步驟可以再次執行。 在自動模式中，再次部署應用程式也會觸發另一次升級嘗試。

如果重複嘗試失敗，請要求應用程式開發人員保留執行，或嘗試ID和任何執行啟動ID以進行疑難排解。 如需狀態命令、嘗試歷程記錄和執行階段記錄檔，請參閱開發人員檔案中的[重試失敗的升級](https://developer.adobe.com/commerce/extensibility/app-management/upgrade-app/#retry-a-failed-upgrade){target="_blank"}。

## 升級後資源仍會保留

從應用程式設定中移除自訂安裝步驟時，不會執行其解除安裝指令碼或移除其建立的資源。 升級計畫會警告已移除步驟沒有指令碼執行，且步驟在升級後不會出現在進度畫面或應用程式詳細資料中。

請要求您的應用程式開發人員確認資源是否仍為必要，並在需要時提供清理移轉。 請參閱管理員工作流程的[升級應用程式](manage-app.md#upgrade-an-app)。

如需技術疑難排解資訊，請參閱[Commerce擴充性 [!DNL App Management]](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"}。
