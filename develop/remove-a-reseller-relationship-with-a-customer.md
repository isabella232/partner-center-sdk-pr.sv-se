---
title: Ta bort en förfrågan om återförsäljarrelation med en kund
description: Ta bort en återförsäljarrelation med en kund som du inte längre har transaktioner med.
ms.date: 01/12/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 45eca3564c3b9078e04d1f8155d08849a589d52f
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446606"
---
# <a name="remove-a-reseller-relationship-with-a-customer"></a>Ta bort en förfrågan om återförsäljarrelation med en kund

Ta bort en återförsäljarrelation med en kund som du inte längre har transaktioner med.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med app- och användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard) Välj **CSP** på Menyn i Partnercenter följt av **Kunder**. Välj kunden i kundlistan och välj sedan **Konto.** På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.** Microsoft-ID:t är samma som kund-ID :t ( `customer-tenant-id` ).

- Alla azure reserved VM Instance-beställningar måste avbrytas innan en återförsäljarrelation tas bort. Kontakta Azure-supporten om du vill avbryta eventuella öppna azure reserved VM Instance-beställningar.

## <a name="c"></a>C\#

Om du vill ta bort återförsäljarrelationen för en kund måste du först se till att alla aktiva Azure Reserved VM Instances för den kunden avbryts. Kontrollera sedan att alla aktiva prenumerationer för den kunden har inaktiverats. Det gör du genom att fastställa ID:t för den kund som du vill ta bort återförsäljarrelationen för. I följande kodexempel uppmanas användaren att ange kundidentifieraren.

För att avgöra om någon Azure Reserved VM Instances för kunden måste avbrytas hämtar du samlingen med rättigheter genom att anropa metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med hjälp av kundidentifieraren för att ange kunden och egenskapen [**Rättigheter**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) för att hämta ett gränssnitt för åtgärder för berättigandesamling. Anropa metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) för att hämta rättighetssamlingen. Filtrera samlingen för alla rättigheter med värdet [**EntitlementType.VirtualMachineReservedInstance.**](entitlement-resources.md#entitlementtype) Om det finns några kan du avbryta dem genom att anropa supporten innan du fortsätter. [](entitlement-resources.md#entitlementtype)

Hämta sedan en samling av kundens prenumerationer genom att anropa metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med hjälp av kundidentifieraren för att ange kunden och egenskapen [**Prenumerationer**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) för att hämta ett gränssnitt för prenumerationssamlingsåtgärder. Anropa slutligen metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) för att hämta kundens prenumerationssamling. Bläddra igenom prenumerationssamlingen och se till att ingen av prenumerationerna har [**egenskapsvärdet Subscriptions.Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) för [**SubscriptionStatus.Active.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus) Om en prenumeration fortfarande är aktiv kan du läsa [Pausa en prenumeration](suspend-a-subscription.md) för information om hur du pausar den.

När du har bekräftat att alla aktiva Azure Reserved VM Instances för den kunden avbryts och att alla aktiva prenumerationer har inaktiverats kan du ta bort återförsäljarrelationen för kunden. Skapa först ett nytt [Customer/dotnet/api/microsoft.store.partnercenter.models.customers.customer) med egenskapen [Customer.RelationshipToPartner/dotnet/api/microsoft.store.partnercenter.models.customers.customer.relationshiptopartner) inställd på [**CustomerPartnerRelationship.None**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerpartnerrelationship). Anropa sedan [**metoden IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med hjälp av kundidentifieraren för att ange kunden och anropa **patch-metoden** och skicka in det nya kundobjektet.

Om du vill återupprätta relationen upprepar du processen för [begär en återförsäljarrelation/partner-center/utveckla/begära-återförsäljare-relation).

``` csharp
// IAggregatePartner partnerOperations;

// Prompt the user the enter the customer ID.
var customerIdToDeleteRelationshipOf = this.Context.ConsoleHelper.ReadNonEmptyString("Please enter the ID of the customer you want to delete the relationship with", "The customer ID can't be empty");

// Determine if there are any active Azure Reserved VM Instances for this customer.
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(customerIdToDeleteRelationshipOf).Entitlements.Get();

If (entitlements.Items.Where(x => x.EntitlementType == EntitlementType.VirtualMachineReservedInstance).Any())
{
    this.Context.ConsoleHelper.Warning("Please cancel Azure Reserved Virtual Machine Instance orders through support and try again. Aborting the delete customer relationship operation");
               return;
}

// Verify that there are no active subscriptions.
ResourceCollection<Subscription> customerSubscriptions = partnerOperations.Customers.ById(customerIdToDeleteRelationshipOf).Subscriptions.Get();
IList<Subscription> subscriptions = new List<Subscription>(customerSubscriptions.Items);

foreach (Subscription customerSubscription in subscriptions)
{
    if (customerSubscription.Status == SubscriptionStatus.Active)
    {
        this.Context.ConsoleHelper.Warning(String.Format("Subscription with ID :{0}  OfferName: {1} cannot be in active state, ", customerSubscription.Id, customerSubscription.OfferName));
        this.Context.ConsoleHelper.Warning("Please Suspend all the Subscriptions and try again. Aborting the delete customer relationship operation");
               return;
    }
}

// Delete the customer's relationship to the partner.
Customer customer = new Customer();
customer.RelationshipToPartner = CustomerPartnerRelationship.None;
customer = partnerOperations.Customers.ById(customerIdToDeleteRelationshipOf).Patch(customer);

if (customer.RelationshipToPartner == CustomerPartnerRelationship.None)
{
    this.Context.ConsoleHelper.Success("Customer Partner Relationship successfully deleted");
}
```

**Exempel:** [Konsoltestapp](console-test-app.md). **Project:** PartnerSDK.FeatureSample-klass: DeletePartnerCustomerRelationship.cs 

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod     | URI för förfrågan                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------|
| **Patch**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/ HTTP/1.1 |

### <a name="uri-parameter"></a>URI-parameter

I den här tabellen visas de frågeparametrar som krävs för att ta bort en återförsäljarrelation.

| Namn                   | Typ     | Obligatorisk | Beskrivning                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| **kund-klient-id** | **guid** | Y        | Värdet är ett GUID-formaterat **kundklient-ID** som identifierar kunden. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

En **kundresurs** krävs i begärandetexten. Se till **att egenskapen RelationshipToPartner** har angetts till ingen.

### <a name="request-example"></a>Exempel på begäran

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id> HTTP/1.1
Authorization: Bearer <token>
Content-Length: 74
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9b4bf2ca-f374-4d51-9113-781ca87b8380
MS-RequestId: 9fef8b23-6e3e-45d2-8678-e9fe89c35af5
Date: Fri, 12 Jan 2018 00:31:55 GMT

{
    "relationshipToPartner":"none",
    "attributes":{
        "objectType":"Customer"
    }
}
```

## <a name="rest-response"></a>REST-svar

Om det lyckas tar den här metoden bort en återförsäljarrelation för den angivna kunden.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)

### <a name="response-example"></a>Exempel på svar

```http
HTTP/1.1 200 OK
MS-RequestId: 7988dde4-b516-472c-b226-6d53fb18f04e
MS-CorrelationId: 9b4bf2ca-f374-4d51-9113-781ca87b8380
X-Locale: en-US
Content-Type: application/json
Content-Length: 242
Expect: 100-continue

{
    "Id":null,
    "CommerceId":null,
    "CompanyProfile":null,
    "BillingProfile":null,
    "RelationshipToPartner":"none",
    "AllowDelegatedAccess":null,
    "UserCredentials":null,
    "CustomDomains":null,
    "AssociatedPartnerId":null,
    "Attributes":{
        "ObjectType":"Customer"
    }
}
```
