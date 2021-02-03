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
# <a name="delete-a-customer-account-from-the-integration-sandbox"></a><span data-ttu-id="150f1-103">Ta bort ett kundkonto från sandbox-miljön för integrering</span><span class="sxs-lookup"><span data-stu-id="150f1-103">Delete a customer account from the integration sandbox</span></span>

<span data-ttu-id="150f1-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="150f1-104">**Applies to:**</span></span>

- <span data-ttu-id="150f1-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="150f1-105">Partner Center</span></span>
- <span data-ttu-id="150f1-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="150f1-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="150f1-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="150f1-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="150f1-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="150f1-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="150f1-109">I den här artikeln beskrivs hur du delar upp relationen mellan partnern och kund kontot och återfår kvoten för Testing in Production (Tip)-integration sandbox.</span><span class="sxs-lookup"><span data-stu-id="150f1-109">This article explains, how to break the relationship between the partner and the customer account and regain the quota for Testing in Production (Tip) integration sandbox.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="150f1-110">När du tar bort ett kund konto rensas alla resurser som är kopplade till kund klienten.</span><span class="sxs-lookup"><span data-stu-id="150f1-110">When you delete a customer account, all resources associated with that customer tenant will be purged.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="150f1-111">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="150f1-111">Prerequisites</span></span>

- <span data-ttu-id="150f1-112">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="150f1-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="150f1-113">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="150f1-113">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="150f1-114">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="150f1-114">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="150f1-115">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="150f1-115">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="150f1-116">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="150f1-116">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="150f1-117">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="150f1-117">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="150f1-118">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="150f1-118">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="150f1-119">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="150f1-119">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="150f1-120">Alla Azure Reserved Virtual Machine Instances-och program inköps order måste avbrytas innan du tar bort en kund från det begränsade tipset för tips integrering.</span><span class="sxs-lookup"><span data-stu-id="150f1-120">All Azure Reserved Virtual Machine Instances and software purchase orders must be cancelled before deleting a customer from the Tip integration sandbox.</span></span>

## <a name="c"></a><span data-ttu-id="150f1-121">C\#</span><span class="sxs-lookup"><span data-stu-id="150f1-121">C\#</span></span>

<span data-ttu-id="150f1-122">Så här tar du bort en kund från sandbox-tipset för integrering:</span><span class="sxs-lookup"><span data-stu-id="150f1-122">To delete a customer from the Tip integration sandbox:</span></span>

1. <span data-ttu-id="150f1-123">Skicka dina Tip-kontoautentiseringsuppgifter till [**CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) -metoden för att hämta ett [**IPartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) -gränssnitt till partner åtgärder.</span><span class="sxs-lookup"><span data-stu-id="150f1-123">Pass your Tip account credentials to the [**CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) method to get an [**IPartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) interface to partner operations.</span></span>

2. <span data-ttu-id="150f1-124">Använd partner åtgärds gränssnittet för att hämta en samling rättigheter:</span><span class="sxs-lookup"><span data-stu-id="150f1-124">Use the partner operations interface to retrieve the collection of entitlements:</span></span>

    1. <span data-ttu-id="150f1-125">Anropa Customers [**. ById ()-**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metoden med kund-ID: n för att ange kunden.</span><span class="sxs-lookup"><span data-stu-id="150f1-125">Call the [**Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to specify the customer.</span></span>

    2. <span data-ttu-id="150f1-126">Anropa **rättighets** egenskapen.</span><span class="sxs-lookup"><span data-stu-id="150f1-126">Call the **Entitlements** property.</span></span>

    3. <span data-ttu-id="150f1-127">Anropa **Get** -eller **GetAsync** -metoden för att hämta [**rättighets**](entitlement-resources.md) samlingen.</span><span class="sxs-lookup"><span data-stu-id="150f1-127">Call the **Get** or **GetAsync** method to retrieve the [**Entitlement**](entitlement-resources.md) collection.</span></span>

3. <span data-ttu-id="150f1-128">Se till att alla Azure Reserved Virtual Machine Instances-och program varu inköps order för kunden avbryts.</span><span class="sxs-lookup"><span data-stu-id="150f1-128">Make sure that all Azure Reserved Virtual Machine Instances and software purchase orders for that customer are cancelled.</span></span> <span data-ttu-id="150f1-129">För varje [**rättighet**](entitlement-resources.md) i samlingen:</span><span class="sxs-lookup"><span data-stu-id="150f1-129">For each [**Entitlement**](entitlement-resources.md) in the collection:</span></span>

    1. <span data-ttu-id="150f1-130">Använd [**rättigheten. ReferenceOrder.Id**](entitlement-resources.md#referenceorder) för att få en lokal kopia av motsvarande [order](order-resources.md#order) från kundens samling beställningar.</span><span class="sxs-lookup"><span data-stu-id="150f1-130">Use the [**entitlement.ReferenceOrder.Id**](entitlement-resources.md#referenceorder) to get a local copy of the corresponding [Order](order-resources.md#order) from the customer's collection of orders.</span></span>

    2. <span data-ttu-id="150f1-131">Ange egenskapen [**order. status**](order-resources.md#order) till "avbruten".</span><span class="sxs-lookup"><span data-stu-id="150f1-131">Set the [**Order.Status**](order-resources.md#order) property to "Cancelled".</span></span>

    3. <span data-ttu-id="150f1-132">Använd metoden **patch ()** för att uppdatera ordningen.</span><span class="sxs-lookup"><span data-stu-id="150f1-132">Use the **Patch()** method to update the order.</span></span>

4. <span data-ttu-id="150f1-133">Avbryt alla beställningar.</span><span class="sxs-lookup"><span data-stu-id="150f1-133">Cancel all orders.</span></span> <span data-ttu-id="150f1-134">Exempel: följande kod exempel använder en slinga för att avsöka varje order tills dess status är "avbruten".</span><span class="sxs-lookup"><span data-stu-id="150f1-134">For example, the following code sample uses a loop to poll each order until its status is "Cancelled".</span></span>

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

5. <span data-ttu-id="150f1-135">Se till att alla beställningar avbryts genom att anropa **Delete** -metoden för kunden.</span><span class="sxs-lookup"><span data-stu-id="150f1-135">Make sure all orders are cancelled by calling the **Delete** method for the customer.</span></span>

<span data-ttu-id="150f1-136">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="150f1-136">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="150f1-137">**Projekt**: Partner Center PartnerCenterSDK. FeaturesSamples- **klass**: DeleteCustomerFromTipAccount.CS</span><span class="sxs-lookup"><span data-stu-id="150f1-137">**Project**: Partner Center PartnerCenterSDK.FeaturesSamples **Class**: DeleteCustomerFromTipAccount.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="150f1-138">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="150f1-138">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="150f1-139">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="150f1-139">Request syntax</span></span>

| <span data-ttu-id="150f1-140">Metod</span><span class="sxs-lookup"><span data-stu-id="150f1-140">Method</span></span>     | <span data-ttu-id="150f1-141">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="150f1-141">Request URI</span></span>                                                                            |
|------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="150f1-142">DELETE</span><span class="sxs-lookup"><span data-stu-id="150f1-142">DELETE</span></span>     | <span data-ttu-id="150f1-143">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="150f1-143">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="150f1-144">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="150f1-144">URI parameter</span></span>

<span data-ttu-id="150f1-145">Använd följande frågeparameter för att ta bort en kund.</span><span class="sxs-lookup"><span data-stu-id="150f1-145">Use the following query parameter to delete a customer.</span></span>

| <span data-ttu-id="150f1-146">Namn</span><span class="sxs-lookup"><span data-stu-id="150f1-146">Name</span></span>                   | <span data-ttu-id="150f1-147">Typ</span><span class="sxs-lookup"><span data-stu-id="150f1-147">Type</span></span>     | <span data-ttu-id="150f1-148">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="150f1-148">Required</span></span> | <span data-ttu-id="150f1-149">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="150f1-149">Description</span></span>                                                                         |
|------------------------|----------|----------|-------------------------------------------------------------------------------------|
| <span data-ttu-id="150f1-150">kund-ID för klient organisation</span><span class="sxs-lookup"><span data-stu-id="150f1-150">customer-tenant-id</span></span>     | <span data-ttu-id="150f1-151">GUID</span><span class="sxs-lookup"><span data-stu-id="150f1-151">GUID</span></span>     | <span data-ttu-id="150f1-152">Y</span><span class="sxs-lookup"><span data-stu-id="150f1-152">Y</span></span>        | <span data-ttu-id="150f1-153">Värdet är ett GUID-formaterat **kund-Tenant-ID** som gör det möjligt för åter försäljaren att filtrera resultaten för en specifik kund som tillhör åter försäljaren.</span><span class="sxs-lookup"><span data-stu-id="150f1-153">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="150f1-154">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="150f1-154">Request headers</span></span>

<span data-ttu-id="150f1-155">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="150f1-155">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="150f1-156">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="150f1-156">Request body</span></span>

<span data-ttu-id="150f1-157">Inga.</span><span class="sxs-lookup"><span data-stu-id="150f1-157">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="150f1-158">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="150f1-158">Request example</span></span>

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="150f1-159">REST-svar</span><span class="sxs-lookup"><span data-stu-id="150f1-159">REST response</span></span>

<span data-ttu-id="150f1-160">Om det lyckas returnerar den här metoden ett tomt svar.</span><span class="sxs-lookup"><span data-stu-id="150f1-160">If successful, this method returns an empty response.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="150f1-161">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="150f1-161">Response success and error codes</span></span>

<span data-ttu-id="150f1-162">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="150f1-162">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="150f1-163">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="150f1-163">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="150f1-164">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="150f1-164">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="150f1-165">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="150f1-165">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
Date: Wed, 16 Mar 2016 00:43:02 GMT
```
