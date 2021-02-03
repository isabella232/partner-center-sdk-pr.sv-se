---
title: Konfigurera API-åtkomst i Partner Center
description: Konfigurera konton för utveckling mot Partner Center SDK och test i sandbox-integration.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 873ff2ff9cecbfa92429958d3bfe2aa79fc3ad9a
ms.sourcegitcommit: d5de47c08ba661ba5de4935caa6843d7c2c91710
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/28/2020
ms.locfileid: "97769417"
---
# <a name="set-up-api-access-in-partner-center"></a>Konfigurera API-åtkomst i Partner Center

**Gäller för:**

- Partnercenter
- Partner Center som drivs av 21Vianet
- Välkommen till Partnercenter för Microsoft Cloud for US Government
- Partnercenter för Microsoft Cloud Tyskland

I den här artikeln beskrivs de konton som du måste utveckla mot Partner Center SDK. Den här artikeln beskriver också hur du skapar ett [sandbox-konto](#integration-sandbox-account) och testar det i integration sandbox.

>[!NOTE]
>För att få åtkomst till API: er måste klienten vara en CSP-klient och du måste vara antingen en indirekt provider eller en direkt fakturerings partner.

## <a name="account-definitions"></a>Konto definitioner

För att hjälpa dig att integrera och testa API-integrering stöder Partner Center två typer av konton:

### <a name="primary-partner-account"></a>Primärt partner konto

I det här kontot kan du skapa verkliga beställningar för riktiga kunder. Om du gör ändringar eller transaktioner när du är inloggad på det primära kontot, med hjälp av antingen Partner Center SDK eller partnerns användar gränssnitt, kommer de att behandlas som officiella beställningar för riktiga kunder. De kommer att avspeglas i fakturan och företaget ansvarar för att betala för dem.

### <a name="integration-sandbox-account"></a>Sandbox-konto för integrering

Det här kontot används för att testa din kod och dess integrering med API: er för partner Center innan du distribuerar den i stor ordning. Ändringar och transaktioner som du gör när du är inloggad på det begränsade kontot för integration visas i fakturan, men du behöver inte betala faktura beloppet. Faktura-PDF får en fri skrivning som "betala inte. DETTA ÄR EN SANDBOX-FAKTURA OCH INGEN ÅTGÄRD KRÄVS. "

Det begränsade kontot för integration och det primära kontot fungerar oberoende av varandra och delar inte administratörs konton, användar konton, kunder, beställningar, prenumerationer eller annan information.

-Integrations sand boxen stöder transaktioner med ett begränsat antal kunder, order, prenumerationer, licenser osv.

Som princip är integrations sand Box-konton endast avsedda för integrations testning.

Det finns inget sandbox-konto för integrering som standard. Du måste skapa en själv om du planerar att använda Partner Center SDK.

## <a name="set-up-your-accounts"></a>Konfigurera dina konton

I det här avsnittet beskrivs hur du konfigurerar ett primärt partner konto och ett konto för integration i begränsat läge för partner Center SDK.

### <a name="create-an-integration-sandbox"></a>Skapa en integrations Sand låda

1. Logga in på partner instrument panel med ett globalt administratörs konto (ditt primära partner konto).

2. Från menyn **Inställningar** (kugg hjuls ikon) väljer du **partner inställningar**.

3. Välj fliken **integrations-sandbox** .

    >[!NOTE]
    >Om du inte ser något alternativ för integrations-sandbox kanske du inte har ett globalt administratörs konto. Du kanske också använder ett sandbox-konto för integration och det har redan kon figurer ATS en integrations Sand låda.

4. Ange kontakt information för administratörs kontot för integration sandbox. Välj sedan **Skapa konto**. Vänta några minuter för ett bekräftelse meddelande om att kontot har skapats.

5. När du ser bekräftelse meddelandet loggar du ut från partner instrument panelen.

6. Logga in igen med ditt nya administratörs konto för integration sandbox. Se till att använda formatet **username@domain** för dina autentiseringsuppgifter tillsammans med det lösen ord som du nyss angav.

7. Välj **Konfigurera ett konto** ovanför de **aktuella aktiviteterna** för att slutföra konfigurationen av Sandbox-kontot.

### <a name="enable-api-access"></a>Aktivera API-åtkomst

När ditt konto har konfigurerats måste du aktivera API-åtkomst innan du kan använda SDK:t för Partnercenter med sandbox-kontot för integrering. Du måste aktivera åtkomst till API:et separat för både ditt primära partnerkonto och sandbox-kontot för integrering.

1. Logga in på partner instrument panel med ett globalt administratörs konto.

2. Från menyn **Inställningar** (kugg hjuls ikon) väljer du **partner inställningar**.

3. På sidan **konto inställningar** väljer du **program hantering**.

4. Om du inte redan har en befintlig app lägger du till en ny webbapp. Om du har en befintlig webbapp väljer du knappen **Lägg till nyckel** .

5. Kopiera appens registrerings information, särskilt **nyckeln** om du skapar en webbapp, och lagra den på en säker plats.

6. Logga ut från partner instrument panel.

7. Logga in igen med ditt konto för integration sandbox. Upprepa steg 2-5 för att aktivera API-åtkomst i sandbox-integration.

## <a name="write-and-test-code"></a>Skriv och testa kod

Du kan skriva kod och testa kod i sandbox-integration. Du behöver följande information för att [Konfigurera Partner Center-autentisering](partner-center-authentication.md) med Azure AD.

| Objekt namn | Objekt plats |
| --------- | ------------- |
| App-ID/klient-ID | Från menyn **Inställningar** (kugg hjuls ikon) väljer du **partner inställningar**. På sidan **konto inställningar** väljer du **app Management**. App-ID/klient-ID visas som det **registrerade programmets app-ID**. |
| Nyckel | Om du har skapat en webbapp i avsnittet [Aktivera API-åtkomst](#enable-api-access), är detta den nyckel som du sparade i steg 5. |
| Domain | Domänen för integrations sand boxen. |

## <a name="run-tested-code"></a>Kör testad kod

Om du vill använda din lösning med verkliga kund data måste du ändra från dina autentiseringsuppgifter för integrations-sandbox till dina primära partner konto uppgifter.

När du är redo att använda den testade koden i ditt primära partner konto måste du skaffa en Azure AD-säkerhetstoken. Den här säkerhetstoken är baserad på din partner Center-app, nyckel och domän (i stället för din integrations-sandbox-app, nyckel och domän).

1. Följ stegen i [partner Center-autentisering](partner-center-authentication.md) för att hämta en Azure AD-säkerhetstoken med dina autentiseringsuppgifter för ditt primära partner Center. (Du har tidigare följt dessa steg för att hämta en Azure AD-säkerhetstoken för din integration sandbox.)

2. Ersätt säkerhetstoken för integrering i koden med den nya säkerhetstoken för ditt primära partner konto.
