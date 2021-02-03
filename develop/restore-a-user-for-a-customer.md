---
title: Återställ en borttagen användare för en kund
description: Återställa en borttagen användare med kund-ID och användar-ID.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9fd86a268c804a2fdd5efd67a8982afc043c95a6
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769798"
---
# <a name="restore-a-deleted-user-for-a-customer"></a><span data-ttu-id="d5bab-103">Återställ en borttagen användare för en kund</span><span class="sxs-lookup"><span data-stu-id="d5bab-103">Restore a deleted user for a customer</span></span>

<span data-ttu-id="d5bab-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="d5bab-104">**Applies To**</span></span>

- <span data-ttu-id="d5bab-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="d5bab-105">Partner Center</span></span>

<span data-ttu-id="d5bab-106">Återställa en borttagen **användare** med kund-ID och användar-ID.</span><span class="sxs-lookup"><span data-stu-id="d5bab-106">How to restore a deleted **User** by customer ID and user ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d5bab-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="d5bab-107">Prerequisites</span></span>

- <span data-ttu-id="d5bab-108">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d5bab-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d5bab-109">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="d5bab-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="d5bab-110">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d5bab-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="d5bab-111">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="d5bab-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="d5bab-112">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="d5bab-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="d5bab-113">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="d5bab-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="d5bab-114">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="d5bab-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="d5bab-115">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d5bab-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="d5bab-116">Användar-ID.</span><span class="sxs-lookup"><span data-stu-id="d5bab-116">The user ID.</span></span> <span data-ttu-id="d5bab-117">Om du inte har användar-ID, se [Visa borttagna användare för en kund](view-a-deleted-user.md).</span><span class="sxs-lookup"><span data-stu-id="d5bab-117">If you do not have the user ID, see [View deleted users for a customer](view-a-deleted-user.md).</span></span>

## <a name="when-can-you-restore-a-deleted-user-account"></a><span data-ttu-id="d5bab-118">När kan du återställa ett borttaget användar konto?</span><span class="sxs-lookup"><span data-stu-id="d5bab-118">When can you restore a deleted user account?</span></span>

<span data-ttu-id="d5bab-119">Användar tillstånd är inställt på "inaktiv" när du tar bort ett användar konto.</span><span class="sxs-lookup"><span data-stu-id="d5bab-119">The user state is set to "inactive" when you delete a user account.</span></span> <span data-ttu-id="d5bab-120">Den är på samma sätt i trettio dagar, efter vilken användar kontot och dess associerade data rensas och blir oåterkalleligt.</span><span class="sxs-lookup"><span data-stu-id="d5bab-120">It remains that way for thirty days, after which the user account and its associated data are purged and made unrecoverable.</span></span> <span data-ttu-id="d5bab-121">Du kan bara återställa ett borttaget användar konto under den här trettio dagars perioden.</span><span class="sxs-lookup"><span data-stu-id="d5bab-121">You can only restore a deleted user account during this thirty-day window.</span></span> <span data-ttu-id="d5bab-122">När du har tagit bort och markerat "inaktiv" returneras inte längre användar kontot som medlem i användar samlingen (till exempel med [Hämta en lista över alla användar konton för en kund](get-a-list-of-all-user-accounts-for-a-customer.md)).</span><span class="sxs-lookup"><span data-stu-id="d5bab-122">Once deleted and marked "inactive" the user account is no longer returned as a member of the user collection (for example, using [Get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md)).</span></span>

## <a name="c"></a><span data-ttu-id="d5bab-123">C\#</span><span class="sxs-lookup"><span data-stu-id="d5bab-123">C\#</span></span>

<span data-ttu-id="d5bab-124">Om du vill återställa en användare skapar du en ny instans av klassen [**CustomerUser**](/dotnet/api/microsoft.store.partnercenter.models.users.customeruser) och anger värdet för egenskapen [**User. State**](/dotnet/api/microsoft.store.partnercenter.models.users.user.state) till [**userState. Active**](/dotnet/api/microsoft.store.partnercenter.models.users.userstate).</span><span class="sxs-lookup"><span data-stu-id="d5bab-124">To restore a user, create a new instance of the [**CustomerUser**](/dotnet/api/microsoft.store.partnercenter.models.users.customeruser) class, and set the value of the [**User.State**](/dotnet/api/microsoft.store.partnercenter.models.users.user.state) property to [**UserState.Active**](/dotnet/api/microsoft.store.partnercenter.models.users.userstate).</span></span>

<span data-ttu-id="d5bab-125">Du återställer en borttagen användare genom att ange användarens tillstånd till aktiv.</span><span class="sxs-lookup"><span data-stu-id="d5bab-125">You restore a deleted user by setting the user's state to active.</span></span> <span data-ttu-id="d5bab-126">Du behöver inte fylla i återstående fält i användar resursen igen.</span><span class="sxs-lookup"><span data-stu-id="d5bab-126">You do not have to repopulate the remaining fields in the user resource.</span></span> <span data-ttu-id="d5bab-127">Dessa värden kommer automatiskt att återställas från den borttagna, inaktiva användar resursen.</span><span class="sxs-lookup"><span data-stu-id="d5bab-127">Those values will automatically be restored from the deleted, inactive user resource.</span></span> <span data-ttu-id="d5bab-128">Använd sedan metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: t för att identifiera kunden och metoden [**users. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) för att identifiera användaren.</span><span class="sxs-lookup"><span data-stu-id="d5bab-128">Next, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to identify the user.</span></span>

<span data-ttu-id="d5bab-129">Anropa slutligen [**korrigerings**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.patch) metoden och skicka **CustomerUser** -instansen för att skicka begäran om att återställa användaren.</span><span class="sxs-lookup"><span data-stu-id="d5bab-129">Finally, call the [**Patch**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.patch) method and pass the **CustomerUser** instance to send the request to restore the user.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedCustomerUserId;

var updatedCustomerUser = new CustomerUser()
{
    State = UserState.Active
};

// Restore customer user information.
var restoredCustomerUserInfo = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Patch(updatedCustomerUser);
```

<span data-ttu-id="d5bab-130">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="d5bab-130">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="d5bab-131">**Projekt**: Partner Center SDK-exempel **klass**: CustomerUserRestore.CS</span><span class="sxs-lookup"><span data-stu-id="d5bab-131">**Project**: Partner Center SDK Samples **Class**: CustomerUserRestore.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="d5bab-132">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="d5bab-132">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d5bab-133">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="d5bab-133">Request syntax</span></span>

| <span data-ttu-id="d5bab-134">Metod</span><span class="sxs-lookup"><span data-stu-id="d5bab-134">Method</span></span>    | <span data-ttu-id="d5bab-135">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="d5bab-135">Request URI</span></span>                                                                                            |
|-----------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d5bab-136">**9.0a**</span><span class="sxs-lookup"><span data-stu-id="d5bab-136">**PATCH**</span></span> | <span data-ttu-id="d5bab-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Users/{User-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="d5bab-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="d5bab-138">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="d5bab-138">URI parameter</span></span>

<span data-ttu-id="d5bab-139">Använd följande frågeparametrar för att ange kund-ID och användar-ID.</span><span class="sxs-lookup"><span data-stu-id="d5bab-139">Use the following query parameters to specify the customer id and user id.</span></span>

| <span data-ttu-id="d5bab-140">Namn</span><span class="sxs-lookup"><span data-stu-id="d5bab-140">Name</span></span>                   | <span data-ttu-id="d5bab-141">Typ</span><span class="sxs-lookup"><span data-stu-id="d5bab-141">Type</span></span>     | <span data-ttu-id="d5bab-142">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="d5bab-142">Required</span></span> | <span data-ttu-id="d5bab-143">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="d5bab-143">Description</span></span>                                                                                                              |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d5bab-144">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="d5bab-144">**customer-tenant-id**</span></span> | <span data-ttu-id="d5bab-145">**guid**</span><span class="sxs-lookup"><span data-stu-id="d5bab-145">**guid**</span></span> | <span data-ttu-id="d5bab-146">Y</span><span class="sxs-lookup"><span data-stu-id="d5bab-146">Y</span></span>        | <span data-ttu-id="d5bab-147">Värdet är ett GUID-formaterat **kund-Tenant-ID** som gör det möjligt för åter försäljaren att filtrera resultaten till en bestämd kund.</span><span class="sxs-lookup"><span data-stu-id="d5bab-147">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results to a given customer.</span></span> |
| <span data-ttu-id="d5bab-148">**användar-ID**</span><span class="sxs-lookup"><span data-stu-id="d5bab-148">**user-id**</span></span>            | <span data-ttu-id="d5bab-149">**guid**</span><span class="sxs-lookup"><span data-stu-id="d5bab-149">**guid**</span></span> | <span data-ttu-id="d5bab-150">Y</span><span class="sxs-lookup"><span data-stu-id="d5bab-150">Y</span></span>        | <span data-ttu-id="d5bab-151">Värdet är ett GUID-formaterat **användar-ID** som tillhör ett enda användar konto.</span><span class="sxs-lookup"><span data-stu-id="d5bab-151">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                         |

### <a name="request-headers"></a><span data-ttu-id="d5bab-152">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="d5bab-152">Request headers</span></span>

<span data-ttu-id="d5bab-153">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="d5bab-153">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d5bab-154">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="d5bab-154">Request body</span></span>

<span data-ttu-id="d5bab-155">I den här tabellen beskrivs de egenskaper som krävs i begär ande texten.</span><span class="sxs-lookup"><span data-stu-id="d5bab-155">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="d5bab-156">Namn</span><span class="sxs-lookup"><span data-stu-id="d5bab-156">Name</span></span>       | <span data-ttu-id="d5bab-157">Typ</span><span class="sxs-lookup"><span data-stu-id="d5bab-157">Type</span></span>   | <span data-ttu-id="d5bab-158">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="d5bab-158">Required</span></span> | <span data-ttu-id="d5bab-159">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="d5bab-159">Description</span></span>                                                            |
|------------|--------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="d5bab-160">Stat</span><span class="sxs-lookup"><span data-stu-id="d5bab-160">State</span></span>      | <span data-ttu-id="d5bab-161">sträng</span><span class="sxs-lookup"><span data-stu-id="d5bab-161">string</span></span> | <span data-ttu-id="d5bab-162">Y</span><span class="sxs-lookup"><span data-stu-id="d5bab-162">Y</span></span>        | <span data-ttu-id="d5bab-163">Användar tillstånd.</span><span class="sxs-lookup"><span data-stu-id="d5bab-163">The user state.</span></span> <span data-ttu-id="d5bab-164">Om du vill återställa en borttagen användare måste strängen innehålla "Active".</span><span class="sxs-lookup"><span data-stu-id="d5bab-164">To restore a deleted user, this string must contain "active".</span></span> |
| <span data-ttu-id="d5bab-165">Attribut</span><span class="sxs-lookup"><span data-stu-id="d5bab-165">Attributes</span></span> | <span data-ttu-id="d5bab-166">objekt</span><span class="sxs-lookup"><span data-stu-id="d5bab-166">object</span></span> | <span data-ttu-id="d5bab-167">N</span><span class="sxs-lookup"><span data-stu-id="d5bab-167">N</span></span>        | <span data-ttu-id="d5bab-168">Innehåller "ObjectType": "CustomerUser".</span><span class="sxs-lookup"><span data-stu-id="d5bab-168">Contains "ObjectType": "CustomerUser".</span></span>                                 |

### <a name="request-example"></a><span data-ttu-id="d5bab-169">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="d5bab-169">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 6e668bc0-5bd7-44d6-b6fa-529d41ce9659
MS-CorrelationId: 32be760f-8282-4e01-a37b-829c8a700e8a
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 269
Expect: 100-continue

{
    "State": "active",
    "Attributes": {
        "ObjectType": "CustomerUser"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="d5bab-170">REST-svar</span><span class="sxs-lookup"><span data-stu-id="d5bab-170">REST response</span></span>

<span data-ttu-id="d5bab-171">Om det lyckas returnerar svaret den återställda användar informationen i svars texten.</span><span class="sxs-lookup"><span data-stu-id="d5bab-171">If successful, the response returns the restored user information in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d5bab-172">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="d5bab-172">Response success and error codes</span></span>

<span data-ttu-id="d5bab-173">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="d5bab-173">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d5bab-174">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="d5bab-174">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d5bab-175">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="d5bab-175">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d5bab-176">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="d5bab-176">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 465
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 32be760f-8282-4e01-a37b-829c8a700e8a
MS-RequestId: 6e668bc0-5bd7-44d6-b6fa-529d41ce9659
MS-CV: ZTeBriO7mEaiM13+.0
MS-ServerId: 101112616
Date: Fri, 20 Jan 2017 22:24:55 GMT

{
    "usageLocation": "US",
    "id": "a45f1416-3300-4f65-9e8d-f123b397a4ea",
    "userPrincipalName": "e83763f7f2204ac384cfcd49f79f2749@dtdemocspcustomer005.onmicrosoft.com",
    "firstName": "Ferdinand",
    "lastName": "Filibuster",
    "displayName": "Ferdinand",
    "userDomainType": "none",
    "state": "active",
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "CustomerUser"
    }
}
```
