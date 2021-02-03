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
# <a name="get-prices-for-microsoft-azure-partner-shared-services"></a><span data-ttu-id="27a68-103">Hämta priser för Microsoft Azure Partner Shared Services</span><span class="sxs-lookup"><span data-stu-id="27a68-103">Get prices for Microsoft Azure Partner Shared Services</span></span>

<span data-ttu-id="27a68-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="27a68-104">**Applies To**</span></span>

- <span data-ttu-id="27a68-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="27a68-105">Partner Center</span></span>
- <span data-ttu-id="27a68-106">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="27a68-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="27a68-107">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="27a68-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="27a68-108">Hur du får ett [Azure-pris kort](azure-rate-card-resources.md) med priser för Microsoft Azure partner delade tjänster.</span><span class="sxs-lookup"><span data-stu-id="27a68-108">How to get an [Azure Rate Card](azure-rate-card-resources.md) with prices for Microsoft Azure Partner Shared Services.</span></span>

<span data-ttu-id="27a68-109">Priserna skiljer sig mellan marknaden och valutan, och detta API tar hänsyn till.</span><span class="sxs-lookup"><span data-stu-id="27a68-109">Prices differ by market and currency, and this API takes location into consideration.</span></span> <span data-ttu-id="27a68-110">Som standard använder API dina partner profil inställningar i Partner Center och ditt webb läsar språk, och dessa inställningar är anpassningsbara.</span><span class="sxs-lookup"><span data-stu-id="27a68-110">By default, the API uses your partner profile settings in Partner Center and your browser language, and those settings are customizable.</span></span> <span data-ttu-id="27a68-111">Plats medvetenheten är särskilt relevant om du hanterar försäljning på flera marknader från ett enda centraliserat kontor.</span><span class="sxs-lookup"><span data-stu-id="27a68-111">The location awareness is especially relevant if you manage sales in multiple markets from a single, centralized office.</span></span>

## <a name="example-code"></a><span data-ttu-id="27a68-112">Exempel kod</span><span class="sxs-lookup"><span data-stu-id="27a68-112">Example Code</span></span>

## <a name="c"></a><span data-ttu-id="27a68-113">C\#</span><span class="sxs-lookup"><span data-stu-id="27a68-113">C\#</span></span>

<span data-ttu-id="27a68-114">Du skaffar kortet Azure Rate genom att anropa metoden [**IAzureRateCard. GetShared**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.getshared) för att returnera en [**AzureRateCard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) -resurs som innehåller Azure-priserna.</span><span class="sxs-lookup"><span data-stu-id="27a68-114">To obtain the Azure Rate Card, call the [**IAzureRateCard.GetShared**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.getshared) method to return an [**AzureRateCard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) resource that contains the Azure prices.</span></span>

```csharp
// IAggregatePartner partnerOperations;

var azureRateCard = partner.RateCards.Azure.GetShared();
```

## <a name="java"></a><span data-ttu-id="27a68-115">Java</span><span class="sxs-lookup"><span data-stu-id="27a68-115">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="27a68-116">Hämta kortet Azure Rate genom att anropa funktionen **IAzureRateCard. getShared** för att returnera kort korts information som innehåller Azure-priserna.</span><span class="sxs-lookup"><span data-stu-id="27a68-116">To obtain the Azure Rate Card, call the **IAzureRateCard.getShared** function to return rate card details that contains the Azure prices.</span></span>

```java
// IAggregatePartner partnerOperations;

AzureRateCard azureRateCard = partner.getRateCards().getAzure().getShared();
```

## <a name="powershell"></a><span data-ttu-id="27a68-117">PowerShell</span><span class="sxs-lookup"><span data-stu-id="27a68-117">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="27a68-118">Hämta Azure-kortet genom att köra kommandot [**Get-PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) och ange parametern **SharedServices** för att returnera avgift korts information som innehåller Azure-priserna.</span><span class="sxs-lookup"><span data-stu-id="27a68-118">To obtain the Azure Card, execute the [**Get-PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) command and specify the **SharedServices** parameter to return rate card details that contains the Azure prices.</span></span>

```powershell
Get-PartnerAzureRateCard -SharedServices
```

## <a name="rest-request"></a><span data-ttu-id="27a68-119">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="27a68-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="27a68-120">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="27a68-120">Request syntax</span></span>

| <span data-ttu-id="27a68-121">Metod</span><span class="sxs-lookup"><span data-stu-id="27a68-121">Method</span></span>  | <span data-ttu-id="27a68-122">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="27a68-122">Request URI</span></span>                                                               |
|---------|---------------------------------------------------------------------------|
| <span data-ttu-id="27a68-123">**TA**</span><span class="sxs-lookup"><span data-stu-id="27a68-123">**GET**</span></span> | <span data-ttu-id="27a68-124">*{baseURL}*/v1/ratecards/Azure-Shared? valuta = {currency} &region = {region}</span><span class="sxs-lookup"><span data-stu-id="27a68-124">*{baseURL}*/v1/ratecards/azure-shared?currency={currency}&region={region}</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="27a68-125">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="27a68-125">URI parameters</span></span>

| <span data-ttu-id="27a68-126">Namn</span><span class="sxs-lookup"><span data-stu-id="27a68-126">Name</span></span>     | <span data-ttu-id="27a68-127">Typ</span><span class="sxs-lookup"><span data-stu-id="27a68-127">Type</span></span>   | <span data-ttu-id="27a68-128">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="27a68-128">Required</span></span> | <span data-ttu-id="27a68-129">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="27a68-129">Description</span></span>                                                                                                                                                                               |
|----------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="27a68-130">currency</span><span class="sxs-lookup"><span data-stu-id="27a68-130">currency</span></span> | <span data-ttu-id="27a68-131">sträng</span><span class="sxs-lookup"><span data-stu-id="27a68-131">string</span></span> | <span data-ttu-id="27a68-132">No</span><span class="sxs-lookup"><span data-stu-id="27a68-132">No</span></span>       | <span data-ttu-id="27a68-133">Tre bokstäver, ISO-kod för den valuta där resurs priserna ska tillhandahållas (till exempel `EUR` ).</span><span class="sxs-lookup"><span data-stu-id="27a68-133">Optional three letter ISO code for the currency in which the resource rates will be provided (for example `EUR`).</span></span> <span data-ttu-id="27a68-134">Standardvärdet är den valuta som är kopplad till marknaden i partner profilen.</span><span class="sxs-lookup"><span data-stu-id="27a68-134">The default is the currency associated with the market in the partner profile.</span></span> |
| <span data-ttu-id="27a68-135">region</span><span class="sxs-lookup"><span data-stu-id="27a68-135">region</span></span>   | <span data-ttu-id="27a68-136">sträng</span><span class="sxs-lookup"><span data-stu-id="27a68-136">string</span></span> | <span data-ttu-id="27a68-137">No</span><span class="sxs-lookup"><span data-stu-id="27a68-137">No</span></span>       | <span data-ttu-id="27a68-138">Valfria ISO-land/regions kod med två bokstäver som anger på vilken marknad erbjudandet köps (till exempel `FR` ).</span><span class="sxs-lookup"><span data-stu-id="27a68-138">Optional two-letter ISO country/region code that indicates the market where the offer is purchased (for example `FR`).</span></span> <span data-ttu-id="27a68-139">Standardvärdet är lands/regions koden som anges i partner profilen.</span><span class="sxs-lookup"><span data-stu-id="27a68-139">The default is the country/region code set in the partner profile.</span></span>        |

<span data-ttu-id="27a68-140">Om den valfria X-locale-rubriken ingår i begäran, bestämmer värdet för det språk som används för informationen i svaret.</span><span class="sxs-lookup"><span data-stu-id="27a68-140">If the optional X-Locale header is included in the request, its value determines the language used for the details in the response.</span></span>

### <a name="request-headers"></a><span data-ttu-id="27a68-141">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="27a68-141">Request headers</span></span>

<span data-ttu-id="27a68-142">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="27a68-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="27a68-143">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="27a68-143">Request body</span></span>

<span data-ttu-id="27a68-144">Inga.</span><span class="sxs-lookup"><span data-stu-id="27a68-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="27a68-145">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="27a68-145">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="27a68-146">REST-svar</span><span class="sxs-lookup"><span data-stu-id="27a68-146">REST response</span></span>

<span data-ttu-id="27a68-147">Om begäran lyckas returneras en [Azure-priss kort](azure-rate-card-resources.md) resurs.</span><span class="sxs-lookup"><span data-stu-id="27a68-147">If the request is successful, it returns an [Azure Rate Card](azure-rate-card-resources.md) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="27a68-148">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="27a68-148">Response success and error codes</span></span>

<span data-ttu-id="27a68-149">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="27a68-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="27a68-150">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="27a68-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="27a68-151">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="27a68-151">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="27a68-152">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="27a68-152">Response example</span></span>

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
