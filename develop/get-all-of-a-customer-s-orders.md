---
title: Hämta en kunds alla beställningar
description: Hämtar en samling av alla beställningar för en angiven kund.
ms.date: 06/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 4d71cd138421704d94a55a9fe21e074d92638815
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769726"
---
# <a name="get-all-of-a-customers-orders"></a><span data-ttu-id="2c268-103">Hämta en kunds alla beställningar</span><span class="sxs-lookup"><span data-stu-id="2c268-103">Get all of a customer's orders</span></span>

<span data-ttu-id="2c268-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="2c268-104">**Applies to:**</span></span>

- <span data-ttu-id="2c268-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="2c268-105">Partner Center</span></span>
- <span data-ttu-id="2c268-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="2c268-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="2c268-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="2c268-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="2c268-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="2c268-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="2c268-109">Hämtar en samling av alla beställningar för en angiven kund.</span><span class="sxs-lookup"><span data-stu-id="2c268-109">Gets a collection of all the orders for a specified customer.</span></span> <span data-ttu-id="2c268-110">Det finns en fördröjning på upp till 15 minuter mellan tiden som en beställning skickas och när den kommer att visas i en samling av en kunds beställningar.</span><span class="sxs-lookup"><span data-stu-id="2c268-110">There is a delay of up to 15 minutes between the time an order is submitted and when it will appear in a collection of a customer's orders.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c268-111">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="2c268-111">Prerequisites</span></span>

- <span data-ttu-id="2c268-112">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="2c268-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2c268-113">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="2c268-113">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="2c268-114">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2c268-114">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="2c268-115">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="2c268-115">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="2c268-116">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="2c268-116">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="2c268-117">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="2c268-117">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="2c268-118">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="2c268-118">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="2c268-119">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2c268-119">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="2c268-120">C\#</span><span class="sxs-lookup"><span data-stu-id="2c268-120">C\#</span></span>

<span data-ttu-id="2c268-121">Så här hämtar du en samling av alla kund order:</span><span class="sxs-lookup"><span data-stu-id="2c268-121">To obtain a collection of all of a customer's orders:</span></span>

1. <span data-ttu-id="2c268-122">Använd din [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) -samling och anropa [**ById ()-**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metoden.</span><span class="sxs-lookup"><span data-stu-id="2c268-122">Use your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span>

2. <span data-ttu-id="2c268-123">Anropa egenskapen [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) följt av metoderna [**Get ()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) eller [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync) .</span><span class="sxs-lookup"><span data-stu-id="2c268-123">Call the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property, followed by the [**Get()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var orders = partnerOperations.Customers.ById(selectedCustomerId).Orders.Get();
```

<span data-ttu-id="2c268-124">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="2c268-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="2c268-125">**Projekt**: PartnerSDK. FeatureSamples- **klass**: GetOrders.CS</span><span class="sxs-lookup"><span data-stu-id="2c268-125">**Project**: PartnerSDK.FeatureSamples **Class**: GetOrders.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="2c268-126">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="2c268-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2c268-127">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="2c268-127">Request syntax</span></span>

| <span data-ttu-id="2c268-128">Metod</span><span class="sxs-lookup"><span data-stu-id="2c268-128">Method</span></span>  | <span data-ttu-id="2c268-129">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="2c268-129">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="2c268-130">**TA**</span><span class="sxs-lookup"><span data-stu-id="2c268-130">**GET**</span></span> | <span data-ttu-id="2c268-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Orders http/1.1</span><span class="sxs-lookup"><span data-stu-id="2c268-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders HTTP/1.1</span></span>  |

#### <a name="uri-parameter"></a><span data-ttu-id="2c268-132">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="2c268-132">URI parameter</span></span>

<span data-ttu-id="2c268-133">Använd följande frågeparameter för att hämta alla beställningar.</span><span class="sxs-lookup"><span data-stu-id="2c268-133">Use the following query parameter to get all orders.</span></span>

| <span data-ttu-id="2c268-134">Namn</span><span class="sxs-lookup"><span data-stu-id="2c268-134">Name</span></span>                   | <span data-ttu-id="2c268-135">Typ</span><span class="sxs-lookup"><span data-stu-id="2c268-135">Type</span></span>     | <span data-ttu-id="2c268-136">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="2c268-136">Required</span></span> | <span data-ttu-id="2c268-137">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="2c268-137">Description</span></span>                                               |
|------------------------|----------|----------|-----------------------------------------------------------|
| <span data-ttu-id="2c268-138">kund-ID för klient organisation</span><span class="sxs-lookup"><span data-stu-id="2c268-138">customer-tenant-id</span></span>     | <span data-ttu-id="2c268-139">sträng</span><span class="sxs-lookup"><span data-stu-id="2c268-139">string</span></span>   | <span data-ttu-id="2c268-140">Yes</span><span class="sxs-lookup"><span data-stu-id="2c268-140">Yes</span></span>      | <span data-ttu-id="2c268-141">En GUID-formaterad sträng som motsvarar kunden.</span><span class="sxs-lookup"><span data-stu-id="2c268-141">A GUID formatted string corresponding to the customer.</span></span>    |

### <a name="request-headers"></a><span data-ttu-id="2c268-142">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="2c268-142">Request headers</span></span>

<span data-ttu-id="2c268-143">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="2c268-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2c268-144">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="2c268-144">Request body</span></span>

<span data-ttu-id="2c268-145">Inga.</span><span class="sxs-lookup"><span data-stu-id="2c268-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="2c268-146">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="2c268-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="2c268-147">REST-svar</span><span class="sxs-lookup"><span data-stu-id="2c268-147">REST response</span></span>

<span data-ttu-id="2c268-148">Om det lyckas returnerar den här metoden en samling av [order](order-resources.md) resurser i svars texten.</span><span class="sxs-lookup"><span data-stu-id="2c268-148">If successful, this method returns a collection of [Order](order-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2c268-149">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="2c268-149">Response success and error codes</span></span>

<span data-ttu-id="2c268-150">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="2c268-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2c268-151">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="2c268-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2c268-152">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="2c268-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2c268-153">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="2c268-153">Response example</span></span>

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
