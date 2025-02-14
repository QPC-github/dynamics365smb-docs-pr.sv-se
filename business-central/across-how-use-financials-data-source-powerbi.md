---
title: Skapa rapporter i Power BI Desktop för att visa Business Central-data | Microsoft Docs
description: Gör din data tillgänglig som datakälla i Power BI och bygga kraftfulla rapporter av din verksamhets status.
author: jswymer
ms.topic: conceptual
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.search.keywords: 'business intelligence, KPI, Odata, Power App, SOAP, analysis'
ms.date: 09/07/2022
ms.author: jswymer
---

# <a name="building-power-bi-reports-to-display-include-prodlongincludesprodlongmd-data" />Skapa Power BI-rapporter för att visa [!INCLUDE [prod_long](includes/prod_long.md)]-data

Gör din [!INCLUDE[prod_long](includes/prod_long.md)]-data tillgänglig som datakälla i Power BI Desktop och bygga kraftfulla rapporter av din verksamhets status.

I den här artikeln beskrivs hur du kommer gång med att använda Power BI Desktop för att skapa rapporter som visar [!INCLUDE[prod_long](includes/prod_long.md)]-data.  När du har skapat en rapport kan du publicera den i din Power BI-tjänst eller dela den med samtliga användare i din organisation. När rapporten väl har publicerats i Power BI-tjänsten kan användare som konfigurerats för det se rapporten i [!INCLUDE[prod_long](includes/prod_long.md)].

## <a name="get-ready" />Gör dig redo

- Registrera dig frö Power BI-tjänsten.

  Gå till [https://powerbi.microsoft.com](https://powerbi.microsoft.com) om du inte redan har registrerat dig. När du registrerar dig använder du din e-postadress för arbetet samt ditt lösenord.

- Hämta [Power BI Desktop](https://powerbi.microsoft.com/desktop/).

  Power BI Desktop är ett kostnadsfritt program som du installerar lokalt på din dator. Mer information finns i [snabbstart: Anslut till data i Power BI Desktop](/power-bi/desktop-quickstart-connect-to-data).

- Se till att den data du vill inkludera i rapporten är tillgänglig som en API-sida eller publicerad som en webbtjänst.

  Mer information finns i [Visa data via API-sidor eller OData-webbtjänster](admin-powerbi-setup.md#exposedata).

- För [!INCLUDE[prod_short](includes/prod_short.md)] lokalt hämtar du följande information:

  - OData-URL för [!INCLUDE[prod_short](includes/prod_short.md)].
  
    Denna URL har vanligtvis formatet `http[s]://[computer]:[port]/[serverinstance]/ODataV4`, till exempel `https://localhost:7048/BC190/ODataV4`. Om du har en distribution med flera klientorganisationer bör du inkludera klientorganisationen i URL:en, till exempel `https://localhost:7048/BC190/ODataV4?tenant=tenant1`.
  - Att användarnamn och en åtkomstnyckel till en webbtjänst tillhörande ett [!INCLUDE[prod_short](includes/prod_short.md)]-konto.

    I syfte att hämta data från [!INCLUDE[prod_short](includes/prod_short.md)] använder Power BI grundläggande autentisering. Du behöver därför ett användarnamn och en åtkomstnyckel till en webbtjänst för att ansluta. Kontot kan vara ditt eget användarkonto, eller också kanske din organisation har ett specifikt konto i detta syfte.

- Ladda ned [!INCLUDE [prod_short](includes/prod_short.md)]-rapporttemat (valfritt).

  Mer information finns i [Använda [!INCLUDE [prod_short](includes/prod_short.md)]-rapporttemat](#theme) i denna artikel.

[!INCLUDE[note-multicompany-reports](includes/note-multicompany-reports.md)]

## <a name="a-namegetdataaadd-includeprodshortincludesprodshortmd-as-a-data-source-in-power-bi-desktop" /><a name="getdata"></a>Lägg till [!INCLUDE[prod_short](includes/prod_short.md)] som en datakälla i Power BI Desktop

Den första uppgiften i samband med att skapa rapporter är att lägga till [!INCLUDE[prod_short](includes/prod_short.md)] som en datakälla i Power BI Desktop. När du väl är ansluten kan du börja skapa rapporten.

1. Starta Power BI Desktop.
2. Välj **Hämta data**.

    Om du inte ser **Hämta data** väljer du menyn **Arkiv** och sedan **Hämta data**.
3. På sidan **Hämta data** väljer du **Onlinetjänster**.
4. I fönstret **Onlinetjänster** utför du ett av följande steg:

    - För att ansluta till [!INCLUDE [prod_short](includes/prod_short.md)] online, välj **Dynamics 365 Business Central**, sedan **Anslut**.
    - Om du vill ansluta till [!INCLUDE [prod_short](includes/prod_short.md)] lokalt markerar du **Dynamics 365 Business Central (lokalt)** och **ansluter** sedan.

5. Logga in till [!INCLUDE [prod_short](includes/prod_short.md)] (endast en gång).

    Om du inte har loggat in på [!INCLUDE [prod_short](includes/prod_short.md)] från Power BI desktop förut ombeds du att logga in.

    - För [!INCLUDE [prod_short](includes/prod_short.md)] online, välj **Logga in** och sedan tillhörande konto. Använd samma konto som du använder för att logga in på [!INCLUDE [prod_short](includes/prod_short.md)]. När du är klar, välj **Anslut**.

    - För [!INCLUDE [prod_short](includes/prod_short.md)] lokalt, ange först OData URL för [!INCLUDE[prod_short](includes/prod_short.md)], och välj sedan **OK**. Därefter anger du (på uppmaning) användarnamn och lösenord för det konto som ska användas för att ansluta till [!INCLUDE[prod_short](includes/prod_short.md)]. I rutan **Lösenord** anger du åtkomstnyckeln för webbtjänsten. När du är klar, välj **Anslut**.

    > [!NOTE]  
    > När du väl har anslutit till [!INCLUDE[prod_short](includes/prod_short.md)] kommer du inte uppmanas att logga in en gång till. [Hur ändrar jag eller avmarkerar jag det konto som jag använder för att ansluta till Business Central från Power BI Desktop?](/dynamics365/business-central/power-bi-faq?tabs=designer#perms)

6. När ansluten Power BI kontakten är till Business Central-tjänsten. **Navigator** fönstren visas och visar tillgängliga data källor för att skapa rapporter. Markera en mapp för att expandera den och se tillgängliga datakällor. 

   Dessa datakällor representerar samtliga de webbtjänster och AP-sidor som har publicerats för [!INCLUDE [prod_short](includes/prod_short.md)]. Datakällorna grupperas enligt de Business Central-miljöerna och företagen. Med Business Central online har **Navigator** följande struktur:

    - **Miljönamn**
      - **Företagsnamn**
        - **Avancerade API:er**

          I den här mappen visas avancerade API-sidor som publicerats av Microsoft, till exempel [API-automatisering för Business Central](/dynamics365/business-central/dev-itpro/administration/itpro-introduction-to-automation-apis) och [anpassade API-sidor för Business Central](/dynamics365/business-central/dev-itpro/developer/devenv-develop-custom-api). Anpassade API-sidor grupperas ytterligare i mappar av [APIPublisher](/dynamics365/business-central/dev-itpro/developer/properties/devenv-apipublisher-property)-/[APIGroup](/dynamics365/business-central/dev-itpro/developer/properties/devenv-apigroup-property)-egenskaper för API-sidans källkod.

        - **Standard APIs v2.0**

          I den här mappen listas de API-sidor som visas av [Business Central API V2.0](/dynamics365/business-central/dev-itpro/api-reference/v2.0/).

        - **Webbtjänster \(äldre)**

          I den här mappen visas sidor, kodenheter och frågor som publiceras som webbtjänster inom Business Central.

    > [!NOTE]
    > Strukturen för Business Central lokalt skiljer sig åt eftersom den inte stöder API-sidor.

7. Välj datakälla eller källor som du vill lägga till i din datamodell och välj knappen **Läs in**.
8. Om du senare vill lägga till fler Business Central-data kan du upprepa föregående steg.

När datan har lästs in kan du se den i den högra navigeringen på sidan. Vid denna tidpunkt har du anslutit till dina [!INCLUDE[prod_short](includes/prod_short.md)]-data och kan börja skapa din Power BI-rapport.  

> [!TIP]
> Mer information om hur du använder Power BI Desktop finns i [Komma igång med Power BI Desktop](/power-bi/fundamentals/desktop-getting-started).

## <a name="creating-accessible-reports" />Skapa tillgängliga rapporter

Det är viktigt att du gör dina rapporter användbara för så många personer som möjligt. Försök att utforma rapporter så att de inte kräver någon särskild anpassning för att uppfylla olika behov hos olika användare. Kontrollera att designen tillåter användare att utnyttja vanliga hjälpmedelstekniker, som skärmläsare. Power BI innehåller olika hjälpmedelsfunktioner, verktyg och riktlinjer som hjälper dig att uppnå detta mål. Mer information får du genom att [utforma Power BI-rapporter för tillgänglighet](/power-bi/create-reports/desktop-accessibility-creating-reports) i Power BI-dokumentationen.

## <a name="creating-reports-to-display-data-associated-with-a-list" />Skapa rapporter för att visa data kopplade till en lista

Du kan skapa rapporter som visas i en FactBox tillhörande en [!INCLUDE [prod_short](includes/prod_short.md)]-listsida. Rapporterna kan innehålla data om den post som har valts i listan. Du skapar dessa rapporter på i princip samma sätt som du skapar andra rapporter, förutom att det finns några saker som du måste göra för att rapporten ska visas på avsett sätt. Mer information finns i [Skapa Power BI-rapporter som ska visa listdata i [!INCLUDE[prod_short](includes/prod_short.md)]](across-how-use-powerbi-reports-factbox.md).

## <a name="a-namethemeausing-the-include-prodshortincludesprodshortmd-report-theme-optional" /><a name="theme"></a>Använda [!INCLUDE [prod_short](includes/prod_short.md)]-rapporttemat (tillval)

Innan du skapar din rapport rekommenderar vi att du laddar ned samt importerar [!INCLUDE [prod_short](includes/prod_short.md)]-temafilen. Temafilen skapar en färgpalett så att du kan skapa rapporter med samma färgdesign som [!INCLUDE [prod_short](includes/prod_short.md)]-apparna utan att du behöver ange färger för respektive grafik.

> [!NOTE]
> Denna uppgift är valfri. Du kan alltid skapa dina rapporter och sedan ladda ned och tillämpa designmallen senare.

### <a name="download-the-theme" />Hämta temat

Temafilen finns som json-fil i temagalleriet för Microsoft Power BI Community. Utför följande steg för att ladda ned temafilen:

1. Gå till [Temagalleriet för Microsoft Power BI Community för Microsoft Dynamics 365 Business Central](https://community.powerbi.com/t5/Themes-Gallery/Microsoft-Dynamics-365-Business-Central/m-p/385875).
2. Välj nedladdningsbilagan **Microsoft Dynamics Business Central.json**.

### <a name="import-the-theme-on-a-report" />Importera temat i en rapport

När du har laddat ned [!INCLUDE [prod_short](includes/prod_short.md)]-rapporttemat kan du importera det i din rapport. Om du vill importera uppställningen väljer du **Visa** > **Teman** > **Bläddra efter uppställningar**. Mer information finns i [Power BI Desktop – Importera anpassade rapportuppställningar](/power-bi/create-reports/desktop-report-themes#import-custom-report-theme-files).

## <a name="publish-reports" />Publicera rapporter

När du har skapat eller ändrat en rapport kan du publicera rapporten i din Power BI-tjänst samt dela den med andra i din organisation. När rapporten har publicerats kan du se den i Power BI. Rapporten görs också tillgänglig för val i [!INCLUDE[prod_short](includes/prod_short.md)].

Om du vill publicera en rapport väljer du **Publicera** i fliken **Start** i menyfliksområdet eller i menyn **Arkiv**. Om du har loggat in på Power BI-tjänsten publiceras rapporten i denna tjänst. I annat fall uppmanas du att logga in. 

## <a name="distribute-or-share-a-report" />Distribuera eller dela en rapport

Det finns ett antal olika sätt att skicka rapporter till dina medarbetare och andra:

- Distribuera rapporter som .pbix-filer.

    Rapporter lagras som .pbix-filer på din dator. Du kan distribuera .pbix-rapportfilen till användarna precis som vilken fil som helst. Därefter kan användarna ladda upp filen till sin Power BI-tjänst. Se [Ladda upp rapporter från filer](across-working-with-business-central-in-powerbi.md#upload).

    > [!NOTE]
    > Att distribuera rapporter på detta sätt innebär att datauppdateringen för rapporter utförs individuellt av respektive användare. Denna situation kan komma att påverka [!INCLUDE[prod_short](includes/prod_short.md)]-prestandan.

- Dela rapport från din Power BI-tjänst

    Om du har en Power BI Pro-licens kan du dela rapporten med andra direkt från din Power BI-tjänst. Mer information finns i [Power BI – Dela en instrumentpanel eller rapport](/power-bi/collaborate-share/service-share-dashboards#share-a-dashboard-or-report).

## <a name="fixing-problems" />Åtgärda problem

### <a name="cannot-insert-a-record-current-connection-intent-is-read-only-error-connecting-to-custom-api-page" />"Det går inte att infoga en post. Den aktuella anslutningens syfte är Skrivskyddad." fel vid anslutning till anpassad API-sida

> **GÄLLER:** Business Central online

Från och med februari 2022 kommer nya rapporter som använder Business Central-data att anslutas till en skrivskyddad kopia av Business Central-databasen som standard. I sällsynta fall visas ett felmeddelande, beroende på siddesignen, när du försöker ansluta till och hämtar data från sidan.

1. Starta Power BI Desktop.
2. I menyfliksområdet väljer du **Hämta data** > **Onlinetjänster**.
3. I fönstret **Onlinetjänster** väljer du **Dynamics 365 Business Central** och sedan **Anslut**.
4. I fönstret **Navigator** väljer du den API-ändpunkt som du vill läsa in data från.
5. I förhandsgranskningen till höger visas följande felmeddelande:

   *Dynamics365BusinessCentral: Begäran misslyckades: Fjärrservern returnerade ett fel: (400) Felaktig begäran. (Det går inte att infoga en post. Den aktuella anslutningens syfte är Skrivskyddad. CorrelationId: [...])".*

6. Välj **Omvandla data** istället för **Läs in** som du kanske brukar göra.
7. I **Power Query-redigeraren** väljer du **Avancerad redigerare** i menyfliksområdet.
8. På raden som börjar med **Källa =** ersätter du följande text:

   ```
   Dynamics365BusinessCentral.ApiContentsWithOptions(null, null, null, null)
   ```

   med:

   ```
   Dynamics365BusinessCentral.ApiContentsWithOptions(null, null, null, [UseReadOnlyReplica = false])
   ```

9. Välj **Utfört**.
10. Välj **Stäng och tillämpa** i menyfliksområdet för att spara ändringarna och stäng Power Query-redigeraren.

## <a name="see-related-microsoft-trainingtrainingmodulesconfigure-powerbi-excel-dynamics-365-business-centralindex" />Se relaterad [Microsoft utbildning](/training/modules/configure-powerbi-excel-dynamics-365-business-central/index)

## <a name="see-also" />Se även

[Aktivera dina affärsdata för Power BI](admin-powerbi.md)  
[Affärsstöd](bi.md)  
[Gör dig redo att göra affärer](ui-get-ready-business.md)  
[Importera affärsdata från andra finanssystem](across-import-data-configuration-packages.md)  
[Ställa in [!INCLUDE[prod_short](includes/prod_short.md)]](setup.md)  
[Ekonomi](finance.md)  
[Snabbstart: Ansluta till data i Power BI Desktop](/power-bi/desktop-quickstart-connect-to-data)  


[!INCLUDE[footer-include](includes/footer-banner.md)]
