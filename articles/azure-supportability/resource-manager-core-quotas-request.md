---
title: "Azure Resource Manager kärnkvot öka begäranden | Microsoft Docs"
description: "Azure Resource Manager kärnkvot öka begäranden"
author: ganganarayanan
ms.author: gangan
ms.date: 1/18/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: ce37c848-ddd9-46ab-978e-6a1445728a3b
ms.openlocfilehash: cb6c5b3e86f126d4110d1cd29d8c9891e356e414
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/11/2017
---
# <a name="resource-manager-core-quota-increase-requests"></a>Kärnkvot för hanteraren för filserverresurser öka begäranden

Hanteraren för filserverresurser core kvoter tillämpas på den regionsnivån och SKU-familjen nivå.
Mer information om hur kvoter tillämpas på den [Azure-prenumeration och tjänstbegränsningarna](http://aka.ms/quotalimits) sidan.
Om du vill veta mer om SKU familjer, du kan jämföra kostnader och prestanda på den [prissättning för Virtual Machines](http://aka.ms/pricingcompute) sidan.

Skapa ett supportärende för kvot för kärnor i Azure-portalen om du vill begära en [https://portal.azure.com](https://portal.azure.com).

> [!NOTE]
> Lär dig hur du [skapa en supportbegäran](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request) i Azure-portalen

1. Välj typ av problem som ”kvoten” och typ av kvot som ”kärnor” på sidan nytt stöd för begäran.

    ![Kvoten grunderna bladet](./media/resource-manager-core-quotas-request/Basics-blade.png)

2. Välj distributionsmodell som ”Resource Manager” och välj en plats.

    ![Kvoten problemet bladet](./media/resource-manager-core-quotas-request/Problem-step.png)

3. Välj SKU-familjer som kräver en ökning.

    ![SKU-serien vald](./media/resource-manager-core-quotas-request/SKU-selected.png)

4. Ange de nya gränserna som på prenumerationen.

    ![Begäran om ny SKU kvot](./media/resource-manager-core-quotas-request/SKU-new-quota.png)

- Avmarkera SKU: N i SKU-familjen listrutan för att ta bort en rad eller klicka på ikonen Ignorera ”x”.
Klicka på ”Nästa” på sidan problemet steg för att fortsätta med stöd för begäran skapas när du har angett önskade kvoten för varje SKU-serien.
