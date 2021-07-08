---
title: Verifiera ett partner-MPN-ID
description: Lär dig hur du verifierar en partners Microsoft Partner Network-ID (MPN-ID) genom att begära partnerns MPN-profil via C eller \# REST API.
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6bd51850c7bc5a099a34f9c028a58e247c2600a3
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548829"
---
# <a name="verify-a-partner-mpn-id-via-c-or-the-partner-center-rest-api"></a><span data-ttu-id="64dba-103">Verifiera ett PARTNER-MPN-ID via C \# eller partnercenter-REST API</span><span class="sxs-lookup"><span data-stu-id="64dba-103">Verify a partner MPN ID via C\# or the Partner Center REST API</span></span>

<span data-ttu-id="64dba-104">**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="64dba-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="64dba-105">Så här verifierar du en partners Microsoft Partner Network ID (MPN-ID).</span><span class="sxs-lookup"><span data-stu-id="64dba-105">How to verify a partner's Microsoft Partner Network identifier (MPN ID).</span></span>

<span data-ttu-id="64dba-106">Tekniken som visas här verifierar partnerns Microsoft Partner Network identifierare genom att begära partnerns MPN-profil från Partnercenter.</span><span class="sxs-lookup"><span data-stu-id="64dba-106">The technique shown here verifies the partner's Microsoft Partner Network identifier by requesting the partner's MPN profile from partner center.</span></span> <span data-ttu-id="64dba-107">Identifieraren anses vara giltig om begäran lyckas.</span><span class="sxs-lookup"><span data-stu-id="64dba-107">The identifier is considered valid if the request succeeds.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64dba-108">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="64dba-108">Prerequisites</span></span>

- <span data-ttu-id="64dba-109">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="64dba-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="64dba-110">Det här scenariot har endast stöd för autentisering med app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="64dba-110">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="64dba-111">Partnerns MPN-ID som ska verifieras.</span><span class="sxs-lookup"><span data-stu-id="64dba-111">The partner MPN ID to verify.</span></span> <span data-ttu-id="64dba-112">Om du utelämnar det här värdet hämtar begäran MPN-profilen för den inloggade partnern.</span><span class="sxs-lookup"><span data-stu-id="64dba-112">If you omit this value, the request retrieves the MPN profile of the signed-in partner.</span></span>

## <a name="c"></a><span data-ttu-id="64dba-113">C\#</span><span class="sxs-lookup"><span data-stu-id="64dba-113">C\#</span></span>

<span data-ttu-id="64dba-114">Om du vill verifiera en partners MPN-ID hämtar du först ett gränssnitt för insamlingsåtgärder för partnerprofiler [**från egenskapen IAggregatePartner.Profiles.**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles)</span><span class="sxs-lookup"><span data-stu-id="64dba-114">To verify a partner's MPN ID, first retrieve an interface to partner profile collection operations from the [**IAggregatePartner.Profiles**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) property.</span></span> <span data-ttu-id="64dba-115">Hämta sedan ett gränssnitt för MPN-profilåtgärder från [**egenskapen MpnProfile.**](/dotnet/api/microsoft.store.partnercenter.profiles.ipartnerprofilecollection.mpnprofile)</span><span class="sxs-lookup"><span data-stu-id="64dba-115">Then get an interface to MPN profile operations from the [**MpnProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.ipartnerprofilecollection.mpnprofile) property.</span></span> <span data-ttu-id="64dba-116">Anropa slutligen metoderna [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) med MPN-ID:t för att hämta MPN-profilen.</span><span class="sxs-lookup"><span data-stu-id="64dba-116">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) methods with the MPN ID to retrieve the MPN profile.</span></span> <span data-ttu-id="64dba-117">Om du utelämnar MPN-ID:t från Get- eller GetAsync-anropet försöker begäran hämta MPN-profilen för den inloggade partnern.</span><span class="sxs-lookup"><span data-stu-id="64dba-117">If you omit the MPN ID from the Get or GetAsync call, the request attempts to retrieve the MPN profile of the signed-in partner.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string partnerMpnId;

var partnerProfile = partnerOperations.Profiles.MpnProfile.Get(partnerMpnId);
```

<span data-ttu-id="64dba-118">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="64dba-118">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="64dba-119">**Project:** Partnercenter-SDK Samples **Class**: VerifyPartnerMpnId.cs</span><span class="sxs-lookup"><span data-stu-id="64dba-119">**Project**: Partner Center SDK Samples **Class**: VerifyPartnerMpnId.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="64dba-120">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="64dba-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="64dba-121">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="64dba-121">Request syntax</span></span>

| <span data-ttu-id="64dba-122">Metod</span><span class="sxs-lookup"><span data-stu-id="64dba-122">Method</span></span>  | <span data-ttu-id="64dba-123">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="64dba-123">Request URI</span></span>                                                                         |
|---------|-------------------------------------------------------------------------------------|
| <span data-ttu-id="64dba-124">**Få**</span><span class="sxs-lookup"><span data-stu-id="64dba-124">**GET**</span></span> | <span data-ttu-id="64dba-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/mpn?mpnId={mpn-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="64dba-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/mpn?mpnId={mpn-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="64dba-126">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="64dba-126">URI parameter</span></span>

<span data-ttu-id="64dba-127">Ange följande frågeparameter för att identifiera partnern.</span><span class="sxs-lookup"><span data-stu-id="64dba-127">Provide the following query parameter to identify the partner.</span></span> <span data-ttu-id="64dba-128">Om du utelämnar den här frågeparametern returnerar begäran MPN-profilen för den inloggade partnern.</span><span class="sxs-lookup"><span data-stu-id="64dba-128">If you omit this query parameter, the request returns the MPN profile of the signed-in partner.</span></span>

| <span data-ttu-id="64dba-129">Namn</span><span class="sxs-lookup"><span data-stu-id="64dba-129">Name</span></span>   | <span data-ttu-id="64dba-130">Typ</span><span class="sxs-lookup"><span data-stu-id="64dba-130">Type</span></span> | <span data-ttu-id="64dba-131">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="64dba-131">Required</span></span> | <span data-ttu-id="64dba-132">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="64dba-132">Description</span></span>                                                 |
|--------|------|----------|-------------------------------------------------------------|
| <span data-ttu-id="64dba-133">mpn-id</span><span class="sxs-lookup"><span data-stu-id="64dba-133">mpn-id</span></span> | <span data-ttu-id="64dba-134">int</span><span class="sxs-lookup"><span data-stu-id="64dba-134">int</span></span>  | <span data-ttu-id="64dba-135">Inga</span><span class="sxs-lookup"><span data-stu-id="64dba-135">No</span></span>       | <span data-ttu-id="64dba-136">Ett Microsoft Partner Network-ID som identifierar partnern.</span><span class="sxs-lookup"><span data-stu-id="64dba-136">A Microsoft Partner Network ID that identifies the partner.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="64dba-137">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="64dba-137">Request headers</span></span>

<span data-ttu-id="64dba-138">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="64dba-138">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="64dba-139">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="64dba-139">Request body</span></span>

<span data-ttu-id="64dba-140">Inga.</span><span class="sxs-lookup"><span data-stu-id="64dba-140">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="64dba-141">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="64dba-141">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/mpn?mpnId=9999999 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 560df6b9-6e53-4954-aed7-133477ac1194
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="64dba-142">REST-svar</span><span class="sxs-lookup"><span data-stu-id="64dba-142">REST response</span></span>

<span data-ttu-id="64dba-143">Om det lyckas innehåller svarstexten [MpnProfile-resursen](profile-resources.md#mpnprofile) för partnern.</span><span class="sxs-lookup"><span data-stu-id="64dba-143">If successful, the response body contains the [MpnProfile](profile-resources.md#mpnprofile) resource for the partner.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="64dba-144">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="64dba-144">Response success and error codes</span></span>

<span data-ttu-id="64dba-145">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="64dba-145">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="64dba-146">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="64dba-146">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="64dba-147">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="64dba-147">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example-success"></a><span data-ttu-id="64dba-148">Svarsexempel (lyckades)</span><span class="sxs-lookup"><span data-stu-id="64dba-148">Response example (success)</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 159
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: e39e0ddf-3fd0-4b7e-bb4e-8aebe242d3ee
MS-CV: s2GvkNgZsUSadxQX.0
MS-ServerId: 030011719
Date: Thu, 13 Apr 2017 18:13:40 GMT

{
    "mpnId": "4391507",
    "profileType": "MpnProfile",
    "links": {
        "self": {
            "uri": "/profiles/mpn",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "MpnProfile"
    }
}
```

### <a name="response-example-failure"></a><span data-ttu-id="64dba-149">Svarsexempel (fel)</span><span class="sxs-lookup"><span data-stu-id="64dba-149">Response example (failure)</span></span>

```http
HTTP/1.1 404 Not Found
Content-Length: 124
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: 560df6b9-6e53-4954-aed7-133477ac1194
MS-CV: sLRFZMWm+EKuL47u.0
MS-ServerId: 102030524
Date: Thu, 13 Apr 2017 18:26:51 GMT

{
    "code": 3000,
    "description": "Partner Organization with partner_id 9999999 could not be found",
    "data": [],
    "source": "PartnerFD"
}
```
