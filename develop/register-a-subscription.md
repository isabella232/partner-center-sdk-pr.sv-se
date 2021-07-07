---
title: Registrera en prenumeration
description: Registrera en befintlig prenumeration så att den är aktiverad för att beställa Azure-reservationer.
ms.date: 07/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d26a7c77f60e6ef817cde80b9e97c88bd8bdc786
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446623"
---
# <a name="register-a-subscription"></a><span data-ttu-id="a8712-103">Registrera en prenumeration</span><span class="sxs-lookup"><span data-stu-id="a8712-103">Register a subscription</span></span>

<span data-ttu-id="a8712-104">Registrera en befintlig [prenumeration](subscription-resources.md) så att den är aktiverad för att beställa Azure-reservationer.</span><span class="sxs-lookup"><span data-stu-id="a8712-104">Register an existing [Subscription](subscription-resources.md) so that it is enabled for ordering Azure reservations.</span></span>

<span data-ttu-id="a8712-105">Om du vill köpa en Azure-reservation måste du ha minst en befintlig CSP Azure-prenumeration.</span><span class="sxs-lookup"><span data-stu-id="a8712-105">To purchase an Azure reservation, you must have at least one existing CSP Azure subscription.</span></span> <span data-ttu-id="a8712-106">Med den här metoden kan du registrera din befintliga CSP Azure-prenumeration, vilket gör det möjligt att köpa Azure-reservationer.</span><span class="sxs-lookup"><span data-stu-id="a8712-106">This method allows you to register your existing CSP Azure subscription, enabling it for purchasing Azure reservations.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a8712-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="a8712-107">Prerequisites</span></span>

- <span data-ttu-id="a8712-108">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="a8712-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a8712-109">Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="a8712-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="a8712-110">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a8712-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="a8712-111">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="a8712-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="a8712-112">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="a8712-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="a8712-113">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="a8712-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="a8712-114">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="a8712-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="a8712-115">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a8712-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="a8712-116">Ett prenumerations-ID.</span><span class="sxs-lookup"><span data-stu-id="a8712-116">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="a8712-117">C\#</span><span class="sxs-lookup"><span data-stu-id="a8712-117">C\#</span></span>

<span data-ttu-id="a8712-118">Om du vill registrera en kunds prenumeration hämtar du ett gränssnitt för prenumerationsåtgärder genom att anropa metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="a8712-118">To register a customer's subscription, retrieve an interface to subscription operations by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="a8712-119">Anropa sedan metoden [**Subscription.ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) med prenumerations-ID:t för att identifiera prenumerationen som du registrerar.</span><span class="sxs-lookup"><span data-stu-id="a8712-119">Then, call the [**Subscription.ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method with the subscription ID to identify the subscription that you are registering.</span></span>

<span data-ttu-id="a8712-120">Anropa slutligen metoden **Registration.Register()** för att registrera prenumerationen och hämta en URI som kan användas för att hämta prenumerationens registreringsstatus.</span><span class="sxs-lookup"><span data-stu-id="a8712-120">Finally, call the **Registration.Register()** method to register the subscription and retrieve a URI that can be used to get the subscription registration status.</span></span> <span data-ttu-id="a8712-121">Mer information finns i Hämta [prenumerationsregistreringsstatus](get-subscription-registration-status.md).</span><span class="sxs-lookup"><span data-stu-id="a8712-121">For more information, see [Get subscription registration status](get-subscription-registration-status.md).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve the subscription registration details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).Registration.Register();
```

## <a name="rest-request"></a><span data-ttu-id="a8712-122">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="a8712-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a8712-123">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="a8712-123">Request syntax</span></span>

| <span data-ttu-id="a8712-124">Metod</span><span class="sxs-lookup"><span data-stu-id="a8712-124">Method</span></span>    | <span data-ttu-id="a8712-125">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="a8712-125">Request URI</span></span>                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a8712-126">**Inlägg**</span><span class="sxs-lookup"><span data-stu-id="a8712-126">**POST**</span></span>  | <span data-ttu-id="a8712-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrations HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="a8712-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrations HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="a8712-128">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="a8712-128">URI parameters</span></span>

<span data-ttu-id="a8712-129">Använd följande sökvägsparametrar för att identifiera kunden och prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="a8712-129">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="a8712-130">Namn</span><span class="sxs-lookup"><span data-stu-id="a8712-130">Name</span></span>                    | <span data-ttu-id="a8712-131">Typ</span><span class="sxs-lookup"><span data-stu-id="a8712-131">Type</span></span>       | <span data-ttu-id="a8712-132">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="a8712-132">Required</span></span> | <span data-ttu-id="a8712-133">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="a8712-133">Description</span></span>                                                   |
|-------------------------|------------|----------|---------------------------------------------------------------|
| <span data-ttu-id="a8712-134">kund-ID</span><span class="sxs-lookup"><span data-stu-id="a8712-134">customer-id</span></span>             | <span data-ttu-id="a8712-135">sträng</span><span class="sxs-lookup"><span data-stu-id="a8712-135">string</span></span>     | <span data-ttu-id="a8712-136">Ja</span><span class="sxs-lookup"><span data-stu-id="a8712-136">Yes</span></span>      | <span data-ttu-id="a8712-137">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="a8712-137">A GUID formatted string that identifies the customer.</span></span>         |
| <span data-ttu-id="a8712-138">prenumerations-id</span><span class="sxs-lookup"><span data-stu-id="a8712-138">subscription-id</span></span>         | <span data-ttu-id="a8712-139">sträng</span><span class="sxs-lookup"><span data-stu-id="a8712-139">string</span></span>     | <span data-ttu-id="a8712-140">Ja</span><span class="sxs-lookup"><span data-stu-id="a8712-140">Yes</span></span>      | <span data-ttu-id="a8712-141">En GUID-formaterad sträng som identifierar prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="a8712-141">A GUID formatted string that identifies the subscription.</span></span>     |

### <a name="request-headers"></a><span data-ttu-id="a8712-142">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="a8712-142">Request headers</span></span>

<span data-ttu-id="a8712-143">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="a8712-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a8712-144">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="a8712-144">Request body</span></span>

<span data-ttu-id="a8712-145">Inga.</span><span class="sxs-lookup"><span data-stu-id="a8712-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="a8712-146">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="a8712-146">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/<customer-id>/subscriptions/<subscription-id>/registrations HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="a8712-147">REST-svar</span><span class="sxs-lookup"><span data-stu-id="a8712-147">REST response</span></span>

<span data-ttu-id="a8712-148">Om det lyckas innehåller svaret ett **Location-huvud** med en URI som kan användas för att hämta prenumerationens registreringsstatus.</span><span class="sxs-lookup"><span data-stu-id="a8712-148">If successful, the response contains a **Location** header with a URI that can be used to retrieve the subscription registration status.</span></span> <span data-ttu-id="a8712-149">Spara den här URI:en för användning med andra relaterade REST API:er.</span><span class="sxs-lookup"><span data-stu-id="a8712-149">Save this URI for use with other related REST APIs.</span></span> <span data-ttu-id="a8712-150">Ett exempel på hur du hämtar statusen finns i [Hämta prenumerationsregistreringsstatus](get-subscription-registration-status.md).</span><span class="sxs-lookup"><span data-stu-id="a8712-150">For an example of how to retrieve the status, see [Get subscription registration status](get-subscription-registration-status.md).</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a8712-151">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="a8712-151">Response success and error codes</span></span>

<span data-ttu-id="a8712-152">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="a8712-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a8712-153">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="a8712-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a8712-154">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="a8712-154">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a8712-155">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="a8712-155">Response example</span></span>

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/<customer-id>/subscriptions/<subscription-id>/registrationstatus
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
```
