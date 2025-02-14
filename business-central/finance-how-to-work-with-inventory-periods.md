---
title: Arbeta med lagerperioder
description: Du kan styra den tidsperiod som användare kan bokföra ändringar i lagret genom att definiera lagerperioder.
author: SorenGP
ms.topic: conceptual
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.search.keywords: 'inventory, periods'
ms.search.form: 5828
ms.date: 04/01/2021
ms.author: edupont
---
# <a name="work-with-inventory-periods" />Arbeta med lagerperioder

Under en lagerperiod går det att bokföra ändringar i lagret. Lagerperioden definieras utifrån slutdatumet. När en lagerperiod stängs kan inga ändringar bokföras i lagret, oavsett om de är förväntade eller rör faktureringen, före det här slutdatumet. Det går inte heller att bokföra nya värden i lagret före slutdatumet. Om det finns öppna artikeltransaktioner i den stängda perioden, d.v.s. positiva antal som ännu inte har kopplats till avgående transaktioner, går det fortfarande att koppla avgående antal till de här transaktionerna även om perioden är stängd.  

I följande avsnitt finns beskrivningar om att:

* Skapa lagerperioder.  
* Stänga lagerperioder.  
* Öppna lagerperioder igen.  

## <a name="to-create-an-inventory-period" />Skapa en lagerperiod

1. Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta för mig vad du vill göra") anger du **lagerperioder** och väljer sedan relaterad länk.  
2. Skapa en ny rad.  
3. Ange det sista datumet för lagerperioden som definieras i fältet **Slutdatum**. När perioden har stängts går det inte längre att bokföra lagerändringar före det här datumet.  
4. Ange ett beskrivande namn i fältet **Namn**. Välj **OK**.  

## <a name="closing-inventory-periods" />Stänga lagerperioder

I fältet **Stängd** anges om lagerperioden är stängd för lagervärdeändringar. Fältet kan inte redigeras.  

Det går att stänga vilken lagerperiod som helst, förutsatt att följande villkor är uppfyllda:  

* Det får inte finnas några öppna externa artikeltransaktioner, d.v.s. inget negativt lager, i den perioden.  
* Kostnaden för alla artiklar har justerats med batch-jobbet **Justera kost. – artikeltrans.**.  

Detta innebär att alla avgående transaktionsantal (till exempel antalen från försäljningsorder, avgående överföringar, fakturor, inköpsreturer eller inköpskreditnotor) måste kopplas till ett befintligt antal i lagret.  

### <a name="to-close-an-inventory-period" />Stänga en lagerperiod

1. Välj åtgärden **Justera kost. – artikeltrans.** innan en lagerperiod stängs för att säkerställa att alla kostnadsjusteringar har bokförts.

    Kör rapporten **Stäng lagerperiod – test** för att avgöra om det finns öppna externa artikeltransaktioner i lagerperioden eller om det finns artiklar som saknar justerad kostnad.  
2. Välj åtgärden **Stäng lagerperiod – Test**.  

    Kör batch-jobbet **Bokför lagerkostnad i redov.** för att säkerställa att alla kostnader har bokförts i redovisningen.  
3. Välj åtgärden **Bokför lager i redov.**.  
4. På sidan **Lagerperioder** väljer du den lagerperiod du vill stänga.  
5. Välj åtgärden **Stäng period**. När lagerperioden har stängts kan inga lagerändringar bokföras före slutdatumet. Kostnaden för alla artiklar måste justeras med batch-jobbet **Justera kost. – artikeltrans.** innan lagerperioden kan stängas.  
6. Klicka på **Ja** för att bekräfta stängningen av perioden eller klicka på **Nej** för att avbryta stängningen.  
7. Lagerperioden stängs och en bekräftelse visas när stängningen är klar.  

## <a name="reopening-inventory-periods" />Öppna lagerperioder igen
När lagerperioden har stängts en gång går det inte längre att ta bort den. Det går däremot att öppna lagerperioden igen om bokföring före lagerperiodens slutdatum ska tillåtas. Om en period öppnas igen, öppnas även de lagerperioder som innehåller slutdatum som infaller efter slutdatumet för perioden som öppnas igen.  

### <a name="to-reopen-an-inventory-period" />Öppna en lagerperiod igen
1. Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta för mig vad du vill göra") anger du **lagerperioder** och väljer sedan relaterad länk.  
2. Välj den lagerperiod som du vill öppna igen.  
3. Välj åtgärdenden **Öppna period igen**. Bekräfta att du vill öppna perioden igen.  
4. Alla lagerperioder med slutdatum efter perioden som du har valt öppnas igen.  

## <a name="see-also" />Se även
[Designdetaljer: Lagerperioder](design-details-inventory-periods.md)  
[Ekonomi](finance.md)  
[Lager](inventory-manage-inventory.md)  
[Arbeta med Financials](ui-work-product.md)


[!INCLUDE[footer-include](includes/footer-banner.md)]
