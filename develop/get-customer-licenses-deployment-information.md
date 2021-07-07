---
title: Hämta information om kundlicensdistribution
description: Så här hämtar du information om licensdistribution för en specifik kund.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 91fe9da185aa59025d4dc8263257b207edb4a5be
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446470"
---
# <a name="get-customer-licenses-deployment-information"></a><span data-ttu-id="ff4ef-103">Hämta information om kundlicensdistribution</span><span class="sxs-lookup"><span data-stu-id="ff4ef-103">Get customer licenses deployment information</span></span>

<span data-ttu-id="ff4ef-104">Så här hämtar du information om licensdistribution för en specifik kund.</span><span class="sxs-lookup"><span data-stu-id="ff4ef-104">How to get licenses deployment insights for a specific customer.</span></span>

> [!NOTE]
> <span data-ttu-id="ff4ef-105">Det här scenariot ersätts av hämta [licensdistributionsinformation](get-licenses-deployment-information.md).</span><span class="sxs-lookup"><span data-stu-id="ff4ef-105">This scenario is superceded by [Get licenses deployment information](get-licenses-deployment-information.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff4ef-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="ff4ef-106">Prerequisites</span></span>

<span data-ttu-id="ff4ef-107">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="ff4ef-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ff4ef-108">Det här scenariot stöder autentisering med autentiseringsuppgifter för App+Användare.</span><span class="sxs-lookup"><span data-stu-id="ff4ef-108">This scenario supports authentication with App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="ff4ef-109">C\#</span><span class="sxs-lookup"><span data-stu-id="ff4ef-109">C\#</span></span>

<span data-ttu-id="ff4ef-110">Om du vill hämta aggregerade data vid distributionen för en angiven kund anropar du först [**metoden IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="ff4ef-110">To retrieve aggregated data on deployment for a specified customer, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="ff4ef-111">Hämta sedan ett gränssnitt för insamlingsåtgärder på kundnivå från [**egenskapen**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.analytics) Analytics.</span><span class="sxs-lookup"><span data-stu-id="ff4ef-111">Then get an interface to customer level analytics collection operations from the [**Analytics**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.analytics) property.</span></span> <span data-ttu-id="ff4ef-112">Hämta sedan ett gränssnitt till analyssamlingen för licenser på kundnivå [**från**](/dotnet/api/microsoft.store.partnercenter.analytics.icustomeranalyticscollection.licenses) egenskapen Licenser.</span><span class="sxs-lookup"><span data-stu-id="ff4ef-112">Next, retrieve an interface to the customer level licenses analytics collection from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.icustomeranalyticscollection.licenses) property.</span></span> <span data-ttu-id="ff4ef-113">Anropa slutligen metoden [**Deployment.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) för att hämta aggregerade data om licensdistributionen.</span><span class="sxs-lookup"><span data-stu-id="ff4ef-113">Finally, call the [**Deployment.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) method to get the aggregated data on licenses deployment.</span></span> <span data-ttu-id="ff4ef-114">Om metoden lyckas får du en samling [**CustomerLicensesDeploymentInsights-objekt.**](/dotnet/api/microsoft.store.partnercenter.models.analytics.customerlicensesdeploymentinsights)</span><span class="sxs-lookup"><span data-stu-id="ff4ef-114">If the method succeeds, you'll get a collection of [**CustomerLicensesDeploymentInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.customerlicensesdeploymentinsights) objects.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerIdToRetrieve;

var customerLicensesDeploymentAnalytics = partnerOperations.Customers.ById(customerIdToRetrieve).Analytics.Licenses.Deployment.Get();
```

## <a name="rest-request"></a><span data-ttu-id="ff4ef-115">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="ff4ef-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ff4ef-116">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="ff4ef-116">Request syntax</span></span>

| <span data-ttu-id="ff4ef-117">Metod</span><span class="sxs-lookup"><span data-stu-id="ff4ef-117">Method</span></span>  | <span data-ttu-id="ff4ef-118">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="ff4ef-118">Request URI</span></span>                                                                                                   |
|---------|---------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ff4ef-119">**Få**</span><span class="sxs-lookup"><span data-stu-id="ff4ef-119">**GET**</span></span> | <span data-ttu-id="ff4ef-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/analytics/licenses/deployment HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="ff4ef-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/analytics/licenses/deployment HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="ff4ef-121">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="ff4ef-121">URI parameter</span></span>

<span data-ttu-id="ff4ef-122">Använd följande sökvägsparameter för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="ff4ef-122">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="ff4ef-123">Namn</span><span class="sxs-lookup"><span data-stu-id="ff4ef-123">Name</span></span>        | <span data-ttu-id="ff4ef-124">Typ</span><span class="sxs-lookup"><span data-stu-id="ff4ef-124">Type</span></span> | <span data-ttu-id="ff4ef-125">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="ff4ef-125">Required</span></span> | <span data-ttu-id="ff4ef-126">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="ff4ef-126">Description</span></span>                                                |
|-------------|------|----------|------------------------------------------------------------|
| <span data-ttu-id="ff4ef-127">kund-ID</span><span class="sxs-lookup"><span data-stu-id="ff4ef-127">customer-id</span></span> | <span data-ttu-id="ff4ef-128">guid</span><span class="sxs-lookup"><span data-stu-id="ff4ef-128">guid</span></span> | <span data-ttu-id="ff4ef-129">Ja</span><span class="sxs-lookup"><span data-stu-id="ff4ef-129">Yes</span></span>      | <span data-ttu-id="ff4ef-130">Ett GUID-formaterat kund-ID som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="ff4ef-130">A GUID formatted customer-id that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="ff4ef-131">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="ff4ef-131">Request headers</span></span>

<span data-ttu-id="ff4ef-132">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="ff4ef-132">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ff4ef-133">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="ff4ef-133">Request body</span></span>

<span data-ttu-id="ff4ef-134">Inga.</span><span class="sxs-lookup"><span data-stu-id="ff4ef-134">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="ff4ef-135">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="ff4ef-135">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/analytics/licenses/deployment HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b01b8759-4dbe-4605-adb7-e5839a796c33
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="ff4ef-136">REST-svar</span><span class="sxs-lookup"><span data-stu-id="ff4ef-136">REST response</span></span>

<span data-ttu-id="ff4ef-137">Om det lyckas innehåller svarstexten en samling [CustomerLicensesDeploymentInsights-resurser](analytics-resources.md#customerlicensesdeploymentinsights) som innehåller information om de licenser som distribueras.</span><span class="sxs-lookup"><span data-stu-id="ff4ef-137">If successful, the response body contains a collection of [CustomerLicensesDeploymentInsights](analytics-resources.md#customerlicensesdeploymentinsights) resources that provide information about the licenses deployed.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ff4ef-138">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="ff4ef-138">Response success and error codes</span></span>

<span data-ttu-id="ff4ef-139">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="ff4ef-139">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ff4ef-140">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="ff4ef-140">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ff4ef-141">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="ff4ef-141">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ff4ef-142">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="ff4ef-142">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1012
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
MS-RequestId: b01b8759-4dbe-4605-adb7-e5839a796c33
MS-CV: deEp2Wy6DUitMCYA.0
MS-ServerId: 102030524
Date: Wed, 15 Mar 2017 01:19:18 GMT

{
    "totalCount": 3,
    "items": [{
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "OFFICE 365 BUSINESS ESSENTIALS",
            "licensesDeployed": 0,
            "deploymentPercent": 0.0,
            "licensesSold": 1,
            "processedDateTime": "2017-03-14T03:25:16.36+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesDeploymentInsights"
            }
        }, {
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "EXCHANGE ONLINE (PLAN 1)",
            "licensesDeployed": 0,
            "deploymentPercent": 0.0,
            "licensesSold": 5,
            "processedDateTime": "2017-03-14T03:25:16.36+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesDeploymentInsights"
            }
        }, {
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "EXCHANGE ONLINE ARCHIVING FOR EXCHANGE ONLINE",
            "licensesDeployed": 0,
            "deploymentPercent": 0.0,
            "licensesSold": 2,
            "processedDateTime": "2017-03-14T03:25:16.36+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesDeploymentInsights"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
