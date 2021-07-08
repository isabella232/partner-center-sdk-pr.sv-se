---
title: Hämta en lista över kunder filtrerade efter ett sökfält
description: Hämtar en samling kundresurser som matchar ett filter. Du kan också ange en sidstorlek. Du kan filtrera efter företagsnamn, domän, indirekt återförsäljare eller indirekt molnlösningsleverantör (CSP).
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 663b8509d8704f9c443796d9fbcf72fb9c5b7fb2
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874966"
---
# <a name="get-a-list-of-customers-filtered-by-a-search-field"></a><span data-ttu-id="b1f91-105">Hämta en lista över kunder filtrerade efter ett sökfält</span><span class="sxs-lookup"><span data-stu-id="b1f91-105">Get a list of customers filtered by a search field</span></span>

<span data-ttu-id="b1f91-106">**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="b1f91-106">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="b1f91-107">Hämtar en samling [kundresurser](customer-resources.md#customer) som matchar ett filter.</span><span class="sxs-lookup"><span data-stu-id="b1f91-107">Gets a collection of [Customer](customer-resources.md#customer) resources that match a filter.</span></span> <span data-ttu-id="b1f91-108">Du kan också ange en sidstorlek.</span><span class="sxs-lookup"><span data-stu-id="b1f91-108">You can optionally set a page size.</span></span> <span data-ttu-id="b1f91-109">Du kan filtrera efter företagsnamn, domän, indirekt återförsäljare eller indirekt molnlösningsleverantör (CSP).</span><span class="sxs-lookup"><span data-stu-id="b1f91-109">You can filter by company name, domain, indirect reseller, or indirect cloud solution provider (CSP).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b1f91-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="b1f91-110">Prerequisites</span></span>

- <span data-ttu-id="b1f91-111">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b1f91-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b1f91-112">Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="b1f91-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="b1f91-113">Ett användarkonstruerat filter.</span><span class="sxs-lookup"><span data-stu-id="b1f91-113">A user-constructed filter.</span></span>

## <a name="c"></a><span data-ttu-id="b1f91-114">C\#</span><span class="sxs-lookup"><span data-stu-id="b1f91-114">C\#</span></span>

<span data-ttu-id="b1f91-115">Om du vill hämta en samling kunder som matchar ett filter skapar du först ett [**SimpleFieldFilter-objekt**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) för att skapa filtret.</span><span class="sxs-lookup"><span data-stu-id="b1f91-115">To get a collection of customers that match a filter, first instantiate a [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) object to create the filter.</span></span> <span data-ttu-id="b1f91-116">Du måste skicka en sträng som innehåller [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield)och ange typen av filteråtgärd som [**FieldFilterOperation.StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation).</span><span class="sxs-lookup"><span data-stu-id="b1f91-116">You'll need to pass a string that contains the [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield), and indicate the type of filter operation as [**FieldFilterOperation.StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation).</span></span> <span data-ttu-id="b1f91-117">Det är den enda fältfilteråtgärden som stöds av kundernas slutpunkt.</span><span class="sxs-lookup"><span data-stu-id="b1f91-117">That's the only field filter operation supported by the customers end point.</span></span> <span data-ttu-id="b1f91-118">Du måste också ange strängen att filtrera efter.</span><span class="sxs-lookup"><span data-stu-id="b1f91-118">You'll also need to provide the string to filter by.</span></span>

<span data-ttu-id="b1f91-119">Skapa sedan en instans av [**ett iQuery-objekt**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) som ska överföras till frågan genom att anropa [**metoden BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) och skicka det till filtret.</span><span class="sxs-lookup"><span data-stu-id="b1f91-119">Next, instantiate an [**iQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) object to pass to the query by calling the [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) method and passing it the filter.</span></span> <span data-ttu-id="b1f91-120">BuildSimplyQuery är bara en av de frågetyper som stöds av [**queryFactory-klassen.**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory)</span><span class="sxs-lookup"><span data-stu-id="b1f91-120">BuildSimplyQuery is just one of the query types supported by the [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) class.</span></span>

<span data-ttu-id="b1f91-121">För att slutligen köra filtret och hämta resultatet använder du först [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) för att hämta ett gränssnitt för partnerns kundåtgärder.</span><span class="sxs-lookup"><span data-stu-id="b1f91-121">Finally, to execute the filter and get the result, first use [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) to get an interface to the partner's customer operations.</span></span> <span data-ttu-id="b1f91-122">Anropa sedan [**metoden Query**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) eller [**QueryAsync.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync)</span><span class="sxs-lookup"><span data-stu-id="b1f91-122">Then call the [**Query**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) or [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) method.</span></span>

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

<span data-ttu-id="b1f91-123">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="b1f91-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="b1f91-124">**Project:** Partnercenter-SDK **Exempelklass:** FilterCustomers.cs</span><span class="sxs-lookup"><span data-stu-id="b1f91-124">**Project**: Partner Center SDK Samples **Class**: FilterCustomers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="b1f91-125">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="b1f91-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b1f91-126">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="b1f91-126">Request syntax</span></span>

| <span data-ttu-id="b1f91-127">Metod</span><span class="sxs-lookup"><span data-stu-id="b1f91-127">Method</span></span>  | <span data-ttu-id="b1f91-128">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="b1f91-128">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="b1f91-129">**Få**</span><span class="sxs-lookup"><span data-stu-id="b1f91-129">**GET**</span></span> | <span data-ttu-id="b1f91-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size}&filter={filter} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="b1f91-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size}&filter={filter} HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="b1f91-131">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="b1f91-131">URI parameters</span></span>

<span data-ttu-id="b1f91-132">Använd följande frågeparametrar.</span><span class="sxs-lookup"><span data-stu-id="b1f91-132">Use the following query parameters.</span></span>

| <span data-ttu-id="b1f91-133">Namn</span><span class="sxs-lookup"><span data-stu-id="b1f91-133">Name</span></span>   | <span data-ttu-id="b1f91-134">Typ</span><span class="sxs-lookup"><span data-stu-id="b1f91-134">Type</span></span>   | <span data-ttu-id="b1f91-135">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="b1f91-135">Required</span></span> | <span data-ttu-id="b1f91-136">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="b1f91-136">Description</span></span>                                                                    |
|--------|--------|----------|--------------------------------------------------------------------------------|
| <span data-ttu-id="b1f91-137">ikoner</span><span class="sxs-lookup"><span data-stu-id="b1f91-137">size</span></span>   | <span data-ttu-id="b1f91-138">int</span><span class="sxs-lookup"><span data-stu-id="b1f91-138">int</span></span>    | <span data-ttu-id="b1f91-139">Inga</span><span class="sxs-lookup"><span data-stu-id="b1f91-139">No</span></span>       | <span data-ttu-id="b1f91-140">Antalet resultat som ska visas samtidigt.</span><span class="sxs-lookup"><span data-stu-id="b1f91-140">The number of results to be displayed at one time.</span></span> <span data-ttu-id="b1f91-141">Den här parametern är valfri.</span><span class="sxs-lookup"><span data-stu-id="b1f91-141">This parameter is optional.</span></span> |
| <span data-ttu-id="b1f91-142">filter</span><span class="sxs-lookup"><span data-stu-id="b1f91-142">filter</span></span> | <span data-ttu-id="b1f91-143">filter</span><span class="sxs-lookup"><span data-stu-id="b1f91-143">filter</span></span> | <span data-ttu-id="b1f91-144">Ja</span><span class="sxs-lookup"><span data-stu-id="b1f91-144">Yes</span></span>      | <span data-ttu-id="b1f91-145">Filtret som ska tillämpas på kunder.</span><span class="sxs-lookup"><span data-stu-id="b1f91-145">The filter to apply to customers.</span></span> <span data-ttu-id="b1f91-146">Det här måste vara en kodad sträng.</span><span class="sxs-lookup"><span data-stu-id="b1f91-146">This must be an encoded string.</span></span>              |

### <a name="filter-syntax"></a><span data-ttu-id="b1f91-147">Filtersyntax</span><span class="sxs-lookup"><span data-stu-id="b1f91-147">Filter Syntax</span></span>

<span data-ttu-id="b1f91-148">Du måste skriva filterparametern som en serie kommaavgränsade nyckel/värde-par.</span><span class="sxs-lookup"><span data-stu-id="b1f91-148">You must compose the filter parameter as a series of comma separated, key-value pairs.</span></span> <span data-ttu-id="b1f91-149">Varje nyckel och värde måste anges individuellt och avgränsas med ett kolon.</span><span class="sxs-lookup"><span data-stu-id="b1f91-149">Each key and value must be individually quoted and separated by a colon.</span></span> <span data-ttu-id="b1f91-150">Hela filtret måste vara kodat.</span><span class="sxs-lookup"><span data-stu-id="b1f91-150">The entire filter must be encoded.</span></span>

<span data-ttu-id="b1f91-151">Ett okodat exempel ser ut så här:</span><span class="sxs-lookup"><span data-stu-id="b1f91-151">An unencoded example looks like this:</span></span>

```http
?filter{"Field":"CompanyName","Value":"cont","Operator":"starts_with"}
```

<span data-ttu-id="b1f91-152">I följande tabell beskrivs de nyckel/värde-par som krävs:</span><span class="sxs-lookup"><span data-stu-id="b1f91-152">The following table describes the required key-value pairs:</span></span>

| <span data-ttu-id="b1f91-153">Tangent</span><span class="sxs-lookup"><span data-stu-id="b1f91-153">Key</span></span>      | <span data-ttu-id="b1f91-154">Värde</span><span class="sxs-lookup"><span data-stu-id="b1f91-154">Value</span></span>                                                                                                                    |
|----------|--------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b1f91-155">Fält</span><span class="sxs-lookup"><span data-stu-id="b1f91-155">Field</span></span>    | <span data-ttu-id="b1f91-156">Fältet som ska filtreras.</span><span class="sxs-lookup"><span data-stu-id="b1f91-156">The field to filter.</span></span> <span data-ttu-id="b1f91-157">Giltiga värden finns i [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield).</span><span class="sxs-lookup"><span data-stu-id="b1f91-157">The valid values can be found in [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield).</span></span> |
| <span data-ttu-id="b1f91-158">Värde</span><span class="sxs-lookup"><span data-stu-id="b1f91-158">Value</span></span>    | <span data-ttu-id="b1f91-159">Värdet som ska filtreras efter.</span><span class="sxs-lookup"><span data-stu-id="b1f91-159">The value to filter by.</span></span> <span data-ttu-id="b1f91-160">Värdets fall ignoreras.</span><span class="sxs-lookup"><span data-stu-id="b1f91-160">The case of the value is ignored.</span></span>                                                                |
| <span data-ttu-id="b1f91-161">Operator</span><span class="sxs-lookup"><span data-stu-id="b1f91-161">Operator</span></span> | <span data-ttu-id="b1f91-162">Operatorn som ska tillämpas.</span><span class="sxs-lookup"><span data-stu-id="b1f91-162">The operator to apply.</span></span> <span data-ttu-id="b1f91-163">Det enda värde som stöds för det här kundscenariot är "börjar \_ med".</span><span class="sxs-lookup"><span data-stu-id="b1f91-163">The only supported value for this customer scenario is "starts\_with".</span></span>                            |

### <a name="request-headers"></a><span data-ttu-id="b1f91-164">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="b1f91-164">Request headers</span></span>

<span data-ttu-id="b1f91-165">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="b1f91-165">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b1f91-166">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="b1f91-166">Request body</span></span>

<span data-ttu-id="b1f91-167">Inga.</span><span class="sxs-lookup"><span data-stu-id="b1f91-167">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="b1f91-168">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="b1f91-168">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="b1f91-169">REST-svar</span><span class="sxs-lookup"><span data-stu-id="b1f91-169">REST response</span></span>

<span data-ttu-id="b1f91-170">Om det lyckas returnerar den här metoden en samling matchande [kundresurser](customer-resources.md#customer) i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="b1f91-170">If successful, this method returns a collection of matching [Customer](customer-resources.md#customer) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b1f91-171">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="b1f91-171">Response success and error codes</span></span>

<span data-ttu-id="b1f91-172">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="b1f91-172">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b1f91-173">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="b1f91-173">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b1f91-174">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="b1f91-174">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b1f91-175">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="b1f91-175">Response example</span></span>

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
