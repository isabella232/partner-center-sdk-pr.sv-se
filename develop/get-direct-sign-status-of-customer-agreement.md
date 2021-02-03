---
title: Hämta kundens direkta signerings status för Microsofts kund avtal.
description: Du kan använda DirectSignedCustomerAgreementStatus-resursen för att hämta statusen för en kunds direkta signering (direkt godkännande) för Microsofts kund avtal.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 3f1deb20a18bc6e7133cac91db528f2d1ad694e2
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768739"
---
# <a name="get-the-status-of-a-customers-direct-signing-direct-acceptance-of-microsoft-customer-agreement"></a>Hämta statusen för en kunds direkta signering (direkt godkännande) för Microsofts kund avtal

**Gäller för:**

- Partnercenter

**DirectSignedCustomerAgreementStatus** -resursen stöds för närvarande endast av Partner Center i det offentliga Microsoft-molnet.

Den här resursen är *inte tillämplig* för:

- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Den här artikeln förklarar hur du kan hämta statusen för en kunds direkta godkännande av Microsofts kund avtal.

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
| kund-ID för klient organisation | GUID | Yes | Värdet är en GUID-formaterad **CustomerTenantId** som gör att du kan ange klient-ID för en kund. |

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
