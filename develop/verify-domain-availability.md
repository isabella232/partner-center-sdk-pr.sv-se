---
title: Verifiera domäntillgänglighet
description: Så här avgör du om en domän är tillgänglig för användning.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 84edb5b7510642ec44dad3d4f92349e40eb10b24
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769606"
---
# <a name="verify-domain-availability"></a>Verifiera domäntillgänglighet

**Gäller för**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Så här avgör du om en domän är tillgänglig för användning.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.

- En domän (till exempel `contoso.onmicrosoft.com` ).

## <a name="c"></a>C\#

För att kontrol lera om en domän är tillgänglig måste du först anropa [**IAggregatePartner. Domains**](/dotnet/api/microsoft.store.partnercenter.ipartner.domains) för att få ett gränssnitt till domän åtgärder. Anropa sedan metoden [**ByDomain**](/dotnet/api/microsoft.store.partnercenter.domains.idomaincollection.bydomain) med domänen för att kontrol lera. Den här metoden hämtar ett gränssnitt till de åtgärder som är tillgängliga för en speciell domän. Anropa slutligen metoden [**exists**](/dotnet/api/microsoft.store.partnercenter.domains.idomain.exists) för att se om domänen redan finns.

``` csharp
// IAggregatePartner partnerOperations;
// const string domain = "contoso.onmicrosoft.com";

bool result = partnerOperations.Domains.ByDomain(domain).Exists();
```

**Exempel**: [konsol test app](console-test-app.md). **Projekt**: Partner Center SDK-exempel **klass**: CheckDomainAvailability.CS

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod   | URI för förfrågan                                                              |
|----------|--------------------------------------------------------------------------|
| **FÖRETAGETS** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Domains/{Domain} http/1.1 |

### <a name="uri-parameter"></a>URI-parameter

Använd följande frågeparameter för att kontrol lera domänens tillgänglighet.

| Namn       | Typ       | Obligatorisk | Beskrivning                                   |
|------------|------------|----------|-----------------------------------------------|
| **domänsuffix** | **nollängd** | Y        | En sträng som identifierar den domän som ska kontrol leras. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

Inget

### <a name="request-example"></a>Exempel på begäran

```http
HEAD https://api.partnercenter.microsoft.com/v1/domains/contoso.onmicrosoft.com HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: cf5b00d6-9240-431c-a973-cc06c904e5bf
MS-CorrelationId: ec57501a-a4c3-45ee-ab2b-da4250545fc9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST-svar

Om domänen finns är den inte tillgänglig för användning och svars status koden 200 OK returneras. Om domänen inte hittas, är den tillgänglig för användning och en svars status kod 404 som inte hittas returneras.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).

### <a name="response-example-for-when-the-domain-is-already-in-use"></a>Svars exempel för när domänen redan används

```http
HTTP/1.1 200 OK
Content-Length: 0
MS-CorrelationId: ec57501a-a4c3-45ee-ab2b-da4250545fc9
MS-RequestId: cf5b00d6-9240-431c-a973-cc06c904e5bf
MS-CV: 7UXAHds8J0mNUCSp.0
MS-ServerId: 201022015
Date: Tue, 31 Jan 2017 22:22:35 GMT
```

### <a name="response-example-for-when-the-domain-is-available"></a>Svars exempel för när domänen är tillgänglig

```http
HTTP/1.1 404 Not Found
Content-Length: 0
MS-CorrelationId: 54770745-17f0-433c-bd7b-0265e5b38f98
MS-RequestId: 1169a4cd-3be7-4e29-9cb3-0f78ffa2e91e
MS-CV: RRmc+bEw9U2e97CC.0
MS-ServerId: 202010406
Date: Tue, 31 Jan 2017 22:36:01 GMT
```
