---
title: Hämta partnerfaktureringsprofil
description: Hämtar ett objekt som representerar partnerns fakturerings profil.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 94c5ff8fc351282ca3b4721511f02ba6a0cc403c
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769840"
---
# <a name="get-partner-billing-profile"></a><span data-ttu-id="dfc2a-103">Hämta partnerfaktureringsprofil</span><span class="sxs-lookup"><span data-stu-id="dfc2a-103">Get partner billing profile</span></span>

<span data-ttu-id="dfc2a-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="dfc2a-104">**Applies To**</span></span>

- <span data-ttu-id="dfc2a-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="dfc2a-105">Partner Center</span></span>
- <span data-ttu-id="dfc2a-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="dfc2a-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="dfc2a-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="dfc2a-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="dfc2a-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="dfc2a-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="dfc2a-109">Hämtar ett objekt som representerar partnerns fakturerings profil.</span><span class="sxs-lookup"><span data-stu-id="dfc2a-109">Gets an object representing the partner's billing profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dfc2a-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="dfc2a-110">Prerequisites</span></span>

- <span data-ttu-id="dfc2a-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="dfc2a-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="dfc2a-112">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="dfc2a-112">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="dfc2a-113">C\#</span><span class="sxs-lookup"><span data-stu-id="dfc2a-113">C\#</span></span>

<span data-ttu-id="dfc2a-114">Använd din **IAggregatePartner. profiles** -samling och anropa **BillingProfile** -egenskapen för att få en partner fakturerings profil.</span><span class="sxs-lookup"><span data-stu-id="dfc2a-114">To get a partner billing profile, use your **IAggregatePartner.Profiles** collection and call the **BillingProfile** property.</span></span> <span data-ttu-id="dfc2a-115">Anropa slutligen metoderna [**Get ()**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.get) eller [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.getasync) .</span><span class="sxs-lookup"><span data-stu-id="dfc2a-115">Finally, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

BillingProfile billingProfile = partnerOperations.Profiles.BillingProfile.Get();
```

<span data-ttu-id="dfc2a-116">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="dfc2a-116">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="dfc2a-117">**Projekt**: PartnerCenterSDK. FeaturesSamples- **klass**: GetBillingProfile.CS</span><span class="sxs-lookup"><span data-stu-id="dfc2a-117">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: GetBillingProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="dfc2a-118">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="dfc2a-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="dfc2a-119">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="dfc2a-119">Request syntax</span></span>

| <span data-ttu-id="dfc2a-120">Metod</span><span class="sxs-lookup"><span data-stu-id="dfc2a-120">Method</span></span>  | <span data-ttu-id="dfc2a-121">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="dfc2a-121">Request URI</span></span>                                                              |
|---------|--------------------------------------------------------------------------|
| <span data-ttu-id="dfc2a-122">**TA**</span><span class="sxs-lookup"><span data-stu-id="dfc2a-122">**GET**</span></span> | <span data-ttu-id="dfc2a-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/Billing http/1.1</span><span class="sxs-lookup"><span data-stu-id="dfc2a-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/billing HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="dfc2a-124">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="dfc2a-124">Request headers</span></span>

<span data-ttu-id="dfc2a-125">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="dfc2a-125">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="dfc2a-126">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="dfc2a-126">Request body</span></span>

<span data-ttu-id="dfc2a-127">Inga.</span><span class="sxs-lookup"><span data-stu-id="dfc2a-127">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="dfc2a-128">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="dfc2a-128">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/billing HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a0dd6cde-b24c-413c-af24-416446dc5599
MS-CorrelationId: 1bb03149-88d2-4bc2-9cc1-d6e83890fa9e
```

## <a name="rest-response"></a><span data-ttu-id="dfc2a-129">REST-svar</span><span class="sxs-lookup"><span data-stu-id="dfc2a-129">REST response</span></span>

<span data-ttu-id="dfc2a-130">Om det lyckas returnerar den här metoden ett **BillingProfile** -objekt i svars texten.</span><span class="sxs-lookup"><span data-stu-id="dfc2a-130">If successful, this method returns a **BillingProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="dfc2a-131">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="dfc2a-131">Response success and error codes</span></span>

<span data-ttu-id="dfc2a-132">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="dfc2a-132">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="dfc2a-133">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="dfc2a-133">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="dfc2a-134">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="dfc2a-134">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="dfc2a-135">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="dfc2a-135">Response example</span></span>

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
