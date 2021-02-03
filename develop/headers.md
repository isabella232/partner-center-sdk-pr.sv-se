---
title: Partnercenter – REST-huvuden
description: Läs mer om HTTP REST-begärandehuvuden och REST-svarshuvuden som stöds av Partner Center REST API.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9f506c8c610c2584912c24453288d0f3578b84e3
ms.sourcegitcommit: 8a5c37376a29e29fe0002a980082d4acc6b91131
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/11/2020
ms.locfileid: "97769954"
---
# <a name="partner-center-rest-and-response-headers-supported-by-the-partner-center-rest-api"></a>Partner Center REST-och svars rubriker som stöds av Partner Center REST API 

**Gäller för**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Följande HTTP-begäran och svarshuvuden stöds av Partner Center REST API. Alla API-anrop accepterar inte alla huvuden.

## <a name="rest-request-headers"></a>REST-begärandehuvuden

Följande rubriker för HTTP-begäran stöds av Partner Center REST API.

| Huvud                       | Description                                                                                                                                                                                                                                                                            | Värdetyp |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| Auktorisering:               | Krävs. Autentiseringstoken i form Bearer- &lt; token &gt; .                                                                                                                                                                                                                    | sträng     |
| Godkänt                      | Anger begäran och svars typ, "Application/JSON".                                                                                                                                                                                                                           | sträng     |
| MS-RequestId:                | En unik identifierare för anropet som används för att säkerställa ID-potens. Om det finns en timeout bör återförsöket innehålla samma värde. När ett svar har tagits emot (lyckades eller Miss lyckas) måste värdet återställas för nästa anrop.                                            | GUID       |
| MS-CorrelationId:            | En unik identifierare för anropet, användbart i loggar och nätverks spår för fel söknings fel. Värdet måste återställas för varje anrop. Alla åtgärder ska innehålla denna rubrik. Mer information finns i korrelations-ID-information i [test-och fel sökning](test-and-debug.md). | GUID       |
| MS-Contract-version:         | Krävs. Anger versionen för det begärda API: et. allmänt API-version: v1 om inget annat anges i avsnittet [scenarier](scenarios.md) .                                                                                                                                  | sträng     |
| If-Match:                    | Används för concurrency-kontroll. Vissa API-anrop kräver att ETag skickas via If-Matchs huvudet. ETag är vanligt vis på resursen och kräver därför att du har den senaste versionen. Mer information finns i ETag-informationen i [test-och fel sökning](test-and-debug.md).                | sträng     |
| MS-PartnerCenter – program | Valfritt. Anger namnet på det program som använder REST API för partner Center.                                                                                                                                                                                             | sträng     |
| X-språkvariant:                    | Valfritt. Anger det språk som priserna returneras i. Standardvärdet är "en-US". En lista över vilka värden som stöds finns i [support språk som stöds av Partner Center och nationella inställningar](partner-center-supported-languages-and-locales.md).                                                                                                                                                                                                  | sträng     |

## <a name="rest-response-headers"></a>REST-svarshuvuden

Följande HTTP-svarshuvuden kan returneras av Partner Center REST API.

| Huvud            | Description                                                                                                                                                                                                                                 | Värdetyp |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| Godkänt           | Anger begäran och svars typ, "Application/JSON".                                                                                                                                                                                | sträng     |
| MS-RequestId:     | En unik identifierare för anropet som används för att säkerställa ID-potens. Om det finns en timeout bör återförsöket innehålla samma värde. När ett svar har tagits emot (lyckades eller Miss lyckas) måste värdet återställas för nästa anrop. | GUID       |
| MS-CorrelationId: | En unik identifierare för anropet. Det här värdet är användbart för fel sökning av loggar och nätverks spår för att hitta felet. Värdet måste återställas för varje anrop. Alla åtgärder ska innehålla denna rubrik.                                                       | GUID       |
