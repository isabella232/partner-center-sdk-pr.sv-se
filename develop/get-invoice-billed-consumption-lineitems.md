---
title: Hämta fakturafakturerade radobjekt för kommersiell förbrukning
description: Du kan hämta en samling fakturaradsobjekt för kommersiell förbrukning (stängt dagligt klassificerat användningsradobjekt) för en angiven faktura med hjälp av Partner Center-API:erna.
ms.date: 01/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 1406938b16e5a363a73c36ef0338eb5fc4305279
ms.sourcegitcommit: 89aefbff6dbe740b6f27a888492ffc2e5f98b1e9
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/24/2021
ms.locfileid: "110325453"
---
# <a name="get-invoice-billed-commercial-consumption-line-items"></a><span data-ttu-id="f837c-103">Hämta fakturafakturerade radobjekt för kommersiell förbrukning</span><span class="sxs-lookup"><span data-stu-id="f837c-103">Get invoice billed commercial consumption line items</span></span>

<span data-ttu-id="f837c-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="f837c-104">**Applies to:**</span></span>

- <span data-ttu-id="f837c-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="f837c-105">Partner Center</span></span>

<span data-ttu-id="f837c-106">Du kan använda följande metoder för att hämta en samling information om fakturaradsobjekt för kommersiell förbrukning (kallas även stängda artiklar för daglig beräknad användningsrad) för en angiven faktura.</span><span class="sxs-lookup"><span data-stu-id="f837c-106">You can use the following methods to get a collection of details for commercial consumption invoice line items (also known as closed daily rated usage line items) for a specified invoice.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="f837c-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="f837c-107">Prerequisites</span></span>

- <span data-ttu-id="f837c-108">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="f837c-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f837c-109">Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="f837c-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="f837c-110">En fakturaidentifierare.</span><span class="sxs-lookup"><span data-stu-id="f837c-110">An invoice identifier.</span></span> <span data-ttu-id="f837c-111">Detta identifierar fakturan som radobjekten ska hämtas för.</span><span class="sxs-lookup"><span data-stu-id="f837c-111">This identifies the invoice for which to retrieve the line items.</span></span>

## <a name="c"></a><span data-ttu-id="f837c-112">C\#</span><span class="sxs-lookup"><span data-stu-id="f837c-112">C\#</span></span>

<span data-ttu-id="f837c-113">Om du vill hämta de kommersiella radobjekten för den angivna fakturan måste du hämta fakturaobjektet:</span><span class="sxs-lookup"><span data-stu-id="f837c-113">To get the commercial line items for the specified invoice, you must retrieve the invoice object:</span></span>

1. <span data-ttu-id="f837c-114">Anropa [**ById-metoden**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) för att hämta ett gränssnitt för fakturaåtgärder för den angivna fakturan.</span><span class="sxs-lookup"><span data-stu-id="f837c-114">Call the [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) method to get an interface to invoice operations for the specified invoice.</span></span>

2. <span data-ttu-id="f837c-115">Anropa metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) för att hämta fakturaobjektet.</span><span class="sxs-lookup"><span data-stu-id="f837c-115">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the invoice object.</span></span> <span data-ttu-id="f837c-116">Fakturaobjektet innehåller all information för den angivna fakturan.</span><span class="sxs-lookup"><span data-stu-id="f837c-116">The invoice object contains all of the information for the specified invoice.</span></span>

<span data-ttu-id="f837c-117">Providern identifierar källan för den fakturerade detaljinformationen (till exempel **en gång).** </span><span class="sxs-lookup"><span data-stu-id="f837c-117">The **Provider** identifies the source of the billed detail information (for example, **onetime**).</span></span> <span data-ttu-id="f837c-118">**InvoiceLineItemType** anger typen (till exempel **UsageLineItem**).</span><span class="sxs-lookup"><span data-stu-id="f837c-118">The **InvoiceLineItemType** specifies the type (for example, **UsageLineItem**).</span></span>

<span data-ttu-id="f837c-119">I följande exempelkod används en **foreach-loop** för att bearbeta samlingen med radobjekt.</span><span class="sxs-lookup"><span data-stu-id="f837c-119">The following example code uses a **foreach** loop to process the line items collection.</span></span> <span data-ttu-id="f837c-120">En separat samling radobjekt hämtas för varje **InvoiceLineItemType**.</span><span class="sxs-lookup"><span data-stu-id="f837c-120">A separate collection of line items is retrieved for each **InvoiceLineItemType**.</span></span>

<span data-ttu-id="f837c-121">Så här hämtar du en samling radobjekt som motsvarar en **InvoiceDetail-instans:**</span><span class="sxs-lookup"><span data-stu-id="f837c-121">To get a collection of line items that correspond to an **InvoiceDetail** instance:</span></span>

1. <span data-ttu-id="f837c-122">Skicka instansens **BillingProvider och** **InvoiceLineItemType** till [**metoden**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) By.</span><span class="sxs-lookup"><span data-stu-id="f837c-122">Pass the instance's **BillingProvider** and **InvoiceLineItemType** to the [**By**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) method.</span></span>

2. <span data-ttu-id="f837c-123">Anropa metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) för att hämta de associerade radobjekten.</span><span class="sxs-lookup"><span data-stu-id="f837c-123">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the associated line items.</span></span>
3. <span data-ttu-id="f837c-124">Skapa en uppräkning för att bläddra i samlingen enligt följande exempel.</span><span class="sxs-lookup"><span data-stu-id="f837c-124">Create an enumerator to traverse the collection as shown in the following example.</span></span>

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

<span data-ttu-id="f837c-125">Ett liknande exempel finns i följande:</span><span class="sxs-lookup"><span data-stu-id="f837c-125">For a similar example, see the following:</span></span>

- <span data-ttu-id="f837c-126">Exempel: [Konsoltestapp](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="f837c-126">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="f837c-127">Projekt: **Partnercenter-SDK exempel**</span><span class="sxs-lookup"><span data-stu-id="f837c-127">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="f837c-128">Klass: **GetBilledConsumptionReconLineItemsPaging.cs**</span><span class="sxs-lookup"><span data-stu-id="f837c-128">Class: **GetBilledConsumptionReconLineItemsPaging.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="f837c-129">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="f837c-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f837c-130">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="f837c-130">Request syntax</span></span>

<span data-ttu-id="f837c-131">Använd den första syntaxen för att returnera en fullständig lista över varje radobjekt för den angivna fakturan.</span><span class="sxs-lookup"><span data-stu-id="f837c-131">Use the first syntax to return a full list of every line item for the given invoice.</span></span> <span data-ttu-id="f837c-132">För stora fakturor använder du den andra syntaxen med en angiven storlek och 0-baserad förskjutning för att returnera en sidad lista med radobjekt.</span><span class="sxs-lookup"><span data-stu-id="f837c-132">For large invoices, use the second syntax with a specified size and 0-based offset to return a paged list of line items.</span></span> <span data-ttu-id="f837c-133">Använd den tredje syntaxen för att hämta nästa sida med radobjekt med hjälp av `seekOperation = "Next"` .</span><span class="sxs-lookup"><span data-stu-id="f837c-133">Use the third syntax to get the next page of recon line items using `seekOperation = "Next"`.</span></span>

| <span data-ttu-id="f837c-134">Metod</span><span class="sxs-lookup"><span data-stu-id="f837c-134">Method</span></span>  | <span data-ttu-id="f837c-135">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="f837c-135">Request URI</span></span>                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f837c-136">**Få**</span><span class="sxs-lookup"><span data-stu-id="f837c-136">**GET**</span></span> | <span data-ttu-id="f837c-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="f837c-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode} HTTP/1.1</span></span>                              |
| <span data-ttu-id="f837c-138">**Få**</span><span class="sxs-lookup"><span data-stu-id="f837c-138">**GET**</span></span> | <span data-ttu-id="f837c-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="f837c-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size} HTTP/1.1</span></span>  |
| <span data-ttu-id="f837c-140">**Få**</span><span class="sxs-lookup"><span data-stu-id="f837c-140">**GET**</span></span> | <span data-ttu-id="f837c-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size}&seekOperation=Next</span><span class="sxs-lookup"><span data-stu-id="f837c-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size}&seekOperation=Next</span></span>                               |

#### <a name="uri-parameters"></a><span data-ttu-id="f837c-142">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="f837c-142">URI parameters</span></span>

<span data-ttu-id="f837c-143">Använd följande URI- och frågeparametrar när du skapar begäran.</span><span class="sxs-lookup"><span data-stu-id="f837c-143">Use the following URI and query parameters when creating the request.</span></span>

| <span data-ttu-id="f837c-144">Namn</span><span class="sxs-lookup"><span data-stu-id="f837c-144">Name</span></span>                   | <span data-ttu-id="f837c-145">Typ</span><span class="sxs-lookup"><span data-stu-id="f837c-145">Type</span></span>   | <span data-ttu-id="f837c-146">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="f837c-146">Required</span></span> | <span data-ttu-id="f837c-147">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="f837c-147">Description</span></span>                                                       |
|------------------------|--------|----------|-------------------------------------------------------------------|
| <span data-ttu-id="f837c-148">invoice-id</span><span class="sxs-lookup"><span data-stu-id="f837c-148">invoice-id</span></span>             | <span data-ttu-id="f837c-149">sträng</span><span class="sxs-lookup"><span data-stu-id="f837c-149">string</span></span> | <span data-ttu-id="f837c-150">Yes</span><span class="sxs-lookup"><span data-stu-id="f837c-150">Yes</span></span>      | <span data-ttu-id="f837c-151">En sträng som identifierar fakturan.</span><span class="sxs-lookup"><span data-stu-id="f837c-151">A string that identifies the invoice.</span></span>                             |
| <span data-ttu-id="f837c-152">Leverantör</span><span class="sxs-lookup"><span data-stu-id="f837c-152">provider</span></span>               | <span data-ttu-id="f837c-153">sträng</span><span class="sxs-lookup"><span data-stu-id="f837c-153">string</span></span> | <span data-ttu-id="f837c-154">Yes</span><span class="sxs-lookup"><span data-stu-id="f837c-154">Yes</span></span>      | <span data-ttu-id="f837c-155">Providern: "OneTime".</span><span class="sxs-lookup"><span data-stu-id="f837c-155">The provider: "OneTime".</span></span>                                  |
| <span data-ttu-id="f837c-156">invoice-line-item-type</span><span class="sxs-lookup"><span data-stu-id="f837c-156">invoice-line-item-type</span></span> | <span data-ttu-id="f837c-157">sträng</span><span class="sxs-lookup"><span data-stu-id="f837c-157">string</span></span> | <span data-ttu-id="f837c-158">Yes</span><span class="sxs-lookup"><span data-stu-id="f837c-158">Yes</span></span>      | <span data-ttu-id="f837c-159">Typ av fakturainformation: "UsageLineItems".</span><span class="sxs-lookup"><span data-stu-id="f837c-159">The type of invoice detail: "UsageLineItems".</span></span> |
| <span data-ttu-id="f837c-160">currencyCode</span><span class="sxs-lookup"><span data-stu-id="f837c-160">currencyCode</span></span>           | <span data-ttu-id="f837c-161">sträng</span><span class="sxs-lookup"><span data-stu-id="f837c-161">string</span></span> | <span data-ttu-id="f837c-162">Yes</span><span class="sxs-lookup"><span data-stu-id="f837c-162">Yes</span></span>      | <span data-ttu-id="f837c-163">Valutakoden för de fakturerade radobjekten.</span><span class="sxs-lookup"><span data-stu-id="f837c-163">The currency code for the billed line items.</span></span>                    |
| <span data-ttu-id="f837c-164">period</span><span class="sxs-lookup"><span data-stu-id="f837c-164">period</span></span>                 | <span data-ttu-id="f837c-165">sträng</span><span class="sxs-lookup"><span data-stu-id="f837c-165">string</span></span> | <span data-ttu-id="f837c-166">Yes</span><span class="sxs-lookup"><span data-stu-id="f837c-166">Yes</span></span>      | <span data-ttu-id="f837c-167">Perioden för fakturerad rekognosering.</span><span class="sxs-lookup"><span data-stu-id="f837c-167">The period for billed recon.</span></span> <span data-ttu-id="f837c-168">exempel: aktuell, tidigare.</span><span class="sxs-lookup"><span data-stu-id="f837c-168">example: current, previous.</span></span>        |
| <span data-ttu-id="f837c-169">ikoner</span><span class="sxs-lookup"><span data-stu-id="f837c-169">size</span></span>                   | <span data-ttu-id="f837c-170">antal</span><span class="sxs-lookup"><span data-stu-id="f837c-170">number</span></span> | <span data-ttu-id="f837c-171">No</span><span class="sxs-lookup"><span data-stu-id="f837c-171">No</span></span>       | <span data-ttu-id="f837c-172">Det maximala antalet objekt som ska returneras.</span><span class="sxs-lookup"><span data-stu-id="f837c-172">The maximum number of items to return.</span></span> <span data-ttu-id="f837c-173">Standardstorleken är 2 000</span><span class="sxs-lookup"><span data-stu-id="f837c-173">Default size is 2000</span></span>       |
| <span data-ttu-id="f837c-174">seekOperation</span><span class="sxs-lookup"><span data-stu-id="f837c-174">seekOperation</span></span>          | <span data-ttu-id="f837c-175">sträng</span><span class="sxs-lookup"><span data-stu-id="f837c-175">string</span></span> | <span data-ttu-id="f837c-176">No</span><span class="sxs-lookup"><span data-stu-id="f837c-176">No</span></span>       | <span data-ttu-id="f837c-177">Ange seekOperation= Nästa för att hämta nästa sida med rekognoseringsradobjekt.</span><span class="sxs-lookup"><span data-stu-id="f837c-177">Set seekOperation=Next to get the next page of recon line items.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="f837c-178">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="f837c-178">Request headers</span></span>

<span data-ttu-id="f837c-179">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="f837c-179">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f837c-180">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="f837c-180">Request body</span></span>

<span data-ttu-id="f837c-181">Inga.</span><span class="sxs-lookup"><span data-stu-id="f837c-181">None.</span></span>

## <a name="rest-response"></a><span data-ttu-id="f837c-182">REST-svar</span><span class="sxs-lookup"><span data-stu-id="f837c-182">REST response</span></span>

<span data-ttu-id="f837c-183">Om det lyckas innehåller svaret en samling information om radobjekt.</span><span class="sxs-lookup"><span data-stu-id="f837c-183">If successful, the response contains the collection of line item details.</span></span>

<span data-ttu-id="f837c-184">För radobjektet **ChargeType** mappas värdet **Purchase** till **Ny**.</span><span class="sxs-lookup"><span data-stu-id="f837c-184">For the line item **ChargeType**, the value **Purchase** is mapped to **New**.</span></span> <span data-ttu-id="f837c-185">Värdet Återbetalning **mappas** till **Avbryt**.</span><span class="sxs-lookup"><span data-stu-id="f837c-185">The value **Refund** is mapped to **Cancel**.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f837c-186">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="f837c-186">Response success and error codes</span></span>

<span data-ttu-id="f837c-187">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="f837c-187">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f837c-188">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="f837c-188">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f837c-189">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="f837c-189">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

## <a name="rest-examples"></a><span data-ttu-id="f837c-190">REST-exempel</span><span class="sxs-lookup"><span data-stu-id="f837c-190">REST examples</span></span>

### <a name="request-response-example-1"></a><span data-ttu-id="f837c-191">Exempel på begäran-svar 1</span><span class="sxs-lookup"><span data-stu-id="f837c-191">Request-response example 1</span></span>

<span data-ttu-id="f837c-192">Informationen för det här exemplet på REST-begäran och -svar är följande:</span><span class="sxs-lookup"><span data-stu-id="f837c-192">The details for this example REST request and response are as follows:</span></span>

- <span data-ttu-id="f837c-193">**Provider:** **OneTime**</span><span class="sxs-lookup"><span data-stu-id="f837c-193">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="f837c-194">**InvoiceLineItemType:** **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="f837c-194">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="f837c-195">**Period**: **Föregående**</span><span class="sxs-lookup"><span data-stu-id="f837c-195">**Period**: **Previous**</span></span>

#### <a name="request-example-1"></a><span data-ttu-id="f837c-196">Exempel på begäran 1</span><span class="sxs-lookup"><span data-stu-id="f837c-196">Request example 1</span></span>

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

#### <a name="response-example-1"></a><span data-ttu-id="f837c-197">Svarsexempel 1</span><span class="sxs-lookup"><span data-stu-id="f837c-197">Response example 1</span></span>

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

### <a name="request-response-example-2"></a><span data-ttu-id="f837c-198">Exempel på begäran-svar 2</span><span class="sxs-lookup"><span data-stu-id="f837c-198">Request-response example 2</span></span>

<span data-ttu-id="f837c-199">Informationen för det här exemplet på REST-begäran och -svar är följande:</span><span class="sxs-lookup"><span data-stu-id="f837c-199">The details for this example REST request and response are as follows:</span></span>

- <span data-ttu-id="f837c-200">**Provider:** **OneTime**</span><span class="sxs-lookup"><span data-stu-id="f837c-200">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="f837c-201">**InvoiceLineItemType:** **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="f837c-201">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="f837c-202">**Period**: **Föregående**</span><span class="sxs-lookup"><span data-stu-id="f837c-202">**Period**: **Previous**</span></span>
- <span data-ttu-id="f837c-203">**SeekOperation:** **Nästa**</span><span class="sxs-lookup"><span data-stu-id="f837c-203">**SeekOperation**: **Next**</span></span>

#### <a name="request-example-2"></a><span data-ttu-id="f837c-204">Exempel på begäran 2</span><span class="sxs-lookup"><span data-stu-id="f837c-204">Request example 2</span></span>

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

## <a name="response-example-2"></a><span data-ttu-id="f837c-205">Svarsexempel 2</span><span class="sxs-lookup"><span data-stu-id="f837c-205">Response example 2</span></span>

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
