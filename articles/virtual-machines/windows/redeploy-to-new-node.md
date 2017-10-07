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
# <a name="redeploy-windows-virtual-machine-toonew-azure-node"></a>Reimplantar toonew de máquina virtual do Windows Azure nó
Se você tiver enfrentando dificuldades Solucionando problemas de área de trabalho remota (RDP) conexão ou o aplicativo acessar tooWindows com base em máquina virtual do Azure (VM), reimplantando Olá VM pode ajudar. Quando você reimplanta uma VM, ele move Olá VM tooa novo nó no hello infraestrutura do Azure e, em seguida, liga-lo novamente, mantendo todas as suas opções de configuração e recursos associados. Este artigo mostra como tooredeploy uma VM usando o Azure PowerShell ou hello portal do Azure.

> [!NOTE]
> Depois que você reimplanta uma VM, disco temporário Olá é perdido e endereços IP dinâmicos associados à interface de rede virtual são atualizados. 


## <a name="using-azure-powershell"></a>Usando o PowerShell do Azure
Certifique-se de ter hello mais recente do PowerShell do Azure 1. x instalado em seu computador. Para obter mais informações, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).

exemplo a seguir Hello implanta Olá VM denominada `myVM` no grupo de recursos de saudação chamado `myResourceGroup`:

```powershell
Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
```


[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a>Próximas etapas
Se você estiver tendo problemas para se conectar tooyour VM, você pode encontrar ajuda específica na [Solucionando problemas de conexões RDP](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ou [detalhadas RDP etapas de solução de problemas](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Você também pode ler [problemas com a solução de problemas de aplicativo](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) se não conseguir acessar um aplicativo em execução em sua VM.

