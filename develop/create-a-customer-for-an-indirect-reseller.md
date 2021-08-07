---
title: Skapa en kund för en indirekt återförsäljare
description: Lär dig hur en indirekt leverantör kan använda Partner Center-API:er för att skapa en kund för en indirekt återförsäljare.
ms.date: 04/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: e54e083dda758cc712c889916676007a389ba69c8009bb3d4907df343a436004
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991743"
---
# <a name="create-a-customer-for-an-indirect-reseller-using-partner-center-apis"></a>Skapa en kund för en indirekt återförsäljare med partnercenter-API:er

En indirekt leverantör kan skapa en kund för en indirekt återförsäljare.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med app- och användarautentiseringsuppgifter.

- Klientorganisations-ID för den indirekta återförsäljaren.

- Den indirekta återförsäljaren måste ha ett samarbete med den indirekta leverantören.

## <a name="c"></a>C\#

Så här lägger du till en ny kund för en indirekt återförsäljare:

1. Skapa en instans av [**ett nytt**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) kundobjekt och skapa en instans av och fyll i [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) [**och CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile). Se till att tilldela det indirekta återförsäljar-ID:t till [**egenskapen AssociatedPartnerID.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer.associatedpartnerid)

2. Använd egenskapen [**IAggregatePartner.Customers för**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) att hämta ett gränssnitt för kundinsamlingsåtgärder.

3. Anropa metoden [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) eller [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) för att skapa kunden.

### <a name="c-example"></a>\#C-exempel

``` csharp
// IAggregatePartner partnerOperations;
// var indirectResellerId;
var customerToCreate = new Customer()
{
    CompanyProfile = new CustomerCompanyProfile()
    {
        Domain = string.Format(CultureInfo.InvariantCulture,
            "WingtipToys{0}.{1}",
            new Random().Next(),
            this.Context.Configuration.Scenario.CustomerDomainSuffix)
    },
    BillingProfile = new CustomerBillingProfile()
    {
        Culture = "EN-US",
        Email = "Gena@wingtiptoys.com",
        Language = "En",
        CompanyName = "Wingtip Toys" + new Random().Next(),
        DefaultAddress = new Address()
        {
            FirstName = "Gena",
            LastName = "Soto",
            AddressLine1 = "One Microsoft Way",
            City = "Redmond",
            State = "WA",
            Country = "US",
            PostalCode = "98052",
            PhoneNumber = "4255550101"
        }
    },
    AssociatedPartnerId = indirectResellerId
};

var newCustomer = partnerOperations.Customers.Create(customerToCreate);
```

**Exempel:** [Konsoltestapp](console-test-app.md). **Project:** Partnercenter-SDK Samples **Class**: CreateCustomerforIndirectReseller.cs

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod   | URI för förfrågan                                                       |
|----------|-------------------------------------------------------------------|
| **Inlägg** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1 |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

I den här tabellen beskrivs de nödvändiga egenskaperna i begärandetexten.

| Namn                                          | Typ   | Obligatorisk | Beskrivning                                                                                                                                                                                                                                                                                                                                           |
|-----------------------------------------------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [BillingProfile](#billing-profile)             | objekt | Yes      | Kundens faktureringsprofilinformation.                                                                                                                                                                                                                                                                                                           |
| [CompanyProfile](#company-profile)             | objekt | Yes      | Kundens företagsinformation.                                                               
| [AssociatedPartnerId](customer-resources.md#customer) | sträng | Yes      | Det indirekta återförsäljar-ID:t. Den indirekta återförsäljaren som anges av det ID som anges här måste ha ett samarbete med den indirekta leverantören, annars misslyckas begäran. Observera också att om värdet AssociatedPartnerId inte anges skapas kunden som en direkt kund till den indirekta leverantören i stället för den indirekta återförsäljaren. |
|Domain| Sträng| Yes|Kundens domännamn, till exempel contoso.onmicrosoft.com.|
|organizationRegistrationNumber|    sträng|Yes|     Kundens organisationsregistreringsnummer (kallas även INN-nummer i vissa länder). Krävs endast för kundens företag/organisation som finns i följande länder: Förargiga(AM), Gör(AZ), Gör(BY), För kunden(HU), För kundens företag/organisation som finns i följande länder: Förargande(AM), Förargare(AM), Förargare (AZ), För kunden(BY), För kunden krävs att du väljer Att göra så här: Kyrgyzstan(KG), Kyrgyzstan(KG), Hubar(MD), Ryssland(RU), Kerikistan (TJ), Kerten (CUS), Kerten(1996), Hubs(1996), 1996 (1996). För kundens företag/organisation som finns i andra länder är detta ett valfritt fält.|



#### <a name="billing-profile"></a>Faktureringsprofil

I den här tabellen beskrivs de minsta obligatoriska fälten från [resursen CustomerBillingProfile](customer-resources.md#customerbillingprofile) som krävs för att skapa en ny kund.

| Namn             | Typ                                     | Obligatorisk | Beskrivning                                                                                                                                                                                                     |
|------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| e-post            | sträng                                   | Yes      | Kundens e-postadress.                                                                                                                                                                                   |
| Kultur          | sträng                                   | Yes      | Deras önskade kultur för kommunikation och valuta, till exempel "en-US". Se [Språk och språk som stöds i Partnercenter för](partner-center-supported-languages-and-locales.md) de kulturer som stöds. |
| language         | sträng                                   | Yes      | Standardspråket. Två teckenspråkkoder (till `en` exempel `fr` eller ) stöds.                                                                                                                                |
| \_företagsnamn    | sträng                                   | Yes      | Det registrerade företags-/organisationsnamnet.                                                                                                                                                                       |
| \_standardadress | [Adress](utility-resources.md#address) | Yes      | Den registrerade adressen för kundens företag/organisation. Se [Adressresurs](utility-resources.md#address) för information om eventuella längdbegränsningar.                                             |

#### <a name="company-profile"></a>Företagsprofil

I den här tabellen beskrivs de minsta obligatoriska fälten från [resursen CustomerCompanyProfile](customer-resources.md#customercompanyprofile) som krävs för att skapa en ny kund.

| Namn   | Typ   | Obligatorisk | Beskrivning                                                  |
|--------|--------|----------|--------------------------------------------------------------|
| domän | sträng | Yes     | Kundens domännamn, till exempel contoso.onmicrosoft.com. |
| organizationRegistrationNumber | sträng | Beror på villkor | Kundens organisationsregistreringsnummer (kallas även INN-nummer i vissa länder). <br/><br/>Du behöver bara slutföra det här fältet om kundens företag/organisation finns i följande länder: <br/><br/>– 10:00 (AM) <br/>– På så vis (AZ)<br/>– Så här ser det ut (BY)<br/>– På så vis (HU)<br/>– Förlamning (KZ)<br/>– Kyrgyzstan (KG)<br/>– På så vis (MD)<br/>– Ryssland (RU)<br/>–Istikistan (TJ)<br/>–Istan ( CITY)<br/>– Äldsta (UA)<br/>– Indien <br/>– Brasilien <br/>– Sydafrika <br/>– På så vis <br/>– Förenade Arabemiraten <br/>– Saudiarabien <br/>– På så vis <br/>– På så vis <br/>– Vietnam <br/>– På så vis <br/>– På så sätt kan du <br/>– Sydsudan <br/>– På så vis<br/> <br/>För kundens företag/organisation som finns i andra länder är detta ett valfritt fält.  |

### <a name="request-example"></a>Exempel på begäran

```http
POST https://api.partnercenter.microsoft.com/v1/customers HTTP/1.1
Authorization: Bearer <token>
MS-RequestId: d628adbe-b7ee-412e-ac55-58f22b4ba2f4
MS-CorrelationId: 0dd197a8-992c-44ca-aeae-21cd83494dce
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 823
Expect: 100-continue
Connection: Keep-Alive

{
    "Id": null,
    "CommerceId": null,
    "CompanyProfile": {
        "TenantId": null,
        "Domain": "WingtipToys678152504.onmicrosoft.com",
        "CompanyName": null,
        "Attributes": {
            "ObjectType": "CustomerCompanyProfile"
        }
    },
    "BillingProfile": {
        "Id": null,
        "FirstName": null,
        "LastName": null,
        "Email": "Gena@wingtiptoys.com",
        "Culture": "EN-US",
        "Language": "En",
        "CompanyName": "Wingtip Toys678152504",
        "DefaultAddress": {
            "Country": "US",
            "Region": null,
            "City": "Redmond",
            "State": "WA",
            "AddressLine1": "One Microsoft Way",
            "AddressLine2": null,
            "PostalCode": "98052",
            "FirstName": "Gena",
            "LastName": "Soto",
            "PhoneNumber": "4255550101"
        },
        "Attributes": {
            "ObjectType": "CustomerBillingProfile"
        }
    },
    "RelationshipToPartner": "none",
    "AllowDelegatedAccess": null,
    "UserCredentials": null,
    "CustomDomains": null,
    "AssociatedPartnerId": "484e548c-f5f3-4528-93a9-c16c6373cb59",
    "Attributes": {
        "ObjectType": "Customer"
    }
}
```

## <a name="rest-response"></a>REST-svar

Om det lyckas innehåller svaret en [kundresurs](customer-resources.md#customer) för den nya kunden.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Svar har en HTTP-statuskod som anger att det lyckats eller misslyckats och ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 201 Created
Content-Length: 1085
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 0dd197a8-992c-44ca-aeae-21cd83494dce
MS-RequestId: d628adbe-b7ee-412e-ac55-58f22b4ba2f4
MS-CV: Yy/YaA0gYEmfQyR/.0
MS-ServerId: 030020525
Date: Tue, 06 Jun 2017 23:11:40 GMT

{
    "id": "626099fe-17af-4756-9fd0-6a73b7127859",
    "commerceId": "626099fe-17af-4756-9fd0-6a73b7127859",
    "companyProfile": {
        "tenantId": "626099fe-17af-4756-9fd0-6a73b7127859",
        "domain": "WingtipToys678152504.onmicrosoft.com",
        "companyName": "Wingtip Toys678152504",
        "links": {
            "self": {
                "uri": "/customers/626099fe-17af-4756-9fd0-6a73b7127859/profiles/company",
                "method": "GET",
                "headers": []
            }
        },
        "attributes": {
            "objectType": "CustomerCompanyProfile"
        }
    },
    "billingProfile": {
        "id": "7079246e-7b62-56ef-7cbd-a819514b54b5",
        "email": "Gena@wingtiptoys.com",
        "culture": "en-US",
        "language": "En",
        "companyName": "Wingtip Toys678152504",
        "defaultAddress": {
            "country": "US",
            "city": "Redmond",
            "state": "WA",
            "addressLine1": "One Microsoft Way",
            "postalCode": "98052",
            "firstName": "Gena",
            "lastName": "Soto",
            "phoneNumber": "4255550101"
        },
        "attributes": {
            "etag": "-8799889149591823008",
            "objectType": "CustomerBillingProfile"
        }
    },
    "relationshipToPartner": "reseller",
    "allowDelegatedAccess": true,
    "userCredentials": {
        "userName": "admin",
        "password": "0Krha*Io"
    },
    "associatedPartnerId": "484e548c-f5f3-4528-93a9-c16c6373cb59",
    "attributes": {
        "objectType": "Customer"
    }
}
```