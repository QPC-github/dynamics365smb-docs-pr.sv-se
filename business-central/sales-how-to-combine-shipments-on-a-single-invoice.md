---
title: Så här kombinerar du leveranser på en enda faktura | Microsoft Docs
description: Om du vill fakturera mer än en leverans åt gången kan du använda funktionen för kombinerade leveranser.
author: SorenGP
ms.topic: conceptual
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.search.keywords: null
ms.date: 12/16/2021
ms.author: edupont
---
# <a name="combine-shipments-on-a-single-invoice" />Kombinera leveranser på en enda faktura

Om du vill fakturera mer än en leverans åt gången kan du använda funktionen för kombinerade leveranser.  

Innan du kan skapa en kombinerad leverans måste mer än en leverans till samma kund och i samma valuta ha bokförts. Med andra ord måste du ha skapat minst två försäljningsorder och bokfört dem som levererade, men inte fakturerade. 

## <a name="to-manually-combine-shipments-on-a-single-invoice" />Så här kombinerar du utleveranser manuellt på en enda faktura

1. Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta för mig vad du vill göra") anger du **försäljningsfakturor** och väljer sedan relaterad länk.  
2. Välj åtgärden **Ny**. Mer information finns i [Så här fakturerar du försäljningsaktiviteter](sales-how-invoice-sales.md).
3. I fältet **Förs.kundnr.** Ange den kund som ska få fakturan för de levererade artiklarna, i fältet.  
4. På snabbfliken **Rader** klickar du på åtgärden **Hämta utleveransrader**.  
5. Markera den leveransrad som ska inkluderas på fakturan:  

    - Markera alla rader och klicka på **OK** om du vill infoga alla rader.  
    - Markera raderna i fråga och klicka på **OK** om du vill infoga särskilda rader. Du kan använda CTRL-tangenten om du vill markera flera rader som inte är i följd.  

    Om du har markerat fel leveransrad eller om du vill börja om kan du ta bort raderna på fakturan och köra funktionen **Hämta leveransrader** på nytt.  
7. Om du vill bokföra fakturan väljer du åtgärden **Bokför**.  

> [!TIP]  
> Om du har levererat order där du fyller i fältet **Försäljningskundnr.** Skiljer sig från **Faktureringskundnr.**, visas inte raderna i rapporten **Hämta leveransrader**. Använd anpassning för att lägga till fältet **Försäljningskund** och ta bort filtret. Nu kan du lägga till leverans rader på fakturan oavsett värdet i fältet **Försäljningskundnr.** Om du vill använda fältet **Faktureringskundnr.** Fältet på leverans raderna matchar värdet på försäljningsfakturan.  

## <a name="to-automatically-combine-shipments-on-a-single-invoice" />Så här kombinerar du utleveranser automatiskt på en enda faktura

[!INCLUDE[prod_short](includes/prod_short.md)] väljer endast de försäljningsorder där **Kombinera leveranser** har valts. 

1. Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta för mig vad du vill göra") anger du **Kombinera leveranser** och väljer sedan relaterad länk. Sidan för begäran om batch-jobb öppnas.  
2. Fyll i fälten om det behövs. [!INCLUDE[tooltip-inline-tip](includes/tooltip-inline-tip_md.md)]
3. Markera kryssrutan **Bokför fakturor**.  
4. Välj **OK**.  

> [!NOTE]  
>  Fakturorna måste bokföras manuellt om du inte har markerat kryssrutan **Bokför fakturor** för batch-jobbet.  

## <a name="to-remove-open-sales-orders-after-combined-shipment-posting" />Så här tar du bort öppna försäljningsorder efter kombinerad utleveransbokföring

När utleveranser kombineras på en faktura och bokförs, skapas en bokförd försäljningsfaktura för de fakturerade raderna. Innehållet i fältet **Fakturerat antal** på den ursprungliga avropsordern eller försäljningsordern uppdateras utifrån det fakturerade antalet.  

När du fakturerar leveranser på det här sättet finns de order som leveranserna bokfördes från kvar, även om de har levererats och fakturerats i sin helhet.   

1. Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta för mig vad du vill göra") anger du **Ta bort fakturerade försäljningsorder** och väljer sedan länken.  
2. Fälten **Serienr** . vilka försäljningsorder som ska tas bort.  
3. Välj **OK**.  

Du kan också ta bort enskilda försäljningsorder manuellt.  

Upprepa steg 1 till 3 för alla andra berörda dokument, till exempel försäljningsavropsorder.

## <a name="see-related-microsoft-trainingtrainingmodulesinvoicing-customers-dynamics-365-business-central" />Se relaterad [Microsoft utbildning](/training/modules/invoicing-customers-dynamics-365-business-central/)

## <a name="see-also" />Se även

[Försäljning](sales-manage-sales.md)  
[Arbeta med [!INCLUDE[prod_short](includes/prod_short.md)]](ui-work-product.md)


[!INCLUDE[footer-include](includes/footer-banner.md)]
