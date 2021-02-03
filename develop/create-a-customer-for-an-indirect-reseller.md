---
title: Skapa en kund för en indirekt återförsäljare
description: 'Lär dig hur en indirekt Provider kan använda API: er i Partner Center för att skapa en kund för en indirekt åter försäljare.'
ms.date: 11/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: e2386f1963a5bb3ea4269bcbf4327c75987f3b91
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770177"
---
# <a name="create-a-customer-for-an-indirect-reseller-using-partner-center-apis"></a><span data-ttu-id="6fe6f-103">Skapa en kund för en indirekt åter försäljare med hjälp av API: er för partner Center</span><span class="sxs-lookup"><span data-stu-id="6fe6f-103">Create a customer for an indirect reseller using Partner Center APIs</span></span>

<span data-ttu-id="6fe6f-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="6fe6f-104">**Applies to:**</span></span>

- <span data-ttu-id="6fe6f-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="6fe6f-105">Partner Center</span></span>

<span data-ttu-id="6fe6f-106">En indirekt leverantör kan skapa en kund för en indirekt åter försäljare.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-106">An indirect provider can create a customer for an indirect reseller.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6fe6f-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="6fe6f-107">Prerequisites</span></span>

- <span data-ttu-id="6fe6f-108">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="6fe6f-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6fe6f-109">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="6fe6f-110">Klient-ID för den indirekta åter försäljaren.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-110">The tenant identifier of the indirect reseller.</span></span>

- <span data-ttu-id="6fe6f-111">Den indirekta åter försäljaren måste ha ett partnerskap med den indirekta providern.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-111">The indirect reseller must have a partnership with the indirect provider.</span></span>

## <a name="c"></a><span data-ttu-id="6fe6f-112">C\#</span><span class="sxs-lookup"><span data-stu-id="6fe6f-112">C\#</span></span>

<span data-ttu-id="6fe6f-113">Så här lägger du till en ny kund för en indirekt åter försäljare:</span><span class="sxs-lookup"><span data-stu-id="6fe6f-113">To add a new customer for an indirect reseller:</span></span>

1. <span data-ttu-id="6fe6f-114">Instansiera [**ett nytt**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) kundobjekt och instansiera sedan och fyll i [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) och [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile).</span><span class="sxs-lookup"><span data-stu-id="6fe6f-114">Instantiate a new [**Customer**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) object and then instantiate and populate the [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) and [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile).</span></span> <span data-ttu-id="6fe6f-115">Se till att tilldela ID för den indirekta åter försäljaren till [**AssociatedPartnerID**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer.associatedpartnerid) -egenskapen.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-115">Be sure to assign the indirect reseller ID to the [**AssociatedPartnerID**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer.associatedpartnerid) property.</span></span>

2. <span data-ttu-id="6fe6f-116">Använd egenskapen [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) för att hämta ett gränssnitt till kund samlings åtgärder.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-116">Use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) property to get an interface to customer collection operations.</span></span>

3. <span data-ttu-id="6fe6f-117">Anropa [**create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) -eller [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) -metoden för att skapa kunden.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-117">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) method to create the customer.</span></span>

### <a name="c-example"></a><span data-ttu-id="6fe6f-118">C- \# exempel</span><span class="sxs-lookup"><span data-stu-id="6fe6f-118">C\# example</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var indirectResellerId;
var customerToCreate = new Customer()
{
    CompanyProfile = new CustomerCompanyProfile()
    {
        Domain = string.Format(CultureInfo.InvariantCulture,
            "WingtipToys{0}.{1}",
            new Random().Next(),
            this.Context.Configuration.Scenario.CustomerDomainSuffix)
    },
    BillingProfile = new CustomerBillingProfile()
    {
        Culture = "EN-US",
        Email = "Gena@wingtiptoys.com",
        Language = "En",
        CompanyName = "Wingtip Toys" + new Random().Next(),
        DefaultAddress = new Address()
        {
            FirstName = "Gena",
            LastName = "Soto",
            AddressLine1 = "One Microsoft Way",
            City = "Redmond",
            State = "WA",
            Country = "US",
            PostalCode = "98052",
            PhoneNumber = "4255550101"
        }
    },
    AssociatedPartnerId = indirectResellerId
};

var newCustomer = partnerOperations.Customers.Create(customerToCreate);
```

<span data-ttu-id="6fe6f-119">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="6fe6f-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="6fe6f-120">**Projekt**: Partner Center SDK-exempel **klass**: CreateCustomerforIndirectReseller.CS</span><span class="sxs-lookup"><span data-stu-id="6fe6f-120">**Project**: Partner Center SDK Samples **Class**: CreateCustomerforIndirectReseller.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="6fe6f-121">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="6fe6f-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6fe6f-122">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="6fe6f-122">Request syntax</span></span>

| <span data-ttu-id="6fe6f-123">Metod</span><span class="sxs-lookup"><span data-stu-id="6fe6f-123">Method</span></span>   | <span data-ttu-id="6fe6f-124">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="6fe6f-124">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="6fe6f-125">**EFTER**</span><span class="sxs-lookup"><span data-stu-id="6fe6f-125">**POST**</span></span> | <span data-ttu-id="6fe6f-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers http/1.1</span><span class="sxs-lookup"><span data-stu-id="6fe6f-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="6fe6f-127">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="6fe6f-127">Request headers</span></span>

<span data-ttu-id="6fe6f-128">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="6fe6f-128">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6fe6f-129">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="6fe6f-129">Request body</span></span>

<span data-ttu-id="6fe6f-130">I den här tabellen beskrivs de egenskaper som krävs i begär ande texten.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-130">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="6fe6f-131">Namn</span><span class="sxs-lookup"><span data-stu-id="6fe6f-131">Name</span></span>                                          | <span data-ttu-id="6fe6f-132">Typ</span><span class="sxs-lookup"><span data-stu-id="6fe6f-132">Type</span></span>   | <span data-ttu-id="6fe6f-133">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="6fe6f-133">Required</span></span> | <span data-ttu-id="6fe6f-134">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="6fe6f-134">Description</span></span>                                                                                                                                                                                                                                                                                                                                           |
|-----------------------------------------------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="6fe6f-135">BillingProfile</span><span class="sxs-lookup"><span data-stu-id="6fe6f-135">BillingProfile</span></span>](#billing-profile)             | <span data-ttu-id="6fe6f-136">objekt</span><span class="sxs-lookup"><span data-stu-id="6fe6f-136">object</span></span> | <span data-ttu-id="6fe6f-137">Yes</span><span class="sxs-lookup"><span data-stu-id="6fe6f-137">Yes</span></span>      | <span data-ttu-id="6fe6f-138">Kundens fakturerings profil information.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-138">The customer's billing profile information.</span></span>                                                                                                                                                                                                                                                                                                           |
| [<span data-ttu-id="6fe6f-139">CompanyProfile</span><span class="sxs-lookup"><span data-stu-id="6fe6f-139">CompanyProfile</span></span>](#company-profile)             | <span data-ttu-id="6fe6f-140">objekt</span><span class="sxs-lookup"><span data-stu-id="6fe6f-140">object</span></span> | <span data-ttu-id="6fe6f-141">Yes</span><span class="sxs-lookup"><span data-stu-id="6fe6f-141">Yes</span></span>      | <span data-ttu-id="6fe6f-142">Kundens företags profil information.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-142">The customer's company profile information.</span></span>                                                               
| [<span data-ttu-id="6fe6f-143">AssociatedPartnerId</span><span class="sxs-lookup"><span data-stu-id="6fe6f-143">AssociatedPartnerId</span></span>](customer-resources.md#customer) | <span data-ttu-id="6fe6f-144">sträng</span><span class="sxs-lookup"><span data-stu-id="6fe6f-144">string</span></span> | <span data-ttu-id="6fe6f-145">Yes</span><span class="sxs-lookup"><span data-stu-id="6fe6f-145">Yes</span></span>      | <span data-ttu-id="6fe6f-146">ID för den indirekta åter försäljaren.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-146">The indirect reseller ID.</span></span> <span data-ttu-id="6fe6f-147">Den indirekta åter försäljaren som anges av det ID som anges här måste ha ett partnerskap med den indirekta providern eller så Miss förfrågans begäran.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-147">The indirect reseller as indicated by the ID supplied here must have a partnership with the indirect provider or the request will fail.</span></span> <span data-ttu-id="6fe6f-148">Observera också att om AssociatedPartnerId-värdet inte anges skapas kunden som en direkt kund för den indirekta leverantören i stället för den indirekta åter försäljaren.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-148">Also note that if the AssociatedPartnerId value isn't supplied, the customer is created as a direct customer of the indirect provider rather than the indirect reseller.</span></span> |
|<span data-ttu-id="6fe6f-149">Domain</span><span class="sxs-lookup"><span data-stu-id="6fe6f-149">Domain</span></span>| <span data-ttu-id="6fe6f-150">Sträng</span><span class="sxs-lookup"><span data-stu-id="6fe6f-150">String</span></span>| <span data-ttu-id="6fe6f-151">Yes</span><span class="sxs-lookup"><span data-stu-id="6fe6f-151">Yes</span></span>|<span data-ttu-id="6fe6f-152">Kundens domän namn, till exempel contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-152">The customer's domain name, such as contoso.onmicrosoft.com.</span></span>|
|<span data-ttu-id="6fe6f-153">organizationRegistrationNumber</span><span class="sxs-lookup"><span data-stu-id="6fe6f-153">organizationRegistrationNumber</span></span>|    <span data-ttu-id="6fe6f-154">sträng</span><span class="sxs-lookup"><span data-stu-id="6fe6f-154">string</span></span>|<span data-ttu-id="6fe6f-155">Yes</span><span class="sxs-lookup"><span data-stu-id="6fe6f-155">Yes</span></span>|     <span data-ttu-id="6fe6f-156">Kundens organisations registrerings nummer (kallas även för INN-nummer i vissa länder).</span><span class="sxs-lookup"><span data-stu-id="6fe6f-156">The customer’s organization registration number (also referred to as INN number in certain countries).</span></span> <span data-ttu-id="6fe6f-157">Krävs endast för kundens företag/organisation i följande länder.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-157">Only required for customer’s company/organization located in the following countries.</span></span> <span data-ttu-id="6fe6f-158">Armenien (AM), Azerbajdzjan (AZ), Vitryssland (av), Ungern (Slovakien), Kazakstan (KZ), Kirgizistan (KG), Moldavien (MD), Ryssland (RU), Tadzjikistan (TJ), Uzbekistan (UZ), Ukraina (UA).</span><span class="sxs-lookup"><span data-stu-id="6fe6f-158">Armenia(AM), Azerbaijan(AZ), Belarus(BY), Hungary(HU), Kazakhstan(KZ), Kyrgyzstan(KG), Moldova(MD), Russia(RU), Tajikistan(TJ), Uzbekistan(UZ), Ukraine(UA).</span></span> <span data-ttu-id="6fe6f-159">För kundens företag/organisation i andra länder bör detta inte anges.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-159">For customer’s company/organization located in other countries this should not be specified.</span></span>|



#### <a name="billing-profile"></a><span data-ttu-id="6fe6f-160">Faktureringsprofil</span><span class="sxs-lookup"><span data-stu-id="6fe6f-160">Billing profile</span></span>

<span data-ttu-id="6fe6f-161">I den här tabellen beskrivs minimi kraven för fält från [CustomerBillingProfile](customer-resources.md#customerbillingprofile) -resursen som behövs för att skapa en ny kund.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-161">This table describes the minimum required fields from the [CustomerBillingProfile](customer-resources.md#customerbillingprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="6fe6f-162">Namn</span><span class="sxs-lookup"><span data-stu-id="6fe6f-162">Name</span></span>             | <span data-ttu-id="6fe6f-163">Typ</span><span class="sxs-lookup"><span data-stu-id="6fe6f-163">Type</span></span>                                     | <span data-ttu-id="6fe6f-164">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="6fe6f-164">Required</span></span> | <span data-ttu-id="6fe6f-165">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="6fe6f-165">Description</span></span>                                                                                                                                                                                                     |
|------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6fe6f-166">e-post</span><span class="sxs-lookup"><span data-stu-id="6fe6f-166">email</span></span>            | <span data-ttu-id="6fe6f-167">sträng</span><span class="sxs-lookup"><span data-stu-id="6fe6f-167">string</span></span>                                   | <span data-ttu-id="6fe6f-168">Yes</span><span class="sxs-lookup"><span data-stu-id="6fe6f-168">Yes</span></span>      | <span data-ttu-id="6fe6f-169">Kundens e-postadress.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-169">The customer's email address.</span></span>                                                                                                                                                                                   |
| <span data-ttu-id="6fe6f-170">substrat</span><span class="sxs-lookup"><span data-stu-id="6fe6f-170">culture</span></span>          | <span data-ttu-id="6fe6f-171">sträng</span><span class="sxs-lookup"><span data-stu-id="6fe6f-171">string</span></span>                                   | <span data-ttu-id="6fe6f-172">Yes</span><span class="sxs-lookup"><span data-stu-id="6fe6f-172">Yes</span></span>      | <span data-ttu-id="6fe6f-173">Deras föredragna kultur för kommunikation och valuta, till exempel "en-US".</span><span class="sxs-lookup"><span data-stu-id="6fe6f-173">Their preferred culture for communication and currency, such as "en-US".</span></span> <span data-ttu-id="6fe6f-174">Se de [språk som stöds av Partner Center och nationella inställningar](partner-center-supported-languages-and-locales.md) för de kulturer som stöds.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-174">See [Partner Center supported languages and locales](partner-center-supported-languages-and-locales.md) for the supported cultures.</span></span> |
| <span data-ttu-id="6fe6f-175">language</span><span class="sxs-lookup"><span data-stu-id="6fe6f-175">language</span></span>         | <span data-ttu-id="6fe6f-176">sträng</span><span class="sxs-lookup"><span data-stu-id="6fe6f-176">string</span></span>                                   | <span data-ttu-id="6fe6f-177">Yes</span><span class="sxs-lookup"><span data-stu-id="6fe6f-177">Yes</span></span>      | <span data-ttu-id="6fe6f-178">Standard språket.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-178">The default language.</span></span> <span data-ttu-id="6fe6f-179">Två characters språk koder (till exempel `en` eller `fr` ) stöds.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-179">Two character language codes (for example `en` or `fr`) are supported.</span></span>                                                                                                                                |
| <span data-ttu-id="6fe6f-180">företags \_ namn</span><span class="sxs-lookup"><span data-stu-id="6fe6f-180">company\_name</span></span>    | <span data-ttu-id="6fe6f-181">sträng</span><span class="sxs-lookup"><span data-stu-id="6fe6f-181">string</span></span>                                   | <span data-ttu-id="6fe6f-182">Yes</span><span class="sxs-lookup"><span data-stu-id="6fe6f-182">Yes</span></span>      | <span data-ttu-id="6fe6f-183">Registrerat företags-/organisations namn.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-183">The registered company/organization name.</span></span>                                                                                                                                                                       |
| <span data-ttu-id="6fe6f-184">standard \_ adress</span><span class="sxs-lookup"><span data-stu-id="6fe6f-184">default\_address</span></span> | [<span data-ttu-id="6fe6f-185">Adress</span><span class="sxs-lookup"><span data-stu-id="6fe6f-185">Address</span></span>](utility-resources.md#address) | <span data-ttu-id="6fe6f-186">Yes</span><span class="sxs-lookup"><span data-stu-id="6fe6f-186">Yes</span></span>      | <span data-ttu-id="6fe6f-187">Den registrerade adressen för kundens företag/organisation.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-187">The registered address of the customer's company/organization.</span></span> <span data-ttu-id="6fe6f-188">Se [adress](utility-resources.md#address) resursen för information om eventuella längd begränsningar.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-188">See the [Address](utility-resources.md#address) resource for information on any length limitations.</span></span>                                             |

#### <a name="company-profile"></a><span data-ttu-id="6fe6f-189">Företags profil</span><span class="sxs-lookup"><span data-stu-id="6fe6f-189">Company profile</span></span>

<span data-ttu-id="6fe6f-190">I den här tabellen beskrivs minimi kraven för fält från [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) -resursen som behövs för att skapa en ny kund.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-190">This table describes the minimum required fields from the [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="6fe6f-191">Namn</span><span class="sxs-lookup"><span data-stu-id="6fe6f-191">Name</span></span>   | <span data-ttu-id="6fe6f-192">Typ</span><span class="sxs-lookup"><span data-stu-id="6fe6f-192">Type</span></span>   | <span data-ttu-id="6fe6f-193">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="6fe6f-193">Required</span></span> | <span data-ttu-id="6fe6f-194">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="6fe6f-194">Description</span></span>                                                  |
|--------|--------|----------|--------------------------------------------------------------|
| <span data-ttu-id="6fe6f-195">domän</span><span class="sxs-lookup"><span data-stu-id="6fe6f-195">domain</span></span> | <span data-ttu-id="6fe6f-196">sträng</span><span class="sxs-lookup"><span data-stu-id="6fe6f-196">string</span></span> | <span data-ttu-id="6fe6f-197">Yes</span><span class="sxs-lookup"><span data-stu-id="6fe6f-197">Yes</span></span>     | <span data-ttu-id="6fe6f-198">Kundens domän namn, till exempel contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-198">The customer's domain name, such as contoso.onmicrosoft.com.</span></span> |
| <span data-ttu-id="6fe6f-199">organizationRegistrationNumber</span><span class="sxs-lookup"><span data-stu-id="6fe6f-199">organizationRegistrationNumber</span></span> | <span data-ttu-id="6fe6f-200">sträng</span><span class="sxs-lookup"><span data-stu-id="6fe6f-200">string</span></span> | <span data-ttu-id="6fe6f-201">Är beroende av villkor</span><span class="sxs-lookup"><span data-stu-id="6fe6f-201">Depends on condition</span></span> | <span data-ttu-id="6fe6f-202">Kundens organisations registrerings nummer (kallas även för INN-numret i vissa länder).</span><span class="sxs-lookup"><span data-stu-id="6fe6f-202">The customer’s organization registration number (also referred to as the INN number in certain countries).</span></span> <br/><br/><span data-ttu-id="6fe6f-203">Du behöver bara fylla i det här fältet om en kunds företag/organisation finns i följande länder:</span><span class="sxs-lookup"><span data-stu-id="6fe6f-203">Completing this field is required only if a customer’s company/organization is located in the following countries:</span></span> <br/><br/><span data-ttu-id="6fe6f-204">-Armenien (AM)</span><span class="sxs-lookup"><span data-stu-id="6fe6f-204">- Armenia (AM)</span></span> <br/><span data-ttu-id="6fe6f-205">– Azerbajdzjan (AZ)</span><span class="sxs-lookup"><span data-stu-id="6fe6f-205">- Azerbaijan (AZ)</span></span><br/><span data-ttu-id="6fe6f-206">– Vitryssland (av)</span><span class="sxs-lookup"><span data-stu-id="6fe6f-206">- Belarus (BY)</span></span><br/><span data-ttu-id="6fe6f-207">– Ungern (HU)</span><span class="sxs-lookup"><span data-stu-id="6fe6f-207">- Hungary (HU)</span></span><br/><span data-ttu-id="6fe6f-208">-Kazakstan (KZ)</span><span class="sxs-lookup"><span data-stu-id="6fe6f-208">- Kazakhstan (KZ)</span></span><br/><span data-ttu-id="6fe6f-209">– Kirgizistan (KG)</span><span class="sxs-lookup"><span data-stu-id="6fe6f-209">- Kyrgyzstan (KG)</span></span><br/><span data-ttu-id="6fe6f-210">– Moldavien (MD)</span><span class="sxs-lookup"><span data-stu-id="6fe6f-210">- Moldova (MD)</span></span><br/><span data-ttu-id="6fe6f-211">– Ryssland (RU)</span><span class="sxs-lookup"><span data-stu-id="6fe6f-211">- Russia (RU)</span></span><br/><span data-ttu-id="6fe6f-212">– Tadzjikistan (TJ)</span><span class="sxs-lookup"><span data-stu-id="6fe6f-212">- Tajikistan (TJ)</span></span><br/><span data-ttu-id="6fe6f-213">-Uzbekistan (UZ)</span><span class="sxs-lookup"><span data-stu-id="6fe6f-213">- Uzbekistan (UZ)</span></span><br/><span data-ttu-id="6fe6f-214">-Ukraina (UA)</span><span class="sxs-lookup"><span data-stu-id="6fe6f-214">- Ukraine (UA)</span></span><br/><br/><span data-ttu-id="6fe6f-215">Det här fältet krävs inte om kundens företag/organisation finns i andra länder än de som visas här.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-215">This field is not required if the customer’s company/organization is located in other countries beyond those shown here.</span></span>  |

### <a name="request-example"></a><span data-ttu-id="6fe6f-216">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="6fe6f-216">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers HTTP/1.1
Authorization: Bearer <token>
MS-RequestId: d628adbe-b7ee-412e-ac55-58f22b4ba2f4
MS-CorrelationId: 0dd197a8-992c-44ca-aeae-21cd83494dce
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 823
Expect: 100-continue
Connection: Keep-Alive

{
    "Id": null,
    "CommerceId": null,
    "CompanyProfile": {
        "TenantId": null,
        "Domain": "WingtipToys678152504.onmicrosoft.com",
        "CompanyName": null,
        "Attributes": {
            "ObjectType": "CustomerCompanyProfile"
        }
    },
    "BillingProfile": {
        "Id": null,
        "FirstName": null,
        "LastName": null,
        "Email": "Gena@wingtiptoys.com",
        "Culture": "EN-US",
        "Language": "En",
        "CompanyName": "Wingtip Toys678152504",
        "DefaultAddress": {
            "Country": "US",
            "Region": null,
            "City": "Redmond",
            "State": "WA",
            "AddressLine1": "One Microsoft Way",
            "AddressLine2": null,
            "PostalCode": "98052",
            "FirstName": "Gena",
            "LastName": "Soto",
            "PhoneNumber": "4255550101"
        },
        "Attributes": {
            "ObjectType": "CustomerBillingProfile"
        }
    },
    "RelationshipToPartner": "none",
    "AllowDelegatedAccess": null,
    "UserCredentials": null,
    "CustomDomains": null,
    "AssociatedPartnerId": "484e548c-f5f3-4528-93a9-c16c6373cb59",
    "Attributes": {
        "ObjectType": "Customer"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="6fe6f-217">REST-svar</span><span class="sxs-lookup"><span data-stu-id="6fe6f-217">REST response</span></span>

<span data-ttu-id="6fe6f-218">Om det lyckas innehåller svaret en [kund](customer-resources.md#customer) resurs för den nya kunden.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-218">If successful, the response contains a [Customer](customer-resources.md#customer) resource for the new customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6fe6f-219">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="6fe6f-219">Response success and error codes</span></span>

<span data-ttu-id="6fe6f-220">Svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-220">Responses come with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6fe6f-221">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-221">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="6fe6f-222">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="6fe6f-222">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="6fe6f-223">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="6fe6f-223">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 1085
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 0dd197a8-992c-44ca-aeae-21cd83494dce
MS-RequestId: d628adbe-b7ee-412e-ac55-58f22b4ba2f4
MS-CV: Yy/YaA0gYEmfQyR/.0
MS-ServerId: 030020525
Date: Tue, 06 Jun 2017 23:11:40 GMT

{
    "id": "626099fe-17af-4756-9fd0-6a73b7127859",
    "commerceId": "626099fe-17af-4756-9fd0-6a73b7127859",
    "companyProfile": {
        "tenantId": "626099fe-17af-4756-9fd0-6a73b7127859",
        "domain": "WingtipToys678152504.onmicrosoft.com",
        "companyName": "Wingtip Toys678152504",
        "links": {
            "self": {
                "uri": "/customers/626099fe-17af-4756-9fd0-6a73b7127859/profiles/company",
                "method": "GET",
                "headers": []
            }
        },
        "attributes": {
            "objectType": "CustomerCompanyProfile"
        }
    },
    "billingProfile": {
        "id": "7079246e-7b62-56ef-7cbd-a819514b54b5",
        "email": "Gena@wingtiptoys.com",
        "culture": "en-US",
        "language": "En",
        "companyName": "Wingtip Toys678152504",
        "defaultAddress": {
            "country": "US",
            "city": "Redmond",
            "state": "WA",
            "addressLine1": "One Microsoft Way",
            "postalCode": "98052",
            "firstName": "Gena",
            "lastName": "Soto",
            "phoneNumber": "4255550101"
        },
        "attributes": {
            "etag": "-8799889149591823008",
            "objectType": "CustomerBillingProfile"
        }
    },
    "relationshipToPartner": "reseller",
    "allowDelegatedAccess": true,
    "userCredentials": {
        "userName": "admin",
        "password": "0Krha*Io"
    },
    "associatedPartnerId": "484e548c-f5f3-4528-93a9-c16c6373cb59",
    "attributes": {
        "objectType": "Customer"
    }
}
```