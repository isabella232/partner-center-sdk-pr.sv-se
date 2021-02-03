---
title: Hämta ett erbjudande efter ID
description: 'Hämtar en erbjudande resurs som matchar erbjudande-ID: t.'
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: brentserbus
ms.author: brserbus
ms.openlocfilehash: 9448276e817affb823eddabbcab8757c79615fbd
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769909"
---
# <a name="get-an-offer-by-id"></a><span data-ttu-id="e28c5-103">Hämta ett erbjudande efter ID</span><span class="sxs-lookup"><span data-stu-id="e28c5-103">Get an offer by ID</span></span>

<span data-ttu-id="e28c5-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="e28c5-104">**Applies To**</span></span>

- <span data-ttu-id="e28c5-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="e28c5-105">Partner Center</span></span>
- <span data-ttu-id="e28c5-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="e28c5-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="e28c5-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="e28c5-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="e28c5-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="e28c5-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="e28c5-109">Hämtar en **erbjudande** resurs som matchar erbjudande-ID: t.</span><span class="sxs-lookup"><span data-stu-id="e28c5-109">Gets an **Offer** resource that matches the offer ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e28c5-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="e28c5-110">Prerequisites</span></span>

- <span data-ttu-id="e28c5-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e28c5-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e28c5-112">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="e28c5-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="e28c5-113">Ett erbjudande-ID.</span><span class="sxs-lookup"><span data-stu-id="e28c5-113">An offer ID.</span></span>

## <a name="c"></a><span data-ttu-id="e28c5-114">C\#</span><span class="sxs-lookup"><span data-stu-id="e28c5-114">C\#</span></span>

<span data-ttu-id="e28c5-115">Om du vill hitta ett särskilt erbjudande med ID använder du din **IAggregatePartner.** samling, etablera land med ett anrop till **ByCountry ()** och anropa sedan metoden [**ByID ()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="e28c5-115">To find a specific offer by ID, use your **IAggregatePartner.Offers** collection, establish the country with a call to **ByCountry()**, and then call the [**ByID()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.byid) method.</span></span> <span data-ttu-id="e28c5-116">Anropa sedan metoden [**Get ()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.get) eller [**Get async ()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.getasync) .</span><span class="sxs-lookup"><span data-stu-id="e28c5-116">Then, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.get) or [**Get Async()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.getasync) method.</span></span>

```csharp
// IAggretagePartner partnerOperations;
// string countryCode;
// string offerId;

// retrieve the offer
var offer = partnerOperations.Offers.ByCountry(countryCode).ById(offerId).Get();
```

<span data-ttu-id="e28c5-117">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="e28c5-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="e28c5-118">**Projekt**: PartnerSDK. FeatureSample- **klass**: GetOffer.CS</span><span class="sxs-lookup"><span data-stu-id="e28c5-118">**Project**: PartnerSDK.FeatureSample **Class**: GetOffer.cs</span></span>

## <a name="java"></a><span data-ttu-id="e28c5-119">Java</span><span class="sxs-lookup"><span data-stu-id="e28c5-119">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="e28c5-120">Om du vill hitta ett särskilt erbjudande med ID använder du din **IAggregatePartner. getOffers** -funktion, upprättar land med ett anrop till funktionen **byCountry ()** och anropar sedan funktionen **byID ()** .</span><span class="sxs-lookup"><span data-stu-id="e28c5-120">To find a specific offer by ID, use your **IAggregatePartner.getOffers** function, establish the country with a call to the **byCountry()** function, and then call the **byID()** function.</span></span> <span data-ttu-id="e28c5-121">Anropa sedan funktionen **Get ()** .</span><span class="sxs-lookup"><span data-stu-id="e28c5-121">Then call the **get()** function.</span></span>

```java
// IAggretagePartner partnerOperations;
// String countryCode;
// String offerId;

// Retrieve the offer
Offer offer = partnerOperations.getOffers().byCountry(countryCode).byId(offerId).get();
```

## <a name="powershell"></a><span data-ttu-id="e28c5-122">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e28c5-122">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="e28c5-123">Om du vill hitta ett särskilt erbjudande efter ID kör du kommandot [**Get-PartnerOffer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOffer.md) och anger parametrarna **CountryCode** och **OfferID** .</span><span class="sxs-lookup"><span data-stu-id="e28c5-123">To find a specific offer by ID, execute the [**Get-PartnerOffer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOffer.md) command, and specify the **CountryCode** and **OfferId** parameters.</span></span>

```powershell
# $countryCode
# $offerId

Get-PartnerOffer -Country $countryCode -OfferId $offerId
```

## <a name="rest-request"></a><span data-ttu-id="e28c5-124">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="e28c5-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e28c5-125">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="e28c5-125">Request syntax</span></span>

| <span data-ttu-id="e28c5-126">Metod</span><span class="sxs-lookup"><span data-stu-id="e28c5-126">Method</span></span>  | <span data-ttu-id="e28c5-127">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="e28c5-127">Request URI</span></span>                                                                                    |
|---------|------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e28c5-128">**TA**</span><span class="sxs-lookup"><span data-stu-id="e28c5-128">**GET**</span></span> | <span data-ttu-id="e28c5-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/offers/{offer-ID}? land = {Country-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="e28c5-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/offers/{offer-id}?country={country-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="e28c5-130">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="e28c5-130">URI parameter</span></span>

| <span data-ttu-id="e28c5-131">Namn</span><span class="sxs-lookup"><span data-stu-id="e28c5-131">Name</span></span>           | <span data-ttu-id="e28c5-132">Typ</span><span class="sxs-lookup"><span data-stu-id="e28c5-132">Type</span></span>       | <span data-ttu-id="e28c5-133">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="e28c5-133">Required</span></span> | <span data-ttu-id="e28c5-134">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="e28c5-134">Description</span></span>                           |
|----------------|------------|----------|---------------------------------------|
| <span data-ttu-id="e28c5-135">**erbjudande-ID**</span><span class="sxs-lookup"><span data-stu-id="e28c5-135">**offer-id**</span></span>   | <span data-ttu-id="e28c5-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="e28c5-136">**guid**</span></span>   | <span data-ttu-id="e28c5-137">Y</span><span class="sxs-lookup"><span data-stu-id="e28c5-137">Y</span></span>        | <span data-ttu-id="e28c5-138">Ett GUID som motsvarar erbjudandet.</span><span class="sxs-lookup"><span data-stu-id="e28c5-138">A GUID that corresponds to the offer.</span></span> |
| <span data-ttu-id="e28c5-139">**lands-ID**</span><span class="sxs-lookup"><span data-stu-id="e28c5-139">**country-id**</span></span> | <span data-ttu-id="e28c5-140">**nollängd**</span><span class="sxs-lookup"><span data-stu-id="e28c5-140">**string**</span></span> | <span data-ttu-id="e28c5-141">Y</span><span class="sxs-lookup"><span data-stu-id="e28c5-141">Y</span></span>        | <span data-ttu-id="e28c5-142">Land/region-ID.</span><span class="sxs-lookup"><span data-stu-id="e28c5-142">The country/region ID.</span></span>                |

### <a name="request-headers"></a><span data-ttu-id="e28c5-143">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="e28c5-143">Request headers</span></span>

- <span data-ttu-id="e28c5-144">Ett **språkvariant-ID** som är formaterat som en sträng krävs.</span><span class="sxs-lookup"><span data-stu-id="e28c5-144">A **locale-id** formatted as a string is required.</span></span>
<span data-ttu-id="e28c5-145">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="e28c5-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e28c5-146">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="e28c5-146">Request body</span></span>

<span data-ttu-id="e28c5-147">Inga.</span><span class="sxs-lookup"><span data-stu-id="e28c5-147">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="e28c5-148">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="e28c5-148">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/offers/<offer-id>?country=<country-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
X-Locale: <locale-id>
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="e28c5-149">REST-svar</span><span class="sxs-lookup"><span data-stu-id="e28c5-149">REST response</span></span>

<span data-ttu-id="e28c5-150">Om det lyckas returnerar den här metoden en **erbjudande** resurs i svars texten.</span><span class="sxs-lookup"><span data-stu-id="e28c5-150">If successful, this method returns an **Offer** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e28c5-151">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="e28c5-151">Response success and error codes</span></span>

<span data-ttu-id="e28c5-152">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="e28c5-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e28c5-153">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="e28c5-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e28c5-154">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e28c5-154">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e28c5-155">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="e28c5-155">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1918
Content-Type: application/json
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
Date: Mon, 23 Nov 2015 23:13:01 GMT

{
    "id": "031C9E47-4802-4248-838E-778FB1D2CC05",
    "name": "Office 365 Business Premium",
    "description": "For businesses with 1 to 300 users that need the latest desktop version of Office,
                    plus anywhere access to email, filesharing, and online conferencing.",
    "minimumQuantity": 1,
    "maximumQuantity": 300,
    "rank": 56,
    "uri": "/3c95518e-8c37-41e3-9627-0ca339200f53/Offers/031C9E47-4802-4248-838E-778FB1D2CC05",
    "locale": "en-us",
    "country": "US",
    "category": {
        "id": "SmallBusiness_Key",
        "name": "Small Business",
        "rank": 30,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    "prerequisiteOffers": [],
    "isAddOn": false,
    "isAvailableForPurchase": true,
    "billing": "license",
    "isAutoRenewable": true,
    "product": {
        "id": "f245ecc8-75af-4f8e-b61f-27d8114de5f3",
        "name": "Office 365 Business Premium",
        "unit": "Licenses"
    },
    "unitType": "Licenses",
    "links": {
        "learnMore": {
            "uri": "http: //g.microsoftonline.com/0BXPS00en/909",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Offer"
    }
}
```
