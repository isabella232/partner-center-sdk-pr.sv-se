---
title: Bekräfta kundgodkännande av Microsoft-kundavtal
description: 'Lär dig hur du bekräftar kund godkännande av Microsofts kund avtal med hjälp av API: er för partner Center.'
ms.date: 02/08/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 62a6cebd5d6d093377dd5940dcff6204b7095c70
ms.sourcegitcommit: ebb36208d6e2dea705f62b7d60d471f10c55132e
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/09/2021
ms.locfileid: "100006072"
---
# <a name="confirm-customer-acceptance-of-the-microsoft-customer-agreement-using-partner-center-apis"></a>Bekräfta kund godkännande av Microsofts kund avtal med hjälp av API: er för partner Center

**Gäller för:**

- Partnercenter

Partner Center har för närvarande endast stöd för bekräftelse av kund godkännande av Microsofts kund avtal i *Microsofts offentliga moln*. Den här funktionen gäller för närvarande inte för:

- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

I den här artikeln beskrivs hur du bekräftar eller ombekräftar kund godkännande av Microsofts kund avtal.

## <a name="prerequisites"></a>Förutsättningar

- Om du använder Partner Center .NET SDK krävs version 1,14 eller senare.

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](./partner-center-authentication.md). *Det här scenariot stöder endast app + användarautentisering.*

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).

- Datumet (**dateAgreed**) när kunden har godkänt Microsofts kund avtal.

- Information om användaren från kund organisationen som har godkänt Microsofts kund avtal. Du måste bland annat:
  - Förnamn
  - Efternamn
  - E-postadress
  - Telefonnummer (valfritt)
- Om följande värden ändras för en kund tillåter Partner Center att ett annat avtal skapas för kunden: förnamn efter namn e-postadress telefonnummer i annat fall får följande felkod, på grund av att en dubblett av kund skapas


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

För att bekräfta eller bekräfta kund godkännande av Microsofts kund avtal:

1. Hämta avtals metadata för Microsofts kund avtal. Du måste skaffa **templateId** till Microsofts kund avtal. Mer information finns i [Hämta avtals-metadata för Microsofts kund avtal](get-customer-agreement-metadata.md).

   ```csharp
   // IAggregatePartner partnerOperations;

   string agreementType = "MicrosoftCustomerAgreement";

   var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
   ```

2. Skapa ett nytt **avtals** objekt som innehåller information om bekräftelsen.

3. Använd **IAgreggatePartner. Customers** -samlingen och anropa **ById** -metoden med angivet **kund-ID**.

4. Använd egenskapen **avtal** , följt av anropa **create** eller **CreateAsync**.

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

Ett fullständigt exempel finns i [CreateCustomerAgreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) -klassen från projektets [test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) -projekt.

## <a name="rest-request"></a>REST-begäran

För att bekräfta eller bekräfta kund godkännande av Microsofts kund avtal:

1. Hämta avtals metadata för Microsofts kund avtal. Du måste skaffa **templateId** till Microsofts kund avtal. Mer information finns i [Hämta avtals-metadata för Microsofts kund avtal](get-customer-agreement-metadata.md).

2. Skapa en ny [ **avtals** resurs](agreement-resources.md) för att bekräfta att en kund har godkänt Microsofts kund avtal. Använd följande [syntax för rest-begäran](#request-syntax).

### <a name="request-syntax"></a>Syntax för begäran

| Metod | URI för förfrågan                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| POST   | [*\{ BASEURL \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Agreements http/1.1 |

#### <a name="uri-parameter"></a>URI-parameter

Använd följande frågeparameter för att ange den kund som du bekräftar.

| Namn               | Typ | Obligatorisk | Beskrivning                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| kund-ID för klient organisation | GUID | Ja | Värdet är ett GUID-formaterat **kund-ID**, som är en identifierare som gör att du kan ange en kund. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

I den här tabellen beskrivs de egenskaper som krävs i innehållet i REST-begäran.

| Namn      | Typ   | Description                                                                                  |
|-----------|--------|----------------------------------------------------------------------------------------------|
| Avtal | objekt | Information som tillhandahålls av partnern för att bekräfta kund godkännande av Microsofts kund avtal. |

#### <a name="agreement"></a>Avtal

I den här tabellen beskrivs minimi kraven för de fält som krävs för att skapa en [ **avtals** resurs](agreement-resources.md).

| Egenskap       | Typ   | Description                              |
|----------------|--------|------------------------------------------|
| primaryContact | [Kontakt](./utility-resources.md#contact) | Information om användaren från kund organisationen som har godkänt Microsofts kund avtal, inklusive:  **FirstName**, **LastName**, **e-post** och **telefonnummer** (valfritt) |
| dateAgreed     | sträng i UTC-datum/tid-format |Datumet då kunden godkände avtalet. |
| templateId     | sträng | Unik identifierare för den avtals typ som kunden har accepterat. Du kan hämta **templateId** för Microsofts kund avtal genom att hämta avtals-metadata för Microsofts kund avtal. Mer information finns i [Hämta avtals metadata för Microsofts kund avtal](./get-customer-agreement-metadata.md) . |
| typ           | sträng | Avtals typ som accepteras av kunden. Använd "MicrosoftCustomerAgreement" om kunden har godkänt Microsofts kund avtal. |

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

Om det lyckas returnerar den här metoden en [ **avtals** resurs](./agreement-resources.md).

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.

Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).

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
