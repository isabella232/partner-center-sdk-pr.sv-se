---
title: Hämta information om kundlicensanvändning
description: Hur du får licenser för användnings information för en specifik kund.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 1ee19e458ec65faa21034dd230b5388f7de981b2
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769708"
---
# <a name="get-customer-licenses-usage-information"></a><span data-ttu-id="42dc4-103">Hämta information om kundlicensanvändning</span><span class="sxs-lookup"><span data-stu-id="42dc4-103">Get customer licenses usage information</span></span>

<span data-ttu-id="42dc4-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="42dc4-104">**Applies To**</span></span>

- <span data-ttu-id="42dc4-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="42dc4-105">Partner Center</span></span>

<span data-ttu-id="42dc4-106">Hur du får distributions information för licenser för en specifik kund.</span><span class="sxs-lookup"><span data-stu-id="42dc4-106">How to get licenses deployment insights for a specific customer.</span></span>

> [!NOTE]
> <span data-ttu-id="42dc4-107">Det här scenariot har ersatts av [Hämta licens användnings information](get-licenses-usage-information.md).</span><span class="sxs-lookup"><span data-stu-id="42dc4-107">This scenario is superceded by [Get licenses usage information](get-licenses-usage-information.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42dc4-108">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="42dc4-108">Prerequisites</span></span>

<span data-ttu-id="42dc4-109">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="42dc4-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="42dc4-110">Det här scenariot stöder autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="42dc4-110">This scenario supports authentication with App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="42dc4-111">C\#</span><span class="sxs-lookup"><span data-stu-id="42dc4-111">C\#</span></span>

<span data-ttu-id="42dc4-112">Om du vill hämta sammanställda data för distribution för en angiven kund anropar du först metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="42dc4-112">To retrieve aggregated data on deployment for a specified customer, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="42dc4-113">Hämta sedan ett gränssnitt till åtgärder för insamling av kund nivå från [**Analytics**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.analytics) -egenskapen.</span><span class="sxs-lookup"><span data-stu-id="42dc4-113">Then get an interface to customer level analytics collection operations from the [**Analytics**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.analytics) property.</span></span> <span data-ttu-id="42dc4-114">Sedan hämtar du ett gränssnitt till kund nivåns licens analys samling från egenskapen [**licenser**](/dotnet/api/microsoft.store.partnercenter.analytics.icustomeranalyticscollection.licenses) .</span><span class="sxs-lookup"><span data-stu-id="42dc4-114">Next, retrieve an interface to the customer level licenses analytics collection from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.icustomeranalyticscollection.licenses) property.</span></span> <span data-ttu-id="42dc4-115">Slutligen anropar du metoden [**Usage. get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) för att hämta de sammanställda data licens användningen.</span><span class="sxs-lookup"><span data-stu-id="42dc4-115">Finally, call the [**Usage.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) method to get the aggregated data on licenses usage.</span></span> <span data-ttu-id="42dc4-116">Om metoden lyckas får du en samling [**CustomerLicensesUsageInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.customerlicensesusageinsights) -objekt.</span><span class="sxs-lookup"><span data-stu-id="42dc4-116">If the method succeeds you'll get a collection of [**CustomerLicensesUsageInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.customerlicensesusageinsights) objects.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerIdToRetrieve;

var customerLicensesDeploymentAnalytics = partnerOperations.Customers.ById(customerIdToRetrieve).Analytics.Licenses.Usage.Get();
```

## <a name="rest-request"></a><span data-ttu-id="42dc4-117">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="42dc4-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="42dc4-118">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="42dc4-118">Request syntax</span></span>

| <span data-ttu-id="42dc4-119">Metod</span><span class="sxs-lookup"><span data-stu-id="42dc4-119">Method</span></span>  | <span data-ttu-id="42dc4-120">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="42dc4-120">Request URI</span></span>                                                                                              |
|---------|----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="42dc4-121">**TA**</span><span class="sxs-lookup"><span data-stu-id="42dc4-121">**GET**</span></span> | <span data-ttu-id="42dc4-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Analytics/licenses/Usage http/1.1</span><span class="sxs-lookup"><span data-stu-id="42dc4-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/analytics/licenses/usage HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="42dc4-123">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="42dc4-123">URI parameter</span></span>

<span data-ttu-id="42dc4-124">Använd följande Sök vägs parameter för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="42dc4-124">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="42dc4-125">Namn</span><span class="sxs-lookup"><span data-stu-id="42dc4-125">Name</span></span>        | <span data-ttu-id="42dc4-126">Typ</span><span class="sxs-lookup"><span data-stu-id="42dc4-126">Type</span></span> | <span data-ttu-id="42dc4-127">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="42dc4-127">Required</span></span> | <span data-ttu-id="42dc4-128">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="42dc4-128">Description</span></span>                                                |
|-------------|------|----------|------------------------------------------------------------|
| <span data-ttu-id="42dc4-129">kund-ID</span><span class="sxs-lookup"><span data-stu-id="42dc4-129">customer-id</span></span> | <span data-ttu-id="42dc4-130">guid</span><span class="sxs-lookup"><span data-stu-id="42dc4-130">guid</span></span> | <span data-ttu-id="42dc4-131">Yes</span><span class="sxs-lookup"><span data-stu-id="42dc4-131">Yes</span></span>      | <span data-ttu-id="42dc4-132">Ett GUID-formaterat kund-ID som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="42dc4-132">A GUID formatted customer-id that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="42dc4-133">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="42dc4-133">Request headers</span></span>

<span data-ttu-id="42dc4-134">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="42dc4-134">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="42dc4-135">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="42dc4-135">Request body</span></span>

<span data-ttu-id="42dc4-136">Inga.</span><span class="sxs-lookup"><span data-stu-id="42dc4-136">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="42dc4-137">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="42dc4-137">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="42dc4-138">REST-svar</span><span class="sxs-lookup"><span data-stu-id="42dc4-138">REST response</span></span>

<span data-ttu-id="42dc4-139">Om det lyckas innehåller svars texten en samling [CustomerLicensesUsageInsights](analytics-resources.md#customerlicensesusageinsights) -resurser som innehåller information om licensernas användning.</span><span class="sxs-lookup"><span data-stu-id="42dc4-139">If successful, the response body contains a collection of [CustomerLicensesUsageInsights](analytics-resources.md#customerlicensesusageinsights) resources that provide information about licenses usage.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="42dc4-140">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="42dc4-140">Response success and error codes</span></span>

<span data-ttu-id="42dc4-141">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="42dc4-141">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="42dc4-142">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="42dc4-142">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="42dc4-143">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="42dc4-143">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="42dc4-144">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="42dc4-144">Response example</span></span>

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
