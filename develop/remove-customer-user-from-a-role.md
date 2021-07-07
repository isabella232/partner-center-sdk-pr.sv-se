---
title: Ta bort en kundanvändare från en roll
description: Ta bort en användare från en katalogroll i ett kundkonto.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 36dc742c4f713131b4996d7dc945b6dd008a3ef5
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445654"
---
# <a name="remove-a-customer-user-from-a-role"></a><span data-ttu-id="6fd52-103">Ta bort en kundanvändare från en roll</span><span class="sxs-lookup"><span data-stu-id="6fd52-103">Remove a customer user from a role</span></span>

<span data-ttu-id="6fd52-104">Ta bort en användare från en katalogroll i ett kundkonto.</span><span class="sxs-lookup"><span data-stu-id="6fd52-104">How to remove a user from a directory role within a customer account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6fd52-105">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="6fd52-105">Prerequisites</span></span>

- <span data-ttu-id="6fd52-106">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="6fd52-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6fd52-107">Det här scenariot stöder endast autentisering med app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="6fd52-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="6fd52-108">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6fd52-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="6fd52-109">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="6fd52-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="6fd52-110">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="6fd52-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="6fd52-111">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="6fd52-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="6fd52-112">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="6fd52-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="6fd52-113">Microsoft-ID:t är samma som kund-ID :t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6fd52-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="6fd52-114">C\#</span><span class="sxs-lookup"><span data-stu-id="6fd52-114">C\#</span></span>

<span data-ttu-id="6fd52-115">Om du vill ta bort en användare från en katalogroll väljer du kunden med användaren som ska ändras med ett anrop till metoden [**IAggregatePartner.Customers.ById.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) Därifrån anger du rollen med hjälp av metoden [**DirectoryRoles.ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) med katalogrolls-ID:t.</span><span class="sxs-lookup"><span data-stu-id="6fd52-115">To remove a user from a directory role, select the customer with the user to modify with a call to the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method, From there, specify the role using the [**DirectoryRoles.ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) method with the directory role ID.</span></span> <span data-ttu-id="6fd52-116">Öppna sedan metoden [**UserMembers.ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.byid) för att identifiera användaren [](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermember.delete) som ska tas bort och ta bort metoden för att ta bort användaren från rollen.</span><span class="sxs-lookup"><span data-stu-id="6fd52-116">Then, access the [**UserMembers.ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.byid) method to identify the user to remove, and the [**Delete**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermember.delete) method to remove the user from the role.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedRoleId;
// string selectedUserMemberId;

partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.ById(selectedRoleId).UserMembers.ById(selectedUserMemberId).Delete();
```

<span data-ttu-id="6fd52-117">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="6fd52-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="6fd52-118">**Project:** Partnercenter-SDK **Samples-klass:** RemoveCustomerUserMemberFromDirectoryRole.cs</span><span class="sxs-lookup"><span data-stu-id="6fd52-118">**Project**: Partner Center SDK Samples **Class**: RemoveCustomerUserMemberFromDirectoryRole.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="6fd52-119">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="6fd52-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6fd52-120">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="6fd52-120">Request syntax</span></span>

| <span data-ttu-id="6fd52-121">Metod</span><span class="sxs-lookup"><span data-stu-id="6fd52-121">Method</span></span>     | <span data-ttu-id="6fd52-122">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="6fd52-122">Request URI</span></span>                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6fd52-123">**Ta bort**</span><span class="sxs-lookup"><span data-stu-id="6fd52-123">**DELETE**</span></span> | <span data-ttu-id="6fd52-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{role-ID}/usermembers/{user-ID} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="6fd52-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{role-ID}/usermembers/{user-ID} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="6fd52-125">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="6fd52-125">URI parameter</span></span>

<span data-ttu-id="6fd52-126">Använd följande URI-parametrar för att identifiera rätt kund, roll och användare.</span><span class="sxs-lookup"><span data-stu-id="6fd52-126">Use the following URI parameters to identify the correct customer, role, and user.</span></span>

| <span data-ttu-id="6fd52-127">Namn</span><span class="sxs-lookup"><span data-stu-id="6fd52-127">Name</span></span>                   | <span data-ttu-id="6fd52-128">Typ</span><span class="sxs-lookup"><span data-stu-id="6fd52-128">Type</span></span>     | <span data-ttu-id="6fd52-129">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="6fd52-129">Required</span></span> | <span data-ttu-id="6fd52-130">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="6fd52-130">Description</span></span>                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| <span data-ttu-id="6fd52-131">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="6fd52-131">**customer-tenant-id**</span></span> | <span data-ttu-id="6fd52-132">**guid**</span><span class="sxs-lookup"><span data-stu-id="6fd52-132">**guid**</span></span> | <span data-ttu-id="6fd52-133">Y</span><span class="sxs-lookup"><span data-stu-id="6fd52-133">Y</span></span>        | <span data-ttu-id="6fd52-134">Värdet är ett GUID-formaterat **kundklient-ID** som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="6fd52-134">The value is a GUID formatted **customer-tenant-id** that identifies the customer.</span></span> |
| <span data-ttu-id="6fd52-135">**roll-id**</span><span class="sxs-lookup"><span data-stu-id="6fd52-135">**role-id**</span></span>            | <span data-ttu-id="6fd52-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="6fd52-136">**guid**</span></span> | <span data-ttu-id="6fd52-137">Y</span><span class="sxs-lookup"><span data-stu-id="6fd52-137">Y</span></span>        | <span data-ttu-id="6fd52-138">Värdet är ett GUID-formaterat **roll-ID** som identifierar rollen.</span><span class="sxs-lookup"><span data-stu-id="6fd52-138">The value is a GUID formatted **role-id** that identifies the role.</span></span>                |
| <span data-ttu-id="6fd52-139">**användar-id**</span><span class="sxs-lookup"><span data-stu-id="6fd52-139">**user-id**</span></span>            | <span data-ttu-id="6fd52-140">**guid**</span><span class="sxs-lookup"><span data-stu-id="6fd52-140">**guid**</span></span> | <span data-ttu-id="6fd52-141">Y</span><span class="sxs-lookup"><span data-stu-id="6fd52-141">Y</span></span>        | <span data-ttu-id="6fd52-142">Värdet är ett GUID-formaterat **användar-ID** som identifierar ett enda användarkonto.</span><span class="sxs-lookup"><span data-stu-id="6fd52-142">The value is a GUID formatted **user-id** that identifies a single user account.</span></span>   |

### <a name="request-headers"></a><span data-ttu-id="6fd52-143">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="6fd52-143">Request headers</span></span>

<span data-ttu-id="6fd52-144">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="6fd52-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6fd52-145">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="6fd52-145">Request body</span></span>

<span data-ttu-id="6fd52-146">Inga.</span><span class="sxs-lookup"><span data-stu-id="6fd52-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="6fd52-147">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="6fd52-147">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="6fd52-148">REST-svar</span><span class="sxs-lookup"><span data-stu-id="6fd52-148">REST response</span></span>

<span data-ttu-id="6fd52-149">Om användaren tas bort från rollen är svarstexten tom.</span><span class="sxs-lookup"><span data-stu-id="6fd52-149">If the user is removed from the role successfully, the response body is empty.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6fd52-150">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="6fd52-150">Response success and error codes</span></span>

<span data-ttu-id="6fd52-151">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="6fd52-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6fd52-152">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="6fd52-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="6fd52-153">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="6fd52-153">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="6fd52-154">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="6fd52-154">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 90bda268-7929-4ad6-be01-89c5af5fc504
MS-RequestId: e784d7aa-8c8d-45ee-8f97-9e09823d7338
MS-CV: es01VX8do0u2aTXw.0
MS-ServerId: 101112616
Date: Tue, 20 Dec 2016 23:16:35 GMT
```
