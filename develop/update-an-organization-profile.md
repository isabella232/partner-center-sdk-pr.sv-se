---
title: Uppdatera en organisationsprofil
description: Uppdaterar en organisations faktureringsprofil.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0ef736a722cde16f95ed6dfdbdab278c98fcf738
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530063"
---
# <a name="update-an-organization-profile"></a><span data-ttu-id="8d03a-103">Uppdatera en organisationsprofil</span><span class="sxs-lookup"><span data-stu-id="8d03a-103">Update an organization profile</span></span>

<span data-ttu-id="8d03a-104">**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="8d03a-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="8d03a-105">Uppdaterar en partners faktureringsprofil.</span><span class="sxs-lookup"><span data-stu-id="8d03a-105">Updates a partner's billing profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d03a-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="8d03a-106">Prerequisites</span></span>

- <span data-ttu-id="8d03a-107">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="8d03a-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8d03a-108">Det här scenariot har endast stöd för autentisering med app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="8d03a-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="8d03a-109">C\#</span><span class="sxs-lookup"><span data-stu-id="8d03a-109">C\#</span></span>

<span data-ttu-id="8d03a-110">Om du vill uppdatera din organisationsprofil hämtar du profilen och gör nödvändiga ändringar.</span><span class="sxs-lookup"><span data-stu-id="8d03a-110">To update your organization profile, retrieve the profile and make any necessary changes.</span></span> <span data-ttu-id="8d03a-111">Använd sedan samlingen **IAggregatePartner.Profiles** och anropa egenskapen **OrganizationProfile.**</span><span class="sxs-lookup"><span data-stu-id="8d03a-111">Then, use your **IAggregatePartner.Profiles** collection and call the **OrganizationProfile** property.</span></span> <span data-ttu-id="8d03a-112">Anropa slutligen metoden **Update().**</span><span class="sxs-lookup"><span data-stu-id="8d03a-112">Finally, call the **Update()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

OrganizationProfile organizationProfile = partnerOperations.Profiles.OrganizationProfile.Get();

// Generating a random phone number to update in the organization profile
organizationProfile.DefaultAddress.PhoneNumber = ((long)(new Random().NextDouble() * 9000000000) + 1000000000).ToString(CultureInfo.InvariantCulture);

OrganizationProfile updatedOrganizationProfile = partnerOperations.Profiles.OrganizationProfile.Update(organizationProfile);
```

<span data-ttu-id="8d03a-113">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="8d03a-113">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="8d03a-114">**Project:** PartnerCenterSDK.FeaturesSamples-klass: UpdateOrganizationProfile.cs </span><span class="sxs-lookup"><span data-stu-id="8d03a-114">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: UpdateOrganizationProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="8d03a-115">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="8d03a-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8d03a-116">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="8d03a-116">Request syntax</span></span>

| <span data-ttu-id="8d03a-117">Metod</span><span class="sxs-lookup"><span data-stu-id="8d03a-117">Method</span></span>  | <span data-ttu-id="8d03a-118">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="8d03a-118">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="8d03a-119">**PUT**</span><span class="sxs-lookup"><span data-stu-id="8d03a-119">**PUT**</span></span> | <span data-ttu-id="8d03a-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/organization HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="8d03a-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/organization HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="8d03a-121">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="8d03a-121">Request headers</span></span>

<span data-ttu-id="8d03a-122">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="8d03a-122">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8d03a-123">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="8d03a-123">Request body</span></span>

<span data-ttu-id="8d03a-124">Inga.</span><span class="sxs-lookup"><span data-stu-id="8d03a-124">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="8d03a-125">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="8d03a-125">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="8d03a-126">REST-svar</span><span class="sxs-lookup"><span data-stu-id="8d03a-126">REST response</span></span>

<span data-ttu-id="8d03a-127">Om det lyckas returnerar den här metoden **ett OrganizationProfile-objekt** i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="8d03a-127">If successful, this method returns an **OrganizationProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8d03a-128">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="8d03a-128">Response success and error codes</span></span>

<span data-ttu-id="8d03a-129">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="8d03a-129">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8d03a-130">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="8d03a-130">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8d03a-131">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="8d03a-131">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="8d03a-132">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="8d03a-132">Response example</span></span>

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
