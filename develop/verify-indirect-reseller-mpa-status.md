---
title: Verifiera en indirekt återförsäljares Microsoft-partneravtal signeringsstatus
description: Du kan använda AGREEMENTStatus-API:et för att kontrollera om en indirekt återförsäljare har signerat Microsoft-partneravtal.
ms.date: 07/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 517c99356a4b623b5b46bc3d33f2355cd569f97326e7d9596cff551329d10da7
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989856"
---
# <a name="verify-an-indirect-resellers-microsoft-partner-agreement-signing-status"></a>Verifiera en indirekt återförsäljares Microsoft-partneravtal signeringsstatus

**Gäller för**: Partner Center-| Partnercenter för Microsoft Cloud for US Government

Du kan kontrollera om en indirekt återförsäljare har signerat Microsoft-partneravtal med sitt Microsoft Partner Network(MPN)-ID (PGA/PLA) eller Molnlösningsleverantör(CSP) klientorganisations-ID (Microsoft ID). Du kan använda någon av dessa identifierare för att kontrollera Microsoft-partneravtal signeringsstatus med hjälp av **AgreementStatus-API:et.**

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med app- och användarautentiseringsuppgifter.

- MPN-ID (PGA/PLA) eller CSP-klientorganisations-ID (Microsoft ID) för den indirekta återförsäljaren. *Du måste använda någon av dessa två identifierare.*

## <a name="c"></a>C\#

Så här hämtar du Microsoft-partneravtal signaturstatus för en indirekt återförsäljare:

1. Använd din **IAggregatePartner.Compliance-samling** för att anropa **egenskapen AgreementSignatureStatus.**

2. Anropa [**metoden Get()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.get) eller [**GetAsync().**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.getasync)

``` csharp
// IAggregatePartner partnerOperations;

var agreementSignatureStatusByMpnId = partnerOperations.Compliance.AgreementSignatureStatus.Get(mpnId:"Enter MPN Id (PGA/PLA)");

var agreementSignatureStatusByTenantId = partnerOperations.Compliance.AgreementSignatureStatus.Get(tenantId: "Enter Tenant Id");
```

- Exempel: **[Konsoltestapp](console-test-app.md)**
- Project: **PartnerCenterSDK.FeaturesExempel**
- Klass: **GetAgreementSignatureStatus.cs**

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod | URI för förfrågan |
| ------ | ----------- |
| **Få** | *[{baseURL}](partner-center-rest-urls.md)*/v1/compliance/{ProgramName}/agreementstatus?mpnId={MpnId}&tenantId={TenantId} |

#### <a name="uri-parameters"></a>URI-parametrar

Du måste ange en av följande två frågeparametrar för att identifiera partnern. Om du inte anger någon av dessa två frågeparametrar får du ett **400-fel (felaktig** begäran).

| Namn | Typ | Obligatorisk | Beskrivning |
| ---- | ---- | -------- | ----------- |
| **MpnId** | int | No | Ett Microsoft Partner Network-ID (PGA/PLA) som identifierar den indirekta återförsäljaren. |
| **TenantId** | GUID | No | Ett Microsoft-ID som identifierar CSP-kontot för den indirekta återförsäljaren. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST](headers.md).

### <a name="request-examples"></a>Begärandeexempel

#### <a name="request-using-mpn-id-pgapla"></a>Begäran med MPN-ID (PGA/PLA)

Följande exempelbegäran hämtar den indirekta återförsäljarens signeringsstatus Microsoft-partneravtal med hjälp av den indirekta återförsäljarens Microsoft Partner Network-ID.

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?mpnid=1234567 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

#### <a name="request-using-csp-tenant-id"></a>Begäran med CSP-klientorganisations-ID

Följande exempelbegäran hämtar den indirekta återförsäljarens signeringsstatus Microsoft-partneravtal med hjälp av den indirekta återförsäljarens CSP-klient-ID (Microsoft-ID).

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

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Partner Center REST error](error-codes.md).

### <a name="response-example-success"></a>Svarsexempel (lyckades)

Följande exempelsvar returnerar om den indirekta återförsäljaren har signerat Microsoft-partneravtal.

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

### <a name="response-examples-failure"></a>Svarsexempel (fel)

Du kan få svar som liknar följande exempel när signeringsstatusen för den indirekta återförsäljarens Microsoft-partneravtal inte kan returneras.

#### <a name="non-guid-formatted-csp-tenant-id"></a>Icke-GUID-formaterat CSP-klient-ID

Följande exempelsvar returneras när det CSP-klient-ID som du skickade till API:et inte är ett GUID.

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

Följande exempelsvar returneras när DET MPN-ID (PGA/PLA) som du skickade till API:et inte är numeriskt.

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

#### <a name="no-mpn-id-or-csp-tenant-id"></a>Inget MPN-ID eller CSP-klientorganisations-ID

Följande exempelsvar returneras när du inte har godkänt ett MPN-ID (PGA/PLA) eller CSP-klient-ID till API:et. Du måste skicka en av de två ID-typerna till API:et.

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

#### <a name="both-mpn-id-and-csp-tenant-id-passed"></a>Både MPN-ID och CSP-klientorganisations-ID har passerat

Följande exempelsvar returneras när du skickar både MPN-ID :t (PGA/PLA) och CSP-klient-ID:t till API:et. Du får bara *skicka en av* de två identifierartyperna till API:et.

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

#### <a name="csp-indirect-reseller-mpn-id-pgapla-is-either-invalid-or-not-migrated-from-partner-membership-center-to-partner-center"></a>CSP Indirect Reseller MPN-ID (PGA/PLA) är ogiltigt eller migreras inte från Partner Membership Center till Partnercenter

Följande exempelsvar returneras när det indirekta återförsäljar-MPN-ID:t (PGA/PLA) skickas är antingen ogiltigt eller om det inte migreras från Partner Membership Center till Partnercenter. [Läs mer](https://partner.microsoft.com/resources/detail/migrate-pmc-pc-mpa-guide-pptx)

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

#### <a name="csp-indirect-provider-region-and-csp-indirect-reseller-region-does-not-match"></a>CSP Indirect Provider och CSP Indirect Reseller region matchar inte

Följande exempelsvar returneras när regionen för INDIREKT återförsäljares MPN ID (PGA/PLA) inte matchar regionen för den indirekta providern. [Läs mer om](/partner-center/mpa-indirect-provider-faq) CSP-regioner.

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

#### <a name="csp-indirect-reseller-account-exists-in-partner-center-but-hasnt-signed-the-mpa"></a>CSP Indirect Reseller konto finns i Partnercenter men har inte signerat MPA

Följande exempelsvar returneras när CSP Indirect Reseller i Partnercenter inte har signerat MPA. [Läs mer](/partner-center/mpa-indirect-provider-faq)

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

#### <a name="no-csp-indirect-reseller-account-is-associated-with-the-given-mpn-id"></a>Inget CSP Indirect Reseller konto är associerat med det angivna MPN-ID:t

Följande exempelsvar returneras när Partner Center kan identifiera det MPN-ID (PGA/PLA) som skickades i begäran, men det inte finns någon CSP-registrering kopplad till det angivna MPN-ID:t (PGA/PLA). [Läs mer](/partner-center/mpa-indirect-provider-faq)

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

#### <a name="invalid-tenant-id"></a>Ogiltigt klientorganisations-ID

Följande exempelsvar returneras när Partnercenter inte hittar något konto som är associerat med det klientorganisations-ID som skickades i begäran.

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

#### <a name="no-mpa-found-with-the-given-tenant-id"></a>Inget MPA hittades med det angivna klientorganisations-ID:t

Följande exempelsvar returneras när Partnercenter inte kan hitta någon MPA-signatur med det angivna klientorganisations-ID:t. [Läs mer](/partner-center/mpa-indirect-provider-faq)

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