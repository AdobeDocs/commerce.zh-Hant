---
source-git-commit: a3ade1a31d3c2905b601f71bda118de89c43cf59
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%
---
# 取得[!DNL Commerce Optimizer]執行個體詳細資料

從[!DNL Commerce Optimizer]執行個體[[!DNL Instance details] 頁面](/help/optimizer/get-started.md#manage-instances)上的&#x200B;_[!DNL Instance Id]_欄位或用來存取執行個體的URL取得_&#x200B;租使用者識別碼&#x200B;_。 例如，在`https://experience.adobe.com/#/@<your organization>/in:<tenant>/commerce-optimizer-studio/home`中。

1. 從Commerce Admin中，選取&#x200B;**[!UICONTROL Adobe Commerce Optimizer]**&#x200B;以顯示包含指示的設定頁面。

   ![[!DNL Commerce Optimizer]設定頁面](/help/aco-connector/assets/aco-connector-admin-installation.png){width="500" zoomable="yes"}

1. 從命令列，[使用SSH](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/secure-connections)連線到[!DNL Adobe Commerce]中繼環境。

1. 若要設定整合，請執行下列[!DNL Adobe Commerce] CLI命令，將預留位置值取代為[!DNL Commerce Optimizer]專案的值：

   ```shell
   bin/magento aco:config:init --org_id=your-org --tenant_id=your-tenant --client_id=your-client-id --client_secret=your-secret
   ```

1. 返回Commerce管理員並選取[!UICONTROL Adobe Commerce Optimizer]選項，以驗證連線。

   當您選取選項時，它會在新索引標籤中開啟[!DNL Commerce Optimizer] UI。
