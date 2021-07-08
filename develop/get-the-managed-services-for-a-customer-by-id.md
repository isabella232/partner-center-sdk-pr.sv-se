---
title: Hämta de hanterade tjänsterna för en kund efter ID
description: Hämtar de hanterade tjänsterna för en kund. Med andra ord får du länkar till alla kundens prenumerationer som du har delegerat administratörsbehörighet för. Du kan använda dessa länkar för att tillhandahålla support- och filtjänstbegäranden till Microsoft.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1cf7e7b62113bd96b00fdc2301e4e7ac4f5d4243
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548455"
---
# <a name="get-the-managed-services-for-a-customer-by-id"></a><span data-ttu-id="44b28-105">Hämta de hanterade tjänsterna för en kund efter ID</span><span class="sxs-lookup"><span data-stu-id="44b28-105">Get the managed services for a customer by ID</span></span>

<span data-ttu-id="44b28-106">**Gäller för**: Partner Center-| PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="44b28-106">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="44b28-107">Hämtar de hanterade tjänsterna för en kund.</span><span class="sxs-lookup"><span data-stu-id="44b28-107">Gets the managed services for a customer.</span></span> <span data-ttu-id="44b28-108">Med andra ord får du länkar till alla kundens prenumerationer som du har delegerat administratörsbehörighet för.</span><span class="sxs-lookup"><span data-stu-id="44b28-108">In other words, get links to all of the customer's subscriptions for which you have delegated admin privileges.</span></span> <span data-ttu-id="44b28-109">Du kan använda dessa länkar för att tillhandahålla support- och filtjänstbegäranden till Microsoft.</span><span class="sxs-lookup"><span data-stu-id="44b28-109">You can use these links to provide support and file service requests with Microsoft.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44b28-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="44b28-110">Prerequisites</span></span>

- <span data-ttu-id="44b28-111">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="44b28-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="44b28-112">Det här scenariot stöder endast autentisering med app+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="44b28-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="44b28-113">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="44b28-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="44b28-114">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="44b28-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="44b28-115">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="44b28-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="44b28-116">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="44b28-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="44b28-117">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="44b28-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="44b28-118">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="44b28-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="44b28-119">C\#</span><span class="sxs-lookup"><span data-stu-id="44b28-119">C\#</span></span>

<span data-ttu-id="44b28-120">Om du vill visa en lista över alla hanterade tjänster för en kund använder du **samlingen IAggregatePartner.Customers** och anropar [**metoden ById().**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)</span><span class="sxs-lookup"><span data-stu-id="44b28-120">To display a list of all the managed services for a customer, use your **IAggregatePartner.Customers** collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="44b28-121">Anropa sedan egenskapen [**ManagedServices**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.managedservices) följt av metoderna [**Get()**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.get) eller [**GetAsync().**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.getasync)</span><span class="sxs-lookup"><span data-stu-id="44b28-121">Then call the [**ManagedServices**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.managedservices) property, followed by the [**Get()**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerID as Customer;

ResourceCollection<ManagedService> managedServices = partnerOperations.Customers.ById(selectedCustomerId).ManagedServices.Get();
```

<span data-ttu-id="44b28-122">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="44b28-122">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="44b28-123">**Project:** PartnerCenterSDK.FeaturesSamples-klass: CustomerManagedServices.cs </span><span class="sxs-lookup"><span data-stu-id="44b28-123">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: CustomerManagedServices.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="44b28-124">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="44b28-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="44b28-125">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="44b28-125">Request syntax</span></span>

| <span data-ttu-id="44b28-126">Metod</span><span class="sxs-lookup"><span data-stu-id="44b28-126">Method</span></span>  | <span data-ttu-id="44b28-127">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="44b28-127">Request URI</span></span>                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="44b28-128">**Få**</span><span class="sxs-lookup"><span data-stu-id="44b28-128">**GET**</span></span> | <span data-ttu-id="44b28-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/managedservices HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="44b28-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/managedservices HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="44b28-130">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="44b28-130">URI parameter</span></span>

<span data-ttu-id="44b28-131">Använd följande frågeparameter för att hämta kundens hanterade tjänster.</span><span class="sxs-lookup"><span data-stu-id="44b28-131">Use the following query parameter to get the customer's managed services.</span></span>

| <span data-ttu-id="44b28-132">Namn</span><span class="sxs-lookup"><span data-stu-id="44b28-132">Name</span></span>                   | <span data-ttu-id="44b28-133">Typ</span><span class="sxs-lookup"><span data-stu-id="44b28-133">Type</span></span>     | <span data-ttu-id="44b28-134">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="44b28-134">Required</span></span> | <span data-ttu-id="44b28-135">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="44b28-135">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="44b28-136">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="44b28-136">**customer-tenant-id**</span></span> | <span data-ttu-id="44b28-137">**guid**</span><span class="sxs-lookup"><span data-stu-id="44b28-137">**guid**</span></span> | <span data-ttu-id="44b28-138">Y</span><span class="sxs-lookup"><span data-stu-id="44b28-138">Y</span></span>        | <span data-ttu-id="44b28-139">Ett GUID som motsvarar kunden.</span><span class="sxs-lookup"><span data-stu-id="44b28-139">A GUID corresponding to the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="44b28-140">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="44b28-140">Request headers</span></span>

<span data-ttu-id="44b28-141">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="44b28-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="44b28-142">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="44b28-142">Request body</span></span>

<span data-ttu-id="44b28-143">Inga.</span><span class="sxs-lookup"><span data-stu-id="44b28-143">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="44b28-144">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="44b28-144">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/managedservices HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4ff57220-f17b-4d8f-8e09-78334c57ba00
MS-CorrelationId: 03d6064a-f048-4aee-8892-ed46dc5c8bee
```

## <a name="rest-response"></a><span data-ttu-id="44b28-145">REST-svar</span><span class="sxs-lookup"><span data-stu-id="44b28-145">REST response</span></span>

<span data-ttu-id="44b28-146">Om det lyckas returnerar den här metoden en samling **hanterade tjänstobjekt** i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="44b28-146">If successful, this method returns a collection of **Managed Service** objects in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="44b28-147">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="44b28-147">Response success and error codes</span></span>

<span data-ttu-id="44b28-148">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="44b28-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="44b28-149">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="44b28-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="44b28-150">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="44b28-150">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="44b28-151">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="44b28-151">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 10588
Content-Type: application/json
MS-CorrelationId: 03d6064a-f048-4aee-8892-ed46dc5c8bee
MS-RequestId: 4ff57220-f17b-4d8f-8e09-78334c57ba00
Date: Mon, 23 Nov 2015 18:02:12 GMT

{
    "totalCount": 2,
    "items": [{
        "id": "Exchange",
        "name": "Exchange",
        "groupName": "Office",
        "links": {
            "adminService": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=Exchange&InitialDomain=<domain>&PrimaryDomain=<domain>",
                "method": "GET",
                "headers": []
            },
            "serviceHealth": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=ServiceStatus",
                "method": "GET",
                "headers": []
            },
            "serviceTicket": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=Support",
                "method": "GET",
                "headers": []
            }
        },
        "attributes": {
            "objectType": "ManagedService"
        }
    },
    {
        "id": "MicrosoftCommunicationsOnline",
        "name": "SkypeforBusiness",
        "groupName": "Office",
        "links": {
            "adminService": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=MicrosoftCommunicationsOnline",
                "method": "GET",
                "headers": []
            },
            "serviceHealth": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=ServiceStatus",
                "method": "GET",
                "headers": []
            },
            "serviceTicket": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=Support",
                "method": "GET",
                "headers": []
            }
        },
        "attributes": {
            "objectType": "ManagedService"
        }
    }
```
