---
title: Hämta ett erbjudande efter ID
description: Hämtar en erbjudanderesurs som matchar erbjudande-ID:t.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: brentserbus
ms.author: brserbus
ms.openlocfilehash: f759cbdeefb4f550c41b41de40e9979e72e4ddeb
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760648"
---
# <a name="get-an-offer-by-id"></a><span data-ttu-id="3f845-103">Hämta ett erbjudande efter ID</span><span class="sxs-lookup"><span data-stu-id="3f845-103">Get an offer by ID</span></span>

<span data-ttu-id="3f845-104">**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="3f845-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="3f845-105">Hämtar en **erbjudanderesurs** som matchar erbjudande-ID:t.</span><span class="sxs-lookup"><span data-stu-id="3f845-105">Gets an **Offer** resource that matches the offer ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3f845-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="3f845-106">Prerequisites</span></span>

- <span data-ttu-id="3f845-107">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="3f845-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3f845-108">Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="3f845-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="3f845-109">Ett erbjudande-ID.</span><span class="sxs-lookup"><span data-stu-id="3f845-109">An offer ID.</span></span>

## <a name="c"></a><span data-ttu-id="3f845-110">C\#</span><span class="sxs-lookup"><span data-stu-id="3f845-110">C\#</span></span>

<span data-ttu-id="3f845-111">Om du vill hitta ett specifikt erbjudande efter ID använder du **samlingen IAggregatePartner.Offers,** upprättar landet med ett anrop till **ByCountry()** och anropar sedan [**metoden ByID().**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.byid)</span><span class="sxs-lookup"><span data-stu-id="3f845-111">To find a specific offer by ID, use your **IAggregatePartner.Offers** collection, establish the country with a call to **ByCountry()**, and then call the [**ByID()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.byid) method.</span></span> <span data-ttu-id="3f845-112">Anropa sedan metoden [**Get()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.get) eller [**Get Async().**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.getasync)</span><span class="sxs-lookup"><span data-stu-id="3f845-112">Then, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.get) or [**Get Async()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.getasync) method.</span></span>

```csharp
// IAggretagePartner partnerOperations;
// string countryCode;
// string offerId;

// retrieve the offer
var offer = partnerOperations.Offers.ByCountry(countryCode).ById(offerId).Get();
```

<span data-ttu-id="3f845-113">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="3f845-113">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="3f845-114">**Project:** PartnerSDK.FeatureSample-klass: GetOffer.cs </span><span class="sxs-lookup"><span data-stu-id="3f845-114">**Project**: PartnerSDK.FeatureSample **Class**: GetOffer.cs</span></span>

## <a name="java"></a><span data-ttu-id="3f845-115">Java</span><span class="sxs-lookup"><span data-stu-id="3f845-115">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="3f845-116">Om du vill hitta ett specifikt erbjudande efter ID använder du funktionen **IAggregatePartner.getOffers,** etablerar landet med ett anrop till funktionen **byCountry()** och anropar sedan **funktionen byID().**</span><span class="sxs-lookup"><span data-stu-id="3f845-116">To find a specific offer by ID, use your **IAggregatePartner.getOffers** function, establish the country with a call to the **byCountry()** function, and then call the **byID()** function.</span></span> <span data-ttu-id="3f845-117">Anropa sedan **funktionen get().**</span><span class="sxs-lookup"><span data-stu-id="3f845-117">Then call the **get()** function.</span></span>

```java
// IAggretagePartner partnerOperations;
// String countryCode;
// String offerId;

// Retrieve the offer
Offer offer = partnerOperations.getOffers().byCountry(countryCode).byId(offerId).get();
```

## <a name="powershell"></a><span data-ttu-id="3f845-118">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3f845-118">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="3f845-119">Om du vill hitta ett specifikt erbjudande efter ID kör du kommandot [**Get-PartnerOffer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOffer.md) och anger **parametrarna CountryCode** och **OfferId.**</span><span class="sxs-lookup"><span data-stu-id="3f845-119">To find a specific offer by ID, execute the [**Get-PartnerOffer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOffer.md) command, and specify the **CountryCode** and **OfferId** parameters.</span></span>

```powershell
# $countryCode
# $offerId

Get-PartnerOffer -Country $countryCode -OfferId $offerId
```

## <a name="rest-request"></a><span data-ttu-id="3f845-120">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="3f845-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3f845-121">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="3f845-121">Request syntax</span></span>

| <span data-ttu-id="3f845-122">Metod</span><span class="sxs-lookup"><span data-stu-id="3f845-122">Method</span></span>  | <span data-ttu-id="3f845-123">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="3f845-123">Request URI</span></span>                                                                                    |
|---------|------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3f845-124">**Få**</span><span class="sxs-lookup"><span data-stu-id="3f845-124">**GET**</span></span> | <span data-ttu-id="3f845-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/offers/{offer-id}?country={country-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="3f845-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/offers/{offer-id}?country={country-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="3f845-126">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="3f845-126">URI parameter</span></span>

| <span data-ttu-id="3f845-127">Namn</span><span class="sxs-lookup"><span data-stu-id="3f845-127">Name</span></span>           | <span data-ttu-id="3f845-128">Typ</span><span class="sxs-lookup"><span data-stu-id="3f845-128">Type</span></span>       | <span data-ttu-id="3f845-129">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="3f845-129">Required</span></span> | <span data-ttu-id="3f845-130">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="3f845-130">Description</span></span>                           |
|----------------|------------|----------|---------------------------------------|
| <span data-ttu-id="3f845-131">**erbjudande-id**</span><span class="sxs-lookup"><span data-stu-id="3f845-131">**offer-id**</span></span>   | <span data-ttu-id="3f845-132">**guid**</span><span class="sxs-lookup"><span data-stu-id="3f845-132">**guid**</span></span>   | <span data-ttu-id="3f845-133">Y</span><span class="sxs-lookup"><span data-stu-id="3f845-133">Y</span></span>        | <span data-ttu-id="3f845-134">Ett GUID som motsvarar erbjudandet.</span><span class="sxs-lookup"><span data-stu-id="3f845-134">A GUID that corresponds to the offer.</span></span> |
| <span data-ttu-id="3f845-135">**country-id**</span><span class="sxs-lookup"><span data-stu-id="3f845-135">**country-id**</span></span> | <span data-ttu-id="3f845-136">**sträng**</span><span class="sxs-lookup"><span data-stu-id="3f845-136">**string**</span></span> | <span data-ttu-id="3f845-137">Y</span><span class="sxs-lookup"><span data-stu-id="3f845-137">Y</span></span>        | <span data-ttu-id="3f845-138">Land/region-ID.</span><span class="sxs-lookup"><span data-stu-id="3f845-138">The country/region ID.</span></span>                |

### <a name="request-headers"></a><span data-ttu-id="3f845-139">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="3f845-139">Request headers</span></span>

- <span data-ttu-id="3f845-140">Ett **språk-ID** formaterat som en sträng krävs.</span><span class="sxs-lookup"><span data-stu-id="3f845-140">A **locale-id** formatted as a string is required.</span></span>
<span data-ttu-id="3f845-141">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="3f845-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3f845-142">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="3f845-142">Request body</span></span>

<span data-ttu-id="3f845-143">Inga.</span><span class="sxs-lookup"><span data-stu-id="3f845-143">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="3f845-144">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="3f845-144">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/offers/<offer-id>?country=<country-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
X-Locale: <locale-id>
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="3f845-145">REST-svar</span><span class="sxs-lookup"><span data-stu-id="3f845-145">REST response</span></span>

<span data-ttu-id="3f845-146">Om det lyckas returnerar den här metoden **en erbjudanderesurs** i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="3f845-146">If successful, this method returns an **Offer** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3f845-147">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="3f845-147">Response success and error codes</span></span>

<span data-ttu-id="3f845-148">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="3f845-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3f845-149">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="3f845-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3f845-150">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="3f845-150">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="3f845-151">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="3f845-151">Response example</span></span>

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
