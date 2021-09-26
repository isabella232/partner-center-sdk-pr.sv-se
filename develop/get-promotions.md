---
title: Hämtar en lista över aktuella kampanjer för ett givet segment och en marknad
description: Hämtar en lista över aktuella kampanjer för ett givet segment och en marknad.
ms.date: 09/24/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: 0b9cc6ccdebbd641ab8b7dcd6cc5932c191d85ad
ms.sourcegitcommit: 7be22de808a10fa2d05577d6497086c8ca3f678a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/24/2021
ms.locfileid: "128716006"
---
# <a name="get-promotions"></a>Hämta kampanjer

**Gäller för**

- Partnercenter

**Lämpliga roller**

- Global administratör
- Administratörsagent

> [!Note] 
> Nya handelsändringar är för närvarande endast tillgängliga för partner som ingår i den tekniska förhandsversionen av Microsoft 365 och Dynamics 365.

Partner kan hämta en lista över aktiva nya handelskampanjer för en viss marknad (land) och segment. Den här metoden returnerar tillgängliga aktuella kampanjer baserat på tillgängliga start- och slutdatum för kampanjer.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md) Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.

- Segment representerar den typ av kund som kampanjerna är aktiverade för. Stöder för närvarande endast kommersiella.

- Land representerar de kundlandkampanjer som är tillgängliga för. Land representeras av en landskod med två tecken.

## <a name="rest-request"></a>REST-begäran
[GET] /v1/productpromotions?country={country-code}&segment={segment}

### <a name="request-syntax"></a>Begärandesyntax

| Metod   | URI för förfrågan                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| **FÅ**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/productpromotions?country={country-code}&segment={segment} HTTP/1.1 |

### <a name="uri-parameter"></a>URI-parameter

Använd följande frågeparametrar för att returnera tillgängliga kampanjer.

| Namn                    | Typ     | Obligatorisk | Beskrivning                                       |
|-------------------------|----------|----------|---------------------------------------------------|
| **Segment**  | **sträng** | Y        | En sträng som avgör vilka kampanjer som är tillgängliga för ett visst segment.           |
| **Land** | **sträng** | Y        | En landskod med två bokstäver som avgör vilka kundlandkampanjer som är tillgängliga för. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

Ingen

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/v1/productpromotions?country=US&segment=commercial HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden en lista över kampanjer.

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
    "totalCount": 2,
    "items": [
        {
            "id": "39NFJQT1PJQB:0001:39NFJQT1Q5KN",
            "name": "Visio Plan 1",
            "description": "Visio Plan 1",
            "startDate": "2021-09-23T00:00:00+00:00",
            "endDate": "2021-10-14T23:59:59+00:00",
            "properties": {
                "isAutoApplicable": true
            },
            "requiredProducts": [
                {
                    "productId": "CFQ7TTC0HD33",
                    "skuId": "0003",
                    "term": {
                        "duration": "P1Y",
                        "billingCycle": "Annual"
                    },
                    "pricingPolicies": [
                        {
                            "policyType": "PercentDiscount",
                            "value": "0.05"
                        }
                    ]
                }
            ]
        },
        {
            "id": "39NFJQT1PJQC:0001:39NFJQT1Q5KM",
            "name": "Vision Plan 1",
            "description": "Vision Plan 1",
            "startDate": "2021-09-23T00:00:00+00:00",
            "endDate": "2021-10-14T23:59:59+00:00",
            "properties": {
                "isAutoApplicable": true
            },
            "requiredProducts": [
                {
                    "productId": "CFQ7TTC0HD33",
                    "skuId": "0003",
                    "term": {
                        "duration": "P1Y",
                        "billingCycle": "Monthly"
                    },
                    "pricingPolicies": [
                        {
                            "policyType": "PercentDiscount",
                            "value": "0.167"
                        }
                    ]
                }
            ]
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
