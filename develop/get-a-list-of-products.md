---
title: Hämta en lista över produkter (efter land)
description: Du kan använda produktresursen för att hämta en samling produkter efter kundland.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 6ec3a642006a100ef85c0af9eeddd9daf00cc1cd981eabd5dddb77e60e15111f
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989448"
---
# <a name="get-a-list-of-products-by-country"></a>Hämta en lista över produkter (efter land)

**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Du kan använda följande metoder för att hämta en samling produkter som är tillgängliga i ett visst land.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md) Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.

- Ett land.

## <a name="c"></a>C\#

Så här hämtar du en lista över produkter:

1. Använd din **IAggregatePartner.Products-samling** för att välja land med hjälp av **metoden ByCountry().**

2. Välj katalogvyn med hjälp av **metoden ByTargetView().**

3. (Valfritt) Välj reservationsomfånget med hjälp **av metoden ByReservationScope().**

4. (Valfritt) Välj målsegmentet med hjälp **av metoden ByTargetSegment().**

5. Anropa metoden **Get()** eller **GetAsync()** för att returnera samlingen.

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

1. Använd funktionen **IAggregatePartner.getProducts** för att välja land med hjälp av funktionen **byCountry().**

2. Välj katalogvyn med hjälp av **funktionen byTargetView().**
3. (Valfritt) Välj målsegmentet med hjälp **av funktionen byTargetSegment().**

4. Anropa **funktionen get()** för att returnera samlingen.

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

1. Kör kommandot [**Get-PartnerProduct.**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md)

2. Välj katalogen genom att ange **parametern** Catalog.
3. (Valfritt) Välj målsegmentet genom att ange **parametern** Segment.

```powershell
Get-PartnerProduct -Catalog 'Azure' -Segment 'commercial'
```

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod  | URI för förfrågan                                                                                                                                    |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------- |
| **Få** | [*{baseURL}*](partner-center-rest-urls.md)/v1/products?country={country}&targetView={targetView}&targetSegment={targetSegment} HTTP/1.1 |

#### <a name="uri-parameters"></a>URI-parametrar

Använd följande sökväg och frågeparametrar för att hämta en lista över produkter.

| Namn                   | Typ     | Obligatorisk | Beskrivning                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| land                | sträng   | Yes      | Land/region-ID.                                                  |
| targetView             | sträng   | Yes      | Identifierar målvyn för katalogen. Värdena som stöds är: <br/><br/>**Azure**, som innehåller alla Azure-objekt<br/><br/>**AzureReservations**, som innehåller alla Reservationsobjekt i Azure<br/><br/>**AzureReservationsVM**, som innehåller alla reservationsobjekt för virtuella datorer (VM)<br/><br/>**AzureReservationsSQL**, som innehåller alla SQL reservationsobjekt<br/><br/>**AzureReservationsCosmosDb**, som innehåller alla reservationsobjekt för Cosmos-databasen<br/><br/>**MicrosoftAzure**, som innehåller objekt för Microsoft Azure-prenumerationer **(MS-AZR-0145P)** och Azure-planer<br/><br/>**OnlineServices**, som innehåller alla onlinetjänstobjekt (inklusive produkter från den kommersiella marknadsplatsen)<br/><br/>**Programvara**, som innehåller alla programvaruobjekt<br/><br/>**SoftwareSUSELinux**, som innehåller alla SUSE Linux-programobjekt<br/><br/>**SoftwarePerpetual**, som innehåller alla permanenta programvaruobjekt<br/><br/>**SoftwareSubscriptions**, som innehåller alla programprenumerationsobjekt    |
| targetSegment          | sträng   | No       | Identifierar målsegmentet. Vyn för olika målgrupper. Värdena som stöds är: <br/><br/>**Kommersiella**<br/>**Utbildning**<br/>**Regeringen**<br/>**Ideell**  |
| reservationScope | sträng   | No | När du frågar efter en lista över produkter för Azure-reservationer anger du för att hämta en lista över `reservationScope=AzurePlan` produkter som gäller för Azure-planer. Undanta den här parametern för att hämta en lista över produkter för Azure-reservationer, som gäller för Microsoft Azure-prenumerationer **(MS-AZR-0145P).**  |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-examples"></a>Exempel på begäran

#### <a name="products-by-country"></a>Produkter efter land

Följ det här exemplet för att hämta en lista över produkter efter land Microsoft Azure prenumerationer (MS-AZR-0145P) och Azure-planer.

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-azure-plan"></a>Reservationer för virtuella Azure-datorer (Azure-plan)

Följ det här exemplet för att hämta en lista över produkter efter land för Azure VM-reservationer som gäller för Azure-planer.

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureAzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>Azure VM-reservationer Microsoft Azure prenumerationer (MS-AZR-0145P)

Följ det här exemplet för att hämta en lista över produkter efter land för Azure VM-reservationer som gäller för Microsoft Azure-prenumerationer (MS-AZR-0145P).

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a>REST-svar

Om det lyckas innehåller svarstexten en samling [**produktresurser.**](product-resources.md#product)

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder i Partnercenter.](error-codes.md)

Den här metoden returnerar följande felkoder:

| HTTP-statuskod     | Felkod   | Description                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 403                  | 400030       | Åtkomst till det begärda targetSegment tillåts inte.                                                     |
| 403                  | 400036       | Åtkomst till begärd targetView tillåts inte.                                                        |

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
