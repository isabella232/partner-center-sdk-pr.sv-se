---
title: Hämta information om partnerlicensdistribution
description: Hur du får distributions information för partner licenser sammanställd för att inkludera alla kunder.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 229f63d4df4f59cd0fde2bd0fc5e3f10cf6b25c0
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769837"
---
# <a name="get-partner-licenses-deployment-information"></a><span data-ttu-id="75533-103">Hämta information om partnerlicensdistribution</span><span class="sxs-lookup"><span data-stu-id="75533-103">Get partner licenses deployment information</span></span>

<span data-ttu-id="75533-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="75533-104">**Applies To**</span></span>

- <span data-ttu-id="75533-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="75533-105">Partner Center</span></span>

<span data-ttu-id="75533-106">Hur du får distributions information för partner licenser sammanställd för att inkludera alla kunder.</span><span class="sxs-lookup"><span data-stu-id="75533-106">How to get partner licenses deployment information aggregated to include all customers.</span></span>

> [!NOTE]
> <span data-ttu-id="75533-107">Det här scenariot har ersatts av [Hämta distributions information för licenser](get-licenses-deployment-information.md).</span><span class="sxs-lookup"><span data-stu-id="75533-107">This scenario is superceded by [Get licenses deployment information](get-licenses-deployment-information.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="75533-108">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="75533-108">Prerequisites</span></span>

<span data-ttu-id="75533-109">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="75533-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="75533-110">Det här scenariot stöder autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="75533-110">This scenario supports authentication with App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="75533-111">C\#</span><span class="sxs-lookup"><span data-stu-id="75533-111">C\#</span></span>

<span data-ttu-id="75533-112">Om du vill hämta sammanställda data för distribution av licenser, får du först ett gränssnitt till samlings åtgärder för analys av partner nivå från egenskapen [**IAggregatePartner. Analytics**](/dotnet/api/microsoft.store.partnercenter.ipartner.analytics) .</span><span class="sxs-lookup"><span data-stu-id="75533-112">To retrieve aggregated data on licenses deployment, first get an interface to partner level analytics collection operations from the [**IAggregatePartner.Analytics**](/dotnet/api/microsoft.store.partnercenter.ipartner.analytics) property.</span></span> <span data-ttu-id="75533-113">Hämta sedan ett gränssnitt till partner levels Analytics-samling från egenskapen [**licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses) .</span><span class="sxs-lookup"><span data-stu-id="75533-113">Then retrieve an interface to the partner level licenses analytics collection from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses) property.</span></span> <span data-ttu-id="75533-114">Slutligen kan du anropa [**Deployment. get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) -metoden för att hämta de sammanställda data distributionerna för licenser.</span><span class="sxs-lookup"><span data-stu-id="75533-114">Finally, call the [**Deployment.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) method to get the aggregated data on licenses deployment.</span></span> <span data-ttu-id="75533-115">Om metoden lyckas får du en samling [**PartnerLicensesDeploymentInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesdeploymentinsights) -objekt.</span><span class="sxs-lookup"><span data-stu-id="75533-115">If the method succeeds you'll get a collection of [**PartnerLicensesDeploymentInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesdeploymentinsights) objects.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var partnerLicensesDeploymentAnalytics = partnerOperations.Analytics.Licenses.Deployment.Get();
```

## <a name="rest-request"></a><span data-ttu-id="75533-116">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="75533-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="75533-117">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="75533-117">Request syntax</span></span>

| <span data-ttu-id="75533-118">Metod</span><span class="sxs-lookup"><span data-stu-id="75533-118">Method</span></span>  | <span data-ttu-id="75533-119">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="75533-119">Request URI</span></span>                                                                           |
|---------|---------------------------------------------------------------------------------------|
| <span data-ttu-id="75533-120">**TA**</span><span class="sxs-lookup"><span data-stu-id="75533-120">**GET**</span></span> | <span data-ttu-id="75533-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/Analytics/licenses/Deployment http/1.1</span><span class="sxs-lookup"><span data-stu-id="75533-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/licenses/deployment HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="75533-122">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="75533-122">Request headers</span></span>

<span data-ttu-id="75533-123">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="75533-123">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="75533-124">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="75533-124">Request body</span></span>

<span data-ttu-id="75533-125">Inga.</span><span class="sxs-lookup"><span data-stu-id="75533-125">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="75533-126">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="75533-126">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/analytics/licenses/deployment HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 25b6edd5-1f53-456b-b48c-c64f60ec2dda
MS-CorrelationId: 6492b9d6-5629-429b-934c-040b1946e760
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="75533-127">REST-svar</span><span class="sxs-lookup"><span data-stu-id="75533-127">REST response</span></span>

<span data-ttu-id="75533-128">Om det lyckas innehåller svars texten en samling [PartnerLicensesDeploymentInsights](analytics-resources.md#partnerlicensesdeploymentinsights) -resurser som innehåller information om de licenser som har distribuerats.</span><span class="sxs-lookup"><span data-stu-id="75533-128">If successful, the response body contains a collection of [PartnerLicensesDeploymentInsights](analytics-resources.md#partnerlicensesdeploymentinsights) resources that provide information about the licenses deployed.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="75533-129">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="75533-129">Response success and error codes</span></span>

<span data-ttu-id="75533-130">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="75533-130">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="75533-131">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="75533-131">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="75533-132">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="75533-132">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="75533-133">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="75533-133">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 487
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 6492b9d6-5629-429b-934c-040b1946e760
MS-RequestId: 25b6edd5-1f53-456b-b48c-c64f60ec2dda
MS-CV: f0trvmq8mEScHcFS.0
MS-ServerId: 102030524
Date: Tue, 14 Mar 2017 17:55:01 GMT

{
    "totalCount": 2,
    "items": [{
            "proratedDeploymentPercent": 0.0,
            "licensesSold": 343,
            "processedDateTime": "2017-03-10T00:00:00+00:00",
            "serviceName": "crm",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesDeploymentInsights"
            }
        }, {
            "proratedDeploymentPercent": 1.0,
            "licensesSold": 4464,
            "processedDateTime": "2017-03-14T03:25:16.36+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesDeploymentInsights"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
