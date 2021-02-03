---
title: Ta bort ett användarkonto för en kund
description: Så här tar du bort ett befintligt användar konto för en kund.
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 77fc1a1c7264779ca549be8d52798e90c91138bb
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769381"
---
# <a name="delete-a-user-account-for-a-customer"></a><span data-ttu-id="b4c59-103">Ta bort ett användarkonto för en kund</span><span class="sxs-lookup"><span data-stu-id="b4c59-103">Delete a user account for a customer</span></span>

<span data-ttu-id="b4c59-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="b4c59-104">**Applies to:**</span></span>

- <span data-ttu-id="b4c59-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="b4c59-105">Partner Center</span></span>

<span data-ttu-id="b4c59-106">Den här artikeln förklarar hur du tar bort ett befintligt användar konto för en kund.</span><span class="sxs-lookup"><span data-stu-id="b4c59-106">This article explains how to delete an existing user account for a customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b4c59-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="b4c59-107">Prerequisites</span></span>

- <span data-ttu-id="b4c59-108">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b4c59-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b4c59-109">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="b4c59-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="b4c59-110">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b4c59-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="b4c59-111">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="b4c59-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="b4c59-112">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="b4c59-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="b4c59-113">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="b4c59-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="b4c59-114">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="b4c59-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="b4c59-115">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b4c59-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="b4c59-116">Ett användar-ID.</span><span class="sxs-lookup"><span data-stu-id="b4c59-116">A user ID.</span></span> <span data-ttu-id="b4c59-117">Om du inte har användar-ID, se [Hämta en lista över alla användar konton för en kund](get-a-list-of-all-user-accounts-for-a-customer.md).</span><span class="sxs-lookup"><span data-stu-id="b4c59-117">If you do not have the user ID, see [Get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md).</span></span>

## <a name="deleting-a-user-account"></a><span data-ttu-id="b4c59-118">Ta bort ett användar konto</span><span class="sxs-lookup"><span data-stu-id="b4c59-118">Deleting a user account</span></span>

<span data-ttu-id="b4c59-119">När du tar bort ett användar konto är användar tillstånd inställt på **inaktiv** i trettio dagar.</span><span class="sxs-lookup"><span data-stu-id="b4c59-119">When you delete a user account, the user state is set to **inactive** for thirty days.</span></span> <span data-ttu-id="b4c59-120">Efter trettio dagar rensas användar kontot och dess associerade data och blir oåterkalleliga.</span><span class="sxs-lookup"><span data-stu-id="b4c59-120">After thirty days, the user account and its associated data are purged and made unrecoverable.</span></span>

<span data-ttu-id="b4c59-121">Du kan [återställa ett borttaget användar konto för en kund](restore-a-user-for-a-customer.md) om det inaktiva kontot är inom trettio dagars period.</span><span class="sxs-lookup"><span data-stu-id="b4c59-121">You can [restore a deleted user account for a customer](restore-a-user-for-a-customer.md) if the inactive account is within the thirty day window.</span></span> <span data-ttu-id="b4c59-122">Men när du återställer ett konto som har tagits bort och marker ATS som inaktivt returneras inte längre kontot som medlem i användar samlingen (till exempel när du [hämtar en lista över alla användar konton för en kund](get-a-list-of-all-user-accounts-for-a-customer.md)).</span><span class="sxs-lookup"><span data-stu-id="b4c59-122">However, when you restore an account that was deleted and marked as inactive, the account is no longer returned as a member of the user collection (for example, when you [get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md)).</span></span>

## <a name="c"></a><span data-ttu-id="b4c59-123">C\#</span><span class="sxs-lookup"><span data-stu-id="b4c59-123">C\#</span></span>

<span data-ttu-id="b4c59-124">Ta bort ett befintligt kund användar konto:</span><span class="sxs-lookup"><span data-stu-id="b4c59-124">To delete an existing customer user account:</span></span>

1. <span data-ttu-id="b4c59-125">Använd metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="b4c59-125">Use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="b4c59-126">Anropa metoden [**users. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) för att identifiera användaren.</span><span class="sxs-lookup"><span data-stu-id="b4c59-126">Call the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to identify the user.</span></span>

3. <span data-ttu-id="b4c59-127">Anropa [**Delete**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.delete) -metoden för att ta bort användaren och ange att användar statusen är inaktiv.</span><span class="sxs-lookup"><span data-stu-id="b4c59-127">Call the [**Delete**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.delete) method to delete the user and set the user state to inactive.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string customerUserIdToDelete;

partnerOperations.Customers.ById(selectedCustomerId).Users.ById(customerUserIdToDelete).Delete();
```

<span data-ttu-id="b4c59-128">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="b4c59-128">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="b4c59-129">**Projekt**: Partner Center SDK-exempel **klass**: DeleteCustomerUser.CS</span><span class="sxs-lookup"><span data-stu-id="b4c59-129">**Project**: Partner Center SDK Samples **Class**: DeleteCustomerUser.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="b4c59-130">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="b4c59-130">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b4c59-131">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="b4c59-131">Request syntax</span></span>

| <span data-ttu-id="b4c59-132">Metod</span><span class="sxs-lookup"><span data-stu-id="b4c59-132">Method</span></span>     | <span data-ttu-id="b4c59-133">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="b4c59-133">Request URI</span></span>                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b4c59-134">DELETE</span><span class="sxs-lookup"><span data-stu-id="b4c59-134">DELETE</span></span>     | <span data-ttu-id="b4c59-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Users/{User-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="b4c59-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="b4c59-136">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="b4c59-136">URI parameters</span></span>

<span data-ttu-id="b4c59-137">Använd följande frågeparametrar för att identifiera kunden och användaren.</span><span class="sxs-lookup"><span data-stu-id="b4c59-137">Use the following query parameters to identify the customer and user.</span></span>

| <span data-ttu-id="b4c59-138">Namn</span><span class="sxs-lookup"><span data-stu-id="b4c59-138">Name</span></span>                   | <span data-ttu-id="b4c59-139">Typ</span><span class="sxs-lookup"><span data-stu-id="b4c59-139">Type</span></span>     | <span data-ttu-id="b4c59-140">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="b4c59-140">Required</span></span> | <span data-ttu-id="b4c59-141">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="b4c59-141">Description</span></span>                                                                                                               |
|------------------------|----------|----------|---------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b4c59-142">kund-ID för klient organisation</span><span class="sxs-lookup"><span data-stu-id="b4c59-142">customer-tenant-id</span></span>     | <span data-ttu-id="b4c59-143">GUID</span><span class="sxs-lookup"><span data-stu-id="b4c59-143">GUID</span></span>     | <span data-ttu-id="b4c59-144">Y</span><span class="sxs-lookup"><span data-stu-id="b4c59-144">Y</span></span>        | <span data-ttu-id="b4c59-145">Värdet är ett GUID-formaterat **kund-ID** som gör det möjligt för åter försäljaren att filtrera resultaten för en bestämd kund.</span><span class="sxs-lookup"><span data-stu-id="b4c59-145">The value is a GUID-formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer.</span></span> |
| <span data-ttu-id="b4c59-146">användar-id</span><span class="sxs-lookup"><span data-stu-id="b4c59-146">user-id</span></span>                | <span data-ttu-id="b4c59-147">GUID</span><span class="sxs-lookup"><span data-stu-id="b4c59-147">GUID</span></span>     | <span data-ttu-id="b4c59-148">Y</span><span class="sxs-lookup"><span data-stu-id="b4c59-148">Y</span></span>        | <span data-ttu-id="b4c59-149">Värdet är ett GUID-formaterat **användar-ID** som tillhör ett enda användar konto.</span><span class="sxs-lookup"><span data-stu-id="b4c59-149">The value is a GUID-formatted **user-id** that belongs to a single user account.</span></span>                                          |

### <a name="request-headers"></a><span data-ttu-id="b4c59-150">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="b4c59-150">Request headers</span></span>

<span data-ttu-id="b4c59-151">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b4c59-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b4c59-152">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="b4c59-152">Request body</span></span>

<span data-ttu-id="b4c59-153">Inga.</span><span class="sxs-lookup"><span data-stu-id="b4c59-153">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="b4c59-154">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="b4c59-154">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="b4c59-155">REST-svar</span><span class="sxs-lookup"><span data-stu-id="b4c59-155">REST response</span></span>

<span data-ttu-id="b4c59-156">Om det lyckas returnerar den här metoden en **204-innehålls** status kod.</span><span class="sxs-lookup"><span data-stu-id="b4c59-156">If successful, this method returns a **204 No Content** status code.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b4c59-157">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="b4c59-157">Response success and error codes</span></span>

<span data-ttu-id="b4c59-158">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="b4c59-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b4c59-159">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="b4c59-159">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b4c59-160">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b4c59-160">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b4c59-161">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="b4c59-161">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 709c0b80-016c-4662-b29f-697fdf03e87a
MS-RequestId: f113b126-ec13-4baa-ab4d-67c245244971
MS-CV: 90KUJA7HKEaG8wHu.0
MS-ServerId: 101112616
Date: Tue, 24 Jan 2017 23:27:18 GMT
```
