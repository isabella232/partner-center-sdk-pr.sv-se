---
title: Hämta information om licensanvändning
description: Så här hämtar du licens användnings information på arbets belastnings nivå för Office och Dynamics.
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a144fd078a36289e4a2c70880817b1f0ca627e8a
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/14/2020
ms.locfileid: "97769429"
---
# <a name="get-licenses-usage-information"></a>Hämta information om licensanvändning

**Gäller för**

- Partnercenter

Så här hämtar du licens användnings information på arbets belastnings nivå för Office och Dynamics.

## <a name="prerequisites"></a>Förutsättningar

Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med app + användarautentiseringsuppgifter.

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod  | URI för förfrågan                                                                                |
|---------|--------------------------------------------------------------------------------------------|
| **TA** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Analytics/Commercial/Usage/License/http/1.1 |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="uri-parameters"></a>URI-parametrar

| Parameter         | Typ     | Beskrivning | Krävs |
|-------------------|----------|-------------|----------|
| top               | sträng   | Det antal rader med data som ska returneras i begäran. Det maximala värdet och standardvärdet om det inte anges är 10000. Om det finns fler rader i frågan, innehåller svars texten en nästa länk som du kan använda för att begära nästa sida med data. | No |
| hoppa över              | int      | Antalet rader som ska hoppas över i frågan. Använd den här parametern för att växla mellan stora data mängder. Till exempel Top = 10000 och Skip = 0 hämtar de första 10000 raderna med data, Top = 10000 och Skip = 10000 hämtar nästa 10000 rader med data och så vidare. | No |
| filter            | sträng   | *Filter* parametern för begäran innehåller en eller flera instruktioner som filtrerar raderna i svaret. Varje instruktion innehåller ett fält och ett värde som är associerat **`eq`** med **`ne`** operatorerna or och som kan kombineras med hjälp av **`and`** eller **`or`** . Här följer några exempel på *filter* parametrar:<br/><br/>*filter = workloadCode EQ ' SFB '*<br/><br/>*filter = workloadCode EQ ' SFB '* eller (*kanal EQ åter försäljare*)<br/><br/>Du kan ange följande fält:<br/><br/>**workloadCode**<br/>**workloadName**<br/>**serviceCode**<br/>**serviceName**<br/>**kanalig**<br/>**customerTenantId**<br/>**customerName**<br/>**productId**<br/>**Namn** | No |
| groupby           | sträng   | En instruktion som endast tillämpar data agg regering på de angivna fälten. Du kan ange följande fält:<br/><br/>**workloadCode**<br/>**workloadName**<br/>**serviceCode**<br/>**serviceName**<br/>**channelcustomerTenantId**<br/>**customerName**<br/>**productId**<br/>**Namn**<br/><br/>De returnerade data raderna innehåller fälten som anges i *groupby* -parametern samt följande:<br/><br/>**licensesActive**<br/>**licensesQualified** | No |
| processedDateTime | DateTime | En kan ange det datum från vilket användnings data bearbetades. Standardvärdet är det senaste datumet då data bearbetades | No |

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

Om det lyckas innehåller svars texten följande fält som innehåller data om licens användning.

| Fält             | Typ     | Description                                   |
|-------------------|----------|-----------------------------------------------|
| workloadCode      | sträng   | Arbets belastnings kod                                 |
| workloadName      | sträng   | Arbets belastnings namn                                 |
| serviceCode       | sträng   | Service kod                                  |
| serviceName       | sträng   | Tjänstnamn                                  |
| kanalig           | sträng   | Kanal namn, åter försäljare                        |
| customerTenantId  | sträng   | Unikt ID för kunden            |
| customerName      | sträng   | Kundnamn                                 |
| productId         | sträng   | Unikt ID för produkten             |
| Namn       | sträng   | Produktnamn                                  |
| licensesActive    | long     | Antal aktiva licenser per arbets belastning        |
| licensesQualified | long     | Antal kvalificerade licenser för arbets belastningen |
| processedDateTime | DateTime | Datum när data senast bearbetades         |

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).

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
