---
title: Viktig information om Partner Center .NET SDK
description: Viktig information för den senaste versionen av Partner Center .NET SDK.
ms.date: 07/07/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c1532d48c00550f5eb437ed0164d6a1f7bb340dd
ms.sourcegitcommit: 53c94db33b09c30e762b842c4275b2b531dba932
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/09/2021
ms.locfileid: "113522642"
---
# <a name="net-sdk-release-notes"></a><span data-ttu-id="36bc7-103">.NET SDK – information</span><span class="sxs-lookup"><span data-stu-id="36bc7-103">.NET SDK release notes</span></span>

<span data-ttu-id="36bc7-104">Följande viktig information är tillgänglig för nya versioner av [Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter).</span><span class="sxs-lookup"><span data-stu-id="36bc7-104">The following release notes are available for new versions of [Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter).</span></span> <span data-ttu-id="36bc7-105">Du hittar [.NET SDK-exempel](https://github.com/Microsoft/Partner-Center-DotNet-Samples) på GitHub.</span><span class="sxs-lookup"><span data-stu-id="36bc7-105">You can find [.NET SDK samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) on GitHub.</span></span> <span data-ttu-id="36bc7-106">Du hittar Partner [Center .NET API-referensen](/dotnet/api/?view=partnercenter-dotnet-latest&preserve-view=true) i .NET API-webbläsaren.</span><span class="sxs-lookup"><span data-stu-id="36bc7-106">You can find the [Partner Center .NET API reference](/dotnet/api/?view=partnercenter-dotnet-latest&preserve-view=true) in the .NET API Browser.</span></span>

## <a name="version-201"></a><span data-ttu-id="36bc7-107">Version 2.0.1</span><span class="sxs-lookup"><span data-stu-id="36bc7-107">Version 2.0.1</span></span>

<span data-ttu-id="36bc7-108">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/2.0.1) v2.0.1 är nu allmänt tillgänglig.</span><span class="sxs-lookup"><span data-stu-id="36bc7-108">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/2.0.1) v2.0.1 is now general availability.</span></span> <span data-ttu-id="36bc7-109">Uppdaterade [GitHub exempel](https://github.com/Microsoft/Partner-Center-DotNet-Samples) är också tillgängliga.</span><span class="sxs-lookup"><span data-stu-id="36bc7-109">Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="36bc7-110">Följande ändringar ingår i den här versionen:</span><span class="sxs-lookup"><span data-stu-id="36bc7-110">The following changes are included in this version:</span></span>

> [!NOTE]
> <span data-ttu-id="36bc7-111">Några av ändringarna introducerades som en del av New Commerce Experiences ("NCE") som för närvarande är tillgängliga baserat på inbjudan endast till partner som ingår i den tekniska förhandsversionen av den nya handelsupplevelsen M365/D365.</span><span class="sxs-lookup"><span data-stu-id="36bc7-111">Some of changes introduced as part of New Commerce Experiences (“NCE”) which are currently available based on invitation only to partners who are part of the M365/D365 new commerce experience technical preview.</span></span> <span data-ttu-id="36bc7-112">Partner som inte är en del av den privata förhandsversionen av ny handel bör inte märka påverkan och bör vara bakåtkompatibla.</span><span class="sxs-lookup"><span data-stu-id="36bc7-112">Partners who are not part of New commerce private preview should not notice impacts and should be backward compatible.</span></span>

### <a name="common"></a><span data-ttu-id="36bc7-113">Common</span><span class="sxs-lookup"><span data-stu-id="36bc7-113">Common</span></span>
* <span data-ttu-id="36bc7-114">Ändra referensen till autentiseringsbiblioteket – Referensen ändras från Azure Active Directory Authentication Library[(ADAL)](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet)till Microsoft Authentication Library[(MSAL)](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet)</span><span class="sxs-lookup"><span data-stu-id="36bc7-114">Change on the reference to authentication library – The reference is changed from Azure Active Directory Authentication Library ([ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet)) to Microsoft Authentication Library ([MSAL](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet))</span></span>

  <span data-ttu-id="36bc7-115">Följande ändringar bör göras för att säkerställa att MSAL körs korrekt på ditt program eller .NET-exempel:</span><span class="sxs-lookup"><span data-stu-id="36bc7-115">Following changes should be made to ensure MSAL runs correctly on your application or .NET sample:</span></span>

  * <span data-ttu-id="36bc7-116">Lägg `https://login.microsoftonline.com/common/oauth2/nativeclient` till som RedirectUrl för mobil- och datorprogram</span><span class="sxs-lookup"><span data-stu-id="36bc7-116">Add `https://login.microsoftonline.com/common/oauth2/nativeclient` as RedirectUrl for Mobile and desktop applications</span></span>
  * <span data-ttu-id="36bc7-117">Lägg **till** domän i avsnittet UserAuthentication i programkonfigurationsfilen.</span><span class="sxs-lookup"><span data-stu-id="36bc7-117">Add **Domain** into UserAuthentication section in your application configuration file.</span></span> 

    <span data-ttu-id="36bc7-118">Domän är det Azure Active Directory domän- eller klientorganisations-ID där Azure AD-programmet skapades</span><span class="sxs-lookup"><span data-stu-id="36bc7-118">Domain is the Azure Active Directory domain or tenant ID where the Azure AD application was created</span></span>

* <span data-ttu-id="36bc7-119">[Felkoder –](error-codes.md) ny felkod har lagts till</span><span class="sxs-lookup"><span data-stu-id="36bc7-119">[Error codes](error-codes.md) – New error code added</span></span> 
  * <span data-ttu-id="36bc7-120">408: Tidsgräns för begäran</span><span class="sxs-lookup"><span data-stu-id="36bc7-120">408: Request timeout</span></span>
  * <span data-ttu-id="36bc7-121">504: Gateway-timeout</span><span class="sxs-lookup"><span data-stu-id="36bc7-121">504: Gateway timeout</span></span> 

### <a name="manage-billing"></a><span data-ttu-id="36bc7-122">Hantera fakturering</span><span class="sxs-lookup"><span data-stu-id="36bc7-122">Manage billing</span></span>

* <span data-ttu-id="36bc7-123">[Fakturaradsobjekt – nya](get-invoiceline-items.md) attribut läggs till i följande API:er:</span><span class="sxs-lookup"><span data-stu-id="36bc7-123">[Invoice line-items](get-invoiceline-items.md) - new attributes added to following APIs:</span></span>
  * `GET /invoices/{invoice-id}/lineitems?provider={provider}&invoicelineitemtype=billinglineitems`
  * `GET /invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems`

  <span data-ttu-id="36bc7-124">Nya attribut:</span><span class="sxs-lookup"><span data-stu-id="36bc7-124">New attributes:</span></span> 
  * <span data-ttu-id="36bc7-125">productQualifiers</span><span class="sxs-lookup"><span data-stu-id="36bc7-125">productQualifiers</span></span>
  * <span data-ttu-id="36bc7-126">subscriptionStartDate</span><span class="sxs-lookup"><span data-stu-id="36bc7-126">subscriptionStartDate</span></span>
  * <span data-ttu-id="36bc7-127">subscriptionEndDate</span><span class="sxs-lookup"><span data-stu-id="36bc7-127">subscriptionEndDate</span></span>
  * <span data-ttu-id="36bc7-128">referenceId</span><span class="sxs-lookup"><span data-stu-id="36bc7-128">referenceId</span></span>
  * <span data-ttu-id="36bc7-129">creditReasonCode (gäller endast NCE)</span><span class="sxs-lookup"><span data-stu-id="36bc7-129">creditReasonCode  (Only applicable to NCE)</span></span>
  * <span data-ttu-id="36bc7-130">promotionId</span><span class="sxs-lookup"><span data-stu-id="36bc7-130">promotionId</span></span> 


* <span data-ttu-id="36bc7-131">[Radobjekt för daglig beräknad användning –](get-invoice-billed-consumption-lineitems.md) nya attribut läggs till i följande API:</span><span class="sxs-lookup"><span data-stu-id="36bc7-131">[Daily rated usage Line-items](get-invoice-billed-consumption-lineitems.md) – new attributes added to following API:</span></span> 
  * `GET /invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems`
  
  <span data-ttu-id="36bc7-132">Nya attribut:</span><span class="sxs-lookup"><span data-stu-id="36bc7-132">New attributes:</span></span> 
  * <span data-ttu-id="36bc7-133">hasPartnerEarnedCredit (gäller endast för NCE)</span><span class="sxs-lookup"><span data-stu-id="36bc7-133">hasPartnerEarnedCredit (Only applicable to NCE)</span></span>
  * <span data-ttu-id="36bc7-134">creditType (gäller endast för NCE)</span><span class="sxs-lookup"><span data-stu-id="36bc7-134">creditType (Only applicable to NCE)</span></span>
  * <span data-ttu-id="36bc7-135">rateOfCredit (gäller endast för NCE)</span><span class="sxs-lookup"><span data-stu-id="36bc7-135">rateOfCredit (Only applicable to NCE)</span></span>


### <a name="manage-orders"></a><span data-ttu-id="36bc7-136">Hantera beställningar</span><span class="sxs-lookup"><span data-stu-id="36bc7-136">Manage orders</span></span>

* <span data-ttu-id="36bc7-137">[Prenumerationsresurser](subscription-resources.md) – Ny egenskap har lagts till.</span><span class="sxs-lookup"><span data-stu-id="36bc7-137">[Subscription Resources](subscription-resources.md) – New property added.</span></span> 
  * <span data-ttu-id="36bc7-138">CancellationAllowedUntilDate – (gäller endast NCE)</span><span class="sxs-lookup"><span data-stu-id="36bc7-138">CancellationAllowedUntilDate  - (Only applicable to NCE)</span></span>

* <span data-ttu-id="36bc7-139">Övergångsresurser (gäller endast för NCE) – Ny egenskap har lagts till</span><span class="sxs-lookup"><span data-stu-id="36bc7-139">Transition Resources (Only applicable to NCE) – New property added</span></span> 
  * <span data-ttu-id="36bc7-140">FromSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="36bc7-140">FromSubscriptionId</span></span>

### <a name="manage-customer-accounts"></a><span data-ttu-id="36bc7-141">Hantera kundkonton</span><span class="sxs-lookup"><span data-stu-id="36bc7-141">Manage customer accounts</span></span>

* <span data-ttu-id="36bc7-142">[Verifiera en adress](validate-an-address.md) – Svaret ändras från ett booleskt till en ny API-modell:</span><span class="sxs-lookup"><span data-stu-id="36bc7-142">[Validate an address](validate-an-address.md) – Response is changed from a Boolean to a new model for API:</span></span>
  * `POST /validations/address`
  
  <span data-ttu-id="36bc7-143">Ny svarsmodell:</span><span class="sxs-lookup"><span data-stu-id="36bc7-143">New response model:</span></span> 
  * <span data-ttu-id="36bc7-144">AddressValidationResponse</span><span class="sxs-lookup"><span data-stu-id="36bc7-144">AddressValidationResponse</span></span>

* <span data-ttu-id="36bc7-145">Kundens synkrona API för kvalificering är inaktuell.</span><span class="sxs-lookup"><span data-stu-id="36bc7-145">Customer’s qualification synchronous API is deprecated.</span></span>  


## <a name="version-1170"></a><span data-ttu-id="36bc7-146">Version 1.17.0</span><span class="sxs-lookup"><span data-stu-id="36bc7-146">Version 1.17.0</span></span>

<span data-ttu-id="36bc7-147">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.17.0) v1.17.0 är nu allmänt tillgänglig.</span><span class="sxs-lookup"><span data-stu-id="36bc7-147">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.17.0) v1.17.0 is now general availability.</span></span> <span data-ttu-id="36bc7-148">Uppdaterade [GitHub exempel](https://github.com/Microsoft/Partner-Center-DotNet-Samples) är också tillgängliga.</span><span class="sxs-lookup"><span data-stu-id="36bc7-148">Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="36bc7-149">Följande ändringar ingår i den här versionen:</span><span class="sxs-lookup"><span data-stu-id="36bc7-149">The following changes are included in this version:</span></span>

* <span data-ttu-id="36bc7-150">Granska uppdaterad – Nya åtgärdstyper har lagts till för att veta när kunden har godkänt och avslutat DAP</span><span class="sxs-lookup"><span data-stu-id="36bc7-150">Audit Updated - Added new operation types for knowing when the customer approved and terminated DAP</span></span>
  * [<span data-ttu-id="36bc7-151">DapAdminRelationshipApproved</span><span class="sxs-lookup"><span data-stu-id="36bc7-151">DapAdminRelationshipApproved</span></span>](auditing-resources.md)
  * [<span data-ttu-id="36bc7-152">DapAdminRelationshipTerminated</span><span class="sxs-lookup"><span data-stu-id="36bc7-152">DapAdminRelationshipTerminated</span></span>](auditing-resources.md)

* <span data-ttu-id="36bc7-153">Granska uppdaterad – nya resurs- och åtgärdstyper har lagts till för att stödja scenariot med kundkatalogrollen</span><span class="sxs-lookup"><span data-stu-id="36bc7-153">Audit Updated – Added new resource and operation types for supporting the customer directory role scenario</span></span>
  * <span data-ttu-id="36bc7-154">Resurstyp "[CustomerDirectoryRole](auditing-resources.md)"</span><span class="sxs-lookup"><span data-stu-id="36bc7-154">Resource type "[CustomerDirectoryRole](auditing-resources.md)"</span></span>
  * <span data-ttu-id="36bc7-155">Åtgärdstyperna[AddUserMember](auditing-resources.md)och[RemoveUserMember](auditing-resources.md)</span><span class="sxs-lookup"><span data-stu-id="36bc7-155">Operation types "[AddUserMember](auditing-resources.md)" and "[RemoveUserMember](auditing-resources.md)"</span></span>

* <span data-ttu-id="36bc7-156">SDK-uppdateringar till kundkonto – stöd för följande API:er</span><span class="sxs-lookup"><span data-stu-id="36bc7-156">SDK Updates to Customers Account - Support for following API's</span></span>
  * <span data-ttu-id="36bc7-157">GET /customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus</span><span class="sxs-lookup"><span data-stu-id="36bc7-157">GET /customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus</span></span>
  * <span data-ttu-id="36bc7-158">GET /customers/{customer-tenant-id}/kvalificering</span><span class="sxs-lookup"><span data-stu-id="36bc7-158">GET /customers/{customer-tenant-id}/qualifications</span></span> 
  * <span data-ttu-id="36bc7-159">POST /customers/{customer_id}/qualifications?code={validationCode}</span><span class="sxs-lookup"><span data-stu-id="36bc7-159">POST /customers/{customer_id}/qualifications?code={validationCode}</span></span>

* <span data-ttu-id="36bc7-160">**Följande ändringar introducerades som en del av New Commerce som för närvarande är tillgängliga baserat på inbjudan till partner som ingår i den tekniska förhandsversionen av den nya handelsupplevelsen M365/D365.**</span><span class="sxs-lookup"><span data-stu-id="36bc7-160">**Following changes introduced as part of New Commerce which are currently available based on invitation only to partners who are part of the M365/D365 new commerce experience technical preview.**</span></span> <span data-ttu-id="36bc7-161">Partner som inte är en del av den privata förhandsversionen av ny handel bör inte märka påverkan och bör vara bakåtkompatibla.</span><span class="sxs-lookup"><span data-stu-id="36bc7-161">Partners who are not part of New commerce private preview should not notice impacts and should be backward compatible.</span></span>
  * <span data-ttu-id="36bc7-162">Katalogändringar:</span><span class="sxs-lookup"><span data-stu-id="36bc7-162">Catalog Changes:</span></span>
    * <span data-ttu-id="36bc7-163">GET /products/{product-id}/skus/{sku-id}</span><span class="sxs-lookup"><span data-stu-id="36bc7-163">GET /products/{product-id}/skus/{sku-id}</span></span>
  * <span data-ttu-id="36bc7-164">Köpa och hantera:</span><span class="sxs-lookup"><span data-stu-id="36bc7-164">Purchase and Manage:</span></span>
    * <span data-ttu-id="36bc7-165">GET /customers/{customerId}/subscriptions</span><span class="sxs-lookup"><span data-stu-id="36bc7-165">GET /customers/{customerId}/subscriptions</span></span>
    * <span data-ttu-id="36bc7-166">GET /customers/{customerId}/subscriptions/{subscriptionId}</span><span class="sxs-lookup"><span data-stu-id="36bc7-166">GET /customers/{customerId}/subscriptions/{subscriptionId}</span></span>
    * <span data-ttu-id="36bc7-167">PATCH /customers/{customerId}/subscriptions/{subscriptionId}</span><span class="sxs-lookup"><span data-stu-id="36bc7-167">PATCH /customers/{customerId}/subscriptions/{subscriptionId}</span></span>
    * <span data-ttu-id="36bc7-168">GET /customers/{customerId}/subscriptions/{subscriptionId}/transitioneligibilities</span><span class="sxs-lookup"><span data-stu-id="36bc7-168">GET /customers/{customerId}/subscriptions/{subscriptionId}/transitioneligibilities</span></span>
    * <span data-ttu-id="36bc7-169">GET /customers/{customerId}/subscriptions/{subscriptionId}/transitions</span><span class="sxs-lookup"><span data-stu-id="36bc7-169">GET /customers/{customerId}/subscriptions/{subscriptionId}/transitions</span></span>
    * <span data-ttu-id="36bc7-170">POST /customers/{customerId}/subscriptions/{subscriptionId}/transitions</span><span class="sxs-lookup"><span data-stu-id="36bc7-170">POST /customers/{customerId}/subscriptions/{subscriptionId}/transitions</span></span>


## <a name="version-1163"></a><span data-ttu-id="36bc7-171">Version 1.16.3</span><span class="sxs-lookup"><span data-stu-id="36bc7-171">Version 1.16.3</span></span>

<span data-ttu-id="36bc7-172">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.3) v1.16.3 är nu allmänt tillgänglig.</span><span class="sxs-lookup"><span data-stu-id="36bc7-172">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.3) v1.16.3 is now general availability.</span></span> <span data-ttu-id="36bc7-173">Uppdaterade [GitHub exempel](https://github.com/Microsoft/Partner-Center-DotNet-Samples) är också tillgängliga.</span><span class="sxs-lookup"><span data-stu-id="36bc7-173">Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="36bc7-174">Följande ändringar ingår i den här versionen:</span><span class="sxs-lookup"><span data-stu-id="36bc7-174">The following changes are included in this version:</span></span>

* <span data-ttu-id="36bc7-175">SelfServePolicies – nya funktioner har lagts till</span><span class="sxs-lookup"><span data-stu-id="36bc7-175">SelfServePolicies - new functionality added</span></span>
  * [<span data-ttu-id="36bc7-176">GetSelfServePolicies</span><span class="sxs-lookup"><span data-stu-id="36bc7-176">GetSelfServePolicies</span></span>](get-a-self-serve-policy-by-id.md)
  * [<span data-ttu-id="36bc7-177">GetListOfSelfServicePolicies</span><span class="sxs-lookup"><span data-stu-id="36bc7-177">GetListOfSelfServicePolicies</span></span>](get-a-list-of-self-serve-policies.md)
  * [<span data-ttu-id="36bc7-178">CreateSelfServePolicies</span><span class="sxs-lookup"><span data-stu-id="36bc7-178">CreateSelfServePolicies</span></span>](create-a-self-serve-policy.md)
  * [<span data-ttu-id="36bc7-179">UpdateSelfServePolicies</span><span class="sxs-lookup"><span data-stu-id="36bc7-179">UpdateSelfServePolicies</span></span>](update-a-self-serve-policy.md)
  * [<span data-ttu-id="36bc7-180">DeleteSelfServePolicies</span><span class="sxs-lookup"><span data-stu-id="36bc7-180">DeleteSelfServePolicies</span></span>](delete-a-self-serve-policy.md)

* <span data-ttu-id="36bc7-181">Kunders företagsprofil</span><span class="sxs-lookup"><span data-stu-id="36bc7-181">Customers Company Profile</span></span>
  * <span data-ttu-id="36bc7-182">[OrganizationRegistrationNumber har lagts till](create-a-customer.md)</span><span class="sxs-lookup"><span data-stu-id="36bc7-182">Added [OrganizationRegistrationNumber](create-a-customer.md)</span></span>

* <span data-ttu-id="36bc7-183">CustomerBillingProfile.DefaultAddress</span><span class="sxs-lookup"><span data-stu-id="36bc7-183">CustomerBillingProfile.DefaultAddress</span></span>
  * <span data-ttu-id="36bc7-184">MiddleName har lagts till</span><span class="sxs-lookup"><span data-stu-id="36bc7-184">Added MiddleName</span></span>

## <a name="version-1162"></a><span data-ttu-id="36bc7-185">Version 1.16.2</span><span class="sxs-lookup"><span data-stu-id="36bc7-185">Version 1.16.2</span></span>

<span data-ttu-id="36bc7-186">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.2) v1.16.2 är nu allmänt tillgänglig.</span><span class="sxs-lookup"><span data-stu-id="36bc7-186">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.2) v1.16.2 is now general availability.</span></span> <span data-ttu-id="36bc7-187">Uppdaterade [GitHub exempel](https://github.com/Microsoft/Partner-Center-DotNet-Samples) är också tillgängliga.</span><span class="sxs-lookup"><span data-stu-id="36bc7-187">Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="36bc7-188">Följande ändringar ingår i den här versionen:</span><span class="sxs-lookup"><span data-stu-id="36bc7-188">The following changes are included in this version:</span></span>

* <span data-ttu-id="36bc7-189">Uppdatera åtgärdstyper som stöds för Granskningspost.</span><span class="sxs-lookup"><span data-stu-id="36bc7-189">Update supported operation types for Audit Record.</span></span> <span data-ttu-id="36bc7-190">De nyligen tillagda är:</span><span class="sxs-lookup"><span data-stu-id="36bc7-190">The newly added ones are:</span></span>
  * <span data-ttu-id="36bc7-191">CreateSelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="36bc7-191">CreateSelfServePolicy</span></span>
  * <span data-ttu-id="36bc7-192">UpdateSelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="36bc7-192">UpdateSelfServePolicy</span></span>
  * <span data-ttu-id="36bc7-193">DeleteSelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="36bc7-193">DeleteSelfServePolicy</span></span>
  * <span data-ttu-id="36bc7-194">RemovePartnerRelationship</span><span class="sxs-lookup"><span data-stu-id="36bc7-194">RemovePartnerRelationship</span></span>
  * <span data-ttu-id="36bc7-195">DeleteTipCustomer</span><span class="sxs-lookup"><span data-stu-id="36bc7-195">DeleteTipCustomer</span></span>
  * <span data-ttu-id="36bc7-196">CreateRelatedReferral</span><span class="sxs-lookup"><span data-stu-id="36bc7-196">CreateRelatedReferral</span></span>
  * <span data-ttu-id="36bc7-197">UpdateRelatedReferral</span><span class="sxs-lookup"><span data-stu-id="36bc7-197">UpdateRelatedReferral</span></span>

* <span data-ttu-id="36bc7-198">Skapandet av tjänstbegäran är nu inaktuellt</span><span class="sxs-lookup"><span data-stu-id="36bc7-198">Service request creation is now deprecated</span></span>
* <span data-ttu-id="36bc7-199">Supportämnen är nu inaktuella</span><span class="sxs-lookup"><span data-stu-id="36bc7-199">Support topics are now deprecated</span></span>


## <a name="version-1161"></a><span data-ttu-id="36bc7-200">Version 1.16.1</span><span class="sxs-lookup"><span data-stu-id="36bc7-200">Version 1.16.1</span></span>

<span data-ttu-id="36bc7-201">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.1) v1.16.1 är nu allmänt tillgänglig.</span><span class="sxs-lookup"><span data-stu-id="36bc7-201">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.1) v1.16.1 is now general availability.</span></span> <span data-ttu-id="36bc7-202">Uppdaterade [GitHub exempel](https://github.com/Microsoft/Partner-Center-DotNet-Samples) är också tillgängliga.</span><span class="sxs-lookup"><span data-stu-id="36bc7-202">Updated [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="36bc7-203">Följande ändringar ingår i den här versionen:</span><span class="sxs-lookup"><span data-stu-id="36bc7-203">The following changes are included in this version:</span></span>

<span data-ttu-id="36bc7-204">Vi har migrerat den befintliga Microsoft Partnercenter-SDK från .NET Framework till .NET Standard 2.0-plattformen.</span><span class="sxs-lookup"><span data-stu-id="36bc7-204">We have migrated the existing Microsoft Partner Center SDK from .NET Framework to .NET Standard 2.0 platform.</span></span> <span data-ttu-id="36bc7-205">Detta gör SDK kompatibel med befintliga program med hjälp .NET Framework 4.6.1 och högre.</span><span class="sxs-lookup"><span data-stu-id="36bc7-205">This will make the SDK compatible with existing applications using .NET Framework 4.6.1 and above.</span></span> <span data-ttu-id="36bc7-206">SDK stöder .NET Core 2.0 och högre.</span><span class="sxs-lookup"><span data-stu-id="36bc7-206">The SDK will support .NET Core 2.0 and above.</span></span> <span data-ttu-id="36bc7-207">Kontrollera [.NET-implementeringsstöd](/dotnet/standard/net-standard) innan du portar det till befintliga program.</span><span class="sxs-lookup"><span data-stu-id="36bc7-207">Check [.NET implementation support](/dotnet/standard/net-standard) before porting it to existing applications.</span></span>   


## <a name="version-1153"></a><span data-ttu-id="36bc7-208">Version 1.15.3</span><span class="sxs-lookup"><span data-stu-id="36bc7-208">Version 1.15.3</span></span>
<span data-ttu-id="36bc7-209">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.15.3) v1.15.3 är nu allmänt tillgänglig.</span><span class="sxs-lookup"><span data-stu-id="36bc7-209">[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.15.3) v1.15.3 is now general availability.</span></span> <span data-ttu-id="36bc7-210">Uppdaterade REST API:er [och GitHub exempel](https://github.com/Microsoft/Partner-Center-DotNet-Samples) är också tillgängliga.</span><span class="sxs-lookup"><span data-stu-id="36bc7-210">Updated REST APIs and [GitHub samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) are also available.</span></span> <span data-ttu-id="36bc7-211">Följande ändringar ingår i den här versionen:</span><span class="sxs-lookup"><span data-stu-id="36bc7-211">The following changes are included in this version:</span></span>

* <span data-ttu-id="36bc7-212">Partneravtal</span><span class="sxs-lookup"><span data-stu-id="36bc7-212">Partner Agreement</span></span>
  * <span data-ttu-id="36bc7-213">Lade till möjligheten för indirekta leverantörer att [verifiera Microsoft-partneravtal status för indirekta återförsäljare.](verify-indirect-reseller-mpa-status.md)</span><span class="sxs-lookup"><span data-stu-id="36bc7-213">Added the ability for indirect providers to [verify Microsoft Partner Agreement status of indirect resellers](verify-indirect-reseller-mpa-status.md).</span></span>
* <span data-ttu-id="36bc7-214">Produkter</span><span class="sxs-lookup"><span data-stu-id="36bc7-214">Products</span></span>
  * <span data-ttu-id="36bc7-215">Följande två gränssnitt placerades felaktigt under namnområdet Microsoft.Store.PartnerCenter.Products.</span><span class="sxs-lookup"><span data-stu-id="36bc7-215">The following two interfaces were incorrectly placed under the Microsoft.Store.PartnerCenter.Products namespace.</span></span> <span data-ttu-id="36bc7-216">De finns nu under namnområdet Microsoft.Store.PartnerCenter.Customers.Products.</span><span class="sxs-lookup"><span data-stu-id="36bc7-216">Now, they are located under the Microsoft.Store.PartnerCenter.Customers.Products namespace.</span></span>
    * <span data-ttu-id="36bc7-217">ICustomerProductByReservationScope</span><span class="sxs-lookup"><span data-stu-id="36bc7-217">ICustomerProductByReservationScope</span></span>
    * <span data-ttu-id="36bc7-218">ICustomerSkuByReservationScope</span><span class="sxs-lookup"><span data-stu-id="36bc7-218">ICustomerSkuByReservationScope</span></span>
