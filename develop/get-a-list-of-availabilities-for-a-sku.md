---
title: Hämta en lista över tillgängliga för en SKU (efter land)
description: Så här hämtar du en samling tillgänglighet för den angivna produkten och SKU:n efter kundland.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 89ffa4156490bd321055f12a1c8c385800b65d8d9e5a460df0cc41edda5c1a27
ms.sourcegitcommit: f5e2d3e2ad5447b99d339662e00b2ac3a03d7d04
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/10/2021
ms.locfileid: "116998507"
---
# <a name="get-a-list-of-availabilities-for-a-sku-by-country"></a>Hämta en lista över tillgängliga för en SKU (efter land)

Den här artikeln beskriver hur du hämtar en samling tillgänglighet i ett visst land för en angiven produkt och SKU.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md) Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.

- En produktidentifierare.

- En SKU-identifierare.

- Ett land.

## <a name="c"></a>C\#

Hämta listan över [tillgänglighet för en](product-resources.md#availability) [SKU:](product-resources.md#sku)

1. Följ stegen i Hämta [en SKU efter ID för](get-a-sku-by-id.md) att hämta gränssnittet för en specifik SKU:s åtgärder.

2. Från SKU-gränssnittet väljer du **egenskapen Availabilities** (Tillgänglighet) för att hämta ett gränssnitt med åtgärderna för tillgänglighet.

3. (Valfritt) Använd metoden **ByTargetSegment()** för att filtrera tillgängligheten efter målsegment.

4. Anropa **Get()** eller **GetAsync()** för att hämta en samling tillgänglighet för denna SKU.

``` csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId;
string skuId;
string targetSegment;
string productIdForAzureReservation;
string skuIdForAzureReservation;

// Get the availabilities.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.Get();

// Get the availabilities, filtered by target segment.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.BySegment(targetSegment).Get();

// Get the availabilities for an Azure reservation product and sku which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions only.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.ById(skuIdForAzureReservation).Availabilities.ByReservationScope("AzurePlan").Get();

// Get the availabilities for an Azure reservation product and sku which are applicable to Azure plans only.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.ById(skuIdForAzureReservation).Availabilities.Get();

```

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod  | URI för förfrågan                                                                                                                              |
|---------|------------------------------------------------------------------------------------------------------------------------------------------|
| **Få** | [*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}/availabilities?country={country-code}&targetSegment={target-segment} HTTP/1.1     |

### <a name="uri-parameters"></a>URI-parametrar

Använd följande sökväg och frågeparametrar för att hämta en lista över tillgänglighet för en SKU.

| Namn                   | Typ     | Obligatorisk | Beskrivning                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| produkt-id             | sträng   | Yes      | En sträng som identifierar produkten.                           |
| sku-id                 | sträng   | Yes      | En sträng som identifierar SKU:n.                               |
| landskod           | sträng   | Yes      | Ett lands-/regions-ID.                                            |
| målsegment         | sträng   | No       | En sträng som identifierar målsegmentet som används för filtrering. |
| reservationScope | sträng   | No | När du frågar efter en lista över tillgänglighet för en Azure-reservations-SKU anger du för att hämta en lista över tillgänglighet som `reservationScope=AzurePlan` gäller för AzurePlan. Undanta den här parametern för att hämta en lista över tillgänglighet som gäller för Microsoft Azure-prenumerationer (MS-AZR-0145P).  |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-examples"></a>Exempel på begäran

#### <a name="availabilities-for-sku-by-country"></a>Tillgänglighet för SKU efter land

Följ det här exemplet för att hämta en lista över tillgänglighet för en viss SKU efter land:

```http
GET http:// api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 70324727-62d8-4195-8f99-70ea25058d02
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58
```

#### <a name="availabilities-for-vm-reservations-azure-plan"></a>Tillgänglighet för VM-reservationer (Azure-plan)

Följ det här exemplet för att hämta en lista över tillgänglighet per land för AZURE VM-reservations-SKU:er. Det här exemplet är för SKU:er som gäller för Azure-planer:

```http
GET https://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="availabilities-for-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>Tillgänglighet för VM-reservationer för Microsoft Azure prenumerationer (MS-AZR-0145P)

Följ det här exemplet för att hämta en lista över tillgänglighet per land för Azure VM-reservationer som gäller för Microsoft Azure-prenumerationer (MS-AZR-0145P).

```http
GET https://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureAzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a>REST-svar

Om det lyckas innehåller svarstexten en samling [**tillgänglighetsresurser.**](product-resources.md#availability)

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder i Partnercenter.](error-codes.md)

Den här metoden returnerar följande felkoder:

| HTTP-statuskod     | Felkod   | Description                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 403                  | 400030       | Åtkomst till det begärda **targetSegment** tillåts inte.                                                     |

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58,83b644b5-e54a-4bdc-b354-f96c525b3c58
MS-RequestId: 70324727-62d8-4195-8f99-70ea25058d02,70324727-62d8-4195-8f99-70ea25058d02
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTNRXHNrdXNcMDAwMVxhdmFpbGFiaWxpdGllcw==?=
X-Powered-By: ASP.NET
Date: Wed, 14 Mar 2018 22:19:37 GMT
Content-Length: 808

{
    "totalCount": 1,
    "items": [
        {
            "id": "DZH318XZXVNF",
            "productId": "DZH318Z0BQ3Q",
            "skuId": "0001",
            "catalogItemId": "DZH318Z0BQ3Q:0001:DZH318XZXVNF",
            "defaultCurrency": {
                "code": "USD",
                "symbol": "$"
            },
            "segment": "commercial",
            "country": "US",
            "isPurchasable": true,
            "isRenewable": false,
            "terms": [{
                "duration": "P1Y",
                "description": "1 Year Prepaid"
            }],
            "product": { ... },
            "sku": { ... },
            "links": {
                "self": {
                    "uri": "/products/DZH318Z0BQ3Q/skus/0001/availabilities/DZH318Z0HMKQ?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetSegment=commercial",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
