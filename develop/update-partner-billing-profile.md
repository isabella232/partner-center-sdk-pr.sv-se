---
title: Uppdatera partnerfaktureringsprofilen
description: Uppdaterar en partners faktureringsprofil.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: parthpandyaMSFT
ms.author: parthp
ms.openlocfilehash: 2b09a0045df15d774c892a59fba8502d4d4f7024
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/05/2021
ms.locfileid: "111529774"
---
# <a name="update-the-partner-billing-profile"></a><span data-ttu-id="ba505-103">Uppdatera partnerfaktureringsprofilen</span><span class="sxs-lookup"><span data-stu-id="ba505-103">Update the partner billing profile</span></span>

<span data-ttu-id="ba505-104">**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="ba505-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="ba505-105">Uppdaterar en partners faktureringsprofil</span><span class="sxs-lookup"><span data-stu-id="ba505-105">Updates a partner's billing profile</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba505-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="ba505-106">Prerequisites</span></span>

- <span data-ttu-id="ba505-107">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="ba505-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ba505-108">Det här scenariot stöder endast autentisering med app+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="ba505-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="ba505-109">C\#</span><span class="sxs-lookup"><span data-stu-id="ba505-109">C\#</span></span>

<span data-ttu-id="ba505-110">Om du vill uppdatera en partnerfaktureringsprofil hämtar du den befintliga profilen.</span><span class="sxs-lookup"><span data-stu-id="ba505-110">To update a partner billing profile, retrieve the existing profile.</span></span> <span data-ttu-id="ba505-111">När du har uppdaterat profilen använder du samlingen **IAggregatePartner.Profiles** och anropar **egenskapen BillingProfile.**</span><span class="sxs-lookup"><span data-stu-id="ba505-111">Once you have updated the profile, use your **IAggregatePartner.Profiles** collection and call the **BillingProfile** property.</span></span> <span data-ttu-id="ba505-112">Anropa slutligen metoden **Update().**</span><span class="sxs-lookup"><span data-stu-id="ba505-112">Finally, call the **Update()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

BillingProfile existingBillingProfile = partnerOperations.Profiles.BillingProfile.Get();

// update the profile with a purchase order number
existingBillingProfile.PurchaseOrderNumber = new Random().Next(9000, 10000).ToString(CultureInfo.InvariantCulture);

BillingProfile updatedPartnerBillingProfile = partnerOperations.Profiles.BillingProfile.Update(existingBillingProfile);
```

<span data-ttu-id="ba505-113">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="ba505-113">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="ba505-114">**Project:** Partnercenter-SDK **exempelklass:** UpdateBillingProfile.cs</span><span class="sxs-lookup"><span data-stu-id="ba505-114">**Project**: Partner Center SDK Samples **Class**: UpdateBillingProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="ba505-115">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="ba505-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ba505-116">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="ba505-116">Request syntax</span></span>

| <span data-ttu-id="ba505-117">Metod</span><span class="sxs-lookup"><span data-stu-id="ba505-117">Method</span></span>  | <span data-ttu-id="ba505-118">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="ba505-118">Request URI</span></span>                                                              |
|---------|--------------------------------------------------------------------------|
| <span data-ttu-id="ba505-119">**PUT**</span><span class="sxs-lookup"><span data-stu-id="ba505-119">**PUT**</span></span> | <span data-ttu-id="ba505-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/billing HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="ba505-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/billing HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="ba505-121">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="ba505-121">Request headers</span></span>

<span data-ttu-id="ba505-122">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="ba505-122">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ba505-123">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="ba505-123">Request body</span></span>

<span data-ttu-id="ba505-124">Inga.</span><span class="sxs-lookup"><span data-stu-id="ba505-124">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="ba505-125">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="ba505-125">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/profiles/billing HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 9231559e-ed95-41e4-810b-e754ae32dc2f
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
Content-Length: 613
Expect: 100-continue

{
    "CompanyName":"TEST_TEST_BugBash1",
    "Address":{
        "Country":"US",
        "Region":null,
        "City":"Redmond",
        "State":"WA",
        "AddressLine1":"1 Microsoft Way",
        "AddressLine2":"","PostalCode":"98052",
        "FirstName":null,
        "LastName":null,
        "PhoneNumber":null
    },
    "PrimaryContact":{
        "FirstName":"Test",
        "LastName":"Customer",
        "Email":null,
        "PhoneNumber":""
    },
    "PurchaseOrderNumber":"9888",
    "TaxId":<TaxId>,
    "BillingCurrency":"USD",
    "Links":{
        "Self":{
            "Uri":"/profiles/billing",
            "Method":"GET","Headers":[]
        }
    },
    "Attributes":{
        "Etag":<etag>,
        "ObjectType":"BillingProfile"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="ba505-126">REST-svar</span><span class="sxs-lookup"><span data-stu-id="ba505-126">REST response</span></span>

<span data-ttu-id="ba505-127">Om det lyckas returnerar den här metoden **ett BillingProfile-objekt** i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="ba505-127">If successful, this method returns a **BillingProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ba505-128">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="ba505-128">Response success and error codes</span></span>

<span data-ttu-id="ba505-129">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="ba505-129">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ba505-130">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="ba505-130">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ba505-131">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="ba505-131">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ba505-132">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="ba505-132">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 568
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
MS-RequestId: 9231559e-ed95-41e4-810b-e754ae32dc2f
Date: Mon, 21 Mar 2016 05:47:16 GMT

{
    "CompanyName":"TEST_TEST_BugBash1",
    "Address":{
        "Country":"US",
        "Region":null,
        "City":"Redmond",
        "State":"WA",
        "AddressLine1":"1 Microsoft Way",
        "AddressLine2":"","PostalCode":"98052",
        "FirstName":null,
        "LastName":null,
        "PhoneNumber":null
    },
    "PrimaryContact":{
        "FirstName":"Test",
        "LastName":"Customer",
        "Email":null,
        "PhoneNumber":""
    },
    "PurchaseOrderNumber":"9888",
    "TaxId":<TaxId>,
    "BillingCurrency":"USD",
    "Links":{
        "Self":{
            "Uri":"/profiles/billing",
            "Method":"GET","Headers":[]
        }
    },
    "Attributes":{
        "Etag":<etag>,
        "ObjectType":"BillingProfile"
    }
}
```
