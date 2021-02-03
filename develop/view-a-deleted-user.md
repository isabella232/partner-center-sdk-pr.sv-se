---
title: Visa borttagna användare för en kund
description: Hämtar en lista över borttagna CustomerUser-resurser för en kund efter kund-ID. Du kan också ange en sid storlek. Du måste ange ett filter.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9b1a9b85e3eba7ae7ec1dab8e951134d03371604
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769534"
---
# <a name="view-deleted-users-for-a-customer"></a><span data-ttu-id="68ac2-105">Visa borttagna användare för en kund</span><span class="sxs-lookup"><span data-stu-id="68ac2-105">View deleted users for a customer</span></span>

<span data-ttu-id="68ac2-106">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="68ac2-106">**Applies To**</span></span>

- <span data-ttu-id="68ac2-107">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="68ac2-107">Partner Center</span></span>

<span data-ttu-id="68ac2-108">Hämtar en lista över borttagna CustomerUser-resurser för en kund efter kund-ID.</span><span class="sxs-lookup"><span data-stu-id="68ac2-108">Gets a list of deleted CustomerUser resources for a customer by customer ID.</span></span> <span data-ttu-id="68ac2-109">Du kan också ange en sid storlek.</span><span class="sxs-lookup"><span data-stu-id="68ac2-109">You can optionally set a page size.</span></span> <span data-ttu-id="68ac2-110">Du måste ange ett filter.</span><span class="sxs-lookup"><span data-stu-id="68ac2-110">You must supply a filter.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68ac2-111">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="68ac2-111">Prerequisites</span></span>

- <span data-ttu-id="68ac2-112">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="68ac2-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="68ac2-113">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="68ac2-113">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="68ac2-114">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="68ac2-114">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="68ac2-115">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="68ac2-115">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="68ac2-116">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="68ac2-116">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="68ac2-117">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="68ac2-117">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="68ac2-118">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="68ac2-118">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="68ac2-119">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="68ac2-119">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="what-happens-when-you-delete-a-user-account"></a><span data-ttu-id="68ac2-120">Vad händer när du tar bort ett användar konto?</span><span class="sxs-lookup"><span data-stu-id="68ac2-120">What happens when you delete a user account?</span></span>

<span data-ttu-id="68ac2-121">Användar tillstånd är inställt på "inaktiv" när du tar bort ett användar konto.</span><span class="sxs-lookup"><span data-stu-id="68ac2-121">The user state is set to "inactive" when you delete a user account.</span></span> <span data-ttu-id="68ac2-122">Den är på samma sätt i trettio dagar, efter vilken användar kontot och dess associerade data rensas och blir oåterkalleligt.</span><span class="sxs-lookup"><span data-stu-id="68ac2-122">It remains that way for thirty days, after which the user account and its associated data are purged and made unrecoverable.</span></span> <span data-ttu-id="68ac2-123">Om du vill återställa ett borttaget användar konto inom den trettio dags perioden, se [återställa en borttagen användare för en kund](restore-a-user-for-a-customer.md).</span><span class="sxs-lookup"><span data-stu-id="68ac2-123">If you want to restore a deleted user account within the thirty day window, see [Restore a deleted user for a customer](restore-a-user-for-a-customer.md).</span></span> <span data-ttu-id="68ac2-124">När du har tagit bort och markerat "inaktiv" returneras användar kontot inte längre som medlem i användar samlingen (till exempel med [Hämta en lista över alla användar konton för en kund](get-a-list-of-all-user-accounts-for-a-customer.md)).</span><span class="sxs-lookup"><span data-stu-id="68ac2-124">Once deleted and marked "inactive", the user account is no longer returned as a member of the user collection (for example, using [Get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md)).</span></span> <span data-ttu-id="68ac2-125">Om du vill hämta en lista över borttagna användare som ännu inte har rensats måste du fråga efter användar konton som har angetts till inaktiva.</span><span class="sxs-lookup"><span data-stu-id="68ac2-125">To get a list of deleted users that have not yet been purged, you must query for user accounts that have been set to inactive.</span></span>

## <a name="c"></a><span data-ttu-id="68ac2-126">C\#</span><span class="sxs-lookup"><span data-stu-id="68ac2-126">C\#</span></span>

<span data-ttu-id="68ac2-127">Om du vill hämta en lista över borttagna användare skapar du en fråga som filtrerar kund användare vars status är inaktive rad.</span><span class="sxs-lookup"><span data-stu-id="68ac2-127">To retrieve a list of deleted users, construct a query that filters for customer users whose status is set to inactive.</span></span> <span data-ttu-id="68ac2-128">Först skapar du filtret genom att instansiera ett [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) -objekt med parametrarna som de visas i följande kodfragment.</span><span class="sxs-lookup"><span data-stu-id="68ac2-128">First, create the filter by instantiating a [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) object with the parameters as shown in the following code snippet.</span></span> <span data-ttu-id="68ac2-129">Skapa sedan frågan med metoden [**BuildIndexedQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) .</span><span class="sxs-lookup"><span data-stu-id="68ac2-129">Then create the query using the [**BuildIndexedQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) method.</span></span> <span data-ttu-id="68ac2-130">Om du inte vill ha växlade resultat kan du använda metoden [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) i stället.</span><span class="sxs-lookup"><span data-stu-id="68ac2-130">If you do not want paged results, you can use the [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) method instead.</span></span> <span data-ttu-id="68ac2-131">Använd sedan metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="68ac2-131">Next, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="68ac2-132">Anropa slutligen [**fråge**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.query) metoden för att skicka begäran.</span><span class="sxs-lookup"><span data-stu-id="68ac2-132">Finally, call the [**Query**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.query) method to send the request.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// int customerUserPageSize;

// Create a filter for users whose status is inactive (i.e. deleted).
var filter = new SimpleFieldFilter("UserState", FieldFilterOperation.Equals, "Inactive");

// Build a paged query.
var simpleQueryWithFilter = QueryFactory.Instance.BuildIndexedQuery(customerUserPageSize, 0, filter);

// Send the request.
var customerUsers = partnerOperations.Customers.ById(selectedCustomerId).Users.Query(simpleQueryWithFilter);
```

<span data-ttu-id="68ac2-133">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="68ac2-133">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="68ac2-134">**Projekt**: Partner Center SDK-exempel **klass**: GetCustomerInactiveUsers.CS</span><span class="sxs-lookup"><span data-stu-id="68ac2-134">**Project**: Partner Center SDK Samples **Class**: GetCustomerInactiveUsers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="68ac2-135">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="68ac2-135">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="68ac2-136">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="68ac2-136">Request syntax</span></span>

| <span data-ttu-id="68ac2-137">Metod</span><span class="sxs-lookup"><span data-stu-id="68ac2-137">Method</span></span>  | <span data-ttu-id="68ac2-138">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="68ac2-138">Request URI</span></span>                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="68ac2-139">**TA**</span><span class="sxs-lookup"><span data-stu-id="68ac2-139">**GET**</span></span> | <span data-ttu-id="68ac2-140">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Users? size = {size} &filter = {filter} http/1.1</span><span class="sxs-lookup"><span data-stu-id="68ac2-140">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users?size={size}&filter={filter} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="68ac2-141">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="68ac2-141">URI parameter</span></span>

<span data-ttu-id="68ac2-142">Använd följande sökväg och frågeparametrar när du skapar begäran.</span><span class="sxs-lookup"><span data-stu-id="68ac2-142">Use the following path and query parameters when creating the request.</span></span>

| <span data-ttu-id="68ac2-143">Namn</span><span class="sxs-lookup"><span data-stu-id="68ac2-143">Name</span></span>        | <span data-ttu-id="68ac2-144">Typ</span><span class="sxs-lookup"><span data-stu-id="68ac2-144">Type</span></span>   | <span data-ttu-id="68ac2-145">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="68ac2-145">Required</span></span> | <span data-ttu-id="68ac2-146">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="68ac2-146">Description</span></span>                                                                                                                                                                        |
|-------------|--------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="68ac2-147">kund-ID</span><span class="sxs-lookup"><span data-stu-id="68ac2-147">customer-id</span></span> | <span data-ttu-id="68ac2-148">guid</span><span class="sxs-lookup"><span data-stu-id="68ac2-148">guid</span></span>   | <span data-ttu-id="68ac2-149">Yes</span><span class="sxs-lookup"><span data-stu-id="68ac2-149">Yes</span></span>      | <span data-ttu-id="68ac2-150">Värdet är ett GUID-formaterat kund-ID som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="68ac2-150">The value is a GUID formatted customer-id that identifies the customer.</span></span>                                                                                                            |
| <span data-ttu-id="68ac2-151">ikoner</span><span class="sxs-lookup"><span data-stu-id="68ac2-151">size</span></span>        | <span data-ttu-id="68ac2-152">int</span><span class="sxs-lookup"><span data-stu-id="68ac2-152">int</span></span>    | <span data-ttu-id="68ac2-153">No</span><span class="sxs-lookup"><span data-stu-id="68ac2-153">No</span></span>       | <span data-ttu-id="68ac2-154">Antalet resultat som ska visas samtidigt.</span><span class="sxs-lookup"><span data-stu-id="68ac2-154">The number of results to be displayed at one time.</span></span> <span data-ttu-id="68ac2-155">Den här parametern är valfri.</span><span class="sxs-lookup"><span data-stu-id="68ac2-155">This parameter is optional.</span></span>                                                                                                     |
| <span data-ttu-id="68ac2-156">filter</span><span class="sxs-lookup"><span data-stu-id="68ac2-156">filter</span></span>      | <span data-ttu-id="68ac2-157">filter</span><span class="sxs-lookup"><span data-stu-id="68ac2-157">filter</span></span> | <span data-ttu-id="68ac2-158">Yes</span><span class="sxs-lookup"><span data-stu-id="68ac2-158">Yes</span></span>      | <span data-ttu-id="68ac2-159">Frågan som filtrerar användar sökningen.</span><span class="sxs-lookup"><span data-stu-id="68ac2-159">The query that filters the user search.</span></span> <span data-ttu-id="68ac2-160">Om du vill hämta borttagna användare måste du ta med och koda följande sträng: {"Field": "UserState", "value": "inactive", "Operator": "equals"}.</span><span class="sxs-lookup"><span data-stu-id="68ac2-160">To retrieve deleted users, you must include and encode the following string: {"Field":"UserState","Value":"Inactive","Operator":"equals"}.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="68ac2-161">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="68ac2-161">Request headers</span></span>

<span data-ttu-id="68ac2-162">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="68ac2-162">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="68ac2-163">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="68ac2-163">Request body</span></span>

<span data-ttu-id="68ac2-164">Inga.</span><span class="sxs-lookup"><span data-stu-id="68ac2-164">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="68ac2-165">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="68ac2-165">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users?size=500&filter=%7B%22Field%22%3A%22UserState%22%2C%22Value%22%3A%22Inactive%22%2C%22Operator%22%3A%22equals%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c11feb95-55d2-45b6-9d1b-74b55d2221fb
MS-CorrelationId: 2b4ab588-f48c-4874-b479-a61895e107b2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="68ac2-166">REST-svar</span><span class="sxs-lookup"><span data-stu-id="68ac2-166">REST response</span></span>

<span data-ttu-id="68ac2-167">Om det lyckas returnerar den här metoden en samling [CustomerUser](user-resources.md#customeruser) -resurser i svars texten.</span><span class="sxs-lookup"><span data-stu-id="68ac2-167">If successful, this method returns a collection of [CustomerUser](user-resources.md#customeruser) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="68ac2-168">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="68ac2-168">Response success and error codes</span></span>

<span data-ttu-id="68ac2-169">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="68ac2-169">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="68ac2-170">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="68ac2-170">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="68ac2-171">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="68ac2-171">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="68ac2-172">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="68ac2-172">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 802
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 690b34ca-07c8-4f8a-ab13-f22a50594a43
MS-RequestId: 1187f9ad-02b4-4d96-b668-7cf3d289467b
MS-CV: 3TLmR9gz6EaCVCjR.0
MS-ServerId: 101112616
Date: Fri, 20 Jan 2017 19:13:14 GMT

{
    "totalCount": 1,
    "items": [{
            "usageLocation": "US",
            "id": "a45f1416-3300-4f65-9e8d-f123b397a4ea",
            "userPrincipalName": "e83763f7f2204ac384cfcd49f79f2749@dtdemocspcustomer005.onmicrosoft.com",
            "firstName": "Ferdinand",
            "lastName": "Filibuster",
            "displayName": "Ferdinand",
            "userDomainType": "none",
            "state": "inactive",
            "softDeletionTime": "2017-01-20T00:33:34Z",
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
    ],
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users?size=500&filter=%7B%22Field%22%3A%22UserStatus%22%2C%22Value%22%3A%22Inactive%22%2C%22Operator%22%3A%22equals%22%7D",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
