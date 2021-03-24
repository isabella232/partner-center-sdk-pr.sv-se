---
title: Viktig information för partner Center .NET SDK
description: Viktig information för den senaste versionen av Partner Center .NET SDK.
ms.date: 09/18/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2fe309500cc80e962c101ad97f0712bef7e11eb3
ms.sourcegitcommit: f7fce0b35ab1579e59136abc357b71cf768b81b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/23/2021
ms.locfileid: "104895541"
---
# <a name="net-sdk-release-notes"></a>Viktig information för .NET SDK

Följande viktig information är tillgänglig för nya versioner av [Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter). Du hittar [.NET SDK-exempel](https://github.com/Microsoft/Partner-Center-DotNet-Samples) på GitHub. Du hittar [partner Center .NET API-referens](/dotnet/api/?view=partnercenter-dotnet-latest&preserve-view=true) i .NET API-webbläsaren.

## <a name="version-1170"></a>Version 1.17.0

[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.17.0) v-1.17.0 är nu allmänt tillgänglig. Uppdaterade [GitHub-exempel](https://github.com/Microsoft/Partner-Center-DotNet-Samples) finns också tillgängliga. Följande ändringar ingår i den här versionen:

* Granska uppdaterade – tillagda nya åtgärds typer för att veta när kunden godkände och avslutade DAP
  * [DapAdminRelationshipApproved](auditing-resources.md)
  * [DapAdminRelationshipTerminated](auditing-resources.md)

* Granska uppdaterad – nya resurs-och åtgärds typer har lagts till för att stödja scenariot för kund katalog roll
  * Resurs typ "[CustomerDirectoryRole](auditing-resources.md)"
  * Åtgärds typer "[AddUserMember](auditing-resources.md)" och "[RemoveUserMember](auditing-resources.md)"

* SDK-uppdateringar till kund konto – stöd för följande API: er
  * Hämta/customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus
  * Hämta/Customers/{Customer-Tenant-ID}/Qualifications 
  * PUBLICERA/Customers/{customer_id}/Qualifications? Code = {validationCode}

* **Följande ändringar införs som en del av en ny handel som för närvarande endast är tillgängliga utifrån inbjudan till partner som är en del av M365/D365 nya Commerce Experience Technical Preview.** Partner som inte ingår i den nya privata Commerce-förhands granskningen bör inte märkas och bör vara bakåtkompatibla.
  * Katalog ändringar:
    * Hämta/Products/{Product-ID}/SKUs/{SKU-ID}
  * Köp och hantera:
    * Hämta/customers/{customerId}/subscriptions
    * Hämta/customers/{customerId}/subscriptions/{subscriptionId}
    * KORRIGERINGs/customers/{customerId}/subscriptions/{subscriptionId}
    * Hämta/customers/{customerId}/subscriptions/{subscriptionId}/transitioneligibilities
    * Hämta/customers/{customerId}/subscriptions/{subscriptionId}/transitions
    * PUBLICERA/customers/{customerId}/subscriptions/{subscriptionId}/transitions


## <a name="version-1163"></a>Version 1.16.3

[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.3) v-1.16.3 är nu allmänt tillgänglig. Uppdaterade [GitHub-exempel](https://github.com/Microsoft/Partner-Center-DotNet-Samples) finns också tillgängliga. Följande ändringar ingår i den här versionen:

* SelfServePolicies – nya funktioner har lagts till
  * [GetSelfServePolicies](get-a-self-serve-policy-by-id.md)
  * [GetListOfSelfServicePolicies](get-a-list-of-self-serve-policies.md)
  * [CreateSelfServePolicies](create-a-self-serve-policy.md)
  * [UpdateSelfServePolicies](update-a-self-serve-policy.md)
  * [DeleteSelfServePolicies](delete-a-self-serve-policy.md)

* Kund företags profil
  * Lade till [OrganizationRegistrationNumber](create-a-customer.md)

* CustomerBillingProfile.DefaultAddress
  * Lade till MiddleName

## <a name="version-1162"></a>Version 1.16.2

[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.2) v-1.16.2 är nu allmänt tillgänglig. Uppdaterade [GitHub-exempel](https://github.com/Microsoft/Partner-Center-DotNet-Samples) finns också tillgängliga. Följande ändringar ingår i den här versionen:

* Uppdatera åtgärds typer som stöds för gransknings post. De nyligen tillagda är:
  * CreateSelfServePolicy
  * UpdateSelfServePolicy
  * DeleteSelfServePolicy
  * RemovePartnerRelationship
  * DeleteTipCustomer
  * CreateRelatedReferral
  * UpdateRelatedReferral

* Genereringen av tjänstbegäran är nu föråldrad
* Support ämnen är nu föråldrade


## <a name="version-1161"></a>Version 1.16.1

[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.1) v-1.16.1 är nu allmänt tillgänglig. Uppdaterade [GitHub-exempel](https://github.com/Microsoft/Partner-Center-DotNet-Samples) finns också tillgängliga. Följande ändringar ingår i den här versionen:

Vi har migrerat den befintliga Microsoft Partner Center SDK: n från .NET Framework till .NET standard 2,0-plattformen. Detta gör SDK-kompatibel med befintliga program med hjälp av .NET Framework 4.6.1 och senare. SDK kommer att stödja .NET Core 2,0 och senare. Kontrol lera [supporten för .net-implementering](/dotnet/standard/net-standard) innan du hamnar i befintliga program.   


## <a name="version-1153"></a>Version 1.15.3
[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.15.3) v-1.15.3 är nu allmänt tillgänglig. Uppdaterade REST-API: er och [GitHub-exempel](https://github.com/Microsoft/Partner-Center-DotNet-Samples) är också tillgängliga. Följande ändringar ingår i den här versionen:

* Partner avtal
  * Har lagt till möjligheten för indirekta leverantörer att [Verifiera status för Microsofts partner avtal för indirekta åter försäljare](verify-indirect-reseller-mpa-status.md).
* Produkter
  * Följande två gränssnitt placerades felaktigt under namn rymden Microsoft. Store. PartnerCenter. Production. Nu finns de i namn rymden Microsoft. Store. PartnerCenter. Customers. Products.
    * ICustomerProductByReservationScope
    * ICustomerSkuByReservationScope
