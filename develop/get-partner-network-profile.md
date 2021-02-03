---
title: Hämta Microsoft Partner Network-profil
description: Hämtar ett objekt som representerar partnerns MPN-profil.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f8f3e74462da05de0be47964beb34228650b1f53
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769912"
---
# <a name="get-microsoft-partner-network-profile"></a><span data-ttu-id="9aab3-103">Hämta Microsoft Partner Network-profil</span><span class="sxs-lookup"><span data-stu-id="9aab3-103">Get Microsoft Partner Network profile</span></span>

<span data-ttu-id="9aab3-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="9aab3-104">**Applies To**</span></span>

- <span data-ttu-id="9aab3-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="9aab3-105">Partner Center</span></span>
- <span data-ttu-id="9aab3-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="9aab3-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="9aab3-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="9aab3-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="9aab3-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="9aab3-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="9aab3-109">Hämtar ett objekt som representerar partnerns MPN-profil.</span><span class="sxs-lookup"><span data-stu-id="9aab3-109">Gets an object representing the partner's MPN profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9aab3-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="9aab3-110">Prerequisites</span></span>

- <span data-ttu-id="9aab3-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="9aab3-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9aab3-112">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="9aab3-112">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="9aab3-113">C\#</span><span class="sxs-lookup"><span data-stu-id="9aab3-113">C\#</span></span>

<span data-ttu-id="9aab3-114">Om du vill få en partner nätverks profil använder du din **IAggregatePartner. profiles** -samling och anropar egenskapen **MpnProfile** .</span><span class="sxs-lookup"><span data-stu-id="9aab3-114">To get a partner network profile, use your **IAggregatePartner.Profiles** collection and call the **MpnProfile** property.</span></span> <span data-ttu-id="9aab3-115">Anropa slutligen metoderna [**Get ()**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) eller [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) .</span><span class="sxs-lookup"><span data-stu-id="9aab3-115">Finally, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var mpnProfile = partnerOperations.Profiles.MpnProfile.Get();
```

<span data-ttu-id="9aab3-116">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="9aab3-116">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="9aab3-117">**Projekt**:P Artnercentersdk. FeaturesSamples- **klass**: GetMPNProfile.CS</span><span class="sxs-lookup"><span data-stu-id="9aab3-117">**Project**:PartnerCenterSDK.FeaturesSamples **Class**: GetMPNProfile.cs</span></span>

## <a name="java"></a><span data-ttu-id="9aab3-118">Java</span><span class="sxs-lookup"><span data-stu-id="9aab3-118">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="9aab3-119">För att få en partner nätverks profil använder du din **IAggregatePartner. getProfiles** -funktion och anropar funktionen **getMpnProfile** .</span><span class="sxs-lookup"><span data-stu-id="9aab3-119">To get a partner network profile, use your **IAggregatePartner.getProfiles** function and call the **getMpnProfile** function.</span></span> <span data-ttu-id="9aab3-120">Slutligen anropar du funktionen **Get ()** .</span><span class="sxs-lookup"><span data-stu-id="9aab3-120">Finally, call the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;

MpnProfile mpnProfile = partnerOperations.getProfiles().getMpnProfile().get();
```

## <a name="powershell"></a><span data-ttu-id="9aab3-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9aab3-121">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="9aab3-122">Kör kommandot [**Get-PartnerMpnProfile**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerMpnProfile.md) för att få en partner nätverks profil.</span><span class="sxs-lookup"><span data-stu-id="9aab3-122">To get a partner network profile, execute the [**Get-PartnerMpnProfile**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerMpnProfile.md) command.</span></span>

```powershell
Get-PartnerMpnProfile
```

## <a name="rest-request"></a><span data-ttu-id="9aab3-123">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="9aab3-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9aab3-124">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="9aab3-124">Request syntax</span></span>

| <span data-ttu-id="9aab3-125">Metod</span><span class="sxs-lookup"><span data-stu-id="9aab3-125">Method</span></span>  | <span data-ttu-id="9aab3-126">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="9aab3-126">Request URI</span></span>                                                          |
|---------|----------------------------------------------------------------------|
| <span data-ttu-id="9aab3-127">**TA**</span><span class="sxs-lookup"><span data-stu-id="9aab3-127">**GET**</span></span> | <span data-ttu-id="9aab3-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/MPN http/1.1</span><span class="sxs-lookup"><span data-stu-id="9aab3-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/mpn HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="9aab3-129">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="9aab3-129">Request headers</span></span>

<span data-ttu-id="9aab3-130">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="9aab3-130">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9aab3-131">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="9aab3-131">Request body</span></span>

<span data-ttu-id="9aab3-132">Inga.</span><span class="sxs-lookup"><span data-stu-id="9aab3-132">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="9aab3-133">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="9aab3-133">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/mpn HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 76879323-92d1-437e-90dd-c84dbb9f7dec
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="9aab3-134">REST-svar</span><span class="sxs-lookup"><span data-stu-id="9aab3-134">REST response</span></span>

<span data-ttu-id="9aab3-135">Om det lyckas returnerar den här metoden ett **MPNProfile** -objekt i svars texten.</span><span class="sxs-lookup"><span data-stu-id="9aab3-135">If successful, this method returns a **MPNProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9aab3-136">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="9aab3-136">Response success and error codes</span></span>

<span data-ttu-id="9aab3-137">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="9aab3-137">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9aab3-138">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="9aab3-138">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9aab3-139">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9aab3-139">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9aab3-140">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="9aab3-140">Response example</span></span>

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
