---
title: Skapa en kund
description: 'Lär dig hur en partner av en moln lösnings leverantör (CSP) kan använda API: er för partner Center för att skapa en ny kund. Artikeln beskriver krav och vad som händer mer.'
ms.date: 03/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: bc8e9d38353511e747ba4da99b11be40d08781e3
ms.sourcegitcommit: faea78fe3264cbafc2b02c04d98d5ce30e992124
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/03/2021
ms.locfileid: "106274605"
---
# <a name="create-a-customer-using-partner-center-apis"></a>Skapa en kund med hjälp av API: er för partner Center

**Gäller för:**

- Partnercenter
- Partnercenter drivs av 21Vianet
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Den här artikeln beskriver hur du skapar en ny kund.

> [!IMPORTANT]
> Om du är en indirekt leverantör och vill skapa en kund för en indirekt åter försäljare, se [skapa en kund för en indirekt åter försäljare](create-a-customer-for-an-indirect-reseller.md).

Som en partner av en moln lösnings leverantör (CSP) kan du, när du skapar en kund, placera beställningar för kundens räkning. När du skapar en kund skapar du även:

- Ett Azure Active Directory (AD) klient objekt för kunden.

- En relation mellan åter försäljaren och kunden, som används för delegerade administratörs privilegier.

- Ett användar namn och lösen ord för att logga in som administratör för kunden.

När kunden har skapats, se till att spara kund-ID och Azure AD-information för framtida användning med partner Center SDK (till exempel konto hantering).

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.

> [!IMPORTANT]
> Om du vill skapa en kund klient organisation måste du ange en giltig fysisk adress under skapande processen. En adress kan verifieras genom att följa stegen som beskrivs i avsnittet [validera ett adress](validate-an-address.md) scenario. Om du skapar en kund med en ogiltig adress i sandbox-miljön kommer du inte att kunna ta bort den kund klienten.

## <a name="c"></a>C\#

Så här lägger du till en kund:

1. Instansiera ett nytt [**kund**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) objekt. Se till att fylla i [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) och [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile).

2. Lägg till den nya kunden i din [**IAggregatePartner. Customer**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) -samling genom att anropa [**create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) eller [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync).

### <a name="c-example"></a>C- \# exempel

```csharp
// IAggregatePartner partnerOperations;

var partnerOperations = this.Context.UserPartnerOperations;

var customerToCreate = new Customer()
{
    CompanyProfile = new CustomerCompanyProfile()
    {
        Domain = string.Format(CultureInfo.InvariantCulture,
            "SampleApplication{0}.{1}",
            new Random().Next(),
            this.Context.Configuration.Scenario.CustomerDomainSuffix),
        //// OrganizationRegistrationNumber = "123456" // Please add if in specific country that requires
    },
    BillingProfile = new CustomerBillingProfile()
    {
        Culture = "EN-US",
        Email = "someone@example.com",
        Language = "En",
        CompanyName = "Some Company" + new Random().Next(),
        DefaultAddress = new Address()
        {
            FirstName = "Tania",
            MiddleName = "MiddleName",
            LastName = "Carr",
            AddressLine1 = "One Microsoft Way",
            City = "Redmond",
            State = "WA",
            Country = "US",
            PostalCode = "98052",
            PhoneNumber = ""
        }
    }
};

var newCustomer = partnerOperations.Customers.Create(customerToCreate);
```

**Exempel**: [konsol test app](console-test-app.md). **Projekt**: Partner Center SDK-exempel **klass**: CreateCustomer. CS

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Så här skapar du en ny kund:

1. Skapa en ny instans av **CustomerBillingProfile** och **CustomerCompanyProfile** -objekten. Var noga med att fylla i de obligatoriska fälten.

2. Skapa kunden genom att anropa funktionen **IAggregatePartner. getCustomers (). Create** .

### <a name="java-example"></a>Java-exempel

```java
// IAggregatePartner partnerOperations;

Address address = new Address();

address.setFirstName( "Gena" );
address.setLastName( "Soto" );
address.setAddressLine1( "One Microsoft Way" );
address.setCity( "Redmond" );
address.setState( "WA" );
address.setCountry( "US" );
address.setPostalCode( "98052" );
address.setPhoneNumber( "4255550101" );

CustomerBillingProfile billingProfile = new CustomerBillingProfile();

billingProfile.setCulture( "en-US" );
billingProfile.setEmail( "gena@wingtiptoys.com" );
billingProfile.setLanguage( "en" );
billingProfile.setCompanyName( "Wingtip Toys" + new Random().nextInt() );
billingProfile.setDefaultAddress( address );

CustomerCompanyProfile companyProfile = new CustomerCompanyProfile();

companyProfile.setDomain( "WingtipToys" + Math.abs( new Random().nextInt() ) + ".onmicrosoft.com" );

Customer customerToCreate = new Customer();

customerToCreate.setBillingProfile( billingProfile );
customerToCreate.setCompanyProfile( companyProfile );

Customer newCustomer = partnerOperations.getCustomers().create( customerToCreate );
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Om du vill skapa en kund kör du kommandot [**New-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomer.md) .

```powershell
New-PartnerCustomer -BillingAddressLine1 '1 Microsoft Way' -BillingAddressCity 'Redmond' -BillingAddressCountry 'US' -BillingAddressPostalCode '98052' -BillingAddressState 'WA' -ContactEmail 'jdoe@customer.com' -ContactFirstName 'Jane' -ContactLastName 'Doe' -Culture 'en-US' -Domain 'newcustomer.onmicrosoft.com' -Language 'en' -Name 'New Customer'
```

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod   | URI för förfrågan                                                       |
|----------|-------------------------------------------------------------------|
| **EFTER** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers http/1.1 |

### <a name="request-headers"></a>Begärandehuvuden

- Detta API är idempotenta (det ger inte något annat resultat om du anropar det flera gånger).

- ID för begäran och korrelations-ID krävs.

- Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

I den här tabellen beskrivs de egenskaper som krävs i begär ande texten.

| Namn                              | Typ   | Beskrivning                                 |
|-----------------------------------|--------|---------------------------------------------|
| [BillingProfile](#billing-profile) | objekt | Kundens fakturerings profil information. |
| [CompanyProfile](#company-profile) | objekt | Kundens företags profil information. |

#### <a name="billing-profile"></a>Faktureringsprofil

I den här tabellen beskrivs minimi kraven för fält från [CustomerBillingProfile](customer-resources.md#customerbillingprofile) -resursen som behövs för att skapa en ny kund.

| Namn             | Typ                                     | Beskrivning                                                                                                                                                                                                     |
|------------------|------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| e-post            | sträng                                   | Kundens e-postadress.                                                                                                                                                                                   |
| substrat          | sträng                                   | Deras föredragna kultur för kommunikation och valuta, till exempel "en-US". Se de [språk som stöds av Partner Center och nationella inställningar](partner-center-supported-languages-and-locales.md) för de kulturer som stöds. |
| language         | sträng                                   | Standard språket. Två characters språk koder (till exempel `en` eller `fr` ) stöds.                                                                                                                                |
| företags \_ namn    | sträng                                   | Registrerat företags-/organisations namn.                                                                                                                                                                       |
| standard \_ adress | [Adress](utility-resources.md#address) | Den registrerade adressen för kundens företag/organisation. Se [adress](utility-resources.md#address) resursen för information om eventuella längd begränsningar.                                             |

#### <a name="company-profile"></a>Företags profil

I den här tabellen beskrivs minimi kraven för fält från [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) -resursen som behövs för att skapa en ny kund.

| Namn   | Typ   | Beskrivning                                                  |
|--------|--------|--------------------------------------------------------------|
| domän | sträng | Kundens domän namn, till exempel contoso.onmicrosoft.com. |
|organizationRegistrationNumber|Sträng|Kundens organisations registrerings nummer (kallas även för INN-nummer i vissa länder). Krävs endast för kundens företag/organisation i följande länder: Armenien (AM), Azerbajdzjan (AZ), Vitryssland (av), Ungern (HU), Kazakstan (KZ), Kirgizistan (KG), Moldavien (MD), Ryssland (RU), Tadzjikistan (TJ), Uzbekistan (UZ), Ukraina (UA), Brasilien (BR), Indien, Sydafrika, Polen, Förenade Arabemiraten, Saudiarabien, Turkiet, Thailand, Vietnam, Myanmar, Irak, Sydsudan och Venezuela. För kundens företag/organisation i andra länder är detta ett valfritt fält.|

### <a name="request-example"></a>Exempel på begäran

```http
POST https://api.partnercenter.microsoft.com/v1/customers HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 789
Expect: 100-continue
Connection: Keep-Alive

{
    "CompanyProfile": {
        "Domain": "xyz.ccsctp.net",
    },
    "BillingProfile": {
        "Culture": "EN-US",
        "Email": "test@outlook.com",
        "Language": "en",
        "CompanyName": "test company",
        "DefaultAddress": {
            "FirstName": "Test",
            "LastName": "Test",
            "AddressLine1": "One Microsoft Way",
            "City": "Redmond",
            "State": "WA",
            "PostalCode": "98052",
            "Country": "US",
        }
    }
}
```

## <a name="rest-response"></a>REST-svar

Om detta lyckas returnerar detta API en [kund](customer-resources.md#customer) resurs för den nya kunden. Spara kund-ID och Azure AD-information för framtida användning med partner Center SDK. Du behöver dem för att kunna använda med konto hantering, till exempel.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 201 Created
Content-Length: 834
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CV: ObwhuhD2tUKJoM+Z.0
MS-ServerId: 202010223
Date: Tue, 14 Feb 2017 20:06:02 GMT

{
    "id": "dfd8cc0a-c592-468c-8461-869a38d24738",
    "commerceId": "0a4ce58a-6f96-4273-8035-d9c7d31b9ba4",
    "companyProfile": {
        "tenantId": "dfd8cc0a-c592-468c-8461-869a38d24738",
        "domain": "xyz.ccsctp.net",
        "attributes": {
            "objectType": "CustomerCompanyProfile"
        }
    },
    "billingProfile": {
        "id": "d17c0275-da92-5c33-9032-782ef1d0b69b",
        "email": "test@outlook.com",
        "culture": "en-US",
        "language": "en",
        "companyName": "test company",
        "defaultAddress": {
            "country": "US",
            "city": "Redmond",
            "state": "WA",
            "addressLine1": "One Microsoft Way",
            "postalCode": "98052",
            "firstName": "Test",
            "lastName": "Test",
            "phoneNumber": ""
        },
        "attributes": {
            "etag": "5920358838484612121",
            "objectType": "CustomerBillingProfile"
        }
    },
    "relationshipToPartner": "none",
    "userCredentials": {
        "userName": "admin",
        "password": "=;;n.=s9Z"
    },
    "attributes": {
        "objectType": "Customer"
    }
}
```
