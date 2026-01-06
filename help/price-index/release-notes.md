---
title: '[!DNL Catalog Adapter]發行說明'
description: 適用於Adobe Commerce的 [!DNL Catalog Adapter] 的最新發行資訊。
feature: Services, Release Notes
recommendations: noCatalog
roles: Admin, Developer
exl-id: d4dd0288-8853-43fe-9103-1aead8d3b56e
source-git-commit: 47419e7e19611dc4a045c195f259e2126ab77372
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# [!DNL Catalog Adapter]擴充功能發行說明

下列發行說明說明[!DNL Catalog Adapter]擴充功能的最新版本。 支援目前的主要發行版本。 舊版的發行說明僅供參考。

更新包括：

![新](../assets/new.svg)新功能
![修正](../assets/fix.svg)修正和改良
![錯誤](../assets/bug.svg)已知問題


>[!NOTE]
>
>[目錄配接器擴充功能](catalog-adapter.md)會停用Adobe Commerce價格索引。 如果已安裝，您可以使用撰寫器檢查系統上安裝的版本。 在某些情況下，您可能會想要升級系統上的目錄配接器擴充功能，以取得修正或新功能，而不更新Commerce服務版本。

## 目前的主要版本

## 1.0.10版本

![修正](../assets/fix.svg)修正針對匯入或新建立的套件組合產品進行價格查詢時，因為系統嘗試使用串連的SKU來查詢，而非正確的、有效的SKU，而導致內部伺服器錯誤的問題。 套件組合產品的價格查詢現在使用適當的SKU並正確解析。<!--MDEE-1040-->

## 1.0.9版

![修正](../assets/fix.svg)已新增PHP 8.4的相容性。<!--MDEE-941-->

## 1.0.8版本

![修正](../assets/fix.svg)修正將具有數值SKU的可設定產品變體新增至願望清單時，造成例外狀況記錄錯誤的問題。<!--MDEE-876-->
