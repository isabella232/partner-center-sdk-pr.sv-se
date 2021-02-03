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
# <a name="assign-licenses-to-a-user-via-partner-center-apis"></a>Tilldela licenser till en användare via API: er för partner Center

**Gäller för:**

- Partnercenter

Tilldela licenser till en kund användare.

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder endast autentisering med app + användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).

- Ett kund användar-ID. Detta ID identifierar användaren som licensen ska tilldelas till.

- En produkt-SKU-identifierare som identifierar produkten för licensen.

## <a name="assigning-licenses-through-code"></a>Tilldela licenser via kod

När du tilldelar licenser till en användare måste du välja bland kundens samling med prenumererade SKU: er. Sedan måste du hämta produkt-SKU-ID: t för varje produkt för att kunna utföra tilldelningarna med identifierade produkter som du vill tilldela. Varje [**SubscribedSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku) -instans innehåller en [**ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku.productsku) -egenskap som du kan använda för att referera till [**ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku) -objektet och hämta [**ID: t**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku.id).

En begäran om licens tilldelning måste innehålla licenser från en enda licens grupp. Du kan till exempel inte tilldela licenser från [**Grupp1**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid) och **group2** i samma begäran. Ett försök att tilldela licenser från mer än en grupp i en enskild begäran kommer att Miss lyckas med ett lämpligt fel. För att ta reda på vilka licenser som är tillgängliga av licens gruppen, se [Hämta en lista över tillgängliga licenser per licens grupp](get-a-list-of-available-licenses-by-license-group.md).

Här följer stegen för att tilldela licenser via kod:

1. Instansiera ett [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) -objekt. Du använder det här objektet för att ange den produkt-SKU och de tjänst planer som ska tilldelas.

    ``` csharp
    LicenseAssignment license = new LicenseAssignment();
    ```

2. Fyll i objekt egenskaperna enligt vad som visas nedan. Den här koden förutsätter att du redan har produkt-SKU-ID: t och att alla tillgängliga Service planer tilldelas (det vill säga ingen kommer att undantas).

    ```csharp
    license.SkuId = selectedProductSkuId;
    license.ExcludedPlans = null;
    ```

3. Om du inte har produkt-SKU-ID: t måste du hämta samlingen med de prenumererade SKU: erna och hämta produkt-SKU-ID: t från en av dem. Här är ett exempel om du känner till produktens SKU-namn.

    ```csharp
    var customerSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get();
    var sku = customerSubscribedSkus.Items.Where(n => n.ProductSku.Name == "Office 365 Enterprise E3").First();
    license.SkuId = sku.ProductSku.Id;
    license.ExcludedPlans = null;
    ```

4. Skapa sedan en ny lista med typen [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment)och Lägg till License-objektet. Du kan tilldela mer än en licens genom att lägga till var och en i listan. Licenserna som ingår i den här listan måste vara från samma licens grupp.

    ```csharp
    List<LicenseAssignment> licenseList = new List<LicenseAssignment>();
    licenseList.Add(license);
    ```

5. Skapa en [**LicenseUpdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) -instans och tilldela listan över licens tilldelningar till egenskapen [**LicensesToAssign**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) .

    ```csharp
    LicenseUpdate updateLicense = new LicenseUpdate();
    updateLicense.LicensesToAssign = licenseList;
    ```

6. Anropa metoden [**create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) eller [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) och skicka licens uppdaterings objektet så som visas nedan för att tilldela licenserna.

    ```csharp
    var assignLicense = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).LicenseUpdates.Create(updateLicense);
    ```

## <a name="c"></a>C\#

Om du vill tilldela en licens till en kund användare måste du först instansiera ett [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) -objekt och fylla i egenskaperna [**SkuID**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.skuid) och [**ExcludedPlans**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.excludedplans) . Du använder det här objektet för att ange den produkt-SKU som ska tilldelas och vilka Service planer som ska undantas. Skapa sedan en ny lista med typen **LicenseAssignment** och Lägg till licens objekt i listan. Skapa sedan en [**LicenseUpdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) -instans och tilldela listan över licens tilldelningar till egenskapen [**LicensesToAssign**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) .

Använd sedan metoden [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) med kund-ID för att identifiera kunden och metoden [**users. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) med användar-ID för att identifiera användaren. Hämta sedan ett gränssnitt till kund användar licens uppdaterings åtgärder från egenskapen [**LicenseUpdates**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenseupdates) .

Anropa slutligen metoden [**create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) eller [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) och skicka licens uppdaterings objektet för att tilldela licensen.

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

**Exempel**: [konsol test app](console-test-app.md). **Projekt**: Partner Center SDK-exempel **klass**: CustomerUserAssignLicenses.CS

## <a name="rest-request"></a>REST-begäran

### <a name="request-syntax"></a>Syntax för begäran

| Metod   | URI för förfrågan                                                                                                    |
|----------|----------------------------------------------------------------------------------------------------------------|
| **EFTER** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Users/{User-ID}/licenseupdates http/1.1 |

#### <a name="uri-parameters"></a>URI-parametrar

Använd följande Sök vägs parametrar för att identifiera kunden och användaren.

| Namn        | Typ   | Obligatorisk | Beskrivning                                       |
|-------------|--------|----------|---------------------------------------------------|
| kund-ID | sträng | Yes      | Ett GUID-formaterat ID som identifierar kunden. |
| användar-id     | sträng | Yes      | Ett GUID-formaterat ID som identifierar användaren.     |

### <a name="request-headers"></a>Begärandehuvuden

Mer information finns i [partner Center rest-rubriker](headers.md).

### <a name="request-body"></a>Begärandetext

Inkludera en [LicenseUpdate](license-resources.md#licenseupdate) -resurs i begär ande texten som anger de licenser som ska tilldelas.

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

Om det lyckas returneras en status kod 201 för HTTP-svar och svars texten innehåller en [LicenseUpdate](license-resources.md#licenseupdate) -resurs med licens informationen.

### <a name="response-success-and-error-codes"></a>Slutförda svar och felkoder

Varje svar levereras med en HTTP-statuskod som indikerar lyckad eller misslyckad och ytterligare felsöknings information. Använd ett verktyg för nätverks spårning för att läsa den här koden, fel typen och ytterligare parametrar. En fullständig lista finns i [partner Center rest-felkoder](error-codes.md).

### <a name="response-example-success"></a>Svars exempel (lyckades)

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

### <a name="response-example-license-isnt-available"></a>Svars exempel (licensen är inte tillgänglig)

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
