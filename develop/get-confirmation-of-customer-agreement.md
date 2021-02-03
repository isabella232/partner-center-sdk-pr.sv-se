---
title: Få bekräftelse på kundgodkännande av Microsoft-kundavtal
description: Den här artikeln förklarar hur du får bekräftelse på kund godkännande av Microsofts kund avtal.
ms.date: 09/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 55f63311e7bb1857fdc6c4b3d68446674542ba98
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/14/2020
ms.locfileid: "97769438"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-customer-agreement"></a>Få bekräftelse på kundgodkännande av Microsoft-kundavtal

**Gäller för:**

- Partnercenter

**Avtals** resursen stöds för närvarande endast av Partner Center i det *offentliga Microsoft-molnet*. Den här resursen gäller inte för:

- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

I den här artikeln förklaras hur du kan hämta bekräftelse (er) av kundens godkännande av Microsofts kund avtal.

## <a name="prerequisites"></a>Förutsättningar

- Om du använder Partner Center .NET SDK krävs version 1,14 eller senare.

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](./partner-center-authentication.md). Det här scenariot stöder endast app + användarautentisering.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).

## <a name="net"></a>.NET

För att hämta bekräftelser för kundgodkännande som tidigare har tillhandahållits:

- Använd **IAggregatePartner. Customers** -samlingen och anropa **ById** -metoden med det angivna kund-ID: n.

- Hämta **avtals** egenskapen och filtrera resultaten till Microsofts kund avtal genom att anropa **ByAgreementType** -metoden.

- Anropa **Get** -eller **GetAsync** -metoden.

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCustomerAgreement";

var customerAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

Ett fullständigt exempel finns i [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) -klassen från projektets [test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) -projekt.

## <a name="rest-request"></a>REST-begäran

Så här hämtar du bekräftelse på kundgodkännande som tidigare har tillhandahållits:

1. Skapa en REST-begäran för att hämta [avtals](./agreement-resources.md) samlingen för kunden.

2. Använd Frågeparametern **agreementType** för att begränsa resultatet till enbart Microsofts kund avtal.

### <a name="request-syntax"></a>Syntax för begäran

Använd följande syntax för begäran:

| Metod | URI för förfrågan                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Agreements? agreementType = {Agreement-Type} http/1.1 |

#### <a name="uri-parameters"></a>URI-parametrar

Du kan använda följande URI-parametrar med din begäran:

| Namn             | Typ | Obligatorisk | Beskrivning                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| kund-ID för klient organisation | GUID | Yes | Värdet är ett GUID-formaterat **CustomerTenantId** som gör att du kan ange en kund. |
| avtals typ | sträng | No | Den här parametern returnerar alla avtals-metadata. Använd den här parametern om du vill begränsa fråge svaret till en speciell avtals typ. De värden som stöds är: <br/><br/> **MicrosoftCloudAgreement** som endast omfattar avtals-metadata av typen *MicrosoftCloudAgreement*.<br/><br/> **MicrosoftCustomerAgreement** som endast omfattar avtals-metadata av typen *MicrosoftCustomerAgreement*.<br/><br/> **\*** som returnerar alla avtals-metadata. (Använd inte **\*** om din kod har den nödvändiga logiken för att hantera oväntade avtals typer.)<br/><br/> **Obs:** Om URI-parametern inte anges använder frågan standardvärdet för **MicrosoftCloudAgreement** för bakåtkompatibilitet. Microsoft kan införa avtals-metadata med nya avtals typer när som helst.  |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements?agreementType=MicrosoftCustomerAgreement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden en samling **avtals** resurser i svars texten.

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
    "totalCount": 2,
    "items":
    [
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@example.com"
                "phoneNumber":"1234567890"
            },
            "templateId":"117a77b0-9360-443b-8795-c6dedc750cf9",
            "dateAgreed":"2019-08-26T00:00:00",
            "type":"MicrosoftCustomerAgreement",
            "agreementLink":"https://aka.ms/customeragreement"
        },
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@example.com"
                "phoneNumber:"1234567890"
            },
            "templateId":"117a77b0-9360-443b-8795-c6dedc750cf9",
            "dateAgreed":"2019-08-27T00:00:00",
            "type":"MicrosoftCustomerAgreement",
            "agreementLink":"https://aka.ms/customeragreement"
        }
    ]
}
```
