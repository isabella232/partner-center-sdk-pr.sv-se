---
title: Ange användarroller för en kund
description: Det finns en uppsättning katalogroller i ett kundkonto. Du kan tilldela användarkonton till dessa roller.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a035d711ffa91200fa7b479ed5ec53929aa4feaf
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446708"
---
# <a name="set-user-roles-for-a-customer"></a><span data-ttu-id="1d0ed-104">Ange användarroller för en kund</span><span class="sxs-lookup"><span data-stu-id="1d0ed-104">Set user roles for a customer</span></span>

<span data-ttu-id="1d0ed-105">Det finns en uppsättning katalogroller i ett kundkonto.</span><span class="sxs-lookup"><span data-stu-id="1d0ed-105">Within a customer account, there's a set of directory roles.</span></span> <span data-ttu-id="1d0ed-106">Du kan tilldela användarkonton till dessa roller.</span><span class="sxs-lookup"><span data-stu-id="1d0ed-106">You can assign user accounts to those roles.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1d0ed-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="1d0ed-107">Prerequisites</span></span>

- <span data-ttu-id="1d0ed-108">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="1d0ed-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1d0ed-109">Det här scenariot har endast stöd för autentisering med app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="1d0ed-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="1d0ed-110">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1d0ed-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="1d0ed-111">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="1d0ed-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="1d0ed-112">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="1d0ed-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="1d0ed-113">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="1d0ed-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="1d0ed-114">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="1d0ed-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="1d0ed-115">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1d0ed-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="1d0ed-116">C\#</span><span class="sxs-lookup"><span data-stu-id="1d0ed-116">C\#</span></span>

<span data-ttu-id="1d0ed-117">Om du vill tilldela en katalogroll till en kundanvändare skapar du en [**ny UserMember**](/dotnet/api/microsoft.store.partnercenter.models.roles.usermember) med relevant användarinformation.</span><span class="sxs-lookup"><span data-stu-id="1d0ed-117">To assign a directory role to a customer user, create a new [**UserMember**](/dotnet/api/microsoft.store.partnercenter.models.roles.usermember) with the relevant user details.</span></span> <span data-ttu-id="1d0ed-118">Anropa sedan metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med det angivna kund-ID:t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="1d0ed-118">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the specified customer ID to identify the customer.</span></span> <span data-ttu-id="1d0ed-119">Därifrån använder du metoden [**DirectoryRoles.ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) med katalogrolls-ID:t för att ange rollen.</span><span class="sxs-lookup"><span data-stu-id="1d0ed-119">From there, use the [**DirectoryRoles.ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) method with the directory role ID to specify the role.</span></span> <span data-ttu-id="1d0ed-120">Öppna sedan **samlingen UserMembers** och använd metoden [**Skapa**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.create) för att lägga till den nya användarmedlemmen i den samling av användarmedlemmar som tilldelats rollen.</span><span class="sxs-lookup"><span data-stu-id="1d0ed-120">Then, access the **UserMembers** collection, and use the [**Create**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.create) method to add the new user member to the collection of user members assigned to that role.</span></span>

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

<span data-ttu-id="1d0ed-121">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="1d0ed-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="1d0ed-122">**Project:** Partnercenter-SDK Samples **Class**: AddUserMemberToDirectoryRole.cs</span><span class="sxs-lookup"><span data-stu-id="1d0ed-122">**Project**: Partner Center SDK Samples **Class**: AddUserMemberToDirectoryRole.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="1d0ed-123">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="1d0ed-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1d0ed-124">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="1d0ed-124">Request syntax</span></span>

| <span data-ttu-id="1d0ed-125">Metod</span><span class="sxs-lookup"><span data-stu-id="1d0ed-125">Method</span></span>   | <span data-ttu-id="1d0ed-126">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="1d0ed-126">Request URI</span></span>                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1d0ed-127">**Inlägg**</span><span class="sxs-lookup"><span data-stu-id="1d0ed-127">**POST**</span></span> | <span data-ttu-id="1d0ed-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{role-ID}/usermembers HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="1d0ed-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{role-ID}/usermembers HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="1d0ed-129">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="1d0ed-129">URI parameter</span></span>

<span data-ttu-id="1d0ed-130">Använd följande URI-parametrar för att identifiera rätt kund och roll.</span><span class="sxs-lookup"><span data-stu-id="1d0ed-130">Use the following URI parameters to identify the correct customer and role.</span></span> <span data-ttu-id="1d0ed-131">Om du vill identifiera den användare som rollen ska tilldelas till anger du den identifierande informationen i begärandetexten.</span><span class="sxs-lookup"><span data-stu-id="1d0ed-131">To identify the user to whom to assign the role, supply the identifying information in the request body.</span></span>

| <span data-ttu-id="1d0ed-132">Namn</span><span class="sxs-lookup"><span data-stu-id="1d0ed-132">Name</span></span>                   | <span data-ttu-id="1d0ed-133">Typ</span><span class="sxs-lookup"><span data-stu-id="1d0ed-133">Type</span></span>     | <span data-ttu-id="1d0ed-134">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="1d0ed-134">Required</span></span> | <span data-ttu-id="1d0ed-135">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="1d0ed-135">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1d0ed-136">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="1d0ed-136">**customer-tenant-id**</span></span> | <span data-ttu-id="1d0ed-137">**guid**</span><span class="sxs-lookup"><span data-stu-id="1d0ed-137">**guid**</span></span> | <span data-ttu-id="1d0ed-138">Y</span><span class="sxs-lookup"><span data-stu-id="1d0ed-138">Y</span></span>        | <span data-ttu-id="1d0ed-139">Värdet är ett GUID-formaterat **kundklient-ID** som gör att återförsäljaren kan filtrera resultaten för en viss kund som tillhör återförsäljaren.</span><span class="sxs-lookup"><span data-stu-id="1d0ed-139">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="1d0ed-140">**roll-id**</span><span class="sxs-lookup"><span data-stu-id="1d0ed-140">**role-id**</span></span>            | <span data-ttu-id="1d0ed-141">**guid**</span><span class="sxs-lookup"><span data-stu-id="1d0ed-141">**guid**</span></span> | <span data-ttu-id="1d0ed-142">Y</span><span class="sxs-lookup"><span data-stu-id="1d0ed-142">Y</span></span>        | <span data-ttu-id="1d0ed-143">Värdet är ett GUID-formaterat **roll-ID** som identifierar rollen som ska tilldelas användaren.</span><span class="sxs-lookup"><span data-stu-id="1d0ed-143">The value is a GUID formatted **role-id** that identifies the role to assign to the user.</span></span>                                                              |

### <a name="request-headers"></a><span data-ttu-id="1d0ed-144">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="1d0ed-144">Request headers</span></span>

<span data-ttu-id="1d0ed-145">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="1d0ed-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1d0ed-146">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="1d0ed-146">Request body</span></span>

<span data-ttu-id="1d0ed-147">I den här tabellen beskrivs de obligatoriska egenskaperna i begärandetexten.</span><span class="sxs-lookup"><span data-stu-id="1d0ed-147">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="1d0ed-148">Namn</span><span class="sxs-lookup"><span data-stu-id="1d0ed-148">Name</span></span>                  | <span data-ttu-id="1d0ed-149">Typ</span><span class="sxs-lookup"><span data-stu-id="1d0ed-149">Type</span></span>       | <span data-ttu-id="1d0ed-150">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="1d0ed-150">Required</span></span> | <span data-ttu-id="1d0ed-151">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="1d0ed-151">Description</span></span>                            |
|-----------------------|------------|----------|----------------------------------------|
| <span data-ttu-id="1d0ed-152">**Id**</span><span class="sxs-lookup"><span data-stu-id="1d0ed-152">**Id**</span></span>                | <span data-ttu-id="1d0ed-153">**sträng**</span><span class="sxs-lookup"><span data-stu-id="1d0ed-153">**string**</span></span> | <span data-ttu-id="1d0ed-154">Y</span><span class="sxs-lookup"><span data-stu-id="1d0ed-154">Y</span></span>        | <span data-ttu-id="1d0ed-155">ID för den användare som ska läggas till i rollen.</span><span class="sxs-lookup"><span data-stu-id="1d0ed-155">The ID of the user to add to the role.</span></span> |
| <span data-ttu-id="1d0ed-156">**DisplayName**</span><span class="sxs-lookup"><span data-stu-id="1d0ed-156">**DisplayName**</span></span>       | <span data-ttu-id="1d0ed-157">**sträng**</span><span class="sxs-lookup"><span data-stu-id="1d0ed-157">**string**</span></span> | <span data-ttu-id="1d0ed-158">Y</span><span class="sxs-lookup"><span data-stu-id="1d0ed-158">Y</span></span>        | <span data-ttu-id="1d0ed-159">Användarens egna visningsnamn.</span><span class="sxs-lookup"><span data-stu-id="1d0ed-159">The friendly display name of the user.</span></span> |
| <span data-ttu-id="1d0ed-160">**UserPrincipalName**</span><span class="sxs-lookup"><span data-stu-id="1d0ed-160">**UserPrincipalName**</span></span> | <span data-ttu-id="1d0ed-161">**sträng**</span><span class="sxs-lookup"><span data-stu-id="1d0ed-161">**string**</span></span> | <span data-ttu-id="1d0ed-162">Y</span><span class="sxs-lookup"><span data-stu-id="1d0ed-162">Y</span></span>        | <span data-ttu-id="1d0ed-163">Namnet på användarens huvudnamn.</span><span class="sxs-lookup"><span data-stu-id="1d0ed-163">The name of the user principal.</span></span>        |
| <span data-ttu-id="1d0ed-164">**Attribut**</span><span class="sxs-lookup"><span data-stu-id="1d0ed-164">**Attributes**</span></span>        | <span data-ttu-id="1d0ed-165">**Objekt**</span><span class="sxs-lookup"><span data-stu-id="1d0ed-165">**object**</span></span> | <span data-ttu-id="1d0ed-166">Y</span><span class="sxs-lookup"><span data-stu-id="1d0ed-166">Y</span></span>        | <span data-ttu-id="1d0ed-167">Innehåller "ObjectType":"UserMember"</span><span class="sxs-lookup"><span data-stu-id="1d0ed-167">Contains "ObjectType":"UserMember"</span></span>     |

### <a name="request-example"></a><span data-ttu-id="1d0ed-168">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="1d0ed-168">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="1d0ed-169">REST-svar</span><span class="sxs-lookup"><span data-stu-id="1d0ed-169">REST response</span></span>

<span data-ttu-id="1d0ed-170">Den här metoden returnerar användarkontot med roll-ID:t kopplat när användaren har tilldelats rollen.</span><span class="sxs-lookup"><span data-stu-id="1d0ed-170">This method returns the user account with the role ID attached when the user is successfully assigned the role.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1d0ed-171">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="1d0ed-171">Response success and error codes</span></span>

<span data-ttu-id="1d0ed-172">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="1d0ed-172">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1d0ed-173">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="1d0ed-173">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1d0ed-174">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="1d0ed-174">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1d0ed-175">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="1d0ed-175">Response example</span></span>

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
