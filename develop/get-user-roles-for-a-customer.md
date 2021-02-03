---
title: Hämta användarroller för en kund
description: Hämta en lista över alla roller/behörigheter som är kopplade till ett användar konto. Variationerna omfattar att hämta en lista över alla behörigheter för alla användar konton för en kund och hämta en lista över användare som har en specifik roll.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8dad5c035c08905c3d39052de07ebb912452a16b
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768907"
---
# <a name="get-user-roles-for-a-customer"></a>Hämta användarroller för en kund

**Gäller för**

- Partnercenter

Hämta en lista över alla roller/behörigheter som är kopplade till ett användar konto. Variationerna omfattar att hämta en lista över alla behörigheter för alla användar konton för en kund och hämta en lista över användare som har en specifik roll.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Om du vill hämta alla katalog roller för en angiven kund hämtar du först det angivna kund-ID: t. Använd sedan din **IAggregatePartner. Customers** -samling och anropa **ById ()-** metoden. Anropa sedan egenskapen **DirectoryRoles** följt av metoden **Get ()** eller **GetAsync ()**.

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

var directoryRoles = partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.Get();
```

**Exempel**: [konsol test app](console-test-app.md). **Projekt**: Partner Center SDK-exempel **klass**: GetCustomerDirectoryRoles.CS

Hämta en lista med kund användare som har en viss roll genom att först hämta det angivna kund-ID: t och katalog rollens ID. Använd sedan din **IAggregatePartner. Customers** -samling och anropa **ById ()-** metoden. Anropa sedan egenskapen **DirectoryRoles** , sedan **ById ()** -metoden, sedan egenskapen **UserMembers** , följt av metoden **Get ()** eller **GetAsync ()** .

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;
// string selectedDirectoryRoleId;

var userMembers = partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.ById(selectedDirectoryRoleId).UserMembers.Get();
```

**Exempel**: [konsol test app](console-test-app.md). **Projekt**: PartnerSDK. FeatureSamples- **klass**: GetCustomerDirectoryRoleUserMembers.CS

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod  | URI för förfrågan                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------|
| **TA** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Users/{User-ID}/directoryroles http/1.1 |
| **TA** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/directoryroles http/1.1                 |
| **TA** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/directoryroles/{Role-ID}/usermembers    |

### <a name="uri-parameter"></a>URI-parameter

Använd följande frågeparameter för att identifiera rätt kund.

| Namn                   | Typ     | Obligatorisk | Beskrivning                                                                                                                                                                                                 |
|------------------------|----------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **kund-ID för klient organisation** | **guid** | Y        | Värdet är ett GUID-formaterat **kund-Tenant-ID** som gör det möjligt för åter försäljaren att filtrera resultaten för en specifik kund som tillhör åter försäljaren.                                                      |
| **användar-ID**            | **guid** | N        | Värdet är ett GUID-formaterat **användar-ID** som tillhör ett enda användar konto.                                                                                                                            |
| **roll-ID**            | **guid** | N        | Värdet är ett GUID-formaterat **roll-ID** som tillhör en typ av roll. Du kan hämta dessa ID: n genom att fråga alla katalog roller för en kund, över alla användar konton. (Det andra scenariot ovan). |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/users/<user-id>/directoryroles HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden en lista över de roller som är associerade med det aktuella användar kontot.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [felkoder](error-codes.md).

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Length: 31942
Content-Type: application/json
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
Date: June 24 2016 22:00:25 PST

{
      "totalCount": 2,
      "items": [
        {
          "name": "Helpdesk Administrator",
          "id": "729827e3-9c14-49f7-bb1b-9608f156bbb8",
          "attributes": { "objectType": "DirectoryRole" }
        },
        {
          "name": "User Account Administrator",
          "id": "fe930be7-5e62-47db-91af-98c3a49a38b1",
          "attributes": { "objectType": "DirectoryRole" }
        }
      ],
      "attributes": { "objectType": "Collection" }
}
```
