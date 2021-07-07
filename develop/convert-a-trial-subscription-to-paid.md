---
title: Konvertera en utvärderingsprenumeration till betald
description: Lär dig hur du använder Partner Center-API:er för att konvertera en utvärderingsprenumeration till en betald prenumeration.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c1876cfc796b683bfff00b7d137bcfe0b7162c78
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973867"
---
# <a name="convert-a-trial-subscription-to-paid-using-partner-center-apis"></a><span data-ttu-id="401f9-103">Konvertera en utvärderingsprenumeration till betald med partnercenter-API:er</span><span class="sxs-lookup"><span data-stu-id="401f9-103">Convert a trial subscription to paid using Partner Center APIs</span></span>

<span data-ttu-id="401f9-104">Du kan konvertera en utvärderingsprenumeration till betald.</span><span class="sxs-lookup"><span data-stu-id="401f9-104">You can convert a trial subscription to paid.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="401f9-105">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="401f9-105">Prerequisites</span></span>

- <span data-ttu-id="401f9-106">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="401f9-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="401f9-107">Det här scenariot har endast stöd för autentisering med app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="401f9-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="401f9-108">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="401f9-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="401f9-109">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="401f9-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="401f9-110">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="401f9-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="401f9-111">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="401f9-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="401f9-112">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="401f9-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="401f9-113">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="401f9-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="401f9-114">Ett prenumerations-ID för en aktiv utvärderingsprenumeration.</span><span class="sxs-lookup"><span data-stu-id="401f9-114">A subscription ID for an active trial subscription.</span></span>

- <span data-ttu-id="401f9-115">Ett tillgängligt konverteringserbjudande.</span><span class="sxs-lookup"><span data-stu-id="401f9-115">An available conversion offer.</span></span>

## <a name="convert-a-trial-subscription-to-a-paid-subscription-through-code"></a><span data-ttu-id="401f9-116">Konvertera en utvärderingsprenumeration till en betald prenumeration via kod</span><span class="sxs-lookup"><span data-stu-id="401f9-116">Convert a trial subscription to a paid subscription through code</span></span>

<span data-ttu-id="401f9-117">Om du vill konvertera en utvärderingsprenumeration till en betald prenumeration måste du först skaffa en samling med tillgängliga utvärderingskonverteringar.</span><span class="sxs-lookup"><span data-stu-id="401f9-117">To convert a trial subscription to a paid one, you must first obtain a collection of the trial conversions available.</span></span> <span data-ttu-id="401f9-118">Sedan måste du välja det konverteringserbjudande som du vill köpa.</span><span class="sxs-lookup"><span data-stu-id="401f9-118">Then, you must choose the conversion offer that you want to purchase.</span></span>

<span data-ttu-id="401f9-119">Konverteringserbjudandena anger en kvantitet som har samma antal licenser som utvärderingsprenumerationen som standard.</span><span class="sxs-lookup"><span data-stu-id="401f9-119">The conversion offers will specify a quantity that defaults to the same number of licenses as the trial subscription.</span></span> <span data-ttu-id="401f9-120">Du kan ändra den här kvantiteten genom [**att**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion.quantity) ange egenskapen Quantity till det antal licenser som du vill köpa.</span><span class="sxs-lookup"><span data-stu-id="401f9-120">You can change this quantity by setting the [**Quantity**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion.quantity) property to the number of licenses that you want to purchase.</span></span>

> [!NOTE]
> <span data-ttu-id="401f9-121">Oavsett hur många licenser som köpts återanvänds prenumerations-ID:t för utvärderingsversionen för de köpta licenserna.</span><span class="sxs-lookup"><span data-stu-id="401f9-121">Regardless of the number of licenses purchased, the subscription ID of the trial is reused for the purchased licenses.</span></span> <span data-ttu-id="401f9-122">Därför försvinner den utvärderingsversion som används och ersätts av köpet.</span><span class="sxs-lookup"><span data-stu-id="401f9-122">As a result, the trial in effect disappears and is replaced by the purchase.</span></span>

<span data-ttu-id="401f9-123">Använd följande steg för att konvertera en utvärderingsprenumeration via kod:</span><span class="sxs-lookup"><span data-stu-id="401f9-123">Use the following steps to convert a trial subscription through code:</span></span>

1. <span data-ttu-id="401f9-124">Hämta ett gränssnitt för de prenumerationsåtgärder som är tillgängliga.</span><span class="sxs-lookup"><span data-stu-id="401f9-124">Get an interface to the subscription operations available.</span></span> <span data-ttu-id="401f9-125">Du måste identifiera kunden och ange prenumerations-ID för utvärderingsprenumerationen.</span><span class="sxs-lookup"><span data-stu-id="401f9-125">You must identify the customer and specify the subscription identifier of the trial subscription.</span></span>

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2. <span data-ttu-id="401f9-126">Hämta en samling med tillgängliga konverteringserbjudanden.</span><span class="sxs-lookup"><span data-stu-id="401f9-126">Get a collection of the available conversion offers.</span></span> <span data-ttu-id="401f9-127">Mer information om begäran/svar för den här metoden finns i Hämta en [lista över utvärderingsversionserbjudanden.](get-a-list-of-trial-conversion-offers.md)</span><span class="sxs-lookup"><span data-stu-id="401f9-127">For more information and details on the request/response for this method, see [Get a list of trial conversion offers](get-a-list-of-trial-conversion-offers.md).</span></span>

    ``` csharp
    var conversions = subscriptionOperations.Conversions.Get();
    ```

3. <span data-ttu-id="401f9-128">Välj ett konverteringserbjudande.</span><span class="sxs-lookup"><span data-stu-id="401f9-128">Choose a conversion offer.</span></span> <span data-ttu-id="401f9-129">Följande kod väljer det första konverteringserbjudandet i samlingen.</span><span class="sxs-lookup"><span data-stu-id="401f9-129">The following code chooses the first conversion offer in the collection.</span></span>

    ``` csharp
    var selectedConversion = conversions.Items.ToList()[0];
    ```

4. <span data-ttu-id="401f9-130">Du kan också ange antalet licenser som ska köpas.</span><span class="sxs-lookup"><span data-stu-id="401f9-130">Optionally, specify the number of licenses to purchase.</span></span> <span data-ttu-id="401f9-131">Standardvärdet är antalet licenser i utvärderingsprenumerationen.</span><span class="sxs-lookup"><span data-stu-id="401f9-131">The default is the number of licenses in the trial subscription.</span></span>

    ``` csharp
    selectedConversion.Quantity = 10;
    ```

5. <span data-ttu-id="401f9-132">Anropa metoden [**Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) eller [**CreateAsync för**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) att konvertera utvärderingsprenumerationen till betald.</span><span class="sxs-lookup"><span data-stu-id="401f9-132">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) method to convert the trial subscription to paid.</span></span>

    ``` csharp
    var convertResult = subscriptionOperations.Conversions.Create(selectedConversion);
    ```

## <a name="c"></a><span data-ttu-id="401f9-133">C\#</span><span class="sxs-lookup"><span data-stu-id="401f9-133">C\#</span></span>

<span data-ttu-id="401f9-134">Så här konverterar du en utvärderingsprenumeration till en betald prenumeration:</span><span class="sxs-lookup"><span data-stu-id="401f9-134">To convert a trial subscription to a paid one:</span></span>

1. <span data-ttu-id="401f9-135">Använd metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="401f9-135">Use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="401f9-136">Hämta ett gränssnitt för prenumerationsåtgärder genom att anropa [**metoden Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) med utvärderingsprenumerationens ID.</span><span class="sxs-lookup"><span data-stu-id="401f9-136">Get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the trial subscription ID.</span></span> <span data-ttu-id="401f9-137">Spara en referens till gränssnittet för prenumerationsåtgärder i en lokal variabel.</span><span class="sxs-lookup"><span data-stu-id="401f9-137">Save a reference to the subscription operations interface in a local variable.</span></span>

3. <span data-ttu-id="401f9-138">Använd egenskapen [**Konverteringar**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) för att hämta ett gränssnitt till de tillgängliga åtgärderna för konverteringar och anropa sedan metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) för att hämta en samling tillgängliga [**konverteringserbjudanden.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion)</span><span class="sxs-lookup"><span data-stu-id="401f9-138">Use the [**Conversions**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) property to obtain an interface to the available operations on conversions, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) method to retrieve a collection of available [**Conversion**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) offers.</span></span> <span data-ttu-id="401f9-139">Du måste välja en.</span><span class="sxs-lookup"><span data-stu-id="401f9-139">You must choose one.</span></span> <span data-ttu-id="401f9-140">I följande exempel används som standard den första tillgängliga konverteringen.</span><span class="sxs-lookup"><span data-stu-id="401f9-140">The following example defaults to the first conversion available.</span></span>

4. <span data-ttu-id="401f9-141">Använd referensen till det gränssnitt för prenumerationsåtgärder som du sparade i en lokal variabel och egenskapen [**Konverteringar**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) för att hämta ett gränssnitt för de tillgängliga åtgärderna vid konverteringar.</span><span class="sxs-lookup"><span data-stu-id="401f9-141">Use the reference to the subscription operations interface that you saved in a local variable and the [**Conversions**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) property to obtain an interface to the available operations on conversions.</span></span>

5. <span data-ttu-id="401f9-142">Skicka det valda konverteringserbjudandet till metoden [**Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) eller [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) för att försöka konvertera utvärderingsversionen.</span><span class="sxs-lookup"><span data-stu-id="401f9-142">Pass the selected conversion offer object to the [**Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) method to attempt the trial conversion.</span></span>

### <a name="c-example"></a><span data-ttu-id="401f9-143">\#C-exempel</span><span class="sxs-lookup"><span data-stu-id="401f9-143">C\# example</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="401f9-144">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="401f9-144">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="401f9-145">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="401f9-145">Request syntax</span></span>

| <span data-ttu-id="401f9-146">Metod</span><span class="sxs-lookup"><span data-stu-id="401f9-146">Method</span></span>   | <span data-ttu-id="401f9-147">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="401f9-147">Request URI</span></span>                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="401f9-148">**Inlägg**</span><span class="sxs-lookup"><span data-stu-id="401f9-148">**POST**</span></span> | <span data-ttu-id="401f9-149">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="401f9-149">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="401f9-150">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="401f9-150">URI parameter</span></span>

<span data-ttu-id="401f9-151">Använd följande sökvägsparametrar för att identifiera kunden och utvärderingsprenumerationen.</span><span class="sxs-lookup"><span data-stu-id="401f9-151">Use the following path parameters to identify the customer and trial subscription.</span></span>

| <span data-ttu-id="401f9-152">Namn</span><span class="sxs-lookup"><span data-stu-id="401f9-152">Name</span></span>            | <span data-ttu-id="401f9-153">Typ</span><span class="sxs-lookup"><span data-stu-id="401f9-153">Type</span></span>   | <span data-ttu-id="401f9-154">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="401f9-154">Required</span></span> | <span data-ttu-id="401f9-155">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="401f9-155">Description</span></span>                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="401f9-156">kund-ID</span><span class="sxs-lookup"><span data-stu-id="401f9-156">customer-id</span></span>     | <span data-ttu-id="401f9-157">sträng</span><span class="sxs-lookup"><span data-stu-id="401f9-157">string</span></span> | <span data-ttu-id="401f9-158">Ja</span><span class="sxs-lookup"><span data-stu-id="401f9-158">Yes</span></span>      | <span data-ttu-id="401f9-159">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="401f9-159">A GUID formatted string that identifies the customer.</span></span>           |
| <span data-ttu-id="401f9-160">prenumerations-id</span><span class="sxs-lookup"><span data-stu-id="401f9-160">subscription-id</span></span> | <span data-ttu-id="401f9-161">sträng</span><span class="sxs-lookup"><span data-stu-id="401f9-161">string</span></span> | <span data-ttu-id="401f9-162">Ja</span><span class="sxs-lookup"><span data-stu-id="401f9-162">Yes</span></span>      | <span data-ttu-id="401f9-163">En GUID-formaterad sträng som identifierar utvärderingsprenumerationen.</span><span class="sxs-lookup"><span data-stu-id="401f9-163">A GUID formatted string that identifies the trial subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="401f9-164">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="401f9-164">Request headers</span></span>

<span data-ttu-id="401f9-165">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="401f9-165">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="401f9-166">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="401f9-166">Request body</span></span>

<span data-ttu-id="401f9-167">En ifylld [konverteringsresurs](conversions-resources.md#conversion) måste inkluderas i begärandetexten.</span><span class="sxs-lookup"><span data-stu-id="401f9-167">A populated [Conversion](conversions-resources.md#conversion) resource must be included in the request body.</span></span>

### <a name="request-example"></a><span data-ttu-id="401f9-168">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="401f9-168">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="401f9-169">REST-svar</span><span class="sxs-lookup"><span data-stu-id="401f9-169">REST response</span></span>

<span data-ttu-id="401f9-170">Om det lyckas innehåller svarstexten en [ConversionResult-resurs.](conversions-resources.md#conversionresult)</span><span class="sxs-lookup"><span data-stu-id="401f9-170">If successful, the response body contains a [ConversionResult](conversions-resources.md#conversionresult) resource.</span></span>

#### <a name="response-success-and-error-codes"></a><span data-ttu-id="401f9-171">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="401f9-171">Response success and error codes</span></span>

<span data-ttu-id="401f9-172">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="401f9-172">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="401f9-173">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="401f9-173">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="401f9-174">En fullständig lista finns i [Felkoder i Partnercenter.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="401f9-174">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

#### <a name="response-example"></a><span data-ttu-id="401f9-175">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="401f9-175">Response example</span></span>

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
