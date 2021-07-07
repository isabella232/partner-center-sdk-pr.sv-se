---
title: Hämta en användningssammanfattning för en partner
description: Du kan använda resursen PartnerUsageSummary för att hämta en partneranvändningssammanfattning för alla kunder som har köpt en specifik Azure-tjänst eller -resurs under den aktuella faktureringsperioden.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: f003980f1b521ad0ac26dbfd0d4821b9096fdd27
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873912"
---
# <a name="get-a-usage-summary-for-a-partner"></a><span data-ttu-id="d7252-103">Hämta en användningssammanfattning för en partner</span><span class="sxs-lookup"><span data-stu-id="d7252-103">Get a usage summary for a partner</span></span>

<span data-ttu-id="d7252-104">**Gäller för**: Partner Center-| PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="d7252-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d7252-105">Du kan använda resursen **PartnerUsageSummary** för att få en partneranvändningssammanfattning för alla kunder som har köpt en specifik Azure-tjänst eller -resurs under den aktuella faktureringsperioden.</span><span class="sxs-lookup"><span data-stu-id="d7252-105">You can use the **PartnerUsageSummary** resource to get a partner usage summary of all customers that purchased a specific Azure service or resource during the current billing period.</span></span>

<span data-ttu-id="d7252-106">*Summan som returneras av det här API:et returnerar inte förbrukning för kunder som har en Azure-plan.*</span><span class="sxs-lookup"><span data-stu-id="d7252-106">*The total returned by this API will not return consumption for customers that have an Azure plan.*</span></span> <span data-ttu-id="d7252-107">Planerat för utfasning i framtiden.</span><span class="sxs-lookup"><span data-stu-id="d7252-107">Planned for deprecation in the future.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d7252-108">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="d7252-108">Prerequisites</span></span>

- <span data-ttu-id="d7252-109">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d7252-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d7252-110">Det här scenariot stöder endast autentisering med app+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="d7252-110">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="d7252-111">C\#</span><span class="sxs-lookup"><span data-stu-id="d7252-111">C\#</span></span>

<span data-ttu-id="d7252-112">Så här hämtar du en användningssammanfattning för alla kunder som har köpt en specifik Azure-tjänst eller -resurs under den aktuella faktureringsperioden:</span><span class="sxs-lookup"><span data-stu-id="d7252-112">To get a usage summary for all customers that purchased a specific Azure service or resource during the current billing period:</span></span>

1. <span data-ttu-id="d7252-113">Använd din **IAggregatePartner.**</span><span class="sxs-lookup"><span data-stu-id="d7252-113">Use your **IAggregatePartner**.</span></span>

2. <span data-ttu-id="d7252-114">Anropa egenskapen **UsageSummary** följt av **metoderna Get()** eller **GetAsync():**</span><span class="sxs-lookup"><span data-stu-id="d7252-114">Call the **UsageSummary** property, followed by the **Get()** or **GetAsync()** methods:</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;

    var usageSummary = partnerOperations.UsageSummary.Get();
    ```

<span data-ttu-id="d7252-115">Ett exempel finns i följande:</span><span class="sxs-lookup"><span data-stu-id="d7252-115">For an example, see the following:</span></span>

- <span data-ttu-id="d7252-116">Exempel: [Konsoltestapp](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="d7252-116">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="d7252-117">Project: **PartnerSDK.FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="d7252-117">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="d7252-118">Klass: **GetPartnerUsageSummary.cs**</span><span class="sxs-lookup"><span data-stu-id="d7252-118">Class: **GetPartnerUsageSummary.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="d7252-119">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="d7252-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d7252-120">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="d7252-120">Request syntax</span></span>

| <span data-ttu-id="d7252-121">Metod</span><span class="sxs-lookup"><span data-stu-id="d7252-121">Method</span></span>  | <span data-ttu-id="d7252-122">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="d7252-122">Request URI</span></span>                                                         |
|---------|---------------------------------------------------------------------|
| <span data-ttu-id="d7252-123">**Få**</span><span class="sxs-lookup"><span data-stu-id="d7252-123">**GET**</span></span> | <span data-ttu-id="d7252-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/usagesummary HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d7252-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/usagesummary HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d7252-125">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="d7252-125">Request headers</span></span>

<span data-ttu-id="d7252-126">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="d7252-126">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d7252-127">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="d7252-127">Request body</span></span>

<span data-ttu-id="d7252-128">Inga.</span><span class="sxs-lookup"><span data-stu-id="d7252-128">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d7252-129">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="d7252-129">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="d7252-130">REST-svar</span><span class="sxs-lookup"><span data-stu-id="d7252-130">REST response</span></span>

<span data-ttu-id="d7252-131">Om det lyckas returnerar den här metoden **en PartnerUsageSummary-resurs** i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="d7252-131">If successful, this method returns a **PartnerUsageSummary** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d7252-132">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="d7252-132">Response success and error codes</span></span>

<span data-ttu-id="d7252-133">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="d7252-133">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d7252-134">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="d7252-134">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="d7252-135">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="d7252-135">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d7252-136">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="d7252-136">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "customersOverBudget": 1,
    "customersTrendingOver": 0,
    "customersWithUsageBasedSubscription": 11,
    "resourceId": "11111111-4574-4539-bc42-0e539b9684c0",
    "id": "11111111-4574-4539-bc42-0e539b9684c0",
    "resourceName": "PLAMUATT2NETNEW",
    "name": "PLAMUATT2NETNEW",
    "billingStartDate": "2019-08-28T00:00:00-07:00",
    "billingEndDate": "2019-09-27T00:00:00-07:00",
    "totalCost": 22.861172,
    "currencyLocale": "fr-FR",
    "lastModifiedDate": "2019-09-01T23:04:41.193+00:00",
    "links": {
        "self": {
            "uri": "/usagesummary",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "PartnerUsageSummary"
    }
}
```
