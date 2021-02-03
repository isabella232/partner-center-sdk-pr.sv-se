---
title: Uppdatera en organisationsprofil
description: Uppdaterar en organisations fakturerings profil.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ccf938fff285704f54d4717b2678e1419d857d8d
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768994"
---
# <a name="update-an-organization-profile"></a><span data-ttu-id="f7721-103">Uppdatera en organisationsprofil</span><span class="sxs-lookup"><span data-stu-id="f7721-103">Update an organization profile</span></span>

<span data-ttu-id="f7721-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="f7721-104">**Applies To**</span></span>

- <span data-ttu-id="f7721-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="f7721-105">Partner Center</span></span>
- <span data-ttu-id="f7721-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="f7721-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="f7721-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="f7721-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="f7721-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="f7721-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="f7721-109">Uppdaterar en partners fakturerings profil.</span><span class="sxs-lookup"><span data-stu-id="f7721-109">Updates a partner's billing profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f7721-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="f7721-110">Prerequisites</span></span>

- <span data-ttu-id="f7721-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="f7721-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f7721-112">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="f7721-112">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="f7721-113">C\#</span><span class="sxs-lookup"><span data-stu-id="f7721-113">C\#</span></span>

<span data-ttu-id="f7721-114">Om du vill uppdatera din organisations profil hämtar du profilen och gör nödvändiga ändringar.</span><span class="sxs-lookup"><span data-stu-id="f7721-114">To update your organization profile, retrieve the profile and make any necessary changes.</span></span> <span data-ttu-id="f7721-115">Använd sedan din **IAggregatePartner. profils** -samling och anropa **OrganizationProfile** -egenskapen.</span><span class="sxs-lookup"><span data-stu-id="f7721-115">Then, use your **IAggregatePartner.Profiles** collection and call the **OrganizationProfile** property.</span></span> <span data-ttu-id="f7721-116">Anropa slutligen metoden **Update ()** .</span><span class="sxs-lookup"><span data-stu-id="f7721-116">Finally, call the **Update()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

OrganizationProfile organizationProfile = partnerOperations.Profiles.OrganizationProfile.Get();

// Generating a random phone number to update in the organization profile
organizationProfile.DefaultAddress.PhoneNumber = ((long)(new Random().NextDouble() * 9000000000) + 1000000000).ToString(CultureInfo.InvariantCulture);

OrganizationProfile updatedOrganizationProfile = partnerOperations.Profiles.OrganizationProfile.Update(organizationProfile);
```

<span data-ttu-id="f7721-117">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="f7721-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="f7721-118">**Projekt**: PartnerCenterSDK. FeaturesSamples- **klass**: UpdateOrganizationProfile.CS</span><span class="sxs-lookup"><span data-stu-id="f7721-118">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: UpdateOrganizationProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="f7721-119">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="f7721-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f7721-120">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="f7721-120">Request syntax</span></span>

| <span data-ttu-id="f7721-121">Metod</span><span class="sxs-lookup"><span data-stu-id="f7721-121">Method</span></span>  | <span data-ttu-id="f7721-122">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="f7721-122">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="f7721-123">**PUT**</span><span class="sxs-lookup"><span data-stu-id="f7721-123">**PUT**</span></span> | <span data-ttu-id="f7721-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/Organization http/1.1</span><span class="sxs-lookup"><span data-stu-id="f7721-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/organization HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="f7721-125">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="f7721-125">Request headers</span></span>

<span data-ttu-id="f7721-126">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="f7721-126">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f7721-127">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="f7721-127">Request body</span></span>

<span data-ttu-id="f7721-128">Inga.</span><span class="sxs-lookup"><span data-stu-id="f7721-128">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="f7721-129">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="f7721-129">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/profiles/organization HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: fe76387b-9658-47d7-939d-0c70032ef589
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
Content-Length: 624
Expect: 100-continue

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

## <a name="rest-response"></a><span data-ttu-id="f7721-130">REST-svar</span><span class="sxs-lookup"><span data-stu-id="f7721-130">REST response</span></span>

<span data-ttu-id="f7721-131">Om det lyckas returnerar den här metoden ett **OrganizationProfile** -objekt i svars texten.</span><span class="sxs-lookup"><span data-stu-id="f7721-131">If successful, this method returns an **OrganizationProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f7721-132">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="f7721-132">Response success and error codes</span></span>

<span data-ttu-id="f7721-133">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="f7721-133">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f7721-134">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="f7721-134">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f7721-135">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="f7721-135">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f7721-136">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="f7721-136">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 648
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
MS-RequestId: fe76387b-9658-47d7-939d-0c70032ef589
Date: Mon, 21 Mar 2016 05:48:41 GMT

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
