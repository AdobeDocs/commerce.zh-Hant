---
title: 目錄來源
description: 瞭解什麼是目錄來源，以及它們如何定義搜尋、篩選和排序行為的產品、屬性和類別的權威範圍。
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和 [!DNL Adobe Commerce Optimizer] 專案（Adobe管理的SaaS基礎結構）。"
source-git-commit: dc50e4d7bcd118b2b9a800779c600ade5560e0bf
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---


# 目錄來源

目錄來源代表產品、屬性和類別的權威範圍。 目錄來源通常會對應至語言、對象或原始系統邊界，並決定搜尋、篩選和排序行為。

## 目錄來源與相關概念

瞭解目錄來源與其他[!DNL Adobe Commerce Optimizer]概念的相關性，可協助您正確建立資料的模型：

* **目錄來源** — 提供產品資訊的基礎資料內容。 目錄來源通常是地區設定（例如，`en-US`、`fr-CA`）或外部系統，例如PIM或ERP。 產品、屬性中繼資料和類別都是依目錄來源設定範圍。 將目錄來源想像為&#x200B;*其中*&#x200B;原始目錄資料來自，以及&#x200B;*它如何影響產品探索（搜尋結果、篩選和排序行為）*。

* **[目錄檢視](catalog-view.md)** — 針對特定業務需求所設定的目錄檢視。 當您建立目錄檢視時，請選取要使用的目錄來源（或地區設定），然後新增[原則](policies.md)以篩選可見的產品，並連結[價格手冊](pricebooks.md)以控制定價。 單一目錄來源可以支援許多目錄檢視（例如，一個`en-US`來源具有不同品牌或地區的個別目錄檢視）。 將目錄檢視想像為&#x200B;*如何*&#x200B;將該資料公開至店面、頻道或對象。

* **[目錄層](catalog-layer.md)** — 套用至基本目錄資料之上的層，在不變更來源資料的情況下修改產品屬性（名稱、說明、影像、中繼資料）。 當差異必須僅影響店面顯示時（而非產品探索），請使用目錄層。

## 規則和限制

* 目錄來源是透過資料擷取API擷取產品所建立。 如需詳細資訊，請參閱[開發人員檔案 — 資料擷取](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/)。
* 產品唯一性由SKU +目錄來源決定。
* 購物者不會直接存取目錄來源。 目錄資料透過[目錄檢視](catalog-view.md)向店面公開。

## 模型指南

在決定如何建構目錄來源時，請使用下列指引：

* 針對不同的目錄語言建立個別的目錄來源。
* 當產品和屬性的差異必須影響搜尋、篩選或排序行為時（例如，同一屬性的不同可搜尋性、可篩選性或Facet設定），請使用個別的目錄來源。
* 當產品和屬性差異必須只影響店面顯示，而不影響產品探索時，請使用[目錄層](catalog-layer.md)。

>[!MORELIKETHIS]
>
> * [目錄檢視](catalog-view.md) — 在目錄來源之上設定已篩選、已訂價的檢視
> * [目錄層](catalog-layer.md) — 修改產品簡報，而不變更來源資料
> * [原則](policies.md) — 為目錄檢視建立屬性型篩選器
> * [價格簿](pricebooks.md) — 管理不同客戶區段的定價結構
