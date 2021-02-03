---
title: Hämta en kunds prenumerationer efter partner-MPN-ID
description: Så här hämtar du en lista över prenumerationer som tillhandahålls av en viss partner till en angiven kund.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: c95488b62449e1ab6bd2eeefea58d6686c291f4c
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769711"
---
# <a name="get-a-customers-subscriptions-by-partner-mpn-id"></a>Hämta en kunds prenumerationer efter partner-MPN-ID

**Gäller för**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Så här hämtar du en lista över prenumerationer som tillhandahålls av en viss partner till en angiven kund.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).

- Ett partner Microsoft Partner Network (MPN)-ID.

## <a name="c"></a>C\#

Om du vill hämta en lista över prenumerationer från en viss partner till en angiven kund använder du först metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: t för att identifiera kunden. Hämta sedan ett gränssnitt till åtgärder för kund prenumerations insamling från egenskapen [**prenumerationer**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) och anropa metoden [**ByPartner**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.bypartner) med MPN-ID för att identifiera partnern och hämta ett gränssnitt till partner prenumerations åtgärder. Anropa slutligen metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync) för att hämta samlingen.

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string partnerMpnId;

var customerSubscriptionsByMpnId = partnerOperations.Customers.ById(customerId).Subscriptions.ByPartner(partnerMpnId).Get();
```

**Exempel**: [konsol test app](console-test-app.md). **Projekt**: Partner Center SDK-exempel **klass**: GetSubscriptionsByMpnid.CS

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Om du vill hämta en lista över prenumerationer från en viss partner till en angiven kund använder du först funktionen **IAggregatePartner. getCustomers. byId** med kund-ID: t för att identifiera kunden. Hämta sedan ett gränssnitt till åtgärder för kund prenumerations insamling från funktionen **getSubscriptions** och anropa **byPartner** -funktionen med MPN-ID för att identifiera partnern och hämta ett gränssnitt till partner prenumerations åtgärder. Anropa slutligen funktionen **Get** för att hämta samlingen.

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String partnerMpnId;

ResourceCollection<Subscription> customerSubscriptionsByMpnId = partnerOperations.getCustomers().byId(customerId).getSubscriptions().byPartner(partnerMpnId).get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Om du vill hämta en lista över prenumerationer som tillhandahålls av en viss partner till en angiven kund kör du kommandot [**Get-PartnerCustomerSubscription**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscription.md) . Ange kund-ID: t för att identifiera kunden med parametern **CustomerId** och fyll i **MpnId** -parametern med MPN-ID för att identifiera partnern.

```powershell
# $customerId
# $partnerMpnId

Get-PartnerCustomerSubscription -CustomerId $customerId -MpnId $partnerMpnId
```

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod  | URI för förfrågan |
|---------|----------------------------------------------------------------------------------------------------------------|
| **TA** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Subscriptions? MPN \_ -ID = {MPN-ID} http/1.1 |

### <a name="uri-parameters"></a>URI-parametrar

Använd följande sökväg och frågeparametrar för att identifiera kunden och partnern.

| Namn        | Typ   | Obligatorisk | Beskrivning                                                 |
|-------------|--------|----------|-------------------------------------------------------------|
| kund-ID | sträng | Yes      | En GUID-formaterad sträng som identifierar kunden.       |
| MPN-ID      | int    | Yes      | Ett Microsoft Partner Network-ID som identifierar partnern. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/v1/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/subscriptions?mpn_id=4847383 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST-svar

Om det lyckas innehåller svars texten samlingen av [prenumerations](subscription-resources.md) resurser.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Length: 985
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CV: LdFhumtx6Ea0Kl5Z.0
MS-ServerId: 101112202
Date: Thu, 13 Apr 2017 20:58:08 GMT

{
    "totalCount": 1,
    "items": [{
            "id": "42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
            "offerId": "DB2E705F-B82A-4024-A3D5-D88E12F2DB35",
            "offerName": "Intune Device",
            "friendlyName": "new offer purchase",
            "quantity": 5,
            "unitType": "Licenses",
            "creationDate": "2017-04-10T23:02:26.02Z",
            "effectiveStartDate": "2017-04-10T00:00:00Z",
            "commitmentEndDate": "2018-05-07T00:00:00Z",
            "status": "active",
            "autoRenewEnabled": true,
            "isTrial": false,
            "billingType": "license",
            "billingCycle": "monthly",
            "partnerId": "4847383",
            "contractType": "subscription",
            "links": {
                "offer": {
                    "uri": "/offers/DB2E705F-B82A-4024-A3D5-D88E12F2DB35?country=US",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/subscriptions/42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
                    "method": "GET",
                    "headers": []
                }
            },
            "orderId": "3EDDCAC6-63B2-4C40-B0B6-F47E18301492",
            "attributes": {
                "etag": "eyJpZCI6IjQyMjI2ZWQ2LTA3MGEtNGUwZi1iODBjLTRjZGZiM2U5N2FhNyIsInZlcnNpb24iOjF9",
                "objectType": "Subscription"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

## <a name="see-also"></a>Se även

- [Partnercenter-analys – resurser](partner-center-analytics-resources.md)
