---
title: Uppdatera partnerns juridiska företagsprofil
description: Så här uppdaterar du partnerns juridiska affärsprofil.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: parthpandyaMSFT
ms.author: parthp
ms.openlocfilehash: 9be3bf1a5072140cc5f8c1e5b2f9ddaa939d1e682942addcc8d36cec3bf9d494
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997948"
---
# <a name="update-the-partner-legal-business-profile"></a>Uppdatera partnerns juridiska företagsprofil

**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Så här uppdaterar du partnerns juridiska affärsprofil.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med app- och användarautentiseringsuppgifter.

## <a name="c"></a>C\#

Om du vill uppdatera partnerns juridiska affärsprofil instansierar du först **ett LegalBusinessProfile-objekt** och fyller det med den befintliga profilen. Mer information finns i Hämta [partnerns juridiska företagsprofil](get-legal-business-profile.md). Uppdatera sedan de egenskaper som du behöver ändra. I följande kodexempel visas hur du ändrar adressen och de primära kontakttelefonnumren.

Hämta sedan ett gränssnitt till partnerprofilens driftsamling från egenskapen **IAggregatePartner.Profiles.** Hämta sedan värdet för egenskapen **LegalBusinessProfile** för att hämta ett gränssnitt för juridiska affärsprofilåtgärder. Anropa slutligen metoden [**Update**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.update) eller [**UpdateAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.updateasync) med det ändrade objektet för att uppdatera profilen.

``` csharp
// IAggregatePartner partnerOperations;

var legalBusinessProfile = partnerOperations.Profiles.LegalBusinessProfile.Get();

// Change the address and primary contact phone number.
legalBusinessProfile.Address.PhoneNumber = "4255550110";
legalBusinessProfile.PrimaryContact.PhoneNumber = "4255550110";

// Apply changes to the profile.
var updatedLegalBusinessProfile = partnerOperations.Profiles.LegalBusinessProfile.Update(legalBusinessProfile);
```

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod  | URI för förfrågan                                                                    |
|---------|--------------------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/legalbusiness HTTP/1.1 |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

Den juridiska affärsprofilresursen.

### <a name="request-example"></a>Exempel på begäran

```http
PUT https://api.partnercenter.microsoft.com/v1/profiles/legalbusiness HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4549ac0c-0f1d-4d8f-b02f-6d36fadcccee
MS-CorrelationId: aa2a0d8c-7a41-470f-97ae-b82e6c338ee4
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 806
Expect: 100-continue

{
    "CompanyName": "Lucerne Publishing",
    "Address": {
        "Country": "US",
        "Region": null,
        "City": "Redmond",
        "State": "WA",
        "AddressLine1": "123 Main Street",
        "AddressLine2": "",
        "PostalCode": "98052",
        "FirstName": "Gena",
        "LastName": "Soto",
        "PhoneNumber": "4255550110"
    },
    "PrimaryContact": {
        "FirstName": "Gena",
        "LastName": "Soto",
        "Email": "gena@lucernepublishing.com",
        "PhoneNumber": "4255550110"
    },
    "CompanyApproverAddress": {
        "Country": "US",
        "Region": null,
        "City": "Redmond",
        "State": "WA",
        "AddressLine1": "123 Main Street",
        "AddressLine2": "",
        "PostalCode": "98052",
        "FirstName": null,
        "LastName": null,
        "PhoneNumber": null
    },
    "CompanyApproverEmail": "gena@lucernepublishing.com",
    "VettingStatus": "authorized",
    "VettingSubStatus": "none",
    "Links": {
        "Self": {
            "Uri": "/profiles/legalbusiness",
            "Method": "GET",
            "Headers": []
        }
    },
    "Attributes": {
        "ObjectType": "LegalBusinessProfile"
    }
}
```

## <a name="rest-response"></a>REST-svar

Om det lyckas innehåller svarstexten den uppdaterade **LegalBusinessProfile**

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder i Partnercenter.](error-codes.md)

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Length: 1157
Content-Type: application/json; charset=utf-8
MS-CorrelationId: aa2a0d8c-7a41-470f-97ae-b82e6c338ee4
MS-RequestId: 4549ac0c-0f1d-4d8f-b02f-6d36fadcccee
MS-CV: KZLU42qJ4EObO75q.0
MS-ServerId: 030020643
Date: Tue, 21 Mar 2017 22:03:15 GMT

{
    "companyName": "Lucerne Publishing",
    "address": {
        "country": "US",
        "city": "Redmond",
        "state": "WA",
        "addressLine1": "123 Main Street",
        "addressLine2": "",
        "postalCode": "98052",
        "firstName": "Gena",
        "lastName": "Soto",
        "phoneNumber": "4255550110"
    },
    "primaryContact": {
        "firstName": "Gena",
        "lastName": "Soto",
        "email": "gena@lucernepublishing.com",
        "phoneNumber": "4255550110"
    },
    "companyApproverAddress": {
        "country": "US",
        "city": "Redmond",
        "state": "WA",
        "addressLine1": "123 Main Street",
        "addressLine2": "",
        "postalCode": "98052"
    },
    "companyApproverEmail": "gena@lucernepublishing.com",
    "vettingStatus": "authorized",
    "vettingSubStatus": "none",
    "profileType": "LegalBusinessProfile",
    "links": {
        "self": {
            "uri": "/profiles/legalbusiness",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "LegalBusinessProfile"
    }
}
```
