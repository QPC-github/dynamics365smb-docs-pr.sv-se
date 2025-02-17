---
title: Hantera budget för anläggningstillgångar
description: 'Du kan ställa in information om framtida investeringar, avyttringar och avskrivning av anläggningstillgångar för att förbereda budgetar och prognoser.'
author: edupont04
ms.topic: conceptual
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.search.keywords: forecast
ms.search.form: '5610, 5611'
ms.date: 04/01/2021
ms.author: edupont
---
# <a name="manage-budgets-for-fixed-assets" />Hantera budgetar för anläggningstillgångar

Du kan skapa budgeterade anläggningstillgångar. På så sätt kan du t. ex. inkludera eventuella förutsedda anskaffningar och försäljningar i rapporter.  

Om du vill förbereda den budgeterade resultaträkningen, balansräkningen och likviditetsbudgeten måste du ha tillgång till information om framtida investeringar, avyttringar och avskrivning av anläggningstillgångar. Den här informationen får du i rapporten **Anl.tillg. – planerat värde**. Innan du skriver ut rapporten måste du förbereda budgeten.  

## <a name="to-budget-the-acquisition-cost-of-a-fixed-asset" />För att budgetera anskaffningskostnaden för en anläggningstillgång

När du förbereder en budget måste du skapa anläggningstillgångskort för de anläggningstillgångar som du avser att införskaffa i framtiden. De budgeterade anläggningstillgångarna ställs in som vanliga anläggningstillgångar, men de måste ställas in för att inte bokföras i redovisningen.

När du bokför anskaffningskostnaden, anger du numret på den budgeterade fasta anläggningstillgången i fältet **Budgeterat anl.nr.** På så sätt bokförs en anskaffningskostnad med ett motsatt tecken för den budgeterade tillgången. Detta innebär att den totala anskaffningskostnaden för den budgeterade tillgången är mellanskillnaden mellan den budgeterade och den verkliga anskaffningskostnaden.

1. Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta för mig vad du vill göra") anger du **Anläggningstillgångar** och väljer sedan relaterad länk.
2. Välj åtgärden **Ny** för att skapa ett nytt anläggningstillgångskort för den budgeterade anläggningstillgången.
3. Markera kryssrutan **Budgeterad anläggningstillgång** så förhindras bokföring i redovisningen.
4. Fyll i de återstående fälten, tilldela en avskrivningsregel och bokför sedan den första anskaffningskostnaden med budgeterade anläggningstillgången som anges i fältet **Budgeterat anl.nr.** på journalraden. Mer information finns i [Så här anskaffar du anläggningstillgångar](fa-how-acquire.md).

## <a name="to-budget-the-disposal-of-a-fixed-asset" />För att budgetera avyttringen av en anläggningstillgång:

Om du planerar att sälja tillgångar under budgetperioden kan du föra in uppgifter om försäljningspris och försäljningsdatum.

1. Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta för mig vad du vill göra") anger du **Anläggningstillgångar** och väljer sedan relaterad länk.
2. Markera den anläggningstillgång som du vill avyttra och välj sedan åtgärden **Avskrivningsregler**.
3. På sidan **Avskrivningsregler för anl.tillg.**, fyll i fälten **Planerat avyttringsdatum** och **Planerad avyttringsintäkt**. [!INCLUDE[tooltip-inline-tip](includes/tooltip-inline-tip_md.md)]

## <a name="to-view-projected-disposal-values" />Så här visar du planerade avyttringsvärden

Om du vill se de planerade avyttringsvärdena och beräkna vinsten och förlusten kan du använda rapporten **Anl. – planerat värde**.

1. Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta för mig vad du vill göra") anger du **Anl. – planerat värde** och väljer sedan relaterad länk.
2. Fyll i fälten om det behövs.
3. Välj knappen **Skriv ut** eller **Förhandsgranska**.

## <a name="to-budget-depreciation" />Så här budgeterar du avskrivning

Du kan använda rapporten **Anl.tillg. – planerat värde** för att beräkna framtida avskrivning. I rapporten visas bokföringsvärdet och den ackumulerade avskrivningen vid inledningen av den angivna perioden, ändringar under perioden och bokföringsvärde och ackumulerad avskrivning vid slutet av den angivna perioden.

1. Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta vad du vill göra") anger du **Planerat värde för anläggningstillgång** och väljer sedan relaterad länk.
2. Fyll i fälten om det behövs.
3. Om du vill se det totala värdena föra alla tillgångar avmarkerar du kryssrutan **Skriv ut per anl.tillg.**.
4. Fyll inte i fälten på snabbfliken **Anläggningstillgång** så inkluderas alla tillgångar. I fältet **Budgeterad tillgång** kan du fylla i **Nej** om du vill utesluta budgeterade tillgångar eller **Ja** om du endast vill visa de budgeterade tillgångarna.
5. Välj knappen **Skriv ut** eller **Förhandsgranska**.

## <a name="see-related-microsoft-trainingtrainingmodulesbudget-fixed-assets" />Se relaterad [Microsoft utbildning](/training/modules/budget-fixed-assets/)

## <a name="see-also" />Se även

[Anläggningstillgångar](fa-manage.md)  
[Ställa in anläggningstillgångar](fa-setup.md)  
[Ekonomi](finance.md)  
[Gör dig redo att göra affärer](ui-get-ready-business.md)  
[Arbeta med [!INCLUDE[prod_short](includes/prod_short.md)]](ui-work-product.md)


[!INCLUDE[footer-include](includes/footer-banner.md)]
