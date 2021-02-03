---
title: Kontrol lera inventering
description: 'Lär dig hur du använder API: er för partner Center för att kontrol lera inventeringen för en bestämd uppsättning katalog objekt. Du kan göra detta för att identifiera en kunds produkter eller SKU: er.'
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6921760abc0b95aff820467e84b3e8e9435731cd
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/04/2020
ms.locfileid: "97770086"
---
# <a name="check-the-inventory-of-catalog-items-using-partner-center-apis"></a>Kontrol lera förteckningen över katalog objekt med API: er för partner Center

**Gäller för:**

- Partnercenter

Så här kontrollerar du inventeringen för en bestämd uppsättning katalog objekt.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.

- Ett eller flera produkt-ID: n. Du kan också ange SKU-ID: n.

- Eventuell ytterligare kontext som krävs för att verifiera inventeringen av de SKU: er som refereras av de tillhandahållna produkt-eller SKU-ID: n. Dessa krav kan variera beroende på typ av produkt/SKU och kan fastställas från [SKU: s](product-resources.md#sku) **InventoryVariables** -egenskap.

## <a name="c"></a>C\#

Om du vill kontrol lera inventeringen skapar du ett [InventoryCheckRequest](product-resources.md#inventorycheckrequest) -objekt med ett [InventoryItem](product-resources.md#inventoryitem) -objekt för varje objekt som ska kontrol leras. Använd sedan en **IAggregatePartner. Extensions** -accessor, omfånget till **produkten** och välj sedan landet med **ByCountry ()-** metoden. Anropa slutligen metoden **CheckInventory ()** med **InventoryCheckRequest** -objektet.

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

### <a name="request-syntax"></a>Syntax för begäran

| Metod   | URI för förfrågan                                                                                                                              |
|----------|------------------------------------------------------------------------------------------------------------------------------------------|
| **EFTER** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Extensions/Product/checkInventory? land = {Country-Code} HTTP/1.1                        |

### <a name="uri-parameter"></a>URI-parameter

Använd följande frågeparameter för att kontrol lera inventeringen.

| Namn                   | Typ     | Obligatorisk | Beskrivning                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| landskod           | sträng   | Yes      | Ett land/region-ID.                                            |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

Information om inventerings begär Anden som består av en [InventoryCheckRequest](product-resources.md#inventorycheckrequest) -resurs som innehåller en eller flera [InventoryItem](product-resources.md#inventoryitem) -resurser.

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

Om det lyckas innehåller svars texten en samling [InventoryItem](product-resources.md#inventoryitem) -objekt som är ifyllda med begränsnings informationen, om tillämpligt.

>[!NOTE]
>Om en InventoryItem för indata representerar ett objekt som inte kunde hittas i katalogen, kommer det inte att tas med i insamlingen av utdata.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [fel koder för partner Center](error-codes.md).

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
