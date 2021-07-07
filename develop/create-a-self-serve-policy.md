---
title: Skapa en princip för självbetjäning
description: Så här skapar du en ny självbetjäningsprincip.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 14f46e22fbd294c765b745204cf62474250cbfbd
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973697"
---
# <a name="create-a-selfservepolicy"></a><span data-ttu-id="923a9-103">Skapa en SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="923a9-103">Create a SelfServePolicy</span></span>

<span data-ttu-id="923a9-104">Den här artikeln förklarar hur du skapar en ny självbetjäningsprincip.</span><span class="sxs-lookup"><span data-stu-id="923a9-104">This article explains how to create a new self-serve policy.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="923a9-105">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="923a9-105">Prerequisites</span></span>

- <span data-ttu-id="923a9-106">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="923a9-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="923a9-107">Det här scenariot stöder autentisering med autentiseringsuppgifter för program och användare.</span><span class="sxs-lookup"><span data-stu-id="923a9-107">This scenario supports authentication with Application+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="923a9-108">C\#</span><span class="sxs-lookup"><span data-stu-id="923a9-108">C\#</span></span>

<span data-ttu-id="923a9-109">Skapa en princip för självbetjäning:</span><span class="sxs-lookup"><span data-stu-id="923a9-109">Create a self-serve policy:</span></span>

1. <span data-ttu-id="923a9-110">Anropa [**metoden IAggregatePartner.SelfServePolicies.Create**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.create) eller [**IAggregatePartner.SelfServePolicies.CreateAsync**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.createasync) med principinformationen för självbetjäning.</span><span class="sxs-lookup"><span data-stu-id="923a9-110">Call the [**IAggregatePartner.SelfServePolicies.Create**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.create) or [**IAggregatePartner.SelfServePolicies.CreateAsync**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.createasync) method with the self-serve policy info.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
string customerIdAsEntity;

var selfServePolicy = new SelfServePolicy
{
    SelfServeEntity = new SelfServeEntity
    {
        SelfServeEntityType = "customer",
        TenantID = customerIdAsEntity,
    },
    Grantor = new Grantor
    {
        GrantorType = "billToPartner",
        TenantID = partnerIdAsGrantor,
    },
    Permissions = new Permission[]
    {
        new Permission
        {
        Action = "Purchase",
        Resource = "AzureReservedInstances",
        },
    },
};

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// creates the self-serve policy
SelfServePolicy createdSelfServePolicy = scopedPartnerOperations.selfServePolicies.Create(selfServePolicy);
```

<span data-ttu-id="923a9-111">Ett exempel finns i följande:</span><span class="sxs-lookup"><span data-stu-id="923a9-111">For an example, see the following:</span></span>

- <span data-ttu-id="923a9-112">Exempel: [Konsoltestapp](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="923a9-112">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="923a9-113">Project: **PartnerSDK.FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="923a9-113">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="923a9-114">Klass: **CreateSelfServePolicies.cs**</span><span class="sxs-lookup"><span data-stu-id="923a9-114">Class: **CreateSelfServePolicies.cs**</span></span>


## <a name="rest-request"></a><span data-ttu-id="923a9-115">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="923a9-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="923a9-116">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="923a9-116">Request syntax</span></span>

| <span data-ttu-id="923a9-117">Metod</span><span class="sxs-lookup"><span data-stu-id="923a9-117">Method</span></span>   | <span data-ttu-id="923a9-118">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="923a9-118">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="923a9-119">**Inlägg**</span><span class="sxs-lookup"><span data-stu-id="923a9-119">**POST**</span></span> | <span data-ttu-id="923a9-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="923a9-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="923a9-121">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="923a9-121">Request headers</span></span>

- <span data-ttu-id="923a9-122">Ett begärande-ID och korrelations-ID krävs.</span><span class="sxs-lookup"><span data-stu-id="923a9-122">A request ID and correlation ID are required.</span></span>
- <span data-ttu-id="923a9-123">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="923a9-123">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="923a9-124">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="923a9-124">Request body</span></span>

<span data-ttu-id="923a9-125">I den här tabellen beskrivs de obligatoriska egenskaperna i begärandetexten.</span><span class="sxs-lookup"><span data-stu-id="923a9-125">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="923a9-126">Namn</span><span class="sxs-lookup"><span data-stu-id="923a9-126">Name</span></span>                              | <span data-ttu-id="923a9-127">Typ</span><span class="sxs-lookup"><span data-stu-id="923a9-127">Type</span></span>   | <span data-ttu-id="923a9-128">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="923a9-128">Description</span></span>                                 |
|------------------------------------------------------------------|--------|---------------------------------------------|
| [<span data-ttu-id="923a9-129">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="923a9-129">SelfServePolicy</span></span>](self-serve-policy-resources.md#selfservepolicy)| <span data-ttu-id="923a9-130">objekt</span><span class="sxs-lookup"><span data-stu-id="923a9-130">object</span></span> | <span data-ttu-id="923a9-131">Information om självbetjäningsprincipen.</span><span class="sxs-lookup"><span data-stu-id="923a9-131">The self-serve policy information.</span></span> |

#### <a name="selfservepolicy"></a><span data-ttu-id="923a9-132">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="923a9-132">SelfServePolicy</span></span>

<span data-ttu-id="923a9-133">I den här tabellen beskrivs de minsta obligatoriska fälten från [SelfServePolicy-resursen](self-serve-policy-resources.md#selfservepolicy) som behövs för att skapa en ny självbetjäningsprincip.</span><span class="sxs-lookup"><span data-stu-id="923a9-133">This table describes the minimum required fields from the [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource needed to create a new self-serve policy.</span></span>

| <span data-ttu-id="923a9-134">Egenskap</span><span class="sxs-lookup"><span data-stu-id="923a9-134">Property</span></span>              | <span data-ttu-id="923a9-135">Typ</span><span class="sxs-lookup"><span data-stu-id="923a9-135">Type</span></span>             | <span data-ttu-id="923a9-136">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="923a9-136">Description</span></span>                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="923a9-137">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="923a9-137">SelfServeEntity</span></span>       | <span data-ttu-id="923a9-138">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="923a9-138">SelfServeEntity</span></span>  | <span data-ttu-id="923a9-139">Entiteten med självbetjäning som beviljas åtkomst.</span><span class="sxs-lookup"><span data-stu-id="923a9-139">The self-serve entity that is being granted access.</span></span>                                                     |
| <span data-ttu-id="923a9-140">Beviljaren</span><span class="sxs-lookup"><span data-stu-id="923a9-140">Grantor</span></span>               | <span data-ttu-id="923a9-141">Beviljaren</span><span class="sxs-lookup"><span data-stu-id="923a9-141">Grantor</span></span>          | <span data-ttu-id="923a9-142">Den beviljande som beviljar åtkomst.</span><span class="sxs-lookup"><span data-stu-id="923a9-142">The grantor that is granting access.</span></span>                                                                    |
| <span data-ttu-id="923a9-143">Behörigheter</span><span class="sxs-lookup"><span data-stu-id="923a9-143">Permissions</span></span>           | <span data-ttu-id="923a9-144">Matris med behörighet</span><span class="sxs-lookup"><span data-stu-id="923a9-144">Array of Permission</span></span>| <span data-ttu-id="923a9-145">En matris med [behörighetsresurser.](self-serve-policy-resources.md#permission)</span><span class="sxs-lookup"><span data-stu-id="923a9-145">An Array of [Permission](self-serve-policy-resources.md#permission) resources.</span></span>                                                                     |


### <a name="request-example"></a><span data-ttu-id="923a9-146">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="923a9-146">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/SelfServePolicy HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 789
Expect: 100-continue
Connection: Keep-Alive

{
    "selfServeEntity": {
        "selfServeEntityType": "customer",
        "tenantID": "0431a72c-7d8a-4393-b25e-ef63f5efb415"
    },
    "grantor": {
        "grantorType": "billToPartner",
        "tenantID": "634f6379-ad54-449b-9821-564f737158ab"
    },
    "permissions": [{
        "resource": "AzureReservedInstances",
        "action": "Purchase"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="923a9-147">REST-svar</span><span class="sxs-lookup"><span data-stu-id="923a9-147">REST response</span></span>

<span data-ttu-id="923a9-148">Om det lyckas returnerar detta API en [SelfServePolicy-resurs](self-serve-policy-resources.md#selfservepolicy) för den nya självbetjäningsprincipen.</span><span class="sxs-lookup"><span data-stu-id="923a9-148">If successful, this API returns a [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource for the new self-serve policy.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="923a9-149">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="923a9-149">Response success and error codes</span></span>

<span data-ttu-id="923a9-150">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="923a9-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="923a9-151">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="923a9-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="923a9-152">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="923a9-152">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

<span data-ttu-id="923a9-153">Den här metoden returnerar följande felkoder:</span><span class="sxs-lookup"><span data-stu-id="923a9-153">This method returns the following error codes:</span></span>

| <span data-ttu-id="923a9-154">HTTP-statuskod</span><span class="sxs-lookup"><span data-stu-id="923a9-154">HTTP Status Code</span></span>     | <span data-ttu-id="923a9-155">Felkod</span><span class="sxs-lookup"><span data-stu-id="923a9-155">Error code</span></span>   | <span data-ttu-id="923a9-156">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="923a9-156">Description</span></span>                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| <span data-ttu-id="923a9-157">409</span><span class="sxs-lookup"><span data-stu-id="923a9-157">409</span></span>                  | <span data-ttu-id="923a9-158">600041</span><span class="sxs-lookup"><span data-stu-id="923a9-158">600041</span></span>       | <span data-ttu-id="923a9-159">Självbetjäningsprincipen finns redan.</span><span class="sxs-lookup"><span data-stu-id="923a9-159">Self-serve policy already exists.</span></span>                                                     |


### <a name="response-example"></a><span data-ttu-id="923a9-160">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="923a9-160">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 834
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
Date: Tue, 14 Feb 2017 20:06:02 GMT

{
    "id": "634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415",
    "selfServeEntity": {
        "selfServeEntityType": "customer",
        "tenantID": "0431a72c-7d8a-4393-b25e-ef63f5efb415"
    },
    "grantor": {
        "grantorType": "billToPartner",
        "tenantID": "634f6379-ad54-449b-9821-564f737158ab"
    },
    "permissions": [{
        "resource": "AzureReservedInstances",
        "action": "Purchase"
    }],
    "attributes": {
        "etag": "\"933523d1-3f63-4fc3-8789-5e21c02cdaed\"",
        "objectType": "SelfServePolicy"
    }
}
```
