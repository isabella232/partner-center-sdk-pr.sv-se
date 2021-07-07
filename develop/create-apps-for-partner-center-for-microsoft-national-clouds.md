---
title: Registrera appinformation för Partner Center for Microsoft National Cloud
description: Lär dig hur och varför apputvecklare för Partner Center for Microsoft National Cloud måste registrera information om sin app med Azure AD via Azure Portal.
MS-HAID:
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_cloud\_germany
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_national\_clouds
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 93d46a17bc26e9586e5e773bdf934653a571367f
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973459"
---
# <a name="register-app-details-for-partner-center-for-microsoft-national-cloud-through-the-azure-portal"></a>Registrera appinformation för Partner Center for Microsoft National Cloud via Azure Portal

**Gäller för:** Partner Center for Microsoft Cloud Germany | Partnercenter för Microsoft Cloud for US Government

Utvecklare måste registrera information om sin app med Azure AD via Azure Portal. Detta säkerställer att endast angivna appar kan ansluta till partner- och kunddata.

För Partnercenter för Microsoft Cloud for US Government måste du för närvarande hantera appar via PowerShell. Mer information finns i Azure PowerShell [referensdokumentationen](/powershell/module/Azuread/#applications).

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Tänk på följande ytterligare krav när du skapar en app för Partner center för Microsoft Cloud Tyskland eller Partnercenter för Microsoft Cloud for US Government.

## <a name="web-apps"></a>Webbappar

För webbappar använder du följande procedurer för att registrera ditt program-ID.

### <a name="create-or-update-web-app"></a>Skapa eller uppdatera webbapp

1. Gå till [sidan Azure Portal – Appregistreringar](https://go.microsoft.com/fwlink/?linkid=2083908) för att registrera din app. Logga in på Azure-portalen med ett arbets- eller skolkonto eller ett personligt Microsoft-konto.

2. Välj **Ny registrering.** Mer information finns i [Snabbstart: Registrera ett program med Microsofts identitetsplattform](/azure/active-directory/develop/quickstart-register-app).

### <a name="configure-api-access-permissions-for-web-app"></a>Konfigurera API-åtkomstbehörigheter för webbapp

1. Välj din app. Gå **till Inställningar** av webbappen.

2. I **avsnittet API-åtkomst** väljer du **Nödvändiga behörigheter**

3. För Windows Azure Active Directory-behörigheter:

    1. Välj **Windows Azure Active Directory behörigheter**.

    2. I **Programbehörigheter** väljer du Läsa katalogdata.

    3. Spara behörigheterna.

4. Observera program-ID:t **i avsnittet** Egenskaper för webbappen.

### <a name="add-a-secret-key-to-your-app"></a>Lägga till en hemlig nyckel i din app

1. Gå till **avsnittet Nycklar** i webbappen.

2. Ange nyckelbeskrivning och välj varaktighet som 1 eller 2 år, efter behov.

3. Spara och kopiera värdet för den hemliga nyckeln. **Det här värdet visas inte igen när du lämnar den här sidan.**

Du bör ha följande information från webbappskonfigurationen:

- Program-ID:t
- Apphemlighet

### <a name="register-the-web-app-in-partner-center"></a>Registrera webbappen i Partnercenter

1. Logga in på [https://partnercenter.microsoft.com](https://partnercenter.microsoft.com).

2. Välj **Instrumentpanel,** välj **sedan Konto Inställningar** och välj sedan **Apphantering.**

3. I avsnittet **Webbapp** väljer du **Registrera befintlig app.**

4. Välj den webbapp som du skapade Azure Portal.

5. Välj **Registrera din app.**

## <a name="native-apps"></a>Inbyggda appar

Inbyggda appar behöver inte vara registrerade i Partnercenter. Men de här apparna måste konfigureras för att ge åtkomst till Partner Center-API:er.

>[!NOTE]
>Innan du skapar en inbyggd app i Azure Portal loggar du in på Partnercenter med autentiseringsuppgifterna för administratörsanvändaren från partnerklientorganisationen. Detta skapar inställningarna för klientorganisationen för att aktivera appbehörigheter.

### <a name="create-native-app"></a>Skapa inbyggd app

1. Gå till [sidan Azure Portal – Appregistreringar](https://go.microsoft.com/fwlink/?linkid=2083908) för att registrera din app. Logga in på Azure-portalen med ett arbets- eller skolkonto eller ett personligt Microsoft-konto.

2. Välj **Ny registrering.** Mer information finns i [Snabbstart: Registrera ett program med Microsofts identitetsplattform](/azure/active-directory/develop/quickstart-register-app).

### <a name="configure-api-access-permissions-for-native-app"></a>Konfigurera API-åtkomstbehörigheter för inbyggd app

1. Välj din app. Gå till **Inställningar**.

2. I API-åtkomst väljer du **Nödvändiga behörigheter.**

3. Välj **Windows Azure Active Directory behörigheter**. I **Delegerade behörigheter** väljer du följande behörigheter:

    - **Logga in och läsa användarprofil**
    - **Läs katalogdata**
    - **Gå till katalogen som den inloggade användaren**
    - **Läs alla grupper**

4. Spara behörigheterna.

5. Välj **Lägg till** i Nödvändiga **behörigheter.**

6. Välj **Välj ett API**.

    1. I sökrutan anger du **Microsoft Partner Center** och väljer det i resultatlistan.

    2. Välj **Välj**.

7. Välj **Välj behörigheter**.

    1. Välj **Access Partner Center PPE.**
    
    2. Välj **Välj**.

8. Välj alternativet som anger att du är **klar**.

>[!IMPORTANT]
> Observera program-ID:t i Egenskaper för din app.

Du behöver inte registrera inbyggda appar i Partnercenter, men den interna appen måste godkännas av administratören. Observera program-ID:t för din interna app.
