---
title: Koppla en datadisk hanterade till en Windows-VM - Azure | Microsoft Docs
description: "Så här kopplar du nya hanterade datadisk för en virtuell Windows-dator i Azure-portalen med hjälp av Resource Manager-distributionsmodellen."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: cynthn
ms.openlocfilehash: f0cf88a06c5470ef173b22e7213419a6c8760723
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-attach-a-managed-data-disk-to-a-windows-vm-in-the-azure-portal"></a>Så här kopplar du en datadisk hanterade till en virtuell Windows-dator i Azure-portalen

Den här artikeln visar hur du kopplar en ny datadisk hanterade till Windows-datorer via Azure-portalen. Innan du gör detta kan du granska dessa tips:

* Storleken på den virtuella datorn styr hur många datadiskar som du kan bifoga. Mer information finns i [storlekar för virtuella datorer](sizes.md).
* För en ny disk behöver du inte skapa först eftersom Azure skapar den när du ansluter den.

Du kan också [ansluta en datadisk med hjälp av Powershell](attach-disk-ps.md).



## <a name="add-a-data-disk"></a>Lägg till en datadisk
1. Klicka på menyn till vänster **virtuella datorer**.
2. Välj den virtuella datorn i listan.
3. Klicka på bladet för virtuella datorer **diskar**.
   4. På den **diskar** bladet, klickar du på **+ Lägg till datadisk**.
5. Välj i listrutan för den nya disken **skapa tom**.
6. I den **skapa hanterade diskar** bladet, Skriv ett namn för disken och justera de andra inställningarna efter behov. När du är klar klickar du på **skapa**.
7. I den **diskar** bladet Klicka på Spara för att spara den nya diskkonfigurationen för den virtuella datorn.
6. När Azure skapar disken och kopplar den till den virtuella datorn, den nya disken visas i inställningarna för den virtuella disken under **Datadiskar**.


## <a name="initialize-a-new-data-disk"></a>Initiera en ny datadisk

1. Ansluta till den virtuella datorn.
1. Klicka på start-menyn i den virtuella datorn och skriva **diskmgmt.msc** och träffar **RETUR**. Detta startar snapin-modulen Diskhantering.
2. Diskhantering identifierar att du har en ny, ej initierad disk och initiera Disk-fönstret visas.
3. Kontrollera att den nya disken är markerad och klicka på **OK** att initiera den.
4. Den nya disken visas nu som **lediga**. Högerklicka på disken och välj **ny enkel volym**. Den **guiden Ny enkel volym** startar.
5. Gå igenom guiden och hålla alla standardinställningar, när du är klar väljer **Slutför**.
6. Stäng Diskhantering.
7. Du får ett popup-fönster som du vill formatera den nya disken innan du kan använda den. Klicka på **Formatera disk**.
8. I den **Format ny disk** dialogrutan Kontrollera inställningarna och klicka sedan på **starta**.
9. Du får en varning om att formatera diskarna kommer att radera alla data, klickar du på **OK**.
10. När formatet är klar klickar du på **OK**.

## <a name="use-trim-with-standard-storage"></a>Använd Rensa med standardlagring

Om du använder standardlagring (HDD), bör du aktivera TRIMNING. TRIMNING ignorerar oanvända block på disken så att endast debiteras du för lagring som du faktiskt använder. Om du skapar stora filer och ta bort dem kan detta spara på kostnader. 

Du kan köra det här kommandot för att kontrollera TRIM inställningen. Öppna en kommandotolk på din Windows-VM och skriv:

```
fsutil behavior query DisableDeleteNotify
```

Om kommandot returnerar 0, är TRIMNING aktiverat på rätt sätt. Om den returnerar 1, kör du följande kommando för att aktivera TRIMNING:
```
fsutil behavior set DisableDeleteNotify 0
```

När du tar bort data från disken, kan du se till åtgärderna TRIM tömning korrekt genom att köra defragmenterar med TRIMNING:

```
defrag.exe <volume:> -l
```

Du kan också kontrollera hela volymen trimmas genom att formatera volymen.

## <a name="next-steps"></a>Nästa steg
Om du program behöver använda D: enhet för att lagra data, kan du [ändra enhetsbeteckningen för den tillfälliga disken i Windows](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
