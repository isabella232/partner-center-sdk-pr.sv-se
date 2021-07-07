---
title: CSP Indirect-providerfunktioner i sandbox-miljön
description: Indirekta leverantörer kan skapa indirekta återförsäljare i sandbox-miljön i testsyfte.
ms.date: 05/20/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: vinayks-ms
ms.author: vinayks
ms.openlocfilehash: da35dadd4e13247e923259a1cf3a67852f4b9e00
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445909"
---
# <a name="csp-indirect-provider-sandbox-capabilities-for-creating-indirect-reseller-accounts"></a>CSP Indirect provider sandbox-funktioner för att skapa konton för indirekta återförsäljare 

**Lämpliga roller:** Indirekt leverantör

Indirekta CSP-leverantörer kan skapa CSP Indirect Reseller sandbox-konto via sitt eget sandbox-konto på nivå 2 i Partnercenter-portalen.


## <a name="prerequisites"></a>Förutsättningar 

Partner Center Indirect Provider -autentiseringsuppgifter (nivå 2) för sandbox-miljö. Sandbox-scenariot stöder autentisering med både fristående app- och app- och användarautentiseringsuppgifter. 
 

## <a name="sandbox-indirect-provider--create-sandbox-indirect-reseller-using-the-partner-center-user-interface"></a>Sandbox Indirect Provider – Skapa en indirekt Sandbox-återförsäljare med hjälp av Partner Center-användargränssnittet 

 Det här är en funktion för endast sandbox-miljö som gör att indirekta sandbox-leverantörer kan skapa ett sandbox-konto för indirekt återförsäljare via Partner Center-portalen.

Följande scenarier är vad indirekta leverantörer kan göra för indirekta återförsäljare i sandbox-miljön via Partner Center-användargränssnittet: 

1. Indirekta CSP-leverantörer kan skapa ett CSP Indirect Reseller sandbox-konto via sitt eget sandbox-konto på nivå 2 i Partnercenter-portalen.
2. CSP Indirect Resellers kan visa kunden av indirekta leverantörer. 

1. CSP Indirect Resellers kan hantera kundkontot med hjälp av delegerade administratörsbehörigheter.

1. CSP Indirect Providers kan bjuda in indirekta CSP-återförsäljare.
 
1. Indirekta CSP-leverantörer kan ta bort CSP Indirect Reseller sandbox-konto via sitt eget sandbox-konto på nivå 2 i Partnercenter-portalen.

    a.  När sandbox-miljöns indirekta leverantör tar bort relationen med den indirekta Sandbox-återförsäljaren kontrollerar du om den indirekta återförsäljaren har någon annan relation med andra leverantörer. I så fall tas endast relationen med den specifika indirekta providern bort.

    c. Om det är den enda relationen för den indirekta återförsäljaren tas den indirekta återförsäljaren bort.

1. CSP Indirect Providers kan ta bort en CSP Indirect Reseller.

    a. Det här är en funktion för endast sandbox-miljö som gör att indirekta sandbox-leverantörer kan ta bort indirekta Sandbox-återförsäljare.
     
1. Förutsättningar för att ta bort en indirekt Sandbox-återförsäljare:

    1. Pausa prenumerationerna för varje kund hos den indirekta Sandbox-återförsäljaren.

    1. Ta bort alla indirekt återförsäljares kunder.

1. Gräns på fem indirekta Sandbox-återförsäljare per indirekt Sandbox-leverantör. När den indirekta sandbox-återförsäljaren har tagits bort återställs kvoten.

### <a name="pre-requisites"></a>Förutsättningar

- Gräns på fem indirekta Sandbox-återförsäljare per indirekt Sandbox-leverantör. 

- Samma MPN-ID kan användas för att skapa flera sandbox-konton för indirekta återförsäljare om land för MPN-ID och sandbox-land för indirekt återförsäljare är samma. Om du har ett tillgängligt MPN-test-ID kan du använda det eller hämta en lista över MPN-ID:n via [vår Yammer kanal]( https://www.yammer.com/cloudpartnercommunity/#/files/929991598080 ). Om du inte har åtkomst till Yammer ber Yammer dig att begära åtkomst.
 
- Endast 75 kunder tillåts per indirekt sandbox-provider

## <a name="create-csp-indirect-reseller-sandbox-account"></a>Skapa CSP Indirect Reseller Sandbox-konto

1. Logga in på Partner Center via ditt sandbox-konto på nivå 2. 

2. Gå till Indirekta återförsäljare på den vänstra menyn. 

3. Välj knappen **Lägg till sandbox-miljö för** återförsäljare. 

4. Fyll i formuläret för kontoregistrering. Det är självförklarande, men kom ihåg att du skapar ett Sandbox-konto för en indirekt återförsäljare. Det här kontot kommer inte att genomgå någon granskning och aktiveras så snart du är klar med kontoregistreringen.  

5. När kontot har skapats får du autentiseringsuppgifterna för global administratör för sandbox-kontot för indirekt återförsäljare på portalen. Kom ihåg att spara den omedelbart, annars kan du inte logga in som sandbox-miljö för indirekt återförsäljare. 

6. Logga ut och logga in igen på Partner Center med de nya autentiseringsuppgifterna för sandbox-miljön för indirekt återförsäljare. Utforska de funktioner som du kan göra som en indirekt återförsäljare. Några saker är:  

    - Hantera profiler  

    - Hantera användare och roller 

    - Hantera indirekta leverantörer 

    - Hantera CSP Sandbox-kunder 

    - Hantera relationer
    
     
## <a name="sandbox-indirect-provider--delete-sandbox-indirect-reseller-using-the-partner-center-user-interface"></a>Indirekt Sandbox-provider – Ta bort indirekt Sandbox-återförsäljare med hjälp av Partner Center-användargränssnittet

 Det här är en funktion endast för sandbox-miljö som gör det möjligt för indirekta sandbox-leverantörer att ta bort ett befintligt konto för indirekt sandbox-återförsäljare via Partner Center-portalen. 

### <a name="pre-requisites-to-delete-sandbox-indirect-reseller"></a>Förutsättningar för att ta bort indirekt sandbox-återförsäljare:

Ett befintligt CSP Indirect Reseller sandbox-konto som är associerat med ditt CSP Indirect Provider sandbox-konto på nivå 2.  
 

## <a name="delete-csp-indirect-reseller-sandbox-account"></a>Ta CSP Indirect Reseller sandbox-konto

1. Logga in på PartnerCenter med ditt sandbox-konto på nivå 2. 

2. Gå till Indirekta återförsäljare på den vänstra menyn. 

3. Välj länken **Ta bort sandbox-miljö** för återförsäljare bredvid det sandbox-konto för indirekt återförsäljare som du vill ta bort. Sandbox-kontot för indirekt återförsäljare tas bort permanent och kan inte återställas. 

## <a name="api-references"></a>API-referenser

- Skapa indirekt återförsäljare 
- Ta bort indirekt återförsäljare 

 

 