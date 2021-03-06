---
title: Create a test VM in Azure Stack | Microsoft Docs
description: Learn how to provision a test VM in Azure Stack as a cloud operator.
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: c86646e1-a12e-493f-b396-f17bfacd60c2
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 9/25/2017
ms.author: erikje
ms.translationtype: HT
ms.sourcegitcommit: c3a2462b4ce4e1410a670624bcbcec26fd51b811
ms.openlocfilehash: 98770945d5cccc27bfce971491e6ea30fee2460a
ms.contentlocale: sv-se
ms.lasthandoff: 09/25/2017

---
# <a name="create-a-test-virtual-machine-in-azure-stack"></a>Create a test virtual machine in Azure Stack

*Applies to: Azure Stack Development Kit*

As a cloud operator, you can create a test virtual machine to validate your [Azure Stack](azure-stack-poc.md) deployment.

> [!NOTE]
> Before you can provision virtual machines, you must [add the Windows Server 2016 Evaluation image to the Azure Stack marketplace](azure-stack-add-default-image.md).
> 
> 

## <a name="create-a-virtual-machine"></a>Create a virtual machine
1. On the Azure Stack Development Kit host, [sign in](azure-stack-connect-azure-stack.md) to the administrator portal (`https://adminportal.local.azurestack.external`), and then click **New** > **Compute** > **Windows Server 2016 Datacenter Eval** > **Create**.  
2. In the **Basics** blade, type a **Name**, **User name**, and **Password**. Choose a **Subscription**. Create a **Resource group**, or select an existing one, and then click **OK**.  
3. In the **Choose a size** blade, click **A1 Standard**, and then click **Select**.  
4. In the **Settings** blade, accept the defaults and click **OK**
5. In the **Summary** blade, click **OK** to create the virtual machine.  
6. To see your new virtual machine, click **All resources**, then search for the virtual machine and click its name.
    ![](media/azure-stack-provision-vm/image06.png)


## <a name="next-steps"></a>Next steps
[Using the administrator and user portals in Azure Stack](azure-stack-manage-portals.md)

