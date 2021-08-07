---
title: Viktig information om Partner Center .NET SDK
description: Viktig information om den senaste versionen av Partner Center .NET SDK.
ms.date: 07/07/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6fc6182638cb2cc5457bdfada37b928c88e1ca786e401f7eb8d5309a0abd9310
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991232"
---
# <a name="net-sdk-release-notes"></a>Information om .NET SDK

Följande viktig information är tillgänglig för nya versioner av [Microsoft Partner Center .NET SDK.](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter) Du hittar [.NET SDK-exempel](https://github.com/Microsoft/Partner-Center-DotNet-Samples) på GitHub. Du hittar [.NET API-referensen för Partner Center](/dotnet/api/?view=partnercenter-dotnet-latest&preserve-view=true) i .NET API-webbläsaren.

## <a name="version-201"></a>Version 2.0.1

[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/2.0.1) v2.0.1 är nu allmänt tillgängligt. Uppdaterade [GitHub exempel](https://github.com/Microsoft/Partner-Center-DotNet-Samples) är också tillgängliga. Följande ändringar ingår i den här versionen:

> [!NOTE]
> Några av ändringarna introducerades som en del av NCE (New Commerce Experiences) som för närvarande är tillgängliga baserat på inbjudan till partner som ingår i den tekniska förhandsversionen av den nya handelsupplevelsen M365/D365. Partner som inte är en del av den privata förhandsversionen av ny handel bör inte märka påverkan och bör vara bakåtkompatibla.

### <a name="common"></a>Common
* Ändra referensen till autentiseringsbiblioteket – Referensen ändras från Azure Active Directory Authentication Library[(ADAL)](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet)till Microsoft Authentication Library[(MSAL)](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet)

  Följande ändringar bör göras för att säkerställa att MSAL körs korrekt i ditt program eller .NET-exempel:

  * Lägg `https://login.microsoftonline.com/common/oauth2/nativeclient` till som RedirectUrl för mobil- och skrivbordsprogram
  * Lägg **till** domän i avsnittet UserAuthentication i programkonfigurationsfilen. 

    Domän är det Azure Active Directory domän- eller klientorganisations-ID där Azure AD-programmet skapades

* [Felkoder –](error-codes.md) ny felkod har lagts till 
  * 408: Tidsgräns för begäran
  * 504: Gateway-timeout 

### <a name="manage-billing"></a>Hantera fakturering

* [Fakturaradsobjekt – nya](get-invoiceline-items.md) attribut har lagts till i följande API:er:
  * `GET /invoices/{invoice-id}/lineitems?provider={provider}&invoicelineitemtype=billinglineitems`
  * `GET /invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems`

  Nya attribut: 
  * productQualifiers
  * subscriptionStartDate
  * subscriptionEndDate
  * referenceId
  * creditReasonCode (gäller endast för NCE)
  * promotionId 


* [Radobjekt för daglig beräknad användning](get-invoice-billed-consumption-lineitems.md) – nya attribut läggs till i följande API: 
  * `GET /invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems`
  
  Nya attribut: 
  * hasPartnerEarnedCredit (gäller endast för NCE)
  * creditType (gäller endast för NCE)
  * rateOfCredit (gäller endast för NCE)


### <a name="manage-orders"></a>Hantera beställningar

* [Prenumerationsresurser](subscription-resources.md) – Ny egenskap har lagts till. 
  * CancellationAllowedUntilDate – (gäller endast för NCE)

* Övergångsresurser (gäller endast NCE) – Ny egenskap har lagts till 
  * FromSubscriptionId

### <a name="manage-customer-accounts"></a>Hantera kundkonton

* [Verifiera en adress](validate-an-address.md) – Svaret ändras från ett booleskt till en ny modell för API:
  * `POST /validations/address`
  
  Ny svarsmodell: 
  * AddressValidationResponse

* Kundens synkrona API för kvalificering är inaktuell.  


## <a name="version-1170"></a>Version 1.17.0

[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.17.0) v1.17.0 är nu allmänt tillgängligt. Uppdaterade [GitHub exempel](https://github.com/Microsoft/Partner-Center-DotNet-Samples) är också tillgängliga. Följande ändringar ingår i den här versionen:

* Granska uppdaterad – Nya åtgärdstyper har lagts till för att veta när kunden godkände och avslutade DAP
  * [DapAdminRelationshipApproved](auditing-resources.md)
  * [DapAdminRelationshipTerminated](auditing-resources.md)

* Granska uppdaterad – Nya resurs- och åtgärdstyper har lagts till för att stödja scenariot med kundkatalogrollen
  * Resurstyp "[CustomerDirectoryRole](auditing-resources.md)"
  * Åtgärdstyperna[AddUserMember](auditing-resources.md)och[RemoveUserMember](auditing-resources.md)

* SDK-uppdateringar till kundkonto – stöd för följande API:er
  * GET /customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus
  * GET /customers/{customer-tenant-id}/kvalificering 
  * POST /customers/{customer_id}/qualifications?code={validationCode}

* **Följande ändringar introducerades som en del av Ny handel som för närvarande är tillgängliga baserat på inbjudan till partner som ingår i den tekniska förhandsversionen av den nya handelsupplevelsen M365/D365.** Partner som inte är en del av den privata förhandsversionen av ny handel bör inte märka påverkan och bör vara bakåtkompatibla.
  * Katalogändringar:
    * GET /products/{product-id}/skus/{sku-id}
  * Köp och hantera:
    * GET /customers/{customerId}/subscriptions
    * GET /customers/{customerId}/subscriptions/{subscriptionId}
    * PATCH /customers/{customerId}/subscriptions/{subscriptionId}
    * GET /customers/{customerId}/subscriptions/{subscriptionId}/transitioneligibilities
    * GET /customers/{customerId}/subscriptions/{subscriptionId}/transitions
    * POST /customers/{customerId}/subscriptions/{subscriptionId}/transitions


## <a name="version-1163"></a>Version 1.16.3

[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.3) v1.16.3 är nu allmänt tillgängligt. Uppdaterade [GitHub exempel](https://github.com/Microsoft/Partner-Center-DotNet-Samples) är också tillgängliga. Följande ändringar ingår i den här versionen:

* SelfServePolicies – nya funktioner har lagts till
  * [GetSelfServePolicies](get-a-self-serve-policy-by-id.md)
  * [GetListOfSelfServicePolicies](get-a-list-of-self-serve-policies.md)
  * [CreateSelfServePolicies](create-a-self-serve-policy.md)
  * [UpdateSelfServePolicies](update-a-self-serve-policy.md)
  * [DeleteSelfServePolicies](delete-a-self-serve-policy.md)

* Kunders företagsprofil
  * [OrganizationRegistrationNumber har lagts till](create-a-customer.md)

* CustomerBillingProfile.DefaultAddress
  * MiddleName har lagts till

## <a name="version-1162"></a>Version 1.16.2

[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.2) v1.16.2 är nu allmänt tillgängligt. Uppdaterade [GitHub exempel](https://github.com/Microsoft/Partner-Center-DotNet-Samples) är också tillgängliga. Följande ändringar ingår i den här versionen:

* Uppdatera åtgärdstyper som stöds för Granskningspost. De nyligen tillagda är:
  * CreateSelfServePolicy
  * UpdateSelfServePolicy
  * DeleteSelfServePolicy
  * RemovePartnerRelationship
  * DeleteTipCustomer
  * CreateRelatedReferral
  * UpdateRelatedReferral

* Skapandet av tjänstbegäran är nu inaktuell
* Supportämnen är nu inaktuella


## <a name="version-1161"></a>Version 1.16.1

[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.1) v1.16.1 är nu allmänt tillgängligt. Uppdaterade [GitHub exempel](https://github.com/Microsoft/Partner-Center-DotNet-Samples) är också tillgängliga. Följande ändringar ingår i den här versionen:

Vi har migrerat den befintliga Microsoft Partnercenter-SDK från .NET Framework till .NET Standard 2.0-plattformen. Detta gör SDK kompatibelt med befintliga program med hjälp .NET Framework 4.6.1 och högre. SDK stöder .NET Core 2.0 och högre. Kontrollera [.NET-implementeringsstöd](/dotnet/standard/net-standard) innan du portar det till befintliga program.   


## <a name="version-1153"></a>Version 1.15.3
[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.15.3) v1.15.3 är nu allmänt tillgängligt. Uppdaterade REST API:er [och GitHub exempel](https://github.com/Microsoft/Partner-Center-DotNet-Samples) är också tillgängliga. Följande ändringar ingår i den här versionen:

* Partneravtal
  * Lade till möjligheten för indirekta leverantörer att [verifiera Microsoft-partneravtal status för indirekta återförsäljare.](verify-indirect-reseller-mpa-status.md)
* Produkter
  * Följande två gränssnitt placerades felaktigt under namnområdet Microsoft.Store.PartnerCenter.Products. Nu finns de under namnområdet Microsoft.Store.PartnerCenter.Customers.Products.
    * ICustomerProductByReservationScope
    * ICustomerSkuByReservationScope
