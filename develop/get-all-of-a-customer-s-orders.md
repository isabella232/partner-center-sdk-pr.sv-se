---
title: Hämta en kunds alla beställningar
description: Hämtar en samling med alla beställningar för en angiven kund.
ms.date: 06/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: e8f23e90cbb5afb45e519e2c58fd0d3b9ea2de6a
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760308"
---
# <a name="get-all-of-a-customers-orders"></a><span data-ttu-id="219a5-103">Hämta en kunds alla beställningar</span><span class="sxs-lookup"><span data-stu-id="219a5-103">Get all of a customer's orders</span></span>

<span data-ttu-id="219a5-104">**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="219a5-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="219a5-105">Hämtar en samling med alla beställningar för en angiven kund.</span><span class="sxs-lookup"><span data-stu-id="219a5-105">Gets a collection of all the orders for a specified customer.</span></span> <span data-ttu-id="219a5-106">Det finns en fördröjning på upp till 15 minuter från det att en order skickas tills den visas i en samling av en kunds beställningar.</span><span class="sxs-lookup"><span data-stu-id="219a5-106">There is a delay of up to 15 minutes between the time an order is submitted and when it will appear in a collection of a customer's orders.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="219a5-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="219a5-107">Prerequisites</span></span>

- <span data-ttu-id="219a5-108">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="219a5-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="219a5-109">Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="219a5-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="219a5-110">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="219a5-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="219a5-111">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="219a5-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="219a5-112">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="219a5-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="219a5-113">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="219a5-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="219a5-114">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="219a5-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="219a5-115">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="219a5-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="219a5-116">C\#</span><span class="sxs-lookup"><span data-stu-id="219a5-116">C\#</span></span>

<span data-ttu-id="219a5-117">Så här hämtar du en samling av alla en kunds beställningar:</span><span class="sxs-lookup"><span data-stu-id="219a5-117">To obtain a collection of all of a customer's orders:</span></span>

1. <span data-ttu-id="219a5-118">Använd din [**IAggregatePartner.Customers-samling**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) och anropa [**metoden ById().**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)</span><span class="sxs-lookup"><span data-stu-id="219a5-118">Use your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span>

2. <span data-ttu-id="219a5-119">Anropa egenskapen [**Beställningar**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) följt av metoderna [**Get()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) eller [**GetAsync().**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync)</span><span class="sxs-lookup"><span data-stu-id="219a5-119">Call the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property, followed by the [**Get()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var orders = partnerOperations.Customers.ById(selectedCustomerId).Orders.Get();
```

<span data-ttu-id="219a5-120">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="219a5-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="219a5-121">**Project:** PartnerSDK.FeatureSamples-klass: GetOrders.cs </span><span class="sxs-lookup"><span data-stu-id="219a5-121">**Project**: PartnerSDK.FeatureSamples **Class**: GetOrders.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="219a5-122">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="219a5-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="219a5-123">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="219a5-123">Request syntax</span></span>

| <span data-ttu-id="219a5-124">Metod</span><span class="sxs-lookup"><span data-stu-id="219a5-124">Method</span></span>  | <span data-ttu-id="219a5-125">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="219a5-125">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="219a5-126">**Få**</span><span class="sxs-lookup"><span data-stu-id="219a5-126">**GET**</span></span> | <span data-ttu-id="219a5-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="219a5-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders HTTP/1.1</span></span>  |

#### <a name="uri-parameter"></a><span data-ttu-id="219a5-128">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="219a5-128">URI parameter</span></span>

<span data-ttu-id="219a5-129">Använd följande frågeparameter för att hämta alla beställningar.</span><span class="sxs-lookup"><span data-stu-id="219a5-129">Use the following query parameter to get all orders.</span></span>

| <span data-ttu-id="219a5-130">Namn</span><span class="sxs-lookup"><span data-stu-id="219a5-130">Name</span></span>                   | <span data-ttu-id="219a5-131">Typ</span><span class="sxs-lookup"><span data-stu-id="219a5-131">Type</span></span>     | <span data-ttu-id="219a5-132">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="219a5-132">Required</span></span> | <span data-ttu-id="219a5-133">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="219a5-133">Description</span></span>                                               |
|------------------------|----------|----------|-----------------------------------------------------------|
| <span data-ttu-id="219a5-134">kund-klient-id</span><span class="sxs-lookup"><span data-stu-id="219a5-134">customer-tenant-id</span></span>     | <span data-ttu-id="219a5-135">sträng</span><span class="sxs-lookup"><span data-stu-id="219a5-135">string</span></span>   | <span data-ttu-id="219a5-136">Ja</span><span class="sxs-lookup"><span data-stu-id="219a5-136">Yes</span></span>      | <span data-ttu-id="219a5-137">En GUID-formaterad sträng som motsvarar kunden.</span><span class="sxs-lookup"><span data-stu-id="219a5-137">A GUID formatted string corresponding to the customer.</span></span>    |

### <a name="request-headers"></a><span data-ttu-id="219a5-138">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="219a5-138">Request headers</span></span>

<span data-ttu-id="219a5-139">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="219a5-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="219a5-140">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="219a5-140">Request body</span></span>

<span data-ttu-id="219a5-141">Inga.</span><span class="sxs-lookup"><span data-stu-id="219a5-141">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="219a5-142">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="219a5-142">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="219a5-143">REST-svar</span><span class="sxs-lookup"><span data-stu-id="219a5-143">REST response</span></span>

<span data-ttu-id="219a5-144">Om det lyckas returnerar den här metoden en samling [Order-resurser](order-resources.md) i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="219a5-144">If successful, this method returns a collection of [Order](order-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="219a5-145">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="219a5-145">Response success and error codes</span></span>

<span data-ttu-id="219a5-146">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="219a5-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="219a5-147">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="219a5-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="219a5-148">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="219a5-148">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="219a5-149">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="219a5-149">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 22463
Content-Type: application/json; charset=utf-8
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
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
            "id": "eeba9d00-7b46-443a-917e-22887a8fc993",
            "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
            "billingCycle": "monthly",
            "currencyCode": "USD",
            "lineItems": [
                {
                    "lineItemNumber": 0,
                    "offerId": "E59159FC-6F67-4599-B3CB-17FF4020F643",
                    "subscriptionId": "DB8C695B-1C3C-4C55-B697-771503DD46BF",
                    "friendlyName": "Azure Active Directory Premium P2",
                    "quantity": 1,
                    "links": {
                        "subscription": {
                            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/subscriptions/DB8C695B-1C3C-4C55-B697-771503DD46BF",
                            "method": "GET",
                            "headers": []
                        },
                        "sku": {
                            "uri": "/products/84A661C4-E949-4BD2-A560-ED7766FCAF2B/skus/E59159FC-6F67-4599-B3CB-17FF4020F643",
                            "method": "GET",
                            "headers": []
                        },
                        "provisioningStatus": {
                            "uri": "/subscriptions/DB8C695B-1C3C-4C55-B697-771503DD46BF/provisioningstatus",
                            "method": "GET",
                            "headers": []
                        }
                    }
            ],
            "creationDate": "2018-03-06T17:37:05.253-08:00",
            "status": "completed",
            "links": {
                "self": {
                    "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/eeba9d00-7b46-443a-917e-22887a8fc993",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "etag": "eyJpZCI6ImVlYmE5ZDAwLTdiNDYtNDQzYS05MTdlLTIyODg3YThmYzk5MyIsInZlcnNpb24iOjF9",
                "objectType": "Order"
            }
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
         "objectType": "Collection"
    }
}
```
