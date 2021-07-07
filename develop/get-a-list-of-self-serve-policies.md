---
title: Hämta en lista över självbetjäningsprinciper
description: Hur du hämtar en samling resurser som representerar en kunds självbetjäningsprinciper.
ms.date: 07/06/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: b18fde8a11d3ed3dd31e50fdba746dd6b0bf3f97
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025741"
---
# <a name="get-a-list-of-self-serve-policies"></a><span data-ttu-id="d0ef4-103">Hämta en lista över självbetjäningsprinciper</span><span class="sxs-lookup"><span data-stu-id="d0ef4-103">Get a list of self-serve policies</span></span>

<span data-ttu-id="d0ef4-104">Hämtar en samling resurser som representerar självbetjäningsprinciper för en entitet.</span><span class="sxs-lookup"><span data-stu-id="d0ef4-104">Gets a collection of resources that represents self-serve policies for an entity.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d0ef4-105">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="d0ef4-105">Prerequisites</span></span>

- <span data-ttu-id="d0ef4-106">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="d0ef4-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d0ef4-107">Det här scenariot stöder autentisering med autentiseringsuppgifter för program och användare.</span><span class="sxs-lookup"><span data-stu-id="d0ef4-107">This scenario supports authentication with Application+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="d0ef4-108">C\#</span><span class="sxs-lookup"><span data-stu-id="d0ef4-108">C\#</span></span>

<span data-ttu-id="d0ef4-109">Så här hämtar du en lista över alla självbetjäningsprinciper:</span><span class="sxs-lookup"><span data-stu-id="d0ef4-109">To get a list of all self-serve policies:</span></span>

1. <span data-ttu-id="d0ef4-110">Anropa metoden [**IAggregatePartner.SelfServePolicies**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection) med entitetsidentifieraren för att hämta ett gränssnitt till åtgärder för principerna.</span><span class="sxs-lookup"><span data-stu-id="d0ef4-110">Call the [**IAggregatePartner.SelfServePolicies**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection) method with the entity identifier to retrieve an interface to operations on the policies.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// gets the self-serve policies
var SelfServePolicies = scopedPartnerOperations.SelfServePolicies.Get(customerIdAsEntity);
```

<span data-ttu-id="d0ef4-111">Ett exempel finns i följande:</span><span class="sxs-lookup"><span data-stu-id="d0ef4-111">For an example, see the following:</span></span>

- <span data-ttu-id="d0ef4-112">Exempel: [Konsoltestapp](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="d0ef4-112">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="d0ef4-113">Project: **PartnerSDK.FeatureExempel**</span><span class="sxs-lookup"><span data-stu-id="d0ef4-113">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="d0ef4-114">Klass: **GetSelfServePolicies.cs**</span><span class="sxs-lookup"><span data-stu-id="d0ef4-114">Class: **GetSelfServePolicies.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="d0ef4-115">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="d0ef4-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d0ef4-116">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="d0ef4-116">Request syntax</span></span>

| <span data-ttu-id="d0ef4-117">Metod</span><span class="sxs-lookup"><span data-stu-id="d0ef4-117">Method</span></span>  | <span data-ttu-id="d0ef4-118">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="d0ef4-118">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="d0ef4-119">**Få**</span><span class="sxs-lookup"><span data-stu-id="d0ef4-119">**GET**</span></span> | <span data-ttu-id="d0ef4-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy?entity_id={entity_id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d0ef4-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy?entity_id={entity_id} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="d0ef4-121">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="d0ef4-121">URI parameter</span></span>

<span data-ttu-id="d0ef4-122">Använd följande frågeparameter för att hämta en lista över kunder.</span><span class="sxs-lookup"><span data-stu-id="d0ef4-122">Use the following query parameter to get a list of customers.</span></span>

| <span data-ttu-id="d0ef4-123">Namn</span><span class="sxs-lookup"><span data-stu-id="d0ef4-123">Name</span></span>          | <span data-ttu-id="d0ef4-124">Typ</span><span class="sxs-lookup"><span data-stu-id="d0ef4-124">Type</span></span>       | <span data-ttu-id="d0ef4-125">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="d0ef4-125">Required</span></span> | <span data-ttu-id="d0ef4-126">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="d0ef4-126">Description</span></span>                                        |
|---------------|------------|----------|----------------------------------------------------|
| <span data-ttu-id="d0ef4-127">**entity_id**</span><span class="sxs-lookup"><span data-stu-id="d0ef4-127">**entity_id**</span></span> | <span data-ttu-id="d0ef4-128">**sträng**</span><span class="sxs-lookup"><span data-stu-id="d0ef4-128">**string**</span></span> | <span data-ttu-id="d0ef4-129">Y</span><span class="sxs-lookup"><span data-stu-id="d0ef4-129">Y</span></span>        | <span data-ttu-id="d0ef4-130">Den entitetsidentifierare som begär åtkomst.</span><span class="sxs-lookup"><span data-stu-id="d0ef4-130">The entity identifier requesting access for.</span></span> <span data-ttu-id="d0ef4-131">Detta är kundens klientorganisations-ID.</span><span class="sxs-lookup"><span data-stu-id="d0ef4-131">This will be the customer's tenant ID.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d0ef4-132">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="d0ef4-132">Request headers</span></span>

<span data-ttu-id="d0ef4-133">Mer information finns i [Rubriker.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="d0ef4-133">For more information, see [Headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d0ef4-134">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="d0ef4-134">Request body</span></span>

<span data-ttu-id="d0ef4-135">Inga.</span><span class="sxs-lookup"><span data-stu-id="d0ef4-135">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d0ef4-136">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="d0ef4-136">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/SelfServePolicy?entity_id=0431a72c-7d8a-4393-b25e-ef63f5efb415 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a><span data-ttu-id="d0ef4-137">REST-svar</span><span class="sxs-lookup"><span data-stu-id="d0ef4-137">REST response</span></span>

<span data-ttu-id="d0ef4-138">Om det lyckas returnerar den här metoden en samling [SelfServePolicy-resurser](self-serve-policy-resources.md#selfservepolicy) i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="d0ef4-138">If successful, this method returns a collection of [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d0ef4-139">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="d0ef4-139">Response success and error codes</span></span>

<span data-ttu-id="d0ef4-140">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="d0ef4-140">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d0ef4-141">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="d0ef4-141">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d0ef4-142">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="d0ef4-142">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d0ef4-143">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="d0ef4-143">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 15650
Content-Type: application/json
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
Date: Fri, 20 Nov 2015 01:08:23 GMT

{
    "totalCount": 1,
    "items": [{
        "id": "634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415",
        "selfServeEntity": {
            "selfServeEntityType": "customer",
            "tenantID": "0431a72c-7d8a-4393-b25e-ef63f5efb415"
        },
        "grantor": {
            "grantorType": "billToPartner",
            "tenantID": "634f6379-ad54-449b-9821-564f737158ab"
        },
        "permissions": [{
            "resource": "AzureReservedInstances",
            "action": "Purchase"
        }],
        "attributes": {
            "etag": "\"933523d1-3f63-4fc3-8789-5e21c02cdaed\"",
            "objectType": "SelfServePolicy"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}
```
