---
title: Resurser för tjänstbegäran
description: Partner kan skicka tjänstbegäranden åt sina partner för att rapportera avbrottstjänster som tillhandahålls av Microsoft eller för att begära annan teknisk support som de inte kan tillhandahålla.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f919b3c34ff179a7a6cd0541f34c53737ec4148e44791419d2252fae64b0658d
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115993239"
---
# <a name="service-request-resources"></a>Resurser för tjänstbegäran

**Gäller för**: Partner Center-| PartnerCenter för Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Partner kan skicka tjänstbegäranden åt sina partner för att rapportera avbrottstjänster som tillhandahålls av Microsoft eller för att begära annan teknisk support som de inte kan tillhandahålla.

## <a name="servicerequest"></a>ServiceRequest

Beskriver en tjänstbegäran som har arkiverats av en partner, inklusive hur begäran fortskrider.

| Egenskap         | Typ                                                          | Description                                                                          |
|------------------|---------------------------------------------------------------|--------------------------------------------------------------------------------------|
| Rubrik            | sträng                                                        | Rubriken för tjänstbegäran.                                                           |
| Description      | sträng                                                        | Beskrivningen.                                                                     |
| Allvarlighetsgrad         | sträng                                                        | Allvarlighetsgraden: "okänd", "kritisk", "måttlig" eller "minimal".                       |
| SupportTopicId   | sträng                                                        | ID för supportämnet.                                                         |
| SupportTopicName | sträng                                                        | Namnet på supportämnet.                                                       |
| Id               | sträng                                                        | ID för tjänstbegäran.                                                       |
| Status           | sträng                                                        | Status för tjänstbegäran: "none", "open", "closed" eller "attention \_ needed". |
| Organisation     | [ServiceRequestOrganization](#servicerequestorganization)     | Organisation som tjänstbegäran skapas för.                               |
| PrimaryContact   | [ServiceRequestContact](#servicerequestcontact)               | Primär kontakt i tjänstbegäran.                                              |
| LastUpdatedBy    | [ServiceRequestContact](#servicerequestcontact)               | "Senast uppdaterad av"-kontakt för ändringar i tjänstbegäran.                        |
| ProductName      | sträng                                                        | Namnet på den produkt som motsvarar tjänstbegäran.                     |
| ProductId        | sträng                                                        | ID för produkten.                                                               |
| CreatedDate      | date                                                          | Datumet då tjänstbegäran skapades.                                          |
| LastModifiedDate | date                                                          | Det datum då tjänstbegäran senast ändrades.                                 |
| LastClosedDate   | date                                                          | Det datum då tjänstbegäran senast avslutades.                                   |
| FileLinks        | matris med [FileInfo-resurser](utility-resources.md#fileinfo) | Den samling fillänkar som hör till tjänstbegäran.                    |
| NewNote          | [ServiceRequestNote](#servicerequestnote)                     | En anteckning kan läggas till i en befintlig tjänstbegäran.                                  |
| Kommentarer            | matris med [ServiceRequestNotes](#servicerequestnote)           | En samling anteckningar som lagts till i tjänstbegäran.                                  |
| CountryCode      | sträng                                                        | Det land som motsvarar tjänstbegäran.                                    |
| Attribut       | ResourceAttributes                                            | Metadataattributen som motsvarar tjänstbegäran.                        |

## <a name="servicerequestcontact"></a>ServiceRequestContact

Beskriver en kontakt som skapar eller ändrar en tjänstbegäran.

| Egenskap     | Typ                                                      | Description                                            |
|--------------|-----------------------------------------------------------|--------------------------------------------------------|
| Organisation | [ServiceRequestOrganization](#servicerequestorganization) | Organisation som tjänstbegäran skapas för. |
| ContactId    | sträng                                                    | Kontaktens unika ID.                               |
| LastName     | sträng                                                    | Kontaktens efternamn.                          |
| FirstName    | sträng                                                    | Kontaktens förnamn.                         |
| E-post        | sträng                                                    | Kontaktens e-postadress.                              |
| PhoneNumber  | sträng                                                    | Kontaktens telefonnummer.                       |

## <a name="servicerequestnote"></a>ServiceRequestNote

Beskriver en anteckning som är kopplad till en tjänstbegäran.

| Egenskap      | Typ   | Description                                  |
|---------------|--------|----------------------------------------------|
| CreatedByName | sträng | Namnet på anteckningens skapare.         |
| CreatedDate   | date   | Datum och tid då anteckningen skapades. |
| Text          | sträng | Anteckningens text.                        |

## <a name="servicerequestorganization"></a>ServiceRequestOrganization

Beskriver den organisation som tjänstbegäran skapas för.

| Egenskap    | Typ   | Description                           |
|-------------|--------|---------------------------------------|
| Id          | sträng | Organisationens unika ID.    |
| Name        | sträng | Organisationens namn.         |
| PhoneNumber | sträng | Organisationens telefonnummer. |

## <a name="supporttopic"></a>SupportTopic

Beskriver ett supportämne. Tjänstförfrågningar anger ett supportämne för att säkerställa att de bearbetas snabbt och effektivt.

| Egenskap    | Typ               | Beskrivning                                                   |
|-------------|--------------------|---------------------------------------------------------------|
| Name        | sträng             | Namnet på supportämnet.                                |
| Description | sträng             | Beskrivning av supportämnet.                         |
| Id          | sträng             | Unikt ID för supportämnet.                           |
| Attribut  | ResourceAttributes | Metadataattributen som motsvarar tjänstbegäran. |

