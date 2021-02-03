---
title: Skapa kund ordning för indirekt åter försäljare
description: 'Lär dig hur du använder API: er för partner Center för att skapa en order för en indirekt åter försäljares kund. Artikeln innehåller krav, steg och exmaples.'
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f72ecec8d82e6b8a1bc53c277206cafd7d8a4e03
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770153"
---
# <a name="create-an-order-for-a-customer-of-an-indirect-reseller"></a>Skapa en beställning för en kund till en indirekt återförsäljare

**Gäller för:**

- Partnercenter

Så här skapar du en order för en indirekt åter försäljares kund.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).

- Erbjudande identifieraren för det objekt som ska köpas.

- Klient-ID för den indirekta åter försäljaren.

## <a name="c"></a>C\#

Så här skapar du en order för en indirekt åter försäljares kund:

1. Hämta en samling av de indirekta åter försäljare som har en relation med den inloggade partnern.

2. Hämta en lokal variabel till objektet i samlingen som matchar det indirekta åter försäljarens ID. Det här steget hjälper dig att komma åt åter försäljarens [**MpnId**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationship.mpnid) -egenskap när du skapar ordern.

3. Instansiera ett [**order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) -objekt och ange [**ReferenceCustomerID**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.referencecustomerid) -egenskapen till kund-ID för att kunna registrera kunden.

4. Skapa en lista med [**OrderLineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) -objekt och tilldela listan till orderns [**rad objekt**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.lineitems) -egenskap. Varje order rads objekt innehåller inköps information för ett erbjudande. Var noga med att fylla i egenskapen [**PartnerIdOnRecord**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem.partneridonrecord) i varje rad objekt med MPN-ID: t för den indirekta åter försäljaren. Du måste ha minst ett order rads objekt.

5. Hämta ett gränssnitt för att beställa åtgärder genom att anropa metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: t för att identifiera kunden och hämta sedan gränssnittet från egenskapen [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) .

6. Anropa [**create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) -eller [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) -metoden för att skapa ordern.

### <a name="c-example"></a>C- \# exempel

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string offerId;
// string indirectResellerId;

// Get the indirect resellers with a relationship to the signed-in partner.
var indirectResellers = partnerOperations.Relationships.Get(PartnerRelationshipType.IsIndirectCloudSolutionProviderOf);

// Find the matching reseller in the collection.
var selectedIndirectReseller = (indirectResellers != null && indirectResellers.Items.Any()) ?
    indirectResellers.Items.FirstOrDefault(reseller => reseller.Id.Equals(indirectResellerId, StringComparison.OrdinalIgnoreCase)) :
    null;

// Prepare the order and populate the PartnerIdOnRecord with the reseller&#39;s Microsoft Partner Network Id.
var order = new Order()
{
    ReferenceCustomerId = customerId,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            OfferId = offerId,
            FriendlyName = "New offer purchase.",
            Quantity = 5,
            PartnerIdOnRecord = selectedIndirectReseller != null ? selectedIndirectReseller.MpnId : null
        }
    }
};

// Place the order.
var createdOrder = partnerOperations.Customers.ById(customerId).Orders.Create(order);
```

**Exempel**: [konsol test app](console-test-app.md)-**projekt**: Partner Center SDK-exempel **klass**: PlaceOrderForCustomer.CS

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod   | URI för förfrågan                                                                            |
|----------|----------------------------------------------------------------------------------------|
| **EFTER** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Orders http/1.1 |

#### <a name="uri-parameters"></a>URI-parametrar

Använd följande Sök vägs parameter för att identifiera kunden.

| Namn        | Typ   | Obligatorisk | Beskrivning                                           |
|-------------|--------|----------|-------------------------------------------------------|
| kund-ID | sträng | Yes      | En GUID-formaterad sträng som identifierar kunden. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

#### <a name="order"></a>Beställning

I den här tabellen beskrivs **beställnings** egenskaperna i begär ande texten.

| Namn | Typ | Obligatorisk | Beskrivning |
| ---- | ---- | -------- | ----------- |
| id | sträng | No | En beställnings identifierare som anges när beställningen har skapats. |
| referenceCustomerId | sträng | Yes | Kund-ID. |
| billingCycle | sträng | No | Den frekvens med vilken partnern debiteras för den här ordern. Standardvärdet är &quot; månatlig &quot; och används när beställningen har skapats. De värden som stöds är medlems namnen som finns i [**BillingCycleType**](/dotnet/api/microsoft.store.partnercenter.models.offers.billingcycletype). OBS! den årliga fakturerings funktionen är ännu inte allmänt tillgänglig. Support för årlig fakturering kommer snart. |
| Rad objekt | objekt mat ris | Yes | En matris med [**OrderLineItem**](#orderlineitem) -resurser. |
| creationDate | sträng | No | Datumet då ordern skapades i datum-/tids format. Används när beställningen har skapats. |
| dokumentattribut | objekt | No | Innehåller "ObjectType": "order". |

#### <a name="orderlineitem"></a>OrderLineItem

I den här tabellen beskrivs egenskaperna för **OrderLineItem** i begär ande texten.

| Namn | Typ | Obligatorisk | Beskrivning |
| ---- | ---- | -------- | ----------- |
| lineItemNumber | int | Yes | Varje rad objekt i samlingen får ett unikt rad nummer, räknat från 0 till count-1. |
| offerId | sträng | Yes | Erbjudande-ID. |
| subscriptionId | sträng | No | Prenumerations-ID. |
| parentSubscriptionId | sträng | No | Valfritt. ID: t för den överordnade prenumerationen i ett tilläggs erbjudande. Gäller enbart för korrigering. |
| friendlyName | sträng | No | Valfritt. Det egna namnet på prenumerationen som definieras av partnern för att hjälpa disambiguate. |
| quantity | int | Yes | Antalet licenser för en licens baserad prenumeration. |
| partnerIdOnRecord | sträng | No | När en indirekt åter försäljare placerar en indirekt åter försäljare, fyller du i det här fältet med MPN-ID: t för den **indirekta åter försäljaren** (aldrig ID: t för den indirekta providern). Detta säkerställer korrekt redovisning av incitament. **Det gick inte att ange MPN-ID: t för åter försäljaren. Åter försäljaren registreras dock inte, vilket innebär att incitaments beräkningar kanske inte omfattar försäljningen.** |
| dokumentattribut | objekt | No | Innehåller "ObjectType": "OrderLineItem". |

### <a name="request-example"></a>Exempel på begäran

```http
POST https://api.partnercenter.microsoft.com/v1/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/orders HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 02109f46-3ff2-4be4-9f37-b2eb6d58d542
MS-CorrelationId: 85195ae6-3de5-4978-abd4-7be2fbfe4c84
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 410
Expect: 100-continue

{
    "Id": null,
    "ReferenceCustomerId": "c501c3c4-d776-40ef-9ecf-9cefb59442c1",
    "BillingCycle": "unknown",
    "LineItems": [{
            "LineItemNumber": 0,
            "OfferId": "DB2E705F-B82A-4024-A3D5-D88E12F2DB35",
            "SubscriptionId": null,
            "ParentSubscriptionId": null,
            "FriendlyName": "New offer purchase.",
            "Quantity": 5,
            "PartnerIdOnRecord": "4847383",
            "Attributes": {
                "ObjectType": "OrderLineItem"
            }
        }
    ],
    "CreationDate": null,
    "Attributes": {
        "ObjectType": "Order"
    }
}
```

## <a name="rest-response"></a>REST-svar

Om det lyckas innehåller svars texten den ifyllda [order](order-resources.md) resursen.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [fel koder för partner Center](error-codes.md).

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 201 Created
Content-Length: 831
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 85195ae6-3de5-4978-abd4-7be2fbfe4c84
MS-RequestId: 02109f46-3ff2-4be4-9f37-b2eb6d58d542
MS-CV: Nd3Oum/L5EywtKQK.0
MS-ServerId: 020021921
Date: Mon, 10 Apr 2017 23:02:24 GMT

{
    "id": "3eddcac6-63b2-4c40-b0b6-f47e18301492",
    "referenceCustomerId": "c501c3c4-d776-40ef-9ecf-9cefb59442c1",
    "billingCycle": "monthly",
    "lineItems": [{
            "lineItemNumber": 0,
            "offerId": "DB2E705F-B82A-4024-A3D5-D88E12F2DB35",
            "subscriptionId": "42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
            "friendlyName": "New offer purchase.",
            "quantity": 5,
            "partnerIdOnRecord": "4847383",
            "links": {
                "subscription": {
                    "uri": "/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/subscriptions/42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2017-04-10T16:02:25.983-07:00",
    "links": {
        "self": {
            "uri": "/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/orders/3eddcac6-63b2-4c40-b0b6-f47e18301492",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "etag": "eyJpZCI6IjNlZGRjYWM2LTYzYjItNGM0MC1iMGI2LWY0N2UxODMwMTQ5MiIsInZlcnNpb24iOjF9",
        "objectType": "Order"
    }
}
```
