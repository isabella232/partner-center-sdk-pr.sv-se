---
title: Hämta portalbegäranden utan MFA
description: Hämta en lista över användar förfrågningar utan Multi-Factor Authentication (MFA) med partner REST API.
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.date: 05/29/2020
ms.openlocfilehash: fd350aa3301f00926942ae6c6af359b0d0edc423
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769075"
---
# <a name="get-portal-requests-without-mfa"></a><span data-ttu-id="77ebb-103">Hämta portalbegäranden utan MFA</span><span class="sxs-lookup"><span data-stu-id="77ebb-103">Get portal requests without MFA</span></span>

<span data-ttu-id="77ebb-104">Gäller för:</span><span class="sxs-lookup"><span data-stu-id="77ebb-104">Applies to:</span></span>

- <span data-ttu-id="77ebb-105">Partner Center-API</span><span class="sxs-lookup"><span data-stu-id="77ebb-105">Partner Center API</span></span>

<span data-ttu-id="77ebb-106">Den här artikeln beskriver hur du hämtar en lista över de senaste förfrågningarna från användare som ansluter till Partner Center-portalen utan att slutföra multifaktorautentisering (MFA).</span><span class="sxs-lookup"><span data-stu-id="77ebb-106">This article explains how to obtain a list of the most recent requests from users who access Partner Center portal without completing multi-factor authentication (MFA).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77ebb-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="77ebb-107">Prerequisites</span></span>

- <span data-ttu-id="77ebb-108">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="77ebb-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="77ebb-109">Det här scenariot stöder autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="77ebb-109">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="77ebb-110">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="77ebb-110">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="77ebb-111">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="77ebb-111">Request syntax</span></span>

| <span data-ttu-id="77ebb-112">Metod</span><span class="sxs-lookup"><span data-stu-id="77ebb-112">Method</span></span>  | <span data-ttu-id="77ebb-113">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="77ebb-113">Request URI</span></span>                                                  |
|---------|--------------------------------------------------------------|
| <span data-ttu-id="77ebb-114">**TA**</span><span class="sxs-lookup"><span data-stu-id="77ebb-114">**GET**</span></span> | <span data-ttu-id="77ebb-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/nonMfaCompliantPartnerPrincipals</span><span class="sxs-lookup"><span data-stu-id="77ebb-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/nonMfaCompliantPartnerPrincipals</span></span> |

### <a name="request-headers"></a><span data-ttu-id="77ebb-116">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="77ebb-116">Request headers</span></span>

- <span data-ttu-id="77ebb-117">Mer information finns i [partner Center rest-rubriker](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="77ebb-117">See [Partner Center REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="77ebb-118">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="77ebb-118">Request body</span></span>

<span data-ttu-id="77ebb-119">Inga.</span><span class="sxs-lookup"><span data-stu-id="77ebb-119">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="77ebb-120">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="77ebb-120">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/nonMfaCompliantPartnerPrincipals HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Accept: application/json
MS-RequestId: 8f489776-a3f3-47cb-91c3-538e1f70f560
MS-CorrelationId: e72e1dc3-4abd-4ce0-908b-d23fdaedcb28
Connection: keep-alive

```

## <a name="rest-response"></a><span data-ttu-id="77ebb-121">REST-svar</span><span class="sxs-lookup"><span data-stu-id="77ebb-121">REST response</span></span>

<span data-ttu-id="77ebb-122">Om det lyckas returnerar den här metoden en samling [begär ande](mfa-resources.md#portal-request-without-mfa) resurser för portalen i svars texten.</span><span class="sxs-lookup"><span data-stu-id="77ebb-122">If successful, this method returns a collection of [Portal request](mfa-resources.md#portal-request-without-mfa) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="77ebb-123">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="77ebb-123">Response success and error codes</span></span>

<span data-ttu-id="77ebb-124">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="77ebb-124">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="77ebb-125">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="77ebb-125">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="77ebb-126">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="77ebb-126">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="77ebb-127">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="77ebb-127">Response example</span></span>

``` http
HTTP/1.1 200 OK
Content-Length: 296
Content-Type: application/json
MS-CorrelationId: 4cb80cbe-566b-4d8b-8b8f-af1454b73089
MS-RequestId: 566330a7-1e4b-4848-9c23-f135c70fd810
Date: Thu, 23 Apr 2020 22:10:30 GMT
{
    "totalCount": 1,
    "items": [
        {
            "objectId": "adc77aa5-7968-4c57-9f48-361018265c1a",
            "tenantId": "6e6aef4a-4ca9-40a8-b5bf-b53a1923c540",
            "upn": "portalnonmfa@yourdomain.onmicrosoft.com",
            "lastNonMfaCompliantRequestDateTime": "2020-04-21T22:09:53.051"
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
