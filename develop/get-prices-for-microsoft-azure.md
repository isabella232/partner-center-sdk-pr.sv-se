---
title: Hämta priser för Microsoft Azure
description: Så här hämtar du ett Azure-priskort med realtidspriser för ett Azure-erbjudande. Priserna för Azure är ganska dynamiska och ändras ofta.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8b69e9e3d8e6e4c4e447b308c890c4c054e6a1e5221bb523a5caca041d1ea115
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989125"
---
# <a name="get-prices-for-microsoft-azure"></a>Hämta priser för Microsoft Azure

**Gäller för:** Partner Center-| Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Så här hämtar du [ett Azure-priskort](azure-rate-card-resources.md) med realtidspriser för ett Azure-erbjudande. Priserna för Azure är ganska dynamiska och ändras ofta.

Om du vill spåra användning och hjälpa till att förutsäga din månadsfaktura och fakturorna för enskilda kunder kan du kombinera den här Azure Rate Card-frågan för att hämta priser för Microsoft Azure med en begäran om att hämta en kunds användningsposter för [Azure](get-a-customer-s-utilization-record-for-azure.md).

Priserna varierar beroende på marknad och valuta, och det här API:et tar hänsyn till platsen. Som standard använder API:et dina partnerprofilinställningar i Partnercenter och ditt webbläsarspråk, och dessa inställningar är anpassningsbara. Platsmedvetenhet är särskilt relevant om du hanterar försäljning på flera marknader från ett enda centraliserat kontor. Mer information finns i [URI-parametrar.](#uri-parameters)

## <a name="c"></a>C\#

Hämta Azure-priskortet genom att anropa [**metoden IAzureRateCard.Get**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.get) för att returnera en [**AzureRateCard-resurs**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) som innehåller Azure-priserna.

```csharp
// IAggregatePartner partnerOperations;

var azureRateCard = partner.RateCards.Azure.Get();
```

**Exempel:** [Konsoltestapp](console-test-app.md). **Project:** Partnercenter-SDK Samples **Class**: GetAzureRateCard.cs

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Hämta Azure-priskortet genom att anropa **funktionen IAzureRateCard.get** för att returnera kortinformation som innehåller Azure-priserna.

```java
// IAggregatePartner partnerOperations;

AzureRateCard azureRateCard = partner.getRateCards().getAzure().get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Hämta Azure-kortet genom att köra kommandot [**Get-PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) för att returnera information om kortet som innehåller Azure-priserna.

```powershell
Get-PartnerAzureRateCard
```

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod  | URI för förfrågan                                                        |
|---------|--------------------------------------------------------------------|
| **Få** | *{baseURL}*/v1/ratecards/azure?currency={currency}&region={region} |

### <a name="uri-parameters"></a>URI-parametrar

| Namn     | Typ   | Obligatorisk | Beskrivning                                                                                                                                                                               |
|----------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| currency | sträng | No       | Valfri ISO-kod med tre bokstäver för den valuta som resurspriserna ska anges i (till exempel `EUR` ). Standardvärdet är `USD`. |
| region   | sträng | No       | Valfri iso-lands-/regionkod med två bokstäver som anger vilken marknad erbjudandet köps på (till exempel `FR` ). Standardvärdet är `US`.        |

Du kan inkludera det valfria X-locale-huvudet i din begäran. [](headers.md#rest-request-headers) Om du inte inkluderar huvudet X-Locale används standardvärdet ("en-US").

- Om du anger valuta- och regionparametrar i din begäran används värdet för X-Locale för att fastställa svarets språk.

- Om du inte anger region- och valutaparametrar i din begäran används värdet för X-Locale för att fastställa svarets region, valuta och språk.

### <a name="request-header"></a>Begärandehuvud

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/v1/ratecards/azure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 07ced227-3f32-4eeb-8062-f0bef849a9bc
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST-svar

Om begäran lyckas returneras en [Azure Rate Card-resurs.](azure-rate-card-resources.md)

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Length: 1545508
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57b25659-fc00-4215-87e7-2b09bac6845d
MS-RequestId: 870118d0-adbb-41a3-82d2-a3d45ade3c73
MS-CV: CYBB8PXMsEukJBIn.0
MS-ServerId: 201021413
Date: Wed, 01 Feb 2017 00:13:45 GMT

{
    "locale": "en",
    "currency": "USD",
    "isTaxIncluded": false,
    "meters": [{
            "id": "4b836326-7e19-46e6-8bce-1b19bb6cd91e",
            "name": "Unlimited Data - 1 Gbps",
            "rates": {
                "0": 7395.0
            },
            "tags": [],
            "category": "Networking",
            "subcategory": "ExpressRoute",
            "region": "Zone 2",
            "unit": "Connections",
            "includedQuantity": 0.0,
            "effectiveDate": "2015-09-01T00:00:00Z"
        }, {
            "id": "1e8f6d9f-8b40-4c97-80cc-cff87a290a93",
            "name": "Compute Hours",
            "rates": {
                "0": 3.9729
            },
            "tags": [],
            "category": "Cloud Services",
            "subcategory": "Standard_L16 Cloud Services",
            "region": "AU East",
            "unit": "1 Hour",
            "includedQuantity": 0.0,
            "effectiveDate": "2016-09-01T00:00:00Z"
        }, {
            "id": "7a2639ce-ae47-4413-9837-6b4f4b78be3d",
            "name": "Compute Hours",
            "rates": {
                "0": 0.1122
            },
            "tags": [],
            "category": "Virtual Machines",
            "subcategory": "Standard_D1_v2 VM (Windows)",
            "region": "BR South",
            "unit": "Hours",
            "includedQuantity": 0.0,
            "effectiveDate": "2017-01-01T00:00:00Z"
        }
    ],
    "offerTerms": [{
            "name": "Overage discount",
            "discount": 0.15,
            "excludedMeterIds": ["53cc0061-0fe2-4249-bf62-e1008c811f5c", "c82dbd27-c978-43a7-ad41-525a90d8962b"],
            "effectiveDate": "2014-01-01T00:00:00"
        }
    ],
    "attributes": {
        "objectType": "AzureRateCard"
    }
}
```
