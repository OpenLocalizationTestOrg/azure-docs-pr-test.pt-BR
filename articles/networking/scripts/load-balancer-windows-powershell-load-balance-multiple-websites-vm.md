---
title: "balanceamento de carga de aaaAzure exemplo de Script do PowerShell - vários sites com o Azure PowerShell | Microsoft Docs"
description: "Exemplo de Script do PowerShell do Azure - toohello de vários sites o balanceamento de carga mesma máquina virtual"
services: load-balancer
documentationcenter: load-balancer
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 316818964eb6928fe4163ef69eb7f05da2dc9636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-multiple-websites"></a>Balanceamento de carga de vários sites

Este exemplo de script cria uma rede virtual com duas VMs (máquinas virtuais) que são membros de um conjunto de disponibilidade. Um balanceador de carga direcione o tráfego para separar duas toohello duas VMs de endereços IP. Após o script hello em execução, você pode implantar web server software toohello VMs e hospedar vários sites, cada qual com seu próprio endereço IP.

Se necessário, instale Olá PowerShell do Azure usando a instrução Olá encontrado no hello [guia do PowerShell do Azure](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)e, em seguida, execute `Login-AzureRmAccount` toocreate uma conexão com o Azure.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-powershell[main](../../../powershell_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.ps1  "Load balance multiple web sites")]

## <a name="clean-up-deployment"></a>Limpar implantação 

Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a>Explicação sobre o script

Esse script usa Olá comandos toocreate um grupo de recursos de rede virtual, o balanceador de carga e relacionados com todos os recursos a seguir. Cada comando na documentação específica do toocommand Olá tabela links.

| Command | Observações |
|---|---|
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Cria um grupo de recursos no qual todos os recursos são armazenados. |
| [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset) | Cria um conjunto de disponibilidade do Azure tooprovide disponibilidade de alta. |
| [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | Cria uma configuração de sub-rede. Essa configuração é usada com o processo de criação de rede virtual hello. |
| [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | Cria uma rede virtual. |
| [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) | Cria um endereço IP público. |
| [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) | Cria uma configuração de IP front-end para um balanceador de carga. |
| [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) | Cria uma configuração de pool de endereços de back-end para um balanceador de carga. |
| [New-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) | Cria uma investigação NLB. Uma investigação NLB é usado toomonitor cada VM no conjunto NLB hello. Se qualquer VM ficar inacessível, o tráfego não é roteado toohello VM. |
| [New-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) | Cria uma regra NLB. Neste exemplo, uma regra é criada para a porta 80. Como o tráfego HTTP chega ao Olá NLB, é roteado tooport 80 uma das VMs Olá Olá NLB conjunto. |
| [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer) | Cria um balanceador de carga. |
| [New-AzureRmNetworkInterfaceIpConfig](/powershell/module/azurerm.network/new-azurermnetworkinterfaceipconfig) | Define os recursos avançados para uma interface de rede virtual. |
| [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) | Cria um adaptador de rede. |
| [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) | Cria uma configuração de VM. Essa configuração inclui informações como nome da VM, sistema operacional e credenciais administrativas. Olá configuração será usada durante a criação da VM. |
| [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) | Crie uma máquina virtual. |
|[Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | Remove um grupo de recursos e todos os recursos contidos nele. |

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre hello Azure PowerShell, consulte [documentação do Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).

Exemplos de script do PowerShell rede adicionais podem ser encontrados no hello [documentação de visão geral da rede do Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).
