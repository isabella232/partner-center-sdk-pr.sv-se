---
title: Hämta en lista över alla partneranvändares begäranden
description: Hämta en lista över alla partneranvändares begäranden med hjälp av partner-REST API.
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.date: 05/29/2020
author: cychua
ms.author: cychua
ms.openlocfilehash: 9a367f912669114969f8792a5afcc7020af1112e
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760512"
---
# <a name="get-app-and-user-api-requests"></a><span data-ttu-id="41288-103">Hämta api-begäranden för appar och användare</span><span class="sxs-lookup"><span data-stu-id="41288-103">Get App and User API requests</span></span>

<span data-ttu-id="41288-104">**Gäller för:** Partner Center API</span><span class="sxs-lookup"><span data-stu-id="41288-104">**Applies to**: Partner Center API</span></span>

<span data-ttu-id="41288-105">Den här artikeln beskriver hur du hämtar en lista över alla partneranvändares begäranden inom en klientorganisation med hjälp av REST-API:er.</span><span class="sxs-lookup"><span data-stu-id="41288-105">This article explains how to obtain a list of all partner user requests within a tenant using REST APIs.</span></span>

 > [!NOTE]
 > <span data-ttu-id="41288-106">Det här API:et returnerar endast de senaste API-begäranden som görs av APP + Användar-autentiseringsuppgifter med en maxgräns på 10 000.</span><span class="sxs-lookup"><span data-stu-id="41288-106">This API only returns the most recent API requests made by APP + User credential with maximum 10K limit.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41288-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="41288-107">Prerequisites</span></span>

- <span data-ttu-id="41288-108">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="41288-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="41288-109">Det här scenariot stöder autentisering med autentiseringsuppgifter för App+Användare.</span><span class="sxs-lookup"><span data-stu-id="41288-109">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="41288-110">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="41288-110">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="41288-111">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="41288-111">Request syntax</span></span>

| <span data-ttu-id="41288-112">Metod</span><span class="sxs-lookup"><span data-stu-id="41288-112">Method</span></span>  | <span data-ttu-id="41288-113">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="41288-113">Request URI</span></span>                                                        |
|---------|--------------------------------------------------------------------|
| <span data-ttu-id="41288-114">**Få**</span><span class="sxs-lookup"><span data-stu-id="41288-114">**GET**</span></span> | <span data-ttu-id="41288-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/partnerRequests</span><span class="sxs-lookup"><span data-stu-id="41288-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/partnerRequests</span></span> |

### <a name="request-headers"></a><span data-ttu-id="41288-116">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="41288-116">Request headers</span></span>

- <span data-ttu-id="41288-117">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="41288-117">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="41288-118">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="41288-118">Request body</span></span>

<span data-ttu-id="41288-119">Inga.</span><span class="sxs-lookup"><span data-stu-id="41288-119">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="41288-120">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="41288-120">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/partnerRequests HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Content-Type: application/json
```

## <a name="rest-response"></a><span data-ttu-id="41288-121">REST-svar</span><span class="sxs-lookup"><span data-stu-id="41288-121">REST response</span></span>

<span data-ttu-id="41288-122">Om det lyckas returnerar den här metoden en samling [API-begäranderesurser](mfa-resources.md#api-request-details) i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="41288-122">If successful, this method returns a collection of [API request details](mfa-resources.md#api-request-details) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="41288-123">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="41288-123">Response success and error codes</span></span>

<span data-ttu-id="41288-124">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="41288-124">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="41288-125">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="41288-125">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="41288-126">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="41288-126">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="41288-127">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="41288-127">Response example</span></span>

``` http
HTTP/1.1 200 OK
Content-Length: 2960
Content-Type: application/json
MS-CorrelationId: 4cb80cbe-566b-4d8b-8b8f-af1454b73089
MS-RequestId: 566330a7-1e4b-4848-9c23-f135c70fd810
Date: Thu, 21 May 2020 22:29:17 GMT
{
    "totalCount": 2,
    "items": [
        {
            "requestId": "6c583d8d-46cd-420c-ae3d-35b6dfdcdb21",
            "correlationId": "",
            "operationName": "Get /v{version}/nonMfaCompliantPartnerPrincipals",
            "requestDateTime": "2020-05-21T21:02:10.31",
            "sourceIpAddress": "13.88.20.150",
            "objectId": "c69854fe-5fb4-4527-a28f-f24f1acaffd6",
            "tenantId": "6e6aef4a-4ca9-40a8-b5bf-b53a1923c540",
            "upn": "admin@yourdomain.onmicrosoft.com",
            "applicationId": "60a00bf2-0644-4279-83b3-87ddf96f2509",
            "mfaCompliant": true
        },
        {
            "requestId": "09f8e434-a9ce-43ea-a9ac-270fbb22371a",
            "correlationId": "",
            "operationName": "Get /v{version}/customers/{customer_id}/subscriptions?order_id={order_id_value}&mpn_id={mpn_id_value}",
            "requestDateTime": "2020-05-21T22:18:35.73",
            "sourceIpAddress": "13.88.20.150",
            "objectId": "adc77aa5-7968-4c57-9f48-361018265c1a",
            "tenantId": "6e6aef4a-4ca9-40a8-b5bf-b53a1923c540",
            "upn": "portalnonmfa@yourdomain.onmicrosoft.com",
            "applicationId": "60a00bf2-0644-4279-83b3-87ddf96f2509",
            "mfaCompliant": false
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
