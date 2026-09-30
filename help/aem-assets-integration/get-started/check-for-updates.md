---
title: 檢查擴充功能更新
description: 瞭解Adobe Commerce如何檢查新的AEM Assets整合擴充功能版本並通知管理員，包括手動CLI檢查。
feature: CMS, Media
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
source-git-commit: 7950f5d171b35054be42ca60d19bafcf43c53cd6
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 4%
---
# 檢查擴充功能更新

透過AEM Assets整合擴充功能1.4.6版及更新版本，Adobe Commerce會自動檢查是否有較新版本的擴充功能可用，並通知管理員使用。 此檢查會以非同步方式作為排程處理的一部分執行，不會阻擋管理員頁面呈現。

## 更新檢查的運作方式

* 更新檢查會將您安裝的`aem-assets-integration`封裝版本與[repo.magento.com](https://repo.magento.com/admin/dashboard)提供的最高相容版本進行比較。
* 快取結果。 載入管理員頁面會讀取最新的快取結果，而非觸發即時網路請求。
* 如果`repo.magento.com`無法使用，或傳回的中繼資料無效，Commerce會保留最後成功的快取結果，而不會封鎖Admin。

>[!NOTE]
>
>更新檢查適用於雲端和內部部署的Adobe Commerce。

## 檢視更新通知

管理員可以在以下任一位置看到可用的更新通知：

* **[!UICONTROL Stores]** > [!UICONTROL Settings] > **[!UICONTROL Configuration]** > **[!UICONTROL Adobe Services]** > **[!UICONTROL AEM Assets Integration]**
* 管理員通知下拉式清單

每個通知都會顯示：

* 安裝的版本
* 可用版本
* 發行分類
* 發行說明的連結

選取&#x200B;**[!UICONTROL Remind me later]**&#x200B;以暫停此Commerce執行個體的通知，或完全選擇退出更新通知。

## 執行手動更新檢查

若要立即檢查是否有可用的更新，請從Commerce根目錄執行下列命令：

```bash
bin/magento aem:assets:check-update
```

這個命令只會檢查和報告可用的更新。 它不會修改Composer檔案或部署更新。 若要安裝更新，請依照[安裝Adobe Commerce套件](configure-commerce.md)中的撰寫器指示操作。

## 擴充功能套件的發行中繼資料

更新檢查會從已安裝封裝`composer.json`檔案的`extra`區段讀取發行中繼資料：

```json
{
  "extra": {
    "release_notes_url": "https://experienceleague.adobe.com/...",
    "release_type": "feature",
    "compatible_commerce_versions": ">=2.4.7 <2.5.0"
  }
}
```

## 下一步

* [安裝Adobe Commerce套件](configure-commerce.md)
