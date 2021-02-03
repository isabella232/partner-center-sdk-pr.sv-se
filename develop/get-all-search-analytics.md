---
title: Hämta all information om sökanalys
description: Hämta all Sök analys information.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 967f8d0ed2d276e0f68a047204b64d83dc69da95
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768757"
---
# <a name="get-all-search-analytics-information"></a>Hämta all information om sökanalys

**Gäller för**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Så här hämtar du all Sök analys information för dina kunder.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med användarautentiseringsuppgifter.

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod  | URI för förfrågan |
|---------|-------------|
| **TA** | [*\{ BASEURL \}*](partner-center-rest-urls.md)/partner/v1/Analytics/search http/1.1 |

### <a name="uri-parameters"></a>URI-parametrar

|    Parameter     |  Typ  |                                                                                                                   Description                                                                                                                    |
|------------------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      filter      | sträng |                                                                     Returnerar data som matchar filter villkoret. </br> **Exempel:**</br> `.../search?filter=field eq 'value'`                                                                     |
|     groupby      | sträng |                                         Har stöd för både villkor och datum. Kort krets logik för att begränsa antalet buckets. </br> **Exempel:**</br> `.../search?groupby=termField1,dateField1,termField2`                                         |
| aggregationLevel | sträng | Parametern *aggregationLevel* kräver en *groupby*. Parametern *aggregationLevel* gäller för alla datum fält som finns i *groupby*. </br> **Exempel:**</br>  `.../search?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
|       top        | sträng |                                                                     Sid gränsen är 10000. Tar ett värde som är mindre än 10000.  </br> **Exempel:**</br>  `.../search?top=100`                                                                     |
|       hoppa över       | sträng |                                                                                  Antal rader som ska hoppas över. </br> **Exempel:**</br> `.../search?top=100&skip=100`                                                                                   |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/search HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>REST-svar

Om det lyckas innehåller svars texten en samling [Sök](partner-center-analytics-resources.md#search-resource) resurser.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [felkoder](error-codes.md).

### <a name="response-example"></a>Exempel på svar

```http
{
  "companyName": "my company",
  "contactButtonClicked": false,
  "keywordCountry": null,
  "detailsViewed": true,
  "keywordIndustryFocus": null,
  "mpnId": 2604568,
  "partnerMarket": "CN",
  "keywordProduct": null,
  "referralSubmitted": false,
  "searchDate": "2018-05-30",
  "keywordSearchText": " my company"
}
```

## <a name="see-also"></a>Se även

- [Partnercenter-analys – resurser](partner-center-analytics-resources.md)
