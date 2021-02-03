---
title: Registrera en prenumeration
description: Registrera en befintlig prenumeration så att den är aktive rad för att beställa Azure-reservationer.
ms.date: 07/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9a96bb350f22430c9fd7a1759e336cc9f3ca1939
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769651"
---
# <a name="register-a-subscription"></a>Registrera en prenumeration

**Gäller för**

- Partnercenter

Registrera en befintlig [prenumeration](subscription-resources.md) så att den är aktive rad för att beställa Azure-reservationer.

Om du vill köpa en Azure-reservation måste du ha minst en befintlig CSP Azure-prenumeration. Med den här metoden kan du registrera din befintliga CSP Azure-prenumeration, så att den kan köpa Azure-reservationer.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).

- Ett prenumerations-ID.

## <a name="c"></a>C\#

Om du vill registrera en kunds prenumeration hämtar du ett gränssnitt för prenumerations åtgärder genom att anropa metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: t för att identifiera kunden. Anropa sedan metoden [**Subscription. ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) med prenumerations-ID: t för att identifiera den prenumeration som du registrerar.

Anropa slutligen metoden **Registration. register ()** för att registrera prenumerationen och hämta en URI som kan användas för att hämta status för prenumerations registrering. Mer information finns i [Hämta status för prenumerations registrering](get-subscription-registration-status.md).

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve the subscription registration details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).Registration.Register();
```

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod    | URI för förfrågan                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| **EFTER**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Subscriptions/{Subscription-ID}/registrations http/1.1 |

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
POST https://api.partnercenter.microsoft.com/v1/customers/<customer-id>/subscriptions/<subscription-id>/registrations HTTP/1.1
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

Om det lyckas innehåller svaret ett **plats** huvud med en URI som kan användas för att hämta status för prenumerations registrering. Spara denna URI för användning med andra relaterade REST API: er. Ett exempel på hur du hämtar status finns i [Hämta status för prenumerations registrering](get-subscription-registration-status.md).

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [felkoder](error-codes.md).

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/<customer-id>/subscriptions/<subscription-id>/registrationstatus
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
```
