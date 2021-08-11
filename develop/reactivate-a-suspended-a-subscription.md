---
title: Återaktivera en inaktiverad prenumeration
description: Återaktiverar en prenumeration som tidigare har inaktiverats för utebliven betalning. På instrumentpanelen i Partnercenter kan du utföra den här åtgärden genom att först välja en kund.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8ef79c28e4b6d0d3517b342ac92163865ed8e8edb21cc0b384fef52e93bc93ac
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997251"
---
# <a name="reactivate-a-suspended-subscription"></a>Återaktivera en inaktiverad prenumeration

**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Återaktiverar en [prenumeration som](subscription-resources.md) tidigare har inaktiverats för utebliven betalning.

På instrumentpanelen i Partnercenter kan du utföra den här åtgärden genom att först [välja en kund.](get-a-customer-by-name.md) Välj sedan den prenumeration som du vill byta namn på. Slutför genom att välja **knappen** Aktiv och sedan **skicka.**

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard) Välj **CSP** på Menyn i Partnercenter följt av **Kunder**. Välj kunden i kundlistan och välj sedan **Konto.** På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.** Microsoft-ID:t är samma som kund-ID :t ( `customer-tenant-id` ).

- Ett prenumerations-ID.

## <a name="c"></a>C\#

Om du vill återaktivera en kunds prenumeration hämtar du [först prenumerationen](get-a-subscription-by-id.md)och ändrar sedan prenumerationens [**statusegenskap.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) Information om **statuskoder** finns i [SubscriptionStatus-uppräkning/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus). När ändringen har gjorts använder du samlingen [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) och anropar [**metoden ById().**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) Anropa sedan egenskapen [**Prenumerationer**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) följt av [**metoden ById().**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) Avsluta sedan med att anropa [**metoden Patch().**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch)

``` csharp
// IPartner partnerOperations;
// var selectedCustomer as Customer;
// var selectedSubscription as Subscription;

updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(
   new Subscription()
   {
      Status = SubscriptionStatus.Active
   });

```

**Exempel:** [Konsoltestapp](console-test-app.md). **Project:** FunktionerExempelApplication. **Klass:** UpdateSubscription

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod    | URI för förfrågan                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| **Patch** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1 |

### <a name="uri-parameter"></a>URI-parameter

I den här tabellen visas den frågeparameter som krävs för att återaktivera prenumerationen.

| Namn                    | Typ     | Obligatorisk | Beskrivning                               |
|-------------------------|----------|----------|-------------------------------------------|
| **kund-klient-id**  | **guid** | Y        | Ett GUID som motsvarar kunden.     |
| **id-for-subscription** | **guid** | Y        | Ett GUID som motsvarar prenumerationen. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

En fullständig **prenumerationsresurs** krävs i begärandetexten. Kontrollera att **egenskapen Status** har uppdaterats.

### <a name="request-example"></a>Exempel på begäran

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive

{
    "Id": "83ef9d05-4169-4ef9-9657-0e86b1eab1de",
    "FriendlyName": "nickname",
    "Quantity": 2,
    "UnitType": "none",
    "ParentSubscriptionId": null,
    "CreationDate": "2015-11-25T06:41:12Z",
    "EffectiveStartDate": "2015-11-24T08:00:00Z",
    "CommitmentEndDate": "2016-12-12T08:00:00Z",
    "Status": "active",
    "AutoRenewEnabled": false,
    "BillingType": "none",
    "PartnerId": null,
    "ContractType": "subscription",
    "OrderId": "6183db3d-6318-4e52-877e-25806e4971be",
    "Attributes": {
        "Etag": "<etag>",
        "ObjectType": "Subscription"
    }
}
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden uppdaterade [prenumerationsresursegenskaper](subscription-resources.md) i svarstexten.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder.](error-codes.md)

### <a name="response-example"></a>Exempel på svar

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<subscriptionID> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-Contract-Version: v1
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive

{
    "Id": "83ef9d05-4169-4ef9-9657-0e86b1eab1de",
    "FriendlyName": "nickname",
    "Quantity": 2,
    "UnitType": "none",
    "ParentSubscriptionId": null,
    "CreationDate": "2015-11-25T06:41:12Z",
    "EffectiveStartDate": "2015-11-24T08:00:00Z",
    "CommitmentEndDate": "2016-12-12T08:00:00Z",
    "Status": "active",
    "AutoRenewEnabled": false,
    "BillingType": "none",
    "PartnerId": null,
    "ContractType": "subscription",
    "Links": {
        "Offer": {
            "Uri": "/v1/offers/0CCA44D6-68E9-4762-94EE-31ECE98783B9",
            "Method": "GET",
            "Headers": []
        },
        "Entitlement": {
            "Uri": "/entitlements?key=<key>",
            "Method": "GET",
            "Headers": []
        },
        "Self": {
            "Uri": "/subscriptions?key=<key>",
            "Method": "GET",
            "Headers": []
        }
    },
    "OrderId": "6183db3d-6318-4e52-877e-25806e4971be",
    "Attributes": {
        "Etag": "<etag>",
        "ObjectType": "Subscription"
    }
}
```
