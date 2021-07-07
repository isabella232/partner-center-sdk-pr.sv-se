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
# <a name="remove-a-reseller-relationship-with-a-customer"></a><span data-ttu-id="d8ab6-103">Ta bort en förfrågan om återförsäljarrelation med en kund</span><span class="sxs-lookup"><span data-stu-id="d8ab6-103">Remove a reseller relationship with a customer</span></span>

<span data-ttu-id="d8ab6-104">Ta bort en återförsäljarrelation med en kund som du inte längre har transaktioner med.</span><span class="sxs-lookup"><span data-stu-id="d8ab6-104">Remove a reseller relationship with a customer that you no longer have transactions with.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d8ab6-105">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="d8ab6-105">Prerequisites</span></span>

- <span data-ttu-id="d8ab6-106">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d8ab6-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d8ab6-107">Det här scenariot stöder endast autentisering med app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="d8ab6-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="d8ab6-108">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d8ab6-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="d8ab6-109">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="d8ab6-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="d8ab6-110">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="d8ab6-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="d8ab6-111">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="d8ab6-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="d8ab6-112">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="d8ab6-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="d8ab6-113">Microsoft-ID:t är samma som kund-ID :t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d8ab6-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="d8ab6-114">Alla azure reserved VM Instance-beställningar måste avbrytas innan en återförsäljarrelation tas bort.</span><span class="sxs-lookup"><span data-stu-id="d8ab6-114">All Azure Reserved VM Instance orders must be canceled before a reseller relationship is removed.</span></span> <span data-ttu-id="d8ab6-115">Kontakta Azure-supporten om du vill avbryta eventuella öppna azure reserved VM Instance-beställningar.</span><span class="sxs-lookup"><span data-stu-id="d8ab6-115">Call Azure support for canceling any open Azure Reserved VM Instance orders.</span></span>

## <a name="c"></a><span data-ttu-id="d8ab6-116">C\#</span><span class="sxs-lookup"><span data-stu-id="d8ab6-116">C\#</span></span>

<span data-ttu-id="d8ab6-117">Om du vill ta bort återförsäljarrelationen för en kund måste du först se till att alla aktiva Azure Reserved VM Instances för den kunden avbryts.</span><span class="sxs-lookup"><span data-stu-id="d8ab6-117">To remove the reseller relationship for a customer, first ensure that any active Azure Reserved VM Instances for that customer are canceled.</span></span> <span data-ttu-id="d8ab6-118">Kontrollera sedan att alla aktiva prenumerationer för den kunden har inaktiverats.</span><span class="sxs-lookup"><span data-stu-id="d8ab6-118">Next, ensure that all active subscriptions for that customer are suspended.</span></span> <span data-ttu-id="d8ab6-119">Det gör du genom att fastställa ID:t för den kund som du vill ta bort återförsäljarrelationen för.</span><span class="sxs-lookup"><span data-stu-id="d8ab6-119">To do so, determine the ID of the customer for whom you want to delete the reseller relationship.</span></span> <span data-ttu-id="d8ab6-120">I följande kodexempel uppmanas användaren att ange kundidentifieraren.</span><span class="sxs-lookup"><span data-stu-id="d8ab6-120">In the following code example, the user is prompted to provide the customer identifier.</span></span>

<span data-ttu-id="d8ab6-121">För att avgöra om någon Azure Reserved VM Instances för kunden måste avbrytas hämtar du samlingen med rättigheter genom att anropa metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med hjälp av kundidentifieraren för att ange kunden och egenskapen [**Rättigheter**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) för att hämta ett gränssnitt för åtgärder för berättigandesamling.</span><span class="sxs-lookup"><span data-stu-id="d8ab6-121">To determine if any Azure Reserved VM Instances for the customer must be canceled, retrieve the collection of entitlements by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method using the customer identifier to specify the customer, and the [**Entitlements**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property to retrieve an interface to entitlement collection operations.</span></span> <span data-ttu-id="d8ab6-122">Anropa metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) för att hämta rättighetssamlingen.</span><span class="sxs-lookup"><span data-stu-id="d8ab6-122">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) method to retrieve the entitlement collection.</span></span> <span data-ttu-id="d8ab6-123">Filtrera samlingen för alla rättigheter med värdet [**EntitlementType.VirtualMachineReservedInstance.**](entitlement-resources.md#entitlementtype) Om det finns några kan du avbryta dem genom att anropa supporten innan du fortsätter. [](entitlement-resources.md#entitlementtype)</span><span class="sxs-lookup"><span data-stu-id="d8ab6-123">Filter the collection for any entitlements with an [**EntitlementType**](entitlement-resources.md#entitlementtype) value of [**EntitlementType.VirtualMachineReservedInstance**](entitlement-resources.md#entitlementtype) and if there are any, cancel them by calling support before proceeding.</span></span>

<span data-ttu-id="d8ab6-124">Hämta sedan en samling av kundens prenumerationer genom att anropa metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med hjälp av kundidentifieraren för att ange kunden och egenskapen [**Prenumerationer**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) för att hämta ett gränssnitt för prenumerationssamlingsåtgärder.</span><span class="sxs-lookup"><span data-stu-id="d8ab6-124">Then, retrieve a collection of the customer's subscriptions by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method using the customer identifier to specify the customer, and the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property to retrieve an interface to subscription collection operations.</span></span> <span data-ttu-id="d8ab6-125">Anropa slutligen metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) för att hämta kundens prenumerationssamling.</span><span class="sxs-lookup"><span data-stu-id="d8ab6-125">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) method to retrieve the customer's subscriptions collection.</span></span> <span data-ttu-id="d8ab6-126">Bläddra igenom prenumerationssamlingen och se till att ingen av prenumerationerna har [**egenskapsvärdet Subscriptions.Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) för [**SubscriptionStatus.Active.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus)</span><span class="sxs-lookup"><span data-stu-id="d8ab6-126">Traverse the subscription collection and ensure that none of the subscriptions have a [**Subscriptions.Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) property value of [**SubscriptionStatus.Active**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span></span> <span data-ttu-id="d8ab6-127">Om en prenumeration fortfarande är aktiv kan du läsa [Pausa en prenumeration](suspend-a-subscription.md) för information om hur du pausar den.</span><span class="sxs-lookup"><span data-stu-id="d8ab6-127">If a subscription is still active, see [Suspend a subscription](suspend-a-subscription.md) for information on how to suspend it.</span></span>

<span data-ttu-id="d8ab6-128">När du har bekräftat att alla aktiva Azure Reserved VM Instances för den kunden avbryts och att alla aktiva prenumerationer har inaktiverats kan du ta bort återförsäljarrelationen för kunden.</span><span class="sxs-lookup"><span data-stu-id="d8ab6-128">After confirming that all active Azure Reserved VM Instances for that customer are canceled and all active subscriptions are suspended, you can remove the reseller relationship for the customer.</span></span> <span data-ttu-id="d8ab6-129">Skapa först ett nytt [Customer/dotnet/api/microsoft.store.partnercenter.models.customers.customer) med egenskapen [Customer.RelationshipToPartner/dotnet/api/microsoft.store.partnercenter.models.customers.customer.relationshiptopartner) inställd på [**CustomerPartnerRelationship.None**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerpartnerrelationship).</span><span class="sxs-lookup"><span data-stu-id="d8ab6-129">First, create a new [Customer/dotnet/api/microsoft.store.partnercenter.models.customers.customer) object with the [Customer.RelationshipToPartner/dotnet/api/microsoft.store.partnercenter.models.customers.customer.relationshiptopartner) property set to [**CustomerPartnerRelationship.None**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerpartnerrelationship).</span></span> <span data-ttu-id="d8ab6-130">Anropa sedan [**metoden IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med hjälp av kundidentifieraren för att ange kunden och anropa **patch-metoden** och skicka in det nya kundobjektet.</span><span class="sxs-lookup"><span data-stu-id="d8ab6-130">Then call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method using the customer identifier to specify the customer, and call the **Patch** method, passing in the new customer object.</span></span>

<span data-ttu-id="d8ab6-131">Om du vill återupprätta relationen upprepar du processen för [begär en återförsäljarrelation/partner-center/utveckla/begära-återförsäljare-relation).</span><span class="sxs-lookup"><span data-stu-id="d8ab6-131">To re-establish the relationship, repeat the process of [requesting a reseller relationship/partner-center/develop/request-reseller-relationship).</span></span>

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

<span data-ttu-id="d8ab6-132">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="d8ab6-132">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="d8ab6-133">**Project:** PartnerSDK.FeatureSample-klass: DeletePartnerCustomerRelationship.cs </span><span class="sxs-lookup"><span data-stu-id="d8ab6-133">**Project**: PartnerSDK.FeatureSample **Class**: DeletePartnerCustomerRelationship.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="d8ab6-134">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="d8ab6-134">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d8ab6-135">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="d8ab6-135">Request syntax</span></span>

| <span data-ttu-id="d8ab6-136">Metod</span><span class="sxs-lookup"><span data-stu-id="d8ab6-136">Method</span></span>     | <span data-ttu-id="d8ab6-137">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="d8ab6-137">Request URI</span></span>                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d8ab6-138">**Patch**</span><span class="sxs-lookup"><span data-stu-id="d8ab6-138">**PATCH**</span></span>  | <span data-ttu-id="d8ab6-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/ HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d8ab6-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/ HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="d8ab6-140">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="d8ab6-140">URI parameter</span></span>

<span data-ttu-id="d8ab6-141">I den här tabellen visas de frågeparametrar som krävs för att ta bort en återförsäljarrelation.</span><span class="sxs-lookup"><span data-stu-id="d8ab6-141">This table lists the required query parameters to remove a reseller relationship.</span></span>

| <span data-ttu-id="d8ab6-142">Namn</span><span class="sxs-lookup"><span data-stu-id="d8ab6-142">Name</span></span>                   | <span data-ttu-id="d8ab6-143">Typ</span><span class="sxs-lookup"><span data-stu-id="d8ab6-143">Type</span></span>     | <span data-ttu-id="d8ab6-144">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="d8ab6-144">Required</span></span> | <span data-ttu-id="d8ab6-145">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="d8ab6-145">Description</span></span>                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| <span data-ttu-id="d8ab6-146">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="d8ab6-146">**customer-tenant-id**</span></span> | <span data-ttu-id="d8ab6-147">**guid**</span><span class="sxs-lookup"><span data-stu-id="d8ab6-147">**guid**</span></span> | <span data-ttu-id="d8ab6-148">Y</span><span class="sxs-lookup"><span data-stu-id="d8ab6-148">Y</span></span>        | <span data-ttu-id="d8ab6-149">Värdet är ett GUID-formaterat **kundklient-ID** som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="d8ab6-149">The value is a GUID formatted **customer-tenant-id** that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d8ab6-150">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="d8ab6-150">Request headers</span></span>

<span data-ttu-id="d8ab6-151">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="d8ab6-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d8ab6-152">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="d8ab6-152">Request body</span></span>

<span data-ttu-id="d8ab6-153">En **kundresurs** krävs i begärandetexten.</span><span class="sxs-lookup"><span data-stu-id="d8ab6-153">A **Customer** resource is required in the request body.</span></span> <span data-ttu-id="d8ab6-154">Se till **att egenskapen RelationshipToPartner** har angetts till ingen.</span><span class="sxs-lookup"><span data-stu-id="d8ab6-154">Ensure the **RelationshipToPartner** property has been set to none.</span></span>

### <a name="request-example"></a><span data-ttu-id="d8ab6-155">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="d8ab6-155">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="d8ab6-156">REST-svar</span><span class="sxs-lookup"><span data-stu-id="d8ab6-156">REST response</span></span>

<span data-ttu-id="d8ab6-157">Om det lyckas tar den här metoden bort en återförsäljarrelation för den angivna kunden.</span><span class="sxs-lookup"><span data-stu-id="d8ab6-157">If successful, this method removes a reseller relationship for the specified customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d8ab6-158">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="d8ab6-158">Response success and error codes</span></span>

<span data-ttu-id="d8ab6-159">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="d8ab6-159">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d8ab6-160">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="d8ab6-160">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d8ab6-161">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="d8ab6-161">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d8ab6-162">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="d8ab6-162">Response example</span></span>

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
