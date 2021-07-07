---
title: Hämta indirekta återförsäljare för en kund
description: Hur du hämtar en lista över indirekta återförsäljare som har en relation med en angiven kund.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 8697c40c22d5c19979c066b8d3a1de733e211f71
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446249"
---
# <a name="get-indirect-resellers-of-a-customer"></a><span data-ttu-id="7379e-103">Hämta indirekta återförsäljare för en kund</span><span class="sxs-lookup"><span data-stu-id="7379e-103">Get indirect resellers of a customer</span></span>

<span data-ttu-id="7379e-104">Hur du hämtar en lista över indirekta återförsäljare som har en relation med en angiven kund.</span><span class="sxs-lookup"><span data-stu-id="7379e-104">How to get a list of the indirect resellers that have a relationship with a specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7379e-105">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="7379e-105">Prerequisites</span></span>

- <span data-ttu-id="7379e-106">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="7379e-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7379e-107">Det här scenariot stöder endast autentisering med app+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="7379e-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="7379e-108">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7379e-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="7379e-109">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="7379e-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="7379e-110">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="7379e-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="7379e-111">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="7379e-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="7379e-112">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="7379e-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="7379e-113">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7379e-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="7379e-114">C\#</span><span class="sxs-lookup"><span data-stu-id="7379e-114">C\#</span></span>

<span data-ttu-id="7379e-115">Om du vill hämta en lista över indirekta återförsäljare som den angivna kunden har en relation med hämtar du först ett gränssnitt för kundinsamlingsåtgärder för den specifika kunden från egenskapen [**partnerOperations.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) genom att ange kund-ID:t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="7379e-115">To retrieve a list of indirect resellers with whom the specified customer has a relationship, first get an interface to customer collection operations for the specific customer from the [**partnerOperations.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) property by providing the customer ID to identify the customer.</span></span> <span data-ttu-id="7379e-116">Anropa sedan metoden [**Relationships.Get**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.get) [**eller Get \_ Async**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.getasync) för att hämta listan över indirekta återförsäljare.</span><span class="sxs-lookup"><span data-stu-id="7379e-116">Then call the [**Relationships.Get**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.get) or [**Get\_Async**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.getasync) method to get the list of indirect resellers.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

 var indirectResellers = partnerOperations.Customers[customerId].Relationships.Get();
```

<span data-ttu-id="7379e-117">**Exempel:** [Konsoltestapp med](console-test-app.md)**Project:** Partnercenter-SDK **Exempelklass:** GetIndirectResellersOfCustomer.cs</span><span class="sxs-lookup"><span data-stu-id="7379e-117">**Sample**: [Console test app](console-test-app.md)**Project**: Partner Center SDK Samples **Class**: GetIndirectResellersOfCustomer.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="7379e-118">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="7379e-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7379e-119">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="7379e-119">Request syntax</span></span>

| <span data-ttu-id="7379e-120">Metod</span><span class="sxs-lookup"><span data-stu-id="7379e-120">Method</span></span>  | <span data-ttu-id="7379e-121">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="7379e-121">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="7379e-122">**Få**</span><span class="sxs-lookup"><span data-stu-id="7379e-122">**GET**</span></span> | <span data-ttu-id="7379e-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/relationships HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="7379e-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/relationships HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="7379e-124">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="7379e-124">URI parameter</span></span>

<span data-ttu-id="7379e-125">Använd följande sökvägsparameter för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="7379e-125">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="7379e-126">Namn</span><span class="sxs-lookup"><span data-stu-id="7379e-126">Name</span></span>        | <span data-ttu-id="7379e-127">Typ</span><span class="sxs-lookup"><span data-stu-id="7379e-127">Type</span></span>   | <span data-ttu-id="7379e-128">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="7379e-128">Required</span></span> | <span data-ttu-id="7379e-129">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="7379e-129">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="7379e-130">kund-id</span><span class="sxs-lookup"><span data-stu-id="7379e-130">customer-id</span></span> | <span data-ttu-id="7379e-131">sträng</span><span class="sxs-lookup"><span data-stu-id="7379e-131">string</span></span> | <span data-ttu-id="7379e-132">Ja</span><span class="sxs-lookup"><span data-stu-id="7379e-132">Yes</span></span>      | <span data-ttu-id="7379e-133">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="7379e-133">A GUID formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="7379e-134">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="7379e-134">Request headers</span></span>

<span data-ttu-id="7379e-135">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="7379e-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7379e-136">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="7379e-136">Request body</span></span>

<span data-ttu-id="7379e-137">Inga.</span><span class="sxs-lookup"><span data-stu-id="7379e-137">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="7379e-138">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="7379e-138">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/relationships HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c9251710-5a30-4cd3-891a-c42d550af9a8
MS-CorrelationId: a96f326c-a392-44f4-bcfe-43152a756ba8
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="7379e-139">REST-svar</span><span class="sxs-lookup"><span data-stu-id="7379e-139">REST response</span></span>

<span data-ttu-id="7379e-140">Om det lyckas innehåller svarstexten en samling [PartnerRelationship-resurser](relationships-resources.md) för att identifiera återförsäljarna.</span><span class="sxs-lookup"><span data-stu-id="7379e-140">If successful, the response body contains a collection of [PartnerRelationship](relationships-resources.md) resources to identify the resellers.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7379e-141">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="7379e-141">Response success and error codes</span></span>

<span data-ttu-id="7379e-142">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="7379e-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7379e-143">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="7379e-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7379e-144">En fullständig lista finns i [Felkoder i Partnercenter.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="7379e-144">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="7379e-145">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="7379e-145">Response example</span></span>

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
