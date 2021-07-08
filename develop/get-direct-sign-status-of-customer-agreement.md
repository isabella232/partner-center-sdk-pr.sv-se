---
title: Hämta kundens direktsigneringsstatus för Microsoft-kundavtal.
description: Du kan använda resursen DirectSignedCustomerAgreementStatus för att hämta status för en kunds direktsignering (direkt godkännande) av Microsoft-kundavtal.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: a17775614b4eb328514b2b32b4cac1e513019cff
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549186"
---
# <a name="get-the-status-of-a-customers-direct-signing-direct-acceptance-of-microsoft-customer-agreement"></a>Hämta status för en kunds direktsignering (direkt godkännande) av Microsoft-kundavtal

**Gäller för:** Partnercenter

**Gäller inte för**: Partner Center som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Resursen **DirectSignedCustomerAgreementStatus** stöds för närvarande endast av PartnerCenter i det offentliga Microsoft-molnet.

Den här artikeln förklarar hur du kan hämta status för en kunds direkta godkännande av Microsoft-kundavtal.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md) Det här scenariot har endast stöd för autentisering med app- och användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard) Välj **CSP** på Menyn i Partnercenter följt av **Kunder.** Välj kunden i kundlistan och välj sedan **Konto.** På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.** Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Om du vill hämta status för en kunds direkta godkännande av Microsoft-kundavtal anropar du [**metoden IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kundidentifieraren. Använd sedan egenskapen [**Agreements**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.agreements) för att hämta ett [**ICustomerAgreementCollection-gränssnitt.**](/dotnet/api/microsoft.store.partnercenter.agreements.icustomeragreementcollection) Anropa eller `GetDirectSignedCustomerAgreementStatus()` för att hämta `GetDirectSignedCustomerAgreementStatusAsync()` statusen.

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
var customerDirectSigningStatus = partnerOperations.Customers.ById(selectedCustomerId).Agreements.GetDirectSignedCustomerAgreementStatus();
```

**Exempel:** [Konsolexempelapp](https://github.com/microsoft/Partner-Center-DotNet-Samples). **Project:** SdkSamples-klass: GetDirectSignedCustomerAgreementStatus.cs 

## <a name="rest-request"></a>REST-begäran

Om du vill hämta status för en kunds direkta godkännande av Microsoft-kundavtal skapar du en REST-begäran för att hämta [DirectSignedCustomerAgreementStatus](./customer-agreement-direct-sign-status-resource.md) för kunden.

### <a name="request-syntax"></a>Begärandesyntax

Använd följande syntax för begäran:

| Metod | URI för förfrågan                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1 |

### <a name="uri-parameters"></a>URI-parametrar

Du kan använda följande URI-parametrar med din begäran:

| Namn             | Typ | Obligatorisk | Beskrivning                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| kund-klient-id | GUID | Ja | Värdet är ett GUID-formaterat **CustomerTenantId** som gör att du kan ange klient-ID för en kund. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden en [ **DirectSignedCustomerAgreementStatus-resurs**](./customer-agreement-direct-sign-status-resource.md) i svarstexten.

Resursen har en **isSigned-egenskap** som anger kundens status för direktsignering (direktgodkännande).

- Värdet true **anger** att avtalet har signerats (godkänts) direkt av kunden.

- Värdet false **anger** att avtalet inte har *signerats* (godkänts) direkt av kunden.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.

Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Length: 20
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b

{"isSigned":true}
```
