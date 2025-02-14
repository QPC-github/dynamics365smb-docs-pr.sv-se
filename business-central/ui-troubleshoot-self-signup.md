---
title: Felsök problem med registrering av Self Service | Microsoft Docs
description: 'Få veta mer om de vanligaste orsakerna till varför du kanske inte kan slutföra registreringen till Business Central, samt hur du åtgärdar dem.'
author: edupont04
ms.topic: conceptual
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/01/2021
ms.author: edupont
---
# Felsöka registrering av Self Service
Det går enkelt och snabbt att registrera sig för [!INCLUDE[prod_short](includes/prod_short.md)]. Du kan skapa ett gratis konto, även om du är en befintlig organisation. Detta inlägg tar upp frågor som du kan ha under registreringen.

## Vilken e-postadress kan jag använda med Business Central?
[!INCLUDE[prod_short](includes/prod_short.md)] kräver att du använder en e-postadress från ditt arbete eller skola för att registrera dig. [!INCLUDE[prod_short](includes/prod_short.md)] har inte stöd för e-postadresser som tillhandahålls av e-posttjänster för konsumenter eller telekommunikationsleverantörer. Dessa omfattar outlook.com, hotmail.com, gmail.com, etc..

Om du försöker att registrera dig med en personlig e-postadress kommer du att få ett meddelande som indikerar att du använder en e-postadress från arbete eller skola.

## Felsökning
I många fall kan registrering för [!INCLUDE[prod_short](includes/prod_short.md)] göras genom att följa registreringsprocessen. Men det finns flera anledningar till att du inte kan slutföra registrering av Self Service. Tabellen nedan summerar några av de vanligaste orsakerna till att du inte kan slutföra registreringen och lösningar till dessa problem.

| Symptom/felmeddelande | Orsak och lösning |
| --------------------- | -------------------- |
| För Microsoft 365-e-postadresser som inte är registrerade i ett land som stöds får du ett meddelande liknande detta under registreringen:<br /><br />**Vi har inte stöd för ditt land eller din region ännu.** |[!INCLUDE[prod_short](includes/prod_short.md)] stöder för närvarande endast Microsoft 365-e-postkonton som är registrerade på ett begränsat antal marknader. För mer information, se [Regional disposition](#regional-availability). |
| Personliga e-postadress som till exempel nancy@gmail.com stöds inte. Du får ett meddelande som följande under registreringen:<br /><br />**Du angav en personlig e-postadress: ange din e-postadress för arbetet så att vi kan lagra dina företagsdata på ett säkert sätt.**<br> eller <br> **Som ser ut som en personlig e-postadress. Ange din jobbadress så att vi kan ansluta dig till andra i företaget. Och oroa dig inte. Vi delar inte din adress med vem som helst.** |[!INCLUDE[prod_short](includes/prod_short.md)] har inte stöd för e-postadresser som tillhandahålls av e-posttjänster för konsumenter eller telekommunikationsleverantörer. För att slutföra registreringen kan du försöka igen genom att använda en e-postadress som tilldelats av ditt arbete eller skola. Om du fortfarande inte kan registrera dig och är villig att slutföra en mer avancerad installationsprocess kan du registrera dig för en ny Microsoft 365-provprenumeration och använda den e-postadressen till att registrera dig. |
| .gov eller .mil-e-postadress får du ett meddelande som följande under registrering:<br /><br />**[!INCLUDE[prod_short](includes/prod_short.md)] är inte tillgänglig: [!INCLUDE[prod_short](includes/prod_short.md)] är inte tillgängligt för användare med e-postadresser som t. ex. .gov eller .mil just nu. Använd en annan jobbadress eller med kom tillbaka senare.** <br>eller <br>**Vi kan inte lutföra registreringen. Det ser ut som att [!INCLUDE[prod_short](includes/prod_short.md)] inte är tillgängligt för ditt arbete eller skola.** |[!INCLUDE[prod_short](includes/prod_short.md)] har inte stöd för e-postadresserna .gov eller .mil för tillfället. |
| Registrering av Self Service har inte aktiverats. Du får ett meddelande som följande under registreringen:<br /><br />**Vi kan inte slutföra registreringen. IT-avdelningen har inaktiverat registrering för [!INCLUDE[prod_short](includes/prod_short.md)]. Kontakta dem för fullständig registrering.** <br>eller <br> **Som ser ut som en personlig e-postadress. Ange din jobbadress så att vi kan ansluta dig till andra i företaget. Och oroa dig inte. Vi delar inte din adress med vem som helst.** |Din organisations IT-administratör har inaktiverat registrering av Self Service för [!INCLUDE[prod_short](includes/prod_short.md)]. För att slutföra registreringen kontaktar du din IT-administratör och be dem att följa instruktionerna på sidan [denna sida](/dynamics365/business-central/dev-itpro/developer/devenv-business-central-manage-selfservice-signups) och låta nya användare gå med din [!INCLUDE[prod_short](includes/prod_short.md)] befintliga klientorganisation. Du kan även få detta problem om du registrerade dig för Microsoft 365 via en partner. |
| E-postadressen är inget Microsoft 365-ID. Du får ett meddelande som följande under registreringen:<br /><br />**Vi hittar inte dig på contoso.com. Använder du ett annat ID på arbetet eller i skolan? Försök logga in med det och om det inte fungerar kan du kontakta IT-avdelningen.** |Din organisation använder ID:n för att logga in på Microsoft 365 och andra Microsoft-tjänster som skiljer sig från din e-postadress. Din e-postadress kan till exempel vara Nancy.Smith@contoso.com men ditt ID är nancys@contoso.com. För att slutföra registreringen, använd det användar-ID som organisationen har tilldelat för att logga in på Microsoft 365 eller någon annan Microsoft-tjänst. Om du inte vet vad det är kontaktar du din IT-administratör. Om du fortfarande inte kan registrera dig och är villig att slutföra en mer avancerad installationsprocess, kan du registrera dig för en ny Microsoft 365-provprenumeration och använda den e-postadressen för att registrera dig. |
| Om ditt Microsoft 365-konto har registrerats i ett land som stöds och du registrerar dig för [!INCLUDE[prod_short](includes/prod_short.md)] i ett annat land, visas ett meddelande liknande följande i samband med registrering:<br /><br />**Vi har inte stöd för ditt land eller din region ännu.**| Organisationens Microsoft 365-prenumeration har registrerats för ett specifikt land i administrationsportalen för Microsoft 365. Registreringsupplevelsen för [!INCLUDE[prod_short](includes/prod_short.md)] använder samma språk och nationella inställningar som den aktuella webbläsaren, och därmed kan du få du felmeddelandet trots att du befinner dig i ett land som stöds. Be IT-administratören att kontrollera det land som anges i organisationsprofilen i [Microsoft 365-administrationsportalen](https://portal.office.com/adminportal/home#/companyprofile). Du kanske måste använda ett annat konto för [!INCLUDE[prod_short](includes/prod_short.md)].|

## Regional tillgänglighet

[!INCLUDE[prod_short](includes/prod_short.md)] är tillgänglig i ett antal länder eller regioner med lokalisering antingen av Microsoft eller en godkänd lokaliseringspartner. En fullständig lista över de länder och regioner som stöds finns i [Tillgänglighet för land/region och översättningar som stöds](/dynamics365/business-central/dev-itpro/compliance/apptest-countries-and-translations?toc=/dynamics365/business-central/toc.json).  

En översikt med de marknader som för närvarande stöds i Dynamics 365 finns i [Internationell tillgänglighet för Microsoft Dynamics 365](/dynamics365/get-started/availability). En översikt över lokala funktioner i [!INCLUDE[prod_short](includes/prod_short.md)] finns på landningssidan [lokal funktion](about-localization.md).  

## Se även

[Registrera dig för en kostnadsfri utvärderingsversion av Dynamics 365 Business Central](trial-signup.md)  
[FAQ för utvärderingsversionen av Dynamics 365 Business Central](trial-faq.md)  
[Välkommen till [!INCLUDE[prod_short](includes/prod_long.md)]](welcome.md)  
[Arbeta med [!INCLUDE[prod_short](includes/prod_short.md)]](ui-work-product.md)  
[Lokal funktionalitet](about-localization.md)  
[Tillgänglighet för land/region och översättningar som stöds](/dynamics365/business-central/dev-itpro/compliance/apptest-countries-and-translations?toc=/dynamics365/business-central/toc.json)  
[Internationella tillgängligheten för Microsoft Dynamics 365](/dynamics365/get-started/availability)  


[!INCLUDE[footer-include](includes/footer-banner.md)]