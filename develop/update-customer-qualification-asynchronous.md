---
title: Uppdatera en kunds kvalificeringar
description: Uppdaterar en kunds kvalificering asynkront, inklusive adressen som är kopplad till profilen.
ms.date: 03/23/2021
ms.service: partner-dashboard
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: d7dd3593894ce91ddc7b96d604b80153d41d3a67
ms.sourcegitcommit: 51237e7e98d71a7e0590b4d6a4034b6409542126
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/09/2021
ms.locfileid: "113572105"
---
# <a name="update-a-customers-qualifications-asynchronously"></a>Uppdatera en kunds kvalificeringar asynkront

Uppdaterar en kunds kvalificeringar asynkront.

En partner kan uppdatera en kunds kompetens asynkront till "Utbildning" eller "GovernmentCommunityCloud". Andra värden, "None" och "Nonprofit", kan inte anges.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md) Det här scenariot har endast stöd för autentisering med app- och användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard) Välj **CSP** på Menyn i Partnercenter följt av **Kunder.** Välj kunden i kundlistan och välj sedan **Konto.** På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.** Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Om du vill skapa en kunds kvalificering för "Utbildning" skapar du först ett objekt som representerar kvalificeringstypen. Anropa sedan metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kundidentifieraren. Använd sedan egenskapen [**Kvalificering för**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) att hämta ett [**ICustomerQualification-gränssnitt.**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) Anropa eller med `CreateQualifications()` `CreateQualificationsAsync()` objektet för kvalificeringstyp som en indataparameter.

``` csharp
var qualificationToCreate = "education";    // can also be "StateOwnedEntity" or "GovernmentCommunityCloud". See GCC example below.
var qualificationType = { Qualification = qualificationToCreate };
var eduCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.CreateQualifications(qualificationType);
```

**Exempel:** [Konsolexempelapp](https://github.com/microsoft/Partner-Center-DotNet-Samples). **Project:** SdkSamples-klass: CreateCustomerQualification.cs 

För att uppdatera en kunds kvalificering till **GovernmentCommunityCloud** på en befintlig kund utan kvalificering måste partnern också inkludera kundens [**valideringskod**](utility-resources.md#validationcode). Skapa först ett objekt som representerar kvalificeringstypen. Anropa sedan metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kundidentifieraren. Använd sedan egenskapen [**Kvalificering för**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) att hämta ett [**ICustomerQualification-gränssnitt.**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) Anropa eller med `CreateQualifications()` `CreateQualificationsAsync()` kvalificeringstypobjektet och valideringskoden som indataparametrar.

``` csharp
// GCC validation is type ValidationCode
var qualificationType = { Qualification = "GovernmentCommunityCloud" };
var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.CreateQualifications(qualificationType, gccValidation);
```

**Exempel:** [Konsolexempelapp](https://github.com/microsoft/Partner-Center-DotNet-Samples). **Project:** SdkSamples-klass: CreateCustomerQualificationWithGCC.cs 

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod  | URI för förfrågan                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| **Inlägg** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/kvalificeringar?code={validationCode} HTTP/1.1 |

### <a name="uri-parameter"></a>URI-parameter

Använd följande frågeparameter för att uppdatera kvalificeringen.

| Namn                   | Typ | Obligatorisk | Beskrivning                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **kund-klient-id** | GUID | Yes      | Värdet är ett GUID-formaterat **kundklient-ID** som gör att återförsäljaren kan filtrera resultaten för en viss kund som tillhör återförsäljaren. |
| **validationCode**     | int  | No       | Behövs bara för Government Community Cloud.                                                                                                            |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

I den här tabellen beskrivs kvalificeringsobjektet i begärandetexten.

Egenskap | Typ | Obligatorisk | Beskrivning
-------- | ---- | -------- | -----------
Kvalificering | sträng | Yes | Strängvärdet från [**uppräkning av CustomerQualification.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification)

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

Om det lyckas returnerar den här metoden ett kvalificeringsobjekt i svarstexten. Nedan visas ett exempel på **POST-anropet** på en kund (med en tidigare kvalificering på **Ingen)** med **utbildningskvalificering.**

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder.](error-codes.md)

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

- [Skaffa en kunds kompetens](./get-customer-qualification-asynchronous.md)
- [Hämta en partners valideringskoder](get-a-partner-s-validation-codes.md)
