---
title: Hämta fakturans rad objekt för ej fakturerad avstämnings rad
description: 'Du kan hämta en samling information om avstämnings rad objekt för den angivna perioden med hjälp av API: er för partner Center.'
ms.date: 01/27/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: ff69798ddfd91fca817ec0d047bf407f326066c2
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769852"
---
# <a name="get-invoices-unbilled-reconciliation-line-items"></a><span data-ttu-id="3523f-103">Hämta fakturans rad objekt för ej fakturerad avstämnings rad</span><span class="sxs-lookup"><span data-stu-id="3523f-103">Get invoice's unbilled reconciliation line items</span></span>

<span data-ttu-id="3523f-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="3523f-104">**Applies to:**</span></span>

- <span data-ttu-id="3523f-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="3523f-105">Partner Center</span></span>
- <span data-ttu-id="3523f-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="3523f-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="3523f-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="3523f-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="3523f-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="3523f-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="3523f-109">Du kan använda följande metoder för att få information om poster för ej fakturerade faktura rader (kallas även öppna fakturerings rads objekt).</span><span class="sxs-lookup"><span data-stu-id="3523f-109">You can use the following methods get a collection of details for unbilled invoice line items (also known as open billing line items).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3523f-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="3523f-110">Prerequisites</span></span>

- <span data-ttu-id="3523f-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="3523f-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3523f-112">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="3523f-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="3523f-113">Ett faktura-ID.</span><span class="sxs-lookup"><span data-stu-id="3523f-113">An invoice identifier.</span></span> <span data-ttu-id="3523f-114">Detta identifierar fakturan som rad artiklarna ska hämtas för.</span><span class="sxs-lookup"><span data-stu-id="3523f-114">This identifies the invoice for which to retrieve the line items.</span></span>

## <a name="c"></a><span data-ttu-id="3523f-115">C\#</span><span class="sxs-lookup"><span data-stu-id="3523f-115">C\#</span></span>

<span data-ttu-id="3523f-116">Hämta faktura objekt för att hämta rad artiklarna för den angivna fakturan:</span><span class="sxs-lookup"><span data-stu-id="3523f-116">To get the line items for the specified invoice, retrieve the invoice object:</span></span>

1. <span data-ttu-id="3523f-117">Anropa [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) -metoden för att hämta ett gränssnitt för att fakturera åtgärder för den angivna fakturan.</span><span class="sxs-lookup"><span data-stu-id="3523f-117">Call the [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) method to get an interface to invoice operations for the specified invoice.</span></span>

2. <span data-ttu-id="3523f-118">Anropa [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) -eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) -metoden för att hämta fakturaprojektet.</span><span class="sxs-lookup"><span data-stu-id="3523f-118">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the invoice object.</span></span>

<span data-ttu-id="3523f-119">Fakturaprojektet innehåller all information för den angivna fakturan:</span><span class="sxs-lookup"><span data-stu-id="3523f-119">The invoice object contains all of the information for the specified invoice:</span></span>

- <span data-ttu-id="3523f-120">**Providern** identifierar källan till den ej fakturerade detalj informationen (till exempel **Databasmigrering**).</span><span class="sxs-lookup"><span data-stu-id="3523f-120">**Provider** identifies the source of the unbilled detail information (for example, **OneTime**).</span></span>

- <span data-ttu-id="3523f-121">**InvoiceLineItemType** anger typen (till exempel **BillingLineItem**).</span><span class="sxs-lookup"><span data-stu-id="3523f-121">**InvoiceLineItemType** specifies the type (for example, **BillingLineItem**).</span></span>

<span data-ttu-id="3523f-122">Hämta en samling av rad objekt som motsvarar en **InvoiceDetail** -instans:</span><span class="sxs-lookup"><span data-stu-id="3523f-122">To get a collection of line items that correspond to an **InvoiceDetail** instance:</span></span>

1. <span data-ttu-id="3523f-123">Skicka instansens BillingProvider och InvoiceLineItemType till [**by**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) -metoden.</span><span class="sxs-lookup"><span data-stu-id="3523f-123">Pass the instance's BillingProvider and InvoiceLineItemType to the [**By**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) method.</span></span>

2. <span data-ttu-id="3523f-124">Anropa [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) -eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) -metoden för att hämta de associerade rad objekten.</span><span class="sxs-lookup"><span data-stu-id="3523f-124">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the associated line items.</span></span>

3. <span data-ttu-id="3523f-125">Skapa en uppräknare för att passera samlingen.</span><span class="sxs-lookup"><span data-stu-id="3523f-125">Create an enumerator to traverse the collection.</span></span> <span data-ttu-id="3523f-126">Ett exempel finns i följande exempel kod.</span><span class="sxs-lookup"><span data-stu-id="3523f-126">For an example, see the following sample code.</span></span>

<span data-ttu-id="3523f-127">Följande exempel kod använder en **förgrunds** slinga för att bearbeta **InvoiceLineItems** -samlingen.</span><span class="sxs-lookup"><span data-stu-id="3523f-127">The following sample code uses a **foreach** loop to process the **InvoiceLineItems** collection.</span></span> <span data-ttu-id="3523f-128">En separat samling av rad objekt hämtas för varje **InvoiceLineItemType**.</span><span class="sxs-lookup"><span data-stu-id="3523f-128">A separate collection of line items is retrieved for each **InvoiceLineItemType**.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string currencyCode;
// string period;
// int pageMaxSizeReconLineItems = 2000;

// all the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

var seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById("unbilled").By("onetime", "billinglineitems", currencyCode, period, pageMaxSizeReconLineItems).Get();

var fetchNext = true;

ConsoleKeyInfo keyInfo;

var itemNumber = 1;
while (fetchNext)
{
    Console.Out.WriteLine("\tLine line items count: " + seekBasedResourceCollection.Items.Count());

    seekBasedResourceCollection.Items.ToList().ForEach(item =>
    {
        // Instance of type OneTimeInvoiceLineItem
        if (item is OneTimeInvoiceLineItem)
        {
            Type t = typeof(OneTimeInvoiceLineItem);
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
            seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById("unbilled").By("onetime", "billinglineitems", currencyCode, period, pageMaxSizeReconLineItems).Seek(seekBasedResourceCollection.ContinuationToken, SeekOperation.Next);
        }
    }
}
```

<span data-ttu-id="3523f-129">Ett liknande exempel finns i:</span><span class="sxs-lookup"><span data-stu-id="3523f-129">For a similar example, see:</span></span>

- <span data-ttu-id="3523f-130">Exempel: [konsol test app](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="3523f-130">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="3523f-131">Projekt: **SDK-exempel för partner Center**</span><span class="sxs-lookup"><span data-stu-id="3523f-131">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="3523f-132">Klass: **GetUnBilledReconLineItemsPaging.cs**</span><span class="sxs-lookup"><span data-stu-id="3523f-132">Class: **GetUnBilledReconLineItemsPaging.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="3523f-133">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="3523f-133">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3523f-134">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="3523f-134">Request syntax</span></span>

<span data-ttu-id="3523f-135">Du kan använda följande syntax för din REST-begäran, beroende på ditt användnings fall.</span><span class="sxs-lookup"><span data-stu-id="3523f-135">You can use the following syntaxes for your REST request, depending on your use case.</span></span> <span data-ttu-id="3523f-136">Mer information finns i beskrivningarna för varje syntax.</span><span class="sxs-lookup"><span data-stu-id="3523f-136">For more information, see the descriptions for each syntax.</span></span>

 | <span data-ttu-id="3523f-137">Metod</span><span class="sxs-lookup"><span data-stu-id="3523f-137">Method</span></span>  | <span data-ttu-id="3523f-138">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="3523f-138">Request URI</span></span>            | <span data-ttu-id="3523f-139">Beskrivning av användnings fall för syntax</span><span class="sxs-lookup"><span data-stu-id="3523f-139">Description of syntax use case</span></span>                                                                                |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3523f-140">**TA**</span><span class="sxs-lookup"><span data-stu-id="3523f-140">**GET**</span></span> | <span data-ttu-id="3523f-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/INVOICES/{Invoice-ID}/lineitems? Provider = Databasmigrering&invoicelineitemtype = billinglineitems&CurrencyCode = {currencycode} &period = {period} http/1.1</span><span class="sxs-lookup"><span data-stu-id="3523f-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode={currencycode}&period={period} HTTP/1.1</span></span>                              | <span data-ttu-id="3523f-142">Använd den här syntaxen för att returnera en fullständig lista över varje rad objekt för den aktuella fakturan.</span><span class="sxs-lookup"><span data-stu-id="3523f-142">Use this syntax to return a full list of every line item for the given invoice.</span></span> |
| <span data-ttu-id="3523f-143">**TA**</span><span class="sxs-lookup"><span data-stu-id="3523f-143">**GET**</span></span> | <span data-ttu-id="3523f-144">[*{baseURL}*](partner-center-rest-urls.md)/v1/INVOICES/{Invoice-ID}/lineitems? Provider = Databasmigrering&invoicelineitemtype = billinglineitems&CurrencyCode = {currencycode} &period = {period} &storlek = {size} http/1.1</span><span class="sxs-lookup"><span data-stu-id="3523f-144">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode={currencycode}&period={period}&size={size} HTTP/1.1</span></span>  | <span data-ttu-id="3523f-145">För stora fakturor använder du den här syntaxen med en angiven storlek och 0-baserad förskjutning för att returnera en växlad lista med rad objekt.</span><span class="sxs-lookup"><span data-stu-id="3523f-145">For large invoices, use this syntax with a specified size and 0-based offset to return a paged list of line items.</span></span> |
| <span data-ttu-id="3523f-146">**TA**</span><span class="sxs-lookup"><span data-stu-id="3523f-146">**GET**</span></span> | <span data-ttu-id="3523f-147">[*{baseURL}*](partner-center-rest-urls.md)/v1/INVOICES/{Invoice-ID}/lineitems? Provider = Databasmigrering&invoicelineitemtype = billinglineitems&CurrencyCode = {currencycode} &period = {period} &storlek = {size} &SeekOperation = nästa</span><span class="sxs-lookup"><span data-stu-id="3523f-147">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode={currencycode}&period={period}&size={size}&seekOperation=Next</span></span>                               | <span data-ttu-id="3523f-148">Använd den här syntaxen för att hämta nästa sida av avstämnings rad objekt med `seekOperation = "Next"` .</span><span class="sxs-lookup"><span data-stu-id="3523f-148">Use this syntax to get the next page of reconciliation line items using `seekOperation = "Next"`.</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="3523f-149">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="3523f-149">URI parameters</span></span>

<span data-ttu-id="3523f-150">Använd följande URI och frågeparametrar när du skapar begäran.</span><span class="sxs-lookup"><span data-stu-id="3523f-150">Use the following URI and query parameters when creating the request.</span></span>

| <span data-ttu-id="3523f-151">Namn</span><span class="sxs-lookup"><span data-stu-id="3523f-151">Name</span></span>                   | <span data-ttu-id="3523f-152">Typ</span><span class="sxs-lookup"><span data-stu-id="3523f-152">Type</span></span>   | <span data-ttu-id="3523f-153">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="3523f-153">Required</span></span> | <span data-ttu-id="3523f-154">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="3523f-154">Description</span></span>                                                                     |
|------------------------|--------|----------|---------------------------------------------------------------------------------|
| <span data-ttu-id="3523f-155">faktura-ID</span><span class="sxs-lookup"><span data-stu-id="3523f-155">invoice-id</span></span>             | <span data-ttu-id="3523f-156">sträng</span><span class="sxs-lookup"><span data-stu-id="3523f-156">string</span></span> | <span data-ttu-id="3523f-157">Yes</span><span class="sxs-lookup"><span data-stu-id="3523f-157">Yes</span></span>      | <span data-ttu-id="3523f-158">En sträng som identifierar fakturan.</span><span class="sxs-lookup"><span data-stu-id="3523f-158">A string that identifies the invoice.</span></span> <span data-ttu-id="3523f-159">Använd unfakturerad för att få ej fakturerade uppskattningar.</span><span class="sxs-lookup"><span data-stu-id="3523f-159">Use 'unbilled' to get unbilled estimates.</span></span> |
| <span data-ttu-id="3523f-160">CSP</span><span class="sxs-lookup"><span data-stu-id="3523f-160">provider</span></span>               | <span data-ttu-id="3523f-161">sträng</span><span class="sxs-lookup"><span data-stu-id="3523f-161">string</span></span> | <span data-ttu-id="3523f-162">Yes</span><span class="sxs-lookup"><span data-stu-id="3523f-162">Yes</span></span>      | <span data-ttu-id="3523f-163">Providern: "Databasmigrering".</span><span class="sxs-lookup"><span data-stu-id="3523f-163">The provider: "OneTime".</span></span>                                                |
| <span data-ttu-id="3523f-164">faktura-rad-objekt-typ</span><span class="sxs-lookup"><span data-stu-id="3523f-164">invoice-line-item-type</span></span> | <span data-ttu-id="3523f-165">sträng</span><span class="sxs-lookup"><span data-stu-id="3523f-165">string</span></span> | <span data-ttu-id="3523f-166">Yes</span><span class="sxs-lookup"><span data-stu-id="3523f-166">Yes</span></span>      | <span data-ttu-id="3523f-167">Typ av faktura information: "BillingLineItems".</span><span class="sxs-lookup"><span data-stu-id="3523f-167">The type of invoice detail: "BillingLineItems".</span></span>               |
| <span data-ttu-id="3523f-168">hasPartnerEarnedCredit</span><span class="sxs-lookup"><span data-stu-id="3523f-168">hasPartnerEarnedCredit</span></span> | <span data-ttu-id="3523f-169">boolesk</span><span class="sxs-lookup"><span data-stu-id="3523f-169">bool</span></span>   | <span data-ttu-id="3523f-170">No</span><span class="sxs-lookup"><span data-stu-id="3523f-170">No</span></span>       | <span data-ttu-id="3523f-171">Det värde som anger om rad artiklarna med partner intjänad kredit ska returneras.</span><span class="sxs-lookup"><span data-stu-id="3523f-171">The value indicating if to return the line items with partner earned credit applied.</span></span> <span data-ttu-id="3523f-172">OBS! den här parametern används endast när providertypen är Databasmigrering och InvoiceLineItemType är UsageLineItems.</span><span class="sxs-lookup"><span data-stu-id="3523f-172">Note: this parameter will be only applied when provider type is OneTime and InvoiceLineItemType is UsageLineItems.</span></span>
| <span data-ttu-id="3523f-173">currencyCode</span><span class="sxs-lookup"><span data-stu-id="3523f-173">currencyCode</span></span>           | <span data-ttu-id="3523f-174">sträng</span><span class="sxs-lookup"><span data-stu-id="3523f-174">string</span></span> | <span data-ttu-id="3523f-175">Yes</span><span class="sxs-lookup"><span data-stu-id="3523f-175">Yes</span></span>      | <span data-ttu-id="3523f-176">Valuta koden för de ej fakturerade rad artiklarna.</span><span class="sxs-lookup"><span data-stu-id="3523f-176">The currency code for the unbilled line items.</span></span>                                  |
| <span data-ttu-id="3523f-177">period</span><span class="sxs-lookup"><span data-stu-id="3523f-177">period</span></span>                 | <span data-ttu-id="3523f-178">sträng</span><span class="sxs-lookup"><span data-stu-id="3523f-178">string</span></span> | <span data-ttu-id="3523f-179">Yes</span><span class="sxs-lookup"><span data-stu-id="3523f-179">Yes</span></span>      | <span data-ttu-id="3523f-180">Perioden för ej fakturerade rekognoseringar.</span><span class="sxs-lookup"><span data-stu-id="3523f-180">The period for unbilled recon.</span></span> <span data-ttu-id="3523f-181">exempel: Current, Previous.</span><span class="sxs-lookup"><span data-stu-id="3523f-181">example: current, previous.</span></span>                      |
| <span data-ttu-id="3523f-182">ikoner</span><span class="sxs-lookup"><span data-stu-id="3523f-182">size</span></span>                   | <span data-ttu-id="3523f-183">antal</span><span class="sxs-lookup"><span data-stu-id="3523f-183">number</span></span> | <span data-ttu-id="3523f-184">No</span><span class="sxs-lookup"><span data-stu-id="3523f-184">No</span></span>       | <span data-ttu-id="3523f-185">Det maximala antalet objekt som ska returneras.</span><span class="sxs-lookup"><span data-stu-id="3523f-185">The maximum number of items to return.</span></span> <span data-ttu-id="3523f-186">Standard storleken är 2000</span><span class="sxs-lookup"><span data-stu-id="3523f-186">Default size is 2000</span></span>                     |
| <span data-ttu-id="3523f-187">seekOperation</span><span class="sxs-lookup"><span data-stu-id="3523f-187">seekOperation</span></span>          | <span data-ttu-id="3523f-188">sträng</span><span class="sxs-lookup"><span data-stu-id="3523f-188">string</span></span> | <span data-ttu-id="3523f-189">No</span><span class="sxs-lookup"><span data-stu-id="3523f-189">No</span></span>       | <span data-ttu-id="3523f-190">Ange seekOperation = nästa för att hämta nästa sida med rekognoseringar rad objekt.</span><span class="sxs-lookup"><span data-stu-id="3523f-190">Set seekOperation=Next to get the next page of recon line items.</span></span>                |

### <a name="request-headers"></a><span data-ttu-id="3523f-191">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="3523f-191">Request headers</span></span>

<span data-ttu-id="3523f-192">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="3523f-192">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3523f-193">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="3523f-193">Request body</span></span>

<span data-ttu-id="3523f-194">Inga.</span><span class="sxs-lookup"><span data-stu-id="3523f-194">None.</span></span>

## <a name="rest-response"></a><span data-ttu-id="3523f-195">REST-svar</span><span class="sxs-lookup"><span data-stu-id="3523f-195">REST response</span></span>

<span data-ttu-id="3523f-196">Om det lyckas innehåller svaret insamling av rad objekts information.</span><span class="sxs-lookup"><span data-stu-id="3523f-196">If successful, the response contains the collection of line item details.</span></span>

<span data-ttu-id="3523f-197">*För rad posten **ChargeType** mappas värdet **inköp** till **New** och värdet **reexporten** mappas för att **avbryta**.*</span><span class="sxs-lookup"><span data-stu-id="3523f-197">*For the line item **ChargeType**, the value **Purchase** is mapped to **New** and the value **Refund** is mapped to **Cancel**.*</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3523f-198">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="3523f-198">Response success and error codes</span></span>

<span data-ttu-id="3523f-199">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="3523f-199">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3523f-200">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="3523f-200">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3523f-201">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="3523f-201">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="request-response-examples"></a><span data-ttu-id="3523f-202">Exempel på begäran-svar</span><span class="sxs-lookup"><span data-stu-id="3523f-202">Request-response examples</span></span>

#### <a name="request-response-example-1"></a><span data-ttu-id="3523f-203">Request-Response-exempel 1</span><span class="sxs-lookup"><span data-stu-id="3523f-203">Request-response example 1</span></span>

<span data-ttu-id="3523f-204">Följande information gäller för det här exemplet:</span><span class="sxs-lookup"><span data-stu-id="3523f-204">The following details apply to this example:</span></span>

- <span data-ttu-id="3523f-205">Provider: **Databasmigrering**</span><span class="sxs-lookup"><span data-stu-id="3523f-205">Provider: **OneTime**</span></span>
- <span data-ttu-id="3523f-206">InvoiceLineItemType: **BillingLineItems**</span><span class="sxs-lookup"><span data-stu-id="3523f-206">InvoiceLineItemType: **BillingLineItems**</span></span>
- <span data-ttu-id="3523f-207">Period: **föregående**</span><span class="sxs-lookup"><span data-stu-id="3523f-207">Period: **Previous**</span></span>

#### <a name="request-example-1"></a><span data-ttu-id="3523f-208">Exempel på begäran 1</span><span class="sxs-lookup"><span data-stu-id="3523f-208">Request example 1</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1//invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode=usd&period=previous&size=2000 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-1"></a><span data-ttu-id="3523f-209">Svars exempel 1</span><span class="sxs-lookup"><span data-stu-id="3523f-209">Response example 1</span></span>

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
            "partnerId": "0c924e8d-4852-4692-a4d7-7dd0dc09ad80",
            "customerId": "org:d7f565f5-5367-492f-a465-9e2057c5e3c3",
            "customerName": "TEST_TEST_GTM1",
            "customerDomainName": "TESTTESTGTM1.ccsctp.net",
            "customerCountry": "US",
            "invoiceNumber": "",
            "mpnId": "1234567",
            "resellerMpnId": 0,
            "orderId": "HJVtMZMkgQ2miuCiNv0RSr51zQDans0m1",
            "orderDate": "2019-02-04T17:59:52.9460102Z",
            "productId": "DZH318Z0BXWC",
            "skuId": "0002",
            "availabilityId": "DZH318Z0BP8B",
            "productName": "Test WAF-as-a-Service",
            "skuName": "Test WaaS - Medium Plan",
            "chargeType": "New",
            "unitPrice": 820,
            "effectiveUnitPrice": 820,
            "unitType": "",
            "quantity": 1,
            "subtotal": 820,
            "taxTotal": 0,
            "totalForCustomer": 0,
            "currency": "USD",
            "publisherName": "Test Networks, Inc.",
            "publisherId": "21223810",
            "subscriptionDescription": "",
            "subscriptionId": "12345678-9cf0-4a1f-9514-7fcc7fe9d1fe",
            "chargeStartDate": "2019-02-04T09:22:40.1767993-08:00",
            "chargeEndDate": "2019-03-03T09:22:40.1767993-08:00",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "123456ad566",
            "priceAdjustmentDescription": "[\"15.0% Partner earned credit for services managed\"]",
            "discountDetails": "",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "billableQuantity": 3.1618,
            "meterDescription": "Bandwidth - Data Transfer In (GB) - Zone 2",
            "reservationOrderId": "883d475b-0000-1234-0000-8818752f1234",
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        },
        {
            "partnerId": "0c924e8d-4852-4692-a4d7-7dd0dc09ad80",
            "customerId": "org:d7f565f5-5367-492f-a465-9e2057c5e3c3",
            "customerName": "TEST_TEST_GTM1",
            "customerDomainName": "TESTTESTGTM1.ccsctp.net",
            "customerCountry": "US",
            "invoiceNumber": "",
            "mpnId": "1234567",
            "resellerMpnId": 0,
            "orderId": "Oi2kwDPEOyGEFUkESk3QR4XSxcpvwp1x1",
            "orderDate": "2019-02-04T17:59:53.1628078Z",
            "productId": "DZH318Z0BXWC",
            "skuId": "0005",
            "availabilityId": "DZH318Z0BH9R",
            "productName": "Test WAF-as-a-Service",
            "skuName": "Test WaaS - Large Plan",
            "chargeType": "New",
            "unitPrice": 2598,
            "effectiveUnitPrice": 2598,
            "unitType": "",
            "quantity": 1,
            "subtotal": 2598,
            "taxTotal": 0,
            "totalForCustomer": 0,
            "currency": "USD",
            "publisherName": "Test Networks, Inc.",
            "publisherId": "21223810",
            "subscriptionDescription": "",
            "subscriptionId": "12345678-28db-48c2-8c30-04d7c9455746",
            "chargeStartDate": "2019-02-04T09:22:34.6455294-08:00",
            "chargeEndDate": "2019-03-03T09:22:34.6455294-08:00",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "123456ad566",
            "priceAdjustmentDescription": "[\"15.0% Partner earned credit for services managed\",\"100.0% Tier 1 Discount\"]",
            "discountDetails": "",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "billableQuantity": 0.737083,
            "meterDescription": "",
            "reservationOrderId": "883d475b-0000-2222-0000-8818752f1234",
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode=usd&period=previous&size=2000&seekOperation=Next",
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

### <a name="request-response-example-2"></a><span data-ttu-id="3523f-210">Request-Response-exempel 2</span><span class="sxs-lookup"><span data-stu-id="3523f-210">Request-response example 2</span></span>

<span data-ttu-id="3523f-211">Följande information gäller för det här exemplet:</span><span class="sxs-lookup"><span data-stu-id="3523f-211">The following details apply to this example:</span></span>

- <span data-ttu-id="3523f-212">Provider: **Databasmigrering**</span><span class="sxs-lookup"><span data-stu-id="3523f-212">Provider: **OneTime**</span></span>
- <span data-ttu-id="3523f-213">InvoiceLineItemType: **BillingLineItems**</span><span class="sxs-lookup"><span data-stu-id="3523f-213">InvoiceLineItemType: **BillingLineItems**</span></span>
- <span data-ttu-id="3523f-214">Period: **föregående**</span><span class="sxs-lookup"><span data-stu-id="3523f-214">Period: **Previous**</span></span>
- <span data-ttu-id="3523f-215">SeekOperation: **Nästa**</span><span class="sxs-lookup"><span data-stu-id="3523f-215">SeekOperation: **Next**</span></span>

#### <a name="request-example-2"></a><span data-ttu-id="3523f-216">Exempel på begäran 2</span><span class="sxs-lookup"><span data-stu-id="3523f-216">Request example 2</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/unbilled/lineitems?provider=onetime&invoiceLineItemType=billinglineitems&currencyCode=usd&period=previous&size=2000&seekoperation=next HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-ContinuationToken: d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-2"></a><span data-ttu-id="3523f-217">Svars exempel 2</span><span class="sxs-lookup"><span data-stu-id="3523f-217">Response example 2</span></span>

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
            "partnerId": "0c924e8d-4852-4692-a4d7-7dd0dc09ad80",
            "customerId": "org:d7f565f5-5367-492f-a465-9e2057c5e3c3",
            "customerName": "TEST_TEST_GTM1",
            "customerDomainName": "TESTTESTGTM1.ccsctp.net",
            "customerCountry": "US",
            "invoiceNumber": "",
            "mpnId": "1234567",
            "resellerMpnId": 0,
            "orderId": "Oi2kwDPEOyGEFUkESk3QR4XSxcpvwp1x1",
            "orderDate": "2019-02-04T17:59:53.1628078Z",
            "productId": "DZH318Z0BXWC",
            "skuId": "0005",
            "availabilityId": "DZH318Z0BH9R",
            "productName": "Test WAF-as-a-Service",
            "skuName": "Test WaaS - Large Plan",
            "chargeType": "New",
            "unitPrice": 2598,
            "effectiveUnitPrice": 2598,
            "unitType": "",
            "quantity": 1,
            "subtotal": 2598,
            "taxTotal": 0,
            "totalForCustomer": 0,
            "currency": "USD",
            "publisherName": "Test Networks, Inc.",
            "publisherId": "21223810",
            "subscriptionDescription": "",
            "subscriptionId": "12345678-28db-48c2-8c30-04d7c9455746",
            "chargeStartDate": "2019-02-04T09:22:34.6455294-08:00",
            "chargeEndDate": "2019-03-03T09:22:34.6455294-08:00",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "123456ad566",
            "priceAdjustmentDescription": "[\"15.0% Partner earned credit for services managed\",\"100.0% Tier 1 Discount\"]",
            "discountDetails": "",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "billableQuantity": 0.737083,
            "meterDescription": "",
            "reservationOrderId": ""
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        }
    ],
    "links": {
        "self": {
             "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

#### <a name="request-example-3"></a><span data-ttu-id="3523f-218">Exempel på begäran 3</span><span class="sxs-lookup"><span data-stu-id="3523f-218">Request example 3</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/unbilled/lineitems?provider=OneTime&invoiceLineItemType=UsageLineItems&currencyCode=usd&period=previous&size=2000&seekoperation=next HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-ContinuationToken: d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-3"></a><span data-ttu-id="3523f-219">Svars exempel 3</span><span class="sxs-lookup"><span data-stu-id="3523f-219">Response example 3</span></span>

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
            "partnerId": "0c924e8d-4852-4692-a4d7-7dd0dc09ad80",
            "PartnerName": "testPartner",
            "customerId": "org:d7f565f5-5367-492f-a465-9e2057c5e3c3",
            "customerName": "TEST_TEST_GTM1",
            "customerDomainName": "TESTTESTGTM1.ccsctp.net",
            "invoiceNumber": "T11ETHHDDD",
            "productId": "DZH318Z0BXWC",
            "skuId": "0005",
            "availabilityId": "DZH318Z0BH9R",
            "productName": "Test WAF-as-a-Service",
            "publisherId": "21223810",
            "subscriptionId": "12345678-28db-48c2-8c30-04d7c9455746",
            "subscriptionDescription": "sub description",
            "chargeStartDate": "2019-02-04T09:22:34.6455294-08:00",
            "chargeEndDate": "2019-03-03T09:22:34.6455294-08:00",
            "UsageDate": "2019-02-07T09:22:34.6455294-08:00",
            "MeterType": "type",
            "MeterCategory": "category",
            "MeterId": "21312312312-fdsfsd",
            "MeterSubCategory": "subcategory",
            "MeterName": "meter name",
            "MeterRegion": "meter region",
            "UnitOfMeasure": "11",
            "skuName": "Test WaaS - Large Plan",
            "publisherName": "Test Networks, Inc.",
            "chargeType": "New",
            "unitPrice": 2598,
            "effectiveUnitPrice": 2598,
            "unitType": "",
            "quantity": 1,
            "subtotal": 2598,
            "taxTotal": 0,
            "totalForCustomer": 0,
            "currency": "USD",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "123456ad566",
            "discountDetails": "",
            "providerSource": "All",
            "RateOfPartnerEarnedCredit": 0.15,
            "IsPartnerEarnedCreditApplied": true,
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        }
    ],
    "links": {
        "self": {
             "uri": "/invoices/unbilled/lineitems?provider=all&invoicelineitemtype=billinglineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
