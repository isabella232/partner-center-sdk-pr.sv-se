---
title: Hämta avtalsmetadata för Microsoft-kundavtalet
description: Den här artikeln förklarar hur du hämtar avtalsmetadata för Microsoft-kundavtal.
ms.date: 8/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khakiali
ms.author: alikhaki
ms.openlocfilehash: 5c20b317edf16b159050884070683880cf7e45bb
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025732"
---
# <a name="get-agreement-metadata-for-the-microsoft-customer-agreement"></a>Hämta avtalsmetadata för Microsoft-kundavtalet

**Gäller för:** Partnercenter

**Gäller inte för**: Partner Center som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Avtalsmetadata för Microsoft-kundavtal stöds för närvarande endast av PartnerCenter i det offentliga Microsoft-molnet.

Du måste hämta avtalets metadata för Microsoft-kundavtal innan du kan:

- [Bekräfta en kunds godkännande av Microsoft-kundavtal](./confirm-customer-consent-customer-agreement.md)
- [Hämta en nedladdningslänk för Microsoft-kundavtal mallen](./download-customer-agreement-template.md)

## <a name="prerequisites"></a>Förutsättningar

- Om du använder Partner Center .NET SDK krävs version 1.14 eller senare.

- Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](./partner-center-authentication.md) Det här scenariot stöder endast app- och användarautentisering.

## <a name="net-version-114-or-newer"></a>.NET (version 1.14 eller senare)

Så här hämtar du avtalsmetadata för Microsoft-kundavtal:

1. Hämta först **samlingen IAggregatePartner.AgreementDetails.**

2. Anropa **metoden ByAgreementType** för att filtrera samlingen till Microsoft-kundavtal.

3. Anropa slutligen **metoden Get** eller **GetAsync.**

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCustomerAgreement";

var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

Ett fullständigt exempel finns i klassen [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) från [konsoltestappsprojektet.](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)

## <a name="rest-request"></a>REST-begäran

Så här hämtar du avtalsmetadata för Microsoft-kundavtal:

1. Skapa en REST-begäran för att hämta [AgreementMetaData-samlingen.](./agreement-metadata-resources.md)

2. Använd **frågeparametern agreementType** för att begränsa resultatet till endast Microsoft-kundavtal.

### <a name="request-syntax"></a>Begärandesyntax

| Metod | URI för förfrågan                                                         |
|--------|---------------------------------------------------------------------|
| GET    | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/agreements?agreementType={agreement-type} HTTP/1.1 |

#### <a name="uri-parameters"></a>URI-parametrar

| Namn                   | Typ     | Obligatorisk | Beskrivning                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| avtalstyp | sträng | No | Använd den här parametern för att begränsa frågesvaret till specifik avtalstyp. Värdena som stöds är: <br/><br/>**MicrosoftCloudAgreement** som endast innehåller avtalsmetadata av typen *MicrosoftCloudAgreement*<br/><br/>**MicrosoftCustomerAgreement** som endast innehåller avtalsmetadata av typen *MicrosoftCustomerAgreement*.<br/><br/>**\**_ som returnerar alla avtalsmetadata. (Använd inte _* \* _ såvida inte din kod har den nödvändiga körningslogiken för att hantera okända avtalstyper eftersom Microsoft kan införa avtalsmetadata med nya avtalstyper när *som helst.) <br/> <br/> _* Obs!** Om URI-parametern inte anges används **MicrosoftCloudAgreement** som standard för bakåtkompatibilitet.  |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/v1/agreements?agreementType=MicrosoftCustomerAgreement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden en samling [ **AgreementMetaData-resurser**](./agreement-metadata-resources.md) i svarstexten.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.

Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Length: 620
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "totalCount": 1,
    "items": [
        {
            "templateId": "117a77b0-9360-443b-8795-c6dedc750cf9",
            "agreementType": "MicrosoftCustomerAgreement",
            "agreementLink": "https://aka.ms/customeragreement",
            "versionRank": 0
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
