---
title: Hämta priser för Microsoft Azure Partner Shared Services
description: Hur du får ett Azure-pris kort med priser för Microsoft Azure partner delade tjänster.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: cd396c35b6b89de4d0f092ba4da738a2ed0ac633
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769906"
---
# <a name="get-prices-for-microsoft-azure-partner-shared-services"></a>Hämta priser för Microsoft Azure Partner Shared Services

**Gäller för**

- Partnercenter
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Hur du får ett [Azure-pris kort](azure-rate-card-resources.md) med priser för Microsoft Azure partner delade tjänster.

Priserna skiljer sig mellan marknaden och valutan, och detta API tar hänsyn till. Som standard använder API dina partner profil inställningar i Partner Center och ditt webb läsar språk, och dessa inställningar är anpassningsbara. Plats medvetenheten är särskilt relevant om du hanterar försäljning på flera marknader från ett enda centraliserat kontor.

## <a name="example-code"></a>Exempel kod

## <a name="c"></a>C\#

Du skaffar kortet Azure Rate genom att anropa metoden [**IAzureRateCard. GetShared**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.getshared) för att returnera en [**AzureRateCard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) -resurs som innehåller Azure-priserna.

```csharp
// IAggregatePartner partnerOperations;

var azureRateCard = partner.RateCards.Azure.GetShared();
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Hämta kortet Azure Rate genom att anropa funktionen **IAzureRateCard. getShared** för att returnera kort korts information som innehåller Azure-priserna.

```java
// IAggregatePartner partnerOperations;

AzureRateCard azureRateCard = partner.getRateCards().getAzure().getShared();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Hämta Azure-kortet genom att köra kommandot [**Get-PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) och ange parametern **SharedServices** för att returnera avgift korts information som innehåller Azure-priserna.

```powershell
Get-PartnerAzureRateCard -SharedServices
```

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod  | URI för förfrågan                                                               |
|---------|---------------------------------------------------------------------------|
| **TA** | *{baseURL}*/v1/ratecards/Azure-Shared? valuta = {currency} &region = {region} |

### <a name="uri-parameters"></a>URI-parametrar

| Namn     | Typ   | Obligatorisk | Beskrivning                                                                                                                                                                               |
|----------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| currency | sträng | No       | Tre bokstäver, ISO-kod för den valuta där resurs priserna ska tillhandahållas (till exempel `EUR` ). Standardvärdet är den valuta som är kopplad till marknaden i partner profilen. |
| region   | sträng | No       | Valfria ISO-land/regions kod med två bokstäver som anger på vilken marknad erbjudandet köps (till exempel `FR` ). Standardvärdet är lands/regions koden som anges i partner profilen.        |

Om den valfria X-locale-rubriken ingår i begäran, bestämmer värdet för det språk som används för informationen i svaret.

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/v1/ratecards/azure-shared HTTP/1.1
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
    "locale": "en-US",
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
