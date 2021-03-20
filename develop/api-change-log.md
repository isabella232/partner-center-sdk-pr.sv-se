---
title: Partnercenter – REST API-ändringslogg
description: 'Den här sidan visar ändringar i REST-API: er för partner Center'
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.topic: reference
ms.date: 12/15/2020
ms.openlocfilehash: b2c2cac36a8bd1bec7aa5bf6e5d1aa73b4779535
ms.sourcegitcommit: 717e483a6eec23607b4e31ddfaa3e2691f3043e6
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/20/2021
ms.locfileid: "104711856"
---
# <a name="december-2020-changes-to-partner-center-rest-apis"></a>Ändringar i 2020 i samarbets-API: er i Partner Center

Sök efter ändringar i REST-API: er för partner Center.

## <a name="enhancements-to-education-pricing-eligibility-apis"></a>Förbättringar av API: er för utbildnings prissättning



### <a name="what-has-changed"></a>Vad har ändrats?

Partner Center-API: et har för närvarande GET-och-kvalifikationer för att verifiera utbildningens kunders berättigande. Inga ändringar görs i GET kvalificerings-API: et. Vi har dock lagt till ett retur ärende i API för att skicka kvalificering.

- GET – ändras inte. [Aktuell API-artikel](./get-customer-qualification-synchronous.md)
- Ärendet för att skicka returer läggs till. [Aktuell API-artikel](./update-customer-qualification-synchronous.md)

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