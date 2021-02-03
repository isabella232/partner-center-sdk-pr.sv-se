---
title: Hämta all information om Azure-användningsanalys
description: Så här hämtar du all information om användnings analys i Azure.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: c281dcdeb93771a69a388ad64e1127b24156c809
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/14/2020
ms.locfileid: "97769441"
---
# <a name="get-all-azure-usage-analytics-information"></a>Hämta all information om Azure-användningsanalys

**Gäller för**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Så här hämtar du all information om Azures användnings analys för dina kunder.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med användarautentiseringsuppgifter.

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod  | URI för förfrågan |
|---------|-------------|
| **TA** | [*\{ BASEURL \}*](partner-center-rest-urls.md)/partner/v1/Analytics/Usage/Azure http/1.1 |

### <a name="uri-parameters"></a>URI-parametrar

|Parameter        |Typ                        |Description               |
|:----------------|:---------------------------|:-------------------------|
|top              | sträng                     | Det antal rader med data som ska returneras i begäran. Det maximala värdet och standardvärdet om det inte anges är 10000. Om det finns fler rader i frågan, innehåller svars texten en nästa länk som du kan använda för att begära nästa sida med data.                        |
|hoppa över             | int                        | Antalet rader som ska hoppas över i frågan. Använd den här parametern för att växla mellan stora data mängder. Hämtar till exempel `top=10000 and skip=0` de första 10000 raderna med data, `top=10000 and skip=10000` hämtar nästa 10000 rader med data och så vidare.                       |
|filter           | sträng                     | *Filter* parametern för begäran innehåller en eller flera instruktioner som filtrerar raderna i svaret. Varje instruktion innehåller ett fält och ett värde som är associerat `eq` med `ne` operatorerna or och som kan kombineras med hjälp av `and` eller `or` . Du kan ange följande strängar:<br/><br/>                                                       `customerTenantId`<br/> `customerName`<br/> `subscriptionId`<br/> `subscriptionName`<br/> `usageDate` <br/> `resourceLocation` <br/> `meterCategory` <br/> `meterSubcategory` <br/> `meterUnit`<br/> `reservationOrderId` <br/> `reservationId`<br/> `consumptionMeterId` <br/> `serviceType` <br/><br/>**Exempel:**<br/> `.../usage/azure?filter=meterCategory eq 'Data Management'`<br/><br/> **Exempel:**<br/>`.../usage/azure?filter=meterCategory eq 'Data Management' or (usageDate le cast('2018-01-01', Edm.DateTimeOffset) and usageDate le cast('2018-04-01', Edm.DateTimeOffset))`                        |
|aggregationLevel | sträng                    | Anger det tidsintervall som aggregerade data ska hämtas från. Kan vara en av följande strängar: `day` , `week` , eller `month` . Om inget anges är standardvärdet `day` .<br/><br/>                                              `aggregationLevel`Parametern stöds inte utan en `groupby` . `aggregationLevel`Parametern gäller för alla datum fält som finns i `groupby` .                                                      |
|OrderBy          |sträng                     | En instruktion som ordnar resultat data värden för varje installation. Syntax: `...&orderby=field [order],field [order],...`. `field`Parametern kan vara en av följande strängar:<br/><br/>                    `customerTenantId`<br/>`customerName`<br/>`subscriptionId`<br/>`subscriptionName`<br/>`usageDate`<br/>`resourceLocation`<br/>`meterCategory`<br/>`meterSubcategory`<br/>`meterUnit`<br/> `reservationOrderId` <br/> `reservationId`<br/> `consumptionMeterId` <br/> `serviceType` <br/><br/> *Sorterings* parametern är valfri och kan vara `asc` eller `desc` Ange stigande eller fallande ordning för respektive fält. Standardvärdet är `asc`.<br/><br/>**Exempel:**<br/> `...&orderby=meterCategory,meterUnit`                                                                                           |
|groupby          |sträng                    | En instruktion som endast tillämpar data agg regering på de angivna fälten. Du kan ange följande fält:<br/><br/>                                                                                                                     `customerTenantId`<br/>`customerName`<br/> `subscriptionId` <br/> `subscriptionName` <br/> `usageDate` <br/> `resourceLocation` <br/> `meterCategory` <br/> `meterSubcategory` <br/> `meterUnit` <br/> `reservationOrderId` <br/> `reservationId` <br/> `consumptionMeterId` <br/> `serviceType` <br/><br/>De returnerade data raderna innehåller fälten som anges i `groupby`  parametern samt *kvantiteten*.<br/><br/>`groupby`Parametern kan användas med `aggregationLevel` parametern.<br/><br/>**Exempel:**<br/>`...&groupby=meterCategory,meterUnit` |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/usage/azure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>REST-svar

Om det lyckas innehåller svars texten en samling [Azures användnings](partner-center-analytics-resources.md#csp-program-azure-usage-analytics) resurser.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [felkoder](error-codes.md).

### <a name="response-example"></a>Exempel på svar

```http
{
  "customerTenantId": "39A1DFAC-4969-4F31-AF94-D76588189CFE",
  "customerName": "A",
  "subscriptionId": "EC649980-D623-49F5-B7C1-80CC772B83A8",
  "subscriptionName": "AZURE PURCHSE SAMPLE APP",
  "usageDate": "2018-05-27T00:00:00",
  "resourceLocation": "useast",
  "meterCategory": "Data Management",
  "meterSubcategory": "None",
  "meterUnit": "10,000s",
  "reservationOrderId": "",
  "reservationId": "",
  "consumptionMeterId": "",
  "serviceType": "",
  "quantity": 20
}
```

## <a name="see-also"></a>Se även

- [Partnercenter-analys – resurser](partner-center-analytics-resources.md)
