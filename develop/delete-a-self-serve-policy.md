---
title: Ta bort en princip för självbetjäning
description: Så här tar du bort en princip för självbetjäning.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3450145d6daf2ffca5e2886245e592406cb0886d
ms.sourcegitcommit: 01e75175077611da92175c777a440a594fb05797
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/08/2020
ms.locfileid: "97770225"
---
# <a name="delete-a-selfservepolicy"></a><span data-ttu-id="f7863-103">Ta bort en SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="f7863-103">Delete a SelfServePolicy</span></span>

<span data-ttu-id="f7863-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="f7863-104">**Applies to:**</span></span>

- <span data-ttu-id="f7863-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="f7863-105">Partner Center</span></span>

<span data-ttu-id="f7863-106">I det här avsnittet beskrivs hur du uppdaterar en princip för självbetjäning.</span><span class="sxs-lookup"><span data-stu-id="f7863-106">This topic explains how to update a self-serve policy.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f7863-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="f7863-107">Prerequisites</span></span>

- <span data-ttu-id="f7863-108">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="f7863-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f7863-109">Det här scenariot stöder autentisering med program-och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="f7863-109">This scenario supports authentication with Application+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="f7863-110">C\#</span><span class="sxs-lookup"><span data-stu-id="f7863-110">C\#</span></span>

<span data-ttu-id="f7863-111">Så här tar du bort en princip för självbetjäning:</span><span class="sxs-lookup"><span data-stu-id="f7863-111">To delete a self-serve policy:</span></span>

1. <span data-ttu-id="f7863-112">Anropa metoden [**IAggregatePartner. SelfServePolicies. ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) med enhets-ID: n för att hämta ett gränssnitt till åtgärder i principerna.</span><span class="sxs-lookup"><span data-stu-id="f7863-112">Call the [**IAggregatePartner.SelfServePolicies.ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) method with the entity identifier to retrieve an interface to operations on the policies.</span></span>

2. <span data-ttu-id="f7863-113">Anropa [**Delete**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.delete) -eller [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.deleteasync) -metoden för att ta bort principen för självbetjäning.</span><span class="sxs-lookup"><span data-stu-id="f7863-113">Call the [**Delete**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.delete) or [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.deleteasync) method to delete the self-serve policy.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
string policyId;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// deletes the self-serve policies
partnerOperations.SelfServePolicies.ById(policyId).Delete();
```

<span data-ttu-id="f7863-114">Ett exempel finns i följande avsnitt:</span><span class="sxs-lookup"><span data-stu-id="f7863-114">For an example, see the following:</span></span>

- <span data-ttu-id="f7863-115">Exempel: [konsol test app](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="f7863-115">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="f7863-116">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="f7863-116">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="f7863-117">Klass: **DeleteSelfServePolicies.cs**</span><span class="sxs-lookup"><span data-stu-id="f7863-117">Class: **DeleteSelfServePolicies.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="f7863-118">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="f7863-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f7863-119">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="f7863-119">Request syntax</span></span>

| <span data-ttu-id="f7863-120">Metod</span><span class="sxs-lookup"><span data-stu-id="f7863-120">Method</span></span>  | <span data-ttu-id="f7863-121">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="f7863-121">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="f7863-122">**TA bort**</span><span class="sxs-lookup"><span data-stu-id="f7863-122">**DELETE**</span></span> | <span data-ttu-id="f7863-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="f7863-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{id} HTTP/1.1</span></span> |

<span data-ttu-id="f7863-124">**URI-parameter**</span><span class="sxs-lookup"><span data-stu-id="f7863-124">**URI parameter**</span></span>

<span data-ttu-id="f7863-125">Använd följande Sök vägs parametrar för att hämta den angivna produkten.</span><span class="sxs-lookup"><span data-stu-id="f7863-125">Use the following path parameters to get the specified product.</span></span>

| <span data-ttu-id="f7863-126">Namn</span><span class="sxs-lookup"><span data-stu-id="f7863-126">Name</span></span>                       | <span data-ttu-id="f7863-127">Typ</span><span class="sxs-lookup"><span data-stu-id="f7863-127">Type</span></span>         | <span data-ttu-id="f7863-128">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="f7863-128">Required</span></span> | <span data-ttu-id="f7863-129">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="f7863-129">Description</span></span>                                                     |
|----------------------------|--------------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="f7863-130">**SelfServePolicy-ID**</span><span class="sxs-lookup"><span data-stu-id="f7863-130">**SelfServePolicy-id**</span></span>     | <span data-ttu-id="f7863-131">**nollängd**</span><span class="sxs-lookup"><span data-stu-id="f7863-131">**string**</span></span>   | <span data-ttu-id="f7863-132">Yes</span><span class="sxs-lookup"><span data-stu-id="f7863-132">Yes</span></span>      | <span data-ttu-id="f7863-133">En sträng som identifierar principen för självbetjäning.</span><span class="sxs-lookup"><span data-stu-id="f7863-133">A string that identifies the self-serve policy.</span></span>                 |

### <a name="request-headers"></a><span data-ttu-id="f7863-134">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="f7863-134">Request headers</span></span>

- <span data-ttu-id="f7863-135">ID för begäran och korrelations-ID krävs.</span><span class="sxs-lookup"><span data-stu-id="f7863-135">A request ID and correlation ID are required.</span></span>
- <span data-ttu-id="f7863-136">Mer information finns i [partner Center rest-rubriker](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="f7863-136">See [Partner Center REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="f7863-137">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="f7863-137">Request body</span></span>

<span data-ttu-id="f7863-138">Inga.</span><span class="sxs-lookup"><span data-stu-id="f7863-138">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="f7863-139">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="f7863-139">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="f7863-140">REST-svar</span><span class="sxs-lookup"><span data-stu-id="f7863-140">REST response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f7863-141">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="f7863-141">Response success and error codes</span></span>

<span data-ttu-id="f7863-142">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="f7863-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f7863-143">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="f7863-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f7863-144">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="f7863-144">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f7863-145">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="f7863-145">Response example</span></span>

```http
HTTP/1.1 204 deleted
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
Date: Tue, 14 Feb 2017 20:06:02 GMT

```
