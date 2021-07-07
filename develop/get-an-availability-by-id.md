---
title: Hämta tillgängligheten efter ID
description: Hämtar tillgängligheten för den angivna produkten och SKU:n med hjälp av ett tillgänglighets-ID.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: c31bc12d8d484cc8042f36aa865145600d9e6738
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760206"
---
# <a name="get-the-availability-by-id"></a>Hämta tillgängligheten efter ID

Hämtar tillgängligheten för den angivna produkten och SKU:n med hjälp av ett tillgänglighets-ID.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.

- Ett produkt-ID.

- Ett SKU-ID.

- Ett tillgänglighets-ID.

## <a name="c"></a>C\#

Om du vill [](product-resources.md#availability)ha information om en specifik tillgänglighet börjar du med att följa stegen i Hämta en [SKU](get-a-sku-by-id.md) efter ID för att hämta gränssnittet för en [specifik SKU:ns](product-resources.md#sku) åtgärder. Från det resulterande gränssnittet väljer du **egenskapen Availabilities (Tillgänglighet)** för att hämta ett gränssnitt med tillgängliga åtgärder för Tillgänglighet. Därefter skickar du tillgänglighets-ID:t till **metoden ById()** för att hämta åtgärderna för den specifika tillgängligheten och anropar **sedan Get()** eller **GetAsync()** för att hämta tillgänglighetsinformationen.

```csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId;
string skuId;
string availabilityId;

// Get the availability details.
var availability = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.ById(availabilityId).Get();
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Om du vill [](product-resources.md#availability)ha information om en specifik tillgänglighet börjar du med att följa stegen i Hämta en [SKU](get-a-sku-by-id.md) efter ID för att hämta gränssnittet för en [specifik SKU:ns](product-resources.md#sku) åtgärder. Från det resulterande gränssnittet väljer du funktionen **getAvailabilities** för att hämta ett gränssnitt med tillgängliga åtgärder för tillgänglighet. Därefter skickar du tillgänglighets-ID:t till **funktionen byId()** för att hämta åtgärderna för den specifika tillgängligheten och anropar **sedan funktionen get()** för att hämta tillgänglighetsinformationen.

```java
IAggregatePartner partnerOperations;
String countryCode;
String productId;
String skuId;
String availabilityId;

// Get the availability details.
Availability availability = partnerOperations.getProducts().byCountry(countryCode).byId(productId).getSkus().byId(skuId).getAvailabilities().byId(availabilityId).get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Om du vill [](product-resources.md#availability)ha information om en specifik tillgänglighet kör du [**parametrarna Get-PartnerProductAvailability**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductAvailability.md) och **availabilityId,** **CountryCode,** **ProductId** och **SkuId** för att hämta tillgänglighetsinformationen.

```powershell
Get-PartnerProductAvailability -Product $productId -SkuId $skuId -AvailabilityId $availabilityId
```

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod  | URI för förfrågan |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Få** | [*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}/availabilities/{availability-id}?country={country-code} HTTP/1.1         |

### <a name="uri-parameter"></a>URI-parameter

Använd följande sökväg och frågeparametrar för att få en specifik tillgänglighet med hjälp av ett tillgänglighets-ID.

| Namn                   | Typ     | Obligatorisk | Beskrivning                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| produkt-id             | sträng   | Ja      | En GUID-formaterad sträng som identifierar produkten.            |
| sku-id                 | sträng   | Ja      | En GUID-formaterad sträng som identifierar SKU:n.                |
| tillgänglighets-id        | sträng   | Ja      | En GUID-formaterad sträng som identifierar tillgängligheten.       |
| landskod           | sträng   | Ja      | Ett lands-/regions-ID.                                            |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-example"></a>Exempel på begäran

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities/DZH318XZXPHL?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 2e12a576-ded5-437e-a5ec-dbfbcbd1624c
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST-svar

Om det lyckas innehåller svarstexten en [tillgänglighetsresurs.](product-resources.md#availability)

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder i Partnercenter.](error-codes.md)

Den här metoden returnerar följande felkoder:

| HTTP-statuskod     | Felkod   | Beskrivning                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 404                  | 400013       | Det gick inte att hitta produkten.                                                                                    |
| 404                  | 400018       | SKU hittades inte.                                                                                        |
| 404                  | 400019       | Det går inte att hitta tillgängligheten.                                                                                   |

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58,83b644b5-e54a-4bdc-b354-f96c525b3c58
MS-RequestId: 2e12a576-ded5-437e-a5ec-dbfbcbd1624c,2e12a576-ded5-437e-a5ec-dbfbcbd1624c
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTNRXHNrdXNcMDAwMVxhdmFpbGFiaWxpdGllc1xEWkgzMThaMEhNS1E=?=
X-Powered-By: ASP.NET
Date: Wed, 14 Mar 2018 22:19:43 GMT
Content-Length: 440

{
    "id": "DZH318XZXPHL",
    "productId": "DZH318Z0BQ3Q",
    "skuId": "0001",
    "catalogItemId": "DZH318Z0BQ3Q:0001:DZH318XZXPHL",
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
            "uri": "/products/DZH318Z0BQ3Q/skus/0001/availabilities/DZH318XZXPHL?country=US",
            "method": "GET",
            "headers": []
        }
    }
}
```
