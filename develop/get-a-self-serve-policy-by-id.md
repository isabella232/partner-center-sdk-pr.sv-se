---
title: Hämta en princip för självbetjäning per ID
description: Hämtar den angivna självbetjäningsprincipen med hjälp av dess ID.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 074d7ba65c7aab91687a67f50e871cee913fc2bb
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873844"
---
# <a name="get-a-self-serve-policy-by-id"></a><span data-ttu-id="a7f41-103">Hämta en princip för självbetjäning per ID</span><span class="sxs-lookup"><span data-stu-id="a7f41-103">Get a self-serve policy by ID</span></span>

<span data-ttu-id="a7f41-104">Hämtar den angivna självbetjäningsprincipen med hjälp av dess ID.</span><span class="sxs-lookup"><span data-stu-id="a7f41-104">Gets the specified self-serve policy using its ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7f41-105">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="a7f41-105">Prerequisites</span></span>

- <span data-ttu-id="a7f41-106">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="a7f41-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a7f41-107">Det här scenariot stöder autentisering med autentiseringsuppgifter för App+Användare.</span><span class="sxs-lookup"><span data-stu-id="a7f41-107">This scenario supports authentication with App+User credentials.</span></span>
- <span data-ttu-id="a7f41-108">Ett princip-ID för självbetjäning.</span><span class="sxs-lookup"><span data-stu-id="a7f41-108">A self-serve policy ID.</span></span>

## <a name="examples"></a><span data-ttu-id="a7f41-109">Exempel</span><span class="sxs-lookup"><span data-stu-id="a7f41-109">Examples</span></span>


## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span data-ttu-id="a7f41-110"><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST-begäran</span><span class="sxs-lookup"><span data-stu-id="a7f41-110"><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST Request</span></span>

<span data-ttu-id="a7f41-111">**Begärandesyntax**</span><span class="sxs-lookup"><span data-stu-id="a7f41-111">**Request syntax**</span></span>

| <span data-ttu-id="a7f41-112">Metod</span><span class="sxs-lookup"><span data-stu-id="a7f41-112">Method</span></span>  | <span data-ttu-id="a7f41-113">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="a7f41-113">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="a7f41-114">**Få**</span><span class="sxs-lookup"><span data-stu-id="a7f41-114">**GET**</span></span> | <span data-ttu-id="a7f41-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="a7f41-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{id} HTTP/1.1</span></span> |

<span data-ttu-id="a7f41-116">**URI-parameter**</span><span class="sxs-lookup"><span data-stu-id="a7f41-116">**URI parameter**</span></span>

<span data-ttu-id="a7f41-117">Använd följande sökvägsparametrar för att hämta den angivna produkten.</span><span class="sxs-lookup"><span data-stu-id="a7f41-117">Use the following path parameters to get the specified product.</span></span>

| <span data-ttu-id="a7f41-118">Namn</span><span class="sxs-lookup"><span data-stu-id="a7f41-118">Name</span></span>                       | <span data-ttu-id="a7f41-119">Typ</span><span class="sxs-lookup"><span data-stu-id="a7f41-119">Type</span></span>         | <span data-ttu-id="a7f41-120">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="a7f41-120">Required</span></span> | <span data-ttu-id="a7f41-121">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="a7f41-121">Description</span></span>                                                     |
|----------------------------|--------------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="a7f41-122">**SelfServePolicy-id**</span><span class="sxs-lookup"><span data-stu-id="a7f41-122">**SelfServePolicy-id**</span></span>     | <span data-ttu-id="a7f41-123">**sträng**</span><span class="sxs-lookup"><span data-stu-id="a7f41-123">**string**</span></span>   | <span data-ttu-id="a7f41-124">Ja</span><span class="sxs-lookup"><span data-stu-id="a7f41-124">Yes</span></span>      | <span data-ttu-id="a7f41-125">En sträng som identifierar självbetjäningsprincipen.</span><span class="sxs-lookup"><span data-stu-id="a7f41-125">A string that identifies the self-serve policy.</span></span>                 |

<span data-ttu-id="a7f41-126">**Begärandehuvuden**</span><span class="sxs-lookup"><span data-stu-id="a7f41-126">**Request headers**</span></span>

- <span data-ttu-id="a7f41-127">Mer information finns i [Rubriker.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="a7f41-127">For more information, see [Headers](headers.md).</span></span>

<span data-ttu-id="a7f41-128">**Begärandetext**</span><span class="sxs-lookup"><span data-stu-id="a7f41-128">**Request body**</span></span>

<span data-ttu-id="a7f41-129">Inga.</span><span class="sxs-lookup"><span data-stu-id="a7f41-129">None.</span></span>

<span data-ttu-id="a7f41-130">**Exempel på begäran**</span><span class="sxs-lookup"><span data-stu-id="a7f41-130">**Request example**</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/SelfServePolicy/634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415 HTTP/1.1
Authorization: Bearer  <token>
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a><span data-ttu-id="a7f41-131">REST-svar</span><span class="sxs-lookup"><span data-stu-id="a7f41-131">REST response</span></span>

<span data-ttu-id="a7f41-132">Om det lyckas innehåller svarstexten en [SelfServePolicy-resurs.](self-serve-policy-resources.md#selfservepolicy)</span><span class="sxs-lookup"><span data-stu-id="a7f41-132">If successful, the response body contains a [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource.</span></span>

<span data-ttu-id="a7f41-133">**Lyckade svar och felkoder**</span><span class="sxs-lookup"><span data-stu-id="a7f41-133">**Response success and error codes**</span></span>

<span data-ttu-id="a7f41-134">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="a7f41-134">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a7f41-135">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="a7f41-135">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a7f41-136">En fullständig lista finns i [Felkoder i Partnercenter.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="a7f41-136">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="a7f41-137">Den här metoden returnerar följande felkoder:</span><span class="sxs-lookup"><span data-stu-id="a7f41-137">This method returns the following error codes:</span></span>

| <span data-ttu-id="a7f41-138">HTTP-statuskod</span><span class="sxs-lookup"><span data-stu-id="a7f41-138">HTTP Status Code</span></span>     | <span data-ttu-id="a7f41-139">Felkod</span><span class="sxs-lookup"><span data-stu-id="a7f41-139">Error code</span></span>   | <span data-ttu-id="a7f41-140">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="a7f41-140">Description</span></span>                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| <span data-ttu-id="a7f41-141">404</span><span class="sxs-lookup"><span data-stu-id="a7f41-141">404</span></span>                  | <span data-ttu-id="a7f41-142">600039</span><span class="sxs-lookup"><span data-stu-id="a7f41-142">600039</span></span>       | <span data-ttu-id="a7f41-143">Det går inte att hitta principen för självbetjäning.</span><span class="sxs-lookup"><span data-stu-id="a7f41-143">Self-serve policy not found.</span></span>                                                     |

<span data-ttu-id="a7f41-144">**Exempel på svar**</span><span class="sxs-lookup"><span data-stu-id="a7f41-144">**Response example**</span></span>

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