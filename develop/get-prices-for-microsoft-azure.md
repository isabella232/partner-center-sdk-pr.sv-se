---
title: Hämta priser för Microsoft Azure
description: Hur du får ett Azure-pris kort med real tids priser för ett Azure-erbjudande. Azures priser är helt dynamiska och förändringar ofta.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0716f0428b13604105b435a2ce8287a8b4609fea
ms.sourcegitcommit: 64c498d3571f2287305968890578bc7396779621
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/19/2020
ms.locfileid: "97770294"
---
# <a name="get-prices-for-microsoft-azure"></a>Hämta priser för Microsoft Azure

**Gäller för**

- Partnercenter
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Hur du får ett [Azure-pris kort](azure-rate-card-resources.md) med real tids priser för ett Azure-erbjudande. Azures priser är helt dynamiska och förändringar ofta.

Om du vill spåra användningen och hjälpa till att förutsäga din månatliga faktura och fakturor för enskilda kunder kan du kombinera den här Azure Rate Card-frågan för att få priser för Microsoft Azure med en begäran om att [få en kunds användnings poster för Azure](get-a-customer-s-utilization-record-for-azure.md).

Priserna skiljer sig mellan marknaden och valutan, och detta API tar hänsyn till. Som standard använder API dina partner profil inställningar i Partner Center och ditt webb läsar språk, och dessa inställningar är anpassningsbara. Plats medvetenheten är särskilt relevant om du hanterar försäljning på flera marknader från ett enda centraliserat kontor. Mer information finns i [URI-parametrar](#uri-parameters).

## <a name="c"></a>C\#

Du skaffar kortet Azure Rate genom att anropa metoden [**IAzureRateCard. get**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.get) för att returnera en [**AzureRateCard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) -resurs som innehåller Azure-priserna.

```csharp
// IAggregatePartner partnerOperations;

var azureRateCard = partner.RateCards.Azure.Get();
```

**Exempel**: [konsol test app](console-test-app.md). **Projekt**: Partner Center SDK-exempel **klass**: GetAzureRateCard.CS

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Hämta kortet Azure Rate genom att anropa funktionen **IAzureRateCard. get** för att returnera pris information som innehåller Azure-priserna.

```java
// IAggregatePartner partnerOperations;

AzureRateCard azureRateCard = partner.getRateCards().getAzure().get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Hämta Azure-kortet genom att köra kommandot [**Get-PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) för att returnera avgift korts information som innehåller Azure-priserna.

```powershell
Get-PartnerAzureRateCard
```

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod  | URI för förfrågan                                                        |
|---------|--------------------------------------------------------------------|
| **TA** | *{baseURL}*/v1/ratecards/Azure? valuta = {currency} &region = {region} |

### <a name="uri-parameters"></a>URI-parametrar

| Namn     | Typ   | Obligatorisk | Beskrivning                                                                                                                                                                               |
|----------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| currency | sträng | No       | Tre bokstäver, ISO-kod för den valuta där resurs priserna ska tillhandahållas (till exempel `EUR` ). Standardvärdet är `USD`. |
| region   | sträng | No       | Valfria ISO-land/regions kod med två bokstäver som anger på vilken marknad erbjudandet köps (till exempel `FR` ). Standardvärdet är `US`.        |

Du kan inkludera valfria X-locale- [huvud](headers.md#rest-request-headers) i din begäran. Om du inte inkluderar rubriken X-locale, används standardvärdet ("en-US").

- Om du anger valuta-och region parametrar i din begäran, används värdet för X-locale för att fastställa svarets språk.

- Om du inte anger regions-och valuta parametrar i din begäran, används värdet för X-locale för att fastställa svarets region, valuta och språk.

### <a name="request-header"></a>Begärandehuvud

Mer information finns i [partner Center rest-rubriker](headers.md).

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

Om begäran lyckas returneras en [Azure-priss kort](azure-rate-card-resources.md) resurs.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).

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
