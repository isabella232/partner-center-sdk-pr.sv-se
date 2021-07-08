---
title: Hämta partnerfaktureringsprofil
description: Hämtar ett objekt som representerar partnerns faktureringsprofil.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 225d8ea2d92933838ae47eaf3308276aa1f1684c
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548982"
---
# <a name="get-partner-billing-profile"></a><span data-ttu-id="176f1-103">Hämta partnerfaktureringsprofil</span><span class="sxs-lookup"><span data-stu-id="176f1-103">Get partner billing profile</span></span>

<span data-ttu-id="176f1-104">**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="176f1-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="176f1-105">Hämtar ett objekt som representerar partnerns faktureringsprofil.</span><span class="sxs-lookup"><span data-stu-id="176f1-105">Gets an object representing the partner's billing profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="176f1-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="176f1-106">Prerequisites</span></span>

- <span data-ttu-id="176f1-107">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="176f1-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="176f1-108">Det här scenariot har endast stöd för autentisering med app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="176f1-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="176f1-109">C\#</span><span class="sxs-lookup"><span data-stu-id="176f1-109">C\#</span></span>

<span data-ttu-id="176f1-110">Om du vill hämta en partnerfaktureringsprofil använder **du samlingen IAggregatePartner.Profiles** och **anropar egenskapen BillingProfile.**</span><span class="sxs-lookup"><span data-stu-id="176f1-110">To get a partner billing profile, use your **IAggregatePartner.Profiles** collection and call the **BillingProfile** property.</span></span> <span data-ttu-id="176f1-111">Anropa slutligen metoderna [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.get) eller [**GetAsync().**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.getasync)</span><span class="sxs-lookup"><span data-stu-id="176f1-111">Finally, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

BillingProfile billingProfile = partnerOperations.Profiles.BillingProfile.Get();
```

<span data-ttu-id="176f1-112">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="176f1-112">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="176f1-113">**Project:** PartnerCenterSDK.FeaturesSamples-klass: GetBillingProfile.cs </span><span class="sxs-lookup"><span data-stu-id="176f1-113">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: GetBillingProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="176f1-114">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="176f1-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="176f1-115">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="176f1-115">Request syntax</span></span>

| <span data-ttu-id="176f1-116">Metod</span><span class="sxs-lookup"><span data-stu-id="176f1-116">Method</span></span>  | <span data-ttu-id="176f1-117">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="176f1-117">Request URI</span></span>                                                              |
|---------|--------------------------------------------------------------------------|
| <span data-ttu-id="176f1-118">**Få**</span><span class="sxs-lookup"><span data-stu-id="176f1-118">**GET**</span></span> | <span data-ttu-id="176f1-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/billing HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="176f1-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/billing HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="176f1-120">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="176f1-120">Request headers</span></span>

<span data-ttu-id="176f1-121">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="176f1-121">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="176f1-122">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="176f1-122">Request body</span></span>

<span data-ttu-id="176f1-123">Inga.</span><span class="sxs-lookup"><span data-stu-id="176f1-123">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="176f1-124">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="176f1-124">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/billing HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a0dd6cde-b24c-413c-af24-416446dc5599
MS-CorrelationId: 1bb03149-88d2-4bc2-9cc1-d6e83890fa9e
```

## <a name="rest-response"></a><span data-ttu-id="176f1-125">REST-svar</span><span class="sxs-lookup"><span data-stu-id="176f1-125">REST response</span></span>

<span data-ttu-id="176f1-126">Om det lyckas returnerar den här metoden **ett BillingProfile-objekt** i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="176f1-126">If successful, this method returns a **BillingProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="176f1-127">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="176f1-127">Response success and error codes</span></span>

<span data-ttu-id="176f1-128">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="176f1-128">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="176f1-129">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="176f1-129">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="176f1-130">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="176f1-130">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="176f1-131">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="176f1-131">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 568
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 1bb03149-88d2-4bc2-9cc1-d6e83890fa9e
MS-RequestId: a0dd6cde-b24c-413c-af24-416446dc5599
Date: Tue, 22 Mar 2016 17:10:02 GMT

{
    "companyName":"TEST_TEST_BugBash1",
    "address":{
        "country":"US",
        "city":"Redmond",
        "state":"WA",
        "addressLine1":"1 Microsoft Way",
        "addressLine2":"","postalCode":"98052"
    },
    "primaryContact":{
        "firstName":"James",
        "lastName":"Burk",
        "phoneNumber":"2066017143"
    },
    "purchaseOrderNumber":"9888",
    "taxId":"12-345678",
    "billingCurrency":"USD",
    "profileType":"BillingProfile",
    "links":{
        "self":{
            "uri":"/profiles/billing",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "etag":<etag>,
        "objectType":"BillingProfile"
    }
}
```
