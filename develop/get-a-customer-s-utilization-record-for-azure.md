---
title: Hämta en kunds användningsposter för Azure
description: Du kan använda Azures användnings-API för att hämta användnings posterna för en kunds Azure-prenumeration under en angiven tids period.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: bcdeb51b04039fd05b923150c85119385c0537e0
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769342"
---
# <a name="get-a-customers-utilization-records-for-azure"></a>Hämta en kunds användningsposter för Azure

**Gäller för:**

- Partnercenter
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Du kan hämta användnings posterna för en kunds Azure-prenumeration under en viss tids period med hjälp av API: et för Azure-användning.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).

- Ett prenumerations-ID.

Det här API: et returnerar en daglig och en Tim Beräknad förbrukning för ett godtyckligt tidsintervall. *Detta API stöds dock inte för Azure-planer*. Om du har en Azure-prenumeration kan du läsa artikeln [få faktura om ej fakturerade förbruknings artiklar](get-invoice-unbilled-consumption-lineitems.md) och [Hämta faktura förbruknings artiklar](get-invoice-billed-consumption-lineitems.md) i stället. I de här artiklarna beskrivs hur du får Beräknad förbrukning på en daglig nivå per mätning per resurs. Den här pris förbrukningen motsvarar den dagliga kornig data som tillhandahålls av Azures användnings-API. Du måste använda faktura identifieraren för att hämta fakturerings användnings data. Eller så kan du använda aktuella och föregående perioder för att få ej fakturerade användnings beräkningar. *Data för varje timmes kornig het och godtyckliga datum intervall filter stöds inte för närvarande för Azure plan-prenumerations resurser*.

## <a name="azure-utilization-api"></a>API för Azure-användning

Detta API för Azure-användning ger till gång till användnings poster för en tids period som representerar när användningen rapporterades i fakturerings systemet. Den ger åtkomst till samma användnings data som används för att skapa och beräkna avstämnings filen. Den har dock inte kunskap om fil logik för fakturerings system. Du bör inte förvänta dig att matcha resultatet från det här API: et för samma tids period.

Till exempel tar fakturerings systemet samma användnings data och tillämpar regler för att fastställa vad som redovisas i en avstämnings fil. När en fakturerings period stängs tas all användning fram till slutet av den dag som fakturerings perioden upphör att ingå i avstämnings filen. All sent användning inom den fakturerings period som rapporteras inom 24 timmar efter fakturerings perioden upphör att gälla i nästa avstämning fil. För reglerna om sena regler för hur partnern faktureras, se [Hämta förbruknings data för en Azure-prenumeration](/previous-versions/azure/reference/mt219001(v=azure.100)).

Den här REST API är växlad. Om nytto lasten för svar är större än en sida måste du följa nästa länk för att få nästa sida med användnings poster.

## <a name="c"></a>C\#

Så här hämtar du Azures användnings poster:

1. Hämta kund-ID och prenumerations-ID.

2. Anropa metoden [**IAzureUtilizationCollection. Query**](/dotnet/api/microsoft.store.partnercenter.utilization.iazureutilizationcollection.query) för att returnera en [**ResourceCollection**](/dotnet/api/microsoft.store.partnercenter.models.resourcecollection-1) som innehåller användnings posterna.

3. Hämta en uppräknare för Azures användnings poster för att passera användnings sidorna. Det här steget är obligatoriskt eftersom resurs samlingen är växlad.

- **Exempel**: [konsol test app](console-test-app.md)
- **Projekt**: SDK-exempel för partner Center
- **Klass**: GetAzureSubscriptionUtilization.CS

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

För att kunna hämta Azures användnings poster behöver du först ett kund-ID och ett prenumerations-ID. Sedan anropar du funktionen **IAzureUtilizationCollection. Query** för att returnera en **ResourceCollection** som innehåller användnings posterna. Eftersom resurs samlingen är växlad måste du hämta en uppräknare för Azures användnings post för att kunna passera användnings sidorna.

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

För att kunna hämta Azures användnings poster behöver du först ett kund-ID och ett prenumerations-ID. Sedan anropar du kommandot [**Get-PartnerCustomerSubscriptionUtilization**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscriptionUtilization.md). Det här kommandot returnerar alla poster som är tillgängliga under den angivna tids perioden.

```powershell
# $customerId
# $subscriptionId

Get-PartnerCustomerSubscriptionUtilization -CustomerId $customerId -SubscriptionId $subscriptionId -StartDate (Get-Date).AddDays(-2).ToUniversalTime() -Granularity Hourly -ShowDetails
```

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod | URI för förfrågan |
|------- | ----------- |
| **TA** | *{baseURL}*/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{Subscription-ID}/utilizations/Azure? Start \_ tid = {start tid} &slut \_ tid = {slut tid} &granularitet = {kornig het} &Visa \_ information = {True} |

#### <a name="uri-parameters"></a>URI-parametrar

Använd följande sökväg och frågeparametrar för att hämta användnings posterna.

| Namn | Typ | Obligatorisk | Beskrivning |
| ---- | ---- | -------- | ----------- |
| kund-ID för klient organisation | sträng | Yes | En GUID-formaterad sträng som identifierar kunden. |
| prenumerations-ID | sträng | Yes | En GUID-formaterad sträng som identifierar prenumerationen. |
| start_time | sträng i UTC-datum-och tids förskjutnings format | Yes | Början av tidsintervallet som representerar när användningen rapporterades i fakturerings systemet. |
| end_time | sträng i UTC-datum-och tids förskjutnings format | Yes | Slutet av tidsintervallet som representerar när användningen rapporterades i fakturerings systemet. |
| kornig het | sträng | No | Definierar kornig het för användnings agg regeringar. Tillgängliga alternativ är: `daily` (standard) och `hourly` .
| show_details | boolean | No | Anger om du vill hämta användnings information på instans nivå. Standardvärdet är `true`. |
| ikoner | antal | No | Anger antalet agg regeringar som returneras av ett enda API-anrop. Standardvärdet är 1000. Max värdet är 1000. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

Inget

### <a name="request-example"></a>Exempel på begäran

Följande exempel förfrågan ger resultat liknande vad som visas i avstämnings filen för perioden 7/2-8/1. De här resultaten matchar kanske inte exakt (se avsnittet [Azures användnings-API](#azure-utilization-api) för mer information).

I den här exempel förfrågan returneras användnings data som rapporter ATS i fakturerings systemet mellan 7/2 kl. 12 (UTC) och 8/2 kl. 12 (UTC).

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

Om det lyckas returnerar den här metoden en samling [Azures användnings post](azure-utilization-record-resources.md) resurser i svars texten. Om Azures användnings data ännu inte är klara i ett beroende system returnerar den här metoden en HTTP-statuskod 204 med ett Retry-After-huvud.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa HTTP-statuskod, [fel kods typ](error-codes.md)och ytterligare parametrar.

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
