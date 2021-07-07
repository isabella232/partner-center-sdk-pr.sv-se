---
title: Hämta en kunds prenumerationer
description: Så här hämtar du en samling av en kunds prenumerationer.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 01ac9e5169258d0ac263d5bbe8cff567c76f98ed
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760631"
---
# <a name="get-a-customers-subscriptions"></a><span data-ttu-id="29a6c-103">Hämta en kunds prenumerationer</span><span class="sxs-lookup"><span data-stu-id="29a6c-103">Get a customer's subscriptions</span></span>

<span data-ttu-id="29a6c-104">**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="29a6c-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="29a6c-105">Så här hämtar du en samling av en kunds prenumerationer.</span><span class="sxs-lookup"><span data-stu-id="29a6c-105">How to get a collection of a customer's subscriptions.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29a6c-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="29a6c-106">Prerequisites</span></span>

- <span data-ttu-id="29a6c-107">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="29a6c-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="29a6c-108">Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="29a6c-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="29a6c-109">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="29a6c-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="29a6c-110">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="29a6c-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="29a6c-111">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="29a6c-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="29a6c-112">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="29a6c-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="29a6c-113">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="29a6c-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="29a6c-114">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="29a6c-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="29a6c-115">C\#</span><span class="sxs-lookup"><span data-stu-id="29a6c-115">C\#</span></span>

<span data-ttu-id="29a6c-116">Om du vill hämta en lista över alla en kunds prenumerationer använder du först [**metoden IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kundidentifieraren för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="29a6c-116">To get a list of all of a customer's subscriptions, first use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to identify the customer.</span></span> <span data-ttu-id="29a6c-117">Använd sedan egenskapen [**Prenumerationer**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) för att hämta ett gränssnitt till prenumerationssamlingsåtgärder.</span><span class="sxs-lookup"><span data-stu-id="29a6c-117">Then use the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property to retrieve an interface to subscription collection operations.</span></span> <span data-ttu-id="29a6c-118">Anropa slutligen [**get- eller**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) [**GetAsync-metoderna**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) för att hämta kundens prenumerationssamling.</span><span class="sxs-lookup"><span data-stu-id="29a6c-118">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) methods to retrieve the customer's subscriptions collection.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

var customerSubscriptions = partnerOperations.Customers.ById(customerId).Subscriptions.Get();
```

<span data-ttu-id="29a6c-119">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="29a6c-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="29a6c-120">**Project:** Partnercenter-SDK Samples **Class**: GetSubscriptions.cs</span><span class="sxs-lookup"><span data-stu-id="29a6c-120">**Project**: Partner Center SDK Samples **Class**: GetSubscriptions.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="29a6c-121">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="29a6c-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="29a6c-122">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="29a6c-122">Request syntax</span></span>

| <span data-ttu-id="29a6c-123">Metod</span><span class="sxs-lookup"><span data-stu-id="29a6c-123">Method</span></span>  | <span data-ttu-id="29a6c-124">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="29a6c-124">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="29a6c-125">**Få**</span><span class="sxs-lookup"><span data-stu-id="29a6c-125">**GET**</span></span> | <span data-ttu-id="29a6c-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="29a6c-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="29a6c-127">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="29a6c-127">URI parameter</span></span>

<span data-ttu-id="29a6c-128">Den här tabellen innehåller frågeparametern som krävs för att hämta alla prenumerationer.</span><span class="sxs-lookup"><span data-stu-id="29a6c-128">This table lists the required query parameter to get all the subscriptions.</span></span>

| <span data-ttu-id="29a6c-129">Namn</span><span class="sxs-lookup"><span data-stu-id="29a6c-129">Name</span></span>               | <span data-ttu-id="29a6c-130">Typ</span><span class="sxs-lookup"><span data-stu-id="29a6c-130">Type</span></span>   | <span data-ttu-id="29a6c-131">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="29a6c-131">Required</span></span> | <span data-ttu-id="29a6c-132">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="29a6c-132">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="29a6c-133">kund-klient-id</span><span class="sxs-lookup"><span data-stu-id="29a6c-133">customer-tenant-id</span></span> | <span data-ttu-id="29a6c-134">sträng</span><span class="sxs-lookup"><span data-stu-id="29a6c-134">string</span></span> | <span data-ttu-id="29a6c-135">Ja</span><span class="sxs-lookup"><span data-stu-id="29a6c-135">Yes</span></span>      | <span data-ttu-id="29a6c-136">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="29a6c-136">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="29a6c-137">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="29a6c-137">Request headers</span></span>

<span data-ttu-id="29a6c-138">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="29a6c-138">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="29a6c-139">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="29a6c-139">Request body</span></span>

<span data-ttu-id="29a6c-140">Inga.</span><span class="sxs-lookup"><span data-stu-id="29a6c-140">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="29a6c-141">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="29a6c-141">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b2d13828-2ca5-41d4-94fb-9946214f4244
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="29a6c-142">REST-svar</span><span class="sxs-lookup"><span data-stu-id="29a6c-142">REST response</span></span>

<span data-ttu-id="29a6c-143">Om det lyckas returnerar den här metoden en samling [prenumerationsresurser](subscription-resources.md) i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="29a6c-143">If successful, this method returns a collection of [Subscription](subscription-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="29a6c-144">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="29a6c-144">Response success and error codes</span></span>

<span data-ttu-id="29a6c-145">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="29a6c-145">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="29a6c-146">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="29a6c-146">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="29a6c-147">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="29a6c-147">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="29a6c-148">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="29a6c-148">Response example</span></span>

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
