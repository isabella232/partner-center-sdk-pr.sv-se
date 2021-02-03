---
title: Skapa en produkt uppgraderings enhet för en kund
description: Du kan använda ProductUpgradeRequest-resursen för att skapa en enhet för produkt uppgradering för att uppgradera en kund till en specifik produkt familj.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 45830033d93e0906eafc169cf04b997e2ff7c3d8
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768814"
---
# <a name="create-a-product-upgrade-entity-for-a-customer"></a>Skapa en produkt uppgraderings enhet för en kund

**Gäller för:**

- Partnercenter

Du kan skapa en produkt uppgraderings enhet för att uppgradera en kund till en specifik produkt serie (till exempel Azure-plan) med hjälp av **ProductUpgradeRequest** -resursen.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med app + användarautentiseringsuppgifter. Följ den [säkra appens modell](enable-secure-app-model.md) när du använder app + User Authentication med API: er för partner Center.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).

- Produkt familjen som du vill uppgradera kunden till.

## <a name="c"></a>C\#

Uppgradera en kund till Azure-plan:

1. Skapa ett **ProductUpgradesRequest** -objekt och ange kund-ID och "Azure" som produkt familj.

2. Använd samlingen **IAggregatePartner. ProductUpgrades** .

3. Anropa metoden **create** och skicka i **ProductUpgradesRequest** -objektet, vilket kommer att returnera en **plats rubrik** sträng.

4. Extrahera **uppgraderings-ID: t** från plats huvud strängen som kan användas för att [fråga uppgraderings statusen](get-product-upgrade-status.md).

```csharp
// IAggregatePartner partnerOperations;

string selectedCustomerId = "58e2af4f-0ad3-4688-8744-be2357cd939a";

string selectedProductFamily = "Azure";

var productUpgradeRequest = new ProductUpgradesRequest
{
    CustomerId = selectedCustomerId,
    ProductFamily = selectedProductFamily
};

var productUpgradeLocationHeader = partnerOperations.ProductUpgrades.Create(productUpgradeRequest);

var upgradeId = Regex.Split(productUpgradeLocationHeader, "/")[1];

```

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod   | URI för förfrågan                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| **EFTER** | [*{baseURL}*](partner-center-rest-urls.md)/v1/productupgrades http/1.1 |

#### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

#### <a name="request-body"></a>Begärandetext

Begär ande texten måste innehålla en [ProductUpgradeRequest](product-upgrade-resources.md#productupgraderequest) -resurs.

#### <a name="request-example"></a>Exempel på begäran

```http
POST https://api.partnercenter.microsoft.com/v1/productupgrades HTTP/1.1
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
  "productFamily": "Azure"
}
```

## <a name="rest-response"></a>REST-svar

Om det lyckas innehåller svaret ett **plats** huvud som har en URI som kan användas för att hämta produkt uppgraderings status. Spara denna URI för användning med andra relaterade REST API: er.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: productUpgrades/42d075a4-bfe7-43e7-af6d-7c68a57edcb4
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: cb82f7d6-f0d9-44d4-82f9-f6eee6e68390
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
Date: Thu, 28 Sep 2019 20:35:35 GMT
```
