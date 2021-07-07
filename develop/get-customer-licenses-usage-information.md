---
title: Hämta information om kundlicensanvändning
description: Så här hämtar du information om licensers användning för en specifik kund.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: cfec12d37ce4f5f50baad57bfd45770388f8a2dc
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446436"
---
# <a name="get-customer-licenses-usage-information"></a><span data-ttu-id="864f2-103">Hämta information om kundlicensanvändning</span><span class="sxs-lookup"><span data-stu-id="864f2-103">Get customer licenses usage information</span></span>

<span data-ttu-id="864f2-104">Så här hämtar du information om licensdistribution för en specifik kund.</span><span class="sxs-lookup"><span data-stu-id="864f2-104">How to get licenses deployment insights for a specific customer.</span></span>

> [!NOTE]
> <span data-ttu-id="864f2-105">Det här scenariot ersätts av [Hämta användningsinformation om licenser.](get-licenses-usage-information.md)</span><span class="sxs-lookup"><span data-stu-id="864f2-105">This scenario is superceded by [Get licenses usage information](get-licenses-usage-information.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="864f2-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="864f2-106">Prerequisites</span></span>

<span data-ttu-id="864f2-107">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="864f2-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="864f2-108">Det här scenariot stöder autentisering med autentiseringsuppgifter för App+Användare.</span><span class="sxs-lookup"><span data-stu-id="864f2-108">This scenario supports authentication with App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="864f2-109">C\#</span><span class="sxs-lookup"><span data-stu-id="864f2-109">C\#</span></span>

<span data-ttu-id="864f2-110">Om du vill hämta aggregerade data vid distributionen för en angiven kund anropar du först [**metoden IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="864f2-110">To retrieve aggregated data on deployment for a specified customer, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="864f2-111">Hämta sedan ett gränssnitt för insamlingsåtgärder på kundnivå från [**egenskapen**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.analytics) Analytics.</span><span class="sxs-lookup"><span data-stu-id="864f2-111">Then get an interface to customer level analytics collection operations from the [**Analytics**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.analytics) property.</span></span> <span data-ttu-id="864f2-112">Hämta sedan ett gränssnitt till analyssamlingen för licenser på kundnivå [**från**](/dotnet/api/microsoft.store.partnercenter.analytics.icustomeranalyticscollection.licenses) egenskapen Licenser.</span><span class="sxs-lookup"><span data-stu-id="864f2-112">Next, retrieve an interface to the customer level licenses analytics collection from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.icustomeranalyticscollection.licenses) property.</span></span> <span data-ttu-id="864f2-113">Anropa slutligen metoden [**Usage.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) för att hämta aggregerade data om licensanvändningen.</span><span class="sxs-lookup"><span data-stu-id="864f2-113">Finally, call the [**Usage.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) method to get the aggregated data on licenses usage.</span></span> <span data-ttu-id="864f2-114">Om metoden lyckas får du en samling [**customerLicensesUsageInsights-objekt.**](/dotnet/api/microsoft.store.partnercenter.models.analytics.customerlicensesusageinsights)</span><span class="sxs-lookup"><span data-stu-id="864f2-114">If the method succeeds, you'll get a collection of [**CustomerLicensesUsageInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.customerlicensesusageinsights) objects.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerIdToRetrieve;

var customerLicensesDeploymentAnalytics = partnerOperations.Customers.ById(customerIdToRetrieve).Analytics.Licenses.Usage.Get();
```

## <a name="rest-request"></a><span data-ttu-id="864f2-115">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="864f2-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="864f2-116">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="864f2-116">Request syntax</span></span>

| <span data-ttu-id="864f2-117">Metod</span><span class="sxs-lookup"><span data-stu-id="864f2-117">Method</span></span>  | <span data-ttu-id="864f2-118">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="864f2-118">Request URI</span></span>                                                                                              |
|---------|----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="864f2-119">**Få**</span><span class="sxs-lookup"><span data-stu-id="864f2-119">**GET**</span></span> | <span data-ttu-id="864f2-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/analytics/licenses/usage HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="864f2-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/analytics/licenses/usage HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="864f2-121">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="864f2-121">URI parameter</span></span>

<span data-ttu-id="864f2-122">Använd följande sökvägsparameter för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="864f2-122">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="864f2-123">Namn</span><span class="sxs-lookup"><span data-stu-id="864f2-123">Name</span></span>        | <span data-ttu-id="864f2-124">Typ</span><span class="sxs-lookup"><span data-stu-id="864f2-124">Type</span></span> | <span data-ttu-id="864f2-125">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="864f2-125">Required</span></span> | <span data-ttu-id="864f2-126">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="864f2-126">Description</span></span>                                                |
|-------------|------|----------|------------------------------------------------------------|
| <span data-ttu-id="864f2-127">kund-ID</span><span class="sxs-lookup"><span data-stu-id="864f2-127">customer-id</span></span> | <span data-ttu-id="864f2-128">guid</span><span class="sxs-lookup"><span data-stu-id="864f2-128">guid</span></span> | <span data-ttu-id="864f2-129">Ja</span><span class="sxs-lookup"><span data-stu-id="864f2-129">Yes</span></span>      | <span data-ttu-id="864f2-130">Ett GUID-formaterat kund-ID som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="864f2-130">A GUID formatted customer-id that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="864f2-131">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="864f2-131">Request headers</span></span>

<span data-ttu-id="864f2-132">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="864f2-132">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="864f2-133">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="864f2-133">Request body</span></span>

<span data-ttu-id="864f2-134">Inga.</span><span class="sxs-lookup"><span data-stu-id="864f2-134">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="864f2-135">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="864f2-135">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/analytics/licenses/usage HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f657d2a8-9ed6-41b4-abfc-3cf4abebd62f
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="864f2-136">REST-svar</span><span class="sxs-lookup"><span data-stu-id="864f2-136">REST response</span></span>

<span data-ttu-id="864f2-137">Om det lyckas innehåller svarstexten en samling [CustomerLicensesUsageInsights-resurser](analytics-resources.md#customerlicensesusageinsights) som innehåller information om licensanvändning.</span><span class="sxs-lookup"><span data-stu-id="864f2-137">If successful, the response body contains a collection of [CustomerLicensesUsageInsights](analytics-resources.md#customerlicensesusageinsights) resources that provide information about licenses usage.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="864f2-138">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="864f2-138">Response success and error codes</span></span>

<span data-ttu-id="864f2-139">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="864f2-139">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="864f2-140">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="864f2-140">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="864f2-141">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="864f2-141">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="864f2-142">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="864f2-142">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1726
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
MS-RequestId: f657d2a8-9ed6-41b4-abfc-3cf4abebd62f
MS-CV: 0mufM0K1kEOoR7oI.0
MS-ServerId: 030020525
Date: Wed, 15 Mar 2017 01:19:58 GMT

{
    "totalCount": 5,
    "items": [{
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "OFFICE 365 BUSINESS ESSENTIALS",
            "licensesActive": 0,
            "licensesQualified": 1,
            "usagePercent": 0.0,
            "workloadName": "Exchange",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesUsageInsights"
            }
        }, {
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "OFFICE 365 BUSINESS ESSENTIALS",
            "licensesActive": 0,
            "licensesQualified": 1,
            "usagePercent": 0.0,
            "workloadName": "SharePoint",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesUsageInsights"
            }
        }, {
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "OFFICE 365 BUSINESS ESSENTIALS",
            "licensesActive": 0,
            "licensesQualified": 1,
            "usagePercent": 0.0,
            "workloadName": "Skype For Business",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesUsageInsights"
            }
        }, {
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "EXCHANGE ONLINE (PLAN 1)",
            "licensesActive": 0,
            "licensesQualified": 5,
            "usagePercent": 0.0,
            "workloadName": "Exchange",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesUsageInsights"
            }
        }, {
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "EXCHANGE ONLINE ARCHIVING FOR EXCHANGE ONLINE",
            "licensesActive": 0,
            "licensesQualified": 2,
            "usagePercent": 0.0,
            "workloadName": "Exchange",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesUsageInsights"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
