---
title: Hämta information om licensanvändning
description: Så här hämtar du användningsinformation om licenser på arbetsbelastningsnivå för Office och Dynamics.
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a93c59c8c2a4c82ad7f3e81e814386e1ac0c046c3b0bada80eaaac40d9179d93
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115990434"
---
# <a name="get-licenses-usage-information"></a>Hämta information om licensanvändning

Så här hämtar du användningsinformation om licenser på arbetsbelastningsnivå för Office och Dynamics.

## <a name="prerequisites"></a>Förutsättningar

Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med autentiseringsuppgifter för App+Användare.

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod  | URI för förfrågan                                                                                |
|---------|--------------------------------------------------------------------------------------------|
| **Få** | [*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/usage/license/ HTTP/1.1 |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="uri-parameters"></a>URI-parametrar

| Parameter         | Typ     | Beskrivning | Krävs |
|-------------------|----------|-------------|----------|
| top               | sträng   | Antalet rader med data som ska returneras i begäran. Det högsta värdet och standardvärdet om inget värde anges är 10000. Om det finns fler rader i frågan innehåller svarstexten en nästa länk som du kan använda för att begära nästa sida med data. | No |
| hoppa över              | int      | Antalet rader som ska hoppas över i frågan. Använd den här parametern för att bläddra igenom stora datamängder. Till exempel hämtar top=10000 och skip=0 de första 10 000 raderna med data, top=10000 och skip=10000 hämtar de nästa 10 000 raderna med data och så vidare. | No |
| filter            | sträng   | *Filterparametern* för begäran innehåller en eller flera instruktioner som filtrerar raderna i svaret. Varje -instruktion innehåller ett fält och värde som är associerade med **`eq`** **`ne`** operatorerna eller , och -instruktioner kan kombineras med hjälp av **`and`** eller **`or`** . Här är några exempel *på filterparametrar:*<br/><br/>*filter=workloadCode eq 'SFB'*<br/><br/>*filter=workloadCode eq 'SFB'* or (*channel eq 'Reseller'*)<br/><br/>Du kan ange följande fält:<br/><br/>**workloadCode**<br/>**workloadName**<br/>**serviceCode**<br/>**Tjänstnamn**<br/>**Kanal**<br/>**customerTenantId**<br/>**customerName**<br/>**Produktionen**<br/>**Productname** | No |
| groupby           | sträng   | En instruktion som endast tillämpar dataaggregering på de angivna fälten. Du kan ange följande fält:<br/><br/>**workloadCode**<br/>**workloadName**<br/>**serviceCode**<br/>**Tjänstnamn**<br/>**channelcustomerTenantId**<br/>**customerName**<br/>**Produktionen**<br/>**Productname**<br/><br/>De returnerade dataraderna innehåller de fält som anges i *parametern groupby* och följande:<br/><br/>**licensesActive**<br/>**licensesQualified** | No |
| processedDateTime | DateTime | Du kan ange det datum då användningsdata bearbetades. Standardvärdet är det senaste datumet då data bearbetades | No |

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/commercial/usage/license?filter=customerTenantId%20eq%20%270112A436-B14E-4888-967B-CA4BB2CF1234%27 HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST-svar

Om det lyckas innehåller svarstexten följande fält som innehåller data om licensanvändningen.

| Fält             | Typ     | Description                                   |
|-------------------|----------|-----------------------------------------------|
| workloadCode      | sträng   | Arbetsbelastningskod                                 |
| workloadName      | sträng   | Namn på arbetsbelastning                                 |
| serviceCode       | sträng   | Tjänstkod                                  |
| Tjänstnamn       | sträng   | Tjänstnamn                                  |
| Kanal           | sträng   | Kanalnamn, återförsäljare                        |
| customerTenantId  | sträng   | Unik identifierare för kunden            |
| customerName      | sträng   | Kundnamn                                 |
| productId         | sträng   | Unik identifierare för produkten             |
| Productname       | sträng   | Produktnamn                                  |
| licensesActive    | long     | Antal aktiva licenser per arbetsbelastning        |
| licensesQualified | long     | Antal kvalificerade licenser för arbetsbelastningen |
| processedDateTime | DateTime | Datum då data senast bearbetades         |

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)

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
      "workloadCode": "SPO",
      "workloadName": "SharePoint",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "6FD2C87F-B296-42F0-B197-1E91E994B900",
      "productName": "OFFICE 365 ENTERPRISE E3",
      "licenseActive": 0,
      "licensesQualified": 1
    },
    {
      "processedDateTime": "2018-10-14T00:00:00",
      "workloadCode": "EXO",
      "workloadName": "Exchange",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "45A2423B-E884-448D-A831-D9E139C52D2F",
      "productName": "EXCHANGE ONLINE PROTECTION",
      "licenseActive": 0,
      "licensesQualified": 1
    }
}
```
