---
title: Hämta en URL för relationsbegäran
description: Så här hämtar du en URL för relationsbegäran som ska skickas till en kund.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 62cf06de327f8f31e908a0cc38cff52ad5c62b036b95d195e0a8040c53a4e110
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996979"
---
# <a name="retrieve-a-relationship-request-url"></a>Hämta en URL för relationsbegäran

**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Tyskland

Så här hämtar du en URL för relationsbegäran som ska skickas till en kund.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md) Det här scenariot har endast stöd för autentisering med app- och användarautentiseringsuppgifter.

## <a name="c"></a>C\#

Om du vill hämta en URL för relationsbegäran [**använder du först IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) för att hämta ett gränssnitt till partnerns kundåtgärder. Använd sedan egenskapen [**RelationshipRequest för**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.relationshiprequest) att hämta ett gränssnitt till åtgärder för kundrelationsbegäran. Anropa slutligen metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.getasync) för att hämta URL:en.

``` csharp
// IAggregatePartner partnerOperations;

var customerRelationshipRequest = partnerOperations.Customers.RelationshipRequest.Get();
```

**Exempel:** [Konsoltestapp](console-test-app.md). **Project:** Partnercenter-SDK Samples **Class**: GetCustomerRelationshipRequest.cs

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod  | URI för förfrågan                                                                            |
|---------|----------------------------------------------------------------------------------------|
| **Få** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/relationshiprequests HTTP/1.1 |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

Ingen

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/v1/customers/relationshiprequests HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ee519026-4c67-4113-bec7-a38aca621bf0
MS-CorrelationId: 02971f0f-1029-47b2-9fdb-1932f0987470
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST-svar

Om det lyckas innehåller svaret [Objektet RelationshipRequest.](relationships-resources.md#relationshiprequest)

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Length: 196
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 02971f0f-1029-47b2-9fdb-1932f0987470
MS-RequestId: ee519026-4c67-4113-bec7-a38aca621bf0
MS-CV: jbYZRWjU3E262f8o.0
MS-ServerId: 030020643
Date: Fri, 19 May 2017 22:32:07 GMT

{
    "url": "https://admin.microsoft.com/Adminportal/Home?invType=ResellerRelationship&partnerId=3b33e682-00c3-41ee-9dd2-a548adf56438&msppId=0&DAP=false#/BillingAccounts/partner-invitation",
    "attributes": {
        "objectType": "RelationshipRequest"
    }
}
```
