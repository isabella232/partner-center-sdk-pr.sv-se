---
title: Uppdatera partnerns juridiska företagsprofil
description: Så här uppdaterar du partnerns juridiska affärsprofil.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: parthpandyaMSFT
ms.author: parthp
ms.openlocfilehash: cb9f5815e0019c5e9b648dfd865e9752f0afdf05
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530335"
---
# <a name="update-the-partner-legal-business-profile"></a><span data-ttu-id="62fc1-103">Uppdatera partnerns juridiska företagsprofil</span><span class="sxs-lookup"><span data-stu-id="62fc1-103">Update the partner legal business profile</span></span>

<span data-ttu-id="62fc1-104">**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="62fc1-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="62fc1-105">Så här uppdaterar du partnerns juridiska affärsprofil.</span><span class="sxs-lookup"><span data-stu-id="62fc1-105">How to update the partner legal business profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="62fc1-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="62fc1-106">Prerequisites</span></span>

- <span data-ttu-id="62fc1-107">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="62fc1-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="62fc1-108">Det här scenariot har endast stöd för autentisering med app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="62fc1-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="62fc1-109">C\#</span><span class="sxs-lookup"><span data-stu-id="62fc1-109">C\#</span></span>

<span data-ttu-id="62fc1-110">Om du vill uppdatera partnerns juridiska affärsprofil instansierar du först **ett LegalBusinessProfile-objekt** och fyller det med den befintliga profilen.</span><span class="sxs-lookup"><span data-stu-id="62fc1-110">To update the partner legal business profile, first instantiate a **LegalBusinessProfile** object and populate it with the existing profile.</span></span> <span data-ttu-id="62fc1-111">Mer information finns i Hämta [partnerns juridiska företagsprofil](get-legal-business-profile.md).</span><span class="sxs-lookup"><span data-stu-id="62fc1-111">For more information, see [Get the partner legal business profile](get-legal-business-profile.md).</span></span> <span data-ttu-id="62fc1-112">Uppdatera sedan de egenskaper som du behöver ändra.</span><span class="sxs-lookup"><span data-stu-id="62fc1-112">Then, update the properties that you need to change.</span></span> <span data-ttu-id="62fc1-113">I följande kodexempel visas hur du ändrar adress- och primära kontakttelefonnummer.</span><span class="sxs-lookup"><span data-stu-id="62fc1-113">The following code example illustrates changing the address and primary contact phone numbers.</span></span>

<span data-ttu-id="62fc1-114">Hämta sedan ett gränssnitt till partnerprofilens driftsamling från egenskapen **IAggregatePartner.Profiles.**</span><span class="sxs-lookup"><span data-stu-id="62fc1-114">Next, get an interface to the partner profile operations collection from the **IAggregatePartner.Profiles** property.</span></span> <span data-ttu-id="62fc1-115">Hämta sedan värdet för egenskapen **LegalBusinessProfile** för att hämta ett gränssnitt för juridiska affärsprofilåtgärder.</span><span class="sxs-lookup"><span data-stu-id="62fc1-115">Then, retrieve the value of the **LegalBusinessProfile** property to get an interface to legal business profile operations.</span></span> <span data-ttu-id="62fc1-116">Anropa slutligen metoden [**Update**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.update) eller [**UpdateAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.updateasync) med det ändrade objektet för att uppdatera profilen.</span><span class="sxs-lookup"><span data-stu-id="62fc1-116">Finally, call the [**Update**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.update) or [**UpdateAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.updateasync) method with the changed object to update the profile.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var legalBusinessProfile = partnerOperations.Profiles.LegalBusinessProfile.Get();

// Change the address and primary contact phone number.
legalBusinessProfile.Address.PhoneNumber = "4255550110";
legalBusinessProfile.PrimaryContact.PhoneNumber = "4255550110";

// Apply changes to the profile.
var updatedLegalBusinessProfile = partnerOperations.Profiles.LegalBusinessProfile.Update(legalBusinessProfile);
```

## <a name="rest-request"></a><span data-ttu-id="62fc1-117">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="62fc1-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="62fc1-118">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="62fc1-118">Request syntax</span></span>

| <span data-ttu-id="62fc1-119">Metod</span><span class="sxs-lookup"><span data-stu-id="62fc1-119">Method</span></span>  | <span data-ttu-id="62fc1-120">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="62fc1-120">Request URI</span></span>                                                                    |
|---------|--------------------------------------------------------------------------------|
| <span data-ttu-id="62fc1-121">**PUT**</span><span class="sxs-lookup"><span data-stu-id="62fc1-121">**PUT**</span></span> | <span data-ttu-id="62fc1-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/legalbusiness HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="62fc1-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/legalbusiness HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="62fc1-123">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="62fc1-123">Request headers</span></span>

<span data-ttu-id="62fc1-124">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="62fc1-124">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="62fc1-125">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="62fc1-125">Request body</span></span>

<span data-ttu-id="62fc1-126">Resursen för juridisk företagsprofil.</span><span class="sxs-lookup"><span data-stu-id="62fc1-126">The legal business profile resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="62fc1-127">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="62fc1-127">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/profiles/legalbusiness HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4549ac0c-0f1d-4d8f-b02f-6d36fadcccee
MS-CorrelationId: aa2a0d8c-7a41-470f-97ae-b82e6c338ee4
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 806
Expect: 100-continue

{
    "CompanyName": "Lucerne Publishing",
    "Address": {
        "Country": "US",
        "Region": null,
        "City": "Redmond",
        "State": "WA",
        "AddressLine1": "123 Main Street",
        "AddressLine2": "",
        "PostalCode": "98052",
        "FirstName": "Gena",
        "LastName": "Soto",
        "PhoneNumber": "4255550110"
    },
    "PrimaryContact": {
        "FirstName": "Gena",
        "LastName": "Soto",
        "Email": "gena@lucernepublishing.com",
        "PhoneNumber": "4255550110"
    },
    "CompanyApproverAddress": {
        "Country": "US",
        "Region": null,
        "City": "Redmond",
        "State": "WA",
        "AddressLine1": "123 Main Street",
        "AddressLine2": "",
        "PostalCode": "98052",
        "FirstName": null,
        "LastName": null,
        "PhoneNumber": null
    },
    "CompanyApproverEmail": "gena@lucernepublishing.com",
    "VettingStatus": "authorized",
    "VettingSubStatus": "none",
    "Links": {
        "Self": {
            "Uri": "/profiles/legalbusiness",
            "Method": "GET",
            "Headers": []
        }
    },
    "Attributes": {
        "ObjectType": "LegalBusinessProfile"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="62fc1-128">REST-svar</span><span class="sxs-lookup"><span data-stu-id="62fc1-128">REST response</span></span>

<span data-ttu-id="62fc1-129">Om det lyckas innehåller svarstexten den uppdaterade **LegalBusinessProfile**</span><span class="sxs-lookup"><span data-stu-id="62fc1-129">If successful, the response body contains the updated **LegalBusinessProfile**</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="62fc1-130">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="62fc1-130">Response success and error codes</span></span>

<span data-ttu-id="62fc1-131">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="62fc1-131">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="62fc1-132">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="62fc1-132">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="62fc1-133">En fullständig lista finns i [Felkoder i Partnercenter.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="62fc1-133">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="62fc1-134">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="62fc1-134">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1157
Content-Type: application/json; charset=utf-8
MS-CorrelationId: aa2a0d8c-7a41-470f-97ae-b82e6c338ee4
MS-RequestId: 4549ac0c-0f1d-4d8f-b02f-6d36fadcccee
MS-CV: KZLU42qJ4EObO75q.0
MS-ServerId: 030020643
Date: Tue, 21 Mar 2017 22:03:15 GMT

{
    "companyName": "Lucerne Publishing",
    "address": {
        "country": "US",
        "city": "Redmond",
        "state": "WA",
        "addressLine1": "123 Main Street",
        "addressLine2": "",
        "postalCode": "98052",
        "firstName": "Gena",
        "lastName": "Soto",
        "phoneNumber": "4255550110"
    },
    "primaryContact": {
        "firstName": "Gena",
        "lastName": "Soto",
        "email": "gena@lucernepublishing.com",
        "phoneNumber": "4255550110"
    },
    "companyApproverAddress": {
        "country": "US",
        "city": "Redmond",
        "state": "WA",
        "addressLine1": "123 Main Street",
        "addressLine2": "",
        "postalCode": "98052"
    },
    "companyApproverEmail": "gena@lucernepublishing.com",
    "vettingStatus": "authorized",
    "vettingSubStatus": "none",
    "profileType": "LegalBusinessProfile",
    "links": {
        "self": {
            "uri": "/profiles/legalbusiness",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "LegalBusinessProfile"
    }
}
```
