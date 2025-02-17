---
title: 'Sälja, sammanställa och leverera satser'
description: För att stödja just-i-tid-lager kan monteringsorder automatiskt skapas och kopplas så snart försäljningsorderraden skapas.
author: SorenGP
ms.topic: conceptual
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.search.keywords: null
ms.date: 06/24/2021
ms.author: edupont
---
# <a name="walkthrough-selling-assembling-and-shipping-kits" />Genomgång: Sälja, sammanställa och leverera satser

<!-- [!INCLUDE[complete_sample_data](includes/complete_sample_data.md)]   -->

För att stödja just-i-tid-lager och kapaciteten för att anpassa produkter till kundförfrågan, kan monteringsorder automatiskt skapas och kopplas så snart försäljningsorderraden skapas. Kopplingen mellan försäljningsbehov och monteringsleverans hjälper försäljningsorderhandläggare att anpassa monteringsartikeln och lova leveransdatum utifrån komponentens tillgänglighet. Monteringsförbrukning och monteringsutflöde bokförs dessutom automatiskt tillsammans med utleveransen av den kopplade försäljningsordern.  

Det finns särskilda funktioner för att styra leverans av montering mot kundorder, både i grundläggande och avancerade distributionslagerkonfigurationer. När arbetare ansvariga för slutfört monterande av komponenter för montering eller hela antalet för montering mot kundorder, registrerar de i fältet **Ant. att utleverera** på distributionslagerutleveransraden i avancerade konfigurationer och väljer **Bokför utleverans**. Resultatet är att motsvarande monteringsutflöde bokförs, inklusive den relaterade komponentförbrukningen, och en utleverans för kvantiteterna bokförs för den kopplade försäljningsordern. I den här genomgången visas den avancerade distributionslagerprocessen.  

När antalet för montering mot kundorder är klar för utleverans i grundläggande konfigurationer bokför ansvarig lagerarbetare en lagerplockning för försäljningsorderraderna. Detta skapar en lagerförflyttning för komponenterna, och bokför monteringsutflöde och försäljningsorderleveransen. Mer information finns i [hantera artiklar för montering mot kundorder i lagerplockningar](warehouse-how-to-pick-items-with-inventory-picks.md#handling-assemble-to-order-items-with-inventory-picks) .  

## <a name="about-this-walkthrough" />Om den här genomgången

I den här genomgången tas följande aktiviteter upp:  

### <a name="setting-up-assembly-items" />Ställa in monteringsartiklar

Monteringsartiklar karakteriseras av sitt återanskaffningssystem och sin monteringsstruktur. Artikelns monteringsmetod kan vara antingen montering mot kundorder (ATO) eller montering mot lager (ATS). I detta avsnitt omfattas följande uppgifter:  

-   Inställning av lämpligt återanskaffningssystem och monteringsmetod för ett nytt monteringsartikelkort.  
-   Skapa en monteringsstruktur som anger monteringskomponenterna och resursen som ingår i monteringsartikeln.  

### <a name="selling-customized-assembly-items" />Sälja anpassade monteringsartiklar

Med [!INCLUDE[prod_short](includes/prod_short.md)] blir det möjligt att både ange lagerkvantitet och kvantitet av montering mot kundorder på försäljningsorderraden. I detta avsnitt omfattas följande uppgifter:  

-   Skapa en ren ATO-försäljningsorderrad där hela kvantiteten är inaktiverad och måste monteras före leverans.  
-   Anpassa ATO-objekt.  
-   Omräkning av a-priset för en anpassad monteringsartikel.  
-   Skapa en blandad försäljningsorderrad, där delar av försäljningsantalet levereras från lagret och den återstående delen måste monteras före leverans.  
-   Förstå varningar om ATO-tillgänglighet.  

### <a name="planning-for-assembly-items" />Planering för monteringsartiklar

Monteringsbehov och monteringsleverans hanteras av planeringssystemet, precis som för inköp, överföring och produktion. I detta avsnitt omfattas följande uppgifter:  

-   Körning av en fullständig plan för artiklar med försäljningsbehov av monteringsleverans.  
-   Framtagning av en monteringsorder för att uppfylla ett försäljningsradantal på det efterfrågade utleveransdatumet.  

### <a name="assembling-items" />Montera artiklar

Monteringsorder fungerar på ungefär samma sätt som produktionsorder, men förbrukning och utflöde registreras och bokförs direkt från beställningen. När artiklar monteras för lager har monteringsarbetaren fullständig åtkomst till alla fält, både i huvudet och på transaktionsraden. När artiklar monteras för en beställning där antal och datum har lovats till kunden, går vissa fält på monteringsordern inte att redigera. I så fall görs monteringsbokningen från distributionslagerutleveransen för den kopplade försäljningsordern. I detta avsnitt omfattas följande uppgifter.  

-   Registrering och bokföring av monteringsförbrukning och monteringsutflöde till lagret.  
-   Åtkomst till en distributionslagerutleveransrad från en ATO-monteringsorder för att registrera monteringsarbete.  
-   Åtkomst till en ATO-monteringsorder från en distributionslagerutleveransrad för att granska data som har angetts automatiskt.  

### <a name="shipping-assembly-items-from-stock-and-assembled-to-order" />Utleverans av monteringsartiklar, från lager och montering mot kundorder

Särskild funktioner finns för att styra fältet av montering mot kundorder. I detta avsnitt omfattas följande uppgifter:  

-   Skapa en distributionslagerplockning för lagermonteringsartiklar och för monteringskomponenter som ska monteras före utleverans.  
-   Registrera distributionslagerplockningar för monteringskomponenter och sedan för monteringsartiklar.  
-   Åtkomst till en monteringsorder från en distributionslagerutleverans för att granska plockade eller förbrukade komponenter.  
-   Utleverans av antalet för montering mot kundorder.  
-   Utleverans av lagermonteringsartiklar.  

## <a name="roles" />Roller

Den här genomgången innehåller arbetsuppgifter som utförs av följande användarroller:  

-   Försäljningsorderhandläggare  
-   Planerare  
-   Monteringsarbetare  
-   Plockare  
-   Sändningsansvarig  

## <a name="prerequisites" />Förutsättningar

Innan du kan utföra aktiviteterna i den här genomgången måste du göra följande  

-   Installera [!INCLUDE[prod_short](includes/prod_short.md)].  
-   Ange dig själv som distributionslageranvändare på lagerstället WHITE i följande steg:  

1.  Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta för mig vad du vill göra") anger du **distributionslagerpersonal** och väljer sedan relaterad länk.  
2.  Välj fältet **Användar-ID** och välj ditt eget användarkonto på sidan **Användare**.  
3.  Ange WHITE i fältet **Lagerställekod**.  
4.  Välj fältet **Standard**.  

> [!NOTE]
> [!INCLUDE [locations-cronus](includes/locations-cronus.md)]

Förbered lagerstället WHITE för bearbetning av monteringen i följande steg:  

1.  Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta för mig vad du vill göra") anger du **Platser** och väljer sedan relaterad länk.  
2.  Öppna lagerställekortet för lagerstället WHITE.  
3.  På snabbfliken **lagerställen** anger du **V-10-0001** i fältet **Till monteringsplats – kod**.  

    Genom att ange denna lagerställeskod som förhindrar plockning är alla monteringsorderrader redo att ta emot komponenter på lagerstället.  

4.  I fältet **Från monteringsplats – kod** anger du **V-01-0001**.  

    När du anger den här lagerstället för plockning överförs alla färdiga monteringsartiklar till lagerstället.  

Ta bort standardledtiden för interna processer genom att följa dessa steg:  

1.  Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta för mig vad du vill göra") anger du **Produktionsinställningar** och väljer sedan relaterad länk.  
2.  På sidan **Produktionsinställningar** klickar du på snabbfliken **planering**, tar bort värdet i fältet **Standard säkerhetsledtid**.  

<!-- Create inventory for assembly components by following [Prepare Sample Data](walkthrough-selling-assembling-and-shipping-kits.md#prepare-sample-data).   -->

## <a name="story" />Situation

Den 23 januari tar försäljningsorderhandläggaren Susan en beställning från The Device Shop på tre enheter av sats B, som är ett ATO-objekt. Alla tre enheterna anpassas och måste innehålla det kraftiga grafikkortet och ett extra RAM-block. Skivenheterna uppgraderas till DWD, eftersom CD-enheterna är inte är tillgängliga. Susan vet att enheterna kan monteras omedelbart, så hon lämnar föreslag på leveransdatum den 23 januari.  

Samtidigt beställer kunden femton enheter av sats A med en särskild beställning av fem anpassade enheter som innehåller den kraftiga grafikkortet. Även om sats A typiskt är montering mot lager, kombinerar orderhandläggaren försäljningsradantalen för att sälja tio enheter från materiel och montera fem enheter anpassade till beställningen. De tio enheterna av sats A är inte tillgängliga och måste först levereras till lagret med en monteringsorder i enlighet med artikelns monteringsmetod. Susan får veta av monteringsavdelningen att enheterna i sats A inte kan slutföras under veckan. Susan anger utleveransdatum för den andra försäljningsorderraden, för den blandade ATO- och lagerkvantiteten, som 27 januari och informerar kunden att 15 enheter av sats A levereras fyra dagar senare än de tre enheterna av sats B. För att signalera till leveransavdelningen att den här försäljningsordern kräver montering skapar Susan ett distributionslagerutleveransdokument från försäljningsordern.  

Planeraren Eduardo kör planeringsförslaget och skapar en monteringsorder på tio standardenheter av sats A med en internt förfallodatum den 27 januari.  

Sammy, som är ansvarig för leveransen, får tre distributionslagerutleveransrader för försäljningsordern: en rad för de tre rena ATO-enheterna, en rad för de fem ATO-enheterna på den blandade försäljningsorderraden och en rad för de tio ATS-enheterna på den blandade försäljningsorderraden. Sammy skapar ett distributionslagerplockningsdokument för alla monteringskomponenter som behövs för att montera de totalt åtta ATO-enheten i distributionslagerutleveransdokumentet.  

Plockaren John hämtar komponenter till alla ATO-delar i distributionslagerutleveransdokumentet och kommer in med dem till monteringsområdet. John anger det antal som ska hanteras och registrerar distributionslagerplockningen.  

Linda monterar de tre ATO-enheterna av sats B. Komponenterna har redan plockats och hon registrerar inte utflödesantal och förbrukningsantal eller bokför ordern eftersom både av dessa uppgifter utförs automatiskt via de relaterade distributionslagerutleveransraderna.  

Sammy registrerar den monterade kvantiteten på distributionslagerutleveransraden och bokför leveransen av de tre enheterna av sats B. Den första raden på försäljningsordern uppdateras som levererad. Den kopplade monteringsordern fortsätter vara öppen tills försäljningsordern har fakturerats helt. De två distributionslagerutleveransraderna, en ATO och en ATS, för sats A med förfallodatum den 27 januari fortsätter vara öppna.  

Den 27 januari bearbetar Linda två monteringsorder för Kit A. Den här beställningen är fem enheter, som hon behandlar på ett annat sätt än ATO-ordern för Kit B som hon behandlade 23 januari. På den här ordern har Linda behörighet att själv komma åt distributionslagrets utleveransrad för att registrera det avslutade monteringsarbetet. Komponenterna som behövs är klara på monteringsavdelningen, där de har plockats tillsammans med komponenter till sats B.  

Den andra monteringsordern är ATS-beställningen på tio enheter, som har skapats i planeringssystemet. På den här ATS-ordern utför Linda alla åtgärder som berörs av monteringsordern. Linda skapar ett dokument för distributionslagerplockningsdokument för monteringskomponenterna som behövs för att montera de tio enheterna. När PC-datorerna har monterats bokför Linda monteringsordern och signalerar därmed att artiklarna finns i lager och kan plockas för utleverans.  

Sammy skapar ett dokument för distributionslagerplockningsdokument för alla kvantiteter som återstår innan utleveransen från distributionslagret kan bokföras. Ett plockningsdokument skapas för de tio enheterna av sats A som precis har slutförts. Komponenterna som behövs för montering av de fem enheterna av sats A plockades den 23 januari.  

John tar med de tio enheterna av sats A från lagret till det angivna utleveransområdet, registrerar volymen som ska hanteras och registrerar sedan plockningen.  

Sammy packar de tio ATS-enheterna med de fem ATO-enheterna som Linda monterade tidigare under dagen. Sammy fyller i antal att leverera på båda raderna och bokför sedan den sista utleveransen till The Device Shop. Den relaterade monteringsordern på fem enheter av sats A bokförs automatiskt. Den andra raden på försäljningsordern uppdateras som utlevererad. Två kopplade monteringsordrar fortsätter vara öppna tills försäljningsordern har fakturerats och stängts.  

När försäljningsordern bokförs senare som fullständigt fakturerad tas försäljningsordern och den kopplade monteringsordern bort.  

## <a name="prepare-sample-data" />Förbereda exempeldata

1.  Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta vad du vill göra") anger du **Dist.lager artikeljournaler** och väljer sedan relaterad länk.  
2.  Välj fältet **Journalnamn** och välj sedan standardjournalen.  
3.  Skapa positiva lagerjusteringar på lagerstället WHITE på arbetsdatumet, den 23 januari, genom att ange följande information.  

    |**Artikelnr**|**Zonkod**|**Lagerställeskod**|**Antal**|  
    |-----------------------------------|---------------------------------------|--------------------------------------|------------------------------------|  
    |80001|PLOCKNING|D-01-0001|20|  
    |80005|PLOCKNING|D-01-0001|20|  
    |80011|PLOCKNING|D-01-0001|20|  
    |80014|PLOCKA|D-01-0001|20|  
    |80203|PLOCKNING|D-01-0001|20|  
    |80209|PLOCKNING|D-01-0001|20|  

4.  Välj åtgärden **Registrera** och sedan knappen **Ja**.  

    Sedan synkroniserar du de nya distributionslagertransaktionerna med lagret.  

5.  Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta vad du vill göra") anger du **Artikeljournaler** och väljer sedan relaterad länk. Sidan **Artikeljournal** öppnas.  
6.  Välj åtgärden **Beräkna dist.lagerjustering**.  
7.  På sidan **Beräkna dist.lager justering** för att köra funktionen **OK**.  
8.  På sidan **Artikeljournal** väljer du åtgärden **Bokför** och väljer sedan knappen **Ja**.  

### <a name="creating-the-assembly-items" />Skapa monteringsartiklarna

1.  Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta vad du vill göra") anger du **Artiklar** och väljer sedan relaterad länk.  
2.  Välj åtgärden **Ny**.  
3.  Skapa den första monteringsartikeln utifrån följande information.  

    |Fält|Värde|  
    |---------------------------------|-----------|  
    |**Beskrivning**|Sats A – Bas-PC|  
    |**Basenhet**|STYCK|  
    |**Artikelkategorikod**|Div.|  
    |**Återanskaffningssystem**|Montering|  
    |**Monteringsmetod**|Montering mot lager|  
    |**Partiformningsmetod**|Parti-för-parti|  

    > [!NOTE]  
    >  Sats A levereras typiskt från montering mot lager och har därför en partiformningsmetod, där den ingår i den allmänna leveransplaneringen.  

4.  Välj åtgärden **Montering** och välj sedan **Monteringsstruktur**.  
5.  Definiera en monteringsstruktur för sats A med följande information.  

    |**Typ**|**Nr**|**Antal per**|  
    |-------------------------------|------------------------------|---------------------------------------|  
    |Artikel|80001|1|  
    |Artikel|80011|1|  
    |Artikel|80209|1|  
    |Resurs|Karin|1|  

6.  Skapa den andra monteringsartikeln utifrån följande information.  

    |Fält|Värde|  
    |---------------------------------|-----------|  
    |**Beskrivning**|Sats B – Proffs-PC|  
    |**Basenhet**|STYCK|  
    |**Artikelkategorikod**|Div.|  
    |**Återanskaffningssystem**|Montering|  
    |**Monteringsmetod**|Montering mot kundorder|  

    > [!NOTE]  
    >  Sats B levereras vanligtvis från montering mot kundorder och har därför inte en partiformningsmetod, eftersom den inte bör ingå i allmän leveransplanering.  

7.  Välj åtgärden **Montering** och välj sedan **Monteringsstruktur**.  
8.  Definiera en monteringsstruktur för sats B med följande information.  

    |**Typ**|**Nr**|**Antal per**|  
    |-------------------------------|------------------------------|---------------------------------------|  
    |Artikel|80005|1|  
    |Artikel|80014|1|  
    |Artikel|80210|1|  
    |Resurs|Karin|1|  

### <a name="selling-the-assembly-items" />Sälja monteringsartiklarna

1.  Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta vad du vill göra") anger du **försäljningsorder** och väljer sedan relaterad länk.  
2.  Välj åtgärden **Ny**.  
3.  Skapa två försäljningsorderrader för kund 62000, The Device Shop, på arbetsdatumet med följande information.  

    |**Typ**|**Beskrivning**|**Antal**|Antal att montera mot kundorder|Utleveransdatum|  
    |--------------|---------------------|------------------|-------------------------------|-------------------|  
    |Artikel|Sats B – Proffs-PC|3|3|23 januari|  
    |Artikel|Sats A – Bas-PC|15|5|27 januari|  

    > [!NOTE]  
    >  Följande problem med tillgängligheten har uppstått på försäljningsorderraden för sats B:  
    >   
    >  -   Monteringskomponent 80210 är inte tillgänglig. Det betyder att de tre angivna enheterna av sats B inte kan monteras, vilket anges som **0** i fältet **Möjlig att montera** på sidan **Monteringsdisposition**.  
    >   
    >  Följande problem med tillgängligheten har uppstått på försäljningsorderraden för sats A:  
    >   
    >  -   De tio enheterna av sats A är inte tillgängliga. Detta indikerar för planeringssystemet att kvantiteten måste monteras mot lager.  

    Sedan ska du anpassa försäljningsordern.  

4.  Välj försäljningsorderraden för tre enheter av sats B.  
5.  På snabbfliken **Rader** väljer du **Rad**, **Montering mot kundorder** och sedan **Montering mot kundorderrader**.  
6.  På sidan **Montering mot kundorderrader** på monteringsorderraden för artikel 80014, ange **2** i fältet **kvantitet per**.  
7.  På monteringsorderraden för artikel 80210, väljer du fältet **nr.** och markerar sedan artikel 80209 i stället.  
8.  Skapa en ny monteringsorder med följande information.  

    |Kontakttyp|Nummer|Antal per|  
    |----------|---------|------------------|  
    |Artikel|80203|1|  

9. Stäng sidan **Montering mot kundorderrader**.  

    Uppdatera sedan a-priset för sats B i enlighet med anpassningen som du just har gjort. Observera det aktuella värdet i fältet **Enhetspris exkl. moms**.  

10. På snabbfliken **Rader** väljer du **Rad**, **Montering mot kundorder** och sedan **Summera pris**.  
11. Välj **Ja**. Observera det ökade värdet i fältet **Enhetspris exkl. moms**.  
12. Välj försäljningsorderraden för 15 enheter av sats A.  
13. På snabbfliken **Rader** väljer du **Rad**, **Montering mot kundorder** och sedan **Montering mot kundorderrader**.  
14. På sidan **Montering mot kundorderrader** skapar du en ny monteringsorder med följande information.  

    |Typ|Nr|Antal per|  
    |----------|---------|------------------|  
    |Artikel|80203|1|  

     Ändra sedan leveransdatumet på den andra försäljningsorderraden enligt monteringschemat.  

15. PÅ försäljningsorderraden för 15 enheter med sats A, ange **01-27-2014** i fältet **Utleveransdatum**.  
16. Välj åtgärden **Släppa**.  
17. Välj åtgärden **Skapa dist.lagerutleverans**.  
18. Stäng försäljningsordern.  

### <a name="planning-for-the-unavailable-ats-items" />Planering för de ATS-artiklar som inte är tillgängliga

1.  Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta vad du vill göra") anger du **planeringsförslag** och väljer sedan relaterad länk.  
2.  Välj åtgärden **Beräkna fullständig plan**.  
3.  Ange följande filter på sidan **Skapa inköpsförslag**.  

    |Startdatum|Slutdatum|Nummer|  
    |-------------------|-----------------|---------|  
    |01-23-2014|01-27-2014|Sats A – Bas-PC|  

4.  Välj **OK**.  

    En ny planeringsrad skapas för den behövda monteringsordern för tio enheter, förfaller den 27 januari. Inga ändringar behövs så att du kan skapa ordern.  

5.  Välj den **Verkställ åtgärdsmeddelande** åtgärd.  
6.  På sidan **Monteringsorder** och välj sedan **Skapa monteringsorder** i fönstret **Verkställ åtgärdsmeddelande**.  
7.  Välj knappen **OK**.  

### <a name="assembling-and-shipping-the-first-ato-quantity" />Sammanställa och leverera det första ATO-antalet

1.  Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta vad du vill göra") anger du **Distributionslagerutleverans** och väljer sedan relaterad länk.  

    > [!NOTE]  
    >  I detta avsnitt ska personen som ansvarar för leveransen registrera det avslutade ATO-monteringsarbetet på utleveransraden. Detta arbetsflöde kan uppstå i miljöer där monteringsarbetet ska utföras av personen som ansvarar för leverans, eller av monteringsarbetare i utleveransområdet.  
    >   
    >  I detta avsnitt utförs på åtgärder på monteringsordern indirekt från distributionslagerutleveransraden. Mer information om hur du bearbetar en monteringsorder direkt finns i avsnittet "Montera artiklar mot lager" i den här genomgången.  

2.  Öppna den senaste distributionslagerutleveransen som har skapats på lagerstället WHITE.  

    Observera de tre distributionslagerutleveransraderna: en rad för ATO-antalet av sats B, förfaller den 23 januari. En rad för ATO-antalet av sats A, förfaller den 27 januari. En rad för lagerkvantiteten av sats A, förfaller den 27 januari.  

    Fältet **Montering mot kundorder** anger monteringsmetoden.

    Sedan skapar du ett plockningsdokument för alla ATO-monteringskomponenter som behövs för utleveransen från distributionslagret.  

3.  Välj åtgärden **Skapa plockning** och sedan knappen **OK**.  

    Utför sedan plockarens uppgift.  

4.  Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta vad du vill göra") anger du **plockningar** och väljer sedan relaterad länk.  
5.  Öppna plockningsdokumentet som du skapade i steg 3 i det här avsnittet.  

    Observera värdet i fältet **Källdokument** och att alla plockningsrader avser monteringkomponenter.  

    Registrera sedan plockningen, utan att ändra standardinformationen.  

6.  Välj åtgärden **Fyll i auto. ant. att hantera**.  
7.  Välj **Registrera plockning**.  

    Återgå till att utföra utleveransuppgifterna.  

8.  Öppna sidan **Dist.lager utleveranslista** igen.  

    Observera att fältet **Plockat antal** fortfarande är tomt på alla rader. Det beror på att du fortfarande inte har plockat artiklarna som ska levereras, utan endast komponenter som krävs för att sammanställa ATO-antalet.  

    Fortsätt med att granska den relaterade monteringsordern.  

9. Välj utleveransraden för tre enheter av sats B.  
10. På snabbfliken **Rader** väljer du **Rad** och sedan **Montering mot kundorder**. Sidan **Monteringsorder** öppnas.  

    Observera att flera fält på monteringsordern är inaktiverade eftersom beställningen är kopplad till en försäljningsorder.  

    Observera på monteringsorderraderna att fältet **Plockat antal** är ifyllt. Det beror på plockningen som du registrerade i steg 7 i det här avsnittet.  

11. I fältet **Antal att montera** prova att ange ett lägre värde än **3**.  

    Läs felmeddelandet som förklarar varför det här fältet endast kan fyllas i via fältet **Ant. att utleverera** på den relaterade leveransen.  

    Fältet **Antal att montera** kan redigeras för situationer där du inte vill skicka delvisa lagerkvantiteter i stället för montering av flera enheter mot order. Mer information finns i avsnittet "Kombinationsscenarion" i [Förstå montering mot kundorder och montering mot lager](assembly-assemble-to-order-or-assemble-to-stock.md).  

12. Stäng sidan **monteringsorder** och återgå till sidan **distributionslagerutleverans**.  
13. På utleveransraden för tre enheter av sats B i **Ant. att utleverera** anger du **3**.  
14. Välj åtgärden **Bokför utleverans** och välj sedan knappen **Leverera**.  

    Tillsammans med den här bokföringen av distributionslagerutleveransen bokförs hela förbrukningen och utflödet av den relaterade monteringsordern och fältet **Återstående antal**. Försäljningsorderraden för sats B uppdateras för att visa att de tre enheterna har levererats.  

    Lageraktiviteterna för att uppfylla den första försäljningsorderraden den 23 januari har slutförts. Uppfyll sedan försäljningsorderraderna som ska levereras den 27 januari  

### <a name="assembling-and-recording-the-second-ato-quantity" />Sammanställa och registrera det andra ATO-antalet

1.  Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta vad du vill göra") anger du **monteringsorder** och väljer sedan relaterad länk.  

    Observera att ATO-ordern för levererade enheter av sats B fortfarande finns i listan, även om **Återstående antal** är tomt. Det beror på att den kopplade försäljningsordern fortfarande inte har fakturerats helt.  

    > [!NOTE]  
    >  I detta avsnitt är monteringsarbetaren ansvarig för att registrera det avslutade ATO-monteringsarbetet på utleveransraden. Detta arbetsflöde kan uppstå i miljöer där monteringsarbetet utförs på en separat monteringsavdelning och monteringsarbetare har behörighet att ändra distributionslagerutleveransraden.  

2.  Öppna ATO-monteringsordern för fem enheter av sats A.  

    Lägg märke till att **Antal att montera** och **Antal att förbruka** är tomma eftersom ingenting har registrerats ännu.  

    Observera på monteringsorderraderna att fältet **Plockat antal** är ifyllt. Det beror på plockningen som registrerades den 23 januari.  

    Registrera sedan att monteringsordern har slutförts.  

3.  Välj åtgärden **Montering mot kundorder, dist.lager utleveransrad**.  
4.  På sidan **Montering mot kundorder, dist.lager utleveransrad** i fältet **Ant. att utleverera**, ange **5** och stäng sedan sidan.  

    Observera på sidan **Monteringsorder** att fälten **Antal att montera** och **Antal att förbruka** nu fylls i med de utflödes- och förbrukningsantal som ska bokföras med utleveransen.  

5.  Stäng sidan **Monteringsorder**.  

### <a name="assembling-the-ats-quantity" />Montering av ATS-antalet

1.  Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta vad du vill göra") anger du **monteringsorder** och väljer sedan relaterad länk.  
2.  Öppna monteringsordern för tio enheter av sats A.  

    Observera att fältet **Antal att montera** fylls i med det förväntade antalet.  

    Sedan ska du skapa ett plockningsdokument för att hämta de nödvändiga komponenternz.  

3.  Välj åtgärden **Frisläpp**.  
4.  Välj åtgärden **Skapa dist.lagerplockning** och sedan knappen **OK**.  

    Utför sedan plockarens uppgift.  

5.  Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta vad du vill göra") anger du **plockningar** och väljer sedan relaterad länk.  
6.  Öppna plockningsdokumentet som du skapade i steg 4 i det här avsnittet.  

     Fortsätt med att registrera plockningen, utan att ändra standardinformationen.  

7.  Välj åtgärden **Fyll i auto. ant. att hantera**.  
8.  Välj **Registrera plockning**.  

    Återgå till monteringsordern för att utföra den sista monteringsuppgiften.  

9. I **Monteringsorder** väljer du åtgärden **Bokför** och väljer sedan knappen **Ja**.  

    Observera att monteringsordern tas bort från listan över öppna beställningar.  

### <a name="shipping-the-remaining-items-partly-from-stock-and-partly-assembled-to-the-order" />Leverera de återstående artiklarna, delvis från materiel och delvis från montering mot kundorder

1.  Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta vad du vill göra") anger du **Distributionslagerutleverans** och väljer sedan relaterad länk.  
2.  Öppna den senaste distributionslagerutleveransen som har skapats på lagerstället WHITE.  

    Observera att på raden för de tio enheterna för sats A är fälten **Ant. att utleverera** och **Plockat antal** är tomma.  

    Välj sedan återstående artiklar.  

3.  Välj åtgärden **Skapa plockning** och sedan knappen **OK**.  

    Utför sedan plockarens senaste uppgift för den här utleveransen från lager.  

4.  Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta vad du vill göra") anger du **plockningar** och väljer sedan relaterad länk.  
5.  Öppna plockningsdokumentet som du skapade i steg 3 i det här avsnittet.  

    Observera att detta plockningsdokument avser monteringsartikeln och inte monteringkomponenterna.  

    Registrera sedan plockningen, utan att ändra standardinformationen.  

6.  Välj åtgärden **Fyll i auto. ant. att hantera**.  
7.  Välj åtgärden **Registrera plockning** och sedan knappen **Ja**.  

    Återgå till distributionslagerutleveransen för att utföra den sista uppgiften.  

8.  Öppna sidan **Dist.lager utleveranslista** igen.  

    På sidan **Utleveranser för dist.lager** på raden för tio enheter av sats A, observera att fälten **Ant. att utleverera** och **Plockat antal** nu innehåller **10**.  

9. Välj åtgärden **Bokför utleverans** och välj **Leverera**.  

    Distributionslagerutleveransdokumentet tas bort, vilket anger att de berörda lageraktiviteterna är slutförda. I nästa steg verifierar du att försäljningsordern har behandlats.  

10. Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta vad du vill göra") anger du **försäljningsorder** och väljer sedan relaterad länk  
11. Öppna försäljningsordern för The Device Shop.  

    Observera att fältet **Utlevererat antal** innehåller hela kvantiteten på båda raderna.  

    När The Device Shop betalar för mottagningen av de 18 PC-datorerna från CRONUS tas försäljningsordern och dess kopplade monteringsorder bort.  

## <a name="see-related-microsoft-trainingtrainingpathsassemble-items-dynamics-365-business-central" />Se relaterad [Microsoft utbildning](/training/paths/assemble-items-dynamics-365-business-central/)

## <a name="see-also" />Se även

 [Förstå montering mot kundorder och montering mot lager](assembly-assemble-to-order-or-assemble-to-stock.md)   
 [Montera Artiklar](assembly-how-to-assemble-items.md)   
 [Plocka artiklar för utleverans från dist.lager](warehouse-how-to-pick-items-for-warehouse-shipment.md)   
 [Sälja en artikel som monterats mot kundorder](assembly-how-to-sell-items-assembled-to-order.md)   
 [Montera Artiklar](assembly-how-to-assemble-items.md)   
 [Designdetaljer: Bokföring av monteringsorder](design-details-assembly-order-posting.md)   
 [Designdetaljer: Interna distributionslagerflöden](design-details-internal-warehouse-flows.md)   
 [Designdetaljer: utgående distributionslagerflöde](design-details-outbound-warehouse-flow.md)   
<!--  [Walkthrough: Planning Supplies Automatically](walkthrough-planning-supplies-automatically.md) -->


[!INCLUDE[footer-include](includes/footer-banner.md)]
