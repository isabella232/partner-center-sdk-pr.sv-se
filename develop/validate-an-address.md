---
title: Validera en adress
description: Så här verifierar du en adress med hjälp av API:et för adressverifiering.
ms.date: 05/17/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 30f5cd526ab038dce400e79822d89b8086ba3799
ms.sourcegitcommit: 41bf9dca55f4c96d382b327a75b2d2418edfc9bc
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/13/2021
ms.locfileid: "113655620"
---
# <a name="validate-an-address"></a>Validera en adress

**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Så här verifierar du en adress med hjälp av API:et för adressverifiering.

API:et för adressverifiering bör endast användas för förvalidering av kundprofiluppdateringar. Använd den med förståelsen att om landet är USA, Kanada, Kina eller Mexiko verifieras fältet Delstat mot en lista över giltiga delstater för respektive land. I alla andra länder utförs inte det här testet och API:et kontrollerar bara att tillståndet är en giltig sträng.

## <a name="prerequisites"></a>Förutsättningar

Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.

## <a name="c"></a>C\#

Verifiera en adress genom att först instansiera ett nytt **Address-objekt** och fylla i det med adressen som ska verifieras. Hämta sedan ett gränssnitt till **valideringsåtgärder** från egenskapen **IAggregatePartner.Validations** och anropa **metoden IsAddressValid** med adressobjektet.

```csharp
IAggregatePartner partnerOperations;

// Create an address to validate.
Address address = new Address()
{
    AddressLine1 = "One Microsoft Way",
    City = "Redmond",
    State = "WA",
    PostalCode = "98052",
    Country = "US"
};

// Validate the address.
AddressValidationResponse result = partnerOperations.Validations.IsAddressValid(address);

// If the request completes successfully, you can inspect the response object.

// See the status of the validation.
Console.WriteLine($"Status: {addressValidationResult.Status}");

// See the validation message returned.
Console.WriteLine($"Validation Message Returned: {addressValidationResult.ValidationMessage ?? "No message returned."}");

// See the original address submitted for validation.
Console.WriteLine($"Original Address:\n{this.DisplayAddress(addressValidationResult.OriginalAddress)}");

// See the suggested addresses returned by the API, if any exist.
Console.WriteLine($"Suggested Addresses Returned: {addressValidationResult.SuggestedAddresses?.Count ?? "None."}");

if (addressValidationResult.SuggestedAddresses != null && addressValidationResult.SuggestedAddresses.Any())
{
    addressValidationResult.SuggestedAddresses.ForEach(a => Console.WriteLine(this.DisplayAddress(a)));
}

// Helper method to pretty-print an Address object.
private string DisplayAddress(Address address)
{
    StringBuilder sb = new StringBuilder();

    foreach (var property in address.GetType().GetProperties())
    {
        sb.AppendLine($"{property.Name}: {property.GetValue(address) ?? "None to Display."}");
    }

    return sb.ToString();
}
```

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod   | URI för förfrågan                                                                 |
|----------|-----------------------------------------------------------------------------|
| **Inlägg** | [*{baseURL}*](partner-center-rest-urls.md)/v1/validations/address HTTP/1.1 |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

I den här tabellen beskrivs de nödvändiga egenskaperna i begärandetexten.

| Namn         | Typ   | Obligatorisk | Beskrivning                                                |
|--------------|--------|----------|------------------------------------------------------------|
| addressline1 | sträng | Y        | Den första adressraden.                             |
| addressline2 | sträng | N        | Den andra raden i adressen. Den här egenskapen är valfri. |
| city         | sträng | Y        | Staden.                                                  |
| state        | sträng | Y        | Tillståndet.                                                 |
| Postnummer   | sträng | Y        | Postnumret.                                           |
| land      | sträng | Y        | Landskoden ISO alpha-2 med två tecken.                |

### <a name="response-details"></a>Svarsinformation

Svaret returnerar något av följande statusmeddelanden:

| Status     | Beskrivning |    Antal föreslagna adresser som returneras |
|-------|---------------|-------------------|
|Verifierad leveransbar | Adressen är verifierad och kan skickas till. | Enkel |
|Verifierat | Adressen är verifierad. | Enkel |
|Interaktion krävs | Den föreslagna adressen har ändrats avsevärt och kräver användarbekräftelse. | Enkel |
|Gatuadress delvis | Den angivna gatuadressen är delvis och behöver mer information. | Multipel – högst tre |
|Delvis lokal | De angivna lokalerna (byggnummer, svitnummer och annat) är ofullständiga och behöver mer information. | Multipel – högst tre |
|Flera | Det finns flera fält som är partiella i adressen (inklusive delvis gatuadress och delvis lokal). | Multipel – högst tre |
|Ingen | Adressen är felaktig. | Ingen |
|Inte validerat | Adressen kunde inte skickas via valideringsprocessen. | Ingen |

### <a name="request-example"></a>Exempel på begäran

```http
# "VerifiedShippable" Request Example

POST https://api.partnercenter.microsoft.com/v1/validations/address HTTP/1.1
Accept: application/json
Content-Type: application/json
Authorization: Bearer <token>
MS-CorrelationId: 29624f3c-90cb-4d34-a7e9-bd2de6d35218
MS-RequestId: eb55c2b8-6f4b-4b44-9557-f76df624b8c0
Host: api.partnercenter.microsoft.com
Content-Length: 137
X-Locale: en-US

{
    "AddressLine1": "1 Microsoft Way",
    "City": "Redmond",
    "State": "WA",
    "PostalCode": "98052",
    "Country": "US"
}

# "StreetPartial" Request Example

POST https://api.partnercenter.microsoft.com/v1/validations/address HTTP/1.1
Accept: application/json
Content-Type: application/json
Authorization: Bearer <token>
MS-CorrelationId: 2c95c9bc-fdfb-4c6a-84f4-57c9b0826b43
MS-RequestId: ee6cf74c-3ab5-48d6-9269-4a4b75bd59dc
Host: api.partnercenter.microsoft.com
Content-Length: 135
X-Locale: en-US

{
    "AddressLine1": "Microsoft Way",
    "City": "Redmond",
    "State": "WA",
    "PostalCode": "98052",
    "Country": "US"
}
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar metoden ett **AddressValidationResponse-objekt** i svarstexten med statuskoden **HTTP 200.** Ett exempel på detta visas nedan.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)

### <a name="response-example"></a>Exempel på svar

```http
# "VerifiedShippable" Response Example

HTTP/1.1 200 OK
Date: Mon, 17 May 2021 23:19:19 GMT
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 29624f3c-90cb-4d34-a7e9-bd2de6d35218
MS-RequestId: eb55c2b8-6f4b-4b44-9557-f76df624b8c0
X-Locale: en-US
 
{
    "originalAddress": {
        "country": "US",
        "city": "Redmond",
        "state": "WA",
        "addressLine1": "1 Microsoft Way",
        "postalCode": "98052"
    },
    "suggestedAddresses": [
        {
            "country": "US",
            "city": "Redmond",
            "state": "WA",
            "addressLine1": "1 Microsoft Way",
            "postalCode": "98052-8300"
        }
    ],
    "status": "VerifiedShippable"
}

# "StreetPartial" Response Example

HTTP/1.1 200 OK
Date: Mon, 17 May 2021 23:34:08 GMT
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 2c95c9bc-fdfb-4c6a-84f4-57c9b0826b43
MS-RequestId: ee6cf74c-3ab5-48d6-9269-4a4b75bd59dc
X-Locale: en-US
 
{
    "originalAddress": {
        "country": "US",
        "city": "Redmond",
        "state": "WA",
        "addressLine1": "Microsoft Way",
        "postalCode": "98052"
    },
    "suggestedAddresses": [
        {
            "country": "US",
            "city": "Redmond",
            "state": "WA",
            "addressLine1": "1 Microsoft Way",
            "postalCode": "98052-6399"
        }
    ],
    "status": "StreetPartial",
    "validationMessage": "Address field invalid for property: 'Region', 'PostalCode', 'City'"
}
```
