---
title: Avbryta en beställning från sandbox-miljön för integrering
description: Lär dig hur du använder Partner Center-API:er för att avbryta olika typer av prenumerationsbeställningar från integrations-sandbox-konton.
ms.date: 04/28/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c3bf862c62804a56e6f73dd3ec36d2e9eb65f997
ms.sourcegitcommit: f59a9311c8a37d45695caf74794ec1697426acc9
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/29/2021
ms.locfileid: "108210027"
---
# <a name="cancel-an-order-from-the-integration-sandbox-using-partner-center-apis"></a><span data-ttu-id="b4701-103">Avbryta en beställning från sandbox-miljön för integrering med partnercenter-API:er</span><span class="sxs-lookup"><span data-stu-id="b4701-103">Cancel an order from the integration sandbox using Partner Center APIs</span></span>

<span data-ttu-id="b4701-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="b4701-104">**Applies to:**</span></span>

- <span data-ttu-id="b4701-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="b4701-105">Partner Center</span></span>
- <span data-ttu-id="b4701-106">Partnercenter drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="b4701-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="b4701-107">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="b4701-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="b4701-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="b4701-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="b4701-109">I den här artikeln beskrivs hur du använder Partner Center-API:er för att avbryta olika typer av prenumerationsbeställningar från integrations-sandbox-konton.</span><span class="sxs-lookup"><span data-stu-id="b4701-109">This article describes how to use Partner Center APIs to cancel different types of subscription orders from integration sandbox accounts.</span></span> <span data-ttu-id="b4701-110">Sådana beställningar kan omfatta reserverade instanser, programvara och saaS-prenumerationsbeställningar (Software as a Service) på den kommersiella marknadsplatsen.</span><span class="sxs-lookup"><span data-stu-id="b4701-110">Such orders can include reserved instances, software, and commercial marketplace Software as a Service (SaaS) subscription orders.</span></span>

>[!NOTE] 
><span data-ttu-id="b4701-111">Observera att annulleringar av reserverade instanser eller SaaS-prenumerationsbeställningar på den kommersiella marknadsplatsen endast är möjliga från integrations-sandbox-konton.</span><span class="sxs-lookup"><span data-stu-id="b4701-111">Please be aware that the cancellations of reserved instance, or commercial marketplace SaaS subscription orders are only possible from integration sandbox accounts.</span></span> <span data-ttu-id="b4701-112">Sandbox-beställningar som är äldre än 60 dagar kan inte annulleras från Partnercenter.</span><span class="sxs-lookup"><span data-stu-id="b4701-112">Any sandbox orders which are older than 60 days cannot be cancelled from Partner Center.</span></span> <span data-ttu-id="b4701-113">Kontakta Partnercenter-supporten om du behöver hjälp.</span><span class="sxs-lookup"><span data-stu-id="b4701-113">If you need assistance, reach out to Partner Center Support.</span></span> 

<span data-ttu-id="b4701-114">Om du vill avbryta produktionsorder för programvara via API använder [du cancel-software-purchases](cancel-software-purchases.md).</span><span class="sxs-lookup"><span data-stu-id="b4701-114">To cancel production orders of software through API, use [cancel-software-purchases](cancel-software-purchases.md).</span></span>
<span data-ttu-id="b4701-115">Du kan också avbryta produktionsorder för programvara via instrumentpanelen med [hjälp av avbryta ett köp.](/partner-center/csp-software-subscriptions)</span><span class="sxs-lookup"><span data-stu-id="b4701-115">You can also cancel production orders of software through dashboard using [cancel a purchase](/partner-center/csp-software-subscriptions).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b4701-116">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="b4701-116">Prerequisites</span></span>

- <span data-ttu-id="b4701-117">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b4701-117">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b4701-118">Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="b4701-118">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="b4701-119">Ett partnerkonto för sandbox-integrering med en kund som har aktiv reserverad instans/programvara/SaaS-prenumerationsbeställningar från tredje part.</span><span class="sxs-lookup"><span data-stu-id="b4701-119">An integration sandbox partner account with a customer having active reserved instance / software / third-party SaaS subscription orders.</span></span>

## <a name="c"></a><span data-ttu-id="b4701-120">C\#</span><span class="sxs-lookup"><span data-stu-id="b4701-120">C\#</span></span>

<span data-ttu-id="b4701-121">Om du vill avbryta en beställning från sandbox-miljön för integrering skickar du autentiseringsuppgifterna för ditt konto till metoden [**`CreatePartnerOperations`**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) för att hämta ett gränssnitt för att hämta [**`IPartner`**](/dotnet/api/microsoft.store.partnercenter.ipartner) partneråtgärder.</span><span class="sxs-lookup"><span data-stu-id="b4701-121">To cancel an order from the integration sandbox, pass your account credentials to the [**`CreatePartnerOperations`**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) method to get an [**`IPartner`**](/dotnet/api/microsoft.store.partnercenter.ipartner) interface to get partner operations.</span></span>

<span data-ttu-id="b4701-122">Om du [](order-resources.md#order)vill välja en viss order använder du partneråtgärderna och anropsmetoden med kund-ID:t för att ange kunden, följt av med orderidentifierare för att ange ordern och slutligen metoden eller metoden för [**`Customers.ById()`**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) att hämta **`Orders.ById()`** **`Get`** **`GetAsync`** den.</span><span class="sxs-lookup"><span data-stu-id="b4701-122">To select a particular [Order](order-resources.md#order), use the partner operations and call [**`Customers.ById()`**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to specify the customer, followed by **`Orders.ById()`** with order identifier to specify the order and finally **`Get`** or **`GetAsync`** method to retrieve it.</span></span>

<span data-ttu-id="b4701-123">Ange egenskapen [**`Order.Status`**](order-resources.md#order) till och använd metoden för att uppdatera `cancelled` **`Patch()`** ordern.</span><span class="sxs-lookup"><span data-stu-id="b4701-123">Set the [**`Order.Status`**](order-resources.md#order) property to `cancelled` and use the **`Patch()`** method to update the order.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="b4701-124">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="b4701-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b4701-125">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="b4701-125">Request syntax</span></span>

| <span data-ttu-id="b4701-126">Metod</span><span class="sxs-lookup"><span data-stu-id="b4701-126">Method</span></span>     | <span data-ttu-id="b4701-127">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="b4701-127">Request URI</span></span>                                                                            |
|------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="b4701-128">**Patch**</span><span class="sxs-lookup"><span data-stu-id="b4701-128">**PATCH**</span></span> | <span data-ttu-id="b4701-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="b4701-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="b4701-130">URI-parameter</span><span class="sxs-lookup"><span data-stu-id="b4701-130">URI parameter</span></span>

<span data-ttu-id="b4701-131">Använd följande frågeparameter för att ta bort en kund.</span><span class="sxs-lookup"><span data-stu-id="b4701-131">Use the following query parameter to delete a customer.</span></span>

| <span data-ttu-id="b4701-132">Namn</span><span class="sxs-lookup"><span data-stu-id="b4701-132">Name</span></span>                   | <span data-ttu-id="b4701-133">Typ</span><span class="sxs-lookup"><span data-stu-id="b4701-133">Type</span></span>     | <span data-ttu-id="b4701-134">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="b4701-134">Required</span></span> | <span data-ttu-id="b4701-135">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="b4701-135">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b4701-136">**kund-klient-id**</span><span class="sxs-lookup"><span data-stu-id="b4701-136">**customer-tenant-id**</span></span> | <span data-ttu-id="b4701-137">**guid**</span><span class="sxs-lookup"><span data-stu-id="b4701-137">**guid**</span></span> | <span data-ttu-id="b4701-138">Y</span><span class="sxs-lookup"><span data-stu-id="b4701-138">Y</span></span>        | <span data-ttu-id="b4701-139">Värdet är ett GUID-formaterat **kundklient-ID** som gör att återförsäljaren kan filtrera resultaten för en viss kund som tillhör återförsäljaren.</span><span class="sxs-lookup"><span data-stu-id="b4701-139">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="b4701-140">**order-id**</span><span class="sxs-lookup"><span data-stu-id="b4701-140">**order-id**</span></span> | <span data-ttu-id="b4701-141">**sträng**</span><span class="sxs-lookup"><span data-stu-id="b4701-141">**string**</span></span> | <span data-ttu-id="b4701-142">Y</span><span class="sxs-lookup"><span data-stu-id="b4701-142">Y</span></span>        | <span data-ttu-id="b4701-143">Värdet är en sträng som anger de order-ID:er som måste avbrytas.</span><span class="sxs-lookup"><span data-stu-id="b4701-143">The value is a string denoting the order IDs that need to be canceled.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b4701-144">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="b4701-144">Request headers</span></span>

<span data-ttu-id="b4701-145">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="b4701-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b4701-146">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="b4701-146">Request body</span></span>

```http
{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "status": "cancelled",
}
```

### <a name="request-example"></a><span data-ttu-id="b4701-147">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="b4701-147">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="b4701-148">REST-svar</span><span class="sxs-lookup"><span data-stu-id="b4701-148">REST response</span></span>

<span data-ttu-id="b4701-149">Om det lyckas returnerar den här metoden den annullerade ordern.</span><span class="sxs-lookup"><span data-stu-id="b4701-149">If successful, this method returns the canceled order.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b4701-150">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="b4701-150">Response success and error codes</span></span>

<span data-ttu-id="b4701-151">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="b4701-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b4701-152">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="b4701-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b4701-153">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="b4701-153">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b4701-154">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="b4701-154">Response example</span></span>

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
