---
title: Hämta användningsposter för alla kunder
description: Du kan använda resurssamlingen CustomerMonthlyUsageRecord för att hämta användningsposter för alla kunder som har köpt en specifik Azure-tjänst eller -resurs.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6b3fb0e1989336810f2afcc2a5bfc3a1d2849b7f
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874898"
---
# <a name="get-usage-records-for-all-customers"></a><span data-ttu-id="6f327-103">Hämta användningsposter för alla kunder</span><span class="sxs-lookup"><span data-stu-id="6f327-103">Get usage records for all customers</span></span>

<span data-ttu-id="6f327-104">**Gäller för:** Partner Center-| Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="6f327-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="6f327-105">Partner kan använda **resurssamlingen CustomerMonthlyUsageRecord** för att hämta användningsposter för alla sina kunder.</span><span class="sxs-lookup"><span data-stu-id="6f327-105">Partners can use the **CustomerMonthlyUsageRecord** resource collection to get usage records for all their customers.</span></span> <span data-ttu-id="6f327-106">Den här resursen representerar användningsposter för alla kunder.</span><span class="sxs-lookup"><span data-stu-id="6f327-106">This resource represents usage records for all customers.</span></span> <span data-ttu-id="6f327-107">Det omfattar de kunder som har en Microsoft Azure-prenumeration (MS-AZR-0145P) eller en Azure-plan.</span><span class="sxs-lookup"><span data-stu-id="6f327-107">That includes those customers with a Microsoft Azure (MS-AZR-0145P) subscription or an Azure plan.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6f327-108">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="6f327-108">Prerequisites</span></span>

- <span data-ttu-id="6f327-109">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="6f327-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6f327-110">Det här scenariot har endast stöd för autentisering med app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="6f327-110">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="6f327-111">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6f327-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="6f327-112">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="6f327-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="6f327-113">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="6f327-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="6f327-114">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="6f327-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="6f327-115">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="6f327-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="6f327-116">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6f327-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="6f327-117">C\#</span><span class="sxs-lookup"><span data-stu-id="6f327-117">C\#</span></span>

<span data-ttu-id="6f327-118">Så här hämtar du alla användningsposter för alla kunder som har köpt en specifik Azure-tjänst eller -resurs under den aktuella faktureringsperioden:</span><span class="sxs-lookup"><span data-stu-id="6f327-118">To get all the usage records for all customers who purchased a specific Azure service or resource during the current billing period:</span></span>

1. <span data-ttu-id="6f327-119">Använd din **IAggregatePartner.Customers-samling** för att anropa **metoden ById().**</span><span class="sxs-lookup"><span data-stu-id="6f327-119">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="6f327-120">Anropa **egenskapen UsageRecords** och anropa sedan **metoden Get()** eller **GetAsync().**</span><span class="sxs-lookup"><span data-stu-id="6f327-120">Call **UsageRecords** property, then call the **Get()** or **GetAsync()** method.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    var usageRecords = partnerOperations.Customers.UsageRecords.Get();
    ```

<span data-ttu-id="6f327-121">Ett exempel finns i följande exempel:</span><span class="sxs-lookup"><span data-stu-id="6f327-121">For an example, see the following sample:</span></span>

- <span data-ttu-id="6f327-122">Exempel: [Konsoltestapp](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="6f327-122">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="6f327-123">Project: **PartnerSDK.FeatureExempel**</span><span class="sxs-lookup"><span data-stu-id="6f327-123">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="6f327-124">Klass: **GetCustomerUsageRecords.cs**</span><span class="sxs-lookup"><span data-stu-id="6f327-124">Class: **GetCustomerUsageRecords.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="6f327-125">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="6f327-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6f327-126">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="6f327-126">Request syntax</span></span>

| <span data-ttu-id="6f327-127">Metod</span><span class="sxs-lookup"><span data-stu-id="6f327-127">Method</span></span>  | <span data-ttu-id="6f327-128">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="6f327-128">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="6f327-129">**Få**</span><span class="sxs-lookup"><span data-stu-id="6f327-129">**GET**</span></span> | <span data-ttu-id="6f327-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/usagerecords HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="6f327-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/usagerecords HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="6f327-131">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="6f327-131">Request headers</span></span>

<span data-ttu-id="6f327-132">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="6f327-132">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6f327-133">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="6f327-133">Request body</span></span>

<span data-ttu-id="6f327-134">Inga.</span><span class="sxs-lookup"><span data-stu-id="6f327-134">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="6f327-135">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="6f327-135">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/usagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="6f327-136">REST-svar</span><span class="sxs-lookup"><span data-stu-id="6f327-136">REST response</span></span>

<span data-ttu-id="6f327-137">Om det lyckas returnerar den här **metoden en CustomerMonthlyUsageRecord-resurs** i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="6f327-137">If successful, this method returns a **CustomerMonthlyUsageRecord** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6f327-138">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="6f327-138">Response success and error codes</span></span>

<span data-ttu-id="6f327-139">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="6f327-139">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6f327-140">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="6f327-140">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="6f327-141">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="6f327-141">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="6f327-142">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="6f327-142">Response example</span></span>

<span data-ttu-id="6f327-143">Du kan använda egenskapen **isUpgraded för** att identifiera kunder som har en Azure-plan.</span><span class="sxs-lookup"><span data-stu-id="6f327-143">You can use the **isUpgraded** property to identify customers who have an Azure plan.</span></span> <span data-ttu-id="6f327-144">Om värdet för **isUpgraded är** **sant innebär** det att kunderna har Azure-planer.</span><span class="sxs-lookup"><span data-stu-id="6f327-144">If the value for **isUpgraded** is **true**, it means the customers have Azure plans.</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "totalCount": 25,
    "items": [
        {
            "budget": {
                "attributes": {
                    "objectType": "SpendingBudget"
                }
            },
            "customerSpendingBudget": {
                "attributes": {
                    "objectType": "SpendingBudget"
                }
            },
            "percentUsed": 0,
            "isUpgraded": false,
            "resourceId": "11111111-1843-4b3b-872f-206e08a08e51",
            "id": "11111111-1843-4b3b-872f-206e08a08e51",
            "resourceName": "LEGACY AZURE CUSTOMER SE",
            "name": "LEGACY AZURE CUSTOMER SE",
            "totalCost": 0,
            "currencyLocale": "fr-FR",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-08-01T23:00:16.57+00:00",
            "attributes": {
                "objectType": "CustomerMonthlyUsageRecord"
            }
        },
        {
            "budget": {
                "amount": 20,
                "attributes": {
                    "objectType": "SpendingBudget"
                }
            },
            "percentUsed": 602.84,
            "isUpgraded": true,
            "resourceId": "11111111-6fb9-4b05-8f15-b3d72e0596e6",
            "id": "11111111-6fb9-4b05-8f15-b3d72e0596e6",
            "resourceName": "Modern Azure Customer SE",
            "name": "Modern Azure Customer SE",
            "totalCost": 120.5682999999995904716,
            "currencyCode": "SEK",
            "usdTotalCost": 12.39999999999999985235,
            "lastModifiedDate": "2019-09-17T17:08:11.1433333+00:00",
            "attributes": {
                "objectType": "CustomerMonthlyUsageRecord"
            }
        },
        {
            "budget": {
                "attributes": {
                    "objectType": "SpendingBudget"
                }
            },
            "percentUsed": 0,
            "isUpgraded": true,
            "resourceId": "11111111-5892-4326-8541-9da1fdb233fb",
            "id": "11111111-5892-4326-8541-9da1fdb233fb",
            "resourceName": "Test_Test_MA20190829_14",
            "name": "Test_Test_MA20190829_14",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T17:08:11.1433333+00:00",
            "attributes": {
                "objectType": "CustomerMonthlyUsageRecord"
            }
        },
           {
            "budget": {
                "amount": 97,
                "attributes": {
                    "objectType": "SpendingBudget"
                }
            },
            "percentUsed": 28.08,
            "isUpgraded": true,
            "resourceId": "11111111-641b-4c53-b7fc-0f2bfca8a581",
            "id": "11111111-641b-4c53-b7fc-0f2bfca8a581",
            "resourceName": "Modern Azure Customer UK",
            "name": "Modern Azure Customer UK",
            "totalCost": 27.23292827625710931604,
            "currencyCode": "GBP",
            "usdTotalCost": 33.280000000000001044,
            "lastModifiedDate": "2019-09-17T17:08:11.1433333+00:00",
            "attributes": {
                "objectType": "CustomerMonthlyUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/usagerecords",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
