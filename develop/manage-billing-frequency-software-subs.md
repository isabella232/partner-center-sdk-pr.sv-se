---
title: Hantera faktureringsfrekvens för programvaruprenumerationer
description: Uppdatera faktureringsfrekvensen för en prenumerationsresurs som matchar kund- och prenumerations-ID:t.
ms.date: 02/23/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3cacfe94868afb0b4c1c93842b187d653dffe64f
ms.sourcegitcommit: 36e88224d0957b7ea6298789c75cdd18fc0f3685
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/07/2021
ms.locfileid: "129664942"
---
# <a name="update-billing-frequency-for-software-subscriptions"></a>Uppdatera faktureringsfrekvensen för programvaruprenumerationer

**Gäller för:** Partnercenter

Uppdatera faktureringsfrekvensen för en prenumerationsresurs [för](subscription-resources.md) programvara som matchar kunden och prenumerations-ID:t.

I instrumentpanelen i Partnercenter utförs den här åtgärden genom att först [välja en kund](get-a-customer-by-name.md). Välj sedan den prenumeration som du vill uppdatera. Klicka slutligen på Hantera schemalagda ändrade för att välja alternativ och välj sedan **Spara**.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md) Det här scenariot stöder autentisering med både fristående app- och app+användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard) Välj **CSP** på Menyn i Partnercenter följt av **Kunder.** Välj kunden i kundlistan och välj sedan **Konto.** På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.** Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).

- Ett prenumerations-ID.

## <a name="c"></a>C\#

Om du vill uppdatera en kunds programvaruprenumeration hämtar du [först](get-a-subscription-by-id.md)prenumerationen och anger sedan prenumerationens [**egenskap billingCycle.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.billingCycle) När ändringen har gjorts använder du samlingen **IAggregatePartner.Customers** och anropar **metoden ById().** Anropa sedan egenskapen [**Prenumerationer**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) följt av [**metoden ById().**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) Avsluta sedan med att anropa **metoden Patch().**

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// Subscription selectedSubscription;

this.Context.ConsoleHelper.StartProgress("Updating subscription scheduled change");
selectedSubscription.ScheduledNextTermInstructions = new ScheduledNextTermInstructions
{
    Product = new ProductTerm
    {
        ProductId = changeToProductId,
        SkuId = changeToSkuId,
        AvailabilityId = changeToAvailabilityId,
        BillingCycle = changeToBillingCycle,
        TermDuration = changeToTermDuration,
    },
    Quantity = changeToQuantity,
};

var updatedSubscription = subscriptionOperations.Patch(selectedSubscription);
```

**Exempel:** [Konsoltestapp](console-test-app.md). **Project:** PartnerSDK.FeatureSample-klass: UpdateSubscription.cs 

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod    | URI för förfrågan                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| **PATCH** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1 |

### <a name="uri-parameter"></a>URI-parameter

I den här tabellen visas frågeparametern som krävs för att pausa prenumerationen.

| Namn                    | Typ     | Obligatorisk | Beskrivning                               |
|-------------------------|----------|----------|-------------------------------------------|
| **kund-klient-id**  | **GUID** | Y        | Ett GUID som motsvarar kunden.     |
| **id-for-subscription** | **GUID** | Y        | Ett GUID som motsvarar prenumerationen. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

En fullständig prenumerationsresurs **för** den kommersiella marknadsplatsen krävs i begärandetexten. Kontrollera att egenskapen **AutoRenewEnabled** har uppdaterats.

### <a name="request-example-for-a-software-subscription"></a>Exempel på begäran för en programvaruprenumeration

```http
{ 
    "id": "d3b7c9a2-9a4b-40b2-b075-6e442909e3e7", 
    "offerId": "DG7GMGF0DVSV:000P:DG7GMGF0F3Q9", 
    "offerName": "Windows Server Remote Desktop Services CAL - 1 User CAL – 3 year", 
    "friendlyName": "Windows Server Remote Desktop Services CAL - 1 User CAL – 3 year", 
    "productType": { 
        "id": "Software", 
        "displayName": "Software" 
    }, 
    "quantity": 1, 
    "unitType": "Licenses", 
    "hasPurchasableAddons": false, 
    "creationDate": "2021-09-14T16:44:14.1210743Z", 
    "effectiveStartDate": "2021-09-14T16:44:03.4609789Z", 
    "commitmentEndDate": "2024-09-13T00:00:00Z", 
    "cancellationAllowedUntilDate": "2021-10-14T23:59:00Z", 
    "status": "active", 
    "autoRenewEnabled": true, 
    "scheduledNextTermInstructions": { 
      "product": { 
         "productId":  "DG7GMGF0DVSV", 
         "skuId":  "000P", 
         "availabilityId":  "DG7GMGF0F3Q9", 
         "billingCycle":  "Annual", 
         "termDuration":  "P3Y" 
        }, 
      "quantity":  1 
     },  // original value = null 
    "isTrial": false, 
    "billingType": "license", 
    "billingCycle": "triennial", 
    "termDuration": "P3Y", 
    "renewalTermDuration": "", 
    "isMicrosoftProduct": true, 
    "partnerId": "", 
    "attentionNeeded": false, 
    "actionTaken": false, 
    "contractType": "subscription", 
    "links": { 
        "product": { 
            "uri": "/products/DG7GMGF0DVSV?country=US", 
            "method": "GET", 
            "headers": [] 
        }, 
        "sku": { 
            "uri": "/products/DG7GMGF0DVSV/skus/000P?country=US", 
            "method": "GET", 
            "headers": [] 
        }, 
        "availability": { 
            "uri": "/products/DG7GMGF0DVSV/skus/000P/availabilities/DG7GMGF0F3Q9?country=US", 
            "method": "GET", 
            "headers": [] 
        }, 
        "self": { 
            "uri": "/customers/1f53d7b3-cd04-43a3-a09f-e52f3eb3c205/subscriptions/d3b7c9a2-9a4b-40b2-b075-6e442909e3e7", 
            "method": "GET", 
            "headers": [] 
        } 
    }, 
    "publisherName": "Microsoft", 
    "orderId": "123456789101", 
    "attributes": { 
        "objectType": "Subscription" 
    } 
} 
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden [uppdaterade prenumerationsresursegenskaper](subscription-resources.md) i svarstexten.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder.](error-codes.md)

### <a name="response-example"></a>Exempel på svar

```http
{ 
    "id": "d3b7c9a2-9a4b-40b2-b075-6e442909e3e7", 
    "offerId": "DG7GMGF0DVSV:000P:DG7GMGF0F3Q9", 
    "offerName": "Windows Server Remote Desktop Services CAL - 1 User CAL – 3 year", 
    "friendlyName": "Windows Server Remote Desktop Services CAL - 1 User CAL – 3 year", 
    "productType": { 
        "id": "Software", 
        "displayName": "Software" 
    }, 
    "quantity": 1, 
    "unitType": "Licenses", 
    "hasPurchasableAddons": false, 
    "creationDate": "2021-09-14T16:44:14.1210743Z", 
    "effectiveStartDate": "2021-09-14T16:44:03.4609789Z", 
    "commitmentEndDate": "2024-09-13T00:00:00Z", 
    "cancellationAllowedUntilDate": "2021-10-14T23:59:00Z", 
    "status": "active", 
    "autoRenewEnabled": true, 
    "scheduledNextTermInstructions": { 
      "product": { 
         "productId":  "DG7GMGF0DVSV", 
         "skuId":  "000P", 
         "availabilityId":  "DG7GMGF0F3Q9", 
         "billingCycle":  "Annual", 
         "termDuration":  "P3Y" 
        }, 
      "quantity":  1 
     },  // original value = null 

    "isTrial": false, 
    "billingType": "license", 
    "billingCycle": "triennial", 
    "termDuration": "P3Y", 
    "renewalTermDuration": "", 
    "isMicrosoftProduct": true, 
    "partnerId": "", 
    "attentionNeeded": false, 
    "actionTaken": false, 
    "contractType": "subscription", 
    "links": { 
        "product": { 
            "uri": "/products/DG7GMGF0DVSV?country=US", 
            "method": "GET", 
            "headers": [] 
        }, 
        "sku": { 
            "uri": "/products/DG7GMGF0DVSV/skus/000P?country=US", 
            "method": "GET", 
            "headers": [] 
        }, 
        "availability": { 
            "uri": "/products/DG7GMGF0DVSV/skus/000P/availabilities/DG7GMGF0F3Q9?country=US", 
            "method": "GET", 
            "headers": [] 
        }, 
        "self": { 
            "uri": "/customers/1f53d7b3-cd04-43a3-a09f-e52f3eb3c205/subscriptions/d3b7c9a2-9a4b-40b2-b075-6e442909e3e7", 
            "method": "GET", 
            "headers": [] 
        } 
    }, 
    "publisherName": "Microsoft", 
    "orderId": "123456789101", 
    "attributes": { 
        "objectType": "Subscription" 
    } 
} 
```
