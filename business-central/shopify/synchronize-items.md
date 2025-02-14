---
title: Synkronisera artiklar och lager
description: Ställ in och kör synkronisering av artiklar mellan Shopify och Business Central
ms.date: 06/06/2023
ms.topic: article
ms.service: dynamics365-business-central
ms.search.form: '30116, 30117, 30126, 30127,'
author: AndreiPanko
ms.author: andreipa
ms.reviewer: bholtorf
---

# Synkronisera artiklar och lager

**Artiklar** i [!INCLUDE[prod_short](../includes/prod_short.md)] motsvarar *produkter* i Shopify, som innefattar fysiska varor, digitala nedladdningar, tjänster och presentkort som du säljer. Det finns två huvudsakliga anledningar till att synkronisera artiklarna:

1. Datahantering utförs främst i [!INCLUDE[prod_short](../includes/prod_short.md)]. Du måste exportera alla eller vissa data därifrån till Shopify och göra det synligt. Du kan exportera artikelnamn, beskrivning, bild, priser, tillgänglighet, varianter, leverantörsinformation och streckkod. När du har exporterat kan du granska objekten eller låta dem ha skapats direkt.
2. När en order importeras från Shopify importeras är informationen om artiklarna väsentlig för ytterligare behandling av dokumentet i [!INCLUDE[prod_short](../includes/prod_short.md)].

De två föregående scenarierna är alltid aktiverade.

Ett tredje scenario är att hantera data i Shopify men importera dessa artiklar till [!INCLUDE[prod_short](../includes/prod_short.md)]. Det här scenariot kan vara användbart för datamigreringshändelser när en befintlig online-butik måste vara ansluten till en ny [!INCLUDE[prod_short](../includes/prod_short.md)] miljö.

## Definiera artikelsynkronisering

1. Välj ikonen med ![glödlampan som öppnar funktionen Berätta](../media/ui-search/search_small.png "Berätta vad du vill göra") och ange **Shopify-butik**. Öppna en butik som du vill konfigurera synkronisering av artiklar för.
2. Från fältet **Synkronisera artikel** väljer du det alternativ som efterfrågas.

   Alternativen beskrivs i tabellen nedan.

|Alternativ|Description|
|------|-----------|
|**Tomt**| Produkter importeras tillsammans med import av order. Produkter exporteras till Shopify om användare kör åtgärden **Lägg till artikel** från sidan **Shopify-produkter**. Den här alternativet är standardprocess.|
|**Till Shopify**| Välj det här alternativet om du, efter den första synkroniseringen som utlösts av åtgärden **Lägg till artikel**, planerar att uppdatera produkter manuellt med hjälp av åtgärden **Synkronisera produkt** eller via jobbkön för återkommande uppdateringar. Glöm inte att aktivera fältet **Kan uppdatera Shopify-produkt**. Om den inte är aktive rad är den lika med det **tomma** alternativet (standardprocess). Mer information finns i avsnittet [Exportera artiklar till Shopify](synchronize-items.md#export-items-to-shopify)|
|**Från Shopify**| Välj det här alternativet om du planerar att importera produkter från Shopify i bulk, antingen manuellt med hjälp av åtgärden **Synkronisera produkt** eller via jobbkön för återkommande uppdateringar. Mer information finns i avsnittet [Importera artiklar från Shopify](synchronize-items.md#import-items-from-shopify)|

## Importera artiklar från Shopify

Importera först artiklar från Shopify antingen i bulk eller tillsammans med order för att lägga till dem i tabellerna **Shopify-produkt** och **Shopify-variant**. Mappa sedan importerade produkter och varianter till artiklar och varianter i [!INCLUDE[prod_short](../includes/prod_short.md)]. Hantera processen med följande inställningar:

|Fält|Beskrivning|
|------|-----------|
|**Skapa okända artiklar automatiskt**|När Shopify-produkter och -varianter importeras till [!INCLUDE[prod_short](../includes/prod_short.md)] försöker alltid funktionen [!INCLUDE[prod_short](../includes/prod_short.md)] att hitta matchande poster i artikellistan först. **SKU-mappning** har en inverkan på hur matchningen utförs och skapar nya artiklar och/eller artikelvarianter. Aktivera det här alternativet om du vill skapa en ny artikel eller om det inte finns någon matchande post. Den nya artikeln skapas med hjälp av importerade data och **Kod för artikelmall**. Om det här alternativet inte har aktiverats måste du skapa en artikel manuellt och använda åtgärden **Mappa produkt** från sidan **Shopify-produkter**.|
|**Kod för artikelmall**|Används denna växlingsknapp **Skapa okända artiklar automatiskt**.<br>Välj den mall som ska användas för automatiskt skapade artiklar.|
|**SKU-mappning**|Välj hur du vill använda **SKU**-värdet som importerats från Shopify under mappning och skapande av artikel/variant. Läs mer i avsnittet [Påverkan av Shopify produkt-SKU:er och streckkoder för att mappa och skapa artiklar och varianter i Business Central](synchronize-items.md#effect-of-shopify-product-skus-and-barcodes-on-mapping-and-creating-items-and-variants-in-business-central).|
|**Fältavgränsare för lagerställeenhet**|Använd med **SKU-mappning** anges till alternativet **[Artikelnr + Variantkod](synchronize-items.md#effect-of-shopify-product-skus-and-barcodes-on-mapping-and-creating-items-and-variants-in-business-central)**.<br>Definiera en avgränsare som ska användas för att dela upp SKU.<br>Om du i Shopify skapar en variant med SKU ”1000/001”, skriver du ”/” i fältet **Fältavgränsare för lagerställeenhet** för att få artikelnumret i [!INCLUDE[prod_short](../includes/prod_short.md)] till ”1000” och artikelvariantkoden till ”001”.|
|**Prefix för variant**|Används tillsammans med **SKU-mappning** inställd på **Variantkod** eller **Artikelnr + Variantkod** som en säkerhetsfunktion när lagerställeenheten som kommer från Shopify är tom.<br>Om du vill skapa artikelvarianten i [!INCLUDE[prod_short](../includes/prod_short.md)] automatiskt måste du ange ett värde i **Kod**. Som standard används det värde som anges i fältet för lagerställeenhet som har importerats från Shopify. Om lagerställeenheten är tom genereras koden med det definierade variantprefixet och ”001”.|
|**Shopify kan uppdatera artikel**|Välj det här alternativet om du vill uppdatera artiklar och/eller varianter automatiskt.|

### Påverkan av Shopify produkt-SKU:er och streckkoder för att mappa och skapa artiklar och varianter i Business Central

När produkter importeras från Shopify till tabellerna **Shopify-produkter** och **Shopify-varianter** försöker [!INCLUDE[prod_short](../includes/prod_short.md)] att hitta befintliga poster.

Skillnaden mellan alternativen i fältet **SKU-mappning** beskrivs i följande tabell.

|Alternativ|Inverkan på mappning|Inverkan på skapande|
|------|-----------------|------------------|
|**Tomt**|Fältet SKU används inte i rutinen för artikelmappning.|Ingen inverkan på skapandet av artikeln.<br>Med det här alternativet förhindrar du att varianter skapas. Vid försäljningsorder används endast huvudartikeln. En variant kan fortfarande mappas manuellt på sidan **Shopify-produkt**.|
|**Artikelnr**|Välj om fältet SKU innehåller artikelnumret|Ingen inverkan på skapandet av artikel utan varianter. För artiklar med varianter skapas varje variant som en separat artikel.<br>Om Shopify har en produkt med två varianter och deras SKU:er är ”1000” och ”2000”, [!INCLUDE[prod_short](../includes/prod_short.md)] skapas två artiklar med numren ”1000” och ”2000”.|
|**Variantkod**|Fältet SKU används inte i rutinen för artikelmappning.|Ingen inverkan på skapandet av artikeln. När en artikelvariant skapas används värdet i fältet SKU som kod. Om SKU är tom genereras en kod med hjälp av fältet **Variantprefix**.|
|**Artikelnr + variantkod**|Välj om fältet SKU innehåller ett artikelnr och artikelvariantkod avgränsade med värdet som definieras i fältet **Fältavgränsare för lagerställeenhet**.|När en artikel skapas tilldelas den första delen av värdet i fältet SKU som **nr**. Om SKU-tomt är tom genereras ett artikelnummer med hjälp av nummerserier som definierats i **Kod för artikelmall** eller **Artikelnr** på sidan **Lagerinställningar**.<br>När en artikel skapas använder variantfunktionen den andra delen av värdet i fältet SKU som **kod**. Om SKU-fältet är tomt genereras en kod med hjälp av fältet **Variantprefix**.|
|**Leverantörens artikelnr**|Välj om fältet SKU innehåller artikelnumret för leverantören. I det här fallet används inte **Artikelleverantörsnr.** på sidan **Artikelkort** i stället för **Leverantörens artikelnr.** från **Artikelns leverantörskatalog**. Om posten i *Katalog från artikelleverantör* innehåller en variantkod används denna kod för att mappa Shopify-varianten.|Om en motsvarande leverantör finns i [!INCLUDE[prod_short](../includes/prod_short.md)], används SKU-värdet som **Leverantörens artikelnr.** på sidan **Artikelkort** och som **Artikelreferens** av typen *Leverantör*. <br>Förhindrar att varianter skapas. Det är användbart när du bara vill använda huvudartikeln i försäljningsordern. Du kan fortfarande mappa en variant manuellt på sidan **Shopify-produkt**.|
|**Streckkod**|Välj om fältet SKU innehåller en streckkod. En sökning utförs bland **Artikelreferenser** av typen *Streckkod*. Om posten Artikelreferens som hittas innehåller en variantkod används denna variantkod för att mappa Shopify-varianten.|Ingen inverkan på skapandet av artikeln. <br>Förhindrar att varianter skapas. Det är användbart när du bara vill använda huvudartikeln i försäljningsordern. Du kan fortfarande mappa en variant manuellt på sidan **Shopify-produkt**.|

I följande tabell beskrivs effekten av fältet **Streckkod**.

|Inverkan på mappning|Inverkan på skapande|
|-----------------|------------------|
|En sökning utförs bland **Artikelreferenser** av typen Streckkod efter det värde som anges i fältet **Streckkod** i Shopify. Om posten Artikelreferens som hittas innehåller en variantkod används denna variantkod för att mappa Shopify-varianten.|Streckkoden sparas som **Artikelreferens** för artikel och artikelvariant.|

> [!NOTE]  
> Du kan utlösa mappning för de valda produkterna/varianterna genom att välja **Försök hitta produktmappning** eller alla importerade omappade produkter genom att välja **Försök att hitta mappningar**.

## Exportera artiklar till Shopify

Välj elementen från artikellistan som ska exporteras till Shopify. Använd åtgärden **Lägg till artikel** från sidan **Shopify-produkter** för att lägga till artiklar till listan över Shopify-produkter. 

>[!IMPORTANT]
>Produkten kommer att läggas till i försäljningskanalen för **onlinebutiken** . Du måste publicera produkter till andra försäljnings kanaler, som Shopify POS, från Shopify.

Du hanterar processen att exportera objekt med dessa inställningar:

|Fält|Beskrivning|
|------|-----------|
|**Synkronisera utökad text för artikel**|Välj detta fält för att synkronisera den utökade texten för artikeln. Så som den läggs till i fältet *Beskrivning* kan den innehålla HTML-kod. |
|**Synkronisera artikelattribut**|Välj detta fält om du vill synkronisera artikelattribut. Attribut formateras som tabeller och inkluderas i fältet *Beskrivning* på Shopify.|
|**Marknadsföringstext för synkroniseringsartikel**|Välj det här fältet för att synkronisera marknadsföringstext för objektet. Även om marknadsföringstexten är en sorts beskrivning är den annorlunda än fältet **Beskrivningar**. Fältet **Beskrivning** används vanligtvis som ett kortfattat visningsnamn för att snabbt identifiera produkten. Marknadsföringstexten är å andra sidan en mer omfattande och beskrivande text. Dess syfte är att lägga till marknadsförings- och reklam innehåll. Texten kan sedan publiceras med artikeln i Shopify. Det finns två sätt att skapa marknadsföringstexten. Använd Copilot, som föreslår AI-genererad text för dig, eller börja från början.|
|**Språkkod**|Välj detta fält om du vill ha översatta versionerna för titel, attribut och utökad text.|
|**SKU-mappning**|Välj hur du vill fylla i SKU-fältet i Shopify. Följande alternativ stöds:<br> - **Artikelnr** för att använda artikelnr för både produkter och varianter.<br> - **Artikelnr + Variantkod** för att skapa en SKU genom att sammanfoga värden från två fält. För artiklar utan varianter används endast artikelnummer.<br>- **Artikelleverantörsnr** för att använda det artikelleverantörsnummer som definierats i *Artikelkort* för både produkter och varianter.<br> - **Streckkod** för att använda streckkod av typen **Artikelreferens**. Det här alternativet respekterar varianter.|
|**Fältavgränsare för lagerställeenhet**|Definiera en avgränsare för alternativet **Artikelnr + Variantkod**.|
|**Lager spårat**| Välj hur systemet ska fylla i fältet **Spåra lager** för produkter som exporteras till Shopify. Du kan uppdatera information om tillgänglighet från [!INCLUDE[prod_short](../includes/prod_short.md)] för produkter i Shopify som lagerspårning har aktiverats för. Läs mer i avsnittet [Lager](synchronize-items.md#sync-inventory-to-shopify).|
|**Standardlagerprincip**|Välj *Neka* för att förhindra negativt lager på Shopify-sidan.|
|**Kan uppdatera Shopify-produkter**|Definiera detta fält om [!INCLUDE[prod_short](../includes/prod_short.md)] kan endast kan skapa artiklar eller om det kan uppdatera artiklar också. Välj det här alternativet om du, efter den första synkroniseringen som utlösts av åtgärden **Lägg till artikel**, planerar att uppdatera produkter manuellt med hjälp av åtgärden **Synkronisera produkt** eller via jobbkön för återkommande uppdateringar. Glöm inte att välja **Till Shopify** i fältet **Artikelsynkronisering**.|

### Översikt över fältmappning

|Shopify|Källan när den exporteras från [!INCLUDE[prod_short](../includes/prod_short.md)]|Mål när den importeras till [!INCLUDE[prod_short](../includes/prod_short.md)]|
|------|-----------------|-----------------|
|Status|Enligt fältet **Status för skapade produkter** på **Shopify-butikskortet**. Mer information finns i avsnittet [Ad-hoc-uppdateringar av Shopify-produkter](synchronize-items.md#ad-hoc-updates-of-shopify-products).|Inte använd.|
|Rubrik | **Beskrivning**. Om språkkoden är definierad och motsvarande artikelöversättning finns kommer artikelöversättningen att användas i stället för beskrivning.|**Beskrivning**|
|Description|Kombinerar utökade texter, marknadsföringstexter och attribut om aktiverar motsvarande reglage på Shopify-butikskortet. Respekterar språkkod.|Inte använd.|
|Sidrubrik, SEO|Fast värde: tom. Mer information finns i avsnittet [Ad-hoc-uppdateringar av Shopify-produkter](synchronize-items.md#ad-hoc-updates-of-shopify-products).|Inte använd.|
|Metabeskrivning, SEO|Fast värde: tom. Mer information finns i avsnittet [Ad-hoc-uppdateringar av Shopify-produkter](synchronize-items.md#ad-hoc-updates-of-shopify-products).|Inte använd.|
|Media|**Bild**. Mer information finns i avsnittet [Synkronisera artikelbilder](synchronize-items.md#sync-item-images)|**Bild**|
|Pris|Beräknande av slutkundens pris omfattar inkluderar artikelenhetspris, kundprisgrupp, kundrabattgrupp och valutakod. Mer information finns i avsnittet [Synkronisera priser](synchronize-items.md#sync-prices-with-shopify)|**A-pris**. Priset importeras bara till nyligen skapade objekt men uppdateras inte vid senare synkroniseringar.|
|Jämför med pris|Beräkningen av priset utan rabatt.|Inte använd.|
|Styckkostnad|**Styckkostnad**|**Styckkostnad**. Enhetspriset importeras bara till nyligen skapade objekt men uppdateras inte vid senare synkroniseringar.|
|Lagerställeenhet|Läs mer om detta under **SKU-mappning** i avsnittet [Exportera artiklar till Shopify](synchronize-items.md#export-items-to-shopify).|Läs mer i avsnittet [Påverkan av Shopify produkt-SKU:er och streckkoder för att mappa och skapa artiklar och varianter i Business Central](synchronize-items.md#effect-of-shopify-product-skus-and-barcodes-on-mapping-and-creating-items-and-variants-in-business-central).|
|Streckkod|**Artikelreferenser** av typen Streckkod.|**Artikelreferenser** av typen Streckkod.|
|Spåra antal|Enligt fältet **Lager spårat** på sidan **Shopify-butikskortet**. Läs mer i avsnittet [Lager](synchronize-items.md#sync-inventory-to-shopify). Används endast när du exporterar en produkt för första gången.|Inte använd.|
|Fortsätta sälja när de är slut i lager|Enligt **Standardlagerprincip** på **Shopify-butikskortet**. Används endast när du exporterar en produkt för första gången.|Inte använd.|
|Kontakttyp|**Beskrivning** av **Artikelkategorikod**. Om typen inte har angetts i Shopify läggs den till som en anpassad typ.|**Artikelkategorikod**. Mappning per beskrivning.|
|Leverantör|**Namn** på leverantör från **Leverantörsnr**|**Leverantörsnr**-mappning efter namn.|
|Vikt|**Bruttovikt**.|Inte använd.|
|Momspliktig|Fast värde: aktiverat.|Inte använd.|
|Momskoder|**Momsgruppskod**. Endast relevant för moms. Läs mer i [Ställa in moms](setup-taxes.md).|Inte använd.|

### Taggar

Granska importerade taggar i faktaboxen **Taggar** på sidan **Shopify produkt**. På samma sida, för att redigera taggar, välj åtgärden **Taggar**.
Om alternativet **Till Shopify** har valts i fältet **Synkronisera artikel** exporteras tilldelade taggar till Shopify vid nästa synkronisering.

## Kör atikelsynkronisering

Fullständig eller delvis synkronisering av artiklar kan utföras på många olika sätt.

### Inledande synkronisering av artiklar från Business Central till Shopify

1. Gå till ikonen med ![glödlampan som öppnar funktionen Berätta](../media/ui-search/search_small.png "Berätta för mig vad du vill göra") och ange **Shopify-produkter** och välj relaterad länk.
2. Välj åtgärden **Lägg till artiklar**.
3. Ange koden i fältet **Butikskod**. Om du öppnar fönstret **Shopify-produkt** från sidan **Butikskort** fylls butikskoden i automatiskt.
4. Om du har konfigurerat avbildning och inventering av synkronisering kan du inkludera dem i samma procedur. Det är praktiskt att inkludera dem i samma procedur för demo scenarier eller för att hantera mindre mängder data. 
5. Definiera filter för artiklar efter behov. Du kan till exempel filtrera per artikelnummer. eller artikelkategorikod.
6. Välj **OK**.

De resulterande artiklarna skapas automatiskt i Shopify med priser. Beroende på vilka val du gjorde kan bilder och lagernivåer ingå. Åtgärden kan ta lite tid om ett stort antal artiklar läggs till.

### Synkronisera produkter från Shopify till Business Central

1. Gå till ikonen med ![glödlampan som öppnar funktionen Berätta](../media/ui-search/search_small.png "Berätta för mig vad du vill göra") och ange **Shopify-butik** och välj relaterad länk.
2. Välj den butik som du vill synkronisera artiklar för och öppna sidan **Shopify-butikskort**.
3. Välj åtgärden **Synkronisera produkter**.

Alternativt kan du använda åtgärden **Synkronisera produkter** på sidan **Shopify-produkter** eller söka efter batchjobbet **Synkronisera produkter**.

Du kan schemalägga uppgifter så att de utförs på ett automatiserat sätt. Läs mer i [Schemalägg återkommande uppgifter](background.md#to-schedule-recurring-tasks).

### Ad-hoc-uppdateringar av Shopify-produkter

När posterna uppdateras i tabellen **Shopify-produkt** synkroniseras följande ändringar med Shopify.

Uppdatera:

* **Status** – du kan välja mellan aktiv, arkiverad och utkast.
* **SEO-rubrik**
* **SEO-beskrivning**

Borttagning:

Baserat på värdet i **Åtgärd för borttagna produkter** på sidan **Shopify-butikskortet** uppdateras produkten i Shopify när posten raderas från sidan **Shopify-produkter**.

* **Tom** – ingenting händer. Om det behövs måste användaren utföra den åtgärd som krävs från **Shopify**-admin.
* **Status till Utkast** – statusen för produkten i Shopify anges till *Utkast*.
* **Status till Arkiverad** – produkten arkiveras i Shopify.

## Synkronisera artikelbilder

Synkronisering av bilder kan konfigureras för synkroniserade artiklar. Välj mellan följande alternativ:

* **Inaktiverad** – synkronisering av bilder inaktiveras.
* **Till Shopify** – bilder på artiklar exporteras till Shopify.
* **Från Shopify** – bilder från Shopify importeras till [!INCLUDE[prod_short](../includes/prod_short.md)].

Synkronisering av bilder kan initieras på två sätt som beskrivs nedan.

### Synkronisera produktbilder från sidan Shopify-butik

1. Gå till ikonen med ![glödlampan som öppnar funktionen Berätta](../media/ui-search/search_small.png "Berätta vad du vill göra") och ange **Shopify-butiker** och välj relaterad länk.
2. Välj den butik som du vill synkronisera bilder för och öppna sidan **Shopify-butikskort**.
3. Välj åtgärden **Synkronisera produktbilder**.

### Synkronisera produktbilder från sidan Shopify-produkter

1. Gå till ikonen med ![glödlampan som öppnar funktionen Berätta](../media/ui-search/search_small.png "Berätta vad du vill göra") och ange **Shopify-produkter** och välj relaterad länk.
2. Välj åtgärden **Synkronisera produktbilder**.

### Anmärkningar om bildsynkronisering

* När du exporterar bilder från [!INCLUDE[prod_short](../includes/prod_short.md)] till Shopify läggs de nya bilderna till i Shopify och de gamla bilderna hålls intakta. Om en bild uppdateras i [!INCLUDE[prod_short](../includes/prod_short.md)] måste du ta bort gamla bilder i **Shopify-admin**.
* Bilder som exporteras till Shopify och inte uppfyller villkoren som anges av Shopify importeras inte. Mer information finns i [Typer av produktmedia på help.shopify.com](https://help.shopify.com/en/manual/products/product-media/product-media-types#images)

## Synkronisera priser med Shopify

Du hanterar processen att exportera priser med dessa inställningar:

|Fält|Beskrivning|
|------|-----------|
|**Kundprisgrupp**|Ange priset för en artikel i Shopify. Försäljningspriset för den här kundprisgruppen har tagits. Om ingen grupp anges används priset på artikelkortet.|
|**Kundrabattgrupp**|Bestäm vilken rabatt som ska användas i beräkningen av priset på en artikel i Shopify. Rabatterade priser lagras i fältet **Pris** och det fulla priset lagras i fältet **Jämför pris**.|
|**Tillåt radrabatt**|Anger om radrabatt tillåts när priser beräknas för Shopify. Den här inställningen gäller endast för priser på artikeln. Priser för kundprisgruppen har ingen växling på raderna.|
|**Priser inkl. moms**|Anger om prisberäkningar för Shopify inkluderar moms. Läs mer i [Ställa in moms](setup-taxes.md).|
|**Moms rörelsebokföringsmall**|Anger vilken moms rörelsebokföringsmall som används för att beräkna priserna i Shopify. Det bör vara den grupp som du använder för inrikes kunder. Läs mer i [Ställa in moms](setup-taxes.md).|
|**Valutakod**|Ange en valutakod om din onlinebutik använder en annan valuta än den lokala valutan (BVA). Den angivna valutan måste ha växlingskurser konfigurerade. Lämna fältet tomt om din onlinebeställning använder samma valuta som [!INCLUDEprod_short].|

Priser kan exporteras för synkroniserade artiklar på två sätt som beskrivs nedan.

### Synkronisera priser från sidan Shopify-produkter

1. Gå till ikonen med ![glödlampan som öppnar funktionen Berätta](../media/ui-search/search_small.png "Berätta vad du vill göra") och ange **Shopify-produkter** och välj relaterad länk.
2. Välj åtgärden **Synkronisera priser med Shopify**.

### Anmärkningar om prisberäkning

* När du fastställer ett pris använder [!INCLUDE[prod_short](../includes/prod_short.md)] logiken ”Lägsta pris”. Den lägsta pris logiken ignorerar emellertid det a-pris som har definierats på artikelkortet om ett pris har definierats i prisgruppen. Detta gäller även om a-priset från artikelns kortpris inte är lägre.
* För att beräkna priser skapar kopplingen en tillfällig försäljningsoffert för artikeln med antal 1 och använder logik för standard prisberäkning. Endast priser och rabatter som gäller för antal 1 används. Du kan inte exportera olika priser eller rabatter baserat på kvantitet.

## Synkronisera lager med Shopify

Lagersynkronisering kan konfigureras för artiklar som redan synkroniserats. Två villkor måste uppfyllas:

1. Lagerspårning måste aktiveras för en produkt i Shopify. Om artiklar exporteras till Shopify bör du överväga att aktivera reglaget **Lager spårat** på sidan **Shopify-butik**. Mer information finns i avsnittet [Exportera artiklar till Shopify](synchronize-items.md#export-items-to-shopify)
2. Lagersynkronisering måste aktiveras för **Shopify-platser**.

### Aktivera lagersynkronisering

1. Gå till ikonen med ![glödlampan som öppnar funktionen Berätta](../media/ui-search/search_small.png "Berätta vad du vill göra") och ange **Shopify-butik** och välj relaterad länk.
2. Välj den butik som du vill synkronisera lager för och öppna sidan **Shopify-butikskort**.
3. Välj åtgärden **Platser** för att öppna **Shopify-butiksplatser**.
4. Välj åtgärden **Hämta Shopify-platser** för att importera alla platser som har definierats i Shopify. Du hittar dem i inställningarna för [**Platser**](https://www.shopify.com/admin/settings/locations) under **Shopify-admin**.
5. I fältet **Platsfilter** lägger du till platser om du endast vill inkludera lager från specifika platser. Du kan ange *ÖST|VÄST*, så att lager från enbart dessa två platser är tillgängligt för försäljning via onlinebutiken.
6. Välj den lager beräkningsmetod som ska användas för de valda Shopify lagerställena.

Du kan starta lagersynkronisering på de två sätt som beskrivs nedan.

### Synkronisera lager från sidan Shopify-butik

1. Gå till ikonen med ![glödlampan som öppnar funktionen Berätta](../media/ui-search/search_small.png "Berätta vad du vill göra") och ange **Shopify-butiker** och välj relaterad länk.
2. Välj den butik som du vill synkronisera lager för och öppna sidan **Shopify-butikskort**.
3. Välj åtgärden **Synkronisera lager**.

### Synkronisera lager från sidan Shopify-produkter

1. Gå till ikonen med ![glödlampan som öppnar funktionen Berätta](../media/ui-search/search_small.png "Berätta vad du vill göra") och ange **Shopify-produkter** och välj relaterad länk.
2. Välj åtgärden **Synkronisera lager**.

### Lageranmärkningar

* Standardmetoden för lagerberäkning har **projekterats tillgängligt saldo t.o.m. datum**. Med utökning kan du lägga till fler alternativ. Om du vill veta mer om utökning, gå till [exempel](https://github.com/microsoft/ALAppExtensions/blob/main/Apps/W1/Shopify/extensibility_examples.md). 
* Du kan inspektera lagerinformationen från Shopify på sidan **Faktabox om Shopify-lager**. I den här faktaboxen får du en översikt över Shopify-lagret och det senast beräknade lagret i [!INCLUDE[prod_short](../includes/prod_short.md)]. Det finns en post per plats.
* Om lagerinformationen i Shopify skiljer sig från **Prognostiserat tillgängligt saldo** i [!INCLUDE[prod_short](../includes/prod_short.md)] uppdateras lagret i Shopify.
* När du lägger till ett nytt lagerställe i Shopify måste du också lägga till lagerposter för det. Shopify gör det inte automatiskt för befintliga produkter och varianter och anslutningsprogram kommer inte att synkronisera lagernivåer för sådana artiklar på det nya lagerstället. Om du vill ha mer information går du till [tilldela lager till lagerställen](https://help.shopify.com/manual/locations/assigning-inventory-to-locations).

#### Exempel på beräkning av planerad disponibel balans

Det finns 10 delar av artikeln som finns tillgängliga i handen och två utestående försäljningsorder. En för måndagen med kvantiteten *en* och en för torsdag med kvantitet *två*. Beroende på när du synkroniserar lager, uppdateras lager nivån i Shopify med olika antal:

|När synkronisering av lagret körs|Värde som används för att uppdatera lagernivå|Kommentar|
|------|-----------------|-----------------|
|Tisdag|9|Lager 10 minus försäljningsorder som levereras till måndag|
|Fredag|7|Lager 10 minus både försäljningsorder|

## Se även

[Kom igång med kopplingen för Shopify](get-started.md)  
