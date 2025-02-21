---
title: 驗證事件集合
description: 瞭解如何確認行為資料是否正傳送至Adobe Commerce。
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# 驗證事件集合

在您[安裝並設定](install-configure.md) `magento/product-recommendations`模組後，您可以驗證行為資料是否已傳送至Adobe Commerce。 您可以使用Chrome中提供的開發人員工具，或安裝Snowplow Chrome擴充功能。 若您需要其他說明，請參閱支援知識庫中的[疑難排解 [!DNL Product Recommendations] 模組](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/troubleshoot-product-recommendations-module-in-magento-commerce.html)。

## 使用Chrome中的開發人員工具進行驗證

若要確保事件收集器JS檔案正在所有網站頁面上載入：

1. 在Chrome中，選擇&#x200B;**自訂及控制Google Chrome**，然後選取&#x200B;**更多工具** > **開發人員工具**。
1. 選擇&#x200B;**網路**&#x200B;標籤，然後選取&#x200B;**JS**&#x200B;型別。
1. `ds.`的篩選器
1. 重新載入頁面。
1. 您應該會在&#x200B;**Name**&#x200B;欄中看到`ds.js`或`ds.min.js`。

![事件收集器JS](assets/filter-ds.png)
_事件收集器JS_

若要確保您的網站上的頁面（首頁、產品、結帳等）都會觸發事件：

1. 請務必停用瀏覽器上的任何廣告封鎖程式，並接受網站上的Cookie。
1. 在Chrome中，選擇&#x200B;**自訂及控制Google Chrome** （瀏覽器右上角的三個垂直點），然後選取&#x200B;**更多工具** > **開發人員工具**。
1. 選擇&#x200B;**網路**&#x200B;索引標籤並篩選`tp2`。
1. 重新載入頁面。
1. 您應該會在&#x200B;**名稱**&#x200B;欄中看到`tp2`底下的呼叫。

![正在引發事件](assets/filter-tp2.png)
_確認事件正在引發_

## 使用Snowplow Chrome擴充功能進行驗證

安裝Chrome](https://chrome.google.com/webstore/detail/snowplow-analytics-debugg/jbnlcgeengmijcghameodeaenefieedm)的[Snowplow Analytics Debugger擴充功能。 此擴充功能會顯示正在收集並傳送至Adobe Commerce的事件。

1. 請務必停用瀏覽器上的任何廣告封鎖程式，並接受網站上的Cookie。

1. 在Chrome中，選擇&#x200B;**自訂及控制Google Chrome** （瀏覽器右上角的三個垂直點），然後選取&#x200B;**更多工具** > **開發人員工具**。

1. 選擇&#x200B;**Snowplow Analytics Debugger**&#x200B;標籤。

1. 在&#x200B;**Event**&#x200B;欄下，選取&#x200B;**結構化事件**。

1. 向下捲動，直到您看到&#x200B;**內容資料&#x200B;_n_**為止。 尋找&#x200B;**結構描述**中的店面執行個體。

1. 確認[SaaS資料空間識別碼](https://experienceleague.adobe.com/docs/commerce-admin/config/services/saas.html)已正確設定。

![雪鏟濾鏡](assets/snowplow-filter.png)
_雪鏟濾鏡_

>[!NOTE]
>
> 偵錯工具中的`Data validity : NOT FOUND`值表示內部結構描述。 Snowplow Chrome外掛程式無法驗證具有內部結構描述的事件。 這對實際功能沒有影響。

## 驗證事件是否正確引發

若要驗證用於量度的事件是否正確引發，請在Snowplow Analytics Debugger中尋找`impression-render`、`view`和`rec-click`事件。 檢視[完整事件清單](https://experienceleague.adobe.com/docs/commerce/product-recommendations/developer/events.html)。

>[!NOTE]
>
> 如果啟用[Cookie限制模式](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html)，Adobe Commerce會在購物者同意前不會收集行為資料。 如果「Cookie限制模式」已停用，系統會依預設收集行為資料。
