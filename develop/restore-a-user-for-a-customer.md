---
title: Återställ en borttagen användare för en kund
description: Återställa en borttagna användare efter kund-ID och användar-ID.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 23caf91c6b29b292c2638b4a1ad208c606c47492
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445722"
---
# <a name="restore-a-deleted-user-for-a-customer"></a><span data-ttu-id="083e3-103">Återställ en borttagen användare för en kund</span><span class="sxs-lookup"><span data-stu-id="083e3-103">Restore a deleted user for a customer</span></span>

<span data-ttu-id="083e3-104">Återställa en borttagna användare efter **kund-ID** och användar-ID.</span><span class="sxs-lookup"><span data-stu-id="083e3-104">How to restore a deleted **User** by customer ID and user ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="083e3-105">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="083e3-105">Prerequisites</span></span>

- <span data-ttu-id="083e3-106">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="083e3-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="083e3-107">Det här scenariot stöder endast autentisering med app+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="083e3-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="083e3-108">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="083e3-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="083e3-109">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="083e3-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="083e3-110">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="083e3-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="083e3-111">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="083e3-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="083e3-112">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="083e3-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="083e3-113">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="083e3-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="083e3-114">Användar-ID:t.</span><span class="sxs-lookup"><span data-stu-id="083e3-114">The user ID.</span></span> <span data-ttu-id="083e3-115">Om du inte har användar-ID kan du se [Visa borttagna användare för en kund.](view-a-deleted-user.md)</span><span class="sxs-lookup"><span data-stu-id="083e3-115">If you do not have the user ID, see [View deleted users for a customer](view-a-deleted-user.md).</span></span>

## <a name="when-can-you-restore-a-deleted-user-account"></a><span data-ttu-id="083e3-116">När kan du återställa ett borttagna användarkonton?</span><span class="sxs-lookup"><span data-stu-id="083e3-116">When can you restore a deleted user account?</span></span>

<span data-ttu-id="083e3-117">Användartillståndet är inaktivt när du tar bort ett användarkonto.</span><span class="sxs-lookup"><span data-stu-id="083e3-117">The user state is set to "inactive" when you delete a user account.</span></span> <span data-ttu-id="083e3-118">Det förblir så i 30 dagar, varpå användarkontot och tillhörande data rensas och görs oåterkalleliga.</span><span class="sxs-lookup"><span data-stu-id="083e3-118">It remains that way for 30 days, after which the user account and its associated data are purged and made unrecoverable.</span></span> <span data-ttu-id="083e3-119">Du kan bara återställa ett borttagna användarkonton under det här 30-dagars fönstret.</span><span class="sxs-lookup"><span data-stu-id="083e3-119">You can only restore a deleted user account during this 30-day window.</span></span> <span data-ttu-id="083e3-120">När användarkontot har tagits bort och markerats som "inaktivt" returneras det inte längre som medlem i användarsamlingen (till exempel genom att använda Hämta en lista över alla användarkonton [för en kund).](get-a-list-of-all-user-accounts-for-a-customer.md)</span><span class="sxs-lookup"><span data-stu-id="083e3-120">Once deleted and marked "inactive" the user account is no longer returned as a member of the user collection (for example, using [Get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md)).</span></span>

## <a name="c"></a><span data-ttu-id="083e3-121">C\#</span><span class="sxs-lookup"><span data-stu-id="083e3-121">C\#</span></span>

<span data-ttu-id="083e3-122">Om du vill återställa en användare skapar du en ny instans av klassen [**CustomerUser**](/dotnet/api/microsoft.store.partnercenter.models.users.customeruser) och anger värdet för egenskapen [**User.State**](/dotnet/api/microsoft.store.partnercenter.models.users.user.state) till [**UserState.Active**](/dotnet/api/microsoft.store.partnercenter.models.users.userstate).</span><span class="sxs-lookup"><span data-stu-id="083e3-122">To restore a user, create a new instance of the [**CustomerUser**](/dotnet/api/microsoft.store.partnercenter.models.users.customeruser) class, and set the value of the [**User.State**](/dotnet/api/microsoft.store.partnercenter.models.users.user.state) property to [**UserState.Active**](/dotnet/api/microsoft.store.partnercenter.models.users.userstate).</span></span>

<span data-ttu-id="083e3-123">Du återställer en borttagna användare genom att ange användarens tillstånd till aktiv.</span><span class="sxs-lookup"><span data-stu-id="083e3-123">You restore a deleted user by setting the user's state to active.</span></span> <span data-ttu-id="083e3-124">Du behöver inte fylla i de återstående fälten i användarresursen på nya sätt.</span><span class="sxs-lookup"><span data-stu-id="083e3-124">You do not have to repopulate the remaining fields in the user resource.</span></span> <span data-ttu-id="083e3-125">Dessa värden återställs automatiskt från den borttagna, inaktiva användarresursen.</span><span class="sxs-lookup"><span data-stu-id="083e3-125">Those values will automatically be restored from the deleted, inactive user resource.</span></span> <span data-ttu-id="083e3-126">Använd sedan metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att identifiera kunden och [**metoden Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) för att identifiera användaren.</span><span class="sxs-lookup"><span data-stu-id="083e3-126">Next, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to identify the user.</span></span>

<span data-ttu-id="083e3-127">Anropa slutligen [**Patch-metoden**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.patch) och skicka **CustomerUser-instansen** för att skicka begäran om att återställa användaren.</span><span class="sxs-lookup"><span data-stu-id="083e3-127">Finally, call the [**Patch**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.patch) method and pass the **CustomerUser** instance to send the request to restore the user.</span></span>

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

<span data-ttu-id="083e3-128">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="083e3-128">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="083e3-129">**Project:** Partnercenter-SDK **Exempelklass:** CustomerUserRestore.cs</span><span class="sxs-lookup"><span data-stu-id="083e3-129">**Project**: Partner Center SDK Samples **Class**: CustomerUserRestore.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="083e3-130">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="083e3-130">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="083e3-131">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="083e3-131">Request syntax</span></span>

| <span data-ttu-id="083e3-132">Metod</span><span class="sxs-lookup"><span data-stu-id="083e3-132">Method</span></span>    | <span data-ttu-id="083e3-133">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="083e3-133">Request URI</span></span>                                                                                            |
|-----------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="083e3-134">**Patch**</span><span class="sxs-lookup"><span data-stu-id="083e3-134">**PATCH**</span></span> | <span data-ttu-id="083e3-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="083e3-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="083e3-136">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="083e3-136">URI parameter</span></span>

<span data-ttu-id="083e3-137">Använd följande frågeparametrar för att ange kund-ID och användar-ID.</span><span class="sxs-lookup"><span data-stu-id="083e3-137">Use the following query parameters to specify the customer ID and user ID.</span></span>

| <span data-ttu-id="083e3-138">Namn</span><span class="sxs-lookup"><span data-stu-id="083e3-138">Name</span></span>                   | <span data-ttu-id="083e3-139">Typ</span><span class="sxs-lookup"><span data-stu-id="083e3-139">Type</span></span>     | <span data-ttu-id="083e3-140">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="083e3-140">Required</span></span> | <span data-ttu-id="083e3-141">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="083e3-141">Description</span></span>                                                                                                              |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="083e3-142">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="083e3-142">**customer-tenant-id**</span></span> | <span data-ttu-id="083e3-143">**guid**</span><span class="sxs-lookup"><span data-stu-id="083e3-143">**guid**</span></span> | <span data-ttu-id="083e3-144">Y</span><span class="sxs-lookup"><span data-stu-id="083e3-144">Y</span></span>        | <span data-ttu-id="083e3-145">Värdet är ett GUID-formaterat **kundklient-ID** som gör att återförsäljaren kan filtrera resultatet till en viss kund.</span><span class="sxs-lookup"><span data-stu-id="083e3-145">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results to a given customer.</span></span> |
| <span data-ttu-id="083e3-146">**användar-id**</span><span class="sxs-lookup"><span data-stu-id="083e3-146">**user-id**</span></span>            | <span data-ttu-id="083e3-147">**guid**</span><span class="sxs-lookup"><span data-stu-id="083e3-147">**guid**</span></span> | <span data-ttu-id="083e3-148">Y</span><span class="sxs-lookup"><span data-stu-id="083e3-148">Y</span></span>        | <span data-ttu-id="083e3-149">Värdet är ett GUID-formaterat **användar-ID** som tillhör ett enda användarkonto.</span><span class="sxs-lookup"><span data-stu-id="083e3-149">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                         |

### <a name="request-headers"></a><span data-ttu-id="083e3-150">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="083e3-150">Request headers</span></span>

<span data-ttu-id="083e3-151">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="083e3-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="083e3-152">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="083e3-152">Request body</span></span>

<span data-ttu-id="083e3-153">I den här tabellen beskrivs de obligatoriska egenskaperna i begärandetexten.</span><span class="sxs-lookup"><span data-stu-id="083e3-153">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="083e3-154">Namn</span><span class="sxs-lookup"><span data-stu-id="083e3-154">Name</span></span>       | <span data-ttu-id="083e3-155">Typ</span><span class="sxs-lookup"><span data-stu-id="083e3-155">Type</span></span>   | <span data-ttu-id="083e3-156">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="083e3-156">Required</span></span> | <span data-ttu-id="083e3-157">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="083e3-157">Description</span></span>                                                            |
|------------|--------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="083e3-158">Tillstånd</span><span class="sxs-lookup"><span data-stu-id="083e3-158">State</span></span>      | <span data-ttu-id="083e3-159">sträng</span><span class="sxs-lookup"><span data-stu-id="083e3-159">string</span></span> | <span data-ttu-id="083e3-160">Y</span><span class="sxs-lookup"><span data-stu-id="083e3-160">Y</span></span>        | <span data-ttu-id="083e3-161">Användartillståndet.</span><span class="sxs-lookup"><span data-stu-id="083e3-161">The user state.</span></span> <span data-ttu-id="083e3-162">Om du vill återställa en borttagna användare måste strängen innehålla "aktiv".</span><span class="sxs-lookup"><span data-stu-id="083e3-162">To restore a deleted user, this string must contain "active".</span></span> |
| <span data-ttu-id="083e3-163">Attribut</span><span class="sxs-lookup"><span data-stu-id="083e3-163">Attributes</span></span> | <span data-ttu-id="083e3-164">objekt</span><span class="sxs-lookup"><span data-stu-id="083e3-164">object</span></span> | <span data-ttu-id="083e3-165">N</span><span class="sxs-lookup"><span data-stu-id="083e3-165">N</span></span>        | <span data-ttu-id="083e3-166">Innehåller "ObjectType": "CustomerUser".</span><span class="sxs-lookup"><span data-stu-id="083e3-166">Contains "ObjectType": "CustomerUser".</span></span>                                 |

### <a name="request-example"></a><span data-ttu-id="083e3-167">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="083e3-167">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="083e3-168">REST-svar</span><span class="sxs-lookup"><span data-stu-id="083e3-168">REST response</span></span>

<span data-ttu-id="083e3-169">Om det lyckas returnerar svaret den återställda användarinformationen i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="083e3-169">If successful, the response returns the restored user information in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="083e3-170">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="083e3-170">Response success and error codes</span></span>

<span data-ttu-id="083e3-171">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="083e3-171">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="083e3-172">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="083e3-172">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="083e3-173">En fullständig lista finns i [Felkoder för Partner Center REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="083e3-173">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="083e3-174">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="083e3-174">Response example</span></span>

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
