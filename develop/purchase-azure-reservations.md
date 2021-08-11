---
title: Köp Azure-reservationer
description: Du kan köpa Azure-reservationer för en kund med partnercenter-API:et via din befintliga Microsoft Azure-prenumeration (MS-AZR-0145P) eller Azure-plan.
ms.date: 11/01/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ed8aa12117e9f13f84f39c97fc87e2c8844b223bd913cbaebf870d7022959dbd
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997302"
---
# <a name="purchase-azure-reservations"></a>Köp Azure-reservationer

**Gäller för**: Partner Center-| Partnercenter för Microsoft Cloud for US Government

Om du vill köpa en Azure-reservation för en kund med partnercenter-API:et måste du ha en befintlig Microsoft Azure-prenumeration **(MS-AZR-0145P)** eller En Azure-plan för dem.

> [!NOTE]
> Azure-reservationer är inte tillgängliga på följande marknader:
>
> | Otillgängliga marknader            | Otillgängliga marknader (forts....) | Otillgängliga marknader (forts....)      |
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
> | Brittiska territoriet i Indiska Oceanen | Jersey                            | Séo Tomé och Prñncipe                    |
> | Brittiska Jungfruöarna         | Kiribati                          | Seychellerna                               |
> | Burkina Faso                   | Kosovo                            | Sierra Leone                             |
> | Burundi                        | Laos                              | Sint Eustatius                           |
> | Kambodja                       | Lesotho                           | Sint Maarten                             |
> | Centralafrikanska Republiken       | Liberia                           | Solomonöarna                          |
> | Tchad                           | Madagaskar                        | Somalia                                  |
> | Kina                          | Malawi                            | Sydgeorgien och Sydsandwichöarna |
> | Julön               | Maldiverna                          | Sydsudan                              |
> | Kokosöarna        | Mali                              | StDirigering, Ascension, Tristan da Cunha   |
> | Komorerna                        | Marshallöarna                  | Surinam                                 |
> | Kongo                          | Martinique                        | Svalbard                                 |
> | Kongo (DR)                    | Mauretanien                        | Swaziland                                |
> | Cooköarna                   | Mayotte                           | Timor-Leste                              |
> | Djibouti                       | Mikronesien                        | Togo                                     |
> | Dominica                       | Montserrat                        | Tokelau                                  |
> | Ekvatorialguinea              | Moçambique                        | Tonga                                    |
> | Eritrea                        | Myanmar                           | Turks- och Caicosöarna                 |
> | Falklandsöarna               | Nauru                             | Tuvalu                                   |
> | Franska Guyana                  | Nya Kaledonien                     | U.S. Outlying Islands                    |
> | Franska Polynesien               | Niger                             | Vanuatu                                  |
> | Franska sydterritorierna    | Niue                              | Vatikanstaten                             |
> | Gabon                          | Norfolkön                    | Wallis och Spanuna                        |
> | Gambia                         | Nordmarianerna          | Jemen                                    |
> | Gibraltar                      | Palau                             | &nbsp;                                   |
>

## <a name="prerequisites"></a>Förutsättningar

- Autentiseringsuppgifter enligt beskrivningen i [Autentisering i Partnercenter.](partner-center-authentication.md) Det här scenariot stöder autentisering med både fristående app- och app-+användarautentiseringsuppgifter.

- Ett kund-ID ( `customer-tenant-id` ). Om du inte känner till kundens ID kan du leta upp det på instrumentpanelen i [Partnercenter.](https://partner.microsoft.com/dashboard) Välj **CSP** på Menyn i Partnercenter följt av **Kunder.** Välj kunden i kundlistan och välj sedan **Konto.** På kundens kontosida letar du upp **Microsoft-ID:t** i **avsnittet Kundkontoinformation.** Microsoft-ID:t är samma som kund-ID:t ( `customer-tenant-id` ).

- Ett prenumerations-ID för en aktiv CSP Azure-prenumeration eller en Azure-plan.

## <a name="how-to-purchase-microsoft-azure-reservations"></a>Så här köper du Microsoft Azure reservationer

När du har identifierat den aktiva CSP Azure-prenumerationen som du vill lägga till en Azure-reservation till kan du köpa den med hjälp av följande steg:

1. [Aktivera – Registrera](#enablement) en aktiv CSP Azure-prenumeration för att aktivera den för att köpa Azure-reservationer.

2. [Identifiering](#discovery) – Hitta och välj de Azure-reservationsprodukter och lagerhållningsenheter (SKU:er) som du vill köpa och kontrollera deras tillgänglighet.

3. [Skicka order](#order-submission) – Skapa en kundvagn med artiklarna i din beställning och skicka den.

4. [Hämta beställningsinformation](#get-order-details) – Granska informationen om en order, alla order för en kund eller visa beställningar efter faktureringsperiodtyp.

När du har köpt Azure-reservationer visar följande scenarier hur du hanterar deras livscykel genom att hämta information om dina Azure-reservationsrättigheter och hur du hämtar saldoutdrag, fakturor och fakturasammanfattningar.

- [Livscykelhantering](#lifecycle-management)
- [Faktura och avstämning](#invoice-and-reconciliation)

## <a name="enablement"></a>Aktivering

Aktivera innebär att associera en befintlig Microsoft Azure-prenumeration **(MS-AZR-0145P)** till en reserverad vm-instans i Azure genom att registrera prenumerationen så att den aktiveras för Azure-reservationer. Registrering är en förutsättning för att köpa Azure Reserved VM Instances.

En prenumeration krävs för att stödja följande uppgifter:

1. För att kontrollera om kunden är berättigad att distribuera resurser och därmed köpa Azure Reserved VM Instances i en region eller inte.

2. Ange kapacitetsprioritet för distributioner i en prenumeration. Detta gäller endast för enskilda omfång Azure Reserved VM Instances med alternativet **kapacitetsprioritet** valt.

När du har identifierat den aktiva prenumeration som du vill lägga till Azure-reservationen i måste du registrera prenumerationen så att den aktiveras för Azure-reservationer. Information om hur du registrerar [en befintlig](subscription-resources.md) prenumerationsresurs så att den är aktiverad för att beställa Azure-reservationer finns i Registrera [en prenumeration.](register-a-subscription.md)

När du har registrerat din prenumeration bör du bekräfta att registreringen har slutförts genom att kontrollera registreringsstatusen. Information om hur du gör detta finns [i Hämta prenumerationsregistreringsstatus](get-subscription-registration-status.md).

> [!NOTE]
> När du Microsoft Azure en reservation för en kund med en Azure-plan måste du först registrera Azure-planen. Precis som en **Microsoft Azure(MS-AZR-0145P)** representeras en Azure-plan av en prenumerationsresurs [i](subscription-resources.md) Partnercenter. Därför kan du använda samma metod för att [registrera en Azure-prenumeration.](register-a-subscription.md)

## <a name="discovery"></a>Identifiering

När prenumerationen har aktiverats för att köpa Azure-reservationer är du redo att välja produkter och SKU:er och kontrollera deras tillgänglighet med hjälp av följande Partner Center API-modeller:

- [Produkt](product-resources.md#product) – en grupperingskonstruktion för köpbara varor eller tjänster. En produkt i sig är inte ett köpbart objekt.

- [SKU](product-resources.md#sku) – en köpbar SKU under en produkt. De representerar olika former av produkten.

- [Tillgänglighet](product-resources.md#availability) – En konfiguration där en SKU är tillgänglig för inköp (till exempel land, valuta och branschsegment).

Utför följande steg innan du köper en Azure-reservation:

1. Identifiera och hämta den produkt och SKU som du vill köpa. Du kan göra detta genom att först visa produkter och SKU:er, eller välja dem om du redan känner till produkt- och SKU:n.

   - [Hämta en lista över produkter (efter land)](get-a-list-of-products.md)
   - [Hämta en produkt med hjälp av produkt-ID:t](get-a-product-by-id.md)
   - [Hämta en lista över SKU:er för en produkt (efter land)](get-a-list-of-skus-for-a-product.md)
   - [Hämta en SKU med hjälp av SKU-ID:t](get-a-sku-by-id.md)

2. Kontrollera inventeringen för en SKU. Det här steget behövs bara för SKU:er som är taggade med en **InventoryCheck-förutsättning.**

   - [Kontrollera lager](check-inventory.md)

3. Hämta [tillgängligheten](product-resources.md#availability) för [SKU:n](product-resources.md#sku). Du behöver **CatalogItemId för** tillgängligheten när du gör beställningen. Använd något av följande API:er för att hämta det här värdet:

   - [Hämta en lista över tillgängliga för en SKU (efter land)](get-a-list-of-availabilities-for-a-sku.md)
   - [Hämta en tillgänglighet med hjälp av tillgänglighets-ID:t](get-an-availability-by-id.md)

> [!IMPORTANT]
> Varje Microsoft Azure-reservationsprodukt har olika tillgänglighet för prenumerationen Microsoft Azure **(MS-AZR-0145P)** och Azure-prenumerationen. Om du vill hämta en lista över produkter [(efter land)](get-a-list-of-products.md)eller Hämta en lista över SKU:er för en produkt [(efter land)](get-a-list-of-skus-for-a-product.md)eller Hämta en lista över tillgänglighet för en [SKU (efter land)](get-a-list-of-availabilities-for-a-sku.md) som endast gäller för Azure-plan anger du parametern "reservationScope=AzurePlan".

## <a name="order-submission"></a>Skicka order

Gör följande för att skicka in din Azure-reservationsbeställning:

1. Skapa en kundvagn för den samling katalogobjekt som du tänker köpa. När du skapar [en kundvagn](cart-resources.md) [grupperas kundvagnsraderna](cart-resources.md#cartlineitem) automatiskt baserat på vad som kan köpas tillsammans i samma [order.](order-resources.md)

   - [Skapa en kundvagn](create-a-cart.md)
   - [Uppdatera en kundvagn](update-a-cart.md)

2. Kolla in kundvagnen. När du checkar ut en kundvagn skapas en [order.](order-resources.md)

   - [Checka ut kundvagnen](checkout-a-cart.md)

## <a name="get-order-details"></a>Hämta beställningsinformation

När du har skapat din Azure-reservationsbeställning kan du hämta information om en enskild beställning med hjälp av order-ID:t eller hämta en lista över beställningar för en kund. Det finns en fördröjning på upp till 15 minuter från det att en order skickas tills den visas i en lista över en kunds beställningar.

- Hämta information om en enskild order med hjälp av order-ID:t. Se Hämta [en order efter ID.](get-an-order-by-id.md)

- Så här hämtar du en lista över beställningar för en kund med hjälp av kund-ID:t. Se [Hämta alla en kunds beställningar.](get-all-of-a-customer-s-orders.md)

- Om du vill hämta en [](product-resources.md#billingcycletype) lista över beställningar för en kund efter faktureringscykeltyp kan du visa en lista med Azure-reservationsbeställningar (entidsavgifter) och årliga eller månatliga fakturerade beställningar separat. Se Hämta [en lista över beställningar efter kund och faktureringscykel av typen](get-a-list-of-orders-by-customer-and-billing-cycle-type.md).

## <a name="lifecycle-management"></a>Livscykelhantering

Som en del av att hantera livscykeln för dina Azure-reservationer i Partnercenter kan du hämta information om dina Azure-reservationsberättiganden och hämta reservationsinformation med hjälp av reservationsbeställnings-ID:t. [](entitlement-resources.md) Exempel på hur du gör detta finns i [Hämta rättigheter](get-a-collection-of-entitlements.md).   

## <a name="invoice-and-reconciliation"></a>Faktura och avstämning

Följande scenarier visar hur du programmatiskt visar kundens fakturor [och](invoice-resources.md)hämtar dina kontosaldon och sammanfattningar som inkluderar engångsavgifter för Azure-reservationer.

### <a name="balance-and-payment"></a>Saldo och betalning

Information om hur du hämtar aktuellt kontosaldo i din standardvalutatyp som är ett saldo för både återkommande avgifter och engångsavgifter (Azure-reservation) finns i Hämta [ditt aktuella kontosaldo](get-the-reseller-s-current-account-balance.md)

### <a name="multi-currency-balance-and-payment"></a>Saldo och betalning i flera valutor

Information om hur du hämtar ditt aktuella kontosaldo och en samling fakturasammanfattningar som innehåller en fakturasammanfattning med både återkommande och engångsavgifter för var och en av kundens valutatyper finns i [Hämta fakturasammanfattningar](get-invoice-summaries.md).

### <a name="invoices"></a>Fakturor

Information om hur du hämtar en samling fakturor som visar både återkommande och engångsavgifter finns i [Hämta en samling fakturor.](get-a-collection-of-invoices.md) 

### <a name="single-invoice"></a>Enskild faktura

Information om hur du hämtar en specifik faktura med hjälp av [faktura-ID:t finns i Hämta en faktura efter ID.](get-invoice-by-id.md)  

### <a name="reconciliation"></a>Försoning

Information om hur du hämtar en samling fakturaradsobjekt (avstämningsradsobjekt) för ett specifikt faktura-ID finns i [Hämta fakturaradsobjekt.](get-invoiceline-items.md)  

### <a name="download-an-invoice-as-a-pdf"></a>Ladda ned en faktura som pdf

Information om hur du hämtar ett fakturautdrag i PDF-format med ett faktura-ID finns [i Hämta ett fakturautdrag](get-invoice-statement.md).
