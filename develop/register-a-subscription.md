---
title: Registrera en prenumeration
description: Registrera en befintlig prenumeration så att den är aktiverad för att beställa Azure-reservationer.
ms.date: 07/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4ea2183ab0c2367c7772bdf40b5988c2b7eff7c539686760332bec4addda8bbe
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997200"
---
# <a name="register-a-subscription"></a>Registrera en prenumeration

Registrera en befintlig [prenumeration](subscription-resources.md) så att den är aktiverad för att beställa Azure-reservationer.

Om du vill köpa en Azure-reservation måste du ha minst en befintlig CSP Azure-prenumeration. Med den här metoden kan du registrera din befintliga CSP Azure-prenumeration, vilket gör det möjligt att köpa Azure-reservationer.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md) Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard) Välj **CSP** på Menyn i Partnercenter följt av **Kunder.** Välj kunden i kundlistan och välj sedan **Konto.** På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.** Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).

- Ett prenumerations-ID.

## <a name="c"></a>C\#

Om du vill registrera en kunds prenumeration hämtar du ett gränssnitt för prenumerationsåtgärder genom att anropa metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att identifiera kunden. Anropa sedan metoden [**Subscription.ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) med prenumerations-ID:t för att identifiera prenumerationen som du registrerar.

Anropa slutligen metoden **Registration.Register()** för att registrera prenumerationen och hämta en URI som kan användas för att hämta prenumerationens registreringsstatus. Mer information finns i Hämta [prenumerationsregistreringsstatus](get-subscription-registration-status.md).

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve the subscription registration details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).Registration.Register();
```

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod    | URI för förfrågan                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| **Inlägg**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrations HTTP/1.1 |

### <a name="uri-parameters"></a>URI-parametrar

Använd följande sökvägsparametrar för att identifiera kunden och prenumerationen.

| Namn                    | Typ       | Obligatorisk | Beskrivning                                                   |
|-------------------------|------------|----------|---------------------------------------------------------------|
| kund-ID             | sträng     | Yes      | En GUID-formaterad sträng som identifierar kunden.         |
| prenumerations-id         | sträng     | Yes      | En GUID-formaterad sträng som identifierar prenumerationen.     |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

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

Om det lyckas innehåller svaret ett **Location-huvud** med en URI som kan användas för att hämta prenumerationens registreringsstatus. Spara den här URI:en för användning med andra relaterade REST API:er. Ett exempel på hur du hämtar statusen finns i [Hämta prenumerationsregistreringsstatus](get-subscription-registration-status.md).

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder.](error-codes.md)

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
