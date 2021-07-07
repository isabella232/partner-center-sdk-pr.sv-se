---
title: Hämta en kunds konfigurationsprincip
description: Så här hämtar du den angivna konfigurationsprincipen för den angivna kunden.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f9a8cb435c63d8d02c3b4633abc8723353116f37
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547503"
---
# <a name="retrieve-a-customers-configuration-policy"></a><span data-ttu-id="e4a4f-103">Hämta en kunds konfigurationsprincip</span><span class="sxs-lookup"><span data-stu-id="e4a4f-103">Retrieve a customer's configuration policy</span></span>

<span data-ttu-id="e4a4f-104">**Gäller för**: Partner Center-| Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="e4a4f-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="e4a4f-105">Så här hämtar du den angivna konfigurationsprincipen för den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="e4a4f-105">How to retrieve the specified configuration policy for the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e4a4f-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="e4a4f-106">Prerequisites</span></span>

- <span data-ttu-id="e4a4f-107">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e4a4f-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e4a4f-108">Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="e4a4f-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="e4a4f-109">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e4a4f-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="e4a4f-110">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="e4a4f-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="e4a4f-111">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="e4a4f-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="e4a4f-112">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="e4a4f-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="e4a4f-113">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="e4a4f-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="e4a4f-114">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e4a4f-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="e4a4f-115">Principidentifieraren.</span><span class="sxs-lookup"><span data-stu-id="e4a4f-115">The policy identifier.</span></span>

## <a name="c"></a><span data-ttu-id="e4a4f-116">C\#</span><span class="sxs-lookup"><span data-stu-id="e4a4f-116">C\#</span></span>

<span data-ttu-id="e4a4f-117">Om du vill hämta en konfigurationsprincip för den angivna kunden anropar du först [**metoden IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att hämta ett gränssnitt till åtgärder på den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="e4a4f-117">To retrieve a configuration policy for the specified customer, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="e4a4f-118">Anropa sedan metoden [**ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) med princip-ID:t för att hämta ett gränssnitt för konfigurationsprincipåtgärder för den angivna principen.</span><span class="sxs-lookup"><span data-stu-id="e4a4f-118">Next, call the [**ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) method with the policy ID to retrieve an interface to configuration policy operations for the specified policy.</span></span> <span data-ttu-id="e4a4f-119">Anropa slutligen metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.getasync) för att hämta konfigurationsprincipen.</span><span class="sxs-lookup"><span data-stu-id="e4a4f-119">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.getasync) method to retrieve the configuration policy.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedConfigurationPolicyId;

ConfigurationPolicy retrievedConfigurationPolicy =
    partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.ById(selectedConfigurationPolicyId).Get();
```

<span data-ttu-id="e4a4f-120">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="e4a4f-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="e4a4f-121">**Project:** Partnercenter-SDK **Samples-klass:** GetConfigurationPolicy.cs</span><span class="sxs-lookup"><span data-stu-id="e4a4f-121">**Project**: Partner Center SDK Samples **Class**: GetConfigurationPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="e4a4f-122">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="e4a4f-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e4a4f-123">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="e4a4f-123">Request syntax</span></span>

| <span data-ttu-id="e4a4f-124">Metod</span><span class="sxs-lookup"><span data-stu-id="e4a4f-124">Method</span></span>  | <span data-ttu-id="e4a4f-125">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="e4a4f-125">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e4a4f-126">**Få**</span><span class="sxs-lookup"><span data-stu-id="e4a4f-126">**GET**</span></span> | <span data-ttu-id="e4a4f-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies/{policy-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e4a4f-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies/{policy-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="e4a4f-128">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="e4a4f-128">URI parameter</span></span>

<span data-ttu-id="e4a4f-129">Använd följande sökväg och frågeparametrar när du skapar begäran.</span><span class="sxs-lookup"><span data-stu-id="e4a4f-129">Use the following path and query parameters when creating the request.</span></span>

| <span data-ttu-id="e4a4f-130">Namn</span><span class="sxs-lookup"><span data-stu-id="e4a4f-130">Name</span></span>        | <span data-ttu-id="e4a4f-131">Typ</span><span class="sxs-lookup"><span data-stu-id="e4a4f-131">Type</span></span>   | <span data-ttu-id="e4a4f-132">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="e4a4f-132">Required</span></span> | <span data-ttu-id="e4a4f-133">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="e4a4f-133">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="e4a4f-134">kund-id</span><span class="sxs-lookup"><span data-stu-id="e4a4f-134">customer-id</span></span> | <span data-ttu-id="e4a4f-135">sträng</span><span class="sxs-lookup"><span data-stu-id="e4a4f-135">string</span></span> | <span data-ttu-id="e4a4f-136">Ja</span><span class="sxs-lookup"><span data-stu-id="e4a4f-136">Yes</span></span>      | <span data-ttu-id="e4a4f-137">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="e4a4f-137">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="e4a4f-138">policy-id</span><span class="sxs-lookup"><span data-stu-id="e4a4f-138">policy-id</span></span>   | <span data-ttu-id="e4a4f-139">sträng</span><span class="sxs-lookup"><span data-stu-id="e4a4f-139">string</span></span> | <span data-ttu-id="e4a4f-140">Ja</span><span class="sxs-lookup"><span data-stu-id="e4a4f-140">Yes</span></span>      | <span data-ttu-id="e4a4f-141">En GUID-formaterad sträng som identifierar principen.</span><span class="sxs-lookup"><span data-stu-id="e4a4f-141">A GUID-formatted string that identifies the policy.</span></span>   |

### <a name="request-headers"></a><span data-ttu-id="e4a4f-142">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="e4a4f-142">Request headers</span></span>

<span data-ttu-id="e4a4f-143">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="e4a4f-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e4a4f-144">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="e4a4f-144">Request body</span></span>

<span data-ttu-id="e4a4f-145">Ingen</span><span class="sxs-lookup"><span data-stu-id="e4a4f-145">None</span></span>

### <a name="request-example"></a><span data-ttu-id="e4a4f-146">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="e4a4f-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies/56edf752-ee77-4fd8-b7f5-df1f74a3a9ac HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 0
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="e4a4f-147">REST-svar</span><span class="sxs-lookup"><span data-stu-id="e4a4f-147">REST response</span></span>

<span data-ttu-id="e4a4f-148">Om det lyckas innehåller svaret den begärda [ConfigurationPolicy-resursen.](device-deployment-resources.md#configurationpolicy)</span><span class="sxs-lookup"><span data-stu-id="e4a4f-148">If successful, the response contains the requested [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e4a4f-149">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="e4a4f-149">Response success and error codes</span></span>

<span data-ttu-id="e4a4f-150">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="e4a4f-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e4a4f-151">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="e4a4f-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e4a4f-152">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="e4a4f-152">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e4a4f-153">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="e4a4f-153">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 443
MS-CorrelationId: abe150cf-c677-435c-b5d5-b34899a6d1ec
MS-RequestId: ab3abfe7-dce7-46c0-ab20-4fd49bc3e2f7
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:08:27 GMT

{
    "id": "56edf752-ee77-4fd8-b7f5-df1f74a3a9ac",
    "name": "Test policy",
    "category": "o_o_b_e",
    "description": "Test policy creation from API 1",
    "devicesAssigned": 0,
    "policySettings": ["skip_express_settings"],
    "createdDate": "2017-07-25T11:03:03.8457116-07:00",
    "lastModifiedDate": "2017-07-25T11:04:00.8149974-07:00",
    "attributes": {
        "objectType": "ConfigurationPolicy"
    }
}
```
