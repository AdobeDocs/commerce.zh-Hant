---
title: 開始使用 [!DNL Adobe Commerce as a Cloud Service]
description: 瞭解如何開始使用 [!DNL Adobe Commerce as a Cloud Service]。
role: Admin, Developer, User
exl-id: 58d98b9e-b41d-44db-9666-c924a5b005b3
source-git-commit: 9b90e6f79a394ec0941c9e48aee3859f0bcdedd5
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 0%

---

# 快速入門

{{accs-early-access}}

[!DNL Adobe Commerce as a Cloud Service]提供大部分的立即可用設定。 完成幾個基本設定程式後，您的存放區將立即啟動並執行。 本指南會逐步引導您建立和使用執行個體。

按一下底下的標籤，以檢視下列使用者型別的高階工作流程概觀：

* 管理員
* 商家
* 開發人員

>[!BEGINTABS]

>[!TAB 管理員與商家工作流程]

此圖表提供管理員和商家如何存取及管理[!DNL Adobe Commerce as a Cloud Service]執行個體的概觀。 如需有關管理員工作流程的詳細資訊，請參閱[Adobe Admin Console指南](https://helpx.adobe.com/enterprise/admin-guide.html)。

![[!DNL Adobe Commerce as a Cloud Service]商家流程圖](./assets/merchant-flow.svg){zoomable="yes"}

>[!TAB 開發人員工作流程]

此圖表提供開發人員如何使用App Builder為[!DNL Adobe Commerce as a Cloud Service]建立整合的整體概觀。 如需詳細資訊，請參閱[API檔案](https://developer.adobe.com/commerce/services/cloud/)。

![[!DNL Adobe Commerce as a Cloud Service]開發人員流程圖](./assets/developer-flow.svg){zoomable="yes"}

>[!ENDTABS]

## 建立執行個體

>[!NOTE]
>
>在您建立執行個體之前，您組織的產品管理員或系統管理員必須將您新增為[!DNL Adobe Commerce as a Cloud Service]產品的使用者。 如需詳細資訊，請參閱[新增使用者和管理員](./user-management.md#add-users-and-admins)。

[!DNL Adobe Commerce as a Cloud Service]執行個體使用信用型系統。 您可以建立多個執行個體，但每個執行個體都需要相對數量的學分。 您最初的退款金額取決於您的訂閱。

1. 登入您的[Adobe Experience Cloud](https://experience.adobe.com/)帳戶。

1. 在[!UICONTROL Quick access]底下，按一下&#x200B;[!UICONTROL **Commerce**]&#x200B;以開啟[!UICONTROL Commerce Cloud Manager]。

   [!UICONTROL Commerce Cloud Manager]會顯示您的Adobe IMS組織中可用的[!DNL Adobe Commerce as a Cloud Service]執行個體清單。

1. 按一下畫面右上角的&#x200B;[!UICONTROL **新增執行個體**]。

   ![建立執行個體](./assets/create-instance.png){width="50%" align="center" zoomable="yes"}

1. 選取&#x200B;[!UICONTROL **Commerce as a Cloud Service**]。

1. 輸入您執行個體的&#x200B;**名稱**&#x200B;和&#x200B;**描述**。

1. 選取您要託管執行個體的區域。

   >[!NOTE]
   >
   >建立執行個體後，您將無法修改區域。

1. 為您的執行個體選擇&#x200B;[!UICONTROL **環境型別**]。 您可以選擇下列選項：

   * [!UICONTROL **沙箱**] — 適用於設計和測試用途。 您應該使用沙箱環境來開始您的[!DNL Adobe Commerce as a Cloud Service]歷程。
   * [!UICONTROL **生產**] — 用於線上商店和客戶對面的網站。

   >[!NOTE]
   >
   >沙箱例專案前僅限北美區域使用。

1. _（選擇性）_&#x200B;如果您想要包含範例產品資料以進行測試和學習，請從&#x200B;[!UICONTROL **測試資料**]&#x200B;下拉式清單中選取&#x200B;[!UICONTROL **Adobe存放區**]。

   您可以略過此選項，但若略過，您的店面將不會有任何產品。 您必須[匯入您的目錄](#import-your-catalog)才能檢視完整的店面體驗。

1. 按一下&#x200B;[!UICONTROL **新增執行個體**]。

## 存取例項

建立執行個體後，您可以從[!UICONTROL Commerce Cloud Manager]存取它。

1. 登入您的[Adobe Experience Cloud](https://experience.adobe.com/)帳戶。

1. 在[!UICONTROL Quick access]底下，按一下&#x200B;[!UICONTROL **Commerce**]&#x200B;以開啟[!UICONTROL Commerce Cloud Manager]。

   [!UICONTROL Commerce Cloud Manager]會顯示您的Adobe IMS組織中可用的執行個體清單。

1. 若要開啟執行個體的[!UICONTROL Commerce Admin]，請按一下執行個體名稱。

>[!TIP]
>
>若要檢視執行個體的相關資訊，包括REST和GraphQL端點以及管理員URL，請按一下執行個體名稱旁邊的資訊圖示。

## 匯入您的目錄

根據預設，[!DNL Adobe Commerce as a Cloud Service]執行個體不包含任何產品資料。 在匯入您自己的目錄之前，當您建立例項以進行測試和學習時，可以選擇包含範例產品資料。

有兩種方式可將您的目錄匯入[!DNL Adobe Commerce as a Cloud Service]：

* [**Commerce管理員**](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/import/data-import) — 使用者易記的介面，可讓您按幾下滑鼠即可匯入目錄資料。
* [**匯入JSON API**](https://developer.adobe.com/commerce/webapi/rest/modules/import/#import-json-api) - REST API可讓您以程式設計方式匯入目錄資料。

<!-- TODO

- Add guidance about how to choose which method to use
- Add guidance for new vs existing customers (cross-reference OR and _include file for migration content)

-->

## 設定店面

現在您已建立執行個體，您已準備好繼續[設定](storefront.md)您的Commerce店面(由Edge Delivery Services提供技術支援)。
