---
title: Ta bort indirekt återförsäljare i sandbox-miljö
description: Innehåller information om hur du tar bort indirekta Sandbox-återförsäljare och aktiverar testning från slutet till slut med hjälp av API:er.
ms.date: 5/24/2021
ms.author: vijvala
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ba1fd002ac62aba4e414d263b33ecc8153054602
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973017"
---
# <a name="delete-indirect-reseller-in-sandbox"></a><span data-ttu-id="1279c-103">Ta bort indirekt återförsäljare i sandbox-miljö</span><span class="sxs-lookup"><span data-stu-id="1279c-103">Delete Indirect Reseller in Sandbox</span></span>

<span data-ttu-id="1279c-104">**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="1279c-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="1279c-105">Det här dokumentet visar hur du tar bort indirekta sandbox-leverantörer och aktiverar testning från slutet till slut med hjälp av API:er.</span><span class="sxs-lookup"><span data-stu-id="1279c-105">This document shows how to delete Sandbox Indirect Providers and enable end-to-end testing using APIs.</span></span>

> [!Important]
> <span data-ttu-id="1279c-106">Det här dokumentet beskriver funktioner som endast tillåts i sandbox-miljön för indirekta modellupplevelser.</span><span class="sxs-lookup"><span data-stu-id="1279c-106">This document describes features that are only allowed in the Sandbox environment for Indirect Model experiences.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1279c-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="1279c-107">Prerequisites</span></span>

- <span data-ttu-id="1279c-108">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="1279c-108">Credentials as described in [Partner Center Authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1279c-109">Det här scenariot stöder autentisering med autentiseringsuppgifter för App+Användare.</span><span class="sxs-lookup"><span data-stu-id="1279c-109">This scenario supports authentication with App+User credentials.</span></span>

## <a name="sandbox-indirect-provider--delete-sandbox-indirect-reseller"></a><span data-ttu-id="1279c-110">Indirekt Sandbox-provider – Ta bort indirekt Sandbox-återförsäljare</span><span class="sxs-lookup"><span data-stu-id="1279c-110">Sandbox Indirect Provider – Delete Sandbox Indirect Reseller</span></span> 

<span data-ttu-id="1279c-111">Den här funktionen är bara tillgänglig i sandbox-miljön och ger indirekta sandbox-leverantörer möjlighet att skapa indirekta Sandbox-återförsäljare.</span><span class="sxs-lookup"><span data-stu-id="1279c-111">This feature is only available in the Sandbox and gives Sandbox Indirect Providers an ability to create Sandbox Indirect Resellers.</span></span>

1. <span data-ttu-id="1279c-112">Krav för att ta bort en indirekt Sandbox-återförsäljare</span><span class="sxs-lookup"><span data-stu-id="1279c-112">Prerequisites for Deleting a Sandbox Indirect Reseller</span></span>
    1. <span data-ttu-id="1279c-113">Pausa prenumerationerna för varje kund av den indirekta Sandbox-återförsäljaren</span><span class="sxs-lookup"><span data-stu-id="1279c-113">Suspend the subscriptions for each customer of Sandbox Indirect Reseller</span></span>
    2. <span data-ttu-id="1279c-114">Ta bort alla indirekt återförsäljares kunder</span><span class="sxs-lookup"><span data-stu-id="1279c-114">Delete all customers of Indirect Reseller</span></span>
2. <span data-ttu-id="1279c-115">Gräns på fem indirekta Sandbox-återförsäljare per indirekt Sandbox-leverantör.</span><span class="sxs-lookup"><span data-stu-id="1279c-115">Limit of five Sandbox Indirect Resellers allowed per Sandbox Indirect Provider.</span></span> <span data-ttu-id="1279c-116">När den indirekta sandbox-återförsäljaren har tagits bort återställs kvoten.</span><span class="sxs-lookup"><span data-stu-id="1279c-116">Once the Sandbox Indirect reseller is deleted, the quota will be reset.</span></span>

## <a name="delete-sandbox-indirect-reseller-through-api"></a><span data-ttu-id="1279c-117">Ta bort indirekt Sandbox-återförsäljare via API</span><span class="sxs-lookup"><span data-stu-id="1279c-117">Delete Sandbox Indirect Reseller through API</span></span>

### <a name="rest-request"></a><span data-ttu-id="1279c-118">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="1279c-118">REST request</span></span>

#### <a name="request-syntax"></a><span data-ttu-id="1279c-119">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="1279c-119">Request syntax</span></span>

| <span data-ttu-id="1279c-120">Metod</span><span class="sxs-lookup"><span data-stu-id="1279c-120">Method</span></span> | <span data-ttu-id="1279c-121">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="1279c-121">Request URI</span></span>                                                                             |
|------------|-------------------------------------------------------------------------------------|
| <span data-ttu-id="1279c-122">**Ta bort**</span><span class="sxs-lookup"><span data-stu-id="1279c-122">**DELETE**</span></span> | <span data-ttu-id="1279c-123">[*{baseURL}*](partner-center-rest-urls.md)/v1//sandboxIndirectReseller/{resellerId}</span><span class="sxs-lookup"><span data-stu-id="1279c-123">[*{baseURL}*](partner-center-rest-urls.md)/v1//sandboxIndirectReseller/{resellerId}</span></span> |

#### <a name="request-headers"></a><span data-ttu-id="1279c-124">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="1279c-124">Request headers</span></span>

- <span data-ttu-id="1279c-125">Det här API:et är idempotent (det ger inte ett annat resultat om du anropar det flera gånger)</span><span class="sxs-lookup"><span data-stu-id="1279c-125">This API is idempotent (it will not yield a different result if you call it multiple times)</span></span>
- <span data-ttu-id="1279c-126">Ett begärande-ID och korrelations-ID krävs</span><span class="sxs-lookup"><span data-stu-id="1279c-126">A request ID and correlation ID are required</span></span>
- <span data-ttu-id="1279c-127">Mer information finns i [Partner Center REST-huvuden](headers.md)</span><span class="sxs-lookup"><span data-stu-id="1279c-127">For more information, see [Partner Center REST headers](headers.md)</span></span>

### <a name="request-example"></a><span data-ttu-id="1279c-128">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="1279c-128">Request Example</span></span>

<span data-ttu-id="1279c-129">Ta bort https://api.partnercenter.microsoft.com/v1/sandboxIndirectReseller/{resellerID}</span><span class="sxs-lookup"><span data-stu-id="1279c-129">DELETE https://api.partnercenter.microsoft.com/v1/sandboxIndirectReseller/{resellerID}</span></span>

```http
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

####  <a name="response-example"></a><span data-ttu-id="1279c-130">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="1279c-130">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
Date: Wed, 16 Feb 2021 00:43:02 GMT
```

#### <a name="response-success-and-error-codes"></a><span data-ttu-id="1279c-131">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="1279c-131">Response success and error codes</span></span>

<span data-ttu-id="1279c-132">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad och annan felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="1279c-132">Each response comes with an HTTP status code that indicates success or failure and other debugging information.</span></span> <span data-ttu-id="1279c-133">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="1279c-133">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1279c-134">En fullständig lista finns i [Felkoder i Partnercenter.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="1279c-134">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="1279c-135">Den här metoden returnerar följande status för lyckade och felkoder:</span><span class="sxs-lookup"><span data-stu-id="1279c-135">This method returns the following status success and error codes:</span></span>

| <span data-ttu-id="1279c-136">HTTP-statuskod</span><span class="sxs-lookup"><span data-stu-id="1279c-136">HTTP Status Code</span></span>                     | <span data-ttu-id="1279c-137">Felkod</span><span class="sxs-lookup"><span data-stu-id="1279c-137">Error code</span></span>     | <span data-ttu-id="1279c-138">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="1279c-138">Description</span></span>                                      |
|--------------------------------------|----------------|--------------------------------------------------|
| <span data-ttu-id="1279c-139">401</span><span class="sxs-lookup"><span data-stu-id="1279c-139">401</span></span>                                  | <span data-ttu-id="1279c-140">6002</span><span class="sxs-lookup"><span data-stu-id="1279c-140">6002</span></span>           | <span data-ttu-id="1279c-141">Obehörig token eller Inte ett konto för tipsprovider</span><span class="sxs-lookup"><span data-stu-id="1279c-141">Unauthorized token or Not a Tip Provider Account</span></span> |
| <span data-ttu-id="1279c-142">403</span><span class="sxs-lookup"><span data-stu-id="1279c-142">403</span></span>                                  | <span data-ttu-id="1279c-143">6003</span><span class="sxs-lookup"><span data-stu-id="1279c-143">6003</span></span>           | <span data-ttu-id="1279c-144">Det är inte tillåtet att ta bort sandbox-miljö-IR</span><span class="sxs-lookup"><span data-stu-id="1279c-144">Delete Sandbox IR is not allowed</span></span>                 |
| <span data-ttu-id="1279c-145">403</span><span class="sxs-lookup"><span data-stu-id="1279c-145">403</span></span>                                  | <span data-ttu-id="1279c-146">6004</span><span class="sxs-lookup"><span data-stu-id="1279c-146">6004</span></span>           | <span data-ttu-id="1279c-147">Det går inte att skapa sandbox-miljöns IR-åtgärd</span><span class="sxs-lookup"><span data-stu-id="1279c-147">Create Sandbox IR operation not allowed</span></span>          |
| <span data-ttu-id="1279c-148">409</span><span class="sxs-lookup"><span data-stu-id="1279c-148">409</span></span>                                  | <span data-ttu-id="1279c-149">1003</span><span class="sxs-lookup"><span data-stu-id="1279c-149">1003</span></span>           | <span data-ttu-id="1279c-150">Konflikt när klientorganisationen skapas</span><span class="sxs-lookup"><span data-stu-id="1279c-150">Conflict while creating tenant</span></span>                   |
