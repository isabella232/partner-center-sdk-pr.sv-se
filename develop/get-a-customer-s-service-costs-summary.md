---
title: Hämta sammanfattningen av en kunds servicekostnader
description: Hämtar en kundens tjänste kostnader för den angivna fakturerings perioden.
ms.date: 06/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 635e61342e13c3676120ec0df02f1e8bffda64ac
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769348"
---
# <a name="get-a-customers-service-costs-summary"></a><span data-ttu-id="a007f-103">Hämta sammanfattningen av en kunds servicekostnader</span><span class="sxs-lookup"><span data-stu-id="a007f-103">Get a customer's service costs summary</span></span>

<span data-ttu-id="a007f-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="a007f-104">**Applies to:**</span></span>

- <span data-ttu-id="a007f-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="a007f-105">Partner Center</span></span>

<span data-ttu-id="a007f-106">Hämtar en kundens tjänste kostnader för den angivna fakturerings perioden.</span><span class="sxs-lookup"><span data-stu-id="a007f-106">Gets a customer's service costs for the specified billing period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a007f-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="a007f-107">Prerequisites</span></span>

- <span data-ttu-id="a007f-108">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="a007f-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a007f-109">Det här scenariot stöder autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="a007f-109">This scenario supports authentication with App+User credentials.</span></span>

- <span data-ttu-id="a007f-110">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a007f-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="a007f-111">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="a007f-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="a007f-112">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="a007f-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="a007f-113">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="a007f-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="a007f-114">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="a007f-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="a007f-115">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a007f-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="a007f-116">En fakturerings periods indikator ( **`mostrecent`** ).</span><span class="sxs-lookup"><span data-stu-id="a007f-116">A billing period indicator (**`mostrecent`**).</span></span>

## <a name="c"></a><span data-ttu-id="a007f-117">C\#</span><span class="sxs-lookup"><span data-stu-id="a007f-117">C\#</span></span>

<span data-ttu-id="a007f-118">Så här hämtar du en service kostnads Sammanfattning för den angivna kunden:</span><span class="sxs-lookup"><span data-stu-id="a007f-118">To retrieve a service costs summary for the specified customer:</span></span>

1. <span data-ttu-id="a007f-119">Anropa metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="a007f-119">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="a007f-120">Använd egenskapen [**ServiceCosts**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicecosts) för att hämta ett gränssnitt till kund tjänst kostnader för insamlings åtgärder.</span><span class="sxs-lookup"><span data-stu-id="a007f-120">Use the [**ServiceCosts**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicecosts) property to get an interface to customer service costs collection operations.</span></span>

3. <span data-ttu-id="a007f-121">Anropa metoden [**ByBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.icustomerservicecostscollection.bybillingperiod) med en medlem i [**ServiceCostsBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.models.servicecosts.servicecostsbillingperiod) -uppräkningen för att returnera en [**IServiceCostsCollection**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostscollection).</span><span class="sxs-lookup"><span data-stu-id="a007f-121">Call the [**ByBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.icustomerservicecostscollection.bybillingperiod) method with a member of the [**ServiceCostsBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.models.servicecosts.servicecostsbillingperiod) enumeration to return an [**IServiceCostsCollection**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostscollection).</span></span>

4. <span data-ttu-id="a007f-122">Använd metoden [**IServiceCostsCollection. Summary. get**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostsummary.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostsummary.getasync) för att hämta kundens tjänste kostnads Sammanfattning.</span><span class="sxs-lookup"><span data-stu-id="a007f-122">Use the [**IServiceCostsCollection.Summary.Get**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostsummary.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostsummary.getasync) method to get the customer's service costs summary.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var serviceCostsSummary = partnerOperations.Customers.ById(selectedCustomerId).ServiceCosts.ByBillingPeriod(ServiceCostsBillingPeriod.MostRecent).Summary.Get();
```

## <a name="rest-request"></a><span data-ttu-id="a007f-123">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="a007f-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a007f-124">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="a007f-124">Request syntax</span></span>

| <span data-ttu-id="a007f-125">Metod</span><span class="sxs-lookup"><span data-stu-id="a007f-125">Method</span></span>  | <span data-ttu-id="a007f-126">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="a007f-126">Request URI</span></span>                                                                                                   |
|---------|---------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a007f-127">**TA**</span><span class="sxs-lookup"><span data-stu-id="a007f-127">**GET**</span></span> | <span data-ttu-id="a007f-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/servicecosts/{Billing-period} http/1.1</span><span class="sxs-lookup"><span data-stu-id="a007f-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/servicecosts/{billing-period} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="a007f-129">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="a007f-129">URI parameters</span></span>

<span data-ttu-id="a007f-130">Använd följande Sök vägs parametrar för att identifiera kunden och fakturerings perioden.</span><span class="sxs-lookup"><span data-stu-id="a007f-130">Use the following path parameters to identify the customer and the billing period.</span></span>

| <span data-ttu-id="a007f-131">Namn</span><span class="sxs-lookup"><span data-stu-id="a007f-131">Name</span></span>           | <span data-ttu-id="a007f-132">Typ</span><span class="sxs-lookup"><span data-stu-id="a007f-132">Type</span></span>   | <span data-ttu-id="a007f-133">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="a007f-133">Required</span></span> | <span data-ttu-id="a007f-134">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="a007f-134">Description</span></span>                                                                                                                      |
|----------------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a007f-135">kund-ID</span><span class="sxs-lookup"><span data-stu-id="a007f-135">customer-id</span></span>    | <span data-ttu-id="a007f-136">guid</span><span class="sxs-lookup"><span data-stu-id="a007f-136">guid</span></span>   | <span data-ttu-id="a007f-137">Yes</span><span class="sxs-lookup"><span data-stu-id="a007f-137">Yes</span></span>      | <span data-ttu-id="a007f-138">Ett GUID-formaterat kund-ID som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="a007f-138">A GUID formatted customer ID that identifies the customer.</span></span>                                                                       |
| <span data-ttu-id="a007f-139">fakturerings period</span><span class="sxs-lookup"><span data-stu-id="a007f-139">billing-period</span></span> | <span data-ttu-id="a007f-140">sträng</span><span class="sxs-lookup"><span data-stu-id="a007f-140">string</span></span> | <span data-ttu-id="a007f-141">Yes</span><span class="sxs-lookup"><span data-stu-id="a007f-141">Yes</span></span>      | <span data-ttu-id="a007f-142">En indikator som representerar fakturerings perioden.</span><span class="sxs-lookup"><span data-stu-id="a007f-142">An indicator that represents the billing period.</span></span> <span data-ttu-id="a007f-143">Det enda värde som stöds är MostRecent.</span><span class="sxs-lookup"><span data-stu-id="a007f-143">The only supported value is MostRecent.</span></span> <span data-ttu-id="a007f-144">Skift läge för strängen spelar ingen roll.</span><span class="sxs-lookup"><span data-stu-id="a007f-144">The case of the string does not matter.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="a007f-145">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="a007f-145">Request headers</span></span>

<span data-ttu-id="a007f-146">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="a007f-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a007f-147">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="a007f-147">Request body</span></span>

<span data-ttu-id="a007f-148">Inga.</span><span class="sxs-lookup"><span data-stu-id="a007f-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="a007f-149">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="a007f-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65726577-c208-40fd-9735-8c85ac9cac68/servicecosts/mostrecent HTTP/1.1
Authorization: Bearer <authorization token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="a007f-150">REST-svar</span><span class="sxs-lookup"><span data-stu-id="a007f-150">REST response</span></span>

<span data-ttu-id="a007f-151">Om det lyckas innehåller svars texten en [ServiceCostsSummary](service-costs-resources.md) -resurs som ger information om tjänste kostnaderna.</span><span class="sxs-lookup"><span data-stu-id="a007f-151">If successful, the response body contains a [ServiceCostsSummary](service-costs-resources.md) resource that provides information about the service costs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a007f-152">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="a007f-152">Response success and error codes</span></span>

<span data-ttu-id="a007f-153">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="a007f-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a007f-154">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="a007f-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a007f-155">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="a007f-155">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a007f-156">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="a007f-156">Response example</span></span>

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
