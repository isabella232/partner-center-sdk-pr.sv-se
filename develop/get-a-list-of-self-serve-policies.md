---
title: Hämta en lista över självbetjänings principer
description: Så här hämtar du en samling resurser som representerar en kunds principer för självbetjäning.
ms.date: 07/06/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: ff3116b8757e28e03615930ebd19bc75f34e2efe
ms.sourcegitcommit: 01e75175077611da92175c777a440a594fb05797
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/08/2020
ms.locfileid: "97770241"
---
# <a name="get-a-list-of-self-serve-policies"></a><span data-ttu-id="d80f6-103">Hämta en lista över självbetjänings principer</span><span class="sxs-lookup"><span data-stu-id="d80f6-103">Get a list of self-serve policies</span></span>

<span data-ttu-id="d80f6-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="d80f6-104">**Applies to:**</span></span>

- <span data-ttu-id="d80f6-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="d80f6-105">Partner Center</span></span>

<span data-ttu-id="d80f6-106">Den här artikeln beskriver hur du får en samling resurser som representerar självbetjänings principer för en entitet.</span><span class="sxs-lookup"><span data-stu-id="d80f6-106">This article describes how to get a collection of resources that represents self-serve policies for an entity.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d80f6-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="d80f6-107">Prerequisites</span></span>

- <span data-ttu-id="d80f6-108">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d80f6-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d80f6-109">Det här scenariot stöder autentisering med program-och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="d80f6-109">This scenario supports authentication with Application+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="d80f6-110">C\#</span><span class="sxs-lookup"><span data-stu-id="d80f6-110">C\#</span></span>

<span data-ttu-id="d80f6-111">Så här hämtar du en lista över alla självbetjänings principer:</span><span class="sxs-lookup"><span data-stu-id="d80f6-111">To get a list of all self-serve policies:</span></span>

1. <span data-ttu-id="d80f6-112">Anropa metoden [**IAggregatePartner. SelfServePolicies**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection) med enhets-ID: n för att hämta ett gränssnitt till åtgärder i principerna.</span><span class="sxs-lookup"><span data-stu-id="d80f6-112">Call the [**IAggregatePartner.SelfServePolicies**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection) method with the entity identifier to retrieve an interface to operations on the policies.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// gets the self-serve policies
var SelfServePolicies = scopedPartnerOperations.SelfServePolicies.Get(customerIdAsEntity);
```

<span data-ttu-id="d80f6-113">Ett exempel finns i följande avsnitt:</span><span class="sxs-lookup"><span data-stu-id="d80f6-113">For an example, see the following:</span></span>

- <span data-ttu-id="d80f6-114">Exempel: [konsol test app](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="d80f6-114">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="d80f6-115">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="d80f6-115">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="d80f6-116">Klass: **GetSelfServePolicies.cs**</span><span class="sxs-lookup"><span data-stu-id="d80f6-116">Class: **GetSelfServePolicies.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="d80f6-117">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="d80f6-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d80f6-118">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="d80f6-118">Request syntax</span></span>

| <span data-ttu-id="d80f6-119">Metod</span><span class="sxs-lookup"><span data-stu-id="d80f6-119">Method</span></span>  | <span data-ttu-id="d80f6-120">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="d80f6-120">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="d80f6-121">**TA**</span><span class="sxs-lookup"><span data-stu-id="d80f6-121">**GET**</span></span> | <span data-ttu-id="d80f6-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy? entity_id = {ENTITY_ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="d80f6-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy?entity_id={entity_id} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="d80f6-123">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="d80f6-123">URI parameter</span></span>

<span data-ttu-id="d80f6-124">Använd följande frågeparameter för att hämta en lista över kunder.</span><span class="sxs-lookup"><span data-stu-id="d80f6-124">Use the following query parameter to get a list of customers.</span></span>

| <span data-ttu-id="d80f6-125">Namn</span><span class="sxs-lookup"><span data-stu-id="d80f6-125">Name</span></span>          | <span data-ttu-id="d80f6-126">Typ</span><span class="sxs-lookup"><span data-stu-id="d80f6-126">Type</span></span>       | <span data-ttu-id="d80f6-127">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="d80f6-127">Required</span></span> | <span data-ttu-id="d80f6-128">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="d80f6-128">Description</span></span>                                        |
|---------------|------------|----------|----------------------------------------------------|
| <span data-ttu-id="d80f6-129">**entity_id**</span><span class="sxs-lookup"><span data-stu-id="d80f6-129">**entity_id**</span></span> | <span data-ttu-id="d80f6-130">**nollängd**</span><span class="sxs-lookup"><span data-stu-id="d80f6-130">**string**</span></span> | <span data-ttu-id="d80f6-131">Y</span><span class="sxs-lookup"><span data-stu-id="d80f6-131">Y</span></span>        | <span data-ttu-id="d80f6-132">Enhets-ID: t som begär åtkomst för.</span><span class="sxs-lookup"><span data-stu-id="d80f6-132">The entity identifier requesting access for.</span></span> <span data-ttu-id="d80f6-133">Detta är kundens klient-ID.</span><span class="sxs-lookup"><span data-stu-id="d80f6-133">This will be the customer's tenant ID.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d80f6-134">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="d80f6-134">Request headers</span></span>

<span data-ttu-id="d80f6-135">Mer information finns i [sidhuvud](headers.md).</span><span class="sxs-lookup"><span data-stu-id="d80f6-135">For more information, see [Headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d80f6-136">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="d80f6-136">Request body</span></span>

<span data-ttu-id="d80f6-137">Inga.</span><span class="sxs-lookup"><span data-stu-id="d80f6-137">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d80f6-138">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="d80f6-138">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/SelfServePolicy?entity_id=0431a72c-7d8a-4393-b25e-ef63f5efb415 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a><span data-ttu-id="d80f6-139">REST-svar</span><span class="sxs-lookup"><span data-stu-id="d80f6-139">REST response</span></span>

<span data-ttu-id="d80f6-140">Om det lyckas returnerar den här metoden en samling [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) -resurser i svars texten.</span><span class="sxs-lookup"><span data-stu-id="d80f6-140">If successful, this method returns a collection of [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d80f6-141">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="d80f6-141">Response success and error codes</span></span>

<span data-ttu-id="d80f6-142">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="d80f6-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d80f6-143">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="d80f6-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d80f6-144">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="d80f6-144">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d80f6-145">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="d80f6-145">Response example</span></span>

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
