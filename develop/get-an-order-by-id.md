---
title: Hämta en beställning efter ID
description: 'Hämtar en order resurs som matchar kunden och order-ID: t.'
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 0a39d7142e5bf97f9fb345416964d4ed6bb935ad
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769870"
---
# <a name="get-an-order-by-id"></a><span data-ttu-id="e9bd0-103">Hämta en beställning efter ID</span><span class="sxs-lookup"><span data-stu-id="e9bd0-103">Get an order by ID</span></span>

<span data-ttu-id="e9bd0-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="e9bd0-104">**Applies to:**</span></span>

- <span data-ttu-id="e9bd0-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="e9bd0-105">Partner Center</span></span>
- <span data-ttu-id="e9bd0-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="e9bd0-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="e9bd0-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="e9bd0-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="e9bd0-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="e9bd0-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="e9bd0-109">Hämtar en [order](order-resources.md) resurs som matchar kunden och order-ID: t.</span><span class="sxs-lookup"><span data-stu-id="e9bd0-109">Gets an [Order](order-resources.md) resource that matches the customer and order ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e9bd0-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="e9bd0-110">Prerequisites</span></span>

- <span data-ttu-id="e9bd0-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e9bd0-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e9bd0-112">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="e9bd0-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="e9bd0-113">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e9bd0-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="e9bd0-114">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="e9bd0-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="e9bd0-115">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="e9bd0-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="e9bd0-116">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="e9bd0-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="e9bd0-117">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="e9bd0-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="e9bd0-118">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e9bd0-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="e9bd0-119">Ett order-ID.</span><span class="sxs-lookup"><span data-stu-id="e9bd0-119">An order ID.</span></span>

## <a name="c"></a><span data-ttu-id="e9bd0-120">C\#</span><span class="sxs-lookup"><span data-stu-id="e9bd0-120">C\#</span></span>

<span data-ttu-id="e9bd0-121">Så här hämtar du en kund order efter ID:</span><span class="sxs-lookup"><span data-stu-id="e9bd0-121">To get a customer's order by ID:</span></span>

1. <span data-ttu-id="e9bd0-122">Använd din **IAggregatePartner. Customers** -samling och anropa **ById ()-** metoden.</span><span class="sxs-lookup"><span data-stu-id="e9bd0-122">Use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span>

2. <span data-ttu-id="e9bd0-123">Anropa egenskapen [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) följt av metoden [**ByID ()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) en gång till.</span><span class="sxs-lookup"><span data-stu-id="e9bd0-123">Call the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property, followed by the [**ByID()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) method once more.</span></span>
3. <span data-ttu-id="e9bd0-124">Anropa [**Get ()**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.get) eller [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.getasync).</span><span class="sxs-lookup"><span data-stu-id="e9bd0-124">Call [**Get()**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.getasync).</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedOrderId;

var order = partnerOperations.Customers.ById(selectedCustomerId).Orders.ById(selectedOrderId).Get();
```

<span data-ttu-id="e9bd0-125">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="e9bd0-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="e9bd0-126">**Projekt**: PartnerSDK. FeatureSample- **klass**: GetOrder.CS</span><span class="sxs-lookup"><span data-stu-id="e9bd0-126">**Project**: PartnerSDK.FeatureSample **Class**: GetOrder.cs</span></span>

## <a name="java"></a><span data-ttu-id="e9bd0-127">Java</span><span class="sxs-lookup"><span data-stu-id="e9bd0-127">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="e9bd0-128">Så här hämtar du en kund order efter ID:</span><span class="sxs-lookup"><span data-stu-id="e9bd0-128">To get a customer's order by ID:</span></span>

1. <span data-ttu-id="e9bd0-129">Använd din **IAggregatePartner. getCustomers** -funktion och anropa funktionen **byId ()** .</span><span class="sxs-lookup"><span data-stu-id="e9bd0-129">Use your **IAggregatePartner.getCustomers** function and call the **byId()** function.</span></span>

2. <span data-ttu-id="e9bd0-130">Anropa funktionen **getOrders** , följt av funktionen **byID ()** en gång till.</span><span class="sxs-lookup"><span data-stu-id="e9bd0-130">Call the **getOrders** function, followed by the **byID()** function once more.</span></span>
3. <span data-ttu-id="e9bd0-131">Anropa funktionen **Get ()** .</span><span class="sxs-lookup"><span data-stu-id="e9bd0-131">Call the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;
// String selectedCustomerId;
// String selectedOrderId;

Order order = partnerOperations.getCustomers().byId(selectedCustomerId).getOrders().byId(selectedOrderId).get();
```

## <a name="powershell"></a><span data-ttu-id="e9bd0-132">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e9bd0-132">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="e9bd0-133">För att få en kund order utifrån ID kör du kommandot [**Get-PartnerCustomerOrder**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerOrder.md) och anger parametrarna **CustomerId** och **Ordernr** .</span><span class="sxs-lookup"><span data-stu-id="e9bd0-133">To get a customer's order by ID, execute the [**Get-PartnerCustomerOrder**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerOrder.md) command, and specify the **CustomerId** and **OrderId** parameters.</span></span>

```powershell
# $selectedCustomerId
# $selectedOrderId

Get-PartnerCustomerOrder -CustomerId $selectedCustomerId -OrderId $selectedOrderId
```

## <a name="rest-request"></a><span data-ttu-id="e9bd0-134">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="e9bd0-134">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e9bd0-135">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="e9bd0-135">Request syntax</span></span>

| <span data-ttu-id="e9bd0-136">Metod</span><span class="sxs-lookup"><span data-stu-id="e9bd0-136">Method</span></span>  | <span data-ttu-id="e9bd0-137">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="e9bd0-137">Request URI</span></span>                                                                                                  |
|---------|--------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e9bd0-138">**TA**</span><span class="sxs-lookup"><span data-stu-id="e9bd0-138">**GET**</span></span> | <span data-ttu-id="e9bd0-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Orders/{ID-for-order} http/1.1</span><span class="sxs-lookup"><span data-stu-id="e9bd0-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{id-for-order} HTTP/1.1</span></span>  |

#### <a name="uri-parameters"></a><span data-ttu-id="e9bd0-140">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="e9bd0-140">URI parameters</span></span>

<span data-ttu-id="e9bd0-141">Den här tabellen innehåller de frågeparametrar som krävs för att hämta en order efter ID.</span><span class="sxs-lookup"><span data-stu-id="e9bd0-141">This table lists the required query parameters to get an order by ID.</span></span>

| <span data-ttu-id="e9bd0-142">Namn</span><span class="sxs-lookup"><span data-stu-id="e9bd0-142">Name</span></span>                   | <span data-ttu-id="e9bd0-143">Typ</span><span class="sxs-lookup"><span data-stu-id="e9bd0-143">Type</span></span>     | <span data-ttu-id="e9bd0-144">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="e9bd0-144">Required</span></span> | <span data-ttu-id="e9bd0-145">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="e9bd0-145">Description</span></span>                                            |
|------------------------|----------|----------|--------------------------------------------------------|
| <span data-ttu-id="e9bd0-146">kund-ID för klient organisation</span><span class="sxs-lookup"><span data-stu-id="e9bd0-146">customer-tenant-id</span></span>     | <span data-ttu-id="e9bd0-147">sträng</span><span class="sxs-lookup"><span data-stu-id="e9bd0-147">string</span></span>   | <span data-ttu-id="e9bd0-148">Yes</span><span class="sxs-lookup"><span data-stu-id="e9bd0-148">Yes</span></span>      | <span data-ttu-id="e9bd0-149">En GUID-formaterad sträng som motsvarar kunden.</span><span class="sxs-lookup"><span data-stu-id="e9bd0-149">A GUID formatted string corresponding to the customer.</span></span> |
| <span data-ttu-id="e9bd0-150">ID-för-order</span><span class="sxs-lookup"><span data-stu-id="e9bd0-150">id-for-order</span></span>           | <span data-ttu-id="e9bd0-151">sträng</span><span class="sxs-lookup"><span data-stu-id="e9bd0-151">string</span></span>   | <span data-ttu-id="e9bd0-152">Yes</span><span class="sxs-lookup"><span data-stu-id="e9bd0-152">Yes</span></span>      | <span data-ttu-id="e9bd0-153">En sträng som motsvarar order-ID: t.</span><span class="sxs-lookup"><span data-stu-id="e9bd0-153">A string corresponding to the order ID.</span></span>                |

### <a name="request-headers"></a><span data-ttu-id="e9bd0-154">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="e9bd0-154">Request headers</span></span>

<span data-ttu-id="e9bd0-155">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="e9bd0-155">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e9bd0-156">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="e9bd0-156">Request body</span></span>

<span data-ttu-id="e9bd0-157">Inga.</span><span class="sxs-lookup"><span data-stu-id="e9bd0-157">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="e9bd0-158">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="e9bd0-158">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/orders/<id-for-order> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="e9bd0-159">REST-svar</span><span class="sxs-lookup"><span data-stu-id="e9bd0-159">REST response</span></span>

<span data-ttu-id="e9bd0-160">Om det lyckas returnerar den här metoden en [order](order-resources.md) resurs i svars texten.</span><span class="sxs-lookup"><span data-stu-id="e9bd0-160">If successful, this method returns an [Order](order-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e9bd0-161">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="e9bd0-161">Response success and error codes</span></span>

<span data-ttu-id="e9bd0-162">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="e9bd0-162">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e9bd0-163">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="e9bd0-163">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e9bd0-164">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e9bd0-164">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e9bd0-165">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="e9bd0-165">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 823
Content-Type: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Date: Thu, 15 Mar 2018 22:05:30 GMT

{
    "id": "YxH1q4KScfvfkJQjgRI8QY1DznnUWZTH1",
    "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
    "billingCycle": "one_time",
    "currencyCode": "USD",
    "currencySymbol" : "$",
    "lineItems": [
    {
        "lineItemNumber": 0,
        "offerId": "DZH318Z0BQ4Z:002L:DZH318Z0CMNP",
        "friendlyName": "Reserved_VM_Instance_Standard_NC12_AU_East_1_Year",
        "quantity": 1,
        "links": {
            "sku": {
                "uri": "/products/DZH318Z0BQ4Z/skus/002L?country=US",
                "method": "GET",
                "headers": []
            }
        }
    }
    ],
    "creationDate": "2018-03-13T22:49:54.3396949Z",
    "status": "completed",
    "links": {
        "provisioningStatus": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/YxH1q4KScfvfkJQjgRI8QY1DznnUWZTH1/provisioningstatus",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/YxH1q4KScfvfkJQjgRI8QY1DznnUWZTH1",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Order"
    }
}
```
