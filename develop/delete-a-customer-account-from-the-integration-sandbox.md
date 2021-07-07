---
title: Ta bort ett kundkonto från sandbox-miljön för integrering
description: Ta bort ett kundkonto från sandbox-miljön Testing in Production (tips)-integrering.
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b9d9e44ac9c40bd4e3c7e1a9e04253f853dfd96c
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973136"
---
# <a name="delete-a-customer-account-from-the-integration-sandbox"></a>Ta bort ett kundkonto från sandbox-miljön för integrering

**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Den här artikeln förklarar hur du bryter relationen mellan partnern och kundkontot och återfår kvoten för sandbox Testing in Production integrering (tips).

> [!IMPORTANT]
> När du tar bort ett kundkonto rensas alla resurser som är associerade med kundklientorganisationen.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard) Välj **CSP** på Menyn i Partnercenter följt av **Kunder**. Välj kunden i kundlistan och välj sedan **Konto.** På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.** Microsoft-ID:t är samma som kund-ID :t ( `customer-tenant-id` ).

- Alla Azure Reserved Virtual Machine Instances och programvaruköpordrar måste avbrytas innan du tar bort en kund från sandbox-miljön för Tipsintegrering.

## <a name="c"></a>C\#

Så här tar du bort en kund från sandbox-miljön för tipsintegrering:

1. Skicka autentiseringsuppgifterna för ditt tipskonto [**till metoden CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) för att hämta [**ett IPartner-gränssnitt**](/dotnet/api/microsoft.store.partnercenter.ipartner) till partneråtgärder.

2. Använd gränssnittet för partneråtgärder för att hämta samlingen med rättigheter:

    1. Anropa metoden [**Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kundidentifieraren för att ange kunden.

    2. Anropa egenskapen **Berättiganden.**

    3. Anropa metoden **Get** eller **GetAsync** för att hämta [**berättigandesamlingen.**](entitlement-resources.md)

3. Se till att alla Azure Reserved Virtual Machine Instances och programvaruköpsorder för den kunden annulleras. För varje [**berättigande**](entitlement-resources.md) i samlingen:

    1. Använd [**rättigheten. ReferenceOrder.Id**](entitlement-resources.md#referenceorder) hämta en lokal kopia av [motsvarande Order](order-resources.md#order) från kundens ordersamling.

    2. Ange egenskapen [**Order.Status**](order-resources.md#order) till "Cancelled" (Avbruten).

    3. Använd **metoden Patch()** för att uppdatera ordningen.

4. Avbryt alla beställningar. Följande kodexempel använder till exempel en loop för att avssöka varje order tills dess status är "Cancelled".

    ``` csharp
    // IPartnerCredentials tipAccountCredentials;
    // Customer tenant Id to be deleted.
    // string customerTenantId;

    IPartner tipAccountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(tipAccountCredentials);

    // Get all entitlements whose order must be canceled.
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
        // Check if all the orders were canceled.
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

5. Kontrollera att alla beställningar annulleras genom att anropa **delete-metoden** för kunden.

**Exempel:** [Konsoltestapp](console-test-app.md). **Project:** Partner Center PartnerCenterSDK.FeaturesSamples-klass: DeleteCustomerFromTipAccount.cs 

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod     | URI för förfrågan                                                                            |
|------------|----------------------------------------------------------------------------------------|
| DELETE     | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id} HTTP/1.1 |

#### <a name="uri-parameter"></a>URI-parameter

Använd följande frågeparameter för att ta bort en kund.

| Namn                   | Typ     | Obligatorisk | Beskrivning                                                                         |
|------------------------|----------|----------|-------------------------------------------------------------------------------------|
| kund-klient-id     | GUID     | Y        | Värdet är ett GUID-formaterat **kundklient-ID** som gör att återförsäljaren kan filtrera resultaten för en viss kund som tillhör återförsäljaren. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

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

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
Date: Wed, 16 Mar 2016 00:43:02 GMT
```
