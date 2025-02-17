---
title: Servicestatistik
description: 'Få en snabb översikt över innehållet och statistik i servicedokument (order, offert, faktura eller kreditnota), den detaljerade informationen på varje servicerad etc.'
author: brentholtorf
ms.topic: conceptual
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.search.keywords: null
ms.date: 06/23/2021
ms.author: bholtorf
---

# <a name="viewing-service-statistics" />Visa servicestatistik
Du kan använda statistik för att analysera servicedokument och ta reda på hur bra du hanterar dina serviceprocesser. Du kan analysera servicekontrakt, artiklar, offerter, order, fakturor och kreditnotor genom att välja åtgärd **statistik**. För serviceartiklar och kontrakt kan du också använda **Serviceartikel Trendscape** eller **Kontrakt Trendscape** för att visa en översikt över servicetransaktioner för en viss serviceartikel.   

## <a name="viewing-statistics-for-service-orders" />Så här visar du serviceorderstatistik:
Med hjälp av serviceorderstatistiken får du en snabb översikt över innehållet i hela serviceordern, detaljerad information om de specifika serviceraderna och information rörande fakturering, leverans och förbrukning samt kundens saldo.  

Statistikinformationen för en serviceorder visas på sidan **Tjänsteorderstatistik** för den önskade ordern. Du kan öppna statistiksidan från en serviceorder. På sidan **Tjänsteorder** väljer du **Statistik**. På snabbflikarna på sidan visas information om t. ex. antal, belopp, moms, kostnad, vinst och kundkreditlimit. Beloppen på sidan visas i den valuta som används på serviceordern om inget annat anges.  

### <a name="view-totals-for-a-service-order" />Visa summor för en serviceorder
Du kan visa det totala beloppet på serviceraderna (inkl. och exkl. moms), momsandel, kostnad och TB på serviceraderna. Sidan visar också artikelspecifik information, till exempel vikt, volym och antalet förpackningar.  

### <a name="view-shipping-information" />Visa leveransinformation
Du kan visa information om de artiklar, resurser och/eller kostnader som ska levereras. Informationen bygger på värdena som finns angivna i fältet **Ant. att utleverera** på var och en av serviceraderna ordern.  

### <a name="view-order-details" />Visa orderdetaljer
Du kan visa information om de artiklar, resurstimmar och kostnader som ska faktureras och förbrukas. Följande tabell beskriver denna information.  

|Kolumn | Beskrivning|  
|------------|---------------------------------------|  
|**Fakturering**|Visar belopp som ska bokföras som fakturerade från serviceordern.|  
|**Förbrukning**|Visar antal och kostnad för de artiklar och/eller resurser som ska bokföras som förbrukade.|  
|**Totalt**|Visar de totala belopp på serviceordern som uppkommer när faktureringsbeloppen läggs ihop med förbrukningsbeloppen.|  

### <a name="analyze-service-order-lines" />Analysera serviceorderrader
Du kan analysera informationen efter de olika typerna av servicerader som ingår i serviceordern. Separata belopp för:  

* Artiklar  
* Resurser  
* Kostnader och redovisningskonton  

### <a name="view-customer-information" />Visa kundinformation
Se saldot på kundens konto utöver den maximala kredit som kan beviljas den kund som servicedokumentet skapades för.

## <a name="viewing-service-item-statistics" />Visa serviceartikelstatistik
På sidan **Serviceartikelstatistik** kan du visa uppdaterad information om en serviceartikel baserat på följande servicetransaktionstyper:  

* Resurser  
* Artiklar  
* Servicekostnad  
* Servicekontrakt  
* Totalt  

För varje transaktionstyp kan du visa fakturerat belopp, förbrukning (belopp), kostnadsbelopp, fakturerat antal och förbrukat antal, TB-belopp och TB-procent. Täckningsbidraget beräknas enligt följande formel:  

* (Fakturerat belopp – förbrukning (kostnaden)) x 100 / fakturerat belopp  

## <a name="use-trendscapes" />Med hjälp av Trendscapes
För serviceartiklar och servicekontrakt, ger sidorna **Serviceartikel Trendscape** eller **Servicekontrakt Trendscape** innehåller en rullningsbar översikt över servicetransaktioner som skapas i en viss tid för en viss serviceartikel eller kontrakt. Visa trendscape genom att öppna servicekontraktet eller serviceartikeln, välj åtgärden **statistik**, och välj sedan **Trendscape**.

När du rullar i listan beräknas beloppen enligt den lokala valutan enligt det valda tidsintervallet. Alla belopp beräknas från servicetransaktioner, som är transaktioner som skapas när du bokför serviceorder eller -fakturor.

Du kan filtrera listan genom att ange serviceartiklar.  

> [!Tip]  
>  Om du har valt tidsintervallet **Dag** och du behöver rulla i genom en lång period kan du nå informationen snabbare genom att ändra till ett större intervall, såsom **Kvartal**. När du har hittat den period du vill ha kan du ändra tillbaka till det ursprungliga intervallet för att se uppgifterna i detalj.   

## <a name="viewing-gains-and-losses-on-contracts" />Visa vinster och förluster i kontrakt
En transaktion för kontraktets vinst eller förlust skapas automatiskt då kontraktofferter konverteras till servicekontrakt, då kontraktrader läggs till eller tas bort från servicekontrakt och då kontrakt annulleras. Om du vill se kontrakt vinst/förlust kan du göra något av följande:  

|Sida | Beskrivning|  
|----------------|---------------------------------------|  
|**Kontrakt vinst/förlust (kont.)**|Så här visar du kontrakt vinst/förlust per servicekontrakt.|  
|**Kontrakt vinst/förlust (gr.)**|Så här visar du kontrakt vinst/förlust per servicekontraktsgrupp.|  
|**Kontrakt vinst/förlust (kunder)**|Så här visar du kontrakt vinst/förlust per kund.|  
|**Kontrakt vinst/förlust (uppfölj.)**|Så här visar du kontrakt vinst/förlust per uppföljningskod.|  
|**Kontrakt vinst/förlust (ansenh.)**|Så här visar du kontrakt vinst/förlust per ansvarsenhet.|  

1. Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta vad du vill göra") Anger du namnet på sidan som ska visas och väljer sedan relaterad länk.  
2. Fyll i de filtervillkor som du vill koppla. Välj något värde för **Uppföljningskod filter**, till exempel på sidan **Kontrakt vinst/förlust (uppfölj)**.  
3. Välj åtgärden **Visa matris**.

## <a name="viewing-statistics-for-posted-service-documents" />Visa statistik för bokförda servicedokument
Med funktionen för servicestatistik får du en statistisk översikt över innehållet i bokförda servicedokument, t. ex. bokförda leveranser, bokförda fakturor och bokförda kreditnotor.  

Statistikinformationen visas på statistiksidan för varje bokfört servicedokument. Du kan öppna relevant statistik från sidan med den bokförda serviceleveransen, bokförd servicefaktura eller bokförd servicekreditnota. Välj åtgärden **Statistik** för var och en av dessa dokumenttyper. Exempelvis från sidan **Bokförda servicefakturor** väljer du åtgärden **Statistik**.  

### <a name="posted-service-shipment-statistics" />Statistik för bokförda serviceleveranser
På sidan **Serviceleveransstatistik** visas en översikt över den bokförda serviceleveransen. Detta inkluderar information om det fysiska innehållet i utleveransen, t. ex. antalet levererade artiklar, resurstimmar eller kostnader samt vikt och volym för de levererade artiklarna.  

### <a name="posted-service-invoice-statistics" />Statistik för bokförda servicefakturor
Du kan se en statistisk översikt för en bokförd faktura på sidan **Servicefakturastatistik**. Du kan visa alla summor på den bokförda servicefakturan. Datan inkluderar det totala beloppet på de servicerader (inkl. och exkl. moms) som har bokförts som fakturerade, momsandel, kostnad och vinst på den bokförda fakturan. Sidan visar även information om följande:  

* Artiklarna på servicefakturaraderna, till exempel vikt, volym och antalet förpackningar.  
* Saldot på kundens konto samt den maximala kredit som kan utökas till kunden.  

### <a name="posted-service-credit-memo-statistics" />Statistik för bokförda servicekreditnotor
Du kan använda sidan **Statistik för servicekreditnota** för att visa en statistisk översikt över raderna i en bokförd servicekreditnota. Översikten kan inkludera följande:

* De totala beloppen på den bokförda kreditnotan, som antal, belopp, moms, kostnad och vinst. Det finns också specifik information om artiklarna på serviceraderna i den bokförda kreditnotan, t. ex. antal, vikt och volym.  
* Allmän information om kunden, d.v.s. kundens kreditlimit och saldo för kontot.  

## <a name="see-also" />Se även
[Skapa tjänsteorder](service-how-to-create-service-orders.md)   
[Skapa tjänsteartiklar](service-how-to-create-service-items.md)   
[Planera service](service-plan-service.md)  


[!INCLUDE[footer-include](includes/footer-banner.md)]
