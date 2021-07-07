---
title: Hämta all analysinformation för indirekta återförsäljare
description: Hur du hämtar all indirekt återförsäljares analysinformation.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 4252f5fcbbcb038f382408074c8fd6ede3fd1f58
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760750"
---
# <a name="get-all-indirect-resellers-analytics-information"></a>Hämta all analysinformation för indirekta återförsäljare

**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Hur du hämtar all indirekt återförsäljares analysinformation för dina kunder.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md) Det här scenariot stöder autentisering endast med användarautentiseringsuppgifter.

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod  | URI för förfrågan |
|---------|-------------|
| **Få** | [*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/indirectresellers HTTP/1.1 |

### <a name="uri-parameters"></a>URI-parametrar

| Parameter                             | Typ     | Beskrivning                              |
|:--------------------------------------|:---------|:-----------------------------------------|
| partnerTenantId                       | sträng   | Klientorganisations-ID för den partner som du vill hämta indirekta återförsäljares data för. |
| id                                    | sträng   | Id för indirekt återförsäljare                                                                 |
| name                                  | sträng   | Namnet på den partner som du vill hämta indirekta återförsäljares data för.      |
| Marknaden                                | sträng   | Partnerns marknad som du vill hämta data om indirekta återförsäljare för.    |
| firstSubscriptionCreationDate         | sträng i UTC-datum/tid-format  | Skapandedatumet för den första prenumerationen baserat på vilken du vill hämta data för indirekta återförsäljare.  |
| latestSubscriptionCreationDate        | sträng i UTC-datum/tid-format  | Skapandedatumet för den senaste prenumerationen.                 |
| firstSubscriptionEndDate              | sträng i UTC-datum/tid-format  | Första gången någon prenumeration avslutades.                        |
| latestSubscriptionEndDate             | sträng i UTC-datum/tid-format  | Senaste datum då en prenumeration avslutades.                  |
| firstSubscriptionSuspendedDate        | sträng i UTC-datum/tid         | Första gången någon prenumeration pausas.                    |
| latestSubscriptionSuspendedDate       | sträng i UTC-datum/tid-format  | Senaste datum då en prenumeration pausades.              |
| firstSubscriptionDeprovisionedDate    | sträng i UTC-datum/tid-format  | Första gången någon prenumeration avetableades.                |
| latestSubscriptionDeprovisionedDate   | sträng i UTC-datum/tid-format  | Senaste datum då en prenumeration avetableades.          |
| subscriptionCount                     | double   | Prenumerationsantal för alla återförsäljare med mervärde                                     |
| licenseCount                          | double   | Licensantal för alla återförsäljare med mervärde.                                         |
| indirectResellerCount                 | double   | Antal indirekta återförsäljare                                                             |
|  top                                  | sträng   | Antalet rader med data som ska returneras i begäran. Maxvärdet och standardvärdet om det inte anges är 10000. Om det finns fler rader i frågan innehåller svarstexten en nästa länk som du kan använda för att begära nästa datasida.  |
| hoppa över                                  | int      | Antalet rader som ska hoppas över i frågan. Använd den här parametern för att bläddra igenom stora datamängder. Hämtar till exempel de första **`top=10000 and skip=0`** 1 0000 raderna med data, hämtar de **`top=10000 and skip=10000`** kommande 10 000 raderna med data och så vidare.              |
| filter                                | sträng   | *Filterparametern* för begäran innehåller en eller flera instruktioner som filtrerar raderna i svaret. Varje -instruktion innehåller ett fält och värde som är associerade med operatorerna eller , och **`eq`** **`ne`** -instruktioner kan kombineras med hjälp av **`and`** eller **`or`** . Du kan ange följande fält:<br/><br/>     *partnerTenantId*<br/> *id*<br/> *Namn*<br/>                *Marknaden*<br/> *firstSubscriptionCreationDate*<br/> *latestSubscriptionCreationDate*<br/>                *firstSubscriptionEndDate*<br/>                *latestSubscriptionEndDate*<br/>                *firstSubscriptionSuspendedDate*<br/>                *latestSubscriptionSuspendedDate*<br/>                *firstSubscriptionDeprovisionedDate*<br/>                *latestSubscriptionDeprovisionedDate*<br/><br/>         **Exempel:**<br/>              `.../indirectresellers?filter=market eq 'US'`<br/><br/>            **Exempel:**<br/>                `.../indirectresellers?filter=market eq 'US' or (firstSubscriptionCreationDate le cast('2018-01-01',Edm.DateTimeOffset) and firstSubscriptionCreationDate le cast('2018-04-01',Edm.DateTimeOffset))` |              
| aggregationLevel                     | sträng    | Anger det tidsperiod som aggregerade data ska hämtas för. Kan vara någon av följande strängar: &quot; &quot; dag, &quot; vecka eller &quot; månad &quot; &quot; . Om det inte anges är standardvärdet &quot; dag &quot; .<br/><br/>                                 `aggregationLevel` stöds inte utan `aggregationLevel` . `aggregationLevel` gäller för alla **datefields** som finns i `aggregationLevel`                         |
| Orderby                              | sträng    | En instruktion som beställer resultatdatavärdena för varje installation. Syntax: `...&orderby=field[order],field [order],...`. Fältparametern kan vara någon av följande strängar:<br/><br/>                &quot;partnerTenantId&quot;<br/>                &quot;id&quot;<br/>                &quot;Namn&quot;<br/>                &quot;Marknaden&quot;<br/>                &quot;firstSubscriptionCreationDate&quot;<br/>               &quot;latestSubscriptionCreationDate&quot;<br/>                &quot;firstSubscriptionEndDate&quot;<br/>               &quot;latestSubscriptionEndDate&quot;<br/>                &quot;firstSubscriptionSuspendedDate&quot;<br/>                &quot;latestSubscriptionSuspendedDate&quot;<br/>               &quot;firstSubscriptionDeprovisionedDate&quot;<br/>                &quot;latestSubscriptionDeprovisionedDate&quot;<br/>                &quot;subscriptionCount&quot;<br/>                &quot;licenseCount&quot;<br/><br/>   *Orderparametern* är valfri och kan vara eller ; för att ange stigande eller `asc` `desc` fallande ordning för varje fält. Standardvärdet är `asc`.<br/><br/>    **Exempel:**<br/>                `...&orderby=market,subscriptionCount`                                       |                   
| groupby                              | sträng    | En instruktion som endast tillämpar dataaggregering på de angivna fälten. Du kan ange följande fält:<br/><br/>         *partnerTenantId*<br/>    *id*<br/>               *Namn*<br/>                *Marknaden*<br/>                *firstSubscriptionCreationDate*<br/>                *latestSubscriptionCreationDate*<br/>                *firstSubscriptionEndDate*<br/>                *latestSubscriptionEndDate*<br/>                *firstSubscriptionSuspendedDate*<br/>                *latestSubscriptionSuspendedDate*<br/>                *firstSubscriptionDeprovisionedDate*<br/>                *latestSubscriptionDeprovisionedDate*<br/><br/>                 De datarader som returneras innehåller de fält som anges `groupby` i -satsen och följande fält:<br/><br/>            *indirectResellerCount*<br/>                *licenseCount*<br/>                *subscriptionCount*<br/><br/>            Parametern `groupby` kan användas med `aggregationLevel` parametern .<br/><br/>            **Exempel:**</br>               `...&groupby=ageGroup,market&aggregationLevel=week`                         |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/indirectresellers HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>REST-svar

Om åtgärden lyckas innehåller svarstexten en samling [indirekta återförsäljares](partner-center-analytics-resources.md#csp-program-indirect-resellers-analytics) resurser.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder.](error-codes.md)

### <a name="response-example"></a>Exempel på svar

```http
{
    "partnerTenantId": "AAAAAAAA-BBBB-CCCC-DDDD-EEEEEEEEEEEE",
    "id": "1111111",
    "name": "RESELLER NAME",
    "market": "US",
    "firstSubscriptionCreationDate": "2016-10-18T19:16:25.107",
    "latestSubscriptionCreationDate": "2016-10-18T19:16:25.107",
    "firstSubscriptionEndDate": "2018-11-07T00:00:00",
    "latestSubscriptionEndDate": "2018-11-07T00:00:00",
    "firstSubscriptionSuspendedDate": "0001-01-01T00:00:00",
    "latestSubscriptionSuspendedDate": "0001-01-01T00:00:00",
    "firstSubscriptionDeprovisionedDate": "0001-01-01T00:00:00",
    "latestSubscriptionDeprovisionedEndDate": "0001-01-01T00:00:00",
    "subscriptionCount": 10,
    "licenseCount": 20
}
```

## <a name="see-also"></a>Se även

- [Partnercenter-analys – resurser](partner-center-analytics-resources.md)
