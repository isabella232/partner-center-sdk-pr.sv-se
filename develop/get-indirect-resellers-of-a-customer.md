---
title: Hämta indirekta återförsäljare för en kund
description: Så här hämtar du en lista över de indirekta åter försäljare som har en relation med en angiven kund.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: d69abf9530548f110820ca04fefb698e0e37556c
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769690"
---
# <a name="get-indirect-resellers-of-a-customer"></a><span data-ttu-id="0a286-103">Hämta indirekta återförsäljare för en kund</span><span class="sxs-lookup"><span data-stu-id="0a286-103">Get indirect resellers of a customer</span></span>

<span data-ttu-id="0a286-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="0a286-104">**Applies To**</span></span>

- <span data-ttu-id="0a286-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="0a286-105">Partner Center</span></span>

<span data-ttu-id="0a286-106">Så här hämtar du en lista över de indirekta åter försäljare som har en relation med en angiven kund.</span><span class="sxs-lookup"><span data-stu-id="0a286-106">How to get a list of the indirect resellers that have a relationship with a specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a286-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="0a286-107">Prerequisites</span></span>

- <span data-ttu-id="0a286-108">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="0a286-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0a286-109">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="0a286-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="0a286-110">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0a286-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="0a286-111">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="0a286-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="0a286-112">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="0a286-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="0a286-113">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="0a286-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="0a286-114">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="0a286-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="0a286-115">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0a286-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="0a286-116">C\#</span><span class="sxs-lookup"><span data-stu-id="0a286-116">C\#</span></span>

<span data-ttu-id="0a286-117">Om du vill hämta en lista över indirekta åter försäljare som den angivna kunden har en relation till får du först ett gränssnitt till kund samlings åtgärder för den specifika kunden från [**partnerOperations. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) -egenskapen genom att ange kund-ID: t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="0a286-117">To retrieve a list of indirect resellers with whom the specified customer has a relationship, first get an interface to customer collection operations for the specific customer from the [**partnerOperations.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) property by providing the customer ID to identify the customer.</span></span> <span data-ttu-id="0a286-118">Anropa sedan [**relationerna. Hämta**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.get) eller [**Hämta en \_ asynkron**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.getasync) metod för att hämta listan över indirekta åter försäljare.</span><span class="sxs-lookup"><span data-stu-id="0a286-118">Then call the [**Relationships.Get**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.get) or [**Get\_Async**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.getasync) method to get the list of indirect resellers.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

 var indirectResellers = partnerOperations.Customers[customerId].Relationships.Get();
```

<span data-ttu-id="0a286-119">**Exempel**: [konsol test app](console-test-app.md)-**projekt**: Partner Center SDK-exempel **klass**: GetIndirectResellersOfCustomer.CS</span><span class="sxs-lookup"><span data-stu-id="0a286-119">**Sample**: [Console test app](console-test-app.md)**Project**: Partner Center SDK Samples **Class**: GetIndirectResellersOfCustomer.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="0a286-120">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="0a286-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0a286-121">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="0a286-121">Request syntax</span></span>

| <span data-ttu-id="0a286-122">Metod</span><span class="sxs-lookup"><span data-stu-id="0a286-122">Method</span></span>  | <span data-ttu-id="0a286-123">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="0a286-123">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="0a286-124">**TA**</span><span class="sxs-lookup"><span data-stu-id="0a286-124">**GET**</span></span> | <span data-ttu-id="0a286-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Relationships http/1.1</span><span class="sxs-lookup"><span data-stu-id="0a286-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/relationships HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="0a286-126">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="0a286-126">URI parameter</span></span>

<span data-ttu-id="0a286-127">Använd följande Sök vägs parameter för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="0a286-127">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="0a286-128">Namn</span><span class="sxs-lookup"><span data-stu-id="0a286-128">Name</span></span>        | <span data-ttu-id="0a286-129">Typ</span><span class="sxs-lookup"><span data-stu-id="0a286-129">Type</span></span>   | <span data-ttu-id="0a286-130">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="0a286-130">Required</span></span> | <span data-ttu-id="0a286-131">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="0a286-131">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="0a286-132">kund-ID</span><span class="sxs-lookup"><span data-stu-id="0a286-132">customer-id</span></span> | <span data-ttu-id="0a286-133">sträng</span><span class="sxs-lookup"><span data-stu-id="0a286-133">string</span></span> | <span data-ttu-id="0a286-134">Yes</span><span class="sxs-lookup"><span data-stu-id="0a286-134">Yes</span></span>      | <span data-ttu-id="0a286-135">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="0a286-135">A GUID formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="0a286-136">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="0a286-136">Request headers</span></span>

<span data-ttu-id="0a286-137">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="0a286-137">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0a286-138">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="0a286-138">Request body</span></span>

<span data-ttu-id="0a286-139">Inga.</span><span class="sxs-lookup"><span data-stu-id="0a286-139">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="0a286-140">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="0a286-140">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/relationships HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c9251710-5a30-4cd3-891a-c42d550af9a8
MS-CorrelationId: a96f326c-a392-44f4-bcfe-43152a756ba8
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="0a286-141">REST-svar</span><span class="sxs-lookup"><span data-stu-id="0a286-141">REST response</span></span>

<span data-ttu-id="0a286-142">Om det lyckas innehåller svars texten en samling [PartnerRelationship](relationships-resources.md) -resurser för att identifiera åter försäljarna.</span><span class="sxs-lookup"><span data-stu-id="0a286-142">If successful, the response body contains a collection of [PartnerRelationship](relationships-resources.md) resources to identify the resellers.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0a286-143">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="0a286-143">Response success and error codes</span></span>

<span data-ttu-id="0a286-144">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="0a286-144">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0a286-145">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="0a286-145">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="0a286-146">En fullständig lista finns i [fel koder för partner Center](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="0a286-146">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="0a286-147">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="0a286-147">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 264
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a96f326c-a392-44f4-bcfe-43152a756ba8
MS-RequestId: c9251710-5a30-4cd3-891a-c42d550af9a8
MS-CV: plJP3ufU0UqXMeuh.0
MS-ServerId: 020021921
Date: Fri, 07 Apr 2017 23:42:11 GMT

{
    "totalCount": 1,
    "items": [{
            "id": "484e548c-f5f3-4528-93a9-c16c6373cb59",
            "name": "First Up Consultants",
            "relationshipType": "is_indirect_cloud_solution_provider_of",
            "mpnId": "4847383",
            "attributes": {
                "objectType": "PartnerRelationship"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
