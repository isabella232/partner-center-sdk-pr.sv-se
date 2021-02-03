---
title: Hämta en kunds prenumerationer efter partner-MPN-ID
description: Så här hämtar du en lista över prenumerationer som tillhandahålls av en viss partner till en angiven kund.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: c95488b62449e1ab6bd2eeefea58d6686c291f4c
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769711"
---
# <a name="get-a-customers-subscriptions-by-partner-mpn-id"></a><span data-ttu-id="2b59b-103">Hämta en kunds prenumerationer efter partner-MPN-ID</span><span class="sxs-lookup"><span data-stu-id="2b59b-103">Get a customer's subscriptions by partner MPN ID</span></span>

<span data-ttu-id="2b59b-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="2b59b-104">**Applies To**</span></span>

- <span data-ttu-id="2b59b-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="2b59b-105">Partner Center</span></span>
- <span data-ttu-id="2b59b-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="2b59b-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="2b59b-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="2b59b-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="2b59b-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="2b59b-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="2b59b-109">Så här hämtar du en lista över prenumerationer som tillhandahålls av en viss partner till en angiven kund.</span><span class="sxs-lookup"><span data-stu-id="2b59b-109">How to get a list of subscriptions provided by a given partner to a specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b59b-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="2b59b-110">Prerequisites</span></span>

- <span data-ttu-id="2b59b-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="2b59b-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2b59b-112">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="2b59b-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="2b59b-113">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2b59b-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="2b59b-114">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="2b59b-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="2b59b-115">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="2b59b-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="2b59b-116">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="2b59b-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="2b59b-117">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="2b59b-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="2b59b-118">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2b59b-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="2b59b-119">Ett partner Microsoft Partner Network (MPN)-ID.</span><span class="sxs-lookup"><span data-stu-id="2b59b-119">A partner Microsoft Partner Network (MPN) identifier.</span></span>

## <a name="c"></a><span data-ttu-id="2b59b-120">C\#</span><span class="sxs-lookup"><span data-stu-id="2b59b-120">C\#</span></span>

<span data-ttu-id="2b59b-121">Om du vill hämta en lista över prenumerationer från en viss partner till en angiven kund använder du först metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="2b59b-121">To get a list of subscriptions provided by a given partner to a specified customer, first use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="2b59b-122">Hämta sedan ett gränssnitt till åtgärder för kund prenumerations insamling från egenskapen [**prenumerationer**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) och anropa metoden [**ByPartner**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.bypartner) med MPN-ID för att identifiera partnern och hämta ett gränssnitt till partner prenumerations åtgärder.</span><span class="sxs-lookup"><span data-stu-id="2b59b-122">Then get an interface to customer subscription collection operations from the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, and call the [**ByPartner**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.bypartner) method with the MPN ID to identify the partner and retrieve an interface to partner subscription operations.</span></span> <span data-ttu-id="2b59b-123">Anropa slutligen metoden [**Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) eller [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync) för att hämta samlingen.</span><span class="sxs-lookup"><span data-stu-id="2b59b-123">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync) method to get the collection.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string partnerMpnId;

var customerSubscriptionsByMpnId = partnerOperations.Customers.ById(customerId).Subscriptions.ByPartner(partnerMpnId).Get();
```

<span data-ttu-id="2b59b-124">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="2b59b-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="2b59b-125">**Projekt**: Partner Center SDK-exempel **klass**: GetSubscriptionsByMpnid.CS</span><span class="sxs-lookup"><span data-stu-id="2b59b-125">**Project**: Partner Center SDK Samples **Class**: GetSubscriptionsByMpnid.cs</span></span>

## <a name="java"></a><span data-ttu-id="2b59b-126">Java</span><span class="sxs-lookup"><span data-stu-id="2b59b-126">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="2b59b-127">Om du vill hämta en lista över prenumerationer från en viss partner till en angiven kund använder du först funktionen **IAggregatePartner. getCustomers. byId** med kund-ID: t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="2b59b-127">To get a list of subscriptions provided by a given partner to a specified customer, first use the **IAggregatePartner.getCustomers.byId** function with the customer ID to identify the customer.</span></span> <span data-ttu-id="2b59b-128">Hämta sedan ett gränssnitt till åtgärder för kund prenumerations insamling från funktionen **getSubscriptions** och anropa **byPartner** -funktionen med MPN-ID för att identifiera partnern och hämta ett gränssnitt till partner prenumerations åtgärder.</span><span class="sxs-lookup"><span data-stu-id="2b59b-128">Then get an interface to customer subscription collection operations from the **getSubscriptions** function, and call the **byPartner** function with the MPN ID to identify the partner and retrieve an interface to partner subscription operations.</span></span> <span data-ttu-id="2b59b-129">Anropa slutligen funktionen **Get** för att hämta samlingen.</span><span class="sxs-lookup"><span data-stu-id="2b59b-129">Finally, call the **get** function to get the collection.</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String partnerMpnId;

ResourceCollection<Subscription> customerSubscriptionsByMpnId = partnerOperations.getCustomers().byId(customerId).getSubscriptions().byPartner(partnerMpnId).get();
```

## <a name="powershell"></a><span data-ttu-id="2b59b-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2b59b-130">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="2b59b-131">Om du vill hämta en lista över prenumerationer som tillhandahålls av en viss partner till en angiven kund kör du kommandot [**Get-PartnerCustomerSubscription**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscription.md) .</span><span class="sxs-lookup"><span data-stu-id="2b59b-131">To get a list of subscriptions provided by a given partner to a specified customer, execute the [**Get-PartnerCustomerSubscription**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscription.md) command.</span></span> <span data-ttu-id="2b59b-132">Ange kund-ID: t för att identifiera kunden med parametern **CustomerId** och fyll i **MpnId** -parametern med MPN-ID för att identifiera partnern.</span><span class="sxs-lookup"><span data-stu-id="2b59b-132">Specify the customer ID to identify the customer using the **CustomerId** parameter, and populate the **MpnId** parameter with the MPN ID to identify the partner.</span></span>

```powershell
# $customerId
# $partnerMpnId

Get-PartnerCustomerSubscription -CustomerId $customerId -MpnId $partnerMpnId
```

## <a name="rest-request"></a><span data-ttu-id="2b59b-133">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="2b59b-133">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2b59b-134">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="2b59b-134">Request syntax</span></span>

| <span data-ttu-id="2b59b-135">Metod</span><span class="sxs-lookup"><span data-stu-id="2b59b-135">Method</span></span>  | <span data-ttu-id="2b59b-136">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="2b59b-136">Request URI</span></span> |
|---------|----------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2b59b-137">**TA**</span><span class="sxs-lookup"><span data-stu-id="2b59b-137">**GET**</span></span> | <span data-ttu-id="2b59b-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Subscriptions? MPN \_ -ID = {MPN-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="2b59b-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions?mpn\_id={mpn-id} HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="2b59b-139">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="2b59b-139">URI parameters</span></span>

<span data-ttu-id="2b59b-140">Använd följande sökväg och frågeparametrar för att identifiera kunden och partnern.</span><span class="sxs-lookup"><span data-stu-id="2b59b-140">Use the following path and query parameters to identify the customer and partner.</span></span>

| <span data-ttu-id="2b59b-141">Namn</span><span class="sxs-lookup"><span data-stu-id="2b59b-141">Name</span></span>        | <span data-ttu-id="2b59b-142">Typ</span><span class="sxs-lookup"><span data-stu-id="2b59b-142">Type</span></span>   | <span data-ttu-id="2b59b-143">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="2b59b-143">Required</span></span> | <span data-ttu-id="2b59b-144">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="2b59b-144">Description</span></span>                                                 |
|-------------|--------|----------|-------------------------------------------------------------|
| <span data-ttu-id="2b59b-145">kund-ID</span><span class="sxs-lookup"><span data-stu-id="2b59b-145">customer-id</span></span> | <span data-ttu-id="2b59b-146">sträng</span><span class="sxs-lookup"><span data-stu-id="2b59b-146">string</span></span> | <span data-ttu-id="2b59b-147">Yes</span><span class="sxs-lookup"><span data-stu-id="2b59b-147">Yes</span></span>      | <span data-ttu-id="2b59b-148">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="2b59b-148">A GUID formatted string that identifies the customer.</span></span>       |
| <span data-ttu-id="2b59b-149">MPN-ID</span><span class="sxs-lookup"><span data-stu-id="2b59b-149">mpn-id</span></span>      | <span data-ttu-id="2b59b-150">int</span><span class="sxs-lookup"><span data-stu-id="2b59b-150">int</span></span>    | <span data-ttu-id="2b59b-151">Yes</span><span class="sxs-lookup"><span data-stu-id="2b59b-151">Yes</span></span>      | <span data-ttu-id="2b59b-152">Ett Microsoft Partner Network-ID som identifierar partnern.</span><span class="sxs-lookup"><span data-stu-id="2b59b-152">A Microsoft Partner Network ID that identifies the partner.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="2b59b-153">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="2b59b-153">Request headers</span></span>

<span data-ttu-id="2b59b-154">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="2b59b-154">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2b59b-155">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="2b59b-155">Request body</span></span>

<span data-ttu-id="2b59b-156">Inga.</span><span class="sxs-lookup"><span data-stu-id="2b59b-156">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="2b59b-157">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="2b59b-157">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="2b59b-158">REST-svar</span><span class="sxs-lookup"><span data-stu-id="2b59b-158">REST response</span></span>

<span data-ttu-id="2b59b-159">Om det lyckas innehåller svars texten samlingen av [prenumerations](subscription-resources.md) resurser.</span><span class="sxs-lookup"><span data-stu-id="2b59b-159">If successful, the response body contains the collection of [Subscription](subscription-resources.md) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2b59b-160">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="2b59b-160">Response success and error codes</span></span>

<span data-ttu-id="2b59b-161">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="2b59b-161">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2b59b-162">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="2b59b-162">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2b59b-163">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="2b59b-163">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2b59b-164">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="2b59b-164">Response example</span></span>

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

## <a name="see-also"></a><span data-ttu-id="2b59b-165">Se även</span><span class="sxs-lookup"><span data-stu-id="2b59b-165">See also</span></span>

- [<span data-ttu-id="2b59b-166">Partnercenter-analys – resurser</span><span class="sxs-lookup"><span data-stu-id="2b59b-166">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
