---
title: Hämta en lista över erbjudandekategorier efter marknad
description: Lär dig hur du hämtar en samling som innehåller alla erbjudandekategorier i ett visst land/en viss region och språk för alla Microsoft-moln.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: e699355f07dda3941eafed32f5f635d94000abd1
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874286"
---
# <a name="get-a-list-of-offer-categories-by-market"></a><span data-ttu-id="2f000-103">Hämta en lista över erbjudandekategorier efter marknad</span><span class="sxs-lookup"><span data-stu-id="2f000-103">Get a list of offer categories by market</span></span>

<span data-ttu-id="2f000-104">**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="2f000-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="2f000-105">Den här artikeln beskriver hur du hämtar en samling som innehåller alla erbjudandekategorier i ett visst land/region och språk.</span><span class="sxs-lookup"><span data-stu-id="2f000-105">This article describes how to get a collection that contains all the offer categories in a given country/region and locale.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f000-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="2f000-106">Prerequisites</span></span>

- <span data-ttu-id="2f000-107">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="2f000-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2f000-108">Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="2f000-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="2f000-109">C\#</span><span class="sxs-lookup"><span data-stu-id="2f000-109">C\#</span></span>

<span data-ttu-id="2f000-110">Så här hämtar du en lista över erbjudandekategorier i ett visst land/region och språk:</span><span class="sxs-lookup"><span data-stu-id="2f000-110">To get a list of offer categories in a given country/region and locale:</span></span>

1. <span data-ttu-id="2f000-111">Använd din [**IAggregatePartner.Operations-samling**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) för att anropa [**metoden With()**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner.with) i en viss kontext.</span><span class="sxs-lookup"><span data-stu-id="2f000-111">Use your [**IAggregatePartner.Operations**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) collection to call the [**With()**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner.with) method on a given context.</span></span>

2. <span data-ttu-id="2f000-112">Kontrollera egenskapen [**OfferCategories**](/dotnet/api/microsoft.store.partnercenter.ipartner.offercategories) för det resulterande objektet.</span><span class="sxs-lookup"><span data-stu-id="2f000-112">Inspect the [**OfferCategories**](/dotnet/api/microsoft.store.partnercenter.ipartner.offercategories) property of the resulting object.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

ResourceCollection<OfferCategory> offerCategoryResults = partnerOperations.With(RequestContextFactory.Instance.Create()).OfferCategories.ByCountry("US").Get();
```

<span data-ttu-id="2f000-113">Ett exempel finns i följande:</span><span class="sxs-lookup"><span data-stu-id="2f000-113">For an example, see the following:</span></span>

- <span data-ttu-id="2f000-114">Exempel: [Konsoltestapp](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="2f000-114">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="2f000-115">Project: **PartnerSDK.FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="2f000-115">Project: **PartnerSDK.FeatureSample**</span></span>
- <span data-ttu-id="2f000-116">Klass: **PartnerSDK.FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="2f000-116">Class: **PartnerSDK.FeatureSample**</span></span>

## <a name="rest-request"></a><span data-ttu-id="2f000-117">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="2f000-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2f000-118">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="2f000-118">Request syntax</span></span>

| <span data-ttu-id="2f000-119">Metod</span><span class="sxs-lookup"><span data-stu-id="2f000-119">Method</span></span>  | <span data-ttu-id="2f000-120">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="2f000-120">Request URI</span></span>                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="2f000-121">**Få**</span><span class="sxs-lookup"><span data-stu-id="2f000-121">**GET**</span></span> | <span data-ttu-id="2f000-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/offercategories?country={country-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="2f000-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/offercategories?country={country-id} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="2f000-123">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="2f000-123">URI parameter</span></span>

<span data-ttu-id="2f000-124">I den här tabellen visas de frågeparametrar som krävs för att hämta erbjudandekategorierna.</span><span class="sxs-lookup"><span data-stu-id="2f000-124">This table lists the required query parameters to get the offer categories.</span></span>

| <span data-ttu-id="2f000-125">Namn</span><span class="sxs-lookup"><span data-stu-id="2f000-125">Name</span></span>           | <span data-ttu-id="2f000-126">Typ</span><span class="sxs-lookup"><span data-stu-id="2f000-126">Type</span></span>       | <span data-ttu-id="2f000-127">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="2f000-127">Required</span></span> | <span data-ttu-id="2f000-128">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="2f000-128">Description</span></span>            |
|----------------|------------|----------|------------------------|
| <span data-ttu-id="2f000-129">**lands-id**</span><span class="sxs-lookup"><span data-stu-id="2f000-129">**country-id**</span></span> | <span data-ttu-id="2f000-130">**sträng**</span><span class="sxs-lookup"><span data-stu-id="2f000-130">**string**</span></span> | <span data-ttu-id="2f000-131">Y</span><span class="sxs-lookup"><span data-stu-id="2f000-131">Y</span></span>        | <span data-ttu-id="2f000-132">Land/region-ID.</span><span class="sxs-lookup"><span data-stu-id="2f000-132">The country/region ID.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="2f000-133">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="2f000-133">Request headers</span></span>

<span data-ttu-id="2f000-134">Ett **språk-ID formaterat** som en sträng krävs.</span><span class="sxs-lookup"><span data-stu-id="2f000-134">A **locale-id** formatted as a string is required.</span></span>

<span data-ttu-id="2f000-135">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="2f000-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2f000-136">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="2f000-136">Request body</span></span>

<span data-ttu-id="2f000-137">Inga.</span><span class="sxs-lookup"><span data-stu-id="2f000-137">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="2f000-138">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="2f000-138">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/offercategories?country=<country-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fb54bd5-a4c3-4fac-955f-9b6e3436d606
MS-CorrelationId: 47882653-eaed-4a2e-a552-1070a3fa1089
X-Locale: <locale-id>
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="2f000-139">REST-svar</span><span class="sxs-lookup"><span data-stu-id="2f000-139">REST response</span></span>

<span data-ttu-id="2f000-140">Om det lyckas returnerar den här metoden en samling **OfferCategory-resurser** i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="2f000-140">If successful, this method returns a collection of **OfferCategory** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2f000-141">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="2f000-141">Response success and error codes</span></span>

<span data-ttu-id="2f000-142">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="2f000-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2f000-143">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="2f000-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2f000-144">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="2f000-144">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2f000-145">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="2f000-145">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1184
Content-Type: application/json
MS-CorrelationId: 47882653-eaed-4a2e-a552-1070a3fa1089
MS-RequestId: 4fb54bd5-a4c3-4fac-955f-9b6e3436d606
Date: Thu, 26 Nov 2015 00:07:10 GMT

{
    "totalCount": 4,
    "items": [{
        "id": "Enterprise_Key",
        "name": "Enterprise",
        "rank": 20,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "SmallBusiness_Key",
        "name": "SmallBusiness",
        "rank": 30,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "Government_Key",
        "name": "Government",
        "rank": 40,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "Internal_Key",
        "name": "Internal",
        "rank": 100,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}
```
