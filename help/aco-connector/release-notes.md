---
title: '[!DNL Adobe Commerce Optimizer Connector]發行說明'
description: 瞭解 [!DNL Adobe Commerce Optimizer Connector] 發行說明，包括目錄同步和匯出的新功能、錯誤修正和已知問題。
feature: Release Notes
TQID: 'https://experienceleague.adobe.com/6NeLAfThvIWIyV4Y6OWtL8V9mC7lPy7UH-Zli8E-WEk'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
subfeature_v2:
  - id: dad884f1-e840-49a1-970e-2f965bdbc410
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: af45543a52d1c88149574dc22cdef37af01404c8
workflow-type: tm+mt
source-wordcount: 353
ht-degree: 0%

---

# Adobe Commerce Optimizer Connector發行說明

以下版本說明說明[!DNL Adobe Commerce Optimizer Connector]的所有版本，包括：

![新](../assets/new.svg)新功能
![已修正問題](../assets/fix.svg)修正和改良
![已知問題](../assets/bug.svg)已知問題

## 2026版本

### 1.0.14版本

_2026年6月11日_

![修正](../assets/fix.svg) **PHP 8.5相容性** - [!DNL Adobe Commerce Optimizer Connector]現在支援PHP 8.5，因此您可以升級[!DNL Adobe Commerce]環境，而不會中斷聯結器功能或目錄同步處理。<!--MDEE-1388-->

![修正](../assets/fix.svg) **貨幣變更後價格簿更新** — 貨幣變更後，更新的價格會自動反映在Adobe Commerce Optimizer中。<!--MDEE-1384-->

![修正](../assets/fix.svg) **導覽遵循已停用或隱藏的父類別** — 來自已停用或隱藏類別階層的產品不再意外出現在導覽體驗中。<!--MDEE-1385-->

![修正](../assets/fix.svg) **中繼更新後一致的類別URL** — 套用中繼更新後，類別連結和導覽仍會維持正確。<!--MDEE-1395-->

### 1.0.13版本

_2026年5月6日_

![修正](../assets/fix.svg) **已改善[!DNL Adobe Commerce Optimizer Connector]設定指示** — 已更新Commerce管理員中的[!DNL Adobe Commerce Optimizer]設定頁面，以連結至&#x200B;_[!DNL Adobe Commerce Optimizer Connector]整合指南_。
<!--COMOPT-1922-->

![修正](../assets/fix.svg) **[!DNL Adobe Commerce Optimizer Connector]中繼資料增強功能** - [!DNL Adobe Commerce Optimizer Connector]現在會在中繼資料標頭中包含已安裝版本。 這項改善可讓團隊快速識別在疑難排解或支援工作期間使用的聯結器版本。<!--MDEE-1323-->

### 1.0.12版

_2026年4月2日_

![新的](../assets/new.svg) **已在`saas:resync`命令中新增類別摘要的支援** — 您現在可以使用`saas:resync` CLI命令輕鬆重新整理並檢視您最新的類別資料：

```terminal
bin/magento saas:resync --feed=categories
```

### 1.0.11版

_2026年3月10日_

![已修正問題](../assets/fix.svg)修正相容性問題，當[!DNL Adobe Commerce Optimizer Connector]安裝在[!DNL Adobe Commerce]執行個體上時，會封鎖從Commerce管理員&#x200B;**[!UICONTROL System]**&#x200B;與&#x200B;**[!UICONTROL Configuration]**&#x200B;功能表存取[!DNL Commerce Services Connector]設定頁面。  現在，您可以在同時安裝兩個擴充功能時存取[!DNL Commerce Services Connector]設定頁面。<!--MDEE-1322-->


### 1.0.10版本

_2026年3月9日_

![修正](../assets/fix.svg)如果您在完成聯結器設定之前存取&#x200B;**[!UICONTROL Data Feed Sync Status]**&#x200B;頁面，現在會自動重新導向至聯結器設定頁面。 此引導式流程可確保聯結器設定完成，並有助於防止遺失組態設定所造成的錯誤，這些設定可能導致狀態專案失敗或不完整。<!--MDEE-1296-->

### v1.0.9版本

_2026年3月01日_

[!DNL Adobe Commerce Optimizer Connector]的一般可用性版本。

>[!NOTE]
>
>如果您已參與[!DNL Adobe Commerce Optimizer Connector]的Beta程式，且已安裝舊版擴充功能，請升級至「一般可用性」版本，以接收最新更新。
