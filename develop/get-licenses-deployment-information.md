---
title: Hämta information om licensdistribution
description: Så här hämtar du distributions information för Office-och Dynamics-licenser.
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ef0e5d73d34bc51e4cc58143db6c9fc49cb58fcb
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/14/2020
ms.locfileid: "97769435"
---
# <a name="get-licenses-deployment-information"></a>Hämta information om licensdistribution

**Gäller för**

- Partnercenter

Så här hämtar du distributions information för Office-och Dynamics-licenser.

## <a name="prerequisites"></a>Förutsättningar

Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med app + användarautentiseringsuppgifter.

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod  | URI för förfrågan                                                                                     |
|---------|-------------------------------------------------------------------------------------------------|
| **TA** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Analytics/Commercial/Deployment/License/http/1.1 |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="uri-parameters"></a>URI-parametrar

| Parameter         | Typ     | Beskrivning | Krävs |
|-------------------|----------|-------------|----------|
| top               | sträng   | Det antal rader med data som ska returneras i begäran. Det maximala värdet och standardvärdet om det inte anges är 10000. Om det finns fler rader i frågan, innehåller svars texten en nästa länk som du kan använda för att begära nästa sida med data. | No |
| hoppa över              | int      | Antalet rader som ska hoppas över i frågan. Använd den här parametern för att växla mellan stora data mängder. Till exempel Top = 10000 och Skip = 0 hämtar de första 10000 raderna med data, Top = 10000 och Skip = 10000 hämtar nästa 10000 rader med data och så vidare. | No |
| filter            | sträng   | *Filter* parametern för begäran innehåller en eller flera instruktioner som filtrerar raderna i svaret. Varje instruktion innehåller ett fält och ett värde som är associerat `eq` med `ne` operatorerna or och som kan kombineras med hjälp av `and` eller `or` . Här följer några exempel på *filter* parametrar:<br/><br/> *filter = serviceCode EQ ' O365 '*<br/> *filter = serviceCode EQ ' O365 '* eller (*kanal EQ åter försäljare*)<br/><br/> Du kan ange följande fält:<br/><br/>**serviceCode**<br/>**serviceName**<br/>**kanalig**<br/>**customerTenantId**<br/>**customerName**<br/>**productId**<br/>**Namn**  | No |
| groupby           | sträng   | En instruktion som endast tillämpar data agg regering på de angivna fälten. Du kan ange följande fält:<br/><br/>**serviceCode**<br/>**serviceName**<br/>**kanalig**<br/>**customerTenantId**<br/>**customerName**<br/>**productId**<br/>**Namn**<br/><br/> De returnerade data raderna innehåller fälten som anges i *groupby* -parametern samt följande:<br/><br/>**licensesDeployed**<br/>**licensesSold**  | No |
| processedDateTime | DateTime | En kan ange det datum från vilket användnings data bearbetades. Standardvärdet är det senaste datumet då data bearbetades | No |

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

Om det lyckas innehåller svars texten följande fält som innehåller information om de licenser som har distribuerats.

| Fält             | Typ     | Description                           |
|-------------------|----------|---------------------------------------|
| serviceCode       | sträng   | Service kod                          |
| serviceName       | sträng   | Tjänstnamn                          |
| kanalig           | sträng   | Kanal namn, åter försäljare                |
| customerTenantId  | sträng   | Unikt ID för kunden    |
| customerName      | sträng   | Kundnamn                         |
| productId         | sträng   | Unikt ID för produkten     |
| Namn       | sträng   | Produktnamn                          |
| licensesDeployed  | long     | Antal distribuerade licenser           |
| licensesSold      | long     | Antal sålda licenser               |
| processedDateTime | DateTime | Datum när data senast bearbetades |

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
