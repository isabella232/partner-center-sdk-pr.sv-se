---
title: Skapa en kund för en indirekt återförsäljare
description: Lär dig hur en indirekt leverantör kan använda Partner Center-API:er för att skapa en kund för en indirekt återförsäljare.
ms.date: 04/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 9a6218aeb61f3775c89d34b4d57a17741e3a1e93
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973748"
---
# <a name="create-a-customer-for-an-indirect-reseller-using-partner-center-apis"></a><span data-ttu-id="7b253-103">Skapa en kund för en indirekt återförsäljare med partnercenter-API:er</span><span class="sxs-lookup"><span data-stu-id="7b253-103">Create a customer for an indirect reseller using Partner Center APIs</span></span>

<span data-ttu-id="7b253-104">En indirekt leverantör kan skapa en kund för en indirekt återförsäljare.</span><span class="sxs-lookup"><span data-stu-id="7b253-104">An indirect provider can create a customer for an indirect reseller.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b253-105">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="7b253-105">Prerequisites</span></span>

- <span data-ttu-id="7b253-106">Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="7b253-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7b253-107">Det här scenariot stöder endast autentisering med app+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="7b253-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="7b253-108">Klientorganisations-ID för den indirekta återförsäljaren.</span><span class="sxs-lookup"><span data-stu-id="7b253-108">The tenant identifier of the indirect reseller.</span></span>

- <span data-ttu-id="7b253-109">Den indirekta återförsäljaren måste ha ett samarbete med den indirekta leverantören.</span><span class="sxs-lookup"><span data-stu-id="7b253-109">The indirect reseller must have a partnership with the indirect provider.</span></span>

## <a name="c"></a><span data-ttu-id="7b253-110">C\#</span><span class="sxs-lookup"><span data-stu-id="7b253-110">C\#</span></span>

<span data-ttu-id="7b253-111">Så här lägger du till en ny kund för en indirekt återförsäljare:</span><span class="sxs-lookup"><span data-stu-id="7b253-111">To add a new customer for an indirect reseller:</span></span>

1. <span data-ttu-id="7b253-112">Skapa en instans av [**ett nytt**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) kundobjekt och skapa en instans av och fyll i [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) [**och CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile).</span><span class="sxs-lookup"><span data-stu-id="7b253-112">Instantiate a new [**Customer**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) object and then instantiate and populate the [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) and [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile).</span></span> <span data-ttu-id="7b253-113">Se till att tilldela det indirekta återförsäljar-ID:t till [**egenskapen AssociatedPartnerID.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer.associatedpartnerid)</span><span class="sxs-lookup"><span data-stu-id="7b253-113">Be sure to assign the indirect reseller ID to the [**AssociatedPartnerID**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer.associatedpartnerid) property.</span></span>

2. <span data-ttu-id="7b253-114">Använd egenskapen [**IAggregatePartner.Customers för**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) att hämta ett gränssnitt för kundinsamlingsåtgärder.</span><span class="sxs-lookup"><span data-stu-id="7b253-114">Use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) property to get an interface to customer collection operations.</span></span>

3. <span data-ttu-id="7b253-115">Anropa metoden [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) eller [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) för att skapa kunden.</span><span class="sxs-lookup"><span data-stu-id="7b253-115">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) method to create the customer.</span></span>

### <a name="c-example"></a><span data-ttu-id="7b253-116">\#C-exempel</span><span class="sxs-lookup"><span data-stu-id="7b253-116">C\# example</span></span>

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

<span data-ttu-id="7b253-117">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="7b253-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="7b253-118">**Project:** Partnercenter-SDK Samples **Class**: CreateCustomerforIndirectReseller.cs</span><span class="sxs-lookup"><span data-stu-id="7b253-118">**Project**: Partner Center SDK Samples **Class**: CreateCustomerforIndirectReseller.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="7b253-119">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="7b253-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7b253-120">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="7b253-120">Request syntax</span></span>

| <span data-ttu-id="7b253-121">Metod</span><span class="sxs-lookup"><span data-stu-id="7b253-121">Method</span></span>   | <span data-ttu-id="7b253-122">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="7b253-122">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="7b253-123">**Inlägg**</span><span class="sxs-lookup"><span data-stu-id="7b253-123">**POST**</span></span> | <span data-ttu-id="7b253-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="7b253-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="7b253-125">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="7b253-125">Request headers</span></span>

<span data-ttu-id="7b253-126">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="7b253-126">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7b253-127">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="7b253-127">Request body</span></span>

<span data-ttu-id="7b253-128">I den här tabellen beskrivs de obligatoriska egenskaperna i begärandetexten.</span><span class="sxs-lookup"><span data-stu-id="7b253-128">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="7b253-129">Namn</span><span class="sxs-lookup"><span data-stu-id="7b253-129">Name</span></span>                                          | <span data-ttu-id="7b253-130">Typ</span><span class="sxs-lookup"><span data-stu-id="7b253-130">Type</span></span>   | <span data-ttu-id="7b253-131">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="7b253-131">Required</span></span> | <span data-ttu-id="7b253-132">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="7b253-132">Description</span></span>                                                                                                                                                                                                                                                                                                                                           |
|-----------------------------------------------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="7b253-133">BillingProfile</span><span class="sxs-lookup"><span data-stu-id="7b253-133">BillingProfile</span></span>](#billing-profile)             | <span data-ttu-id="7b253-134">objekt</span><span class="sxs-lookup"><span data-stu-id="7b253-134">object</span></span> | <span data-ttu-id="7b253-135">Ja</span><span class="sxs-lookup"><span data-stu-id="7b253-135">Yes</span></span>      | <span data-ttu-id="7b253-136">Kundens faktureringsprofilinformation.</span><span class="sxs-lookup"><span data-stu-id="7b253-136">The customer's billing profile information.</span></span>                                                                                                                                                                                                                                                                                                           |
| [<span data-ttu-id="7b253-137">CompanyProfile</span><span class="sxs-lookup"><span data-stu-id="7b253-137">CompanyProfile</span></span>](#company-profile)             | <span data-ttu-id="7b253-138">objekt</span><span class="sxs-lookup"><span data-stu-id="7b253-138">object</span></span> | <span data-ttu-id="7b253-139">Ja</span><span class="sxs-lookup"><span data-stu-id="7b253-139">Yes</span></span>      | <span data-ttu-id="7b253-140">Kundens företagsinformation.</span><span class="sxs-lookup"><span data-stu-id="7b253-140">The customer's company profile information.</span></span>                                                               
| [<span data-ttu-id="7b253-141">AssociatedPartnerId</span><span class="sxs-lookup"><span data-stu-id="7b253-141">AssociatedPartnerId</span></span>](customer-resources.md#customer) | <span data-ttu-id="7b253-142">sträng</span><span class="sxs-lookup"><span data-stu-id="7b253-142">string</span></span> | <span data-ttu-id="7b253-143">Ja</span><span class="sxs-lookup"><span data-stu-id="7b253-143">Yes</span></span>      | <span data-ttu-id="7b253-144">Det indirekta återförsäljar-ID:t.</span><span class="sxs-lookup"><span data-stu-id="7b253-144">The indirect reseller ID.</span></span> <span data-ttu-id="7b253-145">Den indirekta återförsäljaren som anges av det ID som anges här måste ha ett samarbete med den indirekta leverantören, annars misslyckas begäran.</span><span class="sxs-lookup"><span data-stu-id="7b253-145">The indirect reseller as indicated by the ID supplied here must have a partnership with the indirect provider or the request will fail.</span></span> <span data-ttu-id="7b253-146">Observera också att om värdet AssociatedPartnerId inte anges skapas kunden som en direkt kund till den indirekta leverantören i stället för den indirekta återförsäljaren.</span><span class="sxs-lookup"><span data-stu-id="7b253-146">Also note that if the AssociatedPartnerId value isn't supplied, the customer is created as a direct customer of the indirect provider rather than the indirect reseller.</span></span> |
|<span data-ttu-id="7b253-147">Domain</span><span class="sxs-lookup"><span data-stu-id="7b253-147">Domain</span></span>| <span data-ttu-id="7b253-148">Sträng</span><span class="sxs-lookup"><span data-stu-id="7b253-148">String</span></span>| <span data-ttu-id="7b253-149">Ja</span><span class="sxs-lookup"><span data-stu-id="7b253-149">Yes</span></span>|<span data-ttu-id="7b253-150">Kundens domännamn, till exempel contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="7b253-150">The customer's domain name, such as contoso.onmicrosoft.com.</span></span>|
|<span data-ttu-id="7b253-151">organizationRegistrationNumber</span><span class="sxs-lookup"><span data-stu-id="7b253-151">organizationRegistrationNumber</span></span>|    <span data-ttu-id="7b253-152">sträng</span><span class="sxs-lookup"><span data-stu-id="7b253-152">string</span></span>|<span data-ttu-id="7b253-153">Ja</span><span class="sxs-lookup"><span data-stu-id="7b253-153">Yes</span></span>|     <span data-ttu-id="7b253-154">Kundens organisationsregistreringsnummer (kallas även INN-nummer i vissa länder).</span><span class="sxs-lookup"><span data-stu-id="7b253-154">The customer’s organization registration number (also referred to as INN number in certain countries).</span></span> <span data-ttu-id="7b253-155">Krävs endast för kundens företag/organisation som finns i följande länder: Förargiga(AM), Gör(AZ), Gör(BY), För kunden(HU), För kundens företag/organisation som finns i följande länder: Förargande(AM), Förargare(AM), Förargare (AZ), För kunden(BY), För kunden krävs att du väljer Att göra så här: Kyrgyzstan(KG), Kyrgyzstan(KG), Hubar(MD), Ryssland(RU), Kerikistan (TJ), Kerten (CUS), Kerten(1996), Hubs(1996), 1996 (1996).</span><span class="sxs-lookup"><span data-stu-id="7b253-155">Only required for customer’s company/organization located in the following countries: Armenia(AM), Azerbaijan(AZ), Belarus(BY), Hungary(HU), Kazakhstan(KZ), Kyrgyzstan(KG), Moldova(MD), Russia(RU), Tajikistan(TJ), Uzbekistan(UZ), Ukraine(UA), India, Brazil, South Africa, Poland, United Arab Emirates, Saudi Arabia, Turkey, Thailand, Vietnam, Myanmar, Iraq, South Sudan, and Venezuela.</span></span> <span data-ttu-id="7b253-156">För kundens företag/organisation som finns i andra länder är detta ett valfritt fält.</span><span class="sxs-lookup"><span data-stu-id="7b253-156">For customer’s company/organization located in other countries this is an optional field.</span></span>|



#### <a name="billing-profile"></a><span data-ttu-id="7b253-157">Faktureringsprofil</span><span class="sxs-lookup"><span data-stu-id="7b253-157">Billing profile</span></span>

<span data-ttu-id="7b253-158">I den här tabellen beskrivs de minsta obligatoriska fälten från [resursen CustomerBillingProfile](customer-resources.md#customerbillingprofile) som krävs för att skapa en ny kund.</span><span class="sxs-lookup"><span data-stu-id="7b253-158">This table describes the minimum required fields from the [CustomerBillingProfile](customer-resources.md#customerbillingprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="7b253-159">Namn</span><span class="sxs-lookup"><span data-stu-id="7b253-159">Name</span></span>             | <span data-ttu-id="7b253-160">Typ</span><span class="sxs-lookup"><span data-stu-id="7b253-160">Type</span></span>                                     | <span data-ttu-id="7b253-161">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="7b253-161">Required</span></span> | <span data-ttu-id="7b253-162">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="7b253-162">Description</span></span>                                                                                                                                                                                                     |
|------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7b253-163">e-post</span><span class="sxs-lookup"><span data-stu-id="7b253-163">email</span></span>            | <span data-ttu-id="7b253-164">sträng</span><span class="sxs-lookup"><span data-stu-id="7b253-164">string</span></span>                                   | <span data-ttu-id="7b253-165">Ja</span><span class="sxs-lookup"><span data-stu-id="7b253-165">Yes</span></span>      | <span data-ttu-id="7b253-166">Kundens e-postadress.</span><span class="sxs-lookup"><span data-stu-id="7b253-166">The customer's email address.</span></span>                                                                                                                                                                                   |
| <span data-ttu-id="7b253-167">Kultur</span><span class="sxs-lookup"><span data-stu-id="7b253-167">culture</span></span>          | <span data-ttu-id="7b253-168">sträng</span><span class="sxs-lookup"><span data-stu-id="7b253-168">string</span></span>                                   | <span data-ttu-id="7b253-169">Ja</span><span class="sxs-lookup"><span data-stu-id="7b253-169">Yes</span></span>      | <span data-ttu-id="7b253-170">Deras önskade kultur för kommunikation och valuta, till exempel "en-US".</span><span class="sxs-lookup"><span data-stu-id="7b253-170">Their preferred culture for communication and currency, such as "en-US".</span></span> <span data-ttu-id="7b253-171">Se [Språk och språk som stöds i Partnercenter för](partner-center-supported-languages-and-locales.md) de kulturer som stöds.</span><span class="sxs-lookup"><span data-stu-id="7b253-171">See [Partner Center supported languages and locales](partner-center-supported-languages-and-locales.md) for the supported cultures.</span></span> |
| <span data-ttu-id="7b253-172">language</span><span class="sxs-lookup"><span data-stu-id="7b253-172">language</span></span>         | <span data-ttu-id="7b253-173">sträng</span><span class="sxs-lookup"><span data-stu-id="7b253-173">string</span></span>                                   | <span data-ttu-id="7b253-174">Ja</span><span class="sxs-lookup"><span data-stu-id="7b253-174">Yes</span></span>      | <span data-ttu-id="7b253-175">Standardspråket.</span><span class="sxs-lookup"><span data-stu-id="7b253-175">The default language.</span></span> <span data-ttu-id="7b253-176">Två teckenspråkkoder (till `en` exempel `fr` eller ) stöds.</span><span class="sxs-lookup"><span data-stu-id="7b253-176">Two character language codes (for example `en` or `fr`) are supported.</span></span>                                                                                                                                |
| <span data-ttu-id="7b253-177">\_företagsnamn</span><span class="sxs-lookup"><span data-stu-id="7b253-177">company\_name</span></span>    | <span data-ttu-id="7b253-178">sträng</span><span class="sxs-lookup"><span data-stu-id="7b253-178">string</span></span>                                   | <span data-ttu-id="7b253-179">Ja</span><span class="sxs-lookup"><span data-stu-id="7b253-179">Yes</span></span>      | <span data-ttu-id="7b253-180">Det registrerade företags-/organisationsnamnet.</span><span class="sxs-lookup"><span data-stu-id="7b253-180">The registered company/organization name.</span></span>                                                                                                                                                                       |
| <span data-ttu-id="7b253-181">\_standardadress</span><span class="sxs-lookup"><span data-stu-id="7b253-181">default\_address</span></span> | [<span data-ttu-id="7b253-182">Adress</span><span class="sxs-lookup"><span data-stu-id="7b253-182">Address</span></span>](utility-resources.md#address) | <span data-ttu-id="7b253-183">Ja</span><span class="sxs-lookup"><span data-stu-id="7b253-183">Yes</span></span>      | <span data-ttu-id="7b253-184">Den registrerade adressen för kundens företag/organisation.</span><span class="sxs-lookup"><span data-stu-id="7b253-184">The registered address of the customer's company/organization.</span></span> <span data-ttu-id="7b253-185">Se [Adressresurs](utility-resources.md#address) för information om eventuella längdbegränsningar.</span><span class="sxs-lookup"><span data-stu-id="7b253-185">See the [Address](utility-resources.md#address) resource for information on any length limitations.</span></span>                                             |

#### <a name="company-profile"></a><span data-ttu-id="7b253-186">Företagsprofil</span><span class="sxs-lookup"><span data-stu-id="7b253-186">Company profile</span></span>

<span data-ttu-id="7b253-187">I den här tabellen beskrivs de minsta obligatoriska fälten från [resursen CustomerCompanyProfile](customer-resources.md#customercompanyprofile) som krävs för att skapa en ny kund.</span><span class="sxs-lookup"><span data-stu-id="7b253-187">This table describes the minimum required fields from the [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="7b253-188">Namn</span><span class="sxs-lookup"><span data-stu-id="7b253-188">Name</span></span>   | <span data-ttu-id="7b253-189">Typ</span><span class="sxs-lookup"><span data-stu-id="7b253-189">Type</span></span>   | <span data-ttu-id="7b253-190">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="7b253-190">Required</span></span> | <span data-ttu-id="7b253-191">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="7b253-191">Description</span></span>                                                  |
|--------|--------|----------|--------------------------------------------------------------|
| <span data-ttu-id="7b253-192">domän</span><span class="sxs-lookup"><span data-stu-id="7b253-192">domain</span></span> | <span data-ttu-id="7b253-193">sträng</span><span class="sxs-lookup"><span data-stu-id="7b253-193">string</span></span> | <span data-ttu-id="7b253-194">Ja</span><span class="sxs-lookup"><span data-stu-id="7b253-194">Yes</span></span>     | <span data-ttu-id="7b253-195">Kundens domännamn, till exempel contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="7b253-195">The customer's domain name, such as contoso.onmicrosoft.com.</span></span> |
| <span data-ttu-id="7b253-196">organizationRegistrationNumber</span><span class="sxs-lookup"><span data-stu-id="7b253-196">organizationRegistrationNumber</span></span> | <span data-ttu-id="7b253-197">sträng</span><span class="sxs-lookup"><span data-stu-id="7b253-197">string</span></span> | <span data-ttu-id="7b253-198">Beror på villkor</span><span class="sxs-lookup"><span data-stu-id="7b253-198">Depends on condition</span></span> | <span data-ttu-id="7b253-199">Kundens organisationsregistreringsnummer (kallas även INN-nummer i vissa länder).</span><span class="sxs-lookup"><span data-stu-id="7b253-199">The customer’s organization registration number (also referred to as the INN number in certain countries).</span></span> <br/><br/><span data-ttu-id="7b253-200">Du behöver bara slutföra det här fältet om en kunds företag/organisation finns i följande länder:</span><span class="sxs-lookup"><span data-stu-id="7b253-200">Completing this field is required only if a customer’s company/organization is located in the following countries:</span></span> <br/><br/><span data-ttu-id="7b253-201">– 10:00 (AM)</span><span class="sxs-lookup"><span data-stu-id="7b253-201">- Armenia (AM)</span></span> <br/><span data-ttu-id="7b253-202">– På så vis (AZ)</span><span class="sxs-lookup"><span data-stu-id="7b253-202">- Azerbaijan (AZ)</span></span><br/><span data-ttu-id="7b253-203">– På så vis (BY)</span><span class="sxs-lookup"><span data-stu-id="7b253-203">- Belarus (BY)</span></span><br/><span data-ttu-id="7b253-204">– På så vis (HU)</span><span class="sxs-lookup"><span data-stu-id="7b253-204">- Hungary (HU)</span></span><br/><span data-ttu-id="7b253-205">– Förlamning (KZ)</span><span class="sxs-lookup"><span data-stu-id="7b253-205">- Kazakhstan (KZ)</span></span><br/><span data-ttu-id="7b253-206">– Kyrgyzstan (KG)</span><span class="sxs-lookup"><span data-stu-id="7b253-206">- Kyrgyzstan (KG)</span></span><br/><span data-ttu-id="7b253-207">– Så här gör du (MD)</span><span class="sxs-lookup"><span data-stu-id="7b253-207">- Moldova (MD)</span></span><br/><span data-ttu-id="7b253-208">– Ryssland (RU)</span><span class="sxs-lookup"><span data-stu-id="7b253-208">- Russia (RU)</span></span><br/><span data-ttu-id="7b253-209">–Istikistan (TJ)</span><span class="sxs-lookup"><span data-stu-id="7b253-209">- Tajikistan (TJ)</span></span><br/><span data-ttu-id="7b253-210">–Istan ( CITY)</span><span class="sxs-lookup"><span data-stu-id="7b253-210">- Uzbekistan (UZ)</span></span><br/><span data-ttu-id="7b253-211">– Äldsta (UA)</span><span class="sxs-lookup"><span data-stu-id="7b253-211">- Ukraine (UA)</span></span><br/><span data-ttu-id="7b253-212">– Indien</span><span class="sxs-lookup"><span data-stu-id="7b253-212">- India</span></span> <br/><span data-ttu-id="7b253-213">– Brasilien</span><span class="sxs-lookup"><span data-stu-id="7b253-213">- Brazil</span></span> <br/><span data-ttu-id="7b253-214">– Sydafrika</span><span class="sxs-lookup"><span data-stu-id="7b253-214">- South Africa</span></span> <br/><span data-ttu-id="7b253-215">– På så vis</span><span class="sxs-lookup"><span data-stu-id="7b253-215">- Poland</span></span> <br/><span data-ttu-id="7b253-216">– Förenade Arabemiraten</span><span class="sxs-lookup"><span data-stu-id="7b253-216">- United Arab Emirates</span></span> <br/><span data-ttu-id="7b253-217">– Saudiarabien</span><span class="sxs-lookup"><span data-stu-id="7b253-217">- Saudi Arabia</span></span> <br/><span data-ttu-id="7b253-218">– På så vis</span><span class="sxs-lookup"><span data-stu-id="7b253-218">- Turkey</span></span> <br/><span data-ttu-id="7b253-219">– På så vis</span><span class="sxs-lookup"><span data-stu-id="7b253-219">- Thailand</span></span> <br/><span data-ttu-id="7b253-220">– Vietnam</span><span class="sxs-lookup"><span data-stu-id="7b253-220">- Vietnam</span></span> <br/><span data-ttu-id="7b253-221">– På så vis</span><span class="sxs-lookup"><span data-stu-id="7b253-221">- Myanmar</span></span> <br/><span data-ttu-id="7b253-222">– På så sätt kan du</span><span class="sxs-lookup"><span data-stu-id="7b253-222">- Iraq</span></span> <br/><span data-ttu-id="7b253-223">– Sydsudan</span><span class="sxs-lookup"><span data-stu-id="7b253-223">- South Sudan</span></span> <br/><span data-ttu-id="7b253-224">– På så vis</span><span class="sxs-lookup"><span data-stu-id="7b253-224">- Venezuela</span></span><br/> <br/><span data-ttu-id="7b253-225">För kundens företag/organisation som finns i andra länder är detta ett valfritt fält.</span><span class="sxs-lookup"><span data-stu-id="7b253-225">For customer’s company/organization located in other countries, this is an optional field.</span></span>  |

### <a name="request-example"></a><span data-ttu-id="7b253-226">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="7b253-226">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="7b253-227">REST-svar</span><span class="sxs-lookup"><span data-stu-id="7b253-227">REST response</span></span>

<span data-ttu-id="7b253-228">Om det lyckas innehåller svaret en [kundresurs](customer-resources.md#customer) för den nya kunden.</span><span class="sxs-lookup"><span data-stu-id="7b253-228">If successful, the response contains a [Customer](customer-resources.md#customer) resource for the new customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7b253-229">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="7b253-229">Response success and error codes</span></span>

<span data-ttu-id="7b253-230">Svar har en HTTP-statuskod som anger att det lyckats eller misslyckats och ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="7b253-230">Responses come with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7b253-231">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="7b253-231">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7b253-232">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="7b253-232">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="7b253-233">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="7b253-233">Response example</span></span>

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