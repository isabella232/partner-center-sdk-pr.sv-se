---
title: Hämta status för prenumerationsregistrering
description: Hämta status för en prenumeration som har registrerats för användning med Azure Reserved VM Instances.
ms.date: 03/19/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9e39f94c0eac402a0be3afde84279aa637868f96
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445960"
---
# <a name="get-subscription-registration-status"></a><span data-ttu-id="b07fd-103">Hämta status för prenumerationsregistrering</span><span class="sxs-lookup"><span data-stu-id="b07fd-103">Get subscription registration status</span></span>

<span data-ttu-id="b07fd-104">Så här hämtar du prenumerationsregistreringsstatus för en kundprenumeration som har aktiverats för Azure Reserved VM Instances.</span><span class="sxs-lookup"><span data-stu-id="b07fd-104">How to get the subscription registration status for a customer subscription that has been enabled for purchasing Azure Reserved VM Instances.</span></span>

<span data-ttu-id="b07fd-105">Om du vill köpa en azure-reserverad VM-instans med partnercenter-API:et måste du ha minst en befintlig CSP Azure-prenumeration.</span><span class="sxs-lookup"><span data-stu-id="b07fd-105">To purchase an Azure Reserved VM Instance using the Partner Center API, you must have at least one existing CSP Azure subscription.</span></span> <span data-ttu-id="b07fd-106">Med [metoden Registrera en](register-a-subscription.md) prenumeration kan du registrera din befintliga CSP Azure-prenumeration, vilket gör det möjligt att köpa Azure Reserved VM Instances.</span><span class="sxs-lookup"><span data-stu-id="b07fd-106">The [Register a subscription](register-a-subscription.md) method allows you to register your existing CSP Azure subscription, enabling it for purchasing Azure Reserved VM Instances.</span></span> <span data-ttu-id="b07fd-107">Med den här metoden kan du hämta status för registreringen.</span><span class="sxs-lookup"><span data-stu-id="b07fd-107">This method allows you to retrieve the status of that registration.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b07fd-108">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="b07fd-108">Prerequisites</span></span>

- <span data-ttu-id="b07fd-109">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b07fd-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b07fd-110">Det här scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="b07fd-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="b07fd-111">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b07fd-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="b07fd-112">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="b07fd-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="b07fd-113">Välj **CSP** på Menyn i Partnercenter följt av **Kunder**.</span><span class="sxs-lookup"><span data-stu-id="b07fd-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="b07fd-114">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="b07fd-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="b07fd-115">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="b07fd-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="b07fd-116">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b07fd-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="b07fd-117">Ett prenumerations-ID.</span><span class="sxs-lookup"><span data-stu-id="b07fd-117">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="b07fd-118">C\#</span><span class="sxs-lookup"><span data-stu-id="b07fd-118">C\#</span></span>

<span data-ttu-id="b07fd-119">Om du vill hämta registreringsstatusen för en prenumeration börjar du med att använda metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="b07fd-119">To get the registration status of a subscription, begin by using the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="b07fd-120">Hämta sedan ett gränssnitt för prenumerationsåtgärder genom att anropa [**metoden Subscription.ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) med prenumerations-ID:t för att identifiera prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="b07fd-120">Then, get an interface to subscription operations by calling the [**Subscription.ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method with the subscription ID to identify the subscription.</span></span> <span data-ttu-id="b07fd-121">Använd sedan egenskapen RegistrationStatus för att hämta ett gränssnitt för den aktuella prenumerationens registreringsstatusåtgärder och anropa metoden **Get** eller **GetAsync** för att hämta **objektet SubscriptionRegistrationStatus.**</span><span class="sxs-lookup"><span data-stu-id="b07fd-121">Next, use the RegistrationStatus property to obtain an interface to the current subscription's registration status operations, and call the **Get** or **GetAsync** method to retrieve the **SubscriptionRegistrationStatus** object.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve a subscription's registration status details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).RegistrationStatus.Get();
```

## <a name="rest-request"></a><span data-ttu-id="b07fd-122">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="b07fd-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b07fd-123">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="b07fd-123">Request syntax</span></span>

| <span data-ttu-id="b07fd-124">Metod</span><span class="sxs-lookup"><span data-stu-id="b07fd-124">Method</span></span>    | <span data-ttu-id="b07fd-125">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="b07fd-125">Request URI</span></span>                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b07fd-126">**Få**</span><span class="sxs-lookup"><span data-stu-id="b07fd-126">**GET**</span></span>  | <span data-ttu-id="b07fd-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrationstatus HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="b07fd-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrationstatus HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="b07fd-128">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="b07fd-128">URI parameters</span></span>

<span data-ttu-id="b07fd-129">Använd följande sökvägsparametrar för att identifiera kunden och prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="b07fd-129">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="b07fd-130">Namn</span><span class="sxs-lookup"><span data-stu-id="b07fd-130">Name</span></span>                    | <span data-ttu-id="b07fd-131">Typ</span><span class="sxs-lookup"><span data-stu-id="b07fd-131">Type</span></span>       | <span data-ttu-id="b07fd-132">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="b07fd-132">Required</span></span> | <span data-ttu-id="b07fd-133">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="b07fd-133">Description</span></span>                                                   |
|-------------------------|------------|----------|---------------------------------------------------------------|
| <span data-ttu-id="b07fd-134">kund-id</span><span class="sxs-lookup"><span data-stu-id="b07fd-134">customer-id</span></span>             | <span data-ttu-id="b07fd-135">sträng</span><span class="sxs-lookup"><span data-stu-id="b07fd-135">string</span></span>     | <span data-ttu-id="b07fd-136">Ja</span><span class="sxs-lookup"><span data-stu-id="b07fd-136">Yes</span></span>      | <span data-ttu-id="b07fd-137">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="b07fd-137">A GUID formatted string that identifies the customer.</span></span>         |
| <span data-ttu-id="b07fd-138">prenumerations-id</span><span class="sxs-lookup"><span data-stu-id="b07fd-138">subscription-id</span></span>         | <span data-ttu-id="b07fd-139">sträng</span><span class="sxs-lookup"><span data-stu-id="b07fd-139">string</span></span>     | <span data-ttu-id="b07fd-140">Ja</span><span class="sxs-lookup"><span data-stu-id="b07fd-140">Yes</span></span>      | <span data-ttu-id="b07fd-141">En GUID-formaterad sträng som identifierar prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="b07fd-141">A GUID formatted string that identifies the subscription.</span></span>     |

### <a name="request-headers"></a><span data-ttu-id="b07fd-142">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="b07fd-142">Request headers</span></span>

<span data-ttu-id="b07fd-143">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="b07fd-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b07fd-144">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="b07fd-144">Request body</span></span>

<span data-ttu-id="b07fd-145">Inga.</span><span class="sxs-lookup"><span data-stu-id="b07fd-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="b07fd-146">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="b07fd-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-id>/subscriptions/<subscription-id>/registrationstatus HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="b07fd-147">REST-svar</span><span class="sxs-lookup"><span data-stu-id="b07fd-147">REST response</span></span>

<span data-ttu-id="b07fd-148">Om det lyckas innehåller svarstexten en [SubscriptionRegistrationStatus-resurs.](subscription-resources.md#subscriptionregistrationstatus)</span><span class="sxs-lookup"><span data-stu-id="b07fd-148">If successful, the response body contains a [SubscriptionRegistrationStatus](subscription-resources.md#subscriptionregistrationstatus) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b07fd-149">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="b07fd-149">Response success and error codes</span></span>

<span data-ttu-id="b07fd-150">Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="b07fd-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b07fd-151">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="b07fd-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b07fd-152">En fullständig lista finns i [Felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="b07fd-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b07fd-153">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="b07fd-153">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
MS-CV: InswEQre402koceL.0
MS-ServerId: 030020344

{
    "subscriptionId":"<subscription-id>",
    "status":"NotRegistered",
    "attributes":{
        "objectType":"SubscriptionRegistrationStatus"
    }
}
```
