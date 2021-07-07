---
title: Hämta kunder till en indirekt återförsäljare
description: Så här hämtar du en lista över kunder till en indirekt återförsäljare.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: e05248b16b803529258de806c25b117f3104ad2a
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446334"
---
# <a name="get-customers-of-an-indirect-reseller"></a><span data-ttu-id="09489-103">Hämta kunder till en indirekt återförsäljare</span><span class="sxs-lookup"><span data-stu-id="09489-103">Get customers of an indirect reseller</span></span>

<span data-ttu-id="09489-104">Så här hämtar du en lista över kunder till en indirekt återförsäljare.</span><span class="sxs-lookup"><span data-stu-id="09489-104">How to get a list of the customers of an indirect reseller.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="09489-105">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="09489-105">Prerequisites</span></span>

- <span data-ttu-id="09489-106">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="09489-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="09489-107">Det här scenariot stöder endast autentisering med app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="09489-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="09489-108">Klientorganisations-ID för den indirekta återförsäljaren.</span><span class="sxs-lookup"><span data-stu-id="09489-108">The tenant identifier of the indirect reseller.</span></span>

## <a name="c"></a><span data-ttu-id="09489-109">C\#</span><span class="sxs-lookup"><span data-stu-id="09489-109">C\#</span></span>

<span data-ttu-id="09489-110">Om du vill hämta en samling kunder som har en relation med den angivna indirekta återförsäljaren skapar du först ett [**SimpleFieldFilter-objekt**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) för att skapa filtret.</span><span class="sxs-lookup"><span data-stu-id="09489-110">To get a collection of customers that have a relationship with the specified indirect reseller, first instantiate a [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) object to create the filter.</span></span> <span data-ttu-id="09489-111">Du måste skicka uppräkningsmedlemmen [**CustomerSearchField.IndirectReseller**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield) som konverterats till en sträng och ange [**FieldFilterOperation.StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation) som typ av filteråtgärd.</span><span class="sxs-lookup"><span data-stu-id="09489-111">You'll need to pass the [**CustomerSearchField.IndirectReseller**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield) enumeration member converted to a string, and indicate [**FieldFilterOperation.StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation) as the type of filter operation.</span></span> <span data-ttu-id="09489-112">Du måste också ange klient-ID för den indirekta återförsäljaren att filtrera efter.</span><span class="sxs-lookup"><span data-stu-id="09489-112">You'll also need to provide the tenant identifier of the indirect reseller to filter by.</span></span>

<span data-ttu-id="09489-113">Skapa sedan en instans av [**ett iQuery-objekt**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) som ska överföras till frågan genom att anropa [**metoden BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) och skicka det till filtret.</span><span class="sxs-lookup"><span data-stu-id="09489-113">Next, instantiate an [**iQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) object to pass to the query by calling the [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) method and passing it the filter.</span></span> <span data-ttu-id="09489-114">BuildSimplyQuery är bara en av de frågetyper som stöds av [**queryFactory-klassen.**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory)</span><span class="sxs-lookup"><span data-stu-id="09489-114">BuildSimplyQuery is just one of the query types supported by the [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) class.</span></span>

<span data-ttu-id="09489-115">Om du vill köra filtret och hämta resultatet använder du först [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) för att hämta ett gränssnitt för partnerns kundåtgärder.</span><span class="sxs-lookup"><span data-stu-id="09489-115">To execute the filter and get the result, first use [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) to get an interface to the partner's customer operations.</span></span> <span data-ttu-id="09489-116">Anropa sedan [**metoden Query**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) eller [**QueryAsync.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync)</span><span class="sxs-lookup"><span data-stu-id="09489-116">Then call the [**Query**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) or [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) method.</span></span>

<span data-ttu-id="09489-117">Om du vill skapa en uppräkning för att bläddra i sidindelade resultat hämtar du kundsamlingens uppräkningsfabriksgränssnitt från egenskapen [**IAggregatePartner.Enumerators.Customers**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumeratorcontainer.customers) och anropar [**sedan Skapa**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create)enligt koden nedan och anger variabeln som innehåller kundsamlingen.</span><span class="sxs-lookup"><span data-stu-id="09489-117">To create an enumerator for traversing paged results, get the customer collection enumerator factory interface from the [**IAggregatePartner.Enumerators.Customers**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumeratorcontainer.customers) property, and then call [**Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create), as shown in the code below, passing the variable that holds the customer collection.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string indirectResellerId;

// Create a filter.
var filter = new SimpleFieldFilter(
    CustomerSearchField.IndirectReseller.ToString(),
    FieldFilterOperation.StartsWith,
    indirectResellerId);

// Create an iQuery object to pass to the Query method.
var myQuery = QueryFactory.Instance.BuildSimpleQuery(filter);

// Get the collection of matching customers.
var customersPage = partnerOperations.Customers.Query(myQuery);

// Create a customer enumerator for traversing the customer pages.
var customersEnumerator = partnerOperations.Enumerators.Customers.Create(customersPage);
int pageNumber = 1;

while (customersEnumerator.HasValue)
{
    // Work with the current page.
     foreach (var c in customersEnumerator.Current.Items)
    {
        // Display customer tenant identifier and company name.
        Console.WriteLine(string.Format("{0} - {1}.",c.Id,c.CompanyProfile.CompanyName));
    }
    // Get the next page of customers.
    customersEnumerator.Next();
}
```

<span data-ttu-id="09489-118">**Exempel:** [Konsoltestapp med](console-test-app.md)**Project:** Partnercenter-SDK **Exempelklass:** GetCustomersOfIndirectReseller.cs</span><span class="sxs-lookup"><span data-stu-id="09489-118">**Sample**: [Console test app](console-test-app.md)**Project**: Partner Center SDK Samples **Class**: GetCustomersOfIndirectReseller.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="09489-119">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="09489-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="09489-120">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="09489-120">Request syntax</span></span>

| <span data-ttu-id="09489-121">Metod</span><span class="sxs-lookup"><span data-stu-id="09489-121">Method</span></span>  | <span data-ttu-id="09489-122">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="09489-122">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="09489-123">**Få**</span><span class="sxs-lookup"><span data-stu-id="09489-123">**GET**</span></span> | <span data-ttu-id="09489-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size}?filter={filter} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="09489-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size}?filter={filter} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="09489-125">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="09489-125">URI parameter</span></span>

<span data-ttu-id="09489-126">Använd följande frågeparametrar för att skapa begäran.</span><span class="sxs-lookup"><span data-stu-id="09489-126">Use the following query parameters to create the request.</span></span>

| <span data-ttu-id="09489-127">Namn</span><span class="sxs-lookup"><span data-stu-id="09489-127">Name</span></span>   | <span data-ttu-id="09489-128">Typ</span><span class="sxs-lookup"><span data-stu-id="09489-128">Type</span></span>   | <span data-ttu-id="09489-129">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="09489-129">Required</span></span> | <span data-ttu-id="09489-130">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="09489-130">Description</span></span>                                                                                                                                                                                                                                                                                   |
|--------|--------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="09489-131">ikoner</span><span class="sxs-lookup"><span data-stu-id="09489-131">size</span></span>   | <span data-ttu-id="09489-132">int</span><span class="sxs-lookup"><span data-stu-id="09489-132">int</span></span>    | <span data-ttu-id="09489-133">Inga</span><span class="sxs-lookup"><span data-stu-id="09489-133">No</span></span>       | <span data-ttu-id="09489-134">Antalet resultat som ska visas samtidigt.</span><span class="sxs-lookup"><span data-stu-id="09489-134">The number of results to be displayed at one time.</span></span> <span data-ttu-id="09489-135">Den här parametern är valfri.</span><span class="sxs-lookup"><span data-stu-id="09489-135">This parameter is optional.</span></span>                                                                                                                                                                                                                |
| <span data-ttu-id="09489-136">filter</span><span class="sxs-lookup"><span data-stu-id="09489-136">filter</span></span> | <span data-ttu-id="09489-137">filter</span><span class="sxs-lookup"><span data-stu-id="09489-137">filter</span></span> | <span data-ttu-id="09489-138">Ja</span><span class="sxs-lookup"><span data-stu-id="09489-138">Yes</span></span>      | <span data-ttu-id="09489-139">Frågan som filtrerar sökningen.</span><span class="sxs-lookup"><span data-stu-id="09489-139">The query that filters the search.</span></span> <span data-ttu-id="09489-140">Om du vill hämta kunder för en angiven indirekt återförsäljare måste du infoga den indirekta återförsäljaridentifieraren och inkludera och koda följande sträng: {"Field":"IndirectReseller","Value":"{indirect reseller identifier}","Operator":"starts \_ with"}.</span><span class="sxs-lookup"><span data-stu-id="09489-140">To retrieve customers for a specified indirect reseller, you must insert the indirect reseller identifier and include and encode the following string: {"Field":"IndirectReseller","Value":"{indirect reseller identifier}","Operator":"starts\_with"}.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="09489-141">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="09489-141">Request headers</span></span>

<span data-ttu-id="09489-142">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="09489-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="09489-143">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="09489-143">Request body</span></span>

<span data-ttu-id="09489-144">Inga.</span><span class="sxs-lookup"><span data-stu-id="09489-144">None.</span></span>

### <a name="request-example-encoded"></a><span data-ttu-id="09489-145">Exempel på begäran (kodad)</span><span class="sxs-lookup"><span data-stu-id="09489-145">Request example (encoded)</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter=%7B%22Field%22%3A%22IndirectReseller%22%2C%22Value%22%3A%22484e548c-f5f3-4528-93a9-c16c6373cb59%22%2C%22Operator%22%3A%22starts_with%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="request-example-decoded"></a><span data-ttu-id="09489-146">Exempel på begäran (avkodad)</span><span class="sxs-lookup"><span data-stu-id="09489-146">Request example (decoded)</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter={"Field":"IndirectReseller","Value":"484e548c-f5f3-4528-93a9-c16c6373cb59","Operator":"starts_with"} HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="09489-147">REST-svar</span><span class="sxs-lookup"><span data-stu-id="09489-147">REST response</span></span>

<span data-ttu-id="09489-148">Om det lyckas innehåller svarstexten information om återförsäljarens kunder.</span><span class="sxs-lookup"><span data-stu-id="09489-148">If successful, the response body contains information about the reseller's customers.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="09489-149">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="09489-149">Response success and error codes</span></span>

<span data-ttu-id="09489-150">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="09489-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="09489-151">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="09489-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="09489-152">En fullständig lista finns i [Felkoder i Partnercenter.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="09489-152">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="09489-153">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="09489-153">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2273
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: XI2/vIHmIEGVlGL9.0
MS-ServerId: 101112012
Date: Tue, 11 Apr 2017 23:31:28 GMT

{
    "totalCount": 2,
    "items": [{
            "id": "53eb21cb-6b2d-4ee5-9e92-27dfc927e93c",
            "companyProfile": {
                "tenantId": "53eb21cb-6b2d-4ee5-9e92-27dfc927e93c",
                "domain": "FourthCoffee137.onmicrosoft.com",
                "companyName": "FourthCoffee137",
                "links": {
                    "self": {
                        "uri": "/customers/53eb21cb-6b2d-4ee5-9e92-27dfc927e93c/profiles/company",
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
                    "uri": "/customers/53eb21cb-6b2d-4ee5-9e92-27dfc927e93c",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        }, {
            "id": "3dfe847b-cad9-4fc1-86d3-cf16c2790087",
            "companyProfile": {
                "tenantId": "3dfe847b-cad9-4fc1-86d3-cf16c2790087",
                "domain": "WingtipToys1254789149.onmicrosoft.com",
                "companyName": "Wingtip Toys1254789149",
                "links": {
                    "self": {
                        "uri": "/customers/3dfe847b-cad9-4fc1-86d3-cf16c2790087/profiles/company",
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
                    "uri": "/customers/3dfe847b-cad9-4fc1-86d3-cf16c2790087",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        },
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
