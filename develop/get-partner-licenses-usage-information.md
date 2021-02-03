---
title: Hämta information om partnerlicensanvändning
description: Så här hämtar du partner licenser användnings information sammanställd för att inkludera alla kunder.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 93d003fb269a3421b8efd8cebe8f396f97599a10
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769903"
---
# <a name="get-partner-licenses-usage-information"></a><span data-ttu-id="20f63-103">Hämta information om partnerlicensanvändning</span><span class="sxs-lookup"><span data-stu-id="20f63-103">Get partner licenses usage information</span></span>

<span data-ttu-id="20f63-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="20f63-104">**Applies To**</span></span>

- <span data-ttu-id="20f63-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="20f63-105">Partner Center</span></span>

<span data-ttu-id="20f63-106">Så här hämtar du partner licenser användnings information sammanställd för att inkludera alla kunder.</span><span class="sxs-lookup"><span data-stu-id="20f63-106">How to get partner licenses usage information aggregated to include all customers.</span></span>

> [!NOTE]
> <span data-ttu-id="20f63-107">Det här scenariot har ersatts av [Hämta licens användnings information](get-licenses-usage-information.md).</span><span class="sxs-lookup"><span data-stu-id="20f63-107">This scenario is superceded by [Get licenses usage information](get-licenses-usage-information.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="20f63-108">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="20f63-108">Prerequisites</span></span>

<span data-ttu-id="20f63-109">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="20f63-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="20f63-110">Det här scenariot stöder autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="20f63-110">This scenario supports authentication with App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="20f63-111">C\#</span><span class="sxs-lookup"><span data-stu-id="20f63-111">C\#</span></span>

<span data-ttu-id="20f63-112">Om du vill hämta sammanställda data för distribution av licenser, får du först ett gränssnitt till samlings åtgärder för analys av partner nivå från egenskapen [**IAggregatePartner. Analytics**](/dotnet/api/microsoft.store.partnercenter.ipartner.analytics) .</span><span class="sxs-lookup"><span data-stu-id="20f63-112">To retrieve aggregated data on licenses deployment, first get an interface to partner level analytics collection operations from the [**IAggregatePartner.Analytics**](/dotnet/api/microsoft.store.partnercenter.ipartner.analytics) property.</span></span> <span data-ttu-id="20f63-113">Hämta sedan ett gränssnitt till partner levels Analytics-samling från egenskapen [**licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses) .</span><span class="sxs-lookup"><span data-stu-id="20f63-113">Then retrieve an interface to the partner level licenses analytics collection from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses) property.</span></span> <span data-ttu-id="20f63-114">Slutligen anropar du metoden [**Usage. get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) för att hämta de sammanställda data licens användningen.</span><span class="sxs-lookup"><span data-stu-id="20f63-114">Finally, call the [**Usage.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) method to get the aggregated data on licenses usage.</span></span> <span data-ttu-id="20f63-115">Om metoden lyckas får du en samling [**PartnerLicensesUsageInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesusageinsights) -objekt.</span><span class="sxs-lookup"><span data-stu-id="20f63-115">If the method succeeds you'll get a collection of [**PartnerLicensesUsageInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesusageinsights) objects.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var partnerLicensesUsageAnalytics = partnerOperations.Analytics.Licenses.Usage.Get();
```

## <a name="rest-request"></a><span data-ttu-id="20f63-116">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="20f63-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="20f63-117">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="20f63-117">Request syntax</span></span>

| <span data-ttu-id="20f63-118">Metod</span><span class="sxs-lookup"><span data-stu-id="20f63-118">Method</span></span>  | <span data-ttu-id="20f63-119">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="20f63-119">Request URI</span></span>                                                                      |
|---------|----------------------------------------------------------------------------------|
| <span data-ttu-id="20f63-120">**TA**</span><span class="sxs-lookup"><span data-stu-id="20f63-120">**GET**</span></span> | <span data-ttu-id="20f63-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/Analytics/licenses/Usage http/1.1</span><span class="sxs-lookup"><span data-stu-id="20f63-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/licenses/usage HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="20f63-122">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="20f63-122">Request headers</span></span>

<span data-ttu-id="20f63-123">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="20f63-123">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="20f63-124">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="20f63-124">Request body</span></span>

<span data-ttu-id="20f63-125">Inga.</span><span class="sxs-lookup"><span data-stu-id="20f63-125">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="20f63-126">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="20f63-126">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/analytics/licenses/usage HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 6b588e9b-1d02-471a-bce2-79374497c24e
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="20f63-127">REST-svar</span><span class="sxs-lookup"><span data-stu-id="20f63-127">REST response</span></span>

<span data-ttu-id="20f63-128">Om det lyckas innehåller svars texten en samling [PartnerLicensesUsageInsights](analytics-resources.md#partnerlicensesusageinsights) -resurser som innehåller information om de licenser som används.</span><span class="sxs-lookup"><span data-stu-id="20f63-128">If successful, the response body contains a collection of [PartnerLicensesUsageInsights](analytics-resources.md#partnerlicensesusageinsights) resources that provide information about the licenses used.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="20f63-129">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="20f63-129">Response success and error codes</span></span>

<span data-ttu-id="20f63-130">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="20f63-130">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="20f63-131">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="20f63-131">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="20f63-132">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="20f63-132">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="20f63-133">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="20f63-133">Response example</span></span>

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
