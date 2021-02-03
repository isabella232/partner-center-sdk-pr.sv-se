---
title: Registrera en prenumeration
description: Registrera en befintlig prenumeration så att den är aktive rad för att beställa Azure-reservationer.
ms.date: 07/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9a96bb350f22430c9fd7a1759e336cc9f3ca1939
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769651"
---
# <a name="register-a-subscription"></a><span data-ttu-id="cffc9-103">Registrera en prenumeration</span><span class="sxs-lookup"><span data-stu-id="cffc9-103">Register a subscription</span></span>

<span data-ttu-id="cffc9-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="cffc9-104">**Applies To**</span></span>

- <span data-ttu-id="cffc9-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="cffc9-105">Partner Center</span></span>

<span data-ttu-id="cffc9-106">Registrera en befintlig [prenumeration](subscription-resources.md) så att den är aktive rad för att beställa Azure-reservationer.</span><span class="sxs-lookup"><span data-stu-id="cffc9-106">Register an existing [Subscription](subscription-resources.md) so that it is enabled for ordering Azure reservations.</span></span>

<span data-ttu-id="cffc9-107">Om du vill köpa en Azure-reservation måste du ha minst en befintlig CSP Azure-prenumeration.</span><span class="sxs-lookup"><span data-stu-id="cffc9-107">To purchase an Azure reservation you must have at least one existing CSP Azure subscription.</span></span> <span data-ttu-id="cffc9-108">Med den här metoden kan du registrera din befintliga CSP Azure-prenumeration, så att den kan köpa Azure-reservationer.</span><span class="sxs-lookup"><span data-stu-id="cffc9-108">This method allows you to register your existing CSP Azure subscription, enabling it for purchasing Azure reservations.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cffc9-109">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="cffc9-109">Prerequisites</span></span>

- <span data-ttu-id="cffc9-110">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="cffc9-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="cffc9-111">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="cffc9-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="cffc9-112">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="cffc9-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="cffc9-113">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="cffc9-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="cffc9-114">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="cffc9-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="cffc9-115">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="cffc9-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="cffc9-116">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="cffc9-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="cffc9-117">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="cffc9-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="cffc9-118">Ett prenumerations-ID.</span><span class="sxs-lookup"><span data-stu-id="cffc9-118">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="cffc9-119">C\#</span><span class="sxs-lookup"><span data-stu-id="cffc9-119">C\#</span></span>

<span data-ttu-id="cffc9-120">Om du vill registrera en kunds prenumeration hämtar du ett gränssnitt för prenumerations åtgärder genom att anropa metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="cffc9-120">To register a customer's subscription, retrieve an interface to subscription operations by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="cffc9-121">Anropa sedan metoden [**Subscription. ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) med prenumerations-ID: t för att identifiera den prenumeration som du registrerar.</span><span class="sxs-lookup"><span data-stu-id="cffc9-121">Then, call the [**Subscription.ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method with the subscription ID to identify the subscription that you are registering.</span></span>

<span data-ttu-id="cffc9-122">Anropa slutligen metoden **Registration. register ()** för att registrera prenumerationen och hämta en URI som kan användas för att hämta status för prenumerations registrering.</span><span class="sxs-lookup"><span data-stu-id="cffc9-122">Finally, call the **Registration.Register()** method to register the subscription and retrieve a URI that can be used to get the subscription registration status.</span></span> <span data-ttu-id="cffc9-123">Mer information finns i [Hämta status för prenumerations registrering](get-subscription-registration-status.md).</span><span class="sxs-lookup"><span data-stu-id="cffc9-123">For more information, see [Get subscription registration status](get-subscription-registration-status.md).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve the subscription registration details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).Registration.Register();
```

## <a name="rest-request"></a><span data-ttu-id="cffc9-124">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="cffc9-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="cffc9-125">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="cffc9-125">Request syntax</span></span>

| <span data-ttu-id="cffc9-126">Metod</span><span class="sxs-lookup"><span data-stu-id="cffc9-126">Method</span></span>    | <span data-ttu-id="cffc9-127">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="cffc9-127">Request URI</span></span>                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="cffc9-128">**EFTER**</span><span class="sxs-lookup"><span data-stu-id="cffc9-128">**POST**</span></span>  | <span data-ttu-id="cffc9-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Subscriptions/{Subscription-ID}/registrations http/1.1</span><span class="sxs-lookup"><span data-stu-id="cffc9-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrations HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="cffc9-130">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="cffc9-130">URI parameters</span></span>

<span data-ttu-id="cffc9-131">Använd följande Sök vägs parametrar för att identifiera kunden och prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="cffc9-131">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="cffc9-132">Namn</span><span class="sxs-lookup"><span data-stu-id="cffc9-132">Name</span></span>                    | <span data-ttu-id="cffc9-133">Typ</span><span class="sxs-lookup"><span data-stu-id="cffc9-133">Type</span></span>       | <span data-ttu-id="cffc9-134">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="cffc9-134">Required</span></span> | <span data-ttu-id="cffc9-135">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="cffc9-135">Description</span></span>                                                   |
|-------------------------|------------|----------|---------------------------------------------------------------|
| <span data-ttu-id="cffc9-136">kund-ID</span><span class="sxs-lookup"><span data-stu-id="cffc9-136">customer-id</span></span>             | <span data-ttu-id="cffc9-137">sträng</span><span class="sxs-lookup"><span data-stu-id="cffc9-137">string</span></span>     | <span data-ttu-id="cffc9-138">Yes</span><span class="sxs-lookup"><span data-stu-id="cffc9-138">Yes</span></span>      | <span data-ttu-id="cffc9-139">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="cffc9-139">A GUID formatted string that identifies the customer.</span></span>         |
| <span data-ttu-id="cffc9-140">prenumerations-ID</span><span class="sxs-lookup"><span data-stu-id="cffc9-140">subscription-id</span></span>         | <span data-ttu-id="cffc9-141">sträng</span><span class="sxs-lookup"><span data-stu-id="cffc9-141">string</span></span>     | <span data-ttu-id="cffc9-142">Yes</span><span class="sxs-lookup"><span data-stu-id="cffc9-142">Yes</span></span>      | <span data-ttu-id="cffc9-143">En GUID-formaterad sträng som identifierar prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="cffc9-143">A GUID formatted string that identifies the subscription.</span></span>     |

### <a name="request-headers"></a><span data-ttu-id="cffc9-144">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="cffc9-144">Request headers</span></span>

<span data-ttu-id="cffc9-145">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="cffc9-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="cffc9-146">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="cffc9-146">Request body</span></span>

<span data-ttu-id="cffc9-147">Inga.</span><span class="sxs-lookup"><span data-stu-id="cffc9-147">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="cffc9-148">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="cffc9-148">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="cffc9-149">REST-svar</span><span class="sxs-lookup"><span data-stu-id="cffc9-149">REST response</span></span>

<span data-ttu-id="cffc9-150">Om det lyckas innehåller svaret ett **plats** huvud med en URI som kan användas för att hämta status för prenumerations registrering.</span><span class="sxs-lookup"><span data-stu-id="cffc9-150">If successful, the response contains a **Location** header with a URI that can be used to retrieve the subscription registration status.</span></span> <span data-ttu-id="cffc9-151">Spara denna URI för användning med andra relaterade REST API: er.</span><span class="sxs-lookup"><span data-stu-id="cffc9-151">Save this URI for use with other related REST APIs.</span></span> <span data-ttu-id="cffc9-152">Ett exempel på hur du hämtar status finns i [Hämta status för prenumerations registrering](get-subscription-registration-status.md).</span><span class="sxs-lookup"><span data-stu-id="cffc9-152">For an example of how to retrieve the status, see [Get subscription registration status](get-subscription-registration-status.md).</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="cffc9-153">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="cffc9-153">Response success and error codes</span></span>

<span data-ttu-id="cffc9-154">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="cffc9-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="cffc9-155">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="cffc9-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="cffc9-156">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="cffc9-156">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="cffc9-157">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="cffc9-157">Response example</span></span>

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/<customer-id>/subscriptions/<subscription-id>/registrationstatus
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
```
