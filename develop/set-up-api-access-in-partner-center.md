---
title: Konfigurera API-åtkomst i Partner Center
description: Konfigurera konton för utveckling mot Partnercenter-SDK och testa i sandbox-miljön för integrering.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2c564baa9b626ff6ce21f9bcc517902d7cf99244
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547435"
---
# <a name="set-up-api-access-in-partner-center"></a>Konfigurera API-åtkomst i Partner Center

**Gäller för**: Partner Center-| Partnercenter som drivs av 21Vianet | Partnercenter för Microsoft Cloud for US Government | Partnercenter för Microsoft Cloud Tyskland

I den här artikeln beskrivs de konton som du behöver utveckla mot Partnercenter-SDK. Den här artikeln förklarar också hur du skapar ett [sandbox-konto för integrering och](#integration-sandbox-account) testar i sandbox-miljön för integrering.

>[!NOTE]
>För att få åtkomst till API:er måste din klient vara en CSP-klient och du måste vara antingen en indirekt leverantör eller en partner för direktfakturering.

## <a name="account-definitions"></a>Kontodefinitioner

Partner Center har stöd för två typer av konton som hjälper dig att integrera och testa API-integreringen:

### <a name="primary-partner-account"></a>Primärt partnerkonto

På det här kontot skapar du verkliga beställningar för verkliga kunder. Om du gör ändringar eller transaktioner när du är inloggad på det primära kontot, med hjälp av antingen Partnercenter-SDK eller partnerinstrumentpanelens användargränssnitt, behandlas de som officiella beställningar för verkliga kunder. De visas på din faktura och ditt företag ansvarar för att betala för dem.

### <a name="integration-sandbox-account"></a>Sandbox-konto för integrering

Det här kontot används för att testa din kod och dess integrering med Partner Center-API:erna innan du distribuerar den brett. Ändringar och transaktioner som du gör när du är inloggad på sandbox-kontot för integrering visas på din faktura, men du behöver inte betala fakturabeloppet. Faktura-PDF har en ansvarsfriskrivning som "BETALA INTE. DET HÄR ÄR EN SANDBOX-FAKTURA OCH INGEN ÅTGÄRD KRÄVS."

Sandbox-kontot för integrering och det primära kontot fungerar oberoende och delar inte administratörskonton, användarkonton, kunder, beställningar, prenumerationer eller andra data.

Sandbox-miljön för integrering stöder transaktioner med ett begränsat antal kunder, beställningar, prenumerationer, licenser osv.

Enligt principen är integrations-sandbox-konton endast avsedda för integreringstestning.

Det finns inget sandbox-konto för integrering som standard. Du måste skapa en själv om du planerar att använda Partnercenter-SDK.

## <a name="set-up-your-accounts"></a>Konfigurera dina konton

I det här avsnittet beskrivs hur du ställer in ett primärt partnerkonto och ett sandbox-konto för integrering för Partnercenter-SDK.

### <a name="create-an-integration-sandbox"></a>Skapa en sandbox-miljö för integrering

1. Logga in på partnerinstrumentpanelen med ett globalt administratörskonto (ditt primära partnerkonto.)

2. På **Inställningar** (kugghjulsikonen) väljer du **Partnerinställningar.**

3. Välj **fliken Sandbox-miljö för** integrering.

    >[!NOTE]
    >Om du inte ser alternativet Sandbox-miljö för integrering kanske du inte har något globalt administratörskonto. Du kanske också använder ett sandbox-konto för integrering och en sandbox-miljö för integrering har redan ställts in.

4. Ange kontaktinformationen för administratörskontot för sandbox-integrering. Välj sedan **Skapa konto.** Vänta några minuter på ett bekräftelsemeddelande om att kontot har skapats.

5. När du ser bekräftelsemeddelandet loggar du ut från Partnerinstrumentpanel.

6. Logga in igen med ditt nya administratörskonto för sandbox-integrering. Se till att använda formatet för **username@domain** dina autentiseringsuppgifter tillsammans med det lösenord som du har angett.

7. Välj **Konfigurera konto ovanför Aktuella** uppgifter för **att** slutföra konfigurationen av sandbox-kontot.

### <a name="enable-api-access"></a>Aktivera API-åtkomst

När ditt konto har konfigurerats måste du aktivera API-åtkomst innan du kan använda SDK:t för Partnercenter med sandbox-kontot för integrering. Du måste aktivera åtkomst till API:et separat för både ditt primära partnerkonto och sandbox-kontot för integrering.

1. Logga in på partnerinstrumentpanelen med ett globalt administratörskonto.

2. På **Inställningar** (kugghjulsikonen) väljer du **Partnerinställningar.**

3. På sidan **Kontoinställningar** väljer du **Apphantering.**

4. Om du inte redan har en befintlig app lägger du till en ny webbapp. Om du har en befintlig webbapp väljer du knappen **Lägg till** nyckel.

5. Kopiera appregistreringsinformationen, särskilt **nyckeln** om du skapar en webbapp och lagra den på en säker plats.

6. Logga ut från partnerinstrumentpanelen.

7. Logga in igen med ditt sandbox-konto för integrering. Upprepa steg 2–5 för att aktivera API-åtkomst i sandbox-miljön för integrering.

## <a name="write-and-test-code"></a>Skriva och testa kod

Du kan skriva kod och testa kod i sandbox-miljön för integrering. Du behöver följande information för att konfigurera [Partner Center-autentisering](partner-center-authentication.md) med Azure AD.

| Objektnamn | Objektplats |
| --------- | ------------- |
| App-ID/klient-ID | På **Inställningar** (kugghjulsikonen) väljer du **Partnerinställningar.** På sidan **Kontoinställningar** väljer du **Apphantering.** App-ID/klient-ID visas som **det registrerade app-ID:t.** |
| Nyckel | Om du skapade en webbapp i avsnittet [Aktivera API-åtkomst](#enable-api-access)är det här nyckeln som du sparade i steg 5. |
| Domain | Domänen för sandbox-miljön för integrering. |

## <a name="run-tested-code"></a>Köra testad kod

Om du vill använda din lösning med verkliga kunddata måste du ändra från dina autentiseringsuppgifter för sandbox-integrering till autentiseringsuppgifterna för ditt primära partnerkonto.

När du är redo att använda din testade kod i ditt primära partnerkonto måste du hämta en Azure AD-säkerhetstoken. Den här säkerhetstoken baseras på din Partner Center-app, nyckel och domän (i stället för din integrerings-sandbox-app, nyckel och domän).

1. Följ stegen i Partner [Center-autentisering för att hämta](partner-center-authentication.md) en Azure AD-säkerhetstoken med dina primära Autentiseringsuppgifter för Partnercenter. (Du har tidigare följt de här stegen för att hämta en Azure AD-säkerhetstoken för din sandbox-miljö för integrering.)

2. Ersätt integrationssäkerhetstoken i koden med den nya säkerhetstoken för ditt primära partnerkonto.
