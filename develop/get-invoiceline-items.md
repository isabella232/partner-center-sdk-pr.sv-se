---
title: Hämta radobjekt för faktura
description: 'Du kan hämta en samling faktura rads objekt (stängt fakturerings rads objekt) för en angiven faktura med hjälp av API: er för partner Center.'
ms.date: 01/27/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ddc49e4d83518b809402a65f990f3e9c2658e64b
ms.sourcegitcommit: 4ec053c56fd210b174fe657aa7b86faf4e2b5a7c
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/29/2021
ms.locfileid: "105730237"
---
# <a name="get-invoice-line-items"></a><span data-ttu-id="25d30-103">Hämta radobjekt för faktura</span><span class="sxs-lookup"><span data-stu-id="25d30-103">Get invoice line items</span></span>

<span data-ttu-id="25d30-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="25d30-104">**Applies to:**</span></span>

- <span data-ttu-id="25d30-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="25d30-105">Partner Center</span></span>
- <span data-ttu-id="25d30-106">Partnercenter drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="25d30-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="25d30-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="25d30-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="25d30-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="25d30-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="25d30-109">Du kan använda följande metoder för att hämta en samlings information för faktura rads objekt (även kallat stängda fakturerings rads objekt) för en viss faktura.</span><span class="sxs-lookup"><span data-stu-id="25d30-109">You can use the following methods to get a collection details for of invoice line items (also known as closed billing line items) for a specified invoice.</span></span>

<span data-ttu-id="25d30-110">*Förutom fel korrigeringar, uppdateras inte detta API längre.*</span><span class="sxs-lookup"><span data-stu-id="25d30-110">*Except for bug fixes, this API is no longer being updated.*</span></span> <span data-ttu-id="25d30-111">Du bör uppdatera dina program för att anropa **Databasmigrering** -API: et i stället för **Marketplace**.</span><span class="sxs-lookup"><span data-stu-id="25d30-111">You should update your applications to call the **onetime** API instead of **marketplace**.</span></span> <span data-ttu-id="25d30-112">**Databasmigrering** -API: et tillhandahåller ytterligare funktioner och kommer även fortsättnings vis att uppdateras.</span><span class="sxs-lookup"><span data-stu-id="25d30-112">The **onetime** API provides additional functionality, and will continue to be updated.</span></span>

<span data-ttu-id="25d30-113">Du bör använda **Databasmigrering** för att fråga alla kommersiella förbruknings poster i stället för **Marketplace**.</span><span class="sxs-lookup"><span data-stu-id="25d30-113">You should use **onetime** to query all commercial consumption line items instead of **marketplace**.</span></span> <span data-ttu-id="25d30-114">Du kan också följa länkarna i anropet för att beräkna länkar.</span><span class="sxs-lookup"><span data-stu-id="25d30-114">Or, you can follow the links in the estimate links call.</span></span>

<span data-ttu-id="25d30-115">Detta API stöder även **leverantörs** typerna av **Azure** och **Office** för Microsoft Azure (MS-AZR-0145P) prenumerationer och Office-erbjudanden, vilket gör API-funktionen bakåtkompatibel.</span><span class="sxs-lookup"><span data-stu-id="25d30-115">This API also supports the **provider** types of **azure** and **office** for Microsoft Azure (MS-AZR-0145P) subscriptions and Office offers, which makes the API feature backward compatible.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="25d30-116">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="25d30-116">Prerequisites</span></span>

- <span data-ttu-id="25d30-117">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="25d30-117">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="25d30-118">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="25d30-118">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="25d30-119">Ett faktura-ID.</span><span class="sxs-lookup"><span data-stu-id="25d30-119">An invoice identifier.</span></span> <span data-ttu-id="25d30-120">Detta identifierar fakturan som rad artiklarna ska hämtas för.</span><span class="sxs-lookup"><span data-stu-id="25d30-120">This identifies the invoice for which to retrieve the line items.</span></span>

## <a name="c"></a><span data-ttu-id="25d30-121">C\#</span><span class="sxs-lookup"><span data-stu-id="25d30-121">C\#</span></span>

<span data-ttu-id="25d30-122">Så här hämtar du rad artiklarna för den angivna fakturan:</span><span class="sxs-lookup"><span data-stu-id="25d30-122">To get the line items for the specified invoice:</span></span>

1. <span data-ttu-id="25d30-123">Anropa [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) -metoden för att hämta ett gränssnitt för att fakturera åtgärder för den angivna fakturan.</span><span class="sxs-lookup"><span data-stu-id="25d30-123">Call the [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) method to get an interface to invoice operations for the specified invoice.</span></span>

2. <span data-ttu-id="25d30-124">Anropa [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) -eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) -metoden för att hämta fakturaprojektet.</span><span class="sxs-lookup"><span data-stu-id="25d30-124">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the invoice object.</span></span> <span data-ttu-id="25d30-125">Fakturaprojektet innehåller all information för den angivna fakturan.</span><span class="sxs-lookup"><span data-stu-id="25d30-125">The invoice object contains all of the information for the specified invoice.</span></span>
3. <span data-ttu-id="25d30-126">Använd faktura objektets [**InvoiceDetails**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoice.invoicedetails) -egenskap för att få åtkomst till en samling av [**InvoiceDetail**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoicedetail) -objekt, som var och en innehåller en [**BillingProvider**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoicedetail.billingprovider) och en [**InvoiceLineItemType**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoicedetail.invoicelineitemtype).</span><span class="sxs-lookup"><span data-stu-id="25d30-126">Use the invoice object's [**InvoiceDetails**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoice.invoicedetails) property to get access to a collection of [**InvoiceDetail**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoicedetail) objects, each of which contains a [**BillingProvider**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoicedetail.billingprovider) and an [**InvoiceLineItemType**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoicedetail.invoicelineitemtype).</span></span> <span data-ttu-id="25d30-127">**BillingProvider** identifierar källan till faktura detalj informationen (till exempel **Office**, **Azure**, **Databasmigrering**) och **InvoiceLineItemType** anger typen (till exempel **BillingLineItem**).</span><span class="sxs-lookup"><span data-stu-id="25d30-127">The **BillingProvider** identifies the source of the invoice detail information (such as **Office**, **Azure**, **OneTime**), and the **InvoiceLineItemType** specifies the type (for example, **BillingLineItem**).</span></span>

<span data-ttu-id="25d30-128">I följande exempel kod används en **förgrunds** slinga för att bearbeta **InvoiceDetails** -samlingen.</span><span class="sxs-lookup"><span data-stu-id="25d30-128">The following example code uses a **foreach** loop to process the **InvoiceDetails** collection.</span></span> <span data-ttu-id="25d30-129">En separat samling av rad objekt hämtas för varje **InvoiceDetail** -instans.</span><span class="sxs-lookup"><span data-stu-id="25d30-129">A separate collection of line items is retrieved for each **InvoiceDetail** instance.</span></span>

<span data-ttu-id="25d30-130">Hämta en samling av rad objekt som motsvarar en **InvoiceDetail** -instans:</span><span class="sxs-lookup"><span data-stu-id="25d30-130">To get a collection of line items that correspond to an **InvoiceDetail** instance:</span></span>

1. <span data-ttu-id="25d30-131">Skicka instansens **BillingProvider** och **InvoiceLineItemType** till [**by**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) -metoden.</span><span class="sxs-lookup"><span data-stu-id="25d30-131">Pass the instance's **BillingProvider** and **InvoiceLineItemType** to the [**By**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) method.</span></span>

2. <span data-ttu-id="25d30-132">Anropa [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicelineitemcollection.get) -eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicelineitemcollection.getasync) -metoden för att hämta de associerade rad objekten.</span><span class="sxs-lookup"><span data-stu-id="25d30-132">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicelineitemcollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicelineitemcollection.getasync) method to retrieve the associated line items.</span></span>
3. <span data-ttu-id="25d30-133">Skapa en uppräknare för att passera samlingen som visas i följande exempel.</span><span class="sxs-lookup"><span data-stu-id="25d30-133">Create an enumerator to traverse the collection as shown in the following example.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// int invoicePageSize;
// string invoiceId;

// Retrieve the invoice.
var invoiceOperations = partnerOperations.Invoices.ById(invoiceId);
var invoice = invoiceOperations.Get();

foreach (var invoiceDetail in invoice.InvoiceDetails)
{
    Console.WriteLine(string.Format("Getting invoice line item for product {0} and line item type {1}",
        invoiceDetail.BillingProvider,
        invoiceDetail.InvoiceLineItemType));

    // Is this an unpaged or paged request?
    bool isUnPaged = (this.invoicePageSize <= 0);

    // If the scenario is unpaged, get all the invoice line items, otherwise get the first page.
    var invoiceLineItemsCollection =
        (isUnPaged)
        ? invoiceOperations.By(invoiceDetail.BillingProvider, invoiceDetail.InvoiceLineItemType).Get()
        : invoiceOperations.By(invoiceDetail.BillingProvider, invoiceDetail.InvoiceLineItemType).Get(this.invoicePageSize, 0);

    // Create an enumerator for traversing the line items collection.
    var invoiceLineItemEnumerator =
        partnerOperations.Enumerators.InvoiceLineItems.Create(invoiceLineItemsCollection);

    while (invoiceLineItemEnumerator.HasValue)
    {
        // invoiceLineItemEnumerator.Current contains a collection
        // of line items.
        Console.WriteLine(String.Format("invoiceLineItemEnumerator.Current has {0} line items.",
            invoiceLineItemEnumerator.Current.TotalCount));
        //
        // Insert code here to work with the line items.
        //
        Console.WriteLine();
        Console.Write("Press any key to retrieve the next invoice line items page");
        Console.ReadKey();

        // Get the next list of invoice line items.
        invoiceLineItemEnumerator.Next();
    }
}
```

<span data-ttu-id="25d30-134">Ett liknande exempel finns i följande avsnitt:</span><span class="sxs-lookup"><span data-stu-id="25d30-134">For a similar example, see the following:</span></span>

- <span data-ttu-id="25d30-135">Exempel: [konsol test app](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="25d30-135">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="25d30-136">Projekt: **SDK-exempel för partner Center**</span><span class="sxs-lookup"><span data-stu-id="25d30-136">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="25d30-137">Klass: **GetInvoiceLineItems. cs**</span><span class="sxs-lookup"><span data-stu-id="25d30-137">Class: **GetInvoiceLineItems.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="25d30-138">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="25d30-138">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="25d30-139">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="25d30-139">Request syntax</span></span>

<span data-ttu-id="25d30-140">Gör din begäran med rätt syntax för fakturerings leverantören i ditt scenario.</span><span class="sxs-lookup"><span data-stu-id="25d30-140">Make your request using the appropriate syntax for the billing provider in your scenario.</span></span>

#### <a name="office"></a><span data-ttu-id="25d30-141">Office</span><span class="sxs-lookup"><span data-stu-id="25d30-141">Office</span></span>

<span data-ttu-id="25d30-142">Följande syntax gäller när fakturerings leverantören är **Office**.</span><span class="sxs-lookup"><span data-stu-id="25d30-142">The following syntax applies when the billing provider is **Office**.</span></span>

| <span data-ttu-id="25d30-143">Metod</span><span class="sxs-lookup"><span data-stu-id="25d30-143">Method</span></span>  | <span data-ttu-id="25d30-144">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="25d30-144">Request URI</span></span>                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="25d30-145">**TA**</span><span class="sxs-lookup"><span data-stu-id="25d30-145">**GET**</span></span> | <span data-ttu-id="25d30-146">[*{baseURL}*](partner-center-rest-urls.md)/v1/INVOICES/{Invoice-ID}/lineitems? Provider = Office&invoicelineitemtype = billinglineitems&storlek = {size} &förskjutning = {offset} http/1.1</span><span class="sxs-lookup"><span data-stu-id="25d30-146">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=office&invoicelineitemtype=billinglineitems&size={size}&offset={offset} HTTP/1.1</span></span>                               |

#### <a name="microsoft-azure-ms-azr-0145p-subscription"></a><span data-ttu-id="25d30-147">Microsoft Azure-prenumeration (MS-AZR-0145P)</span><span class="sxs-lookup"><span data-stu-id="25d30-147">Microsoft Azure (MS-AZR-0145P) subscription</span></span>

<span data-ttu-id="25d30-148">Följande syntax gäller när fakturerings leverantören har en Microsoft Azure-prenumeration (MS-AZR-0145P).</span><span class="sxs-lookup"><span data-stu-id="25d30-148">The following syntaxes apply when the billing provider has a Microsoft Azure (MS-AZR-0145P) subscription.</span></span>

| <span data-ttu-id="25d30-149">Metod</span><span class="sxs-lookup"><span data-stu-id="25d30-149">Method</span></span>  | <span data-ttu-id="25d30-150">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="25d30-150">Request URI</span></span>                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="25d30-151">**TA**</span><span class="sxs-lookup"><span data-stu-id="25d30-151">**GET**</span></span> | <span data-ttu-id="25d30-152">[*{baseURL}*](partner-center-rest-urls.md)/v1/INVOICES/{Invoice-ID}/lineitems? Provider = Azure&invoicelineitemtype = billinglineitems&storlek = {size} &förskjutning = {offset} http/1.1</span><span class="sxs-lookup"><span data-stu-id="25d30-152">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=azure&invoicelineitemtype=billinglineitems&size={size}&offset={offset} HTTP/1.1</span></span>  |
| <span data-ttu-id="25d30-153">**TA**</span><span class="sxs-lookup"><span data-stu-id="25d30-153">**GET**</span></span> | <span data-ttu-id="25d30-154">[*{baseURL}*](partner-center-rest-urls.md)/v1/INVOICES/{Invoice-ID}/lineitems? Provider = Azure&invoicelineitemtype = usagelineitems&storlek = {size} &förskjutning = {offset} http/1.1</span><span class="sxs-lookup"><span data-stu-id="25d30-154">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=azure&invoicelineitemtype=usagelineitems&size={size}&offset={offset} HTTP/1.1</span></span>  |

##### <a name="onetime"></a><span data-ttu-id="25d30-155">Databasmigrering</span><span class="sxs-lookup"><span data-stu-id="25d30-155">OneTime</span></span>

<span data-ttu-id="25d30-156">Följande syntax gäller när fakturerings leverantören är **Databasmigrering**.</span><span class="sxs-lookup"><span data-stu-id="25d30-156">The following syntaxes apply when the billing provider is **OneTime**.</span></span> <span data-ttu-id="25d30-157">Detta omfattar kostnader för Azure-reservationer, program vara, Azure-planer och kommersiella Marketplace-produkter.</span><span class="sxs-lookup"><span data-stu-id="25d30-157">This includes charges for Azure reservations, software, Azure plans, and commercial marketplace products.</span></span>

| <span data-ttu-id="25d30-158">Metod</span><span class="sxs-lookup"><span data-stu-id="25d30-158">Method</span></span>  | <span data-ttu-id="25d30-159">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="25d30-159">Request URI</span></span>                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="25d30-160">**TA**</span><span class="sxs-lookup"><span data-stu-id="25d30-160">**GET**</span></span> | <span data-ttu-id="25d30-161">[*{baseURL}*](partner-center-rest-urls.md)/v1/INVOICES/{Invoice-ID}/lineitems? Provider = Databasmigrering&invoicelineitemtype = billinglineitems&storlek = {size} http/1.1</span><span class="sxs-lookup"><span data-stu-id="25d30-161">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&size={size} HTTP/1.1</span></span>  |
| <span data-ttu-id="25d30-162">**TA**</span><span class="sxs-lookup"><span data-stu-id="25d30-162">**GET**</span></span> | <span data-ttu-id="25d30-163">[*{baseURL}*](partner-center-rest-urls.md)/v1/INVOICES/{Invoice-ID}/lineitems/onetime/billinglineitems&storlek = {size}? SeekOperation = nästa</span><span class="sxs-lookup"><span data-stu-id="25d30-163">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems/onetime/billinglineitems&size={size}?seekOperation=Next</span></span>                           |

#### <a name="previous-syntaxes"></a><span data-ttu-id="25d30-164">Tidigare syntax</span><span class="sxs-lookup"><span data-stu-id="25d30-164">Previous syntaxes</span></span>

<span data-ttu-id="25d30-165">Om du använder följande syntax måste du se till att använda rätt syntax för ditt användnings fall.</span><span class="sxs-lookup"><span data-stu-id="25d30-165">If you are using the following syntaxes, be sure to use the appropriate syntax for your use case.</span></span>

<span data-ttu-id="25d30-166">*Förutom fel korrigeringar, uppdateras inte detta API längre.*</span><span class="sxs-lookup"><span data-stu-id="25d30-166">*Except for bug fixes, this API is no longer being updated.*</span></span> <span data-ttu-id="25d30-167">Du bör uppdatera dina program för att anropa **Databasmigrering** -API: et i stället för **Marketplace**.</span><span class="sxs-lookup"><span data-stu-id="25d30-167">You should update your applications to call the **onetime** API instead of **marketplace**.</span></span> <span data-ttu-id="25d30-168">**Databasmigrering** -API: et tillhandahåller ytterligare funktioner och kommer även fortsättnings vis att uppdateras.</span><span class="sxs-lookup"><span data-stu-id="25d30-168">The **onetime** API provides additional functionality, and will continue to be updated.</span></span>

<span data-ttu-id="25d30-169">Du bör använda **Databasmigrering** för att fråga alla kommersiella förbruknings poster i stället för **Marketplace**.</span><span class="sxs-lookup"><span data-stu-id="25d30-169">You should use **onetime** to query all commercial consumption line items instead of **marketplace**.</span></span> <span data-ttu-id="25d30-170">Du kan också följa länkarna i anropet för att beräkna länkar.</span><span class="sxs-lookup"><span data-stu-id="25d30-170">Or, you can follow the links in the estimate links call.</span></span>

| <span data-ttu-id="25d30-171">Metod</span><span class="sxs-lookup"><span data-stu-id="25d30-171">Method</span></span> | <span data-ttu-id="25d30-172">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="25d30-172">Request URI</span></span> | <span data-ttu-id="25d30-173">Beskrivning av användnings fall för syntax</span><span class="sxs-lookup"><span data-stu-id="25d30-173">Description of syntax use case</span></span> |
| ------ | ----------- | -------------------------------- |
| <span data-ttu-id="25d30-174">GET</span><span class="sxs-lookup"><span data-stu-id="25d30-174">GET</span></span> | <span data-ttu-id="25d30-175">[*{baseURL}*](partner-center-rest-urls.md)/v1/INVOICES/{Invoice-ID}/lineitems/{Billing-Provider}/{invoice-line-item-Type} http/1.1</span><span class="sxs-lookup"><span data-stu-id="25d30-175">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems/{billing-provider}/{invoice-line-item-type} HTTP/1.1</span></span>                              | <span data-ttu-id="25d30-176">Du kan använda den här syntaxen för att returnera en fullständig lista över varje rad objekt för den aktuella fakturan.</span><span class="sxs-lookup"><span data-stu-id="25d30-176">You can use this syntax to return a full list of every line item for the given invoice.</span></span> |
| <span data-ttu-id="25d30-177">GET</span><span class="sxs-lookup"><span data-stu-id="25d30-177">GET</span></span> | <span data-ttu-id="25d30-178">[*{baseURL}*](partner-center-rest-urls.md)/v1/INVOICES/{Invoice-ID}/lineitems/{Billing-Provider}/{invoice-line-item-Type}? size = {size} &förskjutning = {offset} http/1.1</span><span class="sxs-lookup"><span data-stu-id="25d30-178">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems/{billing-provider}/{invoice-line-item-type}?size={size}&offset={offset} HTTP/1.1</span></span>  | <span data-ttu-id="25d30-179">För stora fakturor kan du använda den här syntaxen med en angiven storlek och 0-baserad förskjutning för att returnera en sid lista med rad objekt.</span><span class="sxs-lookup"><span data-stu-id="25d30-179">For large invoices, you can use this syntax with a specified size and 0-based offset to return a paged list of line items.</span></span> |
| <span data-ttu-id="25d30-180">GET</span><span class="sxs-lookup"><span data-stu-id="25d30-180">GET</span></span> | <span data-ttu-id="25d30-181">[*{baseURL}*](partner-center-rest-urls.md)/v1/INVOICES/{Invoice-ID}/lineitems/OneTime/{invoice-line-item-Type}? SeekOperation = Next</span><span class="sxs-lookup"><span data-stu-id="25d30-181">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems/OneTime/{invoice-line-item-type}?seekOperation=Next</span></span>                               | <span data-ttu-id="25d30-182">Du kan använda den här syntaxen för en faktura med ett fakturerings leverantörs värde för **Databasmigrering** och ange **seekOperation** till **Nästa** för att hämta nästa sida med faktura rads objekt.</span><span class="sxs-lookup"><span data-stu-id="25d30-182">You can use this syntax for an invoice with a billing-provider value of **OneTime** and set **seekOperation** to **Next** to get the next page of invoice line items.</span></span> |

##### <a name="uri-parameters"></a><span data-ttu-id="25d30-183">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="25d30-183">URI parameters</span></span>

<span data-ttu-id="25d30-184">Använd följande URI och frågeparametrar när du skapar begäran.</span><span class="sxs-lookup"><span data-stu-id="25d30-184">Use the following URI and query parameters when creating the request.</span></span>

| <span data-ttu-id="25d30-185">Namn</span><span class="sxs-lookup"><span data-stu-id="25d30-185">Name</span></span>                   | <span data-ttu-id="25d30-186">Typ</span><span class="sxs-lookup"><span data-stu-id="25d30-186">Type</span></span>   | <span data-ttu-id="25d30-187">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="25d30-187">Required</span></span> | <span data-ttu-id="25d30-188">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="25d30-188">Description</span></span>                                                       |
|------------------------|--------|----------|-------------------------------------------------------------------|
| <span data-ttu-id="25d30-189">faktura-ID</span><span class="sxs-lookup"><span data-stu-id="25d30-189">invoice-id</span></span>             | <span data-ttu-id="25d30-190">sträng</span><span class="sxs-lookup"><span data-stu-id="25d30-190">string</span></span> | <span data-ttu-id="25d30-191">Ja</span><span class="sxs-lookup"><span data-stu-id="25d30-191">Yes</span></span>      | <span data-ttu-id="25d30-192">En sträng som identifierar fakturan.</span><span class="sxs-lookup"><span data-stu-id="25d30-192">A string that identifies the invoice.</span></span>                             |
| <span data-ttu-id="25d30-193">fakturering-Provider</span><span class="sxs-lookup"><span data-stu-id="25d30-193">billing-provider</span></span>       | <span data-ttu-id="25d30-194">sträng</span><span class="sxs-lookup"><span data-stu-id="25d30-194">string</span></span> | <span data-ttu-id="25d30-195">Ja</span><span class="sxs-lookup"><span data-stu-id="25d30-195">Yes</span></span>      | <span data-ttu-id="25d30-196">Fakturerings leverantören: "Office", "Azure", "Databasmigrering".</span><span class="sxs-lookup"><span data-stu-id="25d30-196">The billing provider: "Office", "Azure", "OneTime".</span></span> <span data-ttu-id="25d30-197">I det äldre fallet har vi separata data modeller för Office & Azure-transaktioner.</span><span class="sxs-lookup"><span data-stu-id="25d30-197">In the legacy, we have separate data models for Office & Azure transactions.</span></span> <span data-ttu-id="25d30-198">Men den moderna har en enda data modell över alla transaktioner som filtrerats via värdet "Databasmigrering".</span><span class="sxs-lookup"><span data-stu-id="25d30-198">However, the modern has one single data model across all transactions filtered through the "OneTime" value.</span></span>            |
| <span data-ttu-id="25d30-199">faktura-rad-objekt-typ</span><span class="sxs-lookup"><span data-stu-id="25d30-199">invoice-line-item-type</span></span> | <span data-ttu-id="25d30-200">sträng</span><span class="sxs-lookup"><span data-stu-id="25d30-200">string</span></span> | <span data-ttu-id="25d30-201">Ja</span><span class="sxs-lookup"><span data-stu-id="25d30-201">Yes</span></span>      | <span data-ttu-id="25d30-202">Typ av faktura information: "BillingLineItems", "UsageLineItems".</span><span class="sxs-lookup"><span data-stu-id="25d30-202">The type of invoice detail: "BillingLineItems", "UsageLineItems".</span></span> |
| <span data-ttu-id="25d30-203">ikoner</span><span class="sxs-lookup"><span data-stu-id="25d30-203">size</span></span>                   | <span data-ttu-id="25d30-204">antal</span><span class="sxs-lookup"><span data-stu-id="25d30-204">number</span></span> | <span data-ttu-id="25d30-205">Inga</span><span class="sxs-lookup"><span data-stu-id="25d30-205">No</span></span>       | <span data-ttu-id="25d30-206">Det maximala antalet objekt som ska returneras.</span><span class="sxs-lookup"><span data-stu-id="25d30-206">The maximum number of items to return.</span></span> <span data-ttu-id="25d30-207">Standard Max storlek = 2000</span><span class="sxs-lookup"><span data-stu-id="25d30-207">Default max size = 2000</span></span>    |
| <span data-ttu-id="25d30-208">offset</span><span class="sxs-lookup"><span data-stu-id="25d30-208">offset</span></span>                 | <span data-ttu-id="25d30-209">antal</span><span class="sxs-lookup"><span data-stu-id="25d30-209">number</span></span> | <span data-ttu-id="25d30-210">Inga</span><span class="sxs-lookup"><span data-stu-id="25d30-210">No</span></span>       | <span data-ttu-id="25d30-211">Det nollbaserade indexet för det första rad objekt som ska returneras.</span><span class="sxs-lookup"><span data-stu-id="25d30-211">The zero-based index of the first line item to return.</span></span>            |
| <span data-ttu-id="25d30-212">seekOperation</span><span class="sxs-lookup"><span data-stu-id="25d30-212">seekOperation</span></span>          | <span data-ttu-id="25d30-213">sträng</span><span class="sxs-lookup"><span data-stu-id="25d30-213">string</span></span> | <span data-ttu-id="25d30-214">No</span><span class="sxs-lookup"><span data-stu-id="25d30-214">No</span></span>       | <span data-ttu-id="25d30-215">Om **fakturerings leverantören** är lika med **Databasmigrering** anger du **seekOperation** lika med **Nästa** för att hämta nästa sida med faktura rads objekt.</span><span class="sxs-lookup"><span data-stu-id="25d30-215">If **billing-provider** equals **OneTime**, set **seekOperation** equal to **Next** to get the next page of invoice line items.</span></span> |
| <span data-ttu-id="25d30-216">hasPartnerEarnedCredit</span><span class="sxs-lookup"><span data-stu-id="25d30-216">hasPartnerEarnedCredit</span></span> | <span data-ttu-id="25d30-217">boolesk</span><span class="sxs-lookup"><span data-stu-id="25d30-217">bool</span></span> | <span data-ttu-id="25d30-218">Inga</span><span class="sxs-lookup"><span data-stu-id="25d30-218">No</span></span> | <span data-ttu-id="25d30-219">Det värde som anger om rad artiklarna med partner intjänad kredit ska returneras.</span><span class="sxs-lookup"><span data-stu-id="25d30-219">The value indicating if to return the line items with partner earned credit applied.</span></span> <span data-ttu-id="25d30-220">OBS! den här parametern används endast när fakturerings leverantörens typ är Databasmigrering och InvoiceLineItemType är UsageLineItems.</span><span class="sxs-lookup"><span data-stu-id="25d30-220">Note: this parameter will be only applied when billing provider type is OneTime and InvoiceLineItemType is UsageLineItems.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="25d30-221">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="25d30-221">Request headers</span></span>

<span data-ttu-id="25d30-222">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="25d30-222">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="25d30-223">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="25d30-223">Request body</span></span>

<span data-ttu-id="25d30-224">Inga.</span><span class="sxs-lookup"><span data-stu-id="25d30-224">None.</span></span>

## <a name="rest-response"></a><span data-ttu-id="25d30-225">REST-svar</span><span class="sxs-lookup"><span data-stu-id="25d30-225">REST response</span></span>

<span data-ttu-id="25d30-226">Om det lyckas innehåller svaret insamling av rad objekts information.</span><span class="sxs-lookup"><span data-stu-id="25d30-226">If successful, the response contains the collection of line item details.</span></span>

<span data-ttu-id="25d30-227">*För rad posten **ChargeType** mappas värdet **inköp** till **New**. Värdets **åter betalning** mappas för att **avbryta**.*</span><span class="sxs-lookup"><span data-stu-id="25d30-227">*For the line item **ChargeType**, the value **Purchase** is mapped to **New**. The value **Refund** is mapped to **Cancel**.*</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="25d30-228">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="25d30-228">Response success and error codes</span></span>

<span data-ttu-id="25d30-229">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="25d30-229">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="25d30-230">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="25d30-230">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="25d30-231">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="25d30-231">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="rest-request-response-examples"></a><span data-ttu-id="25d30-232">Exempel på REST-svar</span><span class="sxs-lookup"><span data-stu-id="25d30-232">REST request-response examples</span></span>

### <a name="request-response-example-1"></a><span data-ttu-id="25d30-233">Request-Response-exempel 1</span><span class="sxs-lookup"><span data-stu-id="25d30-233">Request-response example 1</span></span>

<span data-ttu-id="25d30-234">I det här exemplet är informationen följande:</span><span class="sxs-lookup"><span data-stu-id="25d30-234">In this example, the details are as follows:</span></span>

- <span data-ttu-id="25d30-235">**BillingProvider**: **Office**</span><span class="sxs-lookup"><span data-stu-id="25d30-235">**BillingProvider**: **Office**</span></span>
- <span data-ttu-id="25d30-236">**InvoiceLineItemType**: **BillingLineItems**</span><span class="sxs-lookup"><span data-stu-id="25d30-236">**InvoiceLineItemType**: **BillingLineItems**</span></span>

#### <a name="request-example-1"></a><span data-ttu-id="25d30-237">Exempel på begäran 1</span><span class="sxs-lookup"><span data-stu-id="25d30-237">Request example 1</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/1234000000/lineitems?provider=Office&nvoicelineitemtype=BillingLineItems&size=2&offset=0 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-1"></a><span data-ttu-id="25d30-238">Svars exempel 1</span><span class="sxs-lookup"><span data-stu-id="25d30-238">Response example 1</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Thu, 07 Sep 2017 23:31:09 GMT

{
    "totalCount": 2,
    "items": [{
            "partnerId": "3b33e682-00c3-41ee-9dd2-a548adf56438",
            "customerId": "74221236-D09C-4870-AC1D-33E155E9AEBE",
            "customerName": "TSTAGIN1CUST190",
            "mpnId": 4391507,
            "tier2MpnId": -1,
            "orderId": "567735045559164136",
            "subscriptionId": "4KIKawEAAAAAAAEA",
            "syndicationPartnerSubscriptionNumber": "1F58ACD7-FE51-4705-9567-D009C9ADA150",
            "offerId": "AAA5B3F0-0EE2-431B-A42F-3F18F3C6D540",
            "durableOfferId": "2F707C7C-2433-49A5-A437-9CA7CF40D3EB",
            "offerName": "EXCHANGE ONLINE (PLAN 2)",
            "domainName": "TStagin1Cust190.onmicrosoft.com",
            "billingCycleType": "MONTHLY",
            "subscriptionName": "EXCHANGE ONLINE (PLAN 2)",
            "subscriptionDescription": "EXCHANGE ONLINE (PLAN 2)",
            "subscriptionStartDate": "2017-05-12T00:00:00",
            "subscriptionEndDate": "2018-06-10T00:00:00",
            "chargeStartDate": "2017-05-12T00:00:00",
            "chargeEndDate": "2017-06-09T00:00:00",
            "chargeType": "New",
            "unitPrice": 0.0,
            "quantity": 3,
            "amount": 0.0,
            "totalOtherDiscount": 0.0,
            "subtotal": 0.0,
            "tax": 0.0,
            "totalForCustomer": 0.0,
            "currency": "USD",
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "office",
            "attributes": {
                "objectType": "LicenseBasedLineItem"
            }
        }, {
            "partnerId": "3b33e682-00c3-41ee-9dd2-a548adf56438",
            "customerId": "74221236-D09C-4870-AC1D-33E155E9AEBE",
            "customerName": "TSTAGIN1CUST190",
            "mpnId": 4391507,
            "tier2MpnId": -1,
            "orderId": "567735045564795186",
            "subscriptionId": "Ik4YawEAAAAAAAEA",
            "syndicationPartnerSubscriptionNumber": "D8A8F773-9D3E-4244-8797-3182075F09FA",
            "offerId": "618B53FE-9B99-428B-9745-F706AEAF3979",
            "durableOfferId": "69C67983-CF78-4102-83F6-3E5FD246864F",
            "offerName": "SHAREPOINT ONLINE (PLAN 2)",
            "domainName": "TStagin1Cust190.onmicrosoft.com",
            "billingCycleType": "MONTHLY",
            "subscriptionName": "SHAREPOINT ONLINE (PLAN 2)",
            "subscriptionDescription": "SHAREPOINT ONLINE (PLAN 2)",
            "subscriptionStartDate": "2017-05-13T00:00:00",
            "subscriptionEndDate": "2018-06-10T00:00:00",
            "chargeStartDate": "2017-05-13T00:00:00",
            "chargeEndDate": "2017-06-09T00:00:00",
            "chargeType": "New",
            "unitPrice": 0.0,
            "quantity": 1,
            "amount": 0.0,
            "totalOtherDiscount": 0.0,
            "subtotal": 0.0,
            "tax": 0.0,
            "totalForCustomer": 0.0,
            "currency": "USD",
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "office",
            "attributes": {
                "objectType": "LicenseBasedLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/1234000000/lineitems?provider=Office&nvoicelineitemtype=BillingLineItems&size=2&offset=0",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/1234000000/lineitems?provider=Office&nvoicelineitemtype=BillingLineItems&size=2&offset=",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="request-response-example-2"></a><span data-ttu-id="25d30-239">Request-Response-exempel 2</span><span class="sxs-lookup"><span data-stu-id="25d30-239">Request-response example 2</span></span>

<span data-ttu-id="25d30-240">I följande exempel är informationen följande:</span><span class="sxs-lookup"><span data-stu-id="25d30-240">In the following example, the details are as follows:</span></span>

- <span data-ttu-id="25d30-241">**BillingProvider**: **Azure**</span><span class="sxs-lookup"><span data-stu-id="25d30-241">**BillingProvider**: **Azure**</span></span>
- <span data-ttu-id="25d30-242">**InvoiceLineItemType**: **BillingLineItems**</span><span class="sxs-lookup"><span data-stu-id="25d30-242">**InvoiceLineItemType**: **BillingLineItems**</span></span>

#### <a name="request-example-2"></a><span data-ttu-id="25d30-243">Exempel på begäran 2</span><span class="sxs-lookup"><span data-stu-id="25d30-243">Request example 2</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/1234000000/lineitems?provider=Azure&invoicelineitemtype=BillingLineItems&size=2&offset=0 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-2"></a><span data-ttu-id="25d30-244">Svars exempel 2</span><span class="sxs-lookup"><span data-stu-id="25d30-244">Response example 2</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Thu, 07 Sep 2017 23:31:09 GMT

{
    "totalCount": 2,
    "items": [
        {
            "detailLineItemId": 1,
            "sku": "7UD-00001",
            "includedQuantity": 0,
            "overageQuantity": 745,
            "listPrice": 0.085,
            "currency": "USD",
            "pretaxCharges": 63.33,
            "taxAmount": 6.34,
            "postTaxTotal": 69.67,
            "pretaxEffectiveRate": 0.08500671,
            "postTaxEffectiveRate": 0.09351677,
            "chargeType": "Assess usage fee for current cycle",
            "invoiceLineItemType": "billing_line_items",
            "partnerId": "1F5CCB06-8E36-4A74-A74C-FCAA9E000000",
            "partnerName": "TEST_TEST_Big foot consulting",
            "partnerBillableAccountId": "1010578050",
            "customerId": "65726577-c208-40fd-9735-8c85ac000000",
            "domainName": "600test.onmicrosoft.com",
            "customerCompanyName": "601 tests",
            "mpnId": 4390934,
            "tier2MpnId": -1,
            "invoiceNumber": "1234000000",
            "subscriptionId": "87f4b92f-a490-485e-ad34-5b70cb000000",
            "subscriptionName": "Microsoft Azure",
            "subscriptionDescription": "Microsoft Azure",
            "billingCycleType": "Monthly",
            "orderId": "568297985427000000",
            "serviceName": "Azure App Service",
            "serviceType": "Standard Plan",
            "resourceGuid": "505db374-df8a-44df-9d8c-13c14b61dee1",
            "resourceName": "S1",
            "region": "",
            "consumedQuantity": 745,
            "chargeStartDate": "2019-08-02T00:00:00",
            "chargeEndDate": "2019-09-01T00:00:00",
            "unit": "1 Hour",
            "billingProvider": "azure",
            "attributes": {
                "objectType": "UsageBasedLineItem"
            }
        },
        {
            "detailLineItemId": 1,
            "sku": "7UD-00001",
            "includedQuantity": 0,
            "overageQuantity": 0.000882,
            "listPrice": 0.0383,
            "currency": "USD",
            "pretaxCharges": 0,
            "taxAmount": 0,
            "postTaxTotal": 0,
            "pretaxEffectiveRate": 0,
            "postTaxEffectiveRate": 0,
            "chargeType": "Assess usage fee for current cycle",
            "invoiceLineItemType": "billing_line_items",
            "partnerId": "1F5CCB06-8E36-4A74-A74C-FCAA9E87E26A",
            "partnerName": "TEST_TEST_Big foot consulting",
            "partnerBillableAccountId": "1010578050",
            "customerId": "65726577-c208-40fd-9735-8c85ac9cac68",
            "domainName": "600test.onmicrosoft.com",
            "customerCompanyName": "601 tests",
            "mpnId": 4390934,
            "tier2MpnId": -1,
            "invoiceNumber": "1234000000",
            "subscriptionId": "87f4b92f-a490-485e-ad34-5b70cb000000",
            "subscriptionName": "Microsoft Azure",
            "subscriptionDescription": "Microsoft Azure",
            "billingCycleType": "Monthly",
            "orderId": "568297985427000000",
            "serviceName": "Storage",
            "serviceType": "Standard Page Blob",
            "resourceGuid": "d23a5753-ff85-4ddf-af28-8cc5cf2d3882",
            "resourceName": "LRS Data Stored",
            "region": "",
            "consumedQuantity": 0.000882,
            "chargeStartDate": "2019-08-02T00:00:00",
            "chargeEndDate": "2019-09-01T00:00:00",
            "unit": "1 GB/Month",
            "billingProvider": "azure",
            "attributes": {
                "objectType": "UsageBasedLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/1234000000/lineitems?provider=Azure&invoicelineitemtype=BillingLineItems&size=2&offset=0",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/1234000000/lineitems?provider=Azure&invoicelineitemtype=BillingLineItems&size=2&offset=2",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="request-response-example-3"></a><span data-ttu-id="25d30-245">Request-Response-exempel 3</span><span class="sxs-lookup"><span data-stu-id="25d30-245">Request-response example 3</span></span>

<span data-ttu-id="25d30-246">I följande exempel är informationen följande:</span><span class="sxs-lookup"><span data-stu-id="25d30-246">In the following example, the details are as follows:</span></span>

- <span data-ttu-id="25d30-247">**BillingProvider**: **Azure**</span><span class="sxs-lookup"><span data-stu-id="25d30-247">**BillingProvider**: **Azure**</span></span>
- <span data-ttu-id="25d30-248">**InvoiceLineItemType**: **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="25d30-248">**InvoiceLineItemType**: **UsageLineItems**</span></span>

#### <a name="request-example-3"></a><span data-ttu-id="25d30-249">Exempel på begäran 3</span><span class="sxs-lookup"><span data-stu-id="25d30-249">Request example 3</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/1234000000/lineitems?provider=Azure&invoicelineitemtype=UsageLineItems&size=2&offset=0 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-3"></a><span data-ttu-id="25d30-250">Svars exempel 3</span><span class="sxs-lookup"><span data-stu-id="25d30-250">Response example 3</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Thu, 07 Sep 2017 23:31:09 GMT

{
    "totalCount": 2,
    "items": [
        {
            "customerBillableAccount": "1439508127",
            "usageDate": "2019-08-05T00:00:00",
            "invoiceLineItemType": "usage_line_items",
            "partnerId": "1F5CCB06-8E36-4A74-A74C-FCAA9E000000",
            "partnerName": "TEST_TEST_BIG FOOT CONSULTING",
            "partnerBillableAccountId": "1010578050",
            "customerId": "9E9B71BA-3442-458B-B519-E1CCF72FBB54",
            "domainName": "test600.onmicrosoft.com",
            "customerCompanyName": "600 TEST",
            "mpnId": 4390934,
            "tier2MpnId": -1,
            "invoiceNumber": "1234000000",
            "subscriptionId": "F9BA6DA0-6DAC-4F88-B623-313C9B9C117A",
            "subscriptionName": "MICROSOFT AZURE",
            "subscriptionDescription": "MICROSOFT AZURE",
            "billingCycleType": "MONTHLY",
            "orderId": "568297985577171353",
            "serviceName": "STORAGE",
            "serviceType": "STANDARD PAGE BLOB",
            "resourceGuid": "9CC63CF8-6593-410A-B0E7-26A4EF71E8B3",
            "resourceName": "DISK DELETE OPERATIONS",
            "region": "",
            "consumedQuantity": 2.9616,
            "chargeStartDate": "2019-08-05T00:00:00",
            "chargeEndDate": "2019-09-04T00:00:00",
            "unit": "10K",
            "billingProvider": "azure",
            "attributes": {
                "objectType": "DailyUsageLineItem"
            }
        },
        {
            "customerBillableAccount": "1307536861",
            "usageDate": "2019-08-10T00:00:00",
            "invoiceLineItemType": "usage_line_items",
            "partnerId": "1F5CCB06-8E36-4A74-A74C-FCAA9E000000",
            "partnerName": "TEST_TEST_BIG FOOT CONSULTING",
            "partnerBillableAccountId": "1010578050",
            "customerId": "EB53B7BD-267E-440E-B3C0-8F0B40000000",
            "domainName": "brandontest.onmicrosoft.com",
            "customerCompanyName": "BRANDON'S TEST",
            "mpnId": 4390934,
            "tier2MpnId": -1,
            "invoiceNumber": "1234000000",
            "subscriptionId": "62D22561-AB15-41E5-AD59-99025C000000",
            "subscriptionName": "MICROSOFT AZURE",
            "subscriptionDescription": "MICROSOFT AZURE",
            "billingCycleType": "MONTHLY",
            "orderId": "568297985605838583",
            "serviceName": "VIRTUAL MACHINES",
            "serviceType": "D/DS SERIES WINDOWS",
            "resourceGuid": "62C64B6C-4033-4E20-AB33-9E81271AC12A",
            "resourceName": "D1/DS1",
            "region": "US WEST",
            "consumedQuantity": 24,
            "chargeStartDate": "2019-08-05T00:00:00",
            "chargeEndDate": "2019-09-04T00:00:00",
            "unit": "1 HOUR",
            "billingProvider": "azure",
            "attributes": {
                "objectType": "DailyUsageLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/1234000000/lineitems?provider=Azure&invoicelineitemtype=UsageLineItems&size=2&offset=0",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/1234000000/lineitems?provider=Azure&invoicelineitemtype=UsageLineItems&size=2&offset=2",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="request-response-example-4"></a><span data-ttu-id="25d30-251">Request-Response-exempel 4</span><span class="sxs-lookup"><span data-stu-id="25d30-251">Request-response example 4</span></span>

<span data-ttu-id="25d30-252">I följande exempel är informationen följande:</span><span class="sxs-lookup"><span data-stu-id="25d30-252">In the following example, the details are as follows:</span></span>

- <span data-ttu-id="25d30-253">**BillingProvider**: **Databasmigrering**</span><span class="sxs-lookup"><span data-stu-id="25d30-253">**BillingProvider**: **OneTime**</span></span>
- <span data-ttu-id="25d30-254">**InvoiceLineItemType**: **BillingLineItems**</span><span class="sxs-lookup"><span data-stu-id="25d30-254">**InvoiceLineItemType**: **BillingLineItems**</span></span>

#### <a name="request-example-4"></a><span data-ttu-id="25d30-255">Exempel på begäran 4</span><span class="sxs-lookup"><span data-stu-id="25d30-255">Request example 4</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/G000024135/lineitems/OneTime/BillingLineItems?size=2&offset=0 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-4"></a><span data-ttu-id="25d30-256">Svars exempel 4</span><span class="sxs-lookup"><span data-stu-id="25d30-256">Response example 4</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Thu, 07 Sep 2017 23:31:09 GMT

 {
    "continuationToken": "d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7",
    "totalCount": 2,
    "items": [
        {
            "partnerId": "6480d686-cfb4-424d-a945-6b9b9f000000",
            "customerId": "org:9060d13d-c5ed-482e-b059-a15a38000000",
            "customerName": "recipientCustomerName",
            "customerDomainName": "recipientCustomerDomain",
            "invoiceNumber": "1234000000",
            "quoteId": "abcd12345678",
            "mpnId": "4870137",
            "resellerMpnId": 0,
            "orderId": "QDOx5ZN3YR9uYhm4M1MGQJ_0nievUOrx1",
            "orderDate": "2018-02-08T22:31:42.9397946Z",
            "productId": "productid",
            "skuId": "skuid",
            "availabilityId": "availabilityid",
            "productName": "TEST PRODUCT",
            "skuName": "TEST SKU TITLE",
            "chargeType": "New",
            "unitPrice": 431.8,
            "effectiveUnitPrice": 496.07,
            "unitType": "Seats",
            "quantity": 1,
            "subtotal": 431.8,
            "taxTotal": 38.87,
            "totalForCustomer": 470.67,
            "currency": "USD",
            "providerName": "Test Networks Inc",
            "providerId": "12343810",
            "subscriptionDescription": "",
            "subscriptionId": "281e26fe-9ce7-415b-911c-f39232000000",
            "subscriptionStartDate": "2019-01-03T19:53:55.1292512+00:00",
            "subscriptionEndDate": "2019-02-02T19:53:55.1292512+00:00",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "1234278124b8",
            "priceAdjustmentDescription": "[\"100.0% Tier 1 Discount\"]",
            "creditReasonCode": "Azure Consumption Credit",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-09-30T23:59:59Z",
            "billableQuantity": 0.0159369774,
            "meterDescription": "Bandwidth - Data Transfer In (GB) - Zone 2",
            "billingFrequency": "Monthly",
            "reservationOrderId": "883d475b-0000-2222-0000-8818752f1234",
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "one_time",
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        },
        {
            "partnerId": "6480d686-cfb4-424d-a945-6b9b9f4badc2",
            "customerId": "org:9060d13d-c5ed-482e-b059-a15a38cbb28e",
            "customerName": "recipientCustomerName",
            "customerDomainName": "recipientCustomerDomain",
            "invoiceNumber": "1234000000",
            "quoteId": "abcd12345678",
            "mpnId": "4870137",
            "resellerMpnId": 0,
            "orderId": "QDOx5ZN3YR9uYhm4M1MGQJ_0nievUOrx1",
            "orderDate": "2018-02-08T22:31:42.9397946Z",
            "productId": "productid",
            "skuId": "skuid",
            "availabilityId": "availabilityid",
            "productName": "TEST PRODUCT",
            "skuName": "TEST SKU TITLE",
            "chargeType": "New",
            "unitPrice": 26.35,
            "effectiveUnitPrice": 496.07,
            "unitType": "1 Hour",
            "quantity": 1,
            "subtotal": 26.35,
            "taxTotal": 2.37,
            "totalForCustomer": 28.72,
            "currency": "USD",
            "providerName": "Test Networks Inc",
            "providerId": "12343810",
            "subscriptionDescription": "",
            "subscriptionId": "281e26fe-9ce7-415b-911c-f39232ea904a",
            "subscriptionStartDate": "2019-01-03T19:53:55.1292512+00:00",
            "subscriptionEndDate": "2019-02-02T19:53:55.1292512+00:00",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "1234578124b8",
            "priceAdjustmentDescription": "[\"100.0% Tier 1 Discount\"]",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-09-30T23:59:59Z",
            "billableQuantity": 0.0130687981,
            "meterDescription": "Bandwidth - Data Transfer In (GB) - Zone 2",
            "reservationOrderId": "",
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "one_time",
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/G000024135/lineitems?provider=OneTime&nvoicelineitemtype=BillingLineItems&size=2",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/G000024135/lineitems?provider=OneTime&nvoicelineitemtype=BillingLineItems&size=2?seekOperation=Next",
            "method": "GET",
            "headers": [
                {
                    "key": "MS-ContinuationToken",
                    "value": "d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7"
                }
            ]
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="request-response-example-5"></a><span data-ttu-id="25d30-257">Request-Response-exempel 5</span><span class="sxs-lookup"><span data-stu-id="25d30-257">Request-response example 5</span></span>

<span data-ttu-id="25d30-258">I följande exempel finns växling med en tilläggs-token.</span><span class="sxs-lookup"><span data-stu-id="25d30-258">In the following example, there is paging using a continuation token.</span></span> <span data-ttu-id="25d30-259">Så här går det till:</span><span class="sxs-lookup"><span data-stu-id="25d30-259">The details are as follows:</span></span>

- <span data-ttu-id="25d30-260">**BillingProvider**: **Databasmigrering**</span><span class="sxs-lookup"><span data-stu-id="25d30-260">**BillingProvider**: **OneTime**</span></span>
- <span data-ttu-id="25d30-261">**InvoiceLineItemType**: **BillingLineItems**</span><span class="sxs-lookup"><span data-stu-id="25d30-261">**InvoiceLineItemType**: **BillingLineItems**</span></span>
- <span data-ttu-id="25d30-262">**SeekOperation**: **Nästa**</span><span class="sxs-lookup"><span data-stu-id="25d30-262">**SeekOperation**: **Next**</span></span>

#### <a name="request-example-5"></a><span data-ttu-id="25d30-263">Exempel på begäran 5</span><span class="sxs-lookup"><span data-stu-id="25d30-263">Request example 5</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/G000024135/lineitems/OneTime/BillingLineItems?seekOperation=Next HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-ContinuationToken: d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-5"></a><span data-ttu-id="25d30-264">Svars exempel 5</span><span class="sxs-lookup"><span data-stu-id="25d30-264">Response example 5</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Thu, 07 Sep 2017 23:31:09 GMT

{
    "totalCount": 1,
    "items": [
        {
            "partnerId": "6480d686-cfb4-424d-a945-6b9b9f000000",
            "customerId": "org:9060d13d-c5ed-482e-b059-a15a38000000",
            "customerName": "recipientCustomerName",
            "customerDomainName": "recipientCustomerDomain",
            "invoiceNumber": "1234000000",
            "quoteId": "abcd12345678",
            "mpnId": "4870137",
            "resellerMpnId": 0,
            "orderId": "NeqT31Kziwf8gkCXM9YQToWTqU-9Jbm81",
            "orderDate": "2018-02-08T22:31:47.1751688Z",
            "productId": "DZH318Z0BQ3P",
            "skuId": "001F",
            "availabilityId": "DZH318Z0DR0H",
            "productName": "Reserved VM Instance, Standard_D1, AP East, 3 years",
            "skuName": "D Series",
            "chargeType": "New",
            "unitPrice": 1447,
            "effectiveUnitPrice": 496.07,
            "unitType": "Seats",
            "quantity": 1,
            "subtotal": 1447,
            "taxTotal": 130.24,
            "totalForCustomer": 1577.24,
            "currency": "USD",
            "providerName": "Test Networks Inc",
            "providerId": "12343810",
            "subscriptionDescription": "",
            "subscriptionId": "281e26fe-9ce7-415b-911c-f39232000000",
            "subscriptionStartDate": "2019-01-03T19:53:55.1292512+00:00",
            "subscriptionEndDate": "2019-02-02T19:53:55.1292512+00:00",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "1234568124b8",
            "priceAdjustmentDescription": "",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-09-30T23:59:59Z",
            "billableQuantity": 0.0130687981,
            "meterDescription": "Bandwidth - Data Transfer In (GB) - Zone 2",
            "reservationOrderId": "",
            "billingFrequency": "Monthly",
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "one_time",
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/G000024135/lineitems?provider=OneTime&nvoicelineitemtype=BillingLineItems&size=2",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
