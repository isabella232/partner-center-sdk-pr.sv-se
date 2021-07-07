---
title: Hämta en partners Government Community Cloud valideringskoder
description: Hur du hämtar en partners Government Community Cloud valideringskoder.
ms.date: 11/08/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khakiali
ms.author: alikhaki
ms.openlocfilehash: 04bccf587628337004a5825b534048945f791839
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873878"
---
# <a name="get-a-partners-validation-codes"></a><span data-ttu-id="0ab77-103">Hämta en partners valideringskoder</span><span class="sxs-lookup"><span data-stu-id="0ab77-103">Get a partner's validation codes</span></span>

<span data-ttu-id="0ab77-104">Den här artikeln beskriver hur du hämtar en samling av en partners Government Community Cloud valideringskoder.</span><span class="sxs-lookup"><span data-stu-id="0ab77-104">This article describes how to get a collection of a partner's Government Community Cloud validation codes.</span></span> <span data-ttu-id="0ab77-105">En valideringskod krävs för att skapa en kund i government community cloud.</span><span class="sxs-lookup"><span data-stu-id="0ab77-105">A validation code is required to create a customer in the government community cloud.</span></span>

<span data-ttu-id="0ab77-106">Om du är intresserad av att ha din organisation eller din kunds organisation godkänd för Office 365 för myndigheter GCC för CSP kan du gå till Office 365 för myndigheter GCC för [villkor för CSP-partner och kundberättigande.](/partner-center/csp-gcc-validate)</span><span class="sxs-lookup"><span data-stu-id="0ab77-106">If you are interested in having your organization or your customer's organization approved for Office 365 Government GCC for CSP, see [Office 365 Government GCC for CSP Partner and Customer eligibility criteria](/partner-center/csp-gcc-validate).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ab77-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="0ab77-107">Prerequisites</span></span>

- <span data-ttu-id="0ab77-108">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="0ab77-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0ab77-109">Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="0ab77-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="0ab77-110">Verifieringen har bekräftats när du har fyllt i formuläret [här](https://products.office.com/government/eligibility-validation?ReqType=CSPPartner).</span><span class="sxs-lookup"><span data-stu-id="0ab77-110">Confirmed validation after filling out form [here](https://products.office.com/government/eligibility-validation?ReqType=CSPPartner).</span></span>

- <span data-ttu-id="0ab77-111">En kund utan kvalificering.</span><span class="sxs-lookup"><span data-stu-id="0ab77-111">A customer without a qualification.</span></span>

## <a name="c"></a><span data-ttu-id="0ab77-112">C\#</span><span class="sxs-lookup"><span data-stu-id="0ab77-112">C\#</span></span>

<span data-ttu-id="0ab77-113">Om du vill hämta en lista över alla valideringskoder för en partner anropar du **GetValidationCodes**.</span><span class="sxs-lookup"><span data-stu-id="0ab77-113">To get a list of all of a partner's validation codes, call **GetValidationCodes**.</span></span>

``` csharp
// create the partner operations
IAggregatePartner partnerOperations = PartnerService.Instance.CreatePartnerOperations(credentials);

var gccValidations = partnerOperations.Validations.GetValidationCodes();
```

## <a name="rest-request"></a><span data-ttu-id="0ab77-114">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="0ab77-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0ab77-115">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="0ab77-115">Request syntax</span></span>

| <span data-ttu-id="0ab77-116">Metod</span><span class="sxs-lookup"><span data-stu-id="0ab77-116">Method</span></span>  | <span data-ttu-id="0ab77-117">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="0ab77-117">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0ab77-118">**Få**</span><span class="sxs-lookup"><span data-stu-id="0ab77-118">**GET**</span></span> | <span data-ttu-id="0ab77-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/all/validations HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="0ab77-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/all/validations HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="0ab77-120">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="0ab77-120">Request headers</span></span>

<span data-ttu-id="0ab77-121">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="0ab77-121">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0ab77-122">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="0ab77-122">Request body</span></span>

<span data-ttu-id="0ab77-123">Inga.</span><span class="sxs-lookup"><span data-stu-id="0ab77-123">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="0ab77-124">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="0ab77-124">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/all/validations HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 283b9b70-963a-4159-9920-f2bdf7ab7fce
MS-RequestId: 7266f5f6-30ca-4672-9eb6-6c9d6dd0e9d3
```

## <a name="rest-response"></a><span data-ttu-id="0ab77-125">REST-svar</span><span class="sxs-lookup"><span data-stu-id="0ab77-125">REST response</span></span>

<span data-ttu-id="0ab77-126">Om det lyckas returnerar den här metoden en lista [**över ValidationCode-resurser**](utility-resources.md#validationcode) i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="0ab77-126">If successful, this method returns a list of [**ValidationCode**](utility-resources.md#validationcode) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0ab77-127">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="0ab77-127">Response success and error codes</span></span>

<span data-ttu-id="0ab77-128">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="0ab77-128">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0ab77-129">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="0ab77-129">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="0ab77-130">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="0ab77-130">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="0ab77-131">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="0ab77-131">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 434
Content-Type: application/json
MS-CorrelationId: 283b9b70-963a-4159-9920-f2bdf7ab7fce
MS-RequestId: 7266f5f6-30ca-4672-9eb6-6c9d6dd0e9d3

[
  {
    "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d",
    "organizationName": "Contoso, Inc.",
    "validationId": "12345",
    "maxCreates": 5,
    "remainingCreates": 4,
    "eTag": "W/\"datetime'2018-10-10T18%3A49%3A58.727348Z'\""
  },
  {
    "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d",
    "organizationName": "Contoso, Inc. Finance Department",
    "validationId": "987654",
    "maxCreates": 5,
    "remainingCreates": 5,
    "eTag": "W/\"datetime'2018-10-19T17%3A51%3A45.6584512Z'\""
  }
]
```
