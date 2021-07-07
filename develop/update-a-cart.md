---
title: Uppdatera en kundvagn
description: Så här uppdaterar du en order för en kund i en kundvagn.
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8954d4dad39f9b1a1b9a2f213e0231f01856fcd2
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446691"
---
# <a name="update-a-cart"></a>Uppdatera en kundvagn

Så här uppdaterar du en order för en kund i en kundvagn.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard) Välj **CSP** på Menyn i Partnercenter följt av **Kunder**. Välj kunden i kundlistan och välj sedan **Konto.** På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.** Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).

- Ett kundvagns-ID för en befintlig kundvagn.

## <a name="c"></a>C\#

Om du vill uppdatera en order för en kund hämtar du kundvagnen med hjälp av metoden **Get()** genom att skicka kund- och kundvagns-ID:n med hjälp av **funktionen ById().** Gör nödvändiga ändringar i kundvagnen. Anropa nu metoden **Put** med hjälp av kund- och kundvagns-ID:n med hjälp av **metoden ById().**

Anropa slutligen metoden **Put()** eller **PutAsync()** för att skapa ordern.

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string cartId;

var cart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Get();

cart.LineItems.ToArray()[0].Quantity++;

var updatedCart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Put(cart);
```

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod  | URI för förfrågan                                                                                                 |
|---------|-------------------------------------------------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts/{cart-id} HTTP/1.1              |

### <a name="uri-parameters"></a>URI-parametrar

Använd följande sökvägsparametrar för att identifiera kunden och ange vilken kundvagn som ska uppdateras.

| Namn            | Typ     | Obligatorisk | Beskrivning                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **kund-id** | sträng   | Ja      | Ett GUID-formaterat kund-ID som identifierar kunden.             |
| **cart-id**     | sträng   | Ja      | Ett GUID-formaterat kundvagns-ID som identifierar kundvagnen.                     |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

I den här tabellen beskrivs [egenskaperna för](cart-resources.md) Kundvagn i begärandetexten.

| Egenskap              | Typ             | Obligatorisk        | Beskrivning                                                                                               |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| id                    | sträng           | No              | En kundvagnsidentifierare som anges när kundvagnen har skapats.                                  |
| creationTimeStamp     | DateTime         | Inga              | Datumet då kundvagnen skapades i datum/tid-format. Tillämpas när kundvagnen har skapats.        |
| lastModifiedTimeStamp | DateTime         | Inga              | Datum då kundvagnen senast uppdaterades i datum/tid-format. Tillämpas när kundvagnen har skapats.    |
| expirationTimeStamp   | DateTime         | Inga              | Datumet då kundvagnen upphör att gälla i datum/tid-format.  Tillämpas när kundvagnen har skapats.            |
| lastModifiedUser      | sträng           | No              | Den användare som senast uppdaterade kundvagnen. Tillämpas när kundvagnen har skapats.                             |
| lineItems             | Matris med objekt | Ja             | En matris med [CartLineItem-resurser.](cart-resources.md#cartlineitem)                                               |

I den här tabellen beskrivs [egenskaperna för CartLineItem](cart-resources.md#cartlineitem) i begärandetexten.

| Egenskap             | Typ                        | Obligatorisk     | Beskrivning                                                                                        |
|----------------------|-----------------------------|--------------|----------------------------------------------------------------------------------------------------|
| id                   | sträng                      | No           | En unik identifierare för ett kundvagnsradsobjekt. Tillämpas när kundvagnen har skapats.                |
| catalogId            | sträng                      | Ja          | Katalogobjektets identifierare.                                                                       |
| friendlyName         | sträng                      | No           | Valfritt. Det egna namnet för det objekt som definierats av partnern för att undvika tvetydighet.              |
| quantity             | int                         | Ja          | Antalet licenser eller instanser.     |
| currencyCode         | sträng                      | No           | Valutakoden.                                                                                 |
| billingCycle         | Objekt                      | Ja          | Den typ av faktureringsperiod som angetts för den aktuella perioden.                                              |
| deltagare         | Lista över objektsträngpar | Inga           | En samling deltagare i köpet.                                                      |
| provisioningContext  | Ordlista<sträng, sträng>  | Inga           | En kontext som används för etablering av erbjudande.                                                          |
| orderGroup           | sträng                      | No           | En grupp som anger vilka objekt som kan placeras tillsammans.                                            |
| fel                | Objekt                      | Inga           | Tillämpas när kundvagnen har skapats i händelse av ett fel.                                                 |

### <a name="request-example"></a>Exempel på begäran

```http
PUT /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts/65faf57b-0205-47ee-92b3-08dcf233ea73/ HTTP/1.1
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
    {
        "Id":"b4c8fdea-cbe4-4d17-9576-13fcacbf9605",
        "CreationTimestamp":"2018-03-15T17:15:02.3840528Z",
        "LastModifiedTimestamp":"2018-03-15T17:15:02.3840528Z",
        "ExpirationTimestamp":"0001-01-01T00:00:00",
        "LastModifiedUser":"2713ccd7-ea3b-470a-9cfb-451d5d0482cc",
        "LineItems":[
            {
                "Id":0,
                "CatalogItemId":"DG7GMGF0DWTL:0001:DG7GMGF0DSJB",
                "FriendlyName":"A_sample_Azure_RI",
                "Quantity":2,
                "BillingCycle":"one_time",
                "ProvisioningContext": {
                    "SubscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
                    "Scope": "shared",
                    "Duration": "1Year"
                }
            }
        ],
    }
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
    "id": "b4c8fdea-cbe4-4d17-9576-13fcacbf9605",
    "creationTimestamp": "2018-03-15T17:15:02.3840528Z",
    "lastModifiedTimestamp": "2018-03-15T17:15:02.3840528Z",
    "lastModifiedUser": "2713ccd7-ea3b-470a-9cfb-451d5d0482cc",
    "lineItems": [
        {
            "id": 0,
            "catalogItemId": "DG7GMGF0DWTL:0001:DG7GMGF0DSJB",
            "friendlyName": "A_sample_Azure_RI",
            "quantity": 2,
            "currencyCode": "USD",
            "billingCycle": "one_time",
            "ProvisioningContext": {
                "subscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
                "scope": "shared",
                "duration": "1Year"
            }
            "orderGroup": "0"
        }
    ],
    "links": {
        "self": {
            "uri": "/v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts/b4c8fdea-cbe4-4d17-9576-13fcacbf9605/",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Cart"
    }
}
```
