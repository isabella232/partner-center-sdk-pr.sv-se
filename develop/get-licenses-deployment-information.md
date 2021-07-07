---
title: Hämta information om licensdistribution
description: Så här hämtar du distributionsinformation för Office- och Dynamics-licenser.
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9eb0dc655affb2216b11635e58e00ed6464d6792
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445671"
---
# <a name="get-licenses-deployment-information"></a>Hämta information om licensdistribution

Så här hämtar du distributionsinformation för Office- och Dynamics-licenser.

## <a name="prerequisites"></a>Förutsättningar

Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med autentiseringsuppgifter för App+Användare.

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod  | URI för förfrågan                                                                                     |
|---------|-------------------------------------------------------------------------------------------------|
| **Få** | [*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/deployment/license/ HTTP/1.1 |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="uri-parameters"></a>URI-parametrar

| Parameter         | Typ     | Beskrivning | Krävs |
|-------------------|----------|-------------|----------|
| top               | sträng   | Antalet rader med data som ska returneras i begäran. Det högsta värdet och standardvärdet om inget värde anges är 10000. Om det finns fler rader i frågan innehåller svarstexten en nästa länk som du kan använda för att begära nästa sida med data. | Inga |
| hoppa över              | int      | Antalet rader som ska hoppas över i frågan. Använd den här parametern för att bläddra igenom stora datamängder. Till exempel hämtar top=10000 och skip=0 de första 10 000 raderna med data, top=10000 och skip=10000 hämtar de nästa 10 000 raderna med data och så vidare. | Inga |
| filter            | sträng   | *Filterparametern* för begäran innehåller en eller flera instruktioner som filtrerar raderna i svaret. Varje -instruktion innehåller ett fält och värde som är associerade med `eq` `ne` operatorerna eller , och -instruktioner kan kombineras med hjälp av `and` eller `or` . Här är några exempel *på filterparametrar:*<br/><br/> *filter=serviceCode eq 'O365'*<br/> *filter=serviceCode eq 'O365'* or (*channel eq 'Reseller'*)<br/><br/> Du kan ange följande fält:<br/><br/>**serviceCode**<br/>**Tjänstnamn**<br/>**Kanal**<br/>**customerTenantId**<br/>**customerName**<br/>**Produktionen**<br/>**Productname**  | Inga |
| groupby           | sträng   | En instruktion som endast tillämpar dataaggregering på de angivna fälten. Du kan ange följande fält:<br/><br/>**serviceCode**<br/>**Tjänstnamn**<br/>**Kanal**<br/>**customerTenantId**<br/>**customerName**<br/>**Produktionen**<br/>**Productname**<br/><br/> De returnerade dataraderna innehåller de fält som anges i *parametern groupby* och följande:<br/><br/>**licensesDeployed**<br/>**licenserSåld**  | Inga |
| processedDateTime | DateTime | Du kan ange det datum då användningsdata bearbetades. Standardvärdet är det senaste datumet då data bearbetades | Inga |

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/commercial/deployment/license?filter=customerTenantId%20eq%20%270112A436-B14E-4888-967B-CA4BB2CF1234%27 HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST-svar

Om det lyckas innehåller svarstexten följande fält som innehåller data om de distribuerade licenserna.

| Fält             | Typ     | Beskrivning                           |
|-------------------|----------|---------------------------------------|
| serviceCode       | sträng   | Tjänstkod                          |
| Tjänstnamn       | sträng   | Tjänstnamn                          |
| Kanal           | sträng   | Kanalnamn, återförsäljare                |
| customerTenantId  | sträng   | Unik identifierare för kunden    |
| customerName      | sträng   | Kundnamn                         |
| productId         | sträng   | Unik identifierare för produkten     |
| Productname       | sträng   | Produktnamn                          |
| licensesDeployed  | long     | Antal distribuerade licenser           |
| licenserSåld      | long     | Antal sålda licenser               |
| processedDateTime | DateTime | Datum då data senast bearbetades |

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Length: 487
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CV: f0trvmq8mEScHcFS.0
MS-ServerId: 4
Date: Wed, 24 Oct 2018 22:37:18 GMT
{
  "Value": [

{
      "processedDateTime": "2018-10-14T00:00:00",
      "serviceCode": "crm",
      "serviceName": "Microsoft Dynamics",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "54B84594-9C77-4499-8D65-5E0D5F410E78",
      "productName": "DYNAMICS AX TASK",
      "licensesDeployed": 0,
      "licensesSold": 9
    },
    {
      "processedDateTime": "2018-10-14T00:00:00",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "D3B4FE1F-9992-4930-8ACB-CA6EC609365E",
      "productName": "DOMESTIC AND INTERNATIONAL CALLING PLAN",
      "licensesDeployed": 0,
      "licensesSold": 5
    }
],
  "@nextLink": null,
  "TotalCount": 2
}
```
