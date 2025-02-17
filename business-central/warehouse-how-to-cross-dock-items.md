---
title: Beräkna direktutleverans av artiklar
description: Direktutleveransfunktionen är tillgänglig om lagerstället kräver inleverans- och artikelinförselbearbetning.
author: SorenGP
ms.topic: conceptual
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.search.keywords: null
ms.search.form: '15, 5703, 7302, 7332, 5768'
ms.date: 04/01/2021
ms.author: edupont
---
# <a name="cross-dock-items" />Beräkna direktutleverans av artiklar

Artiklar för direktutleverans är artiklar som du tar emot och levererar utan att de tas bort. Processerna för artikelinförsel och plockning kräver begränsad hantering av artiklar. Du kan direktutleverera artiklar för utleveranser och för produktionsorder.

## <a name="cross-dock-bins-and-zones" />Lagerplatser och zoner för direktutleverans

Om du använder lagerplatser registrerar du minst en lagerplats för direktutleverans och anger lagerplatsen i fältet **Direktutleverans lagerställeskod** på lagerställena. Om du använder dirigerad artikelinförsel och plockning ställer du in en zon för direktutleverans.

När du förbereder en utleverans eller plockar artiklar i produktionssyfte, och använder lagerställen, plockas artikeln automatiskt från en lagerplats för direktutleveranser före någon annan lagerplats. Du måste kontrollera området för direktutleveranser och se om de artiklar som behövs är tillgängliga där, innan du hämtar artiklarna från det vanliga lagringsområdet.  

Om du har beräknat kvantiteter för direktutleverans, skapas automatiskt artikelinförselrader i lagerstället för direktutleveranser för beräkning av direktutleveranser när inleveransen bokförs. Övriga artikelinförselrader skapas som vanligt.  

## <a name="cross-dock-select-lines-for-a-receipt" />Direktutleverans markera rader för en inleverans

<!--If a receipt contains items that you want to store, that is, items that you are not cross-docking, you must register a put-away for those items.-->

Om du vill bokföra artiklarna för direktutleverans direkt, så att de blir tillgängliga för plockning, måste du även registrera en artikelinförsel för de övriga artiklarna som kommer från inleveransraden, nämligen de som måste lagras. Om endast några av artiklarna på en inleveransrad direktutlevereras måste du därför försöka införa de återstående artiklarna så snabbt som möjligt. Alternativt kan lagerprincipen vara att uppmuntra direktutleverans av hela inleveransrader närhelst det är möjligt.

I instruktionen för artikelinförsel tar du bort instruktionsraderna för ta och placera för varje inleveransrad för artiklarna som ska föras in. Du kan återskapa instruktionsraderna senare eftersom artikelinförselrader från artikelinförselförslaget eller den bokförda inleveransen. När du har tagit bort instruktionsraderna kan du föra in och registrera raderna för artiklar för direktutleverans.  

## <a name="about-the-put-away-worksheet-page" />Om artikelinförselförslag

Om du aktiverar växlingsknappen **Använd artikelinförselkalkylark** på sidan Lagerställekort och bokförde inleveransen med beräknade direktutleveranser, blir samtliga inleveransrader tillgängliga i kalkylarket. Informationen om direktutleveranserna försvinner och kan inte återskapas. Därför bör du, om du vill använda funktionerna för direktutleverans, lägga om rader till artikelinförselkalkylarket genom att ta bort instruktioner för artikelinförseln i stället för att använda motsvarande automatiska funktion i fältet **Använd artikelinförselkalkylark**.  

Om du bokför lagerinleveransen, och växlingsknappen **Använd artikelinförselkalkylark** är inaktiverad, visas artiklarna som ska direktutlevereras som separata rader i artikelinförselinstruktionen. Fältet **Direktutleverans information** på varje artikelinförselrad visar om raden innehåller följande:

* Direktutleverans av artiklar.
* Alla artiklar från en inleverans måste lagras.
* En del artiklar från en inleverans måste lagras och en del ska direktutlevereras.

Anställda kan enkelt förstå varför hela kvantiteten inte har förts in i lager.  

[!INCLUDE [prod_short](includes/prod_short.md)] behåller inga separata poster för direktutlevererade artiklar men registrerar dem som vanliga artikelinförselinstruktioner.  

## <a name="to-set-up-the-warehouse-for-cross-docking" />Så här konfigurerar du lagret för direktutleveranser:

1. Ange minst en lagerplats för direktutleverans, om du använder lagerplatser. Om du använder dirigerad artikelinförsel och plockning ställer du in en zon för direktutleverans.  

    En direktutleveranslagerplats har **Direktutlevns lagerplats** fältet markerat och måste ha både **Inleverera** och **Plockning** lagerplatstyper valda. Mer information finns i [Skapa lagerställen](warehouse-how-to-create-individual-bins.md) och [Skapa lagerplatstyper](warehouse-how-to-set-up-bin-types.md).  

    Om du använder zoner, skapa en zon för dina direktutleveranslagerställen och välj **Direktutlevns lagerplatszon** fältet. Mer information finns i [Skapa lagerställen för att använda lagerställen](warehouse-how-to-set-up-locations-to-use-bins.md).  

2. Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta för mig vad du vill göra") anger du **Plats** och väljer sedan relaterad länk.  
3. På sidan **Lagerställe** väljer du vilket lagerställe som du vill ställa in direktutleverans för och väljer sedan åtgärden **Redigera**.  
4. På snabbfliken **Distributionslager** på växlingsknappen **Använd direktutleverans** och fyll i fältet **Direktutlev. förfalloberäkning** med tidsperiod att söka efter direktutleveransmöjligheter.

    Alternativet **Använd direktutleverans** är bara tillgängligt om du har markerat fälten **Begär inleveranser**, **Begär utleverans**, **Begär plockning** och **Begär artikelinförsel**.  

5.  Om du använder lagerställen fyller du i fältet **Direktutleverans lagerställeskod** på snabbfliken **Lagerställen** med koden för den lagerplats du vill använda som standardlagerplats för direktutleveranser.  
6.  Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta för mig vad du vill göra") anger du **Lagerställeenhet** och väljer sedan relaterad länk.  
7.  För varje artikel eller lagerställeenhet som du vill kunna direktutleverera till markerar du artikeln och väljer åtgärden **Redigera**.
8. På sidan **lagerställeenhetskort** markerar du kryssrutan **Använd direktutleverans**.  

> [!NOTE]  
>  Du kan bara använda direktutleveranser om lagerstället är inställt på inleverans- och artikelinförselbearbetning för distributionslagret.  

## <a name="to-cross-dock-items-without-viewing-the-opportunities" />Så här direktutlevererar du artiklar utan att visa möjligheterna:
1.  Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta för mig vad du vill göra") anger du **Dist.lager inleveranser** och väljer sedan relaterad länk.  
2.  Skapa distributionslagerinleverans för en artikel som har anlänt och som eventuellt kan komma att direktutlevereras. Mer information finns i [Ta emot artiklar](warehouse-how-receive-items.md).  
3.  Fyll i fältet **Ant. att inlevereras** och välj åtgärden **Beräkna direktutleverans**.  

    utgående ursprungsdokument som söker efter de artiklar som inplanerats att lämna lagret inom angiven tidsperiod identifieras.  [!INCLUDE[prod_short](includes/prod_short.md)] beräknar antal så att du kan direktutleverera så mycket som möjligt och undvika att införa artiklar, men utan att alltför många artiklar samlas i direktutleveransområdet. Värdet i fältet **Ant. för direktutlevns** utgör således summan av alla utgående rader som begär artikeln inom angiven tidsperiod minus det artikelantal som redan har placerats i området för direktutleveranser, eller så är det värdet i fältet **Ant. att inlevereras** på inleveransraden, beroende på vilket som är lägst. Du kan inte direktutleverera mer än vad som har inlevererats.  

4.  Om du vill direktutleverera föreslaget antal bokför du inleveransen. Du kan också välja att ändra antalet till ett högre eller lägre värde och därefter bokföra inleveransen.  

    Det antal som ska direktutlevereras visas nu som rader i artikelinförselinstruktionen, förutsatt att fältet **Använd artikelinförselkalkylark** inte är markerat. Icke direktutlevererade kvantiteter resulterar också i rader i artikelinförselinstruktionen.  

    Om du använder lagerställen har de direktutlevererade artiklarna tilldelats den standardlagerplats för direktutleveranser som angetts på lagerställekortet.  

5.  Ta bort raderna **Ta** och **Placera** för artiklar som inte ska direktutlevereras överhuvudtaget.  
6.  Skriv ut artikelinförselinstruktionen för återstående rader och placera det antal av inleveransen som ska lagras på lämpliga lagerställen eller i lämpligt lagerområde. Placera artiklarna för direktutleverans i lämpligt område eller lagerplats enligt gällande lagerprincip. Ibland kan det krävas att de bara ska lämnas i inleveransområdet.  
7.  Välj åtgärden **Registrera** för att registrera de direktutlevererade artiklarna som införda och tillgängliga för plockning.  

## <a name="to-cross-dock-items-after-viewing-the-opportunities" />Så här direktutlevererar du artiklar när du har visat möjligheterna:
1.  Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta vad du vill göra") anger du **Dist.lager inleveranser** och väljer sedan relaterad länk.  
2.  Skapa distributionslagerinleverans för en artikel som har anlänt och som eventuellt kan komma att direktutlevereras. Mer information finns i [Ta emot artiklar](warehouse-how-receive-items.md).  

    Du vill visa källdokumentrader som kräver artikeln innan du bokför Inleveransen.  
3.  Välj åtgärden **Beräkna direktutleverans**.  

    PÅ sidan **Direktutleveransmöjligheter** visas de viktigaste detaljerna om raderna som begär artikeln, t. ex. dokumenttyp, begärt antal och förfallodatum. Med hjälp av den här informationen kan du enklare bestämma hur mycket som ska direktutlevereras, var artiklarna ska placeras i området för direktutleveranser och hur de ska grupperas.  

4.  Välj **Autofyll Ant. för direktutlevns** för att visa hur antalen på inleveransraderna har beräknats. När du ändrar antalet artiklar i **Ant. för direktutlevns** på varje rad uppdateras beräkningen när du ändrar. Detta innebär dock inte att artiklarna som föreslås för direktutleverans kommer att inkluderas i utleveransen eller på produktionsordern i fråga, eftersom dessa modifikationer endast utförs i testsyfte. Processen kan emellertid ge viktig information i de fall flera enheter är inbegripna.  
5.  Om du vill reservera en kvantitet av artikeln för en viss orderrad placerar du markören på raden och väljer sedan åtgärden **Reservera**. På sidan **Reservation** kan du nu reservera tillgänglig kvantitet av artikeln för den ordern. Reservationen är som andra reservationer och har ingen högre prioritet för att den skapades med direktutleverans. Mer information finns i [Reservera artiklar](inventory-how-to-reserve-items.md).   
6.  När du har utfört önskade beräkningar eller reservationer klickar du på knappen **OK** för att infoga den slutgiltiga beräkningen i fältet **Ant. för direktutlevns** på inleveransraden. Alternativt klickar du på knappen **Avbryt** om du vill gå tillbaka till lagerinleveransen för att beräkna direktutleveransen på nytt.  
7.  Bokför nu inleveransen, och du kan fortsätta i artikelinförselinstruktionen enligt beskrivningen i steg 3 till 7 i avsnittet Så här direktutlevererar du artiklar utan att visa möjligheterna.  

> [!NOTE]  
>  Vid lagerartikelinförseln kan du fortsätta att ändra antalet artiklar som direktutlevereras eller förs in i lager alltefter behov. Till exempel kanske du bestämmer dig för att direktutleverera ytterligare artiklar för att expediera registreringen av direktutleveransen.  

## <a name="to-view-cross-docked-items-in-a-shipment-or-pick-worksheet" />Så här visar du direktutlevererade artiklar i utleveranser eller plockningskalkylark
Om du använder lagerställen kan du, när du öppnar en utleverans eller plockningskalkylarket, visa en uppdaterad beräkning av antalet av respektive artikel som finns på lagerställena för direktutleveranser. Den här informationen är praktisk om du väntar på att en artikel ska anlända. När du ser att artikeln är tillgänglig på lagerstället för direktutleveranser kan du sedan snabbt skapa en plockning för alla artiklarna i utleveransen. I plockningskalkylarket kan du ändra raderna alltefter behov och därefter skapa en plockning.  

Du måste först leta efter artiklar i området för direktutleveranser när du plockar artiklar för en utleverans. Om du under inleveransprocessen vet vilka källdokument som ligger till grund för direktutleveransen kan du lättare avgöra huruvida artikeln kan återfinnas i området för direktutleveranser eller inte.  

När en produktionsorder har släppts är raderna tillgängliga i plockningskalkylarket och du kan, i fältet **Ant. på direktutlevns lagerplats**, se om artiklarna du väntar på har anlänt och placerats på lagerställena för direktutleveranser. När du skapar en plockningsinstruktion föreslås automatiskt att du först plockar artiklarna för direktutleverans på motsvarande lagerställen. Först därefter genomsöks övriga lagerställen efter artikeln.  

Om du inte använder lagerställen måste du komma ihåg att då och då kontrollera området för direktutleveranser eller förlita dig på meddelanden från inleveranser om att artiklar för produktion har anlänt.  

## <a name="see-also" />Se även
[Lager](inventory-manage-inventory.md)  
[Ställa in Warehouse Management](warehouse-setup-warehouse.md)     
[Monteringshantering](assembly-assemble-items.md)    
[Warehouse Management – översikt](design-details-warehouse-management.md)
[Arbeta med [!INCLUDE[prod_short](includes/prod_short.md)]](ui-work-product.md)  


[!INCLUDE[footer-include](includes/footer-banner.md)]
