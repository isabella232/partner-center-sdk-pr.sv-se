---
title: Skapa en kundorder
description: Lär dig hur du använder Partner Center-API:er för att skapa en order för en kund. Artikeln innehåller krav, steg och exempel.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f8a18ef4a6fbdfcd659e6ec1c11bc6bd61c80472
ms.sourcegitcommit: e1db965e8c7b4fe3aaa0ecd6cefea61973ca2232
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/03/2021
ms.locfileid: "123456043"
---
# <a name="create-an-order-for-a-customer-using-partner-center-apis"></a>Skapa en order för en kund med partnercenter-API:er

**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud for US Government

Att skapa en **beställning för azure-produkter för reserverade VM-instanser** *gäller endast* för:

- Partnercenter

Information om vad som för närvarande är tillgängligt för försäljning finns [i Partnererbjudanden i Molnlösningsleverantör program](/partner-center/csp-offers).

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md) Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard) Välj **CSP** på Menyn i Partnercenter följt av **Kunder.** Välj kunden i kundlistan och välj sedan **Konto.** På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.** Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).

- Ett erbjudande-ID.

## <a name="c"></a>C\#

Så här skapar du en order för en kund:

1. Instansiera [**ett Order-objekt**](order-resources.md) och ange **egenskapen ReferenceCustomerID** till kund-ID:t för att registrera kunden.

2. Skapa en lista [**med OrderLineItem-objekt**](order-resources.md#orderlineitem) och tilldela listan till orderns **LineItems-egenskap.** Varje orderradsartikel innehåller inköpsinformationen för ett erbjudande. Du måste ha minst en orderrad.

3. Hämta ett gränssnitt för att ordna åtgärder. Anropa först metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att identifiera kunden. Hämta sedan gränssnittet från [**egenskapen**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) Beställningar.

4. Anropa metoden [**Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) eller [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) och skicka objektet [**Order.**](order-resources.md)

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

**Exempel:** [Konsoltestapp](console-test-app.md). **Project:** Partnercenter-SDK **Exempelklass:** CreateOrder.cs

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod   | URI för förfrågan                                                                            |
|----------|----------------------------------------------------------------------------------------|
| **INLÄGG** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/orders HTTP/1.1 |

#### <a name="uri-parameters"></a>URI-parametrar

Använd följande sökvägsparameter för att identifiera kunden.

| Namn        | Typ   | Obligatorisk | Beskrivning                                                |
|-------------|--------|----------|------------------------------------------------------------|
| kund-ID | sträng | Yes      | Ett GUID-formaterat kund-ID som identifierar kunden. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

#### <a name="order"></a>Beställning

I den här tabellen beskrivs [orderegenskaperna](order-resources.md) i begärandetexten.

| Egenskap             | Typ                        | Obligatorisk                        | Beskrivning                                                                   |
|----------------------|-----------------------------|---------------------------------|-------------------------------------------------------------------------------|
| id                   | sträng                      | No                              | En orderidentifierare som anges när ordern har skapats.   |
| referenceCustomerId  | sträng                      | No                              | Kundidentifieraren. |
| billingCycle         | sträng                      | No                              | Anger med vilken frekvens partnern faktureras för den här beställningen. Värden som stöds är de medlemsnamn som finns [i BillingCycleType](product-resources.md#billingcycletype). Standardvärdet är "Varje månad" eller "OneTime" när ordern skapas. Det här fältet tillämpas när ordern har skapats. |
| lineItems            | matris med [OrderLineItem-resurser](order-resources.md#orderlineitem) | Yes      | En specificerad lista över de erbjudanden som kunden köper, inklusive kvantitet.        |
| currencyCode         | sträng                      | No                              | Skrivskyddade. Den valuta som används när du gör beställningen. Tillämpas när ordern har skapats.           |
| creationDate         | datetime                    | No                              | Skrivskyddade. Det datum då ordern skapades i datum/tid-format. Tillämpas när ordern har skapats.                                   |
| status               | sträng                      | No                              | Skrivskyddade. Status för ordern.  Värden som stöds är de medlemsnamn som finns i [OrderStatus](order-resources.md#orderstatus).        |
| Länkar                | [OrderLinks](utility-resources.md#resourcelinks)              | No                              | Resursen länkar som motsvarar ordern. |
| Attribut           | [ResourceAttributes](utility-resources.md#resourceattributes) | No                              | Metadataattributen som motsvarar ordern. |

#### <a name="orderlineitem"></a>OrderLineItem

I den här tabellen beskrivs [egenskaperna OrderLineItem](order-resources.md#orderlineitem) i begärandetexten.

>[!NOTE]
>PartnerIdOnRecord ska endast anges när en indirekt leverantör gör en beställning åt en indirekt återförsäljare. Det används för att lagra den indirekta återförsäljarens Microsoft Partner Network id (aldrig ID för den indirekta leverantören).

| Namn                 | Typ   | Obligatorisk | Beskrivning                                                                                                                                                                                                                                |
|----------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| lineItemNumber       | int    | Yes      | Varje radobjekt i samlingen får ett unikt radnummer som räknas upp från 0 till count-1.                                                                                                                                                 |
| offerId              | sträng | Yes      | Erbjudandeidentifieraren.                                                                                                                                                                                                                      |
| subscriptionId       | sträng | No       | Prenumerationsidentifieraren.                                                                                                                                                                                                               |
| parentSubscriptionId | sträng | No       | Valfritt. ID:t för den överordnade prenumerationen i ett tilläggserbjudande. Gäller endast PATCH.                                                                                                                                                     |
| friendlyName         | sträng | No       | Valfritt. Det egna namnet för prenumerationen som definierats av partnern för att undvika tvetydighet.                                                                                                                                              |
| quantity             | int    | Yes      | Antalet licenser för en licensbaserad prenumeration.                                                                                                                                                                                   |
| partnerIdOnRecord    | sträng | No       | När en indirekt leverantör gör en beställning åt en indirekt återförsäljare fyller du i det här fältet med endast den indirekta återförsäljarens MPN-ID **(aldrig** DEN indirekta leverantörens ID). Detta säkerställer korrekt redovisning av incitament. |
| provisioningContext  | Ordlista<sträng, sträng>                | No       |  Information som krävs för etablering för vissa objekt i katalogen. Egenskapen provisioningVariables i en SKU anger vilka egenskaper som krävs för specifika objekt i katalogen.                  |
| Länkar                | [OrderLineItemLinks](order-resources.md#orderlineitemlinks) | No       |  Skrivskyddade. Resursen länkar som motsvarar orderradsobjektet.  |
| Attribut           | [ResourceAttributes](utility-resources.md#resourceattributes) | No       | Metadataattributen som motsvarar OrderLineItem. |
| renewsTo             | Matris med objekt                          | No    |En matris med [RenewsTo-resurser.](order-resources.md#renewsto)                                                                            |
| AttestationAccepted             | boolesk                 | No   |  Anger avtal om att erbjuda eller SKU-villkor. Krävs endast för erbjudanden eller SKU:er där SkuAttestationProperties eller OfferAttestationProperties enforceAttestation är True.          |

##### <a name="renewsto"></a>RenewsTo

I den här tabellen beskrivs [egenskaperna RenewsTo](order-resources.md#renewsto) i begärandetexten.

| Egenskap              | Typ             | Obligatorisk        | Beskrivning |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | sträng           | No              | En ISO 8601-representation av förnyelseperiodens varaktighet. De aktuella värdena som stöds **är P1M** (1 månad) och **P1Y** (1 år). |

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

Om det lyckas returnerar metoden en [Order-resurs](order-resources.md) i svarstexten.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder i Partnercenter.](error-codes.md)

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
