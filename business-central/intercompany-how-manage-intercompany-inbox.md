---
title: Hantera koncerninterna in- och utkorgar
description: Koncerninterna transaktioner som du tar emot från dina koncerninterna partner visas i den koncerninterna inkorgen där du behandlar dem manuellt eller automatiskt.
author: brentholtorf
ms.author: bholtorf
ms.reviewer: bnielse
ms.topic: conceptual
ms.date: 02/06/2023
ms.custom: bap-template
ms.search.keywords: incoming document
ms.search.form: '600, 605, 618, 650, 651, 648, 649, 617, 614, 642, 643, 640, 641, 613, 616, 646, 647, 644, 645, 615, 619, 612, 638, 639, 636, 637, 611'
---
# <a name="manage-the-intercompany-inbox-and-outbox" />Hantera koncerninterna in- och utkorgar

Koncerninterna transaktioner som du tar emot från dina koncerninterna partner visas i den **koncerninterna inkorgen**. Om du vill veta hur du behandlar inkommande koncerninterna transaktioner går du till [Behandla inkommande koncerninterna transaktioner](#process-incoming-intercompany-transactions). Koncerninterna transaktioner som du skickar till partner visas i den **koncerninterna utkorgen**. Om du vill veta hur du behandlar utgående koncerninterna transaktioner går du till [Behandla utgående koncerninterna transaktioner](#to-process-outgoing-intercompany-transactions).

Vissa transaktioner hanteras dock automatiskt beroende på de koncerninterna inställningarna. Du kan ställa in källföretaget och partner företagen så att de automatiskt skapar dokument och journaler som motsvarar transaktioner som företag skickar via den koncerninterna redovisningsjournalen. Om du vill lära dig mer om koncerninterna journaler går du till [Fyll i och bokför en koncernintern journal](intercompany-how-work-documents-journals.md#fill-in-and-post-an-intercompany-journal).  

## <a name="organizing-the-inbox" />Ordna inkorgen

Du kan använda filterfälten överst i inkorgen när du vill fastställa vilka transaktioner som ska visas på sidan. Om du till exempel bara vill utforska transaktioner som en viss partner skapat, använd filter **transaktionskälla** och **Kod för koncernintern partner**.  

### <a name="transaction-source" />Transaktionskälla

Vad du kan göra med en transaktion beror på om den har:  

* skapats av en koncernintern partner  
* avvisats av den koncerninterna partnern och returnerats till dig  

Du kan använda fältet **Visa transaktionskälla** om du vill filtrera sidan **Koncerninterna inkorgstransaktioner** så att endast dessa typer av transaktioner visas. Du kan även filtrera efter koncerninterna partner eller efter innehållet i fältet **Radåtgärd**.  

#### <a name="created-by-intercompany-partner" />Skapats av en koncernintern partner

 När du får en ny transaktion som har skapats av din partner kan du välja att:

* Acceptera transaktionen  
* Avvisa transaktionen (returnera den till partnern)  
* Avbryta transaktionen (ta bort transaktionen utan att returnera den till partnern)  

#### <a name="returned-from-intercompany-partner" />Returnerad från koncernintern partner

Om din koncerninterna partner avvisar en transaktion måste du avbryta transaktionen i inkorgen och sedan skapa korrigeringsrader eller återföra journalen eller dokumentet.  

## <a name="recreating-inbox-entries" />Återskapa poster i inkorgen

Om du har accepterat en transaktion i inkorgen men därefter tagit bort dokumentet eller journalen i stället för att bokföra den kan du återskapa posten i inkorgen och acceptera den på nytt.  

## <a name="get-an-overview-of-intercompany-transactions-for-a-period" />Skaffa en översikt över koncerninterna transaktioner för en period

Du kan skapa en översikt över alla koncerninterna transaktioner som du har skickat och tagit emot under en period. I rapporten **Konc.int. transaktioner** visas alla koncerninterna redovisningstransaktioner, kundreskontratransaktioner och leverantörsreskontratransaktioner.

> [!NOTE]  
> Om de koncerninterna partnerna finns i samma databas kan partner acceptera transaktioner automatiskt. Gå direkt till sidan **hanterade koncerninterna inkorgstransaktioner** och **hanterade koncerninterna utkorgstransaktioner**. Om du vill veta mer om automatiskt godtagna transaktioner går du till [Automatiskt godtagande av transaktioner från koncerninterna partner](intercompany-how-setup.md#auto-accept-transactions-from-intercompany-partners).  
>
> * På sidan **Koncernintern inställning** aktivera växlingen **Automatiskt skicka transaktioner** för synkroniseringspartner.
> * För partnerföretag, på sidan **Koncernintern partner** aktiverar du växlingen **Acceptera transaktioner automatiskt**.  

## <a name="import-intercompany-transactions-from-a-file" />Importera koncerninterna transaktioner från en fil

[!INCLUDE [onprem_only_md](includes/onprem_only_md.md)]

Om du har en koncernintern partner som inte finns i samma databas som ditt företag kan du ta emot koncerninterna transaktioner från den partnern i en XML-fil. Därefter måste du importera transaktionerna till inkorgen.  

1. Spara filen på den plats som du har angett i fältet **Koncerninterna detaljer för inkorg** när du konfigurerar koncerninterna aspekter.  
2. Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta för mig vad du vill göra") anger du **koncerninterna inkorgstransaktioner** och väljer sedan relaterad länk.
3. På sidan **koncerninterna inkorgstransaktioner** väljer du åtgärden **Importera transaktionsfil**.  
4. På sidan som visas markerar du XML-filen med transaktionerna och sedan väljer du **Öppna**.  

Transaktionerna importeras till inkorgen där du kan bearbeta dem.

## <a name="process-incoming-intercompany-transactions" />Hantera inkommande koncerninterna transaktioner

När koncerninterna partner skickar koncerninterna transaktioner hamnar de i den koncerninterna inkorgen. Du måste utvärdera varje transaktion i inkorgen och välja lämplig åtgärd.  

1. Välj ![glödlampan som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta för mig vad du vill göra") anger du **koncerninterna inkorgstransaktioner** och väljer sedan relaterad länk.  
2. På sidan **koncerninterna inkorgstransaktioner** markerar du en rad, och väljer sedan en åtgärd som **acceptera** för att bearbeta raden.
3. På sidan **Slutför konc.int. inkorgsåtg.** fyller du i fälten efter behov. [!INCLUDE[tooltip-inline-tip](includes/tooltip-inline-tip_md.md)]
4. Välj **OK**.  

För rader som du accepterar skapas dokument- eller journalrader i ditt företag. Öppna varje dokument eller journal, gör nödvändiga ändringar och bokför.  

Rader som du avvisar och återgår till partnern går till din koncerninterna utkorg, där du kan skicka dem till partnern.

För rader som en partner avvisat och returnerat till dig måste du bokföra en korrigering av den ursprungliga transaktionen som du har bokfört i företaget.

## <a name="to-process-outgoing-intercompany-transactions" />Så här hanterar du utgående koncerninterna transaktioner

När du bokför en koncernintern journal eller ett koncerninternt dokument, eller när du skickar en koncernintern orderbekräftelse, skickas transaktionerna till den koncerninterna utkorgen. Du måste öppna utkorgen och bearbeta dem för att de ska skickas till dina koncerninterna partner.  

1. Välj ![glödlampan som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta för mig vad du vill göra") anger du **koncerninterna utkorgstransaktioner** och väljer sedan relaterad länk.  
2. På sidan **koncerninterna utkorgstransaktioner** markerar du en rad, och väljer sedan en åtgärd som **Returnera till inkorgen** för att bearbeta raden.

Använd åtgärden **Skicka till en koncernintern partner** för att skicka rader till lämplig partners inkorg.

Använd åtgärden **returnera till inkorgen** för att flytta rader till inkorgen där du kan acceptera dem för att skapa dokument- eller journalrader i företaget.  

Om du använder åtgärden **Avbryt** bokför du en korrigering av den ursprungliga transaktionen som du har bokfört i företaget.  

## <a name="recreate-intercompany-inbox-transactions" />Återskapa koncerninterna inkorgstransaktioner

Ibland kan du behöva återskapa en transaktion i inkorgen eller utkorgen. Om du till exempel har accepterat en transaktion i inkorgen men sedan tagit bort dokumentet eller journalen i stället för att bokföra den, kan du återskapa posten i inkorgen och acceptera den på nytt.  

Den här proceduren beskriver hur du återskapar inkorgstransaktioner, men det fungerar på samma sätt i utkorgen.

1. Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta vad du vill göra") anger du **Hanterade konc.int. inkorgstransaktioner** och väljer sedan relaterad länk.  
2. På sidan **Hanterade konc.int. inkorgstransaktioner** markerar du raden med den transaktion som du vill återskapa i inkorgen och väljer sedan åtgärden **Återskapa inkorgstransaktion**.  

## <a name="see-also" />Se även

[Hantera koncerninterna transaktioner](intercompany-manage.md)  
[Ekonomi](finance.md)  
[Ställa in Finance](finance-setup-finance.md)  
[Arbeta med redovisningsjournaler](ui-work-general-journals.md)  
[Arbeta med [!INCLUDE[prod_short](includes/prod_short.md)]](ui-work-product.md)


[!INCLUDE[footer-include](includes/footer-banner.md)]
