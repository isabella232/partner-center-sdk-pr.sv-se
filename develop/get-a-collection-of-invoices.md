---
title: Hämta en samling fakturor
description: Hämta en samling av partnerns fakturor.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: f56c3de8dd227f573921e5b969c2217c2f743a21
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769288"
---
# <a name="get-a-collection-of-invoices"></a><span data-ttu-id="d87ad-103">Hämta en samling fakturor</span><span class="sxs-lookup"><span data-stu-id="d87ad-103">Get a collection of invoices</span></span>

<span data-ttu-id="d87ad-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="d87ad-104">**Applies To**</span></span>

- <span data-ttu-id="d87ad-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="d87ad-105">Partner Center</span></span>
- <span data-ttu-id="d87ad-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="d87ad-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="d87ad-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="d87ad-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="d87ad-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="d87ad-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d87ad-109">Hämta en samling av partnerns fakturor.</span><span class="sxs-lookup"><span data-stu-id="d87ad-109">How to retrieve a collection of the partner's invoices.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d87ad-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="d87ad-110">Prerequisites</span></span>

- <span data-ttu-id="d87ad-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d87ad-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d87ad-112">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="d87ad-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="d87ad-113">C\#</span><span class="sxs-lookup"><span data-stu-id="d87ad-113">C\#</span></span>

<span data-ttu-id="d87ad-114">Om du vill hämta en samling med alla tillgängliga fakturor använder du egenskapen [**fakturor**](/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) för att hämta ett gränssnitt till faktura åtgärder och anropar sedan metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.getasync) för att hämta samlingen.</span><span class="sxs-lookup"><span data-stu-id="d87ad-114">To get a collection of all available invoices, use the [**Invoices**](/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) property to get an interface to invoice operations, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.getasync) method to retrieve the collection.</span></span>

<span data-ttu-id="d87ad-115">För att få en sida med fakturor, anropa först metoden [**BuildIndexedQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) och skicka den till sid storleken för att skapa ett [**IQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) -objekt.</span><span class="sxs-lookup"><span data-stu-id="d87ad-115">To get a paged collection of invoices, first call the [**BuildIndexedQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) method and pass it the page size to create an [**IQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) object.</span></span> <span data-ttu-id="d87ad-116">Använd sedan egenskapen [**fakturor**](/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) för att hämta ett gränssnitt för att fakturera åtgärder och skicka sedan IQuery-objektet till [**frågan**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.query) eller [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.queryasync) -metoden för att skicka begäran och hämta den första sidan.</span><span class="sxs-lookup"><span data-stu-id="d87ad-116">Next, use the [**Invoices**](/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) property to get an interface to invoice operations, and then pass the IQuery object to the [**Query**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.query) or [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.queryasync) method to send the request and get the first page.</span></span>

<span data-ttu-id="d87ad-117">Använd sedan egenskapen [**uppräknings**](/dotnet/api/microsoft.store.partnercenter.ipartner.enumerators) egenskap för att hämta ett gränssnitt till samlingen med uppräknare för insamlade resurs samlingar som stöds och sedan anropa [**fakturor. Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) för att gå igenom mängden med fakturor.</span><span class="sxs-lookup"><span data-stu-id="d87ad-117">Next, use the [**Enumerators**](/dotnet/api/microsoft.store.partnercenter.ipartner.enumerators) property to get an interface to the collection of supported resource collection enumerators, and then call [**Invoices.Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) to create an enumerator for traversing the collection of invoices.</span></span> <span data-ttu-id="d87ad-118">Slutligen använder du uppräkna ren för att hämta och arbeta med varje sida med fakturor, som du ser i följande kod exempel.</span><span class="sxs-lookup"><span data-stu-id="d87ad-118">Finally, use the enumerator to retrieve and work with each page of invoices as shown in the following code example.</span></span> <span data-ttu-id="d87ad-119">Varje anrop till [**Nästa**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumerator-1.next) Metod skickar en begäran till nästa sida med fakturor baserat på sid storleken.</span><span class="sxs-lookup"><span data-stu-id="d87ad-119">Each call to the [**Next**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumerator-1.next) method sends a request for the next page of invoices based on the page size.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// int invoicePageSize;

// Is this an unpaged or paged request?
bool isUnpaged = (this.invoicePageSize <= 0);

// If the scenario is unpaged, get all the invoices, otherwise get the first page.
var invoicesPage = (isUnpaged)
                 ? partnerOperations.Invoices.Get()
                 : partnerOperations.Invoices.Query(QueryFactory.Instance.BuildIndexedQuery(this.invoicePageSize));

// Create an invoice enumerator for traversing the invoice pages.
var invoicesEnumerator = partnerOperations.Enumerators.Invoices.Create(invoicesPage);
int lineCounter = 1;

while (invoicesEnumerator.HasValue)
{
    // Print the current invoice results page.
    var invoices = invoicesEnumerator.Current.Items;

    foreach (var i in invoices)
    {
        Console.WriteLine(String.Format("{0,3}. {1}  {2}  {3,16:C2}",
            lineCounter++,
            i.Id,
            i.InvoiceDate.ToString("yyyy&#39;-&#39;MM&#39;-&#39;dd&#39;T&#39;HH&#39;:&#39;mm&#39;:&#39;ss&#39;Z&#39;"),
            i.TotalCharges));
    }

    Console.WriteLine();
    Console.Write("Press any key to retrieve the next invoices page");
    Console.ReadKey();

    // Get the next page of invoices.
    invoicesEnumerator.Next();
}
```

<span data-ttu-id="d87ad-120">Ett något annat exempel finns i **exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="d87ad-120">For a slightly different example, see **Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="d87ad-121">**Projekt**: Partner Center SDK-exempel **klass**: GetPagedInvoices.CS</span><span class="sxs-lookup"><span data-stu-id="d87ad-121">**Project**: Partner Center SDK Samples **Class**: GetPagedInvoices.cs</span></span>

> [!NOTE] 
> <span data-ttu-id="d87ad-122">Samma API används för alla moderna kommersiella inköp såväl som 145p-och Office-licenser.</span><span class="sxs-lookup"><span data-stu-id="d87ad-122">The same API is used for all modern commercial purchases as well as 145p and Office licenses.</span></span> <span data-ttu-id="d87ad-123">Storlek och förskjutning räknas bara för äldre fakturor.</span><span class="sxs-lookup"><span data-stu-id="d87ad-123">Size and offset are only considered for legacy invoices.</span></span> <span data-ttu-id="d87ad-124">PageSize & förskjutning kommer att ignoreras för alla moderna kommersiella köp.</span><span class="sxs-lookup"><span data-stu-id="d87ad-124">For all modern commercial purchases, pagesize & offset will be ignored.</span></span>

## <a name="rest-request"></a><span data-ttu-id="d87ad-125">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="d87ad-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d87ad-126">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="d87ad-126">Request syntax</span></span>

| <span data-ttu-id="d87ad-127">Metod</span><span class="sxs-lookup"><span data-stu-id="d87ad-127">Method</span></span>  | <span data-ttu-id="d87ad-128">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="d87ad-128">Request URI</span></span>                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="d87ad-129">**TA**</span><span class="sxs-lookup"><span data-stu-id="d87ad-129">**GET**</span></span> | <span data-ttu-id="d87ad-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/INVOICES? size = {size} &förskjutning = {offset} http/1.1</span><span class="sxs-lookup"><span data-stu-id="d87ad-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices?size={size}&offset={offset} HTTP/1.1</span></span>  |

### <a name="uri-parameters"></a><span data-ttu-id="d87ad-131">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="d87ad-131">URI parameters</span></span>

<span data-ttu-id="d87ad-132">Använd följande frågeparametrar när du skapar begäran.</span><span class="sxs-lookup"><span data-stu-id="d87ad-132">Use the following query parameters when creating the request.</span></span>

| <span data-ttu-id="d87ad-133">Namn</span><span class="sxs-lookup"><span data-stu-id="d87ad-133">Name</span></span>   | <span data-ttu-id="d87ad-134">Typ</span><span class="sxs-lookup"><span data-stu-id="d87ad-134">Type</span></span> | <span data-ttu-id="d87ad-135">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="d87ad-135">Required</span></span> | <span data-ttu-id="d87ad-136">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="d87ad-136">Description</span></span>                                                                            |
|--------|------|----------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="d87ad-137">ikoner</span><span class="sxs-lookup"><span data-stu-id="d87ad-137">size</span></span>   | <span data-ttu-id="d87ad-138">int</span><span class="sxs-lookup"><span data-stu-id="d87ad-138">int</span></span>  | <span data-ttu-id="d87ad-139">No</span><span class="sxs-lookup"><span data-stu-id="d87ad-139">No</span></span>       | <span data-ttu-id="d87ad-140">Antalet faktura resurser som ska returneras i svaret.</span><span class="sxs-lookup"><span data-stu-id="d87ad-140">The number of invoice resources to return in the response.</span></span> <span data-ttu-id="d87ad-141">Den här parametern är valfri.</span><span class="sxs-lookup"><span data-stu-id="d87ad-141">This parameter is optional.</span></span> |
| <span data-ttu-id="d87ad-142">offset</span><span class="sxs-lookup"><span data-stu-id="d87ad-142">offset</span></span> | <span data-ttu-id="d87ad-143">int</span><span class="sxs-lookup"><span data-stu-id="d87ad-143">int</span></span>  | <span data-ttu-id="d87ad-144">No</span><span class="sxs-lookup"><span data-stu-id="d87ad-144">No</span></span>       | <span data-ttu-id="d87ad-145">Det nollbaserade indexet för den första fakturan som ska returneras.</span><span class="sxs-lookup"><span data-stu-id="d87ad-145">The zero-based index of the first invoice to return.</span></span>                                   |

### <a name="request-headers"></a><span data-ttu-id="d87ad-146">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="d87ad-146">Request headers</span></span>

<span data-ttu-id="d87ad-147">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="d87ad-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d87ad-148">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="d87ad-148">Request body</span></span>

<span data-ttu-id="d87ad-149">Inget</span><span class="sxs-lookup"><span data-stu-id="d87ad-149">None</span></span>

### <a name="request-example"></a><span data-ttu-id="d87ad-150">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="d87ad-150">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices?size=200&offset=0 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="d87ad-151">REST-svar</span><span class="sxs-lookup"><span data-stu-id="d87ad-151">REST response</span></span>

<span data-ttu-id="d87ad-152">Om det lyckas innehåller svars texten samlingen av [faktura](invoice-resources.md#invoice) resurser.</span><span class="sxs-lookup"><span data-stu-id="d87ad-152">If successful, the response body contains the collection of [Invoice](invoice-resources.md#invoice) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d87ad-153">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="d87ad-153">Response success and error codes</span></span>

<span data-ttu-id="d87ad-154">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="d87ad-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d87ad-155">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="d87ad-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d87ad-156">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="d87ad-156">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d87ad-157">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="d87ad-157">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 256
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
Date: Thu, 24 Mar 2016 05:21:01 GMT
{
    "totalCount": 2,
    "items": [
        {
            "id": "D02005YFHI",
            "invoiceDate": "2017-01-21T00:00:00Z",
            "totalCharges": 24606.35,
            "paidAmount": 1000,
            "currencyCode": "GBP",
            "currencySymbol": "£",
            "pdfDownloadLink": "/invoices/D02005YFHI/documents/statement",
            "taxReceipts": [
                {
                    "id": "123456",
                    "taxReceiptPdfDownloadLink": "/invoices/D02005YFHI/receipts/123456/documents/statement"
                }
            ],
            "invoiceDetails": [
                {
                    "invoiceLineItemType": "billing_line_items",
                    "billingProvider": "office",
                    "links": {
                        "self": {
                            "uri": "/invoices/Recurring-D02005YFHI/lineitems/Office/BillingLineItems",
                            "method": "GET",
                            "headers": []
                        }
                    },
                    "attributes": {
                        "objectType": "InvoiceDetail"
                    }
                }
            ],
            "documentType": "invoice",
            "invoiceType": "Recurring",
            "links": {
                "self": {
                    "uri": "/invoices/Recurring-D02005YFHI",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Invoice"
            }
        },
        {
            "id": "G000024130",
            "invoiceDate": "2018-02-08T01:22:47.603895Z",
            "totalCharges": 586366,
            "paidAmount": 0,
            "currencyCode": "CHF",
            "currencySymbol": "CHF",
            "pdfDownloadLink": "/invoices/G000024130/documents/statement",
            "taxReceipts": [
                {
                    "id": "234567",
                    "taxReceiptPdfDownloadLink": "/invoices/G000024130/receipts/234567/documents/statement"
                }
            ],
            "invoiceDetails": [
                {
                    "invoiceLineItemType": "billing_line_items",
                    "billingProvider": "one_time",
                    "links": {
                        "self": {
                            "uri": "/invoices/OneTime-G000024130/lineitems/OneTime/BillingLineItems",
                            "method": "GET",
                            "headers": []
                        }
                    },
                    "attributes": {
                        "objectType": "InvoiceDetail"
                    }
                }
            ],
            "amendments": [
                {
                    "id": "G000024131",
                    "invoiceDate": "2018-02-08T18:44:37.5381456Z",
                    "totalCharges": 107661.12,
                    "paidAmount": 0,
                    "currencyCode": "CHF",
                    "currencySymbol": "CHF",
                    "invoiceDetails": [
                        {
                            "invoiceLineItemType": "billing_line_items",
                            "billingProvider": "one_time",
                            "attributes": {
                                "objectType": "InvoiceDetail"
                            }
                        }
                    ],
                    "documentType": "adjustment_note",
                    "amendsOf": "G000024130",
                    "invoiceType": "OneTime",
                    "attributes": {
                        "objectType": "Invoice"
                    }
                }
            ],
            "documentType": "void_note",
            "invoiceType": "OneTime",
            "links": {
                "self": {
                    "uri": "/invoices/OneTime-G000024130",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Invoice"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices?size=2&offset=0",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices?size=2&offset=2",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
