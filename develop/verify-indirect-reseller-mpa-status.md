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
# <a name="verify-an-indirect-resellers-microsoft-partner-agreement-signing-status"></a>Verifiera en indirekt åter försäljares signerings status för Microsoft partner Agreement

**Gäller för:**

- Partnercenter
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Du kan kontrol lera om en indirekt åter försäljare har undertecknat Microsoft partner Agreement genom att använda sina Microsoft Partner Network (MPN) ID (PGA/PLA) eller ID för Cloud Solution Provider (CSP) för klient organisation (Microsoft-ID). Du kan använda någon av dessa identifierare för att kontrol lera signerings statusen för Microsoft partner avtalet med **AgreementStatus** -API: et.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.

- MPN-ID (PGA/PLA) eller CSP klient-ID (Microsoft ID) för den indirekta åter försäljaren. *Du måste använda någon av dessa två identifierare.*

## <a name="c"></a>C\#

Så här hämtar du en indirekt åter försäljares signatur status för Microsoft partner Agreement:

1. Använd din **IAggregatePartner. Compliance** -samling för att anropa egenskapen **AgreementSignatureStatus** .

2. Anropa metoden [**Get ()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.get) eller [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.getasync) .

``` csharp
// IAggregatePartner partnerOperations;

var agreementSignatureStatusByMpnId = partnerOperations.Compliance.AgreementSignatureStatus.Get(mpnId:"Enter MPN Id (PGA/PLA)");

var agreementSignatureStatusByTenantId = partnerOperations.Compliance.AgreementSignatureStatus.Get(tenantId: "Enter Tenant Id");
```

- Exempel: **[konsol test app](console-test-app.md)**
- Projekt: **PartnerCenterSDK. FeaturesSamples**
- Klass: **GetAgreementSignatureStatus.cs**

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod | URI för förfrågan |
| ------ | ----------- |
| **TA** | *[{baseURL}](partner-center-rest-urls.md)*/v1/Compliance/{ProgramName}/agreementstatus? mpnId = {mpnId} &tenantId = {tenantId} |

#### <a name="uri-parameters"></a>URI-parametrar

Du måste ange en av följande två frågeparametrar för att identifiera partnern. Om du inte anger någon av dessa två frågeparametrar visas ett **400-fel (felaktig begäran)** .

| Namn | Typ | Obligatorisk | Beskrivning |
| ---- | ---- | -------- | ----------- |
| **MpnId** | int | No | Ett Microsoft Partner Network-ID (PGA/PLA) som identifierar den indirekta åter försäljaren. |
| **TenantId** | GUID | No | Ett Microsoft-ID som identifierar CSP-kontot för den indirekta åter försäljaren. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest](headers.md).

### <a name="request-examples"></a>Exempel på begäran

#### <a name="request-using-mpn-id-pgapla"></a>Begäran med MPN-ID (PGA/PLA)

Följande exempel förfrågan hämtar signerings statusen för den indirekta åter försäljaren från den indirekta åter försäljaren Microsoft Partner Network-ID.

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?mpnid=1234567 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

#### <a name="request-using-csp-tenant-id"></a>Begäran med CSP-klient-ID

I följande exempel förfrågan hämtas signerings statusen för den indirekta åter försäljaren från den indirekta åter försäljarens CSP-ID (Microsoft ID).

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?tenantId=a2898e3a-06ca-454e-a0d0-c73b0ee36bba HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST-svar

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. Fullständig lista finns i REST- [fel i Partner Center](error-codes.md).

### <a name="response-example-success"></a>Svars exempel (lyckades)

Följande exempel svar visar om den indirekta åter försäljaren har undertecknat Microsofts partner avtal.

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

### <a name="response-examples-failure"></a>Svars exempel (haveri)

Du kan få svar som liknar följande exempel när det inte går att returnera signerings statusen för den indirekta åter försäljarens Microsoft-partner avtal.

#### <a name="non-guid-formatted-csp-tenant-id"></a>Icke-GUID formaterat CSP-klient-ID

Följande exempel svar returneras när CSP-klient-ID: t som du skickade till API: t inte är ett GUID.

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

#### <a name="non-numeric-mpn-id"></a>Icke-numeriskt MPN-ID

Följande exempel svar returneras när MPN-ID (PGA/PLA) som du skickade till API: t inte är numeriskt.

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

#### <a name="no-mpn-id-or-csp-tenant-id"></a>Inget MPN-ID eller CSP-ID för klient organisation

Följande exempel svar returneras när du inte har skickat ett MPN-ID (PGA/PLA) eller CSP klient-ID till API: et. Du måste skicka en av de två ID-typerna till API: et.

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

#### <a name="both-mpn-id-and-csp-tenant-id-passed"></a>Både MPN-ID och CSP klient-ID skickades

Följande exempel svar returneras när du skickar både MPN-ID (PGA/PLA) och CSP-klient-ID till API: et. Du måste *bara skicka en* av de två typerna av identifierare till API: et.

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

#### <a name="csp-indirect-reseller-mpn-id-pgapla-is-either-invalid-or-not-migrated-from-partner-membership-center-to-partner-center"></a>MPN-ID för CSP indirekt åter försäljare (PGA/PLA) är antingen ogiltigt eller inte migrerat från partner medlemskaps Center till Partner Center

Följande exempel svar returneras när den indirekta åter försäljaren MPN-ID (PGA/PLA) är antingen ogiltig eller inte migreras från partner medlemskaps Center till Partner Center. [Läs mer](https://partner.microsoft.com/resources/detail/migrate-pmc-pc-mpa-guide-pptx)

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

#### <a name="csp-indirect-provider-region-and-csp-indirect-reseller-region-does-not-match"></a>Regionen för den indirekta CSP-providern och den indirekta KRYPTOGRAFIPROVIDERns region stämmer inte överens

Följande exempel svar returneras när regionen för den indirekta åter försäljaren MPN-ID (PGA/PLA) inte matchar regionen för den indirekta providern. [Läs mer](/partner-center/regional-authorization-overview) om CSP-regioner.

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

#### <a name="csp-indirect-reseller-account-exists-in-partner-center-but-hasnt-signed-the-mpa"></a>Ett indirekt åter försäljar konto för CSP finns i Partner Center men har inte signerat MPA

Följande exempel svar returneras när CSP-indirekt åter försäljarens konto i Partner Center inte har signerat MPA. [Läs mer](https://partner.microsoft.com/resources/detail/verify-mpa-acceptance-status-pptx)

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

#### <a name="no-csp-indirect-reseller-account-is-associated-with-the-given-mpn-id"></a>Inget indirekt åter försäljar konto för CSP är associerat med angivet MPN-ID

Följande exempel svar returneras när Partner Center kan identifiera MPN-ID (PGA/PLA) som skickades i begäran, men det finns ingen CSP-registrering kopplad till angivet MPN-ID (PGA/PLA). [Läs mer](https://partner.microsoft.com/resources/detail/onboard-pc-csp-mpn-mpa-guide-pptx)

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

#### <a name="invalid-tenant-id"></a>Ogiltigt klient-ID

Följande exempel svar returneras när ett partner Center inte hittar något konto kopplat till klient-ID: t som skickas i begäran.

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

#### <a name="no-mpa-found-with-the-given-tenant-id"></a>Ingen MPA hittades med angivet klient-ID

Följande exempel svar returneras när Partner Center inte kan hitta någon MPA-signatur med angivet klient-ID.

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
