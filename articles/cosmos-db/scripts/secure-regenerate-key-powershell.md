---
title: Azure PowerShell Script generera Azure Cosmos DB kontonyckel | Microsoft Docs
description: Azure PowerShell skriptexempel - generera Azure Cosmos-DB-kontonyckel
services: cosmos-db
documentationcenter: cosmosdb
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 187d7b0839e1cd94122d4455c11eda05673f5acc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/11/2017
---
# <a name="regenerate-an-azure-cosmos-db-account-key-using-powershell"></a>Skapa ett Azure Cosmos DB kontonyckel med hjälp av PowerShell

Det här exemplet återskapar alla slags Azure Cosmos DB kontonyckel med hjälp av Azure CLI.  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a>Exempelskript

[!code-powershell[huvudsakliga](../../../powershell_scripts/cosmosdb/regenerate-account-keys/regenerate-account-keys.ps1?highlight=36-41 "återskapa Azure Cosmos DB nycklar")]

## <a name="clean-up-deployment"></a>Rensa distribution

Följande kommando kan användas för att ta bort resursgruppen och alla resurser som är associerade med den efter skriptexempel har körts.

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a>Skriptet förklaring

Det här skriptet använder följande kommandon. Varje kommando i tabellen länkar till kommandot viss dokumentation.

| Kommando | Anteckningar |
|---|---|
| [Ny AzureRmResourceGroup](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | Skapar en resursgrupp som är lagrade i alla resurser. |
| [Ny AzureRmResource](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | Skapar en logisk server som är värd för en databas eller elastisk pool. |
| [Anropa AzureRmResourceAction](https://docs.microsoft.com/powershell/module/azurerm.resources/invoke-azurermresourceaction?view=azurermps-3.8.0) | Anropar en åtgärd på CosmosDB Azure-konto. |
| [Ta bort AzureRmResourceGroup](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | Tar bort en resursgrupp, inklusive alla kapslade resurser. |
|||

## <a name="next-steps"></a>Nästa steg

Mer information om Azure PowerShell finns [Azure PowerShell dokumentationen](https://docs.microsoft.com/powershell/).

Ytterligare Azure Cosmos DB PowerShell skriptexempel finns i den [Azure Cosmos DB PowerShell-skript](../powershell-samples.md).