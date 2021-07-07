---
title: Hämta en beställning efter ID
description: Hämtar en orderresurs som matchar kunden och order-ID:t.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 2cb2822935113fe1c5337b4ffc899fccff333d2f
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760189"
---
# <a name="get-an-order-by-id"></a><span data-ttu-id="635b4-103">Hämta en beställning efter ID</span><span class="sxs-lookup"><span data-stu-id="635b4-103">Get an order by ID</span></span>

<span data-ttu-id="635b4-104">**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="635b4-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="635b4-105">Hämtar en [orderresurs](order-resources.md) som matchar kunden och order-ID:t.</span><span class="sxs-lookup"><span data-stu-id="635b4-105">Gets an [Order](order-resources.md) resource that matches the customer and order ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="635b4-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="635b4-106">Prerequisites</span></span>

- <span data-ttu-id="635b4-107">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="635b4-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="635b4-108">Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="635b4-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="635b4-109">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="635b4-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="635b4-110">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="635b4-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="635b4-111">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="635b4-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="635b4-112">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="635b4-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="635b4-113">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="635b4-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="635b4-114">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="635b4-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="635b4-115">Ett order-ID.</span><span class="sxs-lookup"><span data-stu-id="635b4-115">An order ID.</span></span>

## <a name="c"></a><span data-ttu-id="635b4-116">C\#</span><span class="sxs-lookup"><span data-stu-id="635b4-116">C\#</span></span>

<span data-ttu-id="635b4-117">Så här hämtar du en kunds order efter ID:</span><span class="sxs-lookup"><span data-stu-id="635b4-117">To get a customer's order by ID:</span></span>

1. <span data-ttu-id="635b4-118">Använd din **IAggregatePartner.Customers-samling** och anropa **metoden ById().**</span><span class="sxs-lookup"><span data-stu-id="635b4-118">Use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span>

2. <span data-ttu-id="635b4-119">Anropa egenskapen [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) följt av [**metoden ByID()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) en gång till.</span><span class="sxs-lookup"><span data-stu-id="635b4-119">Call the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property, followed by the [**ByID()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) method once more.</span></span>
3. <span data-ttu-id="635b4-120">Anropa [**Get()**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.get) eller [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.getasync).</span><span class="sxs-lookup"><span data-stu-id="635b4-120">Call [**Get()**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.getasync).</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedOrderId;

var order = partnerOperations.Customers.ById(selectedCustomerId).Orders.ById(selectedOrderId).Get();
```

<span data-ttu-id="635b4-121">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="635b4-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="635b4-122">**Project:** PartnerSDK.FeatureSample-klass: GetOrder.cs </span><span class="sxs-lookup"><span data-stu-id="635b4-122">**Project**: PartnerSDK.FeatureSample **Class**: GetOrder.cs</span></span>

## <a name="java"></a><span data-ttu-id="635b4-123">Java</span><span class="sxs-lookup"><span data-stu-id="635b4-123">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="635b4-124">Så här hämtar du en kunds order efter ID:</span><span class="sxs-lookup"><span data-stu-id="635b4-124">To get a customer's order by ID:</span></span>

1. <span data-ttu-id="635b4-125">Använd funktionen **IAggregatePartner.getCustomers** och anropa **funktionen byId().**</span><span class="sxs-lookup"><span data-stu-id="635b4-125">Use your **IAggregatePartner.getCustomers** function and call the **byId()** function.</span></span>

2. <span data-ttu-id="635b4-126">Anropa funktionen **getOrders,** följt av **funktionen byID()** en gång till.</span><span class="sxs-lookup"><span data-stu-id="635b4-126">Call the **getOrders** function, followed by the **byID()** function once more.</span></span>
3. <span data-ttu-id="635b4-127">Anropa **funktionen get().**</span><span class="sxs-lookup"><span data-stu-id="635b4-127">Call the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;
// String selectedCustomerId;
// String selectedOrderId;

Order order = partnerOperations.getCustomers().byId(selectedCustomerId).getOrders().byId(selectedOrderId).get();
```

## <a name="powershell"></a><span data-ttu-id="635b4-128">PowerShell</span><span class="sxs-lookup"><span data-stu-id="635b4-128">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="635b4-129">Om du vill hämta en kunds order efter ID kör du kommandot [**Get-PartnerCustomerOrder**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerOrder.md) och anger **parametrarna CustomerId** och **OrderId.**</span><span class="sxs-lookup"><span data-stu-id="635b4-129">To get a customer's order by ID, execute the [**Get-PartnerCustomerOrder**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerOrder.md) command, and specify the **CustomerId** and **OrderId** parameters.</span></span>

```powershell
# $selectedCustomerId
# $selectedOrderId

Get-PartnerCustomerOrder -CustomerId $selectedCustomerId -OrderId $selectedOrderId
```

## <a name="rest-request"></a><span data-ttu-id="635b4-130">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="635b4-130">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="635b4-131">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="635b4-131">Request syntax</span></span>

| <span data-ttu-id="635b4-132">Metod</span><span class="sxs-lookup"><span data-stu-id="635b4-132">Method</span></span>  | <span data-ttu-id="635b4-133">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="635b4-133">Request URI</span></span>                                                                                                  |
|---------|--------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="635b4-134">**Få**</span><span class="sxs-lookup"><span data-stu-id="635b4-134">**GET**</span></span> | <span data-ttu-id="635b4-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{id-for-order} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="635b4-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{id-for-order} HTTP/1.1</span></span>  |

#### <a name="uri-parameters"></a><span data-ttu-id="635b4-136">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="635b4-136">URI parameters</span></span>

<span data-ttu-id="635b4-137">I den här tabellen visas de frågeparametrar som krävs för att hämta en order efter ID.</span><span class="sxs-lookup"><span data-stu-id="635b4-137">This table lists the required query parameters to get an order by ID.</span></span>

| <span data-ttu-id="635b4-138">Namn</span><span class="sxs-lookup"><span data-stu-id="635b4-138">Name</span></span>                   | <span data-ttu-id="635b4-139">Typ</span><span class="sxs-lookup"><span data-stu-id="635b4-139">Type</span></span>     | <span data-ttu-id="635b4-140">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="635b4-140">Required</span></span> | <span data-ttu-id="635b4-141">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="635b4-141">Description</span></span>                                            |
|------------------------|----------|----------|--------------------------------------------------------|
| <span data-ttu-id="635b4-142">kund-klient-id</span><span class="sxs-lookup"><span data-stu-id="635b4-142">customer-tenant-id</span></span>     | <span data-ttu-id="635b4-143">sträng</span><span class="sxs-lookup"><span data-stu-id="635b4-143">string</span></span>   | <span data-ttu-id="635b4-144">Ja</span><span class="sxs-lookup"><span data-stu-id="635b4-144">Yes</span></span>      | <span data-ttu-id="635b4-145">En GUID-formaterad sträng som motsvarar kunden.</span><span class="sxs-lookup"><span data-stu-id="635b4-145">A GUID formatted string corresponding to the customer.</span></span> |
| <span data-ttu-id="635b4-146">id-for-order</span><span class="sxs-lookup"><span data-stu-id="635b4-146">id-for-order</span></span>           | <span data-ttu-id="635b4-147">sträng</span><span class="sxs-lookup"><span data-stu-id="635b4-147">string</span></span>   | <span data-ttu-id="635b4-148">Ja</span><span class="sxs-lookup"><span data-stu-id="635b4-148">Yes</span></span>      | <span data-ttu-id="635b4-149">En sträng som motsvarar order-ID:t.</span><span class="sxs-lookup"><span data-stu-id="635b4-149">A string corresponding to the order ID.</span></span>                |

### <a name="request-headers"></a><span data-ttu-id="635b4-150">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="635b4-150">Request headers</span></span>

<span data-ttu-id="635b4-151">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="635b4-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="635b4-152">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="635b4-152">Request body</span></span>

<span data-ttu-id="635b4-153">Inga.</span><span class="sxs-lookup"><span data-stu-id="635b4-153">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="635b4-154">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="635b4-154">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/orders/<id-for-order> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="635b4-155">REST-svar</span><span class="sxs-lookup"><span data-stu-id="635b4-155">REST response</span></span>

<span data-ttu-id="635b4-156">Om det lyckas returnerar den här metoden [en Order-resurs](order-resources.md) i svarstexten.</span><span class="sxs-lookup"><span data-stu-id="635b4-156">If successful, this method returns an [Order](order-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="635b4-157">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="635b4-157">Response success and error codes</span></span>

<span data-ttu-id="635b4-158">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="635b4-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="635b4-159">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="635b4-159">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="635b4-160">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="635b4-160">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="635b4-161">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="635b4-161">Response example</span></span>

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
