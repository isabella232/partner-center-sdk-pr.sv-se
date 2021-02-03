---
title: Hämta en lista över kunder
description: Så här hämtar du en samling resurser som representerar alla partners kunder.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 2dd8469458809ab38b6d6081adc91d6d1184d2d0
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769630"
---
# <a name="get-a-list-of-customers"></a><span data-ttu-id="4719f-103">Hämta en lista över kunder</span><span class="sxs-lookup"><span data-stu-id="4719f-103">Get a list of customers</span></span>

<span data-ttu-id="4719f-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="4719f-104">**Applies to:**</span></span>

- <span data-ttu-id="4719f-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="4719f-105">Partner Center</span></span>
- <span data-ttu-id="4719f-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="4719f-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="4719f-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="4719f-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="4719f-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="4719f-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="4719f-109">Den här artikeln beskriver hur du får en samling resurser som representerar alla partners kunder.</span><span class="sxs-lookup"><span data-stu-id="4719f-109">This article describes how to get a collection of resources that represents all of a partner's customers.</span></span>

> [!TIP]
> <span data-ttu-id="4719f-110">Du kan också utföra den här åtgärden på instrument panelen för partner Center.</span><span class="sxs-lookup"><span data-stu-id="4719f-110">You can also perform this operation in the Partner Center dashboard.</span></span> <span data-ttu-id="4719f-111">Välj **Visa kunder** under **kund hantering** på huvud sidan.</span><span class="sxs-lookup"><span data-stu-id="4719f-111">On the main page, under **Customer management**, select **View Customers**.</span></span> <span data-ttu-id="4719f-112">Eller Välj **kunder** på sid panelen.</span><span class="sxs-lookup"><span data-stu-id="4719f-112">Or, on the sidebar, select **Customers**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4719f-113">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="4719f-113">Prerequisites</span></span>

- <span data-ttu-id="4719f-114">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="4719f-114">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4719f-115">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="4719f-115">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="4719f-116">C\#</span><span class="sxs-lookup"><span data-stu-id="4719f-116">C\#</span></span>

<span data-ttu-id="4719f-117">Så här hämtar du en lista över alla kunder:</span><span class="sxs-lookup"><span data-stu-id="4719f-117">To get a list of all customers:</span></span>

1. <span data-ttu-id="4719f-118">Använd [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) -samlingen för att skapa ett **IPartner** -objekt.</span><span class="sxs-lookup"><span data-stu-id="4719f-118">Use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection to create an **IPartner** object.</span></span>

2. <span data-ttu-id="4719f-119">Hämta kund listan med metoderna [**query ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) eller [**QueryAsync ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) .</span><span class="sxs-lookup"><span data-stu-id="4719f-119">Retrieve the customer list using the [**Query()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) or [**QueryAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) methods.</span></span> <span data-ttu-id="4719f-120">(Instruktioner om hur du skapar en fråga finns i klassen [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) .)</span><span class="sxs-lookup"><span data-stu-id="4719f-120">(For instructions on creating a query, see the [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) class.)</span></span>

``` csharp
// IAggregatePartner partnerOperations;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// read customers into chunks of 40s
var customersBatch = scopedPartnerOperations.Customers.Query(QueryFactory.Instance.BuildIndexedQuery(40));
var customersEnumerator = scopedPartnerOperations.Enumerators.Customers.Create(customersBatch);
```

<span data-ttu-id="4719f-121">Ett exempel finns i följande avsnitt:</span><span class="sxs-lookup"><span data-stu-id="4719f-121">For an example, see the following:</span></span>

- <span data-ttu-id="4719f-122">Exempel: [konsol test app](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="4719f-122">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="4719f-123">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="4719f-123">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="4719f-124">Klass: **CustomerPaging.cs**</span><span class="sxs-lookup"><span data-stu-id="4719f-124">Class: **CustomerPaging.cs**</span></span>

## <a name="java"></a><span data-ttu-id="4719f-125">Java</span><span class="sxs-lookup"><span data-stu-id="4719f-125">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="4719f-126">Så här hämtar du en lista över alla kunder:</span><span class="sxs-lookup"><span data-stu-id="4719f-126">To get a list of all customers:</span></span>

1. <span data-ttu-id="4719f-127">Använd funktionen [**IAggregatePartner. getCustomers**] för att få en referens till kund åtgärderna.</span><span class="sxs-lookup"><span data-stu-id="4719f-127">Use the [**IAggregatePartner.getCustomers**] function to get a reference to the customer operations.</span></span>

2. <span data-ttu-id="4719f-128">Hämta kund listan med funktionen **query ()** .</span><span class="sxs-lookup"><span data-stu-id="4719f-128">Retrieve the customer list using the **query()** function.</span></span>

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

## <a name="powershell"></a><span data-ttu-id="4719f-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4719f-129">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="4719f-130">Kör kommandot [**Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) utan parametrar för att få en fullständig lista över kunder.</span><span class="sxs-lookup"><span data-stu-id="4719f-130">Execute the [**Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) command with no parameters to get a complete list of customers.</span></span>

```powershell
Get-PartnerCustomer
```

## <a name="rest-request"></a><span data-ttu-id="4719f-131">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="4719f-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4719f-132">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="4719f-132">Request syntax</span></span>

| <span data-ttu-id="4719f-133">Metod</span><span class="sxs-lookup"><span data-stu-id="4719f-133">Method</span></span>  | <span data-ttu-id="4719f-134">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="4719f-134">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="4719f-135">**TA**</span><span class="sxs-lookup"><span data-stu-id="4719f-135">**GET**</span></span> | <span data-ttu-id="4719f-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers? size = {size} http/1.1</span><span class="sxs-lookup"><span data-stu-id="4719f-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="4719f-137">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="4719f-137">URI parameter</span></span>

<span data-ttu-id="4719f-138">Använd följande frågeparameter för att hämta en lista över kunder.</span><span class="sxs-lookup"><span data-stu-id="4719f-138">Use the following query parameter to get a list of customers.</span></span>

| <span data-ttu-id="4719f-139">Namn</span><span class="sxs-lookup"><span data-stu-id="4719f-139">Name</span></span>     | <span data-ttu-id="4719f-140">Typ</span><span class="sxs-lookup"><span data-stu-id="4719f-140">Type</span></span>    | <span data-ttu-id="4719f-141">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="4719f-141">Required</span></span> | <span data-ttu-id="4719f-142">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="4719f-142">Description</span></span>                                        |
|----------|---------|----------|----------------------------------------------------|
| <span data-ttu-id="4719f-143">**ändra**</span><span class="sxs-lookup"><span data-stu-id="4719f-143">**size**</span></span> | <span data-ttu-id="4719f-144">**int**</span><span class="sxs-lookup"><span data-stu-id="4719f-144">**int**</span></span> | <span data-ttu-id="4719f-145">Y</span><span class="sxs-lookup"><span data-stu-id="4719f-145">Y</span></span>        | <span data-ttu-id="4719f-146">Antalet resultat som ska visas samtidigt.</span><span class="sxs-lookup"><span data-stu-id="4719f-146">The number of results to be displayed at one time.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="4719f-147">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="4719f-147">Request headers</span></span>

<span data-ttu-id="4719f-148">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="4719f-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4719f-149">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="4719f-149">Request body</span></span>

<span data-ttu-id="4719f-150">Inga.</span><span class="sxs-lookup"><span data-stu-id="4719f-150">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="4719f-151">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="4719f-151">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=40 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a><span data-ttu-id="4719f-152">REST-svar</span><span class="sxs-lookup"><span data-stu-id="4719f-152">REST response</span></span>

<span data-ttu-id="4719f-153">Om det lyckas returnerar den här metoden en samling [kund](customer-resources.md#customer) resurser i svars texten.</span><span class="sxs-lookup"><span data-stu-id="4719f-153">If successful, this method returns a collection of [Customer](customer-resources.md#customer) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4719f-154">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="4719f-154">Response success and error codes</span></span>

<span data-ttu-id="4719f-155">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="4719f-155">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4719f-156">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="4719f-156">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="4719f-157">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="4719f-157">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="4719f-158">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="4719f-158">Response example</span></span>

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
