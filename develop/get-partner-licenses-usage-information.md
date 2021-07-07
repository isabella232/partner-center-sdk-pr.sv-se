---
title: Hämta information om partnerlicensanvändning
description: Hur du hämtar användningsinformation för partnerlicenser sammanställd för att inkludera alla kunder.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f3d05d61ac4f2c90b0d8a4bfd93fe24e94bd5c1b
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445603"
---
# <a name="get-partner-licenses-usage-information"></a><span data-ttu-id="69327-103">Hämta information om partnerlicensanvändning</span><span class="sxs-lookup"><span data-stu-id="69327-103">Get partner licenses usage information</span></span>

<span data-ttu-id="69327-104">Hur du hämtar användningsinformation för partnerlicenser sammanställd för att inkludera alla kunder.</span><span class="sxs-lookup"><span data-stu-id="69327-104">How to get partner licenses usage information aggregated to include all customers.</span></span>

> [!NOTE]
> <span data-ttu-id="69327-105">Det här scenariot ersätts av [Hämta användningsinformation om licenser.](get-licenses-usage-information.md)</span><span class="sxs-lookup"><span data-stu-id="69327-105">This scenario is superceded by [Get licenses usage information](get-licenses-usage-information.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="69327-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="69327-106">Prerequisites</span></span>

<span data-ttu-id="69327-107">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="69327-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="69327-108">Det här scenariot stöder autentisering med autentiseringsuppgifter för App+Användare.</span><span class="sxs-lookup"><span data-stu-id="69327-108">This scenario supports authentication with App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="69327-109">C\#</span><span class="sxs-lookup"><span data-stu-id="69327-109">C\#</span></span>

<span data-ttu-id="69327-110">Om du vill hämta aggregerade data om licensdistributionen hämtar du först ett gränssnitt till analysinsamlingsåtgärder på partnernivå från [**egenskapen IAggregatePartner.Analytics.**](/dotnet/api/microsoft.store.partnercenter.ipartner.analytics)</span><span class="sxs-lookup"><span data-stu-id="69327-110">To retrieve aggregated data on licenses deployment, first get an interface to partner level analytics collection operations from the [**IAggregatePartner.Analytics**](/dotnet/api/microsoft.store.partnercenter.ipartner.analytics) property.</span></span> <span data-ttu-id="69327-111">Hämta sedan ett gränssnitt till analyssamlingen för licenser på partnernivå från [**egenskapen**](/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses) Licenser.</span><span class="sxs-lookup"><span data-stu-id="69327-111">Then retrieve an interface to the partner level licenses analytics collection from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses) property.</span></span> <span data-ttu-id="69327-112">Anropa slutligen metoden [**Usage.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) för att hämta aggregerade data om licensanvändningen.</span><span class="sxs-lookup"><span data-stu-id="69327-112">Finally, call the [**Usage.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) method to get the aggregated data on licenses usage.</span></span> <span data-ttu-id="69327-113">Om metoden lyckas får du en samling med [**PartnerLicensesUsageInsights-objekt.**](/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesusageinsights)</span><span class="sxs-lookup"><span data-stu-id="69327-113">If the method succeeds, you'll get a collection of [**PartnerLicensesUsageInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesusageinsights) objects.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var partnerLicensesUsageAnalytics = partnerOperations.Analytics.Licenses.Usage.Get();
```

## <a name="rest-request"></a><span data-ttu-id="69327-114">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="69327-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="69327-115">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="69327-115">Request syntax</span></span>

| <span data-ttu-id="69327-116">Metod</span><span class="sxs-lookup"><span data-stu-id="69327-116">Method</span></span>  | <span data-ttu-id="69327-117">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="69327-117">Request URI</span></span>                                                                      |
|---------|----------------------------------------------------------------------------------|
| <span data-ttu-id="69327-118">**Få**</span><span class="sxs-lookup"><span data-stu-id="69327-118">**GET**</span></span> | <span data-ttu-id="69327-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/licenses/usage HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="69327-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/licenses/usage HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="69327-120">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="69327-120">Request headers</span></span>

<span data-ttu-id="69327-121">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="69327-121">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="69327-122">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="69327-122">Request body</span></span>

<span data-ttu-id="69327-123">Inga.</span><span class="sxs-lookup"><span data-stu-id="69327-123">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="69327-124">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="69327-124">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/analytics/licenses/usage HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 6b588e9b-1d02-471a-bce2-79374497c24e
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="69327-125">REST-svar</span><span class="sxs-lookup"><span data-stu-id="69327-125">REST response</span></span>

<span data-ttu-id="69327-126">Om det lyckas innehåller svarstexten en samling [partnerlicenserUsageInsights-resurser](analytics-resources.md#partnerlicensesusageinsights) som innehåller information om de licenser som används.</span><span class="sxs-lookup"><span data-stu-id="69327-126">If successful, the response body contains a collection of [PartnerLicensesUsageInsights](analytics-resources.md#partnerlicensesusageinsights) resources that provide information about the licenses used.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="69327-127">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="69327-127">Response success and error codes</span></span>

<span data-ttu-id="69327-128">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="69327-128">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="69327-129">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="69327-129">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="69327-130">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="69327-130">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="69327-131">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="69327-131">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1156
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
MS-RequestId: 6b588e9b-1d02-471a-bce2-79374497c24e
MS-CV: wk0/vjugzEe0Z9cv.0
MS-ServerId: 101112012
Date: Wed, 15 Mar 2017 01:18:26 GMT

{
    "totalCount": 5,
    "items": [{
            "proratedLicensesUsagePercent": 0.0,
            "workloadName": "Microsoft Dynamics CRM",
            "processedDateTime": "2017-03-10T00:00:00+00:00",
            "serviceName": "crm",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesUsageInsights"
            }
        }, {
            "proratedLicensesUsagePercent": 0.0,
            "workloadName": "SharePoint",
            "processedDateTime": "2017-03-10T00:00:00+00:00",
            "serviceName": "crm",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesUsageInsights"
            }
        }, {
            "proratedLicensesUsagePercent": 0.0,
            "workloadName": "Exchange",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesUsageInsights"
            }
        }, {
            "proratedLicensesUsagePercent": 0.0,
            "workloadName": "SharePoint",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesUsageInsights"
            }
        }, {
            "proratedLicensesUsagePercent": 0.0,
            "workloadName": "Skype For Business",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesUsageInsights"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
