---
title: Verifiera en prenumeration för migrering
description: Så här kontrollerar du om en prenumeration är berättigad till migrering.
ms.date: 10/04/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c8d2ae596901a45a794230c79cfb54815963e300
ms.sourcegitcommit: 856b0baa4824960e13ee9672817a2d2e713fdf43
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/05/2021
ms.locfileid: "129528728"
---
# <a name="validate-a-subscription-for-migration"></a>Verifiera en prenumeration för migrering

**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Så här validerar du en prenumeration för migrering till New Commerce Experience

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md) Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard) Välj **CSP** på Menyn i Partnercenter följt av **Kunder.** Välj kunden i kundlistan och välj sedan **Konto.** På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.** Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).

- Ett aktuellt prenumerations-ID

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod  | URI för förfrågan                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
|**INLÄGG** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/migrations/newcommerce/validate HTTP/1.1  |

### <a name="uri-parameter"></a>URI-parameter

I den här tabellen visas de frågeparametrar som krävs för att verifiera en prenumeration för migrering.

| Namn               | Typ   | Obligatorisk | Beskrivning                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| kund-klient-id | sträng | Yes      | En GUID-formaterad sträng som identifierar kunden. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

I den här tabellen beskrivs [prenumerationsegenskaperna](subscription-resources.md) i begärandetexten.

| Egenskap              | Typ             | Obligatorisk        | Beskrivning |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| currentSubscriptionId | sträng           | Yes             | Ett prenumerations-ID som anger vilken prenumeration som kräver validering för migrering.            |

### <a name="request-example"></a>Exempel på begäran

```http
"currentSubscriptionId" : "9beb6319-6889-4d28-a155-68ca9c783842"
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden ett "isEligible"-booleskt värde i svarstexten som anger om den aktuella prenumerationen är berättigad till migrering till ny handel.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)

### <a name="response-examples"></a>Svarsexempel

```http
1. 
    {
        "currentSubscriptionId": "9beb6319-6889-4d28-a155-68ca9c783842",
        "isEligible": false,
        "errors": [
            {
                "code": 5,
                "description": "Subscription cannot be migrated to New Commerce because the equivalent offer is not yet available in New Commerce",
            }
        ]
    }

2. 
    {
        "currentSubscriptionId": "9beb6319-6889-4d28-a155-68ca9c783842",
        "isEligible": true,
    "catalogItemId": "CFQ7TTC0LF8S:0002:CFQ7TTC0KSVV",
    }
```
