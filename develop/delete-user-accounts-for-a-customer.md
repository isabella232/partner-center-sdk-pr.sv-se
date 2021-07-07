---
title: Ta bort ett användarkonto för en kund
description: Så här tar du bort ett befintligt användarkonto för en kund.
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c45646da43b8926f911942374de5da07f318c526
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973068"
---
# <a name="delete-a-user-account-for-a-customer"></a><span data-ttu-id="73a2e-103">Ta bort ett användarkonto för en kund</span><span class="sxs-lookup"><span data-stu-id="73a2e-103">Delete a user account for a customer</span></span>

<span data-ttu-id="73a2e-104">Den här artikeln beskriver hur du tar bort ett befintligt användarkonto för en kund.</span><span class="sxs-lookup"><span data-stu-id="73a2e-104">This article explains how to delete an existing user account for a customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="73a2e-105">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="73a2e-105">Prerequisites</span></span>

- <span data-ttu-id="73a2e-106">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="73a2e-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="73a2e-107">Det här scenariot stöder endast autentisering med app+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="73a2e-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="73a2e-108">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="73a2e-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="73a2e-109">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="73a2e-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="73a2e-110">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="73a2e-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="73a2e-111">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="73a2e-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="73a2e-112">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="73a2e-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="73a2e-113">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="73a2e-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="73a2e-114">Ett användar-ID.</span><span class="sxs-lookup"><span data-stu-id="73a2e-114">A user ID.</span></span> <span data-ttu-id="73a2e-115">Om du inte har användar-ID:t kan [du se Hämta en lista över alla användarkonton för en kund.](get-a-list-of-all-user-accounts-for-a-customer.md)</span><span class="sxs-lookup"><span data-stu-id="73a2e-115">If you do not have the user ID, see [Get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md).</span></span>

## <a name="deleting-a-user-account"></a><span data-ttu-id="73a2e-116">Ta bort ett användarkonto</span><span class="sxs-lookup"><span data-stu-id="73a2e-116">Deleting a user account</span></span>

<span data-ttu-id="73a2e-117">När du tar bort ett användarkonto är användartillståndet **inaktivt i** 30 dagar.</span><span class="sxs-lookup"><span data-stu-id="73a2e-117">When you delete a user account, the user state is set to **inactive** for 30 days.</span></span> <span data-ttu-id="73a2e-118">Efter 30 dagar rensas användarkontot och tillhörande data och kan inte återställas.</span><span class="sxs-lookup"><span data-stu-id="73a2e-118">After thirty 30 days, the user account and its associated data are purged and made unrecoverable.</span></span>

<span data-ttu-id="73a2e-119">Du kan [återställa ett borttagna användarkonto för en kund om](restore-a-user-for-a-customer.md) det inaktiva kontot är inom 30-dagarsfönstret.</span><span class="sxs-lookup"><span data-stu-id="73a2e-119">You can [restore a deleted user account for a customer](restore-a-user-for-a-customer.md) if the inactive account is within the 30-day window.</span></span> <span data-ttu-id="73a2e-120">Men när du återställer ett konto som har tagits bort och markerats som inaktivt returneras kontot inte längre som medlem i användarsamlingen (till exempel när du hämtar en lista över alla användarkonton för en [kund](get-a-list-of-all-user-accounts-for-a-customer.md)).</span><span class="sxs-lookup"><span data-stu-id="73a2e-120">However, when you restore an account that was deleted and marked as inactive, the account is no longer returned as a member of the user collection (for example, when you [get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md)).</span></span>

## <a name="c"></a><span data-ttu-id="73a2e-121">C\#</span><span class="sxs-lookup"><span data-stu-id="73a2e-121">C\#</span></span>

<span data-ttu-id="73a2e-122">Så här tar du bort ett befintligt kundanvändarkonto:</span><span class="sxs-lookup"><span data-stu-id="73a2e-122">To delete an existing customer user account:</span></span>

1. <span data-ttu-id="73a2e-123">Använd metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="73a2e-123">Use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="73a2e-124">Anropa metoden [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) för att identifiera användaren.</span><span class="sxs-lookup"><span data-stu-id="73a2e-124">Call the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to identify the user.</span></span>

3. <span data-ttu-id="73a2e-125">Anropa [**delete-metoden**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.delete) för att ta bort användaren och ange användartillståndet till inaktivt.</span><span class="sxs-lookup"><span data-stu-id="73a2e-125">Call the [**Delete**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.delete) method to delete the user and set the user state to inactive.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string customerUserIdToDelete;

partnerOperations.Customers.ById(selectedCustomerId).Users.ById(customerUserIdToDelete).Delete();
```

<span data-ttu-id="73a2e-126">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="73a2e-126">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="73a2e-127">**Project:** Partnercenter-SDK **Exempelklass:** DeleteCustomerUser.cs</span><span class="sxs-lookup"><span data-stu-id="73a2e-127">**Project**: Partner Center SDK Samples **Class**: DeleteCustomerUser.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="73a2e-128">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="73a2e-128">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="73a2e-129">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="73a2e-129">Request syntax</span></span>

| <span data-ttu-id="73a2e-130">Metod</span><span class="sxs-lookup"><span data-stu-id="73a2e-130">Method</span></span>     | <span data-ttu-id="73a2e-131">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="73a2e-131">Request URI</span></span>                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="73a2e-132">DELETE</span><span class="sxs-lookup"><span data-stu-id="73a2e-132">DELETE</span></span>     | <span data-ttu-id="73a2e-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="73a2e-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="73a2e-134">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="73a2e-134">URI parameters</span></span>

<span data-ttu-id="73a2e-135">Använd följande frågeparametrar för att identifiera kunden och användaren.</span><span class="sxs-lookup"><span data-stu-id="73a2e-135">Use the following query parameters to identify the customer and user.</span></span>

| <span data-ttu-id="73a2e-136">Namn</span><span class="sxs-lookup"><span data-stu-id="73a2e-136">Name</span></span>                   | <span data-ttu-id="73a2e-137">Typ</span><span class="sxs-lookup"><span data-stu-id="73a2e-137">Type</span></span>     | <span data-ttu-id="73a2e-138">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="73a2e-138">Required</span></span> | <span data-ttu-id="73a2e-139">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="73a2e-139">Description</span></span>                                                                                                               |
|------------------------|----------|----------|---------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="73a2e-140">kund-klient-id</span><span class="sxs-lookup"><span data-stu-id="73a2e-140">customer-tenant-id</span></span>     | <span data-ttu-id="73a2e-141">GUID</span><span class="sxs-lookup"><span data-stu-id="73a2e-141">GUID</span></span>     | <span data-ttu-id="73a2e-142">Y</span><span class="sxs-lookup"><span data-stu-id="73a2e-142">Y</span></span>        | <span data-ttu-id="73a2e-143">Värdet är ett GUID-formaterat **kundklient-ID** som gör att återförsäljaren kan filtrera resultatet för en viss kund.</span><span class="sxs-lookup"><span data-stu-id="73a2e-143">The value is a GUID-formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer.</span></span> |
| <span data-ttu-id="73a2e-144">användar-id</span><span class="sxs-lookup"><span data-stu-id="73a2e-144">user-id</span></span>                | <span data-ttu-id="73a2e-145">GUID</span><span class="sxs-lookup"><span data-stu-id="73a2e-145">GUID</span></span>     | <span data-ttu-id="73a2e-146">Y</span><span class="sxs-lookup"><span data-stu-id="73a2e-146">Y</span></span>        | <span data-ttu-id="73a2e-147">Värdet är ett GUID-formaterat **användar-ID** som tillhör ett enda användarkonto.</span><span class="sxs-lookup"><span data-stu-id="73a2e-147">The value is a GUID-formatted **user-id** that belongs to a single user account.</span></span>                                          |

### <a name="request-headers"></a><span data-ttu-id="73a2e-148">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="73a2e-148">Request headers</span></span>

<span data-ttu-id="73a2e-149">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="73a2e-149">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="73a2e-150">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="73a2e-150">Request body</span></span>

<span data-ttu-id="73a2e-151">Inga.</span><span class="sxs-lookup"><span data-stu-id="73a2e-151">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="73a2e-152">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="73a2e-152">Request example</span></span>

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f113b126-ec13-4baa-ab4d-67c245244971
MS-CorrelationId: 709c0b80-016c-4662-b29f-697fdf03e87a
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="73a2e-153">REST-svar</span><span class="sxs-lookup"><span data-stu-id="73a2e-153">REST response</span></span>

<span data-ttu-id="73a2e-154">Om det lyckas returnerar den här metoden **statuskoden 204 Inget** innehåll.</span><span class="sxs-lookup"><span data-stu-id="73a2e-154">If successful, this method returns a **204 No Content** status code.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="73a2e-155">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="73a2e-155">Response success and error codes</span></span>

<span data-ttu-id="73a2e-156">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="73a2e-156">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="73a2e-157">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="73a2e-157">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="73a2e-158">En fullständig lista finns i [Felkoder för Partner Center REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="73a2e-158">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="73a2e-159">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="73a2e-159">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 709c0b80-016c-4662-b29f-697fdf03e87a
MS-RequestId: f113b126-ec13-4baa-ab4d-67c245244971
MS-CV: 90KUJA7HKEaG8wHu.0
MS-ServerId: 101112616
Date: Tue, 24 Jan 2017 23:27:18 GMT
```
