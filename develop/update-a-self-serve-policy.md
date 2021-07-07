---
title: Uppdatera en självbetjäningsprincip
description: Så här uppdaterar du en självbetjäningsprincip.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d94382e73fd2a79751fe5f8f8414df2befde584f
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445263"
---
# <a name="update-a-selfservepolicy"></a><span data-ttu-id="367f4-103">Uppdatera en SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="367f4-103">Update a SelfServePolicy</span></span>

<span data-ttu-id="367f4-104">Den här artikeln förklarar hur du uppdaterar en självbetjäningsprincip.</span><span class="sxs-lookup"><span data-stu-id="367f4-104">This article explains how to update a self-serve policy.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="367f4-105">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="367f4-105">Prerequisites</span></span>

- <span data-ttu-id="367f4-106">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="367f4-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="367f4-107">Det här scenariot stöder autentisering med autentiseringsuppgifter för program och användare.</span><span class="sxs-lookup"><span data-stu-id="367f4-107">This scenario supports authentication with Application+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="367f4-108">C\#</span><span class="sxs-lookup"><span data-stu-id="367f4-108">C\#</span></span>

<span data-ttu-id="367f4-109">Så här tar du bort en självbetjäningsprincip:</span><span class="sxs-lookup"><span data-stu-id="367f4-109">To delete a self-serve policy:</span></span>

1. <span data-ttu-id="367f4-110">Anropa metoden [**IAggregatePartner.SelfServePolicies.ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) med entitetsidentifieraren för att hämta ett gränssnitt till åtgärder för principerna.</span><span class="sxs-lookup"><span data-stu-id="367f4-110">Call the [**IAggregatePartner.SelfServePolicies.ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) method with the entity identifier to retrieve an interface to operations on the policies.</span></span>

2. <span data-ttu-id="367f4-111">Anropa [**Put-**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.put) eller [**PutAsync-metoden**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.putasync) för att uppdatera självbetjäningsprincipen.</span><span class="sxs-lookup"><span data-stu-id="367f4-111">Call the [**Put**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.put) or [**PutAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.putasync) method to update the self-serve policy.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
SelfServePolicy policy;

// All the operations executed on this partner operation instance will share the same correlation identifier but will differ in request identifier
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// updates the self-serve policies
partnerOperations.SelfServePolicies.ById(policy.id).Put(policy);
```

## <a name="rest-request"></a><span data-ttu-id="367f4-112">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="367f4-112">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="367f4-113">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="367f4-113">Request syntax</span></span>

| <span data-ttu-id="367f4-114">Metod</span><span class="sxs-lookup"><span data-stu-id="367f4-114">Method</span></span>   | <span data-ttu-id="367f4-115">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="367f4-115">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="367f4-116">**PUT**</span><span class="sxs-lookup"><span data-stu-id="367f4-116">**PUT**</span></span> | <span data-ttu-id="367f4-117">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="367f4-117">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="367f4-118">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="367f4-118">Request headers</span></span>

- <span data-ttu-id="367f4-119">En begärandeidentifierare och korrelationsidentifierare krävs.</span><span class="sxs-lookup"><span data-stu-id="367f4-119">A request identifier and correlation identifier are required.</span></span>
- <span data-ttu-id="367f4-120">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="367f4-120">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="367f4-121">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="367f4-121">Request body</span></span>

<span data-ttu-id="367f4-122">I den här tabellen beskrivs de obligatoriska egenskaperna i begärandetexten.</span><span class="sxs-lookup"><span data-stu-id="367f4-122">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="367f4-123">Namn</span><span class="sxs-lookup"><span data-stu-id="367f4-123">Name</span></span>                              | <span data-ttu-id="367f4-124">Typ</span><span class="sxs-lookup"><span data-stu-id="367f4-124">Type</span></span>   | <span data-ttu-id="367f4-125">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="367f4-125">Description</span></span>                                 |
|------------------------------------------------------------------|--------|---------------------------------------------|
| [<span data-ttu-id="367f4-126">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="367f4-126">SelfServePolicy</span></span>](self-serve-policy-resources.md#selfservepolicy)| <span data-ttu-id="367f4-127">objekt</span><span class="sxs-lookup"><span data-stu-id="367f4-127">object</span></span> | <span data-ttu-id="367f4-128">Information om självbetjäningsprincipen.</span><span class="sxs-lookup"><span data-stu-id="367f4-128">The self-serve policy information.</span></span> |

#### <a name="selfservepolicy"></a><span data-ttu-id="367f4-129">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="367f4-129">SelfServePolicy</span></span>

<span data-ttu-id="367f4-130">I den här tabellen beskrivs de minsta obligatoriska fälten från [SelfServePolicy-resursen](self-serve-policy-resources.md#selfservepolicy) som krävs för att skapa en ny självbetjäningsprincip.</span><span class="sxs-lookup"><span data-stu-id="367f4-130">This table describes the minimum required fields from the [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource needed to create a new self-serve policy.</span></span>

| <span data-ttu-id="367f4-131">Egenskap</span><span class="sxs-lookup"><span data-stu-id="367f4-131">Property</span></span>              | <span data-ttu-id="367f4-132">Typ</span><span class="sxs-lookup"><span data-stu-id="367f4-132">Type</span></span>             | <span data-ttu-id="367f4-133">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="367f4-133">Description</span></span>                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="367f4-134">id</span><span class="sxs-lookup"><span data-stu-id="367f4-134">id</span></span>                    | <span data-ttu-id="367f4-135">sträng</span><span class="sxs-lookup"><span data-stu-id="367f4-135">string</span></span>           | <span data-ttu-id="367f4-136">En principidentifierare med självbetjäning som tillhandahålls när självbetjäningsprincipen har skapats.</span><span class="sxs-lookup"><span data-stu-id="367f4-136">A self-serve policy identifier that is supplied upon successful creation of the self-serve policy.</span></span>     |
| <span data-ttu-id="367f4-137">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="367f4-137">SelfServeEntity</span></span>       | <span data-ttu-id="367f4-138">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="367f4-138">SelfServeEntity</span></span>  | <span data-ttu-id="367f4-139">Entiteten med självbetjäning som beviljas åtkomst.</span><span class="sxs-lookup"><span data-stu-id="367f4-139">The self-serve entity that is being granted access.</span></span>                                                     |
| <span data-ttu-id="367f4-140">Beviljaren</span><span class="sxs-lookup"><span data-stu-id="367f4-140">Grantor</span></span>               | <span data-ttu-id="367f4-141">Beviljaren</span><span class="sxs-lookup"><span data-stu-id="367f4-141">Grantor</span></span>          | <span data-ttu-id="367f4-142">Den beviljande som beviljar åtkomst.</span><span class="sxs-lookup"><span data-stu-id="367f4-142">The grantor that is granting access.</span></span>                                                                    |
| <span data-ttu-id="367f4-143">Behörigheter</span><span class="sxs-lookup"><span data-stu-id="367f4-143">Permissions</span></span>           | <span data-ttu-id="367f4-144">Behörighetsmatris</span><span class="sxs-lookup"><span data-stu-id="367f4-144">Array of Permission</span></span>| <span data-ttu-id="367f4-145">En matris med [behörighetsresurser.](self-serve-policy-resources.md#permission)</span><span class="sxs-lookup"><span data-stu-id="367f4-145">An Array of [Permission](self-serve-policy-resources.md#permission) resources.</span></span>                                                      |
| <span data-ttu-id="367f4-146">Etag</span><span class="sxs-lookup"><span data-stu-id="367f4-146">Etag</span></span>                  | <span data-ttu-id="367f4-147">sträng</span><span class="sxs-lookup"><span data-stu-id="367f4-147">string</span></span>           | <span data-ttu-id="367f4-148">The Etag.</span><span class="sxs-lookup"><span data-stu-id="367f4-148">The Etag.</span></span>                                                                                               |


### <a name="request-example"></a><span data-ttu-id="367f4-149">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="367f4-149">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="367f4-150">REST-svar</span><span class="sxs-lookup"><span data-stu-id="367f4-150">REST response</span></span>

<span data-ttu-id="367f4-151">Om det lyckas returnerar detta API en [SelfServePolicy-resurs](self-serve-policy-resources.md#selfservepolicy) för den uppdaterade självbetjäningsprincipen.</span><span class="sxs-lookup"><span data-stu-id="367f4-151">If successful, this API returns a [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource for the updated self-serve policy.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="367f4-152">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="367f4-152">Response success and error codes</span></span>

<span data-ttu-id="367f4-153">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="367f4-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="367f4-154">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="367f4-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="367f4-155">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="367f4-155">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

<span data-ttu-id="367f4-156">Den här metoden returnerar följande felkoder:</span><span class="sxs-lookup"><span data-stu-id="367f4-156">This method returns the following error codes:</span></span>

| <span data-ttu-id="367f4-157">HTTP-statuskod</span><span class="sxs-lookup"><span data-stu-id="367f4-157">HTTP Status Code</span></span>     | <span data-ttu-id="367f4-158">Felkod</span><span class="sxs-lookup"><span data-stu-id="367f4-158">Error code</span></span>   | <span data-ttu-id="367f4-159">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="367f4-159">Description</span></span>                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| <span data-ttu-id="367f4-160">404</span><span class="sxs-lookup"><span data-stu-id="367f4-160">404</span></span>                  | <span data-ttu-id="367f4-161">600039</span><span class="sxs-lookup"><span data-stu-id="367f4-161">600039</span></span>       | <span data-ttu-id="367f4-162">Självbetjäningsprincipen hittades inte</span><span class="sxs-lookup"><span data-stu-id="367f4-162">Self-serve policy was not found</span></span>                                            |
| <span data-ttu-id="367f4-163">404</span><span class="sxs-lookup"><span data-stu-id="367f4-163">404</span></span>                  | <span data-ttu-id="367f4-164">600040</span><span class="sxs-lookup"><span data-stu-id="367f4-164">600040</span></span>       | <span data-ttu-id="367f4-165">Principidentifieraren för självbetjäning är felaktig</span><span class="sxs-lookup"><span data-stu-id="367f4-165">Self-serve policy identifier is incorrect</span></span>                                  |


### <a name="response-example"></a><span data-ttu-id="367f4-166">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="367f4-166">Response example</span></span>

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
