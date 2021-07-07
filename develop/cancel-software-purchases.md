---
title: Avbryt programvaruinköp
description: Självbetjäningsalternativ för att avbryta programvaruprenumerationer och beständiga programvaruköp med partnercenter-API:er.
ms.date: 12/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 877702ac930919ff72c6cc45a3c0e8ecc7e1b5f4
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974241"
---
# <a name="cancel-software-purchases"></a><span data-ttu-id="d2ad2-103">Avbryt programvaruinköp</span><span class="sxs-lookup"><span data-stu-id="d2ad2-103">Cancel software purchases</span></span>

<span data-ttu-id="d2ad2-104">Du kan använda Partner Center-API:er för att avbryta programvaruprenumerationer och beständiga programvaruinköp (så länge dessa inköp gjordes inom annulleringsfönstret från inköpsdatum).</span><span class="sxs-lookup"><span data-stu-id="d2ad2-104">You can use the Partner Center APIs to cancel software subscriptions and perpetual software purchases (as long as those purchases were made within the cancellation window from the purchase date).</span></span> <span data-ttu-id="d2ad2-105">Du behöver inte skapa en supportbiljett för att göra sådana uppsägningar och kan använda följande självbetjäningsmetoder i stället.</span><span class="sxs-lookup"><span data-stu-id="d2ad2-105">You don't need to create a support ticket to make such cancellations, and can use the following self-service methods instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d2ad2-106">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="d2ad2-106">Prerequisites</span></span>

- <span data-ttu-id="d2ad2-107">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="d2ad2-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d2ad2-108">Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="d2ad2-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="d2ad2-109">C\#</span><span class="sxs-lookup"><span data-stu-id="d2ad2-109">C\#</span></span>

<span data-ttu-id="d2ad2-110">Om du vill avbryta en programvarubeställning</span><span class="sxs-lookup"><span data-stu-id="d2ad2-110">To cancel a software order,</span></span>

1. <span data-ttu-id="d2ad2-111">Skicka autentiseringsuppgifterna för ditt konto [**till metoden CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) för att hämta [**ett IPartner-gränssnitt**](/dotnet/api/microsoft.store.partnercenter.ipartner) för att hämta partneråtgärder.</span><span class="sxs-lookup"><span data-stu-id="d2ad2-111">Pass your account credentials to the [**CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) method to get an [**IPartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) interface to get partner operations.</span></span>

2. <span data-ttu-id="d2ad2-112">Välj en viss [order](order-resources.md#order) som du vill avbryta.</span><span class="sxs-lookup"><span data-stu-id="d2ad2-112">Select a particular [Order](order-resources.md#order) you wish to cancel.</span></span> <span data-ttu-id="d2ad2-113">Anropa metoden [**Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kundidentifieraren, följt av **Orders.ById() med** orderidentifieraren.</span><span class="sxs-lookup"><span data-stu-id="d2ad2-113">Call the [**Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier, followed by **Orders.ById()** with order identifier.</span></span>

3. <span data-ttu-id="d2ad2-114">Anropa metoden **Get** eller **GetAsync** för att hämta ordern.</span><span class="sxs-lookup"><span data-stu-id="d2ad2-114">Call the **Get** or **GetAsync** method to retrieve the order.</span></span>

4. <span data-ttu-id="d2ad2-115">Ange egenskapen [**Order.Status**](order-resources.md#order) till `cancelled` .</span><span class="sxs-lookup"><span data-stu-id="d2ad2-115">Set the [**Order.Status**](order-resources.md#order) property to `cancelled`.</span></span>

5. <span data-ttu-id="d2ad2-116">(Valfritt) Om du vill ange vissa radobjekt för annullering ställer du in [**Order.LineItems**](order-resources.md#order) på en lista över radobjekt som du vill avbryta.</span><span class="sxs-lookup"><span data-stu-id="d2ad2-116">(Optional) If you want to specify certain line items for cancellation, set the [**Order.LineItems**](order-resources.md#order) to list of line items that you want to cancel.</span></span>

6. <span data-ttu-id="d2ad2-117">Använd **metoden Patch()** för att uppdatera ordningen.</span><span class="sxs-lookup"><span data-stu-id="d2ad2-117">Use the **Patch()** method to update the order.</span></span>

``` csharp
// IPartnerCredentials accountCredentials;
// Customer tenant Id to be deleted.
// string customerTenantId;

IPartner accountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(accountCredentials);

// Cancel order
var order = accountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Get();
order.Status = "cancelled";
order.LineItems = new List<OrderLineItem> {
    order.LineItems.First()
};
order = accountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Patch(order);

```

## <a name="rest-request"></a><span data-ttu-id="d2ad2-118">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="d2ad2-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d2ad2-119">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="d2ad2-119">Request syntax</span></span>

| <span data-ttu-id="d2ad2-120">Metod</span><span class="sxs-lookup"><span data-stu-id="d2ad2-120">Method</span></span>     | <span data-ttu-id="d2ad2-121">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="d2ad2-121">Request URI</span></span>                                                                            |
|------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="d2ad2-122">**Patch**</span><span class="sxs-lookup"><span data-stu-id="d2ad2-122">**PATCH**</span></span> | <span data-ttu-id="d2ad2-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d2ad2-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="d2ad2-124">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="d2ad2-124">URI parameters</span></span>

<span data-ttu-id="d2ad2-125">Använd följande frågeparametrar för att ta bort en kund.</span><span class="sxs-lookup"><span data-stu-id="d2ad2-125">Use the following query parameters to delete a customer.</span></span>

| <span data-ttu-id="d2ad2-126">Namn</span><span class="sxs-lookup"><span data-stu-id="d2ad2-126">Name</span></span>                   | <span data-ttu-id="d2ad2-127">Typ</span><span class="sxs-lookup"><span data-stu-id="d2ad2-127">Type</span></span>     | <span data-ttu-id="d2ad2-128">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="d2ad2-128">Required</span></span> | <span data-ttu-id="d2ad2-129">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="d2ad2-129">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d2ad2-130">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="d2ad2-130">**customer-tenant-id**</span></span> | <span data-ttu-id="d2ad2-131">**guid**</span><span class="sxs-lookup"><span data-stu-id="d2ad2-131">**guid**</span></span> | <span data-ttu-id="d2ad2-132">Y</span><span class="sxs-lookup"><span data-stu-id="d2ad2-132">Y</span></span>        | <span data-ttu-id="d2ad2-133">Värdet är ett GUID-formaterat kundklient-ID som gör att återförsäljaren kan filtrera resultaten för en viss kund som tillhör återförsäljaren.</span><span class="sxs-lookup"><span data-stu-id="d2ad2-133">The value is a GUID formatted customer tenant identifier that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="d2ad2-134">**order-id**</span><span class="sxs-lookup"><span data-stu-id="d2ad2-134">**order-id**</span></span> | <span data-ttu-id="d2ad2-135">**sträng**</span><span class="sxs-lookup"><span data-stu-id="d2ad2-135">**string**</span></span> | <span data-ttu-id="d2ad2-136">Y</span><span class="sxs-lookup"><span data-stu-id="d2ad2-136">Y</span></span>        | <span data-ttu-id="d2ad2-137">Värdet är en sträng som anger identifieraren för den order som du vill avbryta.</span><span class="sxs-lookup"><span data-stu-id="d2ad2-137">The value is a string that denotes the identifier of the order that you want to cancel.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d2ad2-138">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="d2ad2-138">Request headers</span></span>

<span data-ttu-id="d2ad2-139">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="d2ad2-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d2ad2-140">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="d2ad2-140">Request body</span></span>

```http
{
    “id”: “2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
    status": "cancelled",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0FKZV:0003:DG7GMGF0DWMS"
        }
    ]
}
```

### <a name="request-example"></a><span data-ttu-id="d2ad2-141">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="d2ad2-141">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/orders/<order-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd

{
    "id": "2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
    "status": "cancelled",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0FKZV:0003:DG7GMGF0DWMS"
        }
    ]
}
```

## <a name="rest-response"></a><span data-ttu-id="d2ad2-142">REST-svar</span><span class="sxs-lookup"><span data-stu-id="d2ad2-142">REST response</span></span>

<span data-ttu-id="d2ad2-143">Om det lyckas returnerar den här metoden ordern med annullerade radobjekt.</span><span class="sxs-lookup"><span data-stu-id="d2ad2-143">If successful, this method returns the order with canceled line items.</span></span>

<span data-ttu-id="d2ad2-144">Orderstatusen markeras antingen som annullerad om alla radartiklar i  ordern avbryts eller slutförs om inte alla radartiklar i ordern avbryts. </span><span class="sxs-lookup"><span data-stu-id="d2ad2-144">The order status will be marked as either **cancelled** if all the line items in the order are canceled, or **completed** if not all line items in the order are canceled.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d2ad2-145">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="d2ad2-145">Response success and error codes</span></span>

<span data-ttu-id="d2ad2-146">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="d2ad2-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d2ad2-147">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="d2ad2-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d2ad2-148">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="d2ad2-148">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d2ad2-149">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="d2ad2-149">Response example</span></span>

<span data-ttu-id="d2ad2-150">I följande exempelsvar kan du se att antalet radobjekt med erbjudande-ID har **`DG7GMGF0FKZV:0003:DG7GMGF0DWMS`** blivit noll (0).</span><span class="sxs-lookup"><span data-stu-id="d2ad2-150">In the following example response, you can see that the quantity of line item with the offer identifier **`DG7GMGF0FKZV:0003:DG7GMGF0DWMS`** has become zero (0).</span></span> <span data-ttu-id="d2ad2-151">Den här ändringen innebär att radobjektet som markerats för annullering har avbrutits.</span><span class="sxs-lookup"><span data-stu-id="d2ad2-151">This change means that the line item that was marked for cancellation has been canceled successfully.</span></span> <span data-ttu-id="d2ad2-152">Exempelordningen innehåller andra radobjekt som inte **annullerades,** vilket innebär att statusen för den övergripande ordern markeras som slutförd **,** inte annullerad .</span><span class="sxs-lookup"><span data-stu-id="d2ad2-152">The example order contains other line items that weren't canceled, which means that the status of the overall order will be marked as **completed**, not **cancelled**.</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 866
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

{
    "id": "2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
    "alternateId": "c403d91b21d2",
    "referenceCustomerId": "45411344-b09d-47e7-9653-542006bf9766",
    "billingCycle": "one_time",
    "currencyCode": "USD",
    "currencySymbol": "$",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0FKZV:0003:DG7GMGF0DWMS",
            "termDuration": "P3Y",
            "transactionType": "New",
            "friendlyName": "SQL Server Enterprise - 2 Core License Pack - 3 year",
            "quantity": 0,
            "links": {
                "product": {
                    "uri": "/products/DG7GMGF0FKZV?country=US",
                    "method": "GET",
                    "headers": []
                },
                "sku": {
                    "uri": "/products/DG7GMGF0FKZV/skus/0003?country=US",
                    "method": "GET",
                    "headers": []
                },
                "availability": {
                    "uri": "/products/DG7GMGF0FKZV/skus/0003/availabilities/DG7GMGF0DWMS?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        {
            "lineItemNumber": 1,
            "offerId": "DG7GMGF0DVT7:000C:DG7GMGF0FVZM",
            "termDuration": "P3Y",
            "transactionType": "New",
            "friendlyName": "Windows Server CAL - 1 Device CAL - 3 year",
            "quantity": 1,
            "links": {
                "product": {
                    "uri": "/products/DG7GMGF0DVT7?country=US",
                    "method": "GET",
                    "headers": []
                },
                "sku": {
                    "uri": "/products/DG7GMGF0DVT7/skus/000C?country=US",
                    "method": "GET",
                    "headers": []
                },
                "availability": {
                    "uri": "/products/DG7GMGF0DVT7/skus/000C/availabilities/DG7GMGF0FVZM?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2019-12-12T17:33:56.1306495Z",
    "status": "completed",
    "transactionType": "UserPurchase",
    "links": {
        "self": {
            "uri": "/customers/45411344-b09d-47e7-9653-542006bf9766/orders/2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
            "method": "GET",
            "headers": []
        },
        "provisioningStatus": {
            "uri": "/customers/45411344-b09d-47e7-9653-542006bf9766/orders/2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1/provisioningstatus",
            "method": "GET",
            "headers": []
        },
        "patchOperation": {
            "uri": "/customers/45411344-b09d-47e7-9653-542006bf9766/orders/2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
            "method": "PATCH",
            "headers": []
        }
    },
    "client": {
        "marketplaceCountry": "US",
        "deviceFamily": "UniversalStore-PartnerCenter",
        "name": "Partner Center API"
    },
    "attributes": {
        "objectType": "Order"
    }
}
```
