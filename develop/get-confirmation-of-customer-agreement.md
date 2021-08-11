---
title: Få bekräftelse på kundgodkännande av Microsoft-kundavtal
description: Den här artikeln förklarar hur du får en bekräftelse på kundens godkännande av Microsoft-kundavtal.
ms.date: 09/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: f5e71f2660c6db638193deec02e9ba4f25a35be6aabdc1c4219f63b1f3295908
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115993511"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-customer-agreement"></a>Få bekräftelse på kundgodkännande av Microsoft-kundavtal

**Gäller för:** Partnercenter

**Gäller inte för:** Partner Center som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

**Avtalsresursen** stöds för närvarande endast av Partnercenter i det offentliga Microsoft-molnet.

Den här artikeln förklarar hur du kan hämta bekräftelser av en kunds godkännande av Microsoft-kundavtal.

## <a name="prerequisites"></a>Förutsättningar

- Om du använder Partner Center .NET SDK krävs version 1.14 eller senare.

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](./partner-center-authentication.md). Det här scenariot stöder endast app- och användarautentisering.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard) Välj **CSP** på Menyn i Partnercenter följt av **Kunder**. Välj kunden i kundlistan och välj sedan **Konto.** På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.** Microsoft-ID:t är samma som kund-ID :t ( `customer-tenant-id` ).

## <a name="net"></a>.NET

Så här hämtar du bekräftelser av kundgodkännande som tidigare har angetts:

- Använd samlingen **IAggregatePartner.Customers och** anropa **ById-metoden** med den angivna kundidentifieraren.

- Hämta egenskapen **Agreements** och filtrera resultaten så att de Microsoft-kundavtal genom att anropa **metoden ByAgreementType.**

- Anropa **Get-** eller **GetAsync-metoden.**

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCustomerAgreement";

var customerAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

Ett komplett exempel finns i klassen [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) från [konsoltestappsprojektet.](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)

## <a name="rest-request"></a>REST-begäran

Så här hämtar du bekräftelse på kundgodkännande som tidigare har angetts:

1. Skapa en REST-begäran för att [hämta samlingen](./agreement-resources.md) Avtal för kunden.

2. Använd **frågeparametern agreementType** för att begränsa resultatet till endast Microsoft-kundavtal.

### <a name="request-syntax"></a>Begärandesyntax

Använd följande begärandesyntax:

| Metod | URI för förfrågan                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements?agreementType={agreement-type} HTTP/1.1 |

#### <a name="uri-parameters"></a>URI-parametrar

Du kan använda följande URI-parametrar med din begäran:

| Namn             | Typ | Obligatorisk | Beskrivning                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| kund-klient-id | GUID | Yes | Värdet är ett GUID-formaterat **CustomerTenantId** som gör att du kan ange en kund. |
| avtalstyp | sträng | No | Den här parametern returnerar alla avtalsmetadata. Använd den här parametern för att begränsa frågesvaret till en specifik avtalstyp. Värdena som stöds är: <br/><br/> **MicrosoftCloudAgreement** som endast innehåller avtalsmetadata av typen *MicrosoftCloudAgreement*.<br/><br/> **MicrosoftCustomerAgreement** som endast innehåller avtalsmetadata av typen *MicrosoftCustomerAgreement*.<br/><br/> **\**_ som returnerar alla avtalsmetadata. (Använd inte _* \* *_ såvida inte koden har den logik som krävs för att hantera oväntade avtalstyper.) <br/> <br/> _* Obs!** Om URI-parametern inte anges får frågan som standard **MicrosoftCloudAgreement** för bakåtkompatibilitet. Microsoft kan när som helst införa avtalsmetadata med nya avtalstyper.  |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

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

Om det lyckas returnerar den här metoden en samling **avtalsresurser** i svarstexten.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.

Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)

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
