---
title: Hämta de hanterade tjänsterna för en kund efter ID
description: Hämtar de hanterade tjänsterna för en kund. Med andra ord får du länkar till alla kund prenumerationer som du har delegerat administratörs behörigheter för. Du kan använda dessa länkar för att tillhandahålla support-och fil tjänst begär Anden med Microsoft.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4764fce6a80035ea4b9dcc6677a3da28fc863eb7
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769801"
---
# <a name="get-the-managed-services-for-a-customer-by-id"></a><span data-ttu-id="c4d57-105">Hämta de hanterade tjänsterna för en kund efter ID</span><span class="sxs-lookup"><span data-stu-id="c4d57-105">Get the managed services for a customer by ID</span></span>

<span data-ttu-id="c4d57-106">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="c4d57-106">**Applies To**</span></span>

- <span data-ttu-id="c4d57-107">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="c4d57-107">Partner Center</span></span>
- <span data-ttu-id="c4d57-108">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="c4d57-108">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="c4d57-109">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="c4d57-109">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="c4d57-110">Hämtar de hanterade tjänsterna för en kund.</span><span class="sxs-lookup"><span data-stu-id="c4d57-110">Gets the managed services for a customer.</span></span> <span data-ttu-id="c4d57-111">Med andra ord får du länkar till alla kund prenumerationer som du har delegerat administratörs behörigheter för.</span><span class="sxs-lookup"><span data-stu-id="c4d57-111">In other words, get links to all of the customer's subscriptions for which you have delegated admin privileges.</span></span> <span data-ttu-id="c4d57-112">Du kan använda dessa länkar för att tillhandahålla support-och fil tjänst begär Anden med Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c4d57-112">You can use these links to provide support and file service requests with Microsoft.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4d57-113">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="c4d57-113">Prerequisites</span></span>

- <span data-ttu-id="c4d57-114">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="c4d57-114">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c4d57-115">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="c4d57-115">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="c4d57-116">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="c4d57-116">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="c4d57-117">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="c4d57-117">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="c4d57-118">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="c4d57-118">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="c4d57-119">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="c4d57-119">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="c4d57-120">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="c4d57-120">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="c4d57-121">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="c4d57-121">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="c4d57-122">C\#</span><span class="sxs-lookup"><span data-stu-id="c4d57-122">C\#</span></span>

<span data-ttu-id="c4d57-123">Om du vill visa en lista över alla hanterade tjänster för en kund använder du din **IAggregatePartner. Customers** -samling och anropar metoden [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="c4d57-123">To display a list of all the managed services for a customer, use your **IAggregatePartner.Customers** collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="c4d57-124">Anropa sedan egenskapen [**ManagedServices**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.managedservices) följt av metoderna [**Get ()**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.get) eller [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.getasync) .</span><span class="sxs-lookup"><span data-stu-id="c4d57-124">Then call the [**ManagedServices**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.managedservices) property, followed by the [**Get()**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerID as Customer;

ResourceCollection<ManagedService> managedServices = partnerOperations.Customers.ById(selectedCustomerId).ManagedServices.Get();
```

<span data-ttu-id="c4d57-125">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="c4d57-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="c4d57-126">**Projekt**: PartnerCenterSDK. FeaturesSamples- **klass**: CustomerManagedServices.CS</span><span class="sxs-lookup"><span data-stu-id="c4d57-126">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: CustomerManagedServices.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="c4d57-127">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="c4d57-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c4d57-128">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="c4d57-128">Request syntax</span></span>

| <span data-ttu-id="c4d57-129">Metod</span><span class="sxs-lookup"><span data-stu-id="c4d57-129">Method</span></span>  | <span data-ttu-id="c4d57-130">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="c4d57-130">Request URI</span></span>                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="c4d57-131">**TA**</span><span class="sxs-lookup"><span data-stu-id="c4d57-131">**GET**</span></span> | <span data-ttu-id="c4d57-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/managedservices http/1.1</span><span class="sxs-lookup"><span data-stu-id="c4d57-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/managedservices HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="c4d57-133">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="c4d57-133">URI parameter</span></span>

<span data-ttu-id="c4d57-134">Använd följande frågeparameter för att hämta kundens hanterade tjänster.</span><span class="sxs-lookup"><span data-stu-id="c4d57-134">Use the following query parameter to get the customer's managed services.</span></span>

| <span data-ttu-id="c4d57-135">Namn</span><span class="sxs-lookup"><span data-stu-id="c4d57-135">Name</span></span>                   | <span data-ttu-id="c4d57-136">Typ</span><span class="sxs-lookup"><span data-stu-id="c4d57-136">Type</span></span>     | <span data-ttu-id="c4d57-137">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="c4d57-137">Required</span></span> | <span data-ttu-id="c4d57-138">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="c4d57-138">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="c4d57-139">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="c4d57-139">**customer-tenant-id**</span></span> | <span data-ttu-id="c4d57-140">**guid**</span><span class="sxs-lookup"><span data-stu-id="c4d57-140">**guid**</span></span> | <span data-ttu-id="c4d57-141">Y</span><span class="sxs-lookup"><span data-stu-id="c4d57-141">Y</span></span>        | <span data-ttu-id="c4d57-142">Ett GUID som motsvarar kunden.</span><span class="sxs-lookup"><span data-stu-id="c4d57-142">A GUID corresponding to the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="c4d57-143">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="c4d57-143">Request headers</span></span>

<span data-ttu-id="c4d57-144">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="c4d57-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="c4d57-145">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="c4d57-145">Request body</span></span>

<span data-ttu-id="c4d57-146">Inga.</span><span class="sxs-lookup"><span data-stu-id="c4d57-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="c4d57-147">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="c4d57-147">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/managedservices HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4ff57220-f17b-4d8f-8e09-78334c57ba00
MS-CorrelationId: 03d6064a-f048-4aee-8892-ed46dc5c8bee
```

## <a name="rest-response"></a><span data-ttu-id="c4d57-148">REST-svar</span><span class="sxs-lookup"><span data-stu-id="c4d57-148">REST response</span></span>

<span data-ttu-id="c4d57-149">Om det lyckas returnerar den här metoden en samling **hanterade tjänst** objekt i svars texten.</span><span class="sxs-lookup"><span data-stu-id="c4d57-149">If successful, this method returns a collection of **Managed Service** objects in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c4d57-150">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="c4d57-150">Response success and error codes</span></span>

<span data-ttu-id="c4d57-151">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="c4d57-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c4d57-152">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="c4d57-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c4d57-153">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="c4d57-153">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="c4d57-154">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="c4d57-154">Response example</span></span>

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
