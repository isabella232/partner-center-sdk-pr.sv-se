---
title: Hämta status för prenumerationsregistrering
description: Hämta status för en prenumeration som har registrerats för användning med Azure Reserved VM Instances.
ms.date: 03/19/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e06cf8a450d6c281f7f83a68c899d1e5b29e9855
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769849"
---
# <a name="get-subscription-registration-status"></a>Hämta status för prenumerationsregistrering

**Gäller för**

- Partnercenter

Hämta status för prenumerations registrering för en kund prenumeration som har Aktiver ATS för inköps Azure Reserved VM Instances.

Om du vill köpa en virtuell Azure-reserverade VM-instans med hjälp av Partner Center API måste du ha minst en befintlig CSP Azure-prenumeration. Med metoden [Registrera en prenumeration](register-a-subscription.md) kan du registrera din befintliga CSP Azure-prenumeration, så att den kan köpa Azure Reserved VM instances. Med den här metoden kan du hämta statusen för den registreringen.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).

- Ett prenumerations-ID.

## <a name="c"></a>C\#

Om du vill hämta registrerings status för en prenumeration börjar du med att använda metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: t för att identifiera kunden. Sedan kan du hämta ett gränssnitt till prenumerations åtgärder genom att anropa metoden [**Subscription. ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) med prenumerations-ID: t för att identifiera prenumerationen. Använd sedan egenskapen RegistrationStatus för att hämta ett gränssnitt till den aktuella prenumerationens registrerings status åtgärder och anropa metoden **Get** eller **GetAsync** för att hämta **SubscriptionRegistrationStatus** -objektet.

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve a subscription's registration status details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).RegistrationStatus.Get();
```

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod    | URI för förfrågan                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| **TA**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Subscriptions/{Subscription-ID}/registrationstatus http/1.1 |

### <a name="uri-parameters"></a>URI-parametrar

Använd följande Sök vägs parametrar för att identifiera kunden och prenumerationen.

| Namn                    | Typ       | Obligatorisk | Beskrivning                                                   |
|-------------------------|------------|----------|---------------------------------------------------------------|
| kund-ID             | sträng     | Yes      | En GUID-formaterad sträng som identifierar kunden.         |
| prenumerations-ID         | sträng     | Yes      | En GUID-formaterad sträng som identifierar prenumerationen.     |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-id>/subscriptions/<subscription-id>/registrationstatus HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST-svar

Om det lyckas innehåller svars texten en [SubscriptionRegistrationStatus](subscription-resources.md#subscriptionregistrationstatus) -resurs.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [felkoder](error-codes.md).

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
MS-CV: InswEQre402koceL.0
MS-ServerId: 030020344

{
    "subscriptionId":"<subscription-id>",
    "status":"NotRegistered",
    "attributes":{
        "objectType":"SubscriptionRegistrationStatus"
    }
}
```
