---
title: Hämta en kunds faktureringsprofil
description: Hämtar en kunds fakturerings profil. På instrument panelen för partner Center kan du utföra den här åtgärden genom att först välja en kund.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 6c837c1c220e334df82e75eb680b6012862c9686
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769732"
---
# <a name="get-a-customers-billing-profile"></a><span data-ttu-id="191ec-103">Hämta en kunds faktureringsprofil</span><span class="sxs-lookup"><span data-stu-id="191ec-103">Get a customer's billing profile</span></span>

<span data-ttu-id="191ec-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="191ec-104">**Applies To**</span></span>

- <span data-ttu-id="191ec-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="191ec-105">Partner Center</span></span>
- <span data-ttu-id="191ec-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="191ec-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="191ec-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="191ec-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="191ec-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="191ec-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="191ec-109">Hämtar en kunds fakturerings profil.</span><span class="sxs-lookup"><span data-stu-id="191ec-109">Gets the billing profile of a customer.</span></span>

<span data-ttu-id="191ec-110">På instrument panelen för partner Center kan du utföra den här åtgärden genom [att först välja en kund](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="191ec-110">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="191ec-111">Välj sedan **konto** under kundens namn i den vänstra sid panelen.</span><span class="sxs-lookup"><span data-stu-id="191ec-111">Then, under the customer's name in the left sidebar, select **Account**.</span></span> <span data-ttu-id="191ec-112">Du hittar fakturerings profilen under rubriken **fakturerings information** .</span><span class="sxs-lookup"><span data-stu-id="191ec-112">The billing profile can be found under the **Bill-to info** heading.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="191ec-113">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="191ec-113">Prerequisites</span></span>

- <span data-ttu-id="191ec-114">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="191ec-114">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="191ec-115">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="191ec-115">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="191ec-116">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="191ec-116">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="191ec-117">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="191ec-117">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="191ec-118">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="191ec-118">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="191ec-119">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="191ec-119">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="191ec-120">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="191ec-120">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="191ec-121">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="191ec-121">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="191ec-122">C\#</span><span class="sxs-lookup"><span data-stu-id="191ec-122">C\#</span></span>

<span data-ttu-id="191ec-123">Om du vill hämta en kunds fakturerings profil använder du din [**IPartner.-kund**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) samling och anropar metoden [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="191ec-123">To get a customer's billing profile, use your [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="191ec-124">Anropa sedan [**profil**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) egenskapen följt av [**fakturerings**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing) egenskapen.</span><span class="sxs-lookup"><span data-stu-id="191ec-124">Then call the [**Profiles**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) property, followed by the [**Billing**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing) property.</span></span> <span data-ttu-id="191ec-125">Anropa slutligen metoderna [**Get ()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) eller [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync) .</span><span class="sxs-lookup"><span data-stu-id="191ec-125">Finally, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;

var billingProfile = partnerOperations.Customers.ById(selectedCustomerId).Profiles.Billing.Get();
```

<span data-ttu-id="191ec-126">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="191ec-126">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="191ec-127">**Projekt**: PartnerSDK. FeatureSamples- **klass**: GetCustomerBillingProfile.CS</span><span class="sxs-lookup"><span data-stu-id="191ec-127">**Project**: PartnerSDK.FeatureSamples **Class**: GetCustomerBillingProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="191ec-128">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="191ec-128">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="191ec-129">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="191ec-129">Request syntax</span></span>

| <span data-ttu-id="191ec-130">Metod</span><span class="sxs-lookup"><span data-stu-id="191ec-130">Method</span></span>  | <span data-ttu-id="191ec-131">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="191ec-131">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="191ec-132">**TA**</span><span class="sxs-lookup"><span data-stu-id="191ec-132">**GET**</span></span> | <span data-ttu-id="191ec-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Profiles/Billing http/1.1</span><span class="sxs-lookup"><span data-stu-id="191ec-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/profiles/billing HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="191ec-134">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="191ec-134">URI parameter</span></span>

<span data-ttu-id="191ec-135">Använd följande frågeparameter för att hämta fakturerings profilen.</span><span class="sxs-lookup"><span data-stu-id="191ec-135">Use the following query parameter to get the billing profile.</span></span>

| <span data-ttu-id="191ec-136">Namn</span><span class="sxs-lookup"><span data-stu-id="191ec-136">Name</span></span>                   | <span data-ttu-id="191ec-137">Typ</span><span class="sxs-lookup"><span data-stu-id="191ec-137">Type</span></span>     | <span data-ttu-id="191ec-138">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="191ec-138">Required</span></span> | <span data-ttu-id="191ec-139">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="191ec-139">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="191ec-140">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="191ec-140">**customer-tenant-id**</span></span> | <span data-ttu-id="191ec-141">**guid**</span><span class="sxs-lookup"><span data-stu-id="191ec-141">**guid**</span></span> | <span data-ttu-id="191ec-142">Y</span><span class="sxs-lookup"><span data-stu-id="191ec-142">Y</span></span>        | <span data-ttu-id="191ec-143">Värdet är ett GUID-formaterat **kund-Tenant-ID** som gör det möjligt för åter försäljaren att filtrera resultaten för en specifik kund som tillhör åter försäljaren.</span><span class="sxs-lookup"><span data-stu-id="191ec-143">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="191ec-144">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="191ec-144">Request headers</span></span>

<span data-ttu-id="191ec-145">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="191ec-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="191ec-146">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="191ec-146">Request body</span></span>

<span data-ttu-id="191ec-147">Inget</span><span class="sxs-lookup"><span data-stu-id="191ec-147">None</span></span>

### <a name="request-example"></a><span data-ttu-id="191ec-148">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="191ec-148">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/profiles/billing HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a5581a74-2778-4e34-9172-18baa4877081
MS-CorrelationId: 51d521b3-62db-4682-b75d-fb8ab09113b2
```

## <a name="rest-response"></a><span data-ttu-id="191ec-149">REST-svar</span><span class="sxs-lookup"><span data-stu-id="191ec-149">REST response</span></span>

<span data-ttu-id="191ec-150">Om det lyckas returnerar den här metoden en samling [profil](profile-resources.md) resurser i svars texten.</span><span class="sxs-lookup"><span data-stu-id="191ec-150">If successful, this method returns a collection of [Profile](profile-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="191ec-151">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="191ec-151">Response success and error codes</span></span>

<span data-ttu-id="191ec-152">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="191ec-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="191ec-153">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="191ec-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="191ec-154">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="191ec-154">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="191ec-155">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="191ec-155">Response example</span></span>

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
