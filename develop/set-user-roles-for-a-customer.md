---
title: Ange användarroller för en kund
description: Det finns en uppsättning katalog roller inom ett kund konto. Du kan tilldela användar konton till dessa roller.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f42120e40e54ff8bd6242634d97268091abf8e1c
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769591"
---
# <a name="set-user-roles-for-a-customer"></a>Ange användarroller för en kund

**Gäller för**

- Partnercenter

Det finns en uppsättning katalog roller inom ett kund konto. Du kan tilldela användar konton till dessa roller.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Om du vill tilldela en katalog roll till en kund användare skapar du en ny [**UserMember**](/dotnet/api/microsoft.store.partnercenter.models.roles.usermember) med relevanta användar uppgifter. Anropa sedan metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med det angivna kund-ID: t för att identifiera kunden. Därifrån använder du metoden [**DirectoryRoles. ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) med katalog roll-ID: t för att ange rollen. Öppna sedan **UserMembers** -samlingen och Använd [**create**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.create) -metoden för att lägga till den nya användar medlemmen i samlingen av användar medlemmar som tilldelats rollen.

``` csharp
// UserMember createdUser;
// IAggregatePartner partnerOperations;
// Customer selectedCustomer;
// IDirectoryRole selectedRole;

// Create the new user member.
UserMember userMemberToAdd = new UserMember()
{
    UserPrincipalName = createdUser.UserPrincipalName,
    DisplayName = createdUser.DisplayName,
    Id = createdUser.Id
};

// Add the new user member to the role.
var userMemberAdded = partnerOperations.Customers.ById(selectedCustomer.Id).DirectoryRoles.ById(selectedRole.Id).UserMembers.Create(userMemberToAdd);
```

**Exempel**: [konsol test app](console-test-app.md). **Projekt**: Partner Center SDK-exempel **klass**: AddUserMemberToDirectoryRole.CS

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod   | URI för förfrågan                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| **EFTER** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/directoryroles/{Role-ID}/usermembers http/1.1 |

### <a name="uri-parameter"></a>URI-parameter

Använd följande URI-parametrar för att identifiera rätt kund och roll. Identifiera den användare som du vill tilldela rollen genom att ange identifierings informationen i begär ande texten.

| Namn                   | Typ     | Obligatorisk | Beskrivning                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **kund-ID för klient organisation** | **guid** | Y        | Värdet är ett GUID-formaterat **kund-Tenant-ID** som gör det möjligt för åter försäljaren att filtrera resultaten för en specifik kund som tillhör åter försäljaren. |
| **roll-ID**            | **guid** | Y        | Värdet är ett GUID-formaterat **roll-ID** som identifierar den roll som ska tilldelas användaren.                                                              |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

I den här tabellen beskrivs de egenskaper som krävs i begär ande texten.

| Namn                  | Typ       | Obligatorisk | Beskrivning                            |
|-----------------------|------------|----------|----------------------------------------|
| **Identitet**                | **nollängd** | Y        | ID för den användare som ska läggas till i rollen. |
| **DisplayName**       | **nollängd** | Y        | Användarens användarvänliga visnings namn. |
| **UserPrincipalName** | **nollängd** | Y        | Namnet på användarens huvud namn.        |
| **Attribut**        | **jobbobjektet** | Y        | Innehåller "ObjectType": "UserMember"     |

### <a name="request-example"></a>Exempel på begäran

```http
POST https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/directoryroles/f023fd81-a637-4b56-95fd-791ac0226033/usermembers HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a56cb2e5-a156-4f68-9155-57ffe2b93d18
MS-CorrelationId: 90bda268-7929-4ad6-be01-89c5af5fc504
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 180
Expect: 100-continue

{
    "Id": "a9ef48bb-8758-4590-a312-d4a47bfaded4",
    "DisplayName": "Daniel Tsai",
    "UserPrincipalName": "Daniel@dtdemocspcustomer005.onmicrosoft.com",
    "Attributes": {
        "ObjectType": "UserMember"
    }
}
```

## <a name="rest-response"></a>REST-svar

Den här metoden returnerar användar kontot med det roll-ID som är kopplat när användaren har tilldelat rollen.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 201 Created
Content-Length: 231
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 90bda268-7929-4ad6-be01-89c5af5fc504
MS-RequestId: a56cb2e5-a156-4f68-9155-57ffe2b93d18
MS-CV: aia94+gnrEeQqkGr.0
MS-ServerId: 101112202
Date: Tue, 20 Dec 2016 23:36:55 GMT

{
    "displayName": "Daniel Tsai",
    "userPrincipalName": "Daniel@dtdemocspcustomer005.onmicrosoft.com",
    "roleId": "f023fd81-a637-4b56-95fd-791ac0226033",
    "id": "a9ef48bb-8758-4590-a312-d4a47bfaded4",
    "attributes": {
        "objectType": "UserMember"
    }
}
```
