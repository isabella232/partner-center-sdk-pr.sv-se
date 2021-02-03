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
# <a name="get-a-list-of-customers-filtered-by-a-search-field"></a>Hämta en lista över kunder filtrerade efter ett sökfält

**Gäller för**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Hämtar en samling [kund](customer-resources.md#customer) resurser som matchar ett filter. Du kan också ange en sid storlek. Du kan filtrera efter företags namn, domän, indirekt åter försäljare eller CSP (indirekt Cloud Solution Provider).

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.

- Ett användardefinierat filter.

## <a name="c"></a>C\#

Om du vill hämta en samling kunder som matchar ett filter måste du först instansiera ett [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) -objekt för att skapa filtret. Du måste skicka en sträng som innehåller [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield)och ange typ av filter åtgärd som [**FieldFilterOperation. StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation). Det är den enda fält filter åtgärd som stöds av slut punkten för kunder. Du måste också ange strängen för att filtrera efter.

Sedan instansierar du ett [**iQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) -objekt för att skicka till frågan genom att anropa metoden [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) och skicka filtret. BuildSimplyQuery är bara en av de frågetyper som stöds av [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) -klassen.

Slutligen, om du vill köra filtret och få resultatet, använder du först [**IAggregatePartner. kunder**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) för att få ett gränssnitt till partnerns kund åtgärder. Anropa sedan [**fråge**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) -eller [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) -metoden.

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

**Exempel**: [konsol test app](console-test-app.md). **Projekt**: Partner Center SDK-exempel **klass**: FilterCustomers.CS

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod  | URI för förfrågan                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| **TA** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers? size = {size} &filter = {filter} http/1.1 |

### <a name="uri-parameters"></a>URI-parametrar

Använd följande frågeparametrar.

| Namn   | Typ   | Obligatorisk | Beskrivning                                                                    |
|--------|--------|----------|--------------------------------------------------------------------------------|
| ikoner   | int    | No       | Antalet resultat som ska visas samtidigt. Den här parametern är valfri. |
| filter | filter | Yes      | Filtret som ska användas för kunderna. Detta måste vara en kodad sträng.              |

### <a name="filter-syntax"></a>Filter-syntax

Du måste skapa filter parametern som en serie kommaavgränsade par med nyckel/värde-par. Varje nyckel och värde måste anges individuellt och avgränsas med kolon. Hela filtret måste vara kodat.

Ett avkodat exempel ser ut så här:

```http
?filter{"Field":"CompanyName","Value":"cont","Operator":"starts_with"}
```

I följande tabell beskrivs de nyckel/värde-par som krävs:

| Tangent      | Värde                                                                                                                    |
|----------|--------------------------------------------------------------------------------------------------------------------------|
| Fält    | Det fält som ska filtreras. Du hittar giltiga värden i [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield). |
| Värde    | Värdet att filtrera efter. Skift läget för värdet ignoreras.                                                                |
| Operator | Operatorn som ska användas. Det enda värde som stöds för det här kund scenariot är "börjar \_ med".                            |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

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

Om det lyckas returnerar den här metoden en samling matchande [kund](customer-resources.md#customer) resurser i svars texten.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).

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
