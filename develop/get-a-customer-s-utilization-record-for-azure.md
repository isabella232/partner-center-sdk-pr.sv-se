---
title: Hämta en kunds användningsposter för Azure
description: Du kan använda API:et för Azure-användning för att hämta användningsposter för en kunds Azure-prenumeration under en angiven tidsperiod.
ms.date: 04/19/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 23c8d18462081c6d6c95c1d969f269cbb3f8754b
ms.sourcegitcommit: abefe11421edc421491f14b257b2408b4f29b669
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/20/2021
ms.locfileid: "107745600"
---
# <a name="get-a-customers-utilization-records-for-azure"></a>Hämta en kunds användningsposter för Azure

**Gäller för:**

- Partnercenter
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Du kan hämta användningsposter för en kunds Azure-prenumeration under en angiven tidsperiod med hjälp av API:et för Azure-användning.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app och autentiseringsuppgifter för App+Användare.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard) Välj **CSP** på Menyn i Partnercenter följt av **Kunder**. Välj kunden i kundlistan och välj sedan **Konto.** På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.** Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).

- En prenumerationsidentifierare.

Det här API:et returnerar förbrukningen per dag och timme för ett godtyckligt tidsintervall. Det här *API:et stöds dock inte för Azure-planer.* Om du har en Azure-plan kan du läsa artiklarna Get [invoice un-billed consumption line items](get-invoice-unbilled-consumption-lineitems.md) (Hämta faktura, ej fakturerade förbrukningsradsobjekt) och Get invoice billed consumption line items instead (Hämta faktura [fakturerade förbrukningsradobjekt i](get-invoice-billed-consumption-lineitems.md) stället). De här artiklarna beskriver hur du hämtar klassificerad förbrukning på en daglig nivå per mätare per resurs. Den här förbrukningen motsvarar dagliga kornighetsdata som tillhandahålls av API:et för Azure-användning. Du måste använda fakturaidentifieraren för att hämta fakturerade användningsdata. Eller så kan du använda aktuella och tidigare perioder för att få ofakturerade användningsuppskattningar. *Filter för intervall per timme och godtyckliga datumintervall stöds för närvarande inte för Prenumerationsresurser för Azure-plan.*

## <a name="azure-utilization-api"></a>API för Azure-användning

Det här API:et för Azure-användning ger åtkomst till användningsposter för en tidsperiod som representerar när användningen rapporterades i faktureringssystemet. Den ger åtkomst till samma användningsdata som används för att skapa och beräkna avstämningsfilen. Den har dock ingen kunskap om logik för faktureringssystemavstämningsfiler. Du bör inte förvänta dig att sammanfattningsresultaten för avstämningsfilen matchar resultatet som hämtats från det här API:et exakt under samma tidsperiod.

Faktureringssystemet använder till exempel samma användningsdata och tillämpar regler för lateness för att fastställa vad som redovisas i en avstämningsfil. När en faktureringsperiod stängs tas all användning fram till slutet av dagen som faktureringsperioden slutar med i avstämningsfilen. Sen användning inom faktureringsperioden som rapporteras inom 24 timmar efter faktureringsperiodens slut redovisas i nästa avstämningsfil. Information om lateness-regler för hur partnern faktureras finns i [Hämta förbrukningsdata för en Azure-prenumeration.](/previous-versions/azure/reference/mt219001(v=azure.100))

Den REST API är sidindelade. Om svarsnyttolasten är större än en enda sida måste du följa nästa länk för att hämta nästa sida med användningsposter.

### <a name="scenario--partner-a-has-transferred-billing-ownership-of-azure-legacy-subscription-145p-to-partner-b"></a>Scenario: Partner A har överfört faktureringsägarskapet för den äldre Azure-prenumerationen (145P) till Partner B

Om en partner överför faktureringsägarskapet för en äldre Azure-prenumeration till en annan partner måste den nya partnern, när den nya partnern anropar användnings-API:et för den överförda prenumerationen, använda handelsprenumerationens ID (som visas i partnercenterkontot) i stället för Azure-berättigande-ID:t. Azure-berättigande-ID visas endast för Partner B när de är administratör för (AOBO) till kundens Azure Portal. 

För att kunna anropa API:et för utnyttjande för den överförda prenumerationen måste den nya partnern använda handelsprenumerationens ID.

## <a name="c"></a>C\#

Så här hämtar du Azure-användningsposterna:

1. Hämta kund-ID och prenumerations-ID.

2. Anropa metoden [**IAzureUtilizationCollection.Query**](/dotnet/api/microsoft.store.partnercenter.utilization.iazureutilizationcollection.query) för att returnera [**en ResourceCollection**](/dotnet/api/microsoft.store.partnercenter.models.resourcecollection-1) som innehåller användningsposterna.

3. Hämta en uppräkning av Azure-användningsposten för att bläddra bland användningssidorna. Det här steget krävs eftersom resurssamlingen är sidindelade.

- **Exempel:** [Konsoltestapp](console-test-app.md)
- **Projekt:** Partnercenter-SDK exempel
- **Klass:** GetAzureSubscriptionUtilization.cs

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

IPartner partner = PartnerService.Instance.CreatePartnerOperations(credentials);

// Retrieve the utilization records for the last year in pages of 100 records.
var utilizationRecords = partner.Customers[customerId].Subscriptions[subscriptionId].Utilization.Azure.Query(
    DateTimeOffset.Now.AddYears(-1),
    DateTimeOffset.Now,
    size: 100);

// Create an Azure utilization enumerator which will aid us in traversing the utilization pages.
var utilizationRecordEnumerator = partner.Enumerators.Utilization.Azure.Create(utilizationRecords);

while (utilizationRecordEnumerator.HasValue)
{
    //
    // Insert code here to work with this page.
    //

    // Get the next page.
    utilizationRecordEnumerator.Next();
}
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

För att hämta Azure-användningsposterna behöver du först en kundidentifierare och en prenumerationsidentifierare. Sedan anropar du **funktionen IAzureUtilizationCollection.query** för att returnera **en ResourceCollection** som innehåller användningsposterna. Eftersom resurssamlingen är sidindelade måste du sedan hämta en uppräkning av Azure-användningsposten för att gå igenom användningssidorna.

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String subscriptionId;

ResourceCollection<AzureUtilizationRecord> utilizationRecords = partnerOperations.getCustomers()
  .byId(customerId).getSubscriptions().byId(subscriptionId)
  .getUtilization().getAzure().query(
      new DateTime().minusYears(1),
      new DateTime(),
      AzureUtilizationGranularity.Daily,
      true,
      100);

// Create an Azure utilization enumerator which will aid us in traversing the utilization pages
IResourceCollectionEnumerator<ResourceCollection<AzureUtilizationRecord>> utilizationRecordEnumerator =
    partnerOperations.getEnumerators().getUtilization().getAzure().create(utilizationRecords);

while (utilizationRecordEnumerator.hasValue())
{
    //
    // Insert code here to work with this page.
    //

    // get the next page
    utilizationRecordEnumerator.next();
}
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

För att kunna hämta Azure-användningsposterna behöver du först en kundidentifierare och en prenumerationsidentifierare. Sedan anropar du [**Get-PartnerCustomerSubscriptionUtilization**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscriptionUtilization.md). Det här kommandot returnerar alla poster som är tillgängliga under den angivna tidsperioden.

```powershell
# $customerId
# $subscriptionId

Get-PartnerCustomerSubscriptionUtilization -CustomerId $customerId -SubscriptionId $subscriptionId -StartDate (Get-Date).AddDays(-2).ToUniversalTime() -Granularity Hourly -ShowDetails
```

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod | URI för förfrågan |
|------- | ----------- |
| **Få** | *{baseURL}*/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/utilizations/azure?start \_ time={start-time}&end \_ time={end-time}&granularity={granularity}&show \_ details={True} |

#### <a name="uri-parameters"></a>URI-parametrar

Använd följande sökväg och frågeparametrar för att hämta användningsposterna.

| Namn | Typ | Obligatorisk | Beskrivning |
| ---- | ---- | -------- | ----------- |
| kund-klient-id | sträng | Yes | En GUID-formaterad sträng som identifierar kunden. |
| prenumerations-id | sträng | Yes | En GUID-formaterad sträng som identifierar prenumerationen. |
| start_time | sträng i UTC-format för datum/tid-förskjutning | Yes | Starttidsintervallet som representerar när användningen rapporterades i faktureringssystemet. |
| end_time | sträng i UTC-format för datum/tid-förskjutning | Yes | Slutet på det tidsperiod som representerar när användningen rapporterades i faktureringssystemet. |
| Granularitet | sträng | No | Definierar kornigheten för användningsaggregeringar. Tillgängliga alternativ är: `daily` (standard) och `hourly` .
| show_details | boolean | No | Anger om du vill hämta användningsinformation på instansnivå. Standardvärdet är `true`. |
| ikoner | antal | No | Anger antalet aggregeringar som returneras av ett enda API-anrop. Standardvärdet är 1000. Max är 1 000. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

Inget

### <a name="request-example"></a>Exempel på begäran

Följande exempelbegäran ger resultat som liknar det som avstämningsfilen visar för perioden 7/2–8/1. Dessa resultat kanske inte matchar exakt (mer information finns i [avsnittet API för Azure-användning).](#azure-utilization-api)

Den här exempelbegäran returnerar användningsdata som rapporteras i faktureringssystemet mellan 7/2 kl. 12:00 (UTC) och 8/2 kl. 12:00 (UTC).

```http
GET https://api.partnercenter.microsoft.com/v1/customers/E499C962-9218-4DBA-8B83-8ADC94F47B9F/subscriptions/FC8F8908-F918-4406-AF13-D5BC0FE41865/utilizations/azure?start_time=2017-07-02T00:00:00-08:00&end_time=2017-08-02T00:00:00-08:00 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden en samling [Azure Utilization Record-resurser](azure-utilization-record-resources.md) i svarstexten. Om Azure-användningsdata ännu inte är redo i ett beroende system returnerar den här metoden HTTP-statuskod 204 med Retry-After sidhuvud.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa HTTP-statuskoden, [felkodstypen](error-codes.md)och ytterligare parametrar.

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Length: 2630
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CV: PjuGoYrw806o6A3Y.0
MS-ServerId: 030020525
Date: Fri, 04 Aug 2017 23:48:28 GMT

{
  "totalCount": 2,
  "items": [
    {
      "usageStartTime": "2017-06-07T17:00:00-07:00",
      "usageEndTime": "2017-06-08T17:00:00-07:00",
      "resource": {
        "id": "8767aeb3-6909-4db2-9927-3f51e9a9085e",
        "name": "Storage Admin",
        "category": "Storage",
        "subcategory": "Block Blob",
        "region": "Azure Stack"
      },
      "quantity": 0.217790327034891,
      "unit": "1 GB/Hr",
      "infoFields": {},
      "instanceData": {
        "resourceUri": "/subscriptions/ab7e2384-eeee-489a-a14f-1eb41ddd261d/resourcegroups/system.local/providers/Microsoft.Storage/storageaccounts/srphealthaccount",
        "location": "azurestack",
        "partNumber": "",
        "orderNumber": "",
        "additionalInfo": {
          "azureStack.MeterId": "09F8879E-87E9-4305-A572-4B7BE209F857",
          "azureStack.SubscriptionId": "dbd1aa30-e40d-4436-b465-3a8bc11df027",
          "azureStack.Location": "local",
          "azureStack.EventDateTime": "06/05/2017 06:00:00"
        }
      },
      "attributes": {
        "objectType": "AzureUtilizationRecord"
      }
    },
    {
      "usageStartTime": "2017-06-07T17:00:00-07:00",
      "usageEndTime": "2017-06-08T17:00:00-07:00",
      "resource": {
        "id": "8767aeb3-6909-4db2-9927-3f51e9a9085e",
        "name": "Storage Admin",
        "category": "Storage",
        "subcategory": "Block Blob",
        "region": "Azure Stack"
      },
      "quantity": 0.217790327034891,
      "unit": "1 GB/Hr",
      "infoFields": {},
      "instanceData": {
        "resourceUri": "/subscriptions/ab7e2384-eeee-489a-a14f-1eb41ddd261d/resourcegroups/system.local/providers/Microsoft.Storage/storageaccounts/srphealthaccount",
        "location": "azurestack",
        "partNumber": "",
        "orderNumber": "",
        "additionalInfo": {
          "azureStack.MeterId": "09F8879E-87E9-4305-A572-4B7BE209F857",
          "azureStack.SubscriptionId": "dbd1aa30-e40d-4436-b465-3a8bc11df027",
          "azureStack.Location": "local",
          "azureStack.EventDateTime": "06/05/2017 06:00:00"
        },
        "attributes": {
          "objectType": "AzureUtilizationRecord"
        }
      },

      "links": {
        "self": {
          "uri": "customers/E499C962-9218-4DBA-8B83-8ADC94F47B9F/subscriptions/FC8F8908-F918-4406-AF13-D5BC0FE41865/utilizations/azure?start_time=2017-06-10T00:00:00Z&end_time=2017-07-09T00:00:00Z&granularity=Daily&show_details=True&size=1000",
          "method": "GET",
          "headers": []
        }
      },
      "attributes": {
        "objectType": "Collection"
      }
    }
  ]
}
```
