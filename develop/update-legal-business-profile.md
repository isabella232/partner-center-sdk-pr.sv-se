---
title: Uppdatera partnerns juridiska företagsprofil
description: Så här uppdaterar du partnerns juridiska företags profil.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: parthpandyaMSFT
ms.author: parthp
ms.openlocfilehash: 6c61b51ab0680e36daa99c11dc8e8c3506259d29
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769600"
---
# <a name="update-the-partner-legal-business-profile"></a><span data-ttu-id="b2938-103">Uppdatera partnerns juridiska företagsprofil</span><span class="sxs-lookup"><span data-stu-id="b2938-103">Update the partner legal business profile</span></span>

<span data-ttu-id="b2938-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="b2938-104">**Applies To**</span></span>

- <span data-ttu-id="b2938-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="b2938-105">Partner Center</span></span>
- <span data-ttu-id="b2938-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="b2938-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="b2938-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="b2938-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="b2938-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="b2938-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="b2938-109">Så här uppdaterar du partnerns juridiska företags profil.</span><span class="sxs-lookup"><span data-stu-id="b2938-109">How to update the partner legal business profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b2938-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="b2938-110">Prerequisites</span></span>

- <span data-ttu-id="b2938-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b2938-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b2938-112">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="b2938-112">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="b2938-113">C\#</span><span class="sxs-lookup"><span data-stu-id="b2938-113">C\#</span></span>

<span data-ttu-id="b2938-114">Om du vill uppdatera partnerns juridiska företags profil måste du först instansiera ett **LegalBusinessProfile** -objekt och fylla det med den befintliga profilen.</span><span class="sxs-lookup"><span data-stu-id="b2938-114">To update the partner legal business profile, first instantiate a **LegalBusinessProfile** object and populate it with the existing profile.</span></span> <span data-ttu-id="b2938-115">Mer information finns i [Hämta partnerns juridiska företags profil](get-legal-business-profile.md).</span><span class="sxs-lookup"><span data-stu-id="b2938-115">For more information, see [Get the partner legal business profile](get-legal-business-profile.md).</span></span> <span data-ttu-id="b2938-116">Uppdatera sedan de egenskaper som du behöver ändra.</span><span class="sxs-lookup"><span data-stu-id="b2938-116">Then, update the properties that you need to change.</span></span> <span data-ttu-id="b2938-117">Följande kod exempel illustrerar hur du ändrar adress och primära telefonnummer till kontakt.</span><span class="sxs-lookup"><span data-stu-id="b2938-117">The following code example illustrates changing the address and primary contact phone numbers.</span></span>

<span data-ttu-id="b2938-118">Hämta sedan ett gränssnitt till partner profils åtgärds samlingen från egenskapen **IAggregatePartner. profiles** .</span><span class="sxs-lookup"><span data-stu-id="b2938-118">Next, get an interface to the partner profile operations collection from the **IAggregatePartner.Profiles** property.</span></span> <span data-ttu-id="b2938-119">Hämta sedan värdet för egenskapen **LegalBusinessProfile** för att få ett gränssnitt till juridiska affärs profil åtgärder.</span><span class="sxs-lookup"><span data-stu-id="b2938-119">Then, retrieve the value of the **LegalBusinessProfile** property to get an interface to legal business profile operations.</span></span> <span data-ttu-id="b2938-120">Slutligen kan du anropa [**Update**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.update) -eller [**UpdateAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.updateasync) -metoden med det ändrade objektet för att uppdatera profilen.</span><span class="sxs-lookup"><span data-stu-id="b2938-120">Finally, call the [**Update**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.update) or [**UpdateAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.updateasync) method with the changed object to update the profile.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var legalBusinessProfile = partnerOperations.Profiles.LegalBusinessProfile.Get();

// Change the address and primary contact phone number.
legalBusinessProfile.Address.PhoneNumber = "4255550110";
legalBusinessProfile.PrimaryContact.PhoneNumber = "4255550110";

// Apply changes to the profile.
var updatedLegalBusinessProfile = partnerOperations.Profiles.LegalBusinessProfile.Update(legalBusinessProfile);
```

## <a name="rest-request"></a><span data-ttu-id="b2938-121">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="b2938-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b2938-122">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="b2938-122">Request syntax</span></span>

| <span data-ttu-id="b2938-123">Metod</span><span class="sxs-lookup"><span data-stu-id="b2938-123">Method</span></span>  | <span data-ttu-id="b2938-124">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="b2938-124">Request URI</span></span>                                                                    |
|---------|--------------------------------------------------------------------------------|
| <span data-ttu-id="b2938-125">**PUT**</span><span class="sxs-lookup"><span data-stu-id="b2938-125">**PUT**</span></span> | <span data-ttu-id="b2938-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/legalbusiness http/1.1</span><span class="sxs-lookup"><span data-stu-id="b2938-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/legalbusiness HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b2938-127">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="b2938-127">Request headers</span></span>

<span data-ttu-id="b2938-128">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b2938-128">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b2938-129">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="b2938-129">Request body</span></span>

<span data-ttu-id="b2938-130">Resurs för juridisk företags profil.</span><span class="sxs-lookup"><span data-stu-id="b2938-130">The legal business profile resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="b2938-131">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="b2938-131">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="b2938-132">REST-svar</span><span class="sxs-lookup"><span data-stu-id="b2938-132">REST response</span></span>

<span data-ttu-id="b2938-133">Om det lyckas innehåller svars texten den uppdaterade **LegalBusinessProfile**</span><span class="sxs-lookup"><span data-stu-id="b2938-133">If successful, the response body contains the updated **LegalBusinessProfile**</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b2938-134">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="b2938-134">Response success and error codes</span></span>

<span data-ttu-id="b2938-135">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="b2938-135">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b2938-136">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="b2938-136">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b2938-137">En fullständig lista finns i [fel koder för partner Center](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b2938-137">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b2938-138">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="b2938-138">Response example</span></span>

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
