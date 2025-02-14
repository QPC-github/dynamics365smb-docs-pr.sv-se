---
title: Exportera Positive Pay-filer
description: Du kan se till att banken bara godkänner validerade checkar och belopp genom att exportera Positive Pay-fil som innehåller information om leverantör betalning.
author: SorenGP
ms.topic: conceptual
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.search.keywords: 'check, clearing'
ms.search.form: '1231, 1232, 1233, 1234'
ms.date: 04/01/2021
ms.author: edupont
---
# <a name="export-a-positive-pay-file" />Exportera en Positive Pay-fil
För att se till att banken bara godkänner validerade checkar och belopp kan du exportera en Positive Pay-fil med relevant leverantörsinformation, checknummer och betalningsbelopp som du sedan skickar till banken som referens när du behandlar betalningar.

[!INCLUDE[prod_short](includes/prod_short.md)] är förkonfigurerat för att stödja Positive Pay-filer för Bank of America och City Bank.

## <a name="to-set-up-a-bank-account-for-positive-pay" />Så här skapar du ett bankkonto för Positive Pay
1. Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta för mig vad du vill göra") anger du **Bankkonton** och väljer sedan relaterad länk.
2. Öppna kortet för den bank du vill använda Positive Pay för.
3. I fältet **Positive Pay exportkod** anger du POSPAYBANK.
4. Stäng sidan.

## <a name="to-export-a-positive-pay-file" />För att exportera en Positive Pay-fil
1. Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta för mig vad du vill göra") anger du **Bankkonton** och väljer sedan relaterad länk.
2. Välj det bankkonto som du vill exportera en Positive Pay-fil till.
3. Välj åtgärden **Positive Pay-export**.

    Sidan **Positive Pay-export** öppnas och visar betalningar som har gjorts för bankkontot efter det sista överföringsdatumet, enligt fälten **senaste överföringsdatum** och **senaste överföringstid**.
4. I fältet **Brytdatum för uppladdning** anger ett datum före vilket betalningar inte inkluderas i den exporterade filen.
5. Välj åtgärden **Exportera**.
6. Klicka på **Spara** på sidan **Exportera fil** och spara sedan filen till lämplig plats.
7. Överför filen till din elektroniska bank.
8. Skriv ner eller kopiera bekräftelsenumret som du får när filuppladdningen till banken lyckas.

Så här visar du exporterade Positive Pay-poster

1. Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta för mig vad du vill göra") anger du **Bankkonton** och väljer sedan relaterad länk.
2. Välj det bankkonto som du vill visa Positive Pay-exportposter för.
3. Välj åtgärden **Positive Pay-transaktioner**.

    På sidan **Positive Pay-transaktioner** kan du se alla Positive Pay-exportposter för bankkontot.
4. I fältet **bekräftelsenummer** anger du bekräftelsenummer för varje exportpost som du får vid filöverföring till banken.
5. Om du vill visa de relaterade betalningsraderna väljer du åtgärden **Positive Pay-transaktionsinformation**.

Att återexportera Positive Pay-filer

1. Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta vad du vill göra") anger du **Bankkonton** och väljer sedan relaterad länk.
2. Välj det bankkonto som du vill återexportera en Positive Pay-fil till.
3. Välj åtgärden **Positive Pay-transaktioner**.
4. Välj den rad för Positive Pay-exportfilen som du vill återexportera.
5. På sidan **Positive Pay-transaktioner** väljer du åtgärden **Återexportera Positive Pay till fil**.

## <a name="see-also" />Se även
[Ekonomi](finance.md)  
[Ställa in Finance](finance-setup-finance.md)  
[Arbeta med redovisningsjournaler](ui-work-general-journals.md)  
[Arbeta med [!INCLUDE[prod_short](includes/prod_short.md)]](ui-work-product.md)


[!INCLUDE[footer-include](includes/footer-banner.md)]
