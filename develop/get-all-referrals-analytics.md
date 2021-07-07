---
title: Hämta all information om hänvisningsanalys
description: Så här hämtar du all referensanalysinformation.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: Kim-Davis
ms.author: kimnich
ms.openlocfilehash: 7deda4098ceb9eb4e1ee75056c53c754618bf3e2
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760614"
---
# <a name="get-all-referrals-analytics-information"></a>Hämta all information om hänvisningsanalys

**Gäller för**: Partner Center-| PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Hur du hämtar all referensanalysinformation för dina kunder.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med användarautentiseringsuppgifter.

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod  | URI för förfrågan |
|---------|-------------|
| **Få** | [*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/referrals HTTP/1.1 |

### <a name="uri-parameters"></a>URI-parametrar

| Parameter | Typ | Beskrivning |
|-----------|------|-------------|
| filter | sträng | Returnerar data som matchar filtervillkoret.</br> **Exempel:**</br>  `.../referrals?filter=field eq 'value'` |
| groupby | sträng | Stöder både termer och datum. Kortslutningslogik för att begränsa antalet bucketar.</br> **Exempel:**</br>  `.../referrals?groupby=termField1,dateField1,termField2` |
| aggregationLevel | sträng | Parametern *aggregationLevel* kräver en *groupby*. Parametern *aggregationLevel* gäller för alla datumfält som finns i *groupby*.</br> **Exempel:**</br> `.../referrals?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
| top | sträng | Sidgränsen är 10 000. Tar ett värde som är mindre än 10 000.</br> **Exempel:**</br> `.../referrals?top=100`</br> |
| hoppa över | sträng | Antal rader som ska hoppas över.</br> **Exempel:**</br>  `.../referrals?top=100&skip=100` |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

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

Om det lyckas innehåller svarstexten en samling [referensresurser.](partner-center-analytics-resources.md#referrals-resource)

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder.](error-codes.md)

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
