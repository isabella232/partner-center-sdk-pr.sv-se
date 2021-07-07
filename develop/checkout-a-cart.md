---
title: Gå till kassan för en kundvagn
description: Lär dig hur du checkar ut en order för en kund i kundvagn med hjälp av Partner Center-API:er. Du kan göra detta för att slutföra en kundbeställning.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9ee06797602b22a1f8257c94880a2d81e2280f2e
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974054"
---
# <a name="checkout-an-order-for-a-customer-in-a-cart"></a><span data-ttu-id="31a1e-104">Checka ut en order för en kund i en kundvagn</span><span class="sxs-lookup"><span data-stu-id="31a1e-104">Checkout an order for a customer in a cart</span></span>

<span data-ttu-id="31a1e-105">**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="31a1e-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="31a1e-106">Så här checkar du ut en order för en kund i en kundvagn.</span><span class="sxs-lookup"><span data-stu-id="31a1e-106">How to checkout an order for a customer in a cart.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31a1e-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="31a1e-107">Prerequisites</span></span>

- <span data-ttu-id="31a1e-108">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="31a1e-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="31a1e-109">Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="31a1e-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="31a1e-110">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="31a1e-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="31a1e-111">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="31a1e-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="31a1e-112">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="31a1e-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="31a1e-113">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="31a1e-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="31a1e-114">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="31a1e-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="31a1e-115">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="31a1e-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="31a1e-116">Ett kundvagns-ID för en befintlig kundvagn.</span><span class="sxs-lookup"><span data-stu-id="31a1e-116">A Cart ID for an existing cart.</span></span>

## <a name="c"></a><span data-ttu-id="31a1e-117">C\#</span><span class="sxs-lookup"><span data-stu-id="31a1e-117">C\#</span></span>

<span data-ttu-id="31a1e-118">Om du vill checka ut en order för en kund hämtar du en referens till kundvagnen med hjälp av kundvagnen och kundidentifieraren.</span><span class="sxs-lookup"><span data-stu-id="31a1e-118">To checkout an order for a customer, get a reference to the cart using the cart and customer identifier.</span></span> <span data-ttu-id="31a1e-119">Anropa slutligen funktionerna **Create** eller **CreateAsync** för att slutföra beställningen.</span><span class="sxs-lookup"><span data-stu-id="31a1e-119">Finally, call the **Create** or **CreateAsync** functions to complete the order.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string cartId;

var cart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Checkout();
```

## <a name="java"></a><span data-ttu-id="31a1e-120">Java</span><span class="sxs-lookup"><span data-stu-id="31a1e-120">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](<../includes/java-sdk-support.md>)]

<span data-ttu-id="31a1e-121">Om du vill checka ut en order för en kund hämtar du en referens till kundvagnen med hjälp av kundvagnen och kundidentifieraren.</span><span class="sxs-lookup"><span data-stu-id="31a1e-121">To checkout an order for a customer, get a reference to the cart using the cart and customer identifier.</span></span> <span data-ttu-id="31a1e-122">Anropa slutligen **create-funktionen** för att slutföra ordern.</span><span class="sxs-lookup"><span data-stu-id="31a1e-122">Finally, call the **create** function to complete the order.</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String cartId;

Cart cart = partnerOperations.getCustomers().byId(customerId).getCart().byId(cartId).checkout();
```

## <a name="powershell"></a><span data-ttu-id="31a1e-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="31a1e-123">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](<../includes/powershell-module-support.md>)]

<span data-ttu-id="31a1e-124">Om du vill checka ut en order för en kund kör [**du Submit-PartnerCustomerCart**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Submit-PartnerCustomerCart.md) för att slutföra beställningen.</span><span class="sxs-lookup"><span data-stu-id="31a1e-124">To checkout an order for a customer, execute the [**Submit-PartnerCustomerCart**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Submit-PartnerCustomerCart.md) to complete the order.</span></span>

```powershell
# $customerId
# $cartId

Submit-PartnerCustomerCart -CartId $cartId -CustomerId $customerId
```

## <a name="rest-request"></a><span data-ttu-id="31a1e-125">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="31a1e-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="31a1e-126">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="31a1e-126">Request syntax</span></span>

| <span data-ttu-id="31a1e-127">Metod</span><span class="sxs-lookup"><span data-stu-id="31a1e-127">Method</span></span>   | <span data-ttu-id="31a1e-128">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="31a1e-128">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="31a1e-129">**Inlägg**</span><span class="sxs-lookup"><span data-stu-id="31a1e-129">**POST**</span></span> | <span data-ttu-id="31a1e-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts/{cart-id}/checkout HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="31a1e-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts/{cart-id}/checkout HTTP/1.1</span></span>     |

### <a name="uri-parameters"></a><span data-ttu-id="31a1e-131">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="31a1e-131">URI parameters</span></span>

<span data-ttu-id="31a1e-132">Använd följande sökvägsparametrar för att identifiera kunden och ange vilken kundvagn som ska checkas ut.</span><span class="sxs-lookup"><span data-stu-id="31a1e-132">Use the following path parameters to identify the customer and specify the cart to be checked out.</span></span>

| <span data-ttu-id="31a1e-133">Namn</span><span class="sxs-lookup"><span data-stu-id="31a1e-133">Name</span></span>            | <span data-ttu-id="31a1e-134">Typ</span><span class="sxs-lookup"><span data-stu-id="31a1e-134">Type</span></span>     | <span data-ttu-id="31a1e-135">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="31a1e-135">Required</span></span> | <span data-ttu-id="31a1e-136">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="31a1e-136">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="31a1e-137">**kund-ID**</span><span class="sxs-lookup"><span data-stu-id="31a1e-137">**customer-id**</span></span> | <span data-ttu-id="31a1e-138">sträng</span><span class="sxs-lookup"><span data-stu-id="31a1e-138">string</span></span>   | <span data-ttu-id="31a1e-139">Ja</span><span class="sxs-lookup"><span data-stu-id="31a1e-139">Yes</span></span>      | <span data-ttu-id="31a1e-140">Ett GUID-formaterat kund-ID som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="31a1e-140">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="31a1e-141">**cart-id**</span><span class="sxs-lookup"><span data-stu-id="31a1e-141">**cart-id**</span></span>     | <span data-ttu-id="31a1e-142">sträng</span><span class="sxs-lookup"><span data-stu-id="31a1e-142">string</span></span>   | <span data-ttu-id="31a1e-143">Ja</span><span class="sxs-lookup"><span data-stu-id="31a1e-143">Yes</span></span>      | <span data-ttu-id="31a1e-144">Ett GUID-formaterat kundvagns-ID som identifierar kundvagnen.</span><span class="sxs-lookup"><span data-stu-id="31a1e-144">A GUID formatted cart-id that identifies the cart.</span></span>                     |

### <a name="request-headers"></a><span data-ttu-id="31a1e-145">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="31a1e-145">Request headers</span></span>

<span data-ttu-id="31a1e-146">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="31a1e-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="31a1e-147">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="31a1e-147">Request body</span></span>

<span data-ttu-id="31a1e-148">Inga.</span><span class="sxs-lookup"><span data-stu-id="31a1e-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="31a1e-149">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="31a1e-149">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="31a1e-150">REST-svar</span><span class="sxs-lookup"><span data-stu-id="31a1e-150">REST response</span></span>

<span data-ttu-id="31a1e-151">Om det lyckas innehåller svarstexten den ifyllda [resursen CartCheckoutResult.](cart-resources.md#cartcheckoutresult)</span><span class="sxs-lookup"><span data-stu-id="31a1e-151">If successful, the response body contains the populated [CartCheckoutResult](cart-resources.md#cartcheckoutresult) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="31a1e-152">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="31a1e-152">Response success and error codes</span></span>

<span data-ttu-id="31a1e-153">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="31a1e-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="31a1e-154">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="31a1e-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="31a1e-155">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="31a1e-155">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="31a1e-156">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="31a1e-156">Response example</span></span>

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
