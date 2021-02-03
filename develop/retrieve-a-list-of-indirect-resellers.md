---
title: Hämta en lista över indirekta återförsäljare
description: Hämta en lista över den inloggade partnerns indirekta åter försäljare.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e53237b97fa26d3a987f0ee7de491084b596af4a
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769786"
---
# <a name="retrieve-a-list-of-indirect-resellers"></a><span data-ttu-id="a3032-103">Hämta en lista över indirekta återförsäljare</span><span class="sxs-lookup"><span data-stu-id="a3032-103">Retrieve a list of indirect resellers</span></span>

<span data-ttu-id="a3032-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="a3032-104">**Applies To**</span></span>

- <span data-ttu-id="a3032-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="a3032-105">Partner Center</span></span>

<span data-ttu-id="a3032-106">Hämta en lista över den inloggade partnerns indirekta åter försäljare.</span><span class="sxs-lookup"><span data-stu-id="a3032-106">How to retrieve a list of the signed-in partner's indirect resellers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3032-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="a3032-107">Prerequisites</span></span>

- <span data-ttu-id="a3032-108">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="a3032-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a3032-109">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="a3032-109">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="a3032-110">C\#</span><span class="sxs-lookup"><span data-stu-id="a3032-110">C\#</span></span>

<span data-ttu-id="a3032-111">Om du vill hämta en lista över indirekta åter försäljare med vilka den inloggade partnern har en relation, hämtar du först ett gränssnitt till Relations samlings åtgärder från egenskapen [**partnerOperations. Relationships**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) .</span><span class="sxs-lookup"><span data-stu-id="a3032-111">To retrieve a list of indirect resellers with whom the signed-in partner has a relationship, first get an interface to relationship collection operations from the [**partnerOperations.Relationships**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) property.</span></span> <span data-ttu-id="a3032-112">Anropa sedan metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.get) eller [**get \_ async**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.getasync) , och skicka en medlem i [**PartnerRelationshipType**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype) -uppräkningen för att identifiera Relations typen.</span><span class="sxs-lookup"><span data-stu-id="a3032-112">Then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.get) or [**Get\_Async**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.getasync) method, passing a member of the [**PartnerRelationshipType**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype) enumeration to identify the relationship type.</span></span> <span data-ttu-id="a3032-113">Om du vill hämta indirekta åter försäljare måste du använda IsIndirectCloudSolutionProviderOf.</span><span class="sxs-lookup"><span data-stu-id="a3032-113">To retrieve indirect resellers, you must use IsIndirectCloudSolutionProviderOf.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var indirectResellers = partnerOperations.Relationships.Get(PartnerRelationshipType.IsIndirectCloudSolutionProviderOf);
```

<span data-ttu-id="a3032-114">**Exempel**: [konsol test app](console-test-app.md)-**projekt**: Partner Center SDK-exempel **klass**: GetIndirectResellers.CS</span><span class="sxs-lookup"><span data-stu-id="a3032-114">**Sample**: [Console test app](console-test-app.md)**Project**: Partner Center SDK Samples **Class**: GetIndirectResellers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="a3032-115">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="a3032-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a3032-116">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="a3032-116">Request syntax</span></span>

| <span data-ttu-id="a3032-117">Metod</span><span class="sxs-lookup"><span data-stu-id="a3032-117">Method</span></span>  | <span data-ttu-id="a3032-118">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="a3032-118">Request URI</span></span>                                                                                                                |
|---------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a3032-119">**TA**</span><span class="sxs-lookup"><span data-stu-id="a3032-119">**GET**</span></span> | <span data-ttu-id="a3032-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/Relationships? Relations \_ typ = IsIndirectCloudSolutionProviderOf http/1.1</span><span class="sxs-lookup"><span data-stu-id="a3032-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/relationships?relationship\_type=IsIndirectCloudSolutionProviderOf HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="a3032-121">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="a3032-121">URI parameter</span></span>

<span data-ttu-id="a3032-122">Använd följande frågeparameter för att identifiera Relations typen.</span><span class="sxs-lookup"><span data-stu-id="a3032-122">Use the following query parameter to identify the relationship type.</span></span>

| <span data-ttu-id="a3032-123">Namn</span><span class="sxs-lookup"><span data-stu-id="a3032-123">Name</span></span>               | <span data-ttu-id="a3032-124">Typ</span><span class="sxs-lookup"><span data-stu-id="a3032-124">Type</span></span>    | <span data-ttu-id="a3032-125">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="a3032-125">Required</span></span>  | <span data-ttu-id="a3032-126">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="a3032-126">Description</span></span>                         |
|--------------------|---------|-----------|-------------------------------------|
| <span data-ttu-id="a3032-127">relationship_type</span><span class="sxs-lookup"><span data-stu-id="a3032-127">relationship_type</span></span>  | <span data-ttu-id="a3032-128">sträng</span><span class="sxs-lookup"><span data-stu-id="a3032-128">string</span></span>  | <span data-ttu-id="a3032-129">Yes</span><span class="sxs-lookup"><span data-stu-id="a3032-129">Yes</span></span>       | <span data-ttu-id="a3032-130">Värdet är sträng representationen av ett av de medlems namn som finns i [PartnerRelationshipType](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype).</span><span class="sxs-lookup"><span data-stu-id="a3032-130">The value is the string representation of one of the member names found in [PartnerRelationshipType](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype).</span></span><br/><br/> <span data-ttu-id="a3032-131">Om partnern är inloggad som en leverantör och du vill hämta en lista över de indirekta åter försäljare med vilka de har upprättat en relation använder du IsIndirectCloudSolutionProviderOf.</span><span class="sxs-lookup"><span data-stu-id="a3032-131">If the partner is signed in as a provider and you want to get a list of the indirect resellers with whom they have established a relationship, use IsIndirectCloudSolutionProviderOf.</span></span><br/><br/> <span data-ttu-id="a3032-132">Om partnern är inloggad som en åter försäljare och du vill hämta en lista över de indirekta leverantörer med vilka de har upprättat en relation använder du IsIndirectResellerOf.</span><span class="sxs-lookup"><span data-stu-id="a3032-132">If the partner is signed in as a reseller and you want to get a list of the indirect providers with whom they have established a relationship, use IsIndirectResellerOf.</span></span>    |

### <a name="request-headers"></a><span data-ttu-id="a3032-133">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="a3032-133">Request headers</span></span>

<span data-ttu-id="a3032-134">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="a3032-134">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a3032-135">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="a3032-135">Request body</span></span>

<span data-ttu-id="a3032-136">Inga.</span><span class="sxs-lookup"><span data-stu-id="a3032-136">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="a3032-137">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="a3032-137">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/relationships?relationship_type=IsIndirectCloudSolutionProviderOf HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 144391a4-fb06-41ae-b684-3308ce4706bd
MS-CorrelationId: 72524ef8-81aa-4141-a049-45a4fece5d84
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="a3032-138">REST-svar</span><span class="sxs-lookup"><span data-stu-id="a3032-138">REST response</span></span>

<span data-ttu-id="a3032-139">Om det lyckas innehåller svars texten en samling [PartnerRelationship](relationships-resources.md) -resurser för att identifiera åter försäljarna.</span><span class="sxs-lookup"><span data-stu-id="a3032-139">If successful, the response body contains a collection of [PartnerRelationship](relationships-resources.md) resources to identify the resellers.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a3032-140">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="a3032-140">Response success and error codes</span></span>

<span data-ttu-id="a3032-141">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="a3032-141">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a3032-142">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="a3032-142">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a3032-143">En fullständig lista finns i [fel koder för partner Center](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="a3032-143">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a3032-144">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="a3032-144">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 298
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 72524ef8-81aa-4141-a049-45a4fece5d84
MS-RequestId: 144391a4-fb06-41ae-b684-3308ce4706bd
MS-CV: b21Ll1miM0yFMPQQ.0
MS-ServerId: 030020643
Date: Wed, 05 Apr 2017 21:08:44 GMT

{
    "totalCount": 2,
    "items": [{
            "id": "484e548c-f5f3-4528-93a9-c16c6373cb59",
            "name": "First Up Consultants",
            "relationshipType": "is_indirect_cloud_solution_provider_of",
            "state": "Active",
            "mpnId": "4847383",
            "location": "US",
            "attributes": {
                "objectType": "PartnerRelationship"
            }
        }, {
            "id": "b01b1487-b36e-4e6d-9b5e-0b58974c4b28",
            "name": "ReleCloud",
            "relationshipType": "is_indirect_cloud_solution_provider_of",
            "state": "Active",
            "mpnId": "4847433",
            "location": "BR",
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