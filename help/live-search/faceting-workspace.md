---
title: 多面向Workspace
description: 瞭解如何在 [!DNL Live Search] 多面向工作區中運作。
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# 多面向Workspace

*多面向*&#x200B;工作區會列出目前可用的所有Facet，並提供您設定和管理Facet所需工具的存取權。 釘選多面會先出現在現有多面的清單中，然後是動態多面。 您可以篩選清單以顯示所有多面，或僅顯示已釘選或動態的多面。

![多面向工作區](assets/faceting-workspace.png)

## 設定範圍

如果您的Adobe Commerce安裝包含多個存放區檢視，請將&#x200B;**範圍**&#x200B;設定為您的Facet設定套用的[存放區檢視](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html#scope-settings)。

## 篩選清單

1. 按一下&#x200B;**篩選依據**&#x200B;控制項。
1. 選擇下列其中一個選項：

   * 所有篩選器
   * 已固定
   * 動態

## 新增面向

1. 按一下&#x200B;**新增Facet**。
1. 如需詳細指示，請參閱[新增Facet](facets-add.md)。

## 欄說明

| 欄 | 說明 |
|--- |--- |
| （第一欄） | 列出購物者可見的[標籤](facets-type.md)釘選和動態Facet。 |
| 排序型別 | 多面向值的[排序順序](facets-type.md)。 所有[!DNL Commerce]個店面的Facet都是依字母順序排序。 對於[headless]實作，Facet可以依字母順序或計數排序。 選項：字母順序、計數（僅限Headless） |
| 最大值 | 店面中作為篩選器可用的多面值數量（最多10個）。 |

## 控制項

| 控制 | 說明 |
|--- |--- |
| 新增多面向 | 開啟[面向編輯器](facets-add.md)。 |
| 篩選依據 | 決定出現在清單中的Facet[&#128279;](facets-type.md)的型別。 選項：全部、固定、動態 |
