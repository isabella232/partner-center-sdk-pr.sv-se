---
title: Hämta en kunds faktureringsprofil
description: Hämtar faktureringsprofilen för en kund. På instrumentpanelen i Partnercenter kan du utföra den här åtgärden genom att först välja en kund.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: d22be53a5be4efcda76a568578468615495febb6
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760597"
---
# <a name="get-a-customers-billing-profile"></a><span data-ttu-id="b72d7-104">Hämta en kunds faktureringsprofil</span><span class="sxs-lookup"><span data-stu-id="b72d7-104">Get a customer's billing profile</span></span>

<span data-ttu-id="b72d7-105">**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="b72d7-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="b72d7-106">Hämtar faktureringsprofilen för en kund.</span><span class="sxs-lookup"><span data-stu-id="b72d7-106">Gets the billing profile of a customer.</span></span>

<span data-ttu-id="b72d7-107">På instrumentpanelen i Partnercenter kan du utföra den här åtgärden genom att först [välja en kund.](get-a-customer-by-name.md)</span><span class="sxs-lookup"><span data-stu-id="b72d7-107">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="b72d7-108">Välj Sedan Konto under kundens namn i det vänstra **sidofältet.**</span><span class="sxs-lookup"><span data-stu-id="b72d7-108">Then, under the customer's name in the left sidebar, select **Account**.</span></span> <span data-ttu-id="b72d7-109">Faktureringsprofilen finns under **rubriken Faktureringsinformation.**</span><span class="sxs-lookup"><span data-stu-id="b72d7-109">The billing profile can be found under the **Bill-to info** heading.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b72d7-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="b72d7-110">Prerequisites</span></span>

- <span data-ttu-id="b72d7-111">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b72d7-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b72d7-112">Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="b72d7-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="b72d7-113">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b72d7-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="b72d7-114">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="b72d7-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="b72d7-115">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="b72d7-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="b72d7-116">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="b72d7-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="b72d7-117">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="b72d7-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="b72d7-118">Microsoft-ID:t är samma som kund-ID :t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b72d7-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="b72d7-119">C\#</span><span class="sxs-lookup"><span data-stu-id="b72d7-119">C\#</span></span>

<span data-ttu-id="b72d7-120">Om du vill hämta en kunds faktureringsprofil använder du [**samlingen IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) och [**anropar metoden ById().**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)</span><span class="sxs-lookup"><span data-stu-id="b72d7-120">To get a customer's billing profile, use your [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="b72d7-121">Anropa sedan egenskapen [**Profiler**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) följt av [**egenskapen**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing) Fakturering.</span><span class="sxs-lookup"><span data-stu-id="b72d7-121">Then call the [**Profiles**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) property, followed by the [**Billing**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing) property.</span></span> <span data-ttu-id="b72d7-122">Anropa slutligen metoderna [**Get()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) eller [**GetAsync().**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync)</span><span class="sxs-lookup"><span data-stu-id="b72d7-122">Finally, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;

var billingProfile = partnerOperations.Customers.ById(selectedCustomerId).Profiles.Billing.Get();
```

<span data-ttu-id="b72d7-123">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="b72d7-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="b72d7-124">**Project:** PartnerSDK.FeatureSamples-klass: GetCustomerBillingProfile.cs </span><span class="sxs-lookup"><span data-stu-id="b72d7-124">**Project**: PartnerSDK.FeatureSamples **Class**: GetCustomerBillingProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="b72d7-125">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="b72d7-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b72d7-126">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="b72d7-126">Request syntax</span></span>

| <span data-ttu-id="b72d7-127">Metod</span><span class="sxs-lookup"><span data-stu-id="b72d7-127">Method</span></span>  | <span data-ttu-id="b72d7-128">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="b72d7-128">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b72d7-129">**Få**</span><span class="sxs-lookup"><span data-stu-id="b72d7-129">**GET**</span></span> | <span data-ttu-id="b72d7-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/profiles/billing HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="b72d7-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/profiles/billing HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="b72d7-131">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="b72d7-131">URI parameter</span></span>

<span data-ttu-id="b72d7-132">Använd följande frågeparameter för att hämta faktureringsprofilen.</span><span class="sxs-lookup"><span data-stu-id="b72d7-132">Use the following query parameter to get the billing profile.</span></span>

| <span data-ttu-id="b72d7-133">Namn</span><span class="sxs-lookup"><span data-stu-id="b72d7-133">Name</span></span>                   | <span data-ttu-id="b72d7-134">Typ</span><span class="sxs-lookup"><span data-stu-id="b72d7-134">Type</span></span>     | <span data-ttu-id="b72d7-135">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="b72d7-135">Required</span></span> | <span data-ttu-id="b72d7-136">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="b72d7-136">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b72d7-137">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="b72d7-137">**customer-tenant-id**</span></span> | <span data-ttu-id="b72d7-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="b72d7-138">**guid**</span></span> | <span data-ttu-id="b72d7-139">Y</span><span class="sxs-lookup"><span data-stu-id="b72d7-139">Y</span></span>        | <span data-ttu-id="b72d7-140">Värdet är ett GUID-formaterat **kundklient-ID** som gör att återförsäljaren kan filtrera resultaten för en viss kund som tillhör återförsäljaren.</span><span class="sxs-lookup"><span data-stu-id="b72d7-140">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b72d7-141">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="b72d7-141">Request headers</span></span>

<span data-ttu-id="b72d7-142">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="b72d7-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b72d7-143">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="b72d7-143">Request body</span></span>

<span data-ttu-id="b72d7-144">Ingen</span><span class="sxs-lookup"><span data-stu-id="b72d7-144">None</span></span>

### <a name="request-example"></a><span data-ttu-id="b72d7-145">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="b72d7-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/profiles/billing HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a5581a74-2778-4e34-9172-18baa4877081
MS-CorrelationId: 51d521b3-62db-4682-b75d-fb8ab09113b2
```

## <a name="rest-response"></a><span data-ttu-id="b72d7-146">REST-svar</span><span class="sxs-lookup"><span data-stu-id="b72d7-146">REST response</span></span>

<span data-ttu-id="b72d7-147">Om det lyckas returnerar den här metoden en samling [profilresurser](profile-resources.md) i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="b72d7-147">If successful, this method returns a collection of [Profile](profile-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b72d7-148">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="b72d7-148">Response success and error codes</span></span>

<span data-ttu-id="b72d7-149">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="b72d7-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b72d7-150">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="b72d7-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b72d7-151">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="b72d7-151">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b72d7-152">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="b72d7-152">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1206
Content-Type: application/json
MS-CorrelationId: 51d521b3-62db-4682-b75d-fb8ab09113b2
MS-RequestId: a5581a74-2778-4e34-9172-18baa4877081
Date: Mon, 23 Nov 2015 18:13:43 GMT

{
    "id": "<billing-profile-id>",
    "firstName": "FirstName",
    "lastName": "LastName",
    "email": "email@sample.com",
    "culture": "en-US",
    "language": "en",
    "companyName": "CompanyName",
    "defaultAddress": {
        "country": "US",
        "city": "Redmond",
        "state": "WA",
        "addressLine1": "1 Microsoft Way",
        "postalCode": "98052",
        "firstName": "FirstName",
        "lastName": "LastName",
        "phoneNumber": "4255555555"
    },
    "links": {
        "self": {
            "uri": "/v1/customers/<customer-tenant-id>/profiles/billing",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "etag": "<etag>",
        "objectType": "CustomerBillingProfile"
    }
}
```
