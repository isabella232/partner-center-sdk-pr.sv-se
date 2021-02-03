---
title: Hämta alla månatliga användnings poster för en prenumeration.
description: Du kan använda AzureResourceMonthlyUsageRecord-resurs samlingen för att hämta en lista över tjänster i en kunds prenumeration och deras associerade användnings information.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 1dd09d4976c9626e088cda02ce36669dd7121a99
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769735"
---
# <a name="get-all-monthly-usage-records-for-a-subscription"></a>Hämta alla månatliga användnings poster för en prenumeration.

**Gäller för:**

- Partnercenter
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Du kan använda [**AzureResourceMonthlyUsageRecord**](/dotnet/api/microsoft.store.partnercenter.models.usage.azureresourcemonthlyusagerecord) -resurs samlingen för att hämta en lista över tjänster i en kunds prenumeration och deras associerade användnings information.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).

- Ett prenumerations-ID.

*Detta API stöder bara Microsoft Azure (MS-AZR-0145P)-prenumerationer. Om du använder en Azure-plan läser du i stället [Hämta användnings data för prenumeration efter mätare](get-a-customer-subscription-meter-usage-records.md) .*

## <a name="c"></a>C\#

Så här hämtar du en prenumerations resursanvändnings information:

1. Använd din **IAggregatePartner. Customers** -samling för att anropa metoden **ById ()** .

2. Anropa egenskapen **Subscriptions** , och **UsageRecords**, sedan egenskapen **Resources** .
3. Anropa metoderna **Get ()** eller **GetAsync ()** .

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// var selectedSubscriptionID as string;

var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Resources.Get();
```

Ett exempel finns i följande avsnitt:

- Exempel: [konsol test app](console-test-app.md)
- Projekt: **PartnerSDK. FeatureSample**
- Klass: **SubscriptionResourceUsageRecords.cs**

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod  | URI för förfrågan                                                                                                                                       |
|---------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| **TA** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{ID-for-Subscription}/usagerecords/Resources http/1.1 |

#### <a name="uri-parameters"></a>URI-parametrar

Den här tabellen innehåller de frågeparametrar som krävs för att hämta information om den angivna användningen.

| Namn                    | Typ     | Obligatorisk | Beskrivning                               |
|-------------------------|----------|----------|-------------------------------------------|
| **kund-ID för klient organisation**  | **guid** | Y        | Ett GUID som motsvarar kunden.     |
| **prenumerations-ID** | **guid** | Y        | Ett GUID som motsvarar prenumerationen. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-example"></a>Exempel på begäran

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/usagerecords/resources HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 65b26053-37d0-4303-9fd1-46ad8012bcb6
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden en samling **AzureResourceMonthlyUsageRecord** -resurser i svars texten.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [felkoder](error-codes.md).

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
Content-Length: 12014
Content-Type: application/json
MS-CorrelationId: 648a26a4-a63e-459f-844b-4f29d7913353
MS-RequestId: be82a8ba-4a53-49f7-8313-b033c058687e
Date: Tue, 10 Nov 2015 19:09:59 GMT

{
    "totalCount":20,
    "items":[{
        "category":"Storage",
        "subcategory":"LOCALLY REDUNDANT",
        "quantityUsed":0.151287527825352,
        "unit":"GB",
        "id":"2a2419c0-cefe-46b2-8004-8eb002ad606c",
        "name":"Azure Resource 1",
        "totalCost":0.195779159290613,
        "currencyLocale":"en-US",
        "attributes":{
            "objectType":"AzureResourceMonthlyUsageRecord"
        }
    },
    {
        "category":"Remote App",
        "subcategory":"Remote App",
        "quantityUsed":0.932546524299563,
        "unit":"GB",
        "id":"7e4099c8-2b3d-41a6-a1bd-d5cf315989b2",
        "name":"Azure Resource 2",
        "totalCost":0.920983775016379,
        "currencyLocale":"en-US",
        "attributes":{
            "objectType":"AzureResourceMonthlyUsageRecord"
        }
    }],
    "links":{
        "self":{
            "uri":"/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription>%20/usagerecords",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "objectType":"Collection"
    }
}
```
