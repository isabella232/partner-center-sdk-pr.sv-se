---
title: Vägledning för API-begränsning
description: För partner som anropar Partner Center-API:er kan du lära dig vilka API:er som påverkas av Microsoft API-begränsning och metodtips för att undvika eller bättre hantera begränsningar.
ms.date: 04/14/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: vijvala
ms.author: vijvala
ms.openlocfilehash: f18518e88b9bb08d4fd248922f4ce2fefdde004f
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025657"
---
# <a name="api-throttling-guidance-for-partners-calling-partner-center-apis"></a><span data-ttu-id="efdbc-103">Vägledning om API-begränsning för partner som anropar Partner Center-API:er</span><span class="sxs-lookup"><span data-stu-id="efdbc-103">API throttling guidance for partners calling Partner Center APIs</span></span> 

<span data-ttu-id="efdbc-104">Microsoft implementerar API-begränsning för att tillåta mer konsekventa prestanda inom ett tidsintervall för partner som anropar Partner Center-API:erna.</span><span class="sxs-lookup"><span data-stu-id="efdbc-104">Microsoft is implementing API throttling to allow more consistent performance within a time span for partners calling the Partner Center APIs.</span></span> <span data-ttu-id="efdbc-105">Begränsning begränsar antalet begäranden till en tjänst i ett tidsintervall för att förhindra överanvändning av resurser.</span><span class="sxs-lookup"><span data-stu-id="efdbc-105">Throttling limits the number of requests to a service in a time span to prevent overuse of resources.</span></span> <span data-ttu-id="efdbc-106">Partnercenter är utformat för att hantera ett stort antal begäranden, men om ett stort antal begäranden inträffar av få partner hjälper begränsningen till att bibehålla optimal prestanda och tillförlitlighet för alla partner.</span><span class="sxs-lookup"><span data-stu-id="efdbc-106">While Partner Center is designed to handle a high volume of requests, if an overwhelming number of requests occur by few partners, throttling helps maintain optimal performance and reliability for all partners.</span></span>  

<span data-ttu-id="efdbc-107">Begränsningsgränserna varierar beroende på scenariot.</span><span class="sxs-lookup"><span data-stu-id="efdbc-107">Throttling limits vary based on the scenario.</span></span> <span data-ttu-id="efdbc-108">Om du till exempel utför en stor mängd skrivningar är risken för begränsning högre än om du bara utför läsningar.</span><span class="sxs-lookup"><span data-stu-id="efdbc-108">For example, if you are performing a large volume of writes, the possibility for throttling is higher than if you are only performing reads.</span></span>

## <a name="what-happens-when-throttling-occurs"></a><span data-ttu-id="efdbc-109">Vad händer när begränsning inträffar?</span><span class="sxs-lookup"><span data-stu-id="efdbc-109">What happens when throttling occurs?</span></span> 

<span data-ttu-id="efdbc-110">När ett tröskelvärde för begränsning överskrids begränsar PartnerCenter eventuella ytterligare begäranden från klienten under en viss tidsperiod.</span><span class="sxs-lookup"><span data-stu-id="efdbc-110">When a throttling threshold is exceeded, Partner Center limits any further requests from that client for a period of time.</span></span> <span data-ttu-id="efdbc-111">Begränsningsbeteendet beror på typen och antalet begäranden.</span><span class="sxs-lookup"><span data-stu-id="efdbc-111">Throttling behavior depends on the type and number of requests.</span></span>   

### <a name="common-throttling-scenarios"></a><span data-ttu-id="efdbc-112">Vanliga begränsningsscenarier</span><span class="sxs-lookup"><span data-stu-id="efdbc-112">Common throttling scenarios</span></span> 

<span data-ttu-id="efdbc-113">De vanligaste orsakerna till begränsning av klienter är:</span><span class="sxs-lookup"><span data-stu-id="efdbc-113">The most common causes of throttling of clients include:</span></span> 

- <span data-ttu-id="efdbc-114">Ett stort antal begäranden för ett **API per partnerklientorganisations-ID:** för vissa Partner Center-API:er bestäms begränsningen av partnerklient-ID. För många anrop till dessa API:er på samma partnerklientorganisations-ID resulterar i att tröskelvärdet för begränsning överskrids.</span><span class="sxs-lookup"><span data-stu-id="efdbc-114">**A large number of requests for an API per Partner Tenant ID**: for some Partner Center APIs, throttling is determined by Partner Tenant ID, too many calls to those APIs on the same Partner Tenant ID will result in exceeding the throttling threshold.</span></span>  

- <span data-ttu-id="efdbc-115">Ett stort antal begäranden för ett **API per partnerklientorganisations-ID per** kundklientorganisations-ID: för andra API:er bestäms begränsningen av kombination av partnerklient-ID/kundklientorganisations-ID. I dessa fall resulterar för många anrop mot samma klientorganisations-ID för samma kund i begränsningen , medan anrop till andra kunder kan lyckas.</span><span class="sxs-lookup"><span data-stu-id="efdbc-115">**A large number of requests for an API per Partner Tenant ID per Customer Tenant ID**: for other APIs, throttling is determined by Partner Tenant ID/Customer Tenant ID combination; in those cases, making too many calls against the same customer tenant ID will result in throttling - while calls against other customers may succeed.</span></span>

## <a name="best-practices-to-avoid-throttling"></a><span data-ttu-id="efdbc-116">Metodtips för att undvika begränsning</span><span class="sxs-lookup"><span data-stu-id="efdbc-116">Best practices to avoid throttling</span></span> 
 
<span data-ttu-id="efdbc-117">Programmeringsmetoder, till exempel kontinuerlig avsökning av en resurs för att söka efter uppdateringar och regelbundet genomskanning av resurssamlingar för att söka efter nya eller borttagna resurser, leder troligen till begränsning och försämrar den övergripande prestandan.</span><span class="sxs-lookup"><span data-stu-id="efdbc-117">Programming practices such as continuously polling a resource to check for updates and regularly scanning resource collections to check for new or deleted resources are more likely to lead to throttling and will degrade overall performance.</span></span> <span data-ttu-id="efdbc-118">Samtidiga API-anrop kan leda till ett stort antal begäranden per enhetstid, vilket också gör att begäranden begränsas.</span><span class="sxs-lookup"><span data-stu-id="efdbc-118">Concurrent API calls may lead to high number of requests per unit time, which will also cause requests to be throttled.</span></span> <span data-ttu-id="efdbc-119">Du bör i stället använda ändringsspårning och ändringsmeddelanden.</span><span class="sxs-lookup"><span data-stu-id="efdbc-119">You should instead use change tracking and change notifications.</span></span> <span data-ttu-id="efdbc-120">Dessutom bör du kunna använda aktivitetsloggar för att identifiera ändringar.</span><span class="sxs-lookup"><span data-stu-id="efdbc-120">Additionally, you should be able to use activity logs for detecting changes.</span></span> <span data-ttu-id="efdbc-121">Mer information finns i [Aktivitetsloggar i Partnercenter.](get-a-record-of-partner-center-activity-by-user.md)</span><span class="sxs-lookup"><span data-stu-id="efdbc-121">For more information, see [Partner Center activity logs](get-a-record-of-partner-center-activity-by-user.md).</span></span>  <span data-ttu-id="efdbc-122">Vi rekommenderar starkt att partner överväger att använda aktivitetslogg-API:et för att öka effektiviteten och undvika begränsning.</span><span class="sxs-lookup"><span data-stu-id="efdbc-122">We highly recommend partners to consider using the activity log API for more efficiency and to avoid throttling.</span></span> <span data-ttu-id="efdbc-123">Se även exemplet på användning av aktivitetsloggar nedan.</span><span class="sxs-lookup"><span data-stu-id="efdbc-123">See also the example of using activity logs, below.</span></span>

## <a name="best-practices-to-handle-throttling"></a><span data-ttu-id="efdbc-124">Metodtips för att hantera begränsning</span><span class="sxs-lookup"><span data-stu-id="efdbc-124">Best practices to handle throttling</span></span>

<span data-ttu-id="efdbc-125">Följande är metodtips för hantering av begränsningar:</span><span class="sxs-lookup"><span data-stu-id="efdbc-125">The following are best practices for handling throttling:</span></span> 

- <span data-ttu-id="efdbc-126">Minska graden av parallellitet.</span><span class="sxs-lookup"><span data-stu-id="efdbc-126">Reduce the degree of parallelism.</span></span> 
- <span data-ttu-id="efdbc-127">Minska frekvensen för anrop.</span><span class="sxs-lookup"><span data-stu-id="efdbc-127">Reduce the frequency of calls.</span></span> 
- <span data-ttu-id="efdbc-128">Undvik omedelbara återförsök eftersom alla begäranden ackumuleras mot dina användningsgränser.</span><span class="sxs-lookup"><span data-stu-id="efdbc-128">Avoid immediate retries because all requests accrue against your usage limits.</span></span> 

<span data-ttu-id="efdbc-129">När du implementerar felhantering använder du HTTP-felkoden 429 för att identifiera begränsning.</span><span class="sxs-lookup"><span data-stu-id="efdbc-129">When you implement error handling, use the HTTP error code 429 to detect throttling.</span></span> <span data-ttu-id="efdbc-130">Det misslyckade svaret innehåller Retry-After svarshuvudet.</span><span class="sxs-lookup"><span data-stu-id="efdbc-130">The failed response includes the Retry-After response header.</span></span> <span data-ttu-id="efdbc-131">Det snabbaste sättet att återställa från begränsning är att backa bort begäranden med hjälp av retry-after-fördröjning.</span><span class="sxs-lookup"><span data-stu-id="efdbc-131">Backing off requests using the Retry-after delay is the fastest way to recover from throttling.</span></span> 

<span data-ttu-id="efdbc-132">Om du vill använda fördröjningen Försök igen efter gör du följande:</span><span class="sxs-lookup"><span data-stu-id="efdbc-132">To use the Retry-after delay, do the following:</span></span> 

1. <span data-ttu-id="efdbc-133">Vänta det antal sekunder som anges i Retry-After sidhuvud.</span><span class="sxs-lookup"><span data-stu-id="efdbc-133">Wait the number of seconds specified in the Retry-After header.</span></span> 

2. <span data-ttu-id="efdbc-134">Försök att skicka begäran igen.</span><span class="sxs-lookup"><span data-stu-id="efdbc-134">Retry the request.</span></span>  

3. <span data-ttu-id="efdbc-135">Om begäran misslyckas igen med felkoden 429 begränsas du fortfarande.</span><span class="sxs-lookup"><span data-stu-id="efdbc-135">If the request fails again with a 429 error code, you are still being throttled.</span></span> <span data-ttu-id="efdbc-136">Försök igen med exponentiell backoff, använd den rekommenderade Retry-After och försök igen tills den lyckas.</span><span class="sxs-lookup"><span data-stu-id="efdbc-136">Retry with Exponential backoff, use the recommended Retry-After delay and retry the request until it succeeds.</span></span>

4. <span data-ttu-id="efdbc-137">Om du använder SDK:n får du ett undantag med statuskod 429 när din begäran begränsas.</span><span class="sxs-lookup"><span data-stu-id="efdbc-137">If you are using the SDK, you'll receive an exception with status code 429 when your request is being throttled.</span></span> <span data-ttu-id="efdbc-138">Använd egenskapen RetryAfter i undantaget och försök igen när tiden har gått.</span><span class="sxs-lookup"><span data-stu-id="efdbc-138">Use the RetryAfter property in the exception and retry the request after the time is elapsed.</span></span>


## <a name="apis-currently-impacted-by-throttling"></a><span data-ttu-id="efdbc-139">API:er som för närvarande påverkas av begränsning</span><span class="sxs-lookup"><span data-stu-id="efdbc-139">APIs currently impacted by throttling</span></span>

<span data-ttu-id="efdbc-140">I slutändan begränsas varje partnercenter-API som anropar slutpunkten "api.partnercenter.microsoft.com/".</span><span class="sxs-lookup"><span data-stu-id="efdbc-140">In the end, every single Partner Center API that calls the endpoint “api.partnercenter.microsoft.com/” will be throttled.</span></span> <span data-ttu-id="efdbc-141">För närvarande tillämpas begränsningsgränserna endast på de API:er som anges nedan.</span><span class="sxs-lookup"><span data-stu-id="efdbc-141">Currently, the throttling limits are only enforced on the APIs listed below.</span></span> <span data-ttu-id="efdbc-142">Partnercenter samlar in telemetrin på vart och ett av API:erna och justerar begränsningsgränserna dynamiskt.</span><span class="sxs-lookup"><span data-stu-id="efdbc-142">Partner Center will be collecting the telemetry on each of the APIs and will dynamically adjust the throttling limits.</span></span> <span data-ttu-id="efdbc-143">I följande tabell visas de API:er där begränsning för närvarande tillämpas.</span><span class="sxs-lookup"><span data-stu-id="efdbc-143">The following table lists the APIs where throttling is currently enforced.</span></span>  


|<span data-ttu-id="efdbc-144">**Åtgärd**</span><span class="sxs-lookup"><span data-stu-id="efdbc-144">**Operation**</span></span>| <span data-ttu-id="efdbc-145">**Dokumentation för Partnercenter**</span><span class="sxs-lookup"><span data-stu-id="efdbc-145">**Partner Center documentation**</span></span>|
|------------------------|----------------------------|
|<span data-ttu-id="efdbc-146">{baseURL}/v1/customers/{customer_id}/orders</span><span class="sxs-lookup"><span data-stu-id="efdbc-146">{baseURL}/v1/customers/{customer_id}/orders</span></span>|[<span data-ttu-id="efdbc-147">skapa en order</span><span class="sxs-lookup"><span data-stu-id="efdbc-147">create an order</span></span>](create-an-order.md)|
|<span data-ttu-id="efdbc-148">{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/upgrades</span><span class="sxs-lookup"><span data-stu-id="efdbc-148">{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/upgrades</span></span>|[<span data-ttu-id="efdbc-149">övergå till en prenumeration</span><span class="sxs-lookup"><span data-stu-id="efdbc-149">transition a subscription</span></span>](transition-a-subscription.md)|
|<span data-ttu-id="efdbc-150">{baseURL}/v1/customers/{customer-tenant-id}/orders/{order-id}</span><span class="sxs-lookup"><span data-stu-id="efdbc-150">{baseURL}/v1/customers/{customer-tenant-id}/orders/{order-id}</span></span>|[<span data-ttu-id="efdbc-151">köpa ett tillägg till en prenumeration</span><span class="sxs-lookup"><span data-stu-id="efdbc-151">purchase an addon to a subscription</span></span>](purchase-an-add-on-to-a-subscription.md)|
|<span data-ttu-id="efdbc-152">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}</span><span class="sxs-lookup"><span data-stu-id="efdbc-152">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}</span></span>|[<span data-ttu-id="efdbc-153">skapa en kundvagn</span><span class="sxs-lookup"><span data-stu-id="efdbc-153">create a cart</span></span>](create-a-cart.md)|
|<span data-ttu-id="efdbc-154">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}/checkout</span><span class="sxs-lookup"><span data-stu-id="efdbc-154">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}/checkout</span></span>|[<span data-ttu-id="efdbc-155">checka ut en kundvagn</span><span class="sxs-lookup"><span data-stu-id="efdbc-155">checkout a cart</span></span>](checkout-a-cart.md)|
|<span data-ttu-id="efdbc-156">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}</span><span class="sxs-lookup"><span data-stu-id="efdbc-156">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}</span></span>|[<span data-ttu-id="efdbc-157">uppdatera en kundvagn</span><span class="sxs-lookup"><span data-stu-id="efdbc-157">update a cart</span></span>](update-a-cart.md)|
|<span data-ttu-id="efdbc-158">{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrations</span><span class="sxs-lookup"><span data-stu-id="efdbc-158">{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrations</span></span>|[<span data-ttu-id="efdbc-159">registrera en prenumeration</span><span class="sxs-lookup"><span data-stu-id="efdbc-159">register a subscription</span></span>](register-a-subscription.md)|
|<span data-ttu-id="efdbc-160">{baseURL}/v1/productupgrades</span><span class="sxs-lookup"><span data-stu-id="efdbc-160">{baseURL}/v1/productupgrades</span></span>|[<span data-ttu-id="efdbc-161">skapa entitet för produktuppgradering</span><span class="sxs-lookup"><span data-stu-id="efdbc-161">create product upgrade entity</span></span>](create-product-upgrade-entity.md)|
|<span data-ttu-id="efdbc-162">{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions</span><span class="sxs-lookup"><span data-stu-id="efdbc-162">{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions</span></span> |[<span data-ttu-id="efdbc-163">konvertera en utvärderingsprenumeration till betald</span><span class="sxs-lookup"><span data-stu-id="efdbc-163">convert a trial subscription to paid</span></span>](convert-a-trial-subscription-to-paid.md)|
|<span data-ttu-id="efdbc-164">{baseURL}/v1/customers/{customer-tenant-id}</span><span class="sxs-lookup"><span data-stu-id="efdbc-164">{baseURL}/v1/customers/{customer-tenant-id}</span></span>|[<span data-ttu-id="efdbc-165">hämta en kund via ID</span><span class="sxs-lookup"><span data-stu-id="efdbc-165">get a customer by ID</span></span>](get-a-customer-by-id.md)|
|<span data-ttu-id="efdbc-166">{baseURL}/v1/productUpgrades/eligibility</span><span class="sxs-lookup"><span data-stu-id="efdbc-166">{baseURL}/v1/productUpgrades/eligibility</span></span>|[<span data-ttu-id="efdbc-167">få behörighet för produktuppgradering</span><span class="sxs-lookup"><span data-stu-id="efdbc-167">get eligibility for product upgrade</span></span>](get-eligibility-for-product-upgrade.md)|
|<span data-ttu-id="efdbc-168">{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}</span><span class="sxs-lookup"><span data-stu-id="efdbc-168">{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}</span></span> |[<span data-ttu-id="efdbc-169">hantera prenumeration</span><span class="sxs-lookup"><span data-stu-id="efdbc-169">manage subscription</span></span>](manage-orders.md#manage-a-subscription)|
|<span data-ttu-id="efdbc-170">{baseURL}/v1/customers/{customer_id}/subscriptions</span><span class="sxs-lookup"><span data-stu-id="efdbc-170">{baseURL}/v1/customers/{customer_id}/subscriptions</span></span> |[<span data-ttu-id="efdbc-171">get-all-of-a-customer-s-subscriptions</span><span class="sxs-lookup"><span data-stu-id="efdbc-171">get-all-of-a-customer-s-subscriptions</span></span>](get-all-of-a-customer-s-subscriptions.md)|
|<span data-ttu-id="efdbc-172">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}</span><span class="sxs-lookup"><span data-stu-id="efdbc-172">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}</span></span>|[<span data-ttu-id="efdbc-173">Hämta en prenumeration efter ID</span><span class="sxs-lookup"><span data-stu-id="efdbc-173">Get a subscription by ID</span></span>](get-a-subscription-by-id.md)|
|<span data-ttu-id="efdbc-174">{baseURL}/v1/customers/{customer_id}/orders</span><span class="sxs-lookup"><span data-stu-id="efdbc-174">{baseURL}/v1/customers/{customer_id}/orders</span></span>|[<span data-ttu-id="efdbc-175">Hämta alla kundorder</span><span class="sxs-lookup"><span data-stu-id="efdbc-175">Get all customer orders</span></span>](get-all-of-a-customer-s-orders.md)|
|<span data-ttu-id="efdbc-176">{baseURL}/v1/customers/{customer_id}/orders/{order_id}</span><span class="sxs-lookup"><span data-stu-id="efdbc-176">{baseURL}/v1/customers/{customer_id}/orders/{order_id}</span></span>|[<span data-ttu-id="efdbc-177">Hämta en beställning efter ID</span><span class="sxs-lookup"><span data-stu-id="efdbc-177">Get an order by ID</span></span>](get-an-order-by-id.md)|
|<span data-ttu-id="efdbc-178">{baseURL}/v1/customers/{customer_id}/orders/{order_id}/provisioningstatus</span><span class="sxs-lookup"><span data-stu-id="efdbc-178">{baseURL}/v1/customers/{customer_id}/orders/{order_id}/provisioningstatus</span></span>|[<span data-ttu-id="efdbc-179">Hämta status för prenumerationsetablering</span><span class="sxs-lookup"><span data-stu-id="efdbc-179">Get subscription provisioning status</span></span>](get-subscription-provisioning-status.md)|
|<span data-ttu-id="efdbc-180">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}</span><span class="sxs-lookup"><span data-stu-id="efdbc-180">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}</span></span>|[<span data-ttu-id="efdbc-181">Hantera beställningar och hantera en prenumeration</span><span class="sxs-lookup"><span data-stu-id="efdbc-181">Manage orders and manage a subscription</span></span>](manage-orders.md#manage-a-subscription)|
|<span data-ttu-id="efdbc-182">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/addons</span><span class="sxs-lookup"><span data-stu-id="efdbc-182">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/addons</span></span>|[<span data-ttu-id="efdbc-183">Hämta en lista över tillägg för en prenumeration</span><span class="sxs-lookup"><span data-stu-id="efdbc-183">Get a list of add-ons for a subscription</span></span>](get-a-list-of-add-ons-for-a-subscription.md)|
|<span data-ttu-id="efdbc-184">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/azureEntitlements</span><span class="sxs-lookup"><span data-stu-id="efdbc-184">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/azureEntitlements</span></span>|[<span data-ttu-id="efdbc-185">Hämta en lista över Azure-rättigheter för en prenumeration</span><span class="sxs-lookup"><span data-stu-id="efdbc-185">Get a list of Azure entitlements for a subscription</span></span>](get-a-list-of-azure-entitlements-for-subscription.md)|
|<span data-ttu-id="efdbc-186">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/registrationstatus</span><span class="sxs-lookup"><span data-stu-id="efdbc-186">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/registrationstatus</span></span>|[<span data-ttu-id="efdbc-187">Hämta status för prenumerationsregistrering</span><span class="sxs-lookup"><span data-stu-id="efdbc-187">Get subscription registration status</span></span>](get-subscription-registration-status.md)|
|<span data-ttu-id="efdbc-188">{baseURL}/v1/customers/{customer-tenant-id}/transfers</span><span class="sxs-lookup"><span data-stu-id="efdbc-188">{baseURL}/v1/customers/{customer-tenant-id}/transfers</span></span>|[<span data-ttu-id="efdbc-189">Hämta alla en kunds överföringar</span><span class="sxs-lookup"><span data-stu-id="efdbc-189">Get all of a customer's transfers</span></span>](get-all-of-a-customer-s-transfers.md)|
|<span data-ttu-id="efdbc-190">{baseURL}/v1/productUpgrades/{upgrade-id}/status</span><span class="sxs-lookup"><span data-stu-id="efdbc-190">{baseURL}/v1/productUpgrades/{upgrade-id}/status</span></span>|[<span data-ttu-id="efdbc-191">Hämta status för produktuppgradering</span><span class="sxs-lookup"><span data-stu-id="efdbc-191">Get product upgrade status</span></span>](get-product-upgrade-status.md)|
|<span data-ttu-id="efdbc-192">{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions</span><span class="sxs-lookup"><span data-stu-id="efdbc-192">{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions</span></span>|[<span data-ttu-id="efdbc-193">Hämta en lista över erbjudanden för utvärderingskonvertering</span><span class="sxs-lookup"><span data-stu-id="efdbc-193">Get a list of trial conversion offers</span></span>](get-a-list-of-trial-conversion-offers.md)|


### <a name="error-code-response"></a><span data-ttu-id="efdbc-194">Felkodssvar:</span><span class="sxs-lookup"><span data-stu-id="efdbc-194">Error code response:</span></span>
```http
HTTP/1.1 429 Too Many Requests 

Content-Length: 84 

Content-Type: application/json 

Retry-After: 57 

Date: Tue, 21 Jul 2020 04:10:58 GMT 

{ "statusCode": 429, "message": "Rate limit is exceeded. Try again in 57 seconds." } 
```

## <a name="example-of-activity-log"></a><span data-ttu-id="efdbc-195">Exempel på aktivitetslogg</span><span class="sxs-lookup"><span data-stu-id="efdbc-195">Example of activity log</span></span>

<span data-ttu-id="efdbc-196">För bästa praxis vid analys av dagliga ändringar rekommenderar vi att du frågar efter granskningspost för en viss dag.</span><span class="sxs-lookup"><span data-stu-id="efdbc-196">For best practice in analyzing daily changes, we recommend that you query audit record for a specific day.</span></span> 

<span data-ttu-id="efdbc-197">I svaret får du ett resultat med ändringar av den specifika åtgärdstypen.</span><span class="sxs-lookup"><span data-stu-id="efdbc-197">In the response, you will get a result with changes to specific operation type.</span></span><span data-ttu-id="efdbc-198">Du kan filtrera baserat på den åtgärd du bryr dig om.</span><span class="sxs-lookup"><span data-stu-id="efdbc-198">  You can filter based on the operation you care about.</span></span> <span data-ttu-id="efdbc-199">Om du till exempel är intresserad av en nyligen skapad kund kan du titta på operationType = "add_customer".</span><span class="sxs-lookup"><span data-stu-id="efdbc-199"> For example, if you are interested in a newly created customer, you can look at operationType = “add_customer”.</span></span>  

<span data-ttu-id="efdbc-200">Lista över operationtype/resources finns i API-dokumentationen nedan.</span><span class="sxs-lookup"><span data-stu-id="efdbc-200">List of operationtype/resources can be found in below API docs.</span></span>  

- [<span data-ttu-id="efdbc-201">Granska resurser</span><span class="sxs-lookup"><span data-stu-id="efdbc-201">Auditing resources</span></span>](auditing-resources.md)  

- [<span data-ttu-id="efdbc-202">Hämta en post för en Partnercenter-aktivitet per användare</span><span class="sxs-lookup"><span data-stu-id="efdbc-202">Get a record of a Partner Center activity by user</span></span>](get-a-record-of-partner-center-activity-by-user.md)  



### <a name="response-example"></a><span data-ttu-id="efdbc-203">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="efdbc-203">Response example</span></span>

<span data-ttu-id="efdbc-204">**Begäran:**</span><span class="sxs-lookup"><span data-stu-id="efdbc-204">**Request**:</span></span>  
```http
Http Get call:  https://api.partnercenter.microsoft.com/v1/auditrecords?startDate=2020-09-02&endDate=2020-09-02&size=50 

Authorization: Bearer <token> 

Accept: application/json 

MS-RequestId: 127facaa-e389-41f8-8bb7-1d1af99db893 

MS-CorrelationId: de9c2ccc-40dd-4186-9660-65b9b64c3d14 

X-Locale: en-US 

Host: api.partnercenter.microsoft.com 

Connection: Keep-Alive 
```

<span data-ttu-id="efdbc-205">**Svar**:</span><span class="sxs-lookup"><span data-stu-id="efdbc-205">**Response**:</span></span>    
```http
{ 

    "totalCount": 17, 

    "items": [ 

        { 

            "id": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d_e905b566-4779-4e57-944c-7b1b5312705b_updatecustomeruserlicenses_637346859797753934", 

            "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d", 

            "participants": [ 

                "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d" 

            ], 

            "customerId": "e905b566-4779-4e57-944c-7b1b5312705b", 

            "userPrincipalName": "admin@testsw09.onmicrosoft.com", 

            "applicationId": "FulfillmentService", 

            "resourceType": "license", 

            "operationType": "update_customer_user_licenses", 

            "operationDate": "2020-09-02T23:26:19.7753934Z", 

            "operationStatus": "succeeded", 

            "customizedData": [ 

                { 

                    "key": "CustomerUserId", 

                    "value": "933808c7-b165-496c-a24e-1a4b7846fab4" 

                } 

            ], 

            "attributes": { 

                "objectType": "AuditRecord" 

            } 

        }, 

        { 

            "id": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d_86bddccf-9a53-40c6-907c-08067a3f8da7_ia80zlkxp6ewoqpp35pbqjlhqv9iigvz1_createorder_637346662909268372", 

            "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d", 

            "participants": [ 

                "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d" 

            ], 

            "customerId": "86bddccf-9a53-40c6-907c-08067a3f8da7", 

            "customerName": "CustomMetersStagingTest", 

            "userPrincipalName": "admin@testsw09.onmicrosoft.com", 

            "applicationId": "4990cffe-04e8-4e8b-808a-1175604b879f", 

            "resourceType": "order", 

            "resourceNewValue": "{\"Id\":\"Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1\",\"AlternateId\":\"64144d300bde\",\"ReferenceCustomerId\":\"86bddccf-9a53-40c6-907c-08067a3f8da7\",\"BillingCycle\":\"monthly\",\"CurrencyCode\":\"USD\",\"CurrencySymbol\":\"$\",\"LineItems\":[{\"LineItemNumber\":0,\"ProvisioningContext\":null,\"OfferId\":\"DZH318Z0C964:0001:DZH318Z0BZDG\",\"SubscriptionId\":\"f428d44a-d08b-348b-579e-ce92a6362c7b\",\"ParentSubscriptionId\":null,\"TermDuration\":\"P1M\",\"TransactionType\":\"New\",\"FriendlyName\":\"SaaS custom meter offer - Bronze\",\"Quantity\":1,\"Pricing\":null,\"PartnerIdOnRecord\":null,\"RenewsTo\":null,\"Links\":{\"Product\":{\"Uri\":\"/products/DZH318Z0C964?country=US\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"Sku\":{\"Uri\":\"/products/DZH318Z0C964/skus/0001?country=US\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"Availability\":{\"Uri\":\"/products/DZH318Z0C964/skus/0001/availabilities/DZH318Z0BZDG?country=US\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"ActivationLinks\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1/lineitems/0/activationlinks\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]}}}],\"CreationDate\":\"2020-09-02T17:58:01.7755853Z\",\"Status\":\"pending\",\"TransactionType\":\"UserPurchase\",\"Links\":{\"Self\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"ProvisioningStatus\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1/provisioningstatus\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"PatchOperation\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1\",\"Method\":\"PATCH\",\"Body\":null,\"Headers\":[]}},\"Client\":{\"marketplaceCountry\":\"US\",\"deviceFamily\":\"UniversalStore-PartnerCenter\",\"name\":\"Partner Center Web\"},\"Attributes\":{\"ObjectType\":\"Order\"}}", 

            "operationType": "create_order", 

            "originalCorrelationId": "96514ebe-c1b2-4865-cb46-2c2d20a2e911", 

            "operationDate": "2020-09-02T17:58:10.9268372Z", 

            "operationStatus": "succeeded", 

            "customizedData": [ 

                { 

                    "key": "OrderId", 

                    "value": "Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1" 

                }, 

                { 

                    "key": "AlternateId", 

                    "value": "64144d300bde" 

                }, 

                { 

                    "key": "BillingCycle", 

                    "value": "Monthly" 

                }, 

                { 

                    "key": "OfferId-0", 

                    "value": "DZH318Z0C964:0001:DZH318Z0BZDG" 

                }, 

                { 

                    "key": "SubscriptionId-0", 

                    "value": "f428d44a-d08b-348b-579e-ce92a6362c7b" 

                }, 

                { 

                    "key": "SubscriptionName-0", 

                    "value": "SaaS custom meter offer - Bronze" 

                }, 

                { 

                   "key": "Quantity-0", 

                    "value": "1" 

                }, 

                { 

                    "key": "PartnerOnRecord-0", 

                    "value": null 

                } 

            ], 

            "attributes": { 

                "objectType": "AuditRecord" 

            } 

        }, 

                           { 

            "id": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d_86bddccf-9a53-40c6-907c-08067a3f8da7_86bddccf-9a53-40c6-907c-08067a3f8da7_addcustomer_637346648528069005", 

            "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d", 

            "participants": [ 

                "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d" 

            ], 

            "customerId": "86bddccf-9a53-40c6-907c-08067a3f8da7", 

            "customerName": "CustomMetersStagingTest", 

            "userPrincipalName": "admin@testsw09.onmicrosoft.com", 

            "applicationId": "4990cffe-04e8-4e8b-808a-1175604b879f", 

            "resourceType": "customer", 

            "resourceNewValue": "{\"Id\":\"86bddccf-9a53-40c6-907c-08067a3f8da7\",\"CommerceId\":\"9dd78b4f-f98a-44b4-a2fa-2b82ac58d24c\",\"CompanyProfile\":{\"TenantId\":\"86bddccf-9a53-40c6-907c-08067a3f8da7\",\"Domain\":\"CustomMetersStagingTest.onmicrosoft.com\",\"CompanyName\":\"CustomMetersStagingTest\",\"Address\":null,\"Email\":null,\"OrganizationRegistrationNumber\":null,\"Links\":{\"Self\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/profiles/company\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]}},\"Attributes\":{\"ObjectType\":\"CustomerCompanyProfile\"}},\"BillingProfile\":{\"Id\":\"4beafd7b-cdab-5bdc-52ed-02e16edf2e7a\",\"FirstName\":\"CustomMetersStagingTest\",\"LastName\":\"CustomMetersStagingTest\",\"Email\":\"CustomMetersStagingTest@CustomMetersStagingTest.com\",\"Culture\":\"en-US\",\"Language\":\"en\",\"CompanyName\":\"CustomMetersStagingTest\",\"DefaultAddress\":{\"Id\":null,\"Country\":\"US\",\"Region\":null,\"City\":\"Seattle\",\"State\":\"WA\",\"District\":null,\"AddressLine1\":\"CustomMetersStagingTest\",\"AddressLine2\":null,\"AddressLine3\":null,\"PostalCode\":\"98122\",\"FirstName\":\"CustomMetersStagingTest\",\"LastName\":\"CustomMetersStagingTest\",\"EmailAddress\":null,\"PhoneNumber\":null,\"MiddleName\":null},\"Attributes\":{\"Etag\":\"-2279334701316321663\",\"ObjectType\":\"CustomerBillingProfile\"}},\"RelationshipToPartner\":\"reseller\",\"AllowDelegatedAccess\":true,\"UserCredentials\":{\"userName\":\"admin\",\"password\":\"\"},\"AssociatedPartnerId\":null,\"CustomDomains\":null,\"Attributes\":{\"ObjectType\":\"Customer\"}}", 

            "operationType": "add_customer", 

            "originalCorrelationId": "7550d9ea-e64a-416f-e49b-3670c516cf69", 

            "operationDate": "2020-09-02T17:34:12.8069005Z", 

            "operationStatus": "succeeded", 

            "customizedData": [ 

                { 

                    "key": "PrimaryDomainName", 

                    "value": "CustomMetersStagingTest.onmicrosoft.com" 

                }, 

                { 

                    "key": "Relationship", 

                    "value": "Reseller" 

                } 

            ], 

            "attributes": { 

                "objectType": "AuditRecord" 

            } 

        }, 

                            

        ... 

    ], 

    "links": { 

        "self": { 

            "uri": "/auditrecords?startDate=2020-09-02&endDate=2020-09-02&size=50", 

            "method": "GET", 

            "headers": [] 

        } 

    }, 

    "attributes": { 

        "objectType": "Collection" 

    } 

} 
```
 

