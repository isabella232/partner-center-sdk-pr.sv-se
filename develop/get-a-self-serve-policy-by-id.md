---
title: Hämta en självbetjäningsprincip efter ID
description: Hämtar den angivna självbetjänings principen med hjälp av dess ID.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: ec01d0d9b7c3858cdacf1dbaad3b2b0bb7b6a1a4
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769087"
---
# <a name="get-a-self-serve-policy-by-id"></a><span data-ttu-id="1532d-103">Hämta en självbetjäningsprincip efter ID</span><span class="sxs-lookup"><span data-stu-id="1532d-103">Get a self serve policy by ID</span></span>

<span data-ttu-id="1532d-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="1532d-104">**Applies To**</span></span>

- <span data-ttu-id="1532d-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="1532d-105">Partner Center</span></span>

<span data-ttu-id="1532d-106">Hämtar den angivna självbetjänings principen med hjälp av dess ID.</span><span class="sxs-lookup"><span data-stu-id="1532d-106">Gets the specified self serve policy using its ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1532d-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="1532d-107">Prerequisites</span></span>

- <span data-ttu-id="1532d-108">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="1532d-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1532d-109">Det här scenariot stöder autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="1532d-109">This scenario supports authentication with App+User credentials.</span></span>
- <span data-ttu-id="1532d-110">Ett självbetjänings princip-ID.</span><span class="sxs-lookup"><span data-stu-id="1532d-110">A self serve policy ID.</span></span>

## <a name="examples"></a><span data-ttu-id="1532d-111">Exempel</span><span class="sxs-lookup"><span data-stu-id="1532d-111">Examples</span></span>


## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span data-ttu-id="1532d-112"><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST-begäran</span><span class="sxs-lookup"><span data-stu-id="1532d-112"><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST Request</span></span>

<span data-ttu-id="1532d-113">**Syntax för begäran**</span><span class="sxs-lookup"><span data-stu-id="1532d-113">**Request syntax**</span></span>

| <span data-ttu-id="1532d-114">Metod</span><span class="sxs-lookup"><span data-stu-id="1532d-114">Method</span></span>  | <span data-ttu-id="1532d-115">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="1532d-115">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="1532d-116">**TA**</span><span class="sxs-lookup"><span data-stu-id="1532d-116">**GET**</span></span> | <span data-ttu-id="1532d-117">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="1532d-117">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{id} HTTP/1.1</span></span> |

<span data-ttu-id="1532d-118">**URI-parameter**</span><span class="sxs-lookup"><span data-stu-id="1532d-118">**URI parameter**</span></span>

<span data-ttu-id="1532d-119">Använd följande Sök vägs parametrar för att hämta den angivna produkten.</span><span class="sxs-lookup"><span data-stu-id="1532d-119">Use the following path parameters to get the specified product.</span></span>

| <span data-ttu-id="1532d-120">Namn</span><span class="sxs-lookup"><span data-stu-id="1532d-120">Name</span></span>                       | <span data-ttu-id="1532d-121">Typ</span><span class="sxs-lookup"><span data-stu-id="1532d-121">Type</span></span>         | <span data-ttu-id="1532d-122">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="1532d-122">Required</span></span> | <span data-ttu-id="1532d-123">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="1532d-123">Description</span></span>                                                     |
|----------------------------|--------------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="1532d-124">**SelfServePolicy-ID**</span><span class="sxs-lookup"><span data-stu-id="1532d-124">**SelfServePolicy-id**</span></span>     | <span data-ttu-id="1532d-125">**nollängd**</span><span class="sxs-lookup"><span data-stu-id="1532d-125">**string**</span></span>   | <span data-ttu-id="1532d-126">Yes</span><span class="sxs-lookup"><span data-stu-id="1532d-126">Yes</span></span>      | <span data-ttu-id="1532d-127">En sträng som identifierar den självbetjänings principen.</span><span class="sxs-lookup"><span data-stu-id="1532d-127">A string that identifies the self serve policy.</span></span>                 |

<span data-ttu-id="1532d-128">**Begärandehuvuden**</span><span class="sxs-lookup"><span data-stu-id="1532d-128">**Request headers**</span></span>

- <span data-ttu-id="1532d-129">Se [rubriker](headers.md) för mer information.</span><span class="sxs-lookup"><span data-stu-id="1532d-129">See [Headers](headers.md) for more information.</span></span>

<span data-ttu-id="1532d-130">**Brödtext i begäran**</span><span class="sxs-lookup"><span data-stu-id="1532d-130">**Request body**</span></span>

<span data-ttu-id="1532d-131">Inga.</span><span class="sxs-lookup"><span data-stu-id="1532d-131">None.</span></span>

<span data-ttu-id="1532d-132">**Exempel på begäran**</span><span class="sxs-lookup"><span data-stu-id="1532d-132">**Request example**</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/SelfServePolicy/634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415 HTTP/1.1
Authorization: Bearer  <token>
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a><span data-ttu-id="1532d-133">REST-svar</span><span class="sxs-lookup"><span data-stu-id="1532d-133">REST response</span></span>

<span data-ttu-id="1532d-134">Om det lyckas innehåller svars texten en [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) -resurs.</span><span class="sxs-lookup"><span data-stu-id="1532d-134">If successful, the response body contains a [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource.</span></span>

<span data-ttu-id="1532d-135">**Slutförda svar och felkoder**</span><span class="sxs-lookup"><span data-stu-id="1532d-135">**Response success and error codes**</span></span>

<span data-ttu-id="1532d-136">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="1532d-136">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1532d-137">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="1532d-137">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1532d-138">En fullständig lista finns i [fel koder för partner Center](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="1532d-138">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="1532d-139">Den här metoden returnerar följande fel koder:</span><span class="sxs-lookup"><span data-stu-id="1532d-139">This method returns the following error codes:</span></span>

| <span data-ttu-id="1532d-140">HTTP-statuskod</span><span class="sxs-lookup"><span data-stu-id="1532d-140">HTTP Status Code</span></span>     | <span data-ttu-id="1532d-141">Felkod</span><span class="sxs-lookup"><span data-stu-id="1532d-141">Error code</span></span>   | <span data-ttu-id="1532d-142">Description</span><span class="sxs-lookup"><span data-stu-id="1532d-142">Description</span></span>                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| <span data-ttu-id="1532d-143">404</span><span class="sxs-lookup"><span data-stu-id="1532d-143">404</span></span>                  | <span data-ttu-id="1532d-144">600039</span><span class="sxs-lookup"><span data-stu-id="1532d-144">600039</span></span>       | <span data-ttu-id="1532d-145">Det gick inte att hitta principen för självbetjäning.</span><span class="sxs-lookup"><span data-stu-id="1532d-145">Self serve policy not found.</span></span>                                                     |

<span data-ttu-id="1532d-146">**Exempel på svar**</span><span class="sxs-lookup"><span data-stu-id="1532d-146">**Response example**</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1918
Content-Type: application/json
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
Date: Tue, 23 Jan 2018 23:13:01 GMT

{
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
}
```