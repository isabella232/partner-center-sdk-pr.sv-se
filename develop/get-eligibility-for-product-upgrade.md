---
title: Kontrollera om en kund är berättigad för uppgradering till en Azure-plan
description: Du kan använda resursen ProductUpgradeRequest för att returnera en ProductUpgradesEligibility-resurs för att avgöra om en kund är berättigad att uppgradera från en Microsoft Azure-prenumeration (MS-AZR-0145P) till en Azure-plan.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: a72a9f2f3909ac4b3b74754b58a8d8d4745fbb2cadd101ad18cf487b1b02267a
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996035"
---
# <a name="check-a-customers-eligibility-for-upgrading-to-an-azure-plan"></a>Kontrollera om en kund är berättigad för uppgradering till en Azure-plan

Du kan använda resursen [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) för att kontrollera om en kund är berättigad att uppgradera till en Azure-plan från en Microsoft Azure-prenumeration (MS-AZR-0145P) Den här metoden returnerar en [**ProductUpgradesEligibility-resurs**](product-upgrade-resources.md#productupgradeseligibility) med kundens berättigande för produktuppgradering.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md) Det här scenariot stöder autentisering med autentiseringsuppgifter för App+Användare. Följ den [säkra appmodellen när](enable-secure-app-model.md) du använder app-+användarautentisering med Partner Center-API:er.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard) Välj **CSP** på Menyn i Partnercenter följt av **Kunder.** Välj kunden i kundlistan och välj sedan **Konto.** På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.** Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).

- Produktfamiljen.

## <a name="c"></a>C\#

Så här kontrollerar du om en kund är berättigad att uppgradera till En Azure-plan:

1. Skapa ett **ProductUpgradesRequest-objekt** och ange kundidentifieraren och "Azure" som produktfamilj.

2. Använd **samlingen IAggregatePartner.ProductUpgrades.**
3. Anropa **metoden CheckEligibility** och skicka objektet **ProductUpgradesRequest,** som returnerar ett **ProductUpgradesEligibility-objekt.**

```csharp
// IAggregatePartner partnerOperations;

string selectedCustomerId = "58e2af4f-0ad3-4688-8744-be2357cd939a";

string selectedProductFamily = "azure";

var productUpgradeRequest = new ProductUpgradesRequest
{
    CustomerId = selectedCustomerId,
    ProductFamily = selectedProductFamily
};

ProductUpgradesEligibility productUpgradeEligibility = partnerOperations.ProductUpgrades.CheckEligibility(productUpgradeRequest);

if (productUpgradeEligibility.IsEligibile)
{
    ....
}

```

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod   | URI för förfrågan                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| **Inlägg** | [*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/berättigande HTTP/1.1 |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

Begärandetexten måste innehålla en [**ProductUpgradeRequest-resurs.**](product-upgrade-resources.md#productupgraderequest)

### <a name="request-example"></a>Exempel på begäran

```http
POST https://api.partnercenter.microsoft.com/v1/productupgrades/eligibility HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c245d5f2-1de3-4ae0-9e42-95e38e3cb8ff
MS-CorrelationId: e3f26e6a-044f-4371-ad52-0d91ce4200be
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 340
Expect: 100-continue
Connection: Keep-Alive
{
        "customerId": "4c721420-72ad-4708-a0a7-371a2f7b0969",
        "productFamily": "azure"
}
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden [**en ProductUpgradesEligibility-resurs**](product-upgrade-resources.md#productupgradeseligibility) i brödtexten.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 Ok
Content-Length: 150
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: cb82f7d6-f0d9-44d4-82f9-f6eee6e68390
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
Date: Thu, 04 Oct 2019 20:35:35 GMT

{
    "customerId": "c1958bc7-3284-4952-a257-de594ee64743",
    "isEligible": true,
    "productFamily": "azure"
}
```
