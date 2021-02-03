---
title: Annullera en order från sandbox-integration
description: 'Lär dig hur du använder API: er för partner Center för att avbryta olika typer av prenumerations order från högintegrations konton i sandbox.'
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 363bf209e27d5223259c8c533710a3b35bbef1e6
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/04/2020
ms.locfileid: "97770083"
---
# <a name="cancel-an-order-from-the-integration-sandbox-using-partner-center-apis"></a>Avbryta en order från integration sandbox med API: er för partner Center

**Gäller för:**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

I den här artikeln beskrivs hur du använder API: er för partner Center för att avbryta olika typer av prenumerations order från högintegrations konton. Sådana beställningar kan omfatta reserverade instanser, program vara och kommersiella Marketplace-program som en tjänst (SaaS) prenumerations order.

>[!NOTE]
>Tänk på att annulleringen av reserverad instans eller prenumerations order för SaaS på kommersiella marknads platser endast är möjlig från integrations sand Box konton.  

Om du vill avbryta produktions order för program vara via API använder du [Cancel-Software-inköp](cancel-software-purchases.md).
Du kan också avbryta produktions order av program vara via instrument panelen genom att [avbryta ett köp](/partner-center/csp-software-subscriptions).

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.

- Ett partner konto för integration i begränsat läge med en kund som har aktiva prenumerations beställningar för reserverad instans/program vara/tredje part.

## <a name="c"></a>C\#

Om du vill avbryta en beställning från sandbox-integration måste du skicka autentiseringsuppgifterna för ditt konto till- [**`CreatePartnerOperations`**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) metoden för att få ett [**`IPartner`**](/dotnet/api/microsoft.store.partnercenter.ipartner) gränssnitt för att få partner åtgärder.

Om du vill välja en viss [ordning](order-resources.md#order)använder du partner åtgärderna och anrops [**`Customers.ById()`**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metoden med kund-ID: n för att ange kunden, följt av **`Orders.ById()`** med order-ID för att ange ordningen och slutligen **`Get`** eller **`GetAsync`** metoden för att hämta den.

Ange [**`Order.Status`**](order-resources.md#order) egenskapen till `cancelled` och Använd **`Patch()`** metoden för att uppdatera ordningen.

``` csharp
// IPartnerCredentials tipAccountCredentials;
// Customer tenant Id to be deleted.
// string customerTenantId;

IPartner tipAccountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(tipAccountCredentials);

// Cancel order
var order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Get();
order.Status = "cancelled";
order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Patch(order);

```

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod     | URI för förfrågan                                                                            |
|------------|----------------------------------------------------------------------------------------|
| **9.0a** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Orders/{order-ID} http/1.1 |

### <a name="uri-parameter"></a>URI-parameter

Använd följande frågeparameter för att ta bort en kund.

| Namn                   | Typ     | Obligatorisk | Beskrivning                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **kund-ID för klient organisation** | **guid** | Y        | Värdet är ett GUID-formaterat **kund-Tenant-ID** som gör det möjligt för åter försäljaren att filtrera resultaten för en specifik kund som tillhör åter försäljaren. |
| **order-ID** | **nollängd** | Y        | Värdet är en sträng som anger de order-ID: n som behöver avbrytas. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

```http
{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "status": "cancelled",
}
```

### <a name="request-example"></a>Exempel på begäran

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/orders/<order-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd

{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "status": "cancelled",
}
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden den avbrutna ordningen.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Length: 866
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "alternateId": "11fc4bdfd47a",
    "referenceCustomerId": "bd59b416-37f9-4d8f-8df3-5750111fc615",
    "billingCycle": "one_time",
    "currencyCode": "USD",
    "currencySymbol": "$",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0DWT0:0001:DG7GMGF0DSQR",
            "termDuration": "",
            "transactionType": "New",
            "friendlyName": "Microsoft Identity Manager 2016 - 1 User CAL",
            "quantity": 1,
            "links": {
                "product": {
                    "uri": "/products/DG7GMGF0DWT0?country=US",
                    "method": "GET",
                    "headers": []
                },
                "sku": {
                    "uri": "/products/DG7GMGF0DWT0/skus/0001?country=US",
                    "method": "GET",
                    "headers": []
                },
                "availability": {
                    "uri": "/products/DG7GMGF0DWT0/skus/0001/availabilities/DG7GMGF0DSQR?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2019-02-21T17:56:21.1335741Z",
    "status": "cancelled",
    "transactionType": "UserPurchase",
    "attributes": {
        "objectType": "Order"
    }
}
```
