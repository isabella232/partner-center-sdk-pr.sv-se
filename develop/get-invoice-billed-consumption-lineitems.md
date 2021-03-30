---
title: Hämta fakturerade försäljnings artiklar för försäljnings förbrukning
description: 'Du kan hämta en samling av försäljnings objekt för försäljning per dag (stängd dagligt Beräknad användnings rad artikel) information för en viss faktura med hjälp av API: er för partner Center.'
ms.date: 01/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 1e19792da6a7510bf02dd11b3e77f40a8365be2b
ms.sourcegitcommit: 4ec053c56fd210b174fe657aa7b86faf4e2b5a7c
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/29/2021
ms.locfileid: "105730203"
---
# <a name="get-invoice-billed-commercial-consumption-line-items"></a><span data-ttu-id="679d0-103">Hämta fakturerade försäljnings artiklar för försäljnings förbrukning</span><span class="sxs-lookup"><span data-stu-id="679d0-103">Get invoice billed commercial consumption line items</span></span>

<span data-ttu-id="679d0-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="679d0-104">**Applies to:**</span></span>

- <span data-ttu-id="679d0-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="679d0-105">Partner Center</span></span>

<span data-ttu-id="679d0-106">Du kan använda följande metoder för att få en samling information om försäljnings objekt för kommersiella förbruknings fakturor (kallas även avslutade dagliga, beräknade användnings rads objekt) för en viss faktura.</span><span class="sxs-lookup"><span data-stu-id="679d0-106">You can use the following methods to get a collection of details for commercial consumption invoice line items (also known as closed daily rated usage line items) for a specified invoice.</span></span>

<span data-ttu-id="679d0-107">Detta API stöder också **Azure** -providertyp för Microsoft Azure (MS-AZR-0145P)-prenumerationer.</span><span class="sxs-lookup"><span data-stu-id="679d0-107">This API also supports **azure** provider types for Microsoft Azure (MS-AZR-0145P) subscriptions.</span></span> <span data-ttu-id="679d0-108">Detta innebär att denna API är en bakåtkompatibla funktion.</span><span class="sxs-lookup"><span data-stu-id="679d0-108">This means this API is a backward-compatible feature.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="679d0-109">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="679d0-109">Prerequisites</span></span>

- <span data-ttu-id="679d0-110">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="679d0-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="679d0-111">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="679d0-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="679d0-112">Ett faktura-ID.</span><span class="sxs-lookup"><span data-stu-id="679d0-112">An invoice identifier.</span></span> <span data-ttu-id="679d0-113">Detta identifierar fakturan som rad artiklarna ska hämtas för.</span><span class="sxs-lookup"><span data-stu-id="679d0-113">This identifies the invoice for which to retrieve the line items.</span></span>

## <a name="c"></a><span data-ttu-id="679d0-114">C\#</span><span class="sxs-lookup"><span data-stu-id="679d0-114">C\#</span></span>

<span data-ttu-id="679d0-115">Om du vill hämta de kommersiella rad artiklarna för den angivna fakturan måste du hämta faktura objektet:</span><span class="sxs-lookup"><span data-stu-id="679d0-115">To get the commercial line items for the specified invoice, you must retrieve the invoice object:</span></span>

1. <span data-ttu-id="679d0-116">Anropa [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) -metoden för att hämta ett gränssnitt för att fakturera åtgärder för den angivna fakturan.</span><span class="sxs-lookup"><span data-stu-id="679d0-116">Call the [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) method to get an interface to invoice operations for the specified invoice.</span></span>

2. <span data-ttu-id="679d0-117">Anropa [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) -eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) -metoden för att hämta fakturaprojektet.</span><span class="sxs-lookup"><span data-stu-id="679d0-117">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the invoice object.</span></span> <span data-ttu-id="679d0-118">Fakturaprojektet innehåller all information för den angivna fakturan.</span><span class="sxs-lookup"><span data-stu-id="679d0-118">The invoice object contains all of the information for the specified invoice.</span></span>

<span data-ttu-id="679d0-119">**Providern** identifierar källan till den fakturerade detalj informationen (till exempel **Databasmigrering**).</span><span class="sxs-lookup"><span data-stu-id="679d0-119">The **Provider** identifies the source of the billed detail information (for example, **onetime**).</span></span> <span data-ttu-id="679d0-120">**InvoiceLineItemType** anger typen (till exempel **UsageLineItem**).</span><span class="sxs-lookup"><span data-stu-id="679d0-120">The **InvoiceLineItemType** specifies the type (for example, **UsageLineItem**).</span></span>

<span data-ttu-id="679d0-121">I följande exempel kod används en **förgrunds** slinga för att bearbeta samling med rad objekt.</span><span class="sxs-lookup"><span data-stu-id="679d0-121">The following example code uses a **foreach** loop to process the line items collection.</span></span> <span data-ttu-id="679d0-122">En separat samling av rad objekt hämtas för varje **InvoiceLineItemType**.</span><span class="sxs-lookup"><span data-stu-id="679d0-122">A separate collection of line items is retrieved for each **InvoiceLineItemType**.</span></span>

<span data-ttu-id="679d0-123">Hämta en samling av rad objekt som motsvarar en **InvoiceDetail** -instans:</span><span class="sxs-lookup"><span data-stu-id="679d0-123">To get a collection of line items that correspond to an **InvoiceDetail** instance:</span></span>

1. <span data-ttu-id="679d0-124">Skicka instansens **BillingProvider** och **InvoiceLineItemType** till [**by**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) -metoden.</span><span class="sxs-lookup"><span data-stu-id="679d0-124">Pass the instance's **BillingProvider** and **InvoiceLineItemType** to the [**By**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) method.</span></span>

2. <span data-ttu-id="679d0-125">Anropa [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) -eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) -metoden för att hämta de associerade rad objekten.</span><span class="sxs-lookup"><span data-stu-id="679d0-125">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the associated line items.</span></span>
3. <span data-ttu-id="679d0-126">Skapa en uppräknare för att passera samlingen som visas i följande exempel.</span><span class="sxs-lookup"><span data-stu-id="679d0-126">Create an enumerator to traverse the collection as shown in the following example.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string invoiceId;
// string curencyCode;
// string period;
// int pageMaxSizeReconLineItems = 2000;

// all the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

var seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById(invoiceId).By("onetime", "usagelineitems", curencyCode, period, pageMaxSizeReconLineItems).Get();

var fetchNext = true;

ConsoleKeyInfo keyInfo;

var itemNumber = 1;
while (fetchNext)
{
    Console.Out.WriteLine("\tLine line items count: " + seekBasedResourceCollection.Items.Count());

    seekBasedResourceCollection.Items.ToList().ForEach(item =>
    {
        // Instance of type DailyRatedUsageLineItem
        if (item is DailyRatedUsageLineItem)
        {
            Type t = typeof(DailyRatedUsageLineItem);
            PropertyInfo[] properties = t.GetProperties();

            foreach (PropertyInfo property in properties)
            {
                // Insert code here to work with the line item properties
            }
        }
        itemNumber++;
    });

    Console.Out.WriteLine("\tPress any key to fetch next data. Press the Escape (Esc) key to quit: \n");
    keyInfo = Console.ReadKey();

    if (keyInfo.Key == ConsoleKey.Escape)
    {
        break;
    }

    fetchNext = !string.IsNullOrWhiteSpace(seekBasedResourceCollection.ContinuationToken);

    if (fetchNext)
    {
        if (seekBasedResourceCollection.Links.Next.Headers != null && seekBasedResourceCollection.Links.Next.Headers.Any())
        {
            seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById(invoiceId).By("onetime", "usagelineitems", curencyCode, period, pageMaxSizeReconLineItems).Seek(seekBasedResourceCollection.ContinuationToken, SeekOperation.Next);
        }
    }
}
```

<span data-ttu-id="679d0-127">Ett liknande exempel finns i följande avsnitt:</span><span class="sxs-lookup"><span data-stu-id="679d0-127">For a similar example, see the following:</span></span>

- <span data-ttu-id="679d0-128">Exempel: [konsol test app](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="679d0-128">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="679d0-129">Projekt: **SDK-exempel för partner Center**</span><span class="sxs-lookup"><span data-stu-id="679d0-129">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="679d0-130">Klass: **GetBilledConsumptionReconLineItemsPaging. cs**</span><span class="sxs-lookup"><span data-stu-id="679d0-130">Class: **GetBilledConsumptionReconLineItemsPaging.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="679d0-131">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="679d0-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="679d0-132">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="679d0-132">Request syntax</span></span>

<span data-ttu-id="679d0-133">Använd den första syntaxen för att returnera en fullständig lista över varje rad objekt för den aktuella fakturan.</span><span class="sxs-lookup"><span data-stu-id="679d0-133">Use the first syntax to return a full list of every line item for the given invoice.</span></span> <span data-ttu-id="679d0-134">För stora fakturor använder du den andra syntaxen med en angiven storlek och 0-baserad förskjutning för att returnera en sid lista med rad objekt.</span><span class="sxs-lookup"><span data-stu-id="679d0-134">For large invoices, use the second syntax with a specified size and 0-based offset to return a paged list of line items.</span></span> <span data-ttu-id="679d0-135">Använd den tredje syntaxen för att hämta nästa sida av rekognoseringar rad objekt med hjälp av `seekOperation = "Next"` .</span><span class="sxs-lookup"><span data-stu-id="679d0-135">Use the third syntax to get the next page of recon line items using `seekOperation = "Next"`.</span></span>

| <span data-ttu-id="679d0-136">Metod</span><span class="sxs-lookup"><span data-stu-id="679d0-136">Method</span></span>  | <span data-ttu-id="679d0-137">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="679d0-137">Request URI</span></span>                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="679d0-138">**TA**</span><span class="sxs-lookup"><span data-stu-id="679d0-138">**GET**</span></span> | <span data-ttu-id="679d0-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/INVOICES/{Invoice-ID}/lineitems? Provider = Databasmigrering&invoicelineitemtype = usagelineitems&CurrencyCode = {CURRENCYCODE} http/1.1</span><span class="sxs-lookup"><span data-stu-id="679d0-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode} HTTP/1.1</span></span>                              |
| <span data-ttu-id="679d0-140">**TA**</span><span class="sxs-lookup"><span data-stu-id="679d0-140">**GET**</span></span> | <span data-ttu-id="679d0-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/INVOICES/{Invoice-ID}/lineitems? Provider = Databasmigrering&invoicelineitemtype = usagelineitems&CurrencyCode = {currencycode} &storlek = {size} http/1.1</span><span class="sxs-lookup"><span data-stu-id="679d0-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size} HTTP/1.1</span></span>  |
| <span data-ttu-id="679d0-142">**TA**</span><span class="sxs-lookup"><span data-stu-id="679d0-142">**GET**</span></span> | <span data-ttu-id="679d0-143">[*{baseURL}*](partner-center-rest-urls.md)/v1/INVOICES/{Invoice-ID}/lineitems? Provider = Databasmigrering&invoicelineitemtype = usagelineitems&CurrencyCode = {currencycode} &storlek = {size} &SeekOperation = nästa</span><span class="sxs-lookup"><span data-stu-id="679d0-143">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size}&seekOperation=Next</span></span>                               |

#### <a name="uri-parameters"></a><span data-ttu-id="679d0-144">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="679d0-144">URI parameters</span></span>

<span data-ttu-id="679d0-145">Använd följande URI och frågeparametrar när du skapar begäran.</span><span class="sxs-lookup"><span data-stu-id="679d0-145">Use the following URI and query parameters when creating the request.</span></span>

| <span data-ttu-id="679d0-146">Namn</span><span class="sxs-lookup"><span data-stu-id="679d0-146">Name</span></span>                   | <span data-ttu-id="679d0-147">Typ</span><span class="sxs-lookup"><span data-stu-id="679d0-147">Type</span></span>   | <span data-ttu-id="679d0-148">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="679d0-148">Required</span></span> | <span data-ttu-id="679d0-149">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="679d0-149">Description</span></span>                                                       |
|------------------------|--------|----------|-------------------------------------------------------------------|
| <span data-ttu-id="679d0-150">faktura-ID</span><span class="sxs-lookup"><span data-stu-id="679d0-150">invoice-id</span></span>             | <span data-ttu-id="679d0-151">sträng</span><span class="sxs-lookup"><span data-stu-id="679d0-151">string</span></span> | <span data-ttu-id="679d0-152">Ja</span><span class="sxs-lookup"><span data-stu-id="679d0-152">Yes</span></span>      | <span data-ttu-id="679d0-153">En sträng som identifierar fakturan.</span><span class="sxs-lookup"><span data-stu-id="679d0-153">A string that identifies the invoice.</span></span>                             |
| <span data-ttu-id="679d0-154">CSP</span><span class="sxs-lookup"><span data-stu-id="679d0-154">provider</span></span>               | <span data-ttu-id="679d0-155">sträng</span><span class="sxs-lookup"><span data-stu-id="679d0-155">string</span></span> | <span data-ttu-id="679d0-156">Ja</span><span class="sxs-lookup"><span data-stu-id="679d0-156">Yes</span></span>      | <span data-ttu-id="679d0-157">Providern: "Databasmigrering".</span><span class="sxs-lookup"><span data-stu-id="679d0-157">The provider: "OneTime".</span></span>                                  |
| <span data-ttu-id="679d0-158">faktura-rad-objekt-typ</span><span class="sxs-lookup"><span data-stu-id="679d0-158">invoice-line-item-type</span></span> | <span data-ttu-id="679d0-159">sträng</span><span class="sxs-lookup"><span data-stu-id="679d0-159">string</span></span> | <span data-ttu-id="679d0-160">Ja</span><span class="sxs-lookup"><span data-stu-id="679d0-160">Yes</span></span>      | <span data-ttu-id="679d0-161">Typ av faktura information: "UsageLineItems".</span><span class="sxs-lookup"><span data-stu-id="679d0-161">The type of invoice detail: "UsageLineItems".</span></span> |
| <span data-ttu-id="679d0-162">currencyCode</span><span class="sxs-lookup"><span data-stu-id="679d0-162">currencyCode</span></span>           | <span data-ttu-id="679d0-163">sträng</span><span class="sxs-lookup"><span data-stu-id="679d0-163">string</span></span> | <span data-ttu-id="679d0-164">Ja</span><span class="sxs-lookup"><span data-stu-id="679d0-164">Yes</span></span>      | <span data-ttu-id="679d0-165">Valuta koden för de fakturerade rad artiklarna.</span><span class="sxs-lookup"><span data-stu-id="679d0-165">The currency code for the billed line items.</span></span>                    |
| <span data-ttu-id="679d0-166">period</span><span class="sxs-lookup"><span data-stu-id="679d0-166">period</span></span>                 | <span data-ttu-id="679d0-167">sträng</span><span class="sxs-lookup"><span data-stu-id="679d0-167">string</span></span> | <span data-ttu-id="679d0-168">Ja</span><span class="sxs-lookup"><span data-stu-id="679d0-168">Yes</span></span>      | <span data-ttu-id="679d0-169">Period för fakturerad rekognoseringar.</span><span class="sxs-lookup"><span data-stu-id="679d0-169">The period for billed recon.</span></span> <span data-ttu-id="679d0-170">exempel: Current, Previous.</span><span class="sxs-lookup"><span data-stu-id="679d0-170">example: current, previous.</span></span>        |
| <span data-ttu-id="679d0-171">ikoner</span><span class="sxs-lookup"><span data-stu-id="679d0-171">size</span></span>                   | <span data-ttu-id="679d0-172">antal</span><span class="sxs-lookup"><span data-stu-id="679d0-172">number</span></span> | <span data-ttu-id="679d0-173">Inga</span><span class="sxs-lookup"><span data-stu-id="679d0-173">No</span></span>       | <span data-ttu-id="679d0-174">Det maximala antalet objekt som ska returneras.</span><span class="sxs-lookup"><span data-stu-id="679d0-174">The maximum number of items to return.</span></span> <span data-ttu-id="679d0-175">Standard storleken är 2000</span><span class="sxs-lookup"><span data-stu-id="679d0-175">Default size is 2000</span></span>       |
| <span data-ttu-id="679d0-176">seekOperation</span><span class="sxs-lookup"><span data-stu-id="679d0-176">seekOperation</span></span>          | <span data-ttu-id="679d0-177">sträng</span><span class="sxs-lookup"><span data-stu-id="679d0-177">string</span></span> | <span data-ttu-id="679d0-178">No</span><span class="sxs-lookup"><span data-stu-id="679d0-178">No</span></span>       | <span data-ttu-id="679d0-179">Ange seekOperation = nästa för att hämta nästa sida med rekognoseringar rad objekt.</span><span class="sxs-lookup"><span data-stu-id="679d0-179">Set seekOperation=Next to get the next page of recon line items.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="679d0-180">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="679d0-180">Request headers</span></span>

<span data-ttu-id="679d0-181">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="679d0-181">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="679d0-182">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="679d0-182">Request body</span></span>

<span data-ttu-id="679d0-183">Inga.</span><span class="sxs-lookup"><span data-stu-id="679d0-183">None.</span></span>

## <a name="rest-response"></a><span data-ttu-id="679d0-184">REST-svar</span><span class="sxs-lookup"><span data-stu-id="679d0-184">REST response</span></span>

<span data-ttu-id="679d0-185">Om det lyckas innehåller svaret insamling av rad objekts information.</span><span class="sxs-lookup"><span data-stu-id="679d0-185">If successful, the response contains the collection of line item details.</span></span>

<span data-ttu-id="679d0-186">För rad posten **ChargeType** mappas värdet **inköp** till **New**.</span><span class="sxs-lookup"><span data-stu-id="679d0-186">For the line item **ChargeType**, the value **Purchase** is mapped to **New**.</span></span> <span data-ttu-id="679d0-187">Värdets **åter betalning** mappas för att **avbryta**.</span><span class="sxs-lookup"><span data-stu-id="679d0-187">The value **Refund** is mapped to **Cancel**.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="679d0-188">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="679d0-188">Response success and error codes</span></span>

<span data-ttu-id="679d0-189">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="679d0-189">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="679d0-190">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="679d0-190">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="679d0-191">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="679d0-191">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

## <a name="rest-examples"></a><span data-ttu-id="679d0-192">REST-exempel</span><span class="sxs-lookup"><span data-stu-id="679d0-192">REST examples</span></span>

### <a name="request-response-example-1"></a><span data-ttu-id="679d0-193">Request-Response-exempel 1</span><span class="sxs-lookup"><span data-stu-id="679d0-193">Request-response example 1</span></span>

<span data-ttu-id="679d0-194">Detaljerna för det här exemplet på REST-begäran och-svar är följande:</span><span class="sxs-lookup"><span data-stu-id="679d0-194">The details for this example REST request and response are as follows:</span></span>

- <span data-ttu-id="679d0-195">**Provider**: **Databasmigrering**</span><span class="sxs-lookup"><span data-stu-id="679d0-195">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="679d0-196">**InvoiceLineItemType**: **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="679d0-196">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="679d0-197">**Period**: **föregående**</span><span class="sxs-lookup"><span data-stu-id="679d0-197">**Period**: **Previous**</span></span>

#### <a name="request-example-1"></a><span data-ttu-id="679d0-198">Exempel på begäran 1</span><span class="sxs-lookup"><span data-stu-id="679d0-198">Request example 1</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/T000001234/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-1"></a><span data-ttu-id="679d0-199">Svars exempel 1</span><span class="sxs-lookup"><span data-stu-id="679d0-199">Response example 1</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Wed, 20 Feb 2019 19:59:27 GMT

{
    "totalCount": 2,
    "items": [
        {
            "partnerId": "2b8940db-5089-539c-e757-520ed1d1bc88",
            "partnerName": "",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "T000001234",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "Test Test on Windows 2012 R2 (WebHost)",
            "productName": "Test Test on Windows",
            "publisherName": "Test",
            "publisherId": "28503520",
            "subscriptionId": "12345678-9d62-4a85-8fd0-91a87c261bc4",
            "subscriptionDescription": "Subscription 10",
            "chargeStartDate": "2018-11-01T00:00:00Z",
            "chargeEndDate": "2018-12-01T00:00:00Z",
            "usageDate": "2018-11-13T00:00:00Z",
            "meterType": "1 Compute Hour - 1core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "1core",
            "meterSubCategory": "Test Test on Windows",
            "meterName": "Test Test on Windows - Test Test on Windows 2012 R2 (WebHost) - 1 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS2",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "TestWINRG",
            "resourceUri": "/subscriptions/12345678-9d62-4a85-8fd0-91a87c261bc4/resourceGroups/TestWINRG/providers/Microsoft.Compute/virtualMachines/testWinTest",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_B1s\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "new",
            "unitPrice": 0.0209496384791679,
            "quantity": 23.200004,
            "unitType": "1 Hour",
            "billingPreTaxTotal": 0.486031696515249,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 0.486031696515249,
            "pricingCurrency": "USD",
            "creditType": "Credit Not Applied",
            "invoiceLineItemType": "usage_line_items",
            "billingProvider": "marketplace",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
        },
        {
            "partnerId": "2b8940db-5089-539c-e757-520ed1d1bc88",
            "partnerName": "",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "T000001234",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "Test Test on Ubuntu 16.04 (WebHost)",
            "productName": "Test Test on Linux",
            "publisherName": "Test",
            "publisherId": "28503520",
            "subscriptionId": "12345678-9d62-4a85-8fd0-91a87c261bc4",
            "subscriptionDescription": "Subscription 10",
            "chargeStartDate": "2018-11-01T00:00:00Z",
            "chargeEndDate": "2018-12-01T00:00:00Z",
            "usageDate": "2018-11-13T00:00:00Z",
            "meterType": "1 Compute Hour - 1core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "1core",
            "meterSubCategory": "Test Test on Linux",
            "meterName": "Test Test on Linux - Test Test on Ubuntu 16.04 (WebHost) - 1 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "TESTRG",
            "resourceUri": "/subscriptions/12345678-9d62-4a85-8fd0-91a87c261bc4/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/testUbuntuTest",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_B1s\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "new",
            "unitPrice": 0.0209951014286867,
            "quantity": 23.350007,
            "unitType": "1 Hour",
            "billingPreTaxTotal": 0.490235765325545,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 0.490235765325545,
            "pricingCurrency": "USD",
            "entitlementId": "66bada28-271e-4b7a-aaf5-c0ead6312345",
            "entitlementDescription": "Partner Subscription",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "effectiveUnitPrice": 0.1999968000511991808131,
            "rateOfPartnerEarnedCredit": 0,
            "rateOfCredit": 1,
            "creditType": "Azure Credit Applied",
            "invoiceLineItemType": "usage_line_items",
            "billingProvider": "marketplace",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/T000001234/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/T000001234/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000&seekOperation=Next",
            "method": "GET",
            "headers": [
                {
                    "key": "MS-ContinuationToken",
                    "value": "AQAAAA=="
                }
            ]
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="request-response-example-2"></a><span data-ttu-id="679d0-200">Request-Response-exempel 2</span><span class="sxs-lookup"><span data-stu-id="679d0-200">Request-response example 2</span></span>

<span data-ttu-id="679d0-201">Detaljerna för det här exemplet på REST-begäran och-svar är följande:</span><span class="sxs-lookup"><span data-stu-id="679d0-201">The details for this example REST request and response are as follows:</span></span>

- <span data-ttu-id="679d0-202">**Provider**: **Databasmigrering**</span><span class="sxs-lookup"><span data-stu-id="679d0-202">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="679d0-203">**InvoiceLineItemType**: **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="679d0-203">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="679d0-204">**Period**: **föregående**</span><span class="sxs-lookup"><span data-stu-id="679d0-204">**Period**: **Previous**</span></span>
- <span data-ttu-id="679d0-205">**SeekOperation**: **Nästa**</span><span class="sxs-lookup"><span data-stu-id="679d0-205">**SeekOperation**: **Next**</span></span>

#### <a name="request-example-2"></a><span data-ttu-id="679d0-206">Exempel på begäran 2</span><span class="sxs-lookup"><span data-stu-id="679d0-206">Request example 2</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/T000001234/lineitems?provider=onetime&invoiceLineItemType=usagelineitems&currencyCode=usd&period=previous&size=2000&seekoperation=next HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-ContinuationToken: d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

## <a name="response-example-2"></a><span data-ttu-id="679d0-207">Svars exempel 2</span><span class="sxs-lookup"><span data-stu-id="679d0-207">Response example 2</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Wed, 20 Feb 2019 19:59:27 GMT

{
    "totalCount": 1,
    "items": [
          {
            "partnerId": "2b8940db-5089-539c-e757-520ed1d1bc88",
            "partnerName": "",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "T000001234",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "Test Test on Windows 2012 R2 (WebHost)",
            "productName": "Test Test on Windows",
            "publisherName": "Test",
            "publisherId": "28503520",
            "subscriptionId": "12345678-9d62-4a85-8fd0-91a87c261bc4",
            "subscriptionDescription": "Subscription 10",
            "chargeStartDate": "2018-11-01T00:00:00Z",
            "chargeEndDate": "2018-12-01T00:00:00Z",
            "usageDate": "2018-11-13T00:00:00Z",
            "meterType": "1 Compute Hour - 1core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "1core",
            "meterSubCategory": "Test Test on Windows",
            "meterName": "Test Test on Windows - Test Test on Windows 2012 R2 (WebHost) - 1 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS2",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "TestWINRG",
            "resourceUri": "/subscriptions/12345678-9d62-4a85-8fd0-91a87c261bc4/resourceGroups/TestWINRG/providers/Microsoft.Compute/virtualMachines/testWinTest",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_B1s\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "new",
            "unitPrice": 0.0209496384791679,
            "quantity": 23.200004,
            "unitType": "1 Hour",
            "billingPreTaxTotal": 0.486031696515249,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 0.486031696515249,
            "pricingCurrency": "USD",
            "entitlementId": "66bada28-271e-4b7a-aaf5-c0ead6312345",
            "entitlementDescription": "Partner Subscription",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "effectiveUnitPrice": 0.1835431430074643112595,
            "rateOfPartnerEarnedCredit": 0.15,
            "rateOfCredit": 0.15,
            "creditType": "Partner Earned Credit Applied",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
        }
    ],
    "links": {
        "self": {
             "uri": "/invoices/T000001234/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
