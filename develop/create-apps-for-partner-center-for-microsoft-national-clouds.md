---
title: Registrera information om appar för partner Center för Microsoft National Cloud
description: Lär dig hur och varför Apps-utvecklare för partner Center för Microsoft National Cloud måste registrera information om sin app med Azure AD via Azure Portal.
MS-HAID:
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_cloud\_germany
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_national\_clouds
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 887cb71c752ac5d9c61398536711545c19cc7600
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770145"
---
# <a name="register-app-details-for-partner-center-for-microsoft-national-cloud-through-the-azure-portal"></a>Registrera information om appar för partner Center för Microsoft National Cloud via Azure Portal

**Gäller för:**

- Partnercenter för Microsoft Cloud Tyskland
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Utvecklare måste registrera information om sin app med Azure AD via Azure Portal. Detta säkerställer att endast angivna appar kan ansluta till partner-och kund information.

För partner Center för Microsoft Cloud för amerikanska myndigheter måste du för närvarande hantera appar via PowerShell. Mer information finns i [referens dokumentationen för Azure PowerShell](/powershell/module/Azuread/#applications).

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Tänk på följande ytterligare krav när du skapar en app för partner Center för Microsoft Cloud Tyskland eller partner Center för Microsoft Cloud för amerikanska myndigheter.

## <a name="web-apps"></a>Webbappar

För webbappar använder du följande procedurer för att registrera ditt program-ID.

### <a name="create-or-update-web-app"></a>Skapa eller uppdatera en webbapp

1. Gå till sidan [Azure Portal-Appregistreringar](https://go.microsoft.com/fwlink/?linkid=2083908) för att registrera din app. Logga in på Azure-portalen med ett arbets- eller skolkonto eller ett personligt Microsoft-konto.

2. Välj **ny registrering**. Mer information finns i [snabb start: registrera ett program med Microsoft Identity Platform](/azure/active-directory/develop/quickstart-register-app).

### <a name="configure-api-access-permissions-for-web-app"></a>Konfigurera API-åtkomst behörigheter för webb program

1. Välj din app. Gå till **Inställningar** för webbappen.

2. I avsnittet **API-åtkomst** väljer du **nödvändiga behörigheter**

3. För Windows Azure Active Directory-behörigheter:

    1. Välj **Windows Azure Active Directory-behörigheter**.

    2. I **program behörigheter** väljer du läsa katalog data.

    3. Spara behörigheterna.

4. Notera program-ID i avsnittet **Egenskaper** i din webbapp.

### <a name="add-a-secret-key-to-your-app"></a>Lägg till en hemlig nyckel i appen

1. Gå till avsnittet **nycklar** i din webbapp.

2. Ange nyckel beskrivning och välj varaktighet som 1 eller 2 år efter behov.

3. Spara och kopiera värdet för den hemliga nyckeln. **Det här värdet visas inte igen när du lämnar den här sidan.**

Du bör ha följande information från Web App-konfigurationen:

- Program-ID
- Apphemlighet

### <a name="register-the-web-app-in-partner-center"></a>Registrera webb programmet i Partner Center

1. Logga in på [https://partnercenter.microsoft.com](https://partnercenter.microsoft.com) .

2. Välj **instrument panel**, välj sedan **konto inställningar** och sedan **app Management**.

3. I avsnittet **webbapp** väljer du **Registrera befintlig app**.

4. Välj den webbapp som du skapade i Azure Portal.

5. Välj **Registrera din app**.

## <a name="native-apps"></a>Inbyggda appar

Inbyggda appar behöver inte registreras på Partner Center. Men de här apparna måste konfigureras för att ge åtkomst till API: er för partner Center.

>[!NOTE]
>Innan du skapar en intern app i Azure Portal loggar du in på Partner Center med administratörs användarens autentiseringsuppgifter från partner klient organisationen. Detta skapar inställningarna på klienten för att aktivera program behörigheter.

### <a name="create-native-app"></a>Skapa inbyggd app

1. Gå till sidan [Azure Portal-Appregistreringar](https://go.microsoft.com/fwlink/?linkid=2083908) för att registrera din app. Logga in på Azure-portalen med ett arbets- eller skolkonto eller ett personligt Microsoft-konto.

2. Välj **ny registrering**. Mer information finns i [snabb start: registrera ett program med Microsoft Identity Platform](/azure/active-directory/develop/quickstart-register-app).

### <a name="configure-api-access-permissions-for-native-app"></a>Konfigurera API-åtkomst behörigheter för inbyggd app

1. Välj din app. Gå till **Inställningar**.

2. I API-åtkomst väljer du **nödvändiga behörigheter**.

3. Välj **Windows Azure Active Directory-behörigheter**. I **delegerade behörigheter** väljer du följande behörigheter:

    - **Logga in och läsa användarprofil**
    - **Läs katalogdata**
    - **Gå till katalogen som den inloggade användaren**
    - **Läs alla grupper**

4. Spara behörigheterna.

5. Välj **Lägg till** i de **behörigheter som krävs**.

6. Välj **Välj ett API**.

    1. I sökrutan anger du **Microsoft Partner Center** och väljer den i listan resultat.

    2. Välj **Välj**.

7. Välj **Välj behörigheter**.

    1. Välj **åtkomst till Partner Center-skyddsutrustning**.
    
    2. Välj **Välj**.

8. Välj alternativet som anger att du är **klar**.

>[!IMPORTANT]
> Notera program-ID i appens egenskaper.

Du behöver inte registrera interna appar i Partner Center, men den inbyggda appen måste vara administratör godkänd. Notera program-ID för din inbyggda app.
