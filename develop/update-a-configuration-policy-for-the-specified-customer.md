---
title: Uppdatera en konfigurationsprincip för den angivna kunden
description: Så här uppdaterar du den angivna konfigurations principen för den angivna kunden.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 42c57a92020723415b4621e9f9d7c5c3278bfb77
ms.sourcegitcommit: 970031473b2e8cd3d08c6c097949c057a51df3ef
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/03/2021
ms.locfileid: "99505347"
---
# <a name="update-a-configuration-policy-for-the-specified-customer"></a><span data-ttu-id="5c94e-103">Uppdatera en konfigurationsprincip för den angivna kunden</span><span class="sxs-lookup"><span data-stu-id="5c94e-103">Update a configuration policy for the specified customer</span></span>

<span data-ttu-id="5c94e-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="5c94e-104">**Applies To**</span></span>

- <span data-ttu-id="5c94e-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="5c94e-105">Partner Center</span></span>
- <span data-ttu-id="5c94e-106">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="5c94e-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="5c94e-107">Så här uppdaterar du den angivna konfigurations principen för den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="5c94e-107">How to update the specified configuration policy for the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c94e-108">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="5c94e-108">Prerequisites</span></span>

- <span data-ttu-id="5c94e-109">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="5c94e-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5c94e-110">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="5c94e-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="5c94e-111">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5c94e-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="5c94e-112">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="5c94e-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="5c94e-113">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="5c94e-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="5c94e-114">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="5c94e-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="5c94e-115">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="5c94e-115">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="5c94e-116">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5c94e-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="5c94e-117">Princip identifieraren.</span><span class="sxs-lookup"><span data-stu-id="5c94e-117">The policy identifier.</span></span>

## <a name="c"></a><span data-ttu-id="5c94e-118">C\#</span><span class="sxs-lookup"><span data-stu-id="5c94e-118">C\#</span></span>

<span data-ttu-id="5c94e-119">Om du vill uppdatera en befintlig konfigurations princip för den angivna kunden instansierar du ett nytt [**ConfigurationPolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) -objekt som visas i följande kodfragment.</span><span class="sxs-lookup"><span data-stu-id="5c94e-119">To update an existing configuration policy for the specified customer, instantiate a new [**ConfigurationPolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) object as shown in the following code snippet.</span></span> <span data-ttu-id="5c94e-120">Värdena i det nya objektet ersätter motsvarande värden i det befintliga objektet.</span><span class="sxs-lookup"><span data-stu-id="5c94e-120">The values in this new object replace the corresponding values in the existing object.</span></span> <span data-ttu-id="5c94e-121">Anropa sedan metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID för att hämta ett gränssnitt till åtgärder på den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="5c94e-121">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="5c94e-122">Anropa sedan metoden [**ConfigurationPolicies. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) med princip-ID: t för att hämta ett gränssnitt till konfigurations princip åtgärder för den angivna principen.</span><span class="sxs-lookup"><span data-stu-id="5c94e-122">Next, call the [**ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) method with the policy ID to retrieve an interface to configuration policy operations for the specified policy.</span></span> <span data-ttu-id="5c94e-123">Slutligen kan du anropa [**korrigerings filen**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patch) eller [**PatchAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patchasync) -metoden för att uppdatera konfigurations principen.</span><span class="sxs-lookup"><span data-stu-id="5c94e-123">Finally, call the [**Patch**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patch) or [**PatchAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patchasync) method to update the configuration policy.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedConfigurationPolicyId;

ConfigurationPolicy configPolicyToBeUpdated = new ConfigurationPolicy()
{
    Name= "Test Config Policy",
    Id = selectedConfigurationPolicyId,
    PolicySettings = new List<PolicySettingsType>() {
        PolicySettingsType.OobeUserNotLocalAdmin,
        PolicySettingsType.RemoveOemPreinstalls }
};

ConfigurationPolicy updatedConfigurationPolicy =
    partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.ById(selectedConfigurationPolicyId).Patch(configPolicyToBeUpdated);
```

<span data-ttu-id="5c94e-124">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="5c94e-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="5c94e-125">**Projekt**: Partner Center SDK-exempel **klass**: UpdateConfigurationPolicy.CS</span><span class="sxs-lookup"><span data-stu-id="5c94e-125">**Project**: Partner Center SDK Samples **Class**: UpdateConfigurationPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="5c94e-126">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="5c94e-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5c94e-127">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="5c94e-127">Request syntax</span></span>

| <span data-ttu-id="5c94e-128">Metod</span><span class="sxs-lookup"><span data-stu-id="5c94e-128">Method</span></span>  | <span data-ttu-id="5c94e-129">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="5c94e-129">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5c94e-130">**PUT**</span><span class="sxs-lookup"><span data-stu-id="5c94e-130">**PUT**</span></span> | <span data-ttu-id="5c94e-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/policies/{Policy-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="5c94e-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies/{policy-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="5c94e-132">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="5c94e-132">URI parameter</span></span>

<span data-ttu-id="5c94e-133">Använd följande Sök vägs parametrar när du skapar begäran.</span><span class="sxs-lookup"><span data-stu-id="5c94e-133">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="5c94e-134">Namn</span><span class="sxs-lookup"><span data-stu-id="5c94e-134">Name</span></span>        | <span data-ttu-id="5c94e-135">Typ</span><span class="sxs-lookup"><span data-stu-id="5c94e-135">Type</span></span>   | <span data-ttu-id="5c94e-136">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="5c94e-136">Required</span></span> | <span data-ttu-id="5c94e-137">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="5c94e-137">Description</span></span>                                                   |
|-------------|--------|----------|---------------------------------------------------------------|
| <span data-ttu-id="5c94e-138">kund-ID</span><span class="sxs-lookup"><span data-stu-id="5c94e-138">customer-id</span></span> | <span data-ttu-id="5c94e-139">sträng</span><span class="sxs-lookup"><span data-stu-id="5c94e-139">string</span></span> | <span data-ttu-id="5c94e-140">Ja</span><span class="sxs-lookup"><span data-stu-id="5c94e-140">Yes</span></span>      | <span data-ttu-id="5c94e-141">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="5c94e-141">A GUID-formatted string that identifies the customer.</span></span>         |
| <span data-ttu-id="5c94e-142">princip-ID</span><span class="sxs-lookup"><span data-stu-id="5c94e-142">policy-id</span></span>   | <span data-ttu-id="5c94e-143">sträng</span><span class="sxs-lookup"><span data-stu-id="5c94e-143">string</span></span> | <span data-ttu-id="5c94e-144">Ja</span><span class="sxs-lookup"><span data-stu-id="5c94e-144">Yes</span></span>      | <span data-ttu-id="5c94e-145">En GUID-formaterad sträng som identifierar den princip som ska uppdateras.</span><span class="sxs-lookup"><span data-stu-id="5c94e-145">A GUID-formatted string that identifies the policy to update.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="5c94e-146">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="5c94e-146">Request headers</span></span>

<span data-ttu-id="5c94e-147">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="5c94e-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5c94e-148">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="5c94e-148">Request body</span></span>

<span data-ttu-id="5c94e-149">Begär ande texten måste innehålla ett objekt som innehåller princip informationen.</span><span class="sxs-lookup"><span data-stu-id="5c94e-149">The request body must contain an object that provides the policy information.</span></span>

| <span data-ttu-id="5c94e-150">Namn</span><span class="sxs-lookup"><span data-stu-id="5c94e-150">Name</span></span>            | <span data-ttu-id="5c94e-151">Typ</span><span class="sxs-lookup"><span data-stu-id="5c94e-151">Type</span></span>             | <span data-ttu-id="5c94e-152">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="5c94e-152">Required</span></span> | <span data-ttu-id="5c94e-153">Uppdateras</span><span class="sxs-lookup"><span data-stu-id="5c94e-153">Updatable</span></span> | <span data-ttu-id="5c94e-154">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="5c94e-154">Description</span></span>                                                                                                                                              |
|-----------------|------------------|----------|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5c94e-155">id</span><span class="sxs-lookup"><span data-stu-id="5c94e-155">id</span></span>              | <span data-ttu-id="5c94e-156">sträng</span><span class="sxs-lookup"><span data-stu-id="5c94e-156">string</span></span>           | <span data-ttu-id="5c94e-157">Ja</span><span class="sxs-lookup"><span data-stu-id="5c94e-157">Yes</span></span>      | <span data-ttu-id="5c94e-158">Inga</span><span class="sxs-lookup"><span data-stu-id="5c94e-158">No</span></span>        | <span data-ttu-id="5c94e-159">Den GUID-formaterade sträng som identifierar principen.</span><span class="sxs-lookup"><span data-stu-id="5c94e-159">The GUID-formatted string that identifies the policy.</span></span>                                                                                                    |
| <span data-ttu-id="5c94e-160">name</span><span class="sxs-lookup"><span data-stu-id="5c94e-160">name</span></span>            | <span data-ttu-id="5c94e-161">sträng</span><span class="sxs-lookup"><span data-stu-id="5c94e-161">string</span></span>           | <span data-ttu-id="5c94e-162">Ja</span><span class="sxs-lookup"><span data-stu-id="5c94e-162">Yes</span></span>      | <span data-ttu-id="5c94e-163">Ja</span><span class="sxs-lookup"><span data-stu-id="5c94e-163">Yes</span></span>       | <span data-ttu-id="5c94e-164">Det egna namnet på principen.</span><span class="sxs-lookup"><span data-stu-id="5c94e-164">The friendly name of the policy.</span></span>                                                                                                                         |
| <span data-ttu-id="5c94e-165">category</span><span class="sxs-lookup"><span data-stu-id="5c94e-165">category</span></span>        | <span data-ttu-id="5c94e-166">sträng</span><span class="sxs-lookup"><span data-stu-id="5c94e-166">string</span></span>           | <span data-ttu-id="5c94e-167">Ja</span><span class="sxs-lookup"><span data-stu-id="5c94e-167">Yes</span></span>      | <span data-ttu-id="5c94e-168">Inga</span><span class="sxs-lookup"><span data-stu-id="5c94e-168">No</span></span>        | <span data-ttu-id="5c94e-169">Princip kategorin.</span><span class="sxs-lookup"><span data-stu-id="5c94e-169">The policy category.</span></span>                                                                                                                                     |
| <span data-ttu-id="5c94e-170">beskrivning</span><span class="sxs-lookup"><span data-stu-id="5c94e-170">description</span></span>     | <span data-ttu-id="5c94e-171">sträng</span><span class="sxs-lookup"><span data-stu-id="5c94e-171">string</span></span>           | <span data-ttu-id="5c94e-172">Inga</span><span class="sxs-lookup"><span data-stu-id="5c94e-172">No</span></span>       | <span data-ttu-id="5c94e-173">Ja</span><span class="sxs-lookup"><span data-stu-id="5c94e-173">Yes</span></span>       | <span data-ttu-id="5c94e-174">Princip beskrivningen.</span><span class="sxs-lookup"><span data-stu-id="5c94e-174">The policy description.</span></span>                                                                                                                                  |
| <span data-ttu-id="5c94e-175">devicesAssigned</span><span class="sxs-lookup"><span data-stu-id="5c94e-175">devicesAssigned</span></span> | <span data-ttu-id="5c94e-176">antal</span><span class="sxs-lookup"><span data-stu-id="5c94e-176">number</span></span>           | <span data-ttu-id="5c94e-177">Inga</span><span class="sxs-lookup"><span data-stu-id="5c94e-177">No</span></span>       | <span data-ttu-id="5c94e-178">Inga</span><span class="sxs-lookup"><span data-stu-id="5c94e-178">No</span></span>        | <span data-ttu-id="5c94e-179">Antalet enheter.</span><span class="sxs-lookup"><span data-stu-id="5c94e-179">The number of devices.</span></span>                                                                                                                                   |
| <span data-ttu-id="5c94e-180">policySettings</span><span class="sxs-lookup"><span data-stu-id="5c94e-180">policySettings</span></span>  | <span data-ttu-id="5c94e-181">matris med strängar</span><span class="sxs-lookup"><span data-stu-id="5c94e-181">array of strings</span></span> | <span data-ttu-id="5c94e-182">Ja</span><span class="sxs-lookup"><span data-stu-id="5c94e-182">Yes</span></span>      | <span data-ttu-id="5c94e-183">Ja</span><span class="sxs-lookup"><span data-stu-id="5c94e-183">Yes</span></span>       | <span data-ttu-id="5c94e-184">Princip inställningarna: "ingen", "ta bort \_ OEM \_ -förinstallationer", "OOBE \_ User \_ not \_ Local \_ admin", "hoppa över \_ Express \_ Inställningar", "hoppa över \_ OEM \_ -registrering", hoppa över \_ EULA ".</span><span class="sxs-lookup"><span data-stu-id="5c94e-184">The policy settings: "none","remove\_oem\_preinstalls","oobe\_user\_not\_local\_admin","skip\_express\_settings","skip \_oem\_registration,"skip\_eula".</span></span> |

### <a name="request-example"></a><span data-ttu-id="5c94e-185">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="5c94e-185">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies/56edf752-ee77-4fd8-b7f5-df1f74a3a9ac HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 256
Content-Type: application/json
Host: api.partnercenter.microsoft.com

{
    "id": "56edf752-ee77-4fd8-b7f5-df1f74a3a9ac",
    "name": "Windows test policy",
    "category": "o_o_b_e",
    "description": "Test policy creation from API",
    "devicesAssigned": 0,
    "policySettings": ["skip_express_settings"]
}
```

## <a name="rest-response"></a><span data-ttu-id="5c94e-186">REST-svar</span><span class="sxs-lookup"><span data-stu-id="5c94e-186">REST response</span></span>

<span data-ttu-id="5c94e-187">Om det lyckas innehåller svars texten [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) -resursen för den nya principen.</span><span class="sxs-lookup"><span data-stu-id="5c94e-187">If successful, the response body contains the [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resource for the new policy.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5c94e-188">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="5c94e-188">Response success and error codes</span></span>

<span data-ttu-id="5c94e-189">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="5c94e-189">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5c94e-190">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="5c94e-190">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5c94e-191">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="5c94e-191">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5c94e-192">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="5c94e-192">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 421
Content-Type: application/json; charset=utf-8
MS-CorrelationId: f9fd5973-6ad8-4585-aadc-f2b0443fe27b
MS-RequestId: cb1fa1f3-1381-45d9-99c5-511e5d3efa7c
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:10:29 GMT

{
    "id": "56edf752-ee77-4fd8-b7f5-df1f74a3a9ac",
    "name": "Windows test policy",
    "category": "o_o_b_e",
    "description": "Test policy creation from API",
    "devicesAssigned": 0,
    "policySettings": ["skip_express_settings"],
    "createdDate": "2017-01-01T00:00:00",
    "lastModifiedDate": "2017-07-25T18:10:15",
    "attributes": {
        "objectType": "ConfigurationPolicy"
    }
}
```
