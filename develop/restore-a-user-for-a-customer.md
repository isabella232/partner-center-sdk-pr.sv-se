---
title: Återställ en borttagen användare för en kund
description: Återställa en borttagen användare med kund-ID och användar-ID.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9fd86a268c804a2fdd5efd67a8982afc043c95a6
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769798"
---
# <a name="restore-a-deleted-user-for-a-customer"></a>Återställ en borttagen användare för en kund

**Gäller för**

- Partnercenter

Återställa en borttagen **användare** med kund-ID och användar-ID.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).

- Användar-ID. Om du inte har användar-ID, se [Visa borttagna användare för en kund](view-a-deleted-user.md).

## <a name="when-can-you-restore-a-deleted-user-account"></a>När kan du återställa ett borttaget användar konto?

Användar tillstånd är inställt på "inaktiv" när du tar bort ett användar konto. Den är på samma sätt i trettio dagar, efter vilken användar kontot och dess associerade data rensas och blir oåterkalleligt. Du kan bara återställa ett borttaget användar konto under den här trettio dagars perioden. När du har tagit bort och markerat "inaktiv" returneras inte längre användar kontot som medlem i användar samlingen (till exempel med [Hämta en lista över alla användar konton för en kund](get-a-list-of-all-user-accounts-for-a-customer.md)).

## <a name="c"></a>C\#

Om du vill återställa en användare skapar du en ny instans av klassen [**CustomerUser**](/dotnet/api/microsoft.store.partnercenter.models.users.customeruser) och anger värdet för egenskapen [**User. State**](/dotnet/api/microsoft.store.partnercenter.models.users.user.state) till [**userState. Active**](/dotnet/api/microsoft.store.partnercenter.models.users.userstate).

Du återställer en borttagen användare genom att ange användarens tillstånd till aktiv. Du behöver inte fylla i återstående fält i användar resursen igen. Dessa värden kommer automatiskt att återställas från den borttagna, inaktiva användar resursen. Använd sedan metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: t för att identifiera kunden och metoden [**users. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) för att identifiera användaren.

Anropa slutligen [**korrigerings**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.patch) metoden och skicka **CustomerUser** -instansen för att skicka begäran om att återställa användaren.

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

**Exempel**: [konsol test app](console-test-app.md). **Projekt**: Partner Center SDK-exempel **klass**: CustomerUserRestore.CS

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod    | URI för förfrågan                                                                                            |
|-----------|--------------------------------------------------------------------------------------------------------|
| **9.0a** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Users/{User-ID} http/1.1 |

### <a name="uri-parameter"></a>URI-parameter

Använd följande frågeparametrar för att ange kund-ID och användar-ID.

| Namn                   | Typ     | Obligatorisk | Beskrivning                                                                                                              |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------|
| **kund-ID för klient organisation** | **guid** | Y        | Värdet är ett GUID-formaterat **kund-Tenant-ID** som gör det möjligt för åter försäljaren att filtrera resultaten till en bestämd kund. |
| **användar-ID**            | **guid** | Y        | Värdet är ett GUID-formaterat **användar-ID** som tillhör ett enda användar konto.                                         |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

I den här tabellen beskrivs de egenskaper som krävs i begär ande texten.

| Namn       | Typ   | Obligatorisk | Beskrivning                                                            |
|------------|--------|----------|------------------------------------------------------------------------|
| Stat      | sträng | Y        | Användar tillstånd. Om du vill återställa en borttagen användare måste strängen innehålla "Active". |
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

Om det lyckas returnerar svaret den återställda användar informationen i svars texten.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).

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
