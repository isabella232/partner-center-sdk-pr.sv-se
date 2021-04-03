---
title: Skapa en kund för en indirekt återförsäljare
description: 'Lär dig hur en indirekt Provider kan använda API: er i Partner Center för att skapa en kund för en indirekt åter försäljare.'
ms.date: 04/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 0de40d08e9fc2b9cf87b7c3c41214fdd34ad26f3
ms.sourcegitcommit: faea78fe3264cbafc2b02c04d98d5ce30e992124
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/03/2021
ms.locfileid: "106274588"
---
# <a name="create-a-customer-for-an-indirect-reseller-using-partner-center-apis"></a>Skapa en kund för en indirekt åter försäljare med hjälp av API: er för partner Center

**Gäller för:**

- Partnercenter

En indirekt leverantör kan skapa en kund för en indirekt åter försäljare.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.

- Klient-ID för den indirekta åter försäljaren.

- Den indirekta åter försäljaren måste ha ett partnerskap med den indirekta providern.

## <a name="c"></a>C\#

Så här lägger du till en ny kund för en indirekt åter försäljare:

1. Instansiera [**ett nytt**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) kundobjekt och instansiera sedan och fyll i [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) och [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile). Se till att tilldela ID för den indirekta åter försäljaren till [**AssociatedPartnerID**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer.associatedpartnerid) -egenskapen.

2. Använd egenskapen [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) för att hämta ett gränssnitt till kund samlings åtgärder.

3. Anropa [**create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) -eller [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) -metoden för att skapa kunden.

### <a name="c-example"></a>C- \# exempel

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

**Exempel**: [konsol test app](console-test-app.md). **Projekt**: Partner Center SDK-exempel **klass**: CreateCustomerforIndirectReseller. CS

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod   | URI för förfrågan                                                       |
|----------|-------------------------------------------------------------------|
| **EFTER** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers http/1.1 |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

I den här tabellen beskrivs de egenskaper som krävs i begär ande texten.

| Namn                                          | Typ   | Obligatorisk | Beskrivning                                                                                                                                                                                                                                                                                                                                           |
|-----------------------------------------------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [BillingProfile](#billing-profile)             | objekt | Ja      | Kundens fakturerings profil information.                                                                                                                                                                                                                                                                                                           |
| [CompanyProfile](#company-profile)             | objekt | Ja      | Kundens företags profil information.                                                               
| [AssociatedPartnerId](customer-resources.md#customer) | sträng | Ja      | ID för den indirekta åter försäljaren. Den indirekta åter försäljaren som anges av det ID som anges här måste ha ett partnerskap med den indirekta providern eller så Miss förfrågans begäran. Observera också att om AssociatedPartnerId-värdet inte anges skapas kunden som en direkt kund för den indirekta leverantören i stället för den indirekta åter försäljaren. |
|Domain| Sträng| Ja|Kundens domän namn, till exempel contoso.onmicrosoft.com.|
|organizationRegistrationNumber|    sträng|Ja|     Kundens organisations registrerings nummer (kallas även för INN-nummer i vissa länder). Krävs endast för kundens företag/organisation i följande länder: Armenien (AM), Azerbajdzjan (AZ). Vitryssland (BY), Ungern (HU), Kazakstan (KZ), Kirgizistan (KG), Moldavien (MD), Ryssland (RU), Tadzjikistan (TJ), Uzbekistan (UZ), Ukraina (UA), Indien, Brasilien, Sydafrika, Polen, Förenade Arabemiraten, Saudiarabien, Turkiet, Thailand, Vietnam, Myanmar, Irak, Sydsudan och Venezuela. För kundens företag/organisation i andra länder är detta ett valfritt fält.|



#### <a name="billing-profile"></a>Faktureringsprofil

I den här tabellen beskrivs minimi kraven för fält från [CustomerBillingProfile](customer-resources.md#customerbillingprofile) -resursen som behövs för att skapa en ny kund.

| Namn             | Typ                                     | Obligatorisk | Beskrivning                                                                                                                                                                                                     |
|------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| e-post            | sträng                                   | Ja      | Kundens e-postadress.                                                                                                                                                                                   |
| substrat          | sträng                                   | Ja      | Deras föredragna kultur för kommunikation och valuta, till exempel "en-US". Se de [språk som stöds av Partner Center och nationella inställningar](partner-center-supported-languages-and-locales.md) för de kulturer som stöds. |
| language         | sträng                                   | Ja      | Standard språket. Två characters språk koder (till exempel `en` eller `fr` ) stöds.                                                                                                                                |
| företags \_ namn    | sträng                                   | Ja      | Registrerat företags-/organisations namn.                                                                                                                                                                       |
| standard \_ adress | [Adress](utility-resources.md#address) | Ja      | Den registrerade adressen för kundens företag/organisation. Se [adress](utility-resources.md#address) resursen för information om eventuella längd begränsningar.                                             |

#### <a name="company-profile"></a>Företags profil

I den här tabellen beskrivs minimi kraven för fält från [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) -resursen som behövs för att skapa en ny kund.

| Namn   | Typ   | Obligatorisk | Beskrivning                                                  |
|--------|--------|----------|--------------------------------------------------------------|
| domän | sträng | Ja     | Kundens domän namn, till exempel contoso.onmicrosoft.com. |
| organizationRegistrationNumber | sträng | Är beroende av villkor | Kundens organisations registrerings nummer (kallas även för INN-numret i vissa länder). <br/><br/>Du behöver bara fylla i det här fältet om en kunds företag/organisation finns i följande länder: <br/><br/>-Armenien (AM) <br/>– Azerbajdzjan (AZ)<br/>– Vitryssland (av)<br/>– Ungern (HU)<br/>-Kazakstan (KZ)<br/>– Kirgizistan (KG)<br/>– Moldavien (MD)<br/>– Ryssland (RU)<br/>– Tadzjikistan (TJ)<br/>-Uzbekistan (UZ)<br/>-Ukraina (UA)<br/>– Indien <br/>– Brasilien <br/>-Sydafrika <br/>– Polen <br/>– Förenade Arabemiraten <br/>– Saudiarabien <br/>– Turkiet <br/>– Thailand <br/>– Vietnam <br/>– Myanmar <br/>– Irak <br/>– Sydsudan <br/>-Venezuela<br/> <br/>För kundens företag/organisation i andra länder är detta ett valfritt fält.  |

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

Om det lyckas innehåller svaret en [kund](customer-resources.md#customer) resurs för den nya kunden.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).

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