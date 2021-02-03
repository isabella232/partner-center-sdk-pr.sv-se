---
title: Hämta en lista över kunder filtrerade efter ett sökfält
description: Hämtar en samling kund resurser som matchar ett filter. Du kan också ange en sid storlek. Du kan filtrera efter företags namn, domän, indirekt åter försäljare eller CSP (indirekt Cloud Solution Provider).
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: aad9524dbe2c9edbbd7c1d50da7a448f6872fcb9
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769375"
---
# <a name="get-a-list-of-customers-filtered-by-a-search-field"></a><span data-ttu-id="8d71f-105">Hämta en lista över kunder filtrerade efter ett sökfält</span><span class="sxs-lookup"><span data-stu-id="8d71f-105">Get a list of customers filtered by a search field</span></span>

<span data-ttu-id="8d71f-106">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="8d71f-106">**Applies To**</span></span>

- <span data-ttu-id="8d71f-107">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="8d71f-107">Partner Center</span></span>
- <span data-ttu-id="8d71f-108">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="8d71f-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="8d71f-109">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="8d71f-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="8d71f-110">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="8d71f-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="8d71f-111">Hämtar en samling [kund](customer-resources.md#customer) resurser som matchar ett filter.</span><span class="sxs-lookup"><span data-stu-id="8d71f-111">Gets a collection of [Customer](customer-resources.md#customer) resources that match a filter.</span></span> <span data-ttu-id="8d71f-112">Du kan också ange en sid storlek.</span><span class="sxs-lookup"><span data-stu-id="8d71f-112">You can optionally set a page size.</span></span> <span data-ttu-id="8d71f-113">Du kan filtrera efter företags namn, domän, indirekt åter försäljare eller CSP (indirekt Cloud Solution Provider).</span><span class="sxs-lookup"><span data-stu-id="8d71f-113">You can filter by company name, domain, indirect reseller, or indirect cloud solution provider (CSP).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d71f-114">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="8d71f-114">Prerequisites</span></span>

- <span data-ttu-id="8d71f-115">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="8d71f-115">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8d71f-116">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="8d71f-116">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="8d71f-117">Ett användardefinierat filter.</span><span class="sxs-lookup"><span data-stu-id="8d71f-117">A user-constructed filter.</span></span>

## <a name="c"></a><span data-ttu-id="8d71f-118">C\#</span><span class="sxs-lookup"><span data-stu-id="8d71f-118">C\#</span></span>

<span data-ttu-id="8d71f-119">Om du vill hämta en samling kunder som matchar ett filter måste du först instansiera ett [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) -objekt för att skapa filtret.</span><span class="sxs-lookup"><span data-stu-id="8d71f-119">To get a collection of customers that match a filter, first instantiate a [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) object to create the filter.</span></span> <span data-ttu-id="8d71f-120">Du måste skicka en sträng som innehåller [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield)och ange typ av filter åtgärd som [**FieldFilterOperation. StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation).</span><span class="sxs-lookup"><span data-stu-id="8d71f-120">You'll need to pass a string that contains the [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield), and indicate the type of filter operation as [**FieldFilterOperation.StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation).</span></span> <span data-ttu-id="8d71f-121">Det är den enda fält filter åtgärd som stöds av slut punkten för kunder.</span><span class="sxs-lookup"><span data-stu-id="8d71f-121">That's the only field filter operation supported by the customers end point.</span></span> <span data-ttu-id="8d71f-122">Du måste också ange strängen för att filtrera efter.</span><span class="sxs-lookup"><span data-stu-id="8d71f-122">You'll also need to provide the string to filter by.</span></span>

<span data-ttu-id="8d71f-123">Sedan instansierar du ett [**iQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) -objekt för att skicka till frågan genom att anropa metoden [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) och skicka filtret.</span><span class="sxs-lookup"><span data-stu-id="8d71f-123">Next, instantiate an [**iQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) object to pass to the query by calling the [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) method and passing it the filter.</span></span> <span data-ttu-id="8d71f-124">BuildSimplyQuery är bara en av de frågetyper som stöds av [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) -klassen.</span><span class="sxs-lookup"><span data-stu-id="8d71f-124">BuildSimplyQuery is just one of the query types supported by the [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) class.</span></span>

<span data-ttu-id="8d71f-125">Slutligen, om du vill köra filtret och få resultatet, använder du först [**IAggregatePartner. kunder**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) för att få ett gränssnitt till partnerns kund åtgärder.</span><span class="sxs-lookup"><span data-stu-id="8d71f-125">Finally, to execute the filter and get the result, first use [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) to get an interface to the partner's customer operations.</span></span> <span data-ttu-id="8d71f-126">Anropa sedan [**fråge**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) -eller [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) -metoden.</span><span class="sxs-lookup"><span data-stu-id="8d71f-126">Then call the [**Query**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) or [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) method.</span></span>

``` csharp
IAggregatePartner partnerOperations;

// Specify the partial string to filter by (to match Contoso).
string searchPrefix = "cont"

// Create a simple field filter.
var fieldFilter = new SimpleFieldFilter(
    CustomerSearchField.CompanyName.ToString(),
    FieldFilterOperation.StartsWith,
    searchPrefix);

// Create an iQuery object to pass to the Query method.
var myQuery = QueryFactory.Instance.BuildSimpleQuery(fieldFilter);

// Get the collection of matching customers.
var customers = partnerOperations.Customers.Query(myQuery);
```

<span data-ttu-id="8d71f-127">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="8d71f-127">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="8d71f-128">**Projekt**: Partner Center SDK-exempel **klass**: FilterCustomers.CS</span><span class="sxs-lookup"><span data-stu-id="8d71f-128">**Project**: Partner Center SDK Samples **Class**: FilterCustomers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="8d71f-129">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="8d71f-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8d71f-130">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="8d71f-130">Request syntax</span></span>

| <span data-ttu-id="8d71f-131">Metod</span><span class="sxs-lookup"><span data-stu-id="8d71f-131">Method</span></span>  | <span data-ttu-id="8d71f-132">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="8d71f-132">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="8d71f-133">**TA**</span><span class="sxs-lookup"><span data-stu-id="8d71f-133">**GET**</span></span> | <span data-ttu-id="8d71f-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers? size = {size} &filter = {filter} http/1.1</span><span class="sxs-lookup"><span data-stu-id="8d71f-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size}&filter={filter} HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="8d71f-135">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="8d71f-135">URI parameters</span></span>

<span data-ttu-id="8d71f-136">Använd följande frågeparametrar.</span><span class="sxs-lookup"><span data-stu-id="8d71f-136">Use the following query parameters.</span></span>

| <span data-ttu-id="8d71f-137">Namn</span><span class="sxs-lookup"><span data-stu-id="8d71f-137">Name</span></span>   | <span data-ttu-id="8d71f-138">Typ</span><span class="sxs-lookup"><span data-stu-id="8d71f-138">Type</span></span>   | <span data-ttu-id="8d71f-139">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="8d71f-139">Required</span></span> | <span data-ttu-id="8d71f-140">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="8d71f-140">Description</span></span>                                                                    |
|--------|--------|----------|--------------------------------------------------------------------------------|
| <span data-ttu-id="8d71f-141">ikoner</span><span class="sxs-lookup"><span data-stu-id="8d71f-141">size</span></span>   | <span data-ttu-id="8d71f-142">int</span><span class="sxs-lookup"><span data-stu-id="8d71f-142">int</span></span>    | <span data-ttu-id="8d71f-143">No</span><span class="sxs-lookup"><span data-stu-id="8d71f-143">No</span></span>       | <span data-ttu-id="8d71f-144">Antalet resultat som ska visas samtidigt.</span><span class="sxs-lookup"><span data-stu-id="8d71f-144">The number of results to be displayed at one time.</span></span> <span data-ttu-id="8d71f-145">Den här parametern är valfri.</span><span class="sxs-lookup"><span data-stu-id="8d71f-145">This parameter is optional.</span></span> |
| <span data-ttu-id="8d71f-146">filter</span><span class="sxs-lookup"><span data-stu-id="8d71f-146">filter</span></span> | <span data-ttu-id="8d71f-147">filter</span><span class="sxs-lookup"><span data-stu-id="8d71f-147">filter</span></span> | <span data-ttu-id="8d71f-148">Yes</span><span class="sxs-lookup"><span data-stu-id="8d71f-148">Yes</span></span>      | <span data-ttu-id="8d71f-149">Filtret som ska användas för kunderna.</span><span class="sxs-lookup"><span data-stu-id="8d71f-149">The filter to apply to customers.</span></span> <span data-ttu-id="8d71f-150">Detta måste vara en kodad sträng.</span><span class="sxs-lookup"><span data-stu-id="8d71f-150">This must be an encoded string.</span></span>              |

### <a name="filter-syntax"></a><span data-ttu-id="8d71f-151">Filter-syntax</span><span class="sxs-lookup"><span data-stu-id="8d71f-151">Filter Syntax</span></span>

<span data-ttu-id="8d71f-152">Du måste skapa filter parametern som en serie kommaavgränsade par med nyckel/värde-par.</span><span class="sxs-lookup"><span data-stu-id="8d71f-152">You must compose the filter parameter as a series of comma separated, key-value pairs.</span></span> <span data-ttu-id="8d71f-153">Varje nyckel och värde måste anges individuellt och avgränsas med kolon.</span><span class="sxs-lookup"><span data-stu-id="8d71f-153">Each key and value must be individually quoted and separated by a colon.</span></span> <span data-ttu-id="8d71f-154">Hela filtret måste vara kodat.</span><span class="sxs-lookup"><span data-stu-id="8d71f-154">The entire filter must be encoded.</span></span>

<span data-ttu-id="8d71f-155">Ett avkodat exempel ser ut så här:</span><span class="sxs-lookup"><span data-stu-id="8d71f-155">An unencoded example looks like this:</span></span>

```http
?filter{"Field":"CompanyName","Value":"cont","Operator":"starts_with"}
```

<span data-ttu-id="8d71f-156">I följande tabell beskrivs de nyckel/värde-par som krävs:</span><span class="sxs-lookup"><span data-stu-id="8d71f-156">The following table describes the required key-value pairs:</span></span>

| <span data-ttu-id="8d71f-157">Tangent</span><span class="sxs-lookup"><span data-stu-id="8d71f-157">Key</span></span>      | <span data-ttu-id="8d71f-158">Värde</span><span class="sxs-lookup"><span data-stu-id="8d71f-158">Value</span></span>                                                                                                                    |
|----------|--------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8d71f-159">Fält</span><span class="sxs-lookup"><span data-stu-id="8d71f-159">Field</span></span>    | <span data-ttu-id="8d71f-160">Det fält som ska filtreras.</span><span class="sxs-lookup"><span data-stu-id="8d71f-160">The field to filter.</span></span> <span data-ttu-id="8d71f-161">Du hittar giltiga värden i [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield).</span><span class="sxs-lookup"><span data-stu-id="8d71f-161">The valid values can be found in [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield).</span></span> |
| <span data-ttu-id="8d71f-162">Värde</span><span class="sxs-lookup"><span data-stu-id="8d71f-162">Value</span></span>    | <span data-ttu-id="8d71f-163">Värdet att filtrera efter.</span><span class="sxs-lookup"><span data-stu-id="8d71f-163">The value to filter by.</span></span> <span data-ttu-id="8d71f-164">Skift läget för värdet ignoreras.</span><span class="sxs-lookup"><span data-stu-id="8d71f-164">The case of the value is ignored.</span></span>                                                                |
| <span data-ttu-id="8d71f-165">Operator</span><span class="sxs-lookup"><span data-stu-id="8d71f-165">Operator</span></span> | <span data-ttu-id="8d71f-166">Operatorn som ska användas.</span><span class="sxs-lookup"><span data-stu-id="8d71f-166">The operator to apply.</span></span> <span data-ttu-id="8d71f-167">Det enda värde som stöds för det här kund scenariot är "börjar \_ med".</span><span class="sxs-lookup"><span data-stu-id="8d71f-167">The only supported value for this customer scenario is "starts\_with".</span></span>                            |

### <a name="request-headers"></a><span data-ttu-id="8d71f-168">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="8d71f-168">Request headers</span></span>

<span data-ttu-id="8d71f-169">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="8d71f-169">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8d71f-170">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="8d71f-170">Request body</span></span>

<span data-ttu-id="8d71f-171">Inga.</span><span class="sxs-lookup"><span data-stu-id="8d71f-171">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="8d71f-172">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="8d71f-172">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter=%7B%22Field%22%3A%22CompanyName%22%2C%22Value%22%3A%22Cont%22%2C%22Operator%22%3A%22starts_with%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 5ce66de5-eea9-486f-a11c-c852aa3d1502
MS-CorrelationId: a2a912ee-d595-47e2-97ae-1b0ae1efa13d
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="8d71f-173">REST-svar</span><span class="sxs-lookup"><span data-stu-id="8d71f-173">REST response</span></span>

<span data-ttu-id="8d71f-174">Om det lyckas returnerar den här metoden en samling matchande [kund](customer-resources.md#customer) resurser i svars texten.</span><span class="sxs-lookup"><span data-stu-id="8d71f-174">If successful, this method returns a collection of matching [Customer](customer-resources.md#customer) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8d71f-175">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="8d71f-175">Response success and error codes</span></span>

<span data-ttu-id="8d71f-176">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="8d71f-176">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8d71f-177">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="8d71f-177">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8d71f-178">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="8d71f-178">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="8d71f-179">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="8d71f-179">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1839
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a2a912ee-d595-47e2-97ae-1b0ae1efa13d
MS-RequestId: dfeda56c-1af5-43fc-a9c0-346b9e85dc96
MS-CV: n0lMNyJtaUC802pO.0
MS-ServerId: 202010223
Date: Fri, 24 Feb 2017 22:08:20 GMT

{
    "totalCount": 3,
    "items": [{
            "id": "c5757d70-06f3-4f23-8367-5a9e55019f94",
            "companyProfile": {
                "tenantId": "c5757d70-06f3-4f23-8367-5a9e55019f94",
                "domain": "contoso190.onmicrosoft.com",
                "companyName": "Contoso190",
                "links": {
                    "self": {
                        "uri": "/customers/c5757d70-06f3-4f23-8367-5a9e55019f94/profiles/company",
                        "method": "GET",
                        "headers": []
                    }
                },
                "attributes": {
                    "objectType": "CustomerCompanyProfile"
                }
            },
            "relationshipToPartner": "reseller",
            "links": {
                "self": {
                    "uri": "/customers/c5757d70-06f3-4f23-8367-5a9e55019f94",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        }, {
            "id": "7b26b357-9ca3-48b8-a58e-4febe2662a5d",
            "companyProfile": {
                "tenantId": "7b26b357-9ca3-48b8-a58e-4febe2662a5d",
                "domain": "ContosoCorpCo.onmicrosoft.com",
                "companyName": "Contoso",
                "links": {
                    "self": {
                        "uri": "/customers/7b26b357-9ca3-48b8-a58e-4febe2662a5d/profiles/company",
                        "method": "GET",
                        "headers": []
                    }
                },
                "attributes": {
                    "objectType": "CustomerCompanyProfile"
                }
            },
            "relationshipToPartner": "reseller",
            "links": {
                "self": {
                    "uri": "/customers/7b26b357-9ca3-48b8-a58e-4febe2662a5d",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        }, {
            "id": "bfbd6ef0-311f-47ec-bbd7-0fcb7846661b",
            "companyProfile": {
                "tenantId": "bfbd6ef0-311f-47ec-bbd7-0fcb7846661b",
                "domain": "contosocorpdemo.onmicrosoft.com",
                "companyName": "Contoso",
                "links": {
                    "self": {
                        "uri": "/customers/bfbd6ef0-311f-47ec-bbd7-0fcb7846661b/profiles/company",
                        "method": "GET",
                        "headers": []
                    }
                },
                "attributes": {
                    "objectType": "CustomerCompanyProfile"
                }
            },
            "relationshipToPartner": "reseller",
            "links": {
                "self": {
                    "uri": "/customers/bfbd6ef0-311f-47ec-bbd7-0fcb7846661b",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers?size=0&filter=%7B%22Field%22%3A%22Domain%22%2C%22Value%22%3A%22cont%22%2C%22Operator%22%3A%22starts_with%22%7D",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
