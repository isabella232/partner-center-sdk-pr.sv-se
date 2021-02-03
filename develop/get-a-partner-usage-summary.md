---
title: Få en användnings översikt för en partner
description: Du kan använda PartnerUsageSummary-resursen för att få en översikt över partner användningen av alla kunder som har köpt en viss Azure-tjänst eller resurs under den aktuella fakturerings perioden.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: ba1885f46043a75274595239fe61ce3ef0998acf
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769036"
---
# <a name="get-a-usage-summary-for-a-partner"></a><span data-ttu-id="52616-103">Få en användnings översikt för en partner</span><span class="sxs-lookup"><span data-stu-id="52616-103">Get a usage summary for a partner</span></span>

<span data-ttu-id="52616-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="52616-104">**Applies to:**</span></span>

- <span data-ttu-id="52616-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="52616-105">Partner Center</span></span>
- <span data-ttu-id="52616-106">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="52616-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="52616-107">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="52616-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="52616-108">Du kan använda **PartnerUsageSummary** -resursen för att få en översikt över partner användningen av alla kunder som har köpt en viss Azure-tjänst eller resurs under den aktuella fakturerings perioden.</span><span class="sxs-lookup"><span data-stu-id="52616-108">You can use the **PartnerUsageSummary** resource to get a partner usage summary of all customers that purchased a specific Azure service or resource during the current billing period.</span></span>

<span data-ttu-id="52616-109">*Det totala antalet som returneras av detta API returnerar inte förbrukning för kunder som har en Azure-plan.*</span><span class="sxs-lookup"><span data-stu-id="52616-109">*The total returned by this API will not return consumption for customers that have an Azure plan.*</span></span> <span data-ttu-id="52616-110">Planerat för utfasning i framtiden.</span><span class="sxs-lookup"><span data-stu-id="52616-110">Planned for deprecation in the future.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52616-111">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="52616-111">Prerequisites</span></span>

- <span data-ttu-id="52616-112">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="52616-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="52616-113">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="52616-113">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="52616-114">C\#</span><span class="sxs-lookup"><span data-stu-id="52616-114">C\#</span></span>

<span data-ttu-id="52616-115">För att få en användnings översikt för alla kunder som har köpt en viss Azure-tjänst eller resurs under den aktuella fakturerings perioden:</span><span class="sxs-lookup"><span data-stu-id="52616-115">To get a usage summary for all customers that purchased a specific Azure service or resource during the current billing period:</span></span>

1. <span data-ttu-id="52616-116">Använd din **IAggregatePartner**.</span><span class="sxs-lookup"><span data-stu-id="52616-116">Use your **IAggregatePartner**.</span></span>

2. <span data-ttu-id="52616-117">Anropa egenskapen **UsageSummary** följt av metoderna **Get ()** eller **GetAsync ()** :</span><span class="sxs-lookup"><span data-stu-id="52616-117">Call the **UsageSummary** property, followed by the **Get()** or **GetAsync()** methods:</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;

    var usageSummary = partnerOperations.UsageSummary.Get();
    ```

<span data-ttu-id="52616-118">Ett exempel finns i följande avsnitt:</span><span class="sxs-lookup"><span data-stu-id="52616-118">For an example, see the following:</span></span>

- <span data-ttu-id="52616-119">Exempel: [konsol test app](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="52616-119">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="52616-120">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="52616-120">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="52616-121">Klass: **GetPartnerUsageSummary.cs**</span><span class="sxs-lookup"><span data-stu-id="52616-121">Class: **GetPartnerUsageSummary.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="52616-122">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="52616-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="52616-123">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="52616-123">Request syntax</span></span>

| <span data-ttu-id="52616-124">Metod</span><span class="sxs-lookup"><span data-stu-id="52616-124">Method</span></span>  | <span data-ttu-id="52616-125">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="52616-125">Request URI</span></span>                                                         |
|---------|---------------------------------------------------------------------|
| <span data-ttu-id="52616-126">**TA**</span><span class="sxs-lookup"><span data-stu-id="52616-126">**GET**</span></span> | <span data-ttu-id="52616-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/usagesummary http/1.1</span><span class="sxs-lookup"><span data-stu-id="52616-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/usagesummary HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="52616-128">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="52616-128">Request headers</span></span>

<span data-ttu-id="52616-129">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="52616-129">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="52616-130">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="52616-130">Request body</span></span>

<span data-ttu-id="52616-131">Inga.</span><span class="sxs-lookup"><span data-stu-id="52616-131">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="52616-132">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="52616-132">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="52616-133">REST-svar</span><span class="sxs-lookup"><span data-stu-id="52616-133">REST response</span></span>

<span data-ttu-id="52616-134">Om det lyckas returnerar den här metoden en **PartnerUsageSummary** -resurs i svars texten.</span><span class="sxs-lookup"><span data-stu-id="52616-134">If successful, this method returns a **PartnerUsageSummary** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="52616-135">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="52616-135">Response success and error codes</span></span>

<span data-ttu-id="52616-136">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="52616-136">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="52616-137">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="52616-137">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="52616-138">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="52616-138">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="52616-139">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="52616-139">Response example</span></span>

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
