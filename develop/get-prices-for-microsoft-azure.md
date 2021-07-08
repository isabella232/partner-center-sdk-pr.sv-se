---
title: Hämta priser för Microsoft Azure
description: Så här hämtar du ett Azure-priskort med realtidspriser för ett Azure-erbjudande. Priserna för Azure är ganska dynamiska och ändras ofta.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4f66ab19ef3723fbaa27acff941cf48683a7c25c
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548795"
---
# <a name="get-prices-for-microsoft-azure"></a><span data-ttu-id="dc4f5-104">Hämta priser för Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="dc4f5-104">Get prices for Microsoft Azure</span></span>

<span data-ttu-id="dc4f5-105">**Gäller för**: Partner Center-| PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="dc4f5-105">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="dc4f5-106">Så här hämtar du [ett Azure-priskort](azure-rate-card-resources.md) med realtidspriser för ett Azure-erbjudande.</span><span class="sxs-lookup"><span data-stu-id="dc4f5-106">How to get an [Azure Rate Card](azure-rate-card-resources.md) with real-time prices for an Azure offer.</span></span> <span data-ttu-id="dc4f5-107">Priserna för Azure är ganska dynamiska och ändras ofta.</span><span class="sxs-lookup"><span data-stu-id="dc4f5-107">Azure pricing is quite dynamic and changes frequently.</span></span>

<span data-ttu-id="dc4f5-108">Om du vill spåra användning och hjälpa till att förutsäga din månadsfaktura och fakturorna för enskilda kunder kan du kombinera den här Azure Rate Card-frågan för att hämta priser för Microsoft Azure med en begäran om att hämta en [kunds](get-a-customer-s-utilization-record-for-azure.md)användningsposter för Azure .</span><span class="sxs-lookup"><span data-stu-id="dc4f5-108">To track usage and help predict your monthly bill and the bills for individual customers, you can combine this Azure Rate Card query to get prices for Microsoft Azure with a request to [Get a customer's utilization records for Azure](get-a-customer-s-utilization-record-for-azure.md).</span></span>

<span data-ttu-id="dc4f5-109">Priserna varierar beroende på marknad och valuta, och det här API:et tar hänsyn till platsen.</span><span class="sxs-lookup"><span data-stu-id="dc4f5-109">Prices differ by market and currency, and this API takes location into consideration.</span></span> <span data-ttu-id="dc4f5-110">Som standard använder API:et dina partnerprofilinställningar i Partnercenter och ditt webbläsarspråk, och dessa inställningar är anpassningsbara.</span><span class="sxs-lookup"><span data-stu-id="dc4f5-110">By default, the API uses your partner profile settings in Partner Center and your browser language, and those settings are customizable.</span></span> <span data-ttu-id="dc4f5-111">Platsmedvetenhet är särskilt relevant om du hanterar försäljning på flera marknader från ett enda centraliserat kontor.</span><span class="sxs-lookup"><span data-stu-id="dc4f5-111">The location awareness is especially relevant if you manage sales in multiple markets from a single, centralized office.</span></span> <span data-ttu-id="dc4f5-112">Mer information finns i [URI-parametrar](#uri-parameters).</span><span class="sxs-lookup"><span data-stu-id="dc4f5-112">For more information, see [URI parameters](#uri-parameters).</span></span>

## <a name="c"></a><span data-ttu-id="dc4f5-113">C\#</span><span class="sxs-lookup"><span data-stu-id="dc4f5-113">C\#</span></span>

<span data-ttu-id="dc4f5-114">Hämta Azure-priskortet genom att anropa [**metoden IAzureRateCard.Get**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.get) för att returnera en [**AzureRateCard-resurs**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) som innehåller Azure-priserna.</span><span class="sxs-lookup"><span data-stu-id="dc4f5-114">To obtain the Azure Rate Card, call the [**IAzureRateCard.Get**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.get) method to return an [**AzureRateCard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) resource that contains the Azure prices.</span></span>

```csharp
// IAggregatePartner partnerOperations;

var azureRateCard = partner.RateCards.Azure.Get();
```

<span data-ttu-id="dc4f5-115">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="dc4f5-115">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="dc4f5-116">**Project:** Partnercenter-SDK Samples **Class**: GetAzureRateCard.cs</span><span class="sxs-lookup"><span data-stu-id="dc4f5-116">**Project**: Partner Center SDK Samples **Class**: GetAzureRateCard.cs</span></span>

## <a name="java"></a><span data-ttu-id="dc4f5-117">Java</span><span class="sxs-lookup"><span data-stu-id="dc4f5-117">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="dc4f5-118">Hämta Azure-priskortet genom att anropa **funktionen IAzureRateCard.get** för att returnera kortinformation som innehåller Azure-priserna.</span><span class="sxs-lookup"><span data-stu-id="dc4f5-118">To obtain the Azure Rate Card, call the **IAzureRateCard.get** function to return rate card details that contains the Azure prices.</span></span>

```java
// IAggregatePartner partnerOperations;

AzureRateCard azureRateCard = partner.getRateCards().getAzure().get();
```

## <a name="powershell"></a><span data-ttu-id="dc4f5-119">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dc4f5-119">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="dc4f5-120">Hämta Azure-kortet genom att köra kommandot [**Get-PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) för att returnera kortinformation som innehåller Azure-priserna.</span><span class="sxs-lookup"><span data-stu-id="dc4f5-120">To obtain the Azure Card, execute the [**Get-PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) command to return rate card details that contains the Azure prices.</span></span>

```powershell
Get-PartnerAzureRateCard
```

## <a name="rest-request"></a><span data-ttu-id="dc4f5-121">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="dc4f5-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="dc4f5-122">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="dc4f5-122">Request syntax</span></span>

| <span data-ttu-id="dc4f5-123">Metod</span><span class="sxs-lookup"><span data-stu-id="dc4f5-123">Method</span></span>  | <span data-ttu-id="dc4f5-124">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="dc4f5-124">Request URI</span></span>                                                        |
|---------|--------------------------------------------------------------------|
| <span data-ttu-id="dc4f5-125">**Få**</span><span class="sxs-lookup"><span data-stu-id="dc4f5-125">**GET**</span></span> | <span data-ttu-id="dc4f5-126">*{baseURL}*/v1/ratecards/azure?currency={currency}&region={region}</span><span class="sxs-lookup"><span data-stu-id="dc4f5-126">*{baseURL}*/v1/ratecards/azure?currency={currency}&region={region}</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="dc4f5-127">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="dc4f5-127">URI parameters</span></span>

| <span data-ttu-id="dc4f5-128">Namn</span><span class="sxs-lookup"><span data-stu-id="dc4f5-128">Name</span></span>     | <span data-ttu-id="dc4f5-129">Typ</span><span class="sxs-lookup"><span data-stu-id="dc4f5-129">Type</span></span>   | <span data-ttu-id="dc4f5-130">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="dc4f5-130">Required</span></span> | <span data-ttu-id="dc4f5-131">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="dc4f5-131">Description</span></span>                                                                                                                                                                               |
|----------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="dc4f5-132">currency</span><span class="sxs-lookup"><span data-stu-id="dc4f5-132">currency</span></span> | <span data-ttu-id="dc4f5-133">sträng</span><span class="sxs-lookup"><span data-stu-id="dc4f5-133">string</span></span> | <span data-ttu-id="dc4f5-134">No</span><span class="sxs-lookup"><span data-stu-id="dc4f5-134">No</span></span>       | <span data-ttu-id="dc4f5-135">Valfri ISO-kod med tre bokstäver för den valuta som resurspriserna ska anges i (till exempel `EUR` ).</span><span class="sxs-lookup"><span data-stu-id="dc4f5-135">Optional three letter ISO code for the currency in which the resource rates will be provided (for example `EUR`).</span></span> <span data-ttu-id="dc4f5-136">Standardvärdet är `USD`.</span><span class="sxs-lookup"><span data-stu-id="dc4f5-136">The default is `USD`.</span></span> |
| <span data-ttu-id="dc4f5-137">region</span><span class="sxs-lookup"><span data-stu-id="dc4f5-137">region</span></span>   | <span data-ttu-id="dc4f5-138">sträng</span><span class="sxs-lookup"><span data-stu-id="dc4f5-138">string</span></span> | <span data-ttu-id="dc4f5-139">No</span><span class="sxs-lookup"><span data-stu-id="dc4f5-139">No</span></span>       | <span data-ttu-id="dc4f5-140">Valfri ISO-lands-/regionkod med två bokstäver som anger vilken marknad erbjudandet köps på (till exempel `FR` ).</span><span class="sxs-lookup"><span data-stu-id="dc4f5-140">Optional two-letter ISO country/region code that indicates the market where the offer is purchased (for example `FR`).</span></span> <span data-ttu-id="dc4f5-141">Standardvärdet är `US`.</span><span class="sxs-lookup"><span data-stu-id="dc4f5-141">The default is `US`.</span></span>        |

<span data-ttu-id="dc4f5-142">Du kan inkludera det valfria X-Locale-huvudet i din begäran. [](headers.md#rest-request-headers)</span><span class="sxs-lookup"><span data-stu-id="dc4f5-142">You can include the optional X-Locale [header](headers.md#rest-request-headers) in your request.</span></span> <span data-ttu-id="dc4f5-143">Om du inte inkluderar huvudet X-Locale används standardvärdet ("en-US").</span><span class="sxs-lookup"><span data-stu-id="dc4f5-143">If you don't include the X-Locale header, the default value ("en-US") is used.</span></span>

- <span data-ttu-id="dc4f5-144">Om du anger valuta- och regionparametrar i din begäran används värdet för X-Locale för att fastställa svarets språk.</span><span class="sxs-lookup"><span data-stu-id="dc4f5-144">If you provide currency and region parameters in your request, the value of X-Locale is used to determine the response's language.</span></span>

- <span data-ttu-id="dc4f5-145">Om du inte anger region- och valutaparametrar i din begäran används värdet för X-Locale för att fastställa svarets region, valuta och språk.</span><span class="sxs-lookup"><span data-stu-id="dc4f5-145">If you don't provide region and currency parameters in your request, the value of X-Locale is used to determine the response's region, currency, and language.</span></span>

### <a name="request-header"></a><span data-ttu-id="dc4f5-146">Begärandehuvud</span><span class="sxs-lookup"><span data-stu-id="dc4f5-146">Request header</span></span>

<span data-ttu-id="dc4f5-147">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="dc4f5-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="dc4f5-148">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="dc4f5-148">Request body</span></span>

<span data-ttu-id="dc4f5-149">Inga.</span><span class="sxs-lookup"><span data-stu-id="dc4f5-149">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="dc4f5-150">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="dc4f5-150">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="dc4f5-151">REST-svar</span><span class="sxs-lookup"><span data-stu-id="dc4f5-151">REST response</span></span>

<span data-ttu-id="dc4f5-152">Om begäran lyckas returneras en [Azure Rate Card-resurs.](azure-rate-card-resources.md)</span><span class="sxs-lookup"><span data-stu-id="dc4f5-152">If the request is successful, it returns an [Azure Rate Card](azure-rate-card-resources.md) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="dc4f5-153">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="dc4f5-153">Response success and error codes</span></span>

<span data-ttu-id="dc4f5-154">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="dc4f5-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="dc4f5-155">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="dc4f5-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="dc4f5-156">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="dc4f5-156">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="dc4f5-157">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="dc4f5-157">Response example</span></span>

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
