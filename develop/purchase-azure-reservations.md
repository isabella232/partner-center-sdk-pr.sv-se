---
title: Köp Azure-reservationer
description: 'Du kan köpa Azure-reservationer för en kund med hjälp av Partner Center-API: et via din befintliga Microsoft Azure prenumeration (MS-AZR-0145P) eller Azure-abonnemang.'
ms.date: 11/01/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4c09f65ae5105a74be41a7ec45824e3889217a1c
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768982"
---
# <a name="purchase-azure-reservations"></a>Köp Azure-reservationer

**Gäller för:**

- Partnercenter
- Välkommen till Partnercenter för Microsoft Cloud for US Government

Om du vill köpa en Azure-reservation för en kund som använder Partner Center API måste du ha en befintlig Microsoft Azure-prenumeration (**MS-AZR-0145P**) eller Azure-plan för dem.

> [!NOTE]
> Azure-reservationer är inte tillgängliga på följande marknader:
>
> | Ej tillgängliga marknader            | Ej tillgängliga marknader (fortsatte...) | Ej tillgängliga marknader (fortsatte...)      |
> |--------------------------------|-----------------------------------|------------------------------------------|
> | Åland                  | Grönland                         | Papua Nya Guinea                         |
> | Amerikanska Samoa                 | Grenada                           | Pitcairn                         |
> | Andorra                        | Guadeloupe                        | Réunion                                  |
> | Anguilla                       | Guam                              | Ryska federationen                       |
> | Antarktis                     | Guernsey                          | Saba                                     |
> | Antigua och Barbuda            | Guinea                            | Saint Barthélemy                         |
> | Aruba                          | Guinea-Bissau                     | Saint Lucia                              |
> | Benin                          | Guyana                            | Saint Martin                             |
> | Bhutan                         | Haiti                             | Saint-Pierre och Miquelon                |
> | Bonaire                        | Heard- och McDonaldöarna | Saint Vincent och Grenadinerna         |
> | Bouvetön                  | Isle of Man                       | Samoa                                    |
> | Brasilien                         | Jan Mayen                         | San Marino                               |
> | Brittiska territoriet i Indiska Oceanen | Jersey                            | São Tomé och Príncipe                    |
> | Brittiska Jungfruöarna         | Kiribati                          | Seychellerna                               |
> | Burkina Faso                   | Kosovo                            | Sierra Leone                             |
> | Burundi                        | Laos                              | Sint Eustatius                           |
> | Kambodja                       | Lesotho                           | Sint Maarten                             |
> | Centralafrikanska Republiken       | Liberia                           | Solomonöarna                          |
> | Tchad                           | Madagaskar                        | Somalia                                  |
> | Kina                          | Malawi                            | Sydgeorgien och Sydsandwichöarna |
> | Julön               | Maldiverna                          | Sydsudan                              |
> | Kokosöarna        | Mali                              | Saint Helena, Ascension, Tristan da Cunha   |
> | Komorerna                        | Marshallöarna                  | Surinam                                 |
> | Kongo                          | Martinique                        | Svalbard                                 |
> | Kongo (DR)                    | Mauretanien                        | Swaziland                                |
> | Cooköarna                   | Mayotte                           | Timor-Leste                              |
> | Djibouti                       | Mikronesien                        | Togo                                     |
> | Dominica                       | Montserrat                        | Tokelau                                  |
> | Ekvatorialguinea              | Moçambique                        | Tonga                                    |
> | Eritrea                        | Myanmar                           | Turks- och Caicosöarna                 |
> | Falklandsöarna               | Nauru                             | Tuvalu                                   |
> | Franska Guyana                  | Nya Kaledonien                     | Amerikanska öar                    |
> | Franska Polynesien               | Niger                             | Vanuatu                                  |
> | Franska sydterritorierna    | Niue                              | Vatikanstaten                             |
> | Gabon                          | Norfolkön                    | Wallis och Futuna                        |
> | Gambia                         | Nordmarianerna          | Jemen                                    |
> | Gibraltar                      | Palau                             | &nbsp;                                   |
>

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [partner Center-autentisering](partner-center-authentication.md). Det här scenariot stöder autentisering med både fristående app-och app + användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du se det i [instrument panelen](https://partner.microsoft.com/dashboard)för partner Center. Välj **CSP** på menyn Partner Center, följt av **kunder**. Välj kunden från listan kund och välj sedan **konto**. På sidan kund konto letar du upp **Microsoft ID** i avsnittet **kund konto information** . Microsoft-ID: t är detsamma som kund-ID ( `customer-tenant-id` ).

- Ett prenumerations-ID för en aktiv CSP Azure-prenumeration eller en Azure-plan.

## <a name="how-to-purchase-microsoft-azure-reservations"></a>Så här köper du Microsoft Azure reservationer

När du har identifierat den aktiva CSP Azure-prenumerationen som du vill lägga till en Azure-reservation i använder du följande steg för att köpa den:

1. [Aktivering](#enablement) – registrera en aktiv CSP Azure-prenumeration så att den kan köpa Azure-reservationer.

2. [Identifiering](#discovery) – hitta och välj de Azure reservation-produkter och SKU: er som du vill köpa och kontrol lera deras tillgänglighet.

3. [Order sändning](#order-submission) – skapa en Shopping vagn med objekten i din beställning och skicka den.

4. [Hämta beställnings information](#get-order-details) – granska information om en order, alla beställningar för en kund eller Visa beställningar efter fakturerings cykel typ.

När du har köpt Azure-reservationer visar följande scenarier hur du hanterar deras livs cykel genom att hämta information om dina Azure reservations rättigheter och hur du hämtar balans räkningar, fakturor och faktura sammanfattningar.

- [Livs cykel hantering](#lifecycle-management)
- [Faktura och avstämning](#invoice-and-reconciliation)

## <a name="enablement"></a>Aktivering

Det innebär att du kopplar en befintlig Microsoft Azure-prenumeration (**MS-AZR-0145P**) till en virtuell Azure-instans genom att registrera prenumerationen så att den är aktive rad för Azure-reservationer. Registreringen är en förutsättning för att köpa Azure Reserved VM Instances.

En prenumeration krävs på grund av följande:

1. För att kontrol lera om kunden är berättigad att distribuera resurser och därmed köpa Azure Reserved VM Instances i en region eller inte.

2. För att tillhandahålla kapacitets prioritet för distributioner för en prenumeration. Detta gäller endast för ett enda område Azure Reserved VM Instances med alternativet för **kapacitets prioritet** valt.

När du har identifierat den aktiva prenumeration som du vill lägga till Azure-reservationen i måste du registrera prenumerationen så att den är aktive rad för Azure-reservationer. Information om hur du registrerar en befintlig [prenumerations](subscription-resources.md) resurs så att den är aktive rad för att beställa Azure-reservationer finns i [Registrera en prenumeration](register-a-subscription.md).

När du har registrerat din prenumeration bör du kontrol lera att registrerings processen har slutförts genom att kontrol lera registrerings statusen. Mer information finns i [Hämta status för prenumerations registrering](get-subscription-registration-status.md).

> [!NOTE]
> När du köper Microsoft Azure reservation för en kund med en Azure-plan måste du först registrera Azure-planen. I likhet med en Microsoft Azure **-prenumeration (MS-AZR-0145P**) representeras en Azure-prenumeration av en [prenumerations](subscription-resources.md) resurs för partner Center. Därför kan du använda samma [Registrera en prenumerations](register-a-subscription.md) Metod för att registrera en Azure-plan.

## <a name="discovery"></a>Identifiering

När prenumerationen har Aktiver ATS för att köpa Azure-reservationer är du redo att välja produkter och SKU: er och kontrol lera deras tillgänglighet med hjälp av följande Partner Center API-modeller:

- [Produkt](product-resources.md#product) – en grupperings konstruktion för köpbara-varor eller-tjänster. En produkt som själva är inte ett köpbara-objekt.

- [SKU](product-resources.md#sku) – en köpbara lagerhållnings enhet (SKU) under en produkt. Dessa representerar olika former av produkten.

- [Tillgänglighet](product-resources.md#availability) – en konfiguration där en SKU är tillgänglig för köp (till exempel land, valuta och bransch segment).

Innan du köper en Azure-reservation utför du följande steg:

1. Identifiera och hämta den produkt och SKU som du vill köpa. Du kan göra detta genom att först lista produkterna och SKU: er, eller om du redan känner till ID: n för produkten och SKU: n, väljer du dem.

   - [Hämta en lista över produkter (efter land)](get-a-list-of-products.md)
   - [Hämta en produkt med produkt-ID](get-a-product-by-id.md)
   - [Hämta en lista över SKU:er för en produkt (efter land)](get-a-list-of-skus-for-a-product.md)
   - [Hämta en SKU med SKU-ID](get-a-sku-by-id.md)

2. Kontrol lera inventeringen för en SKU. Det här steget behövs bara för SKU: er som är taggade med en **InventoryCheck** -förutsättning.

   - [Kontrollera lager](check-inventory.md)

3. Hämta [tillgänglighet](product-resources.md#availability) för SKU: [n](product-resources.md#sku). Du behöver **CatalogItemId** av tillgängligheten när du placerar ordern. Använd något av följande API: er för att hämta det här värdet:

   - [Hämta en lista över tillgängliga för en SKU (efter land)](get-a-list-of-availabilities-for-a-sku.md)
   - [Få en tillgänglighet med tillgänglighets-ID: t](get-an-availability-by-id.md)

> [!IMPORTANT]
> Varje Microsoft Azure reservations produkt har olika tillgänglighet för Microsoft Azure (**MS-AZR-0145P**) och Azure-abonnemang. Om du vill [Hämta en lista över produkter (per land)](get-a-list-of-products.md)eller [Hämta en lista över SKU: er för en produkt (per land)](get-a-list-of-skus-for-a-product.md)eller [Hämta en lista över tillgänglighet för en SKU (per land)](get-a-list-of-availabilities-for-a-sku.md) som endast gäller för Azure-plan anger du parametern "reservationScope = AzurePlan".

## <a name="order-submission"></a>Order överföring

Gör så här för att skicka din Azure reservations order:

1. Skapa en vagn som innehåller den samling av katalog objekt som du vill köpa. När du skapar en [varukorg](cart-resources.md)grupperas [vagnens rad objekt](cart-resources.md#cartlineitem) automatiskt utifrån vad som kan köpas tillsammans i samma [ordning](order-resources.md).

   - [Skapa en Shopping vagn](create-a-cart.md)
   - [Uppdatera en Shopping vagn](update-a-cart.md)

2. Kolla in vagnen. Att checka ut en vagns resultat i skapandet av en [order](order-resources.md).

   - [Checka ut vagnen](checkout-a-cart.md)

## <a name="get-order-details"></a>Hämta beställnings information

När du har skapat din reservations ordning för Azure kan du hämta information om en enskild order med order-ID: t eller hämta en lista över beställningar för en kund. Det finns en fördröjning på upp till 15 minuter mellan tiden som en beställning skickas och när den visas i en lista över en kunds beställningar.

- Så här hämtar du information om en enskild order med order-ID: t. Se, [Hämta en order efter ID](get-an-order-by-id.md).

- Så här hämtar du en lista över beställningar för en kund med kund-ID. Se, [Hämta alla kund order](get-all-of-a-customer-s-orders.md).

- För att få en lista över beställningar för en kund med [fakturerings cykel typ](product-resources.md#billingcycletype) , så att du kan visa en lista över Azure reservations order (engångs avgifter) och årliga eller månatliga fakturerade beställningar separat. Se, [Hämta en lista över beställningar efter kund-och fakturerings cykel typ](get-a-list-of-orders-by-customer-and-billing-cycle-type.md).

## <a name="lifecycle-management"></a>Livs cykel hantering

Som en del av att hantera livs cykeln för dina Azure-reservationer i Partner Center kan du hämta information om dina Azure reservations [rättigheter](entitlement-resources.md)och få reservations information med hjälp av reservations order-ID: t. Exempel på hur du gör detta finns i [Hämta rättigheter](get-a-collection-of-entitlements.md).   

## <a name="invoice-and-reconciliation"></a>Faktura och avstämning

Följande scenarier visar hur du program mässigt visar din kunds [fakturor](invoice-resources.md)och hur du får dina konto balanser och sammanfattningar som innehåller engångs avgifter för Azure-reservationer.

### <a name="balance-and-payment"></a>Saldo och betalning

Om du vill hämta aktuellt konto saldo i din standard valuta typ som är en balans mellan både återkommande och engångs kostnad (Azure reservation), se [Hämta ditt aktuella konto saldo](get-the-reseller-s-current-account-balance.md)

### <a name="multi-currency-balance-and-payment"></a>Saldo och betalning för flera valutor

Om du vill hämta ditt aktuella konto saldo och en samling av faktura sammanfattningar som innehåller en faktura sammanfattning med både återkommande och engångs kostnader för var och en av kundens valuta typer, se [Hämta faktura sammanfattningar](get-invoice-summaries.md).

### <a name="invoices"></a>Fakturor

Om du vill hämta en samling fakturor som visar både återkommande och en tids avgift, se [Hämta en samling fakturor](get-a-collection-of-invoices.md). 

### <a name="single-invoice"></a>Enskild faktura

Information om hur du hämtar en speciell faktura med hjälp av faktura-ID finns i [Hämta en faktura efter ID](get-invoice-by-id.md).  

### <a name="reconciliation"></a>Konto

Information om hur du hämtar information om faktura rads objekt (avstämnings rad objekt) för ett angivet faktura-ID finns i [Hämta faktura rads objekt](get-invoiceline-items.md).  

### <a name="download-an-invoice-as-a-pdf"></a>Ladda ned en faktura som en PDF

Information om hur du hämtar ett faktura uttryck i PDF-formulär med hjälp av ett faktura-ID finns i [Hämta en faktura instruktion](get-invoice-statement.md).
