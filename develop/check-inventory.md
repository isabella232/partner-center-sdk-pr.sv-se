---
title: Kontrollera inventering
description: Lär dig hur du använder Partner Center-API:er för att kontrollera inventeringen för en specifik uppsättning katalogobjekt. Du kan göra detta för att identifiera en kunds produkter eller SKU:er.
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b982dbd7e5e10d454ef87a1e750546ea50eb8438
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974088"
---
# <a name="check-the-inventory-of-catalog-items-using-partner-center-apis"></a>Kontrollera inventeringen av katalogobjekt med partnercenter-API:er

Så här kontrollerar du lagret för en specifik uppsättning katalogobjekt.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md) Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.

- Ett eller flera produkt-ID:er. Du kan också ange SKU-ID:n.

- Eventuell ytterligare kontext som behövs för att verifiera inventeringen av de SKU:er som refereras av de tillhandahållna produkt-/SKU-ID:erna. Dessa krav kan variera beroende på typ av produkt/SKU och kan fastställas från [SKU:ns](product-resources.md#sku) **egenskap InventoryVariables.**

## <a name="c"></a>C\#

Om du vill kontrollera inventeringen skapar du [ett InventoryCheckRequest-objekt](product-resources.md#inventorycheckrequest) med hjälp av [ett InventoryItem-objekt](product-resources.md#inventoryitem) för varje objekt som ska kontrolleras. Använd sedan en **åtkomstor för IAggregatePartner.Extensions,** begränsa den till **Produkt** och välj sedan land med hjälp av **metoden ByCountry().** Anropa slutligen metoden **CheckInventory()** med ditt **InventoryCheckRequest-objekt.**

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string subscriptionId;
string countryCode;
string productId;

// Build the inventory check request details object.
var inventoryCheckRequest = new InventoryCheckRequest()
{
    TargetItems = new InventoryItem[]{ new InventoryItem { ProductId = productId } },
    InventoryContext = new Dictionary<string, string>()
    {
      { "customerId", customerId },
      { "azureSubscriptionId", subscriptionId }
      { "armRegionName", armRegionName }
    }
};

// Get the inventory results.
var inventoryResults = partnerOperations.Extensions.Product.ByCountry(countryCode).CheckInventory(inventoryCheckRequest);
```

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod   | URI för förfrågan                                                                                                                              |
|----------|------------------------------------------------------------------------------------------------------------------------------------------|
| **Inlägg** | [*{baseURL}*](partner-center-rest-urls.md)/v1/extensions/product/checkInventory?country={country-code} HTTP/1.1                        |

### <a name="uri-parameter"></a>URI-parameter

Använd följande frågeparameter för att kontrollera inventeringen.

| Namn                   | Typ     | Obligatorisk | Beskrivning                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| landskod           | sträng   | Ja      | Ett lands-/regions-ID.                                            |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

Information om inventeringsbegäran som består av en [InventoryCheckRequest-resurs](product-resources.md#inventorycheckrequest) som innehåller en eller flera [InventoryItem-resurser.](product-resources.md#inventoryitem)

### <a name="request-example"></a>Exempel på begäran

```http
POST https://api.partnercenter.microsoft.com/v1/extensions/product/checkinventory?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: d1b1981a-e088-4610-870a-eebec96d6bcd
MS-CorrelationId: 4acb26a1-3536-4081-bc7d-092869a4961a
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json

{"TargetItems":[{"ProductId":"DZH318Z0BQ3P"}],"InventoryContext":{"customerId":"d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d","azureSubscriptionId":"3A231FBE-37FE-4410-93FD-730D3D5D4C75","armRegionName":"Europe"}}
```

## <a name="rest-response"></a>REST-svar

Om det lyckas innehåller svarstexten en samling [InventoryItem-objekt](product-resources.md#inventoryitem) ifyllda med begränsningsinformationen, om tillämpligt.

>[!NOTE]
>Om indatan InventoryItem representerar ett objekt som inte kunde hittas i katalogen inkluderas det inte i utdatasamlingen.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder i Partnercenter.](error-codes.md)

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Length: 1021
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4acb26a1-3536-4081-bc7d-092869a4961a
MS-RequestId: d1b1981a-e088-4610-870a-eebec96d6bcd
X-Locale: en-US
[
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "0039",
        "isRestricted": true,
        "restrictions": [
            {
                "reasonCode": "NotAvailableForSubscription",
                "description": "Restriction identified of type 'Location' with values 'japanwest'.",
                "properties": {
                    "type": "Location",
                    "values": "japanwest"
                }
            }
        ]
    },
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "0038",
        "isRestricted": true,
        "restrictions": [
            {
                "reasonCode": "NotAvailableForSubscription",
                "description": "Restriction identified of type 'Location' with values 'japanwest'.",
                "properties": {
                    "type": "Location",
                    "values": "japanwest"
                }
            }
        ]
    },
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "000S",
        "isRestricted": false,
        "restrictions": []
    },
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "0011",
        "isRestricted": false,
        "restrictions": []
    }
]
```
