---
title: Hämta avtalsmetadata för Microsoft-kundavtalet
description: Den här artikeln förklarar hur du får avtals-metadata för Microsofts kund avtal.
ms.date: 8/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khakiali
ms.author: alikhaki
ms.openlocfilehash: c3ebecc51859c9d2240d319d823f7e555eaecc27
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/14/2020
ms.locfileid: "97769432"
---
# <a name="get-agreement-metadata-for-the-microsoft-customer-agreement"></a>Hämta avtalsmetadata för Microsoft-kundavtalet

**Gäller för:**

- Partnercenter

Avtals-metadata för Microsofts kund avtal stöds för närvarande endast av Partner Center i det *offentliga Microsoft-molnet*. Den gäller inte för:

- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Du måste hämta avtals metadata för Microsofts kund avtal innan du kan:

- [Bekräfta en kunds godkännande av Microsofts kund avtal](./confirm-customer-consent-customer-agreement.md)
- [Hämta en nedladdnings länk för Microsofts kund avtals mall](./download-customer-agreement-template.md)

## <a name="prerequisites"></a>Förutsättningar

- Om du använder Partner Center .NET SDK krävs version 1,14 eller senare.

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](./partner-center-authentication.md). Det här scenariot stöder endast app + User Authentication.

## <a name="net-version-114-or-newer"></a>.NET (version 1,14 eller senare)

Så här hämtar du avtals metadata för Microsofts kund avtal:

1. Börja med att hämta samlingen **IAggregatePartner. AgreementDetails** .

2. Anropa **ByAgreementType** -metoden för att filtrera samlingen till Microsofts kund avtal.

3. Anropa slutligen **Get** -eller **GetAsync** -metoden.

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCustomerAgreement";

var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

Ett fullständigt exempel finns i [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) -klassen från projektets [test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) -projekt.

## <a name="rest-request"></a>REST-begäran

Så här hämtar du avtals metadata för Microsofts kund avtal:

1. Skapa en REST-begäran för att hämta [AgreementMetaData](./agreement-metadata-resources.md) -samlingen.

2. Använd Frågeparametern **agreementType** för att begränsa resultatet till enbart Microsofts kund avtal.

### <a name="request-syntax"></a>Syntax för begäran

| Metod | URI för förfrågan                                                         |
|--------|---------------------------------------------------------------------|
| GET    | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/Agreements? agreementType = {Agreement-Type} http/1.1 |

#### <a name="uri-parameters"></a>URI-parametrar

| Namn                   | Typ     | Obligatorisk | Beskrivning                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| avtals typ | sträng | No | Använd den här parametern om du vill begränsa fråge svaret till en speciell avtals typ. De värden som stöds är: <br/><br/>**MicrosoftCloudAgreement** som endast inkluderar avtals-metadata av typen *MicrosoftCloudAgreement*<br/><br/>**MicrosoftCustomerAgreement** som endast inkluderar avtals-metadata av typen *MicrosoftCustomerAgreement*.<br/><br/>**\*** som returnerar alla avtals-metadata. (Använd inte **\*** om din kod har den nödvändiga körnings logiken för att hantera okända avtals typer eftersom Microsoft kan presentera avtals metadata med nya avtals typer när som helst.)<br/><br/> **Obs:** Om URI-parametern inte anges använder frågan standardvärdet för **MicrosoftCloudAgreement** för bakåtkompatibilitet.  |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

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

Om det lyckas returnerar den här metoden en samling [ **AgreementMetaData** -resurser](./agreement-metadata-resources.md) i svars texten.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.

Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).

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
