---
title: "Exemplo de Script do PowerShell - tooVMs de tráfego de balanceamento de carga para alta disponibilidade de aaaAzure | Microsoft Docs"
description: "Exemplo de Script do PowerShell do Azure - tooVMs de tráfego de balanceamento de carga para alta disponibilidade"
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
ms.openlocfilehash: 332c39e1aad071ca6f7ce420ccc1f423ef647d2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-traffic-toovms-for-high-availability"></a>Carregar tooVMs de tráfego de balanceamento para alta disponibilidade

Este exemplo de script cria todo o necessário toorun várias máquinas virtuais do Windows configurado em uma alta disponibilidade e de carga balanceada configuração. Após o script hello em execução, você terá três máquinas virtuais, tooan ingressado no conjunto de disponibilidade do Azure e acessível por meio de um balanceador de carga do Azure.

Se necessário, instale Olá PowerShell do Azure usando a instrução Olá encontrado no hello [guia do PowerShell do Azure](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)e, em seguida, execute `Login-AzureRmAccount` toocreate uma conexão com o Azure.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.ps1 "Quick Create VM")]

## <a name="clean-up-deployment"></a>Limpar implantação 

Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a>Explicação sobre o script

Esse script usa Olá comandos toocreate um grupo de recursos, máquina virtual, o conjunto de disponibilidade, balanceador de carga e todos os recursos relacionados a seguir. Cada comando na documentação específica do toocommand Olá tabela links.

| Command | Observações |
|---|---|
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Cria um grupo de recursos no qual todos os recursos são armazenados. |
| [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | Cria uma configuração de sub-rede. Essa configuração é usada com o processo de criação de rede virtual hello. |
| [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | Cria uma sub-rede e uma rede virtual do Azure. |
| [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress)  | Cria um endereço IP público com um endereço IP estático e um nome DNS associado. |
| [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer)  | Cria um Azure Load Balancer. |
| [New-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) | Cria uma investigação do balanceador de carga. Uma investigação do balanceador de carga é usado toomonitor cada VM no conjunto de Balanceador de carga de saudação. Se qualquer VM ficar inacessível, o tráfego não é roteado toohello VM. |
| [New-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) | Cria uma regra do balanceador de carga. Neste exemplo, uma regra é criada para a porta 80. Como o tráfego HTTP chega ao balanceador de carga Olá, é roteado tooport 80 uma saudação VMs no conjunto de Balanceador de carga de saudação. |
| [New-AzureRmLoadBalancerInboundNatRuleConfig](/powershell/module/azurerm.network/new-azurermloadbalancerinboundnatruleconfig) | Cria uma regra de conversão de endereços de rede (NAT) do balanceador de carga.  Regras NAT mapeiam uma porta de porta tooa do balanceador de carga Olá em uma máquina virtual. Neste exemplo, uma regra NAT é criada para o SSH tráfego tooeach VM no conjunto de Balanceador de carga de saudação.  |
| [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | Cria um grupo de segurança de rede (NSG), que é um limite de segurança entre a máquina de virtual de internet e Olá Olá. |
| [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | Cria um tooallow de regra NSG o tráfego de entrada. Neste exemplo, a porta 22 é aberta para o tráfego SSH. |
| [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) | Cria uma placa de rede virtual e anexa-rede virtual toohello, sub-rede e NSG. |
| [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset) | Cria um conjunto de disponibilidade. Conjuntos de disponibilidade garantem o funcionamento do aplicativo distribuindo as máquinas virtuais de saudação em recursos físicos, de modo que se ocorrer falha, todo o conjunto de saudação não é afetado. |
| [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) | Cria uma configuração de VM. Essa configuração inclui informações como nome da VM, sistema operacional e credenciais administrativas. Olá configuração será usada durante a criação da VM. |
| [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)  | Cria a máquina virtual de saudação e conecta toohello placa de rede, a rede virtual, sub-rede e NSG. Esse comando também especifica Olá toobe de imagem de máquina virtual usada e as credenciais administrativas.  |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | Exclui um grupo de recursos, incluindo todos os recursos aninhados. |

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre hello Azure PowerShell, consulte [documentação do Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).

Exemplos de script do PowerShell rede adicionais podem ser encontrados no hello [documentação de visão geral da rede do Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).
