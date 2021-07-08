---
title: Hämta en organisationsprofil
description: Hämtar ett objekt som representerar partnerns organisationsprofil.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 1c7272761612e573388d4facea1a78808a5bad52
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760563"
---
# <a name="get-an-organization-profile"></a><span data-ttu-id="702e5-103">Hämta en organisationsprofil</span><span class="sxs-lookup"><span data-stu-id="702e5-103">Get an organization profile</span></span>

<span data-ttu-id="702e5-104">**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="702e5-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="702e5-105">Hämtar ett objekt som representerar partnerns organisationsprofil.</span><span class="sxs-lookup"><span data-stu-id="702e5-105">Gets an object representing the partner's organization profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="702e5-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="702e5-106">Prerequisites</span></span>

- <span data-ttu-id="702e5-107">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="702e5-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="702e5-108">Det här scenariot stöder endast autentisering med app+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="702e5-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="702e5-109">C\#</span><span class="sxs-lookup"><span data-stu-id="702e5-109">C\#</span></span>

<span data-ttu-id="702e5-110">Hämta din organisationsprofil genom att använda samlingen **IAggregatePartner.Profiles** och anropa egenskapen **OrganizationProfile.**</span><span class="sxs-lookup"><span data-stu-id="702e5-110">To get your organization profile, use your **IAggregatePartner.Profiles** collection and call the **OrganizationProfile** property.</span></span> <span data-ttu-id="702e5-111">Anropa slutligen metoderna [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.get) eller [**GetAsync().**](/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.getasync)</span><span class="sxs-lookup"><span data-stu-id="702e5-111">Finally, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.getasync) methods.</span></span>

```csharp
// IAggregatePartner partnerOperations;

OrganizationProfile organizationProfile = partnerOperations.Profiles.OrganizationProfile.Get();
```

<span data-ttu-id="702e5-112">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="702e5-112">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="702e5-113">**Project:** PartnerCenterSDK.FeaturesSamples-klass: GetOrganizationProfile.cs </span><span class="sxs-lookup"><span data-stu-id="702e5-113">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: GetOrganizationProfile.cs</span></span>

## <a name="java"></a><span data-ttu-id="702e5-114">Java</span><span class="sxs-lookup"><span data-stu-id="702e5-114">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="702e5-115">Hämta din organisationsprofil genom att använda **funktionen IAggregatePartner.getProfiles** och anropa **funktionen getOrganizationProfile.**</span><span class="sxs-lookup"><span data-stu-id="702e5-115">To get your organization profile, use your **IAggregatePartner.getProfiles** function and call the **getOrganizationProfile** function.</span></span> <span data-ttu-id="702e5-116">Anropa slutligen funktionen **get().**</span><span class="sxs-lookup"><span data-stu-id="702e5-116">Finally, call the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;

OrganizationProfile organizationProfile = partnerOperations.getProfiles().getOrganizationProfile().get();
```

## <a name="powershell"></a><span data-ttu-id="702e5-117">PowerShell</span><span class="sxs-lookup"><span data-stu-id="702e5-117">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="702e5-118">Hämta din organisationsprofil genom att köra kommandot [**Get-PartnerOrganizationProfile.**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOrganizationProfile.md)</span><span class="sxs-lookup"><span data-stu-id="702e5-118">To get your organization profile, execute the [**Get-PartnerOrganizationProfile**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOrganizationProfile.md) command.</span></span>

```powershell
Get-PartnerOrganizationProfile
```

## <a name="rest-request"></a><span data-ttu-id="702e5-119">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="702e5-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="702e5-120">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="702e5-120">Request syntax</span></span>

| <span data-ttu-id="702e5-121">Metod</span><span class="sxs-lookup"><span data-stu-id="702e5-121">Method</span></span>  | <span data-ttu-id="702e5-122">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="702e5-122">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="702e5-123">**Få**</span><span class="sxs-lookup"><span data-stu-id="702e5-123">**GET**</span></span> | <span data-ttu-id="702e5-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/organization HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="702e5-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/organization HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="702e5-125">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="702e5-125">Request headers</span></span>

<span data-ttu-id="702e5-126">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="702e5-126">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="702e5-127">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="702e5-127">Request body</span></span>

<span data-ttu-id="702e5-128">Inga.</span><span class="sxs-lookup"><span data-stu-id="702e5-128">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="702e5-129">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="702e5-129">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/organization HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b85cb7ab-cc2e-4966-93f0-cf0d8377a93f
MS-CorrelationId: 1bb03149-88d2-4bc2-9cc1-d6e83890fa9e
```

## <a name="rest-response"></a><span data-ttu-id="702e5-130">REST-svar</span><span class="sxs-lookup"><span data-stu-id="702e5-130">REST response</span></span>

<span data-ttu-id="702e5-131">Om det lyckas returnerar den här metoden **ett OrganizationProfile-objekt** i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="702e5-131">If successful, this method returns an **OrganizationProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="702e5-132">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="702e5-132">Response success and error codes</span></span>

<span data-ttu-id="702e5-133">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="702e5-133">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="702e5-134">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="702e5-134">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="702e5-135">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="702e5-135">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="702e5-136">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="702e5-136">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 648
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 1bb03149-88d2-4bc2-9cc1-d6e83890fa9e
MS-RequestId: b85cb7ab-cc2e-4966-93f0-cf0d8377a93f
Date: Tue, 22 Mar 2016 17:11:06 GMT

{
    "id":<id>,
    "companyName":"TEST_TEST_BugBash1",
    "defaultAddress":{
        "country":"US",
        "city":"Redmond",
        "state":"WA",
        "addressLine1":"Two Microsoft Way",
        "addressLine2":"",
        "postalCode":"98052",
        "firstName":"Test",
        "lastName":"Account",
        "phoneNumber":""
    },
    "tenantId":<tenantID>,
    "domain":"testtestbugbash1.onmicrosoft.com",
    "email":"test-partner@microsoft.com",
    "language":"es",
    "culture":"es-US",
    "profileType":"OrganizationProfile",
    "links":{
        "self":{
            "uri":"/profiles/organization",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "etag":<etag>,
        "objectType":"OrganizationProfile"
    }
}
```
