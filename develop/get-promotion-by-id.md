---
title: Hämtar en enskild befordran
description: Hämtar en enskild befordran för ett visst uppflyttnings-ID och land.
ms.date: 09/23/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: 9ed9171cd7bbe8a6d5202deb7cc6111bb76ec923
ms.sourcegitcommit: 7be22de808a10fa2d05577d6497086c8ca3f678a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/24/2021
ms.locfileid: "128716015"
---
# <a name="get-promotion-by-id"></a>Hämta befordran efter ID

**Gäller för**

- Partnercenter

**Lämpliga roller**

- Global administratör
- Administratörsagent

> [!Note] 
> Nya handelsändringar är för närvarande endast tillgängliga för partner som ingår i den tekniska förhandsversionen av Microsoft 365 och Dynamics 365.

Partner kan få en enskild befordran för ett visst uppflyttnings-ID och land. Den här metoden returnerar kampanjdata och ignorerar start- och slutdatumen för befordran. Den här metoden används främst för avstämningsändamål för att hämta information om befordran även efter att befordran har upphört att gälla.



## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md) Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.

- Uppflyttnings-ID är en avgränsad uppsättning strängar som representerar en specifik befordran.

- Land representerar de kundlandkampanjer som är tillgängliga för. Land representeras av en landskod med två tecken.

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod   | URI för förfrågan                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| **FÅ**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/productpromotions/{promotion-id}?country={country-code HTTP/1.1 |

### <a name="uri-parameter"></a>URI-parameter

Använd följande frågeparametrar för att returnera tillgängliga kampanjer.

| Namn                    | Typ     | Obligatorisk | Beskrivning                                       |
|-------------------------|----------|----------|---------------------------------------------------|
| **promotion-id**  | **sträng** | Y        | En sträng som definierar befordran som ska hämtas.           |
| **Land** | **sträng** | Y        | En landskod med två bokstäver som avgör vilka kundlandkampanjer som är tillgängliga för. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

Ingen

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/v1/productpromotions/CFQ7TTC0HD33:0003:CFQ7TTC0K59M?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden en enda befordran.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad och mer felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder.](error-codes.md)

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Length: 138
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
Date: Fri, 24 Sep 2021 20:42:26 GMT

 
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
        }
```
