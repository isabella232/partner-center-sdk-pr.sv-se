---
title: Skapa en kund
description: 'Lär dig hur en partner av en moln lösnings leverantör (CSP) kan använda API: er för partner Center för att skapa en ny kund. Artikeln beskriver krav och vad som händer mer.'
ms.date: 03/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: bc8e9d38353511e747ba4da99b11be40d08781e3
ms.sourcegitcommit: faea78fe3264cbafc2b02c04d98d5ce30e992124
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/03/2021
ms.locfileid: "106274605"
---
# <a name="create-a-customer-using-partner-center-apis"></a><span data-ttu-id="1d3f6-104">Skapa en kund med hjälp av API: er för partner Center</span><span class="sxs-lookup"><span data-stu-id="1d3f6-104">Create a customer using Partner Center APIs</span></span>

<span data-ttu-id="1d3f6-105">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="1d3f6-105">**Applies to:**</span></span>

- <span data-ttu-id="1d3f6-106">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="1d3f6-106">Partner Center</span></span>
- <span data-ttu-id="1d3f6-107">Partnercenter drivs av 21Vianet</span><span class="sxs-lookup"><span data-stu-id="1d3f6-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="1d3f6-108">Välkommen till Partnercenter för Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="1d3f6-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="1d3f6-109">Den här artikeln beskriver hur du skapar en ny kund.</span><span class="sxs-lookup"><span data-stu-id="1d3f6-109">This article explains how to create a new customer.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1d3f6-110">Om du är en indirekt leverantör och vill skapa en kund för en indirekt åter försäljare, se [skapa en kund för en indirekt åter försäljare](create-a-customer-for-an-indirect-reseller.md).</span><span class="sxs-lookup"><span data-stu-id="1d3f6-110">If you are an indirect provider and you want to create a customer for an indirect reseller, please see [Create a customer for an indirect reseller](create-a-customer-for-an-indirect-reseller.md).</span></span>

<span data-ttu-id="1d3f6-111">Som en partner av en moln lösnings leverantör (CSP) kan du, när du skapar en kund, placera beställningar för kundens räkning.</span><span class="sxs-lookup"><span data-stu-id="1d3f6-111">As a cloud solution provider (CSP) partner, when you create a customer you can place orders on behalf of the customer.</span></span> <span data-ttu-id="1d3f6-112">När du skapar en kund skapar du även:</span><span class="sxs-lookup"><span data-stu-id="1d3f6-112">When you create a customer, you also create:</span></span>

- <span data-ttu-id="1d3f6-113">Ett Azure Active Directory (AD) klient objekt för kunden.</span><span class="sxs-lookup"><span data-stu-id="1d3f6-113">An Azure Active Directory (AD) tenant object for the customer.</span></span>

- <span data-ttu-id="1d3f6-114">En relation mellan åter försäljaren och kunden, som används för delegerade administratörs privilegier.</span><span class="sxs-lookup"><span data-stu-id="1d3f6-114">A relationship between the reseller and customer, used for delegated admin privileges.</span></span>

- <span data-ttu-id="1d3f6-115">Ett användar namn och lösen ord för att logga in som administratör för kunden.</span><span class="sxs-lookup"><span data-stu-id="1d3f6-115">A user name and password to sign in as an admin for the customer.</span></span>

<span data-ttu-id="1d3f6-116">När kunden har skapats, se till att spara kund-ID och Azure AD-information för framtida användning med partner Center SDK (till exempel konto hantering).</span><span class="sxs-lookup"><span data-stu-id="1d3f6-116">Once the customer is created, be sure to save the customer ID and Azure AD details for future use with the Partner Center SDK (for example, account management).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1d3f6-117">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="1d3f6-117">Prerequisites</span></span>

- <span data-ttu-id="1d3f6-118">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="1d3f6-118">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1d3f6-119">Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="1d3f6-119">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1d3f6-120">Om du vill skapa en kund klient organisation måste du ange en giltig fysisk adress under skapande processen.</span><span class="sxs-lookup"><span data-stu-id="1d3f6-120">To create a customer tenant you must provide a valid physical address during the creation process.</span></span> <span data-ttu-id="1d3f6-121">En adress kan verifieras genom att följa stegen som beskrivs i avsnittet [validera ett adress](validate-an-address.md) scenario.</span><span class="sxs-lookup"><span data-stu-id="1d3f6-121">An address can be validated by following the steps outlined in the [Validate an address](validate-an-address.md) scenario.</span></span> <span data-ttu-id="1d3f6-122">Om du skapar en kund med en ogiltig adress i sandbox-miljön kommer du inte att kunna ta bort den kund klienten.</span><span class="sxs-lookup"><span data-stu-id="1d3f6-122">If you create a customer using an invalid address in the sandbox environment, you will not be able to delete that customer tenant.</span></span>

## <a name="c"></a><span data-ttu-id="1d3f6-123">C\#</span><span class="sxs-lookup"><span data-stu-id="1d3f6-123">C\#</span></span>

<span data-ttu-id="1d3f6-124">Så här lägger du till en kund:</span><span class="sxs-lookup"><span data-stu-id="1d3f6-124">To add a customer:</span></span>

1. <span data-ttu-id="1d3f6-125">Instansiera ett nytt [**kund**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) objekt.</span><span class="sxs-lookup"><span data-stu-id="1d3f6-125">Instantiate a new [**Customer**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) object.</span></span> <span data-ttu-id="1d3f6-126">Se till att fylla i [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) och [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile).</span><span class="sxs-lookup"><span data-stu-id="1d3f6-126">Be sure to fill in the [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) and [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile).</span></span>

2. <span data-ttu-id="1d3f6-127">Lägg till den nya kunden i din [**IAggregatePartner. Customer**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) -samling genom att anropa [**create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) eller [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync).</span><span class="sxs-lookup"><span data-stu-id="1d3f6-127">Add the new customer to your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection by calling [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync).</span></span>

### <a name="c-example"></a><span data-ttu-id="1d3f6-128">C- \# exempel</span><span class="sxs-lookup"><span data-stu-id="1d3f6-128">C\# example</span></span>

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

<span data-ttu-id="1d3f6-129">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="1d3f6-129">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="1d3f6-130">**Projekt**: Partner Center SDK-exempel **klass**: CreateCustomer. CS</span><span class="sxs-lookup"><span data-stu-id="1d3f6-130">**Project**: Partner Center SDK Samples **Class**: CreateCustomer.cs</span></span>

## <a name="java"></a><span data-ttu-id="1d3f6-131">Java</span><span class="sxs-lookup"><span data-stu-id="1d3f6-131">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="1d3f6-132">Så här skapar du en ny kund:</span><span class="sxs-lookup"><span data-stu-id="1d3f6-132">To create a new customer:</span></span>

1. <span data-ttu-id="1d3f6-133">Skapa en ny instans av **CustomerBillingProfile** och **CustomerCompanyProfile** -objekten.</span><span class="sxs-lookup"><span data-stu-id="1d3f6-133">Create a new instance of the **CustomerBillingProfile** and the **CustomerCompanyProfile** objects.</span></span> <span data-ttu-id="1d3f6-134">Var noga med att fylla i de obligatoriska fälten.</span><span class="sxs-lookup"><span data-stu-id="1d3f6-134">Be sure to populate the required fields.</span></span>

2. <span data-ttu-id="1d3f6-135">Skapa kunden genom att anropa funktionen **IAggregatePartner. getCustomers (). Create** .</span><span class="sxs-lookup"><span data-stu-id="1d3f6-135">Create the customer by calling the **IAggregatePartner.getCustomers().create** function.</span></span>

### <a name="java-example"></a><span data-ttu-id="1d3f6-136">Java-exempel</span><span class="sxs-lookup"><span data-stu-id="1d3f6-136">Java example</span></span>

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

## <a name="powershell"></a><span data-ttu-id="1d3f6-137">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1d3f6-137">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="1d3f6-138">Om du vill skapa en kund kör du kommandot [**New-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomer.md) .</span><span class="sxs-lookup"><span data-stu-id="1d3f6-138">To create a customer execute the [**New-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomer.md) command.</span></span>

```powershell
New-PartnerCustomer -BillingAddressLine1 '1 Microsoft Way' -BillingAddressCity 'Redmond' -BillingAddressCountry 'US' -BillingAddressPostalCode '98052' -BillingAddressState 'WA' -ContactEmail 'jdoe@customer.com' -ContactFirstName 'Jane' -ContactLastName 'Doe' -Culture 'en-US' -Domain 'newcustomer.onmicrosoft.com' -Language 'en' -Name 'New Customer'
```

## <a name="rest-request"></a><span data-ttu-id="1d3f6-139">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="1d3f6-139">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1d3f6-140">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="1d3f6-140">Request syntax</span></span>

| <span data-ttu-id="1d3f6-141">Metod</span><span class="sxs-lookup"><span data-stu-id="1d3f6-141">Method</span></span>   | <span data-ttu-id="1d3f6-142">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="1d3f6-142">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="1d3f6-143">**EFTER**</span><span class="sxs-lookup"><span data-stu-id="1d3f6-143">**POST**</span></span> | <span data-ttu-id="1d3f6-144">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers http/1.1</span><span class="sxs-lookup"><span data-stu-id="1d3f6-144">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="1d3f6-145">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="1d3f6-145">Request headers</span></span>

- <span data-ttu-id="1d3f6-146">Detta API är idempotenta (det ger inte något annat resultat om du anropar det flera gånger).</span><span class="sxs-lookup"><span data-stu-id="1d3f6-146">This API is idempotent (it will not yield a different result if you call it multiple times).</span></span>

- <span data-ttu-id="1d3f6-147">ID för begäran och korrelations-ID krävs.</span><span class="sxs-lookup"><span data-stu-id="1d3f6-147">A request ID and correlation ID are required.</span></span>

- <span data-ttu-id="1d3f6-148">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="1d3f6-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1d3f6-149">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="1d3f6-149">Request body</span></span>

<span data-ttu-id="1d3f6-150">I den här tabellen beskrivs de egenskaper som krävs i begär ande texten.</span><span class="sxs-lookup"><span data-stu-id="1d3f6-150">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="1d3f6-151">Namn</span><span class="sxs-lookup"><span data-stu-id="1d3f6-151">Name</span></span>                              | <span data-ttu-id="1d3f6-152">Typ</span><span class="sxs-lookup"><span data-stu-id="1d3f6-152">Type</span></span>   | <span data-ttu-id="1d3f6-153">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="1d3f6-153">Description</span></span>                                 |
|-----------------------------------|--------|---------------------------------------------|
| [<span data-ttu-id="1d3f6-154">BillingProfile</span><span class="sxs-lookup"><span data-stu-id="1d3f6-154">BillingProfile</span></span>](#billing-profile) | <span data-ttu-id="1d3f6-155">objekt</span><span class="sxs-lookup"><span data-stu-id="1d3f6-155">object</span></span> | <span data-ttu-id="1d3f6-156">Kundens fakturerings profil information.</span><span class="sxs-lookup"><span data-stu-id="1d3f6-156">The customer's billing profile information.</span></span> |
| [<span data-ttu-id="1d3f6-157">CompanyProfile</span><span class="sxs-lookup"><span data-stu-id="1d3f6-157">CompanyProfile</span></span>](#company-profile) | <span data-ttu-id="1d3f6-158">objekt</span><span class="sxs-lookup"><span data-stu-id="1d3f6-158">object</span></span> | <span data-ttu-id="1d3f6-159">Kundens företags profil information.</span><span class="sxs-lookup"><span data-stu-id="1d3f6-159">The customer's company profile information.</span></span> |

#### <a name="billing-profile"></a><span data-ttu-id="1d3f6-160">Faktureringsprofil</span><span class="sxs-lookup"><span data-stu-id="1d3f6-160">Billing profile</span></span>

<span data-ttu-id="1d3f6-161">I den här tabellen beskrivs minimi kraven för fält från [CustomerBillingProfile](customer-resources.md#customerbillingprofile) -resursen som behövs för att skapa en ny kund.</span><span class="sxs-lookup"><span data-stu-id="1d3f6-161">This table describes the minimum required fields from the [CustomerBillingProfile](customer-resources.md#customerbillingprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="1d3f6-162">Namn</span><span class="sxs-lookup"><span data-stu-id="1d3f6-162">Name</span></span>             | <span data-ttu-id="1d3f6-163">Typ</span><span class="sxs-lookup"><span data-stu-id="1d3f6-163">Type</span></span>                                     | <span data-ttu-id="1d3f6-164">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="1d3f6-164">Description</span></span>                                                                                                                                                                                                     |
|------------------|------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1d3f6-165">e-post</span><span class="sxs-lookup"><span data-stu-id="1d3f6-165">email</span></span>            | <span data-ttu-id="1d3f6-166">sträng</span><span class="sxs-lookup"><span data-stu-id="1d3f6-166">string</span></span>                                   | <span data-ttu-id="1d3f6-167">Kundens e-postadress.</span><span class="sxs-lookup"><span data-stu-id="1d3f6-167">The customer's email address.</span></span>                                                                                                                                                                                   |
| <span data-ttu-id="1d3f6-168">substrat</span><span class="sxs-lookup"><span data-stu-id="1d3f6-168">culture</span></span>          | <span data-ttu-id="1d3f6-169">sträng</span><span class="sxs-lookup"><span data-stu-id="1d3f6-169">string</span></span>                                   | <span data-ttu-id="1d3f6-170">Deras föredragna kultur för kommunikation och valuta, till exempel "en-US".</span><span class="sxs-lookup"><span data-stu-id="1d3f6-170">Their preferred culture for communication and currency, such as "en-US".</span></span> <span data-ttu-id="1d3f6-171">Se de [språk som stöds av Partner Center och nationella inställningar](partner-center-supported-languages-and-locales.md) för de kulturer som stöds.</span><span class="sxs-lookup"><span data-stu-id="1d3f6-171">See [Partner Center supported languages and locales](partner-center-supported-languages-and-locales.md) for the supported cultures.</span></span> |
| <span data-ttu-id="1d3f6-172">language</span><span class="sxs-lookup"><span data-stu-id="1d3f6-172">language</span></span>         | <span data-ttu-id="1d3f6-173">sträng</span><span class="sxs-lookup"><span data-stu-id="1d3f6-173">string</span></span>                                   | <span data-ttu-id="1d3f6-174">Standard språket.</span><span class="sxs-lookup"><span data-stu-id="1d3f6-174">The default language.</span></span> <span data-ttu-id="1d3f6-175">Två characters språk koder (till exempel `en` eller `fr` ) stöds.</span><span class="sxs-lookup"><span data-stu-id="1d3f6-175">Two character language codes (for example `en` or `fr`) are supported.</span></span>                                                                                                                                |
| <span data-ttu-id="1d3f6-176">företags \_ namn</span><span class="sxs-lookup"><span data-stu-id="1d3f6-176">company\_name</span></span>    | <span data-ttu-id="1d3f6-177">sträng</span><span class="sxs-lookup"><span data-stu-id="1d3f6-177">string</span></span>                                   | <span data-ttu-id="1d3f6-178">Registrerat företags-/organisations namn.</span><span class="sxs-lookup"><span data-stu-id="1d3f6-178">The registered company/organization name.</span></span>                                                                                                                                                                       |
| <span data-ttu-id="1d3f6-179">standard \_ adress</span><span class="sxs-lookup"><span data-stu-id="1d3f6-179">default\_address</span></span> | [<span data-ttu-id="1d3f6-180">Adress</span><span class="sxs-lookup"><span data-stu-id="1d3f6-180">Address</span></span>](utility-resources.md#address) | <span data-ttu-id="1d3f6-181">Den registrerade adressen för kundens företag/organisation.</span><span class="sxs-lookup"><span data-stu-id="1d3f6-181">The registered address of the customer's company/organization.</span></span> <span data-ttu-id="1d3f6-182">Se [adress](utility-resources.md#address) resursen för information om eventuella längd begränsningar.</span><span class="sxs-lookup"><span data-stu-id="1d3f6-182">See the [Address](utility-resources.md#address) resource for information on any length limitations.</span></span>                                             |

#### <a name="company-profile"></a><span data-ttu-id="1d3f6-183">Företags profil</span><span class="sxs-lookup"><span data-stu-id="1d3f6-183">Company profile</span></span>

<span data-ttu-id="1d3f6-184">I den här tabellen beskrivs minimi kraven för fält från [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) -resursen som behövs för att skapa en ny kund.</span><span class="sxs-lookup"><span data-stu-id="1d3f6-184">This table describes the minimum required fields from the [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="1d3f6-185">Namn</span><span class="sxs-lookup"><span data-stu-id="1d3f6-185">Name</span></span>   | <span data-ttu-id="1d3f6-186">Typ</span><span class="sxs-lookup"><span data-stu-id="1d3f6-186">Type</span></span>   | <span data-ttu-id="1d3f6-187">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="1d3f6-187">Description</span></span>                                                  |
|--------|--------|--------------------------------------------------------------|
| <span data-ttu-id="1d3f6-188">domän</span><span class="sxs-lookup"><span data-stu-id="1d3f6-188">domain</span></span> | <span data-ttu-id="1d3f6-189">sträng</span><span class="sxs-lookup"><span data-stu-id="1d3f6-189">string</span></span> | <span data-ttu-id="1d3f6-190">Kundens domän namn, till exempel contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="1d3f6-190">The customer's domain name, such as contoso.onmicrosoft.com.</span></span> |
|<span data-ttu-id="1d3f6-191">organizationRegistrationNumber</span><span class="sxs-lookup"><span data-stu-id="1d3f6-191">organizationRegistrationNumber</span></span>|<span data-ttu-id="1d3f6-192">Sträng</span><span class="sxs-lookup"><span data-stu-id="1d3f6-192">String</span></span>|<span data-ttu-id="1d3f6-193">Kundens organisations registrerings nummer (kallas även för INN-nummer i vissa länder).</span><span class="sxs-lookup"><span data-stu-id="1d3f6-193">The customer’s organization registration number (also referred to as INN number in certain countries).</span></span> <span data-ttu-id="1d3f6-194">Krävs endast för kundens företag/organisation i följande länder: Armenien (AM), Azerbajdzjan (AZ), Vitryssland (av), Ungern (HU), Kazakstan (KZ), Kirgizistan (KG), Moldavien (MD), Ryssland (RU), Tadzjikistan (TJ), Uzbekistan (UZ), Ukraina (UA), Brasilien (BR), Indien, Sydafrika, Polen, Förenade Arabemiraten, Saudiarabien, Turkiet, Thailand, Vietnam, Myanmar, Irak, Sydsudan och Venezuela.</span><span class="sxs-lookup"><span data-stu-id="1d3f6-194">Only required for customer’s company/organization located in the following countries: Armenia(AM), Azerbaijan(AZ), Belarus(BY), Hungary(HU), Kazakhstan(KZ), Kyrgyzstan(KG), Moldova(MD), Russia(RU), Tajikistan(TJ), Uzbekistan(UZ), Ukraine(UA), Brazil(BR), India, South Africa, Poland, United Arab Emirates, Saudi Arabia, Turkey, Thailand, Vietnam, Myanmar, Iraq, South Sudan and Venezuela.</span></span> <span data-ttu-id="1d3f6-195">För kundens företag/organisation i andra länder är detta ett valfritt fält.</span><span class="sxs-lookup"><span data-stu-id="1d3f6-195">For customer’s company/organization located in other countries this is an optional field.</span></span>|

### <a name="request-example"></a><span data-ttu-id="1d3f6-196">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="1d3f6-196">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="1d3f6-197">REST-svar</span><span class="sxs-lookup"><span data-stu-id="1d3f6-197">REST response</span></span>

<span data-ttu-id="1d3f6-198">Om detta lyckas returnerar detta API en [kund](customer-resources.md#customer) resurs för den nya kunden.</span><span class="sxs-lookup"><span data-stu-id="1d3f6-198">If successful, this API returns a [Customer](customer-resources.md#customer) resource for the new customer.</span></span> <span data-ttu-id="1d3f6-199">Spara kund-ID och Azure AD-information för framtida användning med partner Center SDK.</span><span class="sxs-lookup"><span data-stu-id="1d3f6-199">Save the customer ID and Azure AD details for future use with the Partner Center SDK.</span></span> <span data-ttu-id="1d3f6-200">Du behöver dem för att kunna använda med konto hantering, till exempel.</span><span class="sxs-lookup"><span data-stu-id="1d3f6-200">You will need them for use with account management, for example.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1d3f6-201">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="1d3f6-201">Response success and error codes</span></span>

<span data-ttu-id="1d3f6-202">Svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="1d3f6-202">Responses come with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1d3f6-203">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="1d3f6-203">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1d3f6-204">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="1d3f6-204">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1d3f6-205">Exempel på svar</span><span class="sxs-lookup"><span data-stu-id="1d3f6-205">Response example</span></span>

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
