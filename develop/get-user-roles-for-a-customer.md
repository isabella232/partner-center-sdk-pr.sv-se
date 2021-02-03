---
title: Hämta användarroller för en kund
description: Hämta en lista över alla roller/behörigheter som är kopplade till ett användar konto. Variationerna omfattar att hämta en lista över alla behörigheter för alla användar konton för en kund och hämta en lista över användare som har en specifik roll.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8dad5c035c08905c3d39052de07ebb912452a16b
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768907"
---
# <a name="get-user-roles-for-a-customer"></a><span data-ttu-id="1fd9f-104">Hämta användarroller för en kund</span><span class="sxs-lookup"><span data-stu-id="1fd9f-104">Get user roles for a customer</span></span>

<span data-ttu-id="1fd9f-105">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="1fd9f-105">**Applies To**</span></span>

- <span data-ttu-id="1fd9f-106">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="1fd9f-106">Partner Center</span></span>

<span data-ttu-id="1fd9f-107">Hämta en lista över alla roller/behörigheter som är kopplade till ett användar konto.</span><span class="sxs-lookup"><span data-stu-id="1fd9f-107">Get a list of all the roles/permissions attached to a user account.</span></span> <span data-ttu-id="1fd9f-108">Variationerna omfattar att hämta en lista över alla behörigheter för alla användar konton för en kund och hämta en lista över användare som har en specifik roll.</span><span class="sxs-lookup"><span data-stu-id="1fd9f-108">Variations include getting a list of all permissions across all user accounts for a customer, and getting a list of users that have a given role.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1fd9f-109">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="1fd9f-109">Prerequisites</span></span>

- <span data-ttu-id="1fd9f-110">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="1fd9f-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1fd9f-111">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="1fd9f-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="1fd9f-112">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1fd9f-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="1fd9f-113">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="1fd9f-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="1fd9f-114">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="1fd9f-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="1fd9f-115">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="1fd9f-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="1fd9f-116">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="1fd9f-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="1fd9f-117">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1fd9f-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="1fd9f-118">C\#</span><span class="sxs-lookup"><span data-stu-id="1fd9f-118">C\#</span></span>

<span data-ttu-id="1fd9f-119">Om du vill hämta alla katalog roller för en angiven kund hämtar du först det angivna kund-ID: t.</span><span class="sxs-lookup"><span data-stu-id="1fd9f-119">To retrieve all the directory roles for a specified customer, first retrieve the specified customer ID.</span></span> <span data-ttu-id="1fd9f-120">Använd sedan din **IAggregatePartner. Customers** -samling och anropa **ById ()-** metoden.</span><span class="sxs-lookup"><span data-stu-id="1fd9f-120">Then, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="1fd9f-121">Anropa sedan egenskapen **DirectoryRoles** följt av metoden **Get ()** eller **GetAsync ()**.</span><span class="sxs-lookup"><span data-stu-id="1fd9f-121">Then call the **DirectoryRoles** property, followed by the **Get()** or **GetAsync()** method.</span></span>

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

var directoryRoles = partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.Get();
```

<span data-ttu-id="1fd9f-122">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="1fd9f-122">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="1fd9f-123">**Projekt**: Partner Center SDK-exempel **klass**: GetCustomerDirectoryRoles.CS</span><span class="sxs-lookup"><span data-stu-id="1fd9f-123">**Project**: Partner Center SDK Samples **Class**: GetCustomerDirectoryRoles.cs</span></span>

<span data-ttu-id="1fd9f-124">Hämta en lista med kund användare som har en viss roll genom att först hämta det angivna kund-ID: t och katalog rollens ID.</span><span class="sxs-lookup"><span data-stu-id="1fd9f-124">To retrieve a list of customer users that have a given role, first retrieve the specified customer ID and the directory role ID.</span></span> <span data-ttu-id="1fd9f-125">Använd sedan din **IAggregatePartner. Customers** -samling och anropa **ById ()-** metoden.</span><span class="sxs-lookup"><span data-stu-id="1fd9f-125">Then, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="1fd9f-126">Anropa sedan egenskapen **DirectoryRoles** , sedan **ById ()** -metoden, sedan egenskapen **UserMembers** , följt av metoden **Get ()** eller **GetAsync ()** .</span><span class="sxs-lookup"><span data-stu-id="1fd9f-126">Then call the **DirectoryRoles** property, then **ById()** method, then the **UserMembers** property, the followed by the **Get()** or **GetAsync()** method.</span></span>

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;
// string selectedDirectoryRoleId;

var userMembers = partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.ById(selectedDirectoryRoleId).UserMembers.Get();
```

<span data-ttu-id="1fd9f-127">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="1fd9f-127">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="1fd9f-128">**Projekt**: PartnerSDK. FeatureSamples- **klass**: GetCustomerDirectoryRoleUserMembers.CS</span><span class="sxs-lookup"><span data-stu-id="1fd9f-128">**Project**: PartnerSDK.FeatureSamples **Class**: GetCustomerDirectoryRoleUserMembers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="1fd9f-129">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="1fd9f-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1fd9f-130">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="1fd9f-130">Request syntax</span></span>

| <span data-ttu-id="1fd9f-131">Metod</span><span class="sxs-lookup"><span data-stu-id="1fd9f-131">Method</span></span>  | <span data-ttu-id="1fd9f-132">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="1fd9f-132">Request URI</span></span>                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1fd9f-133">**TA**</span><span class="sxs-lookup"><span data-stu-id="1fd9f-133">**GET**</span></span> | <span data-ttu-id="1fd9f-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Users/{User-ID}/directoryroles http/1.1</span><span class="sxs-lookup"><span data-stu-id="1fd9f-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id}/directoryroles HTTP/1.1</span></span> |
| <span data-ttu-id="1fd9f-135">**TA**</span><span class="sxs-lookup"><span data-stu-id="1fd9f-135">**GET**</span></span> | <span data-ttu-id="1fd9f-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/directoryroles http/1.1</span><span class="sxs-lookup"><span data-stu-id="1fd9f-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles HTTP/1.1</span></span>                 |
| <span data-ttu-id="1fd9f-137">**TA**</span><span class="sxs-lookup"><span data-stu-id="1fd9f-137">**GET**</span></span> | <span data-ttu-id="1fd9f-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/directoryroles/{Role-ID}/usermembers</span><span class="sxs-lookup"><span data-stu-id="1fd9f-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{role-ID}/usermembers</span></span>    |

### <a name="uri-parameter"></a><span data-ttu-id="1fd9f-139">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="1fd9f-139">URI parameter</span></span>

<span data-ttu-id="1fd9f-140">Använd följande frågeparameter för att identifiera rätt kund.</span><span class="sxs-lookup"><span data-stu-id="1fd9f-140">Use the following query parameter to identify the correct customer.</span></span>

| <span data-ttu-id="1fd9f-141">Namn</span><span class="sxs-lookup"><span data-stu-id="1fd9f-141">Name</span></span>                   | <span data-ttu-id="1fd9f-142">Typ</span><span class="sxs-lookup"><span data-stu-id="1fd9f-142">Type</span></span>     | <span data-ttu-id="1fd9f-143">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="1fd9f-143">Required</span></span> | <span data-ttu-id="1fd9f-144">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="1fd9f-144">Description</span></span>                                                                                                                                                                                                 |
|------------------------|----------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1fd9f-145">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="1fd9f-145">**customer-tenant-id**</span></span> | <span data-ttu-id="1fd9f-146">**guid**</span><span class="sxs-lookup"><span data-stu-id="1fd9f-146">**guid**</span></span> | <span data-ttu-id="1fd9f-147">Y</span><span class="sxs-lookup"><span data-stu-id="1fd9f-147">Y</span></span>        | <span data-ttu-id="1fd9f-148">Värdet är ett GUID-formaterat **kund-Tenant-ID** som gör det möjligt för åter försäljaren att filtrera resultaten för en specifik kund som tillhör åter försäljaren.</span><span class="sxs-lookup"><span data-stu-id="1fd9f-148">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span>                                                      |
| <span data-ttu-id="1fd9f-149">**användar-ID**</span><span class="sxs-lookup"><span data-stu-id="1fd9f-149">**user-id**</span></span>            | <span data-ttu-id="1fd9f-150">**guid**</span><span class="sxs-lookup"><span data-stu-id="1fd9f-150">**guid**</span></span> | <span data-ttu-id="1fd9f-151">N</span><span class="sxs-lookup"><span data-stu-id="1fd9f-151">N</span></span>        | <span data-ttu-id="1fd9f-152">Värdet är ett GUID-formaterat **användar-ID** som tillhör ett enda användar konto.</span><span class="sxs-lookup"><span data-stu-id="1fd9f-152">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                                                                                                            |
| <span data-ttu-id="1fd9f-153">**roll-ID**</span><span class="sxs-lookup"><span data-stu-id="1fd9f-153">**role-id**</span></span>            | <span data-ttu-id="1fd9f-154">**guid**</span><span class="sxs-lookup"><span data-stu-id="1fd9f-154">**guid**</span></span> | <span data-ttu-id="1fd9f-155">N</span><span class="sxs-lookup"><span data-stu-id="1fd9f-155">N</span></span>        | <span data-ttu-id="1fd9f-156">Värdet är ett GUID-formaterat **roll-ID** som tillhör en typ av roll.</span><span class="sxs-lookup"><span data-stu-id="1fd9f-156">The value is a GUID formatted **role-id** that belongs to a type of role.</span></span> <span data-ttu-id="1fd9f-157">Du kan hämta dessa ID: n genom att fråga alla katalog roller för en kund, över alla användar konton.</span><span class="sxs-lookup"><span data-stu-id="1fd9f-157">You can get these IDs by querying all the directory roles for a customer, across all user accounts.</span></span> <span data-ttu-id="1fd9f-158">(Det andra scenariot ovan).</span><span class="sxs-lookup"><span data-stu-id="1fd9f-158">(The second scenario, above).</span></span> |

### <a name="request-headers"></a><span data-ttu-id="1fd9f-159">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="1fd9f-159">Request headers</span></span>

<span data-ttu-id="1fd9f-160">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="1fd9f-160">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1fd9f-161">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="1fd9f-161">Request body</span></span>

### <a name="request-example"></a><span data-ttu-id="1fd9f-162">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="1fd9f-162">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/users/<user-id>/directoryroles HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
```

## <a name="rest-response"></a><span data-ttu-id="1fd9f-163">REST-svar</span><span class="sxs-lookup"><span data-stu-id="1fd9f-163">REST response</span></span>

<span data-ttu-id="1fd9f-164">Om det lyckas returnerar den här metoden en lista över de roller som är associerade med det aktuella användar kontot.</span><span class="sxs-lookup"><span data-stu-id="1fd9f-164">If successful, this method returns a list of the roles associated with the given user account.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1fd9f-165">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="1fd9f-165">Response success and error codes</span></span>

<span data-ttu-id="1fd9f-166">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="1fd9f-166">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1fd9f-167">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="1fd9f-167">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1fd9f-168">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="1fd9f-168">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1fd9f-169">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="1fd9f-169">Response example</span></span>

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
