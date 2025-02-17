---
title: Skapa baskalendrar
description: Du kan tilldela företaget och dess affärspartners en baskalender för att beräkna leveransdatum och inleveransdatum enligt de angivna arbetsdagarna.
author: SorenGP
ms.topic: conceptual
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.search.form: '7600, 7601, 7602, 5703'
ms.date: 06/11/2021
ms.author: edupont
---
# <a name="set-up-base-calendars" />Skapa baskalendrar

Du kan tilldela företaget och dess affärspartner, till exempel kunder, leverantörer och lagerställen, en baskalender. De angivna arbetsdagarna i kalendern används för att beräkna leveransdatum och inleveransdatum på rader på försäljningsorder, inköpsorder, överföringsorder och produktionsorder. Huvuduppgiften när du lägger upp en ny baskalender är att ange och definiera de lediga dagar som du vill ska gälla.  

## <a name="to-set-up-a-base-calendar" />Så här lägger du upp en baskalender

1.  Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta för mig vad du vill göra") anger du **Baskalender** och väljer sedan relaterad länk.  
2.  Välj åtgärden **Ny**.  
3.  Fyll i fältet **Kod**.  
4. Välj åtgärden **Bibehåll baskalenderändringar**.
5. På sidan **baskalenderändringar** använd fältet **Återkommande system** för att markera ett visst datum eller en viss dag som återkommande ledig dag. Du kan välja mellan alternativen **Årligen återkommande** eller **Veckovis återkommande**.  

    Om du väljer **Årligen återkommande** måste du även ange vilket datum som avses i fältet **Datum**.  

    Om du väljer **Veckovis återkommande** måste du även ange vilken veckodag som avses i fältet **Dag**. Om du lämnar fältet tomt, måste du fylla i fältet **Datum**. Fältet **Dag** fylls i automatiskt.  

När du gör en transaktion är fältet **Ej arbetsdag** markerat. Du kan välja att ta bort markeringen för att göra detta till en arbetsdag.  
 När du återgår till baskalenderkortet kan du lägga märke till att de lediga dagar som du har angett har uppdaterats. Posterna är nu röda, och **Ej arbetsdag** är markerat.  

> [!NOTE]  
>  När du lägger upp en ny baskalender kan du markera och kopiera rader från en befintligt kalender. Det gör du på sidan **Baskalenderändringar**.  

> [!IMPORTANT]  
>  En baskalender som definierats för leverantörer eller lagerställe inverkar på hur datumen beräknas och avrundas till arbetsdagar.
Anger en datumformel för den tid det tar att fylla på artikeln. Den används för att beräkna fältet **Planerat inleveransdatum** om beräkningen är framåt och fältet **Orderdatum** om beräkningen är bakåt. Se [Ledtidsberäkning](across-how-to-assign-base-calendars.md#lead-time-calculation).

## <a name="lead-time-calculation" />Ledtidsberäkning

En baskalender som definierats för leverantörer eller lagerställe inverkar på hur datumen beräknas och avrundas till arbetsdagar. De viktigaste två datumfält på inköpsorderrader beräknas därför på följande sätt under olika omständigheter.

|Beräkningsriktning|Leverantörskalender har definierats|Leverantörskalender har inte definierats|
|---------------------|-----------------------|---------------------------|
|Framåt|planerat inleveransdatum = orderdatum + leverantörsledtid (per leverantörskalendern och avrundat till nästa arbetsdag först i leverantörskalendern och sedan i lagerställekalendern)|planerat inleveransdatum = orderdatum + ( leverantörsledtid per lagerställekalendern)|
|Bakåt|orderdatum = + planerat inleveransdatum – leverantörsledtid (per leverantörskalendern och avrundat till föregående arbetsdag först i leverantörskalendern och sedan i lagerställekalendern)|orderdatum = planerat inleveransdatum – leverantörsledtid (per lagerställekalendern)|

> [!NOTE]
> Förutom Ledtidsberäkningen som påverkar det planerade inleveransdatumet och Orderdatum, vilket visas i tabellen ovan distributionslagerhanteringstid och säkerhetsledtid läggas till i formlerna till värdet i fältet **förväntat inleveransdatum** följande: planerat inleveransdatum + Säkerhetsledtid + inkommande lagerhanteringstid = Förväntat inleveransdatum.

> [!Important]
> Om ditt lagerställe använder en helt annan kalender än den leverantörerna använder är det viktigt att du lägger upp specifika kalendrar för leverantörerna för att beräkna bästa möjliga leverantörsledtider. Om du vill veta hur du ställer in leverantörskalendrar, se avsnittet [Så här tilldelar du en baskalender](across-how-to-assign-base-calendars.md#to-assign-a-base-calendar).

Innehållet i fältet **Ledtidsberäkning** kopieras från antingen artikelkortet eller lagerställeenhetskortet om ledtiden har angetts för artikeln, eller sidan **Artikelns leverantörskatalog** om ledtiden definieras för leverantören.

## <a name="to-customize-a-calendar" />Så här anpassar du en kalender
Huvuduppgiften när du anpassar en baskalender för företaget, eller någon av dess affärspartner, är att ange eventuella ändringar av status som arbetsdag eller ledig dag.

I en baskalender visas exempelvis alla lördagar normalt som lediga dagar, medan i en anpassad kalender för ett visst lagerställe kan alla lördagar i november och december fram till julhelgen visas som arbetsdagar.

I proceduren nedan används fallet med lagerstället som exempel: Lägg märke till att du i det här skedet redan har fördelat en baskalender till lagerstället.

1. Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta för mig vad du vill göra") anger du **Platser** och väljer sedan relaterad länk.
2. Öppna den plats som du vill uppdatera och välj sedan fältet **anpassad kalender**. Observera att en kalender måste markeras i fältet **Baskalenderkod**.
3. På sidan **Anpassa kalendertransaktioner** väljer du åtgärden **Underhåll ändringar i kalender**.
4. I **Anpassa kalenderändringar** lägger du till rader för anpassade kalendertransaktioner.

    När du registrerar en rad, är kryssrutan **Ej arbetsdag** markerat. Du kan ta bort markeringen om du vill ändra status till en arbetsdag.

    Du kan använda fältet **Återkommande system** för att ange ett visst datum eller en viss dag som återkommande ledig dag. Du kan välja mellan alternativen **Årligen återkommande** eller **Veckovis återkommande**.

    Om du väljer **Årligen återkommande** måste du även ange vilket datum som avses i fältet **Datum**. Om du väljer **Veckovis återkommande** måste du även ange vilken veckodag som avses i fältet **Dag**. Om du lämnar fältet tomt, måste du fylla i fältet **Datum**. Fältet **Dag** fylls i automatiskt. Det kan vara praktiskt om du vill markera ett enstaka datum som arbetsdag eller ledig dag.

5. Välj knappen **OK**.

På sidan **Anpassade kalendertrans.** kan du lägga märke till att de ändringar som du har gjort har uppdaterats dynamiskt.

Observera också, när du öppnar lagerställekortet, att fältet **Anpassad kalender** har värdet **Ja**, vilket indikerar att en anpassad kalender har definierats.

> [!Important]
> Om du inte fyller i fältet **Lagerställekod** på en orderrad används företagets kalender.


Om du inte fyller i fältet **Speditörkod** på en orderrad används företagets kalender.

> [!NOTE]  
> Om du ändrar en baskalender som det finns anpassningsändringar av, uppdateras även alla befintliga, anpassade kalendrar automatiskt.

## <a name="to-assign-a-base-calendar" />Så här tilldelar du en baskalender
Följande procedur schemalägger exempelvis leveransdatum på försäljningsorderrader för en kund.

Baskalendrar tilldelas till ditt eget företag, kunder, leverantörer, lagerställen och speditörer på följande sätt:  

-   På korten **Företagsinformation** och **Kund** tilldelas baskalendern på snabbfliken **Leverans**.  
-   På kortet **Leverantör**  tilldelas baskalendern på snabbfliken **Inleverans**.  
-   På kortet **Lagerställe** tilldelas baskalendern på snabbfliken **Lager**.  
-   På sidan **Speditörer** fördelats baskalendern på sidan **Speditörsservice**.  

1.  Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta för mig vad du vill göra") anger du **Kunder** och väljer sedan relaterad länk.  
2.  Öppna det **Kundkort** som du vill tilldela en anpassad kalender för.  
3.  På Snabbfliken **Leverans**, i fältet **Baskalenderkod**, markera den baskalender som du vill tilldela.  

> [!IMPORTANT]  
>  -   Om du inte tilldelar ett företag en baskalender betraktas alla datum som arbetsdagar.  
> -   Om du anger ett tomt lagerställe på en orderrad betraktas alla datum som arbetsdagar.  
> -   En baskalender som definierats för leverantörer eller lagerställe inverkar på hur datumen beräknas och avrundas till arbetsdagar.

> [!NOTE]  
>  Innan du kan skapa några anpassade kalendertransaktioner måste du först tilldela företaget en baskalender.  

## <a name="see-also" />Se även
[Inköp](purchasing-manage-purchasing.md)  
[Produktion](production-manage-manufacturing.md)    
[Lager](inventory-manage-inventory.md)  
[Arbeta med [!INCLUDE[prod_short](includes/prod_short.md)]](ui-work-product.md)


[!INCLUDE[footer-include](includes/footer-banner.md)]
