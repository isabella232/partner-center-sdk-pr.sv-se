---
title: Hämta Microsoft Partner Network-profil
description: Hämtar ett objekt som representerar partnerns MPN-profil.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 38c12a9a9755b9838b7742d9f38c5cbd52b81210
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548863"
---
# <a name="get-microsoft-partner-network-profile"></a><span data-ttu-id="05f81-103">Hämta Microsoft Partner Network-profil</span><span class="sxs-lookup"><span data-stu-id="05f81-103">Get Microsoft Partner Network profile</span></span>

<span data-ttu-id="05f81-104">**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="05f81-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="05f81-105">Hämtar ett objekt som representerar partnerns MPN-profil.</span><span class="sxs-lookup"><span data-stu-id="05f81-105">Gets an object representing the partner's MPN profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05f81-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="05f81-106">Prerequisites</span></span>

- <span data-ttu-id="05f81-107">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="05f81-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="05f81-108">Det här scenariot stöder endast autentisering med app+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="05f81-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="05f81-109">C\#</span><span class="sxs-lookup"><span data-stu-id="05f81-109">C\#</span></span>

<span data-ttu-id="05f81-110">Om du vill hämta en partnernätverksprofil använder **du samlingen IAggregatePartner.Profiles** och anropar **egenskapen MpnProfile.**</span><span class="sxs-lookup"><span data-stu-id="05f81-110">To get a partner network profile, use your **IAggregatePartner.Profiles** collection and call the **MpnProfile** property.</span></span> <span data-ttu-id="05f81-111">Anropa slutligen metoderna [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) eller [**GetAsync().**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync)</span><span class="sxs-lookup"><span data-stu-id="05f81-111">Finally, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var mpnProfile = partnerOperations.Profiles.MpnProfile.Get();
```

<span data-ttu-id="05f81-112">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="05f81-112">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="05f81-113">**Project**:P CenterSDK.FeaturesSamples-klass: GetMPNProfile.cs </span><span class="sxs-lookup"><span data-stu-id="05f81-113">**Project**:PartnerCenterSDK.FeaturesSamples **Class**: GetMPNProfile.cs</span></span>

## <a name="java"></a><span data-ttu-id="05f81-114">Java</span><span class="sxs-lookup"><span data-stu-id="05f81-114">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="05f81-115">Om du vill hämta en partnernätverksprofil använder du **funktionen IAggregatePartner.getProfiles** och anropar **funktionen getMpnProfile.**</span><span class="sxs-lookup"><span data-stu-id="05f81-115">To get a partner network profile, use your **IAggregatePartner.getProfiles** function and call the **getMpnProfile** function.</span></span> <span data-ttu-id="05f81-116">Anropa slutligen funktionen **get().**</span><span class="sxs-lookup"><span data-stu-id="05f81-116">Finally, call the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;

MpnProfile mpnProfile = partnerOperations.getProfiles().getMpnProfile().get();
```

## <a name="powershell"></a><span data-ttu-id="05f81-117">PowerShell</span><span class="sxs-lookup"><span data-stu-id="05f81-117">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="05f81-118">Om du vill hämta en nätverksprofil för partner kör du kommandot [**Get-PartnerMpnProfile.**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerMpnProfile.md)</span><span class="sxs-lookup"><span data-stu-id="05f81-118">To get a partner network profile, execute the [**Get-PartnerMpnProfile**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerMpnProfile.md) command.</span></span>

```powershell
Get-PartnerMpnProfile
```

## <a name="rest-request"></a><span data-ttu-id="05f81-119">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="05f81-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="05f81-120">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="05f81-120">Request syntax</span></span>

| <span data-ttu-id="05f81-121">Metod</span><span class="sxs-lookup"><span data-stu-id="05f81-121">Method</span></span>  | <span data-ttu-id="05f81-122">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="05f81-122">Request URI</span></span>                                                          |
|---------|----------------------------------------------------------------------|
| <span data-ttu-id="05f81-123">**Få**</span><span class="sxs-lookup"><span data-stu-id="05f81-123">**GET**</span></span> | <span data-ttu-id="05f81-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/mpn HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="05f81-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/mpn HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="05f81-125">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="05f81-125">Request headers</span></span>

<span data-ttu-id="05f81-126">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="05f81-126">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="05f81-127">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="05f81-127">Request body</span></span>

<span data-ttu-id="05f81-128">Inga.</span><span class="sxs-lookup"><span data-stu-id="05f81-128">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="05f81-129">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="05f81-129">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/mpn HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 76879323-92d1-437e-90dd-c84dbb9f7dec
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="05f81-130">REST-svar</span><span class="sxs-lookup"><span data-stu-id="05f81-130">REST response</span></span>

<span data-ttu-id="05f81-131">Om det lyckas returnerar den här metoden **ett MPNProfile-objekt** i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="05f81-131">If successful, this method returns a **MPNProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="05f81-132">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="05f81-132">Response success and error codes</span></span>

<span data-ttu-id="05f81-133">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="05f81-133">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="05f81-134">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="05f81-134">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="05f81-135">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="05f81-135">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="05f81-136">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="05f81-136">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
MS-RequestId: 76879323-92d1-437e-90dd-c84dbb9f7dec
Date: Mon, 21 Mar 2016 05:51:29 GMT

{
    "mpnId":"<mpnID>",
    "profileType":"MpnProfile",
    "links":{
        "self":{
            "uri":"/profiles/mpn",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "objectType":"MpnProfile"
    }
}
```
