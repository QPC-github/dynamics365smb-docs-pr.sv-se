---
title: Koppla betalningar till dokument för obetalda försäljningar
description: 'Du tillämpar belopp betalda av kunder till relaterade försäljningsdokument och bokför betalningen för att uppdatera kund, redovisning och banktransaktioner.'
author: SorenGP
ms.topic: conceptual
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.search.keywords: 'payment process, cash receipts, customer payment'
ms.search.form: '1290, 1294, 1287'
ms.date: 04/01/2021
ms.author: edupont
---
# <a name="reconcile-customer-payments-from-a-list-of-unpaid-sales-documents" />Så här stämmer du av kundutbetalningar från en lista med obetalda försäljningsdokument

När kunderna utför elektroniska betalningar till ditt bankkonto måste du utföra följande åtgärder:

* Koppla varje betalat belopp till det relaterade försäljningsdokumentet
* Bokför betalningen för att uppdatera kunden, redovisningen och bankkontotransaktioner. 

Beroende på ditt företagsbehov kan du få betalt och registrera den betalningen på olika sätt: manuellt, automatiskt eller via betalningstjänster.  

> [!NOTE]  
> Du kan utföra samma uppgifter inklusive leverantörsbetalningar på sidan **Utbetalningavstämningsjournal** med hjälp av funktioner för bankutdragsimport, automatiskt koppling och bankkontoavstämning. Mer information finns i [Stämma av betalningar genom att använda automatisk koppling](receivables-how-reconcile-payments-auto-application.md).

Använd sidan **Registrera kundbetalningar** för att balansera interna konton genom att använda faktiska kontantsiffror för att säkerställa att betalningar samlas in. Du kan snabbt kontrollera och bokföra enskilda betalningar eller betalningar av klumpsumma, hantera rabatterade betalningar och hitta de obetalda dokumenten.

Betalningar för olika kunder som har olika betalningsdatum, ska bokföras som individuella betalningar. Betalningar till samma kund som har samma betalningsdatum, kan bokföras som en klumpbetalning. Betalningar av klumpsumma är användbara, till exempel, när en kund har skapat en enkel betalning som täcker åtskilliga försäljningsfakturor.

## <a name="to-set-up-the-payment-registration-journal" />Så här lägger du upp betalningsregistreringjournal
Eftersom du kan bokföra olika betalningstyper till olika motkonton måste du välja ett motkonto på sidan **Inställning av betalningsregistrering** innan du börjar att behandla kundbetalningar. Om du alltid bokför samma motkonto, kan du ange det konto som standard och undvika detta steg varje gång som du öppnar sidan **Registrera kundbetalningar**.  

1. Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta för mig vad du vill göra") anger du **Inställning av betalningsregistrering** och väljer sedan relaterad länk. Du kan även välja åtgärden **Inställning** på sidan **Registrera kundbetalningar**.
2. Fyll i fälten på sidan **Inställning av betalningsregistrering**. [!INCLUDE [tooltip-inline-tip_md](../archive/SetupAndAdministration/includes/tooltip-inline-tip_md.md)] Välj ett fält om du vill få en kort beskrivning av fältet eller länken till relaterad information.  

> [!TIP]
> Om du vill göra det lättare att senare identifiera transaktioner som har bokförts via journalen, kan du tilldela en specifik nummerserie till journalen. Detta är användbart om du använder betalningsavstämningsjournaler för att registrera och koppla betalningar.

## <a name="to-register-customer-payments-individually" />Registrera kundbetalningar individuellt.

1. Välj ![glödlampan som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta för mig vad du vill göra") anger du **Registrera kundbetalningar** och väljer sedan relaterad länk.  

    Sidan **registrera kundbetalningar** visar alla bokförda dokument som en betalning kan registreras för. Sidan kan även öppnas från sidorna **Kunder** och **Kundkort** där den filtreras automatiskt för den angivna kunden.  
2. Markera kryssrutan **Utförd betalning** på raden som representerar bokfört dokument som en betalning har gjorts för.

    Om kryssrutan **Fyll i Tillbaka datum automatiskt** är markerad på sidan **Inställning av betalningsregistrering** anges arbetsdatumet i fältet **Tillbaka datum**.  
3. I fältet **Tillbaka datum** anger du datumet då betalningen gjordes. Det datum kan skilja sig från arbetsdatumet.  
4. I fältet **Inlevererat belopp** anger du beloppet som har betalats.

    För fullständiga betalningar är detta samma som beloppet i fältet **Återstående belopp** på raden. För delbetalningar är detta belopp lägre än beloppet i fältet **Återstående belopp** på raden.
5. Upprepa steg 2–4 för andra rader som representerar bokförda dokument som betalningar har gjorts för.  
6. Välj åtgärden **Bokför betalningar**.  

Den angivna betalningsinformationen bokförs för de dokument som representeras av rader där kryssrutan **Utförd betalning** är markerad.  

Betalningstransaktioner bokförs på redovisningskonton, bankkonton och kundkonton. Varje betalning kopplas till det relaterade bokförda försäljningsdokumentet.  

## <a name="to-reconcile-lump-sum-payments" />Stämma av betalning av klumpsumma
1. Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta för mig vad du vill göra") anger du **betalningsregistrering** och väljer sedan relaterad länk.
2. Markera kryssrutan **Utförd betalning** på raderna som representerar bokförda dokument för samma kund som en klumpbetalning har gjorts för.  

    > [!NOTE]  
    >   Kunden i **Namn** fältet måste vara samma på alla rader som ska bokföras som en betalning av klumpsumma.  

    Om kryssrutan **Fyll i Tillbaka datum automatiskt** är markerad på sidan **Inställning av betalningsregistrering** fylls arbetsdatumet i fältet **Tillbaka datum**.  
3. I fältet **Tillbaka datum** anger du datumet då betalningen gjordes. Det datum kan skilja sig från arbetsdatumet.  

    > [!NOTE]  
    >   Detta datum måste vara samma på alla rader som ska bokföras som en betalning av klumpsumma.  
4. Ange belopp på flera rader som summerar klumpbetalningsbeloppet i fältet **Inlevererat belopp**.  

    > [!TIP]  
    > Försök att bokföra så många fullständiga betalningar som möjligt med klumpsumman. Ange belopp som är samma som beloppet i fältet **Återstående belopp** på så många rader som möjligt.  
5. Upprepa steg 2–4 för andra rader som representerar bokförda dokument för samma kund som en klumpbetalning har gjorts för.  
6. Välj åtgärden **Bokför som en betalning av klumpsumma**. Den angivna betalningsinformationen bokförs för de dokument som representeras av rader där kryssrutan **Utförd betalning** är markerad.  

Betalningstransaktioner bokförs på redovisningskonton, bankkonton och kundkonton. Varje betalning kopplas till det relaterade bokförda försäljningsdokumentet.  

Om en betalning i banken inte representeras av raden på sidan **Betalningsregistrering** kan det bero på att det relaterade dokumentet inte har bokförts. I så fall kan du använda en sökfunktion för att snabbt hitta dokument och bokföra det för att behandla betalningen. Mer information finns i avsnittet [Att söka efter ett visst försäljningsdokument som inte har fakturerats helt](#to-find-a-specific-sales-document-that-isnt-fully-invoiced).  

Om en betalning i banken inte representeras av ett dokument i [!INCLUDE[prod_short](includes/prod_short.md)], kan du öppna en förifylld redovisningsjournal från sidan **Betalningsregistrering** för att bokföra betalningen direkt till balanskontot, utan att koppla betalningen till ett dokument. Du kan också vilja registrera betalning i journalen tills ursprunget för betalningen har fastställts. Mer information finns i [Så här registrerar eller bokför du en betalning utan ett relaterat dokument](receivables-how-reconcile-customer-payments-list-unpaid-sales-documents.md#to-record-or-post-a-payment-without-a-related-document).  

## <a name="to-process-customer-payments-with-discounts-manually" />Så här behandlar du betalningar med rabatter manuellt
Om du har kommit överens om en kassarabatt med kunden, kan betalningsbeloppen bli lägre än fakturabeloppen, om betalning sker före det överenskomna kassarabattsdatumet.  

Följande procedur förklarar fyra olika sätt att bokföra rabatterade betalningar på sidan **Betalningsregistrering**.  

* Beloppet är lika med det återstående rabatterade beloppet, och betalningsdatumet infaller före kassarabattsdatum. Du bokför betalningen som är.  
* Beloppet är lika med det återstående rabatterade beloppet, men betalningsdatumet infaller efter kassarabattsdatum. Du bokför betalningen som del. Dokumentet förblir öppen för att kräva/betala det återstående beloppet. Du kan även ange rabattdatumet senare för att tillåta betalning i sin helhet.  
* Betalningsbeloppet är lägre än återstående rabatterade beloppet. Du bokför betalningen som del. Dokumentet förblir öppen för att kräva/betala det återstående beloppet.  
* Betalningsbeloppet är högre än återstående rabatterade beloppet. Du bokför betalningar som är. Endast det återstående beloppet bokförs. Det extra beloppet krediteras till kunden.  

### <a name="to-process-a-payment-amount-that-is-equal-to-the-discounted-amount-and-where-the-payment-date-is-before-the-discount-date" />Processa ett betalningsbelopp som är lika med det rabatterade beloppet, och där betalningsdatumet infaller före kassarabattsdatum.
1. Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta vad du vill göra") anger du **betalningsregistrering** och väljer sedan relaterad länk.  
2. Ange betalningsbeloppet i fältet **Inlevererat belopp**. Beloppet är lika med beloppet i fältet **Återstående belopp efter rabatt**.

    Kryssrutan **Utförd betalning** markeras automatiskt, och fältet **Tillbaka datum** fylls i med arbetsdatumet.    
3. Ange betalningsdatumet i fältet **Tillbaka datum**. Datumet är före datumet i fältet **Kassarabattsdatum**.
4. Kontrollera att fältet **Återstående belopp** innehåller värdet noll (0).  
5. Välj åtgärden **Bokför betalningar** för att bokföra den fullständiga betalningen på redovisningskonto bankkontot eller kundkontot.

### <a name="to-process-a-payment-amount-that-is-equal-to-the-discounted-amount-but-where-the-payment-date-is-after-the-discount-date" />Processa ett betalningsbelopp som är lika med det rabatterade beloppet, men där betalningsdatumet infaller efter kassarabattsdatumet
1. Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta vad du vill göra") anger du **betalningsregistrering** och väljer sedan relaterad länk.  
2. Ange betalningsbeloppet i fältet **Inlevererat belopp**. Beloppet är lika med beloppet i fältet **Återstående belopp efter rabatt**.

    Kryssrutan **Utförd betalning** markeras automatiskt, och fältet **Tillbaka datum** fylls i med arbetsdatumet.
3. I fältet **Tillbaka datum** anger du ett betalningsdatum som är efter datumet i fältet **Kassarabattsdatum**. Datumfält ändras till det röda teckensnittet, och ett felmeddelande visas längst ned på sidan.

    > [!TIP]  
    >   Om du vill göra ett undantag och hur bevilja rabatt, även om betalningen är sen, följ de här stegen:
4. Välj åtgärden **Detaljer**.  
5. På sidan **Information om betalningsregistrering** i fältet **Kassarabattsdatum** på snabbfliken **Kassarabatt** anger du ett datum som är efter datumet i fältet **Tillbaka datum** på sidan **Betalningsregistrering**.  

    Felmeddelande och det röda teckensnittet försvinner, och du kan fortsätta att bearbeta den rabatterade betalningen.    
6. Kontrollera att fältet **Återstående belopp** innehåller det belopp som återstår att betala av det helt fakturerade beloppet.  
7. Välj åtgärden **Bokför betalningar** för att bokföra delbetalning på redovisningskontot, bankkontot eller kundkontot.  

Det relaterade dokument förblir öppen.

### <a name="to-process-a-payment-that-is-lower-than-the-remaining-discounted-amount" />Processa en betalning som är lägre än återstående rabatterade beloppet
1. Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta vad du vill göra") anger du **betalningsregistrering** och väljer sedan relaterad länk.  
2. Ange betalningsbeloppet i fältet **Inlevererat belopp**. Beloppet är lägre än beloppet i fältet **Återstående belopp efter rabatt**.

    Kryssrutan **Utförd betalning** markeras automatiskt, och fältet **Tillbaka datum** fylls i med arbetsdatumet.  
3. Ange betalningsdatumet i fältet **Tillbaka datum**. Datumet är före datumet i fältet **Kassarabattsdatum**.
4. Kontrollera att fältet **Återstående belopp** innehåller det belopp som återstår att betala av det rabatterade beloppet.  
5. Välj åtgärden **Bokför betalningar** för att bokföra delbetalning på redovisningskontot, bankkontot eller kundkontot.  

Det relaterade dokument förblir öppen.

### <a name="to-process-a-payment-that-is-more-than-the-remaining-discounted-amount" />Processa en betalning som är högre än återstående rabatterade beloppet
1. Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta vad du vill göra") anger du **betalningsregistrering** och väljer sedan relaterad länk.  
2. Ange betalningsbeloppet i fältet **Inlevererat belopp**. Beloppet är högre än beloppet i fältet **Återstående belopp efter rabatt**.  

    Kryssrutan **Utförd betalning** markeras automatiskt, och fältet **Tillbaka datum** fylls i med arbetsdatumet.    
3. Ange betalningsdatumet i fältet **Tillbaka datum**. Datumet är före datumet i fältet **Kassarabattsdatum**.
4. Kontrollera att fältet **Återstående belopp** innehåller värdet noll (0).  
5. Välj åtgärden **Bokför betalningar** för att bokföra den fullständiga betalningen på redovisningskonto bankkontot eller kundkontot.  

Det relaterade dokument stängs och kunden krediteras för överskottsbeloppet.  

## <a name="to-find-a-specific-sales-document-that-isnt-fully-invoiced" />Om du vill hitta ett visst försäljningsdokument som inte har fakturerats helt
Sidan **Betalningsregistrering** fungerar som stöd för dig i uppgifter som krävs för balansering av interna konton, genom att använda faktiska kassasiffror, för att kontrollera den effektiva samlingen från kunder och förfallna betalningar till leverantörer. Visar utestående inkommande betalningar som rader som representerar försäljningsdokument, där ett belopp har förfallit till betalning.  

Vanligtvis när en betalning har utförts, registrerats i banken eller liknande, representeras det relaterade försäljnings- eller inköpsdokumentet av en rad på sidan **Betalningsregistrering** eftersom dokumentet i fråga väntar på att betalningen bokförs mot utestående belopp. Ibland representeras dock inte en betalning som har gjorts av en rad på sidan **Betalningsregistrering**, vanligtvis eftersom dokumentet i fråga inte helt har fakturabokförts.

På sidan **Dokumentsökning** kan du söka bland dokument som inte har fakturerats helt. Du kan söka baserat på en eller flera av följande villkor:  

* Dokumentnummer  
* Belopp eller beloppsintervall  

Följande procedurer beskriver hur du hittar ett visst dokument, genom att använda både sökvillkor.  

1. Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta vad du vill göra") anger du **betalningsregistrering** och väljer sedan relaterad länk.
2. Välj avsnittet **Sök dokument** med pekaren på någon av raderna.
3. På sidan **Dokumentsökning** anger du ett sökvärde i fältet **Dokumentnr.**  

    > [!NOTE]  
    >   Värdet som du anger i detta fält, omsluts i gömda jokertecken. Det betyder att funktionen söker efter alla verifikationsnummer som innehåller det angivna värdet.    
4. I fältet **Belopp** anger du det specifika belopp som finns på den öppna dokument, som du vill hitta.  
5. Ange ett procentsatsvärde för att definiera intervallet av belopp som du vill söka för att hitta den öppna dokumentet i fältet **Beloppstolerans i %**.  

    Om du anger 10, kommer funktionen söka efter belopp i intervallet tio procent lägre och tio procent högre än värdet i fältet **Belopp**.    
6. Välj åtgärden **Sök**.  

Sökfunktionen söker bland dokument som inte är fullständigt fakturerade baserat på de angivna villkoren.  

Om ett eller flera dokument matchar sökvillkorna, öppnas sidan **Dokumentsökningsresultat** och visar raderna som motsvarar de dokument. Varje rad innehåller ett dokumentnummer, en beskrivning och ett belopp. Informationen gör det enklare att hitta ett visst dokument.

Om en betalning i banken inte representeras av ett dokument i [!INCLUDE[prod_short](includes/prod_short.md)], kan du öppna en förifylld redovisningsjournal från sidan **Betalningsregistrering** för att bokföra betalningen direkt till balanskontot, utan att koppla betalningen till ett dokument. Du kan också vilja registrera betalning i journalen tills ursprunget för betalningen har fastställts.  

## <a name="to-record-or-post-a-payment-without-a-related-document" />Så här registrerar eller bokför du en betalning utan ett relaterat dokument
Om en betalning i banken inte representeras av ett dokument i [!INCLUDE[prod_short](includes/prod_short.md)], kan du öppna en förifylld redovisningsjournalsrad från sidan **Betalningsregistrering** för att bokföra betalningen direkt till balanskontot, utan att koppla betalningen till ett dokument. Du kan också vilja registrera betalning i journalen tills ursprunget för betalningen har klargjorts.  

1. Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta vad du vill göra") anger du **betalningsregistrering** och väljer sedan relaterad länk.
2. Välj åtgärden **Redovisningsjournal**.  

    Sidan **Redovisningsjournal** öppnas med en rad som innehåller balanskontot i journalen som ställs in på sidan **Inställning av betalningsregistrering**.  
3. Fyll i de återstående fälten på redovisningsjournalsraden. Du kan t.ex. ange belopp, kundnummer eller information från kontoutdraget. Mer information finns i [Bokföra transaktioner direkt i redovisningen](finance-how-post-transactions-directly.md).  

Du kan bokföra journalraden för att uppdatera summan på balanskontot. Du kan även lämna journalraden obokförd och eventuellt koppla den till en kommentar om att betalningen behöver mer analys.  

Om du lämnar journalraden obokförd, adderas det till värdet i fältet **Ej bokförd balans** längst ned på sidan **Betalningsregistrering**.  

## <a name="see-also" />Se även
[Hantera kundreskontra](receivables-manage-receivables.md)  
[Försäljning](sales-manage-sales.md)  
[Arbeta med [!INCLUDE[prod_short](includes/prod_short.md)]](ui-work-product.md)


[!INCLUDE[footer-include](includes/footer-banner.md)]
