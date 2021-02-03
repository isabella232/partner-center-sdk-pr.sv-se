---
title: Hämta kunder till en indirekt återförsäljare
description: Så här hämtar du en lista över kunder i en indirekt åter försäljare.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: e4219f544a74bb3f34ec3aefe08cf18eed77fd42
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769687"
---
# <a name="get-customers-of-an-indirect-reseller"></a><span data-ttu-id="17f3d-103">Hämta kunder till en indirekt återförsäljare</span><span class="sxs-lookup"><span data-stu-id="17f3d-103">Get customers of an indirect reseller</span></span>

<span data-ttu-id="17f3d-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="17f3d-104">**Applies To**</span></span>

- <span data-ttu-id="17f3d-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="17f3d-105">Partner Center</span></span>

<span data-ttu-id="17f3d-106">Så här hämtar du en lista över kunder i en indirekt åter försäljare.</span><span class="sxs-lookup"><span data-stu-id="17f3d-106">How to get a list of the customers of an indirect reseller.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="17f3d-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="17f3d-107">Prerequisites</span></span>

- <span data-ttu-id="17f3d-108">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="17f3d-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="17f3d-109">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="17f3d-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="17f3d-110">Klient-ID för den indirekta åter försäljaren.</span><span class="sxs-lookup"><span data-stu-id="17f3d-110">The tenant identifier of the indirect reseller.</span></span>

## <a name="c"></a><span data-ttu-id="17f3d-111">C\#</span><span class="sxs-lookup"><span data-stu-id="17f3d-111">C\#</span></span>

<span data-ttu-id="17f3d-112">För att få en samling kunder som har en relation med den angivna indirekta åter försäljaren måste du först instansiera ett [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) -objekt för att skapa filtret.</span><span class="sxs-lookup"><span data-stu-id="17f3d-112">To get a collection of customers that have a relationship with the specified indirect reseller, first instantiate a [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) object to create the filter.</span></span> <span data-ttu-id="17f3d-113">Du måste skicka [**CustomerSearchField. IndirectReseller**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield) -uppräknings medlemmen konverterad till en sträng och ange [**FieldFilterOperation. StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation) som typ av filter åtgärd.</span><span class="sxs-lookup"><span data-stu-id="17f3d-113">You'll need to pass the [**CustomerSearchField.IndirectReseller**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield) enumeration member converted to a string, and indicate [**FieldFilterOperation.StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation) as the type of filter operation.</span></span> <span data-ttu-id="17f3d-114">Du måste också ange klient-ID: n för den indirekta åter försäljaren för att filtrera efter.</span><span class="sxs-lookup"><span data-stu-id="17f3d-114">You'll also need to provide the tenant identifier of the indirect reseller to filter by.</span></span>

<span data-ttu-id="17f3d-115">Sedan instansierar du ett [**iQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) -objekt för att skicka till frågan genom att anropa metoden [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) och skicka filtret.</span><span class="sxs-lookup"><span data-stu-id="17f3d-115">Next, instantiate an [**iQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) object to pass to the query by calling the [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) method and passing it the filter.</span></span> <span data-ttu-id="17f3d-116">BuildSimplyQuery är bara en av de frågetyper som stöds av [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) -klassen.</span><span class="sxs-lookup"><span data-stu-id="17f3d-116">BuildSimplyQuery is just one of the query types supported by the [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) class.</span></span>

<span data-ttu-id="17f3d-117">Om du vill köra filtret och få resultatet måste du först använda [**IAggregatePartner. kunder**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) för att få ett gränssnitt till partnerns kund åtgärder.</span><span class="sxs-lookup"><span data-stu-id="17f3d-117">To execute the filter and get the result, first use [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) to get an interface to the partner's customer operations.</span></span> <span data-ttu-id="17f3d-118">Anropa sedan [**fråge**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) -eller [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) -metoden.</span><span class="sxs-lookup"><span data-stu-id="17f3d-118">Then call the [**Query**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) or [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) method.</span></span>

<span data-ttu-id="17f3d-119">Om du vill skapa en uppräknare för att passera växlade resultat hämtar du uppräkna ren för kund samlings uppräknare från [**IAggregatePartner. enumerations. Customers**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumeratorcontainer.customers) -egenskapen och anropar sedan [**create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create), som visas i koden nedan, och skickar variabeln som innehåller kund samlingen.</span><span class="sxs-lookup"><span data-stu-id="17f3d-119">To create an enumerator for traversing paged results, get the customer collection enumerator factory interface from the [**IAggregatePartner.Enumerators.Customers**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumeratorcontainer.customers) property, and then call [**Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create), as shown in the code below, passing the variable that holds the customer collection.</span></span>

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

<span data-ttu-id="17f3d-120">**Exempel**: [konsol test app](console-test-app.md)-**projekt**: Partner Center SDK-exempel **klass**: GetCustomersOfIndirectReseller.CS</span><span class="sxs-lookup"><span data-stu-id="17f3d-120">**Sample**: [Console test app](console-test-app.md)**Project**: Partner Center SDK Samples **Class**: GetCustomersOfIndirectReseller.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="17f3d-121">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="17f3d-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="17f3d-122">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="17f3d-122">Request syntax</span></span>

| <span data-ttu-id="17f3d-123">Metod</span><span class="sxs-lookup"><span data-stu-id="17f3d-123">Method</span></span>  | <span data-ttu-id="17f3d-124">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="17f3d-124">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="17f3d-125">**TA**</span><span class="sxs-lookup"><span data-stu-id="17f3d-125">**GET**</span></span> | <span data-ttu-id="17f3d-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers? size = {size}? filter = {filter} http/1.1</span><span class="sxs-lookup"><span data-stu-id="17f3d-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size}?filter={filter} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="17f3d-127">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="17f3d-127">URI parameter</span></span>

<span data-ttu-id="17f3d-128">Använd följande frågeparametrar för att skapa begäran.</span><span class="sxs-lookup"><span data-stu-id="17f3d-128">Use the following query parameters to create the request.</span></span>

| <span data-ttu-id="17f3d-129">Namn</span><span class="sxs-lookup"><span data-stu-id="17f3d-129">Name</span></span>   | <span data-ttu-id="17f3d-130">Typ</span><span class="sxs-lookup"><span data-stu-id="17f3d-130">Type</span></span>   | <span data-ttu-id="17f3d-131">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="17f3d-131">Required</span></span> | <span data-ttu-id="17f3d-132">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="17f3d-132">Description</span></span>                                                                                                                                                                                                                                                                                   |
|--------|--------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="17f3d-133">ikoner</span><span class="sxs-lookup"><span data-stu-id="17f3d-133">size</span></span>   | <span data-ttu-id="17f3d-134">int</span><span class="sxs-lookup"><span data-stu-id="17f3d-134">int</span></span>    | <span data-ttu-id="17f3d-135">No</span><span class="sxs-lookup"><span data-stu-id="17f3d-135">No</span></span>       | <span data-ttu-id="17f3d-136">Antalet resultat som ska visas samtidigt.</span><span class="sxs-lookup"><span data-stu-id="17f3d-136">The number of results to be displayed at one time.</span></span> <span data-ttu-id="17f3d-137">Den här parametern är valfri.</span><span class="sxs-lookup"><span data-stu-id="17f3d-137">This parameter is optional.</span></span>                                                                                                                                                                                                                |
| <span data-ttu-id="17f3d-138">filter</span><span class="sxs-lookup"><span data-stu-id="17f3d-138">filter</span></span> | <span data-ttu-id="17f3d-139">filter</span><span class="sxs-lookup"><span data-stu-id="17f3d-139">filter</span></span> | <span data-ttu-id="17f3d-140">Yes</span><span class="sxs-lookup"><span data-stu-id="17f3d-140">Yes</span></span>      | <span data-ttu-id="17f3d-141">Frågan som filtrerar sökningen.</span><span class="sxs-lookup"><span data-stu-id="17f3d-141">The query that filters the search.</span></span> <span data-ttu-id="17f3d-142">Om du vill hämta kunder för en angiven indirekt åter försäljare måste du infoga den indirekta åter försäljarens identifierare och ta med och koda följande sträng: {"Field": "IndirectReseller", "värde": "{indirekt åter försäljarens identifierare}", "Operator": "börjar \_ med"}.</span><span class="sxs-lookup"><span data-stu-id="17f3d-142">To retrieve customers for a specified indirect reseller, you must insert the indirect reseller identifier and include and encode the following string: {"Field":"IndirectReseller","Value":"{indirect reseller identifier}","Operator":"starts\_with"}.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="17f3d-143">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="17f3d-143">Request headers</span></span>

<span data-ttu-id="17f3d-144">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="17f3d-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="17f3d-145">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="17f3d-145">Request body</span></span>

<span data-ttu-id="17f3d-146">Inga.</span><span class="sxs-lookup"><span data-stu-id="17f3d-146">None.</span></span>

### <a name="request-example-encoded"></a><span data-ttu-id="17f3d-147">Exempel på begäran (kodad)</span><span class="sxs-lookup"><span data-stu-id="17f3d-147">Request example (encoded)</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter=%7B%22Field%22%3A%22IndirectReseller%22%2C%22Value%22%3A%22484e548c-f5f3-4528-93a9-c16c6373cb59%22%2C%22Operator%22%3A%22starts_with%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="request-example-decoded"></a><span data-ttu-id="17f3d-148">Exempel på begäran (avkodad)</span><span class="sxs-lookup"><span data-stu-id="17f3d-148">Request example (decoded)</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter={"Field":"IndirectReseller","Value":"484e548c-f5f3-4528-93a9-c16c6373cb59","Operator":"starts_with"} HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="17f3d-149">REST-svar</span><span class="sxs-lookup"><span data-stu-id="17f3d-149">REST response</span></span>

<span data-ttu-id="17f3d-150">Om det lyckas innehåller svars texten information om åter försäljarens kunder.</span><span class="sxs-lookup"><span data-stu-id="17f3d-150">If successful, the response body contains information about the reseller's customers.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="17f3d-151">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="17f3d-151">Response success and error codes</span></span>

<span data-ttu-id="17f3d-152">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="17f3d-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="17f3d-153">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="17f3d-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="17f3d-154">En fullständig lista finns i [fel koder för partner Center](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="17f3d-154">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="17f3d-155">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="17f3d-155">Response example</span></span>

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
