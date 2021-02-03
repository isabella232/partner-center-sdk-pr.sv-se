---
title: Hämta indirekta återförsäljare för en kund
description: Så här hämtar du en lista över de indirekta åter försäljare som har en relation med en angiven kund.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: d69abf9530548f110820ca04fefb698e0e37556c
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769690"
---
# <a name="get-indirect-resellers-of-a-customer"></a>Hämta indirekta återförsäljare för en kund

**Gäller för**

- Partnercenter

Så här hämtar du en lista över de indirekta åter försäljare som har en relation med en angiven kund.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Om du vill hämta en lista över indirekta åter försäljare som den angivna kunden har en relation till får du först ett gränssnitt till kund samlings åtgärder för den specifika kunden från [**partnerOperations. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) -egenskapen genom att ange kund-ID: t för att identifiera kunden. Anropa sedan [**relationerna. Hämta**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.get) eller [**Hämta en \_ asynkron**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.getasync) metod för att hämta listan över indirekta åter försäljare.

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

 var indirectResellers = partnerOperations.Customers[customerId].Relationships.Get();
```

**Exempel**: [konsol test app](console-test-app.md)-**projekt**: Partner Center SDK-exempel **klass**: GetIndirectResellersOfCustomer.CS

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod  | URI för förfrågan                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| **TA** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Relationships http/1.1 |

### <a name="uri-parameter"></a>URI-parameter

Använd följande Sök vägs parameter för att identifiera kunden.

| Namn        | Typ   | Obligatorisk | Beskrivning                                           |
|-------------|--------|----------|-------------------------------------------------------|
| kund-ID | sträng | Yes      | En GUID-formaterad sträng som identifierar kunden. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/v1/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/relationships HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c9251710-5a30-4cd3-891a-c42d550af9a8
MS-CorrelationId: a96f326c-a392-44f4-bcfe-43152a756ba8
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST-svar

Om det lyckas innehåller svars texten en samling [PartnerRelationship](relationships-resources.md) -resurser för att identifiera åter försäljarna.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [fel koder för partner Center](error-codes.md).

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Length: 264
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a96f326c-a392-44f4-bcfe-43152a756ba8
MS-RequestId: c9251710-5a30-4cd3-891a-c42d550af9a8
MS-CV: plJP3ufU0UqXMeuh.0
MS-ServerId: 020021921
Date: Fri, 07 Apr 2017 23:42:11 GMT

{
    "totalCount": 1,
    "items": [{
            "id": "484e548c-f5f3-4528-93a9-c16c6373cb59",
            "name": "First Up Consultants",
            "relationshipType": "is_indirect_cloud_solution_provider_of",
            "mpnId": "4847383",
            "attributes": {
                "objectType": "PartnerRelationship"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
