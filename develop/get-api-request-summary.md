---
title: Hämta MFA-implementeringsstatus
description: Hämta en lista över implementeringsstatus för multifaktorautentisering för varje partner med hjälp av partner-REST API.
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.date: 05/29/2020
author: amitravat
ms.author: amrava
ms.openlocfilehash: 9b8848c2a4531dd6609f86aae6876cec436eeea9
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760529"
---
# <a name="get-mfa-adoption-status"></a><span data-ttu-id="3f474-103">Hämta MFA-implementeringsstatus</span><span class="sxs-lookup"><span data-stu-id="3f474-103">Get MFA adoption status</span></span>

<span data-ttu-id="3f474-104">**Gäller för:** Partner Center API</span><span class="sxs-lookup"><span data-stu-id="3f474-104">**Applies to**: Partner Center API</span></span>

<span data-ttu-id="3f474-105">Den här artikeln förklarar hur du hämtar implementeringsstatusen för multifaktorautentisering (MFA) för varje partner i en klientorganisation.</span><span class="sxs-lookup"><span data-stu-id="3f474-105">This article explains how to get the multi-factor authentication (MFA) adoption status for each partner within a tenant.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3f474-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="3f474-106">Prerequisites</span></span>

- <span data-ttu-id="3f474-107">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="3f474-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3f474-108">Det här scenariot stöder autentisering med autentiseringsuppgifter för App+Användare.</span><span class="sxs-lookup"><span data-stu-id="3f474-108">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="3f474-109">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="3f474-109">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3f474-110">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="3f474-110">Request syntax</span></span>

| <span data-ttu-id="3f474-111">Metod</span><span class="sxs-lookup"><span data-stu-id="3f474-111">Method</span></span>  | <span data-ttu-id="3f474-112">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="3f474-112">Request URI</span></span>                                                               |
|---------|---------------------------------------------------------------------------|
| <span data-ttu-id="3f474-113">**Få**</span><span class="sxs-lookup"><span data-stu-id="3f474-113">**GET**</span></span> | <span data-ttu-id="3f474-114">[*{baseURL}*](partner-center-rest-urls.md)/v1/applicationmfaadoptionstatus></span><span class="sxs-lookup"><span data-stu-id="3f474-114">[*{baseURL}*](partner-center-rest-urls.md)/v1/applicationmfaadoptionstatus></span></span> |

### <a name="request-headers"></a><span data-ttu-id="3f474-115">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="3f474-115">Request headers</span></span>

- <span data-ttu-id="3f474-116">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="3f474-116">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3f474-117">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="3f474-117">Request body</span></span>

<span data-ttu-id="3f474-118">Inga.</span><span class="sxs-lookup"><span data-stu-id="3f474-118">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="3f474-119">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="3f474-119">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/applicationmfaadoptionstatus HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Content-Type: application/json
```

## <a name="rest-response"></a><span data-ttu-id="3f474-120">REST-svar</span><span class="sxs-lookup"><span data-stu-id="3f474-120">REST response</span></span>

<span data-ttu-id="3f474-121">Om det lyckas returnerar den här metoden en samling [API-begäran som sammanfattas av Programresurser](mfa-resources.md#api-request-summarized-by-application) i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="3f474-121">If successful, this method returns a collection of [API request summarized by Application](mfa-resources.md#api-request-summarized-by-application) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3f474-122">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="3f474-122">Response success and error codes</span></span>

<span data-ttu-id="3f474-123">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="3f474-123">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3f474-124">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="3f474-124">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3f474-125">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="3f474-125">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="3f474-126">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="3f474-126">Response example</span></span>

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
