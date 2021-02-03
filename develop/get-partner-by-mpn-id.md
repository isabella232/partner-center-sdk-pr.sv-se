---
title: Verifiera ett partner-MPN-ID
description: Lär dig hur du verifierar en partners Microsoft Partner Network identifierare (MPN-ID) genom att begära partnerns MPN-profil via C \# eller REST API för partner Center.
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6ef7bcb35274a6bcbaddbe0553ca0cb4dc1b2f9c
ms.sourcegitcommit: 8a5c37376a29e29fe0002a980082d4acc6b91131
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/11/2020
ms.locfileid: "97769939"
---
# <a name="verify-a-partner-mpn-id-via-c-or-the-partner-center-rest-api"></a><span data-ttu-id="05e3b-103">Verifiera ett partner MPN-ID via C \# eller partner Center REST API</span><span class="sxs-lookup"><span data-stu-id="05e3b-103">Verify a partner MPN ID via C\# or the Partner Center REST API</span></span>

<span data-ttu-id="05e3b-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="05e3b-104">**Applies To**</span></span>

- <span data-ttu-id="05e3b-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="05e3b-105">Partner Center</span></span>
- <span data-ttu-id="05e3b-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="05e3b-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="05e3b-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="05e3b-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="05e3b-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="05e3b-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="05e3b-109">Så här verifierar du en partners Microsoft Partner Network identifierare (MPN-ID).</span><span class="sxs-lookup"><span data-stu-id="05e3b-109">How to verify a partner's Microsoft Partner Network identifier (MPN ID).</span></span>

<span data-ttu-id="05e3b-110">Den teknik som visas här verifierar partnerns Microsoft Partner Network identifierare genom att begära partnerns MPN-profil från Partner Center.</span><span class="sxs-lookup"><span data-stu-id="05e3b-110">The technique shown here verifies the partner's Microsoft Partner Network identifier by requesting the partner's MPN profile from partner center.</span></span> <span data-ttu-id="05e3b-111">Identifieraren anses vara giltig om begäran lyckas.</span><span class="sxs-lookup"><span data-stu-id="05e3b-111">The identifier is considered valid if the request succeeds.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05e3b-112">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="05e3b-112">Prerequisites</span></span>

- <span data-ttu-id="05e3b-113">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="05e3b-113">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="05e3b-114">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="05e3b-114">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="05e3b-115">Partnerns MPN-ID som ska verifieras.</span><span class="sxs-lookup"><span data-stu-id="05e3b-115">The partner MPN ID to verify.</span></span> <span data-ttu-id="05e3b-116">Om du utelämnar det här värdet hämtar förfrågan MPN-profilen för den inloggade partnern.</span><span class="sxs-lookup"><span data-stu-id="05e3b-116">If you omit this value, the request retrieves the MPN profile of the signed-in partner.</span></span>

## <a name="c"></a><span data-ttu-id="05e3b-117">C\#</span><span class="sxs-lookup"><span data-stu-id="05e3b-117">C\#</span></span>

<span data-ttu-id="05e3b-118">För att verifiera en partners MPN-ID måste du först hämta ett gränssnitt till partner profil insamlings åtgärder från egenskapen [**IAggregatePartner. profiles**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) .</span><span class="sxs-lookup"><span data-stu-id="05e3b-118">To verify a partner's MPN ID, first retrieve an interface to partner profile collection operations from the [**IAggregatePartner.Profiles**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) property.</span></span> <span data-ttu-id="05e3b-119">Hämta sedan ett gränssnitt för att MPN profil åtgärder från egenskapen [**MpnProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.ipartnerprofilecollection.mpnprofile) .</span><span class="sxs-lookup"><span data-stu-id="05e3b-119">Then get an interface to MPN profile operations from the [**MpnProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.ipartnerprofilecollection.mpnprofile) property.</span></span> <span data-ttu-id="05e3b-120">Anropa slutligen metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) med MPN-ID: t för att hämta MPN-profilen.</span><span class="sxs-lookup"><span data-stu-id="05e3b-120">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) methods with the MPN ID to retrieve the MPN profile.</span></span> <span data-ttu-id="05e3b-121">Om du utelämnar MPN-ID: t från get-eller GetAsync-anropet försöker begäran att hämta MPN-profilen för den inloggade partnern.</span><span class="sxs-lookup"><span data-stu-id="05e3b-121">If you omit the MPN ID from the Get or GetAsync call, the request attempts to retrieve the MPN profile of the signed-in partner.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string partnerMpnId;

var partnerProfile = partnerOperations.Profiles.MpnProfile.Get(partnerMpnId);
```

<span data-ttu-id="05e3b-122">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="05e3b-122">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="05e3b-123">**Projekt**: Partner Center SDK-exempel **klass**: VerifyPartnerMpnId.CS</span><span class="sxs-lookup"><span data-stu-id="05e3b-123">**Project**: Partner Center SDK Samples **Class**: VerifyPartnerMpnId.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="05e3b-124">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="05e3b-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="05e3b-125">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="05e3b-125">Request syntax</span></span>

| <span data-ttu-id="05e3b-126">Metod</span><span class="sxs-lookup"><span data-stu-id="05e3b-126">Method</span></span>  | <span data-ttu-id="05e3b-127">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="05e3b-127">Request URI</span></span>                                                                         |
|---------|-------------------------------------------------------------------------------------|
| <span data-ttu-id="05e3b-128">**TA**</span><span class="sxs-lookup"><span data-stu-id="05e3b-128">**GET**</span></span> | <span data-ttu-id="05e3b-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/MPN? mpnId = {MPN-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="05e3b-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/mpn?mpnId={mpn-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="05e3b-130">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="05e3b-130">URI parameter</span></span>

<span data-ttu-id="05e3b-131">Ange följande frågeparameter för att identifiera partnern.</span><span class="sxs-lookup"><span data-stu-id="05e3b-131">Provide the following query parameter to identify the partner.</span></span> <span data-ttu-id="05e3b-132">Om du utelämnar den här Frågeparametern returnerar begäran MPN-profilen för den inloggade partnern.</span><span class="sxs-lookup"><span data-stu-id="05e3b-132">If you omit this query parameter, the request returns the MPN profile of the signed-in partner.</span></span>

| <span data-ttu-id="05e3b-133">Namn</span><span class="sxs-lookup"><span data-stu-id="05e3b-133">Name</span></span>   | <span data-ttu-id="05e3b-134">Typ</span><span class="sxs-lookup"><span data-stu-id="05e3b-134">Type</span></span> | <span data-ttu-id="05e3b-135">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="05e3b-135">Required</span></span> | <span data-ttu-id="05e3b-136">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="05e3b-136">Description</span></span>                                                 |
|--------|------|----------|-------------------------------------------------------------|
| <span data-ttu-id="05e3b-137">MPN-ID</span><span class="sxs-lookup"><span data-stu-id="05e3b-137">mpn-id</span></span> | <span data-ttu-id="05e3b-138">int</span><span class="sxs-lookup"><span data-stu-id="05e3b-138">int</span></span>  | <span data-ttu-id="05e3b-139">No</span><span class="sxs-lookup"><span data-stu-id="05e3b-139">No</span></span>       | <span data-ttu-id="05e3b-140">Ett Microsoft Partner Network-ID som identifierar partnern.</span><span class="sxs-lookup"><span data-stu-id="05e3b-140">A Microsoft Partner Network ID that identifies the partner.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="05e3b-141">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="05e3b-141">Request headers</span></span>

<span data-ttu-id="05e3b-142">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="05e3b-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="05e3b-143">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="05e3b-143">Request body</span></span>

<span data-ttu-id="05e3b-144">Inga.</span><span class="sxs-lookup"><span data-stu-id="05e3b-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="05e3b-145">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="05e3b-145">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="05e3b-146">REST-svar</span><span class="sxs-lookup"><span data-stu-id="05e3b-146">REST response</span></span>

<span data-ttu-id="05e3b-147">Om det lyckas innehåller svars texten [MpnProfile](profile-resources.md#mpnprofile) -resursen för partnern.</span><span class="sxs-lookup"><span data-stu-id="05e3b-147">If successful, the response body contains the [MpnProfile](profile-resources.md#mpnprofile) resource for the partner.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="05e3b-148">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="05e3b-148">Response success and error codes</span></span>

<span data-ttu-id="05e3b-149">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="05e3b-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="05e3b-150">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="05e3b-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="05e3b-151">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="05e3b-151">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example-success"></a><span data-ttu-id="05e3b-152">Svars exempel (lyckades)</span><span class="sxs-lookup"><span data-stu-id="05e3b-152">Response example (success)</span></span>

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

### <a name="response-example-failure"></a><span data-ttu-id="05e3b-153">Svars exempel (haveri)</span><span class="sxs-lookup"><span data-stu-id="05e3b-153">Response example (failure)</span></span>

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
