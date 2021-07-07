---
title: Uppdatera en konfigurationsprincip för den angivna kunden
description: Så här uppdaterar du den angivna konfigurationsprincipen för den angivna kunden.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 5e008f41a44f2b7cf3ddfd705505175c69bbad38
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530249"
---
# <a name="update-a-configuration-policy-for-the-specified-customer"></a><span data-ttu-id="0b202-103">Uppdatera en konfigurationsprincip för den angivna kunden</span><span class="sxs-lookup"><span data-stu-id="0b202-103">Update a configuration policy for the specified customer</span></span>

<span data-ttu-id="0b202-104">**Gäller för**: Partner Center-| Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="0b202-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="0b202-105">Så här uppdaterar du den angivna konfigurationsprincipen för den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="0b202-105">How to update the specified configuration policy for the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0b202-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="0b202-106">Prerequisites</span></span>

- <span data-ttu-id="0b202-107">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="0b202-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0b202-108">Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="0b202-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="0b202-109">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0b202-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="0b202-110">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="0b202-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="0b202-111">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="0b202-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="0b202-112">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="0b202-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="0b202-113">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="0b202-113">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="0b202-114">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0b202-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="0b202-115">Principidentifieraren.</span><span class="sxs-lookup"><span data-stu-id="0b202-115">The policy identifier.</span></span>

## <a name="c"></a><span data-ttu-id="0b202-116">C\#</span><span class="sxs-lookup"><span data-stu-id="0b202-116">C\#</span></span>

<span data-ttu-id="0b202-117">Om du vill uppdatera en befintlig konfigurationsprincip för den angivna kunden instansierar du ett nytt [**ConfigurationPolicy-objekt**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) enligt följande kodfragment.</span><span class="sxs-lookup"><span data-stu-id="0b202-117">To update an existing configuration policy for the specified customer, instantiate a new [**ConfigurationPolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) object as shown in the following code snippet.</span></span> <span data-ttu-id="0b202-118">Värdena i det här nya objektet ersätter motsvarande värden i det befintliga objektet.</span><span class="sxs-lookup"><span data-stu-id="0b202-118">The values in this new object replace the corresponding values in the existing object.</span></span> <span data-ttu-id="0b202-119">Anropa sedan metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att hämta ett gränssnitt till åtgärder på den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="0b202-119">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="0b202-120">Anropa sedan metoden [**ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) med princip-ID:t för att hämta ett gränssnitt för konfigurationsprincipåtgärder för den angivna principen.</span><span class="sxs-lookup"><span data-stu-id="0b202-120">Next, call the [**ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) method with the policy ID to retrieve an interface to configuration policy operations for the specified policy.</span></span> <span data-ttu-id="0b202-121">Anropa slutligen metoden [**Patch**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patch) eller [**PatchAsync för**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patchasync) att uppdatera konfigurationsprincipen.</span><span class="sxs-lookup"><span data-stu-id="0b202-121">Finally, call the [**Patch**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patch) or [**PatchAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patchasync) method to update the configuration policy.</span></span>

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

<span data-ttu-id="0b202-122">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="0b202-122">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="0b202-123">**Project:** Partnercenter-SDK **exempelklass:** UpdateConfigurationPolicy.cs</span><span class="sxs-lookup"><span data-stu-id="0b202-123">**Project**: Partner Center SDK Samples **Class**: UpdateConfigurationPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="0b202-124">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="0b202-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0b202-125">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="0b202-125">Request syntax</span></span>

| <span data-ttu-id="0b202-126">Metod</span><span class="sxs-lookup"><span data-stu-id="0b202-126">Method</span></span>  | <span data-ttu-id="0b202-127">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="0b202-127">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0b202-128">**PUT**</span><span class="sxs-lookup"><span data-stu-id="0b202-128">**PUT**</span></span> | <span data-ttu-id="0b202-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies/{policy-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="0b202-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies/{policy-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="0b202-130">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="0b202-130">URI parameter</span></span>

<span data-ttu-id="0b202-131">Använd följande sökvägsparametrar när du skapar begäran.</span><span class="sxs-lookup"><span data-stu-id="0b202-131">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="0b202-132">Namn</span><span class="sxs-lookup"><span data-stu-id="0b202-132">Name</span></span>        | <span data-ttu-id="0b202-133">Typ</span><span class="sxs-lookup"><span data-stu-id="0b202-133">Type</span></span>   | <span data-ttu-id="0b202-134">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="0b202-134">Required</span></span> | <span data-ttu-id="0b202-135">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="0b202-135">Description</span></span>                                                   |
|-------------|--------|----------|---------------------------------------------------------------|
| <span data-ttu-id="0b202-136">kund-id</span><span class="sxs-lookup"><span data-stu-id="0b202-136">customer-id</span></span> | <span data-ttu-id="0b202-137">sträng</span><span class="sxs-lookup"><span data-stu-id="0b202-137">string</span></span> | <span data-ttu-id="0b202-138">Ja</span><span class="sxs-lookup"><span data-stu-id="0b202-138">Yes</span></span>      | <span data-ttu-id="0b202-139">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="0b202-139">A GUID-formatted string that identifies the customer.</span></span>         |
| <span data-ttu-id="0b202-140">policy-id</span><span class="sxs-lookup"><span data-stu-id="0b202-140">policy-id</span></span>   | <span data-ttu-id="0b202-141">sträng</span><span class="sxs-lookup"><span data-stu-id="0b202-141">string</span></span> | <span data-ttu-id="0b202-142">Ja</span><span class="sxs-lookup"><span data-stu-id="0b202-142">Yes</span></span>      | <span data-ttu-id="0b202-143">En GUID-formaterad sträng som identifierar principen som ska uppdateras.</span><span class="sxs-lookup"><span data-stu-id="0b202-143">A GUID-formatted string that identifies the policy to update.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="0b202-144">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="0b202-144">Request headers</span></span>

<span data-ttu-id="0b202-145">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="0b202-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0b202-146">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="0b202-146">Request body</span></span>

<span data-ttu-id="0b202-147">Begärandetexten måste innehålla ett -objekt som tillhandahåller principinformationen.</span><span class="sxs-lookup"><span data-stu-id="0b202-147">The request body must contain an object that provides the policy information.</span></span>

| <span data-ttu-id="0b202-148">Namn</span><span class="sxs-lookup"><span data-stu-id="0b202-148">Name</span></span>            | <span data-ttu-id="0b202-149">Typ</span><span class="sxs-lookup"><span data-stu-id="0b202-149">Type</span></span>             | <span data-ttu-id="0b202-150">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="0b202-150">Required</span></span> | <span data-ttu-id="0b202-151">Uppdateringsbar</span><span class="sxs-lookup"><span data-stu-id="0b202-151">Updatable</span></span> | <span data-ttu-id="0b202-152">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="0b202-152">Description</span></span>                                                                                                                                              |
|-----------------|------------------|----------|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0b202-153">id</span><span class="sxs-lookup"><span data-stu-id="0b202-153">id</span></span>              | <span data-ttu-id="0b202-154">sträng</span><span class="sxs-lookup"><span data-stu-id="0b202-154">string</span></span>           | <span data-ttu-id="0b202-155">Ja</span><span class="sxs-lookup"><span data-stu-id="0b202-155">Yes</span></span>      | <span data-ttu-id="0b202-156">Inga</span><span class="sxs-lookup"><span data-stu-id="0b202-156">No</span></span>        | <span data-ttu-id="0b202-157">Den GUID-formaterade sträng som identifierar principen.</span><span class="sxs-lookup"><span data-stu-id="0b202-157">The GUID-formatted string that identifies the policy.</span></span>                                                                                                    |
| <span data-ttu-id="0b202-158">name</span><span class="sxs-lookup"><span data-stu-id="0b202-158">name</span></span>            | <span data-ttu-id="0b202-159">sträng</span><span class="sxs-lookup"><span data-stu-id="0b202-159">string</span></span>           | <span data-ttu-id="0b202-160">Ja</span><span class="sxs-lookup"><span data-stu-id="0b202-160">Yes</span></span>      | <span data-ttu-id="0b202-161">Ja</span><span class="sxs-lookup"><span data-stu-id="0b202-161">Yes</span></span>       | <span data-ttu-id="0b202-162">Principens egna namn.</span><span class="sxs-lookup"><span data-stu-id="0b202-162">The friendly name of the policy.</span></span>                                                                                                                         |
| <span data-ttu-id="0b202-163">category</span><span class="sxs-lookup"><span data-stu-id="0b202-163">category</span></span>        | <span data-ttu-id="0b202-164">sträng</span><span class="sxs-lookup"><span data-stu-id="0b202-164">string</span></span>           | <span data-ttu-id="0b202-165">Ja</span><span class="sxs-lookup"><span data-stu-id="0b202-165">Yes</span></span>      | <span data-ttu-id="0b202-166">Inga</span><span class="sxs-lookup"><span data-stu-id="0b202-166">No</span></span>        | <span data-ttu-id="0b202-167">Principkategorin.</span><span class="sxs-lookup"><span data-stu-id="0b202-167">The policy category.</span></span>                                                                                                                                     |
| <span data-ttu-id="0b202-168">beskrivning</span><span class="sxs-lookup"><span data-stu-id="0b202-168">description</span></span>     | <span data-ttu-id="0b202-169">sträng</span><span class="sxs-lookup"><span data-stu-id="0b202-169">string</span></span>           | <span data-ttu-id="0b202-170">Inga</span><span class="sxs-lookup"><span data-stu-id="0b202-170">No</span></span>       | <span data-ttu-id="0b202-171">Ja</span><span class="sxs-lookup"><span data-stu-id="0b202-171">Yes</span></span>       | <span data-ttu-id="0b202-172">Principbeskrivningen.</span><span class="sxs-lookup"><span data-stu-id="0b202-172">The policy description.</span></span>                                                                                                                                  |
| <span data-ttu-id="0b202-173">devicesAssigned</span><span class="sxs-lookup"><span data-stu-id="0b202-173">devicesAssigned</span></span> | <span data-ttu-id="0b202-174">antal</span><span class="sxs-lookup"><span data-stu-id="0b202-174">number</span></span>           | <span data-ttu-id="0b202-175">Inga</span><span class="sxs-lookup"><span data-stu-id="0b202-175">No</span></span>       | <span data-ttu-id="0b202-176">Inga</span><span class="sxs-lookup"><span data-stu-id="0b202-176">No</span></span>        | <span data-ttu-id="0b202-177">Antalet enheter.</span><span class="sxs-lookup"><span data-stu-id="0b202-177">The number of devices.</span></span>                                                                                                                                   |
| <span data-ttu-id="0b202-178">policySettings</span><span class="sxs-lookup"><span data-stu-id="0b202-178">policySettings</span></span>  | <span data-ttu-id="0b202-179">matris med strängar</span><span class="sxs-lookup"><span data-stu-id="0b202-179">array of strings</span></span> | <span data-ttu-id="0b202-180">Ja</span><span class="sxs-lookup"><span data-stu-id="0b202-180">Yes</span></span>      | <span data-ttu-id="0b202-181">Ja</span><span class="sxs-lookup"><span data-stu-id="0b202-181">Yes</span></span>       | <span data-ttu-id="0b202-182">Principinställningarna: "none","remove \_ oem \_ preinstalls","oobe \_ user not local \_ \_ \_ admin","skip \_ express \_ settings","skip \_ oem \_ registration,"skip \_ eula".</span><span class="sxs-lookup"><span data-stu-id="0b202-182">The policy settings: "none","remove\_oem\_preinstalls","oobe\_user\_not\_local\_admin","skip\_express\_settings","skip \_oem\_registration,"skip\_eula".</span></span> |

### <a name="request-example"></a><span data-ttu-id="0b202-183">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="0b202-183">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="0b202-184">REST-svar</span><span class="sxs-lookup"><span data-stu-id="0b202-184">REST response</span></span>

<span data-ttu-id="0b202-185">Om det lyckas innehåller svarstexten [ConfigurationPolicy-resursen](device-deployment-resources.md#configurationpolicy) för den nya principen.</span><span class="sxs-lookup"><span data-stu-id="0b202-185">If successful, the response body contains the [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resource for the new policy.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0b202-186">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="0b202-186">Response success and error codes</span></span>

<span data-ttu-id="0b202-187">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="0b202-187">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0b202-188">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="0b202-188">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="0b202-189">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="0b202-189">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="0b202-190">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="0b202-190">Response example</span></span>

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
