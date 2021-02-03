---
title: Skapa en kundvagn
description: 'Lär dig hur du använder API: er för partner Center för att lägga till en order för en kund i en varukorg. Avsnittet innehåller information om hur du skapar en kundvagn och eventuella krav.'
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: a1c559b415a7d42af4e904e09795f92aed7f125f
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770128"
---
# <a name="create-a-cart-with-a-customer-order"></a>Skapa en varukorg med en kund order

**Gäller för:**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Du kan lägga till en order för en kund i en varukorg. Mer information om vad som för närvarande är tillgängligt för försäljning finns [i partner erbjudanden i Cloud Solution Provider-programmet](/partner-center/csp-offers).

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Så här skapar du en order för en kund:

1. Instansiera ett vagn objekt.

2. Skapa en lista med **CartLineItem** -objekt och tilldela listan till vagnens rad objekt-egenskap. Varje vagn rads objekt innehåller inköps information för en produkt. Du måste ha minst ett artikel per vagns rad.

3. Hämta ett gränssnitt till shopping-åtgärder genom att anropa metoden **IAggregatePartner. Customers. ById** med kund-ID: t för att identifiera kunden och sedan hämta gränssnittet från egenskapen **kundvagn** .

4. Anropa **create** -eller **CreateAsync** -metoden för att skapa vagnen.

### <a name="c-example"></a>C- \# exempel

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

var cart = new Cart()
{
    LineItems = new List<CartLineItem>()
    {
        new CartLineItem()
        {
      /* Microsoft Azure Subscription */
            Id = 0,
            CatalogItemId = "MS-AZR-0145P",
            Quantity = 1,
            BillingCycle = BillingCycleType.Monthly,
            TermDuration = "P1Y"
        },
        new CartLineItem()
        {
      /* Azure Reserved Instance */
            Id = 1,
            CatalogItemId = "DZH318Z0BQ36:004G:DZH318Z08C0S",
            Quantity = 1,
            BillingCycle = BillingCycleType.OneTime,
            TermDuration = "P1Y",
            ProvisioningContext = new Dictionary<string, string>
            {
                { "subscriptionId", subscriptionId },
                { "scope", "shared" }
            }
        },
        new CartLineItem()
        {
      /* Azure Reserved Instance */
            Id = 2,
            CatalogItemId = "DZH318Z0BQ36:004J:DZH318Z08B8X",
            Quantity = 1,
            BillingCycle = BillingCycleType.OneTime,
            TermDuration = "P3Y",
            ProvisioningContext = new Dictionary<string, string>
            {
                { "subscriptionId", subscriptionId },
                { "scope", "shared" }
            }
        },
        new CartLineItem()
        {
      /* Perpetual Software */
            Id = 3,
            CatalogItemId = "DG7GMGF0DWM3:0002:DG7GMGF0DT1M",
            Quantity = 1,
            BillingCycle = BillingCycleType.OneTime
        },
        new CartLineItem()
        {
      /* SaaS */
            Id = 4,
            CatalogItemId = "DZH318Z0BXWC:0002:DZH318Z0BMRV",
            Quantity = 1,
            BillingCycle = BillingCycleType.Monthly,
            TermDuration = "P1M"
        },
        new CartLineItem()
        {
      /* SaaS Free Trial */
            Id = 5,
            CatalogItemId = "DZH318Z0C0WF:0001:DZH318Z0BP69",
            Quantity = 10,
            BillingCycle = BillingCycleType.None,
            TermDuration = "P1M",
            RenewsTo = new RenewsTo
            {
                TermDuration = "P1Y"
            }
        }
    }
};

cart = partnerOperations.Customers.ById(customerId).Carts.Create(cart);
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Så här skapar du en order för en kund:

1. Instansiera ett vagn objekt.

2. Skapa en lista med **CartLineItem** -objekt och tilldela listan till vagnens rad objekt. Varje vagn rads objekt innehåller inköps information för en produkt. Du måste ha minst ett artikel per vagns rad.

3. Hämta ett gränssnitt till shopping-åtgärder genom att anropa funktionen **IAggregatePartner. getCustomers (). byId** med kund-ID: t för att identifiera kunden och sedan hämta gränssnittet från **getCart** -funktionen.

4. Anropa **create** -funktionen för att skapa vagnen.

## <a name="java-example"></a>Java-exempel

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String subscriptionId;
// String catalogItemId;

CartLineItem lineItem = new CartLineItem();

lineItem.setBillingCycle(BillingCycleType.OneTime);
lineItem.setCatalogItemId(catalogItemId);
lineItem.setFriendlyName("Sample RI Purchase");
lineItem.setQuantity(1);

Map<String, String> provisioningContext = new HashMap<String,String>();

provisioningContext.put("duration", "3Years");
provisioningContext.put("scope", "shared");
provisioningContext.put("subscriptionId", subscriptionId);

lineItem.setProvisioningContext(provisioningContext);

List<CartLineItem> lineItemList = new ArrayList<CartLineItem>();
lineItemList.add(lineItem);

Cart cart = new Cart();
cart.setLineItems(lineItemList);

Cart cartCreated = partnerOperations.getCustomers().byId(customerId).getCarts().create(cart);
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Så här skapar du en order för en kund:

1. Instansiera ett vagn objekt.

2. Skapa en lista med **CartLineItem** -objekt och tilldela listan till vagnens rad objekt. Varje vagn rads objekt innehåller inköps information för en produkt. Du måste ha minst ett artikel per vagns rad.

3. Kör kommandot [**New-PartnerCustomerCart**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomerCart.md) för att skapa vagnen.

```powershell
# $customerId
# $subscriptionId
# $catalogItemId

$lineItem = New-Object -TypeName Microsoft.Store.PartnerCenter.PowerShell.Models.Carts.PSCartLineItem

$lineItem.BillingCycle = 'OneTime'
$lineItem.CatalogItemId = $catalogItemId
$lineItem.FriendlyName = 'Sample RI Purchase'
$lineItem.ProvisioningContext.Add('duration', '1Year')
$lineItem.ProvisioningContext.Add('scope', 'shared')
$lineItem.ProvisioningContext.Add('subscriptionId', $subsciptionId)
$lineItem.Quantity = 10

New-PartnerCustomerCart -CustomerId $customerId -LineItems $lineItem
```

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod   | URI för förfrågan                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **EFTER** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/carts http/1.1                        |

### <a name="uri-parameter"></a>URI-parameter

Använd följande Sök vägs parameter för att identifiera kunden.

| Namn            | Typ     | Obligatorisk | Beskrivning                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **kund-ID** | sträng   | Yes      | Ett GUID-formaterat kund-ID som identifierar kunden.             |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

I den här tabellen beskrivs egenskaperna för [kundvagn](cart-resources.md) i begär ande texten.

| Egenskap              | Typ             | Obligatorisk        | Beskrivning |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| id                    | sträng           | No              | Ett kundvagn-ID som anges när vagnen skapas.                                  |
| creationTimeStamp     | DateTime         | No              | Datumet då vagnen skapades i datum-/tids format. Används när vagnen har skapats.         |
| lastModifiedTimeStamp | DateTime         | No              | Datumet då vagnen senast uppdaterades i datum-/tids format. Används när vagnen har skapats.    |
| expirationTimeStamp   | DateTime         | No              | Datumet då vagnen upphör att gälla, i datum-/tids format.  Används när vagnen har skapats.            |
| lastModifiedUser      | sträng           | No              | Den användare som senast uppdaterade vagnen. Används när vagnen har skapats.                             |
| Rad objekt             | Objekt mat ris | Yes             | En matris med [CartLineItem](cart-resources.md#cartlineitem) -resurser.                                     |

I den här tabellen beskrivs egenskaperna för [CartLineItem](cart-resources.md#cartlineitem) i begär ande texten.

|      Egenskap       |            Typ             | Obligatorisk |                                                                                         Beskrivning                                                                                         |
|---------------------|-----------------------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         id          |           sträng            |    No    |                                                     En unik identifierare för ett vagn rads objekt. Används när vagnen har skapats.                                                     |
|      catalogId      |           sträng            |   Yes    |                                                                                Katalog objekt identifierare.                                                                                 |
|    friendlyName     |           sträng            |    No    |                                                    Valfritt. Det egna namnet på det objekt som definieras av partnern för att hjälpa disambiguate.                                                    |
|      quantity       |             int             |   Yes    |                                                                            Antalet licenser eller instanser.                                                                             |
|    currencyCode     |           sträng            |    No    |                                                                                     Valuta koden.                                                                                      |
|    billingCycle     |           Objekt            |   Yes    |                                                                    Typ av fakturerings cykel som angetts för den aktuella perioden.                                                                    |
|    deltagare     | Lista med objekt sträng par |    No    |                                                                En samling partner on Record (MPNID) på köpet.                                                                 |
| provisioningContext | Ord listans<sträng, sträng>  |    No    | Information krävs för etablering av vissa objekt i katalogen. Egenskapen provisioningVariables i en SKU anger vilka egenskaper som krävs för vissa objekt i katalogen. |
|     orderGroup      |           sträng            |    No    |                                                                   En grupp som visar vilka objekt som kan placeras tillsammans.                                                                   |
|        fel        |           Objekt            |    No    |                                                                     Tillämpas efter att kundvagn har skapats i händelse av ett fel.                                                                      |
|     renewsTo        | Objekt mat ris            |    No    |                                                    En matris med [RenewsTo](cart-resources.md#renewsto) -resurser.                                                                            |

I den här tabellen beskrivs egenskaperna för [RenewsTo](cart-resources.md#renewsto) i begär ande texten.

| Egenskap              | Typ             | Obligatorisk        | Beskrivning |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | sträng           | No              | En ISO 8601-representation av förnyelse periodens varaktighet. De aktuella värdena som stöds är **P1M** (1 månad) och **P1Y** (1 år). |

### <a name="request-example"></a>Exempel på begäran

```http
POST /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 496
Expect: 100-continue

{
  "lineItems": [
    {
    /* Microsoft Azure Subscription */
      "id": 0,
      "catalogItemId": "MS-AZR-0145P",
      "quantity": 1,
      "billingCycle": "monthly",
      "termDuration": "P1Y"
    },
    {
    /* Azure Reserved Instance */
      "id": 1,
      "catalogItemId": "DZH318Z0BQ36:004G:DZH318Z08C0S",
      "quantity": 1,
      "billingCycle": "one_time",
      "termDuration": "P1Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "shared"
      }
    },
    {
    /* Azure Reserved Instance */
      "id": 2,
      "catalogItemId": "DZH318Z0BQ36:004J:DZH318Z08B8X",
      "quantity": 1,
      "billingCycle": "one_time",
      "termDuration": "P3Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "single"
      }
    },
    {
    /* Perpetual Software */
      "id": 3,
      "catalogItemId": "DG7GMGF0DWTL:0001:DG7GMGF0DSFM",
      "quantity": 1,
      "billingCycle": "one_time"
    },
    {
    /* SaaS */
      "id": 4,
      "catalogItemId": "DZH318Z0BXWC:0002:DZH318Z0BMRV",
      "quantity": 1,
      "billingCycle": "monthly",
      "termDuration": "P1M"
    },
  {
    /* SaaS Free Trial */
       "id": 5,
       "catalogItemId": "DZH318Z0C0WF:0001:DZH318Z0BP69",
       "quantity": 10,
       "billingCycle": "none",
       "termDuration": "P1M",
       "renewsTo": {
         "termDuration": "P1Y"
       }
    }
  ]
}
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden den fyllda kund [vagns](cart-resources.md) resursen i svars texten.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [felkoder](error-codes.md).

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 201 Created
Content-Length: 764
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
X-Locale: en-US,en-US
MS-CV: sF/wRa2ih0CzbABc.0
MS-ServerId: 000001
Date: Thu, 15 Mar 2018 17:15:01 GMT
{
  "id": "3655b1a0-b1c9-4268-9824-577fdbc4d0be",
  "creationTimestamp": "2019-01-16T00:45:41.6062996Z",
  "lastModifiedTimestamp": "2019-01-16T00:45:41.6062996Z",
  "expirationTimestamp": "2019-01-16T01:00:54.4188497Z",
  "lastModifiedUser": "1824b7fc-2fac-4478-b177-66823c40ab75",
  "status": "Active",
  "lineItems": [
    {
      "id": 0,
      "catalogItemId": "MS-AZR-0145P",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "monthly",
      "termDuration": "P1Y",
      "orderGroup": "OMS-0"
    },
    {
      "id": 1,
      "catalogItemId": "DZH318Z0BQ36:004G:DZH318Z08C0S",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "one_time",
      "termDuration": "P1Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "shared"
      },
      "orderGroup": "0"
    },
    {
      "id": 2,
      "catalogItemId": "DZH318Z0BQ36:004J:DZH318Z08B8X",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "one_time",
      "termDuration": "P3Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "shared"
      },
      "orderGroup": "0"
    },
    {
      "id": 3,
      "catalogItemId": "DG7GMGF0DWM3:0002:DG7GMGF0DT1M",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "one_time",
      "orderGroup": "0"
    },
    {
      "id": 4,
      "catalogItemId": "DZH318Z0BXWC:0002:DZH318Z0BMRV",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "monthly",
      "termDuration": "P1M",
      "orderGroup": "1"
    },
  {
      "id": 5,
      "catalogItemId": "DZH318Z0C0WF:0001:DZH318Z0BP69",
      "quantity": 10,
      "currencyCode": "USD",
      "billingCycle": "none",
      "termDuration": "P1M",
      "renewsTo": {
  "termDuration": "P1Y"
      },
    "orderGroup": "2"
    }
  ],
  "links": {
    "self": {
      "uri": "/customers/28045616-f6b9-462f-9701-0d89b5e65c44/carts/3655b1a0-b1c9-4268-9824-577fdbc4d0be",
      "method": "GET",
      "headers": []
    }
  },
  "attributes": {
    "objectType": "Cart"
  }
}
```
