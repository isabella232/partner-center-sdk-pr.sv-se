---
title: Ta bort en förfrågan om återförsäljarrelation med en kund
description: Så här tar du bort en åter försäljares relation med en kund som du inte längre har transaktioner med.
ms.date: 01/12/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 084797997e57c63b5c447379bb08ecb88ebd0cc4
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769603"
---
# <a name="remove-a-reseller-relationship-with-a-customer"></a>Ta bort en förfrågan om återförsäljarrelation med en kund

**Gäller för**

- Partnercenter

Ta bort en åter försäljares relation med en kund som du inte längre har transaktioner med.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).

- Alla reserverade VM-instanser för Azure måste avbrytas innan en åter försäljares relation tas bort. Kontakta Azure-supporten om du vill avbryta öppna beställningar av reserverade VM-instanser för Azure.

## <a name="c"></a>C\#

Om du vill ta bort åter försäljarens relation för en kund måste du först se till att alla aktiva Azure Reserved VM Instances för kunden annulleras. Se sedan till att alla aktiva prenumerationer för kunden har pausats. Det gör du genom att fastställa ID: t för den kund för vilken du vill ta bort åter försäljarens relation. I följande kod exempel uppmanas användaren att ange kund-ID: t.

Du kan ta reda på om någon Azure Reserved VM Instances för kunden måste annulleras genom att hämta insamlingen av rättigheter genom att anropa metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med hjälp av kund-ID: t för att ange kunden och egenskapen [**rättigheter**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) för att hämta ett gränssnitt till behörighets insamlings åtgärder. Anropa [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) -eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) -metoden för att hämta rättighets samlingen. Filtrera samlingen för alla rättigheter med ett [**EntitlementType**](entitlement-resources.md#entitlementtype) -värde för [**EntitlementType. VirtualMachineReservedInstance**](entitlement-resources.md#entitlementtype) och om det finns några, kan du avbryta dem genom att anropa supporten innan du fortsätter.

Hämta sedan en samling av kundens prenumerationer genom att anropa metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med hjälp av kund-ID: n för att ange kunden och egenskapen [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) för att hämta ett gränssnitt till prenumerations samlings åtgärder. Anropa slutligen metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) för att hämta kundens prenumerations samling. Gå igenom prenumerations samlingen och se till att ingen av prenumerationerna har några [**prenumerationer. status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) egenskap svärdet för [**SubscriptionStatus. Active**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus). Om en prenumeration fortfarande är aktiv, se [pausa en prenumeration](https://review.docs.microsoft.com/partner-center/develop/suspend-a-subscription) för information om hur du pausar den.

När du har bekräftat att alla aktiva Azure Reserved VM Instances för kunden avbryts och alla aktiva prenumerationer har inaktiverats kan du ta bort åter försäljarens relation för kunden. Först skapar du ett nytt [Custom/dotNet/API/Microsoft. Store. Partnercenter. Models. Customers)-objekt med egenskapen [Custom. RelationshipToPartner/dotNet/API/Microsoft. Store. Partnercenter. Models. Customers. RelationshipToPartner) inställd på [**CustomerPartnerRelationship. None**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerpartnerrelationship). Anropa sedan metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med hjälp av kund-ID: n för att ange kunden och anropa **korrigerings** metoden genom att skicka in det nya kund-objektet.

Om du vill återupprätta relationen upprepar du processen för [begär en åter försäljare relation/partner-Center/utveckla/begäran-åter försäljare-relation).

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

**Exempel**: [konsol test app](console-test-app.md). **Projekt**: PartnerSDK. FeatureSample- **klass**: DeletePartnerCustomerRelationship.CS

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod     | URI för förfrågan                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------|
| **9.0a**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/http/1.1 |

### <a name="uri-parameter"></a>URI-parameter

Den här tabellen innehåller de frågeparametrar som krävs för att ta bort en åter försäljare relation.

| Namn                   | Typ     | Obligatorisk | Beskrivning                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| **kund-ID för klient organisation** | **guid** | Y        | Värdet är ett GUID-formaterat **kund-Tenant-ID** som identifierar kunden. |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

En **kund** resurs krävs i begär ande texten. Se till att egenskapen **RelationshipToPartner** har angetts till none.

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

Om det lyckas, tar den här metoden bort en åter försäljares relation för den angivna kunden.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).

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
