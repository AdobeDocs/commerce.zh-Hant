---
title: 商店履行的設定概述
description: 瞭解可用於自訂Store Fulfillment解決方案所提供的延伸履行功能的管理員組態設定型別，以及完成組態的相關說明連結。
role: Admin
level: Intermediate
feature: Shipping/Delivery, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# Store Fulfillment的設定概述

在「Adobe Commerce管理員」中，Walmart Commerce Technologies的「商店履行服務」組態設定會依型別分類。

**依型別**&#x200B;儲存履行組態設定

| **型別** | **描述** | **可設定的API** |
|--------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------|
| [一般組態](enable-general.md) | 為Store Fulfillment解決方案設定的一般整合、其作用中的功能，以及連線至履行服務的認證。 | 否 |
| [銷售電子郵件設定](sales-emails.md) | 針對簽到程式期間傳送的客戶通知，設定其他電子郵件範本。 | 否 |
| [商家商店設定](merchant-store-configuration.md) | 將增強的Inventory management來源設定為商家商店。 | 是 |
| [產品庫存管理](product-stock.md) | 設定可供客戶使用的商家股票訊息和功能。 | 是 |
| [Inventory management Source傳輸](inventory-stock-transfer.md) | 設定新庫存，將庫存移出預設庫存。 | 是 |
| [多個網站/領域組態](multi-site-and-scope-config.md) | 為多個網站/商店範圍設定庫存和傳送方法。 | 否 |
| [背景處理序系統組態](background-processes.md) | 設定與履行服務同步資料所使用的背景處理排程。 | 否 |
| [存放區位置和對應設定](store-location-map-provider-setup.md) | 設定使用距離提供者來搜尋零售商店並在SLS地圖中顯示此資訊的功能 | 是 |
| [簽入體驗設定](check-in-experience-setup.md) | 設定入庫程式期間可用的汽車顏色和汽車製造選項 | 是 |
| [使用者設定](user-setup.md) | 管理使用Store Assist應用程式之商店關聯的使用者帳戶、角色和許可權。 範圍。 | 是 |
| [應用程式設定](app-setup.md) | 檢閱完成上線流程所需的Store Assist應用程式的可用設定。 這些設定無法從Adobe Commerce管理員進行設定。 | 是 |

## 使用設定參考

在&#x200B;_依型別_&#x200B;儲存履行組態設定中選取型別名稱，以檢視每個設定型別的組態參考。

在每種型別的組態參考中，組態詳細資訊會顯示在含有下列欄標題的表格中：

- **欄位**&#x200B;參考要設定的欄位名稱

- **描述**&#x200B;提供欄位用途和行為的重要詳細資訊

- **範圍**&#x200B;指出設定的Adobe Commerce設定範圍（全域、網站、商店）

- **必要**&#x200B;值表示欄位上是否必須設定值

如需技術參考，您還可以找到每個欄位的內部設定路徑。
