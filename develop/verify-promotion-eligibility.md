---
title: Verifiera berättigande till befordran
description: Verifierar om en kundtransaktion är berättigad för en viss befordran.
ms.date: 02/23/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: ad3346ddca0438c0011e2c6fd03c3ec00b1a1fe3
ms.sourcegitcommit: 7be22de808a10fa2d05577d6497086c8ca3f678a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/24/2021
ms.locfileid: "128716009"
---
# <a name="verify-promotion-eligibility"></a>Verifiera berättigande till befordran

**Gäller för**

- Partnercenter

**Lämpliga roller**

- Global administratör
- Administratörsagent

> [!Note] 
> Nya handelsändringar är för närvarande endast tillgängliga för partner som ingår i den tekniska förhandsversionen av Microsoft 365 och Dynamics 365.

Parters kan kontrollera om en kundtransaktion är berättigad för en viss befordran. Den här metoden *returnerar* True om kundtransaktionen är berättigad för en viss befordran. Partner kan verifiera berättigandet innan en transaktion skickas för att säkerställa att befordran tillämpas.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md) Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.

- Berättigande omfattar den produkt-SKU-tillgänglighet som köps, det kampanj-ID som utvärderas, kvantitet, giltighetstid och faktureringsperiod för transaktionen.

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod   | URI för förfrågan                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| **INLÄGG**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customerId}/promotionEligibilities HTTP/1.1 |

### <a name="uri-parameter"></a>URI-parameter

Använd följande frågeparametrar för att returnera tillgängliga kampanjer.

| Namn                    | Typ     | Obligatorisk | Beskrivning                                       |
|-------------------------|----------|----------|---------------------------------------------------|
| **Customerid**  | **sträng** | Y        | Värdet är ett GUID-formaterat kundklient-id, vilket är en identifierare som gör att du kan ange en kund.          |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

Brödtext innehåller en samling PromotionEligibilitiesRequestItems. I den här tabellen beskrivs egenskaperna för [en PromotionEligibilitiesRequestItem](promotion-resources.md#promotioneligibilitiesrequestitem).

| Egenskap        | Typ             | Obligatorisk        | Beskrivning                                                                                               |
|-----------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| catalogItemId   | sträng           | Yes             | Katalogobjektets identifierare.                         |
| quantity        | int | Yes        | Antalet licenser eller instanser.                 |
| termDuration    | DateTime         | Yes             | En ISO 8601-representation av termens varaktighet. De aktuella värdena som stöds är P1M (en månad), P1Y (ett år) och P3Y (tre år).   |
| billingCycle    | sträng | Yes     | Det värde som anger typen av faktureringsperiod.   |
| promotionId     | sträng           | Yes             | Identifierare för befordransobjekt.                       | 

### <a name="request-example"></a>Exempel på begäran

```http
POST https://api.partnercenter.microsoft.com/v1/customers/46632f71-f052-4384-8f84-4cdb6c12c2a1/promotionEligibilities HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US

{
    "items": [
        {
            "catalogItemId": "CFQ7TTC0KZ59:0001:CFQ7TTC0KZ59",
            "quantity": 1,
            "termDuration": "P1Y",
            "billingCycle": "Monthly",
            "promotionId": " CFQ7TTC0HL8W:0001:CFQ7TTC0K59M"
        }
    ]
}

```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden en samling berättiganderesultat.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad och mer felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och fler parametrar. En fullständig lista finns i [Felkoder.](error-codes.md)

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Length: 138
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
Date: Fri, 26 Feb 2021 20:42:26 GMT

{
    "totalCount": 1,
    "items": [
        {
            "catalogItemId": "CFQ7TTC0KZ59:0001:CFQ7TTC0KZ59",
            "quantity": 1,
            "termDuration": "P1Y",
            "billingCycle": "Monthly",
            "eligibilities": [
                {
                    "promotionId": "CFQ9TTC0HH4R:0001:CFQ8HGC0K77G",
                    "isEligible": false,
                    "errors": [
                        {
                            "type": "SeatCount",
                            "minRequiredSeats": 25,
                            "maxRequiredSeats": 500
                        },
                        {
                            "type": "Term",
                            "eligibleTerms": [
                                {
                                    "duration": "P3Y",
                                    "billingCycle": "Monthly"
                                }
                            ]
                        },
                        {
                            "type": "FirstPurchase"
                        }
                    ]
                }
            ],
            "attributes": {
                "objectType": "PromotionEligibilities"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

