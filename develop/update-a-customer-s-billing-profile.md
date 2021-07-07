---
title: Uppdatera en kunds faktureringsprofil
description: Uppdaterar en kunds faktureringsprofil, inklusive den adress som är associerad med profilen.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: 1605c3e8cb050717209cb482d2299e2a42b9b186
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530046"
---
# <a name="update-a-customers-billing-profile"></a><span data-ttu-id="85004-103">Uppdatera en kunds faktureringsprofil</span><span class="sxs-lookup"><span data-stu-id="85004-103">Update a customer's billing profile</span></span>

<span data-ttu-id="85004-104">**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="85004-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="85004-105">Uppdaterar en kunds faktureringsprofil, inklusive den adress som är associerad med profilen.</span><span class="sxs-lookup"><span data-stu-id="85004-105">Updates a customer's billing profile, including the address associated with the profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="85004-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="85004-106">Prerequisites</span></span>

- <span data-ttu-id="85004-107">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="85004-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="85004-108">Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="85004-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="85004-109">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="85004-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="85004-110">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="85004-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="85004-111">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="85004-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="85004-112">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="85004-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="85004-113">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="85004-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="85004-114">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="85004-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="85004-115">C\#</span><span class="sxs-lookup"><span data-stu-id="85004-115">C\#</span></span>

<span data-ttu-id="85004-116">Om du vill uppdatera en kunds faktureringsprofil hämtar du faktureringsprofilen och uppdaterar egenskaperna efter behov.</span><span class="sxs-lookup"><span data-stu-id="85004-116">To update a customer's billing profile, retrieve the billing profile and update the properties as necessary.</span></span> <span data-ttu-id="85004-117">Hämta sedan samlingen [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) och anropa sedan [**metoden ById().**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)</span><span class="sxs-lookup"><span data-stu-id="85004-117">Then, retrieve your [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection, and then call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="85004-118">Anropa sedan egenskapen [**Profiler**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) följt av [**egenskapen**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing) Fakturering.</span><span class="sxs-lookup"><span data-stu-id="85004-118">Then call the [**Profiles**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) property, followed by the [**Billing**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing) property.</span></span> <span data-ttu-id="85004-119">Avsluta sedan genom att anropa [**metoderna Update()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofile-1.update) eller [**UpdateAsync().**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofile-1.updateasync)</span><span class="sxs-lookup"><span data-stu-id="85004-119">Then, finish by calling the [**Update()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofile-1.update) or [**UpdateAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofile-1.updateasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;

var billingProfile = partnerOperations.Customers.ById(selectedCustomerId).Profiles.Billing.Get();

// Apply changes to profile;

billingProfile = partnerOperations.Customers.ById(selectedCustomerId).Profiles.Billing.Update(billingProfile);
```

<span data-ttu-id="85004-120">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="85004-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="85004-121">**Project:** PartnerSDK.FeatureSamples-klass: UpdateCustomerBillingProfile.cs </span><span class="sxs-lookup"><span data-stu-id="85004-121">**Project**: PartnerSDK.FeatureSamples **Class**: UpdateCustomerBillingProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="85004-122">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="85004-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="85004-123">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="85004-123">Request syntax</span></span>

| <span data-ttu-id="85004-124">Metod</span><span class="sxs-lookup"><span data-stu-id="85004-124">Method</span></span>  | <span data-ttu-id="85004-125">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="85004-125">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="85004-126">**PUT**</span><span class="sxs-lookup"><span data-stu-id="85004-126">**PUT**</span></span> | <span data-ttu-id="85004-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/profiles/billing HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="85004-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/profiles/billing HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="85004-128">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="85004-128">URI parameter</span></span>

<span data-ttu-id="85004-129">Använd följande frågeparameter för att uppdatera faktureringsprofilen.</span><span class="sxs-lookup"><span data-stu-id="85004-129">Use the following query parameter to update the billing profile.</span></span>

| <span data-ttu-id="85004-130">Namn</span><span class="sxs-lookup"><span data-stu-id="85004-130">Name</span></span>                   | <span data-ttu-id="85004-131">Typ</span><span class="sxs-lookup"><span data-stu-id="85004-131">Type</span></span>     | <span data-ttu-id="85004-132">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="85004-132">Required</span></span> | <span data-ttu-id="85004-133">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="85004-133">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="85004-134">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="85004-134">**customer-tenant-id**</span></span> | <span data-ttu-id="85004-135">**guid**</span><span class="sxs-lookup"><span data-stu-id="85004-135">**guid**</span></span> | <span data-ttu-id="85004-136">Y</span><span class="sxs-lookup"><span data-stu-id="85004-136">Y</span></span>        | <span data-ttu-id="85004-137">Värdet är ett GUID-formaterat **kundklient-ID** som gör att återförsäljaren kan filtrera resultaten för en viss kund som tillhör återförsäljaren.</span><span class="sxs-lookup"><span data-stu-id="85004-137">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="85004-138">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="85004-138">Request headers</span></span>

- <span data-ttu-id="85004-139">**If-Match:**" &lt; ETag &gt; " krävs för samtidighetsidentifiering.</span><span class="sxs-lookup"><span data-stu-id="85004-139">**If-Match**: "&lt;ETag&gt;" is required for concurrency detection.</span></span>
<span data-ttu-id="85004-140">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="85004-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="85004-141">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="85004-141">Request body</span></span>

<span data-ttu-id="85004-142">Den fullständiga resursen.</span><span class="sxs-lookup"><span data-stu-id="85004-142">The full resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="85004-143">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="85004-143">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/profiles/billing HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ff85f13a-eb65-4b8e-9b67-05beb0565410
MS-CorrelationId: ff1b757d-cfaf-463a-b48b-0f96d05e95d7
Content-Type: application/json
Content-Length: 639
Expect: 100-continue

{
    "Id": "a58ceba5-60ac-48e4-a0bc-2a855811807a",
    "FirstName": "FirstName",
    "LastName": "LastName",
    "Email": "email@sample.com",
    "Culture": "en-US",
    "Language": "en",
    "CompanyName": "CompanyName",
    "DefaultAddress": {
        "Country": "US",
        "Region": null,
        "City": "Redmond",
        "State": "WA",
        "AddressLine1": "One Microsoft Way",
        "AddressLine2": null,
        "PostalCode": "98052",
        "FirstName": "FirstName",
        "LastName": "LastName",
        "PhoneNumber": "4255555555"
    },
    "Links": {
        "Self": {
            "Uri": "/v1/customers/<customer-tenant-id>/profiles/billing",
            "Method": "GET",
            "Headers": []
        }
    },
    "Attributes": {
        "Etag": "<etag>",
        "ObjectType": "CustomerBillingProfile"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="85004-144">REST-svar</span><span class="sxs-lookup"><span data-stu-id="85004-144">REST response</span></span>

<span data-ttu-id="85004-145">Om det lyckas returnerar den här metoden [uppdaterade profilresursegenskaper](profile-resources.md) i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="85004-145">If successful, this method returns updated [Profile](profile-resources.md) resource properties in the response body.</span></span> <span data-ttu-id="85004-146">Det här anropet kräver en ETag för samtidighetsidentifiering.</span><span class="sxs-lookup"><span data-stu-id="85004-146">This call requires an ETag for concurrency detection.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="85004-147">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="85004-147">Response success and error codes</span></span>

<span data-ttu-id="85004-148">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="85004-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="85004-149">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="85004-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="85004-150">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="85004-150">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="85004-151">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="85004-151">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1210
Content-Type: application/json
MS-CorrelationId: ff1b757d-cfaf-463a-b48b-0f96d05e95d7
MS-RequestId: ff85f13a-eb65-4b8e-9b67-05beb0565410
Date: Mon, 23 Nov 2015 18:20:43 GMT

{
    "id": "a58ceba5-60ac-48e4-a0bc-2a855811807a",
    "firstName": "FirstName",
    "lastName": "LastName",
    "email": "email@sample.com",
    "culture": "en-US",
    "language": "en",
    "companyName": "companyName",
    "defaultAddress": {
        "country": "US",
        "city": "Redmond",
        "state": "WA",
        "addressLine1": "One Microsoft Way",
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
