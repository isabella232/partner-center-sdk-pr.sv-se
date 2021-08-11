---
title: Hantera utbetalningar med hjälp av API:et för utbetalningstjänsten
description: Lär dig hur du använder partnercentrets utbetalningstjänst-API för att få åtkomst till utbetalningsdata
ms.date: 06/23/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: jasongroce
ms.author: sabaja
ms.openlocfilehash: b9bdc6da64a79f4f35466fb62662b086a8e1ab3cadc99c7ca685303752f9d166
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996409"
---
# <a name="manage-payouts-using-the-payout-service-api"></a>Hantera utbetalningar med hjälp av API:et för utbetalningstjänsten

Den här artikeln förklarar hur du kan komma åt utbetalningsdata via API:erna för utbetalningstjänsten i stället för partnercentergränssnittet. Dessa API:er är ett programmatiskt sätt att tillhandahålla funktionerna i [funktionen Exportera data](https://partner.microsoft.com/dashboard/payouts/reports/incentiveexport) i Partnercenter.

## <a name="available-apis"></a>Tillgängliga API:er

Se alla tillgängliga API:er på [Partner payouts (Partnerutbetalningar).](/rest/api/partner-center/partner-payouts)

## <a name="prerequisites"></a>Förutsättningar

- [Registrera ett program med AAD/Microsoft Identity](/graph/auth-register-app-v2) i Azure Portal och lägg till lämpliga ägare och roller i programmet.
- Installera [Visual Studio](https://visualstudio.microsoft.com/downloads/).

## <a name="register-an-application-with-the-microsoft-identity-platform"></a>Registrera en app på Microsoft Identity Platform

Med [Microsofts identitetsplattform](/azure/active-directory/develop/v2-overview) kan du skapa program som dina användare och kunder kan logga in på med sina Microsoft-identiteter eller sociala konton och ge auktoriserad åtkomst till dina egna API:er eller Microsoft-API:er som Microsoft Graph.

1. Logga in på [Azure-portalen](https://portal.azure.com/) med ett arbets- eller skolkonto eller ett personligt Microsoft-konto.

   Om ditt konto ger dig åtkomst till fler än en klientorganisation väljer du ditt konto i det övre högra hörnet och ställer in portalsessionen på rätt Azure AD-klientorganisation.

2. I det vänstra navigeringsfönstret väljer du Azure Active Directory och sedan **Appregistreringar** och **sedan Ny registrering.** Sidan **Registrera ett** program visas.

   :::image type="content" source="./images/manage-payouts/new-app-registration.png" alt-text="Skärmbild som visar skärmen Registrera en app i Azure Portal.":::

3. Ange programmets registreringsinformation:

   - Namn: Ange ett beskrivande programnamn som ska visas för användare av appen.
   - Kontotyper som stöds: Välj vilka konton som ska stödjas av ditt program.

    | **Kontotyper som stöds**                             | **Beskrivning**                                                                                            |
    |---------------------------------------------------------|------------------------------------------------------------------------------------------------------------|
    | Endast konton i den här organisationskatalogen          | Välj det här alternativet om du skapar en verksamhetsspecifik app. Det här alternativet är inte tillgängligt om du inte registrerar programmet i en katalog. Det här alternativet mappar endast till Azure AD för en enskild klientorganisation.  Det här alternativet är standard om du inte registrerar appen utanför en katalog. I fall då appen registreras utanför en katalog är standardalternativet Azure AD för flera klientorganisationer och personliga Microsoft-konton.             |
    | Konton i valfri organisationskatalog                | Välj det här alternativet om du vill rikta dig till mot alla företags- och utbildningskunder.  Det här alternativet mappar endast till Azure AD för flera klientorganisationer. Om du registrerade appen som endast Azure AD för en enskild klientorganisation kan du uppdatera den till att bli endast Azure AD för flera klientorganisationer och tillbaka till en enskild klientorganisation via bladet Autentisering.                                                                                                                                                  |
    | Konton i en valfri organisationskatalog och personliga Microsoft-konton | Välj det här alternativet om målgruppen är bredast möjliga uppsättning av kunder. Det här alternativet mappar till Azure AD för flera klientorganisationer och personliga Microsoft-konton.  Om du har registrerat appen som Azure AD för flera innehavare och personliga Microsoft-konton kan du inte ändra det här valet i användargränssnittet. Du måste i stället använda redigeringsprogrammet för applikationsmanifest för att ändra de kontotyper som stöds.                                                                          |

   - *(valfritt)* Omdirigerings-URI: Välj den typ av app som du skapar, Webb eller Offentlig klient (Mobile & Desktop) och ange sedan omdirigerings-URI (eller svars-URL) för ditt program. (Omdirigerings-URL:en är den plats där autentiseringssvaret skickas när användaren autentiseras.) 

      För webbappar anger du grundläggande URL för appen. Till exempel kan `http://localhost:31544` vara URL för en webbapp som körs på din lokala dator. Användare skulle då använda den här URL:en för att logga in till ett webbklientprogram.
      För offentliga klientprogram anger du den URI som används av Azure AD för att returnera tokensvar. Ange ett värde som är specifikt för ditt program, till exempel `myapp://auth`.

4. Välj **Register** (Registrera). Azure AD tilldelar ett unikt program-ID (klient) till ditt program och programmets översiktssida läses in.

   :::image type="content" source="./images/manage-payouts/register-an-application.png" alt-text="<alternativtext>":::

5. Om du vill lägga till funktioner i ditt program kan du välja andra konfigurationsalternativ, till exempel varumärke, certifikat och hemligheter, API-behörigheter med mera.

## <a name="platform-specific-properties"></a>Plattformsspecifika egenskaper

I följande tabell visas de egenskaper som du behöver för att konfigurera och kopiera för olika typer av appar. **Tilldelad** innebär att du bör använda värdet som tilldelats av Azure AD.

| Typ av app              | Plattform | Program-ID (klient) | Client Secret (Klienthemlighet) | Omdirigerings-URI/URL | Implicit Flow                                                         |
|-----------------------|----------|-------------------------|---------------|------------------|-----------------------------------------------------------------------|
| Intern/mobil         | Intern   | Tilldelad                | No            | Tilldelad         | No                                                                    |
| Webbapp               | Webb      | Tilldelad                | Ja           | Ja              | Valfri Open ID Anslut program använder hybridflöde som standard (Ja) |
| Ensidesapp (SPA) | Webb      | Tilldelad                | Ja           | Ja              | Ja SPA:er använder Open ID Anslut implicit Flow                            |
| Tjänst/Daemon        | Webb      | Tilldelad                | Ja           | Ja              | Inga                                                                    |

## <a name="create-a-service-principal"></a>Skapa ett huvudnamn för tjänsten

Om du vill komma åt resurser i din prenumeration måste du tilldela en roll till programmet. Hjälp med att bestämma vilken roll som ger rätt behörigheter för programmet finns i [Inbyggda Roller i Azure.](/azure/role-based-access-control/built-in-roles)

> [!NOTE]
> Du kan ange omfånget på prenumerationsnivå, resursgrupp eller resursnivå. Behörigheter ärvs till lägre omfångsnivåer. Om du till exempel lägger till ett program i rollen Läsare för en resursgrupp kan den läsa resursgruppen och alla resurser som den innehåller.

1. I Azure Portal du den omfångsnivå som programmet ska tilldelas. Om du till exempel vill tilldela en roll i prenumerationsomfånget söker du efter och väljer Prenumerationer **eller** **väljer** Prenumerationer på startsidan.

   :::image type="content" source="./images/manage-payouts/search-for-subscriptions.png" alt-text="Skärmbild som visar skärmsökningen Prenumerationer.":::

2. Välj den prenumeration som programmet ska tilldelas till.

   :::image type="content" source="./images/manage-payouts/internal-testing-subscription.png" alt-text="Skärmbild som visar skärmen Prenumerationer med flaggan Intern testning inställd på sant.":::

> [!NOTE]
> Om du inte ser den prenumeration som du letar efter väljer du filtret globala prenumerationer och ser till att den prenumeration som du vill använda är markerad för portalen.

3. Välj **Åtkomstkontroll (IAM)** och sedan **Lägg till rolltilldelning**.

4. Välj den roll som du vill tilldela till programmet. Om du till exempel vill tillåta att programmet kör åtgärder som omstart, startar och stoppar instanser väljer du rollen Deltagare. Läs mer om [tillgängliga roller.](/azure/role-based-access-control/built-in-roles)

   Som standard visas inte Azure AD-program i de tillgängliga alternativen. Du hittar programmet genom att söka efter namnet och välja det i resultatet. I skärmbilden nedan är `example-app` AAD-appen som du registrerade.

   :::image type="content" source="./images/manage-payouts/add-role-assignment.png" alt-text="Skärmbild som visar användargränssnittet för att lägga till en rolltilldelning för ett testprogram.":::

5. Välj **Spara**. Du kan sedan se ditt program i listan över användare med en roll för det omfånget.

   Du kan börja använda tjänstens huvudnamn för att köra skript eller appar. Om du vill hantera behörigheter för tjänstens huvudnamn kan du läsa status för användarmedgivande, granska behörigheter, se inloggningsinformation med mera), visa dina företagsprogram i [Azure Portal](https://portal.azure.com).

## <a name="set-up-api-permissions"></a>Konfigurera API-behörigheter

Det här avsnittet innehåller anvisningar om hur du ställer in de API-behörigheter som krävs. Mer information om hur du ställer in API-behörigheter för Partnercenter finns [i Partner-API autentisering](/partner/develop/api-authentication).

**Bevilja behörighet till Graph API**

1. Öppna [Appregistreringar](https://go.microsoft.com/fwlink/?linkid=2083908) i Azure Portal.

2. Välj ett program eller [skapa en app](/azure/active-directory/develop/quickstart-register-app) om du inte redan har en.

3. På programmets översiktssida går du till **Hantera,** väljer **API-behörigheter och** sedan **Lägg till en behörighet.**

4. Välj **Microsoft Graph** listan över tillgängliga API:er.

5. Välj **Delegerade behörigheter** och lägg till nödvändiga behörigheter. Mer information finns i Konfigurera [appåtkomst.](/azure/active-directory/develop/quickstart-configure-app-access-web-apis)

   :::image type="content" source="./images/manage-payouts/graph-request-api-permissions.png" alt-text="Skärmbild som visar skärmen för behörighetsbegäran i Azure Portal med Microsoft Graph valt.":::

**Medgivande till API-åtkomst till Partner Center API via AAD-app**

6. För ditt program väljer du **API-behörigheter.** På skärmen Begär API-behörigheter väljer du Lägg till en behörighet **och** sedan **API:er som min organisation använder.**

7. Sök efter **MICROSOFT Partner (Microsoft Dev Center) API (4990cffe-04e8-4e8b-808a-1175604b879f)**.

   :::image type="content" source="./images/manage-payouts/partner-api-request-permissions.png" alt-text="Skärmbild som visar skärmen API-behörigheter med Microsoft-partner vald.":::

8. Ange Delegerade behörigheter till **Partnercenter.**

   :::image type="content" source="./images/manage-payouts/partner-api-request-permissions.png" alt-text="Skärmbild som visar de delegerade behörigheter som valts för Partnercenter på skärmen Begär API-behörigheter.":::

9. Bevilja **administratörsmedgivande** för API:erna.

   :::image type="content" source="./images/manage-payouts/api-permissions.png" alt-text="Skärmbild som visar växlingsknappen för administratörsmedgivande på skärmen API-behörigheter.":::

   Kontrollera att Administratörsmedgivande är aktiverat på skärmen Status för administratörsmedgivande.

   :::image type="content" source="./images/manage-payouts/admin-consent-verification.png" alt-text="Skärmbild som visar skärmen status för administratörsmedgivande":::

10. I avsnittet **Autentisering** kontrollerar du att alternativet **Tillåt offentliga klientflöden** är inställt på **Ja.**

    :::image type="content" source="./images/manage-payouts/allow-public-client-flows.png" alt-text="Skärmbild som visar skärmen Autentisering med Tillåt offentliga klientflöden inställt på Ja.":::

## <a name="run-the-sample-code-in-visual-studio"></a>Kör exempelkoden i Visual Studio

Exempelkod som visar hur API:et kan användas för betalning och transaktionshistorik finns i [Partner-Center-Payout-API:er](https://github.com/microsoft/Partner-Center-Payout-APIs) GitHub lagringsplatsen.

### <a name="sample-code-notes"></a>Exempel på kodanteckningar

- Konfiguration av klienthemligheter och certifikat som beskrivs i avsnittet Autentisering: Två alternativ i Skapa ett huvudnamn för [tjänsten i Azure Portal](/azure/active-directory/develop/howto-create-service-principal-portal) inte krävs.
- Konton med multifaktorautentisering (MFA) stöds inte för närvarande och kommer att orsaka ett fel.
- Utbetalnings-API stöder endast användar-/lösenordsbaserade autentiseringsuppgifter.

## <a name="next-steps"></a>Nästa steg

- [Använd portalen för att skapa ett Azure AD-program och huvudnamn för tjänsten som kan komma åt resurser](/azure/active-directory/develop/howto-create-service-principal-portal)
- [Registrera en app på Microsoft Identity Platform](/graph/auth-register-app-v2)
- [Konfigurera ett klientprogram för åtkomst till ett webb-API](/azure/active-directory/develop/quickstart-configure-app-access-web-apis)
