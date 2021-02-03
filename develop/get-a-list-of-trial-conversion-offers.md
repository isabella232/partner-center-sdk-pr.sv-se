---
title: Hämta en lista över erbjudanden för utvärderingskonvertering
description: Hämta en lista över erbjudanden om utvärderings konvertering.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e1eadecde9efa0b59fc7790bd474889bb32821dc
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769540"
---
# <a name="get-a-list-of-trial-conversion-offers"></a><span data-ttu-id="48dcf-103">Hämta en lista över erbjudanden för utvärderingskonvertering</span><span class="sxs-lookup"><span data-stu-id="48dcf-103">Get a list of trial conversion offers</span></span>

<span data-ttu-id="48dcf-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="48dcf-104">**Applies To**</span></span>

- <span data-ttu-id="48dcf-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="48dcf-105">Partner Center</span></span>

<span data-ttu-id="48dcf-106">Hämta en lista över erbjudanden om utvärderings konvertering.</span><span class="sxs-lookup"><span data-stu-id="48dcf-106">How to retrieve a list of trial conversion offers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="48dcf-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="48dcf-107">Prerequisites</span></span>

- <span data-ttu-id="48dcf-108">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="48dcf-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="48dcf-109">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="48dcf-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="48dcf-110">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="48dcf-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="48dcf-111">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="48dcf-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="48dcf-112">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="48dcf-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="48dcf-113">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="48dcf-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="48dcf-114">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="48dcf-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="48dcf-115">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="48dcf-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="48dcf-116">Ett prenumerations-ID för en aktiv utvärderings prenumeration.</span><span class="sxs-lookup"><span data-stu-id="48dcf-116">A subscription ID for an active trial subscription.</span></span>

## <a name="c"></a><span data-ttu-id="48dcf-117">C\#</span><span class="sxs-lookup"><span data-stu-id="48dcf-117">C\#</span></span>

<span data-ttu-id="48dcf-118">Om du vill hämta en lista över utvärderings versioner som är tillgängliga börjar du med att använda metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="48dcf-118">To get a list of trial conversions available, start by using the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="48dcf-119">Hämta sedan ett gränssnitt till prenumerations åtgärder genom att anropa metoden [**Subscriptions. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) med utvärderings prenumerationens ID.</span><span class="sxs-lookup"><span data-stu-id="48dcf-119">Then, get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the trial subscription ID.</span></span> <span data-ttu-id="48dcf-120">Använd sedan egenskapen [**konverteringar**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) för att hämta ett gränssnitt till de tillgängliga åtgärderna för konverteringar och anropa sedan metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) för att hämta en samling tillgängliga [**konverterings**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) erbjudanden.</span><span class="sxs-lookup"><span data-stu-id="48dcf-120">Next, use the [**Conversions**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) property to obtain an interface to the available operations on conversions, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) method to retrieve a collection of available [**Conversion**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) offers.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

// Get the available conversions.
var conversions =
    partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId).Conversions.Get();
```

## <a name="rest-request"></a><span data-ttu-id="48dcf-121">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="48dcf-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="48dcf-122">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="48dcf-122">Request syntax</span></span>

| <span data-ttu-id="48dcf-123">Metod</span><span class="sxs-lookup"><span data-stu-id="48dcf-123">Method</span></span>  | <span data-ttu-id="48dcf-124">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="48dcf-124">Request URI</span></span>                                                                                                                 |
|---------|-----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="48dcf-125">**TA**</span><span class="sxs-lookup"><span data-stu-id="48dcf-125">**GET**</span></span> | <span data-ttu-id="48dcf-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Subscriptions/{Subscription-ID}/conversions http/1.1</span><span class="sxs-lookup"><span data-stu-id="48dcf-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="48dcf-127">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="48dcf-127">URI parameter</span></span>

<span data-ttu-id="48dcf-128">Använd följande Sök vägs parametrar för att identifiera kunden och utvärderings prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="48dcf-128">Use the following path parameters to identify the customer and trial subscription.</span></span>

| <span data-ttu-id="48dcf-129">Namn</span><span class="sxs-lookup"><span data-stu-id="48dcf-129">Name</span></span>            | <span data-ttu-id="48dcf-130">Typ</span><span class="sxs-lookup"><span data-stu-id="48dcf-130">Type</span></span>   | <span data-ttu-id="48dcf-131">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="48dcf-131">Required</span></span> | <span data-ttu-id="48dcf-132">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="48dcf-132">Description</span></span>                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="48dcf-133">kund-ID</span><span class="sxs-lookup"><span data-stu-id="48dcf-133">customer-id</span></span>     | <span data-ttu-id="48dcf-134">sträng</span><span class="sxs-lookup"><span data-stu-id="48dcf-134">string</span></span> | <span data-ttu-id="48dcf-135">Yes</span><span class="sxs-lookup"><span data-stu-id="48dcf-135">Yes</span></span>      | <span data-ttu-id="48dcf-136">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="48dcf-136">A GUID formatted string that identifies the customer.</span></span>           |
| <span data-ttu-id="48dcf-137">prenumerations-ID</span><span class="sxs-lookup"><span data-stu-id="48dcf-137">subscription-id</span></span> | <span data-ttu-id="48dcf-138">sträng</span><span class="sxs-lookup"><span data-stu-id="48dcf-138">string</span></span> | <span data-ttu-id="48dcf-139">Yes</span><span class="sxs-lookup"><span data-stu-id="48dcf-139">Yes</span></span>      | <span data-ttu-id="48dcf-140">En GUID-formaterad sträng som identifierar utvärderings prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="48dcf-140">A GUID formatted string that identifies the trial subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="48dcf-141">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="48dcf-141">Request headers</span></span>

<span data-ttu-id="48dcf-142">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="48dcf-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="48dcf-143">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="48dcf-143">Request body</span></span>

<span data-ttu-id="48dcf-144">Inga.</span><span class="sxs-lookup"><span data-stu-id="48dcf-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="48dcf-145">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="48dcf-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/488745B5-2086-4912-802C-6ABB9F7C3638/conversions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e17f5bc6-24bf-4cbe-b632-d7fc6cec3058
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="48dcf-146">REST-svar</span><span class="sxs-lookup"><span data-stu-id="48dcf-146">REST response</span></span>

<span data-ttu-id="48dcf-147">Om det lyckas innehåller svars texten en samling [konverterings](conversions-resources.md#conversionresult) resurser.</span><span class="sxs-lookup"><span data-stu-id="48dcf-147">If successful, the response body contains a collection of [Conversion](conversions-resources.md#conversionresult) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="48dcf-148">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="48dcf-148">Response success and error codes</span></span>

<span data-ttu-id="48dcf-149">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="48dcf-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="48dcf-150">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="48dcf-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="48dcf-151">En fullständig lista finns i [fel koder för partner Center](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="48dcf-151">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="48dcf-152">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="48dcf-152">Response example</span></span>

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
