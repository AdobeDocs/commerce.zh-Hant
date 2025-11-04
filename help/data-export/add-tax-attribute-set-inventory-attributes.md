---
title: 新增稅捐類別、屬性集及存貨屬性
description: 瞭解如何擴充產品摘要資料，以納入稅捐分類、屬性集及進階庫存設定的屬性
role: Admin, Developer
badgePaas: label="僅限PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/
source-git-commit: dd8f518028c9f2025606e6620fc20156fceac9ce
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---

# 新增稅捐類別、屬性集及存貨屬性

Adobe Commerce額外產品屬性模組可擴充產品資料摘要。 其中包括Adobe Commerce產品設定中的其他產品屬性：

* [稅捐分類](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/stores-sales/site-store/taxes/tax-class)
* [屬性集](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/catalog/product-attributes/create/attribute-sets)
* [詳細目錄](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/inventory/configuration/product-options#advanced-product-options)

安裝後，模組會自動運作。 它會在產品同步期間擷取並匯出其他屬性。 不需要額外設定。

## 主要優點

* **自動增強功能**：使用稅捐類別、屬性集及存貨屬性豐富產品摘要
* **緊密整合**：提供外部系統與服務的基本內容
* **零組態**：安裝後立即運作
* **即時更新**：自動與產品變更同步

## 特徵和匯出的屬性

此模組會新增三個其他屬性至您現有的產品資料摘要：

* `ac_tax_class`
* `ac_attribute_set`
* `ac_inventory`

### 1.稅捐類別資訊(`ac_tax_class`)

**用途**：提供每項產品的稅捐類別資訊

**資料格式**：包含稅捐類別名稱的字串值

**範例輸出**：

```json
{
  "attributes": [
    {
      "code": "ac_tax_class",
      "values": ["Taxable Goods"]
    }
  ]
}
```

**使用案例**：

將稅捐類別資料匯出至Commerce目錄服務時，此資料可用於支援以下用途的應用程式：

* 稅捐規定報表
* 與外部稅捐計算服務整合
* 會計系統的產品分類

### 2.屬性集資訊(`ac_attribute_set`)

**用途**：識別指派給每個產品的屬性集

**資料格式**：包含屬性集名稱的字串值

**範例輸出**：

```json
{
  "attributes": [
    {
      "code": "ac_attribute_set",
      "values": [
        "Default"
      ]
    }
  ]
}
```

**使用案例**：

將屬性集資料匯出至Commerce目錄服務時，該功能會在外部系統中啟用進階產品管理功能。 這些功能包括：

* 產品範本識別
* 目錄管理和組織
* 需要屬性集內容的協力廠商系統整合

### 3.進階清查資料(`ac_inventory`)

**用途**：提供每個產品的詳細目錄管理設定

**資料格式**：包含詳細目錄設定的JSON編碼字串

**包含的欄位**：

* `manageStock` （布林值）：是否啟用庫存管理
* `cartMinQty` （浮動）：購物車允許的最小數量
* `cartMaxQty` （浮動）：購物車允許的最大數量
* `backorders` （字串）：延交原則。 值為下列其中一項：
   * `"no"`：不允許延期交貨
   * `"allow"`：允許數量低於0
   * `"allow_notify"`：允許數量低於0並通知客戶
* `enableQtyIncrements` （布林值）：是否啟用數量增加
* `qtyIncrements` （浮點數）：必要的數量增加值

**範例輸出**：

```json
{
  "attributes": [
    {
      "code": "ac_inventory",
      "values": [
        "{\"manageStock\":true,\"cartMinQty\":2,\"cartMaxQty\":42,\"backorders\":\"no\",\"enableQtyIncrements\":false,\"qtyIncrements\":2}"
      ]
    }
  ]
}
```

**使用案例**：

當您將清查資料匯出至Commerce目錄服務時，它會在外部系統中啟用進階清查管理功能。 這些功能包括：

* Inventory management系統整合
* 購物車驗證規則
* 訂單履行流程最佳化
* 客戶體驗自訂

## 資料匯出摘要增強功能

「額外產品屬性」模組強化了現有的產品摘要。 它會自動整合新的屬性資料。

* **產品摘要** (`products`)：已增強3個額外屬性

   * 將`ac_tax_class`、`ac_attribute_set`和`ac_inventory`屬性新增至每個產品記錄
   * 保持原始產品資料不變
   * 維持與現有摘要使用者的回溯相容性

* **產品屬性摘要** (`productAttributes`)：新屬性的屬性中繼資料已增強

   * 在`productAttributes`摘要中自動註冊三個新屬性的中繼資料
   * 提供屬性組態詳細資訊（資料型別、可見度設定等）
   * 協助外部系統瞭解新的屬性結構

## 安裝擴充功能

**需求**

* PHP 8.1、8.2、8.3或8.4
* Adobe Commerce 2.4.4+
* [Adobe Commerce Data Export擴充功能](manage-extension.md#update-a-module-to-a-specific-version)，103.4.11版或更新版本
* 存取[repo.magento.com](https://repo.magento.com)

  若要產生金鑰並取得必要的許可權，請參閱[取得您的驗證金鑰](https://experienceleague.adobe.com/zh-hant/docs/commerce-operations/installation-guide/prerequisites/authentication-keys)。 如需雲端安裝，請參閱[雲端基礎結構上的Commerce指南](https://experienceleague.adobe.com/zh-hant/docs/commerce-on-cloud/user-guide/develop/authentication-keys)。
* 存取Adobe Commerce應用程式伺服器的命令列。

### 安裝步驟

使用撰寫器新增`adobe-commerce/module-extra-product-attributes`模組：

```shell
composer require adobe-commerce/module-extra-product-attributes
```

如需詳細的安裝步驟，請參閱下列指南：

* 在雲端基礎結構上的Adobe Commerce上[安裝擴充功能](https://experienceleague.adobe.com/zh-hant/docs/commerce-on-cloud/user-guide/configure-store/extensions)
* [安裝擴充功能Adobe Commerce內部部署](https://experienceleague.adobe.com/zh-hant/docs/commerce-operations/installation-guide/tutorials/extensions)

## 同步產品資料

重新部署後，Adobe Commerce執行個體會在產品同步期間自動匯出其他資料。 您也可以使用`resync` CLI命令來立即同步處理。

```shell
# Resync the products feed (includes the new attributes)
bin/magento saas:resync --feed=products
```

```shell
# Resync the product attributes feed (includes new attribute metadata)
bin/magento saas:resync --feed=productAttributes
```

## 疑難排解

**遺失其他屬性的產品：**

* 驗證模組是否已正確安裝及啟用
* 執行resync命令以重新整理產品資料
* 檢查產品是否具有有效的稅捐類別與屬性集指定

**詳細目錄資料顯示不正確：**

* 確認已在Admin中正確設定詳細目錄設定
* 檢查網站特定詳細目錄覆寫
* 驗證[Inventory management模組](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/inventory/guide-overview)是否正常運作

如需詳細資訊，請參閱[Inventory management商家檔案](https://experienceleague.adobe.com/zh-hant/docs/commerce-admin/inventory/guide-overview)中的&#x200B;*Adobe Commerce指南*。

**效能問題：**

* 監視安裝後的匯出程式效能
* 考慮在低流量期間排程重新同步

### 記錄與偵錯

此模組會將匯出錯誤和警告記錄到標準Commerce記錄系統。 如果您在產品同步期間遇到問題，請檢查資料匯出記錄檔。

如需詳細資訊，請參閱[檢閱記錄檔及疑難排解](troubleshooting-logging.md)。

