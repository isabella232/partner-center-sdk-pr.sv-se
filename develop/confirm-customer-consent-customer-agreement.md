---
title: Bekräfta kundgodkännande av Microsoft-kundavtal
description: Lär dig hur du bekräftar kundens godkännande av Microsoft-kundavtal partnercenter-API:er.
ms.date: 02/08/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 374a9670f5d4c05209e5cec07afe766bcf57f255f9266138b7aaf0e85f90f0ed
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991930"
---
# <a name="confirm-customer-acceptance-of-the-microsoft-customer-agreement-using-partner-center-apis"></a>Bekräfta kundens godkännande av Microsoft-kundavtal partnercenter-API:er

**Gäller för:** Partnercenter

**Gäller inte för:** Partner Center som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Partnercenter stöder för närvarande endast bekräftelse av kundens godkännande Microsoft-kundavtal i Microsofts offentliga moln.

Den här artikeln beskriver hur du bekräftar eller bekräftar kundens godkännande av Microsoft-kundavtal.

## <a name="prerequisites"></a>Förutsättningar

- Om du använder Partner Center .NET SDK krävs version 1.14 eller senare.

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](./partner-center-authentication.md). *Det här scenariot stöder endast app- och användarautentisering.*

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard) Välj **CSP** på Menyn i Partnercenter följt av **Kunder**. Välj kunden i kundlistan och välj sedan **Konto.** På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.** Microsoft-ID:t är samma som kund-ID :t ( `customer-tenant-id` ).

- Datumet (**dateAgreed**) när kunden godkände Microsoft-kundavtal.

- Information om användaren från kundorganisationen som godkände Microsoft-kundavtal. Du måste bland annat:
  - Förnamn
  - Efternamn
  - E-postadress
  - Telefon (valfritt)
- Om följande värden ändras för en kund tillåter Partnercenter att ett annat avtal skapas för kunden: Förnamn Efternamn E-postadress Telefon-nummer Annars får partner följande felkod på grund av att en dubblett av kunden skapas


```
{
"code": 600061,
"message": "A partner confirmed agreement already exists for the customer.",
"description": "A partner confirmed agreement already exists for the customer.",
"errorName": "PartnerConfirmedAgreementAlreadyExists",
"isRetryable": false,
"parameters": {},
"errorMessageExtended": "InternalErrorCode=600061"
}
 ```

## <a name="net"></a>.NET

Bekräfta eller bekräfta kundens godkännande av Microsoft-kundavtal:

1. Hämta avtalets metadata för Microsoft-kundavtal. Du måste hämta **templateId för** Microsoft-kundavtal. Mer information finns i Hämta [avtalsmetadata för Microsoft-kundavtal](get-customer-agreement-metadata.md).

   ```csharp
   // IAggregatePartner partnerOperations;

   string agreementType = "MicrosoftCustomerAgreement";

   var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
   ```

2. Skapa ett nytt **avtalsobjekt** som innehåller information om bekräftelsen.

3. Använd **samlingen IAgreggatePartner.Customers** och anropa **ById-metoden** med det angivna **kundklient-ID:t**.

4. Använd egenskapen **Avtal** följt av att anropa **Create** eller **CreateAsync**.

   ```csharp
   // string selectedCustomerId;

   var agreementToCreate = new Agreement
   {
       DateAgreed = DateTime.UtcNow,
       TemplateId = microsoftCustomerAgreementDetails.TemplateId,
       PrimaryContact = new Contact
       {
           FirstName = "Tania",
           LastName = "Carr",
           Email = "someone@example.com",
           PhoneNumber = "1234567890"
       }
   };

   Agreement agreement = partnerOperations.Customers.ById(selectedCustomerId).Agreements.Create(agreementToCreate);
   ```

Ett fullständigt exempel finns i klassen [CreateCustomerAgreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) från [konsoltestappsprojektet.](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)

## <a name="rest-request"></a>REST-begäran

Bekräfta eller bekräfta kundens godkännande av Microsoft-kundavtal:

1. Hämta avtalets metadata för Microsoft-kundavtal. Du måste hämta **templateId för** Microsoft-kundavtal. Mer information finns i Hämta [avtalsmetadata för Microsoft-kundavtal](get-customer-agreement-metadata.md).

2. Skapa en ny [ **avtalsresurs**](agreement-resources.md) för att bekräfta att en kund har godkänt Microsoft-kundavtal. Använd följande [REST-begärandesyntax](#request-syntax).

### <a name="request-syntax"></a>Begärandesyntax

| Metod | URI för förfrågan                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| POST   | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1 |

#### <a name="uri-parameter"></a>URI-parameter

Använd följande frågeparameter för att ange den kund som du bekräftar.

| Namn               | Typ | Obligatorisk | Beskrivning                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| kund-klient-id | GUID | Yes | Värdet är ett GUID-formaterat **kundklientorganisations-ID,** vilket är en identifierare som gör att du kan ange en kund. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

I den här tabellen beskrivs de nödvändiga egenskaperna i REST-begärandetexten.

| Namn      | Typ   | Description                                                                                  |
|-----------|--------|----------------------------------------------------------------------------------------------|
| Avtal | objekt | Information som tillhandahålls av partnern för att bekräfta kundens godkännande av Microsoft-kundavtal. |

#### <a name="agreement"></a>Avtal

I den här tabellen beskrivs de minsta obligatoriska fälten för att skapa en [ **avtalsresurs.**](agreement-resources.md)

| Egenskap       | Typ   | Description                              |
|----------------|--------|------------------------------------------|
| primaryContact | [Kontakt](./utility-resources.md#contact) | Information om användaren från kundorganisationen som godkände Microsoft-kundavtal, inklusive:  **firstName,** **lastName,** **email** och **phoneNumber** (valfritt) |
| dateAgreed     | sträng i UTC-datum/tid-format |Det datum då kunden godkände avtalet. |
| templateId     | sträng | Unik identifierare för den avtalstyp som accepteras av kunden. Du kan hämta **templateId för** Microsoft-kundavtal genom att hämta avtalets metadata för Microsoft-kundavtal. Mer [information finns i Hämta avtalsmetadata Microsoft-kundavtal](./get-customer-agreement-metadata.md) information. |
| typ           | sträng | Avtalstyp som accepteras av kunden. Använd "MicrosoftCustomerAgreement" om kunden har godkänt Microsoft-kundavtal. |

#### <a name="request-example"></a>Exempel på begäran

```http
POST https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements HTTP/1.1
Authorization: Bearer <token>
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "primaryContact": {
        "firstName": "Tania",
        "lastName": "Carr",
        "email": "someone@example.com",
        "phoneNumber": "1234567890"
    },
    "templateId": "117a77b0-9360-443b-8795-c6dedc750cf9",
    "dateAgreed": "2018-06-14T00:00:00.000Z",
    "type": "MicrosoftCustomerAgreement"
}
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden en [ **avtalsresurs**](./agreement-resources.md).

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.

Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)

#### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 201 Created
Content-Length: 261
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "userId": "3d6f2c09-eb40-48ca-a4b3-d24c9c007531",
    "primaryContact": {
        "firstName": "Tania",
        "lastName": "Carr",
        "email": "someone@example.com",
        "phoneNumber": "1234567890"
    },
    "templateId": "117a77b0-9360-443b-8795-c6dedc750cf9",
    "dateAgreed": "2018-06-14T00:00:00.000Z",
    "type": "MicrosoftCustomerAgreement"
}
```
