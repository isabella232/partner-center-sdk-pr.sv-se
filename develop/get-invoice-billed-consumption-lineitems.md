---
title: Hämta fakturafakturerade radobjekt för kommersiell förbrukning
description: Du kan hämta en samling fakturaradsobjekt för kommersiell förbrukning (stängt dagligt klassificerat användningsradobjekt) för en angiven faktura med hjälp av Partner Center-API:erna.
ms.date: 01/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 285b6fbda774c9396dee8947550ed774d52bf901
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446232"
---
# <a name="get-invoice-billed-commercial-consumption-line-items"></a><span data-ttu-id="334a0-103">Hämta fakturafakturerade radobjekt för kommersiell förbrukning</span><span class="sxs-lookup"><span data-stu-id="334a0-103">Get invoice billed commercial consumption line items</span></span>

<span data-ttu-id="334a0-104">Du kan använda följande metoder för att hämta en samling information om fakturaradsobjekt för kommersiell förbrukning (kallas även stängda artiklar för daglig beräknad användningsrad) för en angiven faktura.</span><span class="sxs-lookup"><span data-stu-id="334a0-104">You can use the following methods to get a collection of details for commercial consumption invoice line items (also known as closed daily rated usage line items) for a specified invoice.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="334a0-105">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="334a0-105">Prerequisites</span></span>

- <span data-ttu-id="334a0-106">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="334a0-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="334a0-107">Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="334a0-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="334a0-108">En fakturaidentifierare.</span><span class="sxs-lookup"><span data-stu-id="334a0-108">An invoice identifier.</span></span> <span data-ttu-id="334a0-109">Detta identifierar fakturan som radobjekten ska hämtas för.</span><span class="sxs-lookup"><span data-stu-id="334a0-109">This identifies the invoice for which to retrieve the line items.</span></span>

## <a name="c"></a><span data-ttu-id="334a0-110">C\#</span><span class="sxs-lookup"><span data-stu-id="334a0-110">C\#</span></span>

<span data-ttu-id="334a0-111">Om du vill hämta de kommersiella radobjekten för den angivna fakturan måste du hämta fakturaobjektet:</span><span class="sxs-lookup"><span data-stu-id="334a0-111">To get the commercial line items for the specified invoice, you must retrieve the invoice object:</span></span>

1. <span data-ttu-id="334a0-112">Anropa [**ById-metoden**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) för att hämta ett gränssnitt för fakturaåtgärder för den angivna fakturan.</span><span class="sxs-lookup"><span data-stu-id="334a0-112">Call the [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) method to get an interface to invoice operations for the specified invoice.</span></span>

2. <span data-ttu-id="334a0-113">Anropa metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) för att hämta fakturaobjektet.</span><span class="sxs-lookup"><span data-stu-id="334a0-113">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the invoice object.</span></span> <span data-ttu-id="334a0-114">Fakturaobjektet innehåller all information för den angivna fakturan.</span><span class="sxs-lookup"><span data-stu-id="334a0-114">The invoice object contains all of the information for the specified invoice.</span></span>

<span data-ttu-id="334a0-115">Providern identifierar källan för den fakturerade detaljinformationen (till exempel **en gång).** </span><span class="sxs-lookup"><span data-stu-id="334a0-115">The **Provider** identifies the source of the billed detail information (for example, **onetime**).</span></span> <span data-ttu-id="334a0-116">**InvoiceLineItemType** anger typen (till exempel **UsageLineItem**).</span><span class="sxs-lookup"><span data-stu-id="334a0-116">The **InvoiceLineItemType** specifies the type (for example, **UsageLineItem**).</span></span>

<span data-ttu-id="334a0-117">I följande exempelkod används en **foreach-loop** för att bearbeta samlingen med radobjekt.</span><span class="sxs-lookup"><span data-stu-id="334a0-117">The following example code uses a **foreach** loop to process the line items collection.</span></span> <span data-ttu-id="334a0-118">En separat samling radobjekt hämtas för varje **InvoiceLineItemType**.</span><span class="sxs-lookup"><span data-stu-id="334a0-118">A separate collection of line items is retrieved for each **InvoiceLineItemType**.</span></span>

<span data-ttu-id="334a0-119">Så här hämtar du en samling radobjekt som motsvarar en **InvoiceDetail-instans:**</span><span class="sxs-lookup"><span data-stu-id="334a0-119">To get a collection of line items that correspond to an **InvoiceDetail** instance:</span></span>

1. <span data-ttu-id="334a0-120">Skicka instansens **BillingProvider och** **InvoiceLineItemType** till [**metoden**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) By.</span><span class="sxs-lookup"><span data-stu-id="334a0-120">Pass the instance's **BillingProvider** and **InvoiceLineItemType** to the [**By**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) method.</span></span>

2. <span data-ttu-id="334a0-121">Anropa metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) för att hämta de associerade radobjekten.</span><span class="sxs-lookup"><span data-stu-id="334a0-121">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the associated line items.</span></span>
3. <span data-ttu-id="334a0-122">Skapa en uppräkning för att bläddra i samlingen enligt följande exempel.</span><span class="sxs-lookup"><span data-stu-id="334a0-122">Create an enumerator to traverse the collection as shown in the following example.</span></span>

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

<span data-ttu-id="334a0-123">Ett liknande exempel finns i följande:</span><span class="sxs-lookup"><span data-stu-id="334a0-123">For a similar example, see the following:</span></span>

- <span data-ttu-id="334a0-124">Exempel: [Konsoltestapp](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="334a0-124">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="334a0-125">Project: **Partnercenter-SDK exempel**</span><span class="sxs-lookup"><span data-stu-id="334a0-125">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="334a0-126">Klass: **GetBilledConsumptionReconLineItemsPaging.cs**</span><span class="sxs-lookup"><span data-stu-id="334a0-126">Class: **GetBilledConsumptionReconLineItemsPaging.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="334a0-127">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="334a0-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="334a0-128">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="334a0-128">Request syntax</span></span>

<span data-ttu-id="334a0-129">Använd den första syntaxen för att returnera en fullständig lista över alla radobjekt för den angivna fakturan.</span><span class="sxs-lookup"><span data-stu-id="334a0-129">Use the first syntax to return a full list of every line item for the given invoice.</span></span> <span data-ttu-id="334a0-130">För stora fakturor använder du den andra syntaxen med en angiven storlek och 0-baserad förskjutning för att returnera en sidad lista med radobjekt.</span><span class="sxs-lookup"><span data-stu-id="334a0-130">For large invoices, use the second syntax with a specified size and 0-based offset to return a paged list of line items.</span></span> <span data-ttu-id="334a0-131">Använd den tredje syntaxen för att hämta nästa sida med rekognoseringsradobjekt med hjälp av `seekOperation = "Next"` .</span><span class="sxs-lookup"><span data-stu-id="334a0-131">Use the third syntax to get the next page of recon line items using `seekOperation = "Next"`.</span></span>

| <span data-ttu-id="334a0-132">Metod</span><span class="sxs-lookup"><span data-stu-id="334a0-132">Method</span></span>  | <span data-ttu-id="334a0-133">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="334a0-133">Request URI</span></span>                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="334a0-134">**Få**</span><span class="sxs-lookup"><span data-stu-id="334a0-134">**GET**</span></span> | <span data-ttu-id="334a0-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="334a0-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode} HTTP/1.1</span></span>                              |
| <span data-ttu-id="334a0-136">**Få**</span><span class="sxs-lookup"><span data-stu-id="334a0-136">**GET**</span></span> | <span data-ttu-id="334a0-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="334a0-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size} HTTP/1.1</span></span>  |
| <span data-ttu-id="334a0-138">**Få**</span><span class="sxs-lookup"><span data-stu-id="334a0-138">**GET**</span></span> | <span data-ttu-id="334a0-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size}&seekOperation=Next</span><span class="sxs-lookup"><span data-stu-id="334a0-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size}&seekOperation=Next</span></span>                               |

#### <a name="uri-parameters"></a><span data-ttu-id="334a0-140">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="334a0-140">URI parameters</span></span>

<span data-ttu-id="334a0-141">Använd följande URI och frågeparametrar när du skapar begäran.</span><span class="sxs-lookup"><span data-stu-id="334a0-141">Use the following URI and query parameters when creating the request.</span></span>

| <span data-ttu-id="334a0-142">Namn</span><span class="sxs-lookup"><span data-stu-id="334a0-142">Name</span></span>                   | <span data-ttu-id="334a0-143">Typ</span><span class="sxs-lookup"><span data-stu-id="334a0-143">Type</span></span>   | <span data-ttu-id="334a0-144">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="334a0-144">Required</span></span> | <span data-ttu-id="334a0-145">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="334a0-145">Description</span></span>                                                       |
|------------------------|--------|----------|-------------------------------------------------------------------|
| <span data-ttu-id="334a0-146">faktura-id</span><span class="sxs-lookup"><span data-stu-id="334a0-146">invoice-id</span></span>             | <span data-ttu-id="334a0-147">sträng</span><span class="sxs-lookup"><span data-stu-id="334a0-147">string</span></span> | <span data-ttu-id="334a0-148">Ja</span><span class="sxs-lookup"><span data-stu-id="334a0-148">Yes</span></span>      | <span data-ttu-id="334a0-149">En sträng som identifierar fakturan.</span><span class="sxs-lookup"><span data-stu-id="334a0-149">A string that identifies the invoice.</span></span>                             |
| <span data-ttu-id="334a0-150">Leverantör</span><span class="sxs-lookup"><span data-stu-id="334a0-150">provider</span></span>               | <span data-ttu-id="334a0-151">sträng</span><span class="sxs-lookup"><span data-stu-id="334a0-151">string</span></span> | <span data-ttu-id="334a0-152">Ja</span><span class="sxs-lookup"><span data-stu-id="334a0-152">Yes</span></span>      | <span data-ttu-id="334a0-153">Providern: "OneTime".</span><span class="sxs-lookup"><span data-stu-id="334a0-153">The provider: "OneTime".</span></span>                                  |
| <span data-ttu-id="334a0-154">invoice-line-item-type</span><span class="sxs-lookup"><span data-stu-id="334a0-154">invoice-line-item-type</span></span> | <span data-ttu-id="334a0-155">sträng</span><span class="sxs-lookup"><span data-stu-id="334a0-155">string</span></span> | <span data-ttu-id="334a0-156">Ja</span><span class="sxs-lookup"><span data-stu-id="334a0-156">Yes</span></span>      | <span data-ttu-id="334a0-157">Typ av fakturainformation: "UsageLineItems".</span><span class="sxs-lookup"><span data-stu-id="334a0-157">The type of invoice detail: "UsageLineItems".</span></span> |
| <span data-ttu-id="334a0-158">currencyCode</span><span class="sxs-lookup"><span data-stu-id="334a0-158">currencyCode</span></span>           | <span data-ttu-id="334a0-159">sträng</span><span class="sxs-lookup"><span data-stu-id="334a0-159">string</span></span> | <span data-ttu-id="334a0-160">Ja</span><span class="sxs-lookup"><span data-stu-id="334a0-160">Yes</span></span>      | <span data-ttu-id="334a0-161">Valutakoden för de fakturerade radobjekten.</span><span class="sxs-lookup"><span data-stu-id="334a0-161">The currency code for the billed line items.</span></span>                    |
| <span data-ttu-id="334a0-162">period</span><span class="sxs-lookup"><span data-stu-id="334a0-162">period</span></span>                 | <span data-ttu-id="334a0-163">sträng</span><span class="sxs-lookup"><span data-stu-id="334a0-163">string</span></span> | <span data-ttu-id="334a0-164">Ja</span><span class="sxs-lookup"><span data-stu-id="334a0-164">Yes</span></span>      | <span data-ttu-id="334a0-165">Perioden för fakturerad rekognosering.</span><span class="sxs-lookup"><span data-stu-id="334a0-165">The period for billed recon.</span></span> <span data-ttu-id="334a0-166">exempel: aktuell, tidigare.</span><span class="sxs-lookup"><span data-stu-id="334a0-166">example: current, previous.</span></span>        |
| <span data-ttu-id="334a0-167">ikoner</span><span class="sxs-lookup"><span data-stu-id="334a0-167">size</span></span>                   | <span data-ttu-id="334a0-168">antal</span><span class="sxs-lookup"><span data-stu-id="334a0-168">number</span></span> | <span data-ttu-id="334a0-169">Inga</span><span class="sxs-lookup"><span data-stu-id="334a0-169">No</span></span>       | <span data-ttu-id="334a0-170">Det maximala antalet objekt som ska returneras.</span><span class="sxs-lookup"><span data-stu-id="334a0-170">The maximum number of items to return.</span></span> <span data-ttu-id="334a0-171">Standardstorleken är 2 000</span><span class="sxs-lookup"><span data-stu-id="334a0-171">Default size is 2000</span></span>       |
| <span data-ttu-id="334a0-172">seekOperation</span><span class="sxs-lookup"><span data-stu-id="334a0-172">seekOperation</span></span>          | <span data-ttu-id="334a0-173">sträng</span><span class="sxs-lookup"><span data-stu-id="334a0-173">string</span></span> | <span data-ttu-id="334a0-174">No</span><span class="sxs-lookup"><span data-stu-id="334a0-174">No</span></span>       | <span data-ttu-id="334a0-175">Ange seekOperation= Nästa för att hämta nästa sida med rekognoseringsradobjekt.</span><span class="sxs-lookup"><span data-stu-id="334a0-175">Set seekOperation=Next to get the next page of recon line items.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="334a0-176">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="334a0-176">Request headers</span></span>

<span data-ttu-id="334a0-177">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="334a0-177">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="334a0-178">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="334a0-178">Request body</span></span>

<span data-ttu-id="334a0-179">Inga.</span><span class="sxs-lookup"><span data-stu-id="334a0-179">None.</span></span>

## <a name="rest-response"></a><span data-ttu-id="334a0-180">REST-svar</span><span class="sxs-lookup"><span data-stu-id="334a0-180">REST response</span></span>

<span data-ttu-id="334a0-181">Om det lyckas innehåller svaret en samling information om radobjekt.</span><span class="sxs-lookup"><span data-stu-id="334a0-181">If successful, the response contains the collection of line item details.</span></span>

<span data-ttu-id="334a0-182">För radobjektet **ChargeType** mappas värdet **Purchase** till **Ny**.</span><span class="sxs-lookup"><span data-stu-id="334a0-182">For the line item **ChargeType**, the value **Purchase** is mapped to **New**.</span></span> <span data-ttu-id="334a0-183">Värdet Återbetalning **mappas** till **Avbryt**.</span><span class="sxs-lookup"><span data-stu-id="334a0-183">The value **Refund** is mapped to **Cancel**.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="334a0-184">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="334a0-184">Response success and error codes</span></span>

<span data-ttu-id="334a0-185">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="334a0-185">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="334a0-186">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="334a0-186">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="334a0-187">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="334a0-187">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

## <a name="rest-examples"></a><span data-ttu-id="334a0-188">REST-exempel</span><span class="sxs-lookup"><span data-stu-id="334a0-188">REST examples</span></span>

### <a name="request-response-example-1"></a><span data-ttu-id="334a0-189">Exempel på begäran-svar 1</span><span class="sxs-lookup"><span data-stu-id="334a0-189">Request-response example 1</span></span>

<span data-ttu-id="334a0-190">Informationen för det här exemplet på REST-begäran och -svar är följande:</span><span class="sxs-lookup"><span data-stu-id="334a0-190">The details for this example REST request and response are as follows:</span></span>

- <span data-ttu-id="334a0-191">**Provider:** **OneTime**</span><span class="sxs-lookup"><span data-stu-id="334a0-191">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="334a0-192">**InvoiceLineItemType:** **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="334a0-192">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="334a0-193">**Period**: **Föregående**</span><span class="sxs-lookup"><span data-stu-id="334a0-193">**Period**: **Previous**</span></span>

#### <a name="request-example-1"></a><span data-ttu-id="334a0-194">Exempel på begäran 1</span><span class="sxs-lookup"><span data-stu-id="334a0-194">Request example 1</span></span>

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

#### <a name="response-example-1"></a><span data-ttu-id="334a0-195">Svarsexempel 1</span><span class="sxs-lookup"><span data-stu-id="334a0-195">Response example 1</span></span>

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

### <a name="request-response-example-2"></a><span data-ttu-id="334a0-196">Exempel på begäran-svar 2</span><span class="sxs-lookup"><span data-stu-id="334a0-196">Request-response example 2</span></span>

<span data-ttu-id="334a0-197">Informationen för det här exemplet på REST-begäran och -svar är följande:</span><span class="sxs-lookup"><span data-stu-id="334a0-197">The details for this example REST request and response are as follows:</span></span>

- <span data-ttu-id="334a0-198">**Provider:** **OneTime**</span><span class="sxs-lookup"><span data-stu-id="334a0-198">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="334a0-199">**InvoiceLineItemType:** **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="334a0-199">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="334a0-200">**Period**: **Föregående**</span><span class="sxs-lookup"><span data-stu-id="334a0-200">**Period**: **Previous**</span></span>
- <span data-ttu-id="334a0-201">**SeekOperation:** **Nästa**</span><span class="sxs-lookup"><span data-stu-id="334a0-201">**SeekOperation**: **Next**</span></span>

#### <a name="request-example-2"></a><span data-ttu-id="334a0-202">Exempel på begäran 2</span><span class="sxs-lookup"><span data-stu-id="334a0-202">Request example 2</span></span>

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

## <a name="response-example-2"></a><span data-ttu-id="334a0-203">Svarsexempel 2</span><span class="sxs-lookup"><span data-stu-id="334a0-203">Response example 2</span></span>

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
