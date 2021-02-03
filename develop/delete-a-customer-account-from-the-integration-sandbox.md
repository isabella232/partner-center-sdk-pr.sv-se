---
title: Ta bort ett kundkonto från sandbox-miljön för integrering
description: Så här tar du bort ett kund konto från Testing in Production (Tip) integration sandbox.
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e3a1642c0202c174ddd4f65a6aeda2752def9176
ms.sourcegitcommit: b1ff781b67b1d322820bbcac2c583229201a8c07
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/29/2020
ms.locfileid: "97769423"
---
# <a name="delete-a-customer-account-from-the-integration-sandbox"></a>Ta bort ett kundkonto från sandbox-miljön för integrering

**Gäller för:**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

I den här artikeln beskrivs hur du delar upp relationen mellan partnern och kund kontot och återfår kvoten för Testing in Production (Tip)-integration sandbox.

> [!IMPORTANT]
> När du tar bort ett kund konto rensas alla resurser som är kopplade till kund klienten.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).

- Alla Azure Reserved Virtual Machine Instances-och program inköps order måste avbrytas innan du tar bort en kund från det begränsade tipset för tips integrering.

## <a name="c"></a>C\#

Så här tar du bort en kund från sandbox-tipset för integrering:

1. Skicka dina Tip-kontoautentiseringsuppgifter till [**CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) -metoden för att hämta ett [**IPartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) -gränssnitt till partner åtgärder.

2. Använd partner åtgärds gränssnittet för att hämta en samling rättigheter:

    1. Anropa Customers [**. ById ()-**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metoden med kund-ID: n för att ange kunden.

    2. Anropa **rättighets** egenskapen.

    3. Anropa **Get** -eller **GetAsync** -metoden för att hämta [**rättighets**](entitlement-resources.md) samlingen.

3. Se till att alla Azure Reserved Virtual Machine Instances-och program varu inköps order för kunden avbryts. För varje [**rättighet**](entitlement-resources.md) i samlingen:

    1. Använd [**rättigheten. ReferenceOrder.Id**](entitlement-resources.md#referenceorder) för att få en lokal kopia av motsvarande [order](order-resources.md#order) från kundens samling beställningar.

    2. Ange egenskapen [**order. status**](order-resources.md#order) till "avbruten".

    3. Använd metoden **patch ()** för att uppdatera ordningen.

4. Avbryt alla beställningar. Exempel: följande kod exempel använder en slinga för att avsöka varje order tills dess status är "avbruten".

    ``` csharp
    // IPartnerCredentials tipAccountCredentials;
    // Customer tenant Id to be deleted.
    // string customerTenantId;

    IPartner tipAccountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(tipAccountCredentials);

    // Get all entitlements whose order must be cancelled.
    ResourceCollection<Entitlement> entitlements = tipAccountPartnerOperations.Customers.ById(customerTenantId).Entitlements.Get();

    // Cancel all orders
    foreach (var entitlement in entitlements)
    {
        var order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(entitlement.ReferenceOrder.Id).Get();
        order.Status = "Cancelled";
        order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(order.Id).Patch(order);
    }

    // Keep polling until the status of all orders is "Cancelled".
    bool proceed = true;
    do
    {
        // Check if all the orders were cancelled.
        foreach (var entitlement in entitlements)
        {
            var order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(entitlement.ReferenceOrder.Id).Get();
            if (!order.Status.Equals("Cancelled", StringComparison.OrdinalIgnoreCase))
            {
                proceed = false;
            }
        }

        // Wait for a few seconds.
        Thread.Sleep(5000);
    }
    while (proceed == false);

    tipAccountPartnerOperations.Customers.ById(customerTenantId).Delete();
    ```

5. Se till att alla beställningar avbryts genom att anropa **Delete** -metoden för kunden.

**Exempel**: [konsol test app](console-test-app.md). **Projekt**: Partner Center PartnerCenterSDK. FeaturesSamples- **klass**: DeleteCustomerFromTipAccount.CS

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod     | URI för förfrågan                                                                            |
|------------|----------------------------------------------------------------------------------------|
| DELETE     | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID} http/1.1 |

#### <a name="uri-parameter"></a>URI-parameter

Använd följande frågeparameter för att ta bort en kund.

| Namn                   | Typ     | Obligatorisk | Beskrivning                                                                         |
|------------------------|----------|----------|-------------------------------------------------------------------------------------|
| kund-ID för klient organisation     | GUID     | Y        | Värdet är ett GUID-formaterat **kund-Tenant-ID** som gör det möjligt för åter försäljaren att filtrera resultaten för en specifik kund som tillhör åter försäljaren. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-example"></a>Exempel på begäran

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
Content-Length: 0
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden ett tomt svar.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
Date: Wed, 16 Mar 2016 00:43:02 GMT
```
