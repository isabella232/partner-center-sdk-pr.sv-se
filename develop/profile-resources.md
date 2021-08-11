---
title: Profilresurser
description: Beskriver beteendet för Molnlösningsleverantör en enhets profiler.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8d4c091e186b7a3ad13aee7202b3d992af95db8db50acd40a5ade496d7087359
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997319"
---
# <a name="profile-resources"></a>Profilresurser

**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Beskriver beteendet för Molnlösningsleverantör en enhets profiler.

## <a name="billingprofile"></a>BillingProfile

Beskriver en partners faktureringsprofil.

| Egenskap            | Typ                                                           | Description                                                 |
|---------------------|----------------------------------------------------------------|-------------------------------------------------------------|
| companyName         | sträng                                                         | Faktureringsföretagets namn.                                   |
| adress             | [Adress](utility-resources.md#address)                       | Företagets eller organisationens faktureringsadress. |
| primaryContact      | [Kontakt](utility-resources.md#contact)                       | Den primära kontakten för företaget eller organisationen.        |
| purchaseOrderNumber | sträng                                                         | Företagets eller organisationens inköpsordernummer.        |
| taxId               | sträng                                                         | Företagets eller organisationens skatte-ID.                       |
| billingCurrency     | sträng                                                         | Den valuta som används av företaget eller organisationen.           |
| profileType         | sträng                                                         | Partnerprofiltypen.                                   |
| Länkar               | [ResourceLinks](utility-resources.md#resourcelinks)           | Resursen länkar som motsvarar profilen.            |
| Attribut          | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen som motsvarar profilen.       |

## <a name="legalbusinessprofile"></a>LegalBusinessProfile

Beskriver en partners juridiska affärsprofil.

| Egenskap               | Typ                                                           | Description                                                                                                                                                          |
|------------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| companyName            | sträng                                                         | Företagets juridiska namn.                                                                                                                                              |
| adress                | [Adress](utility-resources.md#address)                       | Företagets eller organisationens adress.                                                                                                                          |
| primaryContact         | [Kontakt](utility-resources.md#contact)                       | Den primära kontakten för företaget eller organisationen.                                                                                                                 |
| companyApproverAddress | [Adress](utility-resources.md#address)                       | Företagets godkännaradress.                                                                                                                                        |
| companyApproverEmail   | sträng                                                         | Företagets godkännare skickar e-post.                                                                                                                                          |
| vettingStatus          | sträng                                                         | Granskningsstatus. Det här värdet är strängrepresentationen av ett av medlemsnamnen som finns i [**VettingStatus**](/dotnet/api/microsoft.store.partnercenter.models.partners.vettingstatus).           |
| vettingSubStatus       | sträng                                                         | Understatusen för granskning. Det här värdet är strängrepresentationen av ett av medlemsnamnen som finns i [**VettingSubStatus**](/dotnet/api/microsoft.store.partnercenter.models.partners.vettingsubstatus). |
| profileType            | sträng                                                         | Partnerprofiltypen.                                                                                                                                            |
| Länkar                  | [ResourceLinks](utility-resources.md#resourcelinks)           | Resursen länkar som motsvarar profilen.                                                                                                                     |
| Attribut             | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen som motsvarar profilen.                                                                                                                |

## <a name="mpnprofile"></a>MpnProfile

Beskriver en partners Microsoft Partner Network profil.

| Egenskap    | Typ                                                           | Description                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| partnerName | sträng                                                         | Företagets eller organisationens namn.                     |
| mpnId       | sträng                                                         | ID Microsoft Partner Network (MPN).                     |
| profileType | sträng                                                         | Partnerprofiltypen.                             |
| Länkar       | [ResourceLinks](utility-resources.md#resourcelinks)           | Resursen länkar som motsvarar profilen.      |
| Attribut  | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen som motsvarar profilen. |

## <a name="organizationprofile"></a>OrganizationProfile

Beskriver en partners organisationsprofil.

| Egenskap       | Typ                                                           | Description                                                            |
|----------------|----------------------------------------------------------------|------------------------------------------------------------------------|
| id             | sträng                                                         | Organisationens ID.                                                 |
| companyName    | sträng                                                         | Namnet på företaget eller organisationen.                               |
| defaultAddress | [Adress](utility-resources.md#address)                       | Standardadressen för företaget eller organisationen.                    |
| tenantId       | sträng                                                         | Klientorganisationens identifierare.                                                 |
| domän         | sträng                                                         | Företagets eller organisationens domän.                                  |
| e-post          | sträng                                                         | Hämtar eller anger den överordnade prenumerationen.                                  |
| language       | sträng                                                         | Det föredragna språket för kommunikation.                              |
| Kultur        | sträng                                                         | Den önskade kulturen för kommunikation och valuta, till exempel "en-us". |
| profileType    | sträng                                                         | Partnerprofiltypen.                                              |
| Länkar          | [ResourceLinks](utility-resources.md#resourcelinks)           | Resursen länkar som motsvarar profilen.                       |
| Attribut     | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen som motsvarar profilen.                  |

## <a name="supportprofile"></a>SupportProfile

Beskriver en partners supportprofil.

| Egenskap    | Typ                                                           | Description                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| e-post       | sträng                                                         | Den e-postadress som är associerad med profilen.        |
| telefon   | sträng                                                         | Telefonnumret som är associerat med profilen.         |
| webbplats     | sträng                                                         | Supportwebbplatsen.                                  |
| profileType | sträng                                                         | Partnerprofiltypen.                             |
| Länkar       | [ResourceLinks](utility-resources.md#resourcelinks)           | Resursen länkar som motsvarar profilen.      |
| Attribut  | [ResourceAttributes](utility-resources.md#resourceattributes) | Metadataattributen som motsvarar profilen. |

