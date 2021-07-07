---
title: Hämta fakturaradsobjekt som inte fakturerats för kommersiell förbrukning
description: Du kan hämta en samling ofakturerade radobjekt för en angiven faktura med hjälp av Partner Center-API:erna.
ms.date: 01/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1b7dba3333aaec8df73f0e8147b0bbbc78b9b184
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446154"
---
# <a name="get-invoice-unbilled-commercial-consumption-line-items"></a><span data-ttu-id="4ede1-103">Hämta fakturaradsobjekt som inte fakturerats för kommersiell förbrukning</span><span class="sxs-lookup"><span data-stu-id="4ede1-103">Get invoice unbilled commercial consumption line items</span></span>

<span data-ttu-id="4ede1-104">Så här hämtar du en samling med information om ofakturerade radobjekt för kommersiell förbrukning.</span><span class="sxs-lookup"><span data-stu-id="4ede1-104">How to get a collection of unbilled commercial consumption line item details.</span></span>

<span data-ttu-id="4ede1-105">Du kan använda följande metoder för att hämta en samling information som inte faktureras radobjekt för kommersiell förbrukning (kallas även öppna användningsradsobjekt) programmatiskt.</span><span class="sxs-lookup"><span data-stu-id="4ede1-105">You can use the following methods to get a collection of details unbilled commercial consumption line items (also known as open usage line items) programmatically.</span></span>

>[!NOTE]
><span data-ttu-id="4ede1-106">Daglig beräknad användning tar normalt 24 timmar att visas i Partnercenter eller nås via API:et.</span><span class="sxs-lookup"><span data-stu-id="4ede1-106">Daily-rated usage normally takes 24 hours to appear in Partner Center or to be accessed through the API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4ede1-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="4ede1-107">Prerequisites</span></span>

- <span data-ttu-id="4ede1-108">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="4ede1-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4ede1-109">Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="4ede1-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="4ede1-110">En fakturaidentifierare.</span><span class="sxs-lookup"><span data-stu-id="4ede1-110">An invoice identifier.</span></span> <span data-ttu-id="4ede1-111">Detta identifierar fakturan som radobjekten ska hämtas för.</span><span class="sxs-lookup"><span data-stu-id="4ede1-111">This identifies the invoice for which to retrieve the line items.</span></span>

## <a name="c"></a><span data-ttu-id="4ede1-112">C\#</span><span class="sxs-lookup"><span data-stu-id="4ede1-112">C\#</span></span>

<span data-ttu-id="4ede1-113">Så här hämtar du radobjekten för den angivna fakturan:</span><span class="sxs-lookup"><span data-stu-id="4ede1-113">To get the line items for the specified invoice:</span></span>

1. <span data-ttu-id="4ede1-114">Anropa [**ById-metoden**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) för att få ett gränssnitt till fakturaåtgärder för den angivna fakturan.</span><span class="sxs-lookup"><span data-stu-id="4ede1-114">Call the [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) method to get an interface to invoice operations for the specified invoice.</span></span>

2. <span data-ttu-id="4ede1-115">Anropa metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) för att hämta fakturaobjektet.</span><span class="sxs-lookup"><span data-stu-id="4ede1-115">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the invoice object.</span></span>

<span data-ttu-id="4ede1-116">**Fakturaobjektet** innehåller all information för den angivna fakturan.</span><span class="sxs-lookup"><span data-stu-id="4ede1-116">The **invoice object** contains all of the information for the specified invoice.</span></span> <span data-ttu-id="4ede1-117">**Providern** identifierar källan för den ej fakturerade detaljinformationen (till exempel **OneTime**).</span><span class="sxs-lookup"><span data-stu-id="4ede1-117">The **Provider** identifies the source of the unbilled detail information (for example, **OneTime**).</span></span> <span data-ttu-id="4ede1-118">**InvoiceLineItemType** anger typen (till exempel **UsageLineItem**).</span><span class="sxs-lookup"><span data-stu-id="4ede1-118">The **InvoiceLineItemType** specifies the type (for example, **UsageLineItem**).</span></span>

<span data-ttu-id="4ede1-119">I följande exempelkod används en **foreach-loop** för att bearbeta **samlingen InvoiceLineItems.**</span><span class="sxs-lookup"><span data-stu-id="4ede1-119">The following example code uses a **foreach** loop to process the **InvoiceLineItems** collection.</span></span> <span data-ttu-id="4ede1-120">En separat samling radobjekt hämtas för varje **InvoiceLineItemType**.</span><span class="sxs-lookup"><span data-stu-id="4ede1-120">A separate collection of line items is retrieved for each **InvoiceLineItemType**.</span></span>

<span data-ttu-id="4ede1-121">Så här hämtar du en samling radobjekt som motsvarar en **InvoiceDetail-instans:**</span><span class="sxs-lookup"><span data-stu-id="4ede1-121">To get a collection of line items that correspond to an **InvoiceDetail** instance:</span></span>

1. <span data-ttu-id="4ede1-122">Skicka instansens **BillingProvider och** **InvoiceLineItemType** till [**metoden**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) By.</span><span class="sxs-lookup"><span data-stu-id="4ede1-122">Pass the instance's **BillingProvider** and **InvoiceLineItemType** to the [**By**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) method.</span></span>

2. <span data-ttu-id="4ede1-123">Anropa metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) för att hämta de associerade radobjekten.</span><span class="sxs-lookup"><span data-stu-id="4ede1-123">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the associated line items.</span></span>
3. <span data-ttu-id="4ede1-124">Skapa en uppräkning för att bläddra i samlingen enligt följande exempel.</span><span class="sxs-lookup"><span data-stu-id="4ede1-124">Create an enumerator to traverse the collection as shown in the following example.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string curencyCode;
// string period;
// int pageMaxSizeReconLineItems = 2000;

// all the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

var seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById("unbilled").By("onetime", "usagelineitems", curencyCode, period, pageMaxSizeReconLineItems).Get();

var fetchNext = true;

ConsoleKeyInfo keyInfo;

var itemNumber = 1;
while (fetchNext)
{
    Console.Out.WriteLine("\tLine items count: " + seekBasedResourceCollection.Items.Count());

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
            seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById("unbilled").By("onetime", "usagelineitems", curencyCode, period, pageMaxSizeReconLineItems).Seek(seekBasedResourceCollection.ContinuationToken, SeekOperation.Next);
        }
    }
}
```

<span data-ttu-id="4ede1-125">Ett liknande exempel finns i:</span><span class="sxs-lookup"><span data-stu-id="4ede1-125">For a similar example, see:</span></span>

- <span data-ttu-id="4ede1-126">Exempel: [Konsoltestapp](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="4ede1-126">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="4ede1-127">Project: **Partnercenter-SDK exempel**</span><span class="sxs-lookup"><span data-stu-id="4ede1-127">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="4ede1-128">Klass: **GetUnBilledConsumptionReconLineItemsPaging.cs**</span><span class="sxs-lookup"><span data-stu-id="4ede1-128">Class: **GetUnBilledConsumptionReconLineItemsPaging.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="4ede1-129">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="4ede1-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4ede1-130">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="4ede1-130">Request syntax</span></span>

<span data-ttu-id="4ede1-131">Du kan använda följande syntaxer för DIN REST-begäran, beroende på ditt användningsfall.</span><span class="sxs-lookup"><span data-stu-id="4ede1-131">You can use the following syntaxes for your REST request, depending on your use case.</span></span> <span data-ttu-id="4ede1-132">Mer information finns i beskrivningarna för varje syntax.</span><span class="sxs-lookup"><span data-stu-id="4ede1-132">For more information, see the descriptions for each syntax.</span></span>

| <span data-ttu-id="4ede1-133">Metod</span><span class="sxs-lookup"><span data-stu-id="4ede1-133">Method</span></span>  | <span data-ttu-id="4ede1-134">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="4ede1-134">Request URI</span></span>                                                                                                                                                                                              | <span data-ttu-id="4ede1-135">Beskrivning av syntaxanvändningsfall</span><span class="sxs-lookup"><span data-stu-id="4ede1-135">Description of syntax use case</span></span>                                                                                                     |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="4ede1-136">**Få**</span><span class="sxs-lookup"><span data-stu-id="4ede1-136">**GET**</span></span> | <span data-ttu-id="4ede1-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="4ede1-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period} HTTP/1.1</span></span>                       | <span data-ttu-id="4ede1-138">Använd den här syntaxen för att returnera en fullständig lista över varje radobjekt för den angivna fakturan.</span><span class="sxs-lookup"><span data-stu-id="4ede1-138">Use this syntax to return a full list of every line item for the given invoice.</span></span>                                                    |
| <span data-ttu-id="4ede1-139">**Få**</span><span class="sxs-lookup"><span data-stu-id="4ede1-139">**GET**</span></span> | <span data-ttu-id="4ede1-140">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period}&size={size} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="4ede1-140">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period}&size={size} HTTP/1.1</span></span>           | <span data-ttu-id="4ede1-141">Använd den här syntaxen för stora fakturor.</span><span class="sxs-lookup"><span data-stu-id="4ede1-141">Use this syntax for large invoices.</span></span> <span data-ttu-id="4ede1-142">Använd den här syntaxen med en angiven storlek och 0-baserad förskjutning för att returnera en sidad lista med radobjekt.</span><span class="sxs-lookup"><span data-stu-id="4ede1-142">Use this syntax with a specified size and 0-based offset to return a paged list of line items.</span></span> |
| <span data-ttu-id="4ede1-143">**Få**</span><span class="sxs-lookup"><span data-stu-id="4ede1-143">**GET**</span></span> | <span data-ttu-id="4ede1-144">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period}&size={size}&seekOperation=Next</span><span class="sxs-lookup"><span data-stu-id="4ede1-144">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period}&size={size}&seekOperation=Next</span></span> | <span data-ttu-id="4ede1-145">Använd den här syntaxen för att hämta nästa sida med avstämningsradobjekt med hjälp av `seekOperation = "Next"` .</span><span class="sxs-lookup"><span data-stu-id="4ede1-145">Use this syntax to get the next page of reconciliation line items using `seekOperation = "Next"`.</span></span>                                  |

#### <a name="uri-parameters"></a><span data-ttu-id="4ede1-146">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="4ede1-146">URI parameters</span></span>

<span data-ttu-id="4ede1-147">Använd följande URI- och frågeparametrar när du skapar begäran.</span><span class="sxs-lookup"><span data-stu-id="4ede1-147">Use the following URI and query parameters when creating the request.</span></span>

| <span data-ttu-id="4ede1-148">Namn</span><span class="sxs-lookup"><span data-stu-id="4ede1-148">Name</span></span>                   | <span data-ttu-id="4ede1-149">Typ</span><span class="sxs-lookup"><span data-stu-id="4ede1-149">Type</span></span>   | <span data-ttu-id="4ede1-150">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="4ede1-150">Required</span></span> | <span data-ttu-id="4ede1-151">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="4ede1-151">Description</span></span>                                                                                                                                                                                                                                |
|------------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="4ede1-152">Leverantör</span><span class="sxs-lookup"><span data-stu-id="4ede1-152">provider</span></span>               | <span data-ttu-id="4ede1-153">sträng</span><span class="sxs-lookup"><span data-stu-id="4ede1-153">string</span></span> | <span data-ttu-id="4ede1-154">Ja</span><span class="sxs-lookup"><span data-stu-id="4ede1-154">Yes</span></span>      | <span data-ttu-id="4ede1-155">Providern: "**OneTime**".</span><span class="sxs-lookup"><span data-stu-id="4ede1-155">The provider: "**OneTime**".</span></span>                                                                                                                                                                                                               |
| <span data-ttu-id="4ede1-156">invoice-line-item-type</span><span class="sxs-lookup"><span data-stu-id="4ede1-156">invoice-line-item-type</span></span> | <span data-ttu-id="4ede1-157">sträng</span><span class="sxs-lookup"><span data-stu-id="4ede1-157">string</span></span> | <span data-ttu-id="4ede1-158">Ja</span><span class="sxs-lookup"><span data-stu-id="4ede1-158">Yes</span></span>      | <span data-ttu-id="4ede1-159">Typ av fakturainformation: "**UsageLineItems**", "**UsageLineItems**".</span><span class="sxs-lookup"><span data-stu-id="4ede1-159">The type of invoice detail: "**UsageLineItems**", "**UsageLineItems**".</span></span>                                                                                                                                                                    |
| <span data-ttu-id="4ede1-160">currencyCode</span><span class="sxs-lookup"><span data-stu-id="4ede1-160">currencyCode</span></span>           | <span data-ttu-id="4ede1-161">sträng</span><span class="sxs-lookup"><span data-stu-id="4ede1-161">string</span></span> | <span data-ttu-id="4ede1-162">Ja</span><span class="sxs-lookup"><span data-stu-id="4ede1-162">Yes</span></span>      | <span data-ttu-id="4ede1-163">Valutakoden för de ej fakturerade radobjekten.</span><span class="sxs-lookup"><span data-stu-id="4ede1-163">The currency code for the unbilled line items.</span></span>                                                                                                                                                                                             |
| <span data-ttu-id="4ede1-164">period</span><span class="sxs-lookup"><span data-stu-id="4ede1-164">period</span></span>                 | <span data-ttu-id="4ede1-165">sträng</span><span class="sxs-lookup"><span data-stu-id="4ede1-165">string</span></span> | <span data-ttu-id="4ede1-166">Ja</span><span class="sxs-lookup"><span data-stu-id="4ede1-166">Yes</span></span>      | <span data-ttu-id="4ede1-167">Perioden för ej fakturerad rekognosering (till **exempel** aktuell , **tidigare**).</span><span class="sxs-lookup"><span data-stu-id="4ede1-167">The period for unbilled recon (for example: **current**, **previous**).</span></span> <span data-ttu-id="4ede1-168">Anta att du behöver fråga dina ofakturerade användningsdata för faktureringsperioden (01/01/2020 – 01/31/2020) i januari och välja period **som "Aktuell"** annars **"Föregående".**</span><span class="sxs-lookup"><span data-stu-id="4ede1-168">Suppose you need to query your unbilled usage data of the billing cycle (01/01/2020 – 01/31/2020) in January, choose period as **"Current,"** else **"Previous."**</span></span> |
| <span data-ttu-id="4ede1-169">ikoner</span><span class="sxs-lookup"><span data-stu-id="4ede1-169">size</span></span>                   | <span data-ttu-id="4ede1-170">antal</span><span class="sxs-lookup"><span data-stu-id="4ede1-170">number</span></span> | <span data-ttu-id="4ede1-171">Inga</span><span class="sxs-lookup"><span data-stu-id="4ede1-171">No</span></span>       | <span data-ttu-id="4ede1-172">Det maximala antalet objekt som ska returneras.</span><span class="sxs-lookup"><span data-stu-id="4ede1-172">The maximum number of items to return.</span></span> <span data-ttu-id="4ede1-173">Standardstorleken är 2 000.</span><span class="sxs-lookup"><span data-stu-id="4ede1-173">The default size is 2000.</span></span>                                                                                                                                                                           |
| <span data-ttu-id="4ede1-174">seekOperation</span><span class="sxs-lookup"><span data-stu-id="4ede1-174">seekOperation</span></span>          | <span data-ttu-id="4ede1-175">sträng</span><span class="sxs-lookup"><span data-stu-id="4ede1-175">string</span></span> | <span data-ttu-id="4ede1-176">No</span><span class="sxs-lookup"><span data-stu-id="4ede1-176">No</span></span>       | <span data-ttu-id="4ede1-177">Ange `seekOperation=Next` för att hämta nästa sida med avstämningsradsobjekt.</span><span class="sxs-lookup"><span data-stu-id="4ede1-177">Set `seekOperation=Next` to get the next page of reconciliation line items.</span></span>                                                                                                                                                                |

### <a name="request-headers"></a><span data-ttu-id="4ede1-178">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="4ede1-178">Request headers</span></span>

<span data-ttu-id="4ede1-179">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="4ede1-179">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4ede1-180">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="4ede1-180">Request body</span></span>

<span data-ttu-id="4ede1-181">Inga.</span><span class="sxs-lookup"><span data-stu-id="4ede1-181">None.</span></span>

## <a name="rest-response"></a><span data-ttu-id="4ede1-182">REST-svar</span><span class="sxs-lookup"><span data-stu-id="4ede1-182">REST response</span></span>

<span data-ttu-id="4ede1-183">Om det lyckas innehåller svaret information om samlingen med radobjekt.</span><span class="sxs-lookup"><span data-stu-id="4ede1-183">If successful, the response contains the collection of line item details.</span></span>

<span data-ttu-id="4ede1-184">*För radobjektet **ChargeType** mappas värdet **Purchase** till **New (Nytt)** och värdet **Refund (Återbetalning)** mappas till **Cancel (Avbryt).***</span><span class="sxs-lookup"><span data-stu-id="4ede1-184">*For the line item **ChargeType**, the value **Purchase** is mapped to **New** and the value **Refund** is mapped to **Cancel**.*</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4ede1-185">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="4ede1-185">Response success and error codes</span></span>

<span data-ttu-id="4ede1-186">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="4ede1-186">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4ede1-187">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="4ede1-187">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="4ede1-188">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="4ede1-188">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

## <a name="request-response-examples"></a><span data-ttu-id="4ede1-189">Exempel på begäran-svar</span><span class="sxs-lookup"><span data-stu-id="4ede1-189">Request-response examples</span></span>

### <a name="request-response-example-1"></a><span data-ttu-id="4ede1-190">Exempel på begäran-svar 1</span><span class="sxs-lookup"><span data-stu-id="4ede1-190">Request-response example 1</span></span>

<span data-ttu-id="4ede1-191">Följande information gäller för det här exemplet:</span><span class="sxs-lookup"><span data-stu-id="4ede1-191">The following details apply to this example:</span></span>

- <span data-ttu-id="4ede1-192">**Provider:** **OneTime**</span><span class="sxs-lookup"><span data-stu-id="4ede1-192">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="4ede1-193">**InvoiceLineItemType:** **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="4ede1-193">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="4ede1-194">**Period**: **Föregående**</span><span class="sxs-lookup"><span data-stu-id="4ede1-194">**Period**: **Previous**</span></span>

#### <a name="request-example-1"></a><span data-ttu-id="4ede1-195">Exempel på begäran 1</span><span class="sxs-lookup"><span data-stu-id="4ede1-195">Request example 1</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1//invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

### <a name="response-example-1"></a><span data-ttu-id="4ede1-196">Svarsexempel 1</span><span class="sxs-lookup"><span data-stu-id="4ede1-196">Response example 1</span></span>

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
            "partnerId": "00083575-bbd0-54de-b2ad-0f5b0e927d71",
            "partnerName": "MTBC",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "VM-Series Next-Generation Firewall (Bundle 2 PAYG)",
            "productName": "VM-Series Next Generation Firewall",
            "publisherName": "Test Alto Networks, Inc.",
            "publisherId": "",
            "subscriptionId": "12345678-04d9-421c-baf8-e3b8dd62ddba",
            "subscriptionDescription": "Pay-As-You-Go",
            "chargeStartDate": "2019-01-01T00:00:00Z",
            "chargeEndDate": "2019-02-01T00:00:00Z",
            "usageDate": "2019-01-01T00:00:00Z",
            "meterType": "1 Compute Hour - 4core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "4core",
            "meterSubCategory": "VM-Series Next Generation Firewall",
            "meterName": "VM-Series Next Generation Firewall - VM-Series Next-Generation Firewall (Bundle 2 PAYG) - 4 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "ECH-PAN-RG",
            "resourceUri": "/subscriptions/12345678-04d9-421c-baf8-e3b8dd62ddba/resourceGroups/ECH-PAN-RG/providers/Microsoft.Compute/virtualMachines/echpanfw",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_D3_v2\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "",
            "unitPrice": 1.2799888920023,
            "quantity": 24.0,
            "unitType": "",
            "billingPreTaxTotal": 30.7197334080551,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 30.7197334080551,
            "pricingCurrency": "USD",
            "entitlementId": "1234547f-b249-4edd-9319-637862d8c0b4",
            "entitlementDescription": "Partner Subscription",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "effectiveUnitPrice": 0,
            "rateOfPartnerEarnedCredit": 0,
            "rateOfCredit": 0,
            "creditType": "Credit Not Applied",
            "invoiceLineItemType": "usage_line_items",
            "billingProvider": "marketplace",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
         },
         {
            "partnerId": "00083575-bbd0-54de-b2ad-0f5b0e927d71",
            "partnerName": "MTBC",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "VM-Series Next-Generation Firewall (Bundle 2 PAYG)",
            "productName": "VM-Series Next Generation Firewall",
            "publisherName": "Test Alto Networks, Inc.",
            "publisherId": "",
            "subscriptionId": "12345678-04d9-421c-baf8-e3b8dd62ddba",
            "subscriptionDescription": "Pay-As-You-Go",
            "chargeStartDate": "2019-01-01T00:00:00Z",
            "chargeEndDate": "2019-02-01T00:00:00Z",
            "usageDate": "2019-01-02T00:00:00Z",
            "meterType": "1 Compute Hour - 4core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "4core",
            "meterSubCategory": "VM-Series Next Generation Firewall",
            "meterName": "VM-Series Next Generation Firewall - VM-Series Next-Generation Firewall (Bundle 2 PAYG) - 4 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "ECH-PAN-RG",
            "resourceUri": "/subscriptions/12345678-04d9-421c-baf8-e3b8dd62ddba/resourceGroups/ECH-PAN-RG/providers/Microsoft.Compute/virtualMachines/echpanfw",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_D3_v2\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "",
            "unitPrice": 1.2799888920023,
            "quantity": 24.0,
            "unitType": "",
            "billingPreTaxTotal": 30.7197334080551,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 30.7197334080551,
            "pricingCurrency": "USD",
            "entitlementId": "31cdf47f-b249-4edd-9319-637862d12345",
            "entitlementDescription": "Partner Subscription",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "effectiveUnitPrice": 0,
            "rateOfPartnerEarnedCredit": 0,
            "rateOfCredit": 1,
            "creditType": "Azure Credit Applied",
            "invoiceLineItemTypce": "usage_line_items",
            "billingProvider": "marketplace",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000&seekOperation=Next",
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

### <a name="request-response-example-2"></a><span data-ttu-id="4ede1-197">Exempel på begäran-svar 2</span><span class="sxs-lookup"><span data-stu-id="4ede1-197">Request-response example 2</span></span>

<span data-ttu-id="4ede1-198">Följande information gäller för det här exemplet:</span><span class="sxs-lookup"><span data-stu-id="4ede1-198">The following details apply to this example:</span></span>

- <span data-ttu-id="4ede1-199">**Provider:** **OneTime**</span><span class="sxs-lookup"><span data-stu-id="4ede1-199">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="4ede1-200">**InvoiceLineItemType:** **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="4ede1-200">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="4ede1-201">**Period**: **Föregående**</span><span class="sxs-lookup"><span data-stu-id="4ede1-201">**Period**: **Previous**</span></span>
- <span data-ttu-id="4ede1-202">**SeekOperation:** **Nästa**</span><span class="sxs-lookup"><span data-stu-id="4ede1-202">**SeekOperation**: **Next**</span></span>

#### <a name="request-example-2"></a><span data-ttu-id="4ede1-203">Exempel på begäran 2</span><span class="sxs-lookup"><span data-stu-id="4ede1-203">Request example 2</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/unbilled/lineitems?provider=onetime&invoiceLineItemType=usagelineitems&currencyCode=usd&period=previous&size=2000&seekoperation=next HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-ContinuationToken: d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-2"></a><span data-ttu-id="4ede1-204">Svarsexempel 2</span><span class="sxs-lookup"><span data-stu-id="4ede1-204">Response example 2</span></span>

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
            "partnerId": "00083575-bbd0-54de-b2ad-0f5b0e927d71",
            "partnerName": "MTBC",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "VM-Series Next-Generation Firewall (Bundle 2 PAYG)",
            "productName": "VM-Series Next Generation Firewall",
            "publisherName": "Test Alto Networks, Inc.",
            "publisherId": "",
            "subscriptionId": "12345678-04d9-421c-baf8-e3b8dd62ddba",
            "subscriptionDescription": "Pay-As-You-Go",
            "chargeStartDate": "2019-01-01T00:00:00Z",
            "chargeEndDate": "2019-02-01T00:00:00Z",
            "usageDate": "2019-01-02T00:00:00Z",
            "meterType": "1 Compute Hour - 4core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "4core",
            "meterSubCategory": "VM-Series Next Generation Firewall",
            "meterName": "VM-Series Next Generation Firewall - VM-Series Next-Generation Firewall (Bundle 2 PAYG) - 4 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "ECH-PAN-RG",
            "resourceUri": "/subscriptions/12345678-04d9-421c-baf8-e3b8dd62ddba/resourceGroups/ECH-PAN-RG/providers/Microsoft.Compute/virtualMachines/echpanfw",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_D3_v2\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "",
            "unitPrice": 1.2799888920023,
            "quantity": 24.0,
            "unitType": "",
            "billingPreTaxTotal": 30.7197334080551,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 30.7197334080551,
            "pricingCurrency": "USD",
            "entitlementId": "31cdf47f-b249-4edd-9319-637862d8c0b4",
            "entitlementDescription": "Partner Subscription",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "effectiveUnitPrice": 0,
            "rateOfPartnerEarnedCredit": 0.15,
            "rateOfCredit": 0.15,
            "creditType": "Partner Earned Credit Applied",
            "invoiceLineItemType": "usage_line_items",
            "billingProvider": "marketplace",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
        }
    ],
    "links": {
        "self": {
             "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
