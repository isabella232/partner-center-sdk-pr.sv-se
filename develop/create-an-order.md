---
title: Skapa en kund order
description: 'Lär dig hur du använder API: er för partner Center för att skapa en order för en kund. Artikeln innehåller krav, steg och exempel.'
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ce176909a1f9c350f1c16615171de57a7beb888d
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770125"
---
# <a name="create-an-order-for-a-customer-using-partner-center-apis"></a>Skapa en order för en kund med hjälp av API: er för partner Center

**Gäller för:**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Att skapa en **beställning för reserverade produkter från virtuella Azure-datorer** gäller *endast* för:

- Partnercenter

Information om vad som för närvarande är tillgängligt för försäljning finns [i partner erbjudanden i Cloud Solution Provider-programmet](/partner-center/csp-offers).

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).

- Ett erbjudande-ID.

## <a name="c"></a>C\#

Så här skapar du en order för en kund:

1. Instansiera ett [**order**](order-resources.md) -objekt och ange **ReferenceCustomerID** -egenskapen till kund-ID: t för att registrera kunden.

2. Skapa en lista med [**OrderLineItem**](order-resources.md#orderlineitem) -objekt och tilldela listan till orderns **rad objekt** -egenskap. Varje order rads objekt innehåller inköps information för ett erbjudande. Du måste ha minst ett order rads objekt.

3. Hämta ett gränssnitt för att beställa åtgärder. Anropa först metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: t för att identifiera kunden. Hämta sedan gränssnittet från egenskapen [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) .

4. Anropa metoden [**create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) eller [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) och skicka det till [**order**](order-resources.md) -objektet.

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string offerId;

var order = new Order()
{
    ReferenceCustomerId = customerId,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            OfferId = offerId,
            FriendlyName = "new offer purchase",
            Quantity = 1,
            ProvisioningContext = new Dictionary<string, string>
            {
                { "subscriptionId", "5198C069-3DAA-403A-8660-5BE11BFD12EE" },
                { "scope", "shared" },
                { "duration", "3Years" }
            }
        }
    }
};

var createdOrder = partnerOperations.Customers.ById(customerId).Orders.Create(order);
```

**Exempel**: [konsol test app](console-test-app.md). **Projekt**: Partner Center SDK-exempel **klass**: CreateOrder.CS

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod   | URI för förfrågan                                                                            |
|----------|----------------------------------------------------------------------------------------|
| **EFTER** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Orders http/1.1 |

#### <a name="uri-parameters"></a>URI-parametrar

Använd följande Sök vägs parameter för att identifiera kunden.

| Namn        | Typ   | Obligatorisk | Beskrivning                                                |
|-------------|--------|----------|------------------------------------------------------------|
| kund-ID | sträng | Yes      | Ett GUID-formaterat kund-ID som identifierar kunden. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

#### <a name="order"></a>Beställning

I den här tabellen beskrivs [beställnings](order-resources.md) egenskaperna i begär ande texten.

| Egenskap             | Typ                        | Obligatorisk                        | Beskrivning                                                                   |
|----------------------|-----------------------------|---------------------------------|-------------------------------------------------------------------------------|
| id                   | sträng                      | No                              | En beställnings identifierare som anges när beställningen har skapats.   |
| referenceCustomerId  | sträng                      | No                              | Kund-ID. |
| billingCycle         | sträng                      | No                              | Anger med vilken frekvens partnern faktureras för den här ordern. De värden som stöds är medlems namnen som finns i [BillingCycleType](product-resources.md#billingcycletype). Standardvärdet är "Monthly" eller "Databasmigrering" när ordern skapas. Det här fältet används när beställningen har skapats. |
| Rad objekt            | matris med [OrderLineItem](order-resources.md#orderlineitem) -resurser | Yes      | En lista med specificerade erbjudanden som kunden köper inklusive kvantiteten.        |
| currencyCode         | sträng                      | No                              | Skrivskyddad. Den valuta som används när ordern placeras. Används när beställningen har skapats.           |
| creationDate         | datetime                    | No                              | Skrivskyddad. Datumet då ordern skapades i datum-/tids format. Används när beställningen har skapats.                                   |
| status               | sträng                      | No                              | Skrivskyddad. Status för ordern.  De värden som stöds är medlems namnen som finns i [OrderStatus](order-resources.md#orderstatus).        |
| Länkar                | [OrderLinks](utility-resources.md#resourcelinks)              | No                              | Resurs länkarna som motsvarar beställningen. |
| dokumentattribut           | [ResourceAttributes](utility-resources.md#resourceattributes) | No                              | De metadata-attribut som motsvarar beställningen. |

#### <a name="orderlineitem"></a>OrderLineItem

I den här tabellen beskrivs egenskaperna för [OrderLineItem](order-resources.md#orderlineitem) i begär ande texten.

>[!NOTE]
>PartnerIdOnRecord bör endast anges när en indirekt leverantör placerar en order på uppdrag av en indirekt åter försäljare. Den används endast för att lagra Microsoft Partner Network-ID: t för den indirekta åter försäljaren (aldrig ID: t för den indirekta providern).

| Namn                 | Typ   | Obligatorisk | Beskrivning                                                                                                                                                                                                                                |
|----------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| lineItemNumber       | int    | Yes      | Varje rad objekt i samlingen får ett unikt rad nummer, räknat från 0 till count-1.                                                                                                                                                 |
| offerId              | sträng | Yes      | Erbjudande-ID.                                                                                                                                                                                                                      |
| subscriptionId       | sträng | No       | Prenumerations-ID.                                                                                                                                                                                                               |
| parentSubscriptionId | sträng | No       | Valfritt. ID: t för den överordnade prenumerationen i ett tilläggs erbjudande. Gäller enbart för korrigering.                                                                                                                                                     |
| friendlyName         | sträng | No       | Valfritt. Det egna namnet på prenumerationen som definieras av partnern för att hjälpa disambiguate.                                                                                                                                              |
| quantity             | int    | Yes      | Antalet licenser för en licens baserad prenumeration.                                                                                                                                                                                   |
| partnerIdOnRecord    | sträng | No       | När en indirekt åter försäljare placerar en indirekt åter försäljare, fyller du i det här fältet med MPN-ID: t för den **indirekta åter försäljaren** (aldrig ID: t för den indirekta providern). Detta säkerställer korrekt redovisning av incitament. |
| provisioningContext  | Ord listans<sträng, sträng>                | No       |  Information krävs för etablering av vissa objekt i katalogen. Egenskapen provisioningVariables i en SKU anger vilka egenskaper som krävs för vissa objekt i katalogen.                  |
| Länkar                | [OrderLineItemLinks](order-resources.md#orderlineitemlinks) | No       |  Skrivskyddad. Resurs länkarna som motsvarar order rads objektet.  |
| dokumentattribut           | [ResourceAttributes](utility-resources.md#resourceattributes) | No       | De metadata-attribut som motsvarar OrderLineItem. |
| renewsTo             | Objekt mat ris                          | No    |En matris med [RenewsTo](order-resources.md#renewsto) -resurser.                                                                            |

##### <a name="renewsto"></a>RenewsTo

I den här tabellen beskrivs egenskaperna för [RenewsTo](order-resources.md#renewsto) i begär ande texten.

| Egenskap              | Typ             | Obligatorisk        | Beskrivning |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | sträng           | No              | En ISO 8601-representation av förnyelse periodens varaktighet. De aktuella värdena som stöds är **P1M** (1 månad) och **P1Y** (1 år). |

### <a name="request-example"></a>Exempel på begäran

```http
POST https://api.partnercenter.microsoft.com/v1/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Content-Length: 691
Content-Type: application/json

{
  "BillingCycle": "one_time",
  "CurrencyCode": "USD",
  "LineItems": [
    {
      "LineItemNumber": 0,
      "ProvisioningContext": {
        "subscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
        "scope": "shared",
        "duration": "1Year"
      },
      "OfferId": "DZH318Z0BQ4B:0047:DZH318Z0DSM8",
      "FriendlyName": "A_sample_Azure_RI",
      "Quantity": 1
    }
  ]
}
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar metoden en [order](order-resources.md) resurs i svars texten.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [fel koder för partner Center](error-codes.md).

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 201 Created
Content-Length: 788
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b593cbb7-b358-4b31-81fc-e60b9c277a7f
MS-RequestId: 025f4c19-217f-49d6-a056-391902c62fb3
Date: Thu, 15 Mar 2018 22:30:02 GMT

{
  "id": "Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1",
  "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
  "billingCycle": "one_time",
  "currencyCode": "USD",
  "lineItems": [
    {
        "lineItemNumber": 0,
        "offerId": "84A03D81-6B37-4D66-8D4A-FAEA24541538",
        "friendlyName": "A_sample_Azure_RI",
        "quantity": 1,
        "links": {
            "sku": {
                "uri": "/products/DZH318Z0BQ4B/skus/0047?country=US",
                "method": "GET",
                "headers": []
            }
        }
    } ],
    "creationDate": "2018-03-15T22:30:02.085152Z",
    "status": "pending",
    "links": {
        "provisioningStatus": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1/provisioningstatus",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Order"
    }
}
```
