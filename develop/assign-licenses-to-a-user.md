---
title: Tilldela licenser till en användare
description: Lär dig hur du tilldelar licenser till en kundanvändare via Partner Center-API:er, till exempel användning av C \# eller REST API:er.
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 88ce0f185b0b043c4a7862b7f9808fb8805d40b9
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974377"
---
# <a name="assign-licenses-to-a-user-via-partner-center-apis"></a><span data-ttu-id="98e69-103">Tilldela licenser till en användare via Partner Center-API:er</span><span class="sxs-lookup"><span data-stu-id="98e69-103">Assign licenses to a user via Partner Center APIs</span></span>

<span data-ttu-id="98e69-104">Så här tilldelar du licenser till en kundanvändare.</span><span class="sxs-lookup"><span data-stu-id="98e69-104">How to assign licenses to a customer user.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="98e69-105">Förutsättningar</span><span class="sxs-lookup"><span data-stu-id="98e69-105">Prerequisites</span></span>

- <span data-ttu-id="98e69-106">Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="98e69-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="98e69-107">Det här scenariot har endast stöd för autentisering med app- och användarautentiseringsuppgifter.</span><span class="sxs-lookup"><span data-stu-id="98e69-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="98e69-108">Ett kund-ID ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="98e69-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="98e69-109">Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="98e69-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="98e69-110">Välj **CSP** på Menyn i Partnercenter följt av **Kunder.**</span><span class="sxs-lookup"><span data-stu-id="98e69-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="98e69-111">Välj kunden i kundlistan och välj sedan **Konto.**</span><span class="sxs-lookup"><span data-stu-id="98e69-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="98e69-112">På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.**</span><span class="sxs-lookup"><span data-stu-id="98e69-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="98e69-113">Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="98e69-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="98e69-114">En kundanvändares identifierare.</span><span class="sxs-lookup"><span data-stu-id="98e69-114">A customer user identifier.</span></span> <span data-ttu-id="98e69-115">Det här ID:t identifierar den användare som licensen ska tilldelas till.</span><span class="sxs-lookup"><span data-stu-id="98e69-115">This ID identifies the user to whom to assign the license.</span></span>

- <span data-ttu-id="98e69-116">En produkt-SKU-identifierare som identifierar produkten för licensen.</span><span class="sxs-lookup"><span data-stu-id="98e69-116">A product SKU identifier that identifies the product for the license.</span></span>

## <a name="assigning-licenses-through-code"></a><span data-ttu-id="98e69-117">Tilldela licenser via kod</span><span class="sxs-lookup"><span data-stu-id="98e69-117">Assigning licenses through code</span></span>

<span data-ttu-id="98e69-118">När du tilldelar licenser till en användare måste du välja från kundens samling med prenumerations-SKU:er.</span><span class="sxs-lookup"><span data-stu-id="98e69-118">When you assign licenses to a user, you must choose from the customer's collection of subscribed SKUs.</span></span> <span data-ttu-id="98e69-119">När du sedan har identifierat de produkter som du vill tilldela måste du hämta produktens SKU-ID för varje produkt för att kunna göra tilldelningarna.</span><span class="sxs-lookup"><span data-stu-id="98e69-119">Then, having identified the products that you want to assign, you must obtain the product SKU ID for each product in order to make the assignments.</span></span> <span data-ttu-id="98e69-120">Varje [**SubscribedSku-instans**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku) innehåller en [**ProductSku-egenskap**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku.productsku) som du kan referera till [**ProductSku-objektet**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku) från och hämta [**ID:t .**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku.id)</span><span class="sxs-lookup"><span data-stu-id="98e69-120">Each [**SubscribedSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku) instance contains a [**ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku.productsku) property from which you can reference the [**ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku) object and get the [**ID**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku.id).</span></span>

<span data-ttu-id="98e69-121">En licenstilldelningsbegäran måste innehålla licenser från en enda licensgrupp.</span><span class="sxs-lookup"><span data-stu-id="98e69-121">A license assignment request must contain licenses from a single license group.</span></span> <span data-ttu-id="98e69-122">Du kan till exempel inte tilldela licenser från [**Group1**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid) **och Group2** i samma begäran.</span><span class="sxs-lookup"><span data-stu-id="98e69-122">For example, you cannot assign licenses from [**Group1**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid) and **Group2** in the same request.</span></span> <span data-ttu-id="98e69-123">Ett försök att tilldela licenser från mer än en grupp i en enskild begäran misslyckas med ett lämpligt fel.</span><span class="sxs-lookup"><span data-stu-id="98e69-123">An attempt to assign licenses from more than one group in a single request will fail with an appropriate error.</span></span> <span data-ttu-id="98e69-124">Information om vilka licenser som är tillgängliga efter licensgrupp finns i [Hämta en lista över tillgängliga licenser efter licensgrupp.](get-a-list-of-available-licenses-by-license-group.md)</span><span class="sxs-lookup"><span data-stu-id="98e69-124">To find out what licenses are available by license group, see [Get a list of available licenses by license group](get-a-list-of-available-licenses-by-license-group.md).</span></span>

<span data-ttu-id="98e69-125">Här är stegen för att tilldela licenser via kod:</span><span class="sxs-lookup"><span data-stu-id="98e69-125">Here are the steps to assign licenses through code:</span></span>

1. <span data-ttu-id="98e69-126">Instansiera [**ett LicenseAssignment-objekt.**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment)</span><span class="sxs-lookup"><span data-stu-id="98e69-126">Instantiate a [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) object.</span></span> <span data-ttu-id="98e69-127">Du använder det här objektet för att ange produkt-SKU och tjänstplaner som ska tilldelas.</span><span class="sxs-lookup"><span data-stu-id="98e69-127">You use this object to specify the product SKU and service plans to assign.</span></span>

    ``` csharp
    LicenseAssignment license = new LicenseAssignment();
    ```

2. <span data-ttu-id="98e69-128">Fyll i objektegenskaperna enligt nedan.</span><span class="sxs-lookup"><span data-stu-id="98e69-128">Populate the object properties as shown below.</span></span> <span data-ttu-id="98e69-129">Den här koden förutsätter att du redan har produktens SKU-ID och att alla tillgängliga tjänstplaner kommer att tilldelas (d.v.s. inga kommer att undantas).</span><span class="sxs-lookup"><span data-stu-id="98e69-129">This code assumes that you already have the product SKU ID, and that all of the available service plans will be assigned (that is, none will be excluded).</span></span>

    ```csharp
    license.SkuId = selectedProductSkuId;
    license.ExcludedPlans = null;
    ```

3. <span data-ttu-id="98e69-130">Om du inte har produktens SKU-ID måste du hämta samlingen med prenumerations-SKU:er och hämta produktens SKU-ID från en av dem.</span><span class="sxs-lookup"><span data-stu-id="98e69-130">If you don't have the product SKU ID, you need to retrieve the collection of subscribed SKUs and get the product SKU ID from one of them.</span></span> <span data-ttu-id="98e69-131">Här är ett exempel om du känner till produktens SKU-namn.</span><span class="sxs-lookup"><span data-stu-id="98e69-131">Here is an example if you know the product SKU name.</span></span>

    ```csharp
    var customerSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get();
    var sku = customerSubscribedSkus.Items.Where(n => n.ProductSku.Name == "Office 365 Enterprise E3").First();
    license.SkuId = sku.ProductSku.Id;
    license.ExcludedPlans = null;
    ```

4. <span data-ttu-id="98e69-132">Skapa sedan en instans av en ny lista av [**typen LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment)och lägg till licensobjektet.</span><span class="sxs-lookup"><span data-stu-id="98e69-132">Next, instantiate a new list of type [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment), and add the license object.</span></span> <span data-ttu-id="98e69-133">Du kan tilldela fler än en licens genom att lägga till varje licens individuellt i listan.</span><span class="sxs-lookup"><span data-stu-id="98e69-133">You can assign more than one license by adding each individually to the list.</span></span> <span data-ttu-id="98e69-134">Licenserna som ingår i den här listan måste komma från samma licensgrupp.</span><span class="sxs-lookup"><span data-stu-id="98e69-134">The licenses included in this list must be from the same license group.</span></span>

    ```csharp
    List<LicenseAssignment> licenseList = new List<LicenseAssignment>();
    licenseList.Add(license);
    ```

5. <span data-ttu-id="98e69-135">Skapa en [**LicenseUpdate-instans**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) och tilldela listan över licenstilldelningar till egenskapen [**LicensesToAssign.**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign)</span><span class="sxs-lookup"><span data-stu-id="98e69-135">Create a [**LicenseUpdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) instance and assign the list of license assignments to the [**LicensesToAssign**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) property.</span></span>

    ```csharp
    LicenseUpdate updateLicense = new LicenseUpdate();
    updateLicense.LicensesToAssign = licenseList;
    ```

6. <span data-ttu-id="98e69-136">Anropa metoden [**Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) eller [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) och skicka licensuppdateringsobjektet enligt nedan för att tilldela licenserna.</span><span class="sxs-lookup"><span data-stu-id="98e69-136">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) method and pass the license update object as shown below to assign the licenses.</span></span>

    ```csharp
    var assignLicense = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).LicenseUpdates.Create(updateLicense);
    ```

## <a name="c"></a><span data-ttu-id="98e69-137">C\#</span><span class="sxs-lookup"><span data-stu-id="98e69-137">C\#</span></span>

<span data-ttu-id="98e69-138">Om du vill tilldela en licens till en kundanvändare instansierar du först ett [**LicenseAssignment-objekt**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) och fyller i [**egenskaperna Skuid**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.skuid) [**och ExcludedPlans.**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.excludedplans)</span><span class="sxs-lookup"><span data-stu-id="98e69-138">To assign a license to a customer user, first instantiate a [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) object, and populate the [**Skuid**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.skuid) and [**ExcludedPlans**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.excludedplans) properties.</span></span> <span data-ttu-id="98e69-139">Du använder det här objektet för att ange vilken produkt-SKU som ska tilldelas och vilka tjänstplaner som ska undantas.</span><span class="sxs-lookup"><span data-stu-id="98e69-139">You use this object to specify the product SKU to assign and service plans to exclude.</span></span> <span data-ttu-id="98e69-140">Skapa sedan en instans av en ny lista av **typen LicenseAssignment** och lägg till licensobjektet i listan.</span><span class="sxs-lookup"><span data-stu-id="98e69-140">Next, instantiate a new list of type **LicenseAssignment**, and add the license object to the list.</span></span> <span data-ttu-id="98e69-141">Skapa sedan en [**LicenseUpdate-instans**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) och tilldela listan över licenstilldelningar till egenskapen [**LicensesToAssign.**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign)</span><span class="sxs-lookup"><span data-stu-id="98e69-141">Then create a [**LicenseUpdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) instance and assign the list of license assignments to the [**LicensesToAssign**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) property.</span></span>

<span data-ttu-id="98e69-142">Använd sedan metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att identifiera kunden och metoden [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) med användar-ID:t för att identifiera användaren.</span><span class="sxs-lookup"><span data-stu-id="98e69-142">Next, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the user ID to identify the user.</span></span> <span data-ttu-id="98e69-143">Hämta sedan ett gränssnitt för åtgärder för uppdatering av kundanvändarlicens från egenskapen [**LicenseUpdates.**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenseupdates)</span><span class="sxs-lookup"><span data-stu-id="98e69-143">Then get an interface to customer user license update operations from the [**LicenseUpdates**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenseupdates) property.</span></span>

<span data-ttu-id="98e69-144">Anropa slutligen metoden [**Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) eller [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) och skicka licensuppdateringsobjektet för att tilldela licensen.</span><span class="sxs-lookup"><span data-stu-id="98e69-144">Finally, call the [**Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) method and pass the license update object to assign the license.</span></span>

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

<span data-ttu-id="98e69-145">**Exempel:** [Konsoltestapp](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="98e69-145">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="98e69-146">**Project:** **Partnercenter-SDK-exempelklass:** CustomerUserAssignLicenses.cs</span><span class="sxs-lookup"><span data-stu-id="98e69-146">**Project**: Partner Center SDK Samples **Class**: CustomerUserAssignLicenses.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="98e69-147">REST-begäran</span><span class="sxs-lookup"><span data-stu-id="98e69-147">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="98e69-148">Begärandesyntax</span><span class="sxs-lookup"><span data-stu-id="98e69-148">Request syntax</span></span>

| <span data-ttu-id="98e69-149">Metod</span><span class="sxs-lookup"><span data-stu-id="98e69-149">Method</span></span>   | <span data-ttu-id="98e69-150">URI för förfrågan</span><span class="sxs-lookup"><span data-stu-id="98e69-150">Request URI</span></span>                                                                                                    |
|----------|----------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="98e69-151">**Inlägg**</span><span class="sxs-lookup"><span data-stu-id="98e69-151">**POST**</span></span> | <span data-ttu-id="98e69-152">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenseupdates HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="98e69-152">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenseupdates HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="98e69-153">URI-parametrar</span><span class="sxs-lookup"><span data-stu-id="98e69-153">URI parameters</span></span>

<span data-ttu-id="98e69-154">Använd följande sökvägsparametrar för att identifiera kunden och användaren.</span><span class="sxs-lookup"><span data-stu-id="98e69-154">Use the following path parameters to identify the customer and user.</span></span>

| <span data-ttu-id="98e69-155">Namn</span><span class="sxs-lookup"><span data-stu-id="98e69-155">Name</span></span>        | <span data-ttu-id="98e69-156">Typ</span><span class="sxs-lookup"><span data-stu-id="98e69-156">Type</span></span>   | <span data-ttu-id="98e69-157">Obligatorisk</span><span class="sxs-lookup"><span data-stu-id="98e69-157">Required</span></span> | <span data-ttu-id="98e69-158">Beskrivning</span><span class="sxs-lookup"><span data-stu-id="98e69-158">Description</span></span>                                       |
|-------------|--------|----------|---------------------------------------------------|
| <span data-ttu-id="98e69-159">kund-ID</span><span class="sxs-lookup"><span data-stu-id="98e69-159">customer-id</span></span> | <span data-ttu-id="98e69-160">sträng</span><span class="sxs-lookup"><span data-stu-id="98e69-160">string</span></span> | <span data-ttu-id="98e69-161">Ja</span><span class="sxs-lookup"><span data-stu-id="98e69-161">Yes</span></span>      | <span data-ttu-id="98e69-162">Ett GUID-formaterat ID som identifierar kunden.</span><span class="sxs-lookup"><span data-stu-id="98e69-162">A GUID formatted ID that identifies the customer.</span></span> |
| <span data-ttu-id="98e69-163">användar-id</span><span class="sxs-lookup"><span data-stu-id="98e69-163">user-id</span></span>     | <span data-ttu-id="98e69-164">sträng</span><span class="sxs-lookup"><span data-stu-id="98e69-164">string</span></span> | <span data-ttu-id="98e69-165">Ja</span><span class="sxs-lookup"><span data-stu-id="98e69-165">Yes</span></span>      | <span data-ttu-id="98e69-166">Ett GUID-formaterat ID som identifierar användaren.</span><span class="sxs-lookup"><span data-stu-id="98e69-166">A GUID formatted ID that identifies the user.</span></span>     |

### <a name="request-headers"></a><span data-ttu-id="98e69-167">Begärandehuvuden</span><span class="sxs-lookup"><span data-stu-id="98e69-167">Request headers</span></span>

<span data-ttu-id="98e69-168">Mer information finns i [Partner Center REST-huvuden.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="98e69-168">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="98e69-169">Begärandetext</span><span class="sxs-lookup"><span data-stu-id="98e69-169">Request body</span></span>

<span data-ttu-id="98e69-170">Inkludera en [LicenseUpdate-resurs](license-resources.md#licenseupdate) i begärandetexten som anger vilka licenser som ska tilldelas.</span><span class="sxs-lookup"><span data-stu-id="98e69-170">Include a [LicenseUpdate](license-resources.md#licenseupdate) resource in the request body that specifies the licenses to assign.</span></span>

### <a name="request-example"></a><span data-ttu-id="98e69-171">Exempel på begäran</span><span class="sxs-lookup"><span data-stu-id="98e69-171">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="98e69-172">REST-svar</span><span class="sxs-lookup"><span data-stu-id="98e69-172">REST response</span></span>

<span data-ttu-id="98e69-173">Om det lyckas returneras en HTTP-svarsstatuskod 201 och svarstexten innehåller en [LicenseUpdate-resurs](license-resources.md#licenseupdate) med licensinformationen.</span><span class="sxs-lookup"><span data-stu-id="98e69-173">If successful, an HTTP response status code 201 is returned and the response body contains a [LicenseUpdate](license-resources.md#licenseupdate) resource with the license information.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="98e69-174">Lyckade svar och felkoder</span><span class="sxs-lookup"><span data-stu-id="98e69-174">Response success and error codes</span></span>

<span data-ttu-id="98e69-175">Varje svar levereras med en HTTP-statuskod som anger lyckad eller misslyckad samt ytterligare felsökningsinformation.</span><span class="sxs-lookup"><span data-stu-id="98e69-175">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="98e69-176">Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar.</span><span class="sxs-lookup"><span data-stu-id="98e69-176">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="98e69-177">En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="98e69-177">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example-success"></a><span data-ttu-id="98e69-178">Svarsexempel (lyckades)</span><span class="sxs-lookup"><span data-stu-id="98e69-178">Response example (success)</span></span>

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

### <a name="response-example-license-isnt-available"></a><span data-ttu-id="98e69-179">Svarsexempel (licens är inte tillgänglig)</span><span class="sxs-lookup"><span data-stu-id="98e69-179">Response example (license isn't available)</span></span>

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
