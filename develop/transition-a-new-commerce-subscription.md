---
title: Övergå från en ny handelsprenumeration
description: Uppgraderar en kunds nya commmerce-prenumeration till en angiven målprenumeration.
ms.date: 02/23/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: 2bbf2f63cec416e4d4b4a671d2e2b2914b5f5713
ms.sourcegitcommit: e1db965e8c7b4fe3aaa0ecd6cefea61973ca2232
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/03/2021
ms.locfileid: "123457323"
---
# <a name="transition-a-new-commerce-subscription"></a>Övergå från en ny handelsprenumeration

**Gäller för:** Partnercenter

**Lämpliga roller**

- Global administratör
- Administratörsagent

> [!Note] 
> Nya handelsändringar är för närvarande endast tillgängliga för partner som ingår i den tekniska förhandsversionen av den nya handelsupplevelsen M365/D365.

Används för att uppgradera en kunds nya commmerce-prenumeration till en målprenumeration. Hämta först berättigade övergångar för att få SKU:erna tillgängliga för uppgradering. Sedan efter övergången för att köra övergången. Dessa metoder stöder både traditionella och nya prenumerationer på handelskällor.  

## <a name="get-transition-eligibilities"></a>Hämta övergångseligi-

Returnerar en lista över berättigade övergångar för en viss kund, prenumeration och begärd typ.

### <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard) Välj **CSP** på Menyn i Partnercenter följt av **Kunder**. Välj kunden i kundlistan och välj sedan **Konto.** På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.** Microsoft-ID:t är samma som kund-ID :t ( `customer-tenant-id` ).

- Ett prenumerations-ID för den första prenumerationen.

### <a name="rest-request"></a>REST-begäran

#### <a name="request-syntax"></a>Begärandesyntax

| Metod   | URI för förfrågan                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| **FÅ**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-Id}/transitionEligibilities?eligibilityType={immediate, scheduled} HTTP/1.1 |

#### <a name="uri-parameter"></a>URI-parameter

Använd följande frågeparametrar för att returnera berättigade övergångar.

| Namn                    | Typ     | Obligatorisk | Beskrivning                                       |
|-------------------------|----------|----------|---------------------------------------------------|
| **kund-klient-id**  | **guid** | Y        | Ett GUID som motsvarar kundens klientorganisation.             |
| **subscriptoin-Id** | **guid** | Y        | Ett GUID som motsvarar den första prenumerationen. |
| **eligibilityType**       | **sträng** | Y        | Beskriver när transtion ska köras, kan vara omedelbara eller schemalagda.  |

#### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

#### <a name="request-body"></a>Begärandetext

Ingen

#### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-Id}/transitionEligibilities?eligibilityType=immediate HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US
```

### <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden en lista över berättigade övergångar i svarstexten.

#### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder.](error-codes.md)

#### <a name="eligibility-errors"></a>Berättigandefel

Felbeskrivningar och innebörd.

| Felbeskrivning | Innebörd  |
|-------------------------|----------|
|Prenumerationen kan inte övergå – källprenumerationen är inte aktiv. | Ursprunglig understatus är inte aktiv |
|Prenumerationen kan inte övergå – källprenumerationen har inte etablerats ännu. | Ursprunglig del av FulfillmentState lyckas inte |
|Övergångstypen är inte kompatibel – AzureAD-prenumerationsmappning krävs. | LegacyCannotConvertSubscriptionId-fel vid anrop av GetSubscriptionUpgradeConflicts |
|Övergångstypen är inte kompatibel – det finns motstridiga prenumerationer för licensöverföring. | Om en AAD-tjänst har prenumerations-ID:n från en annan prenumeration lägger du till den i konfliktlistan (inklusive inköp som görs med ett äldre eller modernt inköpsflöde) |

#### <a name="response-example"></a>Exempel på svar

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
            "catalogItemId": "CFQ7TTC0KZCR:0001:CFQ7TTC0K71H",
            "title": "Microsoft 365 E5 Test Sku Title",
            "description": "Microsoft 365 E5 Test Sku Description",
            "quantity": 1,
            "eligibilities": [
{
                    "isEligible": true,
                    "transitionType": "transition_only",
                    "errors": []
                },
                
{
                    "isEligible": false,
                    "transitionType": "transition_with_license_transfer",
                    "errors": [
                        {
                            "code": 3,
                            "description": "Subscription cannot be transitioned because there are conflicting services."
                        }
                    ]
                }
            ],
            "attributes": {
                "objectType": "TransitionEligibility"
            }
        },
        {
            "catalogItemId": "CFQ7TTC0L4M3:0001:CFQ7TTC0K78T",
            "title": "Business Premium Test Sku Title",
            "description": "Business Premium Test Sku Description",
            "quantity": 1,
            "eligibilities": [
                {
                    "isEligible": false,
                    "transitionType": "transition_with_license_transfer",
                    "errors": [
                        {
                            "code": 3,
                            "description": "Subscription cannot be transitioned because there are conflicting services."
                        }
                    ]
                }
            ],
            "attributes": {
                "objectType": "TransitionEligibility"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

## <a name="post-transition"></a>Efter övergången

Publicerar en övergångsbegäran för en viss kund och prenumeration. Returnerar övergången med intial status.

### <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard) Välj **CSP** på Menyn i Partnercenter följt av **Kunder**. Välj kunden i kundlistan och välj sedan **Konto.** På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.** Microsoft-ID:t är samma som kund-ID :t ( `customer-tenant-id` ).

- Ett prenumerations-ID för den första prenumerationen.

### <a name="rest-request"></a>REST-begäran

#### <a name="request-syntax"></a>Begärandesyntax

| Metod   | URI för förfrågan                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| **INLÄGG**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscriptoin-Id}/transitions HTTP/1.1 |


#### <a name="uri-parameter"></a>URI-parameter

Använd följande frågeparametrar för att köra en övergång.

| Namn                    | Typ     | Obligatorisk | Beskrivning                                       |
|-------------------------|----------|----------|---------------------------------------------------|
| **kund-klient-id**  | **guid** | Y        | Ett GUID som motsvarar kundens klientorganisation.             |
| **subscriptoin-Id** | **guid** | Y        | Ett GUID som motsvarar den första prenumerationen. |

#### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

#### <a name="request-body"></a>Begärandetext

En fullständig **övergångsresurs** krävs i begärandetexten.

#### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customerId}/subscriptions/{subscriptionId}/transitions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US

{
    "toCatalogItemId": "CFQ7TTC0KZ59:0001:CFQ7TTC0KZ59",
    "quantity": 5,
    "transitionType": "transition_with_license_transfer",
    "events": []
}
```

### <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden en övergångsresurs med de första händelserna.

#### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder.](error-codes.md)

#### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Length: 138
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
Date: Fri, 26 Feb 2021 20:42:26 GMT

{
    "FromCatalogItemId": "CFQ7TTC0LDPB:0001:CFQ7TTC0LGNT",
    "ToCatalogItemId": "CFQ7TTC0LF8S:0001:CFQ7TTC0K9G9",
    "quantity": 1,
    "transitionType": "transition_with_license_transfer",
    "Events": [
        {
            "name": "Conversion",
            "status": "Started ",
            "timestamp": "2021-01-08T18:01:14.7488618Z",
            "attributes":
            {
                "objectType": "TransitionEvent"
            }
        }
    ],
    "attributes":
    {
        "objectType": "Transition"
    }
}
```
