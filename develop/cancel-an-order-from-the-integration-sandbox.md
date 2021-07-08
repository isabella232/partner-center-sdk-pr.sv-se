---
title: Avbryta en beställning från sandbox-miljön för integrering
description: Lär dig hur du använder Partner Center-API:er för att avbryta olika typer av prenumerationsbeställningar från integrations-sandbox-konton.
ms.date: 04/28/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4c4b658f406e420d8d3cd425688364fe3d440d3d
ms.sourcegitcommit: a3a78ec0f5078645b5a4f3b534165eef30f2c822
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/30/2021
ms.locfileid: "113104979"
---
# <a name="cancel-an-order-from-the-integration-sandbox-using-partner-center-apis"></a>Avbryta en beställning från sandbox-miljön för integrering med partnercenter-API:er

**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

I den här artikeln beskrivs hur du använder Partner Center-API:er för att avbryta olika typer av prenumerationsbeställningar från integrations-sandbox-konton. Sådana beställningar kan omfatta reserverade instanser, programvara och saaS-prenumerationsbeställningar (Software as a Service) på den kommersiella marknadsplatsen.

> [!NOTE] 
> Observera att annulleringar av reserverade instanser eller SaaS-prenumerationsbeställningar på den kommersiella marknadsplatsen endast är möjliga från integrations-sandbox-konton. Sandbox-beställningar som är äldre än 60 dagar kan inte annulleras från Partnercenter.

Om du vill avbryta produktionsorder för programvara via API använder [du cancel-software-purchases](cancel-software-purchases.md).
Du kan också avbryta produktionsorder för programvara via instrumentpanelen med [hjälp av avbryta ett köp.](/partner-center/csp-software-subscriptions)

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md) Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.

- Ett partnerkonto för sandbox-integrering med en kund som har aktiv reserverad instans/programvara/SaaS-prenumerationsbeställningar från tredje part.

## <a name="c"></a>C\#

Om du vill avbryta en beställning från sandbox-miljön för integrering skickar du autentiseringsuppgifterna för ditt konto till metoden [**`CreatePartnerOperations`**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) för att hämta ett gränssnitt för att hämta [**`IPartner`**](/dotnet/api/microsoft.store.partnercenter.ipartner) partneråtgärder.

Om du vill välja en viss [order](order-resources.md#order)använder du partneråtgärderna och anropar -metoden med kund-ID:t för att ange kunden, följt av med orderidentifierare för att ange ordern och slutligen metoden eller metoden för [**`Customers.ById()`**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) att hämta **`Orders.ById()`** **`Get`** **`GetAsync`** den.

Ange egenskapen [**`Order.Status`**](order-resources.md#order) till och använd metoden för att uppdatera `cancelled` **`Patch()`** ordern.

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

### <a name="request-syntax"></a>Begärandesyntax

| Metod     | URI för förfrågan                                                                            |
|------------|----------------------------------------------------------------------------------------|
| **Patch** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1 |

### <a name="uri-parameter"></a>URI-parameter

Använd följande frågeparameter för att ta bort en kund.

| Namn                   | Typ     | Obligatorisk | Beskrivning                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **kund-klient-id** | **guid** | Y        | Värdet är ett GUID-formaterat **kundklient-ID** som gör att återförsäljaren kan filtrera resultaten för en viss kund som tillhör återförsäljaren. |
| **order-id** | **sträng** | Y        | Värdet är en sträng som anger de order-ID:er som måste avbrytas. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

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

Om det lyckas returnerar den här metoden den annullerade ordern.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)

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
