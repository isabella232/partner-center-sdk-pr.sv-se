---
title: Ta bort en kundanvändare från en roll
description: Så här tar du bort en användare från en katalog roll i ett kund konto.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6253e86f3733bbf2b9c593c5ca3f3e2fccce7c2c
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769648"
---
# <a name="remove-a-customer-user-from-a-role"></a><span data-ttu-id="d0ae9-103">Ta bort en kundanvändare från en roll</span><span class="sxs-lookup"><span data-stu-id="d0ae9-103">Remove a customer user from a role</span></span>

<span data-ttu-id="d0ae9-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="d0ae9-104">**Applies To**</span></span>

- <span data-ttu-id="d0ae9-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="d0ae9-105">Partner Center</span></span>

<span data-ttu-id="d0ae9-106">Så här tar du bort en användare från en katalog roll i ett kund konto.</span><span class="sxs-lookup"><span data-stu-id="d0ae9-106">How to remove a user from a directory role within a customer account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d0ae9-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="d0ae9-107">Prerequisites</span></span>

- <span data-ttu-id="d0ae9-108">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d0ae9-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d0ae9-109">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="d0ae9-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="d0ae9-110">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d0ae9-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="d0ae9-111">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="d0ae9-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="d0ae9-112">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="d0ae9-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="d0ae9-113">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="d0ae9-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="d0ae9-114">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="d0ae9-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="d0ae9-115">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d0ae9-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="d0ae9-116">C\#</span><span class="sxs-lookup"><span data-stu-id="d0ae9-116">C\#</span></span>

<span data-ttu-id="d0ae9-117">Om du vill ta bort en användare från en katalog roll markerar du kunden med användaren att ändra med ett anrop till metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) , där anger du rollen med hjälp av metoden [**DirectoryRoles. ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) med katalog roll-ID: t.</span><span class="sxs-lookup"><span data-stu-id="d0ae9-117">To remove a user from a directory role, select the customer with the user to modify with a call to the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method, From there, specify the role using the [**DirectoryRoles.ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) method with the directory role ID.</span></span> <span data-ttu-id="d0ae9-118">Öppna sedan metoden [**UserMembers. ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.byid) för att identifiera den användare som ska tas bort och metoden [**Delete**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermember.delete) för att ta bort användaren från rollen.</span><span class="sxs-lookup"><span data-stu-id="d0ae9-118">Then, access the [**UserMembers.ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.byid) method to identify the user to remove, and the [**Delete**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermember.delete) method to remove the user from the role.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedRoleId;
// string selectedUserMemberId;

partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.ById(selectedRoleId).UserMembers.ById(selectedUserMemberId).Delete();
```

<span data-ttu-id="d0ae9-119">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="d0ae9-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="d0ae9-120">**Projekt**: Partner Center SDK-exempel **klass**: RemoveCustomerUserMemberFromDirectoryRole.CS</span><span class="sxs-lookup"><span data-stu-id="d0ae9-120">**Project**: Partner Center SDK Samples **Class**: RemoveCustomerUserMemberFromDirectoryRole.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="d0ae9-121">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="d0ae9-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d0ae9-122">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="d0ae9-122">Request syntax</span></span>

| <span data-ttu-id="d0ae9-123">Metod</span><span class="sxs-lookup"><span data-stu-id="d0ae9-123">Method</span></span>     | <span data-ttu-id="d0ae9-124">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="d0ae9-124">Request URI</span></span>                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d0ae9-125">**TA bort**</span><span class="sxs-lookup"><span data-stu-id="d0ae9-125">**DELETE**</span></span> | <span data-ttu-id="d0ae9-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/directoryroles/{Role-ID}/usermembers/{User-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="d0ae9-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{role-ID}/usermembers/{user-ID} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="d0ae9-127">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="d0ae9-127">URI parameter</span></span>

<span data-ttu-id="d0ae9-128">Använd följande URI-parametrar för att identifiera rätt kund, roll och användare.</span><span class="sxs-lookup"><span data-stu-id="d0ae9-128">Use the following URI parameters to identify the correct customer, role and user.</span></span>

| <span data-ttu-id="d0ae9-129">Namn</span><span class="sxs-lookup"><span data-stu-id="d0ae9-129">Name</span></span>                   | <span data-ttu-id="d0ae9-130">Typ</span><span class="sxs-lookup"><span data-stu-id="d0ae9-130">Type</span></span>     | <span data-ttu-id="d0ae9-131">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="d0ae9-131">Required</span></span> | <span data-ttu-id="d0ae9-132">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="d0ae9-132">Description</span></span>                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| <span data-ttu-id="d0ae9-133">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="d0ae9-133">**customer-tenant-id**</span></span> | <span data-ttu-id="d0ae9-134">**guid**</span><span class="sxs-lookup"><span data-stu-id="d0ae9-134">**guid**</span></span> | <span data-ttu-id="d0ae9-135">Y</span><span class="sxs-lookup"><span data-stu-id="d0ae9-135">Y</span></span>        | <span data-ttu-id="d0ae9-136">Värdet är ett GUID-formaterat **kund-Tenant-ID** som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="d0ae9-136">The value is a GUID formatted **customer-tenant-id** that identifies the customer.</span></span> |
| <span data-ttu-id="d0ae9-137">**roll-ID**</span><span class="sxs-lookup"><span data-stu-id="d0ae9-137">**role-id**</span></span>            | <span data-ttu-id="d0ae9-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="d0ae9-138">**guid**</span></span> | <span data-ttu-id="d0ae9-139">Y</span><span class="sxs-lookup"><span data-stu-id="d0ae9-139">Y</span></span>        | <span data-ttu-id="d0ae9-140">Värdet är ett GUID-formaterat **roll-ID** som identifierar rollen.</span><span class="sxs-lookup"><span data-stu-id="d0ae9-140">The value is a GUID formatted **role-id** that identifies the role.</span></span>                |
| <span data-ttu-id="d0ae9-141">**användar-ID**</span><span class="sxs-lookup"><span data-stu-id="d0ae9-141">**user-id**</span></span>            | <span data-ttu-id="d0ae9-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="d0ae9-142">**guid**</span></span> | <span data-ttu-id="d0ae9-143">Y</span><span class="sxs-lookup"><span data-stu-id="d0ae9-143">Y</span></span>        | <span data-ttu-id="d0ae9-144">Värdet är ett GUID-formaterat **användar-ID** som identifierar ett enskilt användar konto.</span><span class="sxs-lookup"><span data-stu-id="d0ae9-144">The value is a GUID formatted **user-id** that identifies a single user account.</span></span>   |

### <a name="request-headers"></a><span data-ttu-id="d0ae9-145">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="d0ae9-145">Request headers</span></span>

<span data-ttu-id="d0ae9-146">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="d0ae9-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d0ae9-147">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="d0ae9-147">Request body</span></span>

<span data-ttu-id="d0ae9-148">Inga.</span><span class="sxs-lookup"><span data-stu-id="d0ae9-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d0ae9-149">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="d0ae9-149">Request example</span></span>

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04%20/directoryroles/729827e3-9c14-49f7-bb1b-9608f156bbb8/usermembers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04%20 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0a00ec08-6273-46bb-ab6f-14a13959b381
MS-CorrelationId: 87d18a45-81fc-40cf-921a-b91cb82d67fe
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 0
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="d0ae9-150">REST-svar</span><span class="sxs-lookup"><span data-stu-id="d0ae9-150">REST response</span></span>

<span data-ttu-id="d0ae9-151">Svars texten är tom om användaren tas bort från rollen.</span><span class="sxs-lookup"><span data-stu-id="d0ae9-151">If the user is removed from the role successfully, the response body is empty.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d0ae9-152">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="d0ae9-152">Response success and error codes</span></span>

<span data-ttu-id="d0ae9-153">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="d0ae9-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d0ae9-154">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="d0ae9-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d0ae9-155">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="d0ae9-155">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d0ae9-156">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="d0ae9-156">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 90bda268-7929-4ad6-be01-89c5af5fc504
MS-RequestId: e784d7aa-8c8d-45ee-8f97-9e09823d7338
MS-CV: es01VX8do0u2aTXw.0
MS-ServerId: 101112616
Date: Tue, 20 Dec 2016 23:16:35 GMT
```
