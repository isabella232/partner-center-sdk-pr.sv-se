---
title: Hämta kundens direkta signerings status för Microsofts kund avtal.
description: Du kan använda DirectSignedCustomerAgreementStatus-resursen för att hämta statusen för en kunds direkta signering (direkt godkännande) för Microsofts kund avtal.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 267e3aa63a94c5045977ad566eb5061df3b59882
ms.sourcegitcommit: bbdb5f7c9ddd42c2fc4eaadbb67d61aeeae805ca
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/24/2021
ms.locfileid: "105030578"
---
# <a name="get-the-status-of-a-customers-direct-signing-direct-acceptance-of-microsoft-customer-agreement"></a>Hämta statusen för en kunds direkta signering (direkt godkännande) för Microsofts kund avtal

**Gäller för:**

- Partnercenter

**DirectSignedCustomerAgreementStatus** -resursen stöds för närvarande endast av Partner Center i det offentliga Microsoft-molnet.

Den här resursen är *inte tillämplig* för:

- Partnercenter drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Den här artikeln förklarar hur du kan hämta statusen för en kunds direkta godkännande av Microsofts kund avtal.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).

## <a name="c"></a>C\#

För att hämta statusen för en kunds direkta godkännande av Microsofts kund avtal, anropa metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID. Använd sedan egenskapen [**Agreements**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.agreements) för att hämta ett [**ICustomerAgreementCollection**](/dotnet/api/microsoft.store.partnercenter.agreements.icustomeragreementcollection) -gränssnitt. Till sist anropa `GetDirectSignedCustomerAgreementStatus()` eller `GetDirectSignedCustomerAgreementStatusAsync()` för att hämta statusen.

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
var customerDirectSigningStatus = partnerOperations.Customers.ById(selectedCustomerId).Agreements.GetDirectSignedCustomerAgreementStatus();
```

**Exempel**: [app för konsol exempel](https://github.com/microsoft/Partner-Center-DotNet-Samples). **Projekt**: SdkSamples- **klass**: GetDirectSignedCustomerAgreementStatus. CS

## <a name="rest-request"></a>REST-begäran

Om du vill hämta statusen för en kunds direkta godkännande av Microsofts kund avtal, skapar du en REST-begäran för att hämta [DirectSignedCustomerAgreementStatus](./customer-agreement-direct-sign-status-resource.md) för kunden.

### <a name="request-syntax"></a>Syntax för begäran

Använd följande syntax för begäran:

| Metod | URI för förfrågan                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | [*\{ BASEURL \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/directSignedMicrosoftCustomerAgreementStatus http/1.1 |

### <a name="uri-parameters"></a>URI-parametrar

Du kan använda följande URI-parametrar med din begäran:

| Namn             | Typ | Obligatorisk | Beskrivning                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| kund-ID för klient organisation | GUID | Ja | Värdet är en GUID-formaterad **CustomerTenantId** som gör att du kan ange klient-ID för en kund. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

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

Om det lyckas returnerar den här metoden en [ **DirectSignedCustomerAgreementStatus** -resurs](./customer-agreement-direct-sign-status-resource.md) i svars texten.

Resursen har en **isSigned** -egenskap som anger kundens direkta signerings status (direkt godkännande).

- Värdet **True** anger att avtalet har signerats (accepterats) direkt av kunden.

- Värdet **false** anger att avtalet *inte* har signerats (accepterats) direkt av kunden.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.

Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Length: 20
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b

{"isSigned":true}
```
