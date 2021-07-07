---
title: Skapa en ny kundkonfigurationsprincip
description: Lär dig hur du använder Partner Center-API:er för att skapa en ny konfigurationsprincip för en angiven kund. Artikeln innehåller krav, steg och exempel.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 530ff72862204bda093385252450f4eb81b63160
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973681"
---
# <a name="create-a-new-configuration-policy-for-the-specified-customer"></a><span data-ttu-id="3e086-104">Skapa en ny konfigurationsprincip för den angivna kunden</span><span class="sxs-lookup"><span data-stu-id="3e086-104">Create a new configuration policy for the specified customer</span></span>

<span data-ttu-id="3e086-105">**Gäller för:** Partner Center-| Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="3e086-105">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="3e086-106">Så här skapar du en ny konfigurationsprincip för den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="3e086-106">How to create a new configuration policy for the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e086-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="3e086-107">Prerequisites</span></span>

- <span data-ttu-id="3e086-108">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="3e086-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3e086-109">Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="3e086-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="3e086-110">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3e086-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="3e086-111">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="3e086-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="3e086-112">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="3e086-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="3e086-113">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="3e086-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="3e086-114">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="3e086-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="3e086-115">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3e086-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="3e086-116">C\#</span><span class="sxs-lookup"><span data-stu-id="3e086-116">C\#</span></span>

<span data-ttu-id="3e086-117">Så här skapar du en ny konfigurationsprincip för den angivna kunden:</span><span class="sxs-lookup"><span data-stu-id="3e086-117">To create a new configuration policy for the specified customer:</span></span>

1. <span data-ttu-id="3e086-118">Skapa en instans av [**ett nytt ConfigurationPolicy-objekt**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) enligt följande kodfragment.</span><span class="sxs-lookup"><span data-stu-id="3e086-118">Instantiate a new [**ConfigurationPolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) object as shown in the following code snippet.</span></span> <span data-ttu-id="3e086-119">Anropa sedan [**metoden IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att hämta ett gränssnitt till åtgärder på den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="3e086-119">Then call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span>

2. <span data-ttu-id="3e086-120">Hämta egenskapen [**ConfigurationPolicies för**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) att hämta ett gränssnitt till konfigurationsprincipinsamlingsåtgärder.</span><span class="sxs-lookup"><span data-stu-id="3e086-120">Retrieve the [**ConfigurationPolicies**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) property to get an interface to configuration policy collection operations.</span></span>

3. <span data-ttu-id="3e086-121">Anropa metoden [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) eller [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) för att skapa konfigurationsprincipen.</span><span class="sxs-lookup"><span data-stu-id="3e086-121">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) method to create the configuration policy.</span></span>

### <a name="c-example"></a><span data-ttu-id="3e086-122">\#C-exempel</span><span class="sxs-lookup"><span data-stu-id="3e086-122">C\# example</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var configurationPolicyToCreate = new ConfigurationPolicy
{
    Name = "Test Config Policy",
    Description = "This configuration policy is created by the SDK samples",
    PolicySettings = new List<PolicySettingsType>() {
        PolicySettingsType.OobeUserNotLocalAdmin,
        PolicySettingsType.SkipEula }
};

var createdConfigurationPolicy =
    partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.Create(configurationPolicyToCreate);
```

<span data-ttu-id="3e086-123">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="3e086-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="3e086-124">**Project:** **Partnercenter-SDK-exempelklass:** CreateConfigurationPolicy.cs</span><span class="sxs-lookup"><span data-stu-id="3e086-124">**Project**: Partner Center SDK Samples **Class**: CreateConfigurationPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="3e086-125">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="3e086-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3e086-126">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="3e086-126">Request syntax</span></span>

| <span data-ttu-id="3e086-127">Metod</span><span class="sxs-lookup"><span data-stu-id="3e086-127">Method</span></span>   | <span data-ttu-id="3e086-128">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="3e086-128">Request URI</span></span>                                                                              |
|----------|------------------------------------------------------------------------------------------|
| <span data-ttu-id="3e086-129">**Inlägg**</span><span class="sxs-lookup"><span data-stu-id="3e086-129">**POST**</span></span> | <span data-ttu-id="3e086-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="3e086-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="3e086-131">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="3e086-131">URI parameter</span></span>

<span data-ttu-id="3e086-132">Använd följande sökvägsparametrar när du skapar begäran.</span><span class="sxs-lookup"><span data-stu-id="3e086-132">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="3e086-133">Namn</span><span class="sxs-lookup"><span data-stu-id="3e086-133">Name</span></span>        | <span data-ttu-id="3e086-134">Typ</span><span class="sxs-lookup"><span data-stu-id="3e086-134">Type</span></span>   | <span data-ttu-id="3e086-135">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="3e086-135">Required</span></span> | <span data-ttu-id="3e086-136">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="3e086-136">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="3e086-137">kund-ID</span><span class="sxs-lookup"><span data-stu-id="3e086-137">customer-id</span></span> | <span data-ttu-id="3e086-138">sträng</span><span class="sxs-lookup"><span data-stu-id="3e086-138">string</span></span> | <span data-ttu-id="3e086-139">Ja</span><span class="sxs-lookup"><span data-stu-id="3e086-139">Yes</span></span>      | <span data-ttu-id="3e086-140">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="3e086-140">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="3e086-141">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="3e086-141">Request headers</span></span>

<span data-ttu-id="3e086-142">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="3e086-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3e086-143">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="3e086-143">Request body</span></span>

<span data-ttu-id="3e086-144">Begärandetexten måste innehålla ett -objekt med konfigurationsprincipens information enligt beskrivningen i följande tabell:</span><span class="sxs-lookup"><span data-stu-id="3e086-144">The request body must contain an object with the configuration policy information as described in the following table:</span></span>

| <span data-ttu-id="3e086-145">Namn</span><span class="sxs-lookup"><span data-stu-id="3e086-145">Name</span></span>           | <span data-ttu-id="3e086-146">Typ</span><span class="sxs-lookup"><span data-stu-id="3e086-146">Type</span></span>             | <span data-ttu-id="3e086-147">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="3e086-147">Required</span></span> | <span data-ttu-id="3e086-148">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="3e086-148">Description</span></span>                      |
|----------------|------------------|----------|----------------------------------|
| <span data-ttu-id="3e086-149">name</span><span class="sxs-lookup"><span data-stu-id="3e086-149">name</span></span>           | <span data-ttu-id="3e086-150">sträng</span><span class="sxs-lookup"><span data-stu-id="3e086-150">string</span></span>           | <span data-ttu-id="3e086-151">Ja</span><span class="sxs-lookup"><span data-stu-id="3e086-151">Yes</span></span>      | <span data-ttu-id="3e086-152">Principens egna namn.</span><span class="sxs-lookup"><span data-stu-id="3e086-152">The friendly name of the policy.</span></span> |
| <span data-ttu-id="3e086-153">category</span><span class="sxs-lookup"><span data-stu-id="3e086-153">category</span></span>       | <span data-ttu-id="3e086-154">sträng</span><span class="sxs-lookup"><span data-stu-id="3e086-154">string</span></span>           | <span data-ttu-id="3e086-155">Ja</span><span class="sxs-lookup"><span data-stu-id="3e086-155">Yes</span></span>      | <span data-ttu-id="3e086-156">Principkategorin.</span><span class="sxs-lookup"><span data-stu-id="3e086-156">The policy category.</span></span>             |
| <span data-ttu-id="3e086-157">beskrivning</span><span class="sxs-lookup"><span data-stu-id="3e086-157">description</span></span>    | <span data-ttu-id="3e086-158">sträng</span><span class="sxs-lookup"><span data-stu-id="3e086-158">string</span></span>           | <span data-ttu-id="3e086-159">No</span><span class="sxs-lookup"><span data-stu-id="3e086-159">No</span></span>       | <span data-ttu-id="3e086-160">Principbeskrivningen.</span><span class="sxs-lookup"><span data-stu-id="3e086-160">The policy description.</span></span>          |
| <span data-ttu-id="3e086-161">policySettings</span><span class="sxs-lookup"><span data-stu-id="3e086-161">policySettings</span></span> | <span data-ttu-id="3e086-162">matris med strängar</span><span class="sxs-lookup"><span data-stu-id="3e086-162">array of strings</span></span> | <span data-ttu-id="3e086-163">Ja</span><span class="sxs-lookup"><span data-stu-id="3e086-163">Yes</span></span>      | <span data-ttu-id="3e086-164">Principinställningarna.</span><span class="sxs-lookup"><span data-stu-id="3e086-164">The policy settings.</span></span>             |

### <a name="request-example"></a><span data-ttu-id="3e086-165">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="3e086-165">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com//v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 212
Content-Type: application/json
Host: api.partnercenter.microsoft.com

{
    "name": "Windows 10 Enterprise E5",
    "category": "o_o_b_e",
    "description": "test policy creation from API",
    "policySettings": ["oobe_user_not_local_admin", "skip_express_settings"]
}
```

## <a name="rest-response"></a><span data-ttu-id="3e086-166">REST-svar</span><span class="sxs-lookup"><span data-stu-id="3e086-166">REST response</span></span>

<span data-ttu-id="3e086-167">Om det lyckas innehåller svarstexten [ConfigurationPolicy-resursen](device-deployment-resources.md#configurationpolicy) för den nya principen.</span><span class="sxs-lookup"><span data-stu-id="3e086-167">If successful, the response body contains the [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resource for the new policy.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3e086-168">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="3e086-168">Response success and error codes</span></span>

<span data-ttu-id="3e086-169">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="3e086-169">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3e086-170">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="3e086-170">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3e086-171">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="3e086-171">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="3e086-172">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="3e086-172">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 404
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4beda413-74fc-4839-b74f-f580c353ab45
MS-RequestId: 0dfadf74-aa66-49ed-9a67-b3b78d9297cc
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:07:36 GMT

{
    "id": "40cdb858-edcc-44d7-9083-d6a36d43bd3f",
    "name": "Windows 10 Enterprise E5",
    "category": "o_o_b_e",
    "description": "test policy creation from API",
    "devicesAssigned": 0,
    "policySettings": ["oobe_user_not_local_admin", "skip_express_settings"],
    "createdDate": "2017-07-25T18:07:36",
    "lastModifiedDate": "2017-07-25T18:07:36",
    "attributes": {
        "objectType": "ConfigurationPolicy"
    }
}
```
