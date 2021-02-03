---
title: Hämta radobjekt för en kunds servicekostnader
description: Hämtar en kunds service kostnads rads objekt för den angivna fakturerings perioden.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c2034eaf11342493797688b44b634b8e9598e2e4
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769366"
---
# <a name="get-a-customers-service-costs-line-items"></a><span data-ttu-id="2bb9e-103">Hämta radobjekt för en kunds servicekostnader</span><span class="sxs-lookup"><span data-stu-id="2bb9e-103">Get a customer's service costs line items</span></span>

<span data-ttu-id="2bb9e-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="2bb9e-104">**Applies to:**</span></span>

- <span data-ttu-id="2bb9e-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="2bb9e-105">Partner Center</span></span>

<span data-ttu-id="2bb9e-106">Hämtar en kunds service kostnads rads objekt för den angivna fakturerings perioden.</span><span class="sxs-lookup"><span data-stu-id="2bb9e-106">Gets a customer's service cost line items for the specified billing period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2bb9e-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="2bb9e-107">Prerequisites</span></span>

- <span data-ttu-id="2bb9e-108">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="2bb9e-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2bb9e-109">Det här scenariot stöder autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="2bb9e-109">This scenario supports authentication with App+User credentials.</span></span>

- <span data-ttu-id="2bb9e-110">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2bb9e-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="2bb9e-111">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="2bb9e-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="2bb9e-112">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="2bb9e-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="2bb9e-113">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="2bb9e-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="2bb9e-114">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="2bb9e-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="2bb9e-115">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2bb9e-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="2bb9e-116">En fakturerings periods indikator ( **`mostrecent`** ).</span><span class="sxs-lookup"><span data-stu-id="2bb9e-116">A billing period indicator (**`mostrecent`**).</span></span>

## <a name="c"></a><span data-ttu-id="2bb9e-117">C\#</span><span class="sxs-lookup"><span data-stu-id="2bb9e-117">C\#</span></span>

<span data-ttu-id="2bb9e-118">Så här hämtar du en service kostnads Sammanfattning för den angivna kunden:</span><span class="sxs-lookup"><span data-stu-id="2bb9e-118">To retrieve a service costs summary for the specified customer:</span></span>

1. <span data-ttu-id="2bb9e-119">Anropa metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="2bb9e-119">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="2bb9e-120">Använd egenskapen [**ServiceCosts**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicecosts) för att hämta ett gränssnitt till kund tjänst kostnader för insamlings åtgärder.</span><span class="sxs-lookup"><span data-stu-id="2bb9e-120">Use the [**ServiceCosts**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicecosts) property to get an interface to customer service costs collection operations.</span></span>

3. <span data-ttu-id="2bb9e-121">Anropa metoden [**ByBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.icustomerservicecostscollection.bybillingperiod) med en medlem i [**ServiceCostsBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.models.servicecosts.servicecostsbillingperiod) -uppräkningen för att returnera en [**IServiceCostsCollection**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostscollection).</span><span class="sxs-lookup"><span data-stu-id="2bb9e-121">Call the [**ByBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.icustomerservicecostscollection.bybillingperiod) method with a member of the [**ServiceCostsBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.models.servicecosts.servicecostsbillingperiod) enumeration to return an [**IServiceCostsCollection**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostscollection).</span></span>

4. <span data-ttu-id="2bb9e-122">Använd metoden [**IServiceCostsCollection. rad objekt. get**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostlineitemscollection.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostlineitemscollection.getasync) för att hämta kundens service kostnads rads objekt.</span><span class="sxs-lookup"><span data-stu-id="2bb9e-122">Use the [**IServiceCostsCollection.LineItems.Get**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostlineitemscollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostlineitemscollection.getasync) method to get the customer's service costs line items.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var serviceCostsSummary = partnerOperations.Customers.ById(selectedCustomerId).ServiceCosts.ByBillingPeriod(ServiceCostsBillingPeriod.MostRecent).LineItems.Get();
```

## <a name="rest-request"></a><span data-ttu-id="2bb9e-123">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="2bb9e-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2bb9e-124">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="2bb9e-124">Request syntax</span></span>

| <span data-ttu-id="2bb9e-125">Metod</span><span class="sxs-lookup"><span data-stu-id="2bb9e-125">Method</span></span>  | <span data-ttu-id="2bb9e-126">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="2bb9e-126">Request URI</span></span>                                                                                                             |
|---------|-------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2bb9e-127">**TA**</span><span class="sxs-lookup"><span data-stu-id="2bb9e-127">**GET**</span></span> | <span data-ttu-id="2bb9e-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/servicecosts/{Billing-period}/lineitems http/1.1</span><span class="sxs-lookup"><span data-stu-id="2bb9e-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/servicecosts/{billing-period}/lineitems HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="2bb9e-129">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="2bb9e-129">URI parameters</span></span>

<span data-ttu-id="2bb9e-130">Använd följande Sök vägs parametrar för att identifiera kunden och fakturerings perioden.</span><span class="sxs-lookup"><span data-stu-id="2bb9e-130">Use the following path parameters to identify the customer and the billing period.</span></span>

| <span data-ttu-id="2bb9e-131">Namn</span><span class="sxs-lookup"><span data-stu-id="2bb9e-131">Name</span></span>           | <span data-ttu-id="2bb9e-132">Typ</span><span class="sxs-lookup"><span data-stu-id="2bb9e-132">Type</span></span>   | <span data-ttu-id="2bb9e-133">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="2bb9e-133">Required</span></span> | <span data-ttu-id="2bb9e-134">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="2bb9e-134">Description</span></span>                                                                                                                      |
|----------------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2bb9e-135">kund-ID</span><span class="sxs-lookup"><span data-stu-id="2bb9e-135">customer-id</span></span>    | <span data-ttu-id="2bb9e-136">guid</span><span class="sxs-lookup"><span data-stu-id="2bb9e-136">guid</span></span>   | <span data-ttu-id="2bb9e-137">Yes</span><span class="sxs-lookup"><span data-stu-id="2bb9e-137">Yes</span></span>      | <span data-ttu-id="2bb9e-138">Ett GUID-formaterat kund-ID som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="2bb9e-138">A GUID formatted customer ID that identifies the customer.</span></span>                                                                       |
| <span data-ttu-id="2bb9e-139">fakturerings period</span><span class="sxs-lookup"><span data-stu-id="2bb9e-139">billing-period</span></span> | <span data-ttu-id="2bb9e-140">sträng</span><span class="sxs-lookup"><span data-stu-id="2bb9e-140">string</span></span> | <span data-ttu-id="2bb9e-141">Yes</span><span class="sxs-lookup"><span data-stu-id="2bb9e-141">Yes</span></span>      | <span data-ttu-id="2bb9e-142">En indikator som representerar fakturerings perioden.</span><span class="sxs-lookup"><span data-stu-id="2bb9e-142">An indicator that represents the billing period.</span></span> <span data-ttu-id="2bb9e-143">Det enda värde som stöds är MostRecent.</span><span class="sxs-lookup"><span data-stu-id="2bb9e-143">The only supported value is MostRecent.</span></span> <span data-ttu-id="2bb9e-144">Skift läge för strängen spelar ingen roll.</span><span class="sxs-lookup"><span data-stu-id="2bb9e-144">The case of the string does not matter.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="2bb9e-145">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="2bb9e-145">Request headers</span></span>

<span data-ttu-id="2bb9e-146">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="2bb9e-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2bb9e-147">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="2bb9e-147">Request body</span></span>

<span data-ttu-id="2bb9e-148">Inga.</span><span class="sxs-lookup"><span data-stu-id="2bb9e-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="2bb9e-149">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="2bb9e-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65726577-c208-40fd-9735-8c85ac9cac68/servicecosts/mostrecent/lineitems HTTP/1.1
Authorization: Bearer <authorization token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="2bb9e-150">REST-svar</span><span class="sxs-lookup"><span data-stu-id="2bb9e-150">REST response</span></span>

<span data-ttu-id="2bb9e-151">Om det lyckas innehåller svars texten en [ServiceCostLineItem](service-costs-resources.md) -resurs som ger information om tjänste kostnaderna.</span><span class="sxs-lookup"><span data-stu-id="2bb9e-151">If successful, the response body contains a [ServiceCostLineItem](service-costs-resources.md) resource that provides information about the service costs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2bb9e-152">Följande egenskaper *gäller bara för* service kostnads rad objekt där produkten är ett *Engångs köp*: **productId**, **productName**, **skuId**, **skuName**, **availabilityId**, **publisherId**, **publisherName**, **termAndBillingCycle**, **discountDetails**.</span><span class="sxs-lookup"><span data-stu-id="2bb9e-152">The following properties *only apply to* service cost line items where the product is a *one-time purchase*: **productId**, **productName**, **skuId**, **skuName**, **availabilityId**, **publisherId**, **publisherName**, **termAndBillingCycle**, **discountDetails**.</span></span> <span data-ttu-id="2bb9e-153">Dessa egenskaper *gäller inte för* service rad objekt där produkten är ett *återkommande köp*.</span><span class="sxs-lookup"><span data-stu-id="2bb9e-153">These properties *don't apply to* service line items where the product is a *recurring purchase*.</span></span> <span data-ttu-id="2bb9e-154">Dessa egenskaper gäller till exempel *inte* för prenumerations Office 365-och Azure-datorer.</span><span class="sxs-lookup"><span data-stu-id="2bb9e-154">For example, these properties *don't apply* to subscription-based Office 365 and Azure.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2bb9e-155">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="2bb9e-155">Response success and error codes</span></span>

<span data-ttu-id="2bb9e-156">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="2bb9e-156">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2bb9e-157">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="2bb9e-157">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2bb9e-158">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="2bb9e-158">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2bb9e-159">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="2bb9e-159">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2148
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CV: gPPoyNX1X0asAAcw.0
MS-ServerId: 101112202
Date: Fri, 02 Dec 2016 18: 54: 38 GMT

{
    "attributes": {
        "objectType": "Collection"
    },
    "items":
    [{
            "afterTaxTotal": 0.0,
            "chargeType": "PURCHASE FEE",
            "currencyCode": "USD",
            "currencySymbol": "$",
            "customerId": "ae1d5b32-f9ff-4252-b2bf-40e21937a51a",
            "customerName": "AABB CCDD",
            "endDate": "2016-01-11T00:00:00",
            "offerId": "11E3C9A9-24A2-4CFD-9F60-A9797D68E296",
            "offerName": "Project for Office 365 (Government Pricing)",
            "orderId": "4FEB262A-FAF3-4710-B216-D563421B006F",
            "pretaxTotal": 0.0,
            "quantity": 1.0,
            "resellerMPNId": "-1",
            "startDate": "2015-12-15T00:00:00",
            "subscriptionFriendlyName": "Project Pro for Office 365 (Government Pricing)",
            "subscriptionId": "71B5BCDD-51C8-4BF2-B704-D3432EE33064",
            "tax": 0.0,
            "unitPrice": 0.0,
            "invoiceNumber": "T000003163",
            "invoiceType": "OneTime",
            "productId": "DZH318Z0BJR6",
            "skuId": "0001",
            "availabilityId": "DZH318Z0BMFK",
            "productName": "Azure Managed Experience",
            "skuName": "Azure Managed Experience - Optimize",
            "publisherName": "Microsoft",
            "publisherId": "01323244",
            "termAndBillingCycle": "",
            "discountDetails": "N/A"
        }, {
            "afterTaxTotal": 17.219999999999999,
            "chargeType": "CYCLE FEE",
            "currencyCode": "USD",
            "currencySymbol": "$",
            "customerId": "ae1d5b32-f9ff-4252-b2bf-40e21937a51a",
            "customerName": "AABB CCDD",
            "endDate": "2016-02-11T00:00:00",
            "offerId": "11E3C9A9-24A2-4CFD-9F60-A9797D68E296",
            "offerName": "Project for Office 365 (Government Pricing)",
            "orderId": "4FEB262A-FAF3-4710-B216-D563421B006F",
            "pretaxTotal": 17.219999999999999,
            "quantity": 1.0,
            "resellerMPNId": "-1",
            "startDate": "2016-01-12T00:00:00",
            "subscriptionFriendlyName": "Project Pro for Office 365 (Government Pricing)",
            "subscriptionId": "71B5BCDD-51C8-4BF2-B704-D3432EE33064",
            "tax": 0.0,
            "unitPrice": 17.219999999999999,
            "invoiceNumber": "D000003163",
            "invoiceType": "Recurring",
            "productId": "DZH318Z0BJR7",
            "skuId": "0001",
            "availabilityId": "DZH318Z0BTTTT",
            "productName": "NGINX Plus",
            "skuName": "NGINX Plus (Ubuntu 14.04)",
            "publisherName": "Nginx, Inc.",
            "publisherId": "212336222",
            "termAndBillingCycle": "30 Days Trial",
            "discountDetails": "20%"
        }
    ],
    "links": {
        "self": {
            "headers": [],
            "method": "GET",
            "uri": "/customers/ae1d5b32-f9ff-4252-b2bf-40e21937a51a/servicecosts/MostRecent/lineitems"
        }
    },
    "totalCount": 2
}
```
