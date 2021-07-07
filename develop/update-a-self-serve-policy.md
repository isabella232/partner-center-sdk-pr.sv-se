---
title: Uppdatera en självbetjäningsprincip
description: Så här uppdaterar du en självbetjäningsprincip.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d94382e73fd2a79751fe5f8f8414df2befde584f
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445263"
---
# <a name="update-a-selfservepolicy"></a>Uppdatera en SelfServePolicy

Den här artikeln förklarar hur du uppdaterar en självbetjäningsprincip.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md) Det här scenariot stöder autentisering med autentiseringsuppgifter för program och användare.

## <a name="c"></a>C\#

Så här tar du bort en självbetjäningsprincip:

1. Anropa metoden [**IAggregatePartner.SelfServePolicies.ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) med entitetsidentifieraren för att hämta ett gränssnitt till åtgärder för principerna.

2. Anropa [**Put-**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.put) eller [**PutAsync-metoden**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.putasync) för att uppdatera självbetjäningsprincipen.

``` csharp
// IAggregatePartner partnerOperations;
SelfServePolicy policy;

// All the operations executed on this partner operation instance will share the same correlation identifier but will differ in request identifier
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// updates the self-serve policies
partnerOperations.SelfServePolicies.ById(policy.id).Put(policy);
```

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod   | URI för förfrågan                                                       |
|----------|-------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy HTTP/1.1 |

### <a name="request-headers"></a>Begärandehuvuden

- En begärandeidentifierare och korrelationsidentifierare krävs.
- Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

I den här tabellen beskrivs de obligatoriska egenskaperna i begärandetexten.

| Namn                              | Typ   | Beskrivning                                 |
|------------------------------------------------------------------|--------|---------------------------------------------|
| [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy)| objekt | Information om självbetjäningsprincipen. |

#### <a name="selfservepolicy"></a>SelfServePolicy

I den här tabellen beskrivs de minsta obligatoriska fälten från [SelfServePolicy-resursen](self-serve-policy-resources.md#selfservepolicy) som krävs för att skapa en ny självbetjäningsprincip.

| Egenskap              | Typ             | Beskrivning                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | sträng           | En principidentifierare med självbetjäning som tillhandahålls när självbetjäningsprincipen har skapats.     |
| SelfServeEntity       | SelfServeEntity  | Entiteten med självbetjäning som beviljas åtkomst.                                                     |
| Beviljaren               | Beviljaren          | Den beviljande som beviljar åtkomst.                                                                    |
| Behörigheter           | Behörighetsmatris| En matris med [behörighetsresurser.](self-serve-policy-resources.md#permission)                                                      |
| Etag                  | sträng           | The Etag.                                                                                               |


### <a name="request-example"></a>Exempel på begäran

```http
PUT https://api.partnercenter.microsoft.com/v1/SelfServePolicy HTTP/1.1
Authorization: Bearer <token>
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive

{
    "id": "634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415",
    "selfServeEntity": {
        "selfServeEntityType": "customer",
        "tenantID": "0431a72c-7d8a-4393-b25e-ef63f5efb415"
    },
    "grantor": {
        "grantorType": "billToPartner",
        "tenantID": "634f6379-ad54-449b-9821-564f737158ab"
    },
    "permissions": [{
        "resource": "AzureReservedInstances",
        "action": "Purchase"
    }],
    "attributes": {
        "etag": "\"933523d1-3f63-4fc3-8789-5e21c02cdaed\"",
        "objectType": "SelfServePolicy"
    }
}
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar detta API en [SelfServePolicy-resurs](self-serve-policy-resources.md#selfservepolicy) för den uppdaterade självbetjäningsprincipen.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)

Den här metoden returnerar följande felkoder:

| HTTP-statuskod     | Felkod   | Beskrivning                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| 404                  | 600039       | Självbetjäningsprincipen hittades inte                                            |
| 404                  | 600040       | Principidentifieraren för självbetjäning är felaktig                                  |


### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 Ok
Content-Length: 834
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
Date: Tue, 14 Feb 2017 20:06:02 GMT

{
    "id": "634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415",
    "selfServeEntity": {
        "selfServeEntityType": "customer",
        "tenantID": "0431a72c-7d8a-4393-b25e-ef63f5efb415"
    },
    "grantor": {
        "grantorType": "billToPartner",
        "tenantID": "634f6379-ad54-449b-9821-564f737158ab"
    },
    "permissions": [{
        "resource": "AzureReservedInstances",
        "action": "Purchase"
    }],
    "attributes": {
        "etag": "\"1ec98034-a249-46f4-b9dd-9cd464fb5e47\"",
        "objectType": "SelfServePolicy"
    }
}
```
