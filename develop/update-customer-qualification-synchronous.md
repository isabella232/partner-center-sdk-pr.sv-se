---
title: Uppdatera en kunds kvalificering
description: Lär dig hur du uppdaterar en kunds kompetens via synkron kontroll eller kontroll, inklusive adressen som är associerad med profilen.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 5047743afdef02033d9494e3d8c16c9ab96b3fe9
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446657"
---
# <a name="update-a-customers-qualification-via-synchronous-validation"></a>Uppdatera en kunds kvalificering via synkron validering

Lär dig hur du uppdaterar en kunds kvalificeringar synkront via Partner Center-API:er. Information om hur du gör detta asynkront finns i [Uppdatera en kunds kvalificering via asynkron validering](update-customer-qualification-asynchronous.md).

En partner kan uppdatera en kunds kvalificering till "Education" eller "GovernmentCommunityCloud". Andra värden, "None" och "Nonprofit", kan inte anges.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med app- och användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard) Välj **CSP** på Menyn i Partnercenter följt av **Kunder**. Välj kunden i kundlistan och välj sedan **Konto.** På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.** Microsoft-ID:t är samma som kund-ID :t ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Om du vill uppdatera en kunds kvalificering till "Education" anropar du **[Update/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification.update)** på en  [**befintlig kund**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer).

``` csharp
// CustomerQualification is an enum

var eduCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.Education);
```

**Exempel:** [Konsoltestapp](console-test-app.md). **Project:** PartnerSDK.FeatureSamples-klass: CustomerQualificationOperations.cs 

För att uppdatera en kunds kvalificering **till GovernmentCommunityCloud** på en befintlig kund utan kvalificering måste partnern inkludera kundens [**valideringskod.**](utility-resources.md#validationcode)

``` csharp
// CustomerQualification is an enum
// GCC validation is type ValidationCode

var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.GovernmentCommunityCloud, gccValidation);
```

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod  | URI för förfrågan                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualification?code={validationCode} HTTP/1.1 |

### <a name="uri-parameter"></a>URI-parameter

Använd följande frågeparameter för att uppdatera kvalificeringen.

| Namn                   | Typ | Obligatorisk | Beskrivning                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **kund-klient-id** | GUID | Ja      | Värdet är ett GUID-formaterat **kundklient-ID** som gör att återförsäljaren kan filtrera resultaten för en viss kund som tillhör återförsäljaren. |
| **validationCode**     | int  | Inga       | Behövs bara för Government Community Cloud.                                                                                                            |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

Heltalsvärdet från [**CustomerQualification-uppräkning.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification)

### <a name="request-example"></a>Exempel på begäran

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualification?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden den uppdaterade kvalificeringsegenskapen i svarstexten. [](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification)

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder.](error-codes.md)

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Length: 14
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
"governmentcommunitycloud"
```

## <a name="related-articles"></a>Relaterade artiklar

- [Hämta en kunds kvalificering](./get-customer-qualification-synchronous.md)
- [Hämta en partners valideringskoder](get-a-partner-s-validation-codes.md)
