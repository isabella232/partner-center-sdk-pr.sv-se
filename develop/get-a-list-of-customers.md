---
title: Hämta en lista över kunder
description: Hur du hämtar en samling resurser som representerar alla en partners kunder.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 840c9d1a61451763d37a19639f99b12f1deb7521
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874354"
---
# <a name="get-a-list-of-customers"></a><span data-ttu-id="69bf3-103">Hämta en lista över kunder</span><span class="sxs-lookup"><span data-stu-id="69bf3-103">Get a list of customers</span></span>

<span data-ttu-id="69bf3-104">**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="69bf3-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="69bf3-105">Den här artikeln beskriver hur du hämtar en samling resurser som representerar alla en partners kunder.</span><span class="sxs-lookup"><span data-stu-id="69bf3-105">This article describes how to get a collection of resources that represents all of a partner's customers.</span></span>

> [!TIP]
> <span data-ttu-id="69bf3-106">Du kan också utföra den här åtgärden på instrumentpanelen i Partnercenter.</span><span class="sxs-lookup"><span data-stu-id="69bf3-106">You can also perform this operation in the Partner Center dashboard.</span></span> <span data-ttu-id="69bf3-107">På huvudsidan går du till **Kundhantering och** väljer **Visa kunder.**</span><span class="sxs-lookup"><span data-stu-id="69bf3-107">On the main page, under **Customer management**, select **View Customers**.</span></span> <span data-ttu-id="69bf3-108">Eller välj Kunder i **sidopanelen.**</span><span class="sxs-lookup"><span data-stu-id="69bf3-108">Or, on the sidebar, select **Customers**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="69bf3-109">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="69bf3-109">Prerequisites</span></span>

- <span data-ttu-id="69bf3-110">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="69bf3-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="69bf3-111">Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="69bf3-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="69bf3-112">C\#</span><span class="sxs-lookup"><span data-stu-id="69bf3-112">C\#</span></span>

<span data-ttu-id="69bf3-113">Så här hämtar du en lista över alla kunder:</span><span class="sxs-lookup"><span data-stu-id="69bf3-113">To get a list of all customers:</span></span>

1. <span data-ttu-id="69bf3-114">Använd samlingen [**IAggregatePartner.Customers för**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) att skapa ett **IPartner-objekt.**</span><span class="sxs-lookup"><span data-stu-id="69bf3-114">Use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection to create an **IPartner** object.</span></span>

2. <span data-ttu-id="69bf3-115">Hämta kundlistan med metoderna [**Query()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) [**eller QueryAsync().**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync)</span><span class="sxs-lookup"><span data-stu-id="69bf3-115">Retrieve the customer list using the [**Query()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) or [**QueryAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) methods.</span></span> <span data-ttu-id="69bf3-116">(Anvisningar om hur du skapar en fråga finns i [**klassen QueryFactory.)**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory)</span><span class="sxs-lookup"><span data-stu-id="69bf3-116">(For instructions on creating a query, see the [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) class.)</span></span>

``` csharp
// IAggregatePartner partnerOperations;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// read customers into chunks of 40s
var customersBatch = scopedPartnerOperations.Customers.Query(QueryFactory.Instance.BuildIndexedQuery(40));
var customersEnumerator = scopedPartnerOperations.Enumerators.Customers.Create(customersBatch);
```

<span data-ttu-id="69bf3-117">Ett exempel finns i följande:</span><span class="sxs-lookup"><span data-stu-id="69bf3-117">For an example, see the following:</span></span>

- <span data-ttu-id="69bf3-118">Exempel: [Konsoltestapp](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="69bf3-118">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="69bf3-119">Project: **PartnerSDK.FeatureExempel**</span><span class="sxs-lookup"><span data-stu-id="69bf3-119">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="69bf3-120">Klass: **CustomerPaging.cs**</span><span class="sxs-lookup"><span data-stu-id="69bf3-120">Class: **CustomerPaging.cs**</span></span>

## <a name="java"></a><span data-ttu-id="69bf3-121">Java</span><span class="sxs-lookup"><span data-stu-id="69bf3-121">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="69bf3-122">Så här hämtar du en lista över alla kunder:</span><span class="sxs-lookup"><span data-stu-id="69bf3-122">To get a list of all customers:</span></span>

1. <span data-ttu-id="69bf3-123">Använd funktionen [**IAggregatePartner.getCustomers**] för att hämta en referens till kundåtgärderna.</span><span class="sxs-lookup"><span data-stu-id="69bf3-123">Use the [**IAggregatePartner.getCustomers**] function to get a reference to the customer operations.</span></span>

2. <span data-ttu-id="69bf3-124">Hämta kundlistan med hjälp av **funktionen query().**</span><span class="sxs-lookup"><span data-stu-id="69bf3-124">Retrieve the customer list using the **query()** function.</span></span>

```java
// Query the customers, get the first page if a page size was set, otherwise get all customers
SeekBasedResourceCollection<Customer> customersPage = partnerOperations.getCustomers().query(QueryFactory.getInstance().buildIndexedQuery(40));

// Create a customer enumerator which will aid us in traversing the customer pages
IResourceCollectionEnumerator<SeekBasedResourceCollection<Customer>> customersEnumerator =
    partnerOperations.getEnumerators().getCustomers().create( customersPage );

int pageNumber = 1;

while (customersEnumerator.hasValue())
{
    /*
     * Use the customersEnumerator.getCurrent() function to
     * access the current page of customers.
     */

    // Get the next page of customers
    customersEnumerator.next();
}
```

## <a name="powershell"></a><span data-ttu-id="69bf3-125">PowerShell</span><span class="sxs-lookup"><span data-stu-id="69bf3-125">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="69bf3-126">Kör kommandot [**Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) utan parametrar för att få en fullständig lista över kunder.</span><span class="sxs-lookup"><span data-stu-id="69bf3-126">Execute the [**Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) command with no parameters to get a complete list of customers.</span></span>

```powershell
Get-PartnerCustomer
```

## <a name="rest-request"></a><span data-ttu-id="69bf3-127">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="69bf3-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="69bf3-128">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="69bf3-128">Request syntax</span></span>

| <span data-ttu-id="69bf3-129">Metod</span><span class="sxs-lookup"><span data-stu-id="69bf3-129">Method</span></span>  | <span data-ttu-id="69bf3-130">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="69bf3-130">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="69bf3-131">**Få**</span><span class="sxs-lookup"><span data-stu-id="69bf3-131">**GET**</span></span> | <span data-ttu-id="69bf3-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="69bf3-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="69bf3-133">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="69bf3-133">URI parameter</span></span>

<span data-ttu-id="69bf3-134">Använd följande frågeparameter för att hämta en lista över kunder.</span><span class="sxs-lookup"><span data-stu-id="69bf3-134">Use the following query parameter to get a list of customers.</span></span>

| <span data-ttu-id="69bf3-135">Namn</span><span class="sxs-lookup"><span data-stu-id="69bf3-135">Name</span></span>     | <span data-ttu-id="69bf3-136">Typ</span><span class="sxs-lookup"><span data-stu-id="69bf3-136">Type</span></span>    | <span data-ttu-id="69bf3-137">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="69bf3-137">Required</span></span> | <span data-ttu-id="69bf3-138">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="69bf3-138">Description</span></span>                                        |
|----------|---------|----------|----------------------------------------------------|
| <span data-ttu-id="69bf3-139">**Storlek**</span><span class="sxs-lookup"><span data-stu-id="69bf3-139">**size**</span></span> | <span data-ttu-id="69bf3-140">**int**</span><span class="sxs-lookup"><span data-stu-id="69bf3-140">**int**</span></span> | <span data-ttu-id="69bf3-141">Y</span><span class="sxs-lookup"><span data-stu-id="69bf3-141">Y</span></span>        | <span data-ttu-id="69bf3-142">Antalet resultat som ska visas samtidigt.</span><span class="sxs-lookup"><span data-stu-id="69bf3-142">The number of results to be displayed at one time.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="69bf3-143">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="69bf3-143">Request headers</span></span>

<span data-ttu-id="69bf3-144">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="69bf3-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="69bf3-145">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="69bf3-145">Request body</span></span>

<span data-ttu-id="69bf3-146">Inga.</span><span class="sxs-lookup"><span data-stu-id="69bf3-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="69bf3-147">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="69bf3-147">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=40 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a><span data-ttu-id="69bf3-148">REST-svar</span><span class="sxs-lookup"><span data-stu-id="69bf3-148">REST response</span></span>

<span data-ttu-id="69bf3-149">Om det lyckas returnerar den här metoden en samling [kundresurser](customer-resources.md#customer) i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="69bf3-149">If successful, this method returns a collection of [Customer](customer-resources.md#customer) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="69bf3-150">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="69bf3-150">Response success and error codes</span></span>

<span data-ttu-id="69bf3-151">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="69bf3-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="69bf3-152">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="69bf3-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="69bf3-153">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="69bf3-153">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="69bf3-154">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="69bf3-154">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 15650
Content-Type: application/json
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
Date: Fri, 20 Nov 2015 01:08:23 GMT

{
    "totalCount": 2,
    "items": [{
        "id": "b44bb1fb-c595-45b0-9e09-d657365580bf",
        "companyProfile": {
            "tenantId": "<guid>",
            "domain": "domain",
            "companyName": "companyName",
            "attributes": {
                "objectType": "CustomerCompanyProfile"
            }
        },
        "relationshipToPartner": "reseller",
        "attributes": {
            "objectType": "Customer"
        }
    },
    {
        "id": "45c44870-ef77-4fdd-b6fe-3dacb075cff2",
        "companyProfile": {
            "tenantId": "<guid>",
            "domain": "domain",
            "companyName": "companyName",
            "attributes": {
                "objectType": "CustomerCompanyProfile"
            }
        },
        "relationshipToPartner": "reseller",
        "attributes": {
            "objectType": "Customer"
        }
    }],
    "links": {
        "self": {
            "uri": "/v1/customers?size=40",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
