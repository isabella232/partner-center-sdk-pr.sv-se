---
title: Hämta en lista över indirekta återförsäljare
description: Så här hämtar du en lista över den inloggade partnerns indirekta återförsäljare.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 901bf045d1de29744114bb58ed445f9eb17f70a4744786fd4617da9697e7c683
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996928"
---
# <a name="retrieve-a-list-of-indirect-resellers"></a>Hämta en lista över indirekta återförsäljare

Så här hämtar du en lista över den inloggade partnerns indirekta återförsäljare.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md) Det här scenariot har endast stöd för autentisering med app- och användarautentiseringsuppgifter.

## <a name="c"></a>C\#

Om du vill hämta en lista över indirekta återförsäljare med vilka den inloggade partnern har en relation hämtar du först ett gränssnitt till åtgärder för relationssamling från egenskapen [**partnerOperations.Relationships.**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) Anropa sedan metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.get) eller [**Get \_ Async**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.getasync) och skicka en medlem i [**Uppräkningen PartnerRelationshipType**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype) för att identifiera relationstypen. Om du vill hämta indirekta återförsäljare måste du använda IsIndirectCloudSolutionProviderOf.

``` csharp
// IAggregatePartner partnerOperations;

var indirectResellers = partnerOperations.Relationships.Get(PartnerRelationshipType.IsIndirectCloudSolutionProviderOf);
```

**Exempel:** [Konsoltestappen](console-test-app.md)**är Project:** Partnercenter-SDK **Exempelklass:** GetIndirectResellers.cs

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod  | URI för förfrågan                                                                                                                |
|---------|----------------------------------------------------------------------------------------------------------------------------|
| **Få** | [*{baseURL}*](partner-center-rest-urls.md)/v1/relationships?relationship \_ type=IsIndirectCloudSolutionProviderOf HTTP/1.1 |

### <a name="uri-parameter"></a>URI-parameter

Använd följande frågeparameter för att identifiera relationstypen.

| Namn               | Typ    | Obligatorisk  | Beskrivning                         |
|--------------------|---------|-----------|-------------------------------------|
| relationship_type  | sträng  | Yes       | Värdet är strängrepresentationen av ett av medlemsnamnen i [PartnerRelationshipType](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype).<br/><br/> Om partnern är inloggad som en provider och du vill hämta en lista över de indirekta återförsäljare som de har upprättat en relation med använder du IsIndirectCloudSolutionProviderOf.<br/><br/> Om partnern är inloggad som återförsäljare och du vill hämta en lista över de indirekta leverantörer som de har upprättat en relation med använder du IsIndirectResellerOf.    |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

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

Om det lyckas innehåller svarstexten en samling [PartnerRelationship-resurser](relationships-resources.md) för att identifiera återförsäljarna.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder i Partnercenter.](error-codes.md)

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