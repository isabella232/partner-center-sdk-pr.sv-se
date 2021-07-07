---
title: Hämta information om partnerlicensdistribution
description: Hur du hämtar information om distribution av partnerlicenser sammanställd för att inkludera alla kunder.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2464242fc6dc4e7464511eac5d4197630e22fac0
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445993"
---
# <a name="get-partner-licenses-deployment-information"></a><span data-ttu-id="3f2b3-103">Hämta information om partnerlicensdistribution</span><span class="sxs-lookup"><span data-stu-id="3f2b3-103">Get partner licenses deployment information</span></span>

<span data-ttu-id="3f2b3-104">Hur du hämtar information om distribution av partnerlicenser sammanställd för att inkludera alla kunder.</span><span class="sxs-lookup"><span data-stu-id="3f2b3-104">How to get partner licenses deployment information aggregated to include all customers.</span></span>

> [!NOTE]
> <span data-ttu-id="3f2b3-105">Det här scenariot ersätts av hämta [licensdistributionsinformation](get-licenses-deployment-information.md).</span><span class="sxs-lookup"><span data-stu-id="3f2b3-105">This scenario is superceded by [Get licenses deployment information](get-licenses-deployment-information.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3f2b3-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="3f2b3-106">Prerequisites</span></span>

<span data-ttu-id="3f2b3-107">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="3f2b3-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3f2b3-108">Det här scenariot stöder autentisering med autentiseringsuppgifter för App+Användare.</span><span class="sxs-lookup"><span data-stu-id="3f2b3-108">This scenario supports authentication with App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="3f2b3-109">C\#</span><span class="sxs-lookup"><span data-stu-id="3f2b3-109">C\#</span></span>

<span data-ttu-id="3f2b3-110">Om du vill hämta aggregerade data om licensdistributionen hämtar du först ett gränssnitt till analysinsamlingsåtgärder på partnernivå från [**egenskapen IAggregatePartner.Analytics.**](/dotnet/api/microsoft.store.partnercenter.ipartner.analytics)</span><span class="sxs-lookup"><span data-stu-id="3f2b3-110">To retrieve aggregated data on licenses deployment, first get an interface to partner level analytics collection operations from the [**IAggregatePartner.Analytics**](/dotnet/api/microsoft.store.partnercenter.ipartner.analytics) property.</span></span> <span data-ttu-id="3f2b3-111">Hämta sedan ett gränssnitt till analyssamlingen för licenser på partnernivå från [**egenskapen**](/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses) Licenser.</span><span class="sxs-lookup"><span data-stu-id="3f2b3-111">Then retrieve an interface to the partner level licenses analytics collection from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses) property.</span></span> <span data-ttu-id="3f2b3-112">Anropa slutligen metoden [**Deployment.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) för att hämta aggregerade data om licensdistributionen.</span><span class="sxs-lookup"><span data-stu-id="3f2b3-112">Finally, call the [**Deployment.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) method to get the aggregated data on licenses deployment.</span></span> <span data-ttu-id="3f2b3-113">Om metoden lyckas får du en samling [**PartnerLicensesDeploymentInsights-objekt.**](/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesdeploymentinsights)</span><span class="sxs-lookup"><span data-stu-id="3f2b3-113">If the method succeeds, you'll get a collection of [**PartnerLicensesDeploymentInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesdeploymentinsights) objects.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var partnerLicensesDeploymentAnalytics = partnerOperations.Analytics.Licenses.Deployment.Get();
```

## <a name="rest-request"></a><span data-ttu-id="3f2b3-114">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="3f2b3-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3f2b3-115">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="3f2b3-115">Request syntax</span></span>

| <span data-ttu-id="3f2b3-116">Metod</span><span class="sxs-lookup"><span data-stu-id="3f2b3-116">Method</span></span>  | <span data-ttu-id="3f2b3-117">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="3f2b3-117">Request URI</span></span>                                                                           |
|---------|---------------------------------------------------------------------------------------|
| <span data-ttu-id="3f2b3-118">**Få**</span><span class="sxs-lookup"><span data-stu-id="3f2b3-118">**GET**</span></span> | <span data-ttu-id="3f2b3-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/licenses/deployment HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="3f2b3-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/licenses/deployment HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="3f2b3-120">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="3f2b3-120">Request headers</span></span>

<span data-ttu-id="3f2b3-121">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="3f2b3-121">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3f2b3-122">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="3f2b3-122">Request body</span></span>

<span data-ttu-id="3f2b3-123">Inga.</span><span class="sxs-lookup"><span data-stu-id="3f2b3-123">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="3f2b3-124">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="3f2b3-124">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/analytics/licenses/deployment HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 25b6edd5-1f53-456b-b48c-c64f60ec2dda
MS-CorrelationId: 6492b9d6-5629-429b-934c-040b1946e760
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="3f2b3-125">REST-svar</span><span class="sxs-lookup"><span data-stu-id="3f2b3-125">REST response</span></span>

<span data-ttu-id="3f2b3-126">Om det lyckas innehåller svarstexten en samling [PartnerLicensesDeploymentInsights-resurser](analytics-resources.md#partnerlicensesdeploymentinsights) som innehåller information om de licenser som distribueras.</span><span class="sxs-lookup"><span data-stu-id="3f2b3-126">If successful, the response body contains a collection of [PartnerLicensesDeploymentInsights](analytics-resources.md#partnerlicensesdeploymentinsights) resources that provide information about the licenses deployed.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3f2b3-127">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="3f2b3-127">Response success and error codes</span></span>

<span data-ttu-id="3f2b3-128">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="3f2b3-128">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3f2b3-129">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="3f2b3-129">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3f2b3-130">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="3f2b3-130">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="3f2b3-131">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="3f2b3-131">Response example</span></span>

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
