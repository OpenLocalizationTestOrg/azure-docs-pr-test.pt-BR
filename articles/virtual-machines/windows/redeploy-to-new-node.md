---
title: "máquinas virtuais do aaaRedeploy Windows no Azure | Microsoft Docs"
description: "Como máquinas virtuais do tooredeploy Windows na conexão de RDP toomitigate do Azure emite."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: genlin
manager: timlt
tags: azure-resource-manager,top-support-issue
ms.assetid: 0ee456ee-4595-4a14-8916-72c9110fc8bd
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 903d9d5bf241075931ee4b746690c553d808a58f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="redeploy-windows-virtual-machine-toonew-azure-node"></a><span data-ttu-id="0acf4-103">Reimplantar toonew de máquina virtual do Windows Azure nó</span><span class="sxs-lookup"><span data-stu-id="0acf4-103">Redeploy Windows virtual machine toonew Azure node</span></span>
<span data-ttu-id="0acf4-104">Se você tiver enfrentando dificuldades Solucionando problemas de área de trabalho remota (RDP) conexão ou o aplicativo acessar tooWindows com base em máquina virtual do Azure (VM), reimplantando Olá VM pode ajudar.</span><span class="sxs-lookup"><span data-stu-id="0acf4-104">If you have been facing difficulties troubleshooting Remote Desktop (RDP) connection or application access tooWindows-based Azure virtual machine (VM), redeploying hello VM may help.</span></span> <span data-ttu-id="0acf4-105">Quando você reimplanta uma VM, ele move Olá VM tooa novo nó no hello infraestrutura do Azure e, em seguida, liga-lo novamente, mantendo todas as suas opções de configuração e recursos associados.</span><span class="sxs-lookup"><span data-stu-id="0acf4-105">When you redeploy a VM, it moves hello VM tooa new node within hello Azure infrastructure and then powers it back on, retaining all your configuration options and associated resources.</span></span> <span data-ttu-id="0acf4-106">Este artigo mostra como tooredeploy uma VM usando o Azure PowerShell ou hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0acf4-106">This article shows you how tooredeploy a VM using Azure PowerShell or hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="0acf4-107">Depois que você reimplanta uma VM, disco temporário Olá é perdido e endereços IP dinâmicos associados à interface de rede virtual são atualizados.</span><span class="sxs-lookup"><span data-stu-id="0acf4-107">After you redeploy a VM, hello temporary disk is lost and dynamic IP addresses associated with virtual network interface are updated.</span></span> 


## <a name="using-azure-powershell"></a><span data-ttu-id="0acf4-108">Usando o PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="0acf4-108">Using Azure PowerShell</span></span>
<span data-ttu-id="0acf4-109">Certifique-se de ter hello mais recente do PowerShell do Azure 1. x instalado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="0acf4-109">Make sure you have hello latest Azure PowerShell 1.x installed on your machine.</span></span> <span data-ttu-id="0acf4-110">Para obter mais informações, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0acf4-110">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="0acf4-111">exemplo a seguir Hello implanta Olá VM denominada `myVM` no grupo de recursos de saudação chamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="0acf4-111">hello following example deploys hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```powershell
Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
```


[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a><span data-ttu-id="0acf4-112">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0acf4-112">Next steps</span></span>
<span data-ttu-id="0acf4-113">Se você estiver tendo problemas para se conectar tooyour VM, você pode encontrar ajuda específica na [Solucionando problemas de conexões RDP](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ou [detalhadas RDP etapas de solução de problemas](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0acf4-113">If you are having issues connecting tooyour VM, you can find specific help on [troubleshooting RDP connections](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) or [detailed RDP troubleshooting steps](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="0acf4-114">Você também pode ler [problemas com a solução de problemas de aplicativo](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) se não conseguir acessar um aplicativo em execução em sua VM.</span><span class="sxs-lookup"><span data-stu-id="0acf4-114">If you cannot access an application running on your VM, you can also read [application troubleshooting issues](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

