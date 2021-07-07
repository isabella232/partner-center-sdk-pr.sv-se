---
title: Verifiera domäntillgänglighet
description: Så här avgör du om en domän är tillgänglig för användning.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e2b8f0438516cc0aff9c4d8159c22de43ec582e4
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530284"
---
# <a name="verify-domain-availability"></a><span data-ttu-id="bf346-103">Verifiera domäntillgänglighet</span><span class="sxs-lookup"><span data-stu-id="bf346-103">Verify domain availability</span></span>

<span data-ttu-id="bf346-104">**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="bf346-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="bf346-105">Så här avgör du om en domän är tillgänglig för användning.</span><span class="sxs-lookup"><span data-stu-id="bf346-105">How to determine if a domain is available for use.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bf346-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="bf346-106">Prerequisites</span></span>

- <span data-ttu-id="bf346-107">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="bf346-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="bf346-108">Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="bf346-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="bf346-109">En domän (till exempel `contoso.onmicrosoft.com` ).</span><span class="sxs-lookup"><span data-stu-id="bf346-109">A domain (for example `contoso.onmicrosoft.com`).</span></span>

## <a name="c"></a><span data-ttu-id="bf346-110">C\#</span><span class="sxs-lookup"><span data-stu-id="bf346-110">C\#</span></span>

<span data-ttu-id="bf346-111">Om du vill kontrollera om en domän är tillgänglig anropar du [**först IAggregatePartner.Domains för**](/dotnet/api/microsoft.store.partnercenter.ipartner.domains) att hämta ett gränssnitt till domänåtgärder.</span><span class="sxs-lookup"><span data-stu-id="bf346-111">To verify if a domain is available, first call [**IAggregatePartner.Domains**](/dotnet/api/microsoft.store.partnercenter.ipartner.domains) to obtain an interface to domain operations.</span></span> <span data-ttu-id="bf346-112">Anropa sedan [**metoden ByDomain**](/dotnet/api/microsoft.store.partnercenter.domains.idomaincollection.bydomain) med domänen för att kontrollera.</span><span class="sxs-lookup"><span data-stu-id="bf346-112">Then call the [**ByDomain**](/dotnet/api/microsoft.store.partnercenter.domains.idomaincollection.bydomain) method with the domain to check.</span></span> <span data-ttu-id="bf346-113">Den här metoden hämtar ett gränssnitt för de åtgärder som är tillgängliga för en specifik domän.</span><span class="sxs-lookup"><span data-stu-id="bf346-113">This method retrieves an interface to the operations available for a specific domain.</span></span> <span data-ttu-id="bf346-114">Anropa slutligen metoden [**Exists**](/dotnet/api/microsoft.store.partnercenter.domains.idomain.exists) för att se om domänen redan finns.</span><span class="sxs-lookup"><span data-stu-id="bf346-114">Finally, call the [**Exists**](/dotnet/api/microsoft.store.partnercenter.domains.idomain.exists) method to see if the domain already exists.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// const string domain = "contoso.onmicrosoft.com";

bool result = partnerOperations.Domains.ByDomain(domain).Exists();
```

<span data-ttu-id="bf346-115">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="bf346-115">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="bf346-116">**Project:** Partnercenter-SDK **exempelklass:** CheckDomainAvailability.cs</span><span class="sxs-lookup"><span data-stu-id="bf346-116">**Project**: Partner Center SDK Samples **Class**: CheckDomainAvailability.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="bf346-117">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="bf346-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="bf346-118">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="bf346-118">Request syntax</span></span>

| <span data-ttu-id="bf346-119">Metod</span><span class="sxs-lookup"><span data-stu-id="bf346-119">Method</span></span>   | <span data-ttu-id="bf346-120">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="bf346-120">Request URI</span></span>                                                              |
|----------|--------------------------------------------------------------------------|
| <span data-ttu-id="bf346-121">**Huvud**</span><span class="sxs-lookup"><span data-stu-id="bf346-121">**HEAD**</span></span> | <span data-ttu-id="bf346-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/domains/{domain} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="bf346-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/domains/{domain} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="bf346-123">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="bf346-123">URI parameter</span></span>

<span data-ttu-id="bf346-124">Använd följande frågeparameter för att verifiera domänens tillgänglighet.</span><span class="sxs-lookup"><span data-stu-id="bf346-124">Use the following query parameter to verify domain availability.</span></span>

| <span data-ttu-id="bf346-125">Namn</span><span class="sxs-lookup"><span data-stu-id="bf346-125">Name</span></span>       | <span data-ttu-id="bf346-126">Typ</span><span class="sxs-lookup"><span data-stu-id="bf346-126">Type</span></span>       | <span data-ttu-id="bf346-127">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="bf346-127">Required</span></span> | <span data-ttu-id="bf346-128">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="bf346-128">Description</span></span>                                   |
|------------|------------|----------|-----------------------------------------------|
| <span data-ttu-id="bf346-129">**Domän**</span><span class="sxs-lookup"><span data-stu-id="bf346-129">**domain**</span></span> | <span data-ttu-id="bf346-130">**sträng**</span><span class="sxs-lookup"><span data-stu-id="bf346-130">**string**</span></span> | <span data-ttu-id="bf346-131">Y</span><span class="sxs-lookup"><span data-stu-id="bf346-131">Y</span></span>        | <span data-ttu-id="bf346-132">En sträng som identifierar domänen som ska kontrolleras.</span><span class="sxs-lookup"><span data-stu-id="bf346-132">A string that identifies the domain to check.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="bf346-133">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="bf346-133">Request headers</span></span>

<span data-ttu-id="bf346-134">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="bf346-134">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="bf346-135">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="bf346-135">Request body</span></span>

<span data-ttu-id="bf346-136">Ingen</span><span class="sxs-lookup"><span data-stu-id="bf346-136">None</span></span>

### <a name="request-example"></a><span data-ttu-id="bf346-137">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="bf346-137">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="bf346-138">REST-svar</span><span class="sxs-lookup"><span data-stu-id="bf346-138">REST response</span></span>

<span data-ttu-id="bf346-139">Om domänen finns är den inte tillgänglig för användning och svarsstatuskoden 200 OK returneras.</span><span class="sxs-lookup"><span data-stu-id="bf346-139">If the domain exists, it isn't available for use and a response status code 200 OK is returned.</span></span> <span data-ttu-id="bf346-140">Om domänen inte hittas är den tillgänglig för användning och svarsstatuskoden 404 Hittades inte returneras.</span><span class="sxs-lookup"><span data-stu-id="bf346-140">If the domain isn't found, it's available for use and a response status code 404 Not Found is returned.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="bf346-141">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="bf346-141">Response success and error codes</span></span>

<span data-ttu-id="bf346-142">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="bf346-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="bf346-143">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="bf346-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="bf346-144">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="bf346-144">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example-for-when-the-domain-is-already-in-use"></a><span data-ttu-id="bf346-145">Svarsexempel för när domänen redan används</span><span class="sxs-lookup"><span data-stu-id="bf346-145">Response example for when the domain is already in use</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 0
MS-CorrelationId: ec57501a-a4c3-45ee-ab2b-da4250545fc9
MS-RequestId: cf5b00d6-9240-431c-a973-cc06c904e5bf
MS-CV: 7UXAHds8J0mNUCSp.0
MS-ServerId: 201022015
Date: Tue, 31 Jan 2017 22:22:35 GMT
```

### <a name="response-example-for-when-the-domain-is-available"></a><span data-ttu-id="bf346-146">Svarsexempel för när domänen är tillgänglig</span><span class="sxs-lookup"><span data-stu-id="bf346-146">Response example for when the domain is available</span></span>

```http
HTTP/1.1 404 Not Found
Content-Length: 0
MS-CorrelationId: 54770745-17f0-433c-bd7b-0265e5b38f98
MS-RequestId: 1169a4cd-3be7-4e29-9cb3-0f78ffa2e91e
MS-CV: RRmc+bEw9U2e97CC.0
MS-ServerId: 202010406
Date: Tue, 31 Jan 2017 22:36:01 GMT
```
