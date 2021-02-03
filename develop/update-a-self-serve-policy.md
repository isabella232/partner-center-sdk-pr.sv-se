---
title: Uppdatera en princip för självbetjäning
description: Så här uppdaterar du en självbetjänings princip.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4d53ab8e5b8ef5b7be83360a3f43ec7791b2e3b4
ms.sourcegitcommit: 01e75175077611da92175c777a440a594fb05797
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/08/2020
ms.locfileid: "97770249"
---
# <a name="update-a-selfservepolicy"></a><span data-ttu-id="5354a-103">Uppdatera en SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="5354a-103">Update a SelfServePolicy</span></span>

<span data-ttu-id="5354a-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="5354a-104">**Applies to:**</span></span>

- <span data-ttu-id="5354a-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="5354a-105">Partner Center</span></span>

<span data-ttu-id="5354a-106">I det här avsnittet beskrivs hur du uppdaterar en princip för självbetjäning.</span><span class="sxs-lookup"><span data-stu-id="5354a-106">This topic explains how to update a self-serve policy.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5354a-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="5354a-107">Prerequisites</span></span>

- <span data-ttu-id="5354a-108">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="5354a-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5354a-109">Det här scenariot stöder autentisering med program-och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="5354a-109">This scenario supports authentication with Application+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="5354a-110">C\#</span><span class="sxs-lookup"><span data-stu-id="5354a-110">C\#</span></span>

<span data-ttu-id="5354a-111">Så här tar du bort en princip för självbetjäning:</span><span class="sxs-lookup"><span data-stu-id="5354a-111">To delete a self-serve policy:</span></span>

1. <span data-ttu-id="5354a-112">Anropa metoden [**IAggregatePartner. SelfServePolicies. ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) med enhets-ID: n för att hämta ett gränssnitt till åtgärder i principerna.</span><span class="sxs-lookup"><span data-stu-id="5354a-112">Call the [**IAggregatePartner.SelfServePolicies.ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) method with the entity identifier to retrieve an interface to operations on the policies.</span></span>

2. <span data-ttu-id="5354a-113">Anropa metoden för att [**Skicka**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.put) eller [**PutAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.putasync) för att uppdatera principen för självbetjäning.</span><span class="sxs-lookup"><span data-stu-id="5354a-113">Call the [**Put**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.put) or [**PutAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.putasync) method to update the self-serve policy.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
SelfServePolicy policy;

// All the operations executed on this partner operation instance will share the same correlation identifier but will differ in request identifier
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// updates the self-serve policies
partnerOperations.SelfServePolicies.ById(policy.id).Put(policy);
```

## <a name="rest-request"></a><span data-ttu-id="5354a-114">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="5354a-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5354a-115">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="5354a-115">Request syntax</span></span>

| <span data-ttu-id="5354a-116">Metod</span><span class="sxs-lookup"><span data-stu-id="5354a-116">Method</span></span>   | <span data-ttu-id="5354a-117">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="5354a-117">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="5354a-118">**PUT**</span><span class="sxs-lookup"><span data-stu-id="5354a-118">**PUT**</span></span> | <span data-ttu-id="5354a-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy http/1.1</span><span class="sxs-lookup"><span data-stu-id="5354a-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="5354a-120">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="5354a-120">Request headers</span></span>

- <span data-ttu-id="5354a-121">ID för begäran och korrelation krävs.</span><span class="sxs-lookup"><span data-stu-id="5354a-121">A request identifier and correlation identifier are required.</span></span>
- <span data-ttu-id="5354a-122">Mer information finns i [partner Center rest-rubriker](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="5354a-122">See [Partner Center REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="5354a-123">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="5354a-123">Request body</span></span>

<span data-ttu-id="5354a-124">I den här tabellen beskrivs de egenskaper som krävs i begär ande texten.</span><span class="sxs-lookup"><span data-stu-id="5354a-124">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="5354a-125">Namn</span><span class="sxs-lookup"><span data-stu-id="5354a-125">Name</span></span>                              | <span data-ttu-id="5354a-126">Typ</span><span class="sxs-lookup"><span data-stu-id="5354a-126">Type</span></span>   | <span data-ttu-id="5354a-127">Description</span><span class="sxs-lookup"><span data-stu-id="5354a-127">Description</span></span>                                 |
|------------------------------------------------------------------|--------|---------------------------------------------|
| [<span data-ttu-id="5354a-128">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="5354a-128">SelfServePolicy</span></span>](self-serve-policy-resources.md#selfservepolicy)| <span data-ttu-id="5354a-129">objekt</span><span class="sxs-lookup"><span data-stu-id="5354a-129">object</span></span> | <span data-ttu-id="5354a-130">Den självbetjänings princip informationen.</span><span class="sxs-lookup"><span data-stu-id="5354a-130">The self-serve policy information.</span></span> |

#### <a name="selfservepolicy"></a><span data-ttu-id="5354a-131">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="5354a-131">SelfServePolicy</span></span>

<span data-ttu-id="5354a-132">I den här tabellen beskrivs de minimi krav som krävs från den [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) -resurs som krävs för att skapa en ny princip för självbetjäning.</span><span class="sxs-lookup"><span data-stu-id="5354a-132">This table describes the minimum required fields from the [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource needed to create a new self-serve policy.</span></span>

| <span data-ttu-id="5354a-133">Egenskap</span><span class="sxs-lookup"><span data-stu-id="5354a-133">Property</span></span>              | <span data-ttu-id="5354a-134">Typ</span><span class="sxs-lookup"><span data-stu-id="5354a-134">Type</span></span>             | <span data-ttu-id="5354a-135">Description</span><span class="sxs-lookup"><span data-stu-id="5354a-135">Description</span></span>                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5354a-136">id</span><span class="sxs-lookup"><span data-stu-id="5354a-136">id</span></span>                    | <span data-ttu-id="5354a-137">sträng</span><span class="sxs-lookup"><span data-stu-id="5354a-137">string</span></span>           | <span data-ttu-id="5354a-138">Ett självbetjänings princip-ID som anges när du skapar en egen princip.</span><span class="sxs-lookup"><span data-stu-id="5354a-138">A self-serve policy identifier that is supplied upon successful creation of the self-serve policy.</span></span>     |
| <span data-ttu-id="5354a-139">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="5354a-139">SelfServeEntity</span></span>       | <span data-ttu-id="5354a-140">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="5354a-140">SelfServeEntity</span></span>  | <span data-ttu-id="5354a-141">Den självbetjänings enhet som beviljas åtkomst.</span><span class="sxs-lookup"><span data-stu-id="5354a-141">The self-serve entity that is being granted access.</span></span>                                                     |
| <span data-ttu-id="5354a-142">Den beviljande användaren</span><span class="sxs-lookup"><span data-stu-id="5354a-142">Grantor</span></span>               | <span data-ttu-id="5354a-143">Den beviljande användaren</span><span class="sxs-lookup"><span data-stu-id="5354a-143">Grantor</span></span>          | <span data-ttu-id="5354a-144">Den beviljande behörighet som beviljar åtkomst.</span><span class="sxs-lookup"><span data-stu-id="5354a-144">The grantor that is granting access.</span></span>                                                                    |
| <span data-ttu-id="5354a-145">Behörigheter</span><span class="sxs-lookup"><span data-stu-id="5354a-145">Permissions</span></span>           | <span data-ttu-id="5354a-146">Behörighets mat ris</span><span class="sxs-lookup"><span data-stu-id="5354a-146">Array of Permission</span></span>| <span data-ttu-id="5354a-147">En matris med [behörighets](self-serve-policy-resources.md#permission) resurser.</span><span class="sxs-lookup"><span data-stu-id="5354a-147">An Array of [Permission](self-serve-policy-resources.md#permission) resources.</span></span>                                                      |
| <span data-ttu-id="5354a-148">Etag</span><span class="sxs-lookup"><span data-stu-id="5354a-148">Etag</span></span>                  | <span data-ttu-id="5354a-149">sträng</span><span class="sxs-lookup"><span data-stu-id="5354a-149">string</span></span>           | <span data-ttu-id="5354a-150">Etag.</span><span class="sxs-lookup"><span data-stu-id="5354a-150">The Etag.</span></span>                                                                                               |


### <a name="request-example"></a><span data-ttu-id="5354a-151">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="5354a-151">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/SelfServePolicy HTTP/1.1
Authorization: Bearer <token>
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive

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

## <a name="rest-response"></a><span data-ttu-id="5354a-152">REST-svar</span><span class="sxs-lookup"><span data-stu-id="5354a-152">REST response</span></span>

<span data-ttu-id="5354a-153">Om det lyckas, returnerar detta API en [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) -resurs för den uppdaterade självbetjänings principen.</span><span class="sxs-lookup"><span data-stu-id="5354a-153">If successful, this API returns a [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource for the updated self-serve policy.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5354a-154">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="5354a-154">Response success and error codes</span></span>

<span data-ttu-id="5354a-155">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="5354a-155">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5354a-156">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="5354a-156">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5354a-157">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="5354a-157">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

<span data-ttu-id="5354a-158">Den här metoden returnerar följande fel koder:</span><span class="sxs-lookup"><span data-stu-id="5354a-158">This method returns the following error codes:</span></span>

| <span data-ttu-id="5354a-159">HTTP-statuskod</span><span class="sxs-lookup"><span data-stu-id="5354a-159">HTTP Status Code</span></span>     | <span data-ttu-id="5354a-160">Felkod</span><span class="sxs-lookup"><span data-stu-id="5354a-160">Error code</span></span>   | <span data-ttu-id="5354a-161">Description</span><span class="sxs-lookup"><span data-stu-id="5354a-161">Description</span></span>                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| <span data-ttu-id="5354a-162">404</span><span class="sxs-lookup"><span data-stu-id="5354a-162">404</span></span>                  | <span data-ttu-id="5354a-163">600039</span><span class="sxs-lookup"><span data-stu-id="5354a-163">600039</span></span>       | <span data-ttu-id="5354a-164">Det gick inte att hitta principen för självbetjäning</span><span class="sxs-lookup"><span data-stu-id="5354a-164">Self-serve policy was not found</span></span>                                            |
| <span data-ttu-id="5354a-165">404</span><span class="sxs-lookup"><span data-stu-id="5354a-165">404</span></span>                  | <span data-ttu-id="5354a-166">600040</span><span class="sxs-lookup"><span data-stu-id="5354a-166">600040</span></span>       | <span data-ttu-id="5354a-167">Den självbetjänings princip identifieraren är felaktig</span><span class="sxs-lookup"><span data-stu-id="5354a-167">Self-serve policy identifier is incorrect</span></span>                                  |


### <a name="response-example"></a><span data-ttu-id="5354a-168">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="5354a-168">Response example</span></span>

```http
HTTP/1.1 200 Ok
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
        "etag": "\"1ec98034-a249-46f4-b9dd-9cd464fb5e47\"",
        "objectType": "SelfServePolicy"
    }
}
```
