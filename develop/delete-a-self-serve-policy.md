---
title: Ta bort en princip för självbetjäning
description: Ta bort en princip för självbetjäning.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 063cf98d4c78e82622e486427baeb1a5721715e5
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973102"
---
# <a name="delete-a-selfservepolicy"></a><span data-ttu-id="999ed-103">Ta bort en SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="999ed-103">Delete a SelfServePolicy</span></span>

<span data-ttu-id="999ed-104">Den här artikeln förklarar hur du uppdaterar en självbetjäningsprincip.</span><span class="sxs-lookup"><span data-stu-id="999ed-104">This article explains how to update a self-serve policy.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="999ed-105">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="999ed-105">Prerequisites</span></span>

- <span data-ttu-id="999ed-106">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="999ed-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="999ed-107">Det här scenariot stöder autentisering med autentiseringsuppgifter för program+användare.</span><span class="sxs-lookup"><span data-stu-id="999ed-107">This scenario supports authentication with Application+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="999ed-108">C\#</span><span class="sxs-lookup"><span data-stu-id="999ed-108">C\#</span></span>

<span data-ttu-id="999ed-109">Så här tar du bort en princip för självbetjäning:</span><span class="sxs-lookup"><span data-stu-id="999ed-109">To delete a self-serve policy:</span></span>

1. <span data-ttu-id="999ed-110">Anropa metoden [**IAggregatePartner.SelfServePolicies.ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) med entitetsidentifieraren för att hämta ett gränssnitt till åtgärder för principerna.</span><span class="sxs-lookup"><span data-stu-id="999ed-110">Call the [**IAggregatePartner.SelfServePolicies.ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) method with the entity identifier to retrieve an interface to operations on the policies.</span></span>

2. <span data-ttu-id="999ed-111">Anropa metoden [**Delete**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.delete) eller [**DeleteAsync för**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.deleteasync) att ta bort principen för självbetjäning.</span><span class="sxs-lookup"><span data-stu-id="999ed-111">Call the [**Delete**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.delete) or [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.deleteasync) method to delete the self-serve policy.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
string policyId;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// deletes the self-serve policies
partnerOperations.SelfServePolicies.ById(policyId).Delete();
```

<span data-ttu-id="999ed-112">Ett exempel finns i följande:</span><span class="sxs-lookup"><span data-stu-id="999ed-112">For an example, see the following:</span></span>

- <span data-ttu-id="999ed-113">Exempel: [Konsoltestapp](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="999ed-113">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="999ed-114">Project: **PartnerSDK.FeatureExempel**</span><span class="sxs-lookup"><span data-stu-id="999ed-114">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="999ed-115">Klass: **DeleteSelfServePolicies.cs**</span><span class="sxs-lookup"><span data-stu-id="999ed-115">Class: **DeleteSelfServePolicies.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="999ed-116">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="999ed-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="999ed-117">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="999ed-117">Request syntax</span></span>

| <span data-ttu-id="999ed-118">Metod</span><span class="sxs-lookup"><span data-stu-id="999ed-118">Method</span></span>  | <span data-ttu-id="999ed-119">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="999ed-119">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="999ed-120">**Ta bort**</span><span class="sxs-lookup"><span data-stu-id="999ed-120">**DELETE**</span></span> | <span data-ttu-id="999ed-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="999ed-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{id} HTTP/1.1</span></span> |

<span data-ttu-id="999ed-122">**URI-parameter**</span><span class="sxs-lookup"><span data-stu-id="999ed-122">**URI parameter**</span></span>

<span data-ttu-id="999ed-123">Använd följande sökvägsparametrar för att hämta den angivna produkten.</span><span class="sxs-lookup"><span data-stu-id="999ed-123">Use the following path parameters to get the specified product.</span></span>

| <span data-ttu-id="999ed-124">Namn</span><span class="sxs-lookup"><span data-stu-id="999ed-124">Name</span></span>                       | <span data-ttu-id="999ed-125">Typ</span><span class="sxs-lookup"><span data-stu-id="999ed-125">Type</span></span>         | <span data-ttu-id="999ed-126">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="999ed-126">Required</span></span> | <span data-ttu-id="999ed-127">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="999ed-127">Description</span></span>                                                     |
|----------------------------|--------------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="999ed-128">**SelfServePolicy-id**</span><span class="sxs-lookup"><span data-stu-id="999ed-128">**SelfServePolicy-id**</span></span>     | <span data-ttu-id="999ed-129">**sträng**</span><span class="sxs-lookup"><span data-stu-id="999ed-129">**string**</span></span>   | <span data-ttu-id="999ed-130">Ja</span><span class="sxs-lookup"><span data-stu-id="999ed-130">Yes</span></span>      | <span data-ttu-id="999ed-131">En sträng som identifierar självbetjäningsprincipen.</span><span class="sxs-lookup"><span data-stu-id="999ed-131">A string that identifies the self-serve policy.</span></span>                 |

### <a name="request-headers"></a><span data-ttu-id="999ed-132">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="999ed-132">Request headers</span></span>

- <span data-ttu-id="999ed-133">Ett begärande-ID och korrelations-ID krävs.</span><span class="sxs-lookup"><span data-stu-id="999ed-133">A request ID and correlation ID are required.</span></span>
- <span data-ttu-id="999ed-134">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="999ed-134">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="999ed-135">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="999ed-135">Request body</span></span>

<span data-ttu-id="999ed-136">Inga.</span><span class="sxs-lookup"><span data-stu-id="999ed-136">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="999ed-137">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="999ed-137">Request example</span></span>

```http
DELETE https://api.partnercenter.microsoft.com/v1/SelfServePolicy/634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 789
Connection: Keep-Alive

```

## <a name="rest-response"></a><span data-ttu-id="999ed-138">REST-svar</span><span class="sxs-lookup"><span data-stu-id="999ed-138">REST response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="999ed-139">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="999ed-139">Response success and error codes</span></span>

<span data-ttu-id="999ed-140">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="999ed-140">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="999ed-141">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="999ed-141">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="999ed-142">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="999ed-142">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="999ed-143">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="999ed-143">Response example</span></span>

```http
HTTP/1.1 204 deleted
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
Date: Tue, 14 Feb 2017 20:06:02 GMT

```
