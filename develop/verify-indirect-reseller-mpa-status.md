---
title: Verifiera en indirekt åter försäljares signerings status för Microsoft partner Agreement
description: 'Du kan använda AgreementStatus-API: et för att kontrol lera om en indirekt åter försäljare har undertecknat Microsofts partner avtal.'
ms.date: 07/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 436f690991a2920465a5a13c73eb4c194956ae94
ms.sourcegitcommit: ca932ba511bf7464a634195d71891f989036ab74
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/29/2020
ms.locfileid: "97769933"
---
# <a name="verify-an-indirect-resellers-microsoft-partner-agreement-signing-status"></a><span data-ttu-id="67eb6-103">Verifiera en indirekt åter försäljares signerings status för Microsoft partner Agreement</span><span class="sxs-lookup"><span data-stu-id="67eb6-103">Verify an indirect reseller's Microsoft Partner Agreement signing status</span></span>

<span data-ttu-id="67eb6-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="67eb6-104">**Applies to:**</span></span>

- <span data-ttu-id="67eb6-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="67eb6-105">Partner Center</span></span>
- <span data-ttu-id="67eb6-106">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="67eb6-106">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="67eb6-107">Du kan kontrol lera om en indirekt åter försäljare har undertecknat Microsoft partner Agreement genom att använda sina Microsoft Partner Network (MPN) ID (PGA/PLA) eller ID för Cloud Solution Provider (CSP) för klient organisation (Microsoft-ID).</span><span class="sxs-lookup"><span data-stu-id="67eb6-107">You can verify whether an indirect reseller has signed the Microsoft Partner Agreement using their Microsoft Partner Network (MPN) ID (PGA/PLA) or Cloud Solution Provider (CSP) tenant ID (Microsoft ID).</span></span> <span data-ttu-id="67eb6-108">Du kan använda någon av dessa identifierare för att kontrol lera signerings statusen för Microsoft partner avtalet med **AgreementStatus** -API: et.</span><span class="sxs-lookup"><span data-stu-id="67eb6-108">You can use one of these identifiers to check the Microsoft Partner Agreement signing status using the **AgreementStatus** API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="67eb6-109">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="67eb6-109">Prerequisites</span></span>

- <span data-ttu-id="67eb6-110">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="67eb6-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="67eb6-111">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="67eb6-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="67eb6-112">MPN-ID (PGA/PLA) eller CSP klient-ID (Microsoft ID) för den indirekta åter försäljaren.</span><span class="sxs-lookup"><span data-stu-id="67eb6-112">The MPN ID (PGA/PLA) or the CSP tenant ID (Microsoft ID) of the indirect reseller.</span></span> <span data-ttu-id="67eb6-113">*Du måste använda någon av dessa två identifierare.*</span><span class="sxs-lookup"><span data-stu-id="67eb6-113">*You must use one of these two identifiers.*</span></span>

## <a name="c"></a><span data-ttu-id="67eb6-114">C\#</span><span class="sxs-lookup"><span data-stu-id="67eb6-114">C\#</span></span>

<span data-ttu-id="67eb6-115">Så här hämtar du en indirekt åter försäljares signatur status för Microsoft partner Agreement:</span><span class="sxs-lookup"><span data-stu-id="67eb6-115">To get the Microsoft Partner Agreement signature status of an indirect reseller:</span></span>

1. <span data-ttu-id="67eb6-116">Använd din **IAggregatePartner. Compliance** -samling för att anropa egenskapen **AgreementSignatureStatus** .</span><span class="sxs-lookup"><span data-stu-id="67eb6-116">Use your **IAggregatePartner.Compliance** collection to call the **AgreementSignatureStatus** property.</span></span>

2. <span data-ttu-id="67eb6-117">Anropa metoden [**Get ()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.get) eller [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.getasync) .</span><span class="sxs-lookup"><span data-stu-id="67eb6-117">Call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.getasync) method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var agreementSignatureStatusByMpnId = partnerOperations.Compliance.AgreementSignatureStatus.Get(mpnId:"Enter MPN Id (PGA/PLA)");

var agreementSignatureStatusByTenantId = partnerOperations.Compliance.AgreementSignatureStatus.Get(tenantId: "Enter Tenant Id");
```

- <span data-ttu-id="67eb6-118">Exempel: **[konsol test app](console-test-app.md)**</span><span class="sxs-lookup"><span data-stu-id="67eb6-118">Sample: **[Console test app](console-test-app.md)**</span></span>
- <span data-ttu-id="67eb6-119">Projekt: **PartnerCenterSDK. FeaturesSamples**</span><span class="sxs-lookup"><span data-stu-id="67eb6-119">Project: **PartnerCenterSDK.FeaturesSamples**</span></span>
- <span data-ttu-id="67eb6-120">Klass: **GetAgreementSignatureStatus.cs**</span><span class="sxs-lookup"><span data-stu-id="67eb6-120">Class: **GetAgreementSignatureStatus.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="67eb6-121">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="67eb6-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="67eb6-122">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="67eb6-122">Request syntax</span></span>

| <span data-ttu-id="67eb6-123">Metod</span><span class="sxs-lookup"><span data-stu-id="67eb6-123">Method</span></span> | <span data-ttu-id="67eb6-124">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="67eb6-124">Request URI</span></span> |
| ------ | ----------- |
| <span data-ttu-id="67eb6-125">**TA**</span><span class="sxs-lookup"><span data-stu-id="67eb6-125">**GET**</span></span> | <span data-ttu-id="67eb6-126">*[{baseURL}](partner-center-rest-urls.md)*/v1/Compliance/{ProgramName}/agreementstatus? mpnId = {mpnId} &tenantId = {tenantId}</span><span class="sxs-lookup"><span data-stu-id="67eb6-126">*[{baseURL}](partner-center-rest-urls.md)*/v1/compliance/{ProgramName}/agreementstatus?mpnId={MpnId}&tenantId={TenantId}</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="67eb6-127">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="67eb6-127">URI parameters</span></span>

<span data-ttu-id="67eb6-128">Du måste ange en av följande två frågeparametrar för att identifiera partnern.</span><span class="sxs-lookup"><span data-stu-id="67eb6-128">You must provide one of the following two query parameters to identify the partner.</span></span> <span data-ttu-id="67eb6-129">Om du inte anger någon av dessa två frågeparametrar visas ett **400-fel (felaktig begäran)** .</span><span class="sxs-lookup"><span data-stu-id="67eb6-129">If you don't provide one of these two query parameters, you will receive a **400 (Bad request)** error.</span></span>

| <span data-ttu-id="67eb6-130">Namn</span><span class="sxs-lookup"><span data-stu-id="67eb6-130">Name</span></span> | <span data-ttu-id="67eb6-131">Typ</span><span class="sxs-lookup"><span data-stu-id="67eb6-131">Type</span></span> | <span data-ttu-id="67eb6-132">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="67eb6-132">Required</span></span> | <span data-ttu-id="67eb6-133">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="67eb6-133">Description</span></span> |
| ---- | ---- | -------- | ----------- |
| <span data-ttu-id="67eb6-134">**MpnId**</span><span class="sxs-lookup"><span data-stu-id="67eb6-134">**MpnId**</span></span> | <span data-ttu-id="67eb6-135">int</span><span class="sxs-lookup"><span data-stu-id="67eb6-135">int</span></span> | <span data-ttu-id="67eb6-136">No</span><span class="sxs-lookup"><span data-stu-id="67eb6-136">No</span></span> | <span data-ttu-id="67eb6-137">Ett Microsoft Partner Network-ID (PGA/PLA) som identifierar den indirekta åter försäljaren.</span><span class="sxs-lookup"><span data-stu-id="67eb6-137">A Microsoft Partner Network ID (PGA/PLA) that identifies the indirect reseller.</span></span> |
| <span data-ttu-id="67eb6-138">**TenantId**</span><span class="sxs-lookup"><span data-stu-id="67eb6-138">**TenantId**</span></span> | <span data-ttu-id="67eb6-139">GUID</span><span class="sxs-lookup"><span data-stu-id="67eb6-139">GUID</span></span> | <span data-ttu-id="67eb6-140">No</span><span class="sxs-lookup"><span data-stu-id="67eb6-140">No</span></span> | <span data-ttu-id="67eb6-141">Ett Microsoft-ID som identifierar CSP-kontot för den indirekta åter försäljaren.</span><span class="sxs-lookup"><span data-stu-id="67eb6-141">A Microsoft ID that identifies the CSP account of the indirect reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="67eb6-142">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="67eb6-142">Request headers</span></span>

<span data-ttu-id="67eb6-143">Mer information finns i [partner Center rest](headers.md).</span><span class="sxs-lookup"><span data-stu-id="67eb6-143">For more information, see [Partner Center REST](headers.md).</span></span>

### <a name="request-examples"></a><span data-ttu-id="67eb6-144">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="67eb6-144">Request examples</span></span>

#### <a name="request-using-mpn-id-pgapla"></a><span data-ttu-id="67eb6-145">Begäran med MPN-ID (PGA/PLA)</span><span class="sxs-lookup"><span data-stu-id="67eb6-145">Request using MPN ID (PGA/PLA)</span></span>

<span data-ttu-id="67eb6-146">Följande exempel förfrågan hämtar signerings statusen för den indirekta åter försäljaren från den indirekta åter försäljaren Microsoft Partner Network-ID.</span><span class="sxs-lookup"><span data-stu-id="67eb6-146">The following example request gets the indirect reseller's Microsoft Partner Agreement signing status using the indirect reseller's Microsoft Partner Network ID.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?mpnid=1234567 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

#### <a name="request-using-csp-tenant-id"></a><span data-ttu-id="67eb6-147">Begäran med CSP-klient-ID</span><span class="sxs-lookup"><span data-stu-id="67eb6-147">Request using CSP tenant ID</span></span>

<span data-ttu-id="67eb6-148">I följande exempel förfrågan hämtas signerings statusen för den indirekta åter försäljaren från den indirekta åter försäljarens CSP-ID (Microsoft ID).</span><span class="sxs-lookup"><span data-stu-id="67eb6-148">The following example request gets the indirect reseller's Microsoft Partner Agreement signing status using the indirect reseller's CSP tenant ID (Microsoft ID).</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?tenantId=a2898e3a-06ca-454e-a0d0-c73b0ee36bba HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="67eb6-149">REST-svar</span><span class="sxs-lookup"><span data-stu-id="67eb6-149">REST response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="67eb6-150">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="67eb6-150">Response success and error codes</span></span>

<span data-ttu-id="67eb6-151">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="67eb6-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="67eb6-152">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="67eb6-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="67eb6-153">Fullständig lista finns i REST- [fel i Partner Center](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="67eb6-153">For the full list, see [Partner Center REST error](error-codes.md).</span></span>

### <a name="response-example-success"></a><span data-ttu-id="67eb6-154">Svars exempel (lyckades)</span><span class="sxs-lookup"><span data-stu-id="67eb6-154">Response example (success)</span></span>

<span data-ttu-id="67eb6-155">Följande exempel svar visar om den indirekta åter försäljaren har undertecknat Microsofts partner avtal.</span><span class="sxs-lookup"><span data-stu-id="67eb6-155">The following example response successfully returns whether the indirect reseller has signed the Microsoft Partner Agreement.</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 29
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: jn3r+1wpE06nCt/0.0
MS-ServerId: 0000005B
Date: Tue, 15 Oct 2019 12:44:34 GMT
Connection: close
{
    "isAgreementSigned": true
}
```

### <a name="response-examples-failure"></a><span data-ttu-id="67eb6-156">Svars exempel (haveri)</span><span class="sxs-lookup"><span data-stu-id="67eb6-156">Response examples (failure)</span></span>

<span data-ttu-id="67eb6-157">Du kan få svar som liknar följande exempel när det inte går att returnera signerings statusen för den indirekta åter försäljarens Microsoft-partner avtal.</span><span class="sxs-lookup"><span data-stu-id="67eb6-157">You may receive responses similar to the following examples when the signing status of the indirect reseller's Microsoft Partner Agreement can't be returned.</span></span>

#### <a name="non-guid-formatted-csp-tenant-id"></a><span data-ttu-id="67eb6-158">Icke-GUID formaterat CSP-klient-ID</span><span class="sxs-lookup"><span data-stu-id="67eb6-158">Non-GUID formatted CSP tenant ID</span></span>

<span data-ttu-id="67eb6-159">Följande exempel svar returneras när CSP-klient-ID: t som du skickade till API: t inte är ett GUID.</span><span class="sxs-lookup"><span data-stu-id="67eb6-159">The following example response is returned when the CSP tenant ID that you passed to the API isn't a GUID.</span></span>

```http
HTTP/1.1 400 Bad Request
Content-Length: 105
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: rbuZl5lbAkyq8WGK.0
MS-ServerId: 00000055
Date: Wed, 16 Oct 2019 08:55:23 GMT
Connection: close
{
    "code": 2000,
    "description": "Tenant Id must be a GUID.",
    "data": [],
    "source": "PartnerApiServiceControllers"
}
```

#### <a name="non-numeric-mpn-id"></a><span data-ttu-id="67eb6-160">Icke-numeriskt MPN-ID</span><span class="sxs-lookup"><span data-stu-id="67eb6-160">Non-numeric MPN ID</span></span>

<span data-ttu-id="67eb6-161">Följande exempel svar returneras när MPN-ID (PGA/PLA) som du skickade till API: t inte är numeriskt.</span><span class="sxs-lookup"><span data-stu-id="67eb6-161">The following example response is returned when the MPN ID (PGA/PLA) that you passed to the API is non-numeric.</span></span>

```http
HTTP/1.1 400 Bad Request
Content-Length: 103
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: cP5JiS4sv0GJxlJ9.0
MS-ServerId: 0000005B
Date: Wed, 16 Oct 2019 08:58:45 GMT
Connection: close
{
    "code": 2000,
    "description": "MPN Id must be numeric.",
    "data": [],
    "source": "PartnerApiServiceControllers"
}
```

#### <a name="no-mpn-id-or-csp-tenant-id"></a><span data-ttu-id="67eb6-162">Inget MPN-ID eller CSP-ID för klient organisation</span><span class="sxs-lookup"><span data-stu-id="67eb6-162">No MPN ID or CSP tenant ID</span></span>

<span data-ttu-id="67eb6-163">Följande exempel svar returneras när du inte har skickat ett MPN-ID (PGA/PLA) eller CSP klient-ID till API: et.</span><span class="sxs-lookup"><span data-stu-id="67eb6-163">The following example response is returned when you haven't passed an MPN ID (PGA/PLA) or CSP tenant ID to the API.</span></span> <span data-ttu-id="67eb6-164">Du måste skicka en av de två ID-typerna till API: et.</span><span class="sxs-lookup"><span data-stu-id="67eb6-164">You must pass one of the two ID types to the API.</span></span>

```http
HTTP/1.1 400 Bad Request
Content-Length: 114
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: hEV736v4qk6joDMR.0
MS-ServerId: 00000055
Date: Wed, 16 Oct 2019 09:00:30 GMT
Connection: close
{
    "code": 2001,
    "description": "Both MPN Id and Tenant Id cannot be empty.",
    "data": [],
    "source": "ComplianceController"
}
```

#### <a name="both-mpn-id-and-csp-tenant-id-passed"></a><span data-ttu-id="67eb6-165">Både MPN-ID och CSP klient-ID skickades</span><span class="sxs-lookup"><span data-stu-id="67eb6-165">Both MPN ID and CSP tenant ID passed</span></span>

<span data-ttu-id="67eb6-166">Följande exempel svar returneras när du skickar både MPN-ID (PGA/PLA) och CSP-klient-ID till API: et.</span><span class="sxs-lookup"><span data-stu-id="67eb6-166">The following example response is returned when you pass both the MPN ID (PGA/PLA) and CSP tenant ID to the API.</span></span> <span data-ttu-id="67eb6-167">Du måste *bara skicka en* av de två typerna av identifierare till API: et.</span><span class="sxs-lookup"><span data-stu-id="67eb6-167">You must pass *only one* of the two identifier types to the API.</span></span>

```http
HTTP/1.1 400 Bad Request
Content-Length: 119
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: WTsLWK5UlUW9sZjH.0
MS-ServerId: 0000005B
Date: Wed, 16 Oct 2019 09:02:30 GMT
Connection: close
{
    "code": 2000,
    "description": "Both MPN Id and Tenant Id should not be passed.",
    "data": [],
    "source": "ComplianceController"
}
```

#### <a name="csp-indirect-reseller-mpn-id-pgapla-is-either-invalid-or-not-migrated-from-partner-membership-center-to-partner-center"></a><span data-ttu-id="67eb6-168">MPN-ID för CSP indirekt åter försäljare (PGA/PLA) är antingen ogiltigt eller inte migrerat från partner medlemskaps Center till Partner Center</span><span class="sxs-lookup"><span data-stu-id="67eb6-168">CSP Indirect Reseller MPN Id (PGA/PLA) is either invalid or not migrated from Partner Membership Center to Partner Center</span></span>

<span data-ttu-id="67eb6-169">Följande exempel svar returneras när den indirekta åter försäljaren MPN-ID (PGA/PLA) är antingen ogiltig eller inte migreras från partner medlemskaps Center till Partner Center.</span><span class="sxs-lookup"><span data-stu-id="67eb6-169">The following example response is returned when Indirect reseller MPN ID (PGA/PLA) passed is either invalid or it is not migrated from Partner Membership Center to Partner Center.</span></span> [<span data-ttu-id="67eb6-170">Läs mer</span><span class="sxs-lookup"><span data-stu-id="67eb6-170">Learn More</span></span>](https://partner.microsoft.com/resources/detail/migrate-pmc-pc-mpa-guide-pptx)

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2200,
    "description": "MPN Id 123456 is either invalid or not yet migrated to Partner Center. Please advise your reseller to migrate the reseller MPN ID to Partner Center to continue with this order.",
    "data": [
        "https://partner.microsoft.com/en-us/resources/detail/migrate-pmc-pc-mpa-guide-pptx"
    ],
    "source": "PartnerFD"
}
```

#### <a name="csp-indirect-provider-region-and-csp-indirect-reseller-region-does-not-match"></a><span data-ttu-id="67eb6-171">Regionen för den indirekta CSP-providern och den indirekta KRYPTOGRAFIPROVIDERns region stämmer inte överens</span><span class="sxs-lookup"><span data-stu-id="67eb6-171">CSP Indirect Provider region and CSP Indirect Reseller region does not match</span></span>

<span data-ttu-id="67eb6-172">Följande exempel svar returneras när regionen för den indirekta åter försäljaren MPN-ID (PGA/PLA) inte matchar regionen för den indirekta providern.</span><span class="sxs-lookup"><span data-stu-id="67eb6-172">The following example response is returned when region of Indirect reseller MPN ID (PGA/PLA) doesn't match with region of the Indirect Provider.</span></span> <span data-ttu-id="67eb6-173">[Läs mer](/partner-center/regional-authorization-overview) om CSP-regioner.</span><span class="sxs-lookup"><span data-stu-id="67eb6-173">[Learn more](/partner-center/regional-authorization-overview) about CSP Regions.</span></span>

```http
HTTP/1.1 400 Bad Request
Content-Length: 119
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: WTsLWK5UlUW9sZjH.0
MS-ServerId: 0000005B
Date: Wed, 16 Oct 2019 09:02:30 GMT
Connection: close
{
    "code": 2201,
    "description": "The CSP region of the MPN ID 1234567 doesn’t match the CSP region from where you are placing the order. Provide the MPN ID for the CSP region where you are placing the order.",
    "data": [
        "https://docs.microsoft.com/en-us/partner-center/regional-authorization-overview" 
    ],
    "source": "PartnerFD"
}
```

#### <a name="csp-indirect-reseller-account-exists-in-partner-center-but-hasnt-signed-the-mpa"></a><span data-ttu-id="67eb6-174">Ett indirekt åter försäljar konto för CSP finns i Partner Center men har inte signerat MPA</span><span class="sxs-lookup"><span data-stu-id="67eb6-174">CSP Indirect Reseller account exists in Partner Center but hasn't signed the MPA</span></span>

<span data-ttu-id="67eb6-175">Följande exempel svar returneras när CSP-indirekt åter försäljarens konto i Partner Center inte har signerat MPA.</span><span class="sxs-lookup"><span data-stu-id="67eb6-175">The following example response is returned when CSP Indirect Reseller account in Partner Center hasn't signed the MPA.</span></span> [<span data-ttu-id="67eb6-176">Läs mer</span><span class="sxs-lookup"><span data-stu-id="67eb6-176">Learn More</span></span>](https://partner.microsoft.com/resources/detail/verify-mpa-acceptance-status-pptx)

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2203,
    "description": "MPN Id 123456 has not signed Microsoft Partner Agreement (MPA) for the CSP region where the order is being placed. Please advise your reseller to sign MPA to continue with the order.",
    "data": [
        "https://partner.microsoft.com/en-gb/resources/detail/verify-mpa-acceptance-status-pptx"
    ],
    "source": "PartnerFD"
}
```

#### <a name="no-csp-indirect-reseller-account-is-associated-with-the-given-mpn-id"></a><span data-ttu-id="67eb6-177">Inget indirekt åter försäljar konto för CSP är associerat med angivet MPN-ID</span><span class="sxs-lookup"><span data-stu-id="67eb6-177">No CSP Indirect Reseller account is associated with the given MPN ID</span></span>

<span data-ttu-id="67eb6-178">Följande exempel svar returneras när Partner Center kan identifiera MPN-ID (PGA/PLA) som skickades i begäran, men det finns ingen CSP-registrering kopplad till angivet MPN-ID (PGA/PLA).</span><span class="sxs-lookup"><span data-stu-id="67eb6-178">The following example response is returned when Partner Center can recognize the MPN ID (PGA/PLA) passed in the request but there is no CSP enrollment associated to the given MPN ID (PGA/PLA).</span></span> [<span data-ttu-id="67eb6-179">Läs mer</span><span class="sxs-lookup"><span data-stu-id="67eb6-179">Learn More</span></span>](https://partner.microsoft.com/resources/detail/onboard-pc-csp-mpn-mpa-guide-pptx)

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2204,
    "description": "MPN Id 123456 is not associated with a CSP Indirect Reseller account in Partner Center. Please advise your reseller to enroll into the CSP program as an indirect reseller in Partner Center.",
    "data": [
        "https://partner.microsoft.com/en-us/resources/detail/onboard-pc-csp-mpn-mpa-guide-pptx"
    ],
    "source": "PartnerFD"
}
```

#### <a name="invalid-tenant-id"></a><span data-ttu-id="67eb6-180">Ogiltigt klient-ID</span><span class="sxs-lookup"><span data-stu-id="67eb6-180">Invalid Tenant ID</span></span>

<span data-ttu-id="67eb6-181">Följande exempel svar returneras när ett partner Center inte hittar något konto kopplat till klient-ID: t som skickas i begäran.</span><span class="sxs-lookup"><span data-stu-id="67eb6-181">The following example response is returned when Partner Center doesn't find any account associated to the Tenant ID passed in the request.</span></span>

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2205,
    "description": "Partner Center doesn't find any account associated to the Tenant ID 12345678-ACBD-1234-ABCD-123456789ABC",
    "data": [],
    "source": "PartnerFD"
}
```

#### <a name="no-mpa-found-with-the-given-tenant-id"></a><span data-ttu-id="67eb6-182">Ingen MPA hittades med angivet klient-ID</span><span class="sxs-lookup"><span data-stu-id="67eb6-182">No MPA found with the given Tenant ID</span></span>

<span data-ttu-id="67eb6-183">Följande exempel svar returneras när Partner Center inte kan hitta någon MPA-signatur med angivet klient-ID.</span><span class="sxs-lookup"><span data-stu-id="67eb6-183">The following example response is returned when Partner Center can't find any MPA signature with the given Tenant ID.</span></span>

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2206,
    "description": "Parnter Center Account associated to Tenant Id 12345678-ACBD-1234-ABCD-123456789ABC hasn't signed the agreement",
    "data": [],
    "source": "PartnerFD"
}
```
