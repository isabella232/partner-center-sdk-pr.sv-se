---
title: Hämta användarroller för en kund
description: Hämta en lista över alla roller/behörigheter som är kopplade till ett användarkonto. Variationer omfattar att hämta en lista över alla behörigheter för alla användarkonton för en kund och hämta en lista över användare som har en viss roll.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b139ee69ae5148896b1a438b061907e022175f318956667cebb91ead15b863f6
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989346"
---
# <a name="get-user-roles-for-a-customer"></a>Hämta användarroller för en kund

Hämta en lista över alla roller/behörigheter som är kopplade till ett användarkonto. Variationer omfattar att hämta en lista över alla behörigheter för alla användarkonton för en kund och hämta en lista över användare som har en viss roll.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med app- och användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard) Välj **CSP** på Menyn i Partnercenter följt av **Kunder**. Välj kunden i kundlistan och välj sedan **Konto.** På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.** Microsoft-ID:t är samma som kund-ID :t ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Om du vill hämta alla katalogroller för en angiven kund hämtar du först det angivna kund-ID:t. Använd sedan samlingen **IAggregatePartner.Customers** och anropa **metoden ById().** Anropa sedan egenskapen **DirectoryRoles** följt av metoden **Get()** eller **GetAsync().**

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

var directoryRoles = partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.Get();
```

**Exempel:** [Konsoltestapp](console-test-app.md). **Project:** Partnercenter-SDK **Samples-klass:** GetCustomerDirectoryRoles.cs

Om du vill hämta en lista över kundanvändare som har en viss roll hämtar du först det angivna kund-ID:t och katalogrolls-ID:t. Använd sedan samlingen **IAggregatePartner.Customers** och anropa **metoden ById().** Anropa sedan **egenskapen DirectoryRoles,** sedan **metoden ById()** och sedan egenskapen **UserMembers** följt av **metoden Get()** **eller GetAsync().**

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;
// string selectedDirectoryRoleId;

var userMembers = partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.ById(selectedDirectoryRoleId).UserMembers.Get();
```

**Exempel:** [Konsoltestapp](console-test-app.md). **Project:** PartnerSDK.FeatureSamples-klass: GetCustomerDirectoryRoleUserMembers.cs 

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod  | URI för förfrågan                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------|
| **Få** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id}/directoryroles HTTP/1.1 |
| **Få** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles HTTP/1.1                 |
| **Få** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{role-ID}/usermembers    |

### <a name="uri-parameter"></a>URI-parameter

Använd följande frågeparameter för att identifiera rätt kund.

| Namn                   | Typ     | Obligatorisk | Beskrivning                                                                                                                                                                                                 |
|------------------------|----------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **kund-klient-id** | **guid** | Y        | Värdet är ett GUID-formaterat **kundklient-ID** som gör att återförsäljaren kan filtrera resultaten för en viss kund som tillhör återförsäljaren.                                                      |
| **användar-id**            | **guid** | N        | Värdet är ett GUID-formaterat **användar-ID** som tillhör ett enda användarkonto.                                                                                                                            |
| **roll-id**            | **guid** | N        | Värdet är ett GUID-formaterat **roll-ID** som tillhör en typ av roll. Du kan hämta dessa ID:er genom att fråga alla katalogroller för en kund, för alla användarkonton. (Det andra scenariot ovan). |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

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

Om det lyckas returnerar den här metoden en lista över de roller som är associerade med det angivna användarkontot.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder.](error-codes.md)

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
