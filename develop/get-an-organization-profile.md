---
title: Hämta en organisationsprofil
description: Hämtar ett objekt som representerar partnerns organisations profil.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 132a1e0efa3efea69d4bf649e55b412e300b0685
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769867"
---
# <a name="get-an-organization-profile"></a><span data-ttu-id="29601-103">Hämta en organisationsprofil</span><span class="sxs-lookup"><span data-stu-id="29601-103">Get an organization profile</span></span>

<span data-ttu-id="29601-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="29601-104">**Applies To**</span></span>

- <span data-ttu-id="29601-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="29601-105">Partner Center</span></span>
- <span data-ttu-id="29601-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="29601-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="29601-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="29601-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="29601-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="29601-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="29601-109">Hämtar ett objekt som representerar partnerns organisations profil.</span><span class="sxs-lookup"><span data-stu-id="29601-109">Gets an object representing the partner's organization profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29601-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="29601-110">Prerequisites</span></span>

- <span data-ttu-id="29601-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="29601-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="29601-112">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="29601-112">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="29601-113">C\#</span><span class="sxs-lookup"><span data-stu-id="29601-113">C\#</span></span>

<span data-ttu-id="29601-114">Om du vill hämta din organisations profil använder du din **IAggregatePartner. profiles** -samling och anropar egenskapen **OrganizationProfile** .</span><span class="sxs-lookup"><span data-stu-id="29601-114">To get your organization profile, use your **IAggregatePartner.Profiles** collection and call the **OrganizationProfile** property.</span></span> <span data-ttu-id="29601-115">Anropa slutligen metoderna [**Get ()**](/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.get) eller [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.getasync) .</span><span class="sxs-lookup"><span data-stu-id="29601-115">Finally, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.getasync) methods.</span></span>

```csharp
// IAggregatePartner partnerOperations;

OrganizationProfile organizationProfile = partnerOperations.Profiles.OrganizationProfile.Get();
```

<span data-ttu-id="29601-116">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="29601-116">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="29601-117">**Projekt**: PartnerCenterSDK. FeaturesSamples- **klass**: GetOrganizationProfile.CS</span><span class="sxs-lookup"><span data-stu-id="29601-117">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: GetOrganizationProfile.cs</span></span>

## <a name="java"></a><span data-ttu-id="29601-118">Java</span><span class="sxs-lookup"><span data-stu-id="29601-118">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="29601-119">Om du vill hämta din organisations profil använder du funktionen **IAggregatePartner. getProfiles** och anropar funktionen **getOrganizationProfile** .</span><span class="sxs-lookup"><span data-stu-id="29601-119">To get your organization profile, use your **IAggregatePartner.getProfiles** function and call the **getOrganizationProfile** function.</span></span> <span data-ttu-id="29601-120">Slutligen anropar du funktionen **Get ()** .</span><span class="sxs-lookup"><span data-stu-id="29601-120">Finally, call the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;

OrganizationProfile organizationProfile = partnerOperations.getProfiles().getOrganizationProfile().get();
```

## <a name="powershell"></a><span data-ttu-id="29601-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="29601-121">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="29601-122">Kör kommandot [**Get-PartnerOrganizationProfile**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOrganizationProfile.md) för att hämta din organisations profil.</span><span class="sxs-lookup"><span data-stu-id="29601-122">To get your organization profile, execute the [**Get-PartnerOrganizationProfile**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOrganizationProfile.md) command.</span></span>

```powershell
Get-PartnerOrganizationProfile
```

## <a name="rest-request"></a><span data-ttu-id="29601-123">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="29601-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="29601-124">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="29601-124">Request syntax</span></span>

| <span data-ttu-id="29601-125">Metod</span><span class="sxs-lookup"><span data-stu-id="29601-125">Method</span></span>  | <span data-ttu-id="29601-126">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="29601-126">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="29601-127">**TA**</span><span class="sxs-lookup"><span data-stu-id="29601-127">**GET**</span></span> | <span data-ttu-id="29601-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/Organization http/1.1</span><span class="sxs-lookup"><span data-stu-id="29601-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/organization HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="29601-129">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="29601-129">Request headers</span></span>

<span data-ttu-id="29601-130">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="29601-130">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="29601-131">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="29601-131">Request body</span></span>

<span data-ttu-id="29601-132">Inga.</span><span class="sxs-lookup"><span data-stu-id="29601-132">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="29601-133">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="29601-133">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/organization HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b85cb7ab-cc2e-4966-93f0-cf0d8377a93f
MS-CorrelationId: 1bb03149-88d2-4bc2-9cc1-d6e83890fa9e
```

## <a name="rest-response"></a><span data-ttu-id="29601-134">REST-svar</span><span class="sxs-lookup"><span data-stu-id="29601-134">REST response</span></span>

<span data-ttu-id="29601-135">Om det lyckas returnerar den här metoden ett **OrganizationProfile** -objekt i svars texten.</span><span class="sxs-lookup"><span data-stu-id="29601-135">If successful, this method returns an **OrganizationProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="29601-136">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="29601-136">Response success and error codes</span></span>

<span data-ttu-id="29601-137">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="29601-137">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="29601-138">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="29601-138">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="29601-139">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="29601-139">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="29601-140">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="29601-140">Response example</span></span>

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
