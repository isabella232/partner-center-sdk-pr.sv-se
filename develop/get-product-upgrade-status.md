---
title: Hämta produktuppgraderingsstatus för en kund
description: Du kan använda resursen ProductUpgradeRequest för att fastställa status för en produktuppgradering för en kund till en ny produktfamilj, till exempel från en Microsoft Azure-prenumeration (MS-AZR-0145P) till en Azure-plan.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e33ac61d77fc4e14ff6f7801e2c15a968cf9f1a667087df612c0f76b216f891a
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115995755"
---
# <a name="get-the-product-upgrade-status-for-a-customer"></a>Hämta produktuppgraderingsstatus för en kund

Du kan använda [**resursen ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) för att hämta statusen för en uppgradering till en ny produktfamilj. Den här resursen gäller när du uppgraderar en kund från en Microsoft Azure-prenumeration (MS-AZR-0145P) till en Azure-plan. En lyckad begäran returnerar [**resursen ProductUpgradesEligibility.**](product-upgrade-resources.md#productupgradeseligibility)

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med autentiseringsuppgifter för App+Användare. Följ den [säkra appmodellen när du](enable-secure-app-model.md) använder app-/användarautentisering med Partner Center-API:er.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard) Välj **CSP** på Menyn i Partnercenter följt av **Kunder**. Välj kunden i kundlistan och välj sedan **Konto.** På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.** Microsoft-ID:t är samma som kund-ID :t ( `customer-tenant-id` ).

- Produktfamiljen.

- Uppgraderings-ID för en uppgraderingsbegäran.

## <a name="c"></a>C\#

Så här kontrollerar du om en kund är berättigad att uppgradera till En Azure-plan:

1. Skapa ett **ProductUpgradesRequest-objekt** och ange kundidentifieraren och "Azure" som produktfamilj.

2. Använd **samlingen IAggregatePartner.ProductUpgrades.**

3. Anropa **ById-metoden** och skicka **upgrade-id.**

4. Anropa **checkStatus-metoden** och skicka objektet **ProductUpgradesRequest,** som returnerar ett **ProductUpgradeStatus-objekt.**

```csharp
// IAggregatePartner partnerOperations;

string selectedCustomerId = "58e2af4f-0ad3-4688-8744-be2357cd939a";

string selectedProductFamily = "azure";

var productUpgradeRequest = new ProductUpgradesRequest
{
    CustomerId = selectedCustomerId,
    ProductFamily = selectedProductFamily
};

ProductUpgradesStatus productUpgradeStatus = partnerOperations.ProductUpgrades.ById(selectedUpgradeId).CheckStatus(productUpgradeRequest);

if (productUpgradeEligibility.IsEligibile)
{
    ....
}

```

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod   | URI för förfrågan |
|----------|-----------------------------------------------------------------------------------------------|
| **Inlägg** | [*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/{upgrade-id}/status HTTP/1.1 |

### <a name="uri-parameter"></a>URI-parameter

Använd följande frågeparameter för att ange den kund som du får en produktuppgraderingsstatus för.

| Namn               | Typ | Obligatorisk | Beskrivning                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| **upgrade-id** | GUID | Yes | Värdet är en GUID-formaterad uppgraderingsidentifierare. Du kan använda den här identifieraren för att ange en uppgradering som ska spåras. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

Begärandetexten måste innehålla en [**ProductUpgradeRequest-resurs.**](product-upgrade-resources.md#productupgraderequest)

### <a name="request-example"></a>Exempel på begäran

```http
POST https://api.partnercenter.microsoft.com/v1/productupgrades/42d075a4-bfe7-43e7-af6d-7c68a57edcb4/status  HTTP/1.1
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
 {
    "customerId": "4c721420-72ad-4708-a0a7-371a2f7b0969",
    "productFamily": "azure"
  }
  "Attributes": {
  "ObjectType": "ProductUpgradeRequest"
  }
}
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden [**en ProductUpgradesEligibility-resurs**](product-upgrade-resources.md#productupgradeseligibility) i brödtexten.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)

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
    "id": "42d075a4-bfe7-43e7-af6d-7c68a57edcb4",
    "status": "Completed",
    "productFamily": "Azure",
    "lineItems": [
        {
            "sourceProduct": {
                "id": "b1beb621-3cad-4d7a-b360-62db33ce028e",
                "name": "AzureSubscription"
            },
            "targetProduct": {
                "id": "d231908e-31c1-de0e-027b-bc5ce11f09d9",
                "name": "Microsoft Azure plan"
            },
            "upgradedDate": "2019-08-29T23:47:28.8524555Z",
            "status": "Completed"
        }
    ]
}

```
