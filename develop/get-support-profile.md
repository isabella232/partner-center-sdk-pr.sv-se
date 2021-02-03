---
title: Hämta supportprofil
description: Hämtar ett objekt som representerar en användares support profil.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b8b0fa533aaba74418985ea02cbb13bd722cede2
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769807"
---
# <a name="get-support-profile"></a><span data-ttu-id="7a21f-103">Hämta supportprofil</span><span class="sxs-lookup"><span data-stu-id="7a21f-103">Get support profile</span></span>

<span data-ttu-id="7a21f-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="7a21f-104">**Applies To**</span></span>

- <span data-ttu-id="7a21f-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="7a21f-105">Partner Center</span></span>
- <span data-ttu-id="7a21f-106">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="7a21f-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="7a21f-107">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="7a21f-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="7a21f-108">Hämtar ett objekt som representerar en användares support profil.</span><span class="sxs-lookup"><span data-stu-id="7a21f-108">Gets an object representing a user's support profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a21f-109">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="7a21f-109">Prerequisites</span></span>

- <span data-ttu-id="7a21f-110">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="7a21f-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7a21f-111">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="7a21f-111">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="7a21f-112">C\#</span><span class="sxs-lookup"><span data-stu-id="7a21f-112">C\#</span></span>

<span data-ttu-id="7a21f-113">Använd din **IAggregatePartner.** Profiles-samling för att få din support profil.</span><span class="sxs-lookup"><span data-stu-id="7a21f-113">To get your support profile, use your **IAggregatePartner.Profiles** collection.</span></span> <span data-ttu-id="7a21f-114">Anropa egenskapen [**SupportProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) följt av metoderna [**Get ()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.get) eller [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.getasync) .</span><span class="sxs-lookup"><span data-stu-id="7a21f-114">Call the [**SupportProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) property, followed by the [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

SupportProfile supportProfile = partnerOperations.Profiles.SupportProfile.Get();
```

<span data-ttu-id="7a21f-115">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="7a21f-115">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="7a21f-116">**Projekt**: PartnerCenterSDK. FeaturesSamples- **klass**: GetSupportProfile.CS</span><span class="sxs-lookup"><span data-stu-id="7a21f-116">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: GetSupportProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="7a21f-117">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="7a21f-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7a21f-118">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="7a21f-118">Request syntax</span></span>

| <span data-ttu-id="7a21f-119">Metod</span><span class="sxs-lookup"><span data-stu-id="7a21f-119">Method</span></span>  | <span data-ttu-id="7a21f-120">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="7a21f-120">Request URI</span></span>                                                              |
|---------|--------------------------------------------------------------------------|
| <span data-ttu-id="7a21f-121">**TA**</span><span class="sxs-lookup"><span data-stu-id="7a21f-121">**GET**</span></span> | <span data-ttu-id="7a21f-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/support http/1.1</span><span class="sxs-lookup"><span data-stu-id="7a21f-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/support HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="7a21f-123">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="7a21f-123">Request headers</span></span>

<span data-ttu-id="7a21f-124">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="7a21f-124">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7a21f-125">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="7a21f-125">Request body</span></span>

<span data-ttu-id="7a21f-126">Inga.</span><span class="sxs-lookup"><span data-stu-id="7a21f-126">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="7a21f-127">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="7a21f-127">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/support HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 07029132-385d-416f-a9a6-df5e9e4c78d3
MS-CorrelationId: 20604323-50bf-4738-9968-c5486ab32be0
```

## <a name="rest-response"></a><span data-ttu-id="7a21f-128">REST-svar</span><span class="sxs-lookup"><span data-stu-id="7a21f-128">REST response</span></span>

<span data-ttu-id="7a21f-129">Om det lyckas returnerar den här metoden ett **SupportProfile** -objekt i svars texten.</span><span class="sxs-lookup"><span data-stu-id="7a21f-129">If successful, this method returns a **SupportProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7a21f-130">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="7a21f-130">Response success and error codes</span></span>

<span data-ttu-id="7a21f-131">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="7a21f-131">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7a21f-132">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="7a21f-132">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7a21f-133">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="7a21f-133">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="7a21f-134">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="7a21f-134">Response example</span></span>

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
