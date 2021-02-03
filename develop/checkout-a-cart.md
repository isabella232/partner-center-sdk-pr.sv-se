---
title: Gå till kassan för en kundvagn
description: 'Lär dig mer om att ta en titt på en kund i en varukorg med API: er för partner Center. Du kan göra detta för att slutföra en kund order.'
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 094817a34cd29bc96788fcfb6a16610a8192d784
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/04/2020
ms.locfileid: "97770080"
---
# <a name="checkout-an-order-for-a-customer-in-a-cart"></a><span data-ttu-id="7a63a-104">Checka ut en order för en kund i en varukorg</span><span class="sxs-lookup"><span data-stu-id="7a63a-104">Checkout an order for a customer in a cart</span></span>

<span data-ttu-id="7a63a-105">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="7a63a-105">**Applies to:**</span></span>

- <span data-ttu-id="7a63a-106">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="7a63a-106">Partner Center</span></span>
- <span data-ttu-id="7a63a-107">Partner Center som drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="7a63a-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="7a63a-108">Partnercenter för Microsoft Cloud Tyskland</span><span class="sxs-lookup"><span data-stu-id="7a63a-108">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="7a63a-109">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="7a63a-109">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="7a63a-110">Så här checkar du ut en order för en kund i en kundvagn.</span><span class="sxs-lookup"><span data-stu-id="7a63a-110">How to checkout an order for a customer in a cart.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a63a-111">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="7a63a-111">Prerequisites</span></span>

- <span data-ttu-id="7a63a-112">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="7a63a-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7a63a-113">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="7a63a-113">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="7a63a-114">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7a63a-114">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="7a63a-115">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="7a63a-115">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="7a63a-116">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="7a63a-116">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="7a63a-117">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="7a63a-117">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="7a63a-118">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="7a63a-118">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="7a63a-119">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7a63a-119">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="7a63a-120">Ett kundvagn-ID för en befintlig varukorg.</span><span class="sxs-lookup"><span data-stu-id="7a63a-120">A Cart ID for an existing cart.</span></span>

## <a name="c"></a><span data-ttu-id="7a63a-121">C\#</span><span class="sxs-lookup"><span data-stu-id="7a63a-121">C\#</span></span>

<span data-ttu-id="7a63a-122">Om du vill checka ut en order för en kund får du en referens till vagnen med hjälp av varukorg och kund-ID.</span><span class="sxs-lookup"><span data-stu-id="7a63a-122">To checkout an order for a customer, get a reference to the cart using the cart and customer identifier.</span></span> <span data-ttu-id="7a63a-123">Slutligen kan du anropa **create** -eller **CreateAsync** -funktionerna för att slutföra beställningen.</span><span class="sxs-lookup"><span data-stu-id="7a63a-123">Finally, call the **Create** or **CreateAsync** functions to complete the order.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string cartId;

var cart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Checkout();
```

## <a name="java"></a><span data-ttu-id="7a63a-124">Java</span><span class="sxs-lookup"><span data-stu-id="7a63a-124">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](<../includes/java-sdk-support.md>)]

<span data-ttu-id="7a63a-125">Om du vill checka ut en order för en kund får du en referens till vagnen med hjälp av varukorg och kund-ID.</span><span class="sxs-lookup"><span data-stu-id="7a63a-125">To checkout an order for a customer, get a reference to the cart using the cart and customer identifier.</span></span> <span data-ttu-id="7a63a-126">Slutligen kan du anropa **create** -funktionen för att slutföra beställningen.</span><span class="sxs-lookup"><span data-stu-id="7a63a-126">Finally, call the **create** function to complete the order.</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String cartId;

Cart cart = partnerOperations.getCustomers().byId(customerId).getCart().byId(cartId).checkout();
```

## <a name="powershell"></a><span data-ttu-id="7a63a-127">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7a63a-127">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](<../includes/powershell-module-support.md>)]

<span data-ttu-id="7a63a-128">Om du vill checka in en order för en kund kan du köra [**Submit-PartnerCustomerCart**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Submit-PartnerCustomerCart.md) för att slutföra beställningen.</span><span class="sxs-lookup"><span data-stu-id="7a63a-128">To checkout an order for a customer, execute the [**Submit-PartnerCustomerCart**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Submit-PartnerCustomerCart.md) to complete the order.</span></span>

```powershell
# $customerId
# $cartId

Submit-PartnerCustomerCart -CartId $cartId -CustomerId $customerId
```

## <a name="rest-request"></a><span data-ttu-id="7a63a-129">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="7a63a-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7a63a-130">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="7a63a-130">Request syntax</span></span>

| <span data-ttu-id="7a63a-131">Metod</span><span class="sxs-lookup"><span data-stu-id="7a63a-131">Method</span></span>   | <span data-ttu-id="7a63a-132">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="7a63a-132">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7a63a-133">**EFTER**</span><span class="sxs-lookup"><span data-stu-id="7a63a-133">**POST**</span></span> | <span data-ttu-id="7a63a-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/carts/{Cart-ID}/Checkout http/1.1</span><span class="sxs-lookup"><span data-stu-id="7a63a-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts/{cart-id}/checkout HTTP/1.1</span></span>     |

### <a name="uri-parameters"></a><span data-ttu-id="7a63a-135">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="7a63a-135">URI parameters</span></span>

<span data-ttu-id="7a63a-136">Använd följande Sök vägs parametrar för att identifiera kunden och ange den varukorg som ska checkas ut.</span><span class="sxs-lookup"><span data-stu-id="7a63a-136">Use the following path parameters to identify the customer and specify the cart to be checked out.</span></span>

| <span data-ttu-id="7a63a-137">Namn</span><span class="sxs-lookup"><span data-stu-id="7a63a-137">Name</span></span>            | <span data-ttu-id="7a63a-138">Typ</span><span class="sxs-lookup"><span data-stu-id="7a63a-138">Type</span></span>     | <span data-ttu-id="7a63a-139">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="7a63a-139">Required</span></span> | <span data-ttu-id="7a63a-140">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="7a63a-140">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="7a63a-141">**kund-ID**</span><span class="sxs-lookup"><span data-stu-id="7a63a-141">**customer-id**</span></span> | <span data-ttu-id="7a63a-142">sträng</span><span class="sxs-lookup"><span data-stu-id="7a63a-142">string</span></span>   | <span data-ttu-id="7a63a-143">Yes</span><span class="sxs-lookup"><span data-stu-id="7a63a-143">Yes</span></span>      | <span data-ttu-id="7a63a-144">Ett GUID-formaterat kund-ID som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="7a63a-144">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="7a63a-145">**kundvagn-ID**</span><span class="sxs-lookup"><span data-stu-id="7a63a-145">**cart-id**</span></span>     | <span data-ttu-id="7a63a-146">sträng</span><span class="sxs-lookup"><span data-stu-id="7a63a-146">string</span></span>   | <span data-ttu-id="7a63a-147">Yes</span><span class="sxs-lookup"><span data-stu-id="7a63a-147">Yes</span></span>      | <span data-ttu-id="7a63a-148">Ett GUID-formaterat vagn-ID som identifierar vagnen.</span><span class="sxs-lookup"><span data-stu-id="7a63a-148">A GUID formatted cart-id that identifies the cart.</span></span>                     |

### <a name="request-headers"></a><span data-ttu-id="7a63a-149">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="7a63a-149">Request headers</span></span>

<span data-ttu-id="7a63a-150">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="7a63a-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7a63a-151">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="7a63a-151">Request body</span></span>

<span data-ttu-id="7a63a-152">Inga.</span><span class="sxs-lookup"><span data-stu-id="7a63a-152">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="7a63a-153">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="7a63a-153">Request example</span></span>

```http
POST /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts/b4c8fdea-cbe4-4d17-9576-13fcacbf9605/checkout HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 0
Expect: 100-continue

No-Content-Body
```

## <a name="rest-response"></a><span data-ttu-id="7a63a-154">REST-svar</span><span class="sxs-lookup"><span data-stu-id="7a63a-154">REST response</span></span>

<span data-ttu-id="7a63a-155">Om det lyckas innehåller svars texten den ifyllda [CartCheckoutResult](cart-resources.md#cartcheckoutresult) -resursen.</span><span class="sxs-lookup"><span data-stu-id="7a63a-155">If successful, the response body contains the populated [CartCheckoutResult](cart-resources.md#cartcheckoutresult) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7a63a-156">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="7a63a-156">Response success and error codes</span></span>

<span data-ttu-id="7a63a-157">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="7a63a-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7a63a-158">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="7a63a-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7a63a-159">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="7a63a-159">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="7a63a-160">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="7a63a-160">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 764
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
X-Locale: en-US,en-US
MS-CV: sF/wRa2ih0CzbABc.0
MS-ServerId: 000001
Date: Thu, 15 Mar 2018 17:15:01 GMT
?{
  "orders": [
    {
      "id": "3c6f2530-1e31-4088-8230-dd1c31a18bce",
      "alternateId": "3c6f2530-1e31-4088-8230-dd1c31a18bce",
      "referenceCustomerId": "28045616-f6b9-462f-9701-0d89b5e65c44",
      "billingCycle": "monthly",
      "currencyCode": "USD",
      "lineItems": [
        {
          "lineItemNumber": 0,
          "offerId": "MS-AZR-0145P",
          "subscriptionId": "EF2E1307-86E6-40E3-A794-872403FBD31C",
          "termDuration": "P1Y",
          "transactionType": "New",
          "friendlyName": "Microsoft Azure",
          "quantity": 1,
          "links": {...}
        }
      ],
      "creationDate": "2019-01-16T00:48:44.76+00:00",
      "status": "completed",
      "transactionType": "UserPurchase",
      "links": {...},
      ...
    },
    {
      "id": "311qiN8iFwkv-XARWMvXRYAwYKMACVqv1",
      "alternateId": "0a3624c6e47d",
      "referenceCustomerId": "28045616-f6b9-462f-9701-0d89b5e65c44",
      "billingCycle": "one_time",
      "currencyCode": "USD",
      "currencySymbol": "$",
      "lineItems": [
        {
          "lineItemNumber": 0,
          "offerId": "DZH318Z0BQ36:004G:DZH318Z08C0S",
          "termDuration": "P1Y",
          "transactionType": "New",
          "friendlyName": "Reserved VM Instance, Standard_NV12, US East 2, 1 Year",
          "quantity": 1,
          "links": {...}
        },
        {
          "lineItemNumber": 1,
          "offerId": "DZH318Z0BQ36:004J:DZH318Z08B8X",
          "termDuration": "P3Y",
          "transactionType": "New",
          "friendlyName": "Reserved VM Instance, Standard_NV12, US East 2, 3 Years",
          "quantity": 1,
          "links": {...}
        },
        {
          "lineItemNumber": 2,
          "offerId": "DG7GMGF0DWM3:0002:DG7GMGF0DT1M",
          "transactionType": "New",
          "friendlyName": "BizTalk Server 2016 Branch",
          "quantity": 1,
          "links": {...}
        }
      ],
      "creationDate": "2019-01-16T00:48:51.6578126Z",
      "status": "pending",
      "transactionType": "UserPurchase",
      "links": {...},
      ...
    },
    {
      "id": "HVu_cO8Ea7fNRQP4ia1QTpZap-kg_7P71",
      "alternateId": "55a4e6854d54",
      "referenceCustomerId": "28045616-f6b9-462f-9701-0d89b5e65c44",
      "billingCycle": "monthly",
      "currencyCode": "USD",
      "currencySymbol": "$",
      "lineItems": [
        {
          "lineItemNumber": 0,
          "offerId": "DZH318Z0BXWC:0002:DZH318Z0BMRV",
          "termDuration": "P1M",
          "transactionType": "New",
          "friendlyName": "Barracuda WaaS - Medium Plan",
          "quantity": 1,
          "links": {...}
        }
      ],
      "creationDate": "2019-01-16T00:48:44.4514129Z",
      "status": "pending",
      "transactionType": "UserPurchase",
      "links": {...},
      ...
    }
  ],
  ...
}
```
