---
title: Partnercenter – REST API-ändringslogg
description: På den här sidan visas ändringar i Partner Center REST API:er
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.topic: reference
ms.date: 12/15/2020
ms.openlocfilehash: d4f7f034a36a26b6219086ca952b189f7a313ef7
ms.sourcegitcommit: 51237e7e98d71a7e0590b4d6a4034b6409542126
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/09/2021
ms.locfileid: "113572003"
---
# <a name="december-2020-changes-to-partner-center-rest-apis"></a>December 2020 -ändringar i Partner Center REST API:er

Kontrollera här om det finns ändringar i Partner Center REST API:er.

## <a name="enhancements-to-education-pricing-eligibility-apis"></a>Förbättringar av API:er för berättigande till utbildningspriser



### <a name="what-has-changed"></a>Vad har ändrats?

Partner Center-API:et har för närvarande GET- och PUT-kvalificeringar för att verifiera berättigandet för Education-kunder. Det kommer inte att ske några ändringar i GET-kvalificerings-API:et. Vi har dock lagt till ett returfall i PUT-kvalificerings-API:et.

- GET – ändras inte.
- PUT – returfall läggs till.

Dessa API:er dras tillbaka i slutet av februari 2021 för att ersättas med nya API:er enligt beskrivningen nedan.

### <a name="scenarios-impacted"></a>Scenarier som påverkas:

Kundberättigande till utbildningsprissättning för utvalda SKU:er

### <a name="detail-descriptions"></a>Informationsbeskrivningar

Två nya GET- och POST-kvalificerings-API:er kommer att introduceras. De nya API:erna kommer att använda **kvalificering**, inte **kvalificering.** API:erna kommer att vara tillgängliga för testning under FY21 Q2.

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
   - Begränsad att vara utbildningskund
   - Inte en academic-domän
   - Inte ett kvalificerande bibliotek
   - Inte berättigad Till detta
 
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
