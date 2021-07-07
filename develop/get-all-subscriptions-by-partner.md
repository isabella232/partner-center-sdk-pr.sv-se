---
title: Hämta en kunds prenumerationer efter partner-MPN-ID
description: Hur du hämtar en lista över prenumerationer som tillhandahålls av en viss partner till en angiven kund.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 857caa667245503f111b27379a5c8f93aa1fb0b0
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760665"
---
# <a name="get-a-customers-subscriptions-by-partner-mpn-id"></a><span data-ttu-id="163b7-103">Hämta en kunds prenumerationer efter partner-MPN-ID</span><span class="sxs-lookup"><span data-stu-id="163b7-103">Get a customer's subscriptions by partner MPN ID</span></span>

<span data-ttu-id="163b7-104">**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="163b7-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="163b7-105">Hur du hämtar en lista över prenumerationer som tillhandahålls av en viss Microsoft Partner Network (MPN)-partner till en angiven kund.</span><span class="sxs-lookup"><span data-stu-id="163b7-105">How to get a list of subscriptions provided by a given Microsoft Partner Network (MPN) partner to a specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="163b7-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="163b7-106">Prerequisites</span></span>

- <span data-ttu-id="163b7-107">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="163b7-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="163b7-108">Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="163b7-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="163b7-109">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="163b7-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="163b7-110">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="163b7-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="163b7-111">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="163b7-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="163b7-112">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="163b7-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="163b7-113">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="163b7-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="163b7-114">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="163b7-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="163b7-115">En MPN-partneridentifierare.</span><span class="sxs-lookup"><span data-stu-id="163b7-115">A partner MPN identifier.</span></span>

## <a name="c"></a><span data-ttu-id="163b7-116">C\#</span><span class="sxs-lookup"><span data-stu-id="163b7-116">C\#</span></span>

<span data-ttu-id="163b7-117">Om du vill hämta en lista över prenumerationer som tillhandahålls av en viss partner till en angiven kund använder du först [**metoden IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="163b7-117">To get a list of subscriptions provided by a given partner to a specified customer, first use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="163b7-118">Hämta sedan ett gränssnitt för insamlingsåtgärder för kundprenumeration från egenskapen Prenumerationer och anropa [**metoden ByPartner**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.bypartner) med MPN-ID:t för att identifiera partnern och hämta ett gränssnitt för åtgärder för partnerprenumeration. [](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions)</span><span class="sxs-lookup"><span data-stu-id="163b7-118">Then get an interface to customer subscription collection operations from the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, and call the [**ByPartner**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.bypartner) method with the MPN ID to identify the partner and retrieve an interface to partner subscription operations.</span></span> <span data-ttu-id="163b7-119">Anropa slutligen metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync) för att hämta samlingen.</span><span class="sxs-lookup"><span data-stu-id="163b7-119">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync) method to get the collection.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string partnerMpnId;

var customerSubscriptionsByMpnId = partnerOperations.Customers.ById(customerId).Subscriptions.ByPartner(partnerMpnId).Get();
```

<span data-ttu-id="163b7-120">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="163b7-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="163b7-121">**Project:** Partnercenter-SDK Samples **Class**: GetSubscriptionsByMpnid.cs</span><span class="sxs-lookup"><span data-stu-id="163b7-121">**Project**: Partner Center SDK Samples **Class**: GetSubscriptionsByMpnid.cs</span></span>

## <a name="java"></a><span data-ttu-id="163b7-122">Java</span><span class="sxs-lookup"><span data-stu-id="163b7-122">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="163b7-123">Om du vill hämta en lista över prenumerationer som tillhandahålls av en viss partner till en angiven kund använder du först funktionen **IAggregatePartner.getCustomers.byId** med kund-ID:t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="163b7-123">To get a list of subscriptions provided by a given partner to a specified customer, first use the **IAggregatePartner.getCustomers.byId** function with the customer ID to identify the customer.</span></span> <span data-ttu-id="163b7-124">Hämta sedan ett gränssnitt för insamlingsåtgärder för kundprenumeration från funktionen **getSubscriptions** och anropa funktionen **byPartner** med MPN-ID:t för att identifiera partnern och hämta ett gränssnitt till åtgärder för partnerprenumeration.</span><span class="sxs-lookup"><span data-stu-id="163b7-124">Then get an interface to customer subscription collection operations from the **getSubscriptions** function, and call the **byPartner** function with the MPN ID to identify the partner and retrieve an interface to partner subscription operations.</span></span> <span data-ttu-id="163b7-125">Anropa slutligen **get-funktionen** för att hämta samlingen.</span><span class="sxs-lookup"><span data-stu-id="163b7-125">Finally, call the **get** function to get the collection.</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String partnerMpnId;

ResourceCollection<Subscription> customerSubscriptionsByMpnId = partnerOperations.getCustomers().byId(customerId).getSubscriptions().byPartner(partnerMpnId).get();
```

## <a name="powershell"></a><span data-ttu-id="163b7-126">PowerShell</span><span class="sxs-lookup"><span data-stu-id="163b7-126">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="163b7-127">Om du vill hämta en lista över prenumerationer som tillhandahålls av en viss partner till en angiven kund kör du kommandot [**Get-PartnerCustomerSubscription.**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscription.md)</span><span class="sxs-lookup"><span data-stu-id="163b7-127">To get a list of subscriptions provided by a given partner to a specified customer, execute the [**Get-PartnerCustomerSubscription**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscription.md) command.</span></span> <span data-ttu-id="163b7-128">Ange kund-ID:t för att identifiera kunden med hjälp av parametern **CustomerId** och fyll i **mpnId-parametern** med MPN-ID:t för att identifiera partnern.</span><span class="sxs-lookup"><span data-stu-id="163b7-128">Specify the customer ID to identify the customer using the **CustomerId** parameter, and populate the **MpnId** parameter with the MPN ID to identify the partner.</span></span>

```powershell
# $customerId
# $partnerMpnId

Get-PartnerCustomerSubscription -CustomerId $customerId -MpnId $partnerMpnId
```

## <a name="rest-request"></a><span data-ttu-id="163b7-129">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="163b7-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="163b7-130">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="163b7-130">Request syntax</span></span>

| <span data-ttu-id="163b7-131">Metod</span><span class="sxs-lookup"><span data-stu-id="163b7-131">Method</span></span>  | <span data-ttu-id="163b7-132">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="163b7-132">Request URI</span></span> |
|---------|----------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="163b7-133">**Få**</span><span class="sxs-lookup"><span data-stu-id="163b7-133">**GET**</span></span> | <span data-ttu-id="163b7-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions?mpn \_ id={mpn-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="163b7-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions?mpn\_id={mpn-id} HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="163b7-135">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="163b7-135">URI parameters</span></span>

<span data-ttu-id="163b7-136">Använd följande sökväg och frågeparametrar för att identifiera kunden och partnern.</span><span class="sxs-lookup"><span data-stu-id="163b7-136">Use the following path and query parameters to identify the customer and partner.</span></span>

| <span data-ttu-id="163b7-137">Namn</span><span class="sxs-lookup"><span data-stu-id="163b7-137">Name</span></span>        | <span data-ttu-id="163b7-138">Typ</span><span class="sxs-lookup"><span data-stu-id="163b7-138">Type</span></span>   | <span data-ttu-id="163b7-139">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="163b7-139">Required</span></span> | <span data-ttu-id="163b7-140">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="163b7-140">Description</span></span>                                                 |
|-------------|--------|----------|-------------------------------------------------------------|
| <span data-ttu-id="163b7-141">kund-ID</span><span class="sxs-lookup"><span data-stu-id="163b7-141">customer-id</span></span> | <span data-ttu-id="163b7-142">sträng</span><span class="sxs-lookup"><span data-stu-id="163b7-142">string</span></span> | <span data-ttu-id="163b7-143">Ja</span><span class="sxs-lookup"><span data-stu-id="163b7-143">Yes</span></span>      | <span data-ttu-id="163b7-144">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="163b7-144">A GUID formatted string that identifies the customer.</span></span>       |
| <span data-ttu-id="163b7-145">mpn-id</span><span class="sxs-lookup"><span data-stu-id="163b7-145">mpn-id</span></span>      | <span data-ttu-id="163b7-146">int</span><span class="sxs-lookup"><span data-stu-id="163b7-146">int</span></span>    | <span data-ttu-id="163b7-147">Ja</span><span class="sxs-lookup"><span data-stu-id="163b7-147">Yes</span></span>      | <span data-ttu-id="163b7-148">Ett Microsoft Partner Network-ID som identifierar partnern.</span><span class="sxs-lookup"><span data-stu-id="163b7-148">A Microsoft Partner Network ID that identifies the partner.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="163b7-149">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="163b7-149">Request headers</span></span>

<span data-ttu-id="163b7-150">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="163b7-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="163b7-151">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="163b7-151">Request body</span></span>

<span data-ttu-id="163b7-152">Inga.</span><span class="sxs-lookup"><span data-stu-id="163b7-152">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="163b7-153">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="163b7-153">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/subscriptions?mpn_id=4847383 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="163b7-154">REST-svar</span><span class="sxs-lookup"><span data-stu-id="163b7-154">REST response</span></span>

<span data-ttu-id="163b7-155">Om det lyckas innehåller svarstexten samlingen [prenumerationsresurser.](subscription-resources.md)</span><span class="sxs-lookup"><span data-stu-id="163b7-155">If successful, the response body contains the collection of [Subscription](subscription-resources.md) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="163b7-156">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="163b7-156">Response success and error codes</span></span>

<span data-ttu-id="163b7-157">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="163b7-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="163b7-158">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="163b7-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="163b7-159">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="163b7-159">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="163b7-160">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="163b7-160">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 985
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CV: LdFhumtx6Ea0Kl5Z.0
MS-ServerId: 101112202
Date: Thu, 13 Apr 2017 20:58:08 GMT

{
    "totalCount": 1,
    "items": [{
            "id": "42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
            "offerId": "DB2E705F-B82A-4024-A3D5-D88E12F2DB35",
            "offerName": "Intune Device",
            "friendlyName": "new offer purchase",
            "quantity": 5,
            "unitType": "Licenses",
            "creationDate": "2017-04-10T23:02:26.02Z",
            "effectiveStartDate": "2017-04-10T00:00:00Z",
            "commitmentEndDate": "2018-05-07T00:00:00Z",
            "status": "active",
            "autoRenewEnabled": true,
            "isTrial": false,
            "billingType": "license",
            "billingCycle": "monthly",
            "partnerId": "4847383",
            "contractType": "subscription",
            "links": {
                "offer": {
                    "uri": "/offers/DB2E705F-B82A-4024-A3D5-D88E12F2DB35?country=US",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/subscriptions/42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
                    "method": "GET",
                    "headers": []
                }
            },
            "orderId": "3EDDCAC6-63B2-4C40-B0B6-F47E18301492",
            "attributes": {
                "etag": "eyJpZCI6IjQyMjI2ZWQ2LTA3MGEtNGUwZi1iODBjLTRjZGZiM2U5N2FhNyIsInZlcnNpb24iOjF9",
                "objectType": "Subscription"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

## <a name="see-also"></a><span data-ttu-id="163b7-161">Se även</span><span class="sxs-lookup"><span data-stu-id="163b7-161">See also</span></span>

- [<span data-ttu-id="163b7-162">Partnercenter-analys – resurser</span><span class="sxs-lookup"><span data-stu-id="163b7-162">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
