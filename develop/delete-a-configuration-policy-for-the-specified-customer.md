---
title: Ta bort en konfigurationsprincip för den angivna kunden
description: Så här tar du bort en konfigurations princip för en angiven kund och princip identifierare.
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 586878367fc0873ef0fb1415799b2b7022954053
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769390"
---
# <a name="delete-a-configuration-policy-for-the-specified-customer"></a><span data-ttu-id="68103-103">Ta bort en konfigurationsprincip för den angivna kunden</span><span class="sxs-lookup"><span data-stu-id="68103-103">Delete a configuration policy for the specified customer</span></span>

<span data-ttu-id="68103-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="68103-104">**Applies to:**</span></span>

- <span data-ttu-id="68103-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="68103-105">Partner Center</span></span>
- <span data-ttu-id="68103-106">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="68103-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="68103-107">Så här tar du bort en konfigurations princip för en angiven kund och princip identifierare.</span><span class="sxs-lookup"><span data-stu-id="68103-107">How to delete a configuration policy for a specified customer and policy identifier.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68103-108">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="68103-108">Prerequisites</span></span>

- <span data-ttu-id="68103-109">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="68103-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="68103-110">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="68103-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="68103-111">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="68103-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="68103-112">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="68103-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="68103-113">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="68103-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="68103-114">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="68103-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="68103-115">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="68103-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="68103-116">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="68103-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="68103-117">Princip identifieraren.</span><span class="sxs-lookup"><span data-stu-id="68103-117">The policy identifier.</span></span>

## <a name="c"></a><span data-ttu-id="68103-118">C\#</span><span class="sxs-lookup"><span data-stu-id="68103-118">C\#</span></span>

<span data-ttu-id="68103-119">Så här tar du bort en konfigurations princip för en angiven kund:</span><span class="sxs-lookup"><span data-stu-id="68103-119">To delete a configuration policy for a specified customer:</span></span>

1. <span data-ttu-id="68103-120">Anropa metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: t för att hämta ett gränssnitt till åtgärder på den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="68103-120">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span>

2. <span data-ttu-id="68103-121">Anropa metoden [**ConfigurationPolicies. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) med princip-ID: t för att hämta ett gränssnitt till konfigurations princip åtgärder för den angivna principen.</span><span class="sxs-lookup"><span data-stu-id="68103-121">Call the [**ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) method with the policy ID to retrieve an interface to configuration policy operations for the specified policy.</span></span>

3. <span data-ttu-id="68103-122">Anropa [**Delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.delete) -eller [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.deleteasync) -metoden för att ta bort konfigurations principen.</span><span class="sxs-lookup"><span data-stu-id="68103-122">Call the [**Delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.delete) or [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.deleteasync) method to delete the configuration policy.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedPolicyId;

partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.ById(selectedPolicyId).Delete();
```

<span data-ttu-id="68103-123">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="68103-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="68103-124">**Projekt**: Partner Center SDK-exempel **klass**: DeleteConfigurationPolicy.CS</span><span class="sxs-lookup"><span data-stu-id="68103-124">**Project**: Partner Center SDK Samples **Class**: DeleteConfigurationPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="68103-125">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="68103-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="68103-126">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="68103-126">Request syntax</span></span>

| <span data-ttu-id="68103-127">Metod</span><span class="sxs-lookup"><span data-stu-id="68103-127">Method</span></span>     | <span data-ttu-id="68103-128">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="68103-128">Request URI</span></span>                                                                                          |
|------------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="68103-129">**TA bort**</span><span class="sxs-lookup"><span data-stu-id="68103-129">**DELETE**</span></span> | <span data-ttu-id="68103-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/policies/{Policy-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="68103-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies/{policy-id} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="68103-131">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="68103-131">URI parameters</span></span>

<span data-ttu-id="68103-132">Använd följande Sök vägs parametrar när du skapar begäran.</span><span class="sxs-lookup"><span data-stu-id="68103-132">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="68103-133">Namn</span><span class="sxs-lookup"><span data-stu-id="68103-133">Name</span></span>        | <span data-ttu-id="68103-134">Typ</span><span class="sxs-lookup"><span data-stu-id="68103-134">Type</span></span>   | <span data-ttu-id="68103-135">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="68103-135">Required</span></span> | <span data-ttu-id="68103-136">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="68103-136">Description</span></span>                                                   |
|-------------|--------|----------|---------------------------------------------------------------|
| <span data-ttu-id="68103-137">kund-ID</span><span class="sxs-lookup"><span data-stu-id="68103-137">customer-id</span></span> | <span data-ttu-id="68103-138">sträng</span><span class="sxs-lookup"><span data-stu-id="68103-138">string</span></span> | <span data-ttu-id="68103-139">Yes</span><span class="sxs-lookup"><span data-stu-id="68103-139">Yes</span></span>      | <span data-ttu-id="68103-140">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="68103-140">A GUID-formatted string that identifies the customer.</span></span>         |
| <span data-ttu-id="68103-141">princip-ID</span><span class="sxs-lookup"><span data-stu-id="68103-141">policy-id</span></span>   | <span data-ttu-id="68103-142">sträng</span><span class="sxs-lookup"><span data-stu-id="68103-142">string</span></span> | <span data-ttu-id="68103-143">Yes</span><span class="sxs-lookup"><span data-stu-id="68103-143">Yes</span></span>      | <span data-ttu-id="68103-144">En GUID-formaterad sträng som identifierar den princip som ska tas bort.</span><span class="sxs-lookup"><span data-stu-id="68103-144">A GUID-formatted string that identifies the policy to delete.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="68103-145">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="68103-145">Request headers</span></span>

<span data-ttu-id="68103-146">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="68103-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="68103-147">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="68103-147">Request body</span></span>

<span data-ttu-id="68103-148">Inget</span><span class="sxs-lookup"><span data-stu-id="68103-148">None</span></span>

### <a name="request-example"></a><span data-ttu-id="68103-149">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="68103-149">Request example</span></span>

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies/56edf752-ee77-4fd8-b7f5-df1f74a3a9ac HTTP/1.1
Authorization: Bearer <token>
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 0
Content-Type: application/json
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="68103-150">REST-svar</span><span class="sxs-lookup"><span data-stu-id="68103-150">REST response</span></span>

<span data-ttu-id="68103-151">Om det lyckas returnerar svaret en 204-innehålls status kod.</span><span class="sxs-lookup"><span data-stu-id="68103-151">If successful, the response returns a 204 No Content status code.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="68103-152">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="68103-152">Response success and error codes</span></span>

<span data-ttu-id="68103-153">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="68103-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="68103-154">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="68103-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="68103-155">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="68103-155">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="68103-156">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="68103-156">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: cee5caf4-c322-4baa-b1d7-e94afb9891a4
MS-RequestId: 76b6f317-1da1-4b61-a6fd-9952439a2c46
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:10:41 GMT
```
