---
title: Hämta tillgänglighet efter ID
description: 'Hämtar tillgänglighet för den angivna produkten och SKU: n med hjälp av ett tillgänglighets-ID.'
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 824303d40e1dcb0405246c8e29562c4527d147fd
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768760"
---
# <a name="get-the-availability-by-id"></a>Hämta tillgänglighet efter ID

**Gäller för**

- Partnercenter

Hämtar tillgänglighet för den angivna produkten och SKU: n med hjälp av ett tillgänglighets-ID.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.

- Ett produkt-ID.

- ETT SKU-ID.

- Ett tillgänglighets-ID.

## <a name="c"></a>C\#

Om du vill ha information om en speciell [tillgänglighet](product-resources.md#availability)börjar du med att följa stegen i [Hämta en SKU efter ID](get-a-sku-by-id.md) för att hämta gränssnittet för en speciell [SKU: s](product-resources.md#sku) åtgärder. Från det resulterande gränssnittet väljer du egenskapen **tillgänglighet** för att hämta ett gränssnitt med tillgängliga åtgärder för tillgänglighet. Därefter skickar du tillgänglighets-ID: t till metoden **ById ()** för att hämta åtgärder för den aktuella tillgängligheten och anropa sedan **Get ()** eller **GetAsync ()** för att hämta tillgänglighets information.

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

Om du vill ha information om en speciell [tillgänglighet](product-resources.md#availability)börjar du med att följa stegen i [Hämta en SKU efter ID](get-a-sku-by-id.md) för att hämta gränssnittet för en speciell [SKU: s](product-resources.md#sku) åtgärder. Från det resulterande gränssnittet väljer du funktionen **getAvailabilities** för att hämta ett gränssnitt med tillgängliga åtgärder för tillgänglighet. Därefter skickar du tillgänglighets-ID: t till funktionen **byId ()** för att hämta åtgärder för den aktuella tillgängligheten och anropar sedan funktionen **Get ()** för att hämta tillgänglighets informationen.

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

Om du vill ha information om en speciell [tillgänglighet](product-resources.md#availability)kör du [**Get-PartnerProductAvailability**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductAvailability.md) och anger **parametrarna AvailabilityId**, **CountryCode**, **ProductID** och **SkuId** för att hämta tillgänglighets informationen.

```powershell
Get-PartnerProductAvailability -Product $productId -SkuId $skuId -AvailabilityId $availabilityId
```

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod  | URI för förfrågan |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **TA** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Products/{Product-ID}/SKUs/{SKU-ID}/availabilities/{Availability-ID}? land = {Country-Code} HTTP/1.1         |

### <a name="uri-parameter"></a>URI-parameter

Använd följande sökväg och frågeparametrar för att få en speciell tillgänglighet med hjälp av ett tillgänglighets-ID.

| Namn                   | Typ     | Obligatorisk | Beskrivning                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| produkt-ID             | sträng   | Yes      | En GUID-formaterad sträng som identifierar produkten.            |
| SKU-ID                 | sträng   | Yes      | En GUID-formaterad sträng som identifierar SKU: n.                |
| tillgänglighets-ID        | sträng   | Yes      | En GUID-formaterad sträng som identifierar tillgängligheten.       |
| landskod           | sträng   | Yes      | Ett land/region-ID.                                            |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

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

Om det lyckas innehåller svars texten en [tillgänglighets](product-resources.md#availability) resurs.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [fel koder för partner Center](error-codes.md).

Den här metoden returnerar följande fel koder:

| HTTP-statuskod     | Felkod   | Description                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 404                  | 400013       | Det gick inte att hitta produkten.                                                                                    |
| 404                  | 400018       | Det gick inte att hitta SKU: n.                                                                                        |
| 404                  | 400019       | Tillgänglighet hittades inte.                                                                                   |

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
