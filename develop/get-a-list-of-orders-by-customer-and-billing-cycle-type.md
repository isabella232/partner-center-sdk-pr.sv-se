---
title: Hämta en lista över beställningar efter kund och faktureringscykeltyp
description: Hämtar en samling orderresurser för den angivna kund- och faktureringscykeltypen.
ms.date: 06/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: c52a556887dba065c4ccd1a82d6223624d0ad1f2
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874235"
---
# <a name="get-a-list-of-orders-by-customer-and-billing-cycle-type"></a><span data-ttu-id="42290-103">Hämta en lista över beställningar efter kund och faktureringscykeltyp</span><span class="sxs-lookup"><span data-stu-id="42290-103">Get a list of orders by customer and billing cycle type</span></span>

<span data-ttu-id="42290-104">**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="42290-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="42290-105">Hämtar en samling orderresurser som motsvarar en viss kund och faktureringscykeltyp.</span><span class="sxs-lookup"><span data-stu-id="42290-105">Gets a collection of Order resources that correspond to a given customer and billing cycle type.</span></span> <span data-ttu-id="42290-106">Det finns en fördröjning på upp till 15 minuter mellan den tidpunkt då en order skickas och när den visas i en samling av en kunds beställningar.</span><span class="sxs-lookup"><span data-stu-id="42290-106">There is a delay of up to 15 minutes between the time an order is submitted and when it will appear in a collection of a customer's orders.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42290-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="42290-107">Prerequisites</span></span>

- <span data-ttu-id="42290-108">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="42290-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="42290-109">Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="42290-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="42290-110">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="42290-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="42290-111">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="42290-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="42290-112">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="42290-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="42290-113">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="42290-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="42290-114">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="42290-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="42290-115">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="42290-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="42290-116">C\#</span><span class="sxs-lookup"><span data-stu-id="42290-116">C\#</span></span>

<span data-ttu-id="42290-117">Så här hämtar du en samling av en kunds beställningar:</span><span class="sxs-lookup"><span data-stu-id="42290-117">To get a collection of a customer's orders:</span></span>

1. <span data-ttu-id="42290-118">Använd samlingen [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) och anropa [**metoden ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med det valda kund-ID:t.</span><span class="sxs-lookup"><span data-stu-id="42290-118">Use your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the selected customer ID.</span></span>

2. <span data-ttu-id="42290-119">Anropa egenskapen [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) och **metoden ByBillingCycleType()** med din angivna  [**BillingCycleType**](product-resources.md#billingcycletype).</span><span class="sxs-lookup"><span data-stu-id="42290-119">Call the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property and the **ByBillingCycleType()** method with your specified  [**BillingCycleType**](product-resources.md#billingcycletype).</span></span>
3. <span data-ttu-id="42290-120">Anropa [**metoden Get()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) eller [**GetAsync().**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync)</span><span class="sxs-lookup"><span data-stu-id="42290-120">Call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync) method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// BillingCycleType selectedBillingCycleType;

var orders = partnerOperations.Customers.ById(selectedCustomerId).Orders.ByBillingCycleType(selectedBillingCycleType).Get();
```

## <a name="rest-request"></a><span data-ttu-id="42290-121">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="42290-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="42290-122">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="42290-122">Request syntax</span></span>

| <span data-ttu-id="42290-123">Metod</span><span class="sxs-lookup"><span data-stu-id="42290-123">Method</span></span>  | <span data-ttu-id="42290-124">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="42290-124">Request URI</span></span>                                                                                                                    |
|---------|--------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="42290-125">**Få**</span><span class="sxs-lookup"><span data-stu-id="42290-125">**GET**</span></span> | <span data-ttu-id="42290-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders?billingType={billing-cycle-type} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="42290-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders?billingType={billing-cycle-type} HTTP/1.1</span></span>  |

#### <a name="uri-parameters"></a><span data-ttu-id="42290-127">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="42290-127">URI parameters</span></span>

<span data-ttu-id="42290-128">I den här tabellen visas de frågeparametrar som krävs för att hämta en samling beställningar efter kund-ID och faktureringscykeltyp.</span><span class="sxs-lookup"><span data-stu-id="42290-128">This table lists the required query parameters to get a collection of orders by customer ID and billing cycle type.</span></span>

| <span data-ttu-id="42290-129">Namn</span><span class="sxs-lookup"><span data-stu-id="42290-129">Name</span></span>                   | <span data-ttu-id="42290-130">Typ</span><span class="sxs-lookup"><span data-stu-id="42290-130">Type</span></span>     | <span data-ttu-id="42290-131">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="42290-131">Required</span></span> | <span data-ttu-id="42290-132">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="42290-132">Description</span></span>                                               |
|------------------------|----------|----------|-----------------------------------------------------------|
| <span data-ttu-id="42290-133">kund-klient-id</span><span class="sxs-lookup"><span data-stu-id="42290-133">customer-tenant-id</span></span>     | <span data-ttu-id="42290-134">sträng</span><span class="sxs-lookup"><span data-stu-id="42290-134">string</span></span>   | <span data-ttu-id="42290-135">Ja</span><span class="sxs-lookup"><span data-stu-id="42290-135">Yes</span></span>      | <span data-ttu-id="42290-136">En GUID-formaterad sträng som motsvarar kunden.</span><span class="sxs-lookup"><span data-stu-id="42290-136">A GUID formatted string corresponding to the customer.</span></span>    |
| <span data-ttu-id="42290-137">billing-cycle-type</span><span class="sxs-lookup"><span data-stu-id="42290-137">billing-cycle-type</span></span>     | <span data-ttu-id="42290-138">sträng</span><span class="sxs-lookup"><span data-stu-id="42290-138">string</span></span>   | <span data-ttu-id="42290-139">No</span><span class="sxs-lookup"><span data-stu-id="42290-139">No</span></span>       | <span data-ttu-id="42290-140">En sträng som motsvarar faktureringscykeltypen.</span><span class="sxs-lookup"><span data-stu-id="42290-140">A string corresponding to the billing cycle type.</span></span>         |

### <a name="request-headers"></a><span data-ttu-id="42290-141">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="42290-141">Request headers</span></span>

<span data-ttu-id="42290-142">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="42290-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="42290-143">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="42290-143">Request body</span></span>

<span data-ttu-id="42290-144">Inga.</span><span class="sxs-lookup"><span data-stu-id="42290-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="42290-145">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="42290-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders?billingType=onetime HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="42290-146">REST-svar</span><span class="sxs-lookup"><span data-stu-id="42290-146">REST response</span></span>

<span data-ttu-id="42290-147">Om det lyckas returnerar den här metoden en samling [Order-resurser](order-resources.md) i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="42290-147">If successful, this method returns a collection of [Order](order-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="42290-148">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="42290-148">Response success and error codes</span></span>

<span data-ttu-id="42290-149">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="42290-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="42290-150">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="42290-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="42290-151">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="42290-151">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="42290-152">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="42290-152">Response example</span></span>

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
