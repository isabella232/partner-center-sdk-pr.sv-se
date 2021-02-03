---
title: Hämta en lista över tillgängliga för en SKU (efter land)
description: 'Så här hämtar du en samling tillgänglighet för den angivna produkten och SKU: n per kund land.'
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: b97a4ce85b5edd9de1301a577988f8c54096ebeb
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769123"
---
# <a name="get-a-list-of-availabilities-for-a-sku-by-country"></a>Hämta en lista över tillgängliga för en SKU (efter land)

**Gäller för:**

- Partnercenter

Den här artikeln beskriver hur du hämtar en samling tillgänglighet i ett visst land för en angiven produkt och SKU.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.

- Ett produkt-ID.

- Ett SKU-ID.

- Ett land.

## <a name="c"></a>C\#

Hämta listan över [tillgänglighet](product-resources.md#availability) för en [SKU](product-resources.md#sku):

1. Följ stegen i [Hämta ett SKU efter ID](get-a-sku-by-id.md) för att hämta gränssnittet för en speciell SKU: s åtgärder.

2. Välj egenskapen **tillgänglighet** från SKU-gränssnittet för att hämta ett gränssnitt med åtgärder för tillgänglighet.

3. Valfritt Använd metoden **ByTargetSegment ()** för att filtrera tillgänglighet efter mål segment.

4. Anropa **Get ()** eller **GetAsync ()** för att hämta en samling av tillgänglighet för denna SKU.

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

### <a name="request-syntax"></a>Syntax för begäran

| Metod  | URI för förfrågan                                                                                                                              |
|---------|------------------------------------------------------------------------------------------------------------------------------------------|
| **TA** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Products/{Product-ID}/SKUs/{SKU-ID}/availabilities? land = {Country-code} &targetSegment = {Target-segment} http/1.1     |

### <a name="uri-parameters"></a>URI-parametrar

Använd följande sökväg och frågeparametrar för att hämta en lista över tillgänglighet för en SKU.

| Namn                   | Typ     | Obligatorisk | Beskrivning                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| produkt-ID             | sträng   | Yes      | En sträng som identifierar produkten.                           |
| SKU-ID                 | sträng   | Yes      | En sträng som identifierar SKU: n.                               |
| landskod           | sträng   | Yes      | Ett land/region-ID.                                            |
| mål segment         | sträng   | No       | En sträng som identifierar det mål segment som används för filtrering. |
| reservationScope | sträng   | No | När du frågar efter en lista över tillgänglighet för en Azure reservations-SKU, anger `reservationScope=AzurePlan` du för att hämta en lista över tillgänglighet som är tillämpliga på AzurePlan. Undanta den här parametern för att hämta en lista över tillgänglighet som är tillämpliga på Microsoft Azure (MS-AZR-0145P)-prenumerationer.  |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-examples"></a>Exempel på begäran

#### <a name="availabilities-for-sku-by-country"></a>Tillgänglighet för SKU efter land

Följ det här exemplet för att hämta en lista över tillgänglighet för en specifik SKU efter land:

```http
GET http:// api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 70324727-62d8-4195-8f99-70ea25058d02
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58
```

#### <a name="availabilities-for-vm-reservations-azure-plan"></a>Tillgänglighet för VM-reservationer (Azure-plan)

Följ det här exemplet för att hämta en lista över tillgänglighet efter land för Azure VM reservation SKU: er. Det här exemplet avser SKU: er som gäller för Azure-planer:

```http
GET https://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="availabilities-for-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>Tillgänglighet för VM-reservationer för Microsoft Azure (MS-AZR-0145P)-prenumerationer

Följ det här exemplet för att hämta en lista över tillgänglighet efter land för Azure VM-reservationer som är tillämpliga på Microsoft Azure (MS-AZR-0145P)-prenumerationer.

```http
GET https://api.partnercenter.microsoft.com/v1/productsDZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureAzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a>REST-svar

Om det lyckas innehåller svars texten en samling [**tillgänglighets**](product-resources.md#availability) resurser.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [fel koder för partner Center](error-codes.md).

Den här metoden returnerar följande fel koder:

| HTTP-statuskod     | Felkod   | Description                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 403                  | 400030       | Åtkomst till den begärda **targetSegment** är inte tillåten.                                                     |

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
