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
# <a name="delete-a-customer-account-from-the-integration-sandbox"></a><span data-ttu-id="fa02d-103">Ta bort ett kundkonto från sandbox-miljön för integrering</span><span class="sxs-lookup"><span data-stu-id="fa02d-103">Delete a customer account from the integration sandbox</span></span>

<span data-ttu-id="fa02d-104">**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="fa02d-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="fa02d-105">Den här artikeln förklarar hur du bryter relationen mellan partnern och kundkontot och återfår kvoten för sandbox Testing in Production integrering (tips).</span><span class="sxs-lookup"><span data-stu-id="fa02d-105">This article explains, how to break the relationship between the partner and the customer account and regain the quota for Testing in Production (Tip) integration sandbox.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fa02d-106">När du tar bort ett kundkonto rensas alla resurser som är associerade med kundklientorganisationen.</span><span class="sxs-lookup"><span data-stu-id="fa02d-106">When you delete a customer account, all resources associated with that customer tenant will be purged.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fa02d-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="fa02d-107">Prerequisites</span></span>

- <span data-ttu-id="fa02d-108">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="fa02d-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="fa02d-109">Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="fa02d-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="fa02d-110">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fa02d-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="fa02d-111">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="fa02d-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="fa02d-112">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="fa02d-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="fa02d-113">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="fa02d-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="fa02d-114">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="fa02d-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="fa02d-115">Microsoft-ID:t är samma som kund-ID :t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fa02d-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="fa02d-116">Alla Azure Reserved Virtual Machine Instances och programvaruköpordrar måste avbrytas innan du tar bort en kund från sandbox-miljön för Tipsintegrering.</span><span class="sxs-lookup"><span data-stu-id="fa02d-116">All Azure Reserved Virtual Machine Instances and software purchase orders must be canceled before deleting a customer from the Tip integration sandbox.</span></span>

## <a name="c"></a><span data-ttu-id="fa02d-117">C\#</span><span class="sxs-lookup"><span data-stu-id="fa02d-117">C\#</span></span>

<span data-ttu-id="fa02d-118">Så här tar du bort en kund från sandbox-miljön för tipsintegrering:</span><span class="sxs-lookup"><span data-stu-id="fa02d-118">To delete a customer from the Tip integration sandbox:</span></span>

1. <span data-ttu-id="fa02d-119">Skicka autentiseringsuppgifterna för ditt tipskonto [**till metoden CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) för att hämta [**ett IPartner-gränssnitt**](/dotnet/api/microsoft.store.partnercenter.ipartner) till partneråtgärder.</span><span class="sxs-lookup"><span data-stu-id="fa02d-119">Pass your Tip account credentials to the [**CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) method to get an [**IPartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) interface to partner operations.</span></span>

2. <span data-ttu-id="fa02d-120">Använd gränssnittet för partneråtgärder för att hämta samlingen med rättigheter:</span><span class="sxs-lookup"><span data-stu-id="fa02d-120">Use the partner operations interface to retrieve the collection of entitlements:</span></span>

    1. <span data-ttu-id="fa02d-121">Anropa metoden [**Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kundidentifieraren för att ange kunden.</span><span class="sxs-lookup"><span data-stu-id="fa02d-121">Call the [**Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to specify the customer.</span></span>

    2. <span data-ttu-id="fa02d-122">Anropa egenskapen **Berättiganden.**</span><span class="sxs-lookup"><span data-stu-id="fa02d-122">Call the **Entitlements** property.</span></span>

    3. <span data-ttu-id="fa02d-123">Anropa metoden **Get** eller **GetAsync** för att hämta [**berättigandesamlingen.**](entitlement-resources.md)</span><span class="sxs-lookup"><span data-stu-id="fa02d-123">Call the **Get** or **GetAsync** method to retrieve the [**Entitlement**](entitlement-resources.md) collection.</span></span>

3. <span data-ttu-id="fa02d-124">Se till att alla Azure Reserved Virtual Machine Instances och programvaruköpsorder för den kunden annulleras.</span><span class="sxs-lookup"><span data-stu-id="fa02d-124">Make sure that all Azure Reserved Virtual Machine Instances and software purchase orders for that customer are canceled.</span></span> <span data-ttu-id="fa02d-125">För varje [**berättigande**](entitlement-resources.md) i samlingen:</span><span class="sxs-lookup"><span data-stu-id="fa02d-125">For each [**Entitlement**](entitlement-resources.md) in the collection:</span></span>

    1. <span data-ttu-id="fa02d-126">Använd [**rättigheten. ReferenceOrder.Id**](entitlement-resources.md#referenceorder) hämta en lokal kopia av [motsvarande Order](order-resources.md#order) från kundens ordersamling.</span><span class="sxs-lookup"><span data-stu-id="fa02d-126">Use the [**entitlement.ReferenceOrder.Id**](entitlement-resources.md#referenceorder) to get a local copy of the corresponding [Order](order-resources.md#order) from the customer's collection of orders.</span></span>

    2. <span data-ttu-id="fa02d-127">Ange egenskapen [**Order.Status**](order-resources.md#order) till "Cancelled" (Avbruten).</span><span class="sxs-lookup"><span data-stu-id="fa02d-127">Set the [**Order.Status**](order-resources.md#order) property to "Cancelled".</span></span>

    3. <span data-ttu-id="fa02d-128">Använd **metoden Patch()** för att uppdatera ordningen.</span><span class="sxs-lookup"><span data-stu-id="fa02d-128">Use the **Patch()** method to update the order.</span></span>

4. <span data-ttu-id="fa02d-129">Avbryt alla beställningar.</span><span class="sxs-lookup"><span data-stu-id="fa02d-129">Cancel all orders.</span></span> <span data-ttu-id="fa02d-130">Följande kodexempel använder till exempel en loop för att avssöka varje order tills dess status är "Cancelled".</span><span class="sxs-lookup"><span data-stu-id="fa02d-130">For example, the following code sample uses a loop to poll each order until its status is "Cancelled".</span></span>

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

5. <span data-ttu-id="fa02d-131">Kontrollera att alla beställningar annulleras genom att anropa **delete-metoden** för kunden.</span><span class="sxs-lookup"><span data-stu-id="fa02d-131">Make sure all orders are canceled by calling the **Delete** method for the customer.</span></span>

<span data-ttu-id="fa02d-132">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="fa02d-132">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="fa02d-133">**Project:** Partner Center PartnerCenterSDK.FeaturesSamples-klass: DeleteCustomerFromTipAccount.cs </span><span class="sxs-lookup"><span data-stu-id="fa02d-133">**Project**: Partner Center PartnerCenterSDK.FeaturesSamples **Class**: DeleteCustomerFromTipAccount.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="fa02d-134">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="fa02d-134">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="fa02d-135">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="fa02d-135">Request syntax</span></span>

| <span data-ttu-id="fa02d-136">Metod</span><span class="sxs-lookup"><span data-stu-id="fa02d-136">Method</span></span>     | <span data-ttu-id="fa02d-137">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="fa02d-137">Request URI</span></span>                                                                            |
|------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="fa02d-138">DELETE</span><span class="sxs-lookup"><span data-stu-id="fa02d-138">DELETE</span></span>     | <span data-ttu-id="fa02d-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="fa02d-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="fa02d-140">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="fa02d-140">URI parameter</span></span>

<span data-ttu-id="fa02d-141">Använd följande frågeparameter för att ta bort en kund.</span><span class="sxs-lookup"><span data-stu-id="fa02d-141">Use the following query parameter to delete a customer.</span></span>

| <span data-ttu-id="fa02d-142">Namn</span><span class="sxs-lookup"><span data-stu-id="fa02d-142">Name</span></span>                   | <span data-ttu-id="fa02d-143">Typ</span><span class="sxs-lookup"><span data-stu-id="fa02d-143">Type</span></span>     | <span data-ttu-id="fa02d-144">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="fa02d-144">Required</span></span> | <span data-ttu-id="fa02d-145">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="fa02d-145">Description</span></span>                                                                         |
|------------------------|----------|----------|-------------------------------------------------------------------------------------|
| <span data-ttu-id="fa02d-146">kund-klient-id</span><span class="sxs-lookup"><span data-stu-id="fa02d-146">customer-tenant-id</span></span>     | <span data-ttu-id="fa02d-147">GUID</span><span class="sxs-lookup"><span data-stu-id="fa02d-147">GUID</span></span>     | <span data-ttu-id="fa02d-148">Y</span><span class="sxs-lookup"><span data-stu-id="fa02d-148">Y</span></span>        | <span data-ttu-id="fa02d-149">Värdet är ett GUID-formaterat **kundklient-ID** som gör att återförsäljaren kan filtrera resultaten för en viss kund som tillhör återförsäljaren.</span><span class="sxs-lookup"><span data-stu-id="fa02d-149">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="fa02d-150">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="fa02d-150">Request headers</span></span>

<span data-ttu-id="fa02d-151">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="fa02d-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="fa02d-152">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="fa02d-152">Request body</span></span>

<span data-ttu-id="fa02d-153">Inga.</span><span class="sxs-lookup"><span data-stu-id="fa02d-153">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="fa02d-154">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="fa02d-154">Request example</span></span>

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="fa02d-155">REST-svar</span><span class="sxs-lookup"><span data-stu-id="fa02d-155">REST response</span></span>

<span data-ttu-id="fa02d-156">Om det lyckas returnerar den här metoden ett tomt svar.</span><span class="sxs-lookup"><span data-stu-id="fa02d-156">If successful, this method returns an empty response.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="fa02d-157">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="fa02d-157">Response success and error codes</span></span>

<span data-ttu-id="fa02d-158">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="fa02d-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="fa02d-159">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="fa02d-159">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="fa02d-160">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="fa02d-160">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="fa02d-161">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="fa02d-161">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
Date: Wed, 16 Mar 2016 00:43:02 GMT
```
