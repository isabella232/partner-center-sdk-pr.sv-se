---
title: Hämta en lista över beställningar efter kund och faktureringscykeltyp
description: Hämtar en samling order resurser för den angivna kund-och fakturerings cykel typen.
ms.date: 06/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 43fe08b0791851f915e2b39a25394db5ffd022ca
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769537"
---
# <a name="get-a-list-of-orders-by-customer-and-billing-cycle-type"></a><span data-ttu-id="706ec-103">Hämta en lista över beställningar efter kund och faktureringscykeltyp</span><span class="sxs-lookup"><span data-stu-id="706ec-103">Get a list of orders by customer and billing cycle type</span></span>

<span data-ttu-id="706ec-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="706ec-104">**Applies to:**</span></span>

- <span data-ttu-id="706ec-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="706ec-105">Partner Center</span></span>
- <span data-ttu-id="706ec-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="706ec-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="706ec-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="706ec-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="706ec-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="706ec-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="706ec-109">Hämtar en samling order resurser som motsvarar en angiven kund-och fakturerings cykel typ.</span><span class="sxs-lookup"><span data-stu-id="706ec-109">Gets a collection of Order resources that correspond to a given customer and billing cycle type.</span></span> <span data-ttu-id="706ec-110">Det finns en fördröjning på upp till 15 minuter mellan tiden som en beställning skickas och när den kommer att visas i en samling av en kunds beställningar.</span><span class="sxs-lookup"><span data-stu-id="706ec-110">There is a delay of up to 15 minutes between the time an order is submitted and when it will appear in a collection of a customer's orders.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="706ec-111">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="706ec-111">Prerequisites</span></span>

- <span data-ttu-id="706ec-112">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="706ec-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="706ec-113">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="706ec-113">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="706ec-114">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="706ec-114">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="706ec-115">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="706ec-115">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="706ec-116">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="706ec-116">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="706ec-117">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="706ec-117">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="706ec-118">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="706ec-118">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="706ec-119">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="706ec-119">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="706ec-120">C\#</span><span class="sxs-lookup"><span data-stu-id="706ec-120">C\#</span></span>

<span data-ttu-id="706ec-121">Hämta en samling av en kunds beställningar:</span><span class="sxs-lookup"><span data-stu-id="706ec-121">To get a collection of a customer's orders:</span></span>

1. <span data-ttu-id="706ec-122">Använd din [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) -samling och anropa [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) -metoden med det valda kund-ID: t.</span><span class="sxs-lookup"><span data-stu-id="706ec-122">Use your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the selected customer ID.</span></span>

2. <span data-ttu-id="706ec-123">Anropa egenskapen [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) och metoden **ByBillingCycleType ()** med den angivna  [**BillingCycleType**](product-resources.md#billingcycletype).</span><span class="sxs-lookup"><span data-stu-id="706ec-123">Call the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property and the **ByBillingCycleType()** method with your specified  [**BillingCycleType**](product-resources.md#billingcycletype).</span></span>
3. <span data-ttu-id="706ec-124">Anropa metoden [**Get ()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) eller [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync) .</span><span class="sxs-lookup"><span data-stu-id="706ec-124">Call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync) method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// BillingCycleType selectedBillingCycleType;

var orders = partnerOperations.Customers.ById(selectedCustomerId).Orders.ByBillingCycleType(selectedBillingCycleType).Get();
```

## <a name="rest-request"></a><span data-ttu-id="706ec-125">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="706ec-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="706ec-126">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="706ec-126">Request syntax</span></span>

| <span data-ttu-id="706ec-127">Metod</span><span class="sxs-lookup"><span data-stu-id="706ec-127">Method</span></span>  | <span data-ttu-id="706ec-128">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="706ec-128">Request URI</span></span>                                                                                                                    |
|---------|--------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="706ec-129">**TA**</span><span class="sxs-lookup"><span data-stu-id="706ec-129">**GET**</span></span> | <span data-ttu-id="706ec-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Orders? billingType = {fakturerings cykel-typ} http/1.1</span><span class="sxs-lookup"><span data-stu-id="706ec-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders?billingType={billing-cycle-type} HTTP/1.1</span></span>  |

#### <a name="uri-parameters"></a><span data-ttu-id="706ec-131">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="706ec-131">URI parameters</span></span>

<span data-ttu-id="706ec-132">Den här tabellen innehåller de frågeparametrar som krävs för att hämta en samling av beställningar efter kund-ID och typ av fakturerings cykel.</span><span class="sxs-lookup"><span data-stu-id="706ec-132">This table lists the required query parameters to get a collection of orders by customer ID and billing cycle type.</span></span>

| <span data-ttu-id="706ec-133">Namn</span><span class="sxs-lookup"><span data-stu-id="706ec-133">Name</span></span>                   | <span data-ttu-id="706ec-134">Typ</span><span class="sxs-lookup"><span data-stu-id="706ec-134">Type</span></span>     | <span data-ttu-id="706ec-135">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="706ec-135">Required</span></span> | <span data-ttu-id="706ec-136">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="706ec-136">Description</span></span>                                               |
|------------------------|----------|----------|-----------------------------------------------------------|
| <span data-ttu-id="706ec-137">kund-ID för klient organisation</span><span class="sxs-lookup"><span data-stu-id="706ec-137">customer-tenant-id</span></span>     | <span data-ttu-id="706ec-138">sträng</span><span class="sxs-lookup"><span data-stu-id="706ec-138">string</span></span>   | <span data-ttu-id="706ec-139">Yes</span><span class="sxs-lookup"><span data-stu-id="706ec-139">Yes</span></span>      | <span data-ttu-id="706ec-140">En GUID-formaterad sträng som motsvarar kunden.</span><span class="sxs-lookup"><span data-stu-id="706ec-140">A GUID formatted string corresponding to the customer.</span></span>    |
| <span data-ttu-id="706ec-141">fakturering-cykel-typ</span><span class="sxs-lookup"><span data-stu-id="706ec-141">billing-cycle-type</span></span>     | <span data-ttu-id="706ec-142">sträng</span><span class="sxs-lookup"><span data-stu-id="706ec-142">string</span></span>   | <span data-ttu-id="706ec-143">No</span><span class="sxs-lookup"><span data-stu-id="706ec-143">No</span></span>       | <span data-ttu-id="706ec-144">En sträng som motsvarar typen av fakturerings cykel.</span><span class="sxs-lookup"><span data-stu-id="706ec-144">A string corresponding to the billing cycle type.</span></span>         |

### <a name="request-headers"></a><span data-ttu-id="706ec-145">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="706ec-145">Request headers</span></span>

<span data-ttu-id="706ec-146">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="706ec-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="706ec-147">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="706ec-147">Request body</span></span>

<span data-ttu-id="706ec-148">Inga.</span><span class="sxs-lookup"><span data-stu-id="706ec-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="706ec-149">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="706ec-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders?billingType=onetime HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="706ec-150">REST-svar</span><span class="sxs-lookup"><span data-stu-id="706ec-150">REST response</span></span>

<span data-ttu-id="706ec-151">Om det lyckas returnerar den här metoden en samling av [order](order-resources.md) resurser i svars texten.</span><span class="sxs-lookup"><span data-stu-id="706ec-151">If successful, this method returns a collection of [Order](order-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="706ec-152">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="706ec-152">Response success and error codes</span></span>

<span data-ttu-id="706ec-153">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="706ec-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="706ec-154">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="706ec-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="706ec-155">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="706ec-155">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="706ec-156">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="706ec-156">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 22463
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 97fa8b4f-6576-4cd9-dd19-ac7c97a023a7
MS-RequestId: 3c6a034c-82ee-4095-d50f-9b530a415f1f
MS-CV: nb4/b3Yl2keY0eYR.0
MS-ServerId: 202010607
Date: Thu, 15 Mar 2018 20:44:40 GMT

{
    "totalCount": 2,
    "items": [
        {
            "id": "9qg-ErcO-4MPbPqq_3MIQaS7bn8W6HfG1",
            "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
            "billingCycle": "one_time",
            "currencyCode": "USD",
            "lineItems": [
                {
                    "lineItemNumber": 0,
                    "offerId": "DZH318Z0BQ4B:000Z:DZH318Z0DSPL",
                    "friendlyName": "Reserved_VM_Instance_Standard_D1_AP_East_1_Year",
                    "quantity": 1,
                    "links": {
                        "sku": {
                            "uri": "/products/DZH318Z0BQ4B/skus/000Z?country=US",
                            "method": "GET",
                            "headers": []
                        }
                    }
                }
            ],
            "creationDate": "2018-03-15T02:17:15.6455674Z",
            "status": "pending",
            "links": {
                "provisioningStatus": {
                    "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/9qg-ErcO-4MPbPqq_3MIQaS7bn8W6HfG1/provisioningstatus",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/9qg-ErcO-4MPbPqq_3MIQaS7bn8W6HfG1",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Order"
            }
        },
        {
            "id": "s-BZlr_TeGksPNT61SsWRL-sqMaKbyVa1",
            "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
            "billingCycle": "one_time",
            "currencyCode": "USD",
            "lineItems": [
                {
                    "lineItemNumber": 0,
                    "offerId": "DZH318Z0BQ4Z:002P:DZH318Z0CL2D",
                    "friendlyName": "Reserved_VM_Instance_Standard_NC12_AU_East_3_Years",
                    "quantity": 1,
                    "links": {
                        "sku": {
                            "uri": "/products/DZH318Z0BQ4Z/skus/002P?country=US",
                            "method": "GET",
                            "headers": []
                        }
                    }
                }
            ],
            "creationDate": "2018-03-15T01:42:36.8440279Z",
            "status": "pending",
            "links": {
                "provisioningStatus": {
                    "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/s-BZlr_TeGksPNT61SsWRL-sqMaKbyVa1/provisioningstatus",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/s-BZlr_TeGksPNT61SsWRL-sqMaKbyVa1",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": { "objectType": "Order" }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType":
        "Collection"
    }
}
```
