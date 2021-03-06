---
title: Nyckeln valvet .NET-API 2.x viktig information | Microsoft Docs
description: ".NET-utvecklare använder detta API till kod för Azure Key Vault"
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
editor: bruceper
ms.assetid: 1cccf21b-5be9-4a49-8145-483b695124ba
ms.service: key-vault
ms.devlang: CSharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/02/2017
ms.author: bruceper
ms.openlocfilehash: c5b5fd7f16faf17d16ecc82269fb1264adf4dd06
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/11/2017
---
# <a name="azure-key-vault-net-20---release-notes-and-migration-guide"></a>Azure Key Vault .NET 2.0 - viktig information och Migreringsguide
Följande information och vägledning är för utvecklare som arbetar med Azure Key Vault .NET / C#-biblioteket. I övergången från version 1.0 till version 2.0 kan ett antal uppdateringar har gjorts som kräver migrering arbete i koden för att du kan dra nytta av de funktionella förbättringarna och funktion som tillägg kommer **Key Vault-certifikat**  stöder.

## <a name="key-vault-certificates"></a>Key Vault-certifikat

Stöd för Key Vault-certifikat ger hantering av din x509 certifikat och följande:  

* Gör en certifikat-ägare att skapa ett certifikat via en process för att skapa Nyckelvalvet eller importera ett befintligt certifikat. Detta inkluderar både självsignerat och certifikatutfärdare genereras certifikat.
* Gör en Key Vault certifikat ägare att implementera säker lagring och hantering av X509 certifikat utan interaktion med material för privat nyckel.  
* Gör en certifikat-ägare att skapa en princip som leder Key Vault för att hantera livscykeln för ett certifikat.  
* Gör att certifikatet ägare att tillhandahålla kontaktinformation för meddelande om livscykeln händelser för förfallodatum och förnyelse av certifikat.  
* Stöder automatisk förnyelse med valda utfärdare - Key Vault partner X509 certifikat providers / certifikatutfärdare.
  
  * Observera - ej tillsammans providers/myndigheter kan också, men stöder inte automatisk förnyelse av funktionen.

## <a name="net-support"></a>Stöd för .NET

* **.NET 4.0** stöds inte av version 2.0 av Azure Key Vault .NET / C#-biblioteket
* **.NET core** stöds av version 2.0 av Azure Key Vault .NET / C#-biblioteket

## <a name="namespaces"></a>namnområden

* Namnområdet för **modeller** ändras från **Microsoft.Azure.KeyVault** till **Microsoft.Azure.KeyVault.Models**.
* Den **Microsoft.Azure.KeyVault.Internal** namnområde har släppts.
* Azure SDK beroenden namnområdet ändras från **Hyak.Common** och **Hyak.Common.Internals** till **Microsoft.Rest** och  **Microsoft.Rest.Serialization**

## <a name="type-changes"></a>Ändringar av typen

* *Hemligt* ändras till *SecretBundle*
* *Ordlistan* ändras till *IDictionary*
* *Lista<T>, string []* ändras till *IList<T>*
* *NextList* ändras till *NextPageLink*

## <a name="return-types"></a>Returtyper

* **KeyList** och **SecretList** returnerar *IPage<T>*  i stället för *ListKeysResponseMessage*
* Den genererade **BackupKeyAsync** returnerar *BackupKeyResult* som innehåller *värdet* (säkerhetskopiera blob). Innan metoden har omslutna och returnerar värdet.

## <a name="exceptions"></a>Undantag

* *KeyVaultClientException* ändras till *KeyVaultErrorException*
* Fel i tjänsten har ändrats från *undantag. Fel* till *undantag. Body.Error.Message*.
* Ytterligare information bort från felmeddelandet för **[JsonExtensionData]**.

## <a name="constructors"></a>Konstruktorer

* I stället för att acceptera ett *HttpClient* som ett konstruktorargument konstruktorn accepterar bara *HttpClientHandler* eller *DelegatingHandler []*.

## <a name="downloaded-packages"></a>Hämtade paket

När en klient beroende av Key Vault hämtades följande

### <a name="previous-package-list"></a>Tidigare paketlistan

* paketet id="Hyak.Common” version = ”1.0.2” targetFramework = ”net45”
* paketet id="Microsoft.Azure.Common” version = ”2.0.4” targetFramework = ”net45”
* paketet id="Microsoft.Azure.Common.Dependencies” version = ”1.0.0” targetFramework = ”net45”
* paketet id="Microsoft.Azure.KeyVault” version = ”1.0.0” targetFramework = ”net45”
* paketet id="Microsoft.Bcl” version = ”1.1.9” targetFramework = ”net45”
* paketet id="Microsoft.Bcl.Async” version = ”1.0.168” targetFramework = ”net45”
* paketet id="Microsoft.Bcl.Build” version = ”1.0.14” targetFramework = ”net45”
* paketet id="Microsoft.Net.Http” version = ”2.2.22” targetFramework = ”net45”

### <a name="current-package-list"></a>Aktuella paketlistan

* paketet id="Microsoft.Azure.KeyVault” version = ”2.0.0-preview” targetFramework = ”net45”
* paketet id="Microsoft.Rest.ClientRuntime” version = ”2.2.0” targetFramework = ”net45”
* paketet id="Microsoft.Rest.ClientRuntime.Azure” version = ”3.2.0” targetFramework = ”net45”

## <a name="class-changes"></a>Klassen ändringar

* **UnixEpoch** klass har tagits bort
* **Base64UrlConverter** klass har bytt namn till **Base64UrlJsonConverter**

## <a name="other-changes"></a>Andra ändringar

* Stöd för konfigurationen av KV åtgärden återförsöksprincip på tillfälliga fel har lagts till den här versionen av API: et.

## <a name="microsoftazuremanagementkeyvault-nuget"></a>Microsoft.Azure.Management.KeyVault NuGet

* För de åtgärder som returnerade en *valvet*, Returtypen har en klass som innehåller en egenskap för valvet. Returtypen är nu *valvet*.
* *PermissionsToKeys* och *PermissionsToSecrets* är nu *Permissions.Keys* och *Permissions.Secrets*
* Några av de returtyper ändringarna gäller för kontrollen-plan samt.

## <a name="microsoftazurekeyvaultextensions-nuget"></a>Microsoft.Azure.KeyVault.Extensions NuGet

* Paketet har brutits till **Microsoft.Azure.KeyVault.Extensions** och **Microsoft.Azure.KeyVault.Cryptography** för kryptografiska åtgärder.

