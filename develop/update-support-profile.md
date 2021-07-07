---
title: Uppdatera supportprofil
description: Uppdaterar en användares supportprofil.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 143328c5501f525d52911eead805d420f79b78ff
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530352"
---
# <a name="update-support-profile"></a><span data-ttu-id="e4c19-103">Uppdatera supportprofil</span><span class="sxs-lookup"><span data-stu-id="e4c19-103">Update support profile</span></span>

<span data-ttu-id="e4c19-104">**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="e4c19-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="e4c19-105">Uppdaterar en användares supportprofil.</span><span class="sxs-lookup"><span data-stu-id="e4c19-105">Updates a user's support profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e4c19-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="e4c19-106">Prerequisites</span></span>

- <span data-ttu-id="e4c19-107">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e4c19-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e4c19-108">Det här scenariot stöder endast autentisering med app+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="e4c19-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="e4c19-109">C\#</span><span class="sxs-lookup"><span data-stu-id="e4c19-109">C\#</span></span>

<span data-ttu-id="e4c19-110">Om du vill uppdatera din supportprofil [måste du först hämta din supportprofil](get-support-profile.md) och göra önskade ändringar.</span><span class="sxs-lookup"><span data-stu-id="e4c19-110">To update your support profile, first [get your support profile](get-support-profile.md) and make any changes you wish.</span></span> <span data-ttu-id="e4c19-111">Använd sedan samlingen [**IPartnerOperations.Profiles.**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles)</span><span class="sxs-lookup"><span data-stu-id="e4c19-111">Then, use your [**IPartnerOperations.Profiles**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) collection.</span></span> <span data-ttu-id="e4c19-112">Anropa egenskapen [**SupportProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) följt av metoden [**Update()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.update) eller [**UpdateAsync().**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.updateasync)</span><span class="sxs-lookup"><span data-stu-id="e4c19-112">Call the [**SupportProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) property, followed by the [**Update()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.update) or [**UpdateAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.updateasync) method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

// updated profile
SupportProfile newSupportProfile = new SupportProfile
{
   Email = supportProfile.Email,
   Website = supportProfile.Website,
   Telephone = new Random().Next(10000000, 99999999).ToString(CultureInfo.InvariantCulture)
};

SupportProfile updatedSupportProfile = partnerOperations.Profiles.SupportProfile.Update(newSupportProfile);
```

<span data-ttu-id="e4c19-113">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="e4c19-113">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="e4c19-114">**Project:** PartnerCenterSDK.FeaturesSamples-klass: UpdateSupportProfile.cs </span><span class="sxs-lookup"><span data-stu-id="e4c19-114">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: UpdateSupportProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="e4c19-115">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="e4c19-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e4c19-116">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="e4c19-116">Request syntax</span></span>

| <span data-ttu-id="e4c19-117">Metod</span><span class="sxs-lookup"><span data-stu-id="e4c19-117">Method</span></span>  | <span data-ttu-id="e4c19-118">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="e4c19-118">Request URI</span></span>                                                                     |
|---------|---------------------------------------------------------------------------------|
| <span data-ttu-id="e4c19-119">**PUT**</span><span class="sxs-lookup"><span data-stu-id="e4c19-119">**PUT**</span></span> | <span data-ttu-id="e4c19-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/supportprofile HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e4c19-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/supportprofile HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e4c19-121">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="e4c19-121">Request headers</span></span>

<span data-ttu-id="e4c19-122">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="e4c19-122">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e4c19-123">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="e4c19-123">Request body</span></span>

<span data-ttu-id="e4c19-124">Den fullständiga supportprofilresursen.</span><span class="sxs-lookup"><span data-stu-id="e4c19-124">The full support profile resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="e4c19-125">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="e4c19-125">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/profiles/supportprofile HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 603f3cd9-01b8-48f2-b65d-855a246f5bfd
MS-CorrelationId: 20604323-50bf-4738-9968-c5486ab32be0
Content-Type: application/json
Content-Length: 167
Expect: 100-continue

{
    "Email": "email@sample.com",
    "Telephone": "4255555555",
    "Website": "www.microsoft.com",
    "ProfileType": "support_profile",
    "Attributes": {
        "ObjectType": "PartnerSupportProfile"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="e4c19-126">REST-svar</span><span class="sxs-lookup"><span data-stu-id="e4c19-126">REST response</span></span>

<span data-ttu-id="e4c19-127">Om det lyckas returnerar den här metoden uppdaterade **SupportProfile-objektegenskaper** i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="e4c19-127">If successful, this method returns updated **SupportProfile** object properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e4c19-128">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="e4c19-128">Response success and error codes</span></span>

<span data-ttu-id="e4c19-129">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="e4c19-129">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e4c19-130">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="e4c19-130">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e4c19-131">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="e4c19-131">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e4c19-132">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="e4c19-132">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 502
Content-Type: application/json
MS-CorrelationId: 20604323-50bf-4738-9968-c5486ab32be0
MS-RequestId: 603f3cd9-01b8-48f2-b65d-855a246f5bfd
Date: Wed, 25 Nov 2015 07:16:18 GMT

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
