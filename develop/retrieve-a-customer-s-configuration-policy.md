---
title: Hämta en kunds konfigurationsprincip
description: Hur du hämtar den angivna konfigurations principen för den angivna kunden.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8d5d4ee83d1a66f33872d8b1f1327f47eeb4465e
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769789"
---
# <a name="retrieve-a-customers-configuration-policy"></a><span data-ttu-id="9c1e5-103">Hämta en kunds konfigurationsprincip</span><span class="sxs-lookup"><span data-stu-id="9c1e5-103">Retrieve a customer's configuration policy</span></span>

<span data-ttu-id="9c1e5-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="9c1e5-104">**Applies To**</span></span>

- <span data-ttu-id="9c1e5-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="9c1e5-105">Partner Center</span></span>
- <span data-ttu-id="9c1e5-106">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="9c1e5-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="9c1e5-107">Hur du hämtar den angivna konfigurations principen för den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="9c1e5-107">How to retrieve the specified configuration policy for the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9c1e5-108">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="9c1e5-108">Prerequisites</span></span>

- <span data-ttu-id="9c1e5-109">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="9c1e5-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9c1e5-110">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="9c1e5-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="9c1e5-111">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9c1e5-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="9c1e5-112">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="9c1e5-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="9c1e5-113">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="9c1e5-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="9c1e5-114">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="9c1e5-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="9c1e5-115">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="9c1e5-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="9c1e5-116">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9c1e5-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="9c1e5-117">Princip identifieraren.</span><span class="sxs-lookup"><span data-stu-id="9c1e5-117">The policy identifier.</span></span>

## <a name="c"></a><span data-ttu-id="9c1e5-118">C\#</span><span class="sxs-lookup"><span data-stu-id="9c1e5-118">C\#</span></span>

<span data-ttu-id="9c1e5-119">Om du vill hämta en konfigurations princip för den angivna kunden anropar du först metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: t för att hämta ett gränssnitt till åtgärder på den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="9c1e5-119">To retrieve a configuration policy for the specified customer, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="9c1e5-120">Anropa sedan metoden [**ConfigurationPolicies. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) med princip-ID: t för att hämta ett gränssnitt till konfigurations princip åtgärder för den angivna principen.</span><span class="sxs-lookup"><span data-stu-id="9c1e5-120">Next, call the [**ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) method with the policy ID to retrieve an interface to configuration policy operations for the specified policy.</span></span> <span data-ttu-id="9c1e5-121">Anropa slutligen metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.getasync) för att hämta konfigurations principen.</span><span class="sxs-lookup"><span data-stu-id="9c1e5-121">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.getasync) method to retrieve the configuration policy.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedConfigurationPolicyId;

ConfigurationPolicy retrievedConfigurationPolicy =
    partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.ById(selectedConfigurationPolicyId).Get();
```

<span data-ttu-id="9c1e5-122">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="9c1e5-122">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="9c1e5-123">**Projekt**: Partner Center SDK-exempel **klass**: GetConfigurationPolicy.CS</span><span class="sxs-lookup"><span data-stu-id="9c1e5-123">**Project**: Partner Center SDK Samples **Class**: GetConfigurationPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="9c1e5-124">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="9c1e5-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9c1e5-125">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="9c1e5-125">Request syntax</span></span>

| <span data-ttu-id="9c1e5-126">Metod</span><span class="sxs-lookup"><span data-stu-id="9c1e5-126">Method</span></span>  | <span data-ttu-id="9c1e5-127">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="9c1e5-127">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9c1e5-128">**TA**</span><span class="sxs-lookup"><span data-stu-id="9c1e5-128">**GET**</span></span> | <span data-ttu-id="9c1e5-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/policies/{Policy-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="9c1e5-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies/{policy-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="9c1e5-130">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="9c1e5-130">URI parameter</span></span>

<span data-ttu-id="9c1e5-131">Använd följande sökväg och frågeparametrar när du skapar begäran.</span><span class="sxs-lookup"><span data-stu-id="9c1e5-131">Use the following path and query parameters when creating the request.</span></span>

| <span data-ttu-id="9c1e5-132">Namn</span><span class="sxs-lookup"><span data-stu-id="9c1e5-132">Name</span></span>        | <span data-ttu-id="9c1e5-133">Typ</span><span class="sxs-lookup"><span data-stu-id="9c1e5-133">Type</span></span>   | <span data-ttu-id="9c1e5-134">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="9c1e5-134">Required</span></span> | <span data-ttu-id="9c1e5-135">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="9c1e5-135">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="9c1e5-136">kund-ID</span><span class="sxs-lookup"><span data-stu-id="9c1e5-136">customer-id</span></span> | <span data-ttu-id="9c1e5-137">sträng</span><span class="sxs-lookup"><span data-stu-id="9c1e5-137">string</span></span> | <span data-ttu-id="9c1e5-138">Yes</span><span class="sxs-lookup"><span data-stu-id="9c1e5-138">Yes</span></span>      | <span data-ttu-id="9c1e5-139">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="9c1e5-139">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="9c1e5-140">princip-ID</span><span class="sxs-lookup"><span data-stu-id="9c1e5-140">policy-id</span></span>   | <span data-ttu-id="9c1e5-141">sträng</span><span class="sxs-lookup"><span data-stu-id="9c1e5-141">string</span></span> | <span data-ttu-id="9c1e5-142">Yes</span><span class="sxs-lookup"><span data-stu-id="9c1e5-142">Yes</span></span>      | <span data-ttu-id="9c1e5-143">En GUID-formaterad sträng som identifierar principen.</span><span class="sxs-lookup"><span data-stu-id="9c1e5-143">A GUID-formatted string that identifies the policy.</span></span>   |

### <a name="request-headers"></a><span data-ttu-id="9c1e5-144">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="9c1e5-144">Request headers</span></span>

<span data-ttu-id="9c1e5-145">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="9c1e5-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9c1e5-146">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="9c1e5-146">Request body</span></span>

<span data-ttu-id="9c1e5-147">Inget</span><span class="sxs-lookup"><span data-stu-id="9c1e5-147">None</span></span>

### <a name="request-example"></a><span data-ttu-id="9c1e5-148">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="9c1e5-148">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="9c1e5-149">REST-svar</span><span class="sxs-lookup"><span data-stu-id="9c1e5-149">REST response</span></span>

<span data-ttu-id="9c1e5-150">Om det lyckas innehåller svaret den begärda [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) -resursen.</span><span class="sxs-lookup"><span data-stu-id="9c1e5-150">If successful, the response contains the requested [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9c1e5-151">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="9c1e5-151">Response success and error codes</span></span>

<span data-ttu-id="9c1e5-152">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="9c1e5-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9c1e5-153">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="9c1e5-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9c1e5-154">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9c1e5-154">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9c1e5-155">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="9c1e5-155">Response example</span></span>

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
