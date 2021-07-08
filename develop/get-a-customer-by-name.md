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
# <a name="get-a-list-of-customers-filtered-by-a-search-field"></a>Hämta en lista över kunder filtrerade efter ett sökfält

**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Hämtar en samling [kundresurser](customer-resources.md#customer) som matchar ett filter. Du kan också ange en sidstorlek. Du kan filtrera efter företagsnamn, domän, indirekt återförsäljare eller indirekt molnlösningsleverantör (CSP).

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.

- Ett användarkonstruerat filter.

## <a name="c"></a>C\#

Om du vill hämta en samling kunder som matchar ett filter skapar du först ett [**SimpleFieldFilter-objekt**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) för att skapa filtret. Du måste skicka en sträng som innehåller [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield)och ange typen av filteråtgärd som [**FieldFilterOperation.StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation). Det är den enda fältfilteråtgärden som stöds av kundernas slutpunkt. Du måste också ange strängen att filtrera efter.

Skapa sedan en instans av [**ett iQuery-objekt**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) som ska överföras till frågan genom att anropa [**metoden BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) och skicka det till filtret. BuildSimplyQuery är bara en av de frågetyper som stöds av [**queryFactory-klassen.**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory)

För att slutligen köra filtret och hämta resultatet använder du först [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) för att hämta ett gränssnitt för partnerns kundåtgärder. Anropa sedan [**metoden Query**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) eller [**QueryAsync.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync)

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

**Exempel:** [Konsoltestapp](console-test-app.md). **Project:** Partnercenter-SDK **Exempelklass:** FilterCustomers.cs

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod  | URI för förfrågan                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| **Få** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size}&filter={filter} HTTP/1.1 |

### <a name="uri-parameters"></a>URI-parametrar

Använd följande frågeparametrar.

| Namn   | Typ   | Obligatorisk | Beskrivning                                                                    |
|--------|--------|----------|--------------------------------------------------------------------------------|
| ikoner   | int    | Inga       | Antalet resultat som ska visas samtidigt. Den här parametern är valfri. |
| filter | filter | Ja      | Filtret som ska tillämpas på kunder. Det här måste vara en kodad sträng.              |

### <a name="filter-syntax"></a>Filtersyntax

Du måste skriva filterparametern som en serie kommaavgränsade nyckel/värde-par. Varje nyckel och värde måste anges individuellt och avgränsas med ett kolon. Hela filtret måste vara kodat.

Ett okodat exempel ser ut så här:

```http
?filter{"Field":"CompanyName","Value":"cont","Operator":"starts_with"}
```

I följande tabell beskrivs de nyckel/värde-par som krävs:

| Tangent      | Värde                                                                                                                    |
|----------|--------------------------------------------------------------------------------------------------------------------------|
| Fält    | Fältet som ska filtreras. Giltiga värden finns i [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield). |
| Värde    | Värdet som ska filtreras efter. Värdets fall ignoreras.                                                                |
| Operator | Operatorn som ska tillämpas. Det enda värde som stöds för det här kundscenariot är "börjar \_ med".                            |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

Inga.

### <a name="request-example"></a>Exempel på begäran

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

## <a name="rest-response"></a>REST-svar

Om det lyckas returnerar den här metoden en samling matchande [kundresurser](customer-resources.md#customer) i svarstexten.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)

### <a name="response-example"></a>Exempel på svar

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
