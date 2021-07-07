---
title: Verifiera en indirekt återförsäljares Microsoft-partneravtal signeringsstatus
description: Du kan använda AGREEMENTStatus-API:et för att kontrollera om en indirekt återförsäljare har signerat Microsoft-partneravtal.
ms.date: 07/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f83acc61624a72354c390905b1250bc021dd39aa
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/05/2021
ms.locfileid: "111529842"
---
# <a name="verify-an-indirect-resellers-microsoft-partner-agreement-signing-status"></a><span data-ttu-id="2147b-103">Verifiera en indirekt återförsäljares Microsoft-partneravtal signeringsstatus</span><span class="sxs-lookup"><span data-stu-id="2147b-103">Verify an indirect reseller's Microsoft Partner Agreement signing status</span></span>

<span data-ttu-id="2147b-104">**Gäller för:** Partner Center-| Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="2147b-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="2147b-105">Du kan kontrollera om en indirekt återförsäljare har signerat Microsoft-partneravtal med sitt Microsoft Partner Network-ID (MPN) ID (PGA/PLA) eller Molnlösningsleverantör-klientorganisations-ID (Microsoft ID).</span><span class="sxs-lookup"><span data-stu-id="2147b-105">You can verify whether an indirect reseller has signed the Microsoft Partner Agreement using their Microsoft Partner Network (MPN) ID (PGA/PLA) or Cloud Solution Provider (CSP) tenant ID (Microsoft ID).</span></span> <span data-ttu-id="2147b-106">Du kan använda någon av dessa identifierare för att kontrollera Microsoft-partneravtal signeringsstatus med hjälp av **AgreementStatus-API:et.**</span><span class="sxs-lookup"><span data-stu-id="2147b-106">You can use one of these identifiers to check the Microsoft Partner Agreement signing status using the **AgreementStatus** API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2147b-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="2147b-107">Prerequisites</span></span>

- <span data-ttu-id="2147b-108">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="2147b-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2147b-109">Det här scenariot har endast stöd för autentisering med app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="2147b-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="2147b-110">MPN-ID (PGA/PLA) eller CSP-klientorganisations-ID (Microsoft ID) för den indirekta återförsäljaren.</span><span class="sxs-lookup"><span data-stu-id="2147b-110">The MPN ID (PGA/PLA) or the CSP tenant ID (Microsoft ID) of the indirect reseller.</span></span> <span data-ttu-id="2147b-111">*Du måste använda någon av dessa två identifierare.*</span><span class="sxs-lookup"><span data-stu-id="2147b-111">*You must use one of these two identifiers.*</span></span>

## <a name="c"></a><span data-ttu-id="2147b-112">C\#</span><span class="sxs-lookup"><span data-stu-id="2147b-112">C\#</span></span>

<span data-ttu-id="2147b-113">Så här hämtar du Microsoft-partneravtal signaturstatus för en indirekt återförsäljare:</span><span class="sxs-lookup"><span data-stu-id="2147b-113">To get the Microsoft Partner Agreement signature status of an indirect reseller:</span></span>

1. <span data-ttu-id="2147b-114">Använd din **IAggregatePartner.Compliance-samling** för att anropa **agreementSignatureStatus-egenskapen.**</span><span class="sxs-lookup"><span data-stu-id="2147b-114">Use your **IAggregatePartner.Compliance** collection to call the **AgreementSignatureStatus** property.</span></span>

2. <span data-ttu-id="2147b-115">Anropa metoden [**Get()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.get) eller [**GetAsync().**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.getasync)</span><span class="sxs-lookup"><span data-stu-id="2147b-115">Call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.getasync) method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var agreementSignatureStatusByMpnId = partnerOperations.Compliance.AgreementSignatureStatus.Get(mpnId:"Enter MPN Id (PGA/PLA)");

var agreementSignatureStatusByTenantId = partnerOperations.Compliance.AgreementSignatureStatus.Get(tenantId: "Enter Tenant Id");
```

- <span data-ttu-id="2147b-116">Exempel: **[Konsoltestapp](console-test-app.md)**</span><span class="sxs-lookup"><span data-stu-id="2147b-116">Sample: **[Console test app](console-test-app.md)**</span></span>
- <span data-ttu-id="2147b-117">Project: **PartnerCenterSDK.FeaturesExempel**</span><span class="sxs-lookup"><span data-stu-id="2147b-117">Project: **PartnerCenterSDK.FeaturesSamples**</span></span>
- <span data-ttu-id="2147b-118">Klass: **GetAgreementSignatureStatus.cs**</span><span class="sxs-lookup"><span data-stu-id="2147b-118">Class: **GetAgreementSignatureStatus.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="2147b-119">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="2147b-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2147b-120">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="2147b-120">Request syntax</span></span>

| <span data-ttu-id="2147b-121">Metod</span><span class="sxs-lookup"><span data-stu-id="2147b-121">Method</span></span> | <span data-ttu-id="2147b-122">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="2147b-122">Request URI</span></span> |
| ------ | ----------- |
| <span data-ttu-id="2147b-123">**Få**</span><span class="sxs-lookup"><span data-stu-id="2147b-123">**GET**</span></span> | <span data-ttu-id="2147b-124">*[{baseURL}](partner-center-rest-urls.md)*/v1/compliance/{ProgramName}/agreementstatus?mpnId={MpnId}&tenantId={TenantId}</span><span class="sxs-lookup"><span data-stu-id="2147b-124">*[{baseURL}](partner-center-rest-urls.md)*/v1/compliance/{ProgramName}/agreementstatus?mpnId={MpnId}&tenantId={TenantId}</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="2147b-125">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="2147b-125">URI parameters</span></span>

<span data-ttu-id="2147b-126">Du måste ange någon av följande två frågeparametrar för att identifiera partnern.</span><span class="sxs-lookup"><span data-stu-id="2147b-126">You must provide one of the following two query parameters to identify the partner.</span></span> <span data-ttu-id="2147b-127">Om du inte anger någon av dessa två frågeparametrar får du ett **400-fel (felaktig** begäran).</span><span class="sxs-lookup"><span data-stu-id="2147b-127">If you don't provide one of these two query parameters, you will receive a **400 (Bad request)** error.</span></span>

| <span data-ttu-id="2147b-128">Namn</span><span class="sxs-lookup"><span data-stu-id="2147b-128">Name</span></span> | <span data-ttu-id="2147b-129">Typ</span><span class="sxs-lookup"><span data-stu-id="2147b-129">Type</span></span> | <span data-ttu-id="2147b-130">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="2147b-130">Required</span></span> | <span data-ttu-id="2147b-131">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="2147b-131">Description</span></span> |
| ---- | ---- | -------- | ----------- |
| <span data-ttu-id="2147b-132">**MpnId**</span><span class="sxs-lookup"><span data-stu-id="2147b-132">**MpnId**</span></span> | <span data-ttu-id="2147b-133">int</span><span class="sxs-lookup"><span data-stu-id="2147b-133">int</span></span> | <span data-ttu-id="2147b-134">Inga</span><span class="sxs-lookup"><span data-stu-id="2147b-134">No</span></span> | <span data-ttu-id="2147b-135">Ett Microsoft Partner Network-ID (PGA/PLA) som identifierar den indirekta återförsäljaren.</span><span class="sxs-lookup"><span data-stu-id="2147b-135">A Microsoft Partner Network ID (PGA/PLA) that identifies the indirect reseller.</span></span> |
| <span data-ttu-id="2147b-136">**TenantId**</span><span class="sxs-lookup"><span data-stu-id="2147b-136">**TenantId**</span></span> | <span data-ttu-id="2147b-137">GUID</span><span class="sxs-lookup"><span data-stu-id="2147b-137">GUID</span></span> | <span data-ttu-id="2147b-138">Inga</span><span class="sxs-lookup"><span data-stu-id="2147b-138">No</span></span> | <span data-ttu-id="2147b-139">Ett Microsoft-ID som identifierar CSP-kontot för den indirekta återförsäljaren.</span><span class="sxs-lookup"><span data-stu-id="2147b-139">A Microsoft ID that identifies the CSP account of the indirect reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="2147b-140">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="2147b-140">Request headers</span></span>

<span data-ttu-id="2147b-141">Mer information finns i [Partner Center REST](headers.md).</span><span class="sxs-lookup"><span data-stu-id="2147b-141">For more information, see [Partner Center REST](headers.md).</span></span>

### <a name="request-examples"></a><span data-ttu-id="2147b-142">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="2147b-142">Request examples</span></span>

#### <a name="request-using-mpn-id-pgapla"></a><span data-ttu-id="2147b-143">Begäran med MPN-ID (PGA/PLA)</span><span class="sxs-lookup"><span data-stu-id="2147b-143">Request using MPN ID (PGA/PLA)</span></span>

<span data-ttu-id="2147b-144">I följande exempelbegäran hämtar den indirekta återförsäljarens Microsoft-partneravtal signeringsstatus med hjälp av den indirekta återförsäljarens Microsoft Partner Network-ID.</span><span class="sxs-lookup"><span data-stu-id="2147b-144">The following example request gets the indirect reseller's Microsoft Partner Agreement signing status using the indirect reseller's Microsoft Partner Network ID.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?mpnid=1234567 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

#### <a name="request-using-csp-tenant-id"></a><span data-ttu-id="2147b-145">Begäran med CSP-klientorganisations-ID</span><span class="sxs-lookup"><span data-stu-id="2147b-145">Request using CSP tenant ID</span></span>

<span data-ttu-id="2147b-146">Följande exempelbegäran hämtar den indirekta återförsäljarens signeringsstatus Microsoft-partneravtal med hjälp av den indirekta återförsäljarens CSP-klientorganisations-ID (Microsoft-ID).</span><span class="sxs-lookup"><span data-stu-id="2147b-146">The following example request gets the indirect reseller's Microsoft Partner Agreement signing status using the indirect reseller's CSP tenant ID (Microsoft ID).</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?tenantId=a2898e3a-06ca-454e-a0d0-c73b0ee36bba HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="2147b-147">REST-svar</span><span class="sxs-lookup"><span data-stu-id="2147b-147">REST response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2147b-148">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="2147b-148">Response success and error codes</span></span>

<span data-ttu-id="2147b-149">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="2147b-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2147b-150">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="2147b-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2147b-151">En fullständig lista finns i [Partner Center REST-fel.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="2147b-151">For the full list, see [Partner Center REST error](error-codes.md).</span></span>

### <a name="response-example-success"></a><span data-ttu-id="2147b-152">Svarsexempel (lyckades)</span><span class="sxs-lookup"><span data-stu-id="2147b-152">Response example (success)</span></span>

<span data-ttu-id="2147b-153">Följande exempelsvar returnerar om den indirekta återförsäljaren har signerat Microsoft-partneravtal.</span><span class="sxs-lookup"><span data-stu-id="2147b-153">The following example response successfully returns whether the indirect reseller has signed the Microsoft Partner Agreement.</span></span>

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

### <a name="response-examples-failure"></a><span data-ttu-id="2147b-154">Svarsexempel (fel)</span><span class="sxs-lookup"><span data-stu-id="2147b-154">Response examples (failure)</span></span>

<span data-ttu-id="2147b-155">Du kan få svar som liknar följande exempel när signeringsstatusen för den indirekta återförsäljarens Microsoft-partneravtal inte kan returneras.</span><span class="sxs-lookup"><span data-stu-id="2147b-155">You may receive responses similar to the following examples when the signing status of the indirect reseller's Microsoft Partner Agreement can't be returned.</span></span>

#### <a name="non-guid-formatted-csp-tenant-id"></a><span data-ttu-id="2147b-156">Icke-GUID-formaterat CSP-klient-ID</span><span class="sxs-lookup"><span data-stu-id="2147b-156">Non-GUID formatted CSP tenant ID</span></span>

<span data-ttu-id="2147b-157">Följande exempelsvar returneras när det CSP-klient-ID som du skickade till API:et inte är ett GUID.</span><span class="sxs-lookup"><span data-stu-id="2147b-157">The following example response is returned when the CSP tenant ID that you passed to the API isn't a GUID.</span></span>

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

#### <a name="non-numeric-mpn-id"></a><span data-ttu-id="2147b-158">Icke-numeriskt MPN-ID</span><span class="sxs-lookup"><span data-stu-id="2147b-158">Non-numeric MPN ID</span></span>

<span data-ttu-id="2147b-159">Följande exempelsvar returneras när det MPN-ID (PGA/PLA) som du skickade till API:et inte är numeriskt.</span><span class="sxs-lookup"><span data-stu-id="2147b-159">The following example response is returned when the MPN ID (PGA/PLA) that you passed to the API is non-numeric.</span></span>

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

#### <a name="no-mpn-id-or-csp-tenant-id"></a><span data-ttu-id="2147b-160">Inget MPN-ID eller CSP-klientorganisations-ID</span><span class="sxs-lookup"><span data-stu-id="2147b-160">No MPN ID or CSP tenant ID</span></span>

<span data-ttu-id="2147b-161">Följande exempelsvar returneras när du inte har godkänt ett MPN-ID (PGA/PLA) eller CSP-klient-ID till API:et.</span><span class="sxs-lookup"><span data-stu-id="2147b-161">The following example response is returned when you haven't passed an MPN ID (PGA/PLA) or CSP tenant ID to the API.</span></span> <span data-ttu-id="2147b-162">Du måste skicka en av de två ID-typerna till API:et.</span><span class="sxs-lookup"><span data-stu-id="2147b-162">You must pass one of the two ID types to the API.</span></span>

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

#### <a name="both-mpn-id-and-csp-tenant-id-passed"></a><span data-ttu-id="2147b-163">Både MPN-ID och CSP-klientorganisations-ID skickades</span><span class="sxs-lookup"><span data-stu-id="2147b-163">Both MPN ID and CSP tenant ID passed</span></span>

<span data-ttu-id="2147b-164">Följande exempelsvar returneras när du skickar både MPN-ID (PGA/PLA) och CSP-klient-ID till API:et.</span><span class="sxs-lookup"><span data-stu-id="2147b-164">The following example response is returned when you pass both the MPN ID (PGA/PLA) and CSP tenant ID to the API.</span></span> <span data-ttu-id="2147b-165">Du får bara *skicka en av* de två identifierartyperna till API:et.</span><span class="sxs-lookup"><span data-stu-id="2147b-165">You must pass *only one* of the two identifier types to the API.</span></span>

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

#### <a name="csp-indirect-reseller-mpn-id-pgapla-is-either-invalid-or-not-migrated-from-partner-membership-center-to-partner-center"></a><span data-ttu-id="2147b-166">CSP Indirect Reseller MPN ID (PGA/PLA) är ogiltigt eller migreras inte från Partner Membership Center till Partnercenter</span><span class="sxs-lookup"><span data-stu-id="2147b-166">CSP Indirect Reseller MPN ID (PGA/PLA) is either invalid or not migrated from Partner Membership Center to Partner Center</span></span>

<span data-ttu-id="2147b-167">Följande exempelsvar returneras när en indirekt återförsäljares MPN-ID (PGA/PLA) skickas är antingen ogiltigt eller inte migreras från Partner Membership Center till PartnerCenter.</span><span class="sxs-lookup"><span data-stu-id="2147b-167">The following example response is returned when Indirect reseller MPN ID (PGA/PLA) passed is either invalid or it is not migrated from Partner Membership Center to Partner Center.</span></span> [<span data-ttu-id="2147b-168">Läs mer</span><span class="sxs-lookup"><span data-stu-id="2147b-168">Learn More</span></span>](https://partner.microsoft.com/resources/detail/migrate-pmc-pc-mpa-guide-pptx)

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
        "https://partner.microsoft.com/resources/detail/migrate-pmc-pc-mpa-guide-pptx"
    ],
    "source": "PartnerFD"
}
```

#### <a name="csp-indirect-provider-region-and-csp-indirect-reseller-region-does-not-match"></a><span data-ttu-id="2147b-169">CSP Indirect Provider och CSP Indirect Reseller region matchar inte</span><span class="sxs-lookup"><span data-stu-id="2147b-169">CSP Indirect Provider region and CSP Indirect Reseller region does not match</span></span>

<span data-ttu-id="2147b-170">Följande exempelsvar returneras när regionen för indirekt återförsäljares MPN-ID (PGA/PLA) inte matchar regionen för den indirekta leverantören.</span><span class="sxs-lookup"><span data-stu-id="2147b-170">The following example response is returned when region of Indirect reseller MPN ID (PGA/PLA) doesn't match with region of the Indirect Provider.</span></span> <span data-ttu-id="2147b-171">[Läs mer om](/partner-center/mpa-indirect-provider-faq) CSP-regioner.</span><span class="sxs-lookup"><span data-stu-id="2147b-171">[Learn more](/partner-center/mpa-indirect-provider-faq) about CSP Regions.</span></span>

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
        "https://docs.microsoft.com/partner-center/mpa-indirect-provider-faq" 
    ],
    "source": "PartnerFD"
}
```

#### <a name="csp-indirect-reseller-account-exists-in-partner-center-but-hasnt-signed-the-mpa"></a><span data-ttu-id="2147b-172">CSP Indirect Reseller konto finns i Partnercenter men har inte signerat MPA</span><span class="sxs-lookup"><span data-stu-id="2147b-172">CSP Indirect Reseller account exists in Partner Center but hasn't signed the MPA</span></span>

<span data-ttu-id="2147b-173">Följande exempelsvar returneras när CSP Indirect Reseller i Partnercenter inte har signerat MPA.</span><span class="sxs-lookup"><span data-stu-id="2147b-173">The following example response is returned when CSP Indirect Reseller account in Partner Center hasn't signed the MPA.</span></span> [<span data-ttu-id="2147b-174">Läs mer</span><span class="sxs-lookup"><span data-stu-id="2147b-174">Learn More</span></span>](/partner-center/mpa-indirect-provider-faq)

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
        "https://docs.microsoft.com/partner-center/mpa-indirect-provider-faq"
    ],
    "source": "PartnerFD"
}
```

#### <a name="no-csp-indirect-reseller-account-is-associated-with-the-given-mpn-id"></a><span data-ttu-id="2147b-175">Inget CSP Indirect Reseller konto är associerat med det angivna MPN-ID:t</span><span class="sxs-lookup"><span data-stu-id="2147b-175">No CSP Indirect Reseller account is associated with the given MPN ID</span></span>

<span data-ttu-id="2147b-176">Följande exempelsvar returneras när Partner Center kan identifiera det MPN-ID (PGA/PLA) som skickades i begäran, men det inte finns någon CSP-registrering kopplad till det angivna MPN-ID:t (PGA/PLA).</span><span class="sxs-lookup"><span data-stu-id="2147b-176">The following example response is returned when Partner Center can recognize the MPN ID (PGA/PLA) passed in the request but there is no CSP enrollment associated to the given MPN ID (PGA/PLA).</span></span> [<span data-ttu-id="2147b-177">Läs mer</span><span class="sxs-lookup"><span data-stu-id="2147b-177">Learn More</span></span>](/partner-center/mpa-indirect-provider-faq)

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
        "https://docs.microsoft.com/partner-center/mpa-indirect-provider-faq"
    ],
    "source": "PartnerFD"
}
```

#### <a name="invalid-tenant-id"></a><span data-ttu-id="2147b-178">Ogiltigt klientorganisations-ID</span><span class="sxs-lookup"><span data-stu-id="2147b-178">Invalid Tenant ID</span></span>

<span data-ttu-id="2147b-179">Följande exempelsvar returneras när Partnercenter inte hittar något konto som är kopplat till det klient-ID som skickades i begäran.</span><span class="sxs-lookup"><span data-stu-id="2147b-179">The following example response is returned when Partner Center doesn't find any account associated to the Tenant ID passed in the request.</span></span>

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

#### <a name="no-mpa-found-with-the-given-tenant-id"></a><span data-ttu-id="2147b-180">Inget MPA hittades med det angivna klientorganisations-ID:t</span><span class="sxs-lookup"><span data-stu-id="2147b-180">No MPA found with the given Tenant ID</span></span>

<span data-ttu-id="2147b-181">Följande exempelsvar returneras när Partnercenter inte kan hitta någon MPA-signatur med det angivna klientorganisations-ID:t.</span><span class="sxs-lookup"><span data-stu-id="2147b-181">The following example response is returned when Partner Center can't find any MPA signature with the given Tenant ID.</span></span> [<span data-ttu-id="2147b-182">Läs mer</span><span class="sxs-lookup"><span data-stu-id="2147b-182">Learn More</span></span>](/partner-center/mpa-indirect-provider-faq)

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
    "data": [
        "https://docs.microsoft.com/partner-center/mpa-indirect-provider-faq"
    ],
    "source": "PartnerFD"
}
```