---
title: "Kom igång med Azure Service Fabric CLI"
description: "Lär dig hur du använder Azure Service Fabric CLI. Lär dig hur du ansluter till ett kluster och hanterar program."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 08/22/2017
ms.author: edwardsa
ms.translationtype: HT
ms.sourcegitcommit: fda37c1cb0b66a8adb989473f627405ede36ab76
ms.openlocfilehash: 851f04c8b5eee762ec43060f02c8b83f00c1782e
ms.contentlocale: sv-se
ms.lasthandoff: 09/14/2017

---
# <a name="azure-service-fabric-cli"></a>Azure Service Fabric CLI

Azure Service Fabric-kommandoradsgränssnittet (CLI) är ett kommandoradsverktyg för att interagera med och hantera Service Fabric-enheter. Service Fabric CLI kan användas med antingen Windows- eller Linux-kluster. Service Fabric CLI kan köras på valfri plattform där Python stöds.

## <a name="prerequisites"></a>Krav

Kontrollera att din miljö har både Python och pip installerade före installationen. Mer information finns i [snabbstartdokumentationen för pip](https://pip.pypa.io/en/latest/quickstart/) och den officiella [dokumentationen för installation av Python](https://wiki.python.org/moin/BeginnersGuide/Download).

Även om både Python 2.7 och 3.6 stöds, rekommenderar vi att du använder Python 3.6. Följande avsnitt visar hur du installerar alla krav och CLI.

## <a name="install-pip-python-and-the-service-fabric-cli"></a>Installera pip, Python och Service Fabric CLI

 Du kan installera pip och Python på din plattform på många olika sätt. Följande är anvisningar för att snabbt komma igång med Python 3.6 och pip på populära operativsystem.

### <a name="windows"></a>Windows

I Windows 10, Windows Server 2016 och Windows Server 2012 R2 använder du de officiella anvisningarna för standardinstallation. Python-installationsprogrammet installerar även pip som standard.

1. Gå till den officiella [nedladdningssidan för Python](https://www.python.org/downloads/) och ladda ned den senaste versionen av Python 3.6.

2. Starta installationsprogrammet.

3. Längst ned i fönstret väljer du **Add Python 3.6 to PATH** (lägg till Python 3.6 i PATH).

4. Välj **Installera nu** och slutför installationen.

Nu kan du öppna ett nytt kommandofönster och hämta versionen för Python och pip.

```bat
python --version
pip --version
```

Kör sedan följande kommando för att installera Service Fabric CLI:

```
pip install sfctl
sfctl -h
```

### <a name="ubuntu"></a>Ubuntu

I Ubuntu 16.04 Desktop kan du installera Python 3.6 med ett PPA-arkiv (Personal Package Archive) från tredje part.

Kör följande kommandon från terminalen:

```bash
sudo add-apt-repository ppa:jonathonf/python-3.6
sudo apt-get update
sudo apt-get install python3.6
sudo apt-get install python3-pip
```

Om du vill installera Service Fabric CLI för endast din installation av Python 3.6, kör du följande kommando:

```bash
python3.6 -m pip install sfctl
sfctl -h
```

De här stegen påverkar inte systeminstallationen av Python 3.5 och 2.7. Försök inte ändra de här installationerna om du inte är bekant med Ubuntu.

### <a name="macos"></a>MacOS

För MacOS rekommenderar vi att du använder [HomeBrew-pakethanteraren](https://brew.sh). Installera HomeBrew om det inte är installerat genom att köra följande kommando:

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Installera sedan Python 3.6, pip och Service Fabric CLI från terminalen genom att köra följande kommandon:

```bash
brew install python3
pip3 install sfctl
sfctl -h
```

De här stegen ändrar inte installationen av Python 2.7.

## <a name="cli-syntax"></a>CLI-syntax

Kommandon inleds alltid med prefixet `sfctl`. För allmän information om alla kommandon du kan använda använder du `sfctl -h`. För hjälp med ett enda kommando, använd `sfctl <command> -h`.

Kommandon följer en upprepningsbar struktur, där kommandots mål står före verbet eller åtgärden.

```azurecli
sfctl <object> <action>
```

I det här exemplet är `<object>` målet för `<action>`.

## <a name="select-a-cluster"></a>Välj ett kluster

Innan du kan utföra några åtgärder måste du välja ett kluster att ansluta till. Kör till exempel följande kommando för att välja och ansluta till klustret med namnet `testcluster.com`:

> [!WARNING]
> Använd inte oskyddade Service Fabric-kluster i produktionsmiljöer.

```azurecli
sfctl cluster select --endpoint http://testcluster.com:19080
```

Klusterslutpunkten måste föregås av `http` eller `https`. Det måste innehålla porten för HTTP-gateway. Den här porten och adressen är samma som webbadressen för Service Fabric Explorer.

För kluster som skyddas med ett certifikat kan du ange ett PEM-kodat certifikat. Certifikatet kan anges som en enda fil eller ett par med certifikat och nyckel.

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

Mer information finns i [Ansluta till ett Azure Service Fabric-kluster](service-fabric-connect-to-secure-cluster.md).

## <a name="basic-operations"></a>Grundläggande åtgärder

Klustrets anslutningsinformation bevaras mellan olika Service Fabric CLI-sessioner. När du har valt ett Service Fabric-kluster kan du köra alla Service Fabric-kommandon på klustret.

Om du till exempel vill se hälsotillståndet för Service Fabric-klustret kör du följande kommando:

```azurecli
sfctl cluster health
```

Kommandot ger följande utdata:

```json
{
  "aggregatedHealthState": "Ok",
  "applicationHealthStates": [
    {
      "aggregatedHealthState": "Ok",
      "name": "fabric:/System"
    }
  ],
  "healthEvents": [],
  "nodeHealthStates": [
    {
      "aggregatedHealthState": "Ok",
      "id": {
        "id": "66aa824a642124089ee474b398d06a57"
      },
      "name": "_Test_0"
    }
  ],
  "unhealthyEvaluations": []
}
```

## <a name="tips-and-troubleshooting"></a>Felsökning och tips

Här följer några förslag och tips för lösning av vanliga problem.

### <a name="convert-a-certificate-from-pfx-to-pem-format"></a>Konvertera ett certifikat från PFX till PEM

Service Fabric CLI har stöd för certifikat på klientsidan i form av PEM-filer (.pem-filtillägg). Om du använder PFX-filer från Windows måste du konvertera dessa certifikat till PEM-format. Om du vill konvertera en PFX-fil till en PEM-fil använder du följande kommando:

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

Mer information finns i [OpenSSL-dokumentationen](https://www.openssl.org/docs/).

### <a name="connection-problems"></a>Anslutningsproblem

Vissa åtgärder kan generera följande meddelande:

`Failed to establish a new connection: [Errno 8] nodename nor servname provided, or not known`

Kontrollera att den angivna kluster-slutpunkten är tillgänglig och lyssnar. Kontrollera också att gränssnittet för Service Fabric Explorer kan nås på denna värd och port. Använd `sfctl cluster select` till att uppdatera slutpunkten.

### <a name="detailed-logs"></a>Detaljerade loggar

Detaljerade loggar är ofta användbara när du felsöker eller rapporterar problem. En global `--debug`-flagga ökar detaljnivån i loggfilerna.

### <a name="command-help-and-syntax"></a>Hjälp och syntax för kommandon

Om du vill ha hjälp med ett visst kommando eller en grupp med kommandon, använder du flaggan `-h`.

```azurecli
sfctl application -h
```

Här är ett annat exempel:

```azurecli
sfctl application create -h
```

## <a name="next-steps"></a>Nästa steg

* [Distribuera ett program med Azure Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md)
* [Kom igång med Service Fabric på Linux](service-fabric-get-started-linux.md)

