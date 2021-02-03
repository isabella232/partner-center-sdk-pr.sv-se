---
title: Hämta en lista över erbjudanden för en marknad
description: Hämtar en samling som innehåller alla erbjudanden för en speciell marknad.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 3a004f6f8f8de8cd398d82c300793e4f196efaaa
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769108"
---
# <a name="get-a-list-of-offers-for-a-market"></a><span data-ttu-id="b85eb-103">Hämta en lista över erbjudanden för en marknad</span><span class="sxs-lookup"><span data-stu-id="b85eb-103">Get a list of offers for a market</span></span>

<span data-ttu-id="b85eb-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="b85eb-104">**Applies To**</span></span>

- <span data-ttu-id="b85eb-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="b85eb-105">Partner Center</span></span>
- <span data-ttu-id="b85eb-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="b85eb-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="b85eb-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="b85eb-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="b85eb-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="b85eb-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="b85eb-109">Hämtar en samling som innehåller alla erbjudanden för en speciell marknad.</span><span class="sxs-lookup"><span data-stu-id="b85eb-109">Gets a collection that contains all the offers for a specific market.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b85eb-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="b85eb-110">Prerequisites</span></span>

- <span data-ttu-id="b85eb-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b85eb-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b85eb-112">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="b85eb-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="b85eb-113">C\#</span><span class="sxs-lookup"><span data-stu-id="b85eb-113">C\#</span></span>

<span data-ttu-id="b85eb-114">Om du vill hämta en lista över erbjudanden på en specifik marknad använder du din **IAggregatePartner.** samling, Välj marknaden efter land och anropa metoden **Get ()** eller **Get async ()** .</span><span class="sxs-lookup"><span data-stu-id="b85eb-114">To get a list of offers in a given market, use your **IAggregatePartner.Offers** collection, select the market by country, and call the **Get()** or **Get Async()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

ResourceCollection<Offer> offers = partnerOperations.Offers.ByCountry("US").Get();
```

<span data-ttu-id="b85eb-115">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="b85eb-115">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="b85eb-116">**Projekt**: PartnerSDK. FeatureSample- **klass**: offers.CS</span><span class="sxs-lookup"><span data-stu-id="b85eb-116">**Project**: PartnerSDK.FeatureSample **Class**: Offers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="b85eb-117">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="b85eb-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b85eb-118">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="b85eb-118">Request syntax</span></span>

| <span data-ttu-id="b85eb-119">Metod</span><span class="sxs-lookup"><span data-stu-id="b85eb-119">Method</span></span>  | <span data-ttu-id="b85eb-120">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="b85eb-120">Request URI</span></span>                                                                          |
|---------|--------------------------------------------------------------------------------------|
| <span data-ttu-id="b85eb-121">**TA**</span><span class="sxs-lookup"><span data-stu-id="b85eb-121">**GET**</span></span> | <span data-ttu-id="b85eb-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/offers? land = {Country-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="b85eb-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/offers?country={country-id} HTTP/1.1</span></span>   |

### <a name="uri-parameter"></a><span data-ttu-id="b85eb-123">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="b85eb-123">URI parameter</span></span>

<span data-ttu-id="b85eb-124">Den här tabellen innehåller de frågeparametrar som krävs för att hämta erbjudandena.</span><span class="sxs-lookup"><span data-stu-id="b85eb-124">This table lists the required query parameters to get the offers.</span></span>

| <span data-ttu-id="b85eb-125">Namn</span><span class="sxs-lookup"><span data-stu-id="b85eb-125">Name</span></span>           | <span data-ttu-id="b85eb-126">Typ</span><span class="sxs-lookup"><span data-stu-id="b85eb-126">Type</span></span>       | <span data-ttu-id="b85eb-127">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="b85eb-127">Required</span></span> | <span data-ttu-id="b85eb-128">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="b85eb-128">Description</span></span>            |
|----------------|------------|----------|------------------------|
| <span data-ttu-id="b85eb-129">**lands-ID**</span><span class="sxs-lookup"><span data-stu-id="b85eb-129">**country-id**</span></span> | <span data-ttu-id="b85eb-130">**nollängd**</span><span class="sxs-lookup"><span data-stu-id="b85eb-130">**string**</span></span> | <span data-ttu-id="b85eb-131">Y</span><span class="sxs-lookup"><span data-stu-id="b85eb-131">Y</span></span>        | <span data-ttu-id="b85eb-132">Land/region-ID.</span><span class="sxs-lookup"><span data-stu-id="b85eb-132">The country/region ID.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b85eb-133">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="b85eb-133">Request headers</span></span>

- <span data-ttu-id="b85eb-134">Ett **språkvariant-ID** som är formaterat som en sträng krävs.</span><span class="sxs-lookup"><span data-stu-id="b85eb-134">A **locale-id** formatted as a string is required.</span></span>
<span data-ttu-id="b85eb-135">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b85eb-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b85eb-136">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="b85eb-136">Request body</span></span>

<span data-ttu-id="b85eb-137">Inga.</span><span class="sxs-lookup"><span data-stu-id="b85eb-137">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="b85eb-138">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="b85eb-138">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/offers?country=<country-id> HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
X-Locale: <locale-id>
```

## <a name="rest-response"></a><span data-ttu-id="b85eb-139">REST-svar</span><span class="sxs-lookup"><span data-stu-id="b85eb-139">REST response</span></span>

<span data-ttu-id="b85eb-140">Om det lyckas returnerar den här metoden en samling **erbjudande** resurser i svars texten.</span><span class="sxs-lookup"><span data-stu-id="b85eb-140">If successful, this method returns a collection of **Offer** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b85eb-141">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="b85eb-141">Response success and error codes</span></span>

<span data-ttu-id="b85eb-142">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="b85eb-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b85eb-143">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="b85eb-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b85eb-144">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b85eb-144">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b85eb-145">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="b85eb-145">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 26584
Content-Type: application/json
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
Date: Mon, 23 Nov 2015 23:20:44 GMT

{
    "totalCount":12,"items":[{
        "id":"E60E0348-1710-484B-992A-32B294D4CDE1",
        "name":"Azure Rights Management Premium (Government Pricing)",
        "description":"Microsoft Azure Rights Management Premium helps you protect confidential documents and email with strong encryption.
                       Control the use of your information by specifying who can view, edit, print, save and share your data.
                       Simple to use and integrated with Microsoft Office, SharePoint and Exchange.",
        "minimumQuantity":1,
        "maximumQuantity":10000000,
        "rank":5,
        "uri":"/3c95518e-8c37-41e3-9627-0ca339200f53/Offers/E60E0348-1710-484B-992A-32B294D4CDE1",
        "locale":"EN-US",
        "country":"US",
        "category":{
            "id":"Government_Key",
            "name":"Government",
            "rank":40,
            "locale":"en-us",
            "country":"US",
            "attributes":{
                "objectType":"OfferCategory"
            }
        },
        "prerequisiteOffers":[],
        "isAddOn":false,
        "isAvailableForPurchase":true,
        "billing":"license",
        "isAutoRenewable":true,
        "product":{
            "id":"c52ea49f-fe5d-4e95-93ba-1de91d380f89",
            "name":"Azure Rights Management Premium",
            "unit":"Licenses"
        },
        "unitType":"Licenses",
        "links":{
            "learnMore":{
                "uri":"http://g.microsoftonline.com/0BXPS00en/0000",
                "method":"GET",
                "headers":[]
            },
            "self":{
                "uri":"/offers/E60E0348-1710-484B-992A-32B294D4CDE1",
                "method":"GET",
                "headers":[]
            }
        },
        "attributes":{
            "objectType":"Offer"
        }
    },
    "links":{
        "self":{
            "uri":"/v1/offers?country={country-id}",
            "method":"GET",
            "headers":[]
        },
        "previous":{
            "uri":"/v1/offers?country={country-id}",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "objectType":"Collection"
    }
}
```
