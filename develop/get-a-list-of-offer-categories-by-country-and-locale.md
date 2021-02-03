---
title: Hämta en lista över erbjudandekategorier efter marknad
description: Hämta en samling som innehåller alla erbjudande kategorier i ett specifikt land/region och nationella inställningar.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 22c46ed03a8579c53ee18c14cbca9a1e19ddb82a
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769543"
---
# <a name="get-a-list-of-offer-categories-by-market"></a><span data-ttu-id="e7ff4-103">Hämta en lista över erbjudandekategorier efter marknad</span><span class="sxs-lookup"><span data-stu-id="e7ff4-103">Get a list of offer categories by market</span></span>

<span data-ttu-id="e7ff4-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="e7ff4-104">**Applies to:**</span></span>

- <span data-ttu-id="e7ff4-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="e7ff4-105">Partner Center</span></span>
- <span data-ttu-id="e7ff4-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="e7ff4-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="e7ff4-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="e7ff4-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="e7ff4-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="e7ff4-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="e7ff4-109">Den här artikeln beskriver hur du hämtar en samling som innehåller alla erbjudande kategorier i ett specifikt land/region och nationella inställningar.</span><span class="sxs-lookup"><span data-stu-id="e7ff4-109">This article describes how to get a collection that contains all the offer categories in a given country/region and locale.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e7ff4-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="e7ff4-110">Prerequisites</span></span>

- <span data-ttu-id="e7ff4-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e7ff4-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e7ff4-112">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="e7ff4-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="e7ff4-113">C\#</span><span class="sxs-lookup"><span data-stu-id="e7ff4-113">C\#</span></span>

<span data-ttu-id="e7ff4-114">Så här hämtar du en lista över erbjudande kategorier i ett specifikt land/region och nationella inställningar:</span><span class="sxs-lookup"><span data-stu-id="e7ff4-114">To get a list of offer categories in a given country/region and locale:</span></span>

1. <span data-ttu-id="e7ff4-115">Använd din [**IAggregatePartner. Operations**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) -samling för att anropa metoden [**with ()**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner.with) i en specifik kontext.</span><span class="sxs-lookup"><span data-stu-id="e7ff4-115">Use your [**IAggregatePartner.Operations**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) collection to call the [**With()**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner.with) method on a given context.</span></span>

2. <span data-ttu-id="e7ff4-116">Kontrol lera egenskapen [**OfferCategories**](/dotnet/api/microsoft.store.partnercenter.ipartner.offercategories) för det resulterande objektet.</span><span class="sxs-lookup"><span data-stu-id="e7ff4-116">Inspect the [**OfferCategories**](/dotnet/api/microsoft.store.partnercenter.ipartner.offercategories) property of the resulting object.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

ResourceCollection<OfferCategory> offerCategoryResults = partnerOperations.With(RequestContextFactory.Instance.Create()).OfferCategories.ByCountry("US").Get();
```

<span data-ttu-id="e7ff4-117">Ett exempel finns i följande avsnitt:</span><span class="sxs-lookup"><span data-stu-id="e7ff4-117">For an example, see the following:</span></span>

- <span data-ttu-id="e7ff4-118">Exempel: [konsol test app](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="e7ff4-118">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="e7ff4-119">Projekt: **PartnerSDK. FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="e7ff4-119">Project: **PartnerSDK.FeatureSample**</span></span>
- <span data-ttu-id="e7ff4-120">Klass: **PartnerSDK. FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="e7ff4-120">Class: **PartnerSDK.FeatureSample**</span></span>

## <a name="rest-request"></a><span data-ttu-id="e7ff4-121">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="e7ff4-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e7ff4-122">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="e7ff4-122">Request syntax</span></span>

| <span data-ttu-id="e7ff4-123">Metod</span><span class="sxs-lookup"><span data-stu-id="e7ff4-123">Method</span></span>  | <span data-ttu-id="e7ff4-124">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="e7ff4-124">Request URI</span></span>                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="e7ff4-125">**TA**</span><span class="sxs-lookup"><span data-stu-id="e7ff4-125">**GET**</span></span> | <span data-ttu-id="e7ff4-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/offercategories? land = {Country-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="e7ff4-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/offercategories?country={country-id} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="e7ff4-127">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="e7ff4-127">URI parameter</span></span>

<span data-ttu-id="e7ff4-128">Den här tabellen innehåller de frågeparametrar som krävs för att hämta erbjudande kategorier.</span><span class="sxs-lookup"><span data-stu-id="e7ff4-128">This table lists the required query parameters to get the offer categories.</span></span>

| <span data-ttu-id="e7ff4-129">Namn</span><span class="sxs-lookup"><span data-stu-id="e7ff4-129">Name</span></span>           | <span data-ttu-id="e7ff4-130">Typ</span><span class="sxs-lookup"><span data-stu-id="e7ff4-130">Type</span></span>       | <span data-ttu-id="e7ff4-131">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="e7ff4-131">Required</span></span> | <span data-ttu-id="e7ff4-132">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="e7ff4-132">Description</span></span>            |
|----------------|------------|----------|------------------------|
| <span data-ttu-id="e7ff4-133">**lands-ID**</span><span class="sxs-lookup"><span data-stu-id="e7ff4-133">**country-id**</span></span> | <span data-ttu-id="e7ff4-134">**nollängd**</span><span class="sxs-lookup"><span data-stu-id="e7ff4-134">**string**</span></span> | <span data-ttu-id="e7ff4-135">Y</span><span class="sxs-lookup"><span data-stu-id="e7ff4-135">Y</span></span>        | <span data-ttu-id="e7ff4-136">Land/region-ID.</span><span class="sxs-lookup"><span data-stu-id="e7ff4-136">The country/region ID.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e7ff4-137">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="e7ff4-137">Request headers</span></span>

<span data-ttu-id="e7ff4-138">Ett **språkvariant-ID** som är formaterat som en sträng krävs.</span><span class="sxs-lookup"><span data-stu-id="e7ff4-138">A **locale-id** formatted as a string is required.</span></span>

<span data-ttu-id="e7ff4-139">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="e7ff4-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e7ff4-140">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="e7ff4-140">Request body</span></span>

<span data-ttu-id="e7ff4-141">Inga.</span><span class="sxs-lookup"><span data-stu-id="e7ff4-141">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="e7ff4-142">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="e7ff4-142">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/offercategories?country=<country-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fb54bd5-a4c3-4fac-955f-9b6e3436d606
MS-CorrelationId: 47882653-eaed-4a2e-a552-1070a3fa1089
X-Locale: <locale-id>
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="e7ff4-143">REST-svar</span><span class="sxs-lookup"><span data-stu-id="e7ff4-143">REST response</span></span>

<span data-ttu-id="e7ff4-144">Om det lyckas returnerar den här metoden en samling **OfferCategory** -resurser i svars texten.</span><span class="sxs-lookup"><span data-stu-id="e7ff4-144">If successful, this method returns a collection of **OfferCategory** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e7ff4-145">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="e7ff4-145">Response success and error codes</span></span>

<span data-ttu-id="e7ff4-146">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="e7ff4-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e7ff4-147">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="e7ff4-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e7ff4-148">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e7ff4-148">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e7ff4-149">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="e7ff4-149">Response example</span></span>

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
