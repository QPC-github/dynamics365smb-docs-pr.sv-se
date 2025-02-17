---
title: Genomgång – Planera leveranser automatiskt
description: I den här genomgången visar vi hur du använder leveransplaneringssystemet för att automatiskt planera alla inköps- och produktionsorder för olika försäljningsorder.
author: SorenGP
ms.topic: conceptual
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.search.keywords: null
ms.date: 06/24/2021
ms.author: edupont
---
# <a name="walkthrough-planning-supplies-automatically" />Genomgång: Planera leveranser automatiskt

<!-- [!INCLUDE[complete_sample_data](includes/complete_sample_data.md)]   -->

Begreppen "kör planering" eller "kör nettobehov" syftar på beräkningen av den primära produktionsplanen (MPS) och materialbehovsplanen (MRP), baserat på faktiska behov och behovsprognoser.  

-   Nettobehov är beräkningen av en produktionsplan baserat på faktiskt behov och efterfrågeprognosen. Beräkningen av produktionsprogrammet används för slutartiklar som har en prognosrad eller en försäljningsorderrad. Dessa artiklar kallas för "nettobehovsartiklar" och identifieras dynamiskt när beräkningen startar.  
-   Produktionsplan är beräkningen av materialbehov baserat på faktiskt behov av komponenter och efterfrågeprognosen på komponentnivå. Produktionsplanen beräknas endast för artiklar som inte är nettobehovsartiklar. Det övergripande syftet med produktionsplanen är att tillhandahålla tidsfasade formella planer, utifrån artikel, för att leverera rätt artikel i rätt tid, på rätt plats och i rätt antal.  

 De planeringsalgoritmer som används för både nettobehov och produktionsplanen är identiska. Planeringsalgoritmerna använder nettoberäkning, återanvändning av befintliga leveransorder samt åtgärdsmeddelanden. Planeringssystemprocessen används för att söka efter vad som behövs eller kommer att behövas (efterfrågan) och vad som finns i lager eller förväntas finnas i lager (tillgång). När de här kvantiteterna nettoberäknas mot varandra visas åtgärdsmeddelanden i planeringsförslaget. Åtgärdsmeddelanden är förslag på att skapa en ny leveransorder, att ändra en leveransorder (kvantitet eller datum) eller att annullera en befintlig leveransorder. Leveransorder kan vara produktionsorder, inköpsorder eller överföringsorder. Mer information finns i [Designdetaljer: Leveransplanering](design-details-supply-planning.md)  

 Planeringsresultatet beräknas delvis utifrån behovs- och utbudsuppsättningarna i databasen och delvis utifrån inställningarna för lagerställeenhetskort eller artikelkort, produktstrukturer och verksamhetsföljder.  

## <a name="about-this-walkthrough" />Om den här genomgången
 I den här genomgången visar vi hur du använder leveransplaneringssystemet för att automatiskt planera alla inköps- och produktionsorder som krävs för att producera 15 touringcyklar som behövs för att uppfylla olika försäljningsorder. För att genomgången ska bli så tydlig och realistisk som möjligt har antalet planeringsrader begränsats genom att filtrera bort alla övriga behovs- och leveransuppsättningar i demoföretaget CRONUS, förutom försäljningsbehovet vid försäljningsställe ÖST.  

 I den här genomgången tas följande aktiviteter upp:  

-   Skapa en försäljningsorder och beräkna en fullständig leveransplanering.  
-   Visa planeringsparametrar och orderspårningsposter bakom planeringsraderna.  
-   Automatiskt skapa föreslagna leveransorder.  
-   Skapa nytt försäljningsbehov och planera om därefter.  

## <a name="roles" />Roller

-   Produktionsplanerare  
-   Inköpsagent  

## <a name="prerequisites" />Förutsättningar
 För att kunna utföra den här genomgången behöver du:  

-   Demoföretaget CRONUS Sverige AB.  
-   Ändra olika inställningsvärden för artiklar genom att följa stegen i avsnittet “Förbereda exempeldata“ senare i den här genomgången.  

## <a name="story" />Situation
 Kunden Fotograferna AB beställer fem touringcyklar för utleverans 2021-02-05 (5 februari).  

 Eduardo, produktionsplaneraren, utför den rutinmässiga leveransplaneringen till den första veckan i februari 2021. Eduardo filtrerar på det egna lagerstället, ÖST, och anger ett planeringsintervall på arbetsdatumet (2021-01-23) till 2021-02-07 innan han beräknar en första leveransplanering.  

 Det enda behovet den veckan är för Fotograferna AB:s försäljningsorder. Eduardo ser att ingen av planeringsraderna har någon varning och han fortsätter att skapa leveransorder utan ändringar för de föreslagna planeringsraderna.  

 Nästa dag, innan någon av de ursprungliga leveransordrarna har påbörjats eller bokförts blir Eduardo underrättad om att en annan kund har beställt tio touringcyklar för utleverans 2021-02-12. Eduardo gör en ny beräkning för att justera leveransplaneringen för att få med behovsändringen. Omberäkningen resulterar i en nettoändringsplanering som innehåller förslag på ändringar av både datum och kvantitet för en del av de leveransorder som skapades vid den första körningen.  

 Under de olika planeringsstegen slår Eduardo upp de order som berörs och använder funktionen Orderspårning för att kontrollera vilka behov som täcks av vilka leveranser.  

## <a name="preparing-sample-data" />Förbereda exempeldata
 Skapa lagerställeenheter för touringcykeln och ett val av dess komponenter, artikelnumren 1001 till 1300. (Vissa komponenter exkluderas för att förenkla procedurer.) Justera planeringsparametrarna för de valda komponenterna för att ge mer transparenta planeringsresultat.  

### <a name="to-create-stockkeeping-units" />Så här skapar du lagerställeenheter

1.  Öppna artikelkort för artikel 1001, touringcykel.  
2.  Välj åtgärden **Skapa lagerställeenhet**.  
3.  På sidan **Skapa lagerställeenhet** lämnar du alla alternativ och filter oförändrade och klickar sedan på **OK**.  
4.  Upprepa steg 1 till 3 för alla artiklar i nummerintervallet 1100 till 1300.  

### <a name="to-change-selected-planning-parameters" />Så hör kan du ändra de valda planeringsparametrarna

1.  Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta för mig vad du vill göra") anger du **lagerställeenheter** och väljer sedan relaterad länk.  
2.  Öppna det enhetskortet för lagerställe ÖST för artikel 1100, framhjul.  
3.  Fyll i fälten på snabbfliken **Planering** enligt beskrivningen i följande tabell.  

    |Partiformningsmetod|Säkerhetslager|Partiackumuleringsperiod|Omplaneringsperiod|  
    |-------------------------------------------|-----------------------------------------------|-------------------------------------------------|---------------------------------------------|  
    |Parti-för-parti|Tomt|2V|2V|  

4.  Upprepa steg 2 och 3 för alla lagerställeenheter i nummerintervallet 1100 till 1300.  

 Nu är du klar med att förbereda exempeldata för genomgången.  

## <a name="creating-a-regenerative-supply-plan" />Skapa en fullständig leveransplanering
 När en ny försäljningsorder på fem touringcyklar inkommer börjar Ricardo med planeringsprocessen genom att ange inställningar, filter och planeringsintervall för att exkludera alla övriga behov utom de för den första veckan i februari på lagerställe ÖST. Ricardo börjar med att beräkna ett produktionsprogram inom filtren, och fortsätter sedan med att beräkna en fullständig leveransplanering för alla behov på lägre nivå (nettobehov).  

### <a name="to-create-the-sales-order" />Så här skapar du försäljningsreturordern

1.  Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta för mig vad du vill göra") anger du **försäljningsorder** och väljer sedan relaterad länk.  
2.  Välj åtgärden **Ny**.  
3.  På sidan **Försäljningsorder** kan du fylla i fälten enligt beskrivningen i följande tabell.  

    |Förs.kundnamn|Utleveransdatum|Artikelnr|Lagerställe|Antal|  
    |----------------------------|-------------------|--------------|--------------|--------------|  
    |Fotograferna AB|02-05-2014|1001|ÖST|5|  

4.  Acceptera tillgänglighetsvarningen och klicka på **Ja** för att registrera det nya efterfrågade antalet.  

### <a name="to-create-a-regenerative-plan-to-fulfill-demand-at-location-east" />Så här skapar du en fullständig plan för att tillfredsställa behovet vid lagerställe ÖST

1.  Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta vad du vill göra") anger du **planeringsförslag** och väljer sedan relaterad länk.  
2.  Välj åtgärden **Beräkna fullständig plan**.  
3.  På sidan **Skapa inköpsförslag – planeringsförslag** fyll i fälten enligt beskrivningen i följande tabell.  

    |Skapa inköpsförslag|Startdatum|Slutdatum|Visa resultat:|Begränsa totaler till|  
    |--------------------|-------------------|-----------------|-------------------|---------------------|  
    |**MPS** = Ja<br /><br /> **MRP** = Nej|01-23-2021<br /><br /> (arbetsdatum)|02-07-2021|1001..1300|Lagerställefilter = ÖST|  

4.  Klicka på **OK** för att starta planeringskörningen.  

     En planeringsrad skapas med kalkylarket att en planerad produktionsorder ska skapas för att producera de tio touringcyklarna, artikel 1001, senast den 2021-02-05, som är försäljningsorderns utleveransdatum.  

     I nästa steg verifierar du att den här planeringsraden hör till Fotograferna AB:s försäljningsorder genom att använda funktionen **Orderspårning**, som dynamiskt länkar behov till deras planerade leveranser.  

5.  Markera nya planeringsraden och klicka sedan på **Orderspårning**.  
6.  På sidan **Orderspårning** väljer du åtgärden **Visa**.  

     Försäljningsordern för de fem touringcyklarna till kund nummer 10000 2021-02-05 visas.  

7.  Stäng sidorna **Förs.order** och **Orderspårning**.  

### <a name="to-calculate-mrp-to-include-underlying-component-needs" />Beräkna nettobehov för att ta med underliggande komponentbehov

1.  Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta vad du vill göra") anger du **planeringsförslag** och väljer sedan relaterad länk.  
2.  Välj åtgärden **Beräkna fullständig plan**.  
3.  På sidan **Skapa inköpsförslag – planeringsförslag** fyll i fälten enligt beskrivningen i följande tabell.  

    |Beräkna|Startdatum|Slutdatum|Visa resultat:|Begränsa totaler till:|  
    |---------------|-------------------|-----------------|-------------------|----------------------|  
    |**MPS** = Ja<br /><br /> **MRP** = Ja|01-23-2021|02-07-2021|1001..1300|Lagerställefilter = ÖST|  

4.  Klicka på **OK** för att starta planeringskörningen.  

     Totalt 14 planeringsrader skapas med förslag på leveransorder för alla de behov som försäljningsordern för touringcyklarna vid lagerställe ÖST representerar.  

## <a name="analyzing-the-planning-result" />Analysera planeringsresultatet
 Eduardo vill analysera de föreslagna kvantiteterna och visar detaljer på valda planeringsrader för att visa orderspårningsposter och planeringsparametrar.  

 På sidan **Planeringsförslag** observera att kolumnen **Förfallodatum** i planeringsförslaget har planerats baklänges, från försäljningsorderns förfallodatum, 2021-02-05. Tidslinjen börjar på den översta planeringsraden med produktionsordern för att producera de färdiga touringcyklarna. Tidslinjen slutar vid nedersta planeringsraden med inköpsordern för en av artiklarna på lägsta nivå, 1255, Sockel baksida, som förfaller 2021-01-30. Som planeringsraden för artikeln 1251, axelbakhjulet, representerar raden en inköpsorder för komponenter som förfallit på startdatumet för den producerade överordnade undermonteringsartikeln 1250, som i sin tur är förfallet 02-03-2014. Genom hela kalkylarket kan du se att alla underliggande artiklar har förfallit på startdatumet för sina överordnade artiklar.  

 Planeringsraden för artikeln 1300, Kedjemont, föreslår tio enheter. Detta avviker från de fem styckena som vi förväntas behöva för att uppfylla försäljningsorder. Fortsätt med att visa dessa beställningsspårningposter.  

### <a name="to-view-order-tracking-entries-for-item-1300" />Visa orderspårningsposter för artikel 1300

1.  Markera planeringsraden för artikeln 1300 och klicka sedan på **Orderspårning**.  

     De två raderna på sidan **Orderspårning** visar att fem enheter kan spåras från planeringsraden (den första orderspårningsraden) till försäljningsorder 1001 (andra orderspårningsraden). De sista fem enheter som föreslås på planeringsraden är inte kopplade till någon dokumentrad, utan till en planeringsparameter, en prognostransaktion eller en avropsorderpost. De här ospårade kvantiteterna summeras i fältet **Antal, inte spårade** längst upp på sidan **Orderspårning**.  

2.  Välj fältet **ej spårat antal**.  

     På sidan **Planeringselement, inte spårat** visas att artikeln 1300 använder en planeringsparameter, Min. partistorlek, som är 10,00. Därför står planeringsraden för tio enheter totalt, där endast fem kan spåras till ett behov. De sista fem enheterna är en ospårad kvantitet som tillfredsställer planeringsparametern. Fortsätt för att granska planeringsparametrar.  

### <a name="to-check-the-planning-parameter" />Så här kan du kontrollera planeringsparametern

1.  På sidan **Ej spårade planeringselement** markerar du orderspårningsraden för artikel 1300.  
2.  Välj fältet **Artikelnr** och välj sedan **Avancerat**.  
3.  På sidan **artikellista** väljer du åtgärden **Lagerställeenheter**.  
4.  På sidan **Lagerställeenhetslista** öppnar du enhetskortet för lagerställe ÖST.  
5.  Expandera snabbfliken **Planering** och lägg märke till att fältet **Min. partistorlek** har värdet 10.  
6.  Stäng alla sidor utom sidan **Planeringsförslag**.  

### <a name="to-view-more-order-tracking-entries" />Visa fler orderspårningstransaktioner

1.  Markera planeringsraden för artikeln 1110 rim och klicka sedan på **Orderspårning**.  

     Sidan **Orderspårning** visar att fem fälgar behövs för varje produktionsorder för fram- och bakhjul respektive.  

     Samma orderspårning avser planeringsraderna för artiklarna 1120 och 1160 1170. För artikel 1120 fältet **kvantitet per** på produktionsstrukturen av varje hjul är 50 datorer, vilka leder till ett behov av totalt 100.  

     Planeringsraden för artikeln 1150 för sex stycken verkar ojämn. Fortsätt med att analysera.  

2.  Markera planeringsraden för artikeln 1150 och klicka sedan på **Orderspårning**.  

     Sidan **Orderspårning** visar att fem enheter spåras till framhjulet, och en enhet är inte spårats. Fortsätt med att visa det ospårade antalet.  

3.  Välj fältet **ej spårat antal**.  

     Sidan **ej spårade planeringselement** visar att artikeln 1150 använder planeringsparametern Partistorleksmultipel, på 2,00, vilket anger att när artikeln beställdes, måste det vara i kvantiteter som är delbara med 2. Den närmaste kvantiteten för 5 som är delbar med 2 blir 6.  

     Samma beställningsspårning gäller för planeringsraderna för de främre navkomponenterna, artiklarna 1151 och 1155, förutom att varje behov multipliceras med kassationsprocenten som har angetts för artikeln 1150 i fältet **Kassationsprocent** på kortet.  

 Nu är du klar med analysen av den ursprungliga leveransplaneringen. Lägg märke till att kryssrutan **Acceptera åtgärdsmeddelande** är markerad på alla planeringsrader vilket visar att de är klara att omvandlas till leveransorder.  

## <a name="carrying-out-action-messages" />Verkställa åtgärdsmeddelanden
 Nästa steg för Eduardo blir att omvandla de föreslagna planeringsraderna till leveransorder genom att använda funktionen **Skapa order från planering**.  

### <a name="to-automatically-create-the-suggested-supply-orders" />Så här skapar du de föreslagna leveransordrarna automatiskt

1.  Markera kryssrutan **Acceptera åtgärdsmeddelande** på planeringsraderna med en varning av typen undantag.  
2.  Välj den **Verkställ åtgärdsmeddelande** åtgärd.  
3.  På sidan **Skapa order från planering** fyller du i följande fält.  

    |Produktionsorder|Inköpsorder|Överföringsorder|  
    |----------------------|--------------------|--------------------|  
    |Fast planerad|Skapa inköpsorder|Skapa överföringsorder|  

4.  Klicka på **OK** för att skapa alla de föreslagna leveransordrarna automatiskt.  
5.  Stäng den tomma sidan **Planeringsförslag**.  

 Du är nu klar med den första beräkningen, analysen och skapandet av en leveransplanering för behovet vid lagerställe ÖST under första veckan i februari. I följande avsnitt beställer en annan kund tio touringcyklar, vilket tvingar Eduardo att planera om.  

## <a name="creating-a-net-change-plan" />Skapa en nettoförändringsplanering
 Nästa dag, innan någon leveransorder har påbörjats eller bokförts, anländer en ny försäljningsorder från Libros AB för tio touringcyklar med leveransdatum 2021-02-12. Eduardo blir underrättad om det här nya behovet och fortsätter genom att planera om för att justera den aktuella leveransplaneringen. Eduardo använder funktionen Nettoförändringsplanering för att beräkna endast de förändringar som görs i behovet eller leveransen sedan den senaste planeringskörningen. Dessutom utökar Eduardo planeringsperioden till 2021-02-14 så att den även omfattar den nya försäljningsefterfrågan den 2014-02-12.  

 I planeringssystemet beräknas det bästa sättet att täcka behovet för de här två identiska produkterna, t. ex. att slå samman vissa inköps- och produktionsorder, omplanera andra order och skapa nya order vid behov.  

### <a name="to-create-the-new-sales-demand-and-replan-accordingly" />Så här skapar du nytt försäljningsbehov och planerar om därefter

1.  Välj åtgärden **Ny**.  
2.  På sidan **Försäljningsorder** kan du fylla i fälten enligt beskrivningen i följande tabell.  

    |Förs.kundnamn|Utleveransdatum|Artikelnr|Lagerställe|Antal|  
    |----------------------------|-------------------|--------------|--------------|--------------|  
    |Libros S.A.|02-12-2021|1001|ÖST|10|  

3.  Acceptera tillgänglighetsvarningen och klicka på **Ja** för att registrera det efterfrågade antalet.  
4.  Fortsätter genom att planera om genom att justera den nuvarande leveransplaneringen.  
5.  Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta vad du vill göra") anger du **planeringsförslag** och väljer sedan relaterad länk.  
6.  Välj åtgärden **Beräkna nettoförändringsplan**.  
7.  På sidan **Skapa inköpsförslag – planeringsförslag** fyll i fälten enligt beskrivningen i följande tabell.  

    |Skapa inköpsförslag|Startdatum|Slutdatum|Visa resultat:|Begränsa totaler till|  
    |--------------------|-------------------|-----------------|-------------------|---------------------|  
    |**MPS** = Ja<br /><br /> **MRP** = Ja|01-23-2021|02-14-2021|1001..1300|Lagerställefilter = ÖST|  

8.  Klicka på **OK** för att starta planeringskörningen.  

 Totalt 14 planeringsrader skapas. Lägg märke till att i den första planeringsraden så innehåller fältet **Åtgärdsmeddelande** **Ny**, fältet **Antal** 10, och fältet **Förfallodatum** visar 21-02-12. Den här nya raden för den översta överordnade artikeln, 1001, Touringcykel, har skapats eftersom artikeln använder partiformningsmetoden **Order**, vilket innebär att den måste levereras genom en en-till-en-relation i förhållande till behovet, d.v.s. försäljningsordern på tio enheter.  

 Nästa två planeringsrader är produktionsordrarna för touringcyklarnas hjul. Varje befintlig beställning av fem, i **Ursprungligt antal**ökas till 15, i fältet **Antal**. Båda produktionsbeställningarna har oförändrade förfallodatum, vilket visas i fältet **Åtgärdsmeddelande** som innehåller **Ändra antal.** Så är också fallet för planeringsraden för artikel 1300 utom dess orderavrundning till närmaste tiotal för spårad efterfrågan för 15 enheter upp till 20.  

 Alla andra planeringsrader har åtgärdsmeddelandet **Planera & ändra antal**. Detta betyder att förutom att öka kvantiteten så har förfallodatumen flyttats i förhållande till leveransplaneringen för att innefatta det extra antalet i den tillgängliga produktionstiden (kapaciteten). Inköpta komponenter planeras om och ökas för att uppfylla produktionsorder. Fortsätt med att analysera den nya planen.  

## <a name="analyzing-the-changed-planning-result" />Analysera det ändrade planeringsresultatet
 Eftersom alla parti-för-parti-planerade artiklar i filtret, 1100 till 1300, har en omplaneringsperiod på två veckor, ändras deras befintliga leveransorder för att uppfylla det nya behovet, som uppstår under de angivna två veckorna.  

 Flera planeringsrader multipliceras enkelt med tre för att ge 15 touringcyklar i stället för 5, och förfallodatumen flyttas tillbaka för att ge de ökade antalet till försäljningsorderns utleveransdatum till Fotograferna AB. För dessa planeringsrader kan alla kvantiteter spåras. De återstående planeringsraderna ökas med tio stycken förutom att deras förfallodatum flyttas. För dessa planeringsrader är en del av antalen ospårade på grund av olika planeringsparametrar. Fortsätt med att visa några av dessa beställningsspårningposter.  

### <a name="to-view-order-tracking-entries-for-item-1250" />Visa orderspårningsposter för artikel 1250

1.  Markera planeringsraden för artikeln 1250 och klicka sedan på **Orderspårning**.  

     De sju raderna på sidan **Orderspårning** visar att fem och tio stycken spåras via bak hjulet till de touringcyklarna på de två försäljningsorder respektive.  

     De sista fem styckena är inte spårade. Fortsätt med att analysera.  

2.  Välj fältet **ej spårat antal**.  

     På sidan **Planeringselement, inte spårat** visas att artikeln 1250 använder en planeringsparameter, Partistorleksmultipel som är 10,00. Därför är planeringsraden för 20 enheter totalt för att avrunda till faktiskt behov upp till närmaste tal som är delbart med 10. De sista fem enheterna är en ospårad kvantitet som tillfredsställer planeringsparametern.  

3.  Stäng alla sidor utom sidan **Planeringsförslag**.  

### <a name="to-view-an-existing-order" />Visa en befintlig order

1.  På planeringsraden för artikel 1250 klickar du på fältet **Ref. ordernr**. .  
2.  På sidan **Fast planerad prod.order** för Baknav. Den befintliga beställningen på tio stycken, som du skapade i den första planläggningskörningen, öppnas.  
3.  Stäng den fasta planerade produktionsorder.  

 Nu är du klar med genomgången av hur du använder planeringssystemet för att automatiskt upptäcka behov, beräkna lämpliga leveransorder i enlighet med behovet och planeringsparametrar och sedan automatiskt skapa olika typer av leveransorder med passande datum och antal.  

## <a name="see-also" />Se även
 [Genomgång av affärsprocesser](walkthrough-business-process-walkthroughs.md)   
<!--  [Walkthrough: Planning Supplies Manually](walkthrough-planning-supplies-manually.md)    -->
 [Designdetaljer: Leveransplanering](design-details-supply-planning.md)


[!INCLUDE[footer-include](includes/footer-banner.md)]
