---
title: Viktig information för partner Center .NET SDK
description: Viktig information för den senaste versionen av Partner Center .NET SDK.
ms.date: 09/18/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6be8f62e0c202a00b194f5af1dc8904006f8d637
ms.sourcegitcommit: 01e75175077611da92175c777a440a594fb05797
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/08/2020
ms.locfileid: "97770238"
---
# <a name="net-sdk-release-notes"></a>Viktig information för .NET SDK

Följande viktig information är tillgänglig för nya versioner av [Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter). Du hittar [.NET SDK-exempel](https://github.com/Microsoft/Partner-Center-DotNet-Samples) på GitHub. Du hittar [partner Center .NET API-referens](/dotnet/api/?view=partnercenter-dotnet-latest&preserve-view=true) i .NET API-webbläsaren.

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
