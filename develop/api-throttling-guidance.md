---
title: Vägledning för API-begränsning
description: 'För partner som anropar API: er för partner Center, lär dig vilka API: er som påverkas av Microsoft API-begränsning och metod tips för att undvika eller bättre hantera begränsning.'
ms.date: 09/09/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: vijvala
ms.author: vijvala
ms.openlocfilehash: a52751a97e699050075c1aac910cc51e94514f26
ms.sourcegitcommit: 01e75175077611da92175c777a440a594fb05797
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/08/2020
ms.locfileid: "97770233"
---
# <a name="api-throttling-guidance-for-partners-calling-partner-center-apis"></a><span data-ttu-id="62bbb-103">API begränsnings vägledning för partner som anropar API: er för partner Center</span><span class="sxs-lookup"><span data-stu-id="62bbb-103">API throttling guidance for partners calling Partner Center APIs</span></span> 

<span data-ttu-id="62bbb-104">**Gäller för**</span><span class="sxs-lookup"><span data-stu-id="62bbb-104">**Applies to**</span></span>

- <span data-ttu-id="62bbb-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="62bbb-105">Partner Center</span></span>

<span data-ttu-id="62bbb-106">Microsoft implementerar API-begränsningen för att tillåta mer konsekvent prestanda inom ett tidsintervall för partner som anropar API: er för partner Center.</span><span class="sxs-lookup"><span data-stu-id="62bbb-106">Microsoft is implementing API throttling to allow more consistent performance within a time span for partners calling the Partner Center APIs.</span></span> <span data-ttu-id="62bbb-107">Begränsning begränsar antalet begär anden till en tjänst i ett tidsintervall för att förhindra överanvändning av resurser.</span><span class="sxs-lookup"><span data-stu-id="62bbb-107">Throttling limits the number of requests to a service in a time span to prevent overuse of resources.</span></span> <span data-ttu-id="62bbb-108">Även om Partner Center har utformats för att hantera en stor mängd begär Anden, och om ett överbelastat antal förfrågningar sker av några partner, hjälper begränsningen till att upprätthålla optimala prestanda och tillförlitlighet för alla partner.</span><span class="sxs-lookup"><span data-stu-id="62bbb-108">While Partner Center is designed to handle a high volume of requests, if an overwhelming number of requests occur by few partners, throttling helps maintain optimal performance and reliability for all partners.</span></span>  

<span data-ttu-id="62bbb-109">Begränsnings gränserna varierar beroende på scenariot.</span><span class="sxs-lookup"><span data-stu-id="62bbb-109">Throttling limits vary based on the scenario.</span></span> <span data-ttu-id="62bbb-110">Om du till exempel utför en stor mängd skrivningar är risken för begränsning högre än om du bara genomför läsningar.</span><span class="sxs-lookup"><span data-stu-id="62bbb-110">For example, if you are performing a large volume of writes, the possibility for throttling is higher than if you are only performing reads.</span></span>

## <a name="what-happens-when-throttling-occurs"></a><span data-ttu-id="62bbb-111">Vad händer när en begränsning sker?</span><span class="sxs-lookup"><span data-stu-id="62bbb-111">What happens when throttling occurs?</span></span> 

<span data-ttu-id="62bbb-112">När ett tröskelvärde överskrids begränsar Partner Center eventuella ytterligare förfrågningar från klienten under en viss tids period.</span><span class="sxs-lookup"><span data-stu-id="62bbb-112">When a throttling threshold is exceeded, Partner Center limits any further requests from that client for a period of time.</span></span> <span data-ttu-id="62bbb-113">Begränsnings beteendet beror på typen och antalet begär Anden.</span><span class="sxs-lookup"><span data-stu-id="62bbb-113">Throttling behavior depends on the type and number of requests.</span></span>   

### <a name="common-throttling-scenarios"></a><span data-ttu-id="62bbb-114">Vanliga begränsnings scenarier</span><span class="sxs-lookup"><span data-stu-id="62bbb-114">Common throttling scenarios</span></span> 

<span data-ttu-id="62bbb-115">De vanligaste orsakerna till begränsning av klienter är:</span><span class="sxs-lookup"><span data-stu-id="62bbb-115">The most common causes of throttling of clients include:</span></span> 

- <span data-ttu-id="62bbb-116">**Ett stort antal begär Anden för ett API per partner klient-ID**: för vissa partner Center-API: er bestäms begränsningen av klient organisations-ID: t för många anrop till dessa API: er på samma partner klient-ID, vilket leder till att tröskelvärdet överskrids.</span><span class="sxs-lookup"><span data-stu-id="62bbb-116">**A large number of requests for an API per Partner Tenant ID**: for some Partner Center APIs, throttling is determined by Partner Tenant ID, too many calls to those APIs on the same Partner Tenant ID will result in exceeding the throttling threshold.</span></span>  

- <span data-ttu-id="62bbb-117">**Ett stort antal begär Anden för ett API per partner klient-ID per kund-ID**: för andra API: er bestäms begränsningen av partner klient-ID: t/kund INNEHAVAREns ID-kombination; i dessa fall leder det till att för många anrop till samma kund-ID leder till begränsning medan anrop till andra kunder kan lyckas.</span><span class="sxs-lookup"><span data-stu-id="62bbb-117">**A large number of requests for an API per Partner Tenant ID per Customer Tenant ID**: for other APIs, throttling is determined by Partner Tenant ID/Customer Tenant ID combination; in those cases, making too many calls against the same customer tenant ID will result in throttling - while calls against other customers may succeed.</span></span>

## <a name="best-practices-to-avoid-throttling"></a><span data-ttu-id="62bbb-118">Metod tips för att undvika begränsning</span><span class="sxs-lookup"><span data-stu-id="62bbb-118">Best practices to avoid throttling</span></span> 
 
<span data-ttu-id="62bbb-119">Programmerings metoder, till exempel kontinuerlig avsökning av en resurs, för att söka efter uppdateringar och regelbundet genomsöka resurs samlingar för att söka efter nya eller borttagna resurser är mer sannolika att begränsas och försämrar övergripande prestanda.</span><span class="sxs-lookup"><span data-stu-id="62bbb-119">Programming practices such as continuously polling a resource to check for updates and regularly scanning resource collections to check for new or deleted resources are more likely to lead to throttling and will degrade overall performance.</span></span> <span data-ttu-id="62bbb-120">Samtidiga API-anrop kan leda till ett stort antal begär Anden per enhets tid, vilket även kan orsaka att förfrågningar begränsas.</span><span class="sxs-lookup"><span data-stu-id="62bbb-120">Concurrent API calls may lead to high number of requests per unit time, which will also cause requests to be throttled.</span></span> <span data-ttu-id="62bbb-121">I stället bör du använda ändrings spårning och ändrings meddelanden.</span><span class="sxs-lookup"><span data-stu-id="62bbb-121">You should instead leverage change tracking and change notifications.</span></span> <span data-ttu-id="62bbb-122">Dessutom bör du kunna använda aktivitets loggar för att identifiera ändringar, se [aktivitets loggar för partner Center](get-a-record-of-partner-center-activity-by-user.md) för mer information.</span><span class="sxs-lookup"><span data-stu-id="62bbb-122">Additionally, you should be able to leverage activity logs for detecting changes, see [Partner Center activity logs](get-a-record-of-partner-center-activity-by-user.md) for more information.</span></span>  <span data-ttu-id="62bbb-123">Vi rekommenderar starkt att du använder API: et för aktivitets loggen för att få mer effektivitet och undvika begränsning.</span><span class="sxs-lookup"><span data-stu-id="62bbb-123">We highly recommend partners to consider using the activity log API for more efficiency and to avoid throttling.</span></span> <span data-ttu-id="62bbb-124">Se även exemplet på att använda aktivitets loggar nedan.</span><span class="sxs-lookup"><span data-stu-id="62bbb-124">See also the example of using activity logs, below.</span></span>

## <a name="best-practices-to-handle-throttling"></a><span data-ttu-id="62bbb-125">Metod tips för att hantera begränsning</span><span class="sxs-lookup"><span data-stu-id="62bbb-125">Best practices to handle throttling</span></span>

<span data-ttu-id="62bbb-126">Följande är metod tips för hantering av begränsning:</span><span class="sxs-lookup"><span data-stu-id="62bbb-126">The following are best practices for handling throttling:</span></span> 

- <span data-ttu-id="62bbb-127">Minska graden av parallellitet.</span><span class="sxs-lookup"><span data-stu-id="62bbb-127">Reduce the degree of parallelism.</span></span> 
- <span data-ttu-id="62bbb-128">Minska frekvensen för anrop.</span><span class="sxs-lookup"><span data-stu-id="62bbb-128">Reduce the frequency of calls.</span></span> 
- <span data-ttu-id="62bbb-129">Undvik omedelbara återförsök eftersom alla förfrågningar påförs mot dina användnings gränser.</span><span class="sxs-lookup"><span data-stu-id="62bbb-129">Avoid immediate retries because all requests accrue against your usage limits.</span></span> 

<span data-ttu-id="62bbb-130">När du implementerar felhantering använder du HTTP-felkoden 429 för att identifiera begränsning.</span><span class="sxs-lookup"><span data-stu-id="62bbb-130">When you implement error handling, use the HTTP error code 429 to detect throttling.</span></span> <span data-ttu-id="62bbb-131">Det misslyckade svaret innehåller Retry-After svars huvudet.</span><span class="sxs-lookup"><span data-stu-id="62bbb-131">The failed response includes the Retry-After response header.</span></span> <span data-ttu-id="62bbb-132">Att säkerhetskopiera begär Anden med hjälp av återförsök-efter fördröjning är det snabbaste sättet att återställa från begränsning.</span><span class="sxs-lookup"><span data-stu-id="62bbb-132">Backing off requests using the Retry-after delay is the fastest way to recover from throttling.</span></span> 

<span data-ttu-id="62bbb-133">Om du vill använda ett nytt försök efter fördröjningen gör du följande:</span><span class="sxs-lookup"><span data-stu-id="62bbb-133">To use the Retry-after delay, do the following:</span></span> 

1. <span data-ttu-id="62bbb-134">Vänta antalet sekunder som anges i Retry-Afters huvudet.</span><span class="sxs-lookup"><span data-stu-id="62bbb-134">Wait the number of seconds specified in the Retry-After header.</span></span> 

2. <span data-ttu-id="62bbb-135">Gör om begäran.</span><span class="sxs-lookup"><span data-stu-id="62bbb-135">Retry the request.</span></span>  

3. <span data-ttu-id="62bbb-136">Om begäran Miss lyckas med en 429-felkod är du fortfarande begränsad.</span><span class="sxs-lookup"><span data-stu-id="62bbb-136">If the request fails again with a 429 error code, you are still being throttled.</span></span> <span data-ttu-id="62bbb-137">Försök igen med exponentiell backoff, Använd den rekommenderade Retry-After fördröjningen och gör om begäran tills den lyckas.</span><span class="sxs-lookup"><span data-stu-id="62bbb-137">Retry with Exponential backoff, use the recommended Retry-After delay and retry the request until it succeeds.</span></span>

4. <span data-ttu-id="62bbb-138">Om du använder SDK får du ett undantag med status kod 429 när din begäran begränsas.</span><span class="sxs-lookup"><span data-stu-id="62bbb-138">If you are using SDK you'll receive an exception with status code 429 when your request is being throttled.</span></span> <span data-ttu-id="62bbb-139">Använd egenskapen RetryAfter i undantags processen och försök igen när tiden har gått ut.</span><span class="sxs-lookup"><span data-stu-id="62bbb-139">Use the RetryAfter property in the exception and retry the request after the time is elapsed.</span></span>


## <a name="apis-currently-impacted-by-throttling"></a><span data-ttu-id="62bbb-140">API: er som påverkas av begränsning</span><span class="sxs-lookup"><span data-stu-id="62bbb-140">APIs currently impacted by throttling</span></span>

<span data-ttu-id="62bbb-141">I den långa körningen begränsas alla API: er för enskild partner Center som anropar slut punkten "api.partnercenter.microsoft.com/".</span><span class="sxs-lookup"><span data-stu-id="62bbb-141">In the long run, every single Partner Center API that calls the endpoint “api.partnercenter.microsoft.com/” will be throttled.</span></span> <span data-ttu-id="62bbb-142">För närvarande tillämpas begränsnings gränserna bara på de få API: erna som anges nedan.</span><span class="sxs-lookup"><span data-stu-id="62bbb-142">Currently, the throttling limits are only enforced on the few APIs listed below.</span></span> <span data-ttu-id="62bbb-143">Partner Center samlar in Telemetrin för alla API: er och justerar gränserna för begränsningen dynamiskt.</span><span class="sxs-lookup"><span data-stu-id="62bbb-143">Partner Center will be collecting the telemetry on each of the APIs and will dynamically adjust the throttling limits.</span></span> <span data-ttu-id="62bbb-144">I följande tabell visas de API: er där begränsningen för närvarande tillämpas.</span><span class="sxs-lookup"><span data-stu-id="62bbb-144">The following table lists the APIs where throttling is currently enforced.</span></span>  


|<span data-ttu-id="62bbb-145">**Åtgärd**</span><span class="sxs-lookup"><span data-stu-id="62bbb-145">**Operation**</span></span>| <span data-ttu-id="62bbb-146">**Dokumentation för Partnercenter**</span><span class="sxs-lookup"><span data-stu-id="62bbb-146">**Partner Center documentation**</span></span>|       
|------------------------|----------------------------|
|<span data-ttu-id="62bbb-147">{baseURL}/v1/Customers/{customer_id}/Orders</span><span class="sxs-lookup"><span data-stu-id="62bbb-147">{baseURL}/v1/customers/{customer_id}/orders</span></span>|[<span data-ttu-id="62bbb-148">skapa en order</span><span class="sxs-lookup"><span data-stu-id="62bbb-148">create an order</span></span>](create-an-order.md)|
|<span data-ttu-id="62bbb-149">{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/upgrades</span><span class="sxs-lookup"><span data-stu-id="62bbb-149">{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/upgrades</span></span>|[<span data-ttu-id="62bbb-150">över gång till en prenumeration</span><span class="sxs-lookup"><span data-stu-id="62bbb-150">transition a subscription</span></span>](transition-a-subscription.md)|
|<span data-ttu-id="62bbb-151">{baseURL}/v1/customers/{customer-tenant-id}/orders/{order-id}</span><span class="sxs-lookup"><span data-stu-id="62bbb-151">{baseURL}/v1/customers/{customer-tenant-id}/orders/{order-id}</span></span>|[<span data-ttu-id="62bbb-152">Köp ett tillägg till en prenumeration</span><span class="sxs-lookup"><span data-stu-id="62bbb-152">purchase an addon to a subscription</span></span>](purchase-an-add-on-to-a-subscription.md)|
|<span data-ttu-id="62bbb-153">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}</span><span class="sxs-lookup"><span data-stu-id="62bbb-153">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}</span></span>|[<span data-ttu-id="62bbb-154">skapa en kundvagn</span><span class="sxs-lookup"><span data-stu-id="62bbb-154">create a cart</span></span>](create-a-cart.md)|
|<span data-ttu-id="62bbb-155">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}/checkout</span><span class="sxs-lookup"><span data-stu-id="62bbb-155">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}/checkout</span></span>|[<span data-ttu-id="62bbb-156">checka ut en varukorg</span><span class="sxs-lookup"><span data-stu-id="62bbb-156">checkout a cart</span></span>](checkout-a-cart.md)|
|<span data-ttu-id="62bbb-157">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}</span><span class="sxs-lookup"><span data-stu-id="62bbb-157">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}</span></span>|[<span data-ttu-id="62bbb-158">uppdatera en varukorg</span><span class="sxs-lookup"><span data-stu-id="62bbb-158">update a cart</span></span>](update-a-cart.md)|
|<span data-ttu-id="62bbb-159">{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrations</span><span class="sxs-lookup"><span data-stu-id="62bbb-159">{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrations</span></span>|[<span data-ttu-id="62bbb-160">registrera en prenumeration</span><span class="sxs-lookup"><span data-stu-id="62bbb-160">register a subscription</span></span>](register-a-subscription.md)|
|<span data-ttu-id="62bbb-161">{baseURL}/v1/productupgrades</span><span class="sxs-lookup"><span data-stu-id="62bbb-161">{baseURL}/v1/productupgrades</span></span>|[<span data-ttu-id="62bbb-162">skapa produkt uppgraderings enhet</span><span class="sxs-lookup"><span data-stu-id="62bbb-162">create product upgrade entity</span></span>](create-product-upgrade-entity.md)|
|<span data-ttu-id="62bbb-163">{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions</span><span class="sxs-lookup"><span data-stu-id="62bbb-163">{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions</span></span> |[<span data-ttu-id="62bbb-164">konvertera en utvärderings prenumeration till betald</span><span class="sxs-lookup"><span data-stu-id="62bbb-164">convert a trial subscription to paid</span></span>](convert-a-trial-subscription-to-paid.md)|
|<span data-ttu-id="62bbb-165">{baseURL}/v1/customers/{customer-tenant-id}</span><span class="sxs-lookup"><span data-stu-id="62bbb-165">{baseURL}/v1/customers/{customer-tenant-id}</span></span>|[<span data-ttu-id="62bbb-166">Hämta en kund efter ID</span><span class="sxs-lookup"><span data-stu-id="62bbb-166">get a customer by id</span></span>](get-a-customer-by-id.md)|
|<span data-ttu-id="62bbb-167">{baseURL}/v1/productUpgrades/eligibility</span><span class="sxs-lookup"><span data-stu-id="62bbb-167">{baseURL}/v1/productUpgrades/eligibility</span></span>|[<span data-ttu-id="62bbb-168">Hämta berättigande för produkt uppgradering</span><span class="sxs-lookup"><span data-stu-id="62bbb-168">get eligibility for product upgrade</span></span>](get-eligibility-for-product-upgrade.md)|
|<span data-ttu-id="62bbb-169">{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}</span><span class="sxs-lookup"><span data-stu-id="62bbb-169">{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}</span></span> |[<span data-ttu-id="62bbb-170">hantera prenumeration</span><span class="sxs-lookup"><span data-stu-id="62bbb-170">manage subscription</span></span>](manage-orders.md#manage-a-subscription)|


### <a name="error-code-response"></a><span data-ttu-id="62bbb-171">Fel kod svar:</span><span class="sxs-lookup"><span data-stu-id="62bbb-171">Error code response:</span></span>
```http
HTTP/1.1 429 Too Many Requests 

Content-Length: 84 

Content-Type: application/json 

Retry-After: 57 

Date: Tue, 21 Jul 2020 04:10:58 GMT 

{ "statusCode": 429, "message": "Rate limit is exceeded. Try again in 57 seconds." } 
```

## <a name="example-of-activity-log"></a><span data-ttu-id="62bbb-172">Exempel på aktivitets logg</span><span class="sxs-lookup"><span data-stu-id="62bbb-172">Example of activity log</span></span>

<span data-ttu-id="62bbb-173">För bästa praxis när du analyserar dagliga ändringar, rekommenderar vi att du söker efter en speciell dag i gransknings posten.</span><span class="sxs-lookup"><span data-stu-id="62bbb-173">For best practice in analyzing daily changes, we recommend that you query audit record for a specific day.</span></span> 

<span data-ttu-id="62bbb-174">I svaret får du ett resultat av ändringar i en speciell åtgärds typ.</span><span class="sxs-lookup"><span data-stu-id="62bbb-174">In the response, you will get a result with changes to specific operation type.</span></span><span data-ttu-id="62bbb-175">Du kan filtrera baserat på den åtgärd du bryr dig om.</span><span class="sxs-lookup"><span data-stu-id="62bbb-175">  You can filter based on the operation you care about.</span></span> <span data-ttu-id="62bbb-176">Om du till exempel är intresse rad av en nyligen skapad kund kan du titta på operationType = "add_customer".</span><span class="sxs-lookup"><span data-stu-id="62bbb-176"> For example, if you are interested in a newly created customer, you can look at operationType = “add_customer”.</span></span>  

<span data-ttu-id="62bbb-177">Lista över OperationType/-resurser finns i nedanstående API-dokument.</span><span class="sxs-lookup"><span data-stu-id="62bbb-177">List of operationtype/resources can be found in below API docs.</span></span>  

- [<span data-ttu-id="62bbb-178">Granska resurser</span><span class="sxs-lookup"><span data-stu-id="62bbb-178">Auditing resources</span></span>](auditing-resources.md)  

- [<span data-ttu-id="62bbb-179">Hämta en post för en partner Center-aktivitet per användare</span><span class="sxs-lookup"><span data-stu-id="62bbb-179">Get a record of a Partner Center activity by user</span></span>](get-a-record-of-partner-center-activity-by-user.md)  



### <a name="response-example"></a><span data-ttu-id="62bbb-180">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="62bbb-180">Response example</span></span>

<span data-ttu-id="62bbb-181">**Begäran**:</span><span class="sxs-lookup"><span data-stu-id="62bbb-181">**Request**:</span></span>  
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

<span data-ttu-id="62bbb-182">**Svar**:</span><span class="sxs-lookup"><span data-stu-id="62bbb-182">**Response**:</span></span>    
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
 

