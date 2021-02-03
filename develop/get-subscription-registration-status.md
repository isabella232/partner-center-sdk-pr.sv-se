---
title: Hämta status för prenumerationsregistrering
description: Hämta status för en prenumeration som har registrerats för användning med Azure Reserved VM Instances.
ms.date: 03/19/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e06cf8a450d6c281f7f83a68c899d1e5b29e9855
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769849"
---
# <a name="get-subscription-registration-status"></a><span data-ttu-id="929bc-103">Hämta status för prenumerationsregistrering</span><span class="sxs-lookup"><span data-stu-id="929bc-103">Get subscription registration status</span></span>

<span data-ttu-id="929bc-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="929bc-104">**Applies To**</span></span>

- <span data-ttu-id="929bc-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="929bc-105">Partner Center</span></span>

<span data-ttu-id="929bc-106">Hämta status för prenumerations registrering för en kund prenumeration som har Aktiver ATS för inköps Azure Reserved VM Instances.</span><span class="sxs-lookup"><span data-stu-id="929bc-106">How to get the subscription registration status for a customer subscription that has been enabled for purchasing Azure Reserved VM Instances.</span></span>

<span data-ttu-id="929bc-107">Om du vill köpa en virtuell Azure-reserverade VM-instans med hjälp av Partner Center API måste du ha minst en befintlig CSP Azure-prenumeration.</span><span class="sxs-lookup"><span data-stu-id="929bc-107">To purchase an Azure Reserved VM Instance using the Partner Center API, you must have at least one existing CSP Azure subscription.</span></span> <span data-ttu-id="929bc-108">Med metoden [Registrera en prenumeration](register-a-subscription.md) kan du registrera din befintliga CSP Azure-prenumeration, så att den kan köpa Azure Reserved VM instances.</span><span class="sxs-lookup"><span data-stu-id="929bc-108">The [Register a subscription](register-a-subscription.md) method allows you to register your existing CSP Azure subscription, enabling it for purchasing Azure Reserved VM Instances.</span></span> <span data-ttu-id="929bc-109">Med den här metoden kan du hämta statusen för den registreringen.</span><span class="sxs-lookup"><span data-stu-id="929bc-109">This method allows you to retrieve the status of that registration.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="929bc-110">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="929bc-110">Prerequisites</span></span>

- <span data-ttu-id="929bc-111">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="929bc-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="929bc-112">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="929bc-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="929bc-113">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="929bc-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="929bc-114">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="929bc-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="929bc-115">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="929bc-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="929bc-116">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="929bc-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="929bc-117">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="929bc-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="929bc-118">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="929bc-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="929bc-119">Ett prenumerations-ID.</span><span class="sxs-lookup"><span data-stu-id="929bc-119">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="929bc-120">C\#</span><span class="sxs-lookup"><span data-stu-id="929bc-120">C\#</span></span>

<span data-ttu-id="929bc-121">Om du vill hämta registrerings status för en prenumeration börjar du med att använda metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID: t för att identifiera kunden.</span><span class="sxs-lookup"><span data-stu-id="929bc-121">To get the registration status of a subscription, begin by using the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="929bc-122">Sedan kan du hämta ett gränssnitt till prenumerations åtgärder genom att anropa metoden [**Subscription. ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) med prenumerations-ID: t för att identifiera prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="929bc-122">Then, get an interface to subscription operations by calling the [**Subscription.ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method with the subscription ID to identify the subscription.</span></span> <span data-ttu-id="929bc-123">Använd sedan egenskapen RegistrationStatus för att hämta ett gränssnitt till den aktuella prenumerationens registrerings status åtgärder och anropa metoden **Get** eller **GetAsync** för att hämta **SubscriptionRegistrationStatus** -objektet.</span><span class="sxs-lookup"><span data-stu-id="929bc-123">Next, use the RegistrationStatus property to obtain an interface to the current subscription's registration status operations, and call the **Get** or **GetAsync** method to retrieve the **SubscriptionRegistrationStatus** object.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve a subscription's registration status details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).RegistrationStatus.Get();
```

## <a name="rest-request"></a><span data-ttu-id="929bc-124">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="929bc-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="929bc-125">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="929bc-125">Request syntax</span></span>

| <span data-ttu-id="929bc-126">Metod</span><span class="sxs-lookup"><span data-stu-id="929bc-126">Method</span></span>    | <span data-ttu-id="929bc-127">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="929bc-127">Request URI</span></span>                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="929bc-128">**TA**</span><span class="sxs-lookup"><span data-stu-id="929bc-128">**GET**</span></span>  | <span data-ttu-id="929bc-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Subscriptions/{Subscription-ID}/registrationstatus http/1.1</span><span class="sxs-lookup"><span data-stu-id="929bc-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrationstatus HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="929bc-130">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="929bc-130">URI parameters</span></span>

<span data-ttu-id="929bc-131">Använd följande Sök vägs parametrar för att identifiera kunden och prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="929bc-131">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="929bc-132">Namn</span><span class="sxs-lookup"><span data-stu-id="929bc-132">Name</span></span>                    | <span data-ttu-id="929bc-133">Typ</span><span class="sxs-lookup"><span data-stu-id="929bc-133">Type</span></span>       | <span data-ttu-id="929bc-134">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="929bc-134">Required</span></span> | <span data-ttu-id="929bc-135">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="929bc-135">Description</span></span>                                                   |
|-------------------------|------------|----------|---------------------------------------------------------------|
| <span data-ttu-id="929bc-136">kund-ID</span><span class="sxs-lookup"><span data-stu-id="929bc-136">customer-id</span></span>             | <span data-ttu-id="929bc-137">sträng</span><span class="sxs-lookup"><span data-stu-id="929bc-137">string</span></span>     | <span data-ttu-id="929bc-138">Yes</span><span class="sxs-lookup"><span data-stu-id="929bc-138">Yes</span></span>      | <span data-ttu-id="929bc-139">En GUID-formaterad sträng som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="929bc-139">A GUID formatted string that identifies the customer.</span></span>         |
| <span data-ttu-id="929bc-140">prenumerations-ID</span><span class="sxs-lookup"><span data-stu-id="929bc-140">subscription-id</span></span>         | <span data-ttu-id="929bc-141">sträng</span><span class="sxs-lookup"><span data-stu-id="929bc-141">string</span></span>     | <span data-ttu-id="929bc-142">Yes</span><span class="sxs-lookup"><span data-stu-id="929bc-142">Yes</span></span>      | <span data-ttu-id="929bc-143">En GUID-formaterad sträng som identifierar prenumerationen.</span><span class="sxs-lookup"><span data-stu-id="929bc-143">A GUID formatted string that identifies the subscription.</span></span>     |

### <a name="request-headers"></a><span data-ttu-id="929bc-144">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="929bc-144">Request headers</span></span>

<span data-ttu-id="929bc-145">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="929bc-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="929bc-146">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="929bc-146">Request body</span></span>

<span data-ttu-id="929bc-147">Inga.</span><span class="sxs-lookup"><span data-stu-id="929bc-147">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="929bc-148">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="929bc-148">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="929bc-149">REST-svar</span><span class="sxs-lookup"><span data-stu-id="929bc-149">REST response</span></span>

<span data-ttu-id="929bc-150">Om det lyckas innehåller svars texten en [SubscriptionRegistrationStatus](subscription-resources.md#subscriptionregistrationstatus) -resurs.</span><span class="sxs-lookup"><span data-stu-id="929bc-150">If successful, the response body contains a [SubscriptionRegistrationStatus](subscription-resources.md#subscriptionregistrationstatus) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="929bc-151">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="929bc-151">Response success and error codes</span></span>

<span data-ttu-id="929bc-152">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="929bc-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="929bc-153">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="929bc-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="929bc-154">En fullständig lista finns i [felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="929bc-154">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="929bc-155">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="929bc-155">Response example</span></span>

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
