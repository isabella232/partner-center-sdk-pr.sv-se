---
title: Resurser för tjänstbegäran
description: Partner kan skicka fil tjänst begär Anden åt sina partners till att rapportera avbrott i tjänster som tillhandahålls av Microsoft eller begära annan teknisk support som de inte kan tillhandahålla.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 072f9eddaf9d854f1dcc8cc65f7928b6c95700fa
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768925"
---
# <a name="service-request-resources"></a>Resurser för tjänstbegäran

**Gäller för**

- Partnercenter
- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Partner kan skicka fil tjänst begär Anden åt sina partners till att rapportera avbrott i tjänster som tillhandahålls av Microsoft eller begära annan teknisk support som de inte kan tillhandahålla.

## <a name="servicerequest"></a>ServiceRequest

Beskriver en tjänstbegäran som har arkiverats av en partner, inklusive hur begäran fortskrider.

| Egenskap         | Typ                                                          | Description                                                                          |
|------------------|---------------------------------------------------------------|--------------------------------------------------------------------------------------|
| Rubrik            | sträng                                                        | Rubriken för tjänst begär Anden.                                                           |
| Description      | sträng                                                        | Beskrivningen.                                                                     |
| Allvarlighetsgrad         | sträng                                                        | Allvarlighets graden: "okänd", "kritisk", "måttlig" eller "minimal".                       |
| SupportTopicId   | sträng                                                        | ID för support ämnet.                                                         |
| SupportTopicName | sträng                                                        | Namnet på support ämnet.                                                       |
| Id               | sträng                                                        | ID för tjänstbegäran.                                                       |
| Status           | sträng                                                        | Status för tjänstbegäran: "ingen", "öppen", "stängd" eller "åtgärd \_ krävs". |
| Organisation     | [ServiceRequestOrganization](#servicerequestorganization)     | Organisation för vilken tjänstbegäran skapas.                               |
| PrimaryContact   | [ServiceRequestContact](#servicerequestcontact)               | Primär kontakt för tjänstbegäran.                                              |
| LastUpdatedBy    | [ServiceRequestContact](#servicerequestcontact)               | "Senast uppdaterad av" kontakta ändringar i tjänstbegäran.                        |
| ProductName      | sträng                                                        | Namnet på den produkt som motsvarar tjänst förfrågan.                     |
| ProductId        | sträng                                                        | Produktens ID.                                                               |
| CreatedDate      | date                                                          | Datum för när service förfrågan skapades.                                          |
| LastModifiedDate | date                                                          | Det datum då tjänste förfrågan senast ändrades.                                 |
| LastClosedDate   | date                                                          | Datumet då tjänste förfrågan senast stängdes.                                   |
| FileLinks        | matris med [fileinfo](utility-resources.md#fileinfo) -resurser | Den samling med fil länkar som hör till tjänstbegäran.                    |
| NewNote          | [ServiceRequestNote](#servicerequestnote)                     | En anteckning kan läggas till i en befintlig tjänstbegäran.                                  |
| Kommentarer            | matris med [ServiceRequestNotes](#servicerequestnote)           | En samling anteckningar som lagts till i tjänstbegäran.                                  |
| CountryCode      | sträng                                                        | Det land som motsvarar tjänste förfrågan.                                    |
| Attribut       | ResourceAttributes                                            | De metadata-attribut som motsvarar tjänst förfrågan.                        |

## <a name="servicerequestcontact"></a>ServiceRequestContact

Beskriver en kontakt som skapar eller ändrar en tjänstbegäran.

| Egenskap     | Typ                                                      | Description                                            |
|--------------|-----------------------------------------------------------|--------------------------------------------------------|
| Organisation | [ServiceRequestOrganization](#servicerequestorganization) | Organisation för vilken tjänstbegäran skapas. |
| ContactId    | sträng                                                    | Kontaktens unika ID.                               |
| LastName     | sträng                                                    | Kontaktens efter namn.                          |
| FirstName    | sträng                                                    | Kontaktens förnamn.                         |
| E-post        | sträng                                                    | Kontaktens e-postadress.                              |
| PhoneNumber  | sträng                                                    | Telefonnumret till kontakten.                       |

## <a name="servicerequestnote"></a>ServiceRequestNote

Beskriver en anteckning som är kopplad till en tjänstbegäran.

| Egenskap      | Typ   | Description                                  |
|---------------|--------|----------------------------------------------|
| CreatedByName | sträng | Namnet på anteckningens skapare.         |
| CreatedDate   | date   | Datum och tid när anteckningen skapades. |
| Text          | sträng | Anteckningens text.                        |

## <a name="servicerequestorganization"></a>ServiceRequestOrganization

Beskriver den organisation som tjänstbegäran skapas för.

| Egenskap    | Typ   | Description                           |
|-------------|--------|---------------------------------------|
| Id          | sträng | Organisationens unika ID.    |
| Name        | sträng | Organisationens namn.         |
| PhoneNumber | sträng | Organisationens telefonnummer. |

## <a name="supporttopic"></a>SupportTopic

Beskriver ett support avsnitt. Tjänst begär Anden anger ett support ämne för att säkerställa att de bearbetas snabbt och effektivt.

| Egenskap    | Typ               | Beskrivning                                                   |
|-------------|--------------------|---------------------------------------------------------------|
| Name        | sträng             | Namnet på support ämnet.                                |
| Description | sträng             | Beskrivning av support avsnittet.                         |
| Id          | sträng             | Unikt ID för support ämnet.                           |
| Attribut  | ResourceAttributes | De metadata-attribut som motsvarar tjänst förfrågan. |

