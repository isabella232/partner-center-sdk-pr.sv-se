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
# <a name="get-prices-for-microsoft-azure"></a><span data-ttu-id="9887d-104">Hämta priser för Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="9887d-104">Get prices for Microsoft Azure</span></span>

<span data-ttu-id="9887d-105">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="9887d-105">**Applies To**</span></span>

- <span data-ttu-id="9887d-106">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="9887d-106">Partner Center</span></span>
- <span data-ttu-id="9887d-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="9887d-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="9887d-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="9887d-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="9887d-109">Hur du får ett [Azure-pris kort](azure-rate-card-resources.md) med real tids priser för ett Azure-erbjudande.</span><span class="sxs-lookup"><span data-stu-id="9887d-109">How to get an [Azure Rate Card](azure-rate-card-resources.md) with real-time prices for an Azure offer.</span></span> <span data-ttu-id="9887d-110">Azures priser är helt dynamiska och förändringar ofta.</span><span class="sxs-lookup"><span data-stu-id="9887d-110">Azure pricing is quite dynamic and changes frequently.</span></span>

<span data-ttu-id="9887d-111">Om du vill spåra användningen och hjälpa till att förutsäga din månatliga faktura och fakturor för enskilda kunder kan du kombinera den här Azure Rate Card-frågan för att få priser för Microsoft Azure med en begäran om att [få en kunds användnings poster för Azure](get-a-customer-s-utilization-record-for-azure.md).</span><span class="sxs-lookup"><span data-stu-id="9887d-111">To track usage and help predict your monthly bill and the bills for individual customers, you can combine this Azure Rate Card query to get prices for Microsoft Azure with a request to [Get a customer's utilization records for Azure](get-a-customer-s-utilization-record-for-azure.md).</span></span>

<span data-ttu-id="9887d-112">Priserna skiljer sig mellan marknaden och valutan, och detta API tar hänsyn till.</span><span class="sxs-lookup"><span data-stu-id="9887d-112">Prices differ by market and currency, and this API takes location into consideration.</span></span> <span data-ttu-id="9887d-113">Som standard använder API dina partner profil inställningar i Partner Center och ditt webb läsar språk, och dessa inställningar är anpassningsbara.</span><span class="sxs-lookup"><span data-stu-id="9887d-113">By default, the API uses your partner profile settings in Partner Center and your browser language, and those settings are customizable.</span></span> <span data-ttu-id="9887d-114">Plats medvetenheten är särskilt relevant om du hanterar försäljning på flera marknader från ett enda centraliserat kontor.</span><span class="sxs-lookup"><span data-stu-id="9887d-114">The location awareness is especially relevant if you manage sales in multiple markets from a single, centralized office.</span></span> <span data-ttu-id="9887d-115">Mer information finns i [URI-parametrar](#uri-parameters).</span><span class="sxs-lookup"><span data-stu-id="9887d-115">For more information, see [URI parameters](#uri-parameters).</span></span>

## <a name="c"></a><span data-ttu-id="9887d-116">C\#</span><span class="sxs-lookup"><span data-stu-id="9887d-116">C\#</span></span>

<span data-ttu-id="9887d-117">Du skaffar kortet Azure Rate genom att anropa metoden [**IAzureRateCard. get**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.get) för att returnera en [**AzureRateCard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) -resurs som innehåller Azure-priserna.</span><span class="sxs-lookup"><span data-stu-id="9887d-117">To obtain the Azure Rate Card, call the [**IAzureRateCard.Get**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.get) method to return an [**AzureRateCard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) resource that contains the Azure prices.</span></span>

```csharp
// IAggregatePartner partnerOperations;

var azureRateCard = partner.RateCards.Azure.Get();
```

<span data-ttu-id="9887d-118">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="9887d-118">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="9887d-119">**Projekt**: Partner Center SDK-exempel **klass**: GetAzureRateCard.CS</span><span class="sxs-lookup"><span data-stu-id="9887d-119">**Project**: Partner Center SDK Samples **Class**: GetAzureRateCard.cs</span></span>

## <a name="java"></a><span data-ttu-id="9887d-120">Java</span><span class="sxs-lookup"><span data-stu-id="9887d-120">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="9887d-121">Hämta kortet Azure Rate genom att anropa funktionen **IAzureRateCard. get** för att returnera pris information som innehåller Azure-priserna.</span><span class="sxs-lookup"><span data-stu-id="9887d-121">To obtain the Azure Rate Card, call the **IAzureRateCard.get** function to return rate card details that contains the Azure prices.</span></span>

```java
// IAggregatePartner partnerOperations;

AzureRateCard azureRateCard = partner.getRateCards().getAzure().get();
```

## <a name="powershell"></a><span data-ttu-id="9887d-122">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9887d-122">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="9887d-123">Hämta Azure-kortet genom att köra kommandot [**Get-PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) för att returnera avgift korts information som innehåller Azure-priserna.</span><span class="sxs-lookup"><span data-stu-id="9887d-123">To obtain the Azure Card, execute the [**Get-PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) command to return rate card details that contains the Azure prices.</span></span>

```powershell
Get-PartnerAzureRateCard
```

## <a name="rest-request"></a><span data-ttu-id="9887d-124">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="9887d-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9887d-125">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="9887d-125">Request syntax</span></span>

| <span data-ttu-id="9887d-126">Metod</span><span class="sxs-lookup"><span data-stu-id="9887d-126">Method</span></span>  | <span data-ttu-id="9887d-127">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="9887d-127">Request URI</span></span>                                                        |
|---------|--------------------------------------------------------------------|
| <span data-ttu-id="9887d-128">**TA**</span><span class="sxs-lookup"><span data-stu-id="9887d-128">**GET**</span></span> | <span data-ttu-id="9887d-129">*{baseURL}*/v1/ratecards/Azure? valuta = {currency} &region = {region}</span><span class="sxs-lookup"><span data-stu-id="9887d-129">*{baseURL}*/v1/ratecards/azure?currency={currency}&region={region}</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="9887d-130">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="9887d-130">URI parameters</span></span>

| <span data-ttu-id="9887d-131">Namn</span><span class="sxs-lookup"><span data-stu-id="9887d-131">Name</span></span>     | <span data-ttu-id="9887d-132">Typ</span><span class="sxs-lookup"><span data-stu-id="9887d-132">Type</span></span>   | <span data-ttu-id="9887d-133">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="9887d-133">Required</span></span> | <span data-ttu-id="9887d-134">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="9887d-134">Description</span></span>                                                                                                                                                                               |
|----------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9887d-135">currency</span><span class="sxs-lookup"><span data-stu-id="9887d-135">currency</span></span> | <span data-ttu-id="9887d-136">sträng</span><span class="sxs-lookup"><span data-stu-id="9887d-136">string</span></span> | <span data-ttu-id="9887d-137">No</span><span class="sxs-lookup"><span data-stu-id="9887d-137">No</span></span>       | <span data-ttu-id="9887d-138">Tre bokstäver, ISO-kod för den valuta där resurs priserna ska tillhandahållas (till exempel `EUR` ).</span><span class="sxs-lookup"><span data-stu-id="9887d-138">Optional three letter ISO code for the currency in which the resource rates will be provided (for example `EUR`).</span></span> <span data-ttu-id="9887d-139">Standardvärdet är `USD`.</span><span class="sxs-lookup"><span data-stu-id="9887d-139">The default is `USD`.</span></span> |
| <span data-ttu-id="9887d-140">region</span><span class="sxs-lookup"><span data-stu-id="9887d-140">region</span></span>   | <span data-ttu-id="9887d-141">sträng</span><span class="sxs-lookup"><span data-stu-id="9887d-141">string</span></span> | <span data-ttu-id="9887d-142">No</span><span class="sxs-lookup"><span data-stu-id="9887d-142">No</span></span>       | <span data-ttu-id="9887d-143">Valfria ISO-land/regions kod med två bokstäver som anger på vilken marknad erbjudandet köps (till exempel `FR` ).</span><span class="sxs-lookup"><span data-stu-id="9887d-143">Optional two-letter ISO country/region code that indicates the market where the offer is purchased (for example `FR`).</span></span> <span data-ttu-id="9887d-144">Standardvärdet är `US`.</span><span class="sxs-lookup"><span data-stu-id="9887d-144">The default is `US`.</span></span>        |

<span data-ttu-id="9887d-145">Du kan inkludera valfria X-locale- [huvud](headers.md#rest-request-headers) i din begäran.</span><span class="sxs-lookup"><span data-stu-id="9887d-145">You can include the optional X-Locale [header](headers.md#rest-request-headers) in your request.</span></span> <span data-ttu-id="9887d-146">Om du inte inkluderar rubriken X-locale, används standardvärdet ("en-US").</span><span class="sxs-lookup"><span data-stu-id="9887d-146">If you don't include the X-Locale header, the default value ("en-US") is used.</span></span>

- <span data-ttu-id="9887d-147">Om du anger valuta-och region parametrar i din begäran, används värdet för X-locale för att fastställa svarets språk.</span><span class="sxs-lookup"><span data-stu-id="9887d-147">If you provide currency and region parameters in your request, the value of X-Locale is used to determine the response's language.</span></span>

- <span data-ttu-id="9887d-148">Om du inte anger regions-och valuta parametrar i din begäran, används värdet för X-locale för att fastställa svarets region, valuta och språk.</span><span class="sxs-lookup"><span data-stu-id="9887d-148">If you don't provide region and currency parameters in your request, the value of X-Locale is used to determine the response's region, currency, and language.</span></span>

### <a name="request-header"></a><span data-ttu-id="9887d-149">Begärandehuvud</span><span class="sxs-lookup"><span data-stu-id="9887d-149">Request header</span></span>

<span data-ttu-id="9887d-150">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="9887d-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9887d-151">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="9887d-151">Request body</span></span>

<span data-ttu-id="9887d-152">Inga.</span><span class="sxs-lookup"><span data-stu-id="9887d-152">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="9887d-153">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="9887d-153">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="9887d-154">REST-svar</span><span class="sxs-lookup"><span data-stu-id="9887d-154">REST response</span></span>

<span data-ttu-id="9887d-155">Om begäran lyckas returneras en [Azure-priss kort](azure-rate-card-resources.md) resurs.</span><span class="sxs-lookup"><span data-stu-id="9887d-155">If the request is successful, it returns an [Azure Rate Card](azure-rate-card-resources.md) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9887d-156">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="9887d-156">Response success and error codes</span></span>

<span data-ttu-id="9887d-157">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="9887d-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9887d-158">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="9887d-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9887d-159">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9887d-159">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9887d-160">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="9887d-160">Response example</span></span>

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
