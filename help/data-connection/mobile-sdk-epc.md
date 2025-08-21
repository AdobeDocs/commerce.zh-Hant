---
title: 將Adobe Experience Platform Mobile SDK與Commerce整合
description: 瞭解如何搭配無周邊或自訂Adobe Experience Platform店面使用Commerce行動SDK。
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: 02d07abb-8d7f-4f0a-9f96-f42654cd79d3
source-git-commit: a3e19940e2a3d8a240bb17703cfdd9903df311aa
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# 將Adobe Experience Platform Mobile SDK與Commerce整合

>[!IMPORTANT]
>
>適用於iOS的Adobe Experience Platform Mobile SDK支援iOS 11或更新版本。

將[Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/home/)與Commerce行動應用程式整合後，商戶可將Commerce [事件資料](events.md)傳送至Experience Platform Edge。

當Commerce事件資料位於邊緣時，其他Adobe Experience Cloud應用程式即可存取這些資料。 例如，您可以使用資料在Real-Time CDP中建立對象，然後[使用這些對象](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html)個人化您的Commerce行動應用程式。

## 設定

若要開始將Adobe Experience Platform Mobile SDK與Commerce搭配使用，請在Experience Platform中安裝和設定SDK。 接著，在Commerce中完成設定。

### Experience Platform

1. 檢閱行動應用程式教學課程[中的](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/overview.html)Adobe Experience Cloud，瞭解行動應用程式功能。

1. [在Experience Platform中安裝和設定](https://developer.adobe.com/client-sdks/documentation/getting-started/) SDK。

   >[!NOTE]
   >
   >您在Experience Platform中建立和設定的結構描述，與您在Commerce行動應用程式中的應用程式程式碼中使用的結構描述相同。

### Commerce

完成Experience Platform的SDK設定後，請將SDK設定新增至Commerce。

1. 若要透過SDK將Commerce事件資料傳送至Experience Platform，您必須在應用程式程式碼中提供XDM結構描述。 此結構描述必須符合Experience Platform中為SDK設定的結構描述[&#128279;](https://developer.adobe.com/client-sdks/home/getting-started/set-up-schemas-and-datasets/)。

   下列範例說明如何使用電子郵件欄位來追蹤`web.webpagedetails.pageViews`事件及設定`identityMap`。

   ```swift
   let stateName = "luma: content: ios: us: en: home"
   var xdmData: [String: Any] = [
       "eventType": "web.webpagedetails.pageViews",
       "web": [
           "webPageDetails": [
               "pageViews": [
                   "value": 1
               ],
               "name": "Home page"
           ]
       ]
   ]
   
   let experienceEvent = ExperienceEvent(xdm: xdmData)
   Edge.sendEvent(experienceEvent: experienceEvent)
   
   // Adobe Experience Platform - Update Identity
   
   let emailLabel = "mobileuser@example.com"
   
   let identityMap: IdentityMap = IdentityMap()
   identityMap.add(item: IdentityItem(id: emailLabel), withNamespace: "Email")
   Identity.updateIdentities(with: identityMap)
   ```

1. 連線至Commerce Cloud環境。

   在您的專案建置設定中，新增URL至Commerce GraphQL端點。 例如：

   - 偵錯： http://_debug_.commercesite.cloud/graphql/
   - 發行版本： http://_release_.commercesite.cloud/graphql/

1. 若要從Commerce GraphQL端點擷取資料，請先使用[Apollo Code Generator](https://www.apollographql.com/docs/ios/)在您的專案中產生必要的檔案和目錄。

   1. 從您的專案目錄，[安裝](https://www.apollographql.com/docs/ios/get-started#1-install-the-apollo-frameworks) Apollo iOS。

   1. [初始化](https://www.apollographql.com/docs/ios/code-generation/codegen-cli/#initialize) Apollo Codegen CLI。

      這會建立`apollo-codegen-configuration.json`檔案。

   1. 將`apollo-codegen-configuration.json`檔案的內容取代為下列內容，以在專案中產生必要的GraphQL檔案和目錄：

      ```json
      {
      "schemaName" : "MagentoAPI",
      "input" : {
          "operationSearchPaths" : [
          "**/*.graphql"
          ],
          "schemaSearchPaths" : [
          "**/*.graphqls"
          ]
      },
      "output" : {
          "testMocks" : {
          "none" : {
          }
          },
          "schemaTypes" : {
          "path" : "../MagentoAPI",
          "moduleType" : {
              "swiftPackageManager" : {
              }
          }
          },
          "operations" : {
          "inSchemaModule" : {
          }
          }
      },
      "schemaDownloadConfiguration": {
          "downloadMethod": {
              "introspection": {
                  "endpointURL": "http://magento24.com/graphql/",
                  "httpMethod": {
                      "POST": {}
                  },
                  "includeDeprecatedInputValues": false,
                  "outputFormat": "SDL"
              }
          },
          "downloadTimeout": 60,
          "headers": [],
          "outputPath": "magento.graphqls"
      }
      }
      ```

   1. [擷取](https://www.apollographql.com/docs/ios/code-generation/codegen-cli/#fetch-schema) Commerce GraphQL結構描述。

      確保路徑為`./apollo-codegen-config.json`檔案，其中包含對Commerce GraphQL結構描述的參考。

   1. [產生](https://www.apollographql.com/docs/ios/code-generation/codegen-cli/#generate)原始程式碼。

      確定路徑為`./apollo-codegen-config.json`檔案，其中包含產生必要檔案和目錄的組態資訊。

   1. 在新建立的&#x200B;**GraphQLGenerated**&#x200B;資料夾中，新增或編輯GraphQL型別。 例如，您可以新增具有以下內容的`DynamicBlocks.graphql`型別：

      ```graphql
      query dynamicBlocks($input: DynamicBlocksFilterInput){
          dynamicBlocks(input: $input)
          {
              items {
                  content {
                      html
                  }
              }
          }
      }
      ```

   您現在已將Adobe Experience Platform Mobile SDK與Commerce行動應用程式整合。 事件資料會從您的應用程式傳輸至Experience Platform Edge。

## 如何區分從行動應用程式產生的Commerce事件

所有[事件](events.md)都包含名為`channel`的欄位。 `channel`欄位包含`channel._id`和`channel._type`，Luma店面的名稱空間值分別為`"https://ns.adobe.com/xdm/channels/web"`和`"https://ns.adobe.com/xdm/channel-types/web"`。 但對於行動店面，名稱空間值分別為`"https://ns.adobe.com/xdm/channels/mobile-app"`和`"https://ns.adobe.com/xdm/channel-types/mobile"`。

## 後續步驟

若要瞭解如何從您的行動Real-Time CDP應用程式擷取Commerce對象，以告知購物車價格規則、動態區塊和相關產品規則，請參閱[Audience Activation](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html#retrieve-audiences-using-the-adobe-experience-platform-mobile-sdk)。
