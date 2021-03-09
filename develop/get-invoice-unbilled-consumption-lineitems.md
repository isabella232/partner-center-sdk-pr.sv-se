---
title: Hämta fakturor för ej fakturerad kommersiell förbruknings artikel
description: 'Du kan hämta en samling information om ej fakturerad kommersiell förbruknings artikel för en viss faktura med hjälp av API: er för partner Center.'
ms.date: 01/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8d3bbe7921029dc6c40c65fb8d82baaa944089b6
ms.sourcegitcommit: 160296667833366fb3f4021d042094606e1032ec
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/09/2021
ms.locfileid: "102472690"
---
# <a name="get-invoice-unbilled-commercial-consumption-line-items"></a><span data-ttu-id="c40a9-103">Hämta fakturor för ej fakturerad kommersiell förbruknings artikel</span><span class="sxs-lookup"><span data-stu-id="c40a9-103">Get invoice unbilled commercial consumption line items</span></span>

<span data-ttu-id="c40a9-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="c40a9-104">**Applies to:**</span></span>

- <span data-ttu-id="c40a9-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="c40a9-105">Partner Center</span></span>

<span data-ttu-id="c40a9-106">Så här hämtar du en samling med ej fakturerad kommersiell förbruknings artikel information.</span><span class="sxs-lookup"><span data-stu-id="c40a9-106">How to get a collection of unbilled commercial consumption line item details.</span></span>

<span data-ttu-id="c40a9-107">Du kan använda följande metoder för att få en samling information som inte fakturerats på kommersiell förbruknings rad (även kallat öppna användnings rads objekt) program mässigt.</span><span class="sxs-lookup"><span data-stu-id="c40a9-107">You can use the following methods to get a collection of details unbilled commercial consumption line items (also known as open usage line items) programmatically.</span></span>

>[!NOTE]
><span data-ttu-id="c40a9-108">Dagligt Beräknad användning tar normalt 24 timmar att visas i Partner Center eller nås via API: et.</span><span class="sxs-lookup"><span data-stu-id="c40a9-108">Daily-rated usage normally takes 24 hours to appear in Partner Center or to be accessed through the API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c40a9-109">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="c40a9-109">Prerequisites</span></span>

- <span data-ttu-id="c40a9-110">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="c40a9-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c40a9-111">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="c40a9-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="c40a9-112">Ett faktura-ID.</span><span class="sxs-lookup"><span data-stu-id="c40a9-112">An invoice identifier.</span></span> <span data-ttu-id="c40a9-113">Detta identifierar fakturan som rad artiklarna ska hämtas för.</span><span class="sxs-lookup"><span data-stu-id="c40a9-113">This identifies the invoice for which to retrieve the line items.</span></span>

## <a name="c"></a><span data-ttu-id="c40a9-114">C\#</span><span class="sxs-lookup"><span data-stu-id="c40a9-114">C\#</span></span>

<span data-ttu-id="c40a9-115">Så här hämtar du rad artiklarna för den angivna fakturan:</span><span class="sxs-lookup"><span data-stu-id="c40a9-115">To get the line items for the specified invoice:</span></span>

1. <span data-ttu-id="c40a9-116">Anropa [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) -metoden för att hämta ett gränssnitt för att fakturera åtgärder för den angivna fakturan.</span><span class="sxs-lookup"><span data-stu-id="c40a9-116">Call the [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) method to get an interface to invoice operations for the specified invoice.</span></span>

2. <span data-ttu-id="c40a9-117">Anropa [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) -eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) -metoden för att hämta fakturaprojektet.</span><span class="sxs-lookup"><span data-stu-id="c40a9-117">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the invoice object.</span></span>

<span data-ttu-id="c40a9-118">**Fakturaprojektet** innehåller all information för den angivna fakturan.</span><span class="sxs-lookup"><span data-stu-id="c40a9-118">The **invoice object** contains all of the information for the specified invoice.</span></span> <span data-ttu-id="c40a9-119">**Providern** identifierar källan till den ej fakturerade detalj informationen (till exempel **Databasmigrering**).</span><span class="sxs-lookup"><span data-stu-id="c40a9-119">The **Provider** identifies the source of the unbilled detail information (for example, **OneTime**).</span></span> <span data-ttu-id="c40a9-120">**InvoiceLineItemType** anger typen (till exempel **UsageLineItem**).</span><span class="sxs-lookup"><span data-stu-id="c40a9-120">The **InvoiceLineItemType** specifies the type (for example, **UsageLineItem**).</span></span>

<span data-ttu-id="c40a9-121">I följande exempel kod används en **förgrunds** slinga för att bearbeta **InvoiceLineItems** -samlingen.</span><span class="sxs-lookup"><span data-stu-id="c40a9-121">The following example code uses a **foreach** loop to process the **InvoiceLineItems** collection.</span></span> <span data-ttu-id="c40a9-122">En separat samling av rad objekt hämtas för varje **InvoiceLineItemType**.</span><span class="sxs-lookup"><span data-stu-id="c40a9-122">A separate collection of line items is retrieved for each **InvoiceLineItemType**.</span></span>

<span data-ttu-id="c40a9-123">Hämta en samling av rad objekt som motsvarar en **InvoiceDetail** -instans:</span><span class="sxs-lookup"><span data-stu-id="c40a9-123">To get a collection of line items that correspond to an **InvoiceDetail** instance:</span></span>

1. <span data-ttu-id="c40a9-124">Skicka instansens **BillingProvider** och **InvoiceLineItemType** till [**by**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) -metoden.</span><span class="sxs-lookup"><span data-stu-id="c40a9-124">Pass the instance's **BillingProvider** and **InvoiceLineItemType** to the [**By**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) method.</span></span>

2. <span data-ttu-id="c40a9-125">Anropa [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) -eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) -metoden för att hämta de associerade rad objekten.</span><span class="sxs-lookup"><span data-stu-id="c40a9-125">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the associated line items.</span></span>
3. <span data-ttu-id="c40a9-126">Skapa en uppräknare för att passera samlingen som visas i följande exempel.</span><span class="sxs-lookup"><span data-stu-id="c40a9-126">Create an enumerator to traverse the collection as shown in the following example.</span></span>

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

<span data-ttu-id="c40a9-127">Ett liknande exempel finns i:</span><span class="sxs-lookup"><span data-stu-id="c40a9-127">For a similar example, see:</span></span>

- <span data-ttu-id="c40a9-128">Exempel: [konsol test app](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="c40a9-128">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="c40a9-129">Projekt: **SDK-exempel för partner Center**</span><span class="sxs-lookup"><span data-stu-id="c40a9-129">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="c40a9-130">Klass: **GetUnBilledConsumptionReconLineItemsPaging.cs**</span><span class="sxs-lookup"><span data-stu-id="c40a9-130">Class: **GetUnBilledConsumptionReconLineItemsPaging.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="c40a9-131">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="c40a9-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c40a9-132">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="c40a9-132">Request syntax</span></span>

<span data-ttu-id="c40a9-133">Du kan använda följande syntax för din REST-begäran, beroende på ditt användnings fall.</span><span class="sxs-lookup"><span data-stu-id="c40a9-133">You can use the following syntaxes for your REST request, depending on your use case.</span></span> <span data-ttu-id="c40a9-134">Mer information finns i beskrivningarna för varje syntax.</span><span class="sxs-lookup"><span data-stu-id="c40a9-134">For more information, see the descriptions for each syntax.</span></span>

 | <span data-ttu-id="c40a9-135">Metod</span><span class="sxs-lookup"><span data-stu-id="c40a9-135">Method</span></span>  | <span data-ttu-id="c40a9-136">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="c40a9-136">Request URI</span></span>         | <span data-ttu-id="c40a9-137">Beskrivning av användnings fall för syntax</span><span class="sxs-lookup"><span data-stu-id="c40a9-137">Description of syntax use case</span></span> |                                                                                                                                            |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="c40a9-138">**TA**</span><span class="sxs-lookup"><span data-stu-id="c40a9-138">**GET**</span></span> | <span data-ttu-id="c40a9-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/INVOICES/unbilled/lineitems? Provider = Databasmigrering&invoicelineitemtype = usagelineitems&CurrencyCode = {currencycode} &period = {period} http/1.1</span><span class="sxs-lookup"><span data-stu-id="c40a9-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period} HTTP/1.1</span></span>                              | <span data-ttu-id="c40a9-140">Använd den här syntaxen för att returnera en fullständig lista över varje rad objekt för den aktuella fakturan.</span><span class="sxs-lookup"><span data-stu-id="c40a9-140">Use this syntax to return a full list of every line item for the given invoice.</span></span> |
| <span data-ttu-id="c40a9-141">**TA**</span><span class="sxs-lookup"><span data-stu-id="c40a9-141">**GET**</span></span> | <span data-ttu-id="c40a9-142">[*{baseURL}*](partner-center-rest-urls.md)/v1/INVOICES/unbilled/lineitems? Provider = Databasmigrering&invoicelineitemtype = usagelineitems&CurrencyCode = {currencycode} &period = {period} &storlek = {size} http/1.1</span><span class="sxs-lookup"><span data-stu-id="c40a9-142">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period}&size={size} HTTP/1.1</span></span>  | <span data-ttu-id="c40a9-143">Använd den här syntaxen för stora fakturor.</span><span class="sxs-lookup"><span data-stu-id="c40a9-143">Use this syntax for large invoices.</span></span> <span data-ttu-id="c40a9-144">Använd den här syntaxen med en angiven storlek och 0-baserad förskjutning för att returnera en växlad lista med rad objekt.</span><span class="sxs-lookup"><span data-stu-id="c40a9-144">Use this syntax with a specified size and 0-based offset to return a paged list of line items.</span></span> |
| <span data-ttu-id="c40a9-145">**TA**</span><span class="sxs-lookup"><span data-stu-id="c40a9-145">**GET**</span></span> | <span data-ttu-id="c40a9-146">[*{baseURL}*](partner-center-rest-urls.md)/v1/INVOICES/unbilled/lineitems? Provider = Databasmigrering&invoicelineitemtype = usagelineitems&CurrencyCode = {currencycode} &period = {period} &storlek = {size} &SeekOperation = nästa</span><span class="sxs-lookup"><span data-stu-id="c40a9-146">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period}&size={size}&seekOperation=Next</span></span>                               | <span data-ttu-id="c40a9-147">Använd den här syntaxen för att hämta nästa sida av avstämnings rad objekt med `seekOperation = "Next"` .</span><span class="sxs-lookup"><span data-stu-id="c40a9-147">Use this syntax to get the next page of reconciliation line items using `seekOperation = "Next"`.</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="c40a9-148">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="c40a9-148">URI parameters</span></span>

<span data-ttu-id="c40a9-149">Använd följande URI och frågeparametrar när du skapar begäran.</span><span class="sxs-lookup"><span data-stu-id="c40a9-149">Use the following URI and query parameters when creating the request.</span></span>

| <span data-ttu-id="c40a9-150">Namn</span><span class="sxs-lookup"><span data-stu-id="c40a9-150">Name</span></span>                   | <span data-ttu-id="c40a9-151">Typ</span><span class="sxs-lookup"><span data-stu-id="c40a9-151">Type</span></span>   | <span data-ttu-id="c40a9-152">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="c40a9-152">Required</span></span> | <span data-ttu-id="c40a9-153">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="c40a9-153">Description</span></span>                                                                     |
|------------------------|--------|----------|---------------------------------------------------------------------------------|
| <span data-ttu-id="c40a9-154">CSP</span><span class="sxs-lookup"><span data-stu-id="c40a9-154">provider</span></span>               | <span data-ttu-id="c40a9-155">sträng</span><span class="sxs-lookup"><span data-stu-id="c40a9-155">string</span></span> | <span data-ttu-id="c40a9-156">Ja</span><span class="sxs-lookup"><span data-stu-id="c40a9-156">Yes</span></span>      | <span data-ttu-id="c40a9-157">Providern: "**Databasmigrering**".</span><span class="sxs-lookup"><span data-stu-id="c40a9-157">The provider: "**OneTime**".</span></span>                                                |
| <span data-ttu-id="c40a9-158">faktura-rad-objekt-typ</span><span class="sxs-lookup"><span data-stu-id="c40a9-158">invoice-line-item-type</span></span> | <span data-ttu-id="c40a9-159">sträng</span><span class="sxs-lookup"><span data-stu-id="c40a9-159">string</span></span> | <span data-ttu-id="c40a9-160">Ja</span><span class="sxs-lookup"><span data-stu-id="c40a9-160">Yes</span></span>      | <span data-ttu-id="c40a9-161">Typ av faktura information: "**UsageLineItems**", "**UsageLineItems**".</span><span class="sxs-lookup"><span data-stu-id="c40a9-161">The type of invoice detail: "**UsageLineItems**", "**UsageLineItems**".</span></span>               |
| <span data-ttu-id="c40a9-162">currencyCode</span><span class="sxs-lookup"><span data-stu-id="c40a9-162">currencyCode</span></span>           | <span data-ttu-id="c40a9-163">sträng</span><span class="sxs-lookup"><span data-stu-id="c40a9-163">string</span></span> | <span data-ttu-id="c40a9-164">Ja</span><span class="sxs-lookup"><span data-stu-id="c40a9-164">Yes</span></span>      | <span data-ttu-id="c40a9-165">Valuta koden för de ej fakturerade rad artiklarna.</span><span class="sxs-lookup"><span data-stu-id="c40a9-165">The currency code for the unbilled line items.</span></span>                                  |
| <span data-ttu-id="c40a9-166">period</span><span class="sxs-lookup"><span data-stu-id="c40a9-166">period</span></span>                 | <span data-ttu-id="c40a9-167">sträng</span><span class="sxs-lookup"><span data-stu-id="c40a9-167">string</span></span> | <span data-ttu-id="c40a9-168">Ja</span><span class="sxs-lookup"><span data-stu-id="c40a9-168">Yes</span></span>      | <span data-ttu-id="c40a9-169">Perioden för ej fakturerade rekognoseringar (t. ex. **aktuell**, **föregående**).</span><span class="sxs-lookup"><span data-stu-id="c40a9-169">The period for unbilled recon (for example: **current**, **previous**).</span></span> <span data-ttu-id="c40a9-170">Anta att du behöver fråga dina ej fakturerade användnings data för fakturerings cykeln (01/01/2020 – 01/31/2020) i januari väljer du period som **"nuvarande,"** Else **"föregående."**</span><span class="sxs-lookup"><span data-stu-id="c40a9-170">Suppose you need to query your unbilled usage data of the billing cycle (01/01/2020 – 01/31/2020) in January, choose period as **“Current,”** else **“Previous.”**</span></span> |
| <span data-ttu-id="c40a9-171">ikoner</span><span class="sxs-lookup"><span data-stu-id="c40a9-171">size</span></span>                   | <span data-ttu-id="c40a9-172">antal</span><span class="sxs-lookup"><span data-stu-id="c40a9-172">number</span></span> | <span data-ttu-id="c40a9-173">Inga</span><span class="sxs-lookup"><span data-stu-id="c40a9-173">No</span></span>       | <span data-ttu-id="c40a9-174">Det maximala antalet objekt som ska returneras.</span><span class="sxs-lookup"><span data-stu-id="c40a9-174">The maximum number of items to return.</span></span> <span data-ttu-id="c40a9-175">Standard storleken är 2000.</span><span class="sxs-lookup"><span data-stu-id="c40a9-175">The default size is 2000.</span></span>                    |
| <span data-ttu-id="c40a9-176">seekOperation</span><span class="sxs-lookup"><span data-stu-id="c40a9-176">seekOperation</span></span>          | <span data-ttu-id="c40a9-177">sträng</span><span class="sxs-lookup"><span data-stu-id="c40a9-177">string</span></span> | <span data-ttu-id="c40a9-178">No</span><span class="sxs-lookup"><span data-stu-id="c40a9-178">No</span></span>       | <span data-ttu-id="c40a9-179">Ställ in `seekOperation=Next` för att hämta nästa sida med avstämnings rad objekt.</span><span class="sxs-lookup"><span data-stu-id="c40a9-179">Set `seekOperation=Next` to get the next page of reconciliation line items.</span></span>                |

### <a name="request-headers"></a><span data-ttu-id="c40a9-180">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="c40a9-180">Request headers</span></span>

<span data-ttu-id="c40a9-181">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="c40a9-181">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="c40a9-182">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="c40a9-182">Request body</span></span>

<span data-ttu-id="c40a9-183">Inga.</span><span class="sxs-lookup"><span data-stu-id="c40a9-183">None.</span></span>

## <a name="rest-response"></a><span data-ttu-id="c40a9-184">REST-svar</span><span class="sxs-lookup"><span data-stu-id="c40a9-184">REST response</span></span>

<span data-ttu-id="c40a9-185">Om det lyckas innehåller svaret insamling av rad objekts information.</span><span class="sxs-lookup"><span data-stu-id="c40a9-185">If successful, the response contains the collection of line item details.</span></span>

<span data-ttu-id="c40a9-186">*För rad posten **ChargeType** mappas värdet **inköp** till **New** och värdet **reexporten** mappas för att **avbryta**.*</span><span class="sxs-lookup"><span data-stu-id="c40a9-186">*For the line item **ChargeType**, the value **Purchase** is mapped to **New** and the value **Refund** is mapped to **Cancel**.*</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c40a9-187">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="c40a9-187">Response success and error codes</span></span>

<span data-ttu-id="c40a9-188">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="c40a9-188">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c40a9-189">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="c40a9-189">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c40a9-190">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="c40a9-190">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

## <a name="request-response-examples"></a><span data-ttu-id="c40a9-191">Exempel på begäran-svar</span><span class="sxs-lookup"><span data-stu-id="c40a9-191">Request-response examples</span></span>

### <a name="request-response-example-1"></a><span data-ttu-id="c40a9-192">Request-Response-exempel 1</span><span class="sxs-lookup"><span data-stu-id="c40a9-192">Request-response example 1</span></span>

<span data-ttu-id="c40a9-193">Följande information gäller för det här exemplet:</span><span class="sxs-lookup"><span data-stu-id="c40a9-193">The following details apply to this example:</span></span>

- <span data-ttu-id="c40a9-194">**Provider**: **Databasmigrering**</span><span class="sxs-lookup"><span data-stu-id="c40a9-194">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="c40a9-195">**InvoiceLineItemType**: **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="c40a9-195">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="c40a9-196">**Period**: **föregående**</span><span class="sxs-lookup"><span data-stu-id="c40a9-196">**Period**: **Previous**</span></span>

#### <a name="request-example-1"></a><span data-ttu-id="c40a9-197">Exempel på begäran 1</span><span class="sxs-lookup"><span data-stu-id="c40a9-197">Request example 1</span></span>

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

### <a name="response-example-1"></a><span data-ttu-id="c40a9-198">Svars exempel 1</span><span class="sxs-lookup"><span data-stu-id="c40a9-198">Response example 1</span></span>

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

### <a name="request-response-example-2"></a><span data-ttu-id="c40a9-199">Request-Response-exempel 2</span><span class="sxs-lookup"><span data-stu-id="c40a9-199">Request-response example 2</span></span>

<span data-ttu-id="c40a9-200">Följande information gäller för det här exemplet:</span><span class="sxs-lookup"><span data-stu-id="c40a9-200">The following details apply to this example:</span></span>

- <span data-ttu-id="c40a9-201">**Provider**: **Databasmigrering**</span><span class="sxs-lookup"><span data-stu-id="c40a9-201">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="c40a9-202">**InvoiceLineItemType**: **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="c40a9-202">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="c40a9-203">**Period**: **föregående**</span><span class="sxs-lookup"><span data-stu-id="c40a9-203">**Period**: **Previous**</span></span>
- <span data-ttu-id="c40a9-204">**SeekOperation**: **Nästa**</span><span class="sxs-lookup"><span data-stu-id="c40a9-204">**SeekOperation**: **Next**</span></span>

#### <a name="request-example-2"></a><span data-ttu-id="c40a9-205">Exempel på begäran 2</span><span class="sxs-lookup"><span data-stu-id="c40a9-205">Request example 2</span></span>

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

#### <a name="response-example-2"></a><span data-ttu-id="c40a9-206">Svars exempel 2</span><span class="sxs-lookup"><span data-stu-id="c40a9-206">Response example 2</span></span>

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
            "rateOfPartnerEarnedCredit": 0,
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
