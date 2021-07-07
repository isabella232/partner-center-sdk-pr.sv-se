---
title: Visa borttagna användare för en kund
description: Hämtar en lista över borttagna CustomerUser-resurser för en kund efter kund-ID. Du kan också ange en sidstorlek. Du måste ange ett filter.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f4fec958a9a6bb580d35de1cf3007e1db3b2b650
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445314"
---
# <a name="view-deleted-users-for-a-customer"></a>Visa borttagna användare för en kund

Hämtar en lista över borttagna CustomerUser-resurser för en kund efter kund-ID. Du kan också ange en sidstorlek. Du måste ange ett filter.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med app+användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard) Välj **CSP** på Menyn i Partnercenter följt av **Kunder**. Välj kunden i kundlistan och välj sedan **Konto.** På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.** Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).

## <a name="what-happens-when-you-delete-a-user-account"></a>Vad händer när du tar bort ett användarkonto?

Användartillståndet är inaktivt när du tar bort ett användarkonto. Det förblir så i 30 dagar, varpå användarkontot och tillhörande data rensas och görs oåterkalleliga. Om du vill återställa ett borttagna användarkonto inom 30-dagarsfönstret kan du gå till [Återställa en borttagna användare för en kund.](restore-a-user-for-a-customer.md) När användarkontot har tagits bort och markerats som "inaktivt" returneras det inte längre som medlem i användarsamlingen (t.ex. genom att använda Hämta en lista över alla användarkonton [för en kund).](get-a-list-of-all-user-accounts-for-a-customer.md) Om du vill hämta en lista över borttagna användare som ännu inte har rensats måste du fråga efter användarkonton som har angetts till inaktiva.

## <a name="c"></a>C\#

Om du vill hämta en lista över borttagna användare skapar du en fråga som filtrerar efter kundanvändare vars status är inställd på inaktiv. Skapa först filtret genom att instansiera ett [**SimpleFieldFilter-objekt**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) med parametrarna som visas i följande kodfragment. Skapa sedan frågan med hjälp av [**metoden BuildIndexedQuery.**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) Om du inte vill ha sidindelade resultat kan du använda [**metoden BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) i stället. Använd sedan metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att identifiera kunden. Anropa slutligen [**frågemetoden**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.query) för att skicka begäran.

``` csharp
// IAggregatePartner partnerOperations;
// int customerUserPageSize;

// Create a filter for users whose status is inactive (i.e. deleted).
var filter = new SimpleFieldFilter("UserState", FieldFilterOperation.Equals, "Inactive");

// Build a paged query.
var simpleQueryWithFilter = QueryFactory.Instance.BuildIndexedQuery(customerUserPageSize, 0, filter);

// Send the request.
var customerUsers = partnerOperations.Customers.ById(selectedCustomerId).Users.Query(simpleQueryWithFilter);
```

**Exempel:** [Konsoltestapp](console-test-app.md). **Project:** Partnercenter-SDK **Exempelklass:** GetCustomerInactiveUsers.cs

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod  | URI för förfrågan                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| **Få** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users?size={size}&filter={filter} HTTP/1.1 |

### <a name="uri-parameter"></a>URI-parameter

Använd följande sökväg och frågeparametrar när du skapar begäran.

| Namn        | Typ   | Obligatorisk | Beskrivning                                                                                                                                                                        |
|-------------|--------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| kund-id | guid   | Ja      | Värdet är ett GUID-formaterat kund-ID som identifierar kunden.                                                                                                            |
| ikoner        | int    | Inga       | Antalet resultat som ska visas samtidigt. Den här parametern är valfri.                                                                                                     |
| filter      | filter | Ja      | Frågan som filtrerar användarsökningen. För att hämta borttagna användare måste du inkludera och koda följande sträng: {"Field":"UserState","Value":"Inactive","Operator":"equals"}. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users?size=500&filter=%7B%22Field%22%3A%22UserState%22%2C%22Value%22%3A%22Inactive%22%2C%22Operator%22%3A%22equals%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c11feb95-55d2-45b6-9d1b-74b55d2221fb
MS-CorrelationId: 2b4ab588-f48c-4874-b479-a61895e107b2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden en samling [CustomerUser-resurser](user-resources.md#customeruser) i svarstexten.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Length: 802
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 690b34ca-07c8-4f8a-ab13-f22a50594a43
MS-RequestId: 1187f9ad-02b4-4d96-b668-7cf3d289467b
MS-CV: 3TLmR9gz6EaCVCjR.0
MS-ServerId: 101112616
Date: Fri, 20 Jan 2017 19:13:14 GMT

{
    "totalCount": 1,
    "items": [{
            "usageLocation": "US",
            "id": "a45f1416-3300-4f65-9e8d-f123b397a4ea",
            "userPrincipalName": "e83763f7f2204ac384cfcd49f79f2749@dtdemocspcustomer005.onmicrosoft.com",
            "firstName": "Ferdinand",
            "lastName": "Filibuster",
            "displayName": "Ferdinand",
            "userDomainType": "none",
            "state": "inactive",
            "softDeletionTime": "2017-01-20T00:33:34Z",
            "links": {
                "self": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "CustomerUser"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users?size=500&filter=%7B%22Field%22%3A%22UserStatus%22%2C%22Value%22%3A%22Inactive%22%2C%22Operator%22%3A%22equals%22%7D",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
