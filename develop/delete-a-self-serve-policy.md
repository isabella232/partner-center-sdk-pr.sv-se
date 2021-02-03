---
title: Ta bort en princip för självbetjäning
description: Så här tar du bort en princip för självbetjäning.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3450145d6daf2ffca5e2886245e592406cb0886d
ms.sourcegitcommit: 01e75175077611da92175c777a440a594fb05797
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/08/2020
ms.locfileid: "97770225"
---
# <a name="delete-a-selfservepolicy"></a>Ta bort en SelfServePolicy

**Gäller för:**

- Partnercenter

I det här avsnittet beskrivs hur du uppdaterar en princip för självbetjäning.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med program-och användarautentiseringsuppgifter.

## <a name="c"></a>C\#

Så här tar du bort en princip för självbetjäning:

1. Anropa metoden [**IAggregatePartner. SelfServePolicies. ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) med enhets-ID: n för att hämta ett gränssnitt till åtgärder i principerna.

2. Anropa [**Delete**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.delete) -eller [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.deleteasync) -metoden för att ta bort principen för självbetjäning.

``` csharp
// IAggregatePartner partnerOperations;
string policyId;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// deletes the self-serve policies
partnerOperations.SelfServePolicies.ById(policyId).Delete();
```

Ett exempel finns i följande avsnitt:

- Exempel: [konsol test app](console-test-app.md)
- Projekt: **PartnerSDK. FeatureSamples**
- Klass: **DeleteSelfServePolicies.cs**

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod  | URI för förfrågan                                                                   |
|---------|-------------------------------------------------------------------------------|
| **TA bort** | [*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{ID} http/1.1 |

**URI-parameter**

Använd följande Sök vägs parametrar för att hämta den angivna produkten.

| Namn                       | Typ         | Obligatorisk | Beskrivning                                                     |
|----------------------------|--------------|----------|-----------------------------------------------------------------|
| **SelfServePolicy-ID**     | **nollängd**   | Yes      | En sträng som identifierar principen för självbetjäning.                 |

### <a name="request-headers"></a>Begärandehuvuden

- ID för begäran och korrelations-ID krävs.
- Mer information finns i [partner Center rest-rubriker](headers.md) .

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-example"></a>Exempel på begäran

```http
DELETE https://api.partnercenter.microsoft.com/v1/SelfServePolicy/634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 789
Connection: Keep-Alive

```

## <a name="rest-response"></a>REST-svar

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 204 deleted
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
Date: Tue, 14 Feb 2017 20:06:02 GMT

```
