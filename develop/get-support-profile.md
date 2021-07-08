---
title: Hämta supportprofil
description: Hämtar ett objekt som representerar en användares supportprofil.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b112ccbbff731795c21f95845a08be9e9dfb6775
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548642"
---
# <a name="get-support-profile"></a><span data-ttu-id="145e2-103">Hämta supportprofil</span><span class="sxs-lookup"><span data-stu-id="145e2-103">Get support profile</span></span>

<span data-ttu-id="145e2-104">**Gäller för**: Partner Center-| PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="145e2-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="145e2-105">Hämtar ett objekt som representerar en användares supportprofil.</span><span class="sxs-lookup"><span data-stu-id="145e2-105">Gets an object representing a user's support profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="145e2-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="145e2-106">Prerequisites</span></span>

- <span data-ttu-id="145e2-107">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="145e2-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="145e2-108">Det här scenariot stöder endast autentisering med app+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="145e2-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="145e2-109">C\#</span><span class="sxs-lookup"><span data-stu-id="145e2-109">C\#</span></span>

<span data-ttu-id="145e2-110">Hämta din supportprofil genom att använda samlingen **IAggregatePartner.Profiles.**</span><span class="sxs-lookup"><span data-stu-id="145e2-110">To get your support profile, use your **IAggregatePartner.Profiles** collection.</span></span> <span data-ttu-id="145e2-111">Anropa egenskapen [**SupportProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) följt av [**metoderna Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.get) eller [**GetAsync().**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.getasync)</span><span class="sxs-lookup"><span data-stu-id="145e2-111">Call the [**SupportProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) property, followed by the [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

SupportProfile supportProfile = partnerOperations.Profiles.SupportProfile.Get();
```

<span data-ttu-id="145e2-112">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="145e2-112">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="145e2-113">**Project:** PartnerCenterSDK.FeaturesSamples-klass: GetSupportProfile.cs </span><span class="sxs-lookup"><span data-stu-id="145e2-113">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: GetSupportProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="145e2-114">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="145e2-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="145e2-115">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="145e2-115">Request syntax</span></span>

| <span data-ttu-id="145e2-116">Metod</span><span class="sxs-lookup"><span data-stu-id="145e2-116">Method</span></span>  | <span data-ttu-id="145e2-117">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="145e2-117">Request URI</span></span>                                                              |
|---------|--------------------------------------------------------------------------|
| <span data-ttu-id="145e2-118">**Få**</span><span class="sxs-lookup"><span data-stu-id="145e2-118">**GET**</span></span> | <span data-ttu-id="145e2-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/support HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="145e2-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/support HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="145e2-120">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="145e2-120">Request headers</span></span>

<span data-ttu-id="145e2-121">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="145e2-121">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="145e2-122">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="145e2-122">Request body</span></span>

<span data-ttu-id="145e2-123">Inga.</span><span class="sxs-lookup"><span data-stu-id="145e2-123">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="145e2-124">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="145e2-124">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/support HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 07029132-385d-416f-a9a6-df5e9e4c78d3
MS-CorrelationId: 20604323-50bf-4738-9968-c5486ab32be0
```

## <a name="rest-response"></a><span data-ttu-id="145e2-125">REST-svar</span><span class="sxs-lookup"><span data-stu-id="145e2-125">REST response</span></span>

<span data-ttu-id="145e2-126">Om det lyckas returnerar den här metoden **ett SupportProfile-objekt** i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="145e2-126">If successful, this method returns a **SupportProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="145e2-127">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="145e2-127">Response success and error codes</span></span>

<span data-ttu-id="145e2-128">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="145e2-128">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="145e2-129">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="145e2-129">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="145e2-130">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="145e2-130">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="145e2-131">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="145e2-131">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 502
Content-Type: application/json
MS-CorrelationId: 20604323-50bf-4738-9968-c5486ab32be0
MS-RequestId: 07029132-385d-416f-a9a6-df5e9e4c78d3
Date: Wed, 25 Nov 2015 07:16:17 GMT

{
    "email": "email@sample.com",
    "telephone": "4255555555",
    "website": "www.microsoft.com",
    "profileType": "support_profile",
    "links": {
        "self": {
            "uri": "/v1/profiles/support",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "PartnerSupportProfile"
    }
}
```
