---
title: Uppdatera partnerfaktureringsprofilen
description: Uppdaterar en partners fakturerings profil.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: parthpandyaMSFT
ms.author: parthp
ms.openlocfilehash: 34e7d2396d6dbdd45a6cf87a3bda481f51326f1e
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769192"
---
# <a name="update-the-partner-billing-profile"></a><span data-ttu-id="c0e14-103">Uppdatera partnerfaktureringsprofilen</span><span class="sxs-lookup"><span data-stu-id="c0e14-103">Update the partner billing profile</span></span>

<span data-ttu-id="c0e14-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="c0e14-104">**Applies To**</span></span>

- <span data-ttu-id="c0e14-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="c0e14-105">Partner Center</span></span>
- <span data-ttu-id="c0e14-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="c0e14-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="c0e14-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="c0e14-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="c0e14-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="c0e14-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="c0e14-109">Uppdaterar en partners fakturerings profil</span><span class="sxs-lookup"><span data-stu-id="c0e14-109">Updates a partner's billing profile</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c0e14-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="c0e14-110">Prerequisites</span></span>

- <span data-ttu-id="c0e14-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="c0e14-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c0e14-112">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="c0e14-112">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="c0e14-113">C\#</span><span class="sxs-lookup"><span data-stu-id="c0e14-113">C\#</span></span>

<span data-ttu-id="c0e14-114">Hämta den befintliga profilen om du vill uppdatera en partner fakturerings profil.</span><span class="sxs-lookup"><span data-stu-id="c0e14-114">To update a partner billing profile, retrieve the existing profile.</span></span> <span data-ttu-id="c0e14-115">När du har uppdaterat profilen använder du din **IAggregatePartner. profiles** -samling och anropar egenskapen **BillingProfile** .</span><span class="sxs-lookup"><span data-stu-id="c0e14-115">Once you have updated the profile, use your **IAggregatePartner.Profiles** collection and call the **BillingProfile** property.</span></span> <span data-ttu-id="c0e14-116">Anropa slutligen metoden **Update ()** .</span><span class="sxs-lookup"><span data-stu-id="c0e14-116">Finally, call the **Update()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

BillingProfile existingBillingProfile = partnerOperations.Profiles.BillingProfile.Get();

// update the profile with a purchase order number
existingBillingProfile.PurchaseOrderNumber = new Random().Next(9000, 10000).ToString(CultureInfo.InvariantCulture);

BillingProfile updatedPartnerBillingProfile = partnerOperations.Profiles.BillingProfile.Update(existingBillingProfile);
```

<span data-ttu-id="c0e14-117">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="c0e14-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="c0e14-118">**Projekt**: Partner Center SDK-exempel **klass**: UpdateBillingProfile.CS</span><span class="sxs-lookup"><span data-stu-id="c0e14-118">**Project**: Partner Center SDK Samples **Class**: UpdateBillingProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="c0e14-119">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="c0e14-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c0e14-120">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="c0e14-120">Request syntax</span></span>

| <span data-ttu-id="c0e14-121">Metod</span><span class="sxs-lookup"><span data-stu-id="c0e14-121">Method</span></span>  | <span data-ttu-id="c0e14-122">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="c0e14-122">Request URI</span></span>                                                              |
|---------|--------------------------------------------------------------------------|
| <span data-ttu-id="c0e14-123">**PUT**</span><span class="sxs-lookup"><span data-stu-id="c0e14-123">**PUT**</span></span> | <span data-ttu-id="c0e14-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/Billing http/1.1</span><span class="sxs-lookup"><span data-stu-id="c0e14-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/billing HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="c0e14-125">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="c0e14-125">Request headers</span></span>

<span data-ttu-id="c0e14-126">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="c0e14-126">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="c0e14-127">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="c0e14-127">Request body</span></span>

<span data-ttu-id="c0e14-128">Inga.</span><span class="sxs-lookup"><span data-stu-id="c0e14-128">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="c0e14-129">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="c0e14-129">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="c0e14-130">REST-svar</span><span class="sxs-lookup"><span data-stu-id="c0e14-130">REST response</span></span>

<span data-ttu-id="c0e14-131">Om det lyckas returnerar den här metoden ett **BillingProfile** -objekt i svars texten.</span><span class="sxs-lookup"><span data-stu-id="c0e14-131">If successful, this method returns a **BillingProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c0e14-132">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="c0e14-132">Response success and error codes</span></span>

<span data-ttu-id="c0e14-133">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="c0e14-133">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c0e14-134">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="c0e14-134">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c0e14-135">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="c0e14-135">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="c0e14-136">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="c0e14-136">Response example</span></span>

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
