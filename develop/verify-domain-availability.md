---
title: Verifiera domäntillgänglighet
description: Så här avgör du om en domän är tillgänglig för användning.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3515216127219908aeefb2e070b138e75dc1f0e72b1f57f07f1dbff65ab79558
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989057"
---
# <a name="verify-domain-availability"></a>Verifiera domäntillgänglighet

**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Så här avgör du om en domän är tillgänglig för användning.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.

- En domän (till exempel `contoso.onmicrosoft.com` ).

## <a name="c"></a>C\#

Om du vill kontrollera om en domän är tillgänglig anropar du [**först IAggregatePartner.Domains för**](/dotnet/api/microsoft.store.partnercenter.ipartner.domains) att hämta ett gränssnitt till domänåtgärder. Anropa sedan [**metoden ByDomain**](/dotnet/api/microsoft.store.partnercenter.domains.idomaincollection.bydomain) med domänen för att kontrollera. Den här metoden hämtar ett gränssnitt för de åtgärder som är tillgängliga för en specifik domän. Anropa slutligen metoden [**Exists**](/dotnet/api/microsoft.store.partnercenter.domains.idomain.exists) för att se om domänen redan finns.

``` csharp
// IAggregatePartner partnerOperations;
// const string domain = "contoso.onmicrosoft.com";

bool result = partnerOperations.Domains.ByDomain(domain).Exists();
```

**Exempel:** [Konsoltestapp](console-test-app.md). **Project:** Partnercenter-SDK **exempelklass:** CheckDomainAvailability.cs

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod   | URI för förfrågan                                                              |
|----------|--------------------------------------------------------------------------|
| **Huvud** | [*{baseURL}*](partner-center-rest-urls.md)/v1/domains/{domain} HTTP/1.1 |

### <a name="uri-parameter"></a>URI-parameter

Använd följande frågeparameter för att verifiera domänens tillgänglighet.

| Namn       | Typ       | Obligatorisk | Beskrivning                                   |
|------------|------------|----------|-----------------------------------------------|
| **Domän** | **sträng** | Y        | En sträng som identifierar domänen som ska kontrolleras. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

Ingen

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

Om domänen finns är den inte tillgänglig för användning och svarsstatuskoden 200 OK returneras. Om domänen inte hittas är den tillgänglig för användning och svarsstatuskoden 404 Hittades inte returneras.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)

### <a name="response-example-for-when-the-domain-is-already-in-use"></a>Svarsexempel för när domänen redan används

```http
HTTP/1.1 200 OK
Content-Length: 0
MS-CorrelationId: ec57501a-a4c3-45ee-ab2b-da4250545fc9
MS-RequestId: cf5b00d6-9240-431c-a973-cc06c904e5bf
MS-CV: 7UXAHds8J0mNUCSp.0
MS-ServerId: 201022015
Date: Tue, 31 Jan 2017 22:22:35 GMT
```

### <a name="response-example-for-when-the-domain-is-available"></a>Svarsexempel för när domänen är tillgänglig

```http
HTTP/1.1 404 Not Found
Content-Length: 0
MS-CorrelationId: 54770745-17f0-433c-bd7b-0265e5b38f98
MS-RequestId: 1169a4cd-3be7-4e29-9cb3-0f78ffa2e91e
MS-CV: RRmc+bEw9U2e97CC.0
MS-ServerId: 202010406
Date: Tue, 31 Jan 2017 22:36:01 GMT
```
