---
title: Ändra kvantiteten för en prenumeration
description: 'Lär dig hur du använder API: er för partner Center för att ändra antalet licenser för en kund prenumeration. Du kan också göra detta på instrument panelen för partner Center.'
ms.date: 06/05/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b9b781c50895aa3a14819bec43fcca1e931e3b30
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/04/2020
ms.locfileid: "97770071"
---
# <a name="change-the-quantity-of-licenses-in-a-customer-subscription"></a>Ändra antalet licenser i en kund prenumeration

**Gäller för:**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Uppdaterar en [prenumeration](subscription-resources.md) för att öka eller minska antalet licenser.

På instrument panelen för partner Center kan du utföra den här åtgärden genom [att först välja en kund](get-a-customer-by-name.md). Välj sedan den prenumeration i fråga som du vill byta namn på. Slutför genom att ändra värdet i fältet **kvantitet** och sedan **Skicka.**

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).

- Ett prenumerations-ID.

## <a name="c"></a>C\#

Om du vill ändra antalet för en kund prenumeration ska du först [Hämta prenumerationen](get-a-subscription-by-id.md)och sedan ändra prenumerationens egenskap för [**kvantitet**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.quantity) . När ändringen har gjorts använder du din **IAggregatePartner. Customers** -samling och anropar metoden **ById ()** . Anropa sedan egenskapen [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) följt av metoden [**ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) . Sedan avslutar du genom att anropa **patch-metoden ()** .

``` csharp
// IAggregatePartner partnerOperations;
// var customerId;
// var subscriptionId;

//retrieving the subscription, for the purpose of the sample
ResourceCollection<Subscription> customerSubscriptions = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.Get();
Subscription selectedSubscription = customerSubscriptions.Items.FirstOrDefault(sub => sub.Status == SubscriptionStatus.Active);

//update selected subscription,
selectedSubscription.Quantity++;

var updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(selectedSubscription);
```

**Exempel**: [konsol test app](console-test-app.md). **Projekt**: PartnerSDK. FeatureSample- **klass**: UpdateSubscription.CS

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod    | URI för förfrågan                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| **9.0a** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{ID-for-Subscription} http/1.1 |

### <a name="uri-parameter"></a>URI-parameter

Den här tabellen visar den obligatoriska Frågeparametern för att ändra antalet för prenumerationen.

| Namn                    | Typ     | Obligatorisk | Beskrivning                               |
|-------------------------|----------|----------|-------------------------------------------|
| **kund-ID för klient organisation**  | **guid** | Y        | Ett GUID som motsvarar kunden.     |
| **ID för-prenumeration** | **guid** | Y        | Ett GUID som motsvarar prenumerationen. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

En fullständig **prenumerations** resurs krävs i begär ande texten. Se till att egenskapen **kvantitet** har uppdaterats.

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

Om det lyckas returnerar den här metoden en status kod för **http-status 200** och uppdaterade [prenumerations resurs](subscription-resources.md)  egenskaper i svars texten.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar returnerar en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa status koden, fel typen och ytterligare parametrar. En fullständig lista finns i [felkoder](error-codes.md).

När korrigerings åtgärden tar längre tid än den förväntade tiden skickar Partner Center en **http-status 202-** status kod och ett plats huvud som pekar på varifrån prenumerationen ska hämtas. Du kan fråga prenumerationen med jämna mellanrum för att övervaka ändringar av status och antal.

### <a name="response-examples"></a>Svars exempel

#### <a name="response-example-1"></a>Svars exempel 1

Lyckad begäran med **http-status 200** status kod:

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

#### <a name="response-example-2"></a>Svars exempel 2

Lyckad begäran med **http-status 202** status kod:

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<subscriptionID> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 01880c1b-1966-40f0-d470-501a66d9948b
MS-CorrelationId: 2c5827c1-d5f9-4835-cc6d-f1918b782c79
Content-Type: application/json
Content-Length: 1432
Connection: Keep-Alive
Location: /customers/<customer-tenant-id>/subscriptions/<subscriptionID>
```
