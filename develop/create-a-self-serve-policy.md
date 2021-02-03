---
title: Skapa en princip för självbetjäning
description: Så här skapar du en ny princip för självbetjäning.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: fd1579b2775ead57a440db0d6afb3bf22164c319
ms.sourcegitcommit: 01e75175077611da92175c777a440a594fb05797
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/08/2020
ms.locfileid: "97770217"
---
# <a name="create-a-selfservepolicy"></a><span data-ttu-id="3cde7-103">Skapa en SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="3cde7-103">Create a SelfServePolicy</span></span>

<span data-ttu-id="3cde7-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="3cde7-104">**Applies to:**</span></span>

- <span data-ttu-id="3cde7-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="3cde7-105">Partner Center</span></span>

<span data-ttu-id="3cde7-106">I det här avsnittet beskrivs hur du skapar en ny princip för självbetjäning.</span><span class="sxs-lookup"><span data-stu-id="3cde7-106">This topic explains how to create a new self-serve policy.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3cde7-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="3cde7-107">Prerequisites</span></span>

- <span data-ttu-id="3cde7-108">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="3cde7-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3cde7-109">Det här scenariot stöder autentisering med program-och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="3cde7-109">This scenario supports authentication with Application+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="3cde7-110">C\#</span><span class="sxs-lookup"><span data-stu-id="3cde7-110">C\#</span></span>

<span data-ttu-id="3cde7-111">Skapa en princip för självbetjäning:</span><span class="sxs-lookup"><span data-stu-id="3cde7-111">Create a self-serve policy:</span></span>

1. <span data-ttu-id="3cde7-112">Anropa metoden [**IAggregatePartner. SelfServePolicies. Create**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.create) eller [**IAggregatePartner. SelfServePolicies. CreateAsync**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.createasync) med den självbetjänings princip informationen.</span><span class="sxs-lookup"><span data-stu-id="3cde7-112">Call the [**IAggregatePartner.SelfServePolicies.Create**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.create) or [**IAggregatePartner.SelfServePolicies.CreateAsync**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.createasync) method with the self-serve policy info.</span></span>

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

<span data-ttu-id="3cde7-113">Ett exempel finns i följande avsnitt:</span><span class="sxs-lookup"><span data-stu-id="3cde7-113">For an example, see the following:</span></span>

- <span data-ttu-id="3cde7-114">Exempel: [konsol test app](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="3cde7-114">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="3cde7-115">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="3cde7-115">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="3cde7-116">Klass: **CreateSelfServePolicies.cs**</span><span class="sxs-lookup"><span data-stu-id="3cde7-116">Class: **CreateSelfServePolicies.cs**</span></span>


## <a name="rest-request"></a><span data-ttu-id="3cde7-117">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="3cde7-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3cde7-118">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="3cde7-118">Request syntax</span></span>

| <span data-ttu-id="3cde7-119">Metod</span><span class="sxs-lookup"><span data-stu-id="3cde7-119">Method</span></span>   | <span data-ttu-id="3cde7-120">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="3cde7-120">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="3cde7-121">**EFTER**</span><span class="sxs-lookup"><span data-stu-id="3cde7-121">**POST**</span></span> | <span data-ttu-id="3cde7-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy http/1.1</span><span class="sxs-lookup"><span data-stu-id="3cde7-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="3cde7-123">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="3cde7-123">Request headers</span></span>

- <span data-ttu-id="3cde7-124">ID för begäran och korrelations-ID krävs.</span><span class="sxs-lookup"><span data-stu-id="3cde7-124">A request ID and correlation ID are required.</span></span>
- <span data-ttu-id="3cde7-125">Mer information finns i [partner Center rest-rubriker](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="3cde7-125">See [Partner Center REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="3cde7-126">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="3cde7-126">Request body</span></span>

<span data-ttu-id="3cde7-127">I den här tabellen beskrivs de egenskaper som krävs i begär ande texten.</span><span class="sxs-lookup"><span data-stu-id="3cde7-127">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="3cde7-128">Namn</span><span class="sxs-lookup"><span data-stu-id="3cde7-128">Name</span></span>                              | <span data-ttu-id="3cde7-129">Typ</span><span class="sxs-lookup"><span data-stu-id="3cde7-129">Type</span></span>   | <span data-ttu-id="3cde7-130">Description</span><span class="sxs-lookup"><span data-stu-id="3cde7-130">Description</span></span>                                 |
|------------------------------------------------------------------|--------|---------------------------------------------|
| [<span data-ttu-id="3cde7-131">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="3cde7-131">SelfServePolicy</span></span>](self-serve-policy-resources.md#selfservepolicy)| <span data-ttu-id="3cde7-132">objekt</span><span class="sxs-lookup"><span data-stu-id="3cde7-132">object</span></span> | <span data-ttu-id="3cde7-133">Den självbetjänings princip informationen.</span><span class="sxs-lookup"><span data-stu-id="3cde7-133">The self-serve policy information.</span></span> |

#### <a name="selfservepolicy"></a><span data-ttu-id="3cde7-134">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="3cde7-134">SelfServePolicy</span></span>

<span data-ttu-id="3cde7-135">I den här tabellen beskrivs de minimi krav som krävs från den [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) -resurs som krävs för att skapa en ny princip för självbetjäning.</span><span class="sxs-lookup"><span data-stu-id="3cde7-135">This table describes the minimum required fields from the [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource needed to create a new self-serve policy.</span></span>

| <span data-ttu-id="3cde7-136">Egenskap</span><span class="sxs-lookup"><span data-stu-id="3cde7-136">Property</span></span>              | <span data-ttu-id="3cde7-137">Typ</span><span class="sxs-lookup"><span data-stu-id="3cde7-137">Type</span></span>             | <span data-ttu-id="3cde7-138">Description</span><span class="sxs-lookup"><span data-stu-id="3cde7-138">Description</span></span>                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3cde7-139">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="3cde7-139">SelfServeEntity</span></span>       | <span data-ttu-id="3cde7-140">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="3cde7-140">SelfServeEntity</span></span>  | <span data-ttu-id="3cde7-141">Den självbetjänings enhet som beviljas åtkomst.</span><span class="sxs-lookup"><span data-stu-id="3cde7-141">The self-serve entity that is being granted access.</span></span>                                                     |
| <span data-ttu-id="3cde7-142">Den beviljande användaren</span><span class="sxs-lookup"><span data-stu-id="3cde7-142">Grantor</span></span>               | <span data-ttu-id="3cde7-143">Den beviljande användaren</span><span class="sxs-lookup"><span data-stu-id="3cde7-143">Grantor</span></span>          | <span data-ttu-id="3cde7-144">Den beviljande behörighet som beviljar åtkomst.</span><span class="sxs-lookup"><span data-stu-id="3cde7-144">The grantor that is granting access.</span></span>                                                                    |
| <span data-ttu-id="3cde7-145">Behörigheter</span><span class="sxs-lookup"><span data-stu-id="3cde7-145">Permissions</span></span>           | <span data-ttu-id="3cde7-146">Behörighets mat ris</span><span class="sxs-lookup"><span data-stu-id="3cde7-146">Array of Permission</span></span>| <span data-ttu-id="3cde7-147">En matris med [behörighets](self-serve-policy-resources.md#permission) resurser.</span><span class="sxs-lookup"><span data-stu-id="3cde7-147">An Array of [Permission](self-serve-policy-resources.md#permission) resources.</span></span>                                                                     |


### <a name="request-example"></a><span data-ttu-id="3cde7-148">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="3cde7-148">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="3cde7-149">REST-svar</span><span class="sxs-lookup"><span data-stu-id="3cde7-149">REST response</span></span>

<span data-ttu-id="3cde7-150">Om detta lyckas returnerar detta API en [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) -resurs för den nya självbetjänings principen.</span><span class="sxs-lookup"><span data-stu-id="3cde7-150">If successful, this API returns a [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource for the new self-serve policy.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3cde7-151">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="3cde7-151">Response success and error codes</span></span>

<span data-ttu-id="3cde7-152">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="3cde7-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3cde7-153">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="3cde7-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3cde7-154">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="3cde7-154">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

<span data-ttu-id="3cde7-155">Den här metoden returnerar följande fel koder:</span><span class="sxs-lookup"><span data-stu-id="3cde7-155">This method returns the following error codes:</span></span>

| <span data-ttu-id="3cde7-156">HTTP-statuskod</span><span class="sxs-lookup"><span data-stu-id="3cde7-156">HTTP Status Code</span></span>     | <span data-ttu-id="3cde7-157">Felkod</span><span class="sxs-lookup"><span data-stu-id="3cde7-157">Error code</span></span>   | <span data-ttu-id="3cde7-158">Description</span><span class="sxs-lookup"><span data-stu-id="3cde7-158">Description</span></span>                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| <span data-ttu-id="3cde7-159">409</span><span class="sxs-lookup"><span data-stu-id="3cde7-159">409</span></span>                  | <span data-ttu-id="3cde7-160">600041</span><span class="sxs-lookup"><span data-stu-id="3cde7-160">600041</span></span>       | <span data-ttu-id="3cde7-161">Principen för självbetjäning finns redan.</span><span class="sxs-lookup"><span data-stu-id="3cde7-161">Self-serve policy already exists.</span></span>                                                     |


### <a name="response-example"></a><span data-ttu-id="3cde7-162">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="3cde7-162">Response example</span></span>

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
