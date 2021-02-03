---
title: Profil resurser
description: Beskriver beteendet för en moln lösnings leverantörs profiler.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e0561278995f4f9747320866b51de57efea8f712
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769663"
---
# <a name="profile-resources"></a>Profil resurser

**Gäller för**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Beskriver beteendet för en moln lösnings leverantörs profiler.

## <a name="billingprofile"></a>BillingProfile

Beskriver en partners fakturerings profil.

| Egenskap            | Typ                                                           | Description                                                 |
|---------------------|----------------------------------------------------------------|-------------------------------------------------------------|
| companyName         | sträng                                                         | Fakturerings företagets namn.                                   |
| adress             | [Adress](utility-resources.md#address)                       | Företagets eller organisationens fakturerings adress. |
| primaryContact      | [Kontakt](utility-resources.md#contact)                       | Den primära kontakten för företaget eller organisationen.        |
| purchaseOrderNumber | sträng                                                         | Företagets eller organisationens inköps order nummer.        |
| taxI               | sträng                                                         | Företaget eller organisationens skatte-ID.                       |
| billingCurrency     | sträng                                                         | Valutan som används av företaget eller organisationen.           |
| Profiltyp         | sträng                                                         | Partnerns profil typ.                                   |
| Länkar               | [ResourceLinks](utility-resources.md#resourcelinks)           | Resurs länkarna som motsvarar profilen.            |
| dokumentattribut          | [ResourceAttributes](utility-resources.md#resourceattributes) | De metadata-attribut som motsvarar profilen.       |

## <a name="legalbusinessprofile"></a>LegalBusinessProfile

Beskriver en partners juridiska företags profil.

| Egenskap               | Typ                                                           | Description                                                                                                                                                          |
|------------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| companyName            | sträng                                                         | Det juridiska företags namnet.                                                                                                                                              |
| adress                | [Adress](utility-resources.md#address)                       | Företagets eller organisationens adress.                                                                                                                          |
| primaryContact         | [Kontakt](utility-resources.md#contact)                       | Den primära kontakten för företaget eller organisationen.                                                                                                                 |
| companyApproverAddress | [Adress](utility-resources.md#address)                       | Företagets godkännande adress.                                                                                                                                        |
| companyApproverEmail   | sträng                                                         | Företagets e-postadress för god kännare.                                                                                                                                          |
| vettingStatus          | sträng                                                         | Status för först konsumentsajter. Det här värdet är sträng representationen av ett av de medlems namn som finns i [**VettingStatus**](/dotnet/api/microsoft.store.partnercenter.models.partners.vettingstatus).           |
| vettingSubStatus       | sträng                                                         | Först konsumentsajter under status. Det här värdet är sträng representationen av ett av de medlems namn som finns i [**VettingSubStatus**](/dotnet/api/microsoft.store.partnercenter.models.partners.vettingsubstatus). |
| Profiltyp            | sträng                                                         | Partnerns profil typ.                                                                                                                                            |
| Länkar                  | [ResourceLinks](utility-resources.md#resourcelinks)           | Resurs länkarna som motsvarar profilen.                                                                                                                     |
| dokumentattribut             | [ResourceAttributes](utility-resources.md#resourceattributes) | De metadata-attribut som motsvarar profilen.                                                                                                                |

## <a name="mpnprofile"></a>MpnProfile

Beskriver en partners Microsoft Partner Network profil.

| Egenskap    | Typ                                                           | Description                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| partnerName | sträng                                                         | Företagets eller organisationens namn.                     |
| mpnId       | sträng                                                         | Microsoft Partner Network-ID.                     |
| Profiltyp | sträng                                                         | Partnerns profil typ.                             |
| Länkar       | [ResourceLinks](utility-resources.md#resourcelinks)           | Resurs länkarna som motsvarar profilen.      |
| dokumentattribut  | [ResourceAttributes](utility-resources.md#resourceattributes) | De metadata-attribut som motsvarar profilen. |

## <a name="organizationprofile"></a>OrganizationProfile

Beskriver en partner organisations profil.

| Egenskap       | Typ                                                           | Description                                                            |
|----------------|----------------------------------------------------------------|------------------------------------------------------------------------|
| id             | sträng                                                         | Organisationens ID.                                                 |
| companyName    | sträng                                                         | Namnet på företaget eller organisationen.                               |
| defaultAddress | [Adress](utility-resources.md#address)                       | Företagets eller organisationens standard adress.                    |
| tenantId       | sträng                                                         | Klient-ID.                                                 |
| domän         | sträng                                                         | Företaget eller organisationens domän.                                  |
| e-post          | sträng                                                         | Hämtar eller anger den överordnade prenumerationen.                                  |
| language       | sträng                                                         | Det föredragna språket för kommunikation.                              |
| substrat        | sträng                                                         | Den föredragna kulturen för kommunikation och valuta, till exempel "en-US". |
| Profiltyp    | sträng                                                         | Partnerns profil typ.                                              |
| Länkar          | [ResourceLinks](utility-resources.md#resourcelinks)           | Resurs länkarna som motsvarar profilen.                       |
| dokumentattribut     | [ResourceAttributes](utility-resources.md#resourceattributes) | De metadata-attribut som motsvarar profilen.                  |

## <a name="supportprofile"></a>SupportProfile

Beskriver en partners support profil.

| Egenskap    | Typ                                                           | Description                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| e-post       | sträng                                                         | Den e-postadress som är kopplad till profilen.        |
| telefon   | sträng                                                         | Telefonnumret som är kopplat till profilen.         |
| webbplats     | sträng                                                         | Support webbplatsen.                                  |
| Profiltyp | sträng                                                         | Partnerns profil typ.                             |
| Länkar       | [ResourceLinks](utility-resources.md#resourcelinks)           | Resurs länkarna som motsvarar profilen.      |
| dokumentattribut  | [ResourceAttributes](utility-resources.md#resourceattributes) | De metadata-attribut som motsvarar profilen. |

