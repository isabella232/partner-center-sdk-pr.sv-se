---
title: Uppdatera en kunds faktureringsprofil
description: Uppdaterar en kunds fakturerings profil, inklusive adressen som är kopplad till profilen.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: adf4e3de9941fded632e0561624d91d854c5aa24
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769777"
---
# <a name="update-a-customers-billing-profile"></a><span data-ttu-id="8f540-103">Uppdatera en kunds faktureringsprofil</span><span class="sxs-lookup"><span data-stu-id="8f540-103">Update a customer's billing profile</span></span>

<span data-ttu-id="8f540-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="8f540-104">**Applies To**</span></span>

- <span data-ttu-id="8f540-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="8f540-105">Partner Center</span></span>
- <span data-ttu-id="8f540-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="8f540-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="8f540-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="8f540-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="8f540-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="8f540-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="8f540-109">Uppdaterar en kunds fakturerings profil, inklusive adressen som är kopplad till profilen.</span><span class="sxs-lookup"><span data-stu-id="8f540-109">Updates a customer's billing profile, including the address associated with the profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f540-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="8f540-110">Prerequisites</span></span>

- <span data-ttu-id="8f540-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="8f540-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8f540-112">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="8f540-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="8f540-113">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8f540-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="8f540-114">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="8f540-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="8f540-115">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="8f540-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="8f540-116">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="8f540-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="8f540-117">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="8f540-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="8f540-118">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8f540-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="8f540-119">C\#</span><span class="sxs-lookup"><span data-stu-id="8f540-119">C\#</span></span>

<span data-ttu-id="8f540-120">Om du vill uppdatera en kunds fakturerings profil hämtar du fakturerings profilen och uppdaterar egenskaperna vid behov.</span><span class="sxs-lookup"><span data-stu-id="8f540-120">To update a customer's billing profile, retrieve the billing profile and update the properties as necessary.</span></span> <span data-ttu-id="8f540-121">Hämta sedan din [**IPartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) -samling och anropa sedan metoden [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="8f540-121">Then, retrieve your [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection, and then call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="8f540-122">Anropa sedan [**profil**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) egenskapen följt av [**fakturerings**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing) egenskapen.</span><span class="sxs-lookup"><span data-stu-id="8f540-122">Then call the [**Profiles**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) property, followed by the [**Billing**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing) property.</span></span> <span data-ttu-id="8f540-123">Sedan avslutar du genom att anropa metoderna [**Update ()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofile-1.update) eller [**UpdateAsync ()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofile-1.updateasync) .</span><span class="sxs-lookup"><span data-stu-id="8f540-123">Then, finish by calling the [**Update()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofile-1.update) or [**UpdateAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofile-1.updateasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;

var billingProfile = partnerOperations.Customers.ById(selectedCustomerId).Profiles.Billing.Get();

// Apply changes to profile;

billingProfile = partnerOperations.Customers.ById(selectedCustomerId).Profiles.Billing.Update(billingProfile);
```

<span data-ttu-id="8f540-124">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="8f540-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="8f540-125">**Projekt**: PartnerSDK. FeatureSamples- **klass**: UpdateCustomerBillingProfile.CS</span><span class="sxs-lookup"><span data-stu-id="8f540-125">**Project**: PartnerSDK.FeatureSamples **Class**: UpdateCustomerBillingProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="8f540-126">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="8f540-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8f540-127">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="8f540-127">Request syntax</span></span>

| <span data-ttu-id="8f540-128">Metod</span><span class="sxs-lookup"><span data-stu-id="8f540-128">Method</span></span>  | <span data-ttu-id="8f540-129">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="8f540-129">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8f540-130">**PUT**</span><span class="sxs-lookup"><span data-stu-id="8f540-130">**PUT**</span></span> | <span data-ttu-id="8f540-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Profiles/Billing http/1.1</span><span class="sxs-lookup"><span data-stu-id="8f540-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/profiles/billing HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="8f540-132">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="8f540-132">URI parameter</span></span>

<span data-ttu-id="8f540-133">Använd följande frågeparameter för att uppdatera fakturerings profilen.</span><span class="sxs-lookup"><span data-stu-id="8f540-133">Use the following query parameter to update the billing profile.</span></span>

| <span data-ttu-id="8f540-134">Namn</span><span class="sxs-lookup"><span data-stu-id="8f540-134">Name</span></span>                   | <span data-ttu-id="8f540-135">Typ</span><span class="sxs-lookup"><span data-stu-id="8f540-135">Type</span></span>     | <span data-ttu-id="8f540-136">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="8f540-136">Required</span></span> | <span data-ttu-id="8f540-137">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="8f540-137">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8f540-138">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="8f540-138">**customer-tenant-id**</span></span> | <span data-ttu-id="8f540-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="8f540-139">**guid**</span></span> | <span data-ttu-id="8f540-140">Y</span><span class="sxs-lookup"><span data-stu-id="8f540-140">Y</span></span>        | <span data-ttu-id="8f540-141">Värdet är ett GUID-formaterat **kund-Tenant-ID** som gör det möjligt för åter försäljaren att filtrera resultaten för en specifik kund som tillhör åter försäljaren.</span><span class="sxs-lookup"><span data-stu-id="8f540-141">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="8f540-142">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="8f540-142">Request headers</span></span>

- <span data-ttu-id="8f540-143">**If-Match**: " &lt; etag &gt; " krävs för samtidig identifiering.</span><span class="sxs-lookup"><span data-stu-id="8f540-143">**If-Match**: "&lt;ETag&gt;" is required for concurrency detection.</span></span>
<span data-ttu-id="8f540-144">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="8f540-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8f540-145">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="8f540-145">Request body</span></span>

<span data-ttu-id="8f540-146">Den fullständiga resursen.</span><span class="sxs-lookup"><span data-stu-id="8f540-146">The full resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="8f540-147">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="8f540-147">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="8f540-148">REST-svar</span><span class="sxs-lookup"><span data-stu-id="8f540-148">REST response</span></span>

<span data-ttu-id="8f540-149">Om det lyckas returnerar den här metoden uppdaterade [profil](profile-resources.md) resurs egenskaper i svars texten.</span><span class="sxs-lookup"><span data-stu-id="8f540-149">If successful, this method returns updated [Profile](profile-resources.md) resource properties in the response body.</span></span> <span data-ttu-id="8f540-150">Det här anropet kräver en ETag för samtidig identifiering.</span><span class="sxs-lookup"><span data-stu-id="8f540-150">This call requires an ETag for concurrency detection.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8f540-151">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="8f540-151">Response success and error codes</span></span>

<span data-ttu-id="8f540-152">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="8f540-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8f540-153">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="8f540-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8f540-154">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="8f540-154">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="8f540-155">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="8f540-155">Response example</span></span>

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
