---
title: Partnercenter – REST API-ändringslogg
description: 'Den här sidan visar ändringar i REST-API: er för partner Center'
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.topic: reference
ms.date: 12/15/2020
ms.openlocfilehash: 79359414276a1259117a8f506bbfae4441cdcbed
ms.sourcegitcommit: f8ca3a14a763013fefafd3262d0a740881d1d7b1
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/17/2020
ms.locfileid: "97770281"
---
# <a name="december-2020-changes-to-partner-center-rest-apis"></a>Ändringar i 2020 i samarbets-API: er i Partner Center

Sök efter ändringar i REST-API: er för partner Center.

## <a name="enhancements-to-education-pricing-eligibility-apis"></a>Förbättringar av API: er för utbildnings prissättning



### <a name="what-has-changed"></a>Vad har ändrats?

Partner Center-API: et har för närvarande GET-och-kvalifikationer för att verifiera utbildningens kunders berättigande. Inga ändringar görs i GET kvalificerings-API: et. Vi har dock lagt till ett retur ärende i API för att skicka kvalificering.

- GET – ändras inte. [Aktuell API-artikel](get-a-customer-s-qualification.md)
- Ärendet för att skicka returer läggs till. [Aktuell API-artikel](update-a-customer-s-qualification.md)

Dessa API: er kommer att dras tillbaka i slutet av februari 2021 och ersätts av nya API: er enligt beskrivningen nedan.

### <a name="scenarios-impacted"></a>Scenarier som påverkas:

Kund berättigande för utbildnings pris för utvalda SKU: er

### <a name="detail-descriptions"></a>Detalj beskrivningar

Två nya API: er för GET-och POST-kvalifikationer kommer att införas. De nya API: erna kommer att använda **kvalifikationer**, inte **kvalificering**. API: er är tillgängliga för testning i FY21 Q2.

#### <a name="get-qualifications"></a>Hämta kvalifikationer

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

#### <a name="response-fields"></a>Svars fält: 

- VettingStatus-värden: godkänd, nekad, ingranskning osv.

- VettingReason-värden:
   - Inte en utbildnings kund
   - Inte längre en utbildnings kund
   - Inte en utbildnings kund – efter granskning
   - Begränsad som en utbildnings kund
   - Inte en akademisk domän
   - Inte ett giltigt bibliotek
   - Inte en giltig Museum
 
#### <a name="post-qualifications"></a>PUBLICERA kvalifikationer

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
