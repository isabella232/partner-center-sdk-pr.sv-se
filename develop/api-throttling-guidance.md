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
# <a name="api-throttling-guidance-for-partners-calling-partner-center-apis"></a>API begränsnings vägledning för partner som anropar API: er för partner Center 

**Gäller för**

- Partnercenter

Microsoft implementerar API-begränsningen för att tillåta mer konsekvent prestanda inom ett tidsintervall för partner som anropar API: er för partner Center. Begränsning begränsar antalet begär anden till en tjänst i ett tidsintervall för att förhindra överanvändning av resurser. Även om Partner Center har utformats för att hantera en stor mängd begär Anden, och om ett överbelastat antal förfrågningar sker av några partner, hjälper begränsningen till att upprätthålla optimala prestanda och tillförlitlighet för alla partner.  

Begränsnings gränserna varierar beroende på scenariot. Om du till exempel utför en stor mängd skrivningar är risken för begränsning högre än om du bara genomför läsningar.

## <a name="what-happens-when-throttling-occurs"></a>Vad händer när en begränsning sker? 

När ett tröskelvärde överskrids begränsar Partner Center eventuella ytterligare förfrågningar från klienten under en viss tids period. Begränsnings beteendet beror på typen och antalet begär Anden.   

### <a name="common-throttling-scenarios"></a>Vanliga begränsnings scenarier 

De vanligaste orsakerna till begränsning av klienter är: 

- **Ett stort antal begär Anden för ett API per partner klient-ID**: för vissa partner Center-API: er bestäms begränsningen av klient organisations-ID: t för många anrop till dessa API: er på samma partner klient-ID, vilket leder till att tröskelvärdet överskrids.  

- **Ett stort antal begär Anden för ett API per partner klient-ID per kund-ID**: för andra API: er bestäms begränsningen av partner klient-ID: t/kund INNEHAVAREns ID-kombination; i dessa fall leder det till att för många anrop till samma kund-ID leder till begränsning medan anrop till andra kunder kan lyckas.

## <a name="best-practices-to-avoid-throttling"></a>Metod tips för att undvika begränsning 
 
Programmerings metoder, till exempel kontinuerlig avsökning av en resurs, för att söka efter uppdateringar och regelbundet genomsöka resurs samlingar för att söka efter nya eller borttagna resurser är mer sannolika att begränsas och försämrar övergripande prestanda. Samtidiga API-anrop kan leda till ett stort antal begär Anden per enhets tid, vilket även kan orsaka att förfrågningar begränsas. I stället bör du använda ändrings spårning och ändrings meddelanden. Dessutom bör du kunna använda aktivitets loggar för att identifiera ändringar, se [aktivitets loggar för partner Center](get-a-record-of-partner-center-activity-by-user.md) för mer information.  Vi rekommenderar starkt att du använder API: et för aktivitets loggen för att få mer effektivitet och undvika begränsning. Se även exemplet på att använda aktivitets loggar nedan.

## <a name="best-practices-to-handle-throttling"></a>Metod tips för att hantera begränsning

Följande är metod tips för hantering av begränsning: 

- Minska graden av parallellitet. 
- Minska frekvensen för anrop. 
- Undvik omedelbara återförsök eftersom alla förfrågningar påförs mot dina användnings gränser. 

När du implementerar felhantering använder du HTTP-felkoden 429 för att identifiera begränsning. Det misslyckade svaret innehåller Retry-After svars huvudet. Att säkerhetskopiera begär Anden med hjälp av återförsök-efter fördröjning är det snabbaste sättet att återställa från begränsning. 

Om du vill använda ett nytt försök efter fördröjningen gör du följande: 

1. Vänta antalet sekunder som anges i Retry-Afters huvudet. 

2. Gör om begäran.  

3. Om begäran Miss lyckas med en 429-felkod är du fortfarande begränsad. Försök igen med exponentiell backoff, Använd den rekommenderade Retry-After fördröjningen och gör om begäran tills den lyckas.

4. Om du använder SDK får du ett undantag med status kod 429 när din begäran begränsas. Använd egenskapen RetryAfter i undantags processen och försök igen när tiden har gått ut.


## <a name="apis-currently-impacted-by-throttling"></a>API: er som påverkas av begränsning

I den långa körningen begränsas alla API: er för enskild partner Center som anropar slut punkten "api.partnercenter.microsoft.com/". För närvarande tillämpas begränsnings gränserna bara på de få API: erna som anges nedan. Partner Center samlar in Telemetrin för alla API: er och justerar gränserna för begränsningen dynamiskt. I följande tabell visas de API: er där begränsningen för närvarande tillämpas.  


|**Åtgärd**| **Dokumentation för Partnercenter**|       
|------------------------|----------------------------|
|{baseURL}/v1/Customers/{customer_id}/Orders|[skapa en order](create-an-order.md)|
|{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/upgrades|[över gång till en prenumeration](transition-a-subscription.md)|
|{baseURL}/v1/customers/{customer-tenant-id}/orders/{order-id}|[Köp ett tillägg till en prenumeration](purchase-an-add-on-to-a-subscription.md)|
|{baseURL}/v1/customers/{customer-id}/carts/{cart-id}|[skapa en kundvagn](create-a-cart.md)|
|{baseURL}/v1/customers/{customer-id}/carts/{cart-id}/checkout|[checka ut en varukorg](checkout-a-cart.md)|
|{baseURL}/v1/customers/{customer-id}/carts/{cart-id}|[uppdatera en varukorg](update-a-cart.md)|
|{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrations|[registrera en prenumeration](register-a-subscription.md)|
|{baseURL}/v1/productupgrades|[skapa produkt uppgraderings enhet](create-product-upgrade-entity.md)|
|{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions |[konvertera en utvärderings prenumeration till betald](convert-a-trial-subscription-to-paid.md)|
|{baseURL}/v1/customers/{customer-tenant-id}|[Hämta en kund efter ID](get-a-customer-by-id.md)|
|{baseURL}/v1/productUpgrades/eligibility|[Hämta berättigande för produkt uppgradering](get-eligibility-for-product-upgrade.md)|
|{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} |[hantera prenumeration](manage-orders.md#manage-a-subscription)|


### <a name="error-code-response"></a>Fel kod svar:
```http
HTTP/1.1 429 Too Many Requests 

Content-Length: 84 

Content-Type: application/json 

Retry-After: 57 

Date: Tue, 21 Jul 2020 04:10:58 GMT 

{ "statusCode": 429, "message": "Rate limit is exceeded. Try again in 57 seconds." } 
```

## <a name="example-of-activity-log"></a>Exempel på aktivitets logg

För bästa praxis när du analyserar dagliga ändringar, rekommenderar vi att du söker efter en speciell dag i gransknings posten. 

I svaret får du ett resultat av ändringar i en speciell åtgärds typ.Du kan filtrera baserat på den åtgärd du bryr dig om. Om du till exempel är intresse rad av en nyligen skapad kund kan du titta på operationType = "add_customer".  

Lista över OperationType/-resurser finns i nedanstående API-dokument.  

- [Granska resurser](auditing-resources.md)  

- [Hämta en post för en partner Center-aktivitet per användare](get-a-record-of-partner-center-activity-by-user.md)  



### <a name="response-example"></a>Exempel på svar

**Begäran**:  
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

**Svar**:    
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
 

