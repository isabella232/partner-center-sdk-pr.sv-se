---
title: Skapa en kund
description: Lär dig hur en Molnlösningsleverantör(CSP)-partner kan använda Partner Center-API:er för att skapa en ny kund. I artikeln beskrivs förutsättningar och vad som händer mer.
ms.date: 03/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 6232ca77d057f2f5168b73d81ec551669d540246
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973731"
---
# <a name="create-a-customer-using-partner-center-apis"></a>Skapa en kund med partnercenter-API:er

**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud for US Government

Den här artikeln beskriver hur du skapar en ny kund.

> [!IMPORTANT]
> Om du är en indirekt leverantör och vill skapa en kund för en indirekt återförsäljare kan du se [Skapa en kund för en indirekt återförsäljare.](create-a-customer-for-an-indirect-reseller.md)

Som CSP-partner (molnlösningsleverantör) kan du, när du skapar en kund, göra beställningar åt kunden. När du skapar en kund skapar du även:

- Ett Azure Active Directory (AD)-klientobjekt för kunden.

- En relation mellan återförsäljaren och kunden som används för delegerade administratörsbehörigheter.

- Ett användarnamn och lösenord för att logga in som administratör för kunden.

När kunden har skapats ska du spara kund-ID och Azure AD-information för framtida användning med Partnercenter-SDK (till exempel kontohantering).

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md) Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.

> [!IMPORTANT]
> Om du vill skapa en kundklientorganisation måste du ange en giltig fysisk adress under skapandeprocessen. En adress kan verifieras genom att följa stegen i scenariot [Verifiera en](validate-an-address.md) adress. Om du skapar en kund med en ogiltig adress i sandbox-miljön kan du inte ta bort den kundklientorganisationen.

## <a name="c"></a>C\#

Så här lägger du till en kund:

1. Instansiera ett nytt [**kundobjekt.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) Se till att fylla i [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) och [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile).

2. Lägg till den nya kunden i din [**IAggregatePartner.Customers-samling**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) genom att [**anropa Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) eller [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync).

### <a name="c-example"></a>\#C-exempel

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

**Exempel:** [Konsoltestapp](console-test-app.md). **Project:** Partnercenter-SDK Samples **Class**: CreateCustomer.cs

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Så här skapar du en ny kund:

1. Skapa en ny instans av **objekten CustomerBillingProfile** och **CustomerCompanyProfile.** Se till att fylla i de obligatoriska fälten.

2. Skapa kunden genom att anropa **funktionen IAggregatePartner.getCustomers().create.**

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

Skapa en kund genom att köra [**kommandot New-PartnerCustomer.**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomer.md)

```powershell
New-PartnerCustomer -BillingAddressLine1 '1 Microsoft Way' -BillingAddressCity 'Redmond' -BillingAddressCountry 'US' -BillingAddressPostalCode '98052' -BillingAddressState 'WA' -ContactEmail 'jdoe@customer.com' -ContactFirstName 'Jane' -ContactLastName 'Doe' -Culture 'en-US' -Domain 'newcustomer.onmicrosoft.com' -Language 'en' -Name 'New Customer'
```

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod   | URI för förfrågan                                                       |
|----------|-------------------------------------------------------------------|
| **Inlägg** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1 |

### <a name="request-headers"></a>Begärandehuvuden

- Det här API:et är idempotent (det ger inte ett annat resultat om du anropar det flera gånger).

- Ett begärande-ID och korrelations-ID krävs.

- Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

I den här tabellen beskrivs de obligatoriska egenskaperna i begärandetexten.

| Namn                              | Typ   | Beskrivning                                 |
|-----------------------------------|--------|---------------------------------------------|
| [BillingProfile](#billing-profile) | objekt | Kundens faktureringsprofilinformation. |
| [CompanyProfile](#company-profile) | objekt | Kundens företagsinformation. |

#### <a name="billing-profile"></a>Faktureringsprofil

I den här tabellen beskrivs de minsta obligatoriska fälten från [resursen CustomerBillingProfile](customer-resources.md#customerbillingprofile) som krävs för att skapa en ny kund.

| Namn             | Typ                                     | Beskrivning                                                                                                                                                                                                     |
|------------------|------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| e-post            | sträng                                   | Kundens e-postadress.                                                                                                                                                                                   |
| Kultur          | sträng                                   | Deras önskade kultur för kommunikation och valuta, till exempel "en-US". Se [Partnercenter– språk och språk som stöds](partner-center-supported-languages-and-locales.md) för de kulturer som stöds. |
| language         | sträng                                   | Standardspråket. Två teckenspråkkoder (till `en` exempel `fr` eller ) stöds.                                                                                                                                |
| \_företagsnamn    | sträng                                   | Det registrerade företags-/organisationsnamnet.                                                                                                                                                                       |
| \_standardadress | [Adress](utility-resources.md#address) | Den registrerade adressen för kundens företag/organisation. Se [Adressresurs](utility-resources.md#address) för information om eventuella längdbegränsningar.                                             |

#### <a name="company-profile"></a>Företagsprofil

I den här tabellen beskrivs de minsta obligatoriska fälten från [resursen CustomerCompanyProfile](customer-resources.md#customercompanyprofile) som krävs för att skapa en ny kund.

| Namn   | Typ   | Beskrivning                                                  |
|--------|--------|--------------------------------------------------------------|
| domän | sträng | Kundens domännamn, till exempel contoso.onmicrosoft.com. |
|organizationRegistrationNumber|Sträng|Kundens organisationsregistreringsnummer (kallas även INN-nummer i vissa länder). Krävs endast för kundens företag/organisation som finns i följande länder: DoS(AM), DoS (AZ), Hubs(BY), För kunden(HU), För e-post i KZ, Kyrgyzstan(KG), För att få hjälp med det, För att göra det kan du till exempel skriva en lista över frågor som inte kan användas. För kundens företag/organisation som finns i andra länder är detta ett valfritt fält.|

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

Om det lyckas returnerar detta API [en kundresurs](customer-resources.md#customer) för den nya kunden. Spara kund-ID och Azure AD-information för framtida användning med Partnercenter-SDK. Du behöver dem till exempel för användning med kontohantering.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Svar har en HTTP-statuskod som anger att det lyckats eller misslyckats samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)

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
