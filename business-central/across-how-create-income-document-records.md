---
title: Skapa inkommande dokumentposter
description: 'Använd olika funktioner på sidan inkommande dokument för att granska utgifts kvitton, hantera OCR-uppgifter, konvertera inkommande användarfiler och bifoga externa filer.'
author: SorenGP
ms.topic: conceptual
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.search.keywords: 'electronic document, e-invoice, incoming document, OCR, ecommerce, document exchange, import invoice'
ms.date: 06/14/2022
ms.author: edupont
---
# <a name="create-incoming-document-records" />Skapa inkommande dokumentposter

På sidan **Inkommande dokument** använder du olika funktioner för att förhandsgranska utgiftskvitton, hantera OCR-uppgifter och konvertera inkommande dokumentfiler, manuellt eller automatiskt, till relevanta dokument eller journalrader i . De externa filerna kan kopplas till något processteg, inklusive till bokförda dokument och till resulterande leverantörs-, kund- och redovisningstransaktioner.

Om du vill registrera ett externt dokument i [!INCLUDE[prod_short](includes/prod_short.md)], måste du först skapa eller slutföra en inkommande dokumentpost. Du kan göra detta manuellt eller så kan du ta ett foto på det externa dokumentet och sedan skapa en inkommande dokumentpost med bildfilen bifogad.

Innan du kan använda funktionen för **inkommande dokument** måste du utföra de nödvändiga inställningarna. Mer information finns i [Skapa inkommande dokument](across-how-setup-income-documents.md).

## <a name="approve-or-reject-an-incoming-document" />Så här Godkänn eller avvisa ett inkommande dokument.

Om du har ställt in funktionen **inkommande dokument** så att den kräver godkännande för att skapa dokument, måste användare med rätt behörighet godkänna posterna innan de behandlas. Mer information finns i [ställa in god kännare för inkommande dokumentposter](across-how-setup-income-documents.md#to-set-up-approvers-of-incoming-document-records).

1. Välj ikonen med ![glödlampan som öppnar funktionen Berätta](media/ui-search/search_small.png "Berätta för mig vad du vill göra") anger du **Inkommande dokument** och väljer sedan relaterad länk.
2. Markera raden med dokumentet som du vill godkänna eller avvisa, och välj sedan åtgärden **godkänna** eller **avvisa**.

Om du godkänner den inkommande dokumentposten markeras kryssrutan **Släppt** på den inkommande dokumentraden. Användaren som ansvarar för att skapa t.ex inköpsfakturor kan fortsätta med att bearbeta transaktionen.

## <a name="create-an-incoming-document-record-by-taking-a-photo" />Så här skapar du en inkommande dokumentpost genom att ta ett foto

> [!NOTE]  
> Följande proceduren gäller endast [!INCLUDE[prod_short](includes/prod_short.md)] för surfplatte- och telefonklienter.

1. I rollcenter, välj panelen **Skapa inkommande dokument från kamera** i appfältet och gå sedan till steg 4.
2. Stäng alternativt ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta för mig vad du vill göra") anger du **Inkommande dokument** och väljer sedan relaterad länk.
3. På sidan **Inkommande dokument** väljer du **Ny** och sedan **Skapa från kamera**. Kameran på Tablet PC:n eller telefonen aktiveras.
4. Ta ett foto av ett dokument, t. ex. ett inköpskvitto, som du vill bearbeta som ett inkommande dokument, och välj sedan knappen **Använd** .

    En ny inkommande dokumentpost skapas med bilden bifogad.

## <a name="attach-an-image-to-an-incoming-document-record-by-taking-a-photo" />Så här bifogar du en bild till en inkommande dokumentpost genom att ta ett foto

> [!NOTE]  
> Följande proceduren gäller endast [!INCLUDE[prod_short](includes/prod_short.md)] för surfplatte- och telefonklienter.

1. Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta för mig vad du vill göra") anger du **Inkommande dokument** och väljer sedan relaterad länk.
2. Öppna kortet för en befintlig inkommande dokumentpost.
3. På dokumentsidan **Process** väljer du **Bifoga fil från kamera**. Kameran på Tablet PC:n eller telefonen aktiveras.
4. Ta ett foto av ett dokument, t. ex. ett inköpskvitto, som du vill bearbeta som ett inkommande dokument, och välj sedan knappen **Använd** .

    Bilden har bifogats till den inkommande dokumentposten.

## <a name="create-an-incoming-document-record-manually" />Så här skapar du en inkommande dokumentpost manuellt

1. Välj den ![Glödlampa som öppnar funktionen Berätta.](media/ui-search/search_small.png "Berätta vad du vill göra") anger du **Inkommande dokument** och väljer sedan relaterad länk.
2. Välj **Ny** och sedan åtgärden **Skapa från fil**.  
3. Välj en fil och välj sedan **Öppna** på sidan **Infoga fil**. Filen kopplas automatiskt.
4. Välj alternativt åtgärden **Ny**.
5. För att bifoga en fil väljer du åtgärden **Process** och åtgärd **Bifoga fil**.
6. Markera filen som representerar det inkommande dokumentet i fråga och välj sedan knappen **Öppna** på sidan **Infoga fil**.
7. På sidan **Inkommande dokument** fyller du i fälten efter behov. [!INCLUDE[tooltip-inline-tip](includes/tooltip-inline-tip_md.md)]

## <a name="see-related-microsoft-trainingtrainingmodulesincoming-documents-dynamics-365-business-central" />Se relaterad [Microsoft utbildning](/training/modules/incoming-documents-dynamics-365-business-central/)

## <a name="see-also" />Se även

[Använd OCR för att förvandla PDF- och bildfiler till elektroniska dokument](across-how-use-ocr-pdf-images-files.md)
[Skapa inkommande dokumentposter direkt från dokument och poster](across-how-connect-disconnect-income-document-records.md)
[Hitta bokförda dokument utan inkommande dokumentposter](across-how-find-posted-documents-without-income-document-records.md)
[Inkommande dokument](across-income-documents.md)  
[Inköp](purchasing-manage-purchasing.md)  
[Arbeta med [!INCLUDE[prod_short](includes/prod_short.md)]](ui-work-product.md)


[!INCLUDE[footer-include](includes/footer-banner.md)]
