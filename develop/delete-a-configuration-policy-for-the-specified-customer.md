---
title: Ta bort en konfigurationsprincip för den angivna kunden
description: Ta bort en konfigurationsprincip för en angiven kund och principidentifierare.
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2d6a7d392bd6af6850eb7716528e6745943bb7bb
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973034"
---
# <a name="delete-a-configuration-policy-for-the-specified-customer"></a><span data-ttu-id="f9302-103">Ta bort en konfigurationsprincip för den angivna kunden</span><span class="sxs-lookup"><span data-stu-id="f9302-103">Delete a configuration policy for the specified customer</span></span>

<span data-ttu-id="f9302-104">**Gäller för:** Partner Center-| Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="f9302-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="f9302-105">Ta bort en konfigurationsprincip för en angiven kund och principidentifierare.</span><span class="sxs-lookup"><span data-stu-id="f9302-105">How to delete a configuration policy for a specified customer and policy identifier.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f9302-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="f9302-106">Prerequisites</span></span>

- <span data-ttu-id="f9302-107">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="f9302-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f9302-108">Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="f9302-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="f9302-109">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f9302-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="f9302-110">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="f9302-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="f9302-111">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="f9302-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="f9302-112">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="f9302-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="f9302-113">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="f9302-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="f9302-114">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f9302-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="f9302-115">Principidentifieraren.</span><span class="sxs-lookup"><span data-stu-id="f9302-115">The policy identifier.</span></span>

## <a name="c"></a><span data-ttu-id="f9302-116">C\#</span><span class="sxs-lookup"><span data-stu-id="f9302-116">C\#</span></span>

<span data-ttu-id="f9302-117">Så här tar du bort en konfigurationsprincip för en angiven kund:</span><span class="sxs-lookup"><span data-stu-id="f9302-117">To delete a configuration policy for a specified customer:</span></span>

1. <span data-ttu-id="f9302-118">Anropa metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att hämta ett gränssnitt för åtgärder på den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="f9302-118">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span>

2. <span data-ttu-id="f9302-119">Anropa metoden [**ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) med princip-ID:t för att hämta ett gränssnitt för konfigurationsprincipåtgärder för den angivna principen.</span><span class="sxs-lookup"><span data-stu-id="f9302-119">Call the [**ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) method with the policy ID to retrieve an interface to configuration policy operations for the specified policy.</span></span>

3. <span data-ttu-id="f9302-120">Anropa metoden [**Delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.delete) eller [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.deleteasync) för att ta bort konfigurationsprincipen.</span><span class="sxs-lookup"><span data-stu-id="f9302-120">Call the [**Delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.delete) or [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.deleteasync) method to delete the configuration policy.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedPolicyId;

partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.ById(selectedPolicyId).Delete();
```

<span data-ttu-id="f9302-121">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="f9302-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="f9302-122">**Project:** Partnercenter-SDK Samples **Class**: DeleteConfigurationPolicy.cs</span><span class="sxs-lookup"><span data-stu-id="f9302-122">**Project**: Partner Center SDK Samples **Class**: DeleteConfigurationPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="f9302-123">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="f9302-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f9302-124">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="f9302-124">Request syntax</span></span>

| <span data-ttu-id="f9302-125">Metod</span><span class="sxs-lookup"><span data-stu-id="f9302-125">Method</span></span>     | <span data-ttu-id="f9302-126">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="f9302-126">Request URI</span></span>                                                                                          |
|------------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f9302-127">**Ta bort**</span><span class="sxs-lookup"><span data-stu-id="f9302-127">**DELETE**</span></span> | <span data-ttu-id="f9302-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies/{policy-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="f9302-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies/{policy-id} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="f9302-129">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="f9302-129">URI parameters</span></span>

<span data-ttu-id="f9302-130">Använd följande sökvägsparametrar när du skapar begäran.</span><span class="sxs-lookup"><span data-stu-id="f9302-130">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="f9302-131">Namn</span><span class="sxs-lookup"><span data-stu-id="f9302-131">Name</span></span>        | <span data-ttu-id="f9302-132">Typ</span><span class="sxs-lookup"><span data-stu-id="f9302-132">Type</span></span>   | <span data-ttu-id="f9302-133">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="f9302-133">Required</span></span> | <span data-ttu-id="f9302-134">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="f9302-134">Description</span></span>                                                   |
|-------------|--------|----------|---------------------------------------------------------------|
| <span data-ttu-id="f9302-135">kund-ID</span><span class="sxs-lookup"><span data-stu-id="f9302-135">customer-id</span></span> | <span data-ttu-id="f9302-136">sträng</span><span class="sxs-lookup"><span data-stu-id="f9302-136">string</span></span> | <span data-ttu-id="f9302-137">Ja</span><span class="sxs-lookup"><span data-stu-id="f9302-137">Yes</span></span>      | <span data-ttu-id="f9302-138">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="f9302-138">A GUID-formatted string that identifies the customer.</span></span>         |
| <span data-ttu-id="f9302-139">policy-id</span><span class="sxs-lookup"><span data-stu-id="f9302-139">policy-id</span></span>   | <span data-ttu-id="f9302-140">sträng</span><span class="sxs-lookup"><span data-stu-id="f9302-140">string</span></span> | <span data-ttu-id="f9302-141">Ja</span><span class="sxs-lookup"><span data-stu-id="f9302-141">Yes</span></span>      | <span data-ttu-id="f9302-142">En GUID-formaterad sträng som identifierar den princip som ska tas bort.</span><span class="sxs-lookup"><span data-stu-id="f9302-142">A GUID-formatted string that identifies the policy to delete.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="f9302-143">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="f9302-143">Request headers</span></span>

<span data-ttu-id="f9302-144">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="f9302-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f9302-145">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="f9302-145">Request body</span></span>

<span data-ttu-id="f9302-146">Ingen</span><span class="sxs-lookup"><span data-stu-id="f9302-146">None</span></span>

### <a name="request-example"></a><span data-ttu-id="f9302-147">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="f9302-147">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="f9302-148">REST-svar</span><span class="sxs-lookup"><span data-stu-id="f9302-148">REST response</span></span>

<span data-ttu-id="f9302-149">Om det lyckas returnerar svaret statuskoden 204 Inget innehåll.</span><span class="sxs-lookup"><span data-stu-id="f9302-149">If successful, the response returns a 204 No Content status code.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f9302-150">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="f9302-150">Response success and error codes</span></span>

<span data-ttu-id="f9302-151">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="f9302-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f9302-152">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="f9302-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f9302-153">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="f9302-153">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f9302-154">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="f9302-154">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: cee5caf4-c322-4baa-b1d7-e94afb9891a4
MS-RequestId: 76b6f317-1da1-4b61-a6fd-9952439a2c46
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:10:41 GMT
```
