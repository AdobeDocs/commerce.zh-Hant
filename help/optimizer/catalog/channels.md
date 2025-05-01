---
title: 頻道
description: Learn how to use channels to define your retail structure into meaningful business groups.
hide: true
recommendations: noCatalog
source-git-commit: d716dd9d75beb642bfad30271b6ecd3490ee7328
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# 頻道

>[!NOTE]
>
>本檔案說明提早存取開發中的產品，並未反映所有可供一般使用的功能。

管道可協助您將零售結構定義成有意義的業務群組。 A channel affects product visibility by applying specific policies and filters that determine which products are displayed on a storefront. These policies can include attributes like brand, model, or part category, ensuring that only relevant products are visible to shoppers based on the channel configuration. Additionally, channels can use price books to display customer-specific pricing, further tailoring the shopping experience.

## Add channel

In this section, you create a channel. Ensure that you have already [created a policy](./policies.md) before proceeding to create a channel.

1. On the left menu, open the **[!UICONTROL Catalog]** section and click **[!UICONTROL Channels]**.

![管道](../assets/channels.png)

1. Click **[!UICONTROL Add Channel]**. &#x200B;

1. On the Add channel to listing form, fill in the channel details:

   * **Name**—Enter the name of the channel. For example, &quot;Celport&quot;. &#x200B;
   * **領域** — 新增領域（地區設定）。 例如，「en-US」。 Press the **enter** key.
   * **Policies**—Use the drop-down to select the relevant policies. For example, &quot;Brand,&quot; &quot;Model&quot;. &#x200B;Make sure you have already [created a policy](./policies.md).

1. Click **[!UICONTROL Add]** to create the channel. &#x200B;

   If the **[!UICONTROL Add]** button is not active, ensure that the scope is properly added by placing your cursor in the Scopes field and  pressing **enter**. &#x200B;

The Channels page updates to display the new channel.&#x200B;

![Updated Channels Page](../assets/updated-channels-list.png)

After you complete these steps, the new channel is configured to display products and pricing based on the scopes and policies you selected.
