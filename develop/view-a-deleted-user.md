---
title: Visa borttagna användare för en kund
description: Hämtar en lista över borttagna CustomerUser-resurser för en kund efter kund-ID. Du kan också ange en sid storlek. Du måste ange ett filter.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9b1a9b85e3eba7ae7ec1dab8e951134d03371604
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769534"
---
# <a name="view-deleted-users-for-a-customer"></a>Visa borttagna användare för en kund

**Gäller för**

- Partnercenter

Hämtar en lista över borttagna CustomerUser-resurser för en kund efter kund-ID. Du kan också ange en sid storlek. Du måste ange ett filter.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).

## <a name="what-happens-when-you-delete-a-user-account"></a>Vad händer när du tar bort ett användar konto?

Användar tillstånd är inställt på "inaktiv" när du tar bort ett användar konto. Den är på samma sätt i trettio dagar, efter vilken användar kontot och dess associerade data rensas och blir oåterkalleligt. Om du vill återställa ett borttaget användar konto inom den trettio dags perioden, se [återställa en borttagen användare för en kund](restore-a-user-for-a-customer.md). När du har tagit bort och markerat "inaktiv" returneras användar kontot inte längre som medlem i användar samlingen (till exempel med [Hämta en lista över alla användar konton för en kund](get-a-list-of-all-user-accounts-for-a-customer.md)). Om du vill hämta en lista över borttagna användare som ännu inte har rensats måste du fråga efter användar konton som har angetts till inaktiva.

## <a name="c"></a>C\#

Om du vill hämta en lista över borttagna användare skapar du en fråga som filtrerar kund användare vars status är inaktive rad. Först skapar du filtret genom att instansiera ett [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) -objekt med parametrarna som de visas i följande kodfragment. Skapa sedan frågan med metoden [**BuildIndexedQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) . Om du inte vill ha växlade resultat kan du använda metoden [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) i stället. Använd sedan metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID för att identifiera kunden. Anropa slutligen [**fråge**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.query) metoden för att skicka begäran.

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

**Exempel**: [konsol test app](console-test-app.md). **Projekt**: Partner Center SDK-exempel **klass**: GetCustomerInactiveUsers.CS

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod  | URI för förfrågan                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| **TA** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Users? size = {size} &filter = {filter} http/1.1 |

### <a name="uri-parameter"></a>URI-parameter

Använd följande sökväg och frågeparametrar när du skapar begäran.

| Namn        | Typ   | Obligatorisk | Beskrivning                                                                                                                                                                        |
|-------------|--------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| kund-ID | guid   | Yes      | Värdet är ett GUID-formaterat kund-ID som identifierar kunden.                                                                                                            |
| ikoner        | int    | No       | Antalet resultat som ska visas samtidigt. Den här parametern är valfri.                                                                                                     |
| filter      | filter | Yes      | Frågan som filtrerar användar sökningen. Om du vill hämta borttagna användare måste du ta med och koda följande sträng: {"Field": "UserState", "value": "inactive", "Operator": "equals"}. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

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

Om det lyckas returnerar den här metoden en samling [CustomerUser](user-resources.md#customeruser) -resurser i svars texten.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).

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
