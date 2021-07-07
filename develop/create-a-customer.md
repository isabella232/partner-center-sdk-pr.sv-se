---
title: Skapa en kund
description: Lär dig hur en Molnlösningsleverantör(CSP)-partner kan använda Partner Center-API:er för att skapa en ny kund. I artikeln beskrivs förutsättningar och vad som händer mer.
ms.date: 03/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 6232ca77d057f2f5168b73d81ec551669d540246
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973731"
---
# <a name="create-a-customer-using-partner-center-apis"></a><span data-ttu-id="48ed5-104">Skapa en kund med partnercenter-API:er</span><span class="sxs-lookup"><span data-stu-id="48ed5-104">Create a customer using Partner Center APIs</span></span>

<span data-ttu-id="48ed5-105">**Gäller för:** Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="48ed5-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="48ed5-106">Den här artikeln beskriver hur du skapar en ny kund.</span><span class="sxs-lookup"><span data-stu-id="48ed5-106">This article explains how to create a new customer.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="48ed5-107">Om du är en indirekt leverantör och vill skapa en kund för en indirekt återförsäljare kan du se [Skapa en kund för en indirekt återförsäljare.](create-a-customer-for-an-indirect-reseller.md)</span><span class="sxs-lookup"><span data-stu-id="48ed5-107">If you are an indirect provider and you want to create a customer for an indirect reseller, please see [Create a customer for an indirect reseller](create-a-customer-for-an-indirect-reseller.md).</span></span>

<span data-ttu-id="48ed5-108">Som CSP-partner (molnlösningsleverantör) kan du, när du skapar en kund, göra beställningar åt kunden.</span><span class="sxs-lookup"><span data-stu-id="48ed5-108">As a cloud solution provider (CSP) partner, when you create a customer you can place orders on behalf of the customer.</span></span> <span data-ttu-id="48ed5-109">När du skapar en kund skapar du även:</span><span class="sxs-lookup"><span data-stu-id="48ed5-109">When you create a customer, you also create:</span></span>

- <span data-ttu-id="48ed5-110">Ett Azure Active Directory (AD)-klientobjekt för kunden.</span><span class="sxs-lookup"><span data-stu-id="48ed5-110">An Azure Active Directory (AD) tenant object for the customer.</span></span>

- <span data-ttu-id="48ed5-111">En relation mellan återförsäljaren och kunden som används för delegerade administratörsbehörigheter.</span><span class="sxs-lookup"><span data-stu-id="48ed5-111">A relationship between the reseller and customer, used for delegated admin privileges.</span></span>

- <span data-ttu-id="48ed5-112">Ett användarnamn och lösenord för att logga in som administratör för kunden.</span><span class="sxs-lookup"><span data-stu-id="48ed5-112">A user name and password to sign in as an admin for the customer.</span></span>

<span data-ttu-id="48ed5-113">När kunden har skapats ska du spara kund-ID och Azure AD-information för framtida användning med Partnercenter-SDK (till exempel kontohantering).</span><span class="sxs-lookup"><span data-stu-id="48ed5-113">Once the customer is created, be sure to save the customer ID and Azure AD details for future use with the Partner Center SDK (for example, account management).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="48ed5-114">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="48ed5-114">Prerequisites</span></span>

- <span data-ttu-id="48ed5-115">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="48ed5-115">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="48ed5-116">Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="48ed5-116">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="48ed5-117">Om du vill skapa en kundklientorganisation måste du ange en giltig fysisk adress under skapandeprocessen.</span><span class="sxs-lookup"><span data-stu-id="48ed5-117">To create a customer tenant you must provide a valid physical address during the creation process.</span></span> <span data-ttu-id="48ed5-118">En adress kan verifieras genom att följa stegen i scenariot [Verifiera en](validate-an-address.md) adress.</span><span class="sxs-lookup"><span data-stu-id="48ed5-118">An address can be validated by following the steps outlined in the [Validate an address](validate-an-address.md) scenario.</span></span> <span data-ttu-id="48ed5-119">Om du skapar en kund med en ogiltig adress i sandbox-miljön kan du inte ta bort den kundklientorganisationen.</span><span class="sxs-lookup"><span data-stu-id="48ed5-119">If you create a customer using an invalid address in the sandbox environment, you will not be able to delete that customer tenant.</span></span>

## <a name="c"></a><span data-ttu-id="48ed5-120">C\#</span><span class="sxs-lookup"><span data-stu-id="48ed5-120">C\#</span></span>

<span data-ttu-id="48ed5-121">Så här lägger du till en kund:</span><span class="sxs-lookup"><span data-stu-id="48ed5-121">To add a customer:</span></span>

1. <span data-ttu-id="48ed5-122">Instansiera ett nytt [**kundobjekt.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer)</span><span class="sxs-lookup"><span data-stu-id="48ed5-122">Instantiate a new [**Customer**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) object.</span></span> <span data-ttu-id="48ed5-123">Se till att fylla i [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) och [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile).</span><span class="sxs-lookup"><span data-stu-id="48ed5-123">Be sure to fill in the [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) and [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile).</span></span>

2. <span data-ttu-id="48ed5-124">Lägg till den nya kunden i din [**IAggregatePartner.Customers-samling**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) genom att [**anropa Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) eller [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync).</span><span class="sxs-lookup"><span data-stu-id="48ed5-124">Add the new customer to your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection by calling [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync).</span></span>

### <a name="c-example"></a><span data-ttu-id="48ed5-125">\#C-exempel</span><span class="sxs-lookup"><span data-stu-id="48ed5-125">C\# example</span></span>

```csharp
// IAggregatePartner partnerOperations;

var partnerOperations = this.Context.UserPartnerOperations;

var customerToCreate = new Customer()
{
    CompanyProfile = new CustomerCompanyProfile()
    {
        Domain = string.Format(CultureInfo.InvariantCulture,
            "SampleApplication{0}.{1}",
            new Random().Next(),
            this.Context.Configuration.Scenario.CustomerDomainSuffix),
        //// OrganizationRegistrationNumber = "123456" // Please add if in specific country that requires
    },
    BillingProfile = new CustomerBillingProfile()
    {
        Culture = "EN-US",
        Email = "someone@example.com",
        Language = "En",
        CompanyName = "Some Company" + new Random().Next(),
        DefaultAddress = new Address()
        {
            FirstName = "Tania",
            MiddleName = "MiddleName",
            LastName = "Carr",
            AddressLine1 = "One Microsoft Way",
            City = "Redmond",
            State = "WA",
            Country = "US",
            PostalCode = "98052",
            PhoneNumber = ""
        }
    }
};

var newCustomer = partnerOperations.Customers.Create(customerToCreate);
```

<span data-ttu-id="48ed5-126">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="48ed5-126">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="48ed5-127">**Project:** Partnercenter-SDK Samples **Class**: CreateCustomer.cs</span><span class="sxs-lookup"><span data-stu-id="48ed5-127">**Project**: Partner Center SDK Samples **Class**: CreateCustomer.cs</span></span>

## <a name="java"></a><span data-ttu-id="48ed5-128">Java</span><span class="sxs-lookup"><span data-stu-id="48ed5-128">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="48ed5-129">Så här skapar du en ny kund:</span><span class="sxs-lookup"><span data-stu-id="48ed5-129">To create a new customer:</span></span>

1. <span data-ttu-id="48ed5-130">Skapa en ny instans av **objekten CustomerBillingProfile** och **CustomerCompanyProfile.**</span><span class="sxs-lookup"><span data-stu-id="48ed5-130">Create a new instance of the **CustomerBillingProfile** and the **CustomerCompanyProfile** objects.</span></span> <span data-ttu-id="48ed5-131">Se till att fylla i de obligatoriska fälten.</span><span class="sxs-lookup"><span data-stu-id="48ed5-131">Be sure to populate the required fields.</span></span>

2. <span data-ttu-id="48ed5-132">Skapa kunden genom att anropa **funktionen IAggregatePartner.getCustomers().create.**</span><span class="sxs-lookup"><span data-stu-id="48ed5-132">Create the customer by calling the **IAggregatePartner.getCustomers().create** function.</span></span>

### <a name="java-example"></a><span data-ttu-id="48ed5-133">Java-exempel</span><span class="sxs-lookup"><span data-stu-id="48ed5-133">Java example</span></span>

```java
// IAggregatePartner partnerOperations;

Address address = new Address();

address.setFirstName( "Gena" );
address.setLastName( "Soto" );
address.setAddressLine1( "One Microsoft Way" );
address.setCity( "Redmond" );
address.setState( "WA" );
address.setCountry( "US" );
address.setPostalCode( "98052" );
address.setPhoneNumber( "4255550101" );

CustomerBillingProfile billingProfile = new CustomerBillingProfile();

billingProfile.setCulture( "en-US" );
billingProfile.setEmail( "gena@wingtiptoys.com" );
billingProfile.setLanguage( "en" );
billingProfile.setCompanyName( "Wingtip Toys" + new Random().nextInt() );
billingProfile.setDefaultAddress( address );

CustomerCompanyProfile companyProfile = new CustomerCompanyProfile();

companyProfile.setDomain( "WingtipToys" + Math.abs( new Random().nextInt() ) + ".onmicrosoft.com" );

Customer customerToCreate = new Customer();

customerToCreate.setBillingProfile( billingProfile );
customerToCreate.setCompanyProfile( companyProfile );

Customer newCustomer = partnerOperations.getCustomers().create( customerToCreate );
```

## <a name="powershell"></a><span data-ttu-id="48ed5-134">PowerShell</span><span class="sxs-lookup"><span data-stu-id="48ed5-134">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="48ed5-135">Skapa en kund genom att köra [**kommandot New-PartnerCustomer.**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomer.md)</span><span class="sxs-lookup"><span data-stu-id="48ed5-135">To create a customer, execute the [**New-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomer.md) command.</span></span>

```powershell
New-PartnerCustomer -BillingAddressLine1 '1 Microsoft Way' -BillingAddressCity 'Redmond' -BillingAddressCountry 'US' -BillingAddressPostalCode '98052' -BillingAddressState 'WA' -ContactEmail 'jdoe@customer.com' -ContactFirstName 'Jane' -ContactLastName 'Doe' -Culture 'en-US' -Domain 'newcustomer.onmicrosoft.com' -Language 'en' -Name 'New Customer'
```

## <a name="rest-request"></a><span data-ttu-id="48ed5-136">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="48ed5-136">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="48ed5-137">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="48ed5-137">Request syntax</span></span>

| <span data-ttu-id="48ed5-138">Metod</span><span class="sxs-lookup"><span data-stu-id="48ed5-138">Method</span></span>   | <span data-ttu-id="48ed5-139">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="48ed5-139">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="48ed5-140">**Inlägg**</span><span class="sxs-lookup"><span data-stu-id="48ed5-140">**POST**</span></span> | <span data-ttu-id="48ed5-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="48ed5-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="48ed5-142">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="48ed5-142">Request headers</span></span>

- <span data-ttu-id="48ed5-143">Det här API:et är idempotent (det ger inte ett annat resultat om du anropar det flera gånger).</span><span class="sxs-lookup"><span data-stu-id="48ed5-143">This API is idempotent (it will not yield a different result if you call it multiple times).</span></span>

- <span data-ttu-id="48ed5-144">Ett begärande-ID och korrelations-ID krävs.</span><span class="sxs-lookup"><span data-stu-id="48ed5-144">A request ID and correlation ID are required.</span></span>

- <span data-ttu-id="48ed5-145">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="48ed5-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="48ed5-146">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="48ed5-146">Request body</span></span>

<span data-ttu-id="48ed5-147">I den här tabellen beskrivs de obligatoriska egenskaperna i begärandetexten.</span><span class="sxs-lookup"><span data-stu-id="48ed5-147">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="48ed5-148">Namn</span><span class="sxs-lookup"><span data-stu-id="48ed5-148">Name</span></span>                              | <span data-ttu-id="48ed5-149">Typ</span><span class="sxs-lookup"><span data-stu-id="48ed5-149">Type</span></span>   | <span data-ttu-id="48ed5-150">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="48ed5-150">Description</span></span>                                 |
|-----------------------------------|--------|---------------------------------------------|
| [<span data-ttu-id="48ed5-151">BillingProfile</span><span class="sxs-lookup"><span data-stu-id="48ed5-151">BillingProfile</span></span>](#billing-profile) | <span data-ttu-id="48ed5-152">objekt</span><span class="sxs-lookup"><span data-stu-id="48ed5-152">object</span></span> | <span data-ttu-id="48ed5-153">Kundens faktureringsprofilinformation.</span><span class="sxs-lookup"><span data-stu-id="48ed5-153">The customer's billing profile information.</span></span> |
| [<span data-ttu-id="48ed5-154">CompanyProfile</span><span class="sxs-lookup"><span data-stu-id="48ed5-154">CompanyProfile</span></span>](#company-profile) | <span data-ttu-id="48ed5-155">objekt</span><span class="sxs-lookup"><span data-stu-id="48ed5-155">object</span></span> | <span data-ttu-id="48ed5-156">Kundens företagsinformation.</span><span class="sxs-lookup"><span data-stu-id="48ed5-156">The customer's company profile information.</span></span> |

#### <a name="billing-profile"></a><span data-ttu-id="48ed5-157">Faktureringsprofil</span><span class="sxs-lookup"><span data-stu-id="48ed5-157">Billing profile</span></span>

<span data-ttu-id="48ed5-158">I den här tabellen beskrivs de minsta obligatoriska fälten från [resursen CustomerBillingProfile](customer-resources.md#customerbillingprofile) som krävs för att skapa en ny kund.</span><span class="sxs-lookup"><span data-stu-id="48ed5-158">This table describes the minimum required fields from the [CustomerBillingProfile](customer-resources.md#customerbillingprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="48ed5-159">Namn</span><span class="sxs-lookup"><span data-stu-id="48ed5-159">Name</span></span>             | <span data-ttu-id="48ed5-160">Typ</span><span class="sxs-lookup"><span data-stu-id="48ed5-160">Type</span></span>                                     | <span data-ttu-id="48ed5-161">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="48ed5-161">Description</span></span>                                                                                                                                                                                                     |
|------------------|------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="48ed5-162">e-post</span><span class="sxs-lookup"><span data-stu-id="48ed5-162">email</span></span>            | <span data-ttu-id="48ed5-163">sträng</span><span class="sxs-lookup"><span data-stu-id="48ed5-163">string</span></span>                                   | <span data-ttu-id="48ed5-164">Kundens e-postadress.</span><span class="sxs-lookup"><span data-stu-id="48ed5-164">The customer's email address.</span></span>                                                                                                                                                                                   |
| <span data-ttu-id="48ed5-165">Kultur</span><span class="sxs-lookup"><span data-stu-id="48ed5-165">culture</span></span>          | <span data-ttu-id="48ed5-166">sträng</span><span class="sxs-lookup"><span data-stu-id="48ed5-166">string</span></span>                                   | <span data-ttu-id="48ed5-167">Deras önskade kultur för kommunikation och valuta, till exempel "en-US".</span><span class="sxs-lookup"><span data-stu-id="48ed5-167">Their preferred culture for communication and currency, such as "en-US".</span></span> <span data-ttu-id="48ed5-168">Se [Partnercenter– språk och språk som stöds](partner-center-supported-languages-and-locales.md) för de kulturer som stöds.</span><span class="sxs-lookup"><span data-stu-id="48ed5-168">See [Partner Center supported languages and locales](partner-center-supported-languages-and-locales.md) for the supported cultures.</span></span> |
| <span data-ttu-id="48ed5-169">language</span><span class="sxs-lookup"><span data-stu-id="48ed5-169">language</span></span>         | <span data-ttu-id="48ed5-170">sträng</span><span class="sxs-lookup"><span data-stu-id="48ed5-170">string</span></span>                                   | <span data-ttu-id="48ed5-171">Standardspråket.</span><span class="sxs-lookup"><span data-stu-id="48ed5-171">The default language.</span></span> <span data-ttu-id="48ed5-172">Två teckenspråkkoder (till `en` exempel `fr` eller ) stöds.</span><span class="sxs-lookup"><span data-stu-id="48ed5-172">Two character language codes (for example `en` or `fr`) are supported.</span></span>                                                                                                                                |
| <span data-ttu-id="48ed5-173">\_företagsnamn</span><span class="sxs-lookup"><span data-stu-id="48ed5-173">company\_name</span></span>    | <span data-ttu-id="48ed5-174">sträng</span><span class="sxs-lookup"><span data-stu-id="48ed5-174">string</span></span>                                   | <span data-ttu-id="48ed5-175">Det registrerade företags-/organisationsnamnet.</span><span class="sxs-lookup"><span data-stu-id="48ed5-175">The registered company/organization name.</span></span>                                                                                                                                                                       |
| <span data-ttu-id="48ed5-176">\_standardadress</span><span class="sxs-lookup"><span data-stu-id="48ed5-176">default\_address</span></span> | [<span data-ttu-id="48ed5-177">Adress</span><span class="sxs-lookup"><span data-stu-id="48ed5-177">Address</span></span>](utility-resources.md#address) | <span data-ttu-id="48ed5-178">Den registrerade adressen för kundens företag/organisation.</span><span class="sxs-lookup"><span data-stu-id="48ed5-178">The registered address of the customer's company/organization.</span></span> <span data-ttu-id="48ed5-179">Se [Adressresurs](utility-resources.md#address) för information om eventuella längdbegränsningar.</span><span class="sxs-lookup"><span data-stu-id="48ed5-179">See the [Address](utility-resources.md#address) resource for information on any length limitations.</span></span>                                             |

#### <a name="company-profile"></a><span data-ttu-id="48ed5-180">Företagsprofil</span><span class="sxs-lookup"><span data-stu-id="48ed5-180">Company profile</span></span>

<span data-ttu-id="48ed5-181">I den här tabellen beskrivs de minsta obligatoriska fälten från [resursen CustomerCompanyProfile](customer-resources.md#customercompanyprofile) som krävs för att skapa en ny kund.</span><span class="sxs-lookup"><span data-stu-id="48ed5-181">This table describes the minimum required fields from the [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="48ed5-182">Namn</span><span class="sxs-lookup"><span data-stu-id="48ed5-182">Name</span></span>   | <span data-ttu-id="48ed5-183">Typ</span><span class="sxs-lookup"><span data-stu-id="48ed5-183">Type</span></span>   | <span data-ttu-id="48ed5-184">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="48ed5-184">Description</span></span>                                                  |
|--------|--------|--------------------------------------------------------------|
| <span data-ttu-id="48ed5-185">domän</span><span class="sxs-lookup"><span data-stu-id="48ed5-185">domain</span></span> | <span data-ttu-id="48ed5-186">sträng</span><span class="sxs-lookup"><span data-stu-id="48ed5-186">string</span></span> | <span data-ttu-id="48ed5-187">Kundens domännamn, till exempel contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="48ed5-187">The customer's domain name, such as contoso.onmicrosoft.com.</span></span> |
|<span data-ttu-id="48ed5-188">organizationRegistrationNumber</span><span class="sxs-lookup"><span data-stu-id="48ed5-188">organizationRegistrationNumber</span></span>|<span data-ttu-id="48ed5-189">Sträng</span><span class="sxs-lookup"><span data-stu-id="48ed5-189">String</span></span>|<span data-ttu-id="48ed5-190">Kundens organisationsregistreringsnummer (kallas även INN-nummer i vissa länder).</span><span class="sxs-lookup"><span data-stu-id="48ed5-190">The customer’s organization registration number (also referred to as INN number in certain countries).</span></span> <span data-ttu-id="48ed5-191">Krävs endast för kundens företag/organisation som finns i följande länder: DoS(AM), DoS (AZ), Hubs(BY), För kunden(HU), För e-post i KZ, Kyrgyzstan(KG), För att få hjälp med det, För att göra det kan du till exempel skriva en lista över frågor som inte kan användas.</span><span class="sxs-lookup"><span data-stu-id="48ed5-191">Only required for customer’s company/organization located in the following countries: Armenia(AM), Azerbaijan(AZ), Belarus(BY), Hungary(HU), Kazakhstan(KZ), Kyrgyzstan(KG), Moldova(MD), Russia(RU), Tajikistan(TJ), Uzbekistan(UZ), Ukraine(UA), Brazil(BR), India, South Africa, Poland, United Arab Emirates, Saudi Arabia, Turkey, Thailand, Vietnam, Myanmar, Iraq, South Sudan, and Venezuela.</span></span> <span data-ttu-id="48ed5-192">För kundens företag/organisation som finns i andra länder är detta ett valfritt fält.</span><span class="sxs-lookup"><span data-stu-id="48ed5-192">For customer’s company/organization located in other countries, this is an optional field.</span></span>|

### <a name="request-example"></a><span data-ttu-id="48ed5-193">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="48ed5-193">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 789
Expect: 100-continue
Connection: Keep-Alive

{
    "CompanyProfile": {
        "Domain": "xyz.ccsctp.net",
    },
    "BillingProfile": {
        "Culture": "EN-US",
        "Email": "test@outlook.com",
        "Language": "en",
        "CompanyName": "test company",
        "DefaultAddress": {
            "FirstName": "Test",
            "LastName": "Test",
            "AddressLine1": "One Microsoft Way",
            "City": "Redmond",
            "State": "WA",
            "PostalCode": "98052",
            "Country": "US",
        }
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="48ed5-194">REST-svar</span><span class="sxs-lookup"><span data-stu-id="48ed5-194">REST response</span></span>

<span data-ttu-id="48ed5-195">Om det lyckas returnerar detta API [en kundresurs](customer-resources.md#customer) för den nya kunden.</span><span class="sxs-lookup"><span data-stu-id="48ed5-195">If successful, this API returns a [Customer](customer-resources.md#customer) resource for the new customer.</span></span> <span data-ttu-id="48ed5-196">Spara kund-ID och Azure AD-information för framtida användning med Partnercenter-SDK.</span><span class="sxs-lookup"><span data-stu-id="48ed5-196">Save the customer ID and Azure AD details for future use with the Partner Center SDK.</span></span> <span data-ttu-id="48ed5-197">Du behöver dem till exempel för användning med kontohantering.</span><span class="sxs-lookup"><span data-stu-id="48ed5-197">You will need them for use with account management, for example.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="48ed5-198">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="48ed5-198">Response success and error codes</span></span>

<span data-ttu-id="48ed5-199">Svar har en HTTP-statuskod som anger att det lyckats eller misslyckats samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="48ed5-199">Responses come with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="48ed5-200">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="48ed5-200">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="48ed5-201">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="48ed5-201">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="48ed5-202">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="48ed5-202">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 834
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CV: ObwhuhD2tUKJoM+Z.0
MS-ServerId: 202010223
Date: Tue, 14 Feb 2017 20:06:02 GMT

{
    "id": "dfd8cc0a-c592-468c-8461-869a38d24738",
    "commerceId": "0a4ce58a-6f96-4273-8035-d9c7d31b9ba4",
    "companyProfile": {
        "tenantId": "dfd8cc0a-c592-468c-8461-869a38d24738",
        "domain": "xyz.ccsctp.net",
        "attributes": {
            "objectType": "CustomerCompanyProfile"
        }
    },
    "billingProfile": {
        "id": "d17c0275-da92-5c33-9032-782ef1d0b69b",
        "email": "test@outlook.com",
        "culture": "en-US",
        "language": "en",
        "companyName": "test company",
        "defaultAddress": {
            "country": "US",
            "city": "Redmond",
            "state": "WA",
            "addressLine1": "One Microsoft Way",
            "postalCode": "98052",
            "firstName": "Test",
            "lastName": "Test",
            "phoneNumber": ""
        },
        "attributes": {
            "etag": "5920358838484612121",
            "objectType": "CustomerBillingProfile"
        }
    },
    "relationshipToPartner": "none",
    "userCredentials": {
        "userName": "admin",
        "password": "=;;n.=s9Z"
    },
    "attributes": {
        "objectType": "Customer"
    }
}
```
