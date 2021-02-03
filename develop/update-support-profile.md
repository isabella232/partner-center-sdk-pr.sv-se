---
title: Uppdatera supportprofil
description: Uppdaterar en användares support profil.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 605c509eeb18f301144fec6287c9611d5a5acfe2
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769594"
---
# <a name="update-support-profile"></a><span data-ttu-id="265b3-103">Uppdatera supportprofil</span><span class="sxs-lookup"><span data-stu-id="265b3-103">Update support profile</span></span>

<span data-ttu-id="265b3-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="265b3-104">**Applies To**</span></span>

- <span data-ttu-id="265b3-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="265b3-105">Partner Center</span></span>
- <span data-ttu-id="265b3-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="265b3-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="265b3-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="265b3-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="265b3-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="265b3-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="265b3-109">Uppdaterar en användares support profil.</span><span class="sxs-lookup"><span data-stu-id="265b3-109">Updates a user's support profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="265b3-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="265b3-110">Prerequisites</span></span>

- <span data-ttu-id="265b3-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="265b3-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="265b3-112">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="265b3-112">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="265b3-113">C\#</span><span class="sxs-lookup"><span data-stu-id="265b3-113">C\#</span></span>

<span data-ttu-id="265b3-114">Om du vill uppdatera din support profil måste du först [Hämta din support profil](get-support-profile.md) och göra de ändringar du önskar.</span><span class="sxs-lookup"><span data-stu-id="265b3-114">To update your support profile, first [get your support profile](get-support-profile.md) and make any changes you wish.</span></span> <span data-ttu-id="265b3-115">Använd sedan din [**IPartnerOperations. profils**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) -samling.</span><span class="sxs-lookup"><span data-stu-id="265b3-115">Then, use your [**IPartnerOperations.Profiles**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) collection.</span></span> <span data-ttu-id="265b3-116">Anropa egenskapen [**SupportProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) följt av metoden [**Update ()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.update) eller [**UpdateAsync ()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.updateasync) .</span><span class="sxs-lookup"><span data-stu-id="265b3-116">Call the [**SupportProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) property, followed by the [**Update()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.update) or [**UpdateAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.updateasync) method.</span></span>

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

<span data-ttu-id="265b3-117">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="265b3-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="265b3-118">**Projekt**: PartnerCenterSDK. FeaturesSamples- **klass**: UpdateSupportProfile.CS</span><span class="sxs-lookup"><span data-stu-id="265b3-118">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: UpdateSupportProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="265b3-119">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="265b3-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="265b3-120">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="265b3-120">Request syntax</span></span>

| <span data-ttu-id="265b3-121">Metod</span><span class="sxs-lookup"><span data-stu-id="265b3-121">Method</span></span>  | <span data-ttu-id="265b3-122">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="265b3-122">Request URI</span></span>                                                                     |
|---------|---------------------------------------------------------------------------------|
| <span data-ttu-id="265b3-123">**PUT**</span><span class="sxs-lookup"><span data-stu-id="265b3-123">**PUT**</span></span> | <span data-ttu-id="265b3-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/supportprofile http/1.1</span><span class="sxs-lookup"><span data-stu-id="265b3-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/supportprofile HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="265b3-125">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="265b3-125">Request headers</span></span>

<span data-ttu-id="265b3-126">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="265b3-126">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="265b3-127">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="265b3-127">Request body</span></span>

<span data-ttu-id="265b3-128">Den fullständiga support profil resursen.</span><span class="sxs-lookup"><span data-stu-id="265b3-128">The full support profile resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="265b3-129">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="265b3-129">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="265b3-130">REST-svar</span><span class="sxs-lookup"><span data-stu-id="265b3-130">REST response</span></span>

<span data-ttu-id="265b3-131">Om det lyckas returnerar den här metoden uppdaterade **SupportProfile** objekt egenskaper i svars texten.</span><span class="sxs-lookup"><span data-stu-id="265b3-131">If successful, this method returns updated **SupportProfile** object properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="265b3-132">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="265b3-132">Response success and error codes</span></span>

<span data-ttu-id="265b3-133">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="265b3-133">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="265b3-134">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="265b3-134">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="265b3-135">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="265b3-135">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="265b3-136">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="265b3-136">Response example</span></span>

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
