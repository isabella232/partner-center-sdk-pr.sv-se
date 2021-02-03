---
title: Verifiera domäntillgänglighet
description: Så här avgör du om en domän är tillgänglig för användning.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 84edb5b7510642ec44dad3d4f92349e40eb10b24
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769606"
---
# <a name="verify-domain-availability"></a><span data-ttu-id="97d60-103">Verifiera domäntillgänglighet</span><span class="sxs-lookup"><span data-stu-id="97d60-103">Verify domain availability</span></span>

<span data-ttu-id="97d60-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="97d60-104">**Applies To**</span></span>

- <span data-ttu-id="97d60-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="97d60-105">Partner Center</span></span>
- <span data-ttu-id="97d60-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="97d60-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="97d60-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="97d60-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="97d60-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="97d60-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="97d60-109">Så här avgör du om en domän är tillgänglig för användning.</span><span class="sxs-lookup"><span data-stu-id="97d60-109">How to determine if a domain is available for use.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="97d60-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="97d60-110">Prerequisites</span></span>

- <span data-ttu-id="97d60-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="97d60-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="97d60-112">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="97d60-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="97d60-113">En domän (till exempel `contoso.onmicrosoft.com` ).</span><span class="sxs-lookup"><span data-stu-id="97d60-113">A domain (for example `contoso.onmicrosoft.com`).</span></span>

## <a name="c"></a><span data-ttu-id="97d60-114">C\#</span><span class="sxs-lookup"><span data-stu-id="97d60-114">C\#</span></span>

<span data-ttu-id="97d60-115">För att kontrol lera om en domän är tillgänglig måste du först anropa [**IAggregatePartner. Domains**](/dotnet/api/microsoft.store.partnercenter.ipartner.domains) för att få ett gränssnitt till domän åtgärder.</span><span class="sxs-lookup"><span data-stu-id="97d60-115">To verify if a domain is available, first call [**IAggregatePartner.Domains**](/dotnet/api/microsoft.store.partnercenter.ipartner.domains) to obtain an interface to domain operations.</span></span> <span data-ttu-id="97d60-116">Anropa sedan metoden [**ByDomain**](/dotnet/api/microsoft.store.partnercenter.domains.idomaincollection.bydomain) med domänen för att kontrol lera.</span><span class="sxs-lookup"><span data-stu-id="97d60-116">Then call the [**ByDomain**](/dotnet/api/microsoft.store.partnercenter.domains.idomaincollection.bydomain) method with the domain to check.</span></span> <span data-ttu-id="97d60-117">Den här metoden hämtar ett gränssnitt till de åtgärder som är tillgängliga för en speciell domän.</span><span class="sxs-lookup"><span data-stu-id="97d60-117">This method retrieves an interface to the operations available for a specific domain.</span></span> <span data-ttu-id="97d60-118">Anropa slutligen metoden [**exists**](/dotnet/api/microsoft.store.partnercenter.domains.idomain.exists) för att se om domänen redan finns.</span><span class="sxs-lookup"><span data-stu-id="97d60-118">Finally, call the [**Exists**](/dotnet/api/microsoft.store.partnercenter.domains.idomain.exists) method to see if the domain already exists.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// const string domain = "contoso.onmicrosoft.com";

bool result = partnerOperations.Domains.ByDomain(domain).Exists();
```

<span data-ttu-id="97d60-119">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="97d60-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="97d60-120">**Projekt**: Partner Center SDK-exempel **klass**: CheckDomainAvailability.CS</span><span class="sxs-lookup"><span data-stu-id="97d60-120">**Project**: Partner Center SDK Samples **Class**: CheckDomainAvailability.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="97d60-121">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="97d60-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="97d60-122">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="97d60-122">Request syntax</span></span>

| <span data-ttu-id="97d60-123">Metod</span><span class="sxs-lookup"><span data-stu-id="97d60-123">Method</span></span>   | <span data-ttu-id="97d60-124">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="97d60-124">Request URI</span></span>                                                              |
|----------|--------------------------------------------------------------------------|
| <span data-ttu-id="97d60-125">**FÖRETAGETS**</span><span class="sxs-lookup"><span data-stu-id="97d60-125">**HEAD**</span></span> | <span data-ttu-id="97d60-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/Domains/{Domain} http/1.1</span><span class="sxs-lookup"><span data-stu-id="97d60-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/domains/{domain} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="97d60-127">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="97d60-127">URI parameter</span></span>

<span data-ttu-id="97d60-128">Använd följande frågeparameter för att kontrol lera domänens tillgänglighet.</span><span class="sxs-lookup"><span data-stu-id="97d60-128">Use the following query parameter to verify domain availability.</span></span>

| <span data-ttu-id="97d60-129">Namn</span><span class="sxs-lookup"><span data-stu-id="97d60-129">Name</span></span>       | <span data-ttu-id="97d60-130">Typ</span><span class="sxs-lookup"><span data-stu-id="97d60-130">Type</span></span>       | <span data-ttu-id="97d60-131">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="97d60-131">Required</span></span> | <span data-ttu-id="97d60-132">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="97d60-132">Description</span></span>                                   |
|------------|------------|----------|-----------------------------------------------|
| <span data-ttu-id="97d60-133">**domänsuffix**</span><span class="sxs-lookup"><span data-stu-id="97d60-133">**domain**</span></span> | <span data-ttu-id="97d60-134">**nollängd**</span><span class="sxs-lookup"><span data-stu-id="97d60-134">**string**</span></span> | <span data-ttu-id="97d60-135">Y</span><span class="sxs-lookup"><span data-stu-id="97d60-135">Y</span></span>        | <span data-ttu-id="97d60-136">En sträng som identifierar den domän som ska kontrol leras.</span><span class="sxs-lookup"><span data-stu-id="97d60-136">A string that identifies the domain to check.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="97d60-137">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="97d60-137">Request headers</span></span>

<span data-ttu-id="97d60-138">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="97d60-138">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="97d60-139">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="97d60-139">Request body</span></span>

<span data-ttu-id="97d60-140">Inget</span><span class="sxs-lookup"><span data-stu-id="97d60-140">None</span></span>

### <a name="request-example"></a><span data-ttu-id="97d60-141">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="97d60-141">Request example</span></span>

```http
HEAD https://api.partnercenter.microsoft.com/v1/domains/contoso.onmicrosoft.com HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: cf5b00d6-9240-431c-a973-cc06c904e5bf
MS-CorrelationId: ec57501a-a4c3-45ee-ab2b-da4250545fc9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="97d60-142">REST-svar</span><span class="sxs-lookup"><span data-stu-id="97d60-142">REST response</span></span>

<span data-ttu-id="97d60-143">Om domänen finns är den inte tillgänglig för användning och svars status koden 200 OK returneras.</span><span class="sxs-lookup"><span data-stu-id="97d60-143">If the domain exists, it isn't available for use and a response status code 200 OK is returned.</span></span> <span data-ttu-id="97d60-144">Om domänen inte hittas, är den tillgänglig för användning och en svars status kod 404 som inte hittas returneras.</span><span class="sxs-lookup"><span data-stu-id="97d60-144">If the domain isn't found, it's available for use and a response status code 404 Not Found is returned.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="97d60-145">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="97d60-145">Response success and error codes</span></span>

<span data-ttu-id="97d60-146">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="97d60-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="97d60-147">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="97d60-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="97d60-148">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="97d60-148">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example-for-when-the-domain-is-already-in-use"></a><span data-ttu-id="97d60-149">Svars exempel för när domänen redan används</span><span class="sxs-lookup"><span data-stu-id="97d60-149">Response example for when the domain is already in use</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 0
MS-CorrelationId: ec57501a-a4c3-45ee-ab2b-da4250545fc9
MS-RequestId: cf5b00d6-9240-431c-a973-cc06c904e5bf
MS-CV: 7UXAHds8J0mNUCSp.0
MS-ServerId: 201022015
Date: Tue, 31 Jan 2017 22:22:35 GMT
```

### <a name="response-example-for-when-the-domain-is-available"></a><span data-ttu-id="97d60-150">Svars exempel för när domänen är tillgänglig</span><span class="sxs-lookup"><span data-stu-id="97d60-150">Response example for when the domain is available</span></span>

```http
HTTP/1.1 404 Not Found
Content-Length: 0
MS-CorrelationId: 54770745-17f0-433c-bd7b-0265e5b38f98
MS-RequestId: 1169a4cd-3be7-4e29-9cb3-0f78ffa2e91e
MS-CV: RRmc+bEw9U2e97CC.0
MS-ServerId: 202010406
Date: Tue, 31 Jan 2017 22:36:01 GMT
```
