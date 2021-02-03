---
title: Hämta användnings poster för alla kunder
description: Du kan använda CustomerMonthlyUsageRecord-resurs samlingen för att hämta användnings poster för alla kunder som har köpt en enskild Azure-tjänst eller resurs.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: da829a6de3690a9b1117ce9dfa58fbe381cafd81
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769159"
---
# <a name="get-usage-records-for-all-customers"></a><span data-ttu-id="00a9d-103">Hämta användnings poster för alla kunder</span><span class="sxs-lookup"><span data-stu-id="00a9d-103">Get usage records for all customers</span></span>

<span data-ttu-id="00a9d-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="00a9d-104">**Applies to:**</span></span>

- <span data-ttu-id="00a9d-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="00a9d-105">Partner Center</span></span>
- <span data-ttu-id="00a9d-106">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="00a9d-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="00a9d-107">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="00a9d-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="00a9d-108">Partner kan använda **CustomerMonthlyUsageRecord** -resurs samlingen för att hämta användnings poster för alla sina kunder.</span><span class="sxs-lookup"><span data-stu-id="00a9d-108">Partners can use the **CustomerMonthlyUsageRecord** resource collection to get usage records for all their customers.</span></span> <span data-ttu-id="00a9d-109">Den här resursen representerar användnings poster för alla kunder.</span><span class="sxs-lookup"><span data-stu-id="00a9d-109">This resource represents usage records for all customers.</span></span> <span data-ttu-id="00a9d-110">Detta omfattar de kunderna med en Microsoft Azure-prenumeration (MS-AZR-0145P) eller en Azure-plan.</span><span class="sxs-lookup"><span data-stu-id="00a9d-110">That includes those customers with a Microsoft Azure (MS-AZR-0145P) subscription or an Azure plan.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="00a9d-111">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="00a9d-111">Prerequisites</span></span>

- <span data-ttu-id="00a9d-112">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="00a9d-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="00a9d-113">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="00a9d-113">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="00a9d-114">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="00a9d-114">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="00a9d-115">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="00a9d-115">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="00a9d-116">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="00a9d-116">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="00a9d-117">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="00a9d-117">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="00a9d-118">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="00a9d-118">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="00a9d-119">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="00a9d-119">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="00a9d-120">C\#</span><span class="sxs-lookup"><span data-stu-id="00a9d-120">C\#</span></span>

<span data-ttu-id="00a9d-121">För att hämta alla användnings poster för alla kunder som har köpt en viss Azure-tjänst eller resurs under den aktuella fakturerings perioden:</span><span class="sxs-lookup"><span data-stu-id="00a9d-121">To get all the usage records for all customers who purchased a specific Azure service or resource during the current billing period:</span></span>

1. <span data-ttu-id="00a9d-122">Använd din **IAggregatePartner. Customers** -samling för att anropa metoden **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="00a9d-122">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="00a9d-123">Anropa **UsageRecords** -egenskapen och anropa sedan metoden **Get ()** eller **GetAsync ()** .</span><span class="sxs-lookup"><span data-stu-id="00a9d-123">Call **UsageRecords** property, then call the **Get()** or **GetAsync()** method.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    var usageRecords = partnerOperations.Customers.UsageRecords.Get();
    ```

<span data-ttu-id="00a9d-124">Ett exempel finns i följande exempel:</span><span class="sxs-lookup"><span data-stu-id="00a9d-124">For an example, see the following sample:</span></span>

- <span data-ttu-id="00a9d-125">Exempel: [konsol test app](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="00a9d-125">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="00a9d-126">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="00a9d-126">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="00a9d-127">Klass: **GetCustomerUsageRecords.cs**</span><span class="sxs-lookup"><span data-stu-id="00a9d-127">Class: **GetCustomerUsageRecords.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="00a9d-128">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="00a9d-128">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="00a9d-129">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="00a9d-129">Request syntax</span></span>

| <span data-ttu-id="00a9d-130">Metod</span><span class="sxs-lookup"><span data-stu-id="00a9d-130">Method</span></span>  | <span data-ttu-id="00a9d-131">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="00a9d-131">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="00a9d-132">**TA**</span><span class="sxs-lookup"><span data-stu-id="00a9d-132">**GET**</span></span> | <span data-ttu-id="00a9d-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/usagerecords http/1.1</span><span class="sxs-lookup"><span data-stu-id="00a9d-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/usagerecords HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="00a9d-134">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="00a9d-134">Request headers</span></span>

<span data-ttu-id="00a9d-135">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="00a9d-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="00a9d-136">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="00a9d-136">Request body</span></span>

<span data-ttu-id="00a9d-137">Inga.</span><span class="sxs-lookup"><span data-stu-id="00a9d-137">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="00a9d-138">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="00a9d-138">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/usagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="00a9d-139">REST-svar</span><span class="sxs-lookup"><span data-stu-id="00a9d-139">REST response</span></span>

<span data-ttu-id="00a9d-140">Om det lyckas returnerar den här metoden en **CustomerMonthlyUsageRecord** -resurs i svars texten.</span><span class="sxs-lookup"><span data-stu-id="00a9d-140">If successful, this method returns a **CustomerMonthlyUsageRecord** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="00a9d-141">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="00a9d-141">Response success and error codes</span></span>

<span data-ttu-id="00a9d-142">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="00a9d-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="00a9d-143">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="00a9d-143">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="00a9d-144">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="00a9d-144">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="00a9d-145">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="00a9d-145">Response example</span></span>

<span data-ttu-id="00a9d-146">Du kan använda egenskapen **isUpgraded** för att identifiera kunder som har en Azure-plan.</span><span class="sxs-lookup"><span data-stu-id="00a9d-146">You can use the **isUpgraded** property to identify customers who have an Azure plan.</span></span> <span data-ttu-id="00a9d-147">Om värdet för **isUpgraded** är **Sant** innebär det att kunderna har Azure-planer.</span><span class="sxs-lookup"><span data-stu-id="00a9d-147">If the value for **isUpgraded** is **true**, it means the customers have Azure plans.</span></span>

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
