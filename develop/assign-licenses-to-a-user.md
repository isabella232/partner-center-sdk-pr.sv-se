---
title: Tilldela licenser till en användare
description: 'Lär dig hur du tilldelar licenser till en kund användare via API: er för partner Center, till exempel användning av C- \# eller REST-API: er.'
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6eb0b953b9157e48074415bb3207e2946cfb2ab4
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/13/2020
ms.locfileid: "97770008"
---
# <a name="assign-licenses-to-a-user-via-partner-center-apis"></a><span data-ttu-id="db8bc-103">Tilldela licenser till en användare via API: er för partner Center</span><span class="sxs-lookup"><span data-stu-id="db8bc-103">Assign licenses to a user via Partner Center APIs</span></span>

<span data-ttu-id="db8bc-104">**Gäller för:**</span><span class="sxs-lookup"><span data-stu-id="db8bc-104">**Applies to:**</span></span>

- <span data-ttu-id="db8bc-105">Partnercenter</span><span class="sxs-lookup"><span data-stu-id="db8bc-105">Partner Center</span></span>

<span data-ttu-id="db8bc-106">Tilldela licenser till en kund användare.</span><span class="sxs-lookup"><span data-stu-id="db8bc-106">How to assign licenses to a customer user.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="db8bc-107">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="db8bc-107">Prerequisites</span></span>

- <span data-ttu-id="db8bc-108">Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="db8bc-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="db8bc-109">Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="db8bc-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="db8bc-110">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="db8bc-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="db8bc-111">Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center.</span><span class="sxs-lookup"><span data-stu-id="db8bc-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="db8bc-112">Välj **CSP** på menyn Partner Center, följt av **kunder**.</span><span class="sxs-lookup"><span data-stu-id="db8bc-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="db8bc-113">Välj kunden från listan kund och välj sedan **konto**.</span><span class="sxs-lookup"><span data-stu-id="db8bc-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="db8bc-114">På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** .</span><span class="sxs-lookup"><span data-stu-id="db8bc-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="db8bc-115">Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="db8bc-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="db8bc-116">Ett kund användar-ID.</span><span class="sxs-lookup"><span data-stu-id="db8bc-116">A customer user identifier.</span></span> <span data-ttu-id="db8bc-117">Detta ID identifierar användaren som licensen ska tilldelas till.</span><span class="sxs-lookup"><span data-stu-id="db8bc-117">This ID identifies the user to whom to assign the license.</span></span>

- <span data-ttu-id="db8bc-118">En produkt-SKU-identifierare som identifierar produkten för licensen.</span><span class="sxs-lookup"><span data-stu-id="db8bc-118">A product SKU identifier that identifies the product for the license.</span></span>

## <a name="assigning-licenses-through-code"></a><span data-ttu-id="db8bc-119">Tilldela licenser via kod</span><span class="sxs-lookup"><span data-stu-id="db8bc-119">Assigning licenses through code</span></span>

<span data-ttu-id="db8bc-120">När du tilldelar licenser till en användare måste du välja bland kundens samling med prenumererade SKU: er.</span><span class="sxs-lookup"><span data-stu-id="db8bc-120">When you assign licenses to a user, you must choose from the customer's collection of subscribed SKUs.</span></span> <span data-ttu-id="db8bc-121">Sedan måste du hämta produkt-SKU-ID: t för varje produkt för att kunna utföra tilldelningarna med identifierade produkter som du vill tilldela.</span><span class="sxs-lookup"><span data-stu-id="db8bc-121">Then, having identified the products that you want to assign, you must obtain the product SKU ID for each product in order to make the assignments.</span></span> <span data-ttu-id="db8bc-122">Varje [**SubscribedSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku) -instans innehåller en [**ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku.productsku) -egenskap som du kan använda för att referera till [**ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku) -objektet och hämta [**ID: t**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku.id).</span><span class="sxs-lookup"><span data-stu-id="db8bc-122">Each [**SubscribedSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku) instance contains a [**ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku.productsku) property from which you can reference the [**ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku) object and get the [**ID**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku.id).</span></span>

<span data-ttu-id="db8bc-123">En begäran om licens tilldelning måste innehålla licenser från en enda licens grupp.</span><span class="sxs-lookup"><span data-stu-id="db8bc-123">A license assignment request must contain licenses from a single license group.</span></span> <span data-ttu-id="db8bc-124">Du kan till exempel inte tilldela licenser från [**Grupp1**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid) och **group2** i samma begäran.</span><span class="sxs-lookup"><span data-stu-id="db8bc-124">For example, you cannot assign licenses from [**Group1**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid) and **Group2** in the same request.</span></span> <span data-ttu-id="db8bc-125">Ett försök att tilldela licenser från mer än en grupp i en enskild begäran kommer att Miss lyckas med ett lämpligt fel.</span><span class="sxs-lookup"><span data-stu-id="db8bc-125">An attempt to assign licenses from more than one group in a single request will fail with an appropriate error.</span></span> <span data-ttu-id="db8bc-126">För att ta reda på vilka licenser som är tillgängliga av licens gruppen, se [Hämta en lista över tillgängliga licenser per licens grupp](get-a-list-of-available-licenses-by-license-group.md).</span><span class="sxs-lookup"><span data-stu-id="db8bc-126">To find out what licenses are available by license group, see [Get a list of available licenses by license group](get-a-list-of-available-licenses-by-license-group.md).</span></span>

<span data-ttu-id="db8bc-127">Här följer stegen för att tilldela licenser via kod:</span><span class="sxs-lookup"><span data-stu-id="db8bc-127">Here are the steps to assign licenses through code:</span></span>

1. <span data-ttu-id="db8bc-128">Instansiera ett [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) -objekt.</span><span class="sxs-lookup"><span data-stu-id="db8bc-128">Instantiate a [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) object.</span></span> <span data-ttu-id="db8bc-129">Du använder det här objektet för att ange den produkt-SKU och de tjänst planer som ska tilldelas.</span><span class="sxs-lookup"><span data-stu-id="db8bc-129">You use this object to specify the product SKU and service plans to assign.</span></span>

    ``` csharp
    LicenseAssignment license = new LicenseAssignment();
    ```

2. <span data-ttu-id="db8bc-130">Fyll i objekt egenskaperna enligt vad som visas nedan.</span><span class="sxs-lookup"><span data-stu-id="db8bc-130">Populate the object properties as shown below.</span></span> <span data-ttu-id="db8bc-131">Den här koden förutsätter att du redan har produkt-SKU-ID: t och att alla tillgängliga Service planer tilldelas (det vill säga ingen kommer att undantas).</span><span class="sxs-lookup"><span data-stu-id="db8bc-131">This code assumes that you already have the product SKU ID, and that all of the available service plans will be assigned (that is, none will be excluded).</span></span>

    ```csharp
    license.SkuId = selectedProductSkuId;
    license.ExcludedPlans = null;
    ```

3. <span data-ttu-id="db8bc-132">Om du inte har produkt-SKU-ID: t måste du hämta samlingen med de prenumererade SKU: erna och hämta produkt-SKU-ID: t från en av dem.</span><span class="sxs-lookup"><span data-stu-id="db8bc-132">If you don't have the product SKU ID, you need to retrieve the collection of subscribed SKUs and get the product SKU ID from one of them.</span></span> <span data-ttu-id="db8bc-133">Här är ett exempel om du känner till produktens SKU-namn.</span><span class="sxs-lookup"><span data-stu-id="db8bc-133">Here is an example if you know the product SKU name.</span></span>

    ```csharp
    var customerSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get();
    var sku = customerSubscribedSkus.Items.Where(n => n.ProductSku.Name == "Office 365 Enterprise E3").First();
    license.SkuId = sku.ProductSku.Id;
    license.ExcludedPlans = null;
    ```

4. <span data-ttu-id="db8bc-134">Skapa sedan en ny lista med typen [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment)och Lägg till License-objektet.</span><span class="sxs-lookup"><span data-stu-id="db8bc-134">Next, instantiate a new list of type [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment), and add the license object.</span></span> <span data-ttu-id="db8bc-135">Du kan tilldela mer än en licens genom att lägga till var och en i listan.</span><span class="sxs-lookup"><span data-stu-id="db8bc-135">You can assign more than one license by adding each individually to the list.</span></span> <span data-ttu-id="db8bc-136">Licenserna som ingår i den här listan måste vara från samma licens grupp.</span><span class="sxs-lookup"><span data-stu-id="db8bc-136">The licenses included in this list must be from the same license group.</span></span>

    ```csharp
    List<LicenseAssignment> licenseList = new List<LicenseAssignment>();
    licenseList.Add(license);
    ```

5. <span data-ttu-id="db8bc-137">Skapa en [**LicenseUpdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) -instans och tilldela listan över licens tilldelningar till egenskapen [**LicensesToAssign**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) .</span><span class="sxs-lookup"><span data-stu-id="db8bc-137">Create a [**LicenseUpdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) instance and assign the list of license assignments to the [**LicensesToAssign**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) property.</span></span>

    ```csharp
    LicenseUpdate updateLicense = new LicenseUpdate();
    updateLicense.LicensesToAssign = licenseList;
    ```

6. <span data-ttu-id="db8bc-138">Anropa metoden [**create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) eller [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) och skicka licens uppdaterings objektet så som visas nedan för att tilldela licenserna.</span><span class="sxs-lookup"><span data-stu-id="db8bc-138">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) method and pass the license update object as shown below to assign the licenses.</span></span>

    ```csharp
    var assignLicense = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).LicenseUpdates.Create(updateLicense);
    ```

## <a name="c"></a><span data-ttu-id="db8bc-139">C\#</span><span class="sxs-lookup"><span data-stu-id="db8bc-139">C\#</span></span>

<span data-ttu-id="db8bc-140">Om du vill tilldela en licens till en kund användare måste du först instansiera ett [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) -objekt och fylla i egenskaperna [**SkuID**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.skuid) och [**ExcludedPlans**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.excludedplans) .</span><span class="sxs-lookup"><span data-stu-id="db8bc-140">To assign a license to a customer user, first instantiate a [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) object, and populate the [**Skuid**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.skuid) and [**ExcludedPlans**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.excludedplans) properties.</span></span> <span data-ttu-id="db8bc-141">Du använder det här objektet för att ange den produkt-SKU som ska tilldelas och vilka Service planer som ska undantas.</span><span class="sxs-lookup"><span data-stu-id="db8bc-141">You use this object to specify the product SKU to assign and service plans to exclude.</span></span> <span data-ttu-id="db8bc-142">Skapa sedan en ny lista med typen **LicenseAssignment** och Lägg till licens objekt i listan.</span><span class="sxs-lookup"><span data-stu-id="db8bc-142">Next, instantiate a new list of type **LicenseAssignment**, and add the license object to the list.</span></span> <span data-ttu-id="db8bc-143">Skapa sedan en [**LicenseUpdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) -instans och tilldela listan över licens tilldelningar till egenskapen [**LicensesToAssign**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) .</span><span class="sxs-lookup"><span data-stu-id="db8bc-143">Then create a [**LicenseUpdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) instance and assign the list of license assignments to the [**LicensesToAssign**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) property.</span></span>

<span data-ttu-id="db8bc-144">Använd sedan metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID för att identifiera kunden och metoden [**users. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) med användar-ID för att identifiera användaren.</span><span class="sxs-lookup"><span data-stu-id="db8bc-144">Next, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the user ID to identify the user.</span></span> <span data-ttu-id="db8bc-145">Hämta sedan ett gränssnitt till kund användar licens uppdaterings åtgärder från egenskapen [**LicenseUpdates**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenseupdates) .</span><span class="sxs-lookup"><span data-stu-id="db8bc-145">Then get an interface to customer user license update operations from the [**LicenseUpdates**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenseupdates) property.</span></span>

<span data-ttu-id="db8bc-146">Anropa slutligen metoden [**create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) eller [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) och skicka licens uppdaterings objektet för att tilldela licensen.</span><span class="sxs-lookup"><span data-stu-id="db8bc-146">Finally, call the [**Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) method and pass the license update object to assign the license.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerUserId;
// string selectedCustomerId;
// string selectedProductSkuId;

// Instantiate and populate a LicenseAssignment object.
LicenseAssignment license = new LicenseAssignment();
license.SkuId = selectedProductSkuId;
license.ExcludedPlans = null;

// Instantiate a list of licenses to assign and add the license to it.
List<LicenseAssignment> licenseList = new List<LicenseAssignment>();
licenseList.Add(license);

// Instantiate a LicenseUpdate object and add the list of licenses to assign.
LicenseUpdate updateLicense = new LicenseUpdate();
updateLicense.LicensesToAssign = licenseList;

// Update the user licenses.
var assignLicense = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).LicenseUpdates.Create(updateLicense);
```

<span data-ttu-id="db8bc-147">**Exempel**: [konsol test app](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="db8bc-147">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="db8bc-148">**Projekt**: Partner Center SDK-exempel **klass**: CustomerUserAssignLicenses.CS</span><span class="sxs-lookup"><span data-stu-id="db8bc-148">**Project**: Partner Center SDK Samples **Class**: CustomerUserAssignLicenses.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="db8bc-149">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="db8bc-149">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="db8bc-150">Syntax för begäran</span><span class="sxs-lookup"><span data-stu-id="db8bc-150">Request syntax</span></span>

| <span data-ttu-id="db8bc-151">Metod</span><span class="sxs-lookup"><span data-stu-id="db8bc-151">Method</span></span>   | <span data-ttu-id="db8bc-152">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="db8bc-152">Request URI</span></span>                                                                                                    |
|----------|----------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="db8bc-153">**EFTER**</span><span class="sxs-lookup"><span data-stu-id="db8bc-153">**POST**</span></span> | <span data-ttu-id="db8bc-154">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Users/{User-ID}/licenseupdates http/1.1</span><span class="sxs-lookup"><span data-stu-id="db8bc-154">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenseupdates HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="db8bc-155">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="db8bc-155">URI parameters</span></span>

<span data-ttu-id="db8bc-156">Använd följande Sök vägs parametrar för att identifiera kunden och användaren.</span><span class="sxs-lookup"><span data-stu-id="db8bc-156">Use the following path parameters to identify the customer and user.</span></span>

| <span data-ttu-id="db8bc-157">Namn</span><span class="sxs-lookup"><span data-stu-id="db8bc-157">Name</span></span>        | <span data-ttu-id="db8bc-158">Typ</span><span class="sxs-lookup"><span data-stu-id="db8bc-158">Type</span></span>   | <span data-ttu-id="db8bc-159">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="db8bc-159">Required</span></span> | <span data-ttu-id="db8bc-160">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="db8bc-160">Description</span></span>                                       |
|-------------|--------|----------|---------------------------------------------------|
| <span data-ttu-id="db8bc-161">kund-ID</span><span class="sxs-lookup"><span data-stu-id="db8bc-161">customer-id</span></span> | <span data-ttu-id="db8bc-162">sträng</span><span class="sxs-lookup"><span data-stu-id="db8bc-162">string</span></span> | <span data-ttu-id="db8bc-163">Yes</span><span class="sxs-lookup"><span data-stu-id="db8bc-163">Yes</span></span>      | <span data-ttu-id="db8bc-164">Ett GUID-formaterat ID som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="db8bc-164">A GUID formatted ID that identifies the customer.</span></span> |
| <span data-ttu-id="db8bc-165">användar-id</span><span class="sxs-lookup"><span data-stu-id="db8bc-165">user-id</span></span>     | <span data-ttu-id="db8bc-166">sträng</span><span class="sxs-lookup"><span data-stu-id="db8bc-166">string</span></span> | <span data-ttu-id="db8bc-167">Yes</span><span class="sxs-lookup"><span data-stu-id="db8bc-167">Yes</span></span>      | <span data-ttu-id="db8bc-168">Ett GUID-formaterat ID som identifierar användaren.</span><span class="sxs-lookup"><span data-stu-id="db8bc-168">A GUID formatted ID that identifies the user.</span></span>     |

### <a name="request-headers"></a><span data-ttu-id="db8bc-169">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="db8bc-169">Request headers</span></span>

<span data-ttu-id="db8bc-170">Mer information finns i [partner Center rest-rubriker](headers.md).</span><span class="sxs-lookup"><span data-stu-id="db8bc-170">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="db8bc-171">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="db8bc-171">Request body</span></span>

<span data-ttu-id="db8bc-172">Inkludera en [LicenseUpdate](license-resources.md#licenseupdate) -resurs i begär ande texten som anger de licenser som ska tilldelas.</span><span class="sxs-lookup"><span data-stu-id="db8bc-172">Include a [LicenseUpdate](license-resources.md#licenseupdate) resource in the request body that specifies the licenses to assign.</span></span>

### <a name="request-example"></a><span data-ttu-id="db8bc-173">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="db8bc-173">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/users/554526aa-cf5e-46fa-95df-98dbc55d8a1e/licenseupdates HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a37d3009-665d-4e12-b76e-1aa10cf80140
MS-CorrelationId: c73c9570-c352-459e-98a3-dafe4bd8c821
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 183
Expect: 100-continue

{
    "LicensesToAssign": [{
            "ExcludedPlans": null,
            "SkuId": "f8a1db68-be16-40ed-86d5-cb42ce701560"
        }
    ],
    "LicensesToRemove": null,
    "LicenseWarnings": null,
    "Attributes": {
        "ObjectType": "LicenseUpdate"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="db8bc-174">REST-svar</span><span class="sxs-lookup"><span data-stu-id="db8bc-174">REST response</span></span>

<span data-ttu-id="db8bc-175">Om det lyckas returneras en status kod 201 för HTTP-svar och svars texten innehåller en [LicenseUpdate](license-resources.md#licenseupdate) -resurs med licens informationen.</span><span class="sxs-lookup"><span data-stu-id="db8bc-175">If successful, an HTTP response status code 201 is returned and the response body contains a [LicenseUpdate](license-resources.md#licenseupdate) resource with the license information.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="db8bc-176">Slutförda svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="db8bc-176">Response success and error codes</span></span>

<span data-ttu-id="db8bc-177">Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information.</span><span class="sxs-lookup"><span data-stu-id="db8bc-177">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="db8bc-178">Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="db8bc-178">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="db8bc-179">En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="db8bc-179">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example-success"></a><span data-ttu-id="db8bc-180">Svars exempel (lyckades)</span><span class="sxs-lookup"><span data-stu-id="db8bc-180">Response example (success)</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 139
Content-Type: application/json; charset=utf-8
MS-CorrelationId: c73c9570-c352-459e-98a3-dafe4bd8c821
MS-RequestId: a37d3009-665d-4e12-b76e-1aa10cf80140
MS-CV: 5AnzcZQrvUqCq3kd.0
MS-ServerId: 030020525
Date: Thu, 20 Apr 2017 21:50:39 GMT

{
    "licensesToAssign": [{
            "skuId": "f8a1db68-be16-40ed-86d5-cb42ce701560"
        }
    ],
    "licenseWarnings": [],
    "attributes": {
        "objectType": "LicenseUpdate"
    }
}
```

### <a name="response-example-license-isnt-available"></a><span data-ttu-id="db8bc-181">Svars exempel (licensen är inte tillgänglig)</span><span class="sxs-lookup"><span data-stu-id="db8bc-181">Response example (license isn't available)</span></span>

```http
HTTP/1.1 400 Bad Request
Content-Length: 341
Content-Type: application/json; charset=utf-8
MS-CorrelationId: c73c9570-c352-459e-98a3-dafe4bd8c821
MS-RequestId: f4f3b748-8b22-4d07-a5a1-dceb32824192
MS-CV: 5npA0K22CUmWPOzB.0
MS-ServerId: 102030524
Date: Thu, 20 Apr 2017 22:12:36 GMT

{
    "code": 60012,
    "description": "We&#39;re sorry, it looks like you've run out of licenses. Buy more licenses, and then try again.",
    "data": ["LicenseQuotaExceededException : Subscription with Account 0c39d6d5-c70d-4c55-bc02-f620844f3fd1 and SKU f8a1db68-be16-40ed-86d5-cb42ce701560 does not have any available licenses left."],
    "source": "PartnerFD"
}
```
