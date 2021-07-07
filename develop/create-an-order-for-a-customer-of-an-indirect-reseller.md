---
title: Skapa kundorder för indirekt återförsäljare
description: Lär dig hur du använder Partner Center-API:er för att skapa en order för en kund till en indirekt återförsäljare. Artikeln innehåller krav, steg och exempel.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6253ba2289ea1f58e7d8eaa960d7d0daaa887f0d
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973559"
---
# <a name="create-an-order-for-a-customer-of-an-indirect-reseller"></a>Skapa en beställning för en kund till en indirekt återförsäljare

Hur du skapar en order för en kund till en indirekt återförsäljare.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md) Det här scenariot har endast stöd för autentisering med app- och användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard) Välj **CSP** på Menyn i Partnercenter följt av **Kunder.** Välj kunden i kundlistan och välj sedan **Konto.** På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.** Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).

- Erbjudandeidentifieraren för objektet som ska köpas.

- Klient-ID för den indirekta återförsäljaren.

## <a name="c"></a>C\#

Så här skapar du en order för en kund till en indirekt återförsäljare:

1. Hämta en samling av indirekta återförsäljare som har en relation med den inloggade partnern.

2. Hämta en lokal variabel till objektet i samlingen som matchar det indirekta återförsäljar-ID:t. Det här steget hjälper dig att komma åt återförsäljarens [**MpnId-egenskap**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationship.mpnid) när du skapar ordern.

3. Instansiera [**ett Order-objekt**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) och ange [**egenskapen ReferenceCustomerID**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.referencecustomerid) till kundidentifieraren för att registrera kunden.

4. Skapa en lista [**med OrderLineItem-objekt**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) och tilldela listan till orderns [**LineItems-egenskap.**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.lineitems) Varje orderradsartikel innehåller inköpsinformationen för ett erbjudande. Se till att fylla i egenskapen [**PartnerIdOnRecord**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem.partneridonrecord) i varje radobjekt med MPN-ID:t för den indirekta återförsäljaren. Du måste ha minst en orderrad.

5. Hämta ett gränssnitt för att beställa åtgärder genom att anropa [**metoden IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att identifiera kunden och hämta sedan gränssnittet från [**egenskapen**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) Orders.

6. Anropa metoden [**Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) eller [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) för att skapa ordern.

### <a name="c-example"></a>\#C-exempel

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

**Exempel:** [Konsoltestapp med](console-test-app.md)**Project:** Partnercenter-SDK **Samples-klass:** PlaceOrderForCustomer.cs

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod   | URI för förfrågan                                                                            |
|----------|----------------------------------------------------------------------------------------|
| **Inlägg** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/orders HTTP/1.1 |

#### <a name="uri-parameters"></a>URI-parametrar

Använd följande sökvägsparameter för att identifiera kunden.

| Namn        | Typ   | Obligatorisk | Beskrivning                                           |
|-------------|--------|----------|-------------------------------------------------------|
| kund-ID | sträng | Ja      | En GUID-formaterad sträng som identifierar kunden. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

#### <a name="order"></a>Beställning

I den här tabellen beskrivs **orderegenskaperna** i begärandetexten.

| Namn | Typ | Obligatorisk | Beskrivning |
| ---- | ---- | -------- | ----------- |
| id | sträng | No | En orderidentifierare som anges när ordern har skapats. |
| referenceCustomerId | sträng | Ja | Kundidentifieraren. |
| billingCycle | sträng | No | Frekvensen som partnern debiteras med för den här beställningen. Standardvärdet är &quot; Varje månad och tillämpas när &quot; ordern har skapats. Värden som stöds är de medlemsnamn som finns [**i BillingCycleType**](/dotnet/api/microsoft.store.partnercenter.models.offers.billingcycletype). Obs! Den årliga faktureringsfunktionen är ännu inte allmänt tillgänglig. Stöd för årlig fakturering kommer snart. |
| lineItems | matris med objekt | Ja | En matris med [**OrderLineItem-resurser.**](#orderlineitem) |
| creationDate | sträng | No | Det datum då ordern skapades i datum/tid-format. Tillämpas när ordern har skapats. |
| Attribut | objekt | Inga | Innehåller "ObjectType": "Order". |

#### <a name="orderlineitem"></a>OrderLineItem

I den här tabellen beskrivs **egenskaperna OrderLineItem** i begärandetexten.

| Namn | Typ | Obligatorisk | Beskrivning |
| ---- | ---- | -------- | ----------- |
| lineItemNumber | int | Ja | Varje radobjekt i samlingen får ett unikt radnummer som räknas upp från 0 till count-1. |
| offerId | sträng | Ja | Erbjudandeidentifieraren. |
| subscriptionId | sträng | No | Prenumerationsidentifieraren. |
| parentSubscriptionId | sträng | No | Valfritt. ID:t för den överordnade prenumerationen i ett tilläggserbjudande. Gäller endast PATCH. |
| friendlyName | sträng | No | Valfritt. Det egna namnet för prenumerationen som definierats av partnern för att undvika tvetydighet. |
| quantity | int | Ja | Antalet licenser för en licensbaserad prenumeration. |
| partnerIdOnRecord | sträng | No | När en indirekt leverantör gör en beställning åt en indirekt återförsäljare fyller du i det här fältet med mpn-ID:t för den indirekta **återförsäljaren** (aldrig ID för den indirekta leverantören). Detta säkerställer korrekt redovisning av incitament. **Om du inte anger återförsäljarens MPN-ID misslyckas inte beställningen. Återförsäljaren registreras dock inte och därför kanske inte försäljningen ingår i incitamentberäkningarna.** |
| Attribut | objekt | Inga | Innehåller "ObjectType":"OrderLineItem". |

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

Om det lyckas innehåller svarstexten den ifyllda [orderresursen.](order-resources.md)

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder i Partnercenter.](error-codes.md)

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
