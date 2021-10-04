---
title: Uppdateringar av överage för en viss kund
description: Uppdaterar över tiden för en viss kund.
ms.date: 10/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: 58590a1882cfe94ddd9779f9e9f766f3e62cffd6
ms.sourcegitcommit: 856c14b6b351697e3b3d33f1fe376adbb80517c5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/02/2021
ms.locfileid: "129383455"
---
# <a name="update-overage"></a>Uppdatera överage

**Gäller för**

- Partnercenter

**Lämpliga roller**

- Global administratör
- Administratörsagent

> [!Note] 
> Nya handelsändringar är för närvarande endast tillgängliga för partner som ingår i den tekniska förhandsversionen Microsoft 365/Dynamics 365.

Används för att ange överförbrukning för en viss kund till en förbrukningsprenumeration. Kan också användas för att ta bort översättning genom att ställa in den på false. Överanvändning gör det möjligt för en kund att fortsätta använda tjänster om de använder tjänsten utöver de angivna gränserna. Överförbrukning definierar förbrukningsprenumerationens överförbrukning som betalas per användning kommer att ackumuleras.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard) Välj **CSP** på Menyn i Partnercenter följt av **Kunder**. Välj kunden i kundlistan och välj sedan **Konto.** På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.** Microsoft-ID:t är samma som kund-ID :t ( `customer-tenant-id` ).

- Ett prenumerations-ID för den över övergånde prenumerationen.

## <a name="rest-request"></a>REST-begäran
[PUT] /customers/{customer-tenant-id}/subscriptions/overage
### <a name="request-syntax"></a>Begärandesyntax

| Metod   | URI för förfrågan                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| **FÅ**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/overage HTTP/1.1 |

### <a name="uri-parameter"></a>URI-parameter

Använd följande frågeparametrar för att returnera en kunds överanvändning.

| Namn                    | Typ     | Obligatorisk | Beskrivning                                       |
|-------------------------|----------|----------|---------------------------------------------------|
| **kund-klient-id**  | **guid** | Y        | Ett GUID som motsvarar kundens klientorganisation.             |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext


| Namn                    | Typ     | Beskrivning                                       |
|-------------------------|----------|---------------------------------------------------|
| **azureEntitlementId**  | **guid** | Ett GUID som definierar förbrukningsprenumerationen för överförbrukning.             |
| **partnerId**  | **guid** | MPN-ID för en indirekt återförsäljare. Gäller endast för en modell med två nivåer (indirekt provider).            |

| **overageEnabled**   |  **bool** | Definierar om överförbrukning har aktiverats för en viss förbrukningsprenumeration.             |


### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/overage HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US

{
    "azureEntitlementId": "ea1c26b7-8c99-42bb-ba7d-c535831fae8e",
    "partnerId": "5357563",
    "overageEnabled": true
}

```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden överdata för en kund.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder.](error-codes.md)

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Length: 138
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
Date: Fri, 26 Feb 2021 20:42:26 GMT

{
    "azureEntitlementId": "ea1c26b7-8c99-42bb-ba7d-c535831fae8e",
    "partnerId": "5357563",
    "type": "PhoneServices",
    "overageEnabled": true,
    "links": {
        "overage": {
            "uri": "/customers/f62cf10b-8f76-4fc4-9774-c5291f8faf86/subscriptions/overage",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Overage"
    }
}
```
