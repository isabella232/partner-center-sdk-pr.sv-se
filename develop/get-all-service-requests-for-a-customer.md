---
title: Hämta alla tjänstbegäranden för en kund
description: Hämtar alla kundens tjänst begär Anden.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 6f473c7a7d43b1a3929d983fb23dae92fdafbc0f
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769897"
---
# <a name="get-all-service-requests-for-a-customer"></a><span data-ttu-id="9498d-103">Hämta alla tjänstbegäranden för en kund</span><span class="sxs-lookup"><span data-stu-id="9498d-103">Get all service requests for a customer</span></span>

<span data-ttu-id="9498d-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="9498d-104">**Applies To**</span></span>

- <span data-ttu-id="9498d-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="9498d-105">Partner Center</span></span>
- <span data-ttu-id="9498d-106">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="9498d-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="9498d-107">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="9498d-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="9498d-108">Hämtar alla kundens tjänst begär Anden.</span><span class="sxs-lookup"><span data-stu-id="9498d-108">Gets all of a customer's service requests.</span></span>

<span data-ttu-id="9498d-109">På instrument panelen för partner Center kan du utföra den här åtgärden genom [att först välja en kund](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="9498d-109">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="9498d-110">Välj sedan **Service Management** i den vänstra panelen.</span><span class="sxs-lookup"><span data-stu-id="9498d-110">Then, select **Service management** on the left sidebar.</span></span> <span data-ttu-id="9498d-111">Kundens tjänst begär Anden visas under **support biljetter**.</span><span class="sxs-lookup"><span data-stu-id="9498d-111">The customer's service requests are displayed under **Support tickets**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9498d-112">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="9498d-112">Prerequisites</span></span>

- <span data-ttu-id="9498d-113">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="9498d-113">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9498d-114">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="9498d-114">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="9498d-115">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9498d-115">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="9498d-116">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="9498d-116">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="9498d-117">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="9498d-117">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="9498d-118">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="9498d-118">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="9498d-119">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="9498d-119">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="9498d-120">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9498d-120">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="9498d-121">C\#</span><span class="sxs-lookup"><span data-stu-id="9498d-121">C\#</span></span>

<span data-ttu-id="9498d-122">Om du vill visa en lista över alla kundens tjänst begär Anden använder du din **IAggregatePartner. Customers** -samling och anropar metoden [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="9498d-122">To display a list of all of a customer's service requests, use your **IAggregatePartner.Customers** collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="9498d-123">Anropa sedan egenskapen [**ServiceRequests**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicerequests) följt av metoderna [**Get ()**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.get) eller [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.getasync) .</span><span class="sxs-lookup"><span data-stu-id="9498d-123">Then call the [**ServiceRequests**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicerequests) property, followed by the [**Get()**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId as string;

ResourceCollection<ServiceRequest> serviceRequests = partnerOperations.Customers.ById(customerId).ServiceRequests.Get();
```

<span data-ttu-id="9498d-124">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="9498d-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="9498d-125">**Projekt**: PartnerCenterSDK. FeaturesSamples- **klass**: CustomerManagedServices.CS</span><span class="sxs-lookup"><span data-stu-id="9498d-125">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: CustomerManagedServices.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="9498d-126">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="9498d-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9498d-127">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="9498d-127">Request syntax</span></span>

| <span data-ttu-id="9498d-128">Metod</span><span class="sxs-lookup"><span data-stu-id="9498d-128">Method</span></span>  | <span data-ttu-id="9498d-129">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="9498d-129">Request URI</span></span>                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9498d-130">**TA**</span><span class="sxs-lookup"><span data-stu-id="9498d-130">**GET**</span></span> | <span data-ttu-id="9498d-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/servicerequests http/1.1</span><span class="sxs-lookup"><span data-stu-id="9498d-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/servicerequests HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="9498d-132">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="9498d-132">URI parameter</span></span>

<span data-ttu-id="9498d-133">Använd följande frågeparameter för att hämta alla tjänst begär Anden för kunden.</span><span class="sxs-lookup"><span data-stu-id="9498d-133">Use the following query parameter to get all service requests for the customer.</span></span>

| <span data-ttu-id="9498d-134">Namn</span><span class="sxs-lookup"><span data-stu-id="9498d-134">Name</span></span>                   | <span data-ttu-id="9498d-135">Typ</span><span class="sxs-lookup"><span data-stu-id="9498d-135">Type</span></span>     | <span data-ttu-id="9498d-136">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="9498d-136">Required</span></span> | <span data-ttu-id="9498d-137">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="9498d-137">Description</span></span>                            |
|------------------------|----------|----------|----------------------------------------|
| <span data-ttu-id="9498d-138">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="9498d-138">**customer-tenant-id**</span></span> | <span data-ttu-id="9498d-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="9498d-139">**guid**</span></span> | <span data-ttu-id="9498d-140">Y</span><span class="sxs-lookup"><span data-stu-id="9498d-140">Y</span></span>        | <span data-ttu-id="9498d-141">Ett GUID som motsvarar kunden..</span><span class="sxs-lookup"><span data-stu-id="9498d-141">A GUID corresponding to the customer..</span></span> |

### <a name="request-headers"></a><span data-ttu-id="9498d-142">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="9498d-142">Request headers</span></span>

<span data-ttu-id="9498d-143">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="9498d-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9498d-144">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="9498d-144">Request body</span></span>

<span data-ttu-id="9498d-145">Inga.</span><span class="sxs-lookup"><span data-stu-id="9498d-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="9498d-146">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="9498d-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/servicerequests HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 53d5d48c-9693-46b6-8071-2eed07797d6c
MS-CorrelationId: 998e31a1-3f17-4471-a9ee-7678dd72e033
```

## <a name="rest-response"></a><span data-ttu-id="9498d-147">REST-svar</span><span class="sxs-lookup"><span data-stu-id="9498d-147">REST response</span></span>

<span data-ttu-id="9498d-148">Om det lyckas returnerar den här metoden en samling **tjänst begär ande** resurser i svars texten.</span><span class="sxs-lookup"><span data-stu-id="9498d-148">If successful, this method returns a collection of **Service Request** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9498d-149">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="9498d-149">Response success and error codes</span></span>

<span data-ttu-id="9498d-150">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="9498d-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9498d-151">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="9498d-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9498d-152">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9498d-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9498d-153">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="9498d-153">Response example</span></span>

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
