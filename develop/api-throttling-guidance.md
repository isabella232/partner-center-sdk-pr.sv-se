---
title: Vägledning för API-begränsning
description: För partner som anropar Partner Center-API:er kan du lära dig vilka API:er som påverkas av Microsoft API-begränsning och metodtips för att undvika eller bättre hantera begränsning.
ms.date: 04/14/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: vijvala
ms.author: vijvala
ms.openlocfilehash: ab1138e19e06111299ab43ea13a6f033274aaa5d
ms.sourcegitcommit: 3c3a21e73aaadf3023cf4c13b09809ceae5f027a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/14/2021
ms.locfileid: "107496152"
---
# <a name="api-throttling-guidance-for-partners-calling-partner-center-apis"></a><span data-ttu-id="923f6-103">Api-begränsningsvägledning för partner som anropar Partner Center-API:er</span><span class="sxs-lookup"><span data-stu-id="923f6-103">API throttling guidance for partners calling Partner Center APIs</span></span> 

<span data-ttu-id="923f6-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="923f6-104">**Applies to**</span></span>

- <span data-ttu-id="923f6-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="923f6-105">Partner Center</span></span>

<span data-ttu-id="923f6-106">Microsoft implementerar API-begränsning för att tillåta mer konsekventa prestanda inom ett tidsintervall för partner som anropar Partner Center-API:erna.</span><span class="sxs-lookup"><span data-stu-id="923f6-106">Microsoft is implementing API throttling to allow more consistent performance within a time span for partners calling the Partner Center APIs.</span></span> <span data-ttu-id="923f6-107">Begränsning begränsar antalet begäranden till en tjänst under ett tidsintervall för att förhindra överanvändning av resurser.</span><span class="sxs-lookup"><span data-stu-id="923f6-107">Throttling limits the number of requests to a service in a time span to prevent overuse of resources.</span></span> <span data-ttu-id="923f6-108">Partner Center är utformat för att hantera ett stort antal begäranden, men om ett stort antal begäranden inträffar av få partner hjälper begränsningen till att upprätthålla optimala prestanda och tillförlitlighet för alla partner.</span><span class="sxs-lookup"><span data-stu-id="923f6-108">While Partner Center is designed to handle a high volume of requests, if an overwhelming number of requests occur by few partners, throttling helps maintain optimal performance and reliability for all partners.</span></span>  

<span data-ttu-id="923f6-109">Begränsningsgränserna varierar beroende på scenariot.</span><span class="sxs-lookup"><span data-stu-id="923f6-109">Throttling limits vary based on the scenario.</span></span> <span data-ttu-id="923f6-110">Om du till exempel utför en stor mängd skrivningar är risken för begränsning högre än om du bara utför läsningar.</span><span class="sxs-lookup"><span data-stu-id="923f6-110">For example, if you are performing a large volume of writes, the possibility for throttling is higher than if you are only performing reads.</span></span>

## <a name="what-happens-when-throttling-occurs"></a><span data-ttu-id="923f6-111">Vad händer när begränsning inträffar?</span><span class="sxs-lookup"><span data-stu-id="923f6-111">What happens when throttling occurs?</span></span> 

<span data-ttu-id="923f6-112">När ett tröskelvärde för begränsning överskrids begränsar PartnerCenter eventuella ytterligare begäranden från klienten under en viss tidsperiod.</span><span class="sxs-lookup"><span data-stu-id="923f6-112">When a throttling threshold is exceeded, Partner Center limits any further requests from that client for a period of time.</span></span> <span data-ttu-id="923f6-113">Begränsningsbeteendet beror på typen och antalet begäranden.</span><span class="sxs-lookup"><span data-stu-id="923f6-113">Throttling behavior depends on the type and number of requests.</span></span>   

### <a name="common-throttling-scenarios"></a><span data-ttu-id="923f6-114">Vanliga begränsningsscenarier</span><span class="sxs-lookup"><span data-stu-id="923f6-114">Common throttling scenarios</span></span> 

<span data-ttu-id="923f6-115">De vanligaste orsakerna till begränsning av klienter är:</span><span class="sxs-lookup"><span data-stu-id="923f6-115">The most common causes of throttling of clients include:</span></span> 

- <span data-ttu-id="923f6-116">Ett stort antal begäranden för ett **API per partnerklientorganisations-ID:** för vissa Partner Center-API:er bestäms begränsningen av partnerklient-ID. För många anrop till dessa API:er på samma partnerklientorganisations-ID resulterar i att tröskelvärdet för begränsning överskrids.</span><span class="sxs-lookup"><span data-stu-id="923f6-116">**A large number of requests for an API per Partner Tenant ID**: for some Partner Center APIs, throttling is determined by Partner Tenant ID, too many calls to those APIs on the same Partner Tenant ID will result in exceeding the throttling threshold.</span></span>  

- <span data-ttu-id="923f6-117">Ett stort antal begäranden för ett **API per partnerklientorganisations-ID per** kundklientorganisations-ID: för andra API:er bestäms begränsningen av kombinationen partnerklient-ID/kundklientorganisations-ID. I dessa fall resulterar för många anrop mot samma kundklientorganisations-ID i begränsningen , medan anrop till andra kunder kan lyckas.</span><span class="sxs-lookup"><span data-stu-id="923f6-117">**A large number of requests for an API per Partner Tenant ID per Customer Tenant ID**: for other APIs, throttling is determined by Partner Tenant ID/Customer Tenant ID combination; in those cases, making too many calls against the same customer tenant ID will result in throttling - while calls against other customers may succeed.</span></span>

## <a name="best-practices-to-avoid-throttling"></a><span data-ttu-id="923f6-118">Metodtips för att undvika begränsning</span><span class="sxs-lookup"><span data-stu-id="923f6-118">Best practices to avoid throttling</span></span> 
 
<span data-ttu-id="923f6-119">Programmeringsmetoder, till exempel kontinuerlig avsökning av en resurs för att söka efter uppdateringar och regelbundet genomskanning av resurssamlingar för att söka efter nya eller borttagna resurser, leder troligen till begränsning och försämrar den övergripande prestandan.</span><span class="sxs-lookup"><span data-stu-id="923f6-119">Programming practices such as continuously polling a resource to check for updates and regularly scanning resource collections to check for new or deleted resources are more likely to lead to throttling and will degrade overall performance.</span></span> <span data-ttu-id="923f6-120">Samtidiga API-anrop kan leda till ett stort antal begäranden per enhetstid, vilket också gör att begäranden begränsas.</span><span class="sxs-lookup"><span data-stu-id="923f6-120">Concurrent API calls may lead to high number of requests per unit time, which will also cause requests to be throttled.</span></span> <span data-ttu-id="923f6-121">Du bör i stället använda ändringsspårning och ändringsmeddelanden.</span><span class="sxs-lookup"><span data-stu-id="923f6-121">You should instead leverage change tracking and change notifications.</span></span> <span data-ttu-id="923f6-122">Dessutom bör du kunna använda aktivitetsloggar för att identifiera ändringar. Mer information finns [i Aktivitetsloggar](get-a-record-of-partner-center-activity-by-user.md) i Partnercenter.</span><span class="sxs-lookup"><span data-stu-id="923f6-122">Additionally, you should be able to leverage activity logs for detecting changes, see [Partner Center activity logs](get-a-record-of-partner-center-activity-by-user.md) for more information.</span></span>  <span data-ttu-id="923f6-123">Vi rekommenderar starkt att partner överväger att använda aktivitetslogg-API:et för att öka effektiviteten och undvika begränsning.</span><span class="sxs-lookup"><span data-stu-id="923f6-123">We highly recommend partners to consider using the activity log API for more efficiency and to avoid throttling.</span></span> <span data-ttu-id="923f6-124">Se även exemplet på användning av aktivitetsloggar nedan.</span><span class="sxs-lookup"><span data-stu-id="923f6-124">See also the example of using activity logs, below.</span></span>

## <a name="best-practices-to-handle-throttling"></a><span data-ttu-id="923f6-125">Metodtips för att hantera begränsning</span><span class="sxs-lookup"><span data-stu-id="923f6-125">Best practices to handle throttling</span></span>

<span data-ttu-id="923f6-126">Följande är metodtips för hantering av begränsningar:</span><span class="sxs-lookup"><span data-stu-id="923f6-126">The following are best practices for handling throttling:</span></span> 

- <span data-ttu-id="923f6-127">Minska graden av parallellitet.</span><span class="sxs-lookup"><span data-stu-id="923f6-127">Reduce the degree of parallelism.</span></span> 
- <span data-ttu-id="923f6-128">Minska frekvensen för anrop.</span><span class="sxs-lookup"><span data-stu-id="923f6-128">Reduce the frequency of calls.</span></span> 
- <span data-ttu-id="923f6-129">Undvik omedelbara återförsök eftersom alla begäranden ackumuleras mot dina användningsgränser.</span><span class="sxs-lookup"><span data-stu-id="923f6-129">Avoid immediate retries because all requests accrue against your usage limits.</span></span> 

<span data-ttu-id="923f6-130">När du implementerar felhantering använder du HTTP-felkoden 429 för att identifiera begränsning.</span><span class="sxs-lookup"><span data-stu-id="923f6-130">When you implement error handling, use the HTTP error code 429 to detect throttling.</span></span> <span data-ttu-id="923f6-131">Det misslyckade svaret innehåller Retry-After svarshuvudet.</span><span class="sxs-lookup"><span data-stu-id="923f6-131">The failed response includes the Retry-After response header.</span></span> <span data-ttu-id="923f6-132">Det snabbaste sättet att återställa från begränsning är att backa bort begäranden med hjälp av retry-after-fördröjning.</span><span class="sxs-lookup"><span data-stu-id="923f6-132">Backing off requests using the Retry-after delay is the fastest way to recover from throttling.</span></span> 

<span data-ttu-id="923f6-133">Om du vill använda fördröjningen Försök igen efter gör du följande:</span><span class="sxs-lookup"><span data-stu-id="923f6-133">To use the Retry-after delay, do the following:</span></span> 

1. <span data-ttu-id="923f6-134">Vänta det antal sekunder som anges i Retry-After sidhuvud.</span><span class="sxs-lookup"><span data-stu-id="923f6-134">Wait the number of seconds specified in the Retry-After header.</span></span> 

2. <span data-ttu-id="923f6-135">Försök att skicka begäran igen.</span><span class="sxs-lookup"><span data-stu-id="923f6-135">Retry the request.</span></span>  

3. <span data-ttu-id="923f6-136">Om begäran misslyckas igen med felkoden 429 begränsas du fortfarande.</span><span class="sxs-lookup"><span data-stu-id="923f6-136">If the request fails again with a 429 error code, you are still being throttled.</span></span> <span data-ttu-id="923f6-137">Försök igen med exponentiell backoff, använd den rekommenderade Retry-After och försök igen tills den lyckas.</span><span class="sxs-lookup"><span data-stu-id="923f6-137">Retry with Exponential backoff, use the recommended Retry-After delay and retry the request until it succeeds.</span></span>

4. <span data-ttu-id="923f6-138">Om du använder SDK får du ett undantag med statuskod 429 när din begäran begränsas.</span><span class="sxs-lookup"><span data-stu-id="923f6-138">If you are using SDK you'll receive an exception with status code 429 when your request is being throttled.</span></span> <span data-ttu-id="923f6-139">Använd egenskapen RetryAfter i undantaget och försök igen när tiden har gått.</span><span class="sxs-lookup"><span data-stu-id="923f6-139">Use the RetryAfter property in the exception and retry the request after the time is elapsed.</span></span>


## <a name="apis-currently-impacted-by-throttling"></a><span data-ttu-id="923f6-140">API:er som för närvarande påverkas av begränsning</span><span class="sxs-lookup"><span data-stu-id="923f6-140">APIs currently impacted by throttling</span></span>

<span data-ttu-id="923f6-141">I det långa loppet begränsas varje partnercenter-API som anropar slutpunkten "api.partnercenter.microsoft.com/" .</span><span class="sxs-lookup"><span data-stu-id="923f6-141">In the long run, every single Partner Center API that calls the endpoint “api.partnercenter.microsoft.com/” will be throttled.</span></span> <span data-ttu-id="923f6-142">För närvarande tillämpas begränsningsgränserna endast på de API:er som anges nedan.</span><span class="sxs-lookup"><span data-stu-id="923f6-142">Currently, the throttling limits are only enforced on the APIs listed below.</span></span> <span data-ttu-id="923f6-143">Partner Center samlar in telemetrin på var och en av API:erna och justerar begränsningsgränserna dynamiskt.</span><span class="sxs-lookup"><span data-stu-id="923f6-143">Partner Center will be collecting the telemetry on each of the APIs and will dynamically adjust the throttling limits.</span></span> <span data-ttu-id="923f6-144">I följande tabell visas de API:er där begränsningen tillämpas för närvarande.</span><span class="sxs-lookup"><span data-stu-id="923f6-144">The following table lists the APIs where throttling is currently enforced.</span></span>  


|<span data-ttu-id="923f6-145">**Åtgärd**</span><span class="sxs-lookup"><span data-stu-id="923f6-145">**Operation**</span></span>| <span data-ttu-id="923f6-146">**Dokumentation för Partnercenter**</span><span class="sxs-lookup"><span data-stu-id="923f6-146">**Partner Center documentation**</span></span>|
|------------------------|----------------------------|
|<span data-ttu-id="923f6-147">{baseURL}/v1/customers/{customer_id}/orders</span><span class="sxs-lookup"><span data-stu-id="923f6-147">{baseURL}/v1/customers/{customer_id}/orders</span></span>|[<span data-ttu-id="923f6-148">skapa en order</span><span class="sxs-lookup"><span data-stu-id="923f6-148">create an order</span></span>](create-an-order.md)|
|<span data-ttu-id="923f6-149">{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/upgrades</span><span class="sxs-lookup"><span data-stu-id="923f6-149">{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/upgrades</span></span>|[<span data-ttu-id="923f6-150">övergå till en prenumeration</span><span class="sxs-lookup"><span data-stu-id="923f6-150">transition a subscription</span></span>](transition-a-subscription.md)|
|<span data-ttu-id="923f6-151">{baseURL}/v1/customers/{customer-tenant-id}/orders/{order-id}</span><span class="sxs-lookup"><span data-stu-id="923f6-151">{baseURL}/v1/customers/{customer-tenant-id}/orders/{order-id}</span></span>|[<span data-ttu-id="923f6-152">köpa ett tillägg till en prenumeration</span><span class="sxs-lookup"><span data-stu-id="923f6-152">purchase an addon to a subscription</span></span>](purchase-an-add-on-to-a-subscription.md)|
|<span data-ttu-id="923f6-153">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}</span><span class="sxs-lookup"><span data-stu-id="923f6-153">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}</span></span>|[<span data-ttu-id="923f6-154">skapa en kundvagn</span><span class="sxs-lookup"><span data-stu-id="923f6-154">create a cart</span></span>](create-a-cart.md)|
|<span data-ttu-id="923f6-155">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}/checkout</span><span class="sxs-lookup"><span data-stu-id="923f6-155">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}/checkout</span></span>|[<span data-ttu-id="923f6-156">checka ut en kundvagn</span><span class="sxs-lookup"><span data-stu-id="923f6-156">checkout a cart</span></span>](checkout-a-cart.md)|
|<span data-ttu-id="923f6-157">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}</span><span class="sxs-lookup"><span data-stu-id="923f6-157">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}</span></span>|[<span data-ttu-id="923f6-158">uppdatera en kundvagn</span><span class="sxs-lookup"><span data-stu-id="923f6-158">update a cart</span></span>](update-a-cart.md)|
|<span data-ttu-id="923f6-159">{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrations</span><span class="sxs-lookup"><span data-stu-id="923f6-159">{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrations</span></span>|[<span data-ttu-id="923f6-160">registrera en prenumeration</span><span class="sxs-lookup"><span data-stu-id="923f6-160">register a subscription</span></span>](register-a-subscription.md)|
|<span data-ttu-id="923f6-161">{baseURL}/v1/productupgrades</span><span class="sxs-lookup"><span data-stu-id="923f6-161">{baseURL}/v1/productupgrades</span></span>|[<span data-ttu-id="923f6-162">skapa entitet för produktuppgradering</span><span class="sxs-lookup"><span data-stu-id="923f6-162">create product upgrade entity</span></span>](create-product-upgrade-entity.md)|
|<span data-ttu-id="923f6-163">{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions</span><span class="sxs-lookup"><span data-stu-id="923f6-163">{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions</span></span> |[<span data-ttu-id="923f6-164">konvertera en utvärderingsprenumeration till betald</span><span class="sxs-lookup"><span data-stu-id="923f6-164">convert a trial subscription to paid</span></span>](convert-a-trial-subscription-to-paid.md)|
|<span data-ttu-id="923f6-165">{baseURL}/v1/customers/{customer-tenant-id}</span><span class="sxs-lookup"><span data-stu-id="923f6-165">{baseURL}/v1/customers/{customer-tenant-id}</span></span>|[<span data-ttu-id="923f6-166">hämta en kund via ID</span><span class="sxs-lookup"><span data-stu-id="923f6-166">get a customer by id</span></span>](get-a-customer-by-id.md)|
|<span data-ttu-id="923f6-167">{baseURL}/v1/productUpgrades/eligibility</span><span class="sxs-lookup"><span data-stu-id="923f6-167">{baseURL}/v1/productUpgrades/eligibility</span></span>|[<span data-ttu-id="923f6-168">få behörighet för produktuppgradering</span><span class="sxs-lookup"><span data-stu-id="923f6-168">get eligibility for product upgrade</span></span>](get-eligibility-for-product-upgrade.md)|
|<span data-ttu-id="923f6-169">{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}</span><span class="sxs-lookup"><span data-stu-id="923f6-169">{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}</span></span> |[<span data-ttu-id="923f6-170">hantera prenumeration</span><span class="sxs-lookup"><span data-stu-id="923f6-170">manage subscription</span></span>](manage-orders.md#manage-a-subscription)|
|<span data-ttu-id="923f6-171">{baseURL}/v1/customers/{customer_id}/subscriptions</span><span class="sxs-lookup"><span data-stu-id="923f6-171">{baseURL}/v1/customers/{customer_id}/subscriptions</span></span> |[<span data-ttu-id="923f6-172">get-all-of-a-customer-s-subscriptions</span><span class="sxs-lookup"><span data-stu-id="923f6-172">get-all-of-a-customer-s-subscriptions</span></span>](get-all-of-a-customer-s-subscriptions.md)|
|<span data-ttu-id="923f6-173">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}</span><span class="sxs-lookup"><span data-stu-id="923f6-173">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}</span></span>|[<span data-ttu-id="923f6-174">Hämta en prenumeration efter ID</span><span class="sxs-lookup"><span data-stu-id="923f6-174">Get a subscription by ID</span></span>](get-a-subscription-by-id.md)|
|<span data-ttu-id="923f6-175">{baseURL}/v1/customers/{customer_id}/orders</span><span class="sxs-lookup"><span data-stu-id="923f6-175">{baseURL}/v1/customers/{customer_id}/orders</span></span>|[<span data-ttu-id="923f6-176">Hämta alla kundorder</span><span class="sxs-lookup"><span data-stu-id="923f6-176">Get all customer orders</span></span>](get-all-of-a-customer-s-orders.md)|
|<span data-ttu-id="923f6-177">{baseURL}/v1/customers/{customer_id}/orders/{order_id}</span><span class="sxs-lookup"><span data-stu-id="923f6-177">{baseURL}/v1/customers/{customer_id}/orders/{order_id}</span></span>|[<span data-ttu-id="923f6-178">Hämta en beställning efter ID</span><span class="sxs-lookup"><span data-stu-id="923f6-178">Get an order by ID</span></span>](get-an-order-by-id.md)|
|<span data-ttu-id="923f6-179">{baseURL}/v1/customers/{customer_id}/orders/{order_id}/provisioningstatus</span><span class="sxs-lookup"><span data-stu-id="923f6-179">{baseURL}/v1/customers/{customer_id}/orders/{order_id}/provisioningstatus</span></span>|[<span data-ttu-id="923f6-180">Hämta status för prenumerationsetablering</span><span class="sxs-lookup"><span data-stu-id="923f6-180">Get subscription provisioning status</span></span>](get-subscription-provisioning-status.md)|
|<span data-ttu-id="923f6-181">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}</span><span class="sxs-lookup"><span data-stu-id="923f6-181">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}</span></span>|[<span data-ttu-id="923f6-182">Hantera beställningar och hantera en prenumeration</span><span class="sxs-lookup"><span data-stu-id="923f6-182">Manage orders and manage a subscription</span></span>](manage-orders.md#manage-a-subscription)|
|<span data-ttu-id="923f6-183">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/addons</span><span class="sxs-lookup"><span data-stu-id="923f6-183">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/addons</span></span>|[<span data-ttu-id="923f6-184">Hämta en lista över tillägg för en prenumeration</span><span class="sxs-lookup"><span data-stu-id="923f6-184">Get a list of add-ons for a subscription</span></span>](get-a-list-of-add-ons-for-a-subscription.md)|
|<span data-ttu-id="923f6-185">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/azureEntitlements</span><span class="sxs-lookup"><span data-stu-id="923f6-185">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/azureEntitlements</span></span>|[<span data-ttu-id="923f6-186">Hämta en lista över Azure-rättigheter för en prenumeration</span><span class="sxs-lookup"><span data-stu-id="923f6-186">Get a list of Azure entitlements for a subscription</span></span>](get-a-list-of-azure-entitlements-for-subscription.md)|
|<span data-ttu-id="923f6-187">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/registrationstatus</span><span class="sxs-lookup"><span data-stu-id="923f6-187">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/registrationstatus</span></span>|[<span data-ttu-id="923f6-188">Hämta status för prenumerationsregistrering</span><span class="sxs-lookup"><span data-stu-id="923f6-188">Get subscription registration status</span></span>](get-subscription-registration-status.md)|
|<span data-ttu-id="923f6-189">{baseURL}/v1/customers/{customer-tenant-id}/transfers</span><span class="sxs-lookup"><span data-stu-id="923f6-189">{baseURL}/v1/customers/{customer-tenant-id}/transfers</span></span>|[<span data-ttu-id="923f6-190">Hämta alla en kunds överföringar</span><span class="sxs-lookup"><span data-stu-id="923f6-190">Get all of a customer's transfers</span></span>](get-all-of-a-customer-s-transfers.md)|
|<span data-ttu-id="923f6-191">{baseURL}/v1/productUpgrades/{upgrade-id}/status</span><span class="sxs-lookup"><span data-stu-id="923f6-191">{baseURL}/v1/productUpgrades/{upgrade-id}/status</span></span>|[<span data-ttu-id="923f6-192">Hämta status för produktuppgradering</span><span class="sxs-lookup"><span data-stu-id="923f6-192">Get product upgrade status</span></span>](get-product-upgrade-status.md)|
|<span data-ttu-id="923f6-193">{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions</span><span class="sxs-lookup"><span data-stu-id="923f6-193">{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions</span></span>|[<span data-ttu-id="923f6-194">Hämta en lista över erbjudanden för utvärderingskonvertering</span><span class="sxs-lookup"><span data-stu-id="923f6-194">Get a list of trial conversion offers</span></span>](get-a-list-of-trial-conversion-offers.md)|


### <a name="error-code-response"></a><span data-ttu-id="923f6-195">Felkodsvar:</span><span class="sxs-lookup"><span data-stu-id="923f6-195">Error code response:</span></span>
```http
HTTP/1.1 429 Too Many Requests 

Content-Length: 84 

Content-Type: application/json 

Retry-After: 57 

Date: Tue, 21 Jul 2020 04:10:58 GMT 

{ "statusCode": 429, "message": "Rate limit is exceeded. Try again in 57 seconds." } 
```

## <a name="example-of-activity-log"></a><span data-ttu-id="923f6-196">Exempel på aktivitetslogg</span><span class="sxs-lookup"><span data-stu-id="923f6-196">Example of activity log</span></span>

<span data-ttu-id="923f6-197">För bästa praxis vid analys av dagliga ändringar rekommenderar vi att du frågar granskningsposten för en viss dag.</span><span class="sxs-lookup"><span data-stu-id="923f6-197">For best practice in analyzing daily changes, we recommend that you query audit record for a specific day.</span></span> 

<span data-ttu-id="923f6-198">I svaret får du ett resultat med ändringar av den specifika åtgärdstypen.</span><span class="sxs-lookup"><span data-stu-id="923f6-198">In the response, you will get a result with changes to specific operation type.</span></span><span data-ttu-id="923f6-199">Du kan filtrera baserat på den åtgärd du bryr dig om.</span><span class="sxs-lookup"><span data-stu-id="923f6-199">  You can filter based on the operation you care about.</span></span> <span data-ttu-id="923f6-200">Om du till exempel är intresserad av en nyskapad kund kan du titta på operationType = "add_customer".</span><span class="sxs-lookup"><span data-stu-id="923f6-200"> For example, if you are interested in a newly created customer, you can look at operationType = “add_customer”.</span></span>  

<span data-ttu-id="923f6-201">En lista över operationtype/resources finns i API-dokumentationen nedan.</span><span class="sxs-lookup"><span data-stu-id="923f6-201">List of operationtype/resources can be found in below API docs.</span></span>  

- [<span data-ttu-id="923f6-202">Granska resurser</span><span class="sxs-lookup"><span data-stu-id="923f6-202">Auditing resources</span></span>](auditing-resources.md)  

- [<span data-ttu-id="923f6-203">Hämta en post för en PartnerCenter-aktivitet per användare</span><span class="sxs-lookup"><span data-stu-id="923f6-203">Get a record of a Partner Center activity by user</span></span>](get-a-record-of-partner-center-activity-by-user.md)  



### <a name="response-example"></a><span data-ttu-id="923f6-204">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="923f6-204">Response example</span></span>

<span data-ttu-id="923f6-205">**Begäran:**</span><span class="sxs-lookup"><span data-stu-id="923f6-205">**Request**:</span></span>  
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

<span data-ttu-id="923f6-206">**Svar:**</span><span class="sxs-lookup"><span data-stu-id="923f6-206">**Response**:</span></span>    
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
 

