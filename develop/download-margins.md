---
title: Hämtar en lista med marginaler i kommaavgränsat format för en viss partner.
description: Hämtar en lista med marginaler i kommaavgränsat format för en viss partner.
ms.date: 09/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: 6328ab962b2f210cee76b585ce2cf883c41eac3f
ms.sourcegitcommit: deb3207935fb5a74df515ed0fd4ffec90e6a143c
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/07/2021
ms.locfileid: "129646412"
---
# <a name="download-margins"></a>Ladda ned marginaler


**Gäller för:** Partnercenter 

**Lämpliga roller:** Globala | Administratörsagent

Partner kan hämta en lista över aktiva marginaler för en viss partner. Den här metoden returnerar marginaler baserat på partnern och tillgängliga start- och slutdatum. Nedladdningsmarginaler returnerar data i ett kommaavgränsat format.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md) Det här scenariot stöder autentisering med både fristående app- och app+användarautentiseringsuppgifter.


## <a name="rest-request"></a>REST-begäran
[GET] /v1/marginaler

### <a name="request-syntax"></a>Begärandesyntax

| Metod   | URI för förfrågan                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| **FÅ**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/margins/download HTTP/1.1 |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

Ingen

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/v1/margins/download HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden prislistan som en filström som a.csv fil

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad och mer felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och fler parametrar. En fullständig lista finns i [Felkoder.](error-codes.md)

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Length: 138
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
Date: Fri, 26 Feb 2021 20:42:26 GMT

"id","productId","publisherName","productTitle","productType"","marginPercentage","startDate","endDate","status","statusDate"
"97620c21cc32_97cdce68-cce4-42aa-9410-233fd0269502","DZH318Z08L40","Market Place Test","Software As A Service Support Preview App","SaaS","10.0","2021-08-04T23:16:22.4736653Z","2022-03-31T23:59:59Z","live","2021-08-04T23:16:22.4736653Z"

```
