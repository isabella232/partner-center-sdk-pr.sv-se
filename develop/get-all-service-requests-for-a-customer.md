---
title: Hämta alla tjänstbegäranden för en kund
description: Hämtar alla en kunds tjänstbegäranden.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: ffcbbb9cf14b1b2a5b3becab541d3042c3cad508
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760682"
---
# <a name="get-all-service-requests-for-a-customer"></a><span data-ttu-id="2b8d7-103">Hämta alla tjänstbegäranden för en kund</span><span class="sxs-lookup"><span data-stu-id="2b8d7-103">Get all service requests for a customer</span></span>

<span data-ttu-id="2b8d7-104">**Gäller för**: Partner Center-| PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="2b8d7-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="2b8d7-105">Hämtar alla en kunds tjänstbegäranden.</span><span class="sxs-lookup"><span data-stu-id="2b8d7-105">Gets all of a customer's service requests.</span></span>

<span data-ttu-id="2b8d7-106">På instrumentpanelen i Partnercenter kan du utföra den här åtgärden genom att först [välja en kund.](get-a-customer-by-name.md)</span><span class="sxs-lookup"><span data-stu-id="2b8d7-106">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="2b8d7-107">Välj sedan **Tjänsthantering** i det vänstra sidofältet.</span><span class="sxs-lookup"><span data-stu-id="2b8d7-107">Then, select **Service management** on the left sidebar.</span></span> <span data-ttu-id="2b8d7-108">Kundens tjänstbegäranden visas under **Supportbegäranden.**</span><span class="sxs-lookup"><span data-stu-id="2b8d7-108">The customer's service requests are displayed under **Support tickets**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b8d7-109">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="2b8d7-109">Prerequisites</span></span>

- <span data-ttu-id="2b8d7-110">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="2b8d7-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2b8d7-111">Det här scenariot stöder endast autentisering med app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="2b8d7-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="2b8d7-112">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2b8d7-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="2b8d7-113">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="2b8d7-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="2b8d7-114">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="2b8d7-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="2b8d7-115">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="2b8d7-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="2b8d7-116">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="2b8d7-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="2b8d7-117">Microsoft-ID:t är samma som kund-ID :t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2b8d7-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="2b8d7-118">C\#</span><span class="sxs-lookup"><span data-stu-id="2b8d7-118">C\#</span></span>

<span data-ttu-id="2b8d7-119">Om du vill visa en lista över alla en kunds tjänstbegäranden använder du **samlingen IAggregatePartner.Customers** och anropar [**metoden ById().**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)</span><span class="sxs-lookup"><span data-stu-id="2b8d7-119">To display a list of all of a customer's service requests, use your **IAggregatePartner.Customers** collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="2b8d7-120">Anropa sedan egenskapen [**ServiceRequests**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicerequests) följt av metoderna [**Get()**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.get) eller [**GetAsync().**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.getasync)</span><span class="sxs-lookup"><span data-stu-id="2b8d7-120">Then call the [**ServiceRequests**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicerequests) property, followed by the [**Get()**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId as string;

ResourceCollection<ServiceRequest> serviceRequests = partnerOperations.Customers.ById(customerId).ServiceRequests.Get();
```

<span data-ttu-id="2b8d7-121">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="2b8d7-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="2b8d7-122">**Project:** PartnerCenterSDK.FeaturesSamples-klass: CustomerManagedServices.cs </span><span class="sxs-lookup"><span data-stu-id="2b8d7-122">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: CustomerManagedServices.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="2b8d7-123">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="2b8d7-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2b8d7-124">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="2b8d7-124">Request syntax</span></span>

| <span data-ttu-id="2b8d7-125">Metod</span><span class="sxs-lookup"><span data-stu-id="2b8d7-125">Method</span></span>  | <span data-ttu-id="2b8d7-126">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="2b8d7-126">Request URI</span></span>                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2b8d7-127">**Få**</span><span class="sxs-lookup"><span data-stu-id="2b8d7-127">**GET**</span></span> | <span data-ttu-id="2b8d7-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/servicerequests HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="2b8d7-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/servicerequests HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="2b8d7-129">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="2b8d7-129">URI parameter</span></span>

<span data-ttu-id="2b8d7-130">Använd följande frågeparameter för att hämta alla tjänstbegäranden för kunden.</span><span class="sxs-lookup"><span data-stu-id="2b8d7-130">Use the following query parameter to get all service requests for the customer.</span></span>

| <span data-ttu-id="2b8d7-131">Namn</span><span class="sxs-lookup"><span data-stu-id="2b8d7-131">Name</span></span>                   | <span data-ttu-id="2b8d7-132">Typ</span><span class="sxs-lookup"><span data-stu-id="2b8d7-132">Type</span></span>     | <span data-ttu-id="2b8d7-133">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="2b8d7-133">Required</span></span> | <span data-ttu-id="2b8d7-134">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="2b8d7-134">Description</span></span>                            |
|------------------------|----------|----------|----------------------------------------|
| <span data-ttu-id="2b8d7-135">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="2b8d7-135">**customer-tenant-id**</span></span> | <span data-ttu-id="2b8d7-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="2b8d7-136">**guid**</span></span> | <span data-ttu-id="2b8d7-137">Y</span><span class="sxs-lookup"><span data-stu-id="2b8d7-137">Y</span></span>        | <span data-ttu-id="2b8d7-138">Ett GUID som motsvarar kunden.</span><span class="sxs-lookup"><span data-stu-id="2b8d7-138">A GUID corresponding to the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="2b8d7-139">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="2b8d7-139">Request headers</span></span>

<span data-ttu-id="2b8d7-140">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="2b8d7-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2b8d7-141">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="2b8d7-141">Request body</span></span>

<span data-ttu-id="2b8d7-142">Inga.</span><span class="sxs-lookup"><span data-stu-id="2b8d7-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="2b8d7-143">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="2b8d7-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/servicerequests HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 53d5d48c-9693-46b6-8071-2eed07797d6c
MS-CorrelationId: 998e31a1-3f17-4471-a9ee-7678dd72e033
```

## <a name="rest-response"></a><span data-ttu-id="2b8d7-144">REST-svar</span><span class="sxs-lookup"><span data-stu-id="2b8d7-144">REST response</span></span>

<span data-ttu-id="2b8d7-145">Om det lyckas returnerar den här metoden en samling **tjänstbegäranderesurser** i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="2b8d7-145">If successful, this method returns a collection of **Service Request** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2b8d7-146">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="2b8d7-146">Response success and error codes</span></span>

<span data-ttu-id="2b8d7-147">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="2b8d7-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2b8d7-148">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="2b8d7-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2b8d7-149">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="2b8d7-149">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2b8d7-150">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="2b8d7-150">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 742
Content-Type: application/json
MS-CorrelationId: 998e31a1-3f17-4471-a9ee-7678dd72e033
MS-RequestId: 53d5d48c-9693-46b6-8071-2eed07797d6c
Date: Tue, 24 Nov 2015 07:19:21 GMT

{
    "totalCount": 1,
    "items": [{
        "title": "Test",
        "severity": 0,
        "id": "615112491169010",
        "status": 1,
        "primaryContact": {
            "lastName": "LastName",
            "firstName": "FirstName"
        },
        "createdDate": "2015-11-24T01:07:00.863",
        "lastModifiedDate": "2015-11-24T01:17:10.61",
        "lastClosedDate": "0001-01-01T00:00:00",
        "attributes": {
            "objectType": "ServiceRequest"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}
```
