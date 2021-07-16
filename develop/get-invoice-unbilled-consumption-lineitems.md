---
title: Hämta fakturaradsobjekt som inte fakturerats för kommersiell förbrukning
description: Du kan hämta en samling ofakturerade radobjekt för en angiven faktura med hjälp av Partner Center-API:erna.
ms.date: 01/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f7c74bedfd6412fc5954ed2ddc1388936e418fa3
ms.sourcegitcommit: 722992eea6f8ea366dc088e5dd1ee63c17d56f61
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/15/2021
ms.locfileid: "114224776"
---
# <a name="get-invoice-unbilled-commercial-consumption-line-items"></a><span data-ttu-id="a7978-103">Hämta fakturaradsobjekt som inte fakturerats för kommersiell förbrukning</span><span class="sxs-lookup"><span data-stu-id="a7978-103">Get invoice unbilled commercial consumption line items</span></span>

<span data-ttu-id="a7978-104">Så här hämtar du en samling med information om ofakturerade radobjekt för kommersiell förbrukning.</span><span class="sxs-lookup"><span data-stu-id="a7978-104">How to get a collection of unbilled commercial consumption line item details.</span></span>

<span data-ttu-id="a7978-105">Du kan använda följande metoder för att hämta en samling information som inte faktureras radobjekt för kommersiell förbrukning (kallas även öppna användningsradsobjekt) programmatiskt.</span><span class="sxs-lookup"><span data-stu-id="a7978-105">You can use the following methods to get a collection of details unbilled commercial consumption line items (also known as open usage line items) programmatically.</span></span>

>[!NOTE]
><span data-ttu-id="a7978-106">Daglig beräknad användning tar normalt 24 timmar att visas i Partnercenter eller nås via API:et.</span><span class="sxs-lookup"><span data-stu-id="a7978-106">Daily-rated usage normally takes 24 hours to appear in Partner Center or to be accessed through the API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7978-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="a7978-107">Prerequisites</span></span>

- <span data-ttu-id="a7978-108">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="a7978-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a7978-109">Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="a7978-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="a7978-110">C\#</span><span class="sxs-lookup"><span data-stu-id="a7978-110">C\#</span></span>

<span data-ttu-id="a7978-111">Så här hämtar du radobjekten för den angivna fakturan:</span><span class="sxs-lookup"><span data-stu-id="a7978-111">To get the line items for the specified invoice:</span></span>

1. <span data-ttu-id="a7978-112">Anropa [**ById-metoden**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) för att få ett gränssnitt till fakturaåtgärder för den angivna fakturan.</span><span class="sxs-lookup"><span data-stu-id="a7978-112">Call the [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) method to get an interface to invoice operations for the specified invoice.</span></span>

2. <span data-ttu-id="a7978-113">Anropa metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) för att hämta fakturaobjektet.</span><span class="sxs-lookup"><span data-stu-id="a7978-113">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the invoice object.</span></span>

<span data-ttu-id="a7978-114">**Fakturaobjektet** innehåller all information för den angivna fakturan.</span><span class="sxs-lookup"><span data-stu-id="a7978-114">The **invoice object** contains all of the information for the specified invoice.</span></span> <span data-ttu-id="a7978-115">**Providern** identifierar källan för den ej fakturerade detaljinformationen (till exempel **OneTime**).</span><span class="sxs-lookup"><span data-stu-id="a7978-115">The **Provider** identifies the source of the unbilled detail information (for example, **OneTime**).</span></span> <span data-ttu-id="a7978-116">**InvoiceLineItemType** anger typen (till exempel **UsageLineItem**).</span><span class="sxs-lookup"><span data-stu-id="a7978-116">The **InvoiceLineItemType** specifies the type (for example, **UsageLineItem**).</span></span>

<span data-ttu-id="a7978-117">I följande exempelkod används en **foreach-loop** för att bearbeta **samlingen InvoiceLineItems.**</span><span class="sxs-lookup"><span data-stu-id="a7978-117">The following example code uses a **foreach** loop to process the **InvoiceLineItems** collection.</span></span> <span data-ttu-id="a7978-118">En separat samling radobjekt hämtas för varje **InvoiceLineItemType**.</span><span class="sxs-lookup"><span data-stu-id="a7978-118">A separate collection of line items is retrieved for each **InvoiceLineItemType**.</span></span>

<span data-ttu-id="a7978-119">Så här hämtar du en samling radobjekt som motsvarar en **InvoiceDetail-instans:**</span><span class="sxs-lookup"><span data-stu-id="a7978-119">To get a collection of line items that correspond to an **InvoiceDetail** instance:</span></span>

1. <span data-ttu-id="a7978-120">Skicka instansens **BillingProvider och** **InvoiceLineItemType** till [**metoden**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) By.</span><span class="sxs-lookup"><span data-stu-id="a7978-120">Pass the instance's **BillingProvider** and **InvoiceLineItemType** to the [**By**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) method.</span></span>

2. <span data-ttu-id="a7978-121">Anropa metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) för att hämta de associerade radobjekten.</span><span class="sxs-lookup"><span data-stu-id="a7978-121">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the associated line items.</span></span>
3. <span data-ttu-id="a7978-122">Skapa en uppräkning för att bläddra i samlingen enligt följande exempel.</span><span class="sxs-lookup"><span data-stu-id="a7978-122">Create an enumerator to traverse the collection as shown in the following example.</span></span>

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

<span data-ttu-id="a7978-123">Ett liknande exempel finns i:</span><span class="sxs-lookup"><span data-stu-id="a7978-123">For a similar example, see:</span></span>

- <span data-ttu-id="a7978-124">Exempel: [Konsoltestapp](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="a7978-124">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="a7978-125">Project: **Partnercenter-SDK exempel**</span><span class="sxs-lookup"><span data-stu-id="a7978-125">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="a7978-126">Klass: **GetUnBilledConsumptionReconLineItemsPaging.cs**</span><span class="sxs-lookup"><span data-stu-id="a7978-126">Class: **GetUnBilledConsumptionReconLineItemsPaging.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="a7978-127">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="a7978-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a7978-128">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="a7978-128">Request syntax</span></span>

<span data-ttu-id="a7978-129">Du kan använda följande syntaxer för DIN REST-begäran, beroende på ditt användningsfall.</span><span class="sxs-lookup"><span data-stu-id="a7978-129">You can use the following syntaxes for your REST request, depending on your use case.</span></span> <span data-ttu-id="a7978-130">Mer information finns i beskrivningarna för varje syntax.</span><span class="sxs-lookup"><span data-stu-id="a7978-130">For more information, see the descriptions for each syntax.</span></span>

| <span data-ttu-id="a7978-131">Metod</span><span class="sxs-lookup"><span data-stu-id="a7978-131">Method</span></span>  | <span data-ttu-id="a7978-132">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="a7978-132">Request URI</span></span>                                                                                                                                                                                              | <span data-ttu-id="a7978-133">Beskrivning av syntaxanvändningsfall</span><span class="sxs-lookup"><span data-stu-id="a7978-133">Description of syntax use case</span></span>                                                                                                     |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a7978-134">**Få**</span><span class="sxs-lookup"><span data-stu-id="a7978-134">**GET**</span></span> | <span data-ttu-id="a7978-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="a7978-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period} HTTP/1.1</span></span>                       | <span data-ttu-id="a7978-136">Använd den här syntaxen för att returnera en fullständig lista över varje radobjekt för den angivna fakturan.</span><span class="sxs-lookup"><span data-stu-id="a7978-136">Use this syntax to return a full list of every line item for the given invoice.</span></span>                                                    |
| <span data-ttu-id="a7978-137">**Få**</span><span class="sxs-lookup"><span data-stu-id="a7978-137">**GET**</span></span> | <span data-ttu-id="a7978-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period}&size={size} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="a7978-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period}&size={size} HTTP/1.1</span></span>           | <span data-ttu-id="a7978-139">Använd den här syntaxen för stora fakturor.</span><span class="sxs-lookup"><span data-stu-id="a7978-139">Use this syntax for large invoices.</span></span> <span data-ttu-id="a7978-140">Använd den här syntaxen med en angiven storlek och 0-baserad förskjutning för att returnera en sidad lista med radobjekt.</span><span class="sxs-lookup"><span data-stu-id="a7978-140">Use this syntax with a specified size and 0-based offset to return a paged list of line items.</span></span> |
| <span data-ttu-id="a7978-141">**Få**</span><span class="sxs-lookup"><span data-stu-id="a7978-141">**GET**</span></span> | <span data-ttu-id="a7978-142">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period}&size={size}&seekOperation=Next</span><span class="sxs-lookup"><span data-stu-id="a7978-142">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period}&size={size}&seekOperation=Next</span></span> | <span data-ttu-id="a7978-143">Använd den här syntaxen för att hämta nästa sida med avstämningsradobjekt med hjälp av `seekOperation = "Next"` .</span><span class="sxs-lookup"><span data-stu-id="a7978-143">Use this syntax to get the next page of reconciliation line items using `seekOperation = "Next"`.</span></span>                                  |

#### <a name="uri-parameters"></a><span data-ttu-id="a7978-144">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="a7978-144">URI parameters</span></span>

<span data-ttu-id="a7978-145">Använd följande URI- och frågeparametrar när du skapar begäran.</span><span class="sxs-lookup"><span data-stu-id="a7978-145">Use the following URI and query parameters when creating the request.</span></span>

| <span data-ttu-id="a7978-146">Namn</span><span class="sxs-lookup"><span data-stu-id="a7978-146">Name</span></span>                   | <span data-ttu-id="a7978-147">Typ</span><span class="sxs-lookup"><span data-stu-id="a7978-147">Type</span></span>   | <span data-ttu-id="a7978-148">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="a7978-148">Required</span></span> | <span data-ttu-id="a7978-149">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="a7978-149">Description</span></span>                                                                                                                                                                                                                                |
|------------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a7978-150">Leverantör</span><span class="sxs-lookup"><span data-stu-id="a7978-150">provider</span></span>               | <span data-ttu-id="a7978-151">sträng</span><span class="sxs-lookup"><span data-stu-id="a7978-151">string</span></span> | <span data-ttu-id="a7978-152">Yes</span><span class="sxs-lookup"><span data-stu-id="a7978-152">Yes</span></span>      | <span data-ttu-id="a7978-153">Providern: "**OneTime**".</span><span class="sxs-lookup"><span data-stu-id="a7978-153">The provider: "**OneTime**".</span></span>                                                                                                                                                                                                               |
| <span data-ttu-id="a7978-154">invoice-line-item-type</span><span class="sxs-lookup"><span data-stu-id="a7978-154">invoice-line-item-type</span></span> | <span data-ttu-id="a7978-155">sträng</span><span class="sxs-lookup"><span data-stu-id="a7978-155">string</span></span> | <span data-ttu-id="a7978-156">Yes</span><span class="sxs-lookup"><span data-stu-id="a7978-156">Yes</span></span>      | <span data-ttu-id="a7978-157">Typ av fakturainformation: "**UsageLineItems**", "**UsageLineItems**".</span><span class="sxs-lookup"><span data-stu-id="a7978-157">The type of invoice detail: "**UsageLineItems**", "**UsageLineItems**".</span></span>                                                                                                                                                                    |
| <span data-ttu-id="a7978-158">currencyCode</span><span class="sxs-lookup"><span data-stu-id="a7978-158">currencyCode</span></span>           | <span data-ttu-id="a7978-159">sträng</span><span class="sxs-lookup"><span data-stu-id="a7978-159">string</span></span> | <span data-ttu-id="a7978-160">Yes</span><span class="sxs-lookup"><span data-stu-id="a7978-160">Yes</span></span>      | <span data-ttu-id="a7978-161">Valutakoden för de ej fakturerade radobjekten.</span><span class="sxs-lookup"><span data-stu-id="a7978-161">The currency code for the unbilled line items.</span></span>                                                                                                                                                                                             |
| <span data-ttu-id="a7978-162">period</span><span class="sxs-lookup"><span data-stu-id="a7978-162">period</span></span>                 | <span data-ttu-id="a7978-163">sträng</span><span class="sxs-lookup"><span data-stu-id="a7978-163">string</span></span> | <span data-ttu-id="a7978-164">Yes</span><span class="sxs-lookup"><span data-stu-id="a7978-164">Yes</span></span>      | <span data-ttu-id="a7978-165">Perioden för ej fakturerad rekognosering (till **exempel** aktuell , **tidigare**).</span><span class="sxs-lookup"><span data-stu-id="a7978-165">The period for unbilled recon (for example: **current**, **previous**).</span></span> <span data-ttu-id="a7978-166">Anta att du behöver fråga dina ofakturerade användningsdata för faktureringsperioden (01/01/2020 – 01/31/2020) i januari och välja period **som "Aktuell"** annars **"Föregående".**</span><span class="sxs-lookup"><span data-stu-id="a7978-166">Suppose you need to query your unbilled usage data of the billing cycle (01/01/2020 – 01/31/2020) in January, choose period as **"Current,"** else **"Previous."**</span></span> |
| <span data-ttu-id="a7978-167">ikoner</span><span class="sxs-lookup"><span data-stu-id="a7978-167">size</span></span>                   | <span data-ttu-id="a7978-168">antal</span><span class="sxs-lookup"><span data-stu-id="a7978-168">number</span></span> | <span data-ttu-id="a7978-169">No</span><span class="sxs-lookup"><span data-stu-id="a7978-169">No</span></span>       | <span data-ttu-id="a7978-170">Det maximala antalet objekt som ska returneras.</span><span class="sxs-lookup"><span data-stu-id="a7978-170">The maximum number of items to return.</span></span> <span data-ttu-id="a7978-171">Standardstorleken är 2 000.</span><span class="sxs-lookup"><span data-stu-id="a7978-171">The default size is 2000.</span></span>                                                                                                                                                                           |
| <span data-ttu-id="a7978-172">seekOperation</span><span class="sxs-lookup"><span data-stu-id="a7978-172">seekOperation</span></span>          | <span data-ttu-id="a7978-173">sträng</span><span class="sxs-lookup"><span data-stu-id="a7978-173">string</span></span> | <span data-ttu-id="a7978-174">No</span><span class="sxs-lookup"><span data-stu-id="a7978-174">No</span></span>       | <span data-ttu-id="a7978-175">Ange `seekOperation=Next` för att hämta nästa sida med avstämningsradsobjekt.</span><span class="sxs-lookup"><span data-stu-id="a7978-175">Set `seekOperation=Next` to get the next page of reconciliation line items.</span></span>                                                                                                                                                                |

### <a name="request-headers"></a><span data-ttu-id="a7978-176">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="a7978-176">Request headers</span></span>

<span data-ttu-id="a7978-177">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="a7978-177">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a7978-178">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="a7978-178">Request body</span></span>

<span data-ttu-id="a7978-179">Inga.</span><span class="sxs-lookup"><span data-stu-id="a7978-179">None.</span></span>

## <a name="rest-response"></a><span data-ttu-id="a7978-180">REST-svar</span><span class="sxs-lookup"><span data-stu-id="a7978-180">REST response</span></span>

<span data-ttu-id="a7978-181">Om det lyckas innehåller svaret information om samlingen med radobjekt.</span><span class="sxs-lookup"><span data-stu-id="a7978-181">If successful, the response contains the collection of line item details.</span></span>

<span data-ttu-id="a7978-182">*För radobjektet **ChargeType** mappas värdet **Purchase** till **New (Nytt)** och värdet **Refund (Återbetalning)** mappas till **Cancel (Avbryt).***</span><span class="sxs-lookup"><span data-stu-id="a7978-182">*For the line item **ChargeType**, the value **Purchase** is mapped to **New** and the value **Refund** is mapped to **Cancel**.*</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a7978-183">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="a7978-183">Response success and error codes</span></span>

<span data-ttu-id="a7978-184">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="a7978-184">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a7978-185">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="a7978-185">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a7978-186">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="a7978-186">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

## <a name="request-response-examples"></a><span data-ttu-id="a7978-187">Exempel på begäran-svar</span><span class="sxs-lookup"><span data-stu-id="a7978-187">Request-response examples</span></span>

### <a name="request-response-example-1"></a><span data-ttu-id="a7978-188">Exempel på begäran-svar 1</span><span class="sxs-lookup"><span data-stu-id="a7978-188">Request-response example 1</span></span>

<span data-ttu-id="a7978-189">Följande information gäller för det här exemplet:</span><span class="sxs-lookup"><span data-stu-id="a7978-189">The following details apply to this example:</span></span>

- <span data-ttu-id="a7978-190">**Provider:** **OneTime**</span><span class="sxs-lookup"><span data-stu-id="a7978-190">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="a7978-191">**InvoiceLineItemType:** **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="a7978-191">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="a7978-192">**Period**: **Föregående**</span><span class="sxs-lookup"><span data-stu-id="a7978-192">**Period**: **Previous**</span></span>

#### <a name="request-example-1"></a><span data-ttu-id="a7978-193">Exempel på begäran 1</span><span class="sxs-lookup"><span data-stu-id="a7978-193">Request example 1</span></span>

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

### <a name="response-example-1"></a><span data-ttu-id="a7978-194">Svarsexempel 1</span><span class="sxs-lookup"><span data-stu-id="a7978-194">Response example 1</span></span>

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

### <a name="request-response-example-2"></a><span data-ttu-id="a7978-195">Exempel på begäran-svar 2</span><span class="sxs-lookup"><span data-stu-id="a7978-195">Request-response example 2</span></span>

<span data-ttu-id="a7978-196">Följande information gäller för det här exemplet:</span><span class="sxs-lookup"><span data-stu-id="a7978-196">The following details apply to this example:</span></span>

- <span data-ttu-id="a7978-197">**Provider:** **OneTime**</span><span class="sxs-lookup"><span data-stu-id="a7978-197">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="a7978-198">**InvoiceLineItemType:** **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="a7978-198">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="a7978-199">**Period**: **Föregående**</span><span class="sxs-lookup"><span data-stu-id="a7978-199">**Period**: **Previous**</span></span>
- <span data-ttu-id="a7978-200">**SeekOperation:** **Nästa**</span><span class="sxs-lookup"><span data-stu-id="a7978-200">**SeekOperation**: **Next**</span></span>

#### <a name="request-example-2"></a><span data-ttu-id="a7978-201">Exempel på begäran 2</span><span class="sxs-lookup"><span data-stu-id="a7978-201">Request example 2</span></span>

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

#### <a name="response-example-2"></a><span data-ttu-id="a7978-202">Svarsexempel 2</span><span class="sxs-lookup"><span data-stu-id="a7978-202">Response example 2</span></span>

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
