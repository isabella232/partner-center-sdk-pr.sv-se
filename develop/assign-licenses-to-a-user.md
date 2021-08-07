---
title: Tilldela licenser till en användare
description: Lär dig hur du tilldelar licenser till en kundanvändare via Partner Center-API:er, till exempel användning av \# C- eller REST-API:er.
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8263f7f274e453603305324cc7ac6e8b25820561ade3136b873c65ffa21e94fc
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989074"
---
# <a name="assign-licenses-to-a-user-via-partner-center-apis"></a>Tilldela licenser till en användare via Partner Center-API:er

Så här tilldelar du licenser till en kundanvändare.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med app- och användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard) Välj **CSP** på Menyn i Partnercenter följt av **Kunder**. Välj kunden i kundlistan och välj sedan **Konto.** På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.** Microsoft-ID:t är samma som kund-ID :t ( `customer-tenant-id` ).

- En användaridentifierare för kunden. Det här ID:t identifierar den användare som licensen ska tilldelas till.

- En produkt-SKU-identifierare som identifierar produkten för licensen.

## <a name="assigning-licenses-through-code"></a>Tilldela licenser via kod

När du tilldelar licenser till en användare måste du välja från kundens samling med prenumerations-SKU:er. När du sedan har identifierat de produkter som du vill tilldela måste du hämta produktens SKU-ID för varje produkt för att kunna göra tilldelningarna. Varje [**SubscribedSku-instans**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku) innehåller en [**ProductSku-egenskap**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku.productsku) som du kan referera till [**ProductSku-objektet**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku) från och hämta [**ID:t .**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku.id)

En licenstilldelningsbegäran måste innehålla licenser från en enda licensgrupp. Du kan till exempel inte tilldela licenser [**från Group1**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid) **och Group2** i samma begäran. Ett försök att tilldela licenser från mer än en grupp i en enskild begäran misslyckas med ett lämpligt fel. Information om vilka licenser som är tillgängliga efter licensgrupp finns i [Hämta en lista över tillgängliga licenser efter licensgrupp.](get-a-list-of-available-licenses-by-license-group.md)

Här är stegen för att tilldela licenser via kod:

1. Instansiera [**ett LicenseAssignment-objekt.**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) Du använder det här objektet för att ange produkt-SKU och tjänstplaner som ska tilldelas.

    ``` csharp
    LicenseAssignment license = new LicenseAssignment();
    ```

2. Fyll i objektegenskaperna enligt nedan. Den här koden förutsätter att du redan har produktens SKU-ID och att alla tillgängliga tjänstplaner kommer att tilldelas (det vill säga att ingen kommer att undantas).

    ```csharp
    license.SkuId = selectedProductSkuId;
    license.ExcludedPlans = null;
    ```

3. Om du inte har produkt-SKU-ID:t måste du hämta samlingen med prenumerations-SKU:er och hämta produktens SKU-ID från en av dem. Här är ett exempel om du känner till produktens SKU-namn.

    ```csharp
    var customerSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get();
    var sku = customerSubscribedSkus.Items.Where(n => n.ProductSku.Name == "Office 365 Enterprise E3").First();
    license.SkuId = sku.ProductSku.Id;
    license.ExcludedPlans = null;
    ```

4. Skapa sedan en instans av en ny lista av [**typen LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment)och lägg till licensobjektet. Du kan tilldela fler än en licens genom att lägga till varje licens individuellt i listan. Licenserna som ingår i den här listan måste komma från samma licensgrupp.

    ```csharp
    List<LicenseAssignment> licenseList = new List<LicenseAssignment>();
    licenseList.Add(license);
    ```

5. Skapa en [**LicenseUpdate-instans**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) och tilldela listan över licenstilldelningar till egenskapen [**LicensesToAssign.**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign)

    ```csharp
    LicenseUpdate updateLicense = new LicenseUpdate();
    updateLicense.LicensesToAssign = licenseList;
    ```

6. Anropa metoden [**Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) eller [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) och skicka licensuppdateringsobjektet enligt nedan för att tilldela licenserna.

    ```csharp
    var assignLicense = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).LicenseUpdates.Create(updateLicense);
    ```

## <a name="c"></a>C\#

Om du vill tilldela en licens till en kundanvändare instansierar du först ett [**LicenseAssignment-objekt**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) och fyller i [**egenskaperna Skuid**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.skuid) [**och ExcludedPlans.**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.excludedplans) Du använder det här objektet för att ange vilken produkt-SKU som ska tilldelas och vilka tjänstplaner som ska undantas. Skapa sedan en instans av en ny lista av **typen LicenseAssignment** och lägg till licensobjektet i listan. Skapa sedan en [**LicenseUpdate-instans**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) och tilldela listan över licenstilldelningar till egenskapen [**LicensesToAssign.**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign)

Använd sedan metoden [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID:t för att identifiera kunden och [**metoden Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) med användar-ID:t för att identifiera användaren. Hämta sedan ett gränssnitt för uppdateringsåtgärder för kundanvändarlicens från egenskapen [**LicenseUpdates.**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenseupdates)

Anropa slutligen metoden [**Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) eller [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) och skicka licensuppdateringsobjektet för att tilldela licensen.

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

**Exempel:** [Konsoltestapp](console-test-app.md). **Project:** Partnercenter-SDK **Exempelklass:** CustomerUserAssignLicenses.cs

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Begärandesyntax

| Metod   | URI för förfrågan                                                                                                    |
|----------|----------------------------------------------------------------------------------------------------------------|
| **Inlägg** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenseupdates HTTP/1.1 |

#### <a name="uri-parameters"></a>URI-parametrar

Använd följande sökvägsparametrar för att identifiera kunden och användaren.

| Namn        | Typ   | Obligatorisk | Beskrivning                                       |
|-------------|--------|----------|---------------------------------------------------|
| kund-id | sträng | Yes      | Ett GUID-formaterat ID som identifierar kunden. |
| användar-id     | sträng | Yes      | Ett GUID-formaterat ID som identifierar användaren.     |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [Partner Center REST-huvuden.](headers.md)

### <a name="request-body"></a>Begärandetext

Inkludera en [LicenseUpdate-resurs](license-resources.md#licenseupdate) i begärandetexten som anger vilka licenser som ska tilldelas.

### <a name="request-example"></a>Exempel på begäran

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

## <a name="rest-response"></a>REST-svar

Om det lyckas returneras en HTTP-svarsstatuskod 201 och svarstexten innehåller en [LicenseUpdate-resurs](license-resources.md#licenseupdate) med licensinformationen.

### <a name="response-success-and-error-codes"></a>Lyckade svar och felkoder

Varje svar levereras med en HTTP-statuskod som anger lyckat eller misslyckat samt ytterligare felsökningsinformation. Använd ett nätverksspårningsverktyg för att läsa den här koden, feltypen och ytterligare parametrar. En fullständig lista finns i [Partner Center REST-felkoder.](error-codes.md)

### <a name="response-example-success"></a>Svarsexempel (lyckades)

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

### <a name="response-example-license-isnt-available"></a>Svarsexempel (licens är inte tillgänglig)

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
