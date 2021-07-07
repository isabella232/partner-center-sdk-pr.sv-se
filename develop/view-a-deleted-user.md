---
title: Visa borttagna användare för en kund
description: Hämtar en lista över borttagna CustomerUser-resurser för en kund efter kund-ID. Du kan också ange en sidstorlek. Du måste ange ett filter.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f4fec958a9a6bb580d35de1cf3007e1db3b2b650
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445314"
---
# <a name="view-deleted-users-for-a-customer"></a><span data-ttu-id="cc36a-105">Visa borttagna användare för en kund</span><span class="sxs-lookup"><span data-stu-id="cc36a-105">View deleted users for a customer</span></span>

<span data-ttu-id="cc36a-106">Hämtar en lista över borttagna CustomerUser-resurser för en kund efter kund-ID.</span><span class="sxs-lookup"><span data-stu-id="cc36a-106">Gets a list of deleted CustomerUser resources for a customer by customer ID.</span></span> <span data-ttu-id="cc36a-107">Du kan också ange en sidstorlek.</span><span class="sxs-lookup"><span data-stu-id="cc36a-107">You can optionally set a page size.</span></span> <span data-ttu-id="cc36a-108">Du måste ange ett filter.</span><span class="sxs-lookup"><span data-stu-id="cc36a-108">You must supply a filter.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc36a-109">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="cc36a-109">Prerequisites</span></span>

- <span data-ttu-id="cc36a-110">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="cc36a-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="cc36a-111">Det här scenariot stöder endast autentisering med app+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="cc36a-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="cc36a-112">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="cc36a-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="cc36a-113">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="cc36a-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="cc36a-114">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="cc36a-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="cc36a-115">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="cc36a-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="cc36a-116">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="cc36a-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="cc36a-117">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="cc36a-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="what-happens-when-you-delete-a-user-account"></a><span data-ttu-id="cc36a-118">Vad händer när du tar bort ett användarkonto?</span><span class="sxs-lookup"><span data-stu-id="cc36a-118">What happens when you delete a user account?</span></span>

<span data-ttu-id="cc36a-119">Användartillståndet är inaktivt när du tar bort ett användarkonto.</span><span class="sxs-lookup"><span data-stu-id="cc36a-119">The user state is set to "inactive" when you delete a user account.</span></span> <span data-ttu-id="cc36a-120">Det förblir så i 30 dagar, varpå användarkontot och tillhörande data rensas och görs oåterkalleliga.</span><span class="sxs-lookup"><span data-stu-id="cc36a-120">It remains that way for 30 days, after which the user account and its associated data are purged and made unrecoverable.</span></span> <span data-ttu-id="cc36a-121">Om du vill återställa ett borttagna användarkonto inom 30-dagarsfönstret kan du gå till [Återställa en borttagna användare för en kund.](restore-a-user-for-a-customer.md)</span><span class="sxs-lookup"><span data-stu-id="cc36a-121">If you want to restore a deleted user account within the 30-day window, see [Restore a deleted user for a customer](restore-a-user-for-a-customer.md).</span></span> <span data-ttu-id="cc36a-122">När användarkontot har tagits bort och markerats som "inaktivt" returneras det inte längre som medlem i användarsamlingen (t.ex. genom att använda Hämta en lista över alla användarkonton [för en kund).](get-a-list-of-all-user-accounts-for-a-customer.md)</span><span class="sxs-lookup"><span data-stu-id="cc36a-122">Once deleted and marked "inactive", the user account is no longer returned as a member of the user collection (for example, using [Get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md)).</span></span> <span data-ttu-id="cc36a-123">Om du vill hämta en lista över borttagna användare som ännu inte har rensats måste du fråga efter användarkonton som har angetts till inaktiva.</span><span class="sxs-lookup"><span data-stu-id="cc36a-123">To get a list of deleted users that have not yet been purged, you must query for user accounts that have been set to inactive.</span></span>

## <a name="c"></a><span data-ttu-id="cc36a-124">C\#</span><span class="sxs-lookup"><span data-stu-id="cc36a-124">C\#</span></span>

<span data-ttu-id="cc36a-125">Om du vill hämta en lista över borttagna användare skapar du en fråga som filtrerar efter kundanvändare vars status är inställd på inaktiv.</span><span class="sxs-lookup"><span data-stu-id="cc36a-125">To retrieve a list of deleted users, construct a query that filters for customer users whose status is set to inactive.</span></span> <span data-ttu-id="cc36a-126">Skapa först filtret genom att instansiera ett [**SimpleFieldFilter-objekt**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) med parametrarna som visas i följande kodfragment.</span><span class="sxs-lookup"><span data-stu-id="cc36a-126">First, create the filter by instantiating a [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) object with the parameters as shown in the following code snippet.</span></span> <span data-ttu-id="cc36a-127">Skapa sedan frågan med hjälp av [**metoden BuildIndexedQuery.**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery)</span><span class="sxs-lookup"><span data-stu-id="cc36a-127">Then create the query using the [**BuildIndexedQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) method.</span></span> <span data-ttu-id="cc36a-128">Om du inte vill ha sidindelade resultat kan du använda [**metoden BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) i stället.</span><span class="sxs-lookup"><span data-stu-id="cc36a-128">If you do not want paged results, you can use the [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) method instead.</span></span> <span data-ttu-id="cc36a-129">Använd sedan metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="cc36a-129">Next, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="cc36a-130">Anropa slutligen [**frågemetoden**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.query) för att skicka begäran.</span><span class="sxs-lookup"><span data-stu-id="cc36a-130">Finally, call the [**Query**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.query) method to send the request.</span></span>

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

<span data-ttu-id="cc36a-131">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="cc36a-131">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="cc36a-132">**Project:** Partnercenter-SDK **Exempelklass:** GetCustomerInactiveUsers.cs</span><span class="sxs-lookup"><span data-stu-id="cc36a-132">**Project**: Partner Center SDK Samples **Class**: GetCustomerInactiveUsers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="cc36a-133">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="cc36a-133">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="cc36a-134">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="cc36a-134">Request syntax</span></span>

| <span data-ttu-id="cc36a-135">Metod</span><span class="sxs-lookup"><span data-stu-id="cc36a-135">Method</span></span>  | <span data-ttu-id="cc36a-136">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="cc36a-136">Request URI</span></span>                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="cc36a-137">**Få**</span><span class="sxs-lookup"><span data-stu-id="cc36a-137">**GET**</span></span> | <span data-ttu-id="cc36a-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users?size={size}&filter={filter} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="cc36a-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users?size={size}&filter={filter} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="cc36a-139">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="cc36a-139">URI parameter</span></span>

<span data-ttu-id="cc36a-140">Använd följande sökväg och frågeparametrar när du skapar begäran.</span><span class="sxs-lookup"><span data-stu-id="cc36a-140">Use the following path and query parameters when creating the request.</span></span>

| <span data-ttu-id="cc36a-141">Namn</span><span class="sxs-lookup"><span data-stu-id="cc36a-141">Name</span></span>        | <span data-ttu-id="cc36a-142">Typ</span><span class="sxs-lookup"><span data-stu-id="cc36a-142">Type</span></span>   | <span data-ttu-id="cc36a-143">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="cc36a-143">Required</span></span> | <span data-ttu-id="cc36a-144">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="cc36a-144">Description</span></span>                                                                                                                                                                        |
|-------------|--------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="cc36a-145">kund-id</span><span class="sxs-lookup"><span data-stu-id="cc36a-145">customer-id</span></span> | <span data-ttu-id="cc36a-146">guid</span><span class="sxs-lookup"><span data-stu-id="cc36a-146">guid</span></span>   | <span data-ttu-id="cc36a-147">Ja</span><span class="sxs-lookup"><span data-stu-id="cc36a-147">Yes</span></span>      | <span data-ttu-id="cc36a-148">Värdet är ett GUID-formaterat kund-ID som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="cc36a-148">The value is a GUID formatted customer-id that identifies the customer.</span></span>                                                                                                            |
| <span data-ttu-id="cc36a-149">ikoner</span><span class="sxs-lookup"><span data-stu-id="cc36a-149">size</span></span>        | <span data-ttu-id="cc36a-150">int</span><span class="sxs-lookup"><span data-stu-id="cc36a-150">int</span></span>    | <span data-ttu-id="cc36a-151">Inga</span><span class="sxs-lookup"><span data-stu-id="cc36a-151">No</span></span>       | <span data-ttu-id="cc36a-152">Antalet resultat som ska visas samtidigt.</span><span class="sxs-lookup"><span data-stu-id="cc36a-152">The number of results to be displayed at one time.</span></span> <span data-ttu-id="cc36a-153">Den här parametern är valfri.</span><span class="sxs-lookup"><span data-stu-id="cc36a-153">This parameter is optional.</span></span>                                                                                                     |
| <span data-ttu-id="cc36a-154">filter</span><span class="sxs-lookup"><span data-stu-id="cc36a-154">filter</span></span>      | <span data-ttu-id="cc36a-155">filter</span><span class="sxs-lookup"><span data-stu-id="cc36a-155">filter</span></span> | <span data-ttu-id="cc36a-156">Ja</span><span class="sxs-lookup"><span data-stu-id="cc36a-156">Yes</span></span>      | <span data-ttu-id="cc36a-157">Frågan som filtrerar användarsökningen.</span><span class="sxs-lookup"><span data-stu-id="cc36a-157">The query that filters the user search.</span></span> <span data-ttu-id="cc36a-158">För att hämta borttagna användare måste du inkludera och koda följande sträng: {"Field":"UserState","Value":"Inactive","Operator":"equals"}.</span><span class="sxs-lookup"><span data-stu-id="cc36a-158">To retrieve deleted users, you must include and encode the following string: {"Field":"UserState","Value":"Inactive","Operator":"equals"}.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="cc36a-159">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="cc36a-159">Request headers</span></span>

<span data-ttu-id="cc36a-160">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="cc36a-160">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="cc36a-161">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="cc36a-161">Request body</span></span>

<span data-ttu-id="cc36a-162">Inga.</span><span class="sxs-lookup"><span data-stu-id="cc36a-162">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="cc36a-163">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="cc36a-163">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users?size=500&filter=%7B%22Field%22%3A%22UserState%22%2C%22Value%22%3A%22Inactive%22%2C%22Operator%22%3A%22equals%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c11feb95-55d2-45b6-9d1b-74b55d2221fb
MS-CorrelationId: 2b4ab588-f48c-4874-b479-a61895e107b2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="cc36a-164">REST-svar</span><span class="sxs-lookup"><span data-stu-id="cc36a-164">REST response</span></span>

<span data-ttu-id="cc36a-165">Om det lyckas returnerar den här metoden en samling [CustomerUser-resurser](user-resources.md#customeruser) i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="cc36a-165">If successful, this method returns a collection of [CustomerUser](user-resources.md#customeruser) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="cc36a-166">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="cc36a-166">Response success and error codes</span></span>

<span data-ttu-id="cc36a-167">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="cc36a-167">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="cc36a-168">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="cc36a-168">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="cc36a-169">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="cc36a-169">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="cc36a-170">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="cc36a-170">Response example</span></span>

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
