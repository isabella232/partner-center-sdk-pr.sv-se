---
title: Hämta en post för Partnercenter-aktivitet
description: Så här hämtar du en post med åtgärder som utförs av en partneranvändare eller ett program under en viss tidsperiod.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 5d965fc226d326998212ef0f027160d50f69d5e84360c8a9d09c27a76c63310d
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991080"
---
# <a name="get-a-record-of-partner-center-activity"></a>Hämta en post för Partnercenter-aktivitet

**Gäller för**: Partner Center-| PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

I den här artikeln beskrivs hur du hämtar en post med åtgärder som utförts av en partneranvändare eller ett program under en viss tidsperiod.

Använd det här API:et för att hämta granskningsposter för de senaste 30 dagarna från det aktuella datumet eller för ett datumintervall som anges genom att inkludera startdatumet och/eller slutdatumet. Observera dock att tillgängligheten för aktivitetsloggdata av prestandaskäl är begränsad till de senaste 90 dagarna. Begäranden med ett startdatum som är större än 90 dagar före det aktuella datumet får ett undantag för felaktig begäran (felkod: 400) och ett lämpligt meddelande.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.

## <a name="c"></a>C\#

Om du vill hämta en post för Partner Center-åtgärder måste du först upprätta datumintervallet för de poster som du vill hämta. I följande kodexempel används bara ett startdatum, men du kan även inkludera ett slutdatum. Mer information finns i [**Frågemetod.**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) Skapa sedan de variabler som du behöver för den typ av filter som du vill tillämpa och tilldela lämpliga värden. Om du till exempel vill filtrera efter företagsnamnssträng skapar du en variabel som ska innehålla delsträngen. Om du vill filtrera efter kund-ID skapar du en variabel som ska innehålla ID:t.

I följande exempel tillhandahålls exempelkod för att filtrera efter en delsträng för företagsnamn, kund-ID eller resurstyp. Välj en och kommentera ut de andra. I varje fall instansierar du först ett [**SimpleFieldFilter-objekt med**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) dess standardkonstruktor för att skapa filtret. [](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter.-ctor) Du måste skicka en sträng som innehåller fältet att söka efter och lämplig operator för att tillämpa, som du ser i bilden. Du måste också ange strängen att filtrera efter.

Använd sedan egenskapen [**AuditRecords**](/dotnet/api/microsoft.store.partnercenter.ipartner.auditrecords) för att hämta ett gränssnitt för att granska poståtgärder och anropa metoden [**Query**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.query) eller [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.auditrecords.iauditrecordscollection.queryasync) för att köra filtret och hämta samlingen [**med AuditRecords**](/dotnet/api/microsoft.store.partnercenter.models.auditing.auditrecord) som representerar den första sidan i resultatet. Skicka metoden startdatum, ett valfritt slutdatum som inte används i exemplet här och ett [**IQuery-objekt**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) som representerar en fråga på en entitet. IQuery-objektet skapas genom att skicka filtret som skapades ovan till [**QueryFactorys**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) [**BuildSimpleQuery-metod.**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery)

När du har den första sidan med objekt använder du metoden [**Enumerators.AuditRecords.Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) för att skapa en uppräkning som du kan använda för att iterera genom de återstående sidorna.

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

**Exempel:** [Konsoltestapp](console-test-app.md). **Project:** Partnercenter-SDK **exempelmapp:** Granskning

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod  | URI för förfrågan                                                                                                                                                                                    |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Få** | [*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate} HTTP/1.1                                                                                                     |
| **Få** | [*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate} HTTP/1.1                                                                                   |
| **Få** | [*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"CompanyName","Value":"{searchSubstring}","Operator":"substring"} HTTP/1.1 |
| **Få** | [*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"CustomerId","Value":"{customerId}","Operator":"equals"} HTTP/1.1          |
| **Få** | [*{baseURL}*](partner-center-rest-urls.md)/v1/auditrecords?startDate={startDate}&endDate={endDate}&filter={"Field":"ResourceType","Value":"{resourceType}","Operator":"equals"} HTTP/1.1      |

### <a name="uri-parameter"></a>URI-parameter

Använd följande frågeparametrar när du skapar begäran.

| Namn      | Typ   | Obligatorisk | Beskrivning                                                                                                                                                                                                                |
|-----------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Startdate | date   | No       | Startdatumet i formatet yyyy-mm-dd. Om inget anges får resultatuppsättningen standardvärdet 30 dagar före begärandedatumet. Den här parametern är valfri när ett filter anges.                                          |
| endDate   | date   | No       | Slutdatumet i formatet yyyy-mm-dd. Den här parametern är valfri när ett filter anges. När slutdatumet utelämnas eller anges till null returnerar begäran det maximala fönstret eller använder idag som slutdatum, beroende på vilket som är mindre. |
| filter    | sträng | No       | Filtret som ska tillämpas. Den här parametern måste vara en kodad sträng. Den här parametern är valfri när startdatum eller slutdatum anges.                                                                                              |

### <a name="filter-syntax"></a>Filtersyntax
Du måste skriva filterparametern som en serie kommaavgränsade nyckel/värde-par. Varje nyckel och värde måste anges individuellt och avgränsas med ett kolon. Hela filtret måste vara kodat.

Ett okodat exempel ser ut så här:

```
?filter{"Field":"CompanyName","Value":"bri","Operator":"substring"}
```

I följande tabell beskrivs de nyckel/värde-par som krävs:

| Tangent                 | Värde                             |
|:--------------------|:----------------------------------|
| Fält               | Fältet som ska filtreras. Värdena som stöds finns i [Begärandesyntax](get-a-record-of-partner-center-activity-by-user.md#rest-request).                                         |
| Värde               | Det värde som ska filtreras efter. Värdets fall ignoreras. Följande värdeparametrar stöds enligt vad som visas i [Begärandesyntax:](get-a-record-of-partner-center-activity-by-user.md#rest-request)<br/><br/>                                                                *searchSubstring* – Ersätt med namnet på företaget. Du kan ange en delsträng som matchar en del av företagets namn (till exempel `bri` matchar `Fabrikam, Inc` ).<br/>**Exempel:** `"Value":"bri"`<br/><br/>                                                                *customerId* – Ersätt med en GUID-formaterad sträng som representerar kundidentifieraren.<br/>**Exempel:** `"Value":"0c39d6d5-c70d-4c55-bc02-f620844f3fd1"`<br/><br/>                                                                                        *resourceType* – Ersätt med den typ av resurs som du vill hämta granskningsposter för (till exempel Prenumeration). De tillgängliga resurstyperna definieras i [ResourceType](/dotnet/api/microsoft.store.partnercenter.models.auditing.resourcetype).<br/>**Exempel:** `"Value":"Subscription"`                                 |
| Operator          | Operatorn som ska tillämpas. Operatorerna som stöds finns i [Begärandesyntax](get-a-record-of-partner-center-activity-by-user.md#rest-request).   |

### <a name="request-headers"></a>Begärandehuvuden

- Mer information finns i [Parter Center REST-huvuden.](headers.md)

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

Om det lyckas returnerar den här metoden en uppsättning aktiviteter som uppfyller filtren.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)

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