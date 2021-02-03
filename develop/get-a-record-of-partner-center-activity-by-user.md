---
title: Hämta en post för Partnercenter-aktivitet
description: Hur du hämtar en post med åtgärder, som utförs av en partner användare eller ett program, under en viss tids period.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2f37eae8bb96c1c1e7008e8c566b085e25d8807d
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769531"
---
# <a name="get-a-record-of-partner-center-activity"></a>Hämta en post för Partnercenter-aktivitet

**Gäller för**

- Partnercenter
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Den här artikeln beskriver hur du hämtar en post med åtgärder som utfördes av en partner användare eller ett program under en viss tids period.

Använd detta API för att hämta gransknings poster för de senaste 30 dagarna från det aktuella datumet eller för ett datum intervall som anges genom att inkludera start datum och/eller slutdatum. Observera dock att data tillgänglighet för aktivitets loggen för prestanda orsaker är begränsad till föregående 90 dagar. Begär Anden med ett start datum som är större än 90 dagar före det aktuella datumet får ett felaktigt undantag för begäran (felkod: 400) och ett lämpligt meddelande.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.

## <a name="c"></a>C\#

Om du vill hämta en post över partner Center-åtgärder måste du först fastställa datum intervallet för de poster som du vill hämta. I följande kod exempel används endast start datum, men du kan även inkludera ett slutdatum. Mer information finns i [**fråge**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) metoden. Skapa sedan de variabler du behöver för den typ av filter som du vill använda och tilldela lämpliga värden. Om du till exempel vill filtrera efter företagets namn under sträng skapar du en variabel som ska innehålla del strängen. Om du vill filtrera efter kund-ID skapar du en variabel som innehåller ID: t.

I följande exempel finns exempel kod för att filtrera efter företagets namn under sträng, kund-ID eller resurs typ. Välj en och kommentera ut de andra. I varje fall instansierar du först ett [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) -objekt med [**Standardkonstruktorn**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter.-ctor) för att skapa filtret. Du måste skicka en sträng som innehåller det fält som ska sökas och lämplig operator som ska användas, som visas. Du måste också ange strängen för att filtrera efter.

Använd sedan egenskapen [**AuditRecords**](/dotnet/api/microsoft.store.partnercenter.ipartner.auditrecords) för att hämta ett gränssnitt för att granska post åtgärder och anropa [**frågan**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) eller [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.queryasync) -metoden för att köra filtret och hämta insamlingen av [**AuditRecord**](/dotnet/api/microsoft.store.partnercenter.models.auditing.auditrecord) som representerar den första sidan i resultatet. Skicka metoden start datum, ett valfritt slutdatum som inte används i exemplet här och ett [**IQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) -objekt som representerar en fråga på en entitet. IQuery-objektet skapas genom att skicka filtret som skapats ovan till [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) - [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) -metoden.

När du har den första sidan med objekt använder du metoden [**enumerations. AuditRecords. Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) för att skapa en uppräknare som du kan använda för att iterera igenom de återstående sidorna.

```csharp
// IAggregatePartner partnerOperations;

var startDate = new DateTime(DateTime.Now.Year, DateTime.Now.Month, 01);

// First perform the query, then get the enumerator. Choose one of the following and comment out the other two.

// To retrieve audit records by company name substring (for example "bri" matches "Fabrikam, Inc.").
var searchSubstring="bri";
var filter = new SimpleFieldFilter(AuditRecordSearchField.CompanyName.ToString(), FieldFilterOperation.Substring, searchSubstring);
var auditRecordsPage = partnerOperations.AuditRecords.Query(startDate.Date, query: QueryFactory.Instance.BuildSimpleQuery(filter));

// To retrieve audit records by customer ID.
var customerId="0c39d6d5-c70d-4c55-bc02-f620844f3fd1";
var filter = new SimpleFieldFilter(AuditRecordSearchField.CustomerId.ToString(), FieldFilterOperation.Equals, customerId);
var auditRecordsPage = partnerOperations.AuditRecords.Query(startDate.Date, query: QueryFactory.Instance.BuildSimpleQuery(filter));

// To retrieve audit records by resource type.
int resourceTypeInt = 3; // Subscription Resource.
string searchField = Enum.GetName(typeof(ResourceType), resourceTypeInt);
var filter = new SimpleFieldFilter(AuditRecordSearchField.ResourceType.ToString(), FieldFilterOperation.Equals, searchField);
var auditRecordsPage = partnerOperations.AuditRecords.Query(startDate.Date, query: QueryFactory.Instance.BuildSimpleQuery(filter));

var auditRecordEnumerator = partnerOperations.Enumerators.AuditRecords.Create(auditRecordsPage);

int pageNumber = 1;
while (auditRecordEnumerator.HasValue)
{
    // Work with the current page.
    foreach (var c in auditRecordEnumerator.Current.Items)
    {
        // Display some info, such as operation type, operation date, and operation status.
        Console.WriteLine(string.Format("{0} {1} {2}.", c.OperationType, c.OperationDate, c.OperationStatus));
    }

    // Get the next page of audit records.
    auditRecordEnumerator.Next();
}
```

**Exempel**: [konsol test app](console-test-app.md). **Projekt**: Partner Center SDK exempel **mapp**: granskning

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod  | URI för förfrågan                                                                                                                                                                                    |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **TA** | [*{baseURL}*](partner-center-rest-urls.md)/v1/AuditRecords? StartDate = {StartDate} http/1.1                                                                                                     |
| **TA** | [*{baseURL}*](partner-center-rest-urls.md)/v1/AuditRecords? StartDate = {StartDate} &EndDate = {ENDDATE} http/1.1                                                                                   |
| **TA** | [*{baseURL}*](partner-center-rest-urls.md)/v1/AuditRecords? StartDate = {StartDate} &EndDate = {endDate} &filter = {"Field": "företags namn", "värde": "{searchSubstring}", "Operator": "del sträng"} http/1.1 |
| **TA** | [*{baseURL}*](partner-center-rest-urls.md)/v1/AuditRecords? StartDate = {StartDate} &EndDate = {endDate} &filter = {"Field": "CustomerId", "värde": "{CustomerId}", "Operator": "är lika med"} http/1.1          |
| **TA** | [*{baseURL}*](partner-center-rest-urls.md)/v1/AuditRecords? StartDate = {StartDate} &EndDate = {endDate} &filter = {"Field": "resourcetype", "värde": "{resourcetype}", "Operator": "är lika med"} http/1.1      |

### <a name="uri-parameter"></a>URI-parameter

Använd följande frågeparametrar när du skapar begäran.

| Namn      | Typ   | Obligatorisk | Beskrivning                                                                                                                                                                                                                |
|-----------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /SD | date   | No       | Start datumet i formatet åååå-mm-dd. Om inget anges, kommer resultat uppsättningen att standardvärdet 30 dagar före datumet för begäran. Den här parametern är valfri när ett filter anges.                                          |
| endDate   | date   | No       | Slutdatumet i åååå-mm-dd-format. Den här parametern är valfri när ett filter anges. När slutdatumet utelämnas eller är inställt på null, returnerar begäran Max fönstret eller använder dagens datum som slutdatum, beroende på vilket som är mindre. |
| filter    | sträng | No       | Filtret som ska användas. Den här parametern måste vara en kodad sträng. Den här parametern är valfri när start datumet eller slutdatumet anges.                                                                                              |

### <a name="filter-syntax"></a>Filter-syntax
Du måste skapa filter parametern som en serie kommaavgränsade par med nyckel/värde-par. Varje nyckel och värde måste anges individuellt och avgränsas med kolon. Hela filtret måste vara kodat.

Ett avkodat exempel ser ut så här:

```
?filter{"Field":"CompanyName","Value":"bri","Operator":"substring"}
```

I följande tabell beskrivs de nyckel/värde-par som krävs:

| Tangent                 | Värde                             |
|:--------------------|:----------------------------------|
| Fält               | Det fält som ska filtreras. De värden som stöds finns i [syntaxen för begäran](get-a-record-of-partner-center-activity-by-user.md#rest-request).                                         |
| Värde               | Värdet att filtrera efter. Skift läget för värdet ignoreras. Följande värde parametrar stöds som visas i [syntaxen för begäran](get-a-record-of-partner-center-activity-by-user.md#rest-request):<br/><br/>                                                                *searchSubstring* – Ersätt med namnet på företaget. Du kan ange en under sträng som ska matcha en del av företags namnet (till exempel `bri` kommer att matcha `Fabrikam, Inc` ).<br/>**Exempel:**`"Value":"bri"`<br/><br/>                                                                *customerId* – Ersätt med en GUID-formaterad sträng som representerar kund-ID: t.<br/>**Exempel:**`"Value":"0c39d6d5-c70d-4c55-bc02-f620844f3fd1"`<br/><br/>                                                                                        *resourceType* – Ersätt med den typ av resurs som gransknings poster ska hämtas för (till exempel prenumeration). Tillgängliga resurs typer definieras i [resourcetype](/dotnet/api/microsoft.store.partnercenter.models.auditing.resourcetype).<br/>**Exempel:**`"Value":"Subscription"`                                 |
| Operator          | Operatorn som ska användas. De operatorer som stöds finns i [begärans syntax](get-a-record-of-partner-center-activity-by-user.md#rest-request).   |

### <a name="request-headers"></a>Begärandehuvuden

- Mer information finns i [delar av en del i mitten av rest-rubriker](headers.md) .

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/v1/auditrecords?startDate=6/1/2017%2012:00:00%20AM&filter=%7B%22Field%22:%22CustomerId%22,%22Value%22:%220c39d6d5-c70d-4c55-bc02-f620844f3fd1%22,%22Operator%22:%22equals%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 127facaa-e389-41f8-8bb7-1d1af99db893
MS-CorrelationId: de9c2ccc-40dd-4186-9660-65b9b64c3d14
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST-svar

Om det lyckas, returnerar den här metoden en uppsättning aktiviteter som uppfyller filtren.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Length: 2859
Content-Type: application/json; charset=utf-8
MS-CorrelationId: de9c2ccc-40dd-4186-9660-65b9b64c3d14
MS-RequestId: 127facaa-e389-41f8-8bb7-1d1af99db893
MS-CV: 4xDKynq/zE2im0wj.0
MS-ServerId: 030011719
Date: Tue, 27 Jun 2017 22:19:46 GMT

{
    "totalCount": 2,
    "items": [{
            "partnerId": "3b33e682-00c3-41ee-9dd2-a548adf56438",
            "customerId": "0c39d6d5-c70d-4c55-bc02-f620844f3fd1",
            "customerName": "Relecloud",
            "userPrincipalName": "admin@domain.onmicrosoft.com",
            "resourceType": "order",
            "resourceNewValue": "{\"Id\":\"d51a052e-043c-4a2a-aa37-2bb938cef6c1\",\"ReferenceCustomerId\":\"0c39d6d5-c70d-4c55-bc02-f620844f3fd1\",\"BillingCycle\":\"none\",\"LineItems\":[{\"LineItemNumber\":0,\"OfferId\":\"C0BD2E08-11AC-4836-BDC7-3712E744922F\",\"SubscriptionId\":\"488745B5-2086-4912-802C-6ABB9F7C3638\",\"ParentSubscriptionId\":null,\"FriendlyName\":\"Office 365 Business Premium Trial\",\"Quantity\":25,\"PartnerIdOnRecord\":null,\"Links\":{\"Subscription\":{\"Uri\":\"/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/488745B5-2086-4912-802C-6ABB9F7C3638\",\"Method\":\"GET\",\"Headers\":[]}}}],\"CreationDate\":\"2017-06-15T15:56:04.077-07:00\",\"Links\":{\"Self\":{\"Uri\":\"/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/orders/d51a052e-043c-4a2a-aa37-2bb938cef6c1\",\"Method\":\"GET\",\"Headers\":[]}},\"Attributes\":{\"Etag\":\"eyJpZCI6ImQ1MWEwNTJlLTA0M2MtNGEyYS1hYTM3LTJiYjkzOGNlZjZjMSIsInZlcnNpb24iOjF9\",\"ObjectType\":\"Order\"}}",
            "operationType": "create_order",
            "operationDate": "2017-06-15T22:56:05.0589308Z",
            "operationStatus": "succeeded",
            "customizedData": [{
                    "key": "OrderId",
                    "value": "d51a052e-043c-4a2a-aa37-2bb938cef6c1"
                }, {
                    "key": "BillingCycle",
                    "value": "None"
                }, {
                    "key": "OfferId-0",
                    "value": "C0BD2E08-11AC-4836-BDC7-3712E744922F"
                }, {
                    "key": "SubscriptionId-0",
                    "value": "488745B5-2086-4912-802C-6ABB9F7C3638"
                }, {
                    "key": "SubscriptionName-0",
                    "value": "Office 365 Business Premium Trial"
                }, {
                    "key": "Quantity-0",
                    "value": "25"
                }, {
                    "key": "PartnerOnRecord-0",
                    "value": null
                }
            ],
            "attributes": {
                "objectType": "AuditRecord"
            }
        }, {
            "partnerId": "3b33e682-00c3-41ee-9dd2-a548adf56438",
            "customerId": "0c39d6d5-c70d-4c55-bc02-f620844f3fd1",
            "customerName": "Relecloud",
            "userPrincipalName": "admin@domain.onmicrosoft.com",
            "applicationId": "Partner Center Native App",
            "resourceType": "license",
            "resourceNewValue": "{\"LicensesToAssign\":[{\"ExcludedPlans\":null,\"SkuId\":\"efccb6f7-5641-4e0e-bd10-b4976e1bf68e\"}],\"LicensesToRemove\":null,\"LicenseWarnings\":[],\"Attributes\":{\"ObjectType\":\"LicenseUpdate\"}}",
            "operationType": "update_customer_user_licenses",
            "operationDate": "2017-06-01T20:09:07.0450483Z",
            "operationStatus": "succeeded",
            "customizedData": [{
                    "key": "CustomerUserId",
                    "value": "482e2152-4b49-48ec-b715-823365ce3d4c"
                }, {
                    "key": "AddedLicenseSkuId",
                    "value": "efccb6f7-5641-4e0e-bd10-b4976e1bf68e"
                }
            ],
            "attributes": {
                "objectType": "AuditRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/auditrecords?startDate=2017-06-01&size=500&filter=%7B%22Field%22%3A%22CustomerId%22%2C%22Value%22%3A%220c39d6d5-c70d-4c55-bc02-f620844f3fd1%22%2C%22Operator%22%3A%22equals%22%7D",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```