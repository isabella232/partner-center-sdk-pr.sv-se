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
# <a name="convert-a-trial-subscription-to-paid-using-partner-center-apis"></a><span data-ttu-id="cec00-103">Konvertera en utvärderings prenumeration till betald med API: er för partner Center</span><span class="sxs-lookup"><span data-stu-id="cec00-103">Convert a trial subscription to paid using Partner Center APIs</span></span>

<span data-ttu-id="cec00-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="cec00-104">**Applies to:**</span></span>

- <span data-ttu-id="cec00-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="cec00-105">Partner Center</span></span>

<span data-ttu-id="cec00-106">Du kan konvertera en utvärderings prenumeration till betald.</span><span class="sxs-lookup"><span data-stu-id="cec00-106">You can convert a trial subscription to paid.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cec00-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="cec00-107">Prerequisites</span></span>

- <span data-ttu-id="cec00-108">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="cec00-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="cec00-109">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="cec00-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="cec00-110">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="cec00-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="cec00-111">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="cec00-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="cec00-112">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="cec00-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="cec00-113">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="cec00-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="cec00-114">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="cec00-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="cec00-115">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="cec00-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="cec00-116">Ett prenumerations-ID för en aktiv utvärderings prenumeration.</span><span class="sxs-lookup"><span data-stu-id="cec00-116">A subscription ID for an active trial subscription.</span></span>

- <span data-ttu-id="cec00-117">Ett tillgängligt konverterings erbjudande.</span><span class="sxs-lookup"><span data-stu-id="cec00-117">An available conversion offer.</span></span>

## <a name="convert-a-trial-subscription-to-paid-through-code"></a><span data-ttu-id="cec00-118">Konvertera en utvärderings prenumeration till betald via kod</span><span class="sxs-lookup"><span data-stu-id="cec00-118">Convert a trial subscription to paid through code</span></span>

<span data-ttu-id="cec00-119">Om du vill konvertera en utvärderings prenumeration till en betald, måste du först skaffa en samling utvärderings versioner som är tillgängliga.</span><span class="sxs-lookup"><span data-stu-id="cec00-119">To convert a trial subscription to a paid one, you must first obtain a collection of the trial conversions available.</span></span> <span data-ttu-id="cec00-120">Sedan måste du välja det konverterings erbjudande som du vill köpa.</span><span class="sxs-lookup"><span data-stu-id="cec00-120">Then, you must choose the conversion offer that you want to purchase.</span></span>

<span data-ttu-id="cec00-121">Konverterings erbjudandet anger en kvantitet som är standard för samma antal licenser som utvärderings prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="cec00-121">The conversion offers will specify a quantity that defaults to the same number of licenses as the trial subscription.</span></span> <span data-ttu-id="cec00-122">Du kan ändra den här kvantiteten genom att ställa in egenskapen [**kvantitet**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion.quantity) på det antal licenser som du vill köpa.</span><span class="sxs-lookup"><span data-stu-id="cec00-122">You can change this quantity by setting the [**Quantity**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion.quantity) property to the number of licenses that you want to purchase.</span></span>

> [!NOTE]
> <span data-ttu-id="cec00-123">Oavsett hur många licenser du har köpt återanvänds prenumerations-ID: t för utvärderings versionen för de köpta licenserna.</span><span class="sxs-lookup"><span data-stu-id="cec00-123">Regardless of the number of licenses purchased, the subscription ID of the trial is reused for the purchased licenses.</span></span> <span data-ttu-id="cec00-124">På grund av detta försvinner utvärderings versionen och ersätts av köpet.</span><span class="sxs-lookup"><span data-stu-id="cec00-124">As a result, the trial in effect disappears and is replaced by the purchase.</span></span>

<span data-ttu-id="cec00-125">Använd följande steg för att konvertera en utvärderings prenumeration via kod:</span><span class="sxs-lookup"><span data-stu-id="cec00-125">Use the following steps to convert a trial subscription through code:</span></span>

1. <span data-ttu-id="cec00-126">Hämta ett gränssnitt till tillgängliga prenumerations åtgärder.</span><span class="sxs-lookup"><span data-stu-id="cec00-126">Get an interface to the subscription operations available.</span></span> <span data-ttu-id="cec00-127">Du måste identifiera kunden och ange prenumerations-ID för utvärderings prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="cec00-127">You must identify the customer and specify the subscription identifier of the trial subscription.</span></span>

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2. <span data-ttu-id="cec00-128">Hämta en samling av de tillgängliga konverterings erbjudandena.</span><span class="sxs-lookup"><span data-stu-id="cec00-128">Get a collection of the available conversion offers.</span></span> <span data-ttu-id="cec00-129">Mer information och information om begäran/svar för den här metoden finns i [Hämta en lista över erbjudanden om utvärderings konvertering](get-a-list-of-trial-conversion-offers.md).</span><span class="sxs-lookup"><span data-stu-id="cec00-129">For more information and details on the request/response for this method, see [Get a list of trial conversion offers](get-a-list-of-trial-conversion-offers.md).</span></span>

    ``` csharp
    var conversions = subscriptionOperations.Conversions.Get();
    ```

3. <span data-ttu-id="cec00-130">Välj ett konverterings erbjudande.</span><span class="sxs-lookup"><span data-stu-id="cec00-130">Choose a conversion offer.</span></span> <span data-ttu-id="cec00-131">Följande kod väljer det första konverterings erbjudandet i samlingen.</span><span class="sxs-lookup"><span data-stu-id="cec00-131">The following code chooses the first conversion offer in the collection.</span></span>

    ``` csharp
    var selectedConversion = conversions.Items.ToList()[0];
    ```

4. <span data-ttu-id="cec00-132">Alternativt kan du ange antalet licenser som ska köpas.</span><span class="sxs-lookup"><span data-stu-id="cec00-132">Optionally, specify the number of licenses to purchase.</span></span> <span data-ttu-id="cec00-133">Standardvärdet är antalet licenser i utvärderings prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="cec00-133">The default is the number of licenses in the trial subscription.</span></span>

    ``` csharp
    selectedConversion.Quantity = 10;
    ```

5. <span data-ttu-id="cec00-134">Anropa metoden [**create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) eller [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) för att konvertera utvärderings prenumerationen till betald.</span><span class="sxs-lookup"><span data-stu-id="cec00-134">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) method to convert the trial subscription to paid.</span></span>

    ``` csharp
    var convertResult = subscriptionOperations.Conversions.Create(selectedConversion);
    ```

## <a name="c"></a><span data-ttu-id="cec00-135">C\#</span><span class="sxs-lookup"><span data-stu-id="cec00-135">C\#</span></span>

<span data-ttu-id="cec00-136">Så här konverterar du en utvärderings prenumeration till en betald:</span><span class="sxs-lookup"><span data-stu-id="cec00-136">To convert a trial subscription to a paid one:</span></span>

1. <span data-ttu-id="cec00-137">Använd metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="cec00-137">Use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="cec00-138">Hämta ett gränssnitt för prenumerations åtgärder genom att anropa metoden [**Subscriptions. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) med utvärderings prenumerationens ID.</span><span class="sxs-lookup"><span data-stu-id="cec00-138">Get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the trial subscription ID.</span></span> <span data-ttu-id="cec00-139">Spara en referens till prenumerations åtgärds gränssnittet i en lokal variabel.</span><span class="sxs-lookup"><span data-stu-id="cec00-139">Save a reference to the subscription operations interface in a local variable.</span></span>

3. <span data-ttu-id="cec00-140">Använd egenskapen [**konverteringar**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) för att hämta ett gränssnitt till de tillgängliga åtgärderna för konverteringar och anropa sedan metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) för att hämta en samling tillgängliga [**konverterings**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) erbjudanden.</span><span class="sxs-lookup"><span data-stu-id="cec00-140">Use the [**Conversions**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) property to obtain an interface to the available operations on conversions, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) method to retrieve a collection of available [**Conversion**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) offers.</span></span> <span data-ttu-id="cec00-141">Du måste välja ett.</span><span class="sxs-lookup"><span data-stu-id="cec00-141">You must choose one.</span></span> <span data-ttu-id="cec00-142">I följande exempel är standard den första konverteringen tillgänglig.</span><span class="sxs-lookup"><span data-stu-id="cec00-142">The following example defaults to the first conversion available.</span></span>

4. <span data-ttu-id="cec00-143">Använd referensen till det prenumerations åtgärds gränssnitt som du sparade i en lokal variabel och egenskapen [**konverteringar**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) för att hämta ett gränssnitt till de tillgängliga åtgärderna för konverteringar.</span><span class="sxs-lookup"><span data-stu-id="cec00-143">Use the reference to the subscription operations interface that you saved in a local variable and the [**Conversions**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) property to obtain an interface to the available operations on conversions.</span></span>

5. <span data-ttu-id="cec00-144">Överför det valda konverterings erbjudande objektet till metoden [**create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) eller [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) för att försöka utföra utvärderings konverteringen.</span><span class="sxs-lookup"><span data-stu-id="cec00-144">Pass the selected conversion offer object to the [**Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) method to attempt the trial conversion.</span></span>

### <a name="c-example"></a><span data-ttu-id="cec00-145">C- \# exempel</span><span class="sxs-lookup"><span data-stu-id="cec00-145">C\# example</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="cec00-146">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="cec00-146">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="cec00-147">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="cec00-147">Request syntax</span></span>

| <span data-ttu-id="cec00-148">Metod</span><span class="sxs-lookup"><span data-stu-id="cec00-148">Method</span></span>   | <span data-ttu-id="cec00-149">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="cec00-149">Request URI</span></span>                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="cec00-150">**EFTER**</span><span class="sxs-lookup"><span data-stu-id="cec00-150">**POST**</span></span> | <span data-ttu-id="cec00-151">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Subscriptions/{Subscription-ID}/conversions http/1.1</span><span class="sxs-lookup"><span data-stu-id="cec00-151">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="cec00-152">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="cec00-152">URI parameter</span></span>

<span data-ttu-id="cec00-153">Använd följande Sök vägs parametrar för att identifiera kunden och utvärderings prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="cec00-153">Use the following path parameters to identify the customer and trial subscription.</span></span>

| <span data-ttu-id="cec00-154">Namn</span><span class="sxs-lookup"><span data-stu-id="cec00-154">Name</span></span>            | <span data-ttu-id="cec00-155">Typ</span><span class="sxs-lookup"><span data-stu-id="cec00-155">Type</span></span>   | <span data-ttu-id="cec00-156">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="cec00-156">Required</span></span> | <span data-ttu-id="cec00-157">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="cec00-157">Description</span></span>                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="cec00-158">kund-ID</span><span class="sxs-lookup"><span data-stu-id="cec00-158">customer-id</span></span>     | <span data-ttu-id="cec00-159">sträng</span><span class="sxs-lookup"><span data-stu-id="cec00-159">string</span></span> | <span data-ttu-id="cec00-160">Yes</span><span class="sxs-lookup"><span data-stu-id="cec00-160">Yes</span></span>      | <span data-ttu-id="cec00-161">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="cec00-161">A GUID formatted string that identifies the customer.</span></span>           |
| <span data-ttu-id="cec00-162">prenumerations-ID</span><span class="sxs-lookup"><span data-stu-id="cec00-162">subscription-id</span></span> | <span data-ttu-id="cec00-163">sträng</span><span class="sxs-lookup"><span data-stu-id="cec00-163">string</span></span> | <span data-ttu-id="cec00-164">Yes</span><span class="sxs-lookup"><span data-stu-id="cec00-164">Yes</span></span>      | <span data-ttu-id="cec00-165">En GUID-formaterad sträng som identifierar utvärderings prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="cec00-165">A GUID formatted string that identifies the trial subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="cec00-166">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="cec00-166">Request headers</span></span>

<span data-ttu-id="cec00-167">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="cec00-167">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="cec00-168">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="cec00-168">Request body</span></span>

<span data-ttu-id="cec00-169">En ifylld [konverterings](conversions-resources.md#conversion) resurs måste ingå i begär ande texten.</span><span class="sxs-lookup"><span data-stu-id="cec00-169">A populated [Conversion](conversions-resources.md#conversion) resource must be included in the request body.</span></span>

### <a name="request-example"></a><span data-ttu-id="cec00-170">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="cec00-170">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="cec00-171">REST-svar</span><span class="sxs-lookup"><span data-stu-id="cec00-171">REST response</span></span>

<span data-ttu-id="cec00-172">Om det lyckas innehåller svars texten en [ConversionResult](conversions-resources.md#conversionresult) -resurs.</span><span class="sxs-lookup"><span data-stu-id="cec00-172">If successful, the response body contains a [ConversionResult](conversions-resources.md#conversionresult) resource.</span></span>

#### <a name="response-success-and-error-codes"></a><span data-ttu-id="cec00-173">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="cec00-173">Response success and error codes</span></span>

<span data-ttu-id="cec00-174">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="cec00-174">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="cec00-175">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="cec00-175">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="cec00-176">En fullständig lista finns i [fel koder för partner Center](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="cec00-176">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

#### <a name="response-example"></a><span data-ttu-id="cec00-177">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="cec00-177">Response example</span></span>

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
