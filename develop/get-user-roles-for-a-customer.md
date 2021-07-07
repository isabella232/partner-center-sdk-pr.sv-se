---
title: Hämta användarroller för en kund
description: Hämta en lista över alla roller/behörigheter som är kopplade till ett användarkonto. Varianter inkluderar att hämta en lista över alla behörigheter för alla användarkonton för en kund och hämta en lista över användare som har en viss roll.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8f58e8b7eae5bb47265bb1ac83fcdcd160f735d2
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445926"
---
# <a name="get-user-roles-for-a-customer"></a><span data-ttu-id="e5c7d-104">Hämta användarroller för en kund</span><span class="sxs-lookup"><span data-stu-id="e5c7d-104">Get user roles for a customer</span></span>

<span data-ttu-id="e5c7d-105">Hämta en lista över alla roller/behörigheter som är kopplade till ett användarkonto.</span><span class="sxs-lookup"><span data-stu-id="e5c7d-105">Get a list of all the roles/permissions attached to a user account.</span></span> <span data-ttu-id="e5c7d-106">Varianter inkluderar att hämta en lista över alla behörigheter för alla användarkonton för en kund och hämta en lista över användare som har en viss roll.</span><span class="sxs-lookup"><span data-stu-id="e5c7d-106">Variations include getting a list of all permissions across all user accounts for a customer, and getting a list of users that have a given role.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e5c7d-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="e5c7d-107">Prerequisites</span></span>

- <span data-ttu-id="e5c7d-108">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="e5c7d-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e5c7d-109">Det här scenariot har endast stöd för autentisering med app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="e5c7d-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="e5c7d-110">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e5c7d-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="e5c7d-111">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="e5c7d-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="e5c7d-112">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="e5c7d-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="e5c7d-113">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="e5c7d-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="e5c7d-114">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="e5c7d-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="e5c7d-115">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e5c7d-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="e5c7d-116">C\#</span><span class="sxs-lookup"><span data-stu-id="e5c7d-116">C\#</span></span>

<span data-ttu-id="e5c7d-117">Om du vill hämta alla katalogroller för en angiven kund hämtar du först det angivna kund-ID:t.</span><span class="sxs-lookup"><span data-stu-id="e5c7d-117">To retrieve all the directory roles for a specified customer, first retrieve the specified customer ID.</span></span> <span data-ttu-id="e5c7d-118">Använd sedan din **IAggregatePartner.Customers-samling** och anropa **metoden ById().**</span><span class="sxs-lookup"><span data-stu-id="e5c7d-118">Then, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="e5c7d-119">Anropa sedan egenskapen **DirectoryRoles** följt av metoden **Get()** eller **GetAsync().**</span><span class="sxs-lookup"><span data-stu-id="e5c7d-119">Then call the **DirectoryRoles** property, followed by the **Get()** or **GetAsync()** method.</span></span>

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

var directoryRoles = partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.Get();
```

<span data-ttu-id="e5c7d-120">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="e5c7d-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="e5c7d-121">**Project:** Partnercenter-SDK Samples **Class**: GetCustomerDirectoryRoles.cs</span><span class="sxs-lookup"><span data-stu-id="e5c7d-121">**Project**: Partner Center SDK Samples **Class**: GetCustomerDirectoryRoles.cs</span></span>

<span data-ttu-id="e5c7d-122">Om du vill hämta en lista över kundanvändare som har en viss roll hämtar du först det angivna kund-ID:t och katalogrolls-ID:t.</span><span class="sxs-lookup"><span data-stu-id="e5c7d-122">To retrieve a list of customer users that have a given role, first retrieve the specified customer ID and the directory role ID.</span></span> <span data-ttu-id="e5c7d-123">Använd sedan din **IAggregatePartner.Customers-samling** och anropa **metoden ById().**</span><span class="sxs-lookup"><span data-stu-id="e5c7d-123">Then, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="e5c7d-124">Anropa sedan **egenskapen DirectoryRoles,** sedan **metoden ById()** och sedan egenskapen **UserMembers** följt av metoden **Get()** eller **GetAsync().**</span><span class="sxs-lookup"><span data-stu-id="e5c7d-124">Then call the **DirectoryRoles** property, then **ById()** method, then the **UserMembers** property, the followed by the **Get()** or **GetAsync()** method.</span></span>

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;
// string selectedDirectoryRoleId;

var userMembers = partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.ById(selectedDirectoryRoleId).UserMembers.Get();
```

<span data-ttu-id="e5c7d-125">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="e5c7d-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="e5c7d-126">**Project:** PartnerSDK.FeatureSamples-klass: GetCustomerDirectoryRoleUserMembers.cs </span><span class="sxs-lookup"><span data-stu-id="e5c7d-126">**Project**: PartnerSDK.FeatureSamples **Class**: GetCustomerDirectoryRoleUserMembers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="e5c7d-127">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="e5c7d-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e5c7d-128">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="e5c7d-128">Request syntax</span></span>

| <span data-ttu-id="e5c7d-129">Metod</span><span class="sxs-lookup"><span data-stu-id="e5c7d-129">Method</span></span>  | <span data-ttu-id="e5c7d-130">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="e5c7d-130">Request URI</span></span>                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e5c7d-131">**Få**</span><span class="sxs-lookup"><span data-stu-id="e5c7d-131">**GET**</span></span> | <span data-ttu-id="e5c7d-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id}/directoryroles HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e5c7d-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id}/directoryroles HTTP/1.1</span></span> |
| <span data-ttu-id="e5c7d-133">**Få**</span><span class="sxs-lookup"><span data-stu-id="e5c7d-133">**GET**</span></span> | <span data-ttu-id="e5c7d-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e5c7d-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles HTTP/1.1</span></span>                 |
| <span data-ttu-id="e5c7d-135">**Få**</span><span class="sxs-lookup"><span data-stu-id="e5c7d-135">**GET**</span></span> | <span data-ttu-id="e5c7d-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{role-ID}/usermembers</span><span class="sxs-lookup"><span data-stu-id="e5c7d-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{role-ID}/usermembers</span></span>    |

### <a name="uri-parameter"></a><span data-ttu-id="e5c7d-137">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="e5c7d-137">URI parameter</span></span>

<span data-ttu-id="e5c7d-138">Använd följande frågeparameter för att identifiera rätt kund.</span><span class="sxs-lookup"><span data-stu-id="e5c7d-138">Use the following query parameter to identify the correct customer.</span></span>

| <span data-ttu-id="e5c7d-139">Namn</span><span class="sxs-lookup"><span data-stu-id="e5c7d-139">Name</span></span>                   | <span data-ttu-id="e5c7d-140">Typ</span><span class="sxs-lookup"><span data-stu-id="e5c7d-140">Type</span></span>     | <span data-ttu-id="e5c7d-141">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="e5c7d-141">Required</span></span> | <span data-ttu-id="e5c7d-142">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="e5c7d-142">Description</span></span>                                                                                                                                                                                                 |
|------------------------|----------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e5c7d-143">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="e5c7d-143">**customer-tenant-id**</span></span> | <span data-ttu-id="e5c7d-144">**guid**</span><span class="sxs-lookup"><span data-stu-id="e5c7d-144">**guid**</span></span> | <span data-ttu-id="e5c7d-145">Y</span><span class="sxs-lookup"><span data-stu-id="e5c7d-145">Y</span></span>        | <span data-ttu-id="e5c7d-146">Värdet är ett GUID-formaterat **kundklient-ID** som gör att återförsäljaren kan filtrera resultaten för en viss kund som tillhör återförsäljaren.</span><span class="sxs-lookup"><span data-stu-id="e5c7d-146">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span>                                                      |
| <span data-ttu-id="e5c7d-147">**användar-id**</span><span class="sxs-lookup"><span data-stu-id="e5c7d-147">**user-id**</span></span>            | <span data-ttu-id="e5c7d-148">**guid**</span><span class="sxs-lookup"><span data-stu-id="e5c7d-148">**guid**</span></span> | <span data-ttu-id="e5c7d-149">N</span><span class="sxs-lookup"><span data-stu-id="e5c7d-149">N</span></span>        | <span data-ttu-id="e5c7d-150">Värdet är ett GUID-formaterat **användar-ID** som tillhör ett enda användarkonto.</span><span class="sxs-lookup"><span data-stu-id="e5c7d-150">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                                                                                                            |
| <span data-ttu-id="e5c7d-151">**roll-id**</span><span class="sxs-lookup"><span data-stu-id="e5c7d-151">**role-id**</span></span>            | <span data-ttu-id="e5c7d-152">**guid**</span><span class="sxs-lookup"><span data-stu-id="e5c7d-152">**guid**</span></span> | <span data-ttu-id="e5c7d-153">N</span><span class="sxs-lookup"><span data-stu-id="e5c7d-153">N</span></span>        | <span data-ttu-id="e5c7d-154">Värdet är ett GUID-formaterat **roll-ID** som tillhör en typ av roll.</span><span class="sxs-lookup"><span data-stu-id="e5c7d-154">The value is a GUID formatted **role-id** that belongs to a type of role.</span></span> <span data-ttu-id="e5c7d-155">Du kan hämta dessa ID:er genom att fråga alla katalogroller för en kund, för alla användarkonton.</span><span class="sxs-lookup"><span data-stu-id="e5c7d-155">You can get these IDs by querying all the directory roles for a customer, across all user accounts.</span></span> <span data-ttu-id="e5c7d-156">(Det andra scenariot ovan).</span><span class="sxs-lookup"><span data-stu-id="e5c7d-156">(The second scenario, above).</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e5c7d-157">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="e5c7d-157">Request headers</span></span>

<span data-ttu-id="e5c7d-158">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="e5c7d-158">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e5c7d-159">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="e5c7d-159">Request body</span></span>

### <a name="request-example"></a><span data-ttu-id="e5c7d-160">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="e5c7d-160">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/users/<user-id>/directoryroles HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
```

## <a name="rest-response"></a><span data-ttu-id="e5c7d-161">REST-svar</span><span class="sxs-lookup"><span data-stu-id="e5c7d-161">REST response</span></span>

<span data-ttu-id="e5c7d-162">Om det lyckas returnerar den här metoden en lista över de roller som är associerade med det angivna användarkontot.</span><span class="sxs-lookup"><span data-stu-id="e5c7d-162">If successful, this method returns a list of the roles associated with the given user account.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e5c7d-163">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="e5c7d-163">Response success and error codes</span></span>

<span data-ttu-id="e5c7d-164">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="e5c7d-164">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e5c7d-165">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="e5c7d-165">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e5c7d-166">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="e5c7d-166">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e5c7d-167">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="e5c7d-167">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 31942
Content-Type: application/json
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
Date: June 24 2016 22:00:25 PST

{
      "totalCount": 2,
      "items": [
        {
          "name": "Helpdesk Administrator",
          "id": "729827e3-9c14-49f7-bb1b-9608f156bbb8",
          "attributes": { "objectType": "DirectoryRole" }
        },
        {
          "name": "User Account Administrator",
          "id": "fe930be7-5e62-47db-91af-98c3a49a38b1",
          "attributes": { "objectType": "DirectoryRole" }
        }
      ],
      "attributes": { "objectType": "Collection" }
}
```
