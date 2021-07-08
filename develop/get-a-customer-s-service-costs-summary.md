---
title: Hämta sammanfattningen av en kunds servicekostnader
description: Hämtar en kunds tjänstkostnader för den angivna faktureringsperioden.
ms.date: 06/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1cab23238b5f62a02a5f7368f626648d5b1b5b7e
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874915"
---
# <a name="get-a-customers-service-costs-summary"></a><span data-ttu-id="ba492-103">Hämta sammanfattningen av en kunds servicekostnader</span><span class="sxs-lookup"><span data-stu-id="ba492-103">Get a customer's service costs summary</span></span>

<span data-ttu-id="ba492-104">Hämtar en kunds tjänstkostnader för den angivna faktureringsperioden.</span><span class="sxs-lookup"><span data-stu-id="ba492-104">Gets a customer's service costs for the specified billing period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba492-105">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="ba492-105">Prerequisites</span></span>

- <span data-ttu-id="ba492-106">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="ba492-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ba492-107">Det här scenariot stöder autentisering med autentiseringsuppgifter för App+Användare.</span><span class="sxs-lookup"><span data-stu-id="ba492-107">This scenario supports authentication with App+User credentials.</span></span>

- <span data-ttu-id="ba492-108">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ba492-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="ba492-109">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="ba492-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="ba492-110">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="ba492-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="ba492-111">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="ba492-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="ba492-112">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="ba492-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="ba492-113">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ba492-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="ba492-114">En faktureringsperiodindikator ( **`mostrecent`** ).</span><span class="sxs-lookup"><span data-stu-id="ba492-114">A billing period indicator (**`mostrecent`**).</span></span>

## <a name="c"></a><span data-ttu-id="ba492-115">C\#</span><span class="sxs-lookup"><span data-stu-id="ba492-115">C\#</span></span>

<span data-ttu-id="ba492-116">Så här hämtar du en sammanfattning av tjänstkostnader för den angivna kunden:</span><span class="sxs-lookup"><span data-stu-id="ba492-116">To retrieve a service costs summary for the specified customer:</span></span>

1. <span data-ttu-id="ba492-117">Anropa metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="ba492-117">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="ba492-118">Använd egenskapen [**ServiceCosts för**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicecosts) att hämta ett gränssnitt för insamlingsåtgärder för kundtjänstkostnader.</span><span class="sxs-lookup"><span data-stu-id="ba492-118">Use the [**ServiceCosts**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicecosts) property to get an interface to customer service costs collection operations.</span></span>

3. <span data-ttu-id="ba492-119">Anropa metoden [**ByBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.icustomerservicecostscollection.bybillingperiod) med en medlem i [**ServiceCostsBillingPeriod-uppräkningen**](/dotnet/api/microsoft.store.partnercenter.models.servicecosts.servicecostsbillingperiod) för att returnera [**en IServiceCostsCollection**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostscollection).</span><span class="sxs-lookup"><span data-stu-id="ba492-119">Call the [**ByBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.icustomerservicecostscollection.bybillingperiod) method with a member of the [**ServiceCostsBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.models.servicecosts.servicecostsbillingperiod) enumeration to return an [**IServiceCostsCollection**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostscollection).</span></span>

4. <span data-ttu-id="ba492-120">Använd metoden [**IServiceCostsCollection.Summary.Get**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostsummary.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostsummary.getasync) för att hämta en sammanfattning av kundens tjänstkostnader.</span><span class="sxs-lookup"><span data-stu-id="ba492-120">Use the [**IServiceCostsCollection.Summary.Get**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostsummary.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostsummary.getasync) method to get the customer's service costs summary.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var serviceCostsSummary = partnerOperations.Customers.ById(selectedCustomerId).ServiceCosts.ByBillingPeriod(ServiceCostsBillingPeriod.MostRecent).Summary.Get();
```

## <a name="rest-request"></a><span data-ttu-id="ba492-121">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="ba492-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ba492-122">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="ba492-122">Request syntax</span></span>

| <span data-ttu-id="ba492-123">Metod</span><span class="sxs-lookup"><span data-stu-id="ba492-123">Method</span></span>  | <span data-ttu-id="ba492-124">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="ba492-124">Request URI</span></span>                                                                                                   |
|---------|---------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ba492-125">**Få**</span><span class="sxs-lookup"><span data-stu-id="ba492-125">**GET**</span></span> | <span data-ttu-id="ba492-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/servicecosts/{billing-period} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="ba492-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/servicecosts/{billing-period} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="ba492-127">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="ba492-127">URI parameters</span></span>

<span data-ttu-id="ba492-128">Använd följande sökvägsparametrar för att identifiera kunden och faktureringsperioden.</span><span class="sxs-lookup"><span data-stu-id="ba492-128">Use the following path parameters to identify the customer and the billing period.</span></span>

| <span data-ttu-id="ba492-129">Namn</span><span class="sxs-lookup"><span data-stu-id="ba492-129">Name</span></span>           | <span data-ttu-id="ba492-130">Typ</span><span class="sxs-lookup"><span data-stu-id="ba492-130">Type</span></span>   | <span data-ttu-id="ba492-131">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="ba492-131">Required</span></span> | <span data-ttu-id="ba492-132">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="ba492-132">Description</span></span>                                                                                                                      |
|----------------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ba492-133">kund-id</span><span class="sxs-lookup"><span data-stu-id="ba492-133">customer-id</span></span>    | <span data-ttu-id="ba492-134">guid</span><span class="sxs-lookup"><span data-stu-id="ba492-134">guid</span></span>   | <span data-ttu-id="ba492-135">Ja</span><span class="sxs-lookup"><span data-stu-id="ba492-135">Yes</span></span>      | <span data-ttu-id="ba492-136">Ett GUID-formaterat kund-ID som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="ba492-136">A GUID formatted customer ID that identifies the customer.</span></span>                                                                       |
| <span data-ttu-id="ba492-137">faktureringsperiod</span><span class="sxs-lookup"><span data-stu-id="ba492-137">billing-period</span></span> | <span data-ttu-id="ba492-138">sträng</span><span class="sxs-lookup"><span data-stu-id="ba492-138">string</span></span> | <span data-ttu-id="ba492-139">Ja</span><span class="sxs-lookup"><span data-stu-id="ba492-139">Yes</span></span>      | <span data-ttu-id="ba492-140">En indikator som representerar faktureringsperioden.</span><span class="sxs-lookup"><span data-stu-id="ba492-140">An indicator that represents the billing period.</span></span> <span data-ttu-id="ba492-141">Det enda värde som stöds är MostRecent.</span><span class="sxs-lookup"><span data-stu-id="ba492-141">The only supported value is MostRecent.</span></span> <span data-ttu-id="ba492-142">Strängens fall spelar ingen roll.</span><span class="sxs-lookup"><span data-stu-id="ba492-142">The case of the string does not matter.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="ba492-143">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="ba492-143">Request headers</span></span>

<span data-ttu-id="ba492-144">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="ba492-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ba492-145">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="ba492-145">Request body</span></span>

<span data-ttu-id="ba492-146">Inga.</span><span class="sxs-lookup"><span data-stu-id="ba492-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="ba492-147">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="ba492-147">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65726577-c208-40fd-9735-8c85ac9cac68/servicecosts/mostrecent HTTP/1.1
Authorization: Bearer <authorization token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="ba492-148">REST-svar</span><span class="sxs-lookup"><span data-stu-id="ba492-148">REST response</span></span>

<span data-ttu-id="ba492-149">Om det lyckas innehåller svarstexten en [ServiceCostsSummary-resurs](service-costs-resources.md) som innehåller information om tjänstkostnaderna.</span><span class="sxs-lookup"><span data-stu-id="ba492-149">If successful, the response body contains a [ServiceCostsSummary](service-costs-resources.md) resource that provides information about the service costs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ba492-150">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="ba492-150">Response success and error codes</span></span>

<span data-ttu-id="ba492-151">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="ba492-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ba492-152">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="ba492-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ba492-153">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="ba492-153">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ba492-154">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="ba492-154">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 766
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CV: gPPoyNX1X0asAAcw.0
MS-ServerId: 101112202
Date: Fri, 02 Dec 2016 18: 54: 38 GMT

{
    "billingStartDate": "2015-12-12T00:00:00Z",
    "billingEndDate": "2016-01-11T00:00:00Z",
    "pretaxTotal": 17.22,
    "tax": 0.0,
    "afterTaxTotal": 17.22,
    "currencySymbol": "$",
    "customerId": "ae1d5b32-f9ff-4252-b2bf-40e21937a51a",
    "details":
     [
        {
            "invoiceType": "Recurring",
            "summary": {
                "billingStartDate": "2015-12-12T00:00:00Z",
                "billingEndDate": "2016-01-11T00:00:00Z",
                "pretaxTotal": 17.22,
                "tax": 0.0,
                "afterTaxTotal": 17.22,
                "currencyCode": "USD",
                "currencySymbol": "$",
                "customerId": "ae1d5b32-f9ff-4252-b2bf-40e21937a51a",
                "links": {},
                "attributes": {
                    "objectType": "ServiceCostsSummary"
                }
            }
        },
        {
            "invoiceType": "OneTime",
            "summary": {
                "billingStartDate": "2019-04-01T00:00:00Z",
                "billingEndDate": "2019-04-30T23:59:59.9999999Z",
                "pretaxTotal": 2,
                "tax": 0.2,
                "afterTaxTotal": 2.2,
                "currencyCode": "USD",
                "currencySymbol": "$",
                "customerId": "ae1d5b32-f9ff-4252-b2bf-40e21937a51a",
                "links": {},
                "attributes": {
                    "objectType": "ServiceCostsSummary"
                }
            }
        }
    ],
    "links": {
        "serviceCostLineItems": {
            "uri": "/customers/ae1d5b32-f9ff-4252-b2bf-40e21937a51a/servicecosts/MostRecent/lineitems",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/ae1d5b32-f9ff-4252-b2bf-40e21937a51a/servicecosts/MostRecent",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "ServiceCostsSummary"
    }
}
```
