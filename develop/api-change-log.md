---
title: Partnercenter – REST API-ändringslogg
description: Den här sidan visar ändringar i Partner Center REST API:er
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.topic: reference
ms.date: 12/15/2020
ms.openlocfilehash: f74f59969bf8d73c6e6e8b39900a53c337a2af715c168b59009792beddf43159
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115993290"
---
# <a name="december-2020-changes-to-partner-center-rest-apis"></a>December 2020-ändringar i Partner Center REST API:er

Kontrollera här om det finns ändringar i Partner Center REST API:er.

## <a name="enhancements-to-education-pricing-eligibility-apis"></a>Förbättringar av API:er för utbildningsprisberättigade



### <a name="what-has-changed"></a>Vad har ändrats?

Partner Center-API:et har för närvarande GET- och PUT-kvalificeringar för att verifiera education-kundernas berättigande. Det kommer inte att ske några ändringar i GET-kvalificerings-API:et. Vi har dock lagt till ett returfall i PUT-kvalificerings-API:et.

- GET – ändras inte.
- PUT – returfall läggs till.

Dessa API:er dras tillbaka i slutet av februari 2021 för att ersättas med nya API:er enligt beskrivningen nedan.

### <a name="scenarios-impacted"></a>Scenarier som påverkas:

Kundberättigande för utbildningspriser för utvalda SKU:er

### <a name="detail-descriptions"></a>Informationsbeskrivningar

Två nya API:er för GET- och POST-kvalificering kommer att introduceras. De nya API:erna kommer att använda **kvalificering**, inte **kvalificering.** API:erna kommer att vara tillgängliga för testning i FY21 Q2.

#### <a name="get-qualifications"></a>GET-kvalificeringar

```http
GET {customer_id}/qualifications
```

#### <a name="response-example"></a>Svarsexempel:

```json
{
  "Qualification": "Education",
  "VettingStatus": "Denied",
  "VettingReason": "Not an education customer",
  "VettingCreatedDate": "07/09/2020: 00:00:00" //UTC
}
```

#### <a name="response-fields"></a>Svarsfält: 

- VettingStatus-värden: Godkänd, Nekad, InReview osv.

- VettingReason-värden:
   - Inte utbildningskund
   - Inte längre utbildningskund
   - Inte utbildningskund – efter granskning
   - Begränsad är en utbildningskund
   - Inte en academic-domän
   - Inte ett kvalificerande bibliotek
   - Inte berättigad Till en
 
#### <a name="post-qualifications"></a>POST-kvalificeringar

```http
POST {customer_id}/qualifications
    [
            "Qualification": "Education"
    ]
```

#### <a name="response-example"></a>Svarsexempel:

```JSON
{
  "Qualification": "Education",
  "VettingStatus": "InReview",
  "VettingCreatedDate": "07/09/2020: 00:00:00" //UTC
}
```

## <a name="next-steps"></a>Nästa steg

[Partnercenter – REST API-referens](partner-center-rest-api-reference.md)
