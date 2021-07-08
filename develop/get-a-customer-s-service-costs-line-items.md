---
title: Hämta radobjekt för en kunds servicekostnader
description: Hämtar kostnadsradsobjekt för en kunds tjänst för den angivna faktureringsperioden.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1bc2914d7c8d41c6d806131444fdc241aa1feb90
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874949"
---
# <a name="get-a-customers-service-costs-line-items"></a><span data-ttu-id="4a56c-103">Hämta radobjekt för en kunds servicekostnader</span><span class="sxs-lookup"><span data-stu-id="4a56c-103">Get a customer's service costs line items</span></span>

<span data-ttu-id="4a56c-104">Hämtar kostnadsradsobjekt för en kunds tjänst för den angivna faktureringsperioden.</span><span class="sxs-lookup"><span data-stu-id="4a56c-104">Gets a customer's service cost line items for the specified billing period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4a56c-105">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="4a56c-105">Prerequisites</span></span>

- <span data-ttu-id="4a56c-106">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="4a56c-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4a56c-107">Det här scenariot stöder autentisering med autentiseringsuppgifter för App+Användare.</span><span class="sxs-lookup"><span data-stu-id="4a56c-107">This scenario supports authentication with App+User credentials.</span></span>

- <span data-ttu-id="4a56c-108">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4a56c-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="4a56c-109">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="4a56c-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="4a56c-110">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="4a56c-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="4a56c-111">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="4a56c-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="4a56c-112">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="4a56c-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="4a56c-113">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4a56c-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="4a56c-114">En faktureringsperiodsindikator ( **`mostrecent`** ).</span><span class="sxs-lookup"><span data-stu-id="4a56c-114">A billing period indicator (**`mostrecent`**).</span></span>

## <a name="c"></a><span data-ttu-id="4a56c-115">C\#</span><span class="sxs-lookup"><span data-stu-id="4a56c-115">C\#</span></span>

<span data-ttu-id="4a56c-116">Så här hämtar du en sammanfattning av tjänstkostnader för den angivna kunden:</span><span class="sxs-lookup"><span data-stu-id="4a56c-116">To retrieve a service costs summary for the specified customer:</span></span>

1. <span data-ttu-id="4a56c-117">Anropa metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="4a56c-117">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="4a56c-118">Använd egenskapen [**ServiceCosts för**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicecosts) att hämta ett gränssnitt till insamlingsåtgärder för kundtjänstkostnader.</span><span class="sxs-lookup"><span data-stu-id="4a56c-118">Use the [**ServiceCosts**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicecosts) property to get an interface to customer service costs collection operations.</span></span>

3. <span data-ttu-id="4a56c-119">Anropa metoden [**ByBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.icustomerservicecostscollection.bybillingperiod) med en medlem i [**ServiceCostsBillingPeriod-uppräkningen**](/dotnet/api/microsoft.store.partnercenter.models.servicecosts.servicecostsbillingperiod) för att returnera [**en IServiceCostsCollection**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostscollection).</span><span class="sxs-lookup"><span data-stu-id="4a56c-119">Call the [**ByBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.icustomerservicecostscollection.bybillingperiod) method with a member of the [**ServiceCostsBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.models.servicecosts.servicecostsbillingperiod) enumeration to return an [**IServiceCostsCollection**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostscollection).</span></span>

4. <span data-ttu-id="4a56c-120">Använd metoden [**IServiceCostsCollection.LineItems.Get**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostlineitemscollection.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostlineitemscollection.getasync) för att hämta kundens tjänstkostnadsradobjekt.</span><span class="sxs-lookup"><span data-stu-id="4a56c-120">Use the [**IServiceCostsCollection.LineItems.Get**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostlineitemscollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostlineitemscollection.getasync) method to get the customer's service costs line items.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var serviceCostsSummary = partnerOperations.Customers.ById(selectedCustomerId).ServiceCosts.ByBillingPeriod(ServiceCostsBillingPeriod.MostRecent).LineItems.Get();
```

## <a name="rest-request"></a><span data-ttu-id="4a56c-121">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="4a56c-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4a56c-122">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="4a56c-122">Request syntax</span></span>

| <span data-ttu-id="4a56c-123">Metod</span><span class="sxs-lookup"><span data-stu-id="4a56c-123">Method</span></span>  | <span data-ttu-id="4a56c-124">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="4a56c-124">Request URI</span></span>                                                                                                             |
|---------|-------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="4a56c-125">**Få**</span><span class="sxs-lookup"><span data-stu-id="4a56c-125">**GET**</span></span> | <span data-ttu-id="4a56c-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/servicecosts/{billing-period}/lineitems HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="4a56c-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/servicecosts/{billing-period}/lineitems HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="4a56c-127">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="4a56c-127">URI parameters</span></span>

<span data-ttu-id="4a56c-128">Använd följande sökvägsparametrar för att identifiera kunden och faktureringsperioden.</span><span class="sxs-lookup"><span data-stu-id="4a56c-128">Use the following path parameters to identify the customer and the billing period.</span></span>

| <span data-ttu-id="4a56c-129">Namn</span><span class="sxs-lookup"><span data-stu-id="4a56c-129">Name</span></span>           | <span data-ttu-id="4a56c-130">Typ</span><span class="sxs-lookup"><span data-stu-id="4a56c-130">Type</span></span>   | <span data-ttu-id="4a56c-131">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="4a56c-131">Required</span></span> | <span data-ttu-id="4a56c-132">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="4a56c-132">Description</span></span>                                                                                                                      |
|----------------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="4a56c-133">kund-ID</span><span class="sxs-lookup"><span data-stu-id="4a56c-133">customer-id</span></span>    | <span data-ttu-id="4a56c-134">guid</span><span class="sxs-lookup"><span data-stu-id="4a56c-134">guid</span></span>   | <span data-ttu-id="4a56c-135">Ja</span><span class="sxs-lookup"><span data-stu-id="4a56c-135">Yes</span></span>      | <span data-ttu-id="4a56c-136">Ett GUID-formaterat kund-ID som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="4a56c-136">A GUID formatted customer ID that identifies the customer.</span></span>                                                                       |
| <span data-ttu-id="4a56c-137">faktureringsperiod</span><span class="sxs-lookup"><span data-stu-id="4a56c-137">billing-period</span></span> | <span data-ttu-id="4a56c-138">sträng</span><span class="sxs-lookup"><span data-stu-id="4a56c-138">string</span></span> | <span data-ttu-id="4a56c-139">Ja</span><span class="sxs-lookup"><span data-stu-id="4a56c-139">Yes</span></span>      | <span data-ttu-id="4a56c-140">En indikator som representerar faktureringsperioden.</span><span class="sxs-lookup"><span data-stu-id="4a56c-140">An indicator that represents the billing period.</span></span> <span data-ttu-id="4a56c-141">Det enda värde som stöds är MostRecent.</span><span class="sxs-lookup"><span data-stu-id="4a56c-141">The only supported value is MostRecent.</span></span> <span data-ttu-id="4a56c-142">Strängens fall spelar ingen roll.</span><span class="sxs-lookup"><span data-stu-id="4a56c-142">The case of the string does not matter.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="4a56c-143">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="4a56c-143">Request headers</span></span>

<span data-ttu-id="4a56c-144">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="4a56c-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4a56c-145">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="4a56c-145">Request body</span></span>

<span data-ttu-id="4a56c-146">Inga.</span><span class="sxs-lookup"><span data-stu-id="4a56c-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="4a56c-147">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="4a56c-147">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65726577-c208-40fd-9735-8c85ac9cac68/servicecosts/mostrecent/lineitems HTTP/1.1
Authorization: Bearer <authorization token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="4a56c-148">REST-svar</span><span class="sxs-lookup"><span data-stu-id="4a56c-148">REST response</span></span>

<span data-ttu-id="4a56c-149">Om det lyckas innehåller svarstexten en [ServiceCostLineItem-resurs](service-costs-resources.md) som innehåller information om tjänstkostnaderna.</span><span class="sxs-lookup"><span data-stu-id="4a56c-149">If successful, the response body contains a [ServiceCostLineItem](service-costs-resources.md) resource that provides information about the service costs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4a56c-150">Följande egenskaper  gäller endast för tjänstkostnadsradobjekt där produkten är ett engångsköp:  **productId**, **productName**, **skuId**, **skuName**, **availabilityId**, **publisherId**, **publisherName**, **termAndBillingCycle**, **discountDetails**.</span><span class="sxs-lookup"><span data-stu-id="4a56c-150">The following properties *only apply to* service cost line items where the product is a *one-time purchase*: **productId**, **productName**, **skuId**, **skuName**, **availabilityId**, **publisherId**, **publisherName**, **termAndBillingCycle**, **discountDetails**.</span></span> <span data-ttu-id="4a56c-151">Dessa egenskaper *gäller inte för tjänstradobjekt* där produkten är ett *återkommande köp.*</span><span class="sxs-lookup"><span data-stu-id="4a56c-151">These properties *don't apply to* service line items where the product is a *recurring purchase*.</span></span> <span data-ttu-id="4a56c-152">Dessa egenskaper gäller till *exempel inte för* prenumerationsbaserade Office 365 och Azure.</span><span class="sxs-lookup"><span data-stu-id="4a56c-152">For example, these properties *don't apply* to subscription-based Office 365 and Azure.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4a56c-153">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="4a56c-153">Response success and error codes</span></span>

<span data-ttu-id="4a56c-154">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="4a56c-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4a56c-155">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="4a56c-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="4a56c-156">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="4a56c-156">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="4a56c-157">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="4a56c-157">Response example</span></span>

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
