---
title: Hämta status för MFA-införande
description: Hämta en lista över implementerings status för Multi-Factor Authentication för varje partner som använder partner REST API.
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.date: 05/29/2020
author: amitravat
ms.author: amrava
ms.openlocfilehash: f82d163b704323c81e2948b78eb9b9d1a14ddc52
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769021"
---
# <a name="get-mfa-adoption-status"></a><span data-ttu-id="3e689-103">Hämta MFA-implementerings status</span><span class="sxs-lookup"><span data-stu-id="3e689-103">Get MFA adoption status</span></span>

<span data-ttu-id="3e689-104">Gäller för:</span><span class="sxs-lookup"><span data-stu-id="3e689-104">Applies to:</span></span>

- <span data-ttu-id="3e689-105">Partner Center-API</span><span class="sxs-lookup"><span data-stu-id="3e689-105">Partner Center API</span></span>

<span data-ttu-id="3e689-106">Den här artikeln förklarar hur du får tillämpnings status för Multi-Factor Authentication (MFA) för varje partner inom en klient organisation.</span><span class="sxs-lookup"><span data-stu-id="3e689-106">This article explains how to get the multi-factor authentication (MFA) adoption status for each partner within a tenant.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e689-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="3e689-107">Prerequisites</span></span>

- <span data-ttu-id="3e689-108">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="3e689-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3e689-109">Det här scenariot stöder autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="3e689-109">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="3e689-110">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="3e689-110">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3e689-111">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="3e689-111">Request syntax</span></span>

| <span data-ttu-id="3e689-112">Metod</span><span class="sxs-lookup"><span data-stu-id="3e689-112">Method</span></span>  | <span data-ttu-id="3e689-113">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="3e689-113">Request URI</span></span>                                                               |
|---------|---------------------------------------------------------------------------|
| <span data-ttu-id="3e689-114">**TA**</span><span class="sxs-lookup"><span data-stu-id="3e689-114">**GET**</span></span> | <span data-ttu-id="3e689-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/applicationmfaadoptionstatus></span><span class="sxs-lookup"><span data-stu-id="3e689-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/applicationmfaadoptionstatus></span></span> |

### <a name="request-headers"></a><span data-ttu-id="3e689-116">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="3e689-116">Request headers</span></span>

- <span data-ttu-id="3e689-117">Mer information finns i [partner Center rest-rubriker](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="3e689-117">See [Partner Center REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="3e689-118">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="3e689-118">Request body</span></span>

<span data-ttu-id="3e689-119">Inga.</span><span class="sxs-lookup"><span data-stu-id="3e689-119">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="3e689-120">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="3e689-120">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/applicationmfaadoptionstatus HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Content-Type: application/json
```

## <a name="rest-response"></a><span data-ttu-id="3e689-121">REST-svar</span><span class="sxs-lookup"><span data-stu-id="3e689-121">REST response</span></span>

<span data-ttu-id="3e689-122">Om det lyckas returnerar den här metoden en samling [API-begäran som sammanfattas av program](mfa-resources.md#api-request-summarized-by-application) resurser i svars texten.</span><span class="sxs-lookup"><span data-stu-id="3e689-122">If successful, this method returns a collection of [API request summarized by Application](mfa-resources.md#api-request-summarized-by-application) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3e689-123">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="3e689-123">Response success and error codes</span></span>

<span data-ttu-id="3e689-124">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="3e689-124">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3e689-125">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="3e689-125">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3e689-126">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="3e689-126">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="3e689-127">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="3e689-127">Response example</span></span>

``` http
HTTP/1.1 200 OK
Content-Length: 313
Content-Type: application/json
MS-CorrelationId: 4cb80cbe-566b-4d8b-8b8f-af1454b73089
MS-RequestId: 566330a7-1e4b-4848-9c23-f135c70fd810
Date: Thu, 21 May 2020 22:29:17 GMT
[
    {
        "loginDate": "2020-05-20",
        "mfaCompliantRequestCount": 7,
        "totalRequestCount": 7,
        "applicationId": "14f38d7d-c4fc-448a-b2df-0fc60e75465a",
        "applicationName": ""
    },
    {
        "loginDate": "2020-05-19",
        "mfaCompliantRequestCount": 7,
        "totalRequestCount": 14,
        "applicationId": "60a00bf2-0644-4279-83b3-87ddf96f2509",
        "applicationName": ""
    }
]
```
