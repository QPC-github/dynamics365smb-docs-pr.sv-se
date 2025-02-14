---
title: Bearbeta delleveranser
description: Försäljningsorderns leveranser kan behandlas i Business Central med del leveranser med hjälp av fälten Leveransråd och Ant. att utleverera.
author: rubenseishima
ms.service: dynamics365-business-central
ms.topic: conceptual
ms.search.keywords: 'shipping advice, partial shipments, partial deliveries, trade, customer sales order'
ms.date: 08/12/2022
ms.author: a-reishima
---
# <a name="process-partial-shipments" />Bearbeta delleveranser

I en del leverans, levereras ingen order på samma gång. Av en order på exempelvis 100 enheter levereras 40 enheter omedelbart och 60 vid senare tillfälle. Det finns ingen begränsning av antalet utleveranser som kan utföras för en order.

Innan du kan använda del leveranser i [!INCLUDE [prod_short](includes/prod_short.md)] måste du dock ange att kunden ska acceptera del leveranser genom att ställa in fältet **leveransråd** på sidan **kundkort**. Om kunden vanligt vis bara godtar fullständiga leveranser men sedan begär eller accepterar en del leverans för en viss försäljningsorder, kan du ändra fältet **leveransråd** innan du bokför.

Som standard [!INCLUDE [prod_short](includes/prod_short.md)] anges fältet på sidan **kundkort** som **delvis**, vilket tillåter del leveranser. Om däremot fältet har justerats för att specificera **avsluta**, sedan blockeras fältet **Ant. att utleverera** är blockerat i försäljningsorder för den kunden.

[!INCLUDE [order-ship-invoice_md](includes/order-ship-invoice.md)]

## <a name="see-also" />Se även

[Sälja produkter med en kundförsäljningsreturorder](sales-how-sell-products.md)  
[Leverera artiklar](warehouse-how-ship-items.md)  
[Skapa direktleveranser](sales-how-drop-shipment.md)  
[Försäljning](sales-manage-sales.md)  
[Gör dig redo att göra affärer](ui-get-ready-business.md)  
[Administration](admin-setup-and-administration.md)  

[!INCLUDE[footer-include](includes/footer-banner.md)]
