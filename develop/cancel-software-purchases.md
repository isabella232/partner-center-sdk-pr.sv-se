---
title: Avbryt programvaruinköp
description: 'Alternativet för självbetjäning för att avbryta program varu prenumerationer och permanent program varu inköp med API: er för partner Center.'
ms.date: 12/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 25fd10a171fa6ca01f3442d49145443f2382cc18
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769327"
---
# <a name="cancel-software-purchases"></a><span data-ttu-id="a100b-103">Avbryt programvaruinköp</span><span class="sxs-lookup"><span data-stu-id="a100b-103">Cancel software purchases</span></span>

<span data-ttu-id="a100b-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="a100b-104">**Applies to:**</span></span>

- <span data-ttu-id="a100b-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="a100b-105">Partner Center</span></span>

<span data-ttu-id="a100b-106">Du kan använda API: er för partner Center för att avbryta program varu prenumerationer och program varu inköp utan program vara (så länge som de här inköpen gjorts i fönstret för annullering från inköps datumet).</span><span class="sxs-lookup"><span data-stu-id="a100b-106">You can use the Partner Center APIs to cancel software subscriptions and perpetual software purchases (as long as those purchases were made within the cancellation window from the purchase date).</span></span> <span data-ttu-id="a100b-107">Du behöver inte skapa ett support ärende för att göra sådana avbrott och kan använda följande självbetjänings metoder i stället.</span><span class="sxs-lookup"><span data-stu-id="a100b-107">You don't need to create a support ticket to make such cancellations, and can use the following self-service methods instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a100b-108">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="a100b-108">Prerequisites</span></span>

- <span data-ttu-id="a100b-109">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="a100b-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a100b-110">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="a100b-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="a100b-111">C\#</span><span class="sxs-lookup"><span data-stu-id="a100b-111">C\#</span></span>

<span data-ttu-id="a100b-112">Om du vill avbryta en program varu beställning</span><span class="sxs-lookup"><span data-stu-id="a100b-112">To cancel a software order,</span></span>

1. <span data-ttu-id="a100b-113">Skicka dina konto uppgifter till [**CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) -metoden för att hämta ett [**IPartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) -gränssnitt för att hämta partner åtgärder.</span><span class="sxs-lookup"><span data-stu-id="a100b-113">Pass your account credentials to the [**CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) method to get an [**IPartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) interface to get partner operations.</span></span>

2. <span data-ttu-id="a100b-114">Välj en viss [ordning](order-resources.md#order) som du vill avbryta.</span><span class="sxs-lookup"><span data-stu-id="a100b-114">Select a particular [Order](order-resources.md#order) you wish to cancel.</span></span> <span data-ttu-id="a100b-115">Anropa [**Customers. ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) -metoden med kund-ID, följt av **order. ById ()** med order-ID.</span><span class="sxs-lookup"><span data-stu-id="a100b-115">Call the [**Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier, followed by **Orders.ById()** with order identifier.</span></span>

3. <span data-ttu-id="a100b-116">Anropa **Get** -eller **GetAsync** -metoden för att hämta beställningen.</span><span class="sxs-lookup"><span data-stu-id="a100b-116">Call the **Get** or **GetAsync** method to retrieve the order.</span></span>

4. <span data-ttu-id="a100b-117">Ange egenskapen [**order. status**](order-resources.md#order) till `cancelled` .</span><span class="sxs-lookup"><span data-stu-id="a100b-117">Set the [**Order.Status**](order-resources.md#order) property to `cancelled`.</span></span>

5. <span data-ttu-id="a100b-118">Valfritt Om du vill ange vissa rad objekt som ska avbrytas anger du [**order. rad objekt**](order-resources.md#order) till en lista över rad objekt som du vill avbryta.</span><span class="sxs-lookup"><span data-stu-id="a100b-118">(Optional) If you want to specify certain line items for cancellation, set the [**Order.LineItems**](order-resources.md#order) to list of line items that you want to cancel.</span></span>

6. <span data-ttu-id="a100b-119">Använd metoden **patch ()** för att uppdatera ordningen.</span><span class="sxs-lookup"><span data-stu-id="a100b-119">Use the **Patch()** method to update the order.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="a100b-120">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="a100b-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a100b-121">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="a100b-121">Request syntax</span></span>

| <span data-ttu-id="a100b-122">Metod</span><span class="sxs-lookup"><span data-stu-id="a100b-122">Method</span></span>     | <span data-ttu-id="a100b-123">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="a100b-123">Request URI</span></span>                                                                            |
|------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="a100b-124">**9.0a**</span><span class="sxs-lookup"><span data-stu-id="a100b-124">**PATCH**</span></span> | <span data-ttu-id="a100b-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Orders/{order-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="a100b-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="a100b-126">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="a100b-126">URI parameters</span></span>

<span data-ttu-id="a100b-127">Använd följande frågeparametrar för att ta bort en kund.</span><span class="sxs-lookup"><span data-stu-id="a100b-127">Use the following query parameters to delete a customer.</span></span>

| <span data-ttu-id="a100b-128">Namn</span><span class="sxs-lookup"><span data-stu-id="a100b-128">Name</span></span>                   | <span data-ttu-id="a100b-129">Typ</span><span class="sxs-lookup"><span data-stu-id="a100b-129">Type</span></span>     | <span data-ttu-id="a100b-130">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="a100b-130">Required</span></span> | <span data-ttu-id="a100b-131">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="a100b-131">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a100b-132">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="a100b-132">**customer-tenant-id**</span></span> | <span data-ttu-id="a100b-133">**guid**</span><span class="sxs-lookup"><span data-stu-id="a100b-133">**guid**</span></span> | <span data-ttu-id="a100b-134">Y</span><span class="sxs-lookup"><span data-stu-id="a100b-134">Y</span></span>        | <span data-ttu-id="a100b-135">Värdet är ett GUID-formaterat kund klient-ID som gör det möjligt för åter försäljaren att filtrera resultaten för en specifik kund som tillhör åter försäljaren.</span><span class="sxs-lookup"><span data-stu-id="a100b-135">The value is a GUID formatted customer tenant identifier that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="a100b-136">**order-ID**</span><span class="sxs-lookup"><span data-stu-id="a100b-136">**order-id**</span></span> | <span data-ttu-id="a100b-137">**nollängd**</span><span class="sxs-lookup"><span data-stu-id="a100b-137">**string**</span></span> | <span data-ttu-id="a100b-138">Y</span><span class="sxs-lookup"><span data-stu-id="a100b-138">Y</span></span>        | <span data-ttu-id="a100b-139">Värdet är en sträng som anger identifieraren för den ordning som du vill avbryta.</span><span class="sxs-lookup"><span data-stu-id="a100b-139">The value is a string that denotes the identifier of the order that you want to cancel.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="a100b-140">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="a100b-140">Request headers</span></span>

<span data-ttu-id="a100b-141">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="a100b-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a100b-142">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="a100b-142">Request body</span></span>

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

### <a name="request-example"></a><span data-ttu-id="a100b-143">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="a100b-143">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="a100b-144">REST-svar</span><span class="sxs-lookup"><span data-stu-id="a100b-144">REST response</span></span>

<span data-ttu-id="a100b-145">Om det lyckas returnerar den här metoden ordningen med annullerade rad objekt.</span><span class="sxs-lookup"><span data-stu-id="a100b-145">If successful, this method returns the order with canceled line items.</span></span>

<span data-ttu-id="a100b-146">Order status markeras som antingen **avbruten** om alla rad objekt i ordern avbryts eller **slutförs** om inte alla rad objekt i ordern annulleras.</span><span class="sxs-lookup"><span data-stu-id="a100b-146">The order status will be marked as either **cancelled** if all the line items in the order are cancelled, or **completed** if not all line items in the order are canceled.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a100b-147">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="a100b-147">Response success and error codes</span></span>

<span data-ttu-id="a100b-148">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="a100b-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a100b-149">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="a100b-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a100b-150">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="a100b-150">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a100b-151">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="a100b-151">Response example</span></span>

<span data-ttu-id="a100b-152">I följande exempel svar kan du se att antalet rad objekt med erbjudande-ID: t **`DG7GMGF0FKZV:0003:DG7GMGF0DWMS`** har blivit noll (0).</span><span class="sxs-lookup"><span data-stu-id="a100b-152">In the following example response, you can see that the quantity of line item with the offer identifier **`DG7GMGF0FKZV:0003:DG7GMGF0DWMS`** has become zero (0).</span></span> <span data-ttu-id="a100b-153">Den här ändringen innebär att det rad objekt som har marker ATS för annullering har avbrutits.</span><span class="sxs-lookup"><span data-stu-id="a100b-153">This change means that the line item that was marked for cancellation has been canceled successfully.</span></span> <span data-ttu-id="a100b-154">Exempel ordningen innehåller andra rad objekt som inte avbrutits, vilket innebär att statusen för den övergripande ordningen markeras som **slutförd**, inte **avbruten**.</span><span class="sxs-lookup"><span data-stu-id="a100b-154">The example order contains other line items that weren't canceled, which means that the status of the overall order will be marked as **completed**, not **cancelled**.</span></span>

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
