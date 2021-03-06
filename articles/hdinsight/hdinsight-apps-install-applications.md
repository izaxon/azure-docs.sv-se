---
title: "Installera Hadoop-program från tredje part i Azure HDInsight | Microsoft Docs"
description: "Lär dig hur du installerar Hadoop-program från tredje part i Azure HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: eaf5904d-41e2-4a5f-8bec-9dde069039c2
ms.service: hdinsight
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/06/2017
ms.author: jgao
translationtype: Human Translation
ms.sourcegitcommit: 8e7911a3a8080ef8fa125779aa1f6778b9655cde
ms.openlocfilehash: 8780c193c6aa4b6b183723f88d67ac0990347d1e


---
# <a name="install-third-party-hadoop-applications-on-azure-hdinsight"></a>Installera Hadoop-program från tredje part i Azure HDInsight

I den här artikeln lär du dig hur du installerar ett redan publicerat Hadoop-program från tredje part i Azure HDInsight. Anvisningar om hur du installerar ett eget program finns i [Installera anpassade HDInsight-program](hdinsight-apps-install-custom-applications.md).

Ett HDInsight-program är ett program som användarna kan installera på ett Linux-baserat HDInsight-kluster. Dessa program kan utvecklas av Microsoft, oberoende programvaruleverantörer och av dig själv.  

För närvarande finns det fyra publicerade program:

* **DATAIKU DDS på HDInsight**: Dataiku DSS (Data Science Studio) är en programvara som gör att dataspecialister (dataforskare, affärsanalytiker, utvecklare med flera) kan skapa prototyper samt bygga och distribuera specifika tjänster som omvandlar rådata till effektfulla affärsförutsägelser.
* **Datameer**: [Datameer](http://www.datameer.com/documentation/display/DAS50/Home?ls=Partners&lsd=Microsoft&c=Partners&cd=Microsoft) erbjuder analytiker ett interaktivt sätt att identifiera, analysera och visualisera resultat från stordata (Big Data). Hämta enkelt in fler datakällor för att identifiera nya relationer och snabbt få de svar du behöver.
* **Streamsets Data Collector för HDnsight** tillhandahåller en komplett integrerad utvecklingsmiljö (IDE) som du kan använda för att utforma, testa, distribuera och hantera pipelines för ”alla-till-alla”-inmatningar som kopplar ihop dataströms- och batchdata. Du kan också ta med olika interna dataströmstransformationer, allt utan att skriva anpassad kod. 
* **Cask CDAP 3.5 för HDInsight** är den första enhetliga integrationsplattformen för stordata som minskar tiden till produktion för dataprogram och datasjöar med 80 %. Det här programmet stöder endast Standard HBase 3.4-kluster.


I artikelns instruktioner används Azure-portalen. Du kan också exportera Azure Resource Manager-mallen från portalen eller skaffa en kopia av Resource Manager-mallen från leverantörer och distribuera mallen med Azure PowerShell och Azure CLI.  Mer information finns i [Skapa Linux-baserade Hadoop-kluster i HDInsight med hjälp av Resource Manager-mallar](hdinsight-hadoop-create-linux-clusters-arm-templates.md).

## <a name="prerequisites"></a>Krav
Om du vill installera HDInsight-program i ett befintligt HDInsight-kluster måste du ha ett HDInsight-kluster. Om du vill skapa ett läser du [Skapa kluster](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster). Du kan även installera HDInsight-program när du skapar ett HDInsight-kluster.

## <a name="install-applications-to-existing-clusters"></a>Installera program i befintliga kluster
I följande procedur beskriver vi hur du installerar HDInsight-program i ett befintligt HDInsight-kluster.

**Så här installerar du ett HDInsight-program**

1. Logga in på [Azure-portalen](https://portal.azure.com).
2. Klicka på **HDInsight-kluster** i den vänstra menyn.  Om du inte ser det klickar du på **Fler tjänster** och sedan på **HDInsight-kluster**.
3. Klicka på ett HDInsight-kluster.  Om du inte har något måste du skapa ett först.  Mer information finns i [Skapa kluster](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).
4. Klicka på **Program** under kategorin **Konfigurationer**. Du ser en lista över installerade program, om det finns några. Om du inte kan hitta Program innebär det att det inte finns några program för den här versionen av HDInsight-klustret.
   
    ![HDInsight-program – meny på portalen](./media/hdinsight-apps-install-applications/hdinsight-apps-portal-menu.png)
5. Klicka på **Lägg till** från bladets meny. 
   
    ![HDInsight-program – installerade appar](./media/hdinsight-apps-install-applications/hdinsight-apps-installed-apps.png)
   
    Du ser en lista över befintliga HDInsight-program.
   
    ![HDInsight-program – tillgängliga program](./media/hdinsight-apps-install-applications/hdinsight-apps-list.png)
6. Klicka på ett av programmen, godkänn de juridiska villkoren och klicka sedan på **Välj**.

Du kan se installationsstatusen i meddelandena på portalen (klicka på klockikonen överst på portalen). När programmet har installerats visas det på bladet Installerade appar.

## <a name="install-applications-during-cluster-creation"></a>Installera program när du skapar ett kluster
Du kan välja att installera HDInsight-program när du skapar ett kluster. Under processen installeras HDInsight-program när klustret har skapats och är i körläge. Följande steg beskriver hur du installerar HDInsight-program när du skapar ett kluster.

**Så här installerar du ett HDInsight-program**

1. Logga in på [Azure-portalen](https://portal.azure.com).
2. Klicka på **Nytt**, klicka på **Data + Analys** och sedan på **HDInsight**.
3. Ange **klusternamnet**: Det här namnet måste vara globalt unikt.
4. Klicka på **Prenumeration** och välj den Azure-prenumeration som du vill använda för klustret.
5. Klicka på **Välj typ av kluster** och välj sedan:
   
   * **Klustertyp**: Om du inte vet vad du ska välja väljer du **Hadoop**. Det är den mest populära klustertypen.
   * **Operativsystem**: Välj **Linux**.
   * **Version**: Använd standardversionen om du inte vet vad du ska välja. Mer information finns i [HDInsight-klusterversioner](hdinsight-component-versioning.md).
   * **Klusternivå**: Azure HDInsight tillhandahåller molntjänster för stordata i två kategorier: Premium- och standardnivå. Mer information finns i [Klusternivåer](hdinsight-hadoop-provision-linux-clusters.md#cluster-tiers).
6. Klicka på **Program**, klicka på något av de publicerade programmen och sedan på **Välj**.
7. Klicka på **Autentiseringsuppgifter** och ange ett lösenord för administratörsanvändaren. Du måste också ange ett **SSH-användarnamn** och antingen ett **lösenord** eller en **offentliga nyckel**, som används för att autentisera SSH-användaren. Den rekommenderade metoden är att använda en offentlig nyckel. Spara konfigurationen av autentiseringsuppgifterna genom att klicka på **Välj** längst ned.
8. Klicka på **Datakälla**, välj ett befintligt lagringskonto eller skapa ett nytt lagringskonto som ska användas som standardlagringskonto för klustret.
9. Klicka på **Resursgrupp** om du vill välja en befintlig resursgrupp eller på **Nytt** om du vill skapa en ny resursgrupp.
10. På bladet **Nytt HDInsight-kluster** kontrollerar du att **Fäst på startsidan** är valt och klickar sedan på **Skapa**. 

## <a name="list-installed-hdinsight-apps-and-properties"></a>Visa en lista med installerade HDInsight-appar och deras egenskaper
På portalen kan du visa en lista över de installerade HDInsight-programmen för ett kluster och egenskaperna för varje installerat program.

**Så här visar du en lista med HDInsight-program och deras egenskaper**

1. Logga in på [Azure-portalen](https://portal.azure.com).
2. Klicka på **HDInsight-kluster** i den vänstra menyn.  Om du inte ser det klickar du på **Bläddra** och sedan på **HDInsight-kluster**.
3. Klicka på ett HDInsight-kluster.
4. I bladet **Inställningar** klickar du på **Program** under kategorin **Allmänt**. På bladet Installerade appar visas alla installerade program. 
   
    ![HDInsight-program – installerade appar](./media/hdinsight-apps-install-applications/hdinsight-apps-installed-apps-with-apps.png)
5. Klicka på något av de installerade programmen för att visa egenskaperna. Egenskapsbladet innehåller:
   
   * Programnamn: programnamnet.
   * Status: programmets status. 
   * Webbsida: URL:en till den webbapp som du har distribuerat till gränsnoden om en sådan finns. Autentiseringsuppgifterna är samma som HTTP-autentiseringsuppgifterna som du har konfigurerat för klustret.
   * HTTP-slutpunkt: Autentiseringsuppgifterna är samma som HTTP-autentiseringsuppgifterna som du har konfigurerat för klustret. 
   * SSH-slutpunkt: Du kan använda [SSH](hdinsight-hadoop-linux-use-ssh-unix.md) för att ansluta till gränsnoden. SSH-autentiseringsuppgifterna är samma som SSH-autentiseringsuppgifterna som du har konfigurerat för klustret.
6. Om du vill ta bort ett program högerklickar du på programmet och klickar sedan på **Ta bort** på snabbmenyn.

## <a name="connect-to-the-edge-node"></a>Ansluta till gränsnoden
Du kan ansluta till gränsnoden med HTTP och SSH. Du kan hitta information om slutpunkten på [portalen](#list-installed-hdinsight-apps-and-properties). Mer information om hur du använder SSH finns i [Använda SSH med Linux-baserad Hadoop i Linux, Unix eller OS X HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md). 

Autentiseringsuppgifterna för HTTP-slutpunkten är HTTP-autentiseringsuppgifterna som du har konfigurerat för HDInsight-klustret. Autentiseringsuppgifterna för SSH-slutpunkten är SSH-autentiseringsuppgifterna som du har konfigurerat för HDInsight-klustret.

## <a name="troubleshoot"></a>Felsöka
Läs [Felsöka installationen](hdinsight-apps-install-custom-applications.md#troubleshoot-the-installation).

## <a name="next-steps"></a>Nästa steg
* [Installera anpassade HDInsight-program](hdinsight-apps-install-custom-applications.md): information om hur du distribuerar ett opublicerat HDInsight-program till HDInsight.
* [Publicera HDInsight-program](hdinsight-apps-publish-applications.md): information om hur du publicerar anpassade HDInsight-program på Azure Marketplace.
* [MSDN: Installera ett HDInsight-program](https://msdn.microsoft.com/library/mt706515.aspx): information om hur du definierar HDInsight-program.
* [Anpassa Linux-baserade HDInsight-kluster med skriptåtgärder](hdinsight-hadoop-customize-cluster-linux.md): information om hur du använder skriptåtgärd till att installera fler program.
* [Skapa Linux-baserade Hadoop-kluster i HDInsight med hjälp av Resource Manager-mallar](hdinsight-hadoop-create-linux-clusters-arm-templates.md): Lär dig hur du anropar Resource Manager-mallar för att skapa HDInsight-kluster.
* [Använda tomma edge-noder i HDInsight](hdinsight-apps-use-edge-node.md): Information om hur du använder en tom edge-nod för att få åtkomst till HDInsight-kluster, testa HDInsight-program och vara värd för HDInsight-program.




<!--HONumber=Feb17_HO3-->


