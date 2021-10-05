---
title: Konvertera en utvärderingsprenumeration till betald
description: Lär dig hur du använder Partner Center-API:er för att konvertera en utvärderingsprenumeration till en betald prenumeration.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7cee9b9afddb12137bb66b57250a9487bd4902f5
ms.sourcegitcommit: f112efee7344d739bdbf385adba0c554ea2a63e3
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/04/2021
ms.locfileid: "129439335"
---
# <a name="convert-a-trial-subscription-to-paid-using-partner-center-apis"></a>Konvertera en utvärderingsprenumeration till betald med partnercenter-API:er

> [!NOTE]
> De här stegen gäller inte för nya handelsprodukter. Se **Övergångsdokumentation för en ny handelsprenumeration** för konvertering av nya handelsversioner till betalda prenumerationer

Du kan konvertera en utvärderingsprenumeration till betald.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med app+användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard) Välj **CSP** på Menyn i Partnercenter följt av **Kunder**. Välj kunden i kundlistan och välj sedan **Konto.** På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.** Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).

- Ett prenumerations-ID för en aktiv utvärderingsprenumeration.

- Ett tillgängligt konverteringserbjudande.

## <a name="convert-a-trial-subscription-to-a-paid-subscription-through-code"></a>Konvertera en utvärderingsprenumeration till en betald prenumeration via kod

Om du vill konvertera en utvärderingsprenumeration till en betald prenumeration måste du först skaffa en samling med tillgängliga utvärderingskonverteringar. Sedan måste du välja det konverteringserbjudande som du vill köpa.

Konverteringserbjudandena anger en kvantitet som har samma antal licenser som utvärderingsprenumerationen som standard. Du kan ändra den här kvantiteten genom [**att ange**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion.quantity) egenskapen Quantity till det antal licenser som du vill köpa.

> [!NOTE]
> Oavsett antalet köpta licenser återanvänds prenumerations-ID:t för utvärderingsversionen för de köpta licenserna. Därför försvinner den utvärderingsversion som används och ersätts av köpet.

Använd följande steg för att konvertera en utvärderingsprenumeration via kod:

1. Hämta ett gränssnitt för de prenumerationsåtgärder som är tillgängliga. Du måste identifiera kunden och ange prenumerations-ID för utvärderingsprenumerationen.

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2. Hämta en samling med tillgängliga konverteringserbjudanden. Mer information om begäran/svar för den här metoden finns i [Hämta en lista över utvärderingskonverteringserbjudanden.](get-a-list-of-trial-conversion-offers.md)

    ``` csharp
    var conversions = subscriptionOperations.Conversions.Get();
    ```

3. Välj ett konverteringserbjudande. Följande kod väljer det första konverteringserbjudandet i samlingen.

    ``` csharp
    var selectedConversion = conversions.Items.ToList()[0];
    ```

4. Du kan också ange antalet licenser som ska köpas. Standardvärdet är antalet licenser i utvärderingsprenumerationen.

    ``` csharp
    selectedConversion.Quantity = 10;
    ```

5. Anropa metoden [**Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) eller [**CreateAsync för**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) att konvertera utvärderingsprenumerationen till betald.

    ``` csharp
    var convertResult = subscriptionOperations.Conversions.Create(selectedConversion);
    ```

## <a name="c"></a>C\#

Så här konverterar du en utvärderingsprenumeration till en betald prenumeration:

1. Använd metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att identifiera kunden.

2. Hämta ett gränssnitt för prenumerationsåtgärder genom att anropa [**metoden Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) med utvärderingsprenumerationens ID. Spara en referens till gränssnittet för prenumerationsåtgärder i en lokal variabel.

3. Använd egenskapen [**Konverteringar**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) för att hämta ett gränssnitt till de tillgängliga åtgärderna för konverteringar och anropa sedan metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) för att hämta en samling tillgängliga [**konverteringserbjudanden.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) Du måste välja en. I följande exempel används som standard den första tillgängliga konverteringen.

4. Använd referensen till [**prenumerationsgränssnittet**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) som du sparade i en lokal variabel och egenskapen Konverteringar för att hämta ett gränssnitt för de tillgängliga åtgärderna för konverteringar.

5. Skicka det valda konverteringserbjudandet till metoden [**Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) eller [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) för att försöka konvertera utvärderingsversionen.

### <a name="c-example"></a>\#C-exempel

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

### <a name="request-syntax"></a>Begärandesyntax

| Metod   | URI för förfrågan                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| **INLÄGG** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions HTTP/1.1 |

### <a name="uri-parameter"></a>URI-parameter

Använd följande sökvägsparametrar för att identifiera kunden och utvärderingsprenumerationen.

| Namn            | Typ   | Obligatorisk | Beskrivning                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| kund-id     | sträng | Ja      | En GUID-formaterad sträng som identifierar kunden.           |
| prenumerations-id | sträng | Ja      | En GUID-formaterad sträng som identifierar utvärderingsprenumerationen. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

En ifylld [konverteringsresurs](conversions-resources.md#conversion) måste inkluderas i begärandetexten.

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

Om det lyckas innehåller svarstexten en [ConversionResult-resurs.](conversions-resources.md#conversionresult)

#### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Felkoder i Partnercenter.](error-codes.md)

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
