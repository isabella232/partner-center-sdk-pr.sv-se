---
title: Hämta all information om hänvisningsanalys
description: Så här hämtar du all information om referenser till analyser.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: Kim-Davis
ms.author: kimnich
ms.openlocfilehash: b470c59cecf8b214e6d90a244e928e5d15ebd3e0
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769081"
---
# <a name="get-all-referrals-analytics-information"></a>Hämta all information om hänvisningsanalys

**Gäller för**

- Partnercenter
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Så här hämtar du all referensinformations analys information för dina kunder.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med användarautentiseringsuppgifter.

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod  | URI för förfrågan |
|---------|-------------|
| **TA** | [*\{ BASEURL \}*](partner-center-rest-urls.md)/partner/v1/Analytics/Referrals http/1.1 |

### <a name="uri-parameters"></a>URI-parametrar

| Parameter | Typ | Description |
|-----------|------|-------------|
| filter | sträng | Returnerar data som matchar filter villkoret.</br> **Exempel:**</br>  `.../referrals?filter=field eq 'value'` |
| groupby | sträng | Har stöd för både villkor och datum. Kort krets logik för att begränsa antalet buckets.</br> **Exempel:**</br>  `.../referrals?groupby=termField1,dateField1,termField2` |
| aggregationLevel | sträng | Parametern *aggregationLevel* kräver en *groupby*. Parametern *aggregationLevel* gäller för alla datum fält som finns i *groupby*.</br> **Exempel:**</br> `.../referrals?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
| top | sträng | Sid gränsen är 10000. Tar ett värde som är mindre än 10000.</br> **Exempel:**</br> `.../referrals?top=100`</br> |
| hoppa över | sträng | Antal rader som ska hoppas över.</br> **Exempel:**</br>  `.../referrals?top=100&skip=100` |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/referrals HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>REST-svar

Om det lyckas innehåller svars texten en samling av [hänvisnings](partner-center-analytics-resources.md#referrals-resource) resurser.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [felkoder](error-codes.md).

### <a name="response-example"></a>Exempel på svar

```http
{
  "id": "112310",
  "status": "Accepted",
  "customerMarket": "US",
  "customerName": "Best Customer Ever",
  "customerOrgSize": "10to50employees",
  "acceptedDate": "2018-02-07T23:43:19",
  "acknowledgedDate": "2018-02-07T23:40:50",
  "archivedDate": null,
  "declinedDate": null,
  "expiredDate": null,
  "lostDate": null,
  "missedDate": null,
  "createdDate": "2018-02-04T23:08:59",
  "skippedDate": null,
  "wonDate": null,
  "partnerMarket": "US"
}
```

## <a name="see-also"></a>Se även

- [Partnercenter-analys – resurser](partner-center-analytics-resources.md)
