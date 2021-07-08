---
title: Hämta en lista över erbjudandekategorier efter marknad
description: Lär dig hur du hämtar en samling som innehåller alla erbjudandekategorier i ett visst land/en viss region och språk för alla Microsoft-moln.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: e699355f07dda3941eafed32f5f635d94000abd1
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874286"
---
# <a name="get-a-list-of-offer-categories-by-market"></a>Hämta en lista över erbjudandekategorier efter marknad

**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Den här artikeln beskriver hur du hämtar en samling som innehåller alla erbjudandekategorier i ett visst land/region och språk.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.

## <a name="c"></a>C\#

Så här hämtar du en lista över erbjudandekategorier i ett visst land/region och språk:

1. Använd din [**IAggregatePartner.Operations-samling**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) för att anropa [**metoden With()**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner.with) i en viss kontext.

2. Kontrollera egenskapen [**OfferCategories**](/dotnet/api/microsoft.store.partnercenter.ipartner.offercategories) för det resulterande objektet.

``` csharp
// IAggregatePartner partnerOperations;

ResourceCollection<OfferCategory> offerCategoryResults = partnerOperations.With(RequestContextFactory.Instance.Create()).OfferCategories.ByCountry("US").Get();
```

Ett exempel finns i följande:

- Exempel: [Konsoltestapp](console-test-app.md)
- Project: **PartnerSDK.FeatureSample**
- Klass: **PartnerSDK.FeatureSample**

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod  | URI för förfrågan                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| **Få** | [*{baseURL}*](partner-center-rest-urls.md)/v1/offercategories?country={country-id} HTTP/1.1 |

#### <a name="uri-parameter"></a>URI-parameter

I den här tabellen visas de frågeparametrar som krävs för att hämta erbjudandekategorierna.

| Namn           | Typ       | Obligatorisk | Beskrivning            |
|----------------|------------|----------|------------------------|
| **lands-id** | **sträng** | Y        | Land/region-ID. |

### <a name="request-headers"></a>Begärandehuvuden

Ett **språk-ID formaterat** som en sträng krävs.

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/v1/offercategories?country=<country-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fb54bd5-a4c3-4fac-955f-9b6e3436d606
MS-CorrelationId: 47882653-eaed-4a2e-a552-1070a3fa1089
X-Locale: <locale-id>
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden en samling **OfferCategory-resurser** i svarstexten.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder.](error-codes.md)

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Length: 1184
Content-Type: application/json
MS-CorrelationId: 47882653-eaed-4a2e-a552-1070a3fa1089
MS-RequestId: 4fb54bd5-a4c3-4fac-955f-9b6e3436d606
Date: Thu, 26 Nov 2015 00:07:10 GMT

{
    "totalCount": 4,
    "items": [{
        "id": "Enterprise_Key",
        "name": "Enterprise",
        "rank": 20,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "SmallBusiness_Key",
        "name": "SmallBusiness",
        "rank": 30,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "Government_Key",
        "name": "Government",
        "rank": 40,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "Internal_Key",
        "name": "Internal",
        "rank": 100,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}
```
