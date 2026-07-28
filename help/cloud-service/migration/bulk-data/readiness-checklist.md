---
title: 客戶整備檢查清單
description: 瞭解如何透過整備檢查清單（涵蓋參與、機器、來源和目標），準備將大量資料移轉至Adobe Commerce as a Cloud Service。
feature: Cloud
badgeSaas: label="僅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hant/docs/commerce/user-guides/product-solutions" tooltip="僅適用於Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer專案（Adobe管理的SaaS基礎結構）。"
role: Developer
level: Intermediate
autotag-review: '2026-07-22T19:19:18.443Z'
TQID: 'https://experienceleague.adobe.com/728hkK-dzIPzyuBhuNyOqEE9FxlVGdVc9R2wIRcXobk'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
subfeature_v2:
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 670b6214b28be93a16130552a226a8cadb487324
workflow-type: tm+mt
source-wordcount: 1171
ht-degree: 0%

---

# 客戶整備檢查清單

{{bulk-data-early-access}}

使用此檢查清單以準備使用大量資料移轉工具從[!DNL Adobe Commerce on Cloud]或內部部署執行個體移轉到[!DNL Adobe Commerce as a Cloud Service]的資料。

移轉工具會作為Commerce部署工程(CDE)參與流程的一部分發佈。 工具的存取權在已簽署的CDE合約上受限，且無法公開使用。

此檢查清單涵蓋共用工具之前需要準備的專案（[階段1](#stage-1-before-tool-access)），以及準備在擁有工具之後開始設定和執行所需的專案（[階段2](#stage-2-before-running-the-migration)）。 請及早與您的Adobe團隊檢閱此檢查清單，因為有些專案需要Adobe協調。

## 階段1：工具存取前

提供移轉工具和檔案之前，請先完成或確認下列專案。

- **CDE參與** — 已簽署的Commerce部署工程合約必須準備就緒。 工具存取權在CDE生命週期的交易簽署階段授予。 與您的Adobe團隊協調。
- **範圍設定問卷已完成** — 範圍設定問卷已在CDE Discovery期間完成，以驗證使用目前工具功能進行移轉是否可行，並評估資料足跡和複雜性。 在繼續之前，請確定您已與您的Adobe團隊完成此步驟。
- **未確認HIPAA資料** — 來源執行個體不得包含HIPAA規範的資料。 請確認此專案後再繼續。
- **提供的IP位址** — 為您的Adobe團隊提供移轉工具執行來源的靜態IP位址清單。 這是在Adobe端設定網路存取的必要條件。
- **已布建目標執行個體** — 必須在開始移轉前布建目標[!DNL Adobe Commerce as a Cloud Service]執行個體。 與您的Adobe團隊協調，確認執行個體已就緒。

## 階段2：執行移轉之前

存取工具後，請先準備好下列專案，再開始設定和執行。

### 移轉電腦

移轉工具在您控制的機器上執行，例如專用的跳轉方塊。 此電腦必須符合下列需求。

- 已安裝&#x200B;**[!DNL Docker]及[!DNL Docker Compose]** — 工具是以[!DNL Docker]為基礎。 必須同時安裝`docker`和`docker compose` （或舊版`docker-compose`）並在移轉機器上運作。
- **[!DNL Docker]執行許可權** — 執行移轉的使用者必須被允許執行[!DNL Docker]命令。 在[!DNL Linux]，使用者必須屬於`docker`群組。 在[!DNL macOS]和[!DNL Windows]上，[!DNL Docker Desktop]必須正在執行且可存取。
- **可寫入的工作目錄** — 移轉使用者必須完全可寫入擷取移轉工具的目錄。 工具會在執行期間寫入記錄、快取、[!DNL Composer]相依性和產生的檔案。
- **足夠的磁碟空間** — 確保有足夠的可用磁碟空間供擷取的資料、[!DNL Docker]影像和記錄檔輸出使用。 空間需求會依來源資料庫的大小而有所不同。
- **內部部署來源：從移轉機器直接的資料庫連線** — 對於內部部署來源執行個體，移轉機器必須擁有來源資料庫的直接網路存取權。 此工具不會自動建立內部部署資料庫連線。 在執行任何移轉命令之前，請確認可從移轉機器存取主機、連線埠和認證。
- 已安裝&#x200B;**雲端CLI且已登入SSH金鑰** — 對於[!DNL Adobe Commerce on Cloud]來源執行個體，[雲端CLI](https://experienceleague.adobe.com/zh-hant/docs/commerce-on-cloud/user-guide/dev-tools/cloud-cli/cloud-cli-overview)必須安裝在移轉機器上。 您的SSH公開金鑰也必須在帳戶中註冊。 如需指示，請參閱[安全連線指南](https://experienceleague.adobe.com/zh-hant/docs/commerce-on-cloud/user-guide/develop/secure-connections)。

### Source執行個體

- **可存取的Source存放區API** — 來源存放區的REST和GraphQL API必須可從移轉機器存取。 請確定沒有任何HTTP基本驗證或網路限制會封鎖來源URL的API流量。
- **Source OAuth認證** — 移轉工具會使用OAuth驗證來源存放區。 在來源&#x200B;[!UICONTROL **管理員**] （[!UICONTROL **系統**] > [!UICONTROL **擴充功能**] > [!UICONTROL Integrations]）中建立或確認整合，並準備好消費者金鑰、消費者密碼、存取權杖和存取權杖密碼。
- **PaaS來源： Magento Cloud API Token** — 從&#x200B;[!UICONTROL **帳戶設定**] > [!UICONTROL **API Token**]&#x200B;下的[Cloud帳戶設定](https://accounts.magento.cloud)產生[!DNL Cloud]個API Token。 只有在來源是[!DNL Adobe Commerce on Cloud]執行個體時才需要。
- **Source資料庫認證** — （僅限內部部署）讓來源[!DNL MySQL]資料庫連線詳細資料準備好進行設定： `host`、`port`、`user`、`password`以及`database`名稱。
- **暫停cron**&#x200B;的功能 — 您必須能夠在資料擷取期間停止來源執行個體上的cron，以防止同時寫入。
- **暫停整合與背景工作的功能** — 任何協力廠商整合(ERP、OMS、PIM)、排程工作，或寫入來源資料庫的背景處理作業，都必須暫停擷取視窗。
- **啟用和停用維護模式的功能** — （僅階段移轉）如果您使用維護時段執行階段式移轉，則必須在來源執行個體上啟用和停用維護模式。

### 目標執行個體

- **租使用者ID與組織ID已確認** — 設定前，請先從您的Adobe團隊取得您的`TARGET_TENANT_ID`與`TARGET_ORG_ID`。
- **IMS OAuth伺服器對伺服器認證** — 移轉工具驗證目標時需要。 透過[Adobe Developer Console](https://developer.adobe.com/console/)產生。 您需要[!UICONTROL Developer]或[!UICONTROL Admin]存取權才能存取您的Adobe組織，因為基本使用者存取權不足以建立認證。 與您的Adobe團隊協調以選取正確的產品設定檔，並準備好使用者端識別碼(`ADOBE_IMS_CLIENT_ID`)和使用者端密碼(`ADOBE_IMS_CLIENT_SECRET`)。
- **CDMS端點URL** — 由您的Adobe團隊提供。 請勿嘗試推斷此值。 您同時需要沙箱和測試移轉的生產前端點，以及即時直接轉換移轉的生產端點。
- **來源與目標對齊的核心組態** — 工具不會移轉核心組態資料，例如存放區設定和系統組態。 請在移轉前在目標上手動設定以符合來源。
- **B2B存放區：已一致設定B2B功能** — 如果來源是啟用B2B的存放區，請在移轉之前，確定來源和目標上的相關B2B [!UICONTROL Admin]設定已一致設定。 請參閱[移轉指南](migration-guide.md)，瞭解所需的特定設定。

### 移轉規劃

- **移轉方法已決定** — 在開始之前，請先決定適合您使用案例的方法。
  - 單階段移轉 — 不需要維護模式。 適合旱跑、開發或沙箱環境，或任何移轉，在擷取期間來源可以保持即時。
  - 多階段移轉 — 需要維護模式。 生產移轉需要多階段移轉，其中來源必須在擷取期間凍結以確保資料一致性。
- **已規劃的維護期間** — 僅適用於多階段移轉。 事先規劃並傳達維護時段。 在擷取和載入階段的期間，一般使用者無法使用來源例項。
- **已確認存放區檢視代碼** — 識別來源執行個體上的存放區檢視代碼(`STORE_CODE`)。 預設為`default`，但必須符合[!UICONTROL Admin] > [!UICONTROL Stores] > [!UICONTROL All Stores]中的實際代碼。 不正確的存放區代碼可能會影響移轉期間的資料作業。

確認所有專案後，您就可以使用[移轉服務存取指南](cdms-access.md)來驗證服務存取權，然後在[移轉指南](migration-guide.md)中開始設定和執行步驟。
