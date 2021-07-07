---
title: Hämta en lista över erbjudanden för utvärderingskonvertering
description: Så här hämtar du en lista över erbjudanden för utvärderingskonvertering.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 981910560faf7b7957b28e643c09a003826b9cff
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873929"
---
# <a name="get-a-list-of-trial-conversion-offers"></a><span data-ttu-id="1c6d1-103">Hämta en lista över erbjudanden för utvärderingskonvertering</span><span class="sxs-lookup"><span data-stu-id="1c6d1-103">Get a list of trial conversion offers</span></span>

<span data-ttu-id="1c6d1-104">Så här hämtar du en lista över erbjudanden för utvärderingskonvertering.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-104">How to retrieve a list of trial conversion offers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1c6d1-105">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="1c6d1-105">Prerequisites</span></span>

- <span data-ttu-id="1c6d1-106">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="1c6d1-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1c6d1-107">Det här scenariot har endast stöd för autentisering med app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="1c6d1-108">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1c6d1-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="1c6d1-109">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="1c6d1-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="1c6d1-110">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="1c6d1-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="1c6d1-111">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="1c6d1-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="1c6d1-112">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="1c6d1-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="1c6d1-113">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1c6d1-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="1c6d1-114">Ett prenumerations-ID för en aktiv utvärderingsprenumeration.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-114">A subscription ID for an active trial subscription.</span></span>

## <a name="c"></a><span data-ttu-id="1c6d1-115">C\#</span><span class="sxs-lookup"><span data-stu-id="1c6d1-115">C\#</span></span>

<span data-ttu-id="1c6d1-116">Om du vill hämta en lista över tillgängliga utvärderingskonverteringar börjar du med att använda metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-116">To get a list of trial conversions available, start by using the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="1c6d1-117">Hämta sedan ett gränssnitt för prenumerationsåtgärder genom att anropa metoden [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) med prenumerations-ID:t för utvärderingsversionen.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-117">Then, get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the trial subscription ID.</span></span> <span data-ttu-id="1c6d1-118">Använd sedan egenskapen [**Konverteringar**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) för att hämta ett gränssnitt för de tillgängliga åtgärderna vid konverteringar och anropa sedan metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) för att hämta en samling tillgängliga [**konverteringserbjudanden.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion)</span><span class="sxs-lookup"><span data-stu-id="1c6d1-118">Next, use the [**Conversions**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) property to obtain an interface to the available operations on conversions, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) method to retrieve a collection of available [**Conversion**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) offers.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

// Get the available conversions.
var conversions =
    partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId).Conversions.Get();
```

## <a name="rest-request"></a><span data-ttu-id="1c6d1-119">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="1c6d1-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1c6d1-120">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="1c6d1-120">Request syntax</span></span>

| <span data-ttu-id="1c6d1-121">Metod</span><span class="sxs-lookup"><span data-stu-id="1c6d1-121">Method</span></span>  | <span data-ttu-id="1c6d1-122">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="1c6d1-122">Request URI</span></span>                                                                                                                 |
|---------|-----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1c6d1-123">**Få**</span><span class="sxs-lookup"><span data-stu-id="1c6d1-123">**GET**</span></span> | <span data-ttu-id="1c6d1-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="1c6d1-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="1c6d1-125">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="1c6d1-125">URI parameter</span></span>

<span data-ttu-id="1c6d1-126">Använd följande sökvägsparametrar för att identifiera kunden och utvärderingsprenumerationen.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-126">Use the following path parameters to identify the customer and trial subscription.</span></span>

| <span data-ttu-id="1c6d1-127">Namn</span><span class="sxs-lookup"><span data-stu-id="1c6d1-127">Name</span></span>            | <span data-ttu-id="1c6d1-128">Typ</span><span class="sxs-lookup"><span data-stu-id="1c6d1-128">Type</span></span>   | <span data-ttu-id="1c6d1-129">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="1c6d1-129">Required</span></span> | <span data-ttu-id="1c6d1-130">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="1c6d1-130">Description</span></span>                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="1c6d1-131">kund-ID</span><span class="sxs-lookup"><span data-stu-id="1c6d1-131">customer-id</span></span>     | <span data-ttu-id="1c6d1-132">sträng</span><span class="sxs-lookup"><span data-stu-id="1c6d1-132">string</span></span> | <span data-ttu-id="1c6d1-133">Ja</span><span class="sxs-lookup"><span data-stu-id="1c6d1-133">Yes</span></span>      | <span data-ttu-id="1c6d1-134">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-134">A GUID formatted string that identifies the customer.</span></span>           |
| <span data-ttu-id="1c6d1-135">prenumerations-id</span><span class="sxs-lookup"><span data-stu-id="1c6d1-135">subscription-id</span></span> | <span data-ttu-id="1c6d1-136">sträng</span><span class="sxs-lookup"><span data-stu-id="1c6d1-136">string</span></span> | <span data-ttu-id="1c6d1-137">Ja</span><span class="sxs-lookup"><span data-stu-id="1c6d1-137">Yes</span></span>      | <span data-ttu-id="1c6d1-138">En GUID-formaterad sträng som identifierar utvärderingsprenumerationen.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-138">A GUID formatted string that identifies the trial subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="1c6d1-139">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="1c6d1-139">Request headers</span></span>

<span data-ttu-id="1c6d1-140">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="1c6d1-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1c6d1-141">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="1c6d1-141">Request body</span></span>

<span data-ttu-id="1c6d1-142">Inga.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="1c6d1-143">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="1c6d1-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/488745B5-2086-4912-802C-6ABB9F7C3638/conversions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e17f5bc6-24bf-4cbe-b632-d7fc6cec3058
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="1c6d1-144">REST-svar</span><span class="sxs-lookup"><span data-stu-id="1c6d1-144">REST response</span></span>

<span data-ttu-id="1c6d1-145">Om det lyckas innehåller svarstexten en samling [konverteringsresurser.](conversions-resources.md#conversionresult)</span><span class="sxs-lookup"><span data-stu-id="1c6d1-145">If successful, the response body contains a collection of [Conversion](conversions-resources.md#conversionresult) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1c6d1-146">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="1c6d1-146">Response success and error codes</span></span>

<span data-ttu-id="1c6d1-147">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1c6d1-148">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="1c6d1-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1c6d1-149">En fullständig lista finns i [Felkoder i Partnercenter.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="1c6d1-149">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1c6d1-150">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="1c6d1-150">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 305
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
MS-RequestId: e17f5bc6-24bf-4cbe-b632-d7fc6cec3058
MS-CV: feJByqU1X0ObaTQr.0
MS-ServerId: 030011719
Date: Thu, 15 Jun 2017 23:10:01 GMT

 {
    "totalCount": 1,
    "items": [{
            "offerId": "C0BD2E08-11AC-4836-BDC7-3712E744922F",
            "targetOfferId": "031C9E47-4802-4248-838E-778FB1D2CC05",
            "orderId": "D51A052E-043C-4A2A-AA37-2BB938CEF6C1",
            "quantity": 25,
            "billingCycle": "monthly",
            "attributes": {
                "objectType": "Conversion"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
