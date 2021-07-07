---
title: Hämta portalbegäranden utan MFA
description: Hämta en lista över användarbegäranden utan multifaktorautentisering (MFA) med hjälp av REST API.
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.date: 05/29/2020
ms.openlocfilehash: 41627751d3402d7712d96c15c4281a25ed9a44a7
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445586"
---
# <a name="get-portal-requests-without-mfa"></a><span data-ttu-id="3a1f4-103">Hämta portalbegäranden utan MFA</span><span class="sxs-lookup"><span data-stu-id="3a1f4-103">Get portal requests without MFA</span></span>

<span data-ttu-id="3a1f4-104">Den här artikeln beskriver hur du hämtar en lista över de senaste begärandena från användare som använder Partner Center-portalen utan att slutföra multifaktorautentisering (MFA).</span><span class="sxs-lookup"><span data-stu-id="3a1f4-104">This article explains how to obtain a list of the most recent requests from users who access Partner Center portal without completing multi-factor authentication (MFA).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3a1f4-105">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="3a1f4-105">Prerequisites</span></span>

- <span data-ttu-id="3a1f4-106">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="3a1f4-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3a1f4-107">Det här scenariot stöder autentisering med autentiseringsuppgifter för App+Användare.</span><span class="sxs-lookup"><span data-stu-id="3a1f4-107">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="3a1f4-108">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="3a1f4-108">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3a1f4-109">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="3a1f4-109">Request syntax</span></span>

| <span data-ttu-id="3a1f4-110">Metod</span><span class="sxs-lookup"><span data-stu-id="3a1f4-110">Method</span></span>  | <span data-ttu-id="3a1f4-111">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="3a1f4-111">Request URI</span></span>                                                  |
|---------|--------------------------------------------------------------|
| <span data-ttu-id="3a1f4-112">**Få**</span><span class="sxs-lookup"><span data-stu-id="3a1f4-112">**GET**</span></span> | <span data-ttu-id="3a1f4-113">[*{baseURL}*](partner-center-rest-urls.md)/v1/nonMfaCompliantPartnerPrincipals</span><span class="sxs-lookup"><span data-stu-id="3a1f4-113">[*{baseURL}*](partner-center-rest-urls.md)/v1/nonMfaCompliantPartnerPrincipals</span></span> |

### <a name="request-headers"></a><span data-ttu-id="3a1f4-114">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="3a1f4-114">Request headers</span></span>

- <span data-ttu-id="3a1f4-115">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="3a1f4-115">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3a1f4-116">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="3a1f4-116">Request body</span></span>

<span data-ttu-id="3a1f4-117">Inga.</span><span class="sxs-lookup"><span data-stu-id="3a1f4-117">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="3a1f4-118">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="3a1f4-118">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/nonMfaCompliantPartnerPrincipals HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Accept: application/json
MS-RequestId: 8f489776-a3f3-47cb-91c3-538e1f70f560
MS-CorrelationId: e72e1dc3-4abd-4ce0-908b-d23fdaedcb28
Connection: keep-alive

```

## <a name="rest-response"></a><span data-ttu-id="3a1f4-119">REST-svar</span><span class="sxs-lookup"><span data-stu-id="3a1f4-119">REST response</span></span>

<span data-ttu-id="3a1f4-120">Om det lyckas returnerar den här metoden en samling [portalbegäranderesurser](mfa-resources.md#portal-request-without-mfa) i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="3a1f4-120">If successful, this method returns a collection of [Portal request](mfa-resources.md#portal-request-without-mfa) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3a1f4-121">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="3a1f4-121">Response success and error codes</span></span>

<span data-ttu-id="3a1f4-122">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="3a1f4-122">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3a1f4-123">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="3a1f4-123">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3a1f4-124">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="3a1f4-124">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="3a1f4-125">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="3a1f4-125">Response example</span></span>

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
