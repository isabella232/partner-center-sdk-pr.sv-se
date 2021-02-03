---
title: Ta bort ett användarkonto för en kund
description: Så här tar du bort ett befintligt användar konto för en kund.
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 77fc1a1c7264779ca549be8d52798e90c91138bb
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769381"
---
# <a name="delete-a-user-account-for-a-customer"></a>Ta bort ett användarkonto för en kund

**Gäller för:**

- Partnercenter

Den här artikeln förklarar hur du tar bort ett befintligt användar konto för en kund.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).

- Ett användar-ID. Om du inte har användar-ID, se [Hämta en lista över alla användar konton för en kund](get-a-list-of-all-user-accounts-for-a-customer.md).

## <a name="deleting-a-user-account"></a>Ta bort ett användar konto

När du tar bort ett användar konto är användar tillstånd inställt på **inaktiv** i trettio dagar. Efter trettio dagar rensas användar kontot och dess associerade data och blir oåterkalleliga.

Du kan [återställa ett borttaget användar konto för en kund](restore-a-user-for-a-customer.md) om det inaktiva kontot är inom trettio dagars period. Men när du återställer ett konto som har tagits bort och marker ATS som inaktivt returneras inte längre kontot som medlem i användar samlingen (till exempel när du [hämtar en lista över alla användar konton för en kund](get-a-list-of-all-user-accounts-for-a-customer.md)).

## <a name="c"></a>C\#

Ta bort ett befintligt kund användar konto:

1. Använd metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: t för att identifiera kunden.

2. Anropa metoden [**users. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) för att identifiera användaren.

3. Anropa [**Delete**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.delete) -metoden för att ta bort användaren och ange att användar statusen är inaktiv.

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string customerUserIdToDelete;

partnerOperations.Customers.ById(selectedCustomerId).Users.ById(customerUserIdToDelete).Delete();
```

**Exempel**: [konsol test app](console-test-app.md). **Projekt**: Partner Center SDK-exempel **klass**: DeleteCustomerUser.CS

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod     | URI för förfrågan                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| DELETE     | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Users/{User-ID} http/1.1 |

#### <a name="uri-parameters"></a>URI-parametrar

Använd följande frågeparametrar för att identifiera kunden och användaren.

| Namn                   | Typ     | Obligatorisk | Beskrivning                                                                                                               |
|------------------------|----------|----------|---------------------------------------------------------------------------------------------------------------------------|
| kund-ID för klient organisation     | GUID     | Y        | Värdet är ett GUID-formaterat **kund-ID** som gör det möjligt för åter försäljaren att filtrera resultaten för en bestämd kund. |
| användar-id                | GUID     | Y        | Värdet är ett GUID-formaterat **användar-ID** som tillhör ett enda användar konto.                                          |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-example"></a>Exempel på begäran

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f113b126-ec13-4baa-ab4d-67c245244971
MS-CorrelationId: 709c0b80-016c-4662-b29f-697fdf03e87a
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 0
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden en **204-innehålls** status kod.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 709c0b80-016c-4662-b29f-697fdf03e87a
MS-RequestId: f113b126-ec13-4baa-ab4d-67c245244971
MS-CV: 90KUJA7HKEaG8wHu.0
MS-ServerId: 101112616
Date: Tue, 24 Jan 2017 23:27:18 GMT
```
