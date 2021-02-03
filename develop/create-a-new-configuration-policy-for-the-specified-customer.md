---
title: Skapa en ny kund konfigurations princip
description: 'Lär dig hur du använder API: er för partner Center för att skapa en ny konfigurations princip för en angiven kund. Artikeln innehåller krav, steg och exempel.'
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 21a0bfde7f931371ff09d6c27de0281a4ed3b3cb
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770166"
---
# <a name="create-a-new-configuration-policy-for-the-specified-customer"></a><span data-ttu-id="03915-104">Skapa en ny konfigurationsprincip för den angivna kunden</span><span class="sxs-lookup"><span data-stu-id="03915-104">Create a new configuration policy for the specified customer</span></span>

<span data-ttu-id="03915-105">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="03915-105">**Applies to:**</span></span>

- <span data-ttu-id="03915-106">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="03915-106">Partner Center</span></span>
- <span data-ttu-id="03915-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="03915-107">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="03915-108">Så här skapar du en ny konfigurations princip för den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="03915-108">How to create a new configuration policy for the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="03915-109">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="03915-109">Prerequisites</span></span>

- <span data-ttu-id="03915-110">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="03915-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="03915-111">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="03915-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="03915-112">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="03915-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="03915-113">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="03915-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="03915-114">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="03915-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="03915-115">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="03915-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="03915-116">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="03915-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="03915-117">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="03915-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="03915-118">C\#</span><span class="sxs-lookup"><span data-stu-id="03915-118">C\#</span></span>

<span data-ttu-id="03915-119">Så här skapar du en ny konfigurations princip för den angivna kunden:</span><span class="sxs-lookup"><span data-stu-id="03915-119">To create a new configuration policy for the specified customer:</span></span>

1. <span data-ttu-id="03915-120">Instansiera ett nytt [**ConfigurationPolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) -objekt som det visas i följande kodfragment.</span><span class="sxs-lookup"><span data-stu-id="03915-120">Instantiate a new [**ConfigurationPolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) object as shown in the following code snippet.</span></span> <span data-ttu-id="03915-121">Anropa sedan metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID för att hämta ett gränssnitt till åtgärder på den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="03915-121">Then call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span>

2. <span data-ttu-id="03915-122">Hämta egenskapen [**ConfigurationPolicies**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) för att hämta ett gränssnitt för konfiguration av princip insamlings åtgärder.</span><span class="sxs-lookup"><span data-stu-id="03915-122">Retrieve the [**ConfigurationPolicies**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) property to get an interface to configuration policy collection operations.</span></span>

3. <span data-ttu-id="03915-123">Anropa [**create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) -eller [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) -metoden för att skapa konfigurations principen.</span><span class="sxs-lookup"><span data-stu-id="03915-123">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) method to create the configuration policy.</span></span>

### <a name="c-example"></a><span data-ttu-id="03915-124">C- \# exempel</span><span class="sxs-lookup"><span data-stu-id="03915-124">C\# example</span></span>

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

<span data-ttu-id="03915-125">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="03915-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="03915-126">**Projekt**: Partner Center SDK-exempel **klass**: CreateConfigurationPolicy.CS</span><span class="sxs-lookup"><span data-stu-id="03915-126">**Project**: Partner Center SDK Samples **Class**: CreateConfigurationPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="03915-127">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="03915-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="03915-128">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="03915-128">Request syntax</span></span>

| <span data-ttu-id="03915-129">Metod</span><span class="sxs-lookup"><span data-stu-id="03915-129">Method</span></span>   | <span data-ttu-id="03915-130">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="03915-130">Request URI</span></span>                                                                              |
|----------|------------------------------------------------------------------------------------------|
| <span data-ttu-id="03915-131">**EFTER**</span><span class="sxs-lookup"><span data-stu-id="03915-131">**POST**</span></span> | <span data-ttu-id="03915-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/policies http/1.1</span><span class="sxs-lookup"><span data-stu-id="03915-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="03915-133">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="03915-133">URI parameter</span></span>

<span data-ttu-id="03915-134">Använd följande Sök vägs parametrar när du skapar begäran.</span><span class="sxs-lookup"><span data-stu-id="03915-134">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="03915-135">Namn</span><span class="sxs-lookup"><span data-stu-id="03915-135">Name</span></span>        | <span data-ttu-id="03915-136">Typ</span><span class="sxs-lookup"><span data-stu-id="03915-136">Type</span></span>   | <span data-ttu-id="03915-137">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="03915-137">Required</span></span> | <span data-ttu-id="03915-138">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="03915-138">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="03915-139">kund-ID</span><span class="sxs-lookup"><span data-stu-id="03915-139">customer-id</span></span> | <span data-ttu-id="03915-140">sträng</span><span class="sxs-lookup"><span data-stu-id="03915-140">string</span></span> | <span data-ttu-id="03915-141">Yes</span><span class="sxs-lookup"><span data-stu-id="03915-141">Yes</span></span>      | <span data-ttu-id="03915-142">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="03915-142">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="03915-143">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="03915-143">Request headers</span></span>

<span data-ttu-id="03915-144">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="03915-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="03915-145">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="03915-145">Request body</span></span>

<span data-ttu-id="03915-146">Begär ande texten måste innehålla ett objekt med konfigurations princip informationen enligt beskrivningen i följande tabell:</span><span class="sxs-lookup"><span data-stu-id="03915-146">The request body must contain an object with the configuration policy information as described in the following table:</span></span>

| <span data-ttu-id="03915-147">Namn</span><span class="sxs-lookup"><span data-stu-id="03915-147">Name</span></span>           | <span data-ttu-id="03915-148">Typ</span><span class="sxs-lookup"><span data-stu-id="03915-148">Type</span></span>             | <span data-ttu-id="03915-149">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="03915-149">Required</span></span> | <span data-ttu-id="03915-150">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="03915-150">Description</span></span>                      |
|----------------|------------------|----------|----------------------------------|
| <span data-ttu-id="03915-151">name</span><span class="sxs-lookup"><span data-stu-id="03915-151">name</span></span>           | <span data-ttu-id="03915-152">sträng</span><span class="sxs-lookup"><span data-stu-id="03915-152">string</span></span>           | <span data-ttu-id="03915-153">Yes</span><span class="sxs-lookup"><span data-stu-id="03915-153">Yes</span></span>      | <span data-ttu-id="03915-154">Det egna namnet på principen.</span><span class="sxs-lookup"><span data-stu-id="03915-154">The friendly name of the policy.</span></span> |
| <span data-ttu-id="03915-155">category</span><span class="sxs-lookup"><span data-stu-id="03915-155">category</span></span>       | <span data-ttu-id="03915-156">sträng</span><span class="sxs-lookup"><span data-stu-id="03915-156">string</span></span>           | <span data-ttu-id="03915-157">Yes</span><span class="sxs-lookup"><span data-stu-id="03915-157">Yes</span></span>      | <span data-ttu-id="03915-158">Princip kategorin.</span><span class="sxs-lookup"><span data-stu-id="03915-158">The policy category.</span></span>             |
| <span data-ttu-id="03915-159">beskrivning</span><span class="sxs-lookup"><span data-stu-id="03915-159">description</span></span>    | <span data-ttu-id="03915-160">sträng</span><span class="sxs-lookup"><span data-stu-id="03915-160">string</span></span>           | <span data-ttu-id="03915-161">No</span><span class="sxs-lookup"><span data-stu-id="03915-161">No</span></span>       | <span data-ttu-id="03915-162">Princip beskrivningen.</span><span class="sxs-lookup"><span data-stu-id="03915-162">The policy description.</span></span>          |
| <span data-ttu-id="03915-163">policySettings</span><span class="sxs-lookup"><span data-stu-id="03915-163">policySettings</span></span> | <span data-ttu-id="03915-164">matris med strängar</span><span class="sxs-lookup"><span data-stu-id="03915-164">array of strings</span></span> | <span data-ttu-id="03915-165">Yes</span><span class="sxs-lookup"><span data-stu-id="03915-165">Yes</span></span>      | <span data-ttu-id="03915-166">Princip inställningarna.</span><span class="sxs-lookup"><span data-stu-id="03915-166">The policy settings.</span></span>             |

### <a name="request-example"></a><span data-ttu-id="03915-167">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="03915-167">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="03915-168">REST-svar</span><span class="sxs-lookup"><span data-stu-id="03915-168">REST response</span></span>

<span data-ttu-id="03915-169">Om det lyckas innehåller svars texten [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) -resursen för den nya principen.</span><span class="sxs-lookup"><span data-stu-id="03915-169">If successful, the response body contains the [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resource for the new policy.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="03915-170">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="03915-170">Response success and error codes</span></span>

<span data-ttu-id="03915-171">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="03915-171">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="03915-172">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="03915-172">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="03915-173">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="03915-173">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="03915-174">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="03915-174">Response example</span></span>

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
