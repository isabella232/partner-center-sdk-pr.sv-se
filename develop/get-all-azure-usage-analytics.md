---
title: Hämta all information om Azure-användningsanalys
description: Så här hämtar du all användningsanalysinformation i Azure.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 1d671c07185f92a36055af12d9de2e39adeab129bfcb2497da66d35807db270e
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994089"
---
# <a name="get-all-azure-usage-analytics-information"></a>Hämta all information om Azure-användningsanalys

**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Så här hämtar du all information om Azure-användningsanalys för dina kunder.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md) Det här scenariot stöder autentisering endast med användarautentiseringsuppgifter.

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod  | URI för förfrågan |
|---------|-------------|
| **Få** | [*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/usage/azure HTTP/1.1 |

### <a name="uri-parameters"></a>URI-parametrar

|Parameter        |Typ                        |Description               |
|:----------------|:---------------------------|:-------------------------|
|top              | sträng                     | Antalet rader med data som ska returneras i begäran. Maxvärdet och standardvärdet om det inte anges är 10000. Om det finns fler rader i frågan innehåller svarstexten en nästa länk som du kan använda för att begära nästa datasida.                        |
|hoppa över             | int                        | Antalet rader som ska hoppas över i frågan. Använd den här parametern för att bläddra igenom stora datamängder. Hämtar till exempel de första `top=10000 and skip=0` 1 0000 raderna med data, hämtar de `top=10000 and skip=10000` kommande 10 000 raderna med data och så vidare.                       |
|filter           | sträng                     | *Filterparametern* för begäran innehåller en eller flera instruktioner som filtrerar raderna i svaret. Varje -instruktion innehåller ett fält och värde som är associerade med operatorerna eller , och `eq` `ne` -instruktioner kan kombineras med hjälp av `and` eller `or` . Du kan ange följande strängar:<br/><br/>                                                       `customerTenantId`<br/> `customerName`<br/> `subscriptionId`<br/> `subscriptionName`<br/> `usageDate` <br/> `resourceLocation` <br/> `meterCategory` <br/> `meterSubcategory` <br/> `meterUnit`<br/> `reservationOrderId` <br/> `reservationId`<br/> `consumptionMeterId` <br/> `serviceType` <br/><br/>**Exempel:**<br/> `.../usage/azure?filter=meterCategory eq 'Data Management'`<br/><br/> **Exempel:**<br/>`.../usage/azure?filter=meterCategory eq 'Data Management' or (usageDate le cast('2018-01-01', Edm.DateTimeOffset) and usageDate le cast('2018-04-01', Edm.DateTimeOffset))`                        |
|aggregationLevel | sträng                    | Anger det tidsperiod som aggregerade data ska hämtas för. Kan vara någon av följande strängar: `day` , `week` eller `month` . Om det inte anges är standardvärdet `day` .<br/><br/>                                              Parametern `aggregationLevel` stöds inte utan `groupby` . Parametern `aggregationLevel` gäller för alla datumfält som finns i `groupby` .                                                      |
|Orderby          |sträng                     | En instruktion som beställer resultatdatavärdena för varje installation. Syntax: `...&orderby=field [order],field [order],...`. Parametern `field` kan vara någon av följande strängar:<br/><br/>                    `customerTenantId`<br/>`customerName`<br/>`subscriptionId`<br/>`subscriptionName`<br/>`usageDate`<br/>`resourceLocation`<br/>`meterCategory`<br/>`meterSubcategory`<br/>`meterUnit`<br/> `reservationOrderId` <br/> `reservationId`<br/> `consumptionMeterId` <br/> `serviceType` <br/><br/> *Orderparametern* är valfri och kan vara eller för att ange stigande eller fallande ordning för respektive `asc` `desc` fält. Standardvärdet är `asc`.<br/><br/>**Exempel:**<br/> `...&orderby=meterCategory,meterUnit`                                                                                           |
|groupby          |sträng                    | En instruktion som endast tillämpar dataaggregering på de angivna fälten. Du kan ange följande fält:<br/><br/>                                                                                                                     `customerTenantId`<br/>`customerName`<br/> `subscriptionId` <br/> `subscriptionName` <br/> `usageDate` <br/> `resourceLocation` <br/> `meterCategory` <br/> `meterSubcategory` <br/> `meterUnit` <br/> `reservationOrderId` <br/> `reservationId` <br/> `consumptionMeterId` <br/> `serviceType` <br/><br/>De returnerade dataraderna innehåller fälten som anges i `groupby`  parametern och *Quantity*.<br/><br/>Parametern `groupby` kan användas med `aggregationLevel` parametern .<br/><br/>**Exempel:**<br/>`...&groupby=meterCategory,meterUnit` |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

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

Om det lyckas innehåller svarstexten en samling [Azure-användningsresurser.](partner-center-analytics-resources.md#csp-program-azure-usage-analytics)

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder.](error-codes.md)

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
