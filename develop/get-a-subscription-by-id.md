---
title: Hämta en prenumeration efter ID
description: Hämtar en prenumerations resurs som matchar kund-ID och prenumerations-ID.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 6690a6886eeb31a78cdb556280d4bdc2b4beb124
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769627"
---
# <a name="get-a-subscription-by-id"></a><span data-ttu-id="97a1c-103">Hämta en prenumeration efter ID</span><span class="sxs-lookup"><span data-stu-id="97a1c-103">Get a subscription by ID</span></span>

<span data-ttu-id="97a1c-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="97a1c-104">**Applies To**</span></span>

- <span data-ttu-id="97a1c-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="97a1c-105">Partner Center</span></span>
- <span data-ttu-id="97a1c-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="97a1c-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="97a1c-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="97a1c-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="97a1c-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="97a1c-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="97a1c-109">Hämtar en [prenumerations](subscription-resources.md) resurs som matchar kund-ID och PRENUMERATIONS-ID.</span><span class="sxs-lookup"><span data-stu-id="97a1c-109">Gets a [Subscription](subscription-resources.md) resource that matches the customer ID and the subscription ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="97a1c-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="97a1c-110">Prerequisites</span></span>

- <span data-ttu-id="97a1c-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="97a1c-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="97a1c-112">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="97a1c-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="97a1c-113">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="97a1c-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="97a1c-114">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="97a1c-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="97a1c-115">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="97a1c-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="97a1c-116">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="97a1c-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="97a1c-117">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="97a1c-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="97a1c-118">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="97a1c-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="97a1c-119">Ett prenumerations-ID.</span><span class="sxs-lookup"><span data-stu-id="97a1c-119">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="97a1c-120">C\#</span><span class="sxs-lookup"><span data-stu-id="97a1c-120">C\#</span></span>

<span data-ttu-id="97a1c-121">För att få en prenumeration efter ID börjar du med att hämta ett gränssnitt till prenumerations åtgärderna genom att anropa metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: t för att identifiera kunden och metoden [**Subscriptions. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) för att identifiera prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="97a1c-121">To get a subscription by ID, begin by obtaining an interface to the subscription operations by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to identify the subscription.</span></span> <span data-ttu-id="97a1c-122">Använd det [**gränssnittet**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) för att hämta prenumerations informationen genom att anropa [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get).</span><span class="sxs-lookup"><span data-stu-id="97a1c-122">Use that [**interface**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) to retrieve the subscription details by calling [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string subscriptionID;

var subscriptionDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(subscriptionID).Get();
```

<span data-ttu-id="97a1c-123">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="97a1c-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="97a1c-124">**Projekt**: Partner Center SDK-exempel **klass**: GetSubscription.CS</span><span class="sxs-lookup"><span data-stu-id="97a1c-124">**Project**: Partner Center SDK Samples **Class**: GetSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="97a1c-125">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="97a1c-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="97a1c-126">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="97a1c-126">Request syntax</span></span>

| <span data-ttu-id="97a1c-127">Metod</span><span class="sxs-lookup"><span data-stu-id="97a1c-127">Method</span></span>  | <span data-ttu-id="97a1c-128">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="97a1c-128">Request URI</span></span>                                                                                                                |
|---------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="97a1c-129">**TA**</span><span class="sxs-lookup"><span data-stu-id="97a1c-129">**GET**</span></span> | <span data-ttu-id="97a1c-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{ID-for-Subscription} http/1.1</span><span class="sxs-lookup"><span data-stu-id="97a1c-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="97a1c-131">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="97a1c-131">URI parameter</span></span>

<span data-ttu-id="97a1c-132">Den här tabellen innehåller de frågeparametrar som krävs för att hämta prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="97a1c-132">This table lists the required query parameters to get the subscription.</span></span>

| <span data-ttu-id="97a1c-133">Namn</span><span class="sxs-lookup"><span data-stu-id="97a1c-133">Name</span></span>                    | <span data-ttu-id="97a1c-134">Typ</span><span class="sxs-lookup"><span data-stu-id="97a1c-134">Type</span></span>     | <span data-ttu-id="97a1c-135">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="97a1c-135">Required</span></span> | <span data-ttu-id="97a1c-136">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="97a1c-136">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="97a1c-137">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="97a1c-137">**customer-tenant-id**</span></span>  | <span data-ttu-id="97a1c-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="97a1c-138">**guid**</span></span> | <span data-ttu-id="97a1c-139">Y</span><span class="sxs-lookup"><span data-stu-id="97a1c-139">Y</span></span>        | <span data-ttu-id="97a1c-140">Ett GUID som motsvarar kunden.</span><span class="sxs-lookup"><span data-stu-id="97a1c-140">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="97a1c-141">**ID för-prenumeration**</span><span class="sxs-lookup"><span data-stu-id="97a1c-141">**id-for-subscription**</span></span> | <span data-ttu-id="97a1c-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="97a1c-142">**guid**</span></span> | <span data-ttu-id="97a1c-143">Y</span><span class="sxs-lookup"><span data-stu-id="97a1c-143">Y</span></span>        | <span data-ttu-id="97a1c-144">Ett GUID som motsvarar prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="97a1c-144">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="97a1c-145">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="97a1c-145">Request headers</span></span>

<span data-ttu-id="97a1c-146">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="97a1c-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="97a1c-147">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="97a1c-147">Request body</span></span>

<span data-ttu-id="97a1c-148">Inga.</span><span class="sxs-lookup"><span data-stu-id="97a1c-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="97a1c-149">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="97a1c-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/A356AC8C-E310-44F4-BF85-C7F29044AF99 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8f489776-a3f3-47cb-91c3-538e1f70f560
MS-CorrelationId: e72e1dc3-4abd-4ce0-908b-d23fdaedcb28
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="97a1c-150">REST-svar</span><span class="sxs-lookup"><span data-stu-id="97a1c-150">REST response</span></span>

<span data-ttu-id="97a1c-151">Om det lyckas returnerar den här metoden en [prenumerations](subscription-resources.md) resurs i svars texten.</span><span class="sxs-lookup"><span data-stu-id="97a1c-151">If successful, this method returns a [Subscription](subscription-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="97a1c-152">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="97a1c-152">Response success and error codes</span></span>

<span data-ttu-id="97a1c-153">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="97a1c-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="97a1c-154">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="97a1c-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="97a1c-155">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="97a1c-155">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example-for-a-standard-subscription"></a><span data-ttu-id="97a1c-156">Svars exempel för en standard prenumeration</span><span class="sxs-lookup"><span data-stu-id="97a1c-156">Response example for a standard subscription</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 833
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e72e1dc3-4abd-4ce0-908b-d23fdaedcb28
MS-RequestId: 8f489776-a3f3-47cb-91c3-538e1f70f560
MS-CV: 7v11Wa//5EuGEo+A.0
MS-ServerId: 202010406
Date: Fri, 27 Jan 2017 21:51:40 GMT

{
    "id": "A356AC8C-E310-44F4-BF85-C7F29044AF99",
    "entitlementId": "42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
    "offerId": "MS-AZR-0145P",
    "offerName": "Microsoft Azure",
    "friendlyName": "Microsoft Azure",
    "quantity": 1,
    "unitType": "Usage-based",
    "creationDate": "2016-05-10T07:30:05.427Z",
    "effectiveStartDate": "2016-05-10T00:00:00Z",
    "commitmentEndDate": "9999-12-10T00:00:00Z",
    "status": "active",
    "autoRenewEnabled": false,
    "billingType": "usage",
    "contractType": "subscription",
    "links": {
        "offer": {
            "uri": "/offers/MS-AZR-0145P?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/A356AC8C-E310-44F4-BF85-C7F29044AF99",
            "method": "GET",
            "headers": []
        }
    },
    "orderId": "B23FDEDD-D6BD-415A-8B71-3624C81C9644",
    "attributes": {
        "etag": "eyJpZCI6ImEzNTZhYzhjLWUzMTAtNDRmNC1iZjg1LWM3ZjI5MDQ0YWY5OSIsInZlcnNpb24iOjJ9",
        "objectType": "Subscription"
    }
}
```

### <a name="response-example-for-an-add-on-subscription"></a><span data-ttu-id="97a1c-157">Svars exempel för en tilläggs prenumeration</span><span class="sxs-lookup"><span data-stu-id="97a1c-157">Response example for an add-on subscription</span></span>

<span data-ttu-id="97a1c-158">Svaret för en tilläggs prenumeration innehåller det överordnade prenumerations-ID: t i bröd texten och i länkarna.</span><span class="sxs-lookup"><span data-stu-id="97a1c-158">The response for an add-on subscription includes the parent subscription ID in the body and in the links.</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1132
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 6eacec93-852d-4167-9d96-c57809bea7ed
MS-RequestId: 22bfd0fb-d1e6-4a8f-aa1a-124b7c820d80
MS-CV: cmde2DtbuUWi8JLq.0
MS-ServerId: 201022015
Date: Fri, 27 Jan 2017 00:12:53 GMT

{
    "id": "968BA1CF-C146-4ADF-A300-308DCF718EEE",
    "offerId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
    "offerName": "Exchange Online Archiving for Exchange Online",
    "friendlyName": "Some friendly name",
    "quantity": 2,
    "unitType": "Licenses",
    "parentSubscriptionId": "1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
    "creationDate": "2017-01-25T23:01:08.693Z",
    "effectiveStartDate": "2017-01-25T00:00:00Z",
    "commitmentEndDate": "2018-02-10T00:00:00Z",
    "status": "active",
    "autoRenewEnabled": true,
    "billingType": "license",
    "contractType": "subscription",
    "links": {
        "offer": {
            "uri": "/offers/2828BE95-46BA-4F91-B2FD-0BEF192ECF60?country=US",
            "method": "GET",
            "headers": []
        },
        "parentSubscription": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/968BA1CF-C146-4ADF-A300-308DCF718EEE",
            "method": "GET",
            "headers": []
        }
    },
    "orderId": "CF3B0E37-BE0B-4CDD-B584-D1A97D98A922",
    "attributes": {
        "etag": "eyJpZCI6Ijk2OGJhMWNmLWMxNDYtNGFkZi1hMzAwLTMwOGRjZjcxOGVlZSIsInZlcnNpb24iOjF9",
        "objectType": "Subscription"
    }
}
```
