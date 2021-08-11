---
title: Vägledning för API-begränsning
description: För partner som anropar Partner Center-API:er kan du lära dig vilka API:er som påverkas av Microsoft API-begränsning och metodtips för att undvika eller bättre hantera begränsningar.
ms.date: 04/14/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: vijvala
ms.author: vijvala
ms.openlocfilehash: 4eead16c5bb2b01f0fba85e30ea35fbcdae9d5a6682872eecfeeb9e47f43d324
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115993766"
---
# <a name="api-throttling-guidance-for-partners-calling-partner-center-apis"></a>Api-begränsningsvägledning för partner som anropar Partner Center-API:er 

Microsoft implementerar API-begränsning för att tillåta mer konsekventa prestanda inom ett tidsintervall för partner som anropar Partner Center-API:erna. Begränsning begränsar antalet begäranden till en tjänst under ett tidsintervall för att förhindra överanvändning av resurser. Partner Center är utformat för att hantera ett stort antal begäranden, men om ett stort antal begäranden inträffar av få partner hjälper begränsningen till att upprätthålla optimala prestanda och tillförlitlighet för alla partner.  

Begränsningsgränserna varierar beroende på scenariot. Om du till exempel utför en stor mängd skrivningar är risken för begränsning högre än om du bara utför läsningar.

## <a name="what-happens-when-throttling-occurs"></a>Vad händer när begränsning inträffar? 

När ett tröskelvärde för begränsning överskrids begränsar Partnercenter eventuella ytterligare begäranden från klienten under en viss tidsperiod. Begränsningsbeteendet beror på typen och antalet begäranden.   

### <a name="common-throttling-scenarios"></a>Vanliga begränsningsscenarier 

De vanligaste orsakerna till begränsning av klienter är: 

- Ett stort antal begäranden för ett **API per partnerklientorganisations-ID:** för vissa Partner Center-API:er bestäms begränsningen av partnerklient-ID. För många anrop till dessa API:er på samma partnerklientorganisations-ID resulterar i att tröskelvärdet för begränsning överskrids.  

- Ett stort antal begäranden för ett **API per partnerklientorganisations-ID per kundklientorganisations-ID:** för andra API:er bestäms begränsningen av kombinationen partnerklient-ID/kundklientorganisations-ID. I dessa fall resulterar för många anrop mot samma kundklientorganisations-ID i begränsningen , medan anrop mot andra kunder kan lyckas.

## <a name="best-practices-to-avoid-throttling"></a>Metodtips för att undvika begränsning 
 
Programmeringsmetoder som att kontinuerligt söka av en resurs för att söka efter uppdateringar och regelbundet genomskanna resurssamlingar för att söka efter nya eller borttagna resurser leder mer sannolikt till begränsning och försämrar den övergripande prestandan. Samtidiga API-anrop kan leda till ett stort antal begäranden per enhetstid, vilket också gör att begäranden begränsas. Du bör i stället använda ändringsspårning och ändringsmeddelanden. Dessutom bör du kunna använda aktivitetsloggar för att identifiera ändringar. Mer information finns i [Aktivitetsloggar i Partnercenter.](get-a-record-of-partner-center-activity-by-user.md)  Vi rekommenderar starkt att partner överväger att använda aktivitetslogg-API:et för att öka effektiviteten och undvika begränsning. Se även exemplet med att använda aktivitetsloggar nedan.

## <a name="best-practices-to-handle-throttling"></a>Metodtips för att hantera begränsning

Följande är metodtips för hantering av begränsning: 

- Minska graden av parallellitet. 
- Minska frekvensen för anrop. 
- Undvik omedelbara återförsök eftersom alla begäranden ackumuleras mot dina användningsgränser. 

När du implementerar felhantering använder du HTTP-felkoden 429 för att identifiera begränsning. Det misslyckade svaret innehåller Retry-After svarshuvudet. Det snabbaste sättet att återställa från begränsning är att backa bort begäranden med hjälp av fördröjningen Försök igen. 

Om du vill använda retry-after-fördröjningen gör du följande: 

1. Vänta det antal sekunder som anges i Retry-After sidhuvud. 

2. Försök att skicka begäran igen.  

3. Om begäran misslyckas igen med felkoden 429 begränsas du fortfarande. Försök igen med exponentiell backoff, använd den rekommenderade Retry-After och försök igen tills den lyckas.

4. Om du använder SDK:n får du ett undantag med statuskod 429 när din begäran begränsas. Använd egenskapen RetryAfter i undantaget och försök igen när tiden har gått ut.


## <a name="apis-currently-impacted-by-throttling"></a>API:er som för närvarande påverkas av begränsning

I slutändan kommer varje partnercenter-API som anropar slutpunkten "api.partnercenter.microsoft.com/" att begränsas. För närvarande tillämpas begränsningsgränserna endast på de API:er som anges nedan. Partner Center samlar in telemetrin på vart och ett av API:erna och justerar begränsningsgränserna dynamiskt. I följande tabell visas de API:er där begränsningen tillämpas för närvarande.  


|**Åtgärd**| **Dokumentation för Partnercenter**|
|------------------------|----------------------------|
|{baseURL}/v1/customers/{customer_id}/orders|[skapa en order](create-an-order.md)|
|{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/upgrades|[övergå till en prenumeration](transition-a-subscription.md)|
|{baseURL}/v1/customers/{customer-tenant-id}/orders/{order-id}|[köpa ett tillägg till en prenumeration](purchase-an-add-on-to-a-subscription.md)|
|{baseURL}/v1/customers/{customer-id}/carts/{cart-id}|[skapa en kundvagn](create-a-cart.md)|
|{baseURL}/v1/customers/{customer-id}/carts/{cart-id}/checkout|[checka ut en kundvagn](checkout-a-cart.md)|
|{baseURL}/v1/customers/{customer-id}/carts/{cart-id}|[uppdatera en kundvagn](update-a-cart.md)|
|{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrations|[registrera en prenumeration](register-a-subscription.md)|
|{baseURL}/v1/productupgrades|[skapa entitet för produktuppgradering](create-product-upgrade-entity.md)|
|{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions |[konvertera en utvärderingsprenumeration till betald](convert-a-trial-subscription-to-paid.md)|
|{baseURL}/v1/customers/{customer-tenant-id}|[hämta en kund efter ID](get-a-customer-by-id.md)|
|{baseURL}/v1/productUpgrades/eligibility|[få behörighet för produktuppgradering](get-eligibility-for-product-upgrade.md)|
|{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} |[hantera prenumeration](manage-orders.md#manage-a-subscription)|
|{baseURL}/v1/customers/{customer_id}/subscriptions |[get-all-of-a-customer-s-subscriptions](get-all-of-a-customer-s-subscriptions.md)|
|{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}|[Hämta en prenumeration efter ID](get-a-subscription-by-id.md)|
|{baseURL}/v1/customers/{customer_id}/orders|[Hämta alla kundbeställningar](get-all-of-a-customer-s-orders.md)|
|{baseURL}/v1/customers/{customer_id}/orders/{order_id}|[Hämta en beställning efter ID](get-an-order-by-id.md)|
|{baseURL}/v1/customers/{customer_id}/orders/{order_id}/provisioningstatus|[Hämta status för prenumerationsetablering](get-subscription-provisioning-status.md)|
|{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}|[Hantera beställningar och hantera en prenumeration](manage-orders.md#manage-a-subscription)|
|{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/addons|[Hämta en lista över tillägg för en prenumeration](get-a-list-of-add-ons-for-a-subscription.md)|
|{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/azureEntitlements|[Hämta en lista över Azure-rättigheter för en prenumeration](get-a-list-of-azure-entitlements-for-subscription.md)|
|{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/registrationstatus|[Hämta status för prenumerationsregistrering](get-subscription-registration-status.md)|
|{baseURL}/v1/customers/{customer-tenant-id}/transfers|[Hämta alla en kunds överföringar](get-all-of-a-customer-s-transfers.md)|
|{baseURL}/v1/productUpgrades/{upgrade-id}/status|[Hämta status för produktuppgradering](get-product-upgrade-status.md)|
|{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions|[Hämta en lista över erbjudanden för utvärderingskonvertering](get-a-list-of-trial-conversion-offers.md)|


### <a name="error-code-response"></a>Felkodsvar:
```http
HTTP/1.1 429 Too Many Requests 

Content-Length: 84 

Content-Type: application/json 

Retry-After: 57 

Date: Tue, 21 Jul 2020 04:10:58 GMT 

{ "statusCode": 429, "message": "Rate limit is exceeded. Try again in 57 seconds." } 
```

## <a name="example-of-activity-log"></a>Exempel på aktivitetslogg

För bästa praxis vid analys av dagliga ändringar rekommenderar vi att du frågar granskningsposten för en viss dag. 

I svaret får du ett resultat med ändringar av den specifika åtgärdstypen.Du kan filtrera baserat på den åtgärd du bryr dig om. Om du till exempel är intresserad av en nyskapad kund kan du titta på operationType = "add_customer".  

En lista över operationtype/resources finns i API-dokumentationen nedan.  

- [Granskningsresurser](auditing-resources.md)  

- [Hämta en post för en PartnerCenter-aktivitet per användare](get-a-record-of-partner-center-activity-by-user.md)  



### <a name="response-example"></a>Exempel på svar

**Begäran:**  
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

**Svar:**    
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
 

