---
title: Hämta en lista över erbjudanden för en marknad
description: Hämtar en samling som innehåller alla erbjudanden för en specifik marknad.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 6f4fd821879545db4e781fe3202c8ee11f167615
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874252"
---
# <a name="get-a-list-of-offers-for-a-market"></a><span data-ttu-id="e4916-103">Hämta en lista över erbjudanden för en marknad</span><span class="sxs-lookup"><span data-stu-id="e4916-103">Get a list of offers for a market</span></span>

<span data-ttu-id="e4916-104">**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="e4916-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="e4916-105">Hämtar en samling som innehåller alla erbjudanden för en specifik marknad.</span><span class="sxs-lookup"><span data-stu-id="e4916-105">Gets a collection that contains all the offers for a specific market.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e4916-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="e4916-106">Prerequisites</span></span>

- <span data-ttu-id="e4916-107">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="e4916-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e4916-108">Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="e4916-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="e4916-109">C\#</span><span class="sxs-lookup"><span data-stu-id="e4916-109">C\#</span></span>

<span data-ttu-id="e4916-110">Om du vill hämta en lista över erbjudanden på en viss marknad använder du **samlingen IAggregatePartner.Offers,** väljer marknad efter land och anropar metoden **Get()** eller **Get Async().**</span><span class="sxs-lookup"><span data-stu-id="e4916-110">To get a list of offers in a given market, use your **IAggregatePartner.Offers** collection, select the market by country, and call the **Get()** or **Get Async()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

ResourceCollection<Offer> offers = partnerOperations.Offers.ByCountry("US").Get();
```

<span data-ttu-id="e4916-111">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="e4916-111">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="e4916-112">**Project:** PartnerSDK.FeatureSample-klass: Offers.cs </span><span class="sxs-lookup"><span data-stu-id="e4916-112">**Project**: PartnerSDK.FeatureSample **Class**: Offers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="e4916-113">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="e4916-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e4916-114">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="e4916-114">Request syntax</span></span>

| <span data-ttu-id="e4916-115">Metod</span><span class="sxs-lookup"><span data-stu-id="e4916-115">Method</span></span>  | <span data-ttu-id="e4916-116">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="e4916-116">Request URI</span></span>                                                                          |
|---------|--------------------------------------------------------------------------------------|
| <span data-ttu-id="e4916-117">**Få**</span><span class="sxs-lookup"><span data-stu-id="e4916-117">**GET**</span></span> | <span data-ttu-id="e4916-118">[*{baseURL}*](partner-center-rest-urls.md)/v1/offers?country={country-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e4916-118">[*{baseURL}*](partner-center-rest-urls.md)/v1/offers?country={country-id} HTTP/1.1</span></span>   |

### <a name="uri-parameter"></a><span data-ttu-id="e4916-119">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="e4916-119">URI parameter</span></span>

<span data-ttu-id="e4916-120">I den här tabellen visas de frågeparametrar som krävs för att hämta erbjudandena.</span><span class="sxs-lookup"><span data-stu-id="e4916-120">This table lists the required query parameters to get the offers.</span></span>

| <span data-ttu-id="e4916-121">Namn</span><span class="sxs-lookup"><span data-stu-id="e4916-121">Name</span></span>           | <span data-ttu-id="e4916-122">Typ</span><span class="sxs-lookup"><span data-stu-id="e4916-122">Type</span></span>       | <span data-ttu-id="e4916-123">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="e4916-123">Required</span></span> | <span data-ttu-id="e4916-124">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="e4916-124">Description</span></span>            |
|----------------|------------|----------|------------------------|
| <span data-ttu-id="e4916-125">**country-id**</span><span class="sxs-lookup"><span data-stu-id="e4916-125">**country-id**</span></span> | <span data-ttu-id="e4916-126">**sträng**</span><span class="sxs-lookup"><span data-stu-id="e4916-126">**string**</span></span> | <span data-ttu-id="e4916-127">Y</span><span class="sxs-lookup"><span data-stu-id="e4916-127">Y</span></span>        | <span data-ttu-id="e4916-128">Land/region-ID.</span><span class="sxs-lookup"><span data-stu-id="e4916-128">The country/region ID.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e4916-129">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="e4916-129">Request headers</span></span>

- <span data-ttu-id="e4916-130">Ett **språk-ID** formaterat som en sträng krävs.</span><span class="sxs-lookup"><span data-stu-id="e4916-130">A **locale-id** formatted as a string is required.</span></span>
<span data-ttu-id="e4916-131">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="e4916-131">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e4916-132">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="e4916-132">Request body</span></span>

<span data-ttu-id="e4916-133">Inga.</span><span class="sxs-lookup"><span data-stu-id="e4916-133">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="e4916-134">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="e4916-134">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/offers?country=<country-id> HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
X-Locale: <locale-id>
```

## <a name="rest-response"></a><span data-ttu-id="e4916-135">REST-svar</span><span class="sxs-lookup"><span data-stu-id="e4916-135">REST response</span></span>

<span data-ttu-id="e4916-136">Om det lyckas returnerar den här metoden en samling **erbjudanderesurser** i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="e4916-136">If successful, this method returns a collection of **Offer** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e4916-137">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="e4916-137">Response success and error codes</span></span>

<span data-ttu-id="e4916-138">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="e4916-138">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e4916-139">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="e4916-139">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e4916-140">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="e4916-140">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e4916-141">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="e4916-141">Response example</span></span>

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
