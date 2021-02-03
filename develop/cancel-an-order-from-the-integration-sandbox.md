---
title: Annullera en order från sandbox-integration
description: 'Lär dig hur du använder API: er för partner Center för att avbryta olika typer av prenumerations order från högintegrations konton i sandbox.'
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 363bf209e27d5223259c8c533710a3b35bbef1e6
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/04/2020
ms.locfileid: "97770083"
---
# <a name="cancel-an-order-from-the-integration-sandbox-using-partner-center-apis"></a><span data-ttu-id="a0503-103">Avbryta en order från integration sandbox med API: er för partner Center</span><span class="sxs-lookup"><span data-stu-id="a0503-103">Cancel an order from the integration sandbox using Partner Center APIs</span></span>

<span data-ttu-id="a0503-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="a0503-104">**Applies to:**</span></span>

- <span data-ttu-id="a0503-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="a0503-105">Partner Center</span></span>
- <span data-ttu-id="a0503-106">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="a0503-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="a0503-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="a0503-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="a0503-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="a0503-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="a0503-109">I den här artikeln beskrivs hur du använder API: er för partner Center för att avbryta olika typer av prenumerations order från högintegrations konton.</span><span class="sxs-lookup"><span data-stu-id="a0503-109">This article describes how to use Partner Center APIs to cancel different types of subscription orders from integration sandbox accounts.</span></span> <span data-ttu-id="a0503-110">Sådana beställningar kan omfatta reserverade instanser, program vara och kommersiella Marketplace-program som en tjänst (SaaS) prenumerations order.</span><span class="sxs-lookup"><span data-stu-id="a0503-110">Such orders can include reserved instances, software, and commercial marketplace Software as a Service (SaaS) subscription orders.</span></span>

>[!NOTE]
><span data-ttu-id="a0503-111">Tänk på att annulleringen av reserverad instans eller prenumerations order för SaaS på kommersiella marknads platser endast är möjlig från integrations sand Box konton.</span><span class="sxs-lookup"><span data-stu-id="a0503-111">Please be aware that the cancellations of reserved instance, or commercial marketplace SaaS subscription orders are only possible from integration sandbox accounts.</span></span>  

<span data-ttu-id="a0503-112">Om du vill avbryta produktions order för program vara via API använder du [Cancel-Software-inköp](cancel-software-purchases.md).</span><span class="sxs-lookup"><span data-stu-id="a0503-112">To cancel production orders of software through API, use [cancel-software-purchases](cancel-software-purchases.md).</span></span>
<span data-ttu-id="a0503-113">Du kan också avbryta produktions order av program vara via instrument panelen genom att [avbryta ett köp](/partner-center/csp-software-subscriptions).</span><span class="sxs-lookup"><span data-stu-id="a0503-113">You can also cancel production orders of software through dashboard using [cancel a purchase](/partner-center/csp-software-subscriptions).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a0503-114">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="a0503-114">Prerequisites</span></span>

- <span data-ttu-id="a0503-115">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="a0503-115">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a0503-116">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="a0503-116">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="a0503-117">Ett partner konto för integration i begränsat läge med en kund som har aktiva prenumerations beställningar för reserverad instans/program vara/tredje part.</span><span class="sxs-lookup"><span data-stu-id="a0503-117">An integration sandbox partner account with a customer having active reserved instance / software / third-party SaaS subscription orders.</span></span>

## <a name="c"></a><span data-ttu-id="a0503-118">C\#</span><span class="sxs-lookup"><span data-stu-id="a0503-118">C\#</span></span>

<span data-ttu-id="a0503-119">Om du vill avbryta en beställning från sandbox-integration måste du skicka autentiseringsuppgifterna för ditt konto till- [**`CreatePartnerOperations`**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) metoden för att få ett [**`IPartner`**](/dotnet/api/microsoft.store.partnercenter.ipartner) gränssnitt för att få partner åtgärder.</span><span class="sxs-lookup"><span data-stu-id="a0503-119">To cancel an order from the integration sandbox, pass your account credentials to the [**`CreatePartnerOperations`**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) method to get an [**`IPartner`**](/dotnet/api/microsoft.store.partnercenter.ipartner) interface to get partner operations.</span></span>

<span data-ttu-id="a0503-120">Om du vill välja en viss [ordning](order-resources.md#order)använder du partner åtgärderna och anrops [**`Customers.ById()`**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metoden med kund-ID: n för att ange kunden, följt av **`Orders.ById()`** med order-ID för att ange ordningen och slutligen **`Get`** eller **`GetAsync`** metoden för att hämta den.</span><span class="sxs-lookup"><span data-stu-id="a0503-120">To select a particular [Order](order-resources.md#order), use the partner operations and call [**`Customers.ById()`**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to specify the customer, followed by **`Orders.ById()`** with order identifier to specify the order and finally **`Get`** or **`GetAsync`** method to retrieve it.</span></span>

<span data-ttu-id="a0503-121">Ange [**`Order.Status`**](order-resources.md#order) egenskapen till `cancelled` och Använd **`Patch()`** metoden för att uppdatera ordningen.</span><span class="sxs-lookup"><span data-stu-id="a0503-121">Set the [**`Order.Status`**](order-resources.md#order) property to `cancelled` and use the **`Patch()`** method to update the order.</span></span>

``` csharp
// IPartnerCredentials tipAccountCredentials;
// Customer tenant Id to be deleted.
// string customerTenantId;

IPartner tipAccountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(tipAccountCredentials);

// Cancel order
var order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Get();
order.Status = "cancelled";
order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Patch(order);

```

## <a name="rest-request"></a><span data-ttu-id="a0503-122">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="a0503-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a0503-123">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="a0503-123">Request syntax</span></span>

| <span data-ttu-id="a0503-124">Metod</span><span class="sxs-lookup"><span data-stu-id="a0503-124">Method</span></span>     | <span data-ttu-id="a0503-125">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="a0503-125">Request URI</span></span>                                                                            |
|------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="a0503-126">**9.0a**</span><span class="sxs-lookup"><span data-stu-id="a0503-126">**PATCH**</span></span> | <span data-ttu-id="a0503-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Orders/{order-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="a0503-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="a0503-128">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="a0503-128">URI parameter</span></span>

<span data-ttu-id="a0503-129">Använd följande frågeparameter för att ta bort en kund.</span><span class="sxs-lookup"><span data-stu-id="a0503-129">Use the following query parameter to delete a customer.</span></span>

| <span data-ttu-id="a0503-130">Namn</span><span class="sxs-lookup"><span data-stu-id="a0503-130">Name</span></span>                   | <span data-ttu-id="a0503-131">Typ</span><span class="sxs-lookup"><span data-stu-id="a0503-131">Type</span></span>     | <span data-ttu-id="a0503-132">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="a0503-132">Required</span></span> | <span data-ttu-id="a0503-133">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="a0503-133">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a0503-134">**kund-ID för klient organisation**</span><span class="sxs-lookup"><span data-stu-id="a0503-134">**customer-tenant-id**</span></span> | <span data-ttu-id="a0503-135">**guid**</span><span class="sxs-lookup"><span data-stu-id="a0503-135">**guid**</span></span> | <span data-ttu-id="a0503-136">Y</span><span class="sxs-lookup"><span data-stu-id="a0503-136">Y</span></span>        | <span data-ttu-id="a0503-137">Värdet är ett GUID-formaterat **kund-Tenant-ID** som gör det möjligt för åter försäljaren att filtrera resultaten för en specifik kund som tillhör åter försäljaren.</span><span class="sxs-lookup"><span data-stu-id="a0503-137">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="a0503-138">**order-ID**</span><span class="sxs-lookup"><span data-stu-id="a0503-138">**order-id**</span></span> | <span data-ttu-id="a0503-139">**nollängd**</span><span class="sxs-lookup"><span data-stu-id="a0503-139">**string**</span></span> | <span data-ttu-id="a0503-140">Y</span><span class="sxs-lookup"><span data-stu-id="a0503-140">Y</span></span>        | <span data-ttu-id="a0503-141">Värdet är en sträng som anger de order-ID: n som behöver avbrytas.</span><span class="sxs-lookup"><span data-stu-id="a0503-141">The value is a string denoting the order IDs that need to be canceled.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="a0503-142">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="a0503-142">Request headers</span></span>

<span data-ttu-id="a0503-143">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="a0503-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a0503-144">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="a0503-144">Request body</span></span>

```http
{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "status": "cancelled",
}
```

### <a name="request-example"></a><span data-ttu-id="a0503-145">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="a0503-145">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/orders/<order-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd

{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "status": "cancelled",
}
```

## <a name="rest-response"></a><span data-ttu-id="a0503-146">REST-svar</span><span class="sxs-lookup"><span data-stu-id="a0503-146">REST response</span></span>

<span data-ttu-id="a0503-147">Om det lyckas returnerar den här metoden den avbrutna ordningen.</span><span class="sxs-lookup"><span data-stu-id="a0503-147">If successful, this method returns the canceled order.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a0503-148">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="a0503-148">Response success and error codes</span></span>

<span data-ttu-id="a0503-149">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="a0503-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a0503-150">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="a0503-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a0503-151">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="a0503-151">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a0503-152">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="a0503-152">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 866
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "alternateId": "11fc4bdfd47a",
    "referenceCustomerId": "bd59b416-37f9-4d8f-8df3-5750111fc615",
    "billingCycle": "one_time",
    "currencyCode": "USD",
    "currencySymbol": "$",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0DWT0:0001:DG7GMGF0DSQR",
            "termDuration": "",
            "transactionType": "New",
            "friendlyName": "Microsoft Identity Manager 2016 - 1 User CAL",
            "quantity": 1,
            "links": {
                "product": {
                    "uri": "/products/DG7GMGF0DWT0?country=US",
                    "method": "GET",
                    "headers": []
                },
                "sku": {
                    "uri": "/products/DG7GMGF0DWT0/skus/0001?country=US",
                    "method": "GET",
                    "headers": []
                },
                "availability": {
                    "uri": "/products/DG7GMGF0DWT0/skus/0001/availabilities/DG7GMGF0DSQR?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2019-02-21T17:56:21.1335741Z",
    "status": "cancelled",
    "transactionType": "UserPurchase",
    "attributes": {
        "objectType": "Order"
    }
}
```
