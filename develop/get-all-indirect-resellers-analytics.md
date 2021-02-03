---
title: Hämta all analysinformation för indirekta återförsäljare
description: Hämta all den indirekta åter försäljarens analys information.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 9f9c030278ba8fef9090f7be89064ac6054129ef
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/14/2020
ms.locfileid: "97769444"
---
# <a name="get-all-indirect-resellers-analytics-information"></a>Hämta all analysinformation för indirekta återförsäljare

**Gäller för**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Hämta all den indirekta åter försäljarens analys information för dina kunder.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med användarautentiseringsuppgifter.

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod  | URI för förfrågan |
|---------|-------------|
| **TA** | [*\{ BASEURL \}*](partner-center-rest-urls.md)/partner/v1/Analytics/indirectresellers http/1.1 |

### <a name="uri-parameters"></a>URI-parametrar

| Parameter                             | Typ     | Description                              |
|:--------------------------------------|:---------|:-----------------------------------------|
| partnerTenantId                       | sträng   | Klient-ID för den partner som du vill hämta indirekta data om åter försäljare för. |
| id                                    | sträng   | ID för indirekt åter försäljare                                                                 |
| name                                  | sträng   | Namnet på den partner som du vill hämta data om indirekta åter försäljare för.      |
| telefonförsäljning                                | sträng   | Marknaden för den partner som du vill hämta data om indirekta åter försäljare för.    |
| firstSubscriptionCreationDate         | sträng i UTC-datum/tid-format  | Skapande datumet för den första prenumerationen som du vill hämta indirekta åter försäljar data från.  |
| latestSubscriptionCreationDate        | sträng i UTC-datum/tid-format  | Skapande datumet för den senaste prenumerationen.                 |
| firstSubscriptionEndDate              | sträng i UTC-datum/tid-format  | Första gången en prenumeration avslutades.                        |
| latestSubscriptionEndDate             | sträng i UTC-datum/tid-format  | Senaste datum när en prenumeration avslutades.                  |
| firstSubscriptionSuspendedDate        | sträng i UTC-datum/tid         | Första gången en prenumeration pausades.                    |
| latestSubscriptionSuspendedDate       | sträng i UTC-datum/tid-format  | Senaste datum när en prenumeration pausades.              |
| firstSubscriptionDeprovisionedDate    | sträng i UTC-datum/tid-format  | Första gången en prenumeration har avetablerats.                |
| latestSubscriptionDeprovisionedDate   | sträng i UTC-datum/tid-format  | Senaste datum när en prenumeration har avetablerats.          |
| subscriptionCount                     | double   | Prenumerations antal för alla mervärdes åter försäljare                                     |
| licenseCount                          | double   | Licens antal för alla mervärdes åter försäljare.                                         |
| indirectResellerCount                 | double   | Antal indirekta åter försäljare                                                             |
|  top                                  | sträng   | Det antal rader med data som ska returneras i begäran. Det maximala värdet och standardvärdet om det inte anges är 10000. Om det finns fler rader i frågan, innehåller svars texten en nästa länk som du kan använda för att begära nästa sida med data.  |
| hoppa över                                  | int      | Antalet rader som ska hoppas över i frågan. Använd den här parametern för att växla mellan stora data mängder. Hämtar till exempel **`top=10000 and skip=0`** de första 10000 raderna med data, **`top=10000 and skip=10000`** hämtar nästa 10000 rader med data och så vidare.              |
| filter                                | sträng   | *Filter* parametern för begäran innehåller en eller flera instruktioner som filtrerar raderna i svaret. Varje instruktion innehåller ett fält och ett värde som är associerat **`eq`** med **`ne`** operatorerna or och som kan kombineras med hjälp av **`and`** eller **`or`** . Du kan ange följande fält:<br/><br/>     *partnerTenantId*<br/> *id*<br/> *Namn*<br/>                *telefonförsäljning*<br/> *firstSubscriptionCreationDate*<br/> *latestSubscriptionCreationDate*<br/>                *firstSubscriptionEndDate*<br/>                *latestSubscriptionEndDate*<br/>                *firstSubscriptionSuspendedDate*<br/>                *latestSubscriptionSuspendedDate*<br/>                *firstSubscriptionDeprovisionedDate*<br/>                *latestSubscriptionDeprovisionedDate*<br/><br/>         **Exempel:**<br/>              `.../indirectresellers?filter=market eq 'US'`<br/><br/>            **Exempel:**<br/>                `.../indirectresellers?filter=market eq 'US' or (firstSubscriptionCreationDate le cast('2018-01-01',Edm.DateTimeOffset) and firstSubscriptionCreationDate le cast('2018-04-01',Edm.DateTimeOffset))` |              
| aggregationLevel                     | sträng    | Anger det tidsintervall som aggregerade data ska hämtas från. Kan vara en av följande strängar: &quot; dag &quot; , &quot; vecka &quot; eller &quot; månad &quot; . Om inget anges är standardvärdet &quot; dag &quot; .<br/><br/>                                 `aggregationLevel` stöds inte utan en `aggregationLevel` . `aggregationLevel` gäller för alla **datefields** som finns i `aggregationLevel`                         |
| OrderBy                              | sträng    | En instruktion som ordnar resultat data värden för varje installation. Syntax: `...&orderby=field[order],field [order],...`. Fält parametern kan vara en av följande strängar:<br/><br/>                &quot;partnerTenantId&quot;<br/>                &quot;id&quot;<br/>                &quot;Namn&quot;<br/>                &quot;telefonförsäljning&quot;<br/>                &quot;firstSubscriptionCreationDate&quot;<br/>               &quot;latestSubscriptionCreationDate&quot;<br/>                &quot;firstSubscriptionEndDate&quot;<br/>               &quot;latestSubscriptionEndDate&quot;<br/>                &quot;firstSubscriptionSuspendedDate&quot;<br/>                &quot;latestSubscriptionSuspendedDate&quot;<br/>               &quot;firstSubscriptionDeprovisionedDate&quot;<br/>                &quot;latestSubscriptionDeprovisionedDate&quot;<br/>                &quot;subscriptionCount&quot;<br/>                &quot;licenseCount&quot;<br/><br/>   *Sorterings* parametern är valfri och kan vara `asc` eller `desc` ; för att ange stigande eller fallande ordning för varje fält. Standardvärdet är `asc`.<br/><br/>    **Exempel:**<br/>                `...&orderby=market,subscriptionCount`                                       |                   
| groupby                              | sträng    | En instruktion som endast tillämpar data agg regering på de angivna fälten. Du kan ange följande fält:<br/><br/>         *partnerTenantId*<br/>    *id*<br/>               *Namn*<br/>                *telefonförsäljning*<br/>                *firstSubscriptionCreationDate*<br/>                *latestSubscriptionCreationDate*<br/>                *firstSubscriptionEndDate*<br/>                *latestSubscriptionEndDate*<br/>                *firstSubscriptionSuspendedDate*<br/>                *latestSubscriptionSuspendedDate*<br/>                *firstSubscriptionDeprovisionedDate*<br/>                *latestSubscriptionDeprovisionedDate*<br/><br/>                 De data rader som returneras innehåller fälten som anges i `groupby` -satsen och följande fält:<br/><br/>            *indirectResellerCount*<br/>                *licenseCount*<br/>                *subscriptionCount*<br/><br/>            `groupby`Parametern kan användas med `aggregationLevel` parametern.<br/><br/>            **Exempel:**</br>               `...&groupby=ageGroup,market&aggregationLevel=week`                         |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

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

Om det lyckas innehåller svars texten en samling [indirekta åter försäljares](partner-center-analytics-resources.md#csp-program-indirect-resellers-analytics) resurser.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [felkoder](error-codes.md).

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
