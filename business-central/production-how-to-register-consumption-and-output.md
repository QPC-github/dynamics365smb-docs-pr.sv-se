---
title: Registrera förbrukningsutflöde för produktionsorder
description: I det här avsnittet beskrivs hur du registrerar förbrukning och utflöde för en släppt produktions orderrad som visas på produktionsjournal sidan.
author: SorenGP
ms.topic: conceptual
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.search.form: 5510
ms.date: 03/08/2023
ms.author: edupont
---
# <a name="register-consumption-and-output-for-one-released-production-order-line" />Så här registrerar du förbrukning och utflöde för en utsläppt produktionsorderrad

Den här uppgiften utförs på sidan **Produktionsjournal**. I journalen kombineras funktionerna hos de skilda förbruknings- och utflödesjournalerna. Den kombinerade journalen kan öppnas direkt från en släppt produktionsorder. Huvudsyftet med journalen är att komponentförbrukning, antalet slutartiklar som har producerats och den tid som går åt under operationer ska kunna bokföras manuellt. Värdena bokförs i transaktioner under den släppta produktionsordern. förbrukningskvantiteter bokförs som negativa artikeltransaktioner, utdatakvantiteter bokförs som positiva transaktion och åtgången tid bokförs som kapacitetstransaktioner. Dessa bokförda värden visas också längst ned i journalen som faktiska kvantiteter.  

> [!NOTE]  
> Eftersom förbrukningsinformation hanteras tillsammans med utdata kan du i den här journalen visa länkade komponenter och operationer i en logisk processtruktur. komponenterna visas på indragna rader under respektive operation. Detta kan ske under förutsättning att du använder verksamhetsföljdslänkkoder.  

> [!NOTE]  
> Komponenter som saknar operationsföljdslänkkoder visas först i listan i journalen.  

## <a name="to-register-consumption-and-output" />Så här registrerar du förbrukning och utdata

1. Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta för mig vad du vill göra") anger du **utsläppta produktionsorder** och väljer sedan relaterad länk.  
2. Öppna en släppt produktionsorderrad som är klar för registrering. På snabbfliken **Rader** klickar du på **Rader** och väljer sedan åtgärden **Produktionsjournal**.  

    Sidan **Produktionsjournal** öppnas med journalrader för produktionsorderraden enligt sidorna **Prod.orderkomponent** och **Prod.orderverksamhetsföljd**. Dessa rader kommer från den produktionsstruktur och verksamhetsföljd som tilldelats artikeln som produceras. För mer information, se [Skapa produktionsstrukturer](production-how-to-create-routings.md).  

3. I fältet **Bokföringsdatum** högst upp i journalen anger du ett bokföringsdatum som gäller för alla rader. Arbetsdatumet anges som standard. Fältet gör att du snabbt kan samordna bokföringsdatum för alla rader, om det behövs.  

    > [!NOTE]  
    >  Om bokföringsdatum anges på en enskild rad så åsidosätter det värdet i det här fältet för den raden.  

4. I fältet **Filter för rensningsmetod** längst upp i journalen kan du välja om du också vill visa förbrukning och utdata som bokförs automatiskt enligt de bokföringsmetoder som har angetts för artikeln respektive resursen. Mer information finns i [Tillåta bokföring av komponenter enligt operationens utflöde](production-how-to-flush-components-according-to-operation-output.md).

5. Fortsätt med att ange relevanta kvantiteter för förbrukning och utflöde i de fält som kan redigeras.  
  
    För varje typ av rad i journalen visas endast de relevanta fälten. Resten är tomma och skrivskyddade.  

    När journalen öppnas visas förinställda kvantiteter som ska bokföras. Om ingenting har bokförts ännu visas de förväntade kvantiteter som har överförts från produktionsordern som standard. Om en del bokföring har utförts visas de återstående kvantiteterna i kvantitetsfälten. De kvantiteter och tidsvärden som redan har bokförts för ordern visas längst ned i journalen som faktiska transaktioner.  

    Vad gäller kvantiteterna i fältet **Utflöde antal** kan du välja att ange vilka värden som ska vara förinställda när du öppnar journalen första gången. Detta gör du i fältet **Förinställd utleveranskvantitet** på snabbfliken **Allmänt** på sidan **Produktionsinställningar**.

    > [!NOTE]  
    >  Bara utflödesantalet på den sista journalraden av transaktionstypen **Utflöde** kommer att justera lagernivån när journalen bokförs. Du bör därför inte bokföra journalen (med den förväntade utdatakvantiteten förinställd på den sista utflödesraden) förrän alla slutartiklar faktiskt har producerats.  

6. Markera fältet **Avslutad** för utdatarader för att visa att operationen är avslutad. Det här fältet är kopplat till fältet **Flödesstatus** på en verksamhetsföljdrad för en produktionsorder.  
7. Välj åtgärden **Bokföra** när du vill registrera de kvantiteter som du har angett och stänga journalen.  

    [!INCLUDE [preview-posting-inventory](includes/preview-posting-inventory.md)]

    Om värdena som återstår ska bokföras kommer journalen att innehåller dessa återstående värden nästa gång den öppnas. Bokfört värde visas som faktiskt värde längst ned i journalen.  

    > [!NOTE]  
    >  Om en artikel som förbrukas är spärrad så bokförs inte förbrukningskvantiteter för artikeln. Om en maskingrupp eller produktionsgrupp är spärrad så bokförs inte utdatakvantiteter eller processtider för den aktuella utdataraden.  

    > [!NOTE]  
    > Om du stänger journalen utan att bokföra så går alla ändringar förlorade.  

> [!WARNING]  
> Sidan **Produktionsjournal** kan inte användas av två användare samtidigt. Det innebär att om användare 2 öppnar sidan och registrerar data när användare 1 redan arbetar på sidan kan användare 2 förlora data när användare 1 stänger sidan.  

## <a name="see-also" />Se även

[Produktion](production-manage-manufacturing.md)  
[Ställa in Produktion](production-configure-production-processes.md)  
[Planerad](production-planning.md)  
[Lager](inventory-manage-inventory.md)  
[Inköp](purchasing-manage-purchasing.md)  
[Arbeta med [!INCLUDE[prod_short](includes/prod_short.md)]](ui-work-product.md)

[!INCLUDE[footer-include](includes/footer-banner.md)]
