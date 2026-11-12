---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%
---
目錄來源代表產品、屬性和類別的權威範圍。 通常會對應至語言、對象或原始系統邊界，並決定搜尋、篩選和排序行為。

## 目錄來源與相關概念

瞭解目錄來源與其他Merchandising Services概念的關聯性，可協助您正確建立資料的模型：

* **目錄來源** — 提供產品資訊的基礎資料內容。 目錄來源通常代表地區設定（例如`en-US`、`fr-CA`）或外部系統（例如PIM或ERP）提供的資料內容。 產品、屬性中繼資料和類別都是依目錄來源設定範圍。 目錄來源會定義原始目錄資料的來源，及其對產品探索（搜尋結果、篩選和排序行為）的影響。

* **[目錄檢視](/help/optimizer/setup/catalog-view.md)** — 針對特定業務需求所設定的目錄檢視。 目錄檢視會選取目錄來源（或地區設定）、套用[原則](/help/optimizer/setup/policies.md)以篩選產品可見度，並將[價格簿](/help/optimizer/setup/pricebooks.md)與檢視建立關聯。 單一目錄來源可以支援許多目錄檢視（例如，一個`en-US`來源具有不同品牌或地區的個別目錄檢視）。 將目錄檢視想像為&#x200B;*如何*&#x200B;將該資料公開至店面、頻道或對象。

* **[目錄層](catalog-layer.md)** — 套用至基本目錄資料之上的層，在不變更來源資料的情況下修改產品屬性（名稱、說明、影像、中繼資料）。 當差異必須僅影響店面顯示時（而非產品探索），請使用目錄層。

## 如何填入目錄來源

目錄來源是透過目錄資料擷取填入。 您提供這些資料的方式取決於您的實作：

- **Adobe Commerce as a Cloud Service與CCDM** — 原生同步處理會從Commerce Foundation提供目錄資料。 在Commerce Foundation中管理基礎產品和存放區檢視組態，並在[資料同步](data-sync.md)工作區中監視同步處理。 不需要個別的資料擷取API整合。
- **具有協力廠商後端的Adobe Commerce Optimizer** — 您的整合會透過[資料擷取API](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/)提供產品和目錄來源資訊。


## 規則和限制

* 當Merchandising Services資料層第一次收到新地區設定或來源系統的目錄資料時，會建立目錄來源。
* 產品唯一性由SKU +目錄來源決定。
* 購物者不會直接存取目錄來源。 目錄資料透過[目錄檢視](catalog-view.md)向店面公開。

## 模型指南

規劃目錄結構時，請遵循下列指引。 針對具有CCDM的Adobe Commerce as a Cloud Service，請管理Commerce Foundation中的基礎設定，而非透過個別的擷取整合建立目錄來源。

* 針對每種目錄語言使用個別的目錄來源。
* 當產品和屬性差異必須影響搜尋、篩選或排序行為（例如不同的可搜尋性或篩選性設定）時，請使用個別的目錄來源。
* 當產品和屬性差異必須影響產品呈現時使用[目錄層](catalog-layer.md)，而不變更搜尋、篩選或排序行為。

>[!MORELIKETHIS]
>
> * [目錄檢視](catalog-view.md) — 在目錄來源之上設定已篩選、已訂價的檢視
> * [目錄層](catalog-layer.md) — 修改產品簡報，而不變更來源資料
> * [原則](policies.md) — 為目錄檢視建立屬性型篩選器
> * [價格簿](/help/optimizer/setup/pricebooks.md) — 管理不同客戶區段的定價結構
> * [受限制的存取金鑰](restricted-access-keys.md) — 使用已簽署的權杖驗證保護目錄檢視
