---
title: Ange användarroller för en kund
description: Det finns en uppsättning katalog roller inom ett kund konto. Du kan tilldela användar konton till dessa roller.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f42120e40e54ff8bd6242634d97268091abf8e1c
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769591"
---
# <a name="set-user-roles-for-a-customer"></a><span data-ttu-id="e55a1-104">Ange användarroller för en kund</span><span class="sxs-lookup"><span data-stu-id="e55a1-104">Set user roles for a customer</span></span>

<span data-ttu-id="e55a1-105">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="e55a1-105">**Applies To**</span></span>

- <span data-ttu-id="e55a1-106">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="e55a1-106">Partner Center</span></span>

<span data-ttu-id="e55a1-107">Det finns en uppsättning katalog roller inom ett kund konto.</span><span class="sxs-lookup"><span data-stu-id="e55a1-107">Within a customer account, there's a set of directory roles.</span></span> <span data-ttu-id="e55a1-108">Du kan tilldela användar konton till dessa roller.</span><span class="sxs-lookup"><span data-stu-id="e55a1-108">You can assign user accounts to those roles.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e55a1-109">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="e55a1-109">Prerequisites</span></span>

- <span data-ttu-id="e55a1-110">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e55a1-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e55a1-111">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="e55a1-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="e55a1-112">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e55a1-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="e55a1-113">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="e55a1-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="e55a1-114">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="e55a1-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="e55a1-115">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="e55a1-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="e55a1-116">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="e55a1-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="e55a1-117">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e55a1-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="e55a1-118">C\#</span><span class="sxs-lookup"><span data-stu-id="e55a1-118">C\#</span></span>

<span data-ttu-id="e55a1-119">Om du vill tilldela en katalog roll till en kund användare skapar du en ny [**UserMember**](/dotnet/api/microsoft.store.partnercenter.models.roles.usermember) med relevanta användar uppgifter.</span><span class="sxs-lookup"><span data-stu-id="e55a1-119">To assign a directory role to a customer user, create a new [**UserMember**](/dotnet/api/microsoft.store.partnercenter.models.roles.usermember) with the relevant user details.</span></span> <span data-ttu-id="e55a1-120">Anropa sedan metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med det angivna kund-ID: t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="e55a1-120">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the specified customer ID to identify the customer.</span></span> <span data-ttu-id="e55a1-121">Därifrån använder du metoden [**DirectoryRoles. ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) med katalog roll-ID: t för att ange rollen.</span><span class="sxs-lookup"><span data-stu-id="e55a1-121">From there, use the [**DirectoryRoles.ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) method with the directory role ID to specify the role.</span></span> <span data-ttu-id="e55a1-122">Öppna sedan **UserMembers** -samlingen och Använd [**create**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.create) -metoden för att lägga till den nya användar medlemmen i samlingen av användar medlemmar som tilldelats rollen.</span><span class="sxs-lookup"><span data-stu-id="e55a1-122">Then, access the **UserMembers** collection, and use the [**Create**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.create) method to add the new user member to the collection of user members assigned to that role.</span></span>

``` csharp
// UserMember createdUser;
// IAggregatePartner partnerOperations;
// Customer selectedCustomer;
// IDirectoryRole selectedRole;

// Create the new user member.
UserMember userMemberToAdd = new UserMember()
{
    UserPrincipalName = createdUser.UserPrincipalName,
    DisplayName = createdUser.DisplayName,
    Id = createdUser.Id
};

// Add the new user member to the role.
var userMemberAdded = partnerOperations.Customers.ById(selectedCustomer.Id).DirectoryRoles.ById(selectedRole.Id).UserMembers.Create(userMemberToAdd);
```

<span data-ttu-id="e55a1-123">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="e55a1-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="e55a1-124">**Projekt**: Partner Center SDK-exempel **klass**: AddUserMemberToDirectoryRole.CS</span><span class="sxs-lookup"><span data-stu-id="e55a1-124">**Project**: Partner Center SDK Samples **Class**: AddUserMemberToDirectoryRole.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="e55a1-125">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="e55a1-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e55a1-126">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="e55a1-126">Request syntax</span></span>

| <span data-ttu-id="e55a1-127">Metod</span><span class="sxs-lookup"><span data-stu-id="e55a1-127">Method</span></span>   | <span data-ttu-id="e55a1-128">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="e55a1-128">Request URI</span></span>                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e55a1-129">**EFTER**</span><span class="sxs-lookup"><span data-stu-id="e55a1-129">**POST**</span></span> | <span data-ttu-id="e55a1-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/directoryroles/{Role-ID}/usermembers http/1.1</span><span class="sxs-lookup"><span data-stu-id="e55a1-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{role-ID}/usermembers HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="e55a1-131">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="e55a1-131">URI parameter</span></span>

<span data-ttu-id="e55a1-132">Använd följande URI-parametrar för att identifiera rätt kund och roll.</span><span class="sxs-lookup"><span data-stu-id="e55a1-132">Use the following URI parameters to identify the correct customer and role.</span></span> <span data-ttu-id="e55a1-133">Identifiera den användare som du vill tilldela rollen genom att ange identifierings informationen i begär ande texten.</span><span class="sxs-lookup"><span data-stu-id="e55a1-133">To identify the user to whom to assign the role, supply the identifying information in the request body.</span></span>

| <span data-ttu-id="e55a1-134">Namn</span><span class="sxs-lookup"><span data-stu-id="e55a1-134">Name</span></span>                   | <span data-ttu-id="e55a1-135">Typ</span><span class="sxs-lookup"><span data-stu-id="e55a1-135">Type</span></span>     | <span data-ttu-id="e55a1-136">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="e55a1-136">Required</span></span> | <span data-ttu-id="e55a1-137">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="e55a1-137">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e55a1-138">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="e55a1-138">**customer-tenant-id**</span></span> | <span data-ttu-id="e55a1-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="e55a1-139">**guid**</span></span> | <span data-ttu-id="e55a1-140">Y</span><span class="sxs-lookup"><span data-stu-id="e55a1-140">Y</span></span>        | <span data-ttu-id="e55a1-141">Värdet är ett GUID-formaterat **kund-Tenant-ID** som gör det möjligt för åter försäljaren att filtrera resultaten för en specifik kund som tillhör åter försäljaren.</span><span class="sxs-lookup"><span data-stu-id="e55a1-141">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="e55a1-142">**roll-ID**</span><span class="sxs-lookup"><span data-stu-id="e55a1-142">**role-id**</span></span>            | <span data-ttu-id="e55a1-143">**guid**</span><span class="sxs-lookup"><span data-stu-id="e55a1-143">**guid**</span></span> | <span data-ttu-id="e55a1-144">Y</span><span class="sxs-lookup"><span data-stu-id="e55a1-144">Y</span></span>        | <span data-ttu-id="e55a1-145">Värdet är ett GUID-formaterat **roll-ID** som identifierar den roll som ska tilldelas användaren.</span><span class="sxs-lookup"><span data-stu-id="e55a1-145">The value is a GUID formatted **role-id** that identifies the role to assign to the user.</span></span>                                                              |

### <a name="request-headers"></a><span data-ttu-id="e55a1-146">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="e55a1-146">Request headers</span></span>

<span data-ttu-id="e55a1-147">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="e55a1-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e55a1-148">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="e55a1-148">Request body</span></span>

<span data-ttu-id="e55a1-149">I den här tabellen beskrivs de egenskaper som krävs i begär ande texten.</span><span class="sxs-lookup"><span data-stu-id="e55a1-149">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="e55a1-150">Namn</span><span class="sxs-lookup"><span data-stu-id="e55a1-150">Name</span></span>                  | <span data-ttu-id="e55a1-151">Typ</span><span class="sxs-lookup"><span data-stu-id="e55a1-151">Type</span></span>       | <span data-ttu-id="e55a1-152">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="e55a1-152">Required</span></span> | <span data-ttu-id="e55a1-153">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="e55a1-153">Description</span></span>                            |
|-----------------------|------------|----------|----------------------------------------|
| <span data-ttu-id="e55a1-154">**Identitet**</span><span class="sxs-lookup"><span data-stu-id="e55a1-154">**Id**</span></span>                | <span data-ttu-id="e55a1-155">**nollängd**</span><span class="sxs-lookup"><span data-stu-id="e55a1-155">**string**</span></span> | <span data-ttu-id="e55a1-156">Y</span><span class="sxs-lookup"><span data-stu-id="e55a1-156">Y</span></span>        | <span data-ttu-id="e55a1-157">ID för den användare som ska läggas till i rollen.</span><span class="sxs-lookup"><span data-stu-id="e55a1-157">The Id of the user to add to the role.</span></span> |
| <span data-ttu-id="e55a1-158">**DisplayName**</span><span class="sxs-lookup"><span data-stu-id="e55a1-158">**DisplayName**</span></span>       | <span data-ttu-id="e55a1-159">**nollängd**</span><span class="sxs-lookup"><span data-stu-id="e55a1-159">**string**</span></span> | <span data-ttu-id="e55a1-160">Y</span><span class="sxs-lookup"><span data-stu-id="e55a1-160">Y</span></span>        | <span data-ttu-id="e55a1-161">Användarens användarvänliga visnings namn.</span><span class="sxs-lookup"><span data-stu-id="e55a1-161">The friendly display name of the user.</span></span> |
| <span data-ttu-id="e55a1-162">**UserPrincipalName**</span><span class="sxs-lookup"><span data-stu-id="e55a1-162">**UserPrincipalName**</span></span> | <span data-ttu-id="e55a1-163">**nollängd**</span><span class="sxs-lookup"><span data-stu-id="e55a1-163">**string**</span></span> | <span data-ttu-id="e55a1-164">Y</span><span class="sxs-lookup"><span data-stu-id="e55a1-164">Y</span></span>        | <span data-ttu-id="e55a1-165">Namnet på användarens huvud namn.</span><span class="sxs-lookup"><span data-stu-id="e55a1-165">The name of the user principal.</span></span>        |
| <span data-ttu-id="e55a1-166">**Attribut**</span><span class="sxs-lookup"><span data-stu-id="e55a1-166">**Attributes**</span></span>        | <span data-ttu-id="e55a1-167">**jobbobjektet**</span><span class="sxs-lookup"><span data-stu-id="e55a1-167">**object**</span></span> | <span data-ttu-id="e55a1-168">Y</span><span class="sxs-lookup"><span data-stu-id="e55a1-168">Y</span></span>        | <span data-ttu-id="e55a1-169">Innehåller "ObjectType": "UserMember"</span><span class="sxs-lookup"><span data-stu-id="e55a1-169">Contains "ObjectType":"UserMember"</span></span>     |

### <a name="request-example"></a><span data-ttu-id="e55a1-170">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="e55a1-170">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/directoryroles/f023fd81-a637-4b56-95fd-791ac0226033/usermembers HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a56cb2e5-a156-4f68-9155-57ffe2b93d18
MS-CorrelationId: 90bda268-7929-4ad6-be01-89c5af5fc504
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 180
Expect: 100-continue

{
    "Id": "a9ef48bb-8758-4590-a312-d4a47bfaded4",
    "DisplayName": "Daniel Tsai",
    "UserPrincipalName": "Daniel@dtdemocspcustomer005.onmicrosoft.com",
    "Attributes": {
        "ObjectType": "UserMember"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="e55a1-171">REST-svar</span><span class="sxs-lookup"><span data-stu-id="e55a1-171">REST response</span></span>

<span data-ttu-id="e55a1-172">Den här metoden returnerar användar kontot med det roll-ID som är kopplat när användaren har tilldelat rollen.</span><span class="sxs-lookup"><span data-stu-id="e55a1-172">This method returns the user account with the role id attached when the user is successfully assigned the role.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e55a1-173">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="e55a1-173">Response success and error codes</span></span>

<span data-ttu-id="e55a1-174">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="e55a1-174">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e55a1-175">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="e55a1-175">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e55a1-176">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e55a1-176">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e55a1-177">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="e55a1-177">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 231
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 90bda268-7929-4ad6-be01-89c5af5fc504
MS-RequestId: a56cb2e5-a156-4f68-9155-57ffe2b93d18
MS-CV: aia94+gnrEeQqkGr.0
MS-ServerId: 101112202
Date: Tue, 20 Dec 2016 23:36:55 GMT

{
    "displayName": "Daniel Tsai",
    "userPrincipalName": "Daniel@dtdemocspcustomer005.onmicrosoft.com",
    "roleId": "f023fd81-a637-4b56-95fd-791ac0226033",
    "id": "a9ef48bb-8758-4590-a312-d4a47bfaded4",
    "attributes": {
        "objectType": "UserMember"
    }
}
```
