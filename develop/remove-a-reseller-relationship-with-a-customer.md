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
# <a name="remove-a-reseller-relationship-with-a-customer"></a><span data-ttu-id="daaab-103">Ta bort en förfrågan om återförsäljarrelation med en kund</span><span class="sxs-lookup"><span data-stu-id="daaab-103">Remove a reseller relationship with a customer</span></span>

<span data-ttu-id="daaab-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="daaab-104">**Applies To**</span></span>

- <span data-ttu-id="daaab-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="daaab-105">Partner Center</span></span>

<span data-ttu-id="daaab-106">Ta bort en åter försäljares relation med en kund som du inte längre har transaktioner med.</span><span class="sxs-lookup"><span data-stu-id="daaab-106">Remove a reseller relationship with a customer that you no longer have transactions with.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="daaab-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="daaab-107">Prerequisites</span></span>

- <span data-ttu-id="daaab-108">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="daaab-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="daaab-109">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="daaab-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="daaab-110">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="daaab-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="daaab-111">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="daaab-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="daaab-112">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="daaab-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="daaab-113">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="daaab-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="daaab-114">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="daaab-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="daaab-115">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="daaab-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="daaab-116">Alla reserverade VM-instanser för Azure måste avbrytas innan en åter försäljares relation tas bort.</span><span class="sxs-lookup"><span data-stu-id="daaab-116">All Azure Reserved VM Instance orders must be canceled before a reseller relationship is removed.</span></span> <span data-ttu-id="daaab-117">Kontakta Azure-supporten om du vill avbryta öppna beställningar av reserverade VM-instanser för Azure.</span><span class="sxs-lookup"><span data-stu-id="daaab-117">Call Azure support for canceling any open Azure Reserved VM Instance orders.</span></span>

## <a name="c"></a><span data-ttu-id="daaab-118">C\#</span><span class="sxs-lookup"><span data-stu-id="daaab-118">C\#</span></span>

<span data-ttu-id="daaab-119">Om du vill ta bort åter försäljarens relation för en kund måste du först se till att alla aktiva Azure Reserved VM Instances för kunden annulleras.</span><span class="sxs-lookup"><span data-stu-id="daaab-119">To remove the reseller relationship for a customer, first ensure that any active Azure Reserved VM Instances for that customer are canceled.</span></span> <span data-ttu-id="daaab-120">Se sedan till att alla aktiva prenumerationer för kunden har pausats.</span><span class="sxs-lookup"><span data-stu-id="daaab-120">Next, ensure that all active subscriptions for that customer are suspended.</span></span> <span data-ttu-id="daaab-121">Det gör du genom att fastställa ID: t för den kund för vilken du vill ta bort åter försäljarens relation.</span><span class="sxs-lookup"><span data-stu-id="daaab-121">To do so, determine the ID of the customer for whom you want to delete the reseller relationship.</span></span> <span data-ttu-id="daaab-122">I följande kod exempel uppmanas användaren att ange kund-ID: t.</span><span class="sxs-lookup"><span data-stu-id="daaab-122">In the following code example, the user is prompted to provide the customer identifier.</span></span>

<span data-ttu-id="daaab-123">Du kan ta reda på om någon Azure Reserved VM Instances för kunden måste annulleras genom att hämta insamlingen av rättigheter genom att anropa metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med hjälp av kund-ID: t för att ange kunden och egenskapen [**rättigheter**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) för att hämta ett gränssnitt till behörighets insamlings åtgärder.</span><span class="sxs-lookup"><span data-stu-id="daaab-123">To determine if any Azure Reserved VM Instances for the customer must be canceled, retrieve the collection of entitlements by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method using the customer identifier to specify the customer, and the [**Entitlements**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property to retrieve an interface to entitlement collection operations.</span></span> <span data-ttu-id="daaab-124">Anropa [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) -eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) -metoden för att hämta rättighets samlingen.</span><span class="sxs-lookup"><span data-stu-id="daaab-124">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) method to retrieve the entitlement collection.</span></span> <span data-ttu-id="daaab-125">Filtrera samlingen för alla rättigheter med ett [**EntitlementType**](entitlement-resources.md#entitlementtype) -värde för [**EntitlementType. VirtualMachineReservedInstance**](entitlement-resources.md#entitlementtype) och om det finns några, kan du avbryta dem genom att anropa supporten innan du fortsätter.</span><span class="sxs-lookup"><span data-stu-id="daaab-125">Filter the collection for any entitlements with an [**EntitlementType**](entitlement-resources.md#entitlementtype) value of [**EntitlementType.VirtualMachineReservedInstance**](entitlement-resources.md#entitlementtype) and if there are any, cancel them by calling support before proceeding.</span></span>

<span data-ttu-id="daaab-126">Hämta sedan en samling av kundens prenumerationer genom att anropa metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med hjälp av kund-ID: n för att ange kunden och egenskapen [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) för att hämta ett gränssnitt till prenumerations samlings åtgärder.</span><span class="sxs-lookup"><span data-stu-id="daaab-126">Then, retrieve a collection of the customer's subscriptions by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method using the customer identifier to specify the customer, and the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property to retrieve an interface to subscription collection operations.</span></span> <span data-ttu-id="daaab-127">Anropa slutligen metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) för att hämta kundens prenumerations samling.</span><span class="sxs-lookup"><span data-stu-id="daaab-127">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) method to retrieve the customer's subscriptions collection.</span></span> <span data-ttu-id="daaab-128">Gå igenom prenumerations samlingen och se till att ingen av prenumerationerna har några [**prenumerationer. status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) egenskap svärdet för [**SubscriptionStatus. Active**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span><span class="sxs-lookup"><span data-stu-id="daaab-128">Traverse the subscription collection and ensure that none of the subscriptions have a [**Subscriptions.Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) property value of [**SubscriptionStatus.Active**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span></span> <span data-ttu-id="daaab-129">Om en prenumeration fortfarande är aktiv, se [pausa en prenumeration](https://review.docs.microsoft.com/partner-center/develop/suspend-a-subscription) för information om hur du pausar den.</span><span class="sxs-lookup"><span data-stu-id="daaab-129">If a subscription is still active, see [Suspend a subscription](https://review.docs.microsoft.com/partner-center/develop/suspend-a-subscription) for information on how to suspend it.</span></span>

<span data-ttu-id="daaab-130">När du har bekräftat att alla aktiva Azure Reserved VM Instances för kunden avbryts och alla aktiva prenumerationer har inaktiverats kan du ta bort åter försäljarens relation för kunden.</span><span class="sxs-lookup"><span data-stu-id="daaab-130">After confirming that all active Azure Reserved VM Instances for that customer are canceled and all active subscriptions are suspended, you can remove the reseller relationship for the customer.</span></span> <span data-ttu-id="daaab-131">Först skapar du ett nytt [Custom/dotNet/API/Microsoft. Store. Partnercenter. Models. Customers)-objekt med egenskapen [Custom. RelationshipToPartner/dotNet/API/Microsoft. Store. Partnercenter. Models. Customers. RelationshipToPartner) inställd på [**CustomerPartnerRelationship. None**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerpartnerrelationship).</span><span class="sxs-lookup"><span data-stu-id="daaab-131">First, create a new [Customer/dotnet/api/microsoft.store.partnercenter.models.customers.customer) object with the [Customer.RelationshipToPartner/dotnet/api/microsoft.store.partnercenter.models.customers.customer.relationshiptopartner) property set to [**CustomerPartnerRelationship.None**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerpartnerrelationship).</span></span> <span data-ttu-id="daaab-132">Anropa sedan metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med hjälp av kund-ID: n för att ange kunden och anropa **korrigerings** metoden genom att skicka in det nya kund-objektet.</span><span class="sxs-lookup"><span data-stu-id="daaab-132">Then call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method using the customer identifier to specify the customer, and call the **Patch** method, passing in the new customer object.</span></span>

<span data-ttu-id="daaab-133">Om du vill återupprätta relationen upprepar du processen för [begär en åter försäljare relation/partner-Center/utveckla/begäran-åter försäljare-relation).</span><span class="sxs-lookup"><span data-stu-id="daaab-133">To re-establish the relationship, repeat the process of [requesting a reseller relationship/partner-center/develop/request-reseller-relationship).</span></span>

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

<span data-ttu-id="daaab-134">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="daaab-134">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="daaab-135">**Projekt**: PartnerSDK. FeatureSample- **klass**: DeletePartnerCustomerRelationship.CS</span><span class="sxs-lookup"><span data-stu-id="daaab-135">**Project**: PartnerSDK.FeatureSample **Class**: DeletePartnerCustomerRelationship.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="daaab-136">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="daaab-136">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="daaab-137">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="daaab-137">Request syntax</span></span>

| <span data-ttu-id="daaab-138">Metod</span><span class="sxs-lookup"><span data-stu-id="daaab-138">Method</span></span>     | <span data-ttu-id="daaab-139">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="daaab-139">Request URI</span></span>                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="daaab-140">**9.0a**</span><span class="sxs-lookup"><span data-stu-id="daaab-140">**PATCH**</span></span>  | <span data-ttu-id="daaab-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/http/1.1</span><span class="sxs-lookup"><span data-stu-id="daaab-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/ HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="daaab-142">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="daaab-142">URI parameter</span></span>

<span data-ttu-id="daaab-143">Den här tabellen innehåller de frågeparametrar som krävs för att ta bort en åter försäljare relation.</span><span class="sxs-lookup"><span data-stu-id="daaab-143">This table lists the required query parameters to remove a reseller relationship.</span></span>

| <span data-ttu-id="daaab-144">Namn</span><span class="sxs-lookup"><span data-stu-id="daaab-144">Name</span></span>                   | <span data-ttu-id="daaab-145">Typ</span><span class="sxs-lookup"><span data-stu-id="daaab-145">Type</span></span>     | <span data-ttu-id="daaab-146">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="daaab-146">Required</span></span> | <span data-ttu-id="daaab-147">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="daaab-147">Description</span></span>                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| <span data-ttu-id="daaab-148">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="daaab-148">**customer-tenant-id**</span></span> | <span data-ttu-id="daaab-149">**guid**</span><span class="sxs-lookup"><span data-stu-id="daaab-149">**guid**</span></span> | <span data-ttu-id="daaab-150">Y</span><span class="sxs-lookup"><span data-stu-id="daaab-150">Y</span></span>        | <span data-ttu-id="daaab-151">Värdet är ett GUID-formaterat **kund-Tenant-ID** som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="daaab-151">The value is a GUID formatted **customer-tenant-id** that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="daaab-152">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="daaab-152">Request headers</span></span>

<span data-ttu-id="daaab-153">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="daaab-153">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="daaab-154">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="daaab-154">Request body</span></span>

<span data-ttu-id="daaab-155">En **kund** resurs krävs i begär ande texten.</span><span class="sxs-lookup"><span data-stu-id="daaab-155">A **Customer** resource is required in the request body.</span></span> <span data-ttu-id="daaab-156">Se till att egenskapen **RelationshipToPartner** har angetts till none.</span><span class="sxs-lookup"><span data-stu-id="daaab-156">Ensure the **RelationshipToPartner** property has been set to none.</span></span>

### <a name="request-example"></a><span data-ttu-id="daaab-157">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="daaab-157">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="daaab-158">REST-svar</span><span class="sxs-lookup"><span data-stu-id="daaab-158">REST response</span></span>

<span data-ttu-id="daaab-159">Om det lyckas, tar den här metoden bort en åter försäljares relation för den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="daaab-159">If successful, this method removes a reseller relationship for the specified customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="daaab-160">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="daaab-160">Response success and error codes</span></span>

<span data-ttu-id="daaab-161">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="daaab-161">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="daaab-162">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="daaab-162">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="daaab-163">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="daaab-163">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="daaab-164">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="daaab-164">Response example</span></span>

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
