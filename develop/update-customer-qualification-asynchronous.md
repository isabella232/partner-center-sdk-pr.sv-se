---
title: Uppdatera en kunds kvalificeringar
description: Uppdaterar en kunds kvalifikationer asynkront, inklusive adressen som är kopplad till profilen.
ms.date: 03/23/2021
ms.service: partner-dashboard
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: 7606eeaac4df158ec0fad6ffd4e565bb250f448e
ms.sourcegitcommit: bbdb5f7c9ddd42c2fc4eaadbb67d61aeeae805ca
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/24/2021
ms.locfileid: "105030614"
---
# <a name="update-a-customers-qualifications-asynchronously"></a>Uppdatera en kunds kvalifikationer asynkront

Uppdaterar en kunds kvalifikationer asynkront.

En partner kan uppdatera en kunds kvalifikationer asynkront så att de blir "utbildning" eller "GovernmentCommunityCloud". Andra värden, "ingen" och "icke-vinst" kan inte anges.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Skapa en kunds kvalificering för "utbildning" genom att först skapa ett objekt som representerar kvalificerings typen. Anropa sedan metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID. Använd sedan egenskapen [**kvalificering**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) för att hämta ett [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) -gränssnitt. Anropa slutligen `CreateQualifications()` eller `CreateQualificationsAsync()` med kvalificerings typ objektet som en indataparameter.

``` csharp
var qualificationType = { Qualification = "education" };
var eduCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.CreateQualifications(qualificationType);
```

**Exempel**: [app för konsol exempel](https://github.com/microsoft/Partner-Center-DotNet-Samples). **Projekt**: SdkSamples- **klass**: CreateCustomerQualification. CS

För att kunna uppdatera en kunds kvalificering till **GovernmentCommunityCloud** på en befintlig kund utan kvalificering, måste partnern också inkludera kundens [**ValidationCode**](utility-resources.md#validationcode). Börja med att skapa ett objekt som representerar kvalificerings typen. Anropa sedan metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID. Använd sedan egenskapen [**kvalificering**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) för att hämta ett [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) -gränssnitt. Anropa slutligen `CreateQualifications()` eller `CreateQualificationsAsync()` med kvalificerings typ objekt och validerings koden som indataparametrar.

``` csharp
// GCC validation is type ValidationCode
var qualificationType = { Qualification = "GovernmentCommunityCloud" };
var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.CreateQualifications(qualificationType, gccValidation);
```

**Exempel**: [app för konsol exempel](https://github.com/microsoft/Partner-Center-DotNet-Samples). **Projekt**: SdkSamples- **klass**: CreateCustomerQualificationWithGCC. CS

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod  | URI för förfrågan                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| **EFTER** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{customer_id}/Qualifications? Code = {VALIDATIONCODE} http/1.1 |

### <a name="uri-parameter"></a>URI-parameter

Använd följande frågeparameter för att uppdatera kvalificeringen.

| Namn                   | Typ | Obligatorisk | Beskrivning                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **kund-ID för klient organisation** | GUID | Ja      | Värdet är ett GUID-formaterat **kund-Tenant-ID** som gör det möjligt för åter försäljaren att filtrera resultaten för en specifik kund som tillhör åter försäljaren. |
| **validationCode**     | int  | Inga       | Krävs endast för Community-molnet för myndigheter.                                                                                                            |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

I den här tabellen beskrivs kvalificerings objekt i begär ande texten.

Egenskap | Typ | Obligatorisk | Beskrivning
-------- | ---- | -------- | -----------
Kvalificering | sträng | Ja | Strängvärdet från [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) -uppräkningen.

### <a name="request-example"></a>Exempel på begäran

```http
POST https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

{
    "Qualification": "Education"
}

```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden ett kvalificerings objekt i svars texten. Nedan visas ett exempel på **post** anropet på en kund (med ett tidigare kvalificerings **ingen**) med **utbildnings** kompetensen.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [felkoder](error-codes.md).

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 201 CREATED
Content-Length: 29
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
{
    "qualification": "Education",
    "vettingStatus": "InReview",
    "vettingCreateDate": "2020-12-04T20:54:24Z" // UTC
}
```

## <a name="related-articles"></a>Relaterade artiklar

- [Få en kunds kompetens](./get-customer-qualification-asynchronous.md)
- [Hämta en partners valideringskoder](get-a-partner-s-validation-codes.md)
