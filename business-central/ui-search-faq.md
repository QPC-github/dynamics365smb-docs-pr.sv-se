---
title: Vanliga frågor om Berätta
description: Den här artikeln innehåller svar på frågor från våra partners och kunder som ofta frågar om Berätta.
author: brentholtorf
ms.topic: conceptual
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.search.keywords: find
ms.search.form: TellMe
ms.date: 05/23/2022
ms.author: bholtorf
---
# <a name="tell-me-faq" />Vanliga frågor om Berätta
I det här avsnittet besvaras frågor som våra erfarna användare ofta frågar om funktionen berätta för mig.

### <a name="are-all-actions-from-my-current-page-discoverable-in-tell-me" />Är alla åtgärder från den aktuella sidan synliga i Berätta?

Nej. Åtgärder i delar, till exempel Försäljningsraddelar eller faktaboxar, visas inte vet i Berätta.

### <a name="are-the-results-in-tell-me-filtered-by-permissions" />Filtreras resultaten i Berätta efter behörigheter?

Om användaren inte har AccessByPermissions visas inte åtgärder. Sidor och rapporter visas däremot i sökresultaten men kräver att användaren har behörighet att komma åt dem. Ett meddelande visas om användaren inte har behörighet att visa objektet.

### <a name="does-tell-me-display-content-from-my-customizations-or-installed-third-party-extensions" />Visar Berätta innehåll från mina anpassningar eller installerat tillägg från tredje parter?

Åtgärder, sidor och rapporter som kommer från tillägg tas upp av Berätta. Teknisk information om hur du gör egna sidor och rapporter synliga kan finns i [Lägga lägga till sidor och rapporter till Sökning](/dynamics365/business-central/dev-itpro/developer/devenv-al-menusuite-functionality).

### <a name="what-makes-this-different-from-what-was-previously-known-as-page-search" />Vad gör att detta skiljer sig från vad som tidigare var känt som Sidsökning?

Sidsökning har utvecklats till Berätta för att hjälpa dig att få jobbet gjort fortare. Sidsökning kan bara hjälpa dig att navigera till sidor och rapporter. På teknisk nivå baseras Berätta inte längre på äldre MenuSuite-begrepp.

### <a name="i-use-on-premises-includeprodshortincludesprodshortmd-does-that-include-tell-me" />Du kan använda lokal [!INCLUDE[prod_short](includes/prod_short.md)]. Omfattar detta Berätta?

Du kan använda Berätta i den lokala webbklienten för att hitta åtgärder, sidor och rapporter, men inte appar och konsulttjänster i AppSource.

### <a name="is-tell-me-available-for-all-form-factors" />Är Berätta tillgänglig för alla formfaktorer?

Berätta finns bara i webbklienten eller Windows-skrivbordsapp.

<!-- removed in v20 because of Help pane
### <a name="are-the-documentation-results-available-in-any-language" />Are the documentation results available in any language?
The help articles display in the language you have specified in **My Settings**, if help is available in that language.
-->

### <a name="does-tell-me-give-me-help-on-how-to-use-pages-reports-and-other-things" />Kan jag få hjälp med att använda sidor, rapporter och andra saker?

Nej, men det är lätt att komma åt informationen från Hjälp fönstret. Välj bara menyalternativet **Hjälp** (frågetecknet i det övre högra hörnet) eller tryck på <kbd>Ctrl</kbd>+<kbd>F1</kbd> på ditt tangentbord. Mer information finns i [Hjälpfönster](product-help-and-support.md#help-pane).

### <a name="why-dont-i-see-a-bookmark-icon-for-my-search-results" />Varför visas inte en bokmärkesikon för mina sökresultat?

Ikonen för bokmärket visas inte i fönstret berätta för mig när anpassningar inaktiveras för en användarroll.


## <a name="see-also" />Se även
[Spara och anpassa listvyer](ui-views.md)  
[Söka efter sidor och information med berätta](ui-search.md)  
[Söka efter sidor med rollutforskaren](ui-role-explorer.md)  
[Förse en sida eller rapport med ett bokmärke på ditt rollcenter](ui-bookmarks.md)


[!INCLUDE[footer-include](includes/footer-banner.md)]
