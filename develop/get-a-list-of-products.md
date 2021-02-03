---
title: Hämta en lista över produkter (efter land)
description: Du kan använda produkt resursen för att hämta en samling produkter per kund land.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: ea239aa008a5b7c33740e9c4697c3795908415cd
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/14/2020
ms.locfileid: "97769447"
---
# <a name="get-a-list-of-products-by-country"></a>Hämta en lista över produkter (efter land)

**Gäller för:**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Du kan använda följande metoder för att hämta en samling produkter som är tillgängliga i ett visst land.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.

- Ett land.

## <a name="c"></a>C\#

Så här hämtar du en lista över produkter:

1. Använd din **IAggregatePartner. Products** -samling för att välja land med hjälp av metoden **ByCountry ()** .

2. Välj vyn katalog med metoden **ByTargetView ()** .

3. Valfritt Välj reservations omfånget med metoden **ByReservationScope ()** .

4. Valfritt Välj mål segmentet med metoden **ByTargetSegment ()** .

5. Anropa metoden **Get ()** eller **GetAsync ()** för att returnera samlingen.

```csharp
IAggregatePartner partnerOperations;

// Get the products for the specified catalog view.
ResourceCollection<Products> products = partnerOperations.Products.ByCountry("US").ByTargetView("MicrosoftAzure").Get();

// Get the products filtered by target view and target segment.
ResourceCollection<Products> products = partnerOperations.Products.ByCountry("US").ByTargetView("MicrosoftAzure").ByTargetSegment("commercial").Get();

// Get the products for Azure reservations which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions only.
ResourceCollection<Product> products = partnerOperations.Products.ByCountry("US").ByTargetView("AzureReservations").Get();

// Get the products for Azure reservations which are applicable to Azure plans only.
ResourceCollection<Product> products = partnerOperations.Products.ByCountry("US").ByTargetView("AzureReservations").ByReservationScope("AzurePlan").Get();

```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Så här hämtar du en lista över produkter:

1. Använd funktionen **IAggregatePartner. getProducts** för att välja land med hjälp av funktionen **byCountry ()** .

2. Välj vyn katalog med funktionen **byTargetView ()** .
3. Valfritt Välj mål segment med funktionen **byTargetSegment ()** .

4. Anropa funktionen **Get ()** för att returnera samlingen.

```java
// IAggregatePartner partnerOperations;

// Get the products for the specified catalog view.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").get();

// Get the products filtered by target view and target segment.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").byTargetSegment("commercial").get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Så här hämtar du en lista över produkter:

1. Kör kommandot [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) .

2. Välj katalogen genom att ange **katalog** parametern.
3. Valfritt Välj mål segmentet genom att ange **segment** parametern.

```powershell
Get-PartnerProduct -Catalog 'Azure' -Segment 'commercial'
```

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod  | URI för förfrågan                                                                                                                                    |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------- |
| **TA** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Products? Country = {country} &targetView = {targetView} &targetSegment = {TARGETSEGMENT} http/1.1 |

#### <a name="uri-parameters"></a>URI-parametrar

Använd följande sökväg och frågeparametrar för att hämta en lista över produkter.

| Namn                   | Typ     | Obligatorisk | Beskrivning                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| land                | sträng   | Yes      | Land/region-ID.                                                  |
| targetView             | sträng   | Yes      | Identifierar katalogens mållista. De värden som stöds är: <br/><br/>**Azure**, som innehåller alla Azure-objekt<br/><br/>**AzureReservations**, som innehåller alla Azure reservation-objekt<br/><br/>**AzureReservationsVM**, som innehåller alla reservations objekt för virtuella datorer (VM)<br/><br/>**AzureReservationsSQL**, som innehåller alla SQL reservation-objekt<br/><br/>**AzureReservationsCosmosDb**, som innehåller alla Cosmos-databas reservations objekt<br/><br/>**MicrosoftAzure**, som innehåller objekt för Microsoft Azure prenumerationer (**MS-AZR-0145P**) och Azure-planer<br/><br/>**OnlineServices**, som omfattar alla online tjänst objekt (inklusive kommersiella produkter från marknaden)<br/><br/>**Program vara**, som innehåller alla program varu objekt<br/><br/>**SoftwareSUSELinux**, som innehåller alla program vara SUSE Linux-objekt<br/><br/>**SoftwarePerpetual**, som innehåller alla objekt med beständig program vara<br/><br/>**SoftwareSubscriptions**, som innehåller alla program prenumerations objekt    |
| targetSegment          | sträng   | No       | Identifierar mål segmentet. Vyn för olika mål grupper. De värden som stöds är: <br/><br/>**marknadsmässig**<br/>**kontor**<br/>**stat**<br/>**vinstdrivande**  |
| reservationScope | sträng   | No | När du frågar efter en lista över produkter för Azure Reservations anger `reservationScope=AzurePlan` du för att hämta en lista över produkter som är tillämpliga på Azure-planer. Undanta den här parametern för att hämta en lista över produkter för Azure-reservationer som är tillämpliga på Microsoft Azure (**MS-AZR-0145P**)-prenumerationer.  |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-examples"></a>Exempel på begäran

#### <a name="products-by-country"></a>Produkter efter land

Följ det här exemplet för att hämta en lista över produkter efter land för Microsoft Azure (MS-AZR-0145P) prenumerationer och Azure-planer.

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-azure-plan"></a>Azure VM-reservationer (Azure-plan)

Följ det här exemplet för att hämta en lista över produkter efter land för Azure VM-reservationer som är tillämpliga för Azure-planer.

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureAzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>Azure VM-reservationer för Microsoft Azure (MS-AZR-0145P)-prenumerationer

Följ det här exemplet för att hämta en lista över produkter efter land för Azure VM-reservationer som är tillämpliga på Microsoft Azure (MS-AZR-0145P)-prenumerationer.

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a>REST-svar

Om det lyckas innehåller svars texten en samling [**produkt**](product-resources.md#product) resurser.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [fel koder för partner Center](error-codes.md).

Den här metoden returnerar följande fel koder:

| HTTP-statuskod     | Felkod   | Description                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 403                  | 400030       | Åtkomst till den begärda targetSegment är inte tillåten.                                                     |
| 403                  | 400036       | Åtkomst till den begärda targetView är inte tillåten.                                                        |

### <a name="response-example"></a>Exempel på svar

```http
{
    "totalCount": 19,
    "items": [
        {
            "id": "DZH318Z0BQ3Q",
            "title": "Virtual Machines DSv2 Series",
            "description": "Dsv2-series instances are the latest generation of D-series instances that will carry more powerful CPUs which are on average about 35% faster than D-series instances, and carry the same memory and disk configurations as the D-series. Dsv2-series instances are based on the latest generation 2.4 GHz Intel Xeon® E5-2673 v3 (Haswell) processor, and with Intel Turbo Boost Technology 2.0 can go to 3.2 GHz.",
            "productType": {
                "id": "Azure",
                "displayName": "Azure",
                "subType": {
                "id": "VirtualMachines",
                "displayName": "VirtualMachines"
                }
            },
            "isMicrosoftProduct": true,
            "publisherName": "Microsoft",
            "links": {
                "skus": {
                    "uri": "/products/DZH318Z0BQ3Q/skus?country=US",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/products/DZH318Z0BQ3Q?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        ...
    ],
    "links": {
        "self": {
            "uri": "/products?country=US&targetView=Azure",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
