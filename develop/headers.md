---
title: Partnercenter – REST-huvuden
description: Läs mer om HTTP REST-begärandehuvuden och REST-svarshuvuden som stöds av Partner Center REST API.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9c9483e761465be1a60003dcd44cef46af3e99634d99d804d43d101d6b8ef700
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115993833"
---
# <a name="partner-center-rest-and-response-headers-supported-by-the-partner-center-rest-api"></a>PartnerCenter REST- och svarshuvuden som stöds av Partnercenter-REST API 

**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Följande HTTP-begärande- och svarshuvuden stöds av PartnerCenter-REST API. Alla API-anrop accepterar inte alla huvuden.

## <a name="rest-request-headers"></a>REST-begärandehuvuden

Följande HTTP-begärandehuvuden stöds av PartnerCenter-REST API.

| Huvud                       | Description                                                                                                                                                                                                                                                                            | Värdetyp |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| Auktorisering:               | Krävs. Auktoriseringstoken i formuläret &lt; Bearer-token &gt; .                                                                                                                                                                                                                    | sträng     |
| Acceptera:                      | Anger begäran och svarstyp, "application/json".                                                                                                                                                                                                                           | sträng     |
| MS-RequestId:                | En unik identifierare för anropet som används för att säkerställa id-potens. Om det finns en tidsgräns bör återförsöksanropet innehålla samma värde. När du får ett svar (lyckat eller affärsfel) ska värdet återställas för nästa anrop.                                            | GUID       |
| MS-CorrelationId:            | En unik identifierare för anropet, användbart i loggar och nätverksspårningar för felsökning av fel. Värdet ska återställas för varje anrop. Alla åtgärder bör innehålla det här huvudet. Mer information finns i Informationen om korrelations-ID [i Testa och felsöka](test-and-debug.md). | GUID       |
| MS-Contract-Version:         | Krävs. Anger vilken version av API:et som begärdes. vanligtvis api-version: v1 om inget annat anges i [avsnittet](scenarios.md) Scenarier.                                                                                                                                  | sträng     |
| If-Match:                    | Används för samtidighetskontroll. Vissa API-anrop kräver att ETag skickas via If-Match sidhuvud. ETag finns vanligtvis på resursen och kräver därför GET-ting den senaste. Mer information finns i ETag-informationen i [Testa och felsöka](test-and-debug.md).                | sträng     |
| MS-PartnerCenter-Application | Valfritt. Anger namnet på det program som använder PartnerCenter-REST API.                                                                                                                                                                                             | sträng     |
| X-språk:                    | Valfritt. Anger det språk som priserna returneras på. Standardvärdet är "en-US". En lista över värden som stöds finns i [Språk och språk som stöds i Partnercenter.](partner-center-supported-languages-and-locales.md)                                                                                                                                                                                                  | sträng     |

## <a name="rest-response-headers"></a>REST-svarshuvuden

Följande HTTP-svarshuvuden kan returneras av Partner Center-REST API.

| Huvud            | Description                                                                                                                                                                                                                                 | Värdetyp |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| Acceptera:           | Anger begäran och svarstyp, "application/json".                                                                                                                                                                                | sträng     |
| MS-RequestId:     | En unik identifierare för anropet som används för att säkerställa id-potens. Om det finns en tidsgräns bör återförsöksanropet innehålla samma värde. När du får ett svar (lyckat eller affärsfel) ska värdet återställas för nästa anrop. | GUID       |
| MS-CorrelationId: | En unik identifierare för anropet. Det här värdet är användbart för felsökning av loggar och nätverksspårningar för att hitta felet. Värdet ska återställas för varje anrop. Alla åtgärder bör innehålla det här huvudet.                                                       | GUID       |
