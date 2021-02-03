---
title: Hämta en kunds prenumerationer
description: Så här hämtar du en samling av en kunds prenumerationer.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a037e4a81fccbff0a02b0bdf6d93478ee15fd50f
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769717"
---
# <a name="get-a-customers-subscriptions"></a><span data-ttu-id="9e465-103">Hämta en kunds prenumerationer</span><span class="sxs-lookup"><span data-stu-id="9e465-103">Get a customer's subscriptions</span></span>

<span data-ttu-id="9e465-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="9e465-104">**Applies To**</span></span>

- <span data-ttu-id="9e465-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="9e465-105">Partner Center</span></span>
- <span data-ttu-id="9e465-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="9e465-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="9e465-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="9e465-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="9e465-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="9e465-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="9e465-109">Så här hämtar du en samling av en kunds prenumerationer.</span><span class="sxs-lookup"><span data-stu-id="9e465-109">How to get a collection of a customer's subscriptions.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9e465-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="9e465-110">Prerequisites</span></span>

- <span data-ttu-id="9e465-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="9e465-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9e465-112">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="9e465-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="9e465-113">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9e465-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="9e465-114">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="9e465-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="9e465-115">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="9e465-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="9e465-116">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="9e465-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="9e465-117">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="9e465-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="9e465-118">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9e465-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="9e465-119">C\#</span><span class="sxs-lookup"><span data-stu-id="9e465-119">C\#</span></span>

<span data-ttu-id="9e465-120">Om du vill hämta en lista över alla kund prenumerationer använder du först metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund identifieraren för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="9e465-120">To get a list of all of a customer's subscriptions, first use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to identify the customer.</span></span> <span data-ttu-id="9e465-121">Använd sedan egenskapen [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) för att hämta ett gränssnitt för prenumerations samlings åtgärder.</span><span class="sxs-lookup"><span data-stu-id="9e465-121">Then use the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property to retrieve an interface to subscription collection operations.</span></span> <span data-ttu-id="9e465-122">Anropa slutligen metoderna [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) för att hämta kundens prenumerations samling.</span><span class="sxs-lookup"><span data-stu-id="9e465-122">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) methods to retrieve the customer's subscriptions collection.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

var customerSubscriptions = partnerOperations.Customers.ById(customerId).Subscriptions.Get();
```

<span data-ttu-id="9e465-123">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="9e465-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="9e465-124">**Projekt**: Partner Center SDK-exempel **klass**: GetSubscriptions.CS</span><span class="sxs-lookup"><span data-stu-id="9e465-124">**Project**: Partner Center SDK Samples **Class**: GetSubscriptions.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="9e465-125">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="9e465-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9e465-126">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="9e465-126">Request syntax</span></span>

| <span data-ttu-id="9e465-127">Metod</span><span class="sxs-lookup"><span data-stu-id="9e465-127">Method</span></span>  | <span data-ttu-id="9e465-128">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="9e465-128">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9e465-129">**TA**</span><span class="sxs-lookup"><span data-stu-id="9e465-129">**GET**</span></span> | <span data-ttu-id="9e465-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions http/1.1</span><span class="sxs-lookup"><span data-stu-id="9e465-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="9e465-131">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="9e465-131">URI parameter</span></span>

<span data-ttu-id="9e465-132">Den här tabellen innehåller den obligatoriska Frågeparametern för att hämta alla prenumerationer.</span><span class="sxs-lookup"><span data-stu-id="9e465-132">This table lists the required query parameter to get all the subscriptions.</span></span>

| <span data-ttu-id="9e465-133">Namn</span><span class="sxs-lookup"><span data-stu-id="9e465-133">Name</span></span>               | <span data-ttu-id="9e465-134">Typ</span><span class="sxs-lookup"><span data-stu-id="9e465-134">Type</span></span>   | <span data-ttu-id="9e465-135">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="9e465-135">Required</span></span> | <span data-ttu-id="9e465-136">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="9e465-136">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="9e465-137">kund-ID för klient organisation</span><span class="sxs-lookup"><span data-stu-id="9e465-137">customer-tenant-id</span></span> | <span data-ttu-id="9e465-138">sträng</span><span class="sxs-lookup"><span data-stu-id="9e465-138">string</span></span> | <span data-ttu-id="9e465-139">Yes</span><span class="sxs-lookup"><span data-stu-id="9e465-139">Yes</span></span>      | <span data-ttu-id="9e465-140">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="9e465-140">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="9e465-141">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="9e465-141">Request headers</span></span>

<span data-ttu-id="9e465-142">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="9e465-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9e465-143">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="9e465-143">Request body</span></span>

<span data-ttu-id="9e465-144">Inga.</span><span class="sxs-lookup"><span data-stu-id="9e465-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="9e465-145">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="9e465-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b2d13828-2ca5-41d4-94fb-9946214f4244
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="9e465-146">REST-svar</span><span class="sxs-lookup"><span data-stu-id="9e465-146">REST response</span></span>

<span data-ttu-id="9e465-147">Om det lyckas returnerar den här metoden en samling [prenumerations](subscription-resources.md) resurser i svars texten.</span><span class="sxs-lookup"><span data-stu-id="9e465-147">If successful, this method returns a collection of [Subscription](subscription-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9e465-148">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="9e465-148">Response success and error codes</span></span>

<span data-ttu-id="9e465-149">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="9e465-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9e465-150">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="9e465-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9e465-151">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9e465-151">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9e465-152">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="9e465-152">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 73754
Content-Type: application/json
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
MS-RequestId: b2d13828-2ca5-41d4-94fb-9946214f4244
Date: Wed, 25 Nov 2015 05:43:06 GMT

{
    "totalCount": 37,
    "items": [{
        "id": "83ef9d05-4169-4ef9-9657-0e86b1eab1de",
        "entitlementId": "a356ac8c-e310-44f4-bf85-C7f29044af99",
        "friendlyName": "nickname",
        "quantity": 1,
        "unitType": "none",
        "creationDate": "2015-11-25T06: 41: 12Z",
        "effectiveStartDate": "2015-11-24T08: 00: 00Z",
        "commitmentEndDate": "2016-12-12T08: 00: 00Z",
        "status": "active",
        "autoRenewEnabled": false,
        "billingType": "none",
        "contractType": "subscription",
        "links": {
            "offer": {
                "uri": "/v1/offers/0CCA44D6-68E9-4762-94EE-31ECE98783B9",
                "method": "GET",
                "headers": []
            },
            "self": {
                "uri": "/subscriptions?key=<key>",
                "method": "GET",
                "headers": []
            }
        },
        "orderId": "6183db3d-6318-4e52-877e-25806e4971be",
        "attributes": {
            "etag": "<etag>",
            "objectType": "Subscription"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}
```
