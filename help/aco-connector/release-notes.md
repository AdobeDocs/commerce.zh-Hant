---
title: '[!DNL Adobe Commerce Optimizer Connector]發行說明'
description: 適用於Adobe Commerce的 [!DNL Adobe Commerce Optimizer Connector] 的最新發行資訊。
feature: Services, Catalog Service, Release Notes
source-git-commit: 205fca38b379f94027a965b58826ffd922577f61
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# Adobe Commerce Optimizer Connector發行說明

以下版本說明說明[!DNL Adobe Commerce Optimizer Connector]的所有版本，包括：

![新](../assets/new.svg)新功能
![已修正問題](../assets/fix.svg)修正和改良
![已知問題](../assets/bug.svg)已知問題

## 2026版本

### 1.0.12版

_2026年4月2日_

![新](../assets/new.svg) **已在`saas:resync`命令中新增類別摘要的支援** — 您現在可以使用`saas:resync` CLI命令輕鬆重新整理並檢視您最新的類別資料：

```terminal
bin/magento saas:resync --feed=categories
```

_2026年3月10日_

![修正問題](../assets/fix.svg)修正在Commerce執行個體上安裝Commerce聯結器時，無法從Commerce管理系統和設定功能表存取Adobe Commerce Optimizer服務聯結器設定頁面的相容性問題。  現在，您可以在同時安裝兩個擴充功能時，存取Commerce服務聯結器設定頁面。<!--MDEE-1322-->


### v1.0.10版本

_2026年3月9日_

![修正](../assets/fix.svg)如果您在完成聯結器設定之前存取「資料摘要同步狀態」頁面，現在會自動將您重新導向至聯結器設定頁面。 此引導式流程可確保聯結器設定完成，並有助於防止遺失組態設定所造成的錯誤，這些設定可能導致狀態專案失敗或不完整。<!--MDEE-1296-->

### v1.0.9版本

_2026年3月01日_

Adobe Commerce Optimizer Connector正式發行版本。

>[!NOTE]
>
>如果您參與Adobe Commerce Optimizer Connector的Beta計畫，且已安裝舊版擴充功能，請升級至「一般可用性」版本，以接收最新更新。

