---
title: Uppdatera en princip för självbetjäning
description: Så här uppdaterar du en självbetjänings princip.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4d53ab8e5b8ef5b7be83360a3f43ec7791b2e3b4
ms.sourcegitcommit: 01e75175077611da92175c777a440a594fb05797
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/08/2020
ms.locfileid: "97770249"
---
# <a name="update-a-selfservepolicy"></a>Uppdatera en SelfServePolicy

**Gäller för:**

- Partnercenter

I det här avsnittet beskrivs hur du uppdaterar en princip för självbetjäning.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med program-och användarautentiseringsuppgifter.

## <a name="c"></a>C\#

Så här tar du bort en princip för självbetjäning:

1. Anropa metoden [**IAggregatePartner. SelfServePolicies. ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) med enhets-ID: n för att hämta ett gränssnitt till åtgärder i principerna.

2. Anropa metoden för att [**Skicka**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.put) eller [**PutAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.putasync) för att uppdatera principen för självbetjäning.

``` csharp
// IAggregatePartner partnerOperations;
SelfServePolicy policy;

// All the operations executed on this partner operation instance will share the same correlation identifier but will differ in request identifier
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// updates the self-serve policies
partnerOperations.SelfServePolicies.ById(policy.id).Put(policy);
```

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod   | URI för förfrågan                                                       |
|----------|-------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy http/1.1 |

### <a name="request-headers"></a>Begärandehuvuden

- ID för begäran och korrelation krävs.
- Mer information finns i [partner Center rest-rubriker](headers.md) .

### <a name="request-body"></a>Begärandetext

I den här tabellen beskrivs de egenskaper som krävs i begär ande texten.

| Namn                              | Typ   | Description                                 |
|------------------------------------------------------------------|--------|---------------------------------------------|
| [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy)| objekt | Den självbetjänings princip informationen. |

#### <a name="selfservepolicy"></a>SelfServePolicy

I den här tabellen beskrivs de minimi krav som krävs från den [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) -resurs som krävs för att skapa en ny princip för självbetjäning.

| Egenskap              | Typ             | Description                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | sträng           | Ett självbetjänings princip-ID som anges när du skapar en egen princip.     |
| SelfServeEntity       | SelfServeEntity  | Den självbetjänings enhet som beviljas åtkomst.                                                     |
| Den beviljande användaren               | Den beviljande användaren          | Den beviljande behörighet som beviljar åtkomst.                                                                    |
| Behörigheter           | Behörighets mat ris| En matris med [behörighets](self-serve-policy-resources.md#permission) resurser.                                                      |
| Etag                  | sträng           | Etag.                                                                                               |


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

Om det lyckas, returnerar detta API en [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) -resurs för den uppdaterade självbetjänings principen.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).

Den här metoden returnerar följande fel koder:

| HTTP-statuskod     | Felkod   | Description                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| 404                  | 600039       | Det gick inte att hitta principen för självbetjäning                                            |
| 404                  | 600040       | Den självbetjänings princip identifieraren är felaktig                                  |


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
