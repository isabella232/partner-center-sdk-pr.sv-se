---
title: Uppdatera en kundvagn
description: Så här uppdaterar du en order för en kund i en varukorg.
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7c0806ccc87281b9b34005f22cd8d6ad57fb5de5
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768940"
---
# <a name="update-a-cart"></a>Uppdatera en kundvagn

**Gäller för**

- Partnercenter

Så här uppdaterar du en order för en kund i en varukorg.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).

- Ett kundvagn-ID för en befintlig varukorg.

## <a name="c"></a>C\#

Om du vill uppdatera en order för en kund hämtar du vagnen med hjälp av metoden **Get ()** genom att skicka kund-och kundvagn-ID: t med funktionen **ById ()** . Gör nödvändiga ändringar i vagnen. Anropa nu metoden för att **Skicka** med hjälp av kund-och shopping-ID: t med hjälp av metoden **ById ()** .

Anropa slutligen metoden PutAsync ( **)** eller metoden **()** för att skapa ordern.

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string cartId;

var cart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Get();

cart.LineItems.ToArray()[0].Quantity++;

var updatedCart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Put(cart);
```

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod  | URI för förfrågan                                                                                                 |
|---------|-------------------------------------------------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/carts/{Cart-ID} http/1.1              |

### <a name="uri-parameters"></a>URI-parametrar

Använd följande Sök vägs parametrar för att identifiera kunden och ange den varukorg som ska uppdateras.

| Namn            | Typ     | Obligatorisk | Beskrivning                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **kund-ID** | sträng   | Yes      | Ett GUID-formaterat kund-ID som identifierar kunden.             |
| **kundvagn-ID**     | sträng   | Yes      | Ett GUID-formaterat vagn-ID som identifierar vagnen.                     |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

I den här tabellen beskrivs egenskaperna för [kundvagn](cart-resources.md) i begär ande texten.

| Egenskap              | Typ             | Obligatorisk        | Beskrivning                                                                                               |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| id                    | sträng           | No              | Ett kundvagn-ID som anges när vagnen skapas.                                  |
| creationTimeStamp     | DateTime         | No              | Datumet då vagnen skapades i datum-/tids format. Används när vagnen har skapats.        |
| lastModifiedTimeStamp | DateTime         | No              | Datumet då vagnen senast uppdaterades i datum-/tids format. Används när vagnen har skapats.    |
| expirationTimeStamp   | DateTime         | No              | Datumet då vagnen upphör att gälla, i datum-/tids format.  Används när vagnen har skapats.            |
| lastModifiedUser      | sträng           | No              | Den användare som senast uppdaterade vagnen. Används när vagnen har skapats.                             |
| Rad objekt             | Objekt mat ris | Yes             | En matris med [CartLineItem](cart-resources.md#cartlineitem) -resurser.                                               |

I den här tabellen beskrivs egenskaperna för [CartLineItem](cart-resources.md#cartlineitem) i begär ande texten.

| Egenskap             | Typ                        | Obligatorisk     | Beskrivning                                                                                        |
|----------------------|-----------------------------|--------------|----------------------------------------------------------------------------------------------------|
| id                   | sträng                      | No           | En unik identifierare för ett vagn rads objekt. Används när vagnen har skapats.                |
| catalogId            | sträng                      | Yes          | Katalog objekt identifierare.                                                                       |
| friendlyName         | sträng                      | No           | Valfritt. Det egna namnet på det objekt som definieras av partnern för att hjälpa disambiguate.              |
| quantity             | int                         | Yes          | Antalet licenser eller instanser.     |
| currencyCode         | sträng                      | No           | Valuta koden.                                                                                 |
| billingCycle         | Objekt                      | Yes          | Typ av fakturerings cykel som angetts för den aktuella perioden.                                              |
| deltagare         | Lista med objekt sträng par | No           | En samling deltagare på köpet.                                                      |
| provisioningContext  | Ord listans<sträng, sträng>  | No           | En kontext som används för etablering av erbjudande.                                                          |
| orderGroup           | sträng                      | No           | En grupp som visar vilka objekt som kan placeras tillsammans.                                            |
| fel                | Objekt                      | No           | Tillämpas efter att kundvagn har skapats i händelse av ett fel.                                                 |

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
