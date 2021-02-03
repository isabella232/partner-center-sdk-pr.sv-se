---
title: Kontrol lera en kunds berättigande för att uppgradera till en Azure-plan
description: Du kan använda ProductUpgradeRequest-resursen för att returnera en ProductUpgradesEligibility-resurs för att avgöra om en kund är berättigad att uppgradera från en Microsoft Azure-prenumeration (MS-AZR-0145P) till en Azure-plan.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 568ed3f4cff7d9cd520e608d43cb89bb78e00ccc
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768724"
---
# <a name="check-a-customers-eligibility-for-upgrading-to-an-azure-plan"></a>Kontrol lera en kunds berättigande för att uppgradera till en Azure-plan

**Gäller för:**

- Partnercenter

Du kan använda [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) -resursen för att kontrol lera om en kund är berättigad till att uppgradera till en Azure-plan från en Microsoft Azure (MS-AZR-0145P)-prenumeration den här metoden returnerar en [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) -resurs med kundens produkt uppgraderings behörighet.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med app + användarautentiseringsuppgifter. Följ den [säkra appens modell](enable-secure-app-model.md) när du använder app + User Authentication med API: er för partner Center.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).

- Produkt serien.

## <a name="c"></a>C\#

Så här kontrollerar du om en kund är berättigad att uppgradera till Azure-planen:

1. Skapa ett **ProductUpgradesRequest** -objekt och ange kund-ID och "Azure" som produkt familj.

2. Använd samlingen **IAggregatePartner. ProductUpgrades** .
3. Anropa metoden **CheckEligibility** och skicka in **ProductUpgradesRequest** -objektet, vilket kommer att returnera ett **ProductUpgradesEligibility** -objekt.

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

### <a name="request-syntax"></a>Syntax för begäran

| Metod   | URI för förfrågan                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| **EFTER** | [*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/Eligibility http/1.1 |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

Begär ande texten måste innehålla en [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) -resurs.

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

Om det lyckas returnerar den här metoden en [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) -resurs i bröd texten.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).

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
