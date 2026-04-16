---
title: ' [!DNL Product Recommendations]簡介'
description: '[!DNL Product Recommendations]是強大的行銷工具，可用來增加轉換率、增加收入及刺激購物者參與。'
recommendations: noCatalog
badgePaas: label="僅限PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="僅適用於雲端專案（Adobe管理的PaaS基礎結構）和內部部署專案的Adobe Commerce 。"
exl-id: 72850cfd-555c-4e0e-ac3e-097e6dac2030
source-git-commit: 1ae6b0f6786375ca4e7bb7620e164008a08f8965
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 0%

---

# [!DNL Product Recommendations]簡介

產品推薦是強大的行銷工具，可用來增加轉換率、增加收入及刺激購物者參與。 Adobe Commerce產品建議由[Adobe AI](https://business.adobe.com/ai.html)提供技術支援，其使用人工智慧和機器學習演演算法來對彙總的訪客資料執行深入分析。 此資料與您的Adobe Commerce目錄結合後，會產生極為引人入勝、相關且個人化的體驗。

>[!IMPORTANT]
>
>**產品建議不是可供HIPAA使用的服務。**&#x200B;請勿在使用HIPAA就緒的產品或以其他方式處理受保護的健康資訊(PHI)的任何Adobe Commerce實作中啟用或使用產品建議。 產品建議是Commerce SaaS服務的一部分，目前分類為不符合HIPAA標準。
>
>如需哪些是HIPAA就緒的Adobe Commerce功能以及哪些服務不可搭配PHI使用的詳細資訊，請參閱Adobe Commerce[和](https://experienceleague.adobe.com/en/docs/commerce-admin/start/compliance/hipaa-ready-service/overview)作業[上的](https://experienceleague.adobe.com/en/docs/commerce-admin/start/compliance/hipaa-ready-service/operations#adobe-commerce-services)HIPAA就緒性。

產品推薦會以具有標籤的單位形式出現在商店中，例如「檢視過此產品的客戶也檢視過」。 您可以直接從Adobe Commerce管理員跨商店檢視建立、管理和部署建議。

如果您的店面是使用PWA Studio實作，請參閱[PWA檔案](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/)。 如果您使用自訂前端技術，例如React或Vue JS，請瞭解如何[整合](headless.md) [!DNL Product Recommendations]到您的Headless店面。

>[!NOTE]
>
>有許多方法可以開發Headless或自訂實作。 本指南會說明使用PWA Studio來執行此操作的一種方式。 它並未涵蓋所有案例或事件。

## 隱私權

以[!DNL Product Recommendations]為目的的資料收集不包含任何個人識別資訊(PII)。 此外，所有使用者識別碼（例如Cookie ID和IP位址）都需嚴格匿名處理。 若要進一步瞭解，請參閱[Adobe隱私權原則](https://www.adobe.com/privacy/policy.html)。

[!DNL Product Recommendations]使用者可以參考[資料管理儀表板](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html)，以取得資料同步的更多資料。

## 產品建議與產品關係

考慮到線上購物不斷變化的複雜性，最適合店面的往往是多種關鍵技術的組合。 同時使用[!DNL Product Recommendations]和[產品關係](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/product-relationships/product-relationships.html)可讓您在促銷產品時擁有更多彈性。 您可以運用Adobe AI支援的[!DNL Product Recommendations]，以智慧化方式大規模自動化您的建議。 然後，當您必須手動介入並確保向目標購物者區段提出特定建議，或當必須達成某些業務目標時，您可以運用[相關產品規則](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/product-relationships/product-related-rules.html)。

產品建議可讓您：

- 根據下列區域，從9種不同的智慧型建議型別中進行選擇：購物者型、專案型、人氣型、趨勢型和相似度型
- 在整個購物者的店面歷程中使用行為資料來個人化建議
- 測量與每個建議相關的關鍵量度，協助您瞭解建議的影響

## [!DNL Product Recommendations]展示

觀看此影片以瞭解[!DNL Product Recommendations]：

>[!VIDEO](https://video.tv.adobe.com/v/343991?quality=12)

## 目錄資料保留原則

如果您連續90天未提交測試環境中目錄資料的查詢，則目錄資料會設定為休眠模式，且任何查詢都不會傳回任何資料。 此原則不會影響生產環境中的目錄資料。

### 非使用中的測試環境

若要在您的測試環境中重新啟用目錄資料，請[提交標題為「重新啟用](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#experience-league-start-page)」的支援請求[!DNL Product Recommendations]，並包含環境ID。 您測試環境中的目錄資料應在數小時內還原。

### 清空目錄

如果您的環境在建立後45天內有空白目錄，則目錄資料會設定為休眠模式，不會為所有查詢傳回任何資料。 這包括生產和測試環境。

若要在您的環境中重新啟用目錄資料，請[提交標題為「重新啟用](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#experience-league-start-page)」的支援請求[!DNL Product Recommendations]，並包含環境ID。 您環境中的目錄資料應在數小時內還原。
