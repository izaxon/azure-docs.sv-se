---
title: Arbeta med Azure Application Insights i Visual Studio | Microsoft Docs
description: "Prestandaanalys och diagnostik för webbappar vid felsökning och i produktion."
services: application-insights
documentationcenter: .net
author: alancameronwills
manager: carmonm
ms.assetid: 2059802b-1131-477e-a7b4-5f70fb53f974
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/17/2016
ms.author: awills
translationtype: Human Translation
ms.sourcegitcommit: 0d8472cb3b0d891d2b184621d62830d1ccd5e2e7
ms.openlocfilehash: 7fe1b572104416fec62261c60228fa966d197dd9
ms.lasthandoff: 03/21/2017


---
# <a name="working-with-azure-application-insights-in-visual-studio"></a>Arbeta med Azure Application Insights i Visual Studio
I Visual Studio (2015 och senare) kan du analysera prestanda och diagnostisera problem i din ASP.NET-webbapp både när du felsöker och i produktion med hjälp av telemetri från [Azure Application Insights](app-insights-overview.md).

Om du har skapat din ASP.NET-webbapp med Visual Studio 2017 eller senare har den redan Application Insights SDK. I annat fall [lägger du till Application Insights i din app](app-insights-asp-net.md), om du inte redan gjort det.

När appen är live i produktion visar du normalt Application Insights-telemetrin på [Azure Portal](https://portal.azure.com). Där kan du också ställa in aviseringar och använda kraftfulla övervakningsverktyg. Men när det gäller felsökning kan du också söka efter och analysera telemetri i Visual Studio. Med Visual Studio kan du analysera telemetri både från din produktionsplats och från felsökningskörningar på din utvecklingsdator. I det senare fallet kan du analysera felsökningskörningar även om du inte har konfigurerat SDK för att skicka telemetri till Azure Portal ännu. 

## <a name="run"></a> Felsöka ditt projekt
Kör din webbapp i lokalt felsökningsläge genom att välja F5. Öppna olika sidor för att skapa viss telemetri.

I Visual Studio visas antalet händelser som har loggats av modulen Application Insights i projektet.

![I Visual Studio visas knappen Application Insights när du felsöker.](./media/app-insights-visual-studio/appinsights-09eventcount.png)

Klicka på den här knappen om du vill söka i telemetri. 

## <a name="application-insights-search"></a>Söka med Application Insights
I sökfönstret för Application Insights visas händelser som har loggats. (Om du är inloggad i Azure när du konfigurerar Application Insights kan du söka efter samma händelser på Azure Portal.)

![Högerklicka på projektet och välj Application Insights, Sök](./media/app-insights-visual-studio/34.png)

> [!NOTE] 
> När du har markerat eller avmarkerat filter klickar du på knappen Sök i slutet av sökfältet.
>

Fritextsökningen fungerar för alla fält i händelserna. Du kan till exempel söka efter en del av URL-adressen för en sida, efter värdet för en egenskap, t.ex. klientens stad, eller efter specifika ord i en spårningslogg.

Klicka på en händelse om du vill visa händelsens detaljerade egenskaper.

För begäranden till webbappen kan du klicka vidare till koden.

![Under Information om begäran klickar du vidare till koden.](./media/app-insights-visual-studio/31.png)

Du kan också öppna relaterade objekt för att diagnostisera misslyckade begäranden eller undantag.

![Rulla ned till relaterade artiklar under Information om begäran](./media/app-insights-visual-studio/41.png)

## <a name="exceptions-and-failed-requests"></a>Undantag och misslyckade begäranden
Undantagsrapporter visas i sökfönstret. (I vissa äldre versioner av ASP.NET måste du [konfigurera undantagsövervakning](app-insights-asp-net-exceptions.md) för att se undantagen som hanteras av ramverket.)

Klicka på ett undantag för att visa en stackspårning. Om koden för appen är öppen i Visual Studio kan du klicka dig igenom från stackspårningen till relevant kodrad.

![Undantag för stackspårning](./media/app-insights-visual-studio/17.png)

## <a name="request-and-exception-summaries-in-the-code"></a>Sammanfattningar av begäranden och undantag i koden
Antalet begäranden och undantag som loggats av Application Insights de senaste 24 timmarna visas på CodeLens-raden ovanför varje hanterarmetod.

![Undantag för stackspårning](./media/app-insights-visual-studio/21.png)

> [!NOTE] 
> CodeLens visar Application Insights-data endast om du har [konfigurerat appen för att skicka telemetri till Application Insights-portalen](app-insights-asp-net.md).
>

[Läs mer om Application Insights i CodeLens](app-insights-visual-studio-codelens.md)

## <a name="trends"></a>Trends
Trends är ett verktyg för visualisering av hur din app ska bete sig över tiden. 

Välj **Utforska telemetritrender** med verktygsfältsknappen eller sökfönstret för Application Insights. Välj en av fem vanliga frågor för att komma igång. Du kan analysera olika datauppsättningar baserat på telemetrityper, tidsintervall och andra egenskaper. 

För att hitta avvikelser i dina data väljer du ett av avvikelsealternativen i listrutan ”Vytyp”. Filtreringsalternativen längst ned i fönstret gör det lättare att justera efter specifika delmängder av dina telemetri.

![Trends](./media/app-insights-visual-studio/51.png)

[Mer om Trends](app-insights-visual-studio-trends.md).

## <a name="local-monitoring"></a>Lokal övervakning
(Från och med Visual Studio 2015 Update 2) Om du inte har konfigurerat SDK för att skicka telemetri till Application Insights-portalen (så att det inte finns någon instrumentationsnyckel i ApplicationInsights.config) visar diagnostikfönstret telemetri från din senaste felsökningssession. 

Detta är lämpligt om du redan har publicerat en tidigare version av din app. Du vill undvika att telemetri från dina felsökningssessioner blandas med telemetrin på Application Insights-portalen från den publicerade appen.

Det är också användbart om du har [anpassad telemetri](app-insights-api-custom-events-metrics.md) som du vill felsöka innan du skickar telemetri till portalen.

* *Först konfigurerade jag Application Insights att skicka telemetrin till portalen. Men nu vill jag bara visa telemetrin i Visual Studio.*
  
  * I sökfönstrets inställningar finns det ett alternativ för att söka i lokal diagnostik även om din app skickar telemetri till portalen.
  * Om du inte vill att telemetri ska skickas till portalen längre kommenterar du bort raden `<instrumentationkey>...` i ApplicationInsights.config. När du vill skicka telemetri till portalen igen avkommenterar du raden.


## <a name="whats-next"></a>Nästa steg
|  |  |
| --- | --- |
| **[Lägga till mer information](app-insights-asp-net-more.md)**<br/>Övervaka användning, tillgänglighet, beroenden och undantag. Integrera spårningar från loggningsramverk. Skriv anpassad telemetri. |![Visual Studio](./media/app-insights-visual-studio/64.png) |
| **[Arbeta med Application Insights-portalen](app-insights-dashboards.md)**<br/>Instrumentpaneler, kraftfulla verktyg för diagnostik och analys, aviseringar, live-mappning över beroenden för din app och telemetriexport. |![Visual Studio](./media/app-insights-visual-studio/62.png) |


