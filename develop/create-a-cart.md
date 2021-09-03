---
title: Skapa en kundvagn
description: Lär dig hur du använder Partner Center-API:er för att lägga till en order för en kund i en kundvagn. Avsnittet innehåller information om hur du skapar en kundvagn och eventuella krav.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: abe7a0842b0ecf52b217b277cf61603d5c86a368
ms.sourcegitcommit: e1db965e8c7b4fe3aaa0ecd6cefea61973ca2232
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/03/2021
ms.locfileid: "123456100"
---
# <a name="create-a-cart-with-a-customer-order"></a>Skapa en kundvagn med en kundorder

**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Tyskland-| Partnercenter för Microsoft Cloud for US Government

Du kan lägga till en order för en kund i en kundvagn. Mer information om vad som för närvarande är tillgängligt för försäljning finns [i Partnererbjudanden i Molnlösningsleverantör program](/partner-center/csp-offers).

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md) Det här scenariot stöder autentisering med både fristående app- och app+användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard) Välj **CSP** på Menyn i Partnercenter följt av **Kunder.** Välj kunden i kundlistan och välj sedan **Konto.** På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.** Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Så här skapar du en order för en kund:

1. Instansiera ett kundvagnsobjekt.

2. Skapa en lista över **CartLineItem-objekt** och tilldela listan till kundvagnens egenskap LineItems. Varje kundvagnsrad innehåller inköpsinformationen för en produkt. Du måste ha minst en kundvagnsrad.

3. Hämta ett gränssnitt för kundvagnsåtgärder genom att anropa metoden **IAggregatePartner.Customers.ById** med kund-ID:t för att identifiera kunden och sedan hämta gränssnittet från **egenskapen Cart.**

4. Anropa metoden **Create** eller **CreateAsync** för att skapa kundvagnen.

### <a name="c-example"></a>\#C-exempel

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

1. Instansiera ett kundvagnsobjekt.

2. Skapa en lista över **CartLineItem-objekt** och tilldela listan till kundvagnens radobjekt. Varje kundvagnsrad innehåller inköpsinformationen för en produkt. Du måste ha minst en kundvagnsrad.

3. Hämta ett gränssnitt för kundvagnsåtgärder genom att anropa funktionen **IAggregatePartner.getCustomers().byId** med kund-ID:t för att identifiera kunden och sedan hämta gränssnittet från **funktionen getCart.**

4. Anropa **create-funktionen** för att skapa kundvagnen.

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

1. Instansiera ett kundvagnsobjekt.

2. Skapa en lista över **CartLineItem-objekt** och tilldela listan till kundvagnens radobjekt. Varje kundvagnsrad innehåller inköpsinformationen för en produkt. Du måste ha minst en kundvagnsrad.

3. Kör kommandot [**New-PartnerCustomerCart**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomerCart.md) för att skapa kundvagnen.

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

### <a name="request-syntax"></a>Begärandesyntax

| Metod   | URI för förfrågan                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **INLÄGG** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts HTTP/1.1                        |

### <a name="uri-parameter"></a>URI-parameter

Använd följande sökvägsparameter för att identifiera kunden.

| Namn            | Typ     | Obligatorisk | Beskrivning                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **kund-ID** | sträng   | Yes      | Ett GUID-formaterat kund-ID som identifierar kunden.             |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

I den här tabellen beskrivs [egenskaperna för](cart-resources.md) Kundvagn i begärandetexten.

| Egenskap              | Typ             | Obligatorisk        | Beskrivning |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| id                    | sträng           | No              | En kundvagnsidentifierare som anges när kundvagnen har skapats.                                  |
| creationTimeStamp     | DateTime         | No              | Det datum då kundvagnen skapades i datum/tid-format. Tillämpas när kundvagnen har skapats.         |
| lastModifiedTimeStamp | DateTime         | No              | Datum då kundvagnen senast uppdaterades i datum/tid-format. Tillämpas när kundvagnen har skapats.    |
| expirationTimeStamp   | DateTime         | No              | Datumet då kundvagnen upphör att gälla i datum/tid-format.  Tillämpas när kundvagnen har skapats.            |
| lastModifiedUser      | sträng           | No              | Den användare som senast uppdaterade kundvagnen. Tillämpas när kundvagnen har skapats.                             |
| lineItems             | Matris med objekt | Yes             | En matris med [CartLineItem-resurser.](cart-resources.md#cartlineitem)                                     |

I den här tabellen beskrivs [egenskaperna för CartLineItem](cart-resources.md#cartlineitem) i begärandetexten.

|      Egenskap       |            Typ             | Obligatorisk |                                                                                         Beskrivning                                                                                         |
|---------------------|-----------------------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         id          |           sträng            |    No    |                                                     En unik identifierare för ett radobjekt i kundvagnen. Tillämpas när kundvagnen har skapats.                                                     |
|      catalogId      |           sträng            |   Yes    |                                                                                Katalogobjektets identifierare.                                                                                 |
|    friendlyName     |           sträng            |    No    |                                                    Valfritt. Det egna namnet för objektet som definierats av partnern för att undvika tvetydighet.                                                    |
|      quantity       |             int             |   Yes    |                                                                            Antalet licenser eller instanser.                                                                             |
|    currencyCode     |           sträng            |    No    |                                                                                     Valutakoden.                                                                                      |
|    billingCycle     |           Objekt            |   Yes    |                                                                    Den typ av faktureringsperiod som angetts för den aktuella perioden.                                                                    |
|    deltagare     | Lista över objektsträngpar |    No    |                                                                En samling PartnerId on Record (MPNID) för köpet.                                                                 |
| provisioningContext | Ordlista<sträng, sträng>  |    No    | Information som krävs för etablering för vissa objekt i katalogen. Egenskapen provisioningVariables i en SKU anger vilka egenskaper som krävs för specifika objekt i katalogen. |
|     orderGroup      |           sträng            |    No    |                                                                   En grupp som anger vilka objekt som kan placeras tillsammans.                                                                   |
|        fel        |           Objekt            |    No    |                                                                     Tillämpas när kundvagnen har skapats om det finns ett fel.                                                                      |
|     renewsTo        | Matris med objekt            |    No    |                                                    En matris med [RenewsTo-resurser.](cart-resources.md#renewsto)                                                                            |
|     AttestationAccepted        | Boolesk            |    No    |                                                   Anger avtal för att erbjuda eller SKU-villkor. Krävs endast för erbjudanden eller SKU:er där SkuAttestationProperties eller OfferAttestationProperties enforceAttestation är True.                                                                             |

I den här tabellen beskrivs [egenskaperna RenewsTo](cart-resources.md#renewsto) i begärandetexten.

| Egenskap              | Typ             | Obligatorisk        | Beskrivning |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | sträng           | No              | En ISO 8601-representation av förnyelseperiodens varaktighet. De aktuella värdena som stöds **är P1M** (1 månad) och **P1Y** (1 år). |

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

Om det lyckas returnerar den här metoden den ifyllda [kundvagnsresursen](cart-resources.md) i svarstexten.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder.](error-codes.md)

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


## <a name="example-for-new-commerce-license-based-services"></a>Exempel för licensbaserade tjänster för ny handel

> [!Note] 
> Nya handelsändringar är för närvarande endast tillgängliga för partner som ingår i den tekniska förhandsversionen av den nya handelsupplevelsen M365/D365

### <a name="request-example"></a>Exempel på begäran

```http
POST /v1/customers/932c4101-dc08-461b-b4c1-75d80e905775/carts HTTP/1.1
Host: api.partnercenter.microsoft.com
Content-Type: application/json
Content-Length: 165

{
    "LineItems": [
        {
            "CatalogItemId":"CFQ7TTC0LFLZ:0002:CFQ7TTC0K4TS",
            "Quantity": 1,
            "TermDuration": "P1M",
                    "BillingCycle": "Monthly"
        }
    ]
}

```

### <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden den ifyllda [kundvagnsresursen](cart-resources.md) i svarstexten.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder.](error-codes.md)

### <a name="response-example"></a>Exempel på svar

```http

{
    "id": "6b6ba6ea-d1ea-4c2c-9e1c-bec4f61e2049",
    "creationTimestamp": "2021-02-24T19:26:06.947164Z",
    "lastModifiedTimestamp": "2021-02-24T19:26:06.9471649Z",
    "expirationTimestamp": "2021-03-03T19:26:09.0035129Z",
    "lastModifiedUser": "004ec05e-8999-4d02-9315-2b1b667c0deb",
    "status": "Active",
    "lineItems": [
        {
            "id": 0,
            "catalogItemId": "CFQ7TTC0LFLZ:0002:CFQ7TTC0K4TS",
            "quantity": 1,
            "currencyCode": "USD",
            "billingCycle": "monthly",
            "termDuration": "P1M",
            "provisioningContext": {},
            "orderGroup": "0"
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/932c4101-dc08-461b-b4c1-75d80e905775/carts/6b6ba6ea-d1ea-4c2c-9e1c-bec4f61e2049",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Cart"
    }
}



```
