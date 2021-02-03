---
title: Hämta en självbetjäningsprincip efter ID
description: Hämtar den angivna självbetjänings principen med hjälp av dess ID.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: ec01d0d9b7c3858cdacf1dbaad3b2b0bb7b6a1a4
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769087"
---
# <a name="get-a-self-serve-policy-by-id"></a>Hämta en självbetjäningsprincip efter ID

**Gäller för**

- Partnercenter

Hämtar den angivna självbetjänings principen med hjälp av dess ID.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med app + användarautentiseringsuppgifter.
- Ett självbetjänings princip-ID.

## <a name="examples"></a>Exempel


## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST-begäran

**Syntax för begäran**

| Metod  | URI för förfrågan                                                                   |
|---------|-------------------------------------------------------------------------------|
| **TA** | [*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{ID} http/1.1 |

**URI-parameter**

Använd följande Sök vägs parametrar för att hämta den angivna produkten.

| Namn                       | Typ         | Obligatorisk | Beskrivning                                                     |
|----------------------------|--------------|----------|-----------------------------------------------------------------|
| **SelfServePolicy-ID**     | **nollängd**   | Yes      | En sträng som identifierar den självbetjänings principen.                 |

**Begärandehuvuden**

- Se [rubriker](headers.md) för mer information.

**Brödtext i begäran**

Inga.

**Exempel på begäran**

```http
GET https://api.partnercenter.microsoft.com/v1/SelfServePolicy/634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415 HTTP/1.1
Authorization: Bearer  <token>
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a>REST-svar

Om det lyckas innehåller svars texten en [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) -resurs.

**Slutförda svar och felkoder**

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [fel koder för partner Center](error-codes.md).

Den här metoden returnerar följande fel koder:

| HTTP-statuskod     | Felkod   | Description                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| 404                  | 600039       | Det gick inte att hitta principen för självbetjäning.                                                     |

**Exempel på svar**

```http
HTTP/1.1 200 OK
Content-Length: 1918
Content-Type: application/json
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
Date: Tue, 23 Jan 2018 23:13:01 GMT

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