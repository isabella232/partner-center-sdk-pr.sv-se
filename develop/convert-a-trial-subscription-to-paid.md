---
title: Konvertera en utvärderingsprenumeration till betald
description: 'Lär dig hur du använder API: er för partner Center för att konvertera en utvärderings prenumeration till en betald.'
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 59dcf6caf21d407b2fba4cc8438bc435fda9dc77
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/04/2020
ms.locfileid: "97770065"
---
# <a name="convert-a-trial-subscription-to-paid-using-partner-center-apis"></a>Konvertera en utvärderings prenumeration till betald med API: er för partner Center

**Gäller för:**

- Partnercenter

Du kan konvertera en utvärderings prenumeration till betald.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).

- Ett prenumerations-ID för en aktiv utvärderings prenumeration.

- Ett tillgängligt konverterings erbjudande.

## <a name="convert-a-trial-subscription-to-paid-through-code"></a>Konvertera en utvärderings prenumeration till betald via kod

Om du vill konvertera en utvärderings prenumeration till en betald, måste du först skaffa en samling utvärderings versioner som är tillgängliga. Sedan måste du välja det konverterings erbjudande som du vill köpa.

Konverterings erbjudandet anger en kvantitet som är standard för samma antal licenser som utvärderings prenumerationen. Du kan ändra den här kvantiteten genom att ställa in egenskapen [**kvantitet**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion.quantity) på det antal licenser som du vill köpa.

> [!NOTE]
> Oavsett hur många licenser du har köpt återanvänds prenumerations-ID: t för utvärderings versionen för de köpta licenserna. På grund av detta försvinner utvärderings versionen och ersätts av köpet.

Använd följande steg för att konvertera en utvärderings prenumeration via kod:

1. Hämta ett gränssnitt till tillgängliga prenumerations åtgärder. Du måste identifiera kunden och ange prenumerations-ID för utvärderings prenumerationen.

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2. Hämta en samling av de tillgängliga konverterings erbjudandena. Mer information och information om begäran/svar för den här metoden finns i [Hämta en lista över erbjudanden om utvärderings konvertering](get-a-list-of-trial-conversion-offers.md).

    ``` csharp
    var conversions = subscriptionOperations.Conversions.Get();
    ```

3. Välj ett konverterings erbjudande. Följande kod väljer det första konverterings erbjudandet i samlingen.

    ``` csharp
    var selectedConversion = conversions.Items.ToList()[0];
    ```

4. Alternativt kan du ange antalet licenser som ska köpas. Standardvärdet är antalet licenser i utvärderings prenumerationen.

    ``` csharp
    selectedConversion.Quantity = 10;
    ```

5. Anropa metoden [**create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) eller [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) för att konvertera utvärderings prenumerationen till betald.

    ``` csharp
    var convertResult = subscriptionOperations.Conversions.Create(selectedConversion);
    ```

## <a name="c"></a>C\#

Så här konverterar du en utvärderings prenumeration till en betald:

1. Använd metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: t för att identifiera kunden.

2. Hämta ett gränssnitt för prenumerations åtgärder genom att anropa metoden [**Subscriptions. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) med utvärderings prenumerationens ID. Spara en referens till prenumerations åtgärds gränssnittet i en lokal variabel.

3. Använd egenskapen [**konverteringar**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) för att hämta ett gränssnitt till de tillgängliga åtgärderna för konverteringar och anropa sedan metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) för att hämta en samling tillgängliga [**konverterings**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) erbjudanden. Du måste välja ett. I följande exempel är standard den första konverteringen tillgänglig.

4. Använd referensen till det prenumerations åtgärds gränssnitt som du sparade i en lokal variabel och egenskapen [**konverteringar**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) för att hämta ett gränssnitt till de tillgängliga åtgärderna för konverteringar.

5. Överför det valda konverterings erbjudande objektet till metoden [**create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) eller [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) för att försöka utföra utvärderings konverteringen.

### <a name="c-example"></a>C- \# exempel

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

// Get subscription operations for the trial subscription.
var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);

// Get the available conversions.
var conversions = subscriptionOperations.Conversions.Get();

// If there are no conversions available, we&#39;re done.
// Otherwise, convert the trial to the first available conversion offer.
if (conversions.TotalCount <= 0)
{
    System.Console.WriteLine("This subscription has no conversions");
}
else
{
    // Default to the first conversion.
    var selectedConversion = conversions.Items.ToList()[0];

    // Convert the trial and return the result.
    var convertResult = subscriptionOperations.Conversions.Create(selectedConversion);
}
```

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod   | URI för förfrågan                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| **EFTER** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Subscriptions/{Subscription-ID}/conversions http/1.1 |

### <a name="uri-parameter"></a>URI-parameter

Använd följande Sök vägs parametrar för att identifiera kunden och utvärderings prenumerationen.

| Namn            | Typ   | Obligatorisk | Beskrivning                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| kund-ID     | sträng | Yes      | En GUID-formaterad sträng som identifierar kunden.           |
| prenumerations-ID | sträng | Yes      | En GUID-formaterad sträng som identifierar utvärderings prenumerationen. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

En ifylld [konverterings](conversions-resources.md#conversion) resurs måste ingå i begär ande texten.

### <a name="request-example"></a>Exempel på begäran

```http
POST https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/488745B5-2086-4912-802C-6ABB9F7C3638/conversions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bd0cde7f-ba87-4010-8a73-1190b641f2a4
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 234
Expect: 100-continue

{
    "OfferId": "C0BD2E08-11AC-4836-BDC7-3712E744922F",
    "TargetOfferId": "031C9E47-4802-4248-838E-778FB1D2CC05",
    "OrderId": "D51A052E-043C-4A2A-AA37-2BB938CEF6C1",
    "Quantity": 25,
    "BillingCycle": "monthly",
    "Attributes": {
        "ObjectType": "Conversion"
    }
}
```

## <a name="rest-response"></a>REST-svar

Om det lyckas innehåller svars texten en [ConversionResult](conversions-resources.md#conversionresult) -resurs.

#### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [fel koder för partner Center](error-codes.md).

#### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Length: 211
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
MS-RequestId: bd0cde7f-ba87-4010-8a73-1190b641f2a4
MS-CV: kW4GzmhvHEqCq1ls.0
MS-ServerId: 030020643
Date: Thu, 15 Jun 2017 23:10:40 GMT

 {
    "subscriptionId": "488745B5-2086-4912-802C-6ABB9F7C3638",
    "offerId": "C0BD2E08-11AC-4836-BDC7-3712E744922F",
    "targetOfferId": "031C9E47-4802-4248-838E-778FB1D2CC05",
    "attributes": {
        "objectType": "ConversionResult"
    }
}
```
