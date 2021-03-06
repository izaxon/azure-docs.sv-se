---
title: "Förbered Azure-resurser att replikera lokala fysiska servrar till Azure med Azure Site Recovery | Microsoft Docs"
description: "Beskriver vad du behöver på plats i Azure innan du börjar lokala servrar som replikerar till Azure med Azure Site Recovery-tjänsten"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 4e320d9b-8bb8-46bb-ba21-77c5d16748ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/25/2017
ms.author: raynew
ms.openlocfilehash: b7411fa6aba04ffd34f3f4bd03e706ca75afc9c8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/29/2017
---
# <a name="step-5-prepare-azure-resources-for-physical-server-replication-to-azure"></a>Steg 5: Förbered Azure-resurser för fysisk serverreplikering till Azure


Följ instruktionerna i den här artikeln för att förbereda Azure-resurser så att du kan replikera lokala servrar till Azure med hjälp av [Azure Site Recovery](site-recovery-overview.md) service.

Publicera kommentarer och frågor längst ned i den här artikeln eller i den [Azure Recovery Services-forumet](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="before-you-start"></a>Innan du börjar

Kontrollera att du har läst den [krav](physical-walkthrough-prerequisites.md).

## <a name="set-up-an-azure-account"></a>Konfigurera ett Azure-konto

- Hämta en [Microsoft Azure-konto](http://azure.microsoft.com/).
- Du kan börja med en [kostnadsfri utvärderingsversion](https://azure.microsoft.com/pricing/free-trial/).
- Kontrollera regionerna som stöds för Site Recovery under **geografisk tillgänglighet** i [Azure Site Recovery-prisinformation](https://azure.microsoft.com/pricing/details/site-recovery/).
- Lär dig mer om [priserna för Site Recovery](site-recovery-faq.md#pricing), och få de [prisinformationen](https://azure.microsoft.com/pricing/details/site-recovery/).



## <a name="set-up-an-azure-network"></a>Skapa ett Azure-nätverk

- Skapa ett Azure-nätverk. Virtuella Azure-datorer placeras i det här nätverket när de skapas efter växling vid fel.
- Site Recovery på Azure-portalen kan använda nätverk i [Resource Manager](../resource-manager-deployment-model.md), eller i klassiskt läge.
- Nätverket måste finnas på samma region som Recovery Services-valvet.
- Lär dig mer om [priser för virtuella nätverk](https://azure.microsoft.com/pricing/details/virtual-network/).
- Lär dig mer om [Virtuella Azure-anslutningen](physical-walkthrough-network.md) efter växling vid fel.


## <a name="set-up-an-azure-storage-account"></a>Skapa ett Azure-lagringskonto

- Site Recovery replikerar lokala servrar till Azure-lagring. Virtuella Azure-datorer skapas från lagringen efter redundansväxlingen.
- Konfigurera en [Azure storage-konto](../storage/common/storage-create-storage-account.md#create-a-storage-account) för replikerade data.
- Site Recovery på Azure-portalen kan använda storage-konton som skapas i Resource Manager eller i klassiskt läge.
- Lagringskontot kan vara standard eller [premium](../storage/common/storage-premium-storage.md).
- Om du konfigurerar ett premium-konto behöver du även en ytterligare standardkonto för loggdata.


## <a name="next-steps"></a>Nästa steg

Gå till [steg 6: konfigurera ett valv](physical-walkthrough-create-vault.md)
