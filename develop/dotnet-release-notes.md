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
# <a name="net-sdk-release-notes"></a><span data-ttu-id="5fac2-103">Viktig information för .NET SDK</span><span class="sxs-lookup"><span data-stu-id="5fac2-103">.NET SDK release notes</span></span>

<span data-ttu-id="5fac2-104">Följande viktig information är tillgänglig för nya versioner av [Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter).</span><span class="sxs-lookup"><span data-stu-id="5fac2-104">The following release notes are available for new versions of [Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter).</span></span> <span data-ttu-id="5fac2-105">Du hittar [.NET SDK-exempel](https://github.com/Microsoft/Partner-Center-DotNet-Samples) på GitHub.</span><span class="sxs-lookup"><span data-stu-id="5fac2-105">You can find [.NET SDK samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) on GitHub.</span></span> <span data-ttu-id="5fac2-106">Du hittar [partner Center .NET API-referens](/dotnet/api/?view=partnercenter-dotnet-latest&preserve-view=true) i .NET API-webbläsaren.</span><span class="sxs-lookup"><span data-stu-id="5fac2-106">You can find the [Partner Center .NET API reference](/dotnet/api/?view=partnercenter-dotnet-latest&preserve-view=true) in the .NET API Browser.</span></span>

## <a name="version-1170"></a><span data-ttu-id="5fac2-107">Version 1.17.0</span><span class="sxs-lookup"><span data-stu-id="5fac2-107">Version 1.17.0</span></span>

<span data-ttu-id="5fac2-108">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.17.0) v-1.17.0 är nu allmänt tillgänglig.</span><span class="sxs-lookup"><span data-stu-id="5fac2-108">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.17.0) v1.17.0 is now general availability.</span></span> <span data-ttu-id="5fac2-109">Uppdaterade [GitHub-exempel](https://github.com/Microsoft/Partner-Center-DotNet-Samples) finns också tillgängliga.</span><span class="sxs-lookup"><span data-stu-id="5fac2-109">Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="5fac2-110">Följande ändringar ingår i den här versionen:</span><span class="sxs-lookup"><span data-stu-id="5fac2-110">The following changes are included in this version:</span></span>

* <span data-ttu-id="5fac2-111">Granska uppdaterade – tillagda nya åtgärds typer för att veta när kunden godkände och avslutade DAP</span><span class="sxs-lookup"><span data-stu-id="5fac2-111">Audit Updated - Added new operation types for knowing when the customer approved and terminated DAP</span></span>
  * [<span data-ttu-id="5fac2-112">DapAdminRelationshipApproved</span><span class="sxs-lookup"><span data-stu-id="5fac2-112">DapAdminRelationshipApproved</span></span>](auditing-resources.md)
  * [<span data-ttu-id="5fac2-113">DapAdminRelationshipTerminated</span><span class="sxs-lookup"><span data-stu-id="5fac2-113">DapAdminRelationshipTerminated</span></span>](auditing-resources.md)

* <span data-ttu-id="5fac2-114">Granska uppdaterad – nya resurs-och åtgärds typer har lagts till för att stödja scenariot för kund katalog roll</span><span class="sxs-lookup"><span data-stu-id="5fac2-114">Audit Updated – Added new resource and operation types for supporting the customer directory role scenario</span></span>
  * <span data-ttu-id="5fac2-115">Resurs typ "[CustomerDirectoryRole](auditing-resources.md)"</span><span class="sxs-lookup"><span data-stu-id="5fac2-115">Resource type "[CustomerDirectoryRole](auditing-resources.md)"</span></span>
  * <span data-ttu-id="5fac2-116">Åtgärds typer "[AddUserMember](auditing-resources.md)" och "[RemoveUserMember](auditing-resources.md)"</span><span class="sxs-lookup"><span data-stu-id="5fac2-116">Operation types "[AddUserMember](auditing-resources.md)" and "[RemoveUserMember](auditing-resources.md)"</span></span>

* <span data-ttu-id="5fac2-117">SDK-uppdateringar till kund konto – stöd för följande API: er</span><span class="sxs-lookup"><span data-stu-id="5fac2-117">SDK Updates to Customers Account - Support for following API's</span></span>
  * <span data-ttu-id="5fac2-118">Hämta/customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus</span><span class="sxs-lookup"><span data-stu-id="5fac2-118">GET /customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus</span></span>
  * <span data-ttu-id="5fac2-119">Hämta/Customers/{Customer-Tenant-ID}/Qualifications</span><span class="sxs-lookup"><span data-stu-id="5fac2-119">GET /customers/{customer-tenant-id}/qualifications</span></span> 
  * <span data-ttu-id="5fac2-120">PUBLICERA/Customers/{customer_id}/Qualifications? Code = {validationCode}</span><span class="sxs-lookup"><span data-stu-id="5fac2-120">POST /customers/{customer_id}/qualifications?code={validationCode}</span></span>

* <span data-ttu-id="5fac2-121">**Följande ändringar införs som en del av en ny handel som för närvarande endast är tillgängliga utifrån inbjudan till partner som är en del av M365/D365 nya Commerce Experience Technical Preview.**</span><span class="sxs-lookup"><span data-stu-id="5fac2-121">**Following changes introduced as part of New Commerce which are currently available based on invitation only to partners who are part of the M365/D365 new commerce experience technical preview.**</span></span> <span data-ttu-id="5fac2-122">Partner som inte ingår i den nya privata Commerce-förhands granskningen bör inte märkas och bör vara bakåtkompatibla.</span><span class="sxs-lookup"><span data-stu-id="5fac2-122">Partners who are not part of New commerce private preview should not notice impacts and should be backward compatible.</span></span>
  * <span data-ttu-id="5fac2-123">Katalog ändringar:</span><span class="sxs-lookup"><span data-stu-id="5fac2-123">Catalog Changes:</span></span>
    * <span data-ttu-id="5fac2-124">Hämta/Products/{Product-ID}/SKUs/{SKU-ID}</span><span class="sxs-lookup"><span data-stu-id="5fac2-124">GET /products/{product-id}/skus/{sku-id}</span></span>
  * <span data-ttu-id="5fac2-125">Köp och hantera:</span><span class="sxs-lookup"><span data-stu-id="5fac2-125">Purchase and Manage:</span></span>
    * <span data-ttu-id="5fac2-126">Hämta/customers/{customerId}/subscriptions</span><span class="sxs-lookup"><span data-stu-id="5fac2-126">GET /customers/{customerId}/subscriptions</span></span>
    * <span data-ttu-id="5fac2-127">Hämta/customers/{customerId}/subscriptions/{subscriptionId}</span><span class="sxs-lookup"><span data-stu-id="5fac2-127">GET /customers/{customerId}/subscriptions/{subscriptionId}</span></span>
    * <span data-ttu-id="5fac2-128">KORRIGERINGs/customers/{customerId}/subscriptions/{subscriptionId}</span><span class="sxs-lookup"><span data-stu-id="5fac2-128">PATCH /customers/{customerId}/subscriptions/{subscriptionId}</span></span>
    * <span data-ttu-id="5fac2-129">Hämta/customers/{customerId}/subscriptions/{subscriptionId}/transitioneligibilities</span><span class="sxs-lookup"><span data-stu-id="5fac2-129">GET /customers/{customerId}/subscriptions/{subscriptionId}/transitioneligibilities</span></span>
    * <span data-ttu-id="5fac2-130">Hämta/customers/{customerId}/subscriptions/{subscriptionId}/transitions</span><span class="sxs-lookup"><span data-stu-id="5fac2-130">GET /customers/{customerId}/subscriptions/{subscriptionId}/transitions</span></span>
    * <span data-ttu-id="5fac2-131">PUBLICERA/customers/{customerId}/subscriptions/{subscriptionId}/transitions</span><span class="sxs-lookup"><span data-stu-id="5fac2-131">POST /customers/{customerId}/subscriptions/{subscriptionId}/transitions</span></span>


## <a name="version-1163"></a><span data-ttu-id="5fac2-132">Version 1.16.3</span><span class="sxs-lookup"><span data-stu-id="5fac2-132">Version 1.16.3</span></span>

<span data-ttu-id="5fac2-133">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.3) v-1.16.3 är nu allmänt tillgänglig.</span><span class="sxs-lookup"><span data-stu-id="5fac2-133">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.3) v1.16.3 is now general availability.</span></span> <span data-ttu-id="5fac2-134">Uppdaterade [GitHub-exempel](https://github.com/Microsoft/Partner-Center-DotNet-Samples) finns också tillgängliga.</span><span class="sxs-lookup"><span data-stu-id="5fac2-134">Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="5fac2-135">Följande ändringar ingår i den här versionen:</span><span class="sxs-lookup"><span data-stu-id="5fac2-135">The following changes are included in this version:</span></span>

* <span data-ttu-id="5fac2-136">SelfServePolicies – nya funktioner har lagts till</span><span class="sxs-lookup"><span data-stu-id="5fac2-136">SelfServePolicies - new functionality added</span></span>
  * [<span data-ttu-id="5fac2-137">GetSelfServePolicies</span><span class="sxs-lookup"><span data-stu-id="5fac2-137">GetSelfServePolicies</span></span>](get-a-self-serve-policy-by-id.md)
  * [<span data-ttu-id="5fac2-138">GetListOfSelfServicePolicies</span><span class="sxs-lookup"><span data-stu-id="5fac2-138">GetListOfSelfServicePolicies</span></span>](get-a-list-of-self-serve-policies.md)
  * [<span data-ttu-id="5fac2-139">CreateSelfServePolicies</span><span class="sxs-lookup"><span data-stu-id="5fac2-139">CreateSelfServePolicies</span></span>](create-a-self-serve-policy.md)
  * [<span data-ttu-id="5fac2-140">UpdateSelfServePolicies</span><span class="sxs-lookup"><span data-stu-id="5fac2-140">UpdateSelfServePolicies</span></span>](update-a-self-serve-policy.md)
  * [<span data-ttu-id="5fac2-141">DeleteSelfServePolicies</span><span class="sxs-lookup"><span data-stu-id="5fac2-141">DeleteSelfServePolicies</span></span>](delete-a-self-serve-policy.md)

* <span data-ttu-id="5fac2-142">Kund företags profil</span><span class="sxs-lookup"><span data-stu-id="5fac2-142">Customers Company Profile</span></span>
  * <span data-ttu-id="5fac2-143">Lade till [OrganizationRegistrationNumber](create-a-customer.md)</span><span class="sxs-lookup"><span data-stu-id="5fac2-143">Added [OrganizationRegistrationNumber](create-a-customer.md)</span></span>

* <span data-ttu-id="5fac2-144">CustomerBillingProfile.DefaultAddress</span><span class="sxs-lookup"><span data-stu-id="5fac2-144">CustomerBillingProfile.DefaultAddress</span></span>
  * <span data-ttu-id="5fac2-145">Lade till MiddleName</span><span class="sxs-lookup"><span data-stu-id="5fac2-145">Added MiddleName</span></span>

## <a name="version-1162"></a><span data-ttu-id="5fac2-146">Version 1.16.2</span><span class="sxs-lookup"><span data-stu-id="5fac2-146">Version 1.16.2</span></span>

<span data-ttu-id="5fac2-147">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.2) v-1.16.2 är nu allmänt tillgänglig.</span><span class="sxs-lookup"><span data-stu-id="5fac2-147">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.2) v1.16.2 is now general availability.</span></span> <span data-ttu-id="5fac2-148">Uppdaterade [GitHub-exempel](https://github.com/Microsoft/Partner-Center-DotNet-Samples) finns också tillgängliga.</span><span class="sxs-lookup"><span data-stu-id="5fac2-148">Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="5fac2-149">Följande ändringar ingår i den här versionen:</span><span class="sxs-lookup"><span data-stu-id="5fac2-149">The following changes are included in this version:</span></span>

* <span data-ttu-id="5fac2-150">Uppdatera åtgärds typer som stöds för gransknings post.</span><span class="sxs-lookup"><span data-stu-id="5fac2-150">Update supported operation types for Audit Record.</span></span> <span data-ttu-id="5fac2-151">De nyligen tillagda är:</span><span class="sxs-lookup"><span data-stu-id="5fac2-151">The newly added ones are:</span></span>
  * <span data-ttu-id="5fac2-152">CreateSelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="5fac2-152">CreateSelfServePolicy</span></span>
  * <span data-ttu-id="5fac2-153">UpdateSelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="5fac2-153">UpdateSelfServePolicy</span></span>
  * <span data-ttu-id="5fac2-154">DeleteSelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="5fac2-154">DeleteSelfServePolicy</span></span>
  * <span data-ttu-id="5fac2-155">RemovePartnerRelationship</span><span class="sxs-lookup"><span data-stu-id="5fac2-155">RemovePartnerRelationship</span></span>
  * <span data-ttu-id="5fac2-156">DeleteTipCustomer</span><span class="sxs-lookup"><span data-stu-id="5fac2-156">DeleteTipCustomer</span></span>
  * <span data-ttu-id="5fac2-157">CreateRelatedReferral</span><span class="sxs-lookup"><span data-stu-id="5fac2-157">CreateRelatedReferral</span></span>
  * <span data-ttu-id="5fac2-158">UpdateRelatedReferral</span><span class="sxs-lookup"><span data-stu-id="5fac2-158">UpdateRelatedReferral</span></span>

* <span data-ttu-id="5fac2-159">Genereringen av tjänstbegäran är nu föråldrad</span><span class="sxs-lookup"><span data-stu-id="5fac2-159">Service request creation is now deprecated</span></span>
* <span data-ttu-id="5fac2-160">Support ämnen är nu föråldrade</span><span class="sxs-lookup"><span data-stu-id="5fac2-160">Support topics are now deprecated</span></span>


## <a name="version-1161"></a><span data-ttu-id="5fac2-161">Version 1.16.1</span><span class="sxs-lookup"><span data-stu-id="5fac2-161">Version 1.16.1</span></span>

<span data-ttu-id="5fac2-162">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.1) v-1.16.1 är nu allmänt tillgänglig.</span><span class="sxs-lookup"><span data-stu-id="5fac2-162">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.1) v1.16.1 is now general availability.</span></span> <span data-ttu-id="5fac2-163">Uppdaterade [GitHub-exempel](https://github.com/Microsoft/Partner-Center-DotNet-Samples) finns också tillgängliga.</span><span class="sxs-lookup"><span data-stu-id="5fac2-163">Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="5fac2-164">Följande ändringar ingår i den här versionen:</span><span class="sxs-lookup"><span data-stu-id="5fac2-164">The following changes are included in this version:</span></span>

<span data-ttu-id="5fac2-165">Vi har migrerat den befintliga Microsoft Partner Center SDK: n från .NET Framework till .NET standard 2,0-plattformen.</span><span class="sxs-lookup"><span data-stu-id="5fac2-165">We have migrated the existing Microsoft Partner Center SDK from .NET Framework to .NET Standard 2.0 platform.</span></span> <span data-ttu-id="5fac2-166">Detta gör SDK-kompatibel med befintliga program med hjälp av .NET Framework 4.6.1 och senare.</span><span class="sxs-lookup"><span data-stu-id="5fac2-166">This will make the SDK compatible with existing applications using .NET Framework 4.6.1 and above.</span></span> <span data-ttu-id="5fac2-167">SDK kommer att stödja .NET Core 2,0 och senare.</span><span class="sxs-lookup"><span data-stu-id="5fac2-167">The SDK will support .NET Core 2.0 and above.</span></span> <span data-ttu-id="5fac2-168">Kontrol lera [supporten för .net-implementering](/dotnet/standard/net-standard) innan du hamnar i befintliga program.</span><span class="sxs-lookup"><span data-stu-id="5fac2-168">Check [.NET implementation support](/dotnet/standard/net-standard) before porting it to existing applications.</span></span>   


## <a name="version-1153"></a><span data-ttu-id="5fac2-169">Version 1.15.3</span><span class="sxs-lookup"><span data-stu-id="5fac2-169">Version 1.15.3</span></span>
<span data-ttu-id="5fac2-170">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.15.3) v-1.15.3 är nu allmänt tillgänglig.</span><span class="sxs-lookup"><span data-stu-id="5fac2-170">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.15.3) v1.15.3 is now general availability.</span></span> <span data-ttu-id="5fac2-171">Uppdaterade REST-API: er och [GitHub-exempel](https://github.com/Microsoft/Partner-Center-DotNet-Samples) är också tillgängliga.</span><span class="sxs-lookup"><span data-stu-id="5fac2-171">Updated REST APIs and [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="5fac2-172">Följande ändringar ingår i den här versionen:</span><span class="sxs-lookup"><span data-stu-id="5fac2-172">The following changes are included in this version:</span></span>

* <span data-ttu-id="5fac2-173">Partner avtal</span><span class="sxs-lookup"><span data-stu-id="5fac2-173">Partner Agreement</span></span>
  * <span data-ttu-id="5fac2-174">Har lagt till möjligheten för indirekta leverantörer att [Verifiera status för Microsofts partner avtal för indirekta åter försäljare](verify-indirect-reseller-mpa-status.md).</span><span class="sxs-lookup"><span data-stu-id="5fac2-174">Added the ability for indirect providers to [verify Microsoft Partner Agreement status of indirect resellers](verify-indirect-reseller-mpa-status.md).</span></span>
* <span data-ttu-id="5fac2-175">Produkter</span><span class="sxs-lookup"><span data-stu-id="5fac2-175">Products</span></span>
  * <span data-ttu-id="5fac2-176">Följande två gränssnitt placerades felaktigt under namn rymden Microsoft. Store. PartnerCenter. Production.</span><span class="sxs-lookup"><span data-stu-id="5fac2-176">The following two interfaces were incorrectly placed under the Microsoft.Store.PartnerCenter.Products namespace.</span></span> <span data-ttu-id="5fac2-177">Nu finns de i namn rymden Microsoft. Store. PartnerCenter. Customers. Products.</span><span class="sxs-lookup"><span data-stu-id="5fac2-177">Now, they are located under the Microsoft.Store.PartnerCenter.Customers.Products namespace.</span></span>
    * <span data-ttu-id="5fac2-178">ICustomerProductByReservationScope</span><span class="sxs-lookup"><span data-stu-id="5fac2-178">ICustomerProductByReservationScope</span></span>
    * <span data-ttu-id="5fac2-179">ICustomerSkuByReservationScope</span><span class="sxs-lookup"><span data-stu-id="5fac2-179">ICustomerSkuByReservationScope</span></span>
