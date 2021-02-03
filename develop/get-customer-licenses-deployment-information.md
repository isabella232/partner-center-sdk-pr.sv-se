---
title: Hämta information om kundlicensdistribution
description: Hur du får distributions information för licenser för en specifik kund.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 3a39c6c908048305ff2dabf85a29d7ddc3628500
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769855"
---
# <a name="get-customer-licenses-deployment-information"></a><span data-ttu-id="351fe-103">Hämta information om kundlicensdistribution</span><span class="sxs-lookup"><span data-stu-id="351fe-103">Get customer licenses deployment information</span></span>

<span data-ttu-id="351fe-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="351fe-104">**Applies To**</span></span>

- <span data-ttu-id="351fe-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="351fe-105">Partner Center</span></span>

<span data-ttu-id="351fe-106">Hur du får distributions information för licenser för en specifik kund.</span><span class="sxs-lookup"><span data-stu-id="351fe-106">How to get licenses deployment insights for a specific customer.</span></span>

> [!NOTE]
> <span data-ttu-id="351fe-107">Det här scenariot har ersatts av [Hämta distributions information för licenser](get-licenses-deployment-information.md).</span><span class="sxs-lookup"><span data-stu-id="351fe-107">This scenario is superceded by [Get licenses deployment information](get-licenses-deployment-information.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="351fe-108">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="351fe-108">Prerequisites</span></span>

<span data-ttu-id="351fe-109">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="351fe-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="351fe-110">Det här scenariot stöder autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="351fe-110">This scenario supports authentication with App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="351fe-111">C\#</span><span class="sxs-lookup"><span data-stu-id="351fe-111">C\#</span></span>

<span data-ttu-id="351fe-112">Om du vill hämta sammanställda data för distribution för en angiven kund anropar du först metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="351fe-112">To retrieve aggregated data on deployment for a specified customer, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="351fe-113">Hämta sedan ett gränssnitt till åtgärder för insamling av kund nivå från [**Analytics**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.analytics) -egenskapen.</span><span class="sxs-lookup"><span data-stu-id="351fe-113">Then get an interface to customer level analytics collection operations from the [**Analytics**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.analytics) property.</span></span> <span data-ttu-id="351fe-114">Sedan hämtar du ett gränssnitt till kund nivåns licens analys samling från egenskapen [**licenser**](/dotnet/api/microsoft.store.partnercenter.analytics.icustomeranalyticscollection.licenses) .</span><span class="sxs-lookup"><span data-stu-id="351fe-114">Next, retrieve an interface to the customer level licenses analytics collection from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.icustomeranalyticscollection.licenses) property.</span></span> <span data-ttu-id="351fe-115">Slutligen kan du anropa [**Deployment. get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) -metoden för att hämta de sammanställda data distributionerna för licenser.</span><span class="sxs-lookup"><span data-stu-id="351fe-115">Finally, call the [**Deployment.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) method to get the aggregated data on licenses deployment.</span></span> <span data-ttu-id="351fe-116">Om metoden lyckas får du en samling [**CustomerLicensesDeploymentInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.customerlicensesdeploymentinsights) -objekt.</span><span class="sxs-lookup"><span data-stu-id="351fe-116">If the method succeeds you'll get a collection of [**CustomerLicensesDeploymentInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.customerlicensesdeploymentinsights) objects.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerIdToRetrieve;

var customerLicensesDeploymentAnalytics = partnerOperations.Customers.ById(customerIdToRetrieve).Analytics.Licenses.Deployment.Get();
```

## <a name="rest-request"></a><span data-ttu-id="351fe-117">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="351fe-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="351fe-118">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="351fe-118">Request syntax</span></span>

| <span data-ttu-id="351fe-119">Metod</span><span class="sxs-lookup"><span data-stu-id="351fe-119">Method</span></span>  | <span data-ttu-id="351fe-120">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="351fe-120">Request URI</span></span>                                                                                                   |
|---------|---------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="351fe-121">**TA**</span><span class="sxs-lookup"><span data-stu-id="351fe-121">**GET**</span></span> | <span data-ttu-id="351fe-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Analytics/licenses/Deployment http/1.1</span><span class="sxs-lookup"><span data-stu-id="351fe-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/analytics/licenses/deployment HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="351fe-123">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="351fe-123">URI parameter</span></span>

<span data-ttu-id="351fe-124">Använd följande Sök vägs parameter för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="351fe-124">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="351fe-125">Namn</span><span class="sxs-lookup"><span data-stu-id="351fe-125">Name</span></span>        | <span data-ttu-id="351fe-126">Typ</span><span class="sxs-lookup"><span data-stu-id="351fe-126">Type</span></span> | <span data-ttu-id="351fe-127">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="351fe-127">Required</span></span> | <span data-ttu-id="351fe-128">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="351fe-128">Description</span></span>                                                |
|-------------|------|----------|------------------------------------------------------------|
| <span data-ttu-id="351fe-129">kund-ID</span><span class="sxs-lookup"><span data-stu-id="351fe-129">customer-id</span></span> | <span data-ttu-id="351fe-130">guid</span><span class="sxs-lookup"><span data-stu-id="351fe-130">guid</span></span> | <span data-ttu-id="351fe-131">Yes</span><span class="sxs-lookup"><span data-stu-id="351fe-131">Yes</span></span>      | <span data-ttu-id="351fe-132">Ett GUID-formaterat kund-ID som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="351fe-132">A GUID formatted customer-id that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="351fe-133">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="351fe-133">Request headers</span></span>

<span data-ttu-id="351fe-134">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="351fe-134">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="351fe-135">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="351fe-135">Request body</span></span>

<span data-ttu-id="351fe-136">Inga.</span><span class="sxs-lookup"><span data-stu-id="351fe-136">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="351fe-137">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="351fe-137">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/analytics/licenses/deployment HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b01b8759-4dbe-4605-adb7-e5839a796c33
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="351fe-138">REST-svar</span><span class="sxs-lookup"><span data-stu-id="351fe-138">REST response</span></span>

<span data-ttu-id="351fe-139">Om det lyckas innehåller svars texten en samling [CustomerLicensesDeploymentInsights](analytics-resources.md#customerlicensesdeploymentinsights) -resurser som innehåller information om de licenser som har distribuerats.</span><span class="sxs-lookup"><span data-stu-id="351fe-139">If successful, the response body contains a collection of [CustomerLicensesDeploymentInsights](analytics-resources.md#customerlicensesdeploymentinsights) resources that provide information about the licenses deployed.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="351fe-140">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="351fe-140">Response success and error codes</span></span>

<span data-ttu-id="351fe-141">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="351fe-141">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="351fe-142">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="351fe-142">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="351fe-143">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="351fe-143">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="351fe-144">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="351fe-144">Response example</span></span>

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
