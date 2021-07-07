---
title: Återställ en borttagen användare för en kund
description: Återställa en borttagna användare efter kund-ID och användar-ID.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 23caf91c6b29b292c2638b4a1ad208c606c47492
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445722"
---
# <a name="restore-a-deleted-user-for-a-customer"></a>Återställ en borttagen användare för en kund

Återställa en borttagna användare efter **kund-ID** och användar-ID.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med app+användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard) Välj **CSP** på Menyn i Partnercenter följt av **Kunder**. Välj kunden i kundlistan och välj sedan **Konto.** På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.** Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).

- Användar-ID:t. Om du inte har användar-ID kan du se [Visa borttagna användare för en kund.](view-a-deleted-user.md)

## <a name="when-can-you-restore-a-deleted-user-account"></a>När kan du återställa ett borttagna användarkonton?

Användartillståndet är inaktivt när du tar bort ett användarkonto. Det förblir så i 30 dagar, varpå användarkontot och tillhörande data rensas och görs oåterkalleliga. Du kan bara återställa ett borttagna användarkonton under det här 30-dagars fönstret. När användarkontot har tagits bort och markerats som "inaktivt" returneras det inte längre som medlem i användarsamlingen (till exempel genom att använda Hämta en lista över alla användarkonton [för en kund).](get-a-list-of-all-user-accounts-for-a-customer.md)

## <a name="c"></a>C\#

Om du vill återställa en användare skapar du en ny instans av klassen [**CustomerUser**](/dotnet/api/microsoft.store.partnercenter.models.users.customeruser) och anger värdet för egenskapen [**User.State**](/dotnet/api/microsoft.store.partnercenter.models.users.user.state) till [**UserState.Active**](/dotnet/api/microsoft.store.partnercenter.models.users.userstate).

Du återställer en borttagna användare genom att ange användarens tillstånd till aktiv. Du behöver inte fylla i de återstående fälten i användarresursen på nya sätt. Dessa värden återställs automatiskt från den borttagna, inaktiva användarresursen. Använd sedan metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att identifiera kunden och [**metoden Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) för att identifiera användaren.

Anropa slutligen [**Patch-metoden**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.patch) och skicka **CustomerUser-instansen** för att skicka begäran om att återställa användaren.

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedCustomerUserId;

var updatedCustomerUser = new CustomerUser()
{
    State = UserState.Active
};

// Restore customer user information.
var restoredCustomerUserInfo = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Patch(updatedCustomerUser);
```

**Exempel:** [Konsoltestapp](console-test-app.md). **Project:** Partnercenter-SDK **Exempelklass:** CustomerUserRestore.cs

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod    | URI för förfrågan                                                                                            |
|-----------|--------------------------------------------------------------------------------------------------------|
| **Patch** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1 |

### <a name="uri-parameter"></a>URI-parameter

Använd följande frågeparametrar för att ange kund-ID och användar-ID.

| Namn                   | Typ     | Obligatorisk | Beskrivning                                                                                                              |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------|
| **kund-klient-id** | **guid** | Y        | Värdet är ett GUID-formaterat **kundklient-ID** som gör att återförsäljaren kan filtrera resultatet till en viss kund. |
| **användar-id**            | **guid** | Y        | Värdet är ett GUID-formaterat **användar-ID** som tillhör ett enda användarkonto.                                         |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

I den här tabellen beskrivs de obligatoriska egenskaperna i begärandetexten.

| Namn       | Typ   | Obligatorisk | Beskrivning                                                            |
|------------|--------|----------|------------------------------------------------------------------------|
| Tillstånd      | sträng | Y        | Användartillståndet. Om du vill återställa en borttagna användare måste strängen innehålla "aktiv". |
| Attribut | objekt | N        | Innehåller "ObjectType": "CustomerUser".                                 |

### <a name="request-example"></a>Exempel på begäran

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 6e668bc0-5bd7-44d6-b6fa-529d41ce9659
MS-CorrelationId: 32be760f-8282-4e01-a37b-829c8a700e8a
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 269
Expect: 100-continue

{
    "State": "active",
    "Attributes": {
        "ObjectType": "CustomerUser"
    }
}
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar svaret den återställda användarinformationen i svarstexten.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder för Partner Center REST.](error-codes.md)

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Length: 465
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 32be760f-8282-4e01-a37b-829c8a700e8a
MS-RequestId: 6e668bc0-5bd7-44d6-b6fa-529d41ce9659
MS-CV: ZTeBriO7mEaiM13+.0
MS-ServerId: 101112616
Date: Fri, 20 Jan 2017 22:24:55 GMT

{
    "usageLocation": "US",
    "id": "a45f1416-3300-4f65-9e8d-f123b397a4ea",
    "userPrincipalName": "e83763f7f2204ac384cfcd49f79f2749@dtdemocspcustomer005.onmicrosoft.com",
    "firstName": "Ferdinand",
    "lastName": "Filibuster",
    "displayName": "Ferdinand",
    "userDomainType": "none",
    "state": "active",
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
```
