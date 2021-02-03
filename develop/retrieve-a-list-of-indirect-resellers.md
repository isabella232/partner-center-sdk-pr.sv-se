---
title: Hämta en lista över indirekta återförsäljare
description: Hämta en lista över den inloggade partnerns indirekta åter försäljare.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e53237b97fa26d3a987f0ee7de491084b596af4a
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769786"
---
# <a name="retrieve-a-list-of-indirect-resellers"></a>Hämta en lista över indirekta återförsäljare

**Gäller för**

- Partnercenter

Hämta en lista över den inloggade partnerns indirekta åter försäljare.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.

## <a name="c"></a>C\#

Om du vill hämta en lista över indirekta åter försäljare med vilka den inloggade partnern har en relation, hämtar du först ett gränssnitt till Relations samlings åtgärder från egenskapen [**partnerOperations. Relationships**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) . Anropa sedan metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.get) eller [**get \_ async**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.getasync) , och skicka en medlem i [**PartnerRelationshipType**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype) -uppräkningen för att identifiera Relations typen. Om du vill hämta indirekta åter försäljare måste du använda IsIndirectCloudSolutionProviderOf.

``` csharp
// IAggregatePartner partnerOperations;

var indirectResellers = partnerOperations.Relationships.Get(PartnerRelationshipType.IsIndirectCloudSolutionProviderOf);
```

**Exempel**: [konsol test app](console-test-app.md)-**projekt**: Partner Center SDK-exempel **klass**: GetIndirectResellers.CS

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod  | URI för förfrågan                                                                                                                |
|---------|----------------------------------------------------------------------------------------------------------------------------|
| **TA** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Relationships? Relations \_ typ = IsIndirectCloudSolutionProviderOf http/1.1 |

### <a name="uri-parameter"></a>URI-parameter

Använd följande frågeparameter för att identifiera Relations typen.

| Namn               | Typ    | Obligatorisk  | Beskrivning                         |
|--------------------|---------|-----------|-------------------------------------|
| relationship_type  | sträng  | Yes       | Värdet är sträng representationen av ett av de medlems namn som finns i [PartnerRelationshipType](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype).<br/><br/> Om partnern är inloggad som en leverantör och du vill hämta en lista över de indirekta åter försäljare med vilka de har upprättat en relation använder du IsIndirectCloudSolutionProviderOf.<br/><br/> Om partnern är inloggad som en åter försäljare och du vill hämta en lista över de indirekta leverantörer med vilka de har upprättat en relation använder du IsIndirectResellerOf.    |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/v1/relationships?relationship_type=IsIndirectCloudSolutionProviderOf HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 144391a4-fb06-41ae-b684-3308ce4706bd
MS-CorrelationId: 72524ef8-81aa-4141-a049-45a4fece5d84
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
Content-Length: 298
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 72524ef8-81aa-4141-a049-45a4fece5d84
MS-RequestId: 144391a4-fb06-41ae-b684-3308ce4706bd
MS-CV: b21Ll1miM0yFMPQQ.0
MS-ServerId: 030020643
Date: Wed, 05 Apr 2017 21:08:44 GMT

{
    "totalCount": 2,
    "items": [{
            "id": "484e548c-f5f3-4528-93a9-c16c6373cb59",
            "name": "First Up Consultants",
            "relationshipType": "is_indirect_cloud_solution_provider_of",
            "state": "Active",
            "mpnId": "4847383",
            "location": "US",
            "attributes": {
                "objectType": "PartnerRelationship"
            }
        }, {
            "id": "b01b1487-b36e-4e6d-9b5e-0b58974c4b28",
            "name": "ReleCloud",
            "relationshipType": "is_indirect_cloud_solution_provider_of",
            "state": "Active",
            "mpnId": "4847433",
            "location": "BR",
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