---
title: comandos de aaaCommon do PowerShell para redes virtuais do Azure | Microsoft Docs
description: "Comandos de PowerShell comuns tooget que começou a criar uma rede virtual e seus recursos associados para VMs."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 56e1a73c-8299-4996-bd03-f74585caa1dc
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: b46b78f1b7c5a0c5ba917fb48f568d871e5e8789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="common-powershell-commands-for-azure-virtual-networks"></a>Comandos comuns do PowerShell para Redes Virtuais do Azure

Se você quiser toocreate uma máquina virtual, você precisa toocreate um [rede virtual](../../virtual-network/virtual-networks-overview.md) ou saber sobre uma rede virtual existente no qual Olá VM pode ser adicionada. Normalmente, quando você cria uma máquina virtual, também é necessário tooconsider criando Olá recursos descritos neste artigo.

Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter informações sobre como instalar a versão mais recente de saudação do PowerShell do Azure, selecione sua assinatura e tooyour conta de assinatura.

Algumas variáveis podem ser útil para você se executando mais de um dos comandos de saudação neste artigo:

- $location - local Olá Olá dos recursos de rede. Você pode usar [Get-AzureRmLocation](https://docs.microsoft.com/powershell/module/azurerm.resources/get-azurermlocation) toofind um [região geográfica](https://azure.microsoft.com/regions/) que funciona para você.
- $myResourceGroup - nome Olá Olá do grupo de recursos onde se encontram os recursos de rede hello.

## <a name="create-network-resources"></a>Criar recursos da rede

| Tarefa | Command |
| ---- | ------- |
| Criar configurações da sub-rede |$subnet1 = [New-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) -Name "mySubnet1" -AddressPrefix XX.X.X.X/XX<BR>$subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnet2" -AddressPrefix XX.X.X.X/XX<BR><BR>Uma rede típica pode ter uma sub-rede para um [balanceador de carga para a internet](../../load-balancer/load-balancer-internet-overview.md) e uma sub-rede separada para um [balanceador de carga interno](../../load-balancer/load-balancer-internal-overview.md). |
| Criar uma rede virtual |$vnet = [New-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermvirtualnetwork) -Name "myVNet" -ResourceGroupName $myResourceGroup -Location $location -AddressPrefix XX.X.X.X/XX -Subnet $subnet1, $subnet2 |
| Testar um nome de domínio exclusivo |[Test-AzureRmDnsAvailability](https://docs.microsoft.com/powershell/module/azurerm.network/test-azurermdnsavailability) -DomainNameLabel "myDNS" -Location $location<BR><BR>Você pode especificar um nome de domínio DNS para um [recurso IP público](../../virtual-network/virtual-network-ip-addresses-overview-arm.md), que cria um mapeamento para o endereço IP público de toohello domainname.location.cloudapp.azure.com no hello servidores DNS gerenciados do Azure. nome de saudação pode conter apenas letras, números e hifens. Olá primeiro e último caractere deve ser uma letra ou número e o nome de domínio Olá deve ser exclusivo dentro de seu local do Azure. Se **True** retornar, o nome proposto será globalmente exclusivo. |
| Criar um endereço IP público |$pip = [New-AzureRmPublicIpAddress](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermpublicipaddress) -Name "myPublicIp" -ResourceGroupName $myResourceGroup -DomainNameLabel "myDNS" -Location $location -AllocationMethod Dynamic<BR><BR>endereço IP público de saudação usa o nome de domínio de saudação anteriormente testados e é usado pela configuração de front-end Olá Olá do balanceador de carga. |
| Criar uma configuração de IP de front-end |$frontendIP = [New-AzureRmLoadBalancerFrontendIpConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) -Name "myFrontendIP" -PublicIpAddress $pip<BR><BR>configuração de front-end de saudação inclui o endereço IP público Olá que você criou anteriormente para o tráfego de rede. |
| Criar um pool de endereços de back-end |$beAddressPool = [New-AzureRmLoadBalancerBackendAddressPoolConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) -Name "myBackendAddressPool"<BR><BR>Fornece endereços internos para Olá back-end de saudação carregar balanceador que são acessados por meio de uma interface de rede. |
| Criar uma investigação |$healthProbe = [New-AzureRmLoadBalancerProbeConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) -Name "myProbe" -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2<BR><BR>Contém integridade investigações usadas toocheck disponibilidade das instâncias de máquinas virtuais no pool de endereços de back-end de saudação. |
| Criar uma regra de balanceamento de carga |$lbRule = [New-AzureRmLoadBalancerRuleConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) -Name HTTP -FrontendIpConfiguration $frontendIP -BackendAddressPool $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80<BR><BR>Contém regras que atribuir uma porta pública no balanceador de carga Olá porta tooa no pool de endereços de back-end de saudação. |
| Criar uma regra NAT de entrada |$inboundNATRule = [New-AzureRmLoadBalancerInboundNatRuleConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerinboundnatruleconfig) -Name "myInboundRule1" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389<BR><BR>Contém regras de mapeamento de uma porta pública na porta tooa do balanceador de carga Olá para uma máquina virtual no pool de endereços de back-end de saudação. |
| Criar um balanceador de carga |$loadBalancer = [New-AzureRmLoadBalancer](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancer) -ResourceGroupName $myResourceGroup -Name "myLoadBalancer" -Location $location -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule -LoadBalancingRule $lbRule -BackendAddressPool $beAddressPool -Probe $healthProbe |
| Criar um adaptador de rede |$nic1= [New-AzureRmNetworkInterface](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermnetworkinterface) -ResourceGroupName $myResourceGroup -Name "myNIC" -Location $location -PrivateIpAddress XX.X.X.X -Subnet $subnet2 -LoadBalancerBackendAddressPool $loadBalancer.BackendAddressPools[0] -LoadBalancerInboundNatRule $loadBalancer.InboundNatRules[0]<BR><BR>Crie uma interface de rede usando o endereço IP público de saudação e a sub-rede de rede virtual que você criou anteriormente. |

## <a name="get-information-about-network-resources"></a>Obter informações sobre recursos de rede

| Tarefa | Command |
| ---- | ------- |
| Listar redes virtuais |[Get-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermvirtualnetwork) -ResourceGroupName $myResourceGroup<BR><BR>Lista todas as redes virtuais do hello, no grupo de recursos de saudação. |
| Obter informações sobre uma rede virtual |Get-AzureRmVirtualNetwork -Name "myVNet" -ResourceGroupName $myResourceGroup |
| Listar sub-redes em uma rede virtual |Get-AzureRmVirtualNetwork -Name "myVNet" -ResourceGroupName $myResourceGroup &#124; Select Subnets |
| Obter informações sobre uma sub-rede |[Get-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) -Name "mySubnet1" -VirtualNetwork $vnet<BR><BR>Obtém informações sobre sub-redes Olá na rede virtual especificado do hello. valor de saudação $vnet representa o objeto de saudação retornado por Get-AzureRmVirtualNetwork. |
| Listar endereços IP |[Get-AzureRmPublicIpAddress](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermpublicipaddress) -ResourceGroupName $myResourceGroup<BR><BR>Lista os endereços IP públicos Olá no grupo de recursos de saudação. |
| Listar balanceadores de carga |[Get-AzureRmLoadBalancer](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermloadbalancer) -ResourceGroupName $myResourceGroup<BR><BR>Lista todos os balanceadores de carga Olá no grupo de recursos de saudação. |
| Listar adaptadores de rede |[Get-AzureRmNetworkInterface](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermnetworkinterface) -ResourceGroupName $myResourceGroup<BR><BR>Lista todas as interfaces de rede Olá no grupo de recursos de saudação. |
| Obter informações sobre um adaptador de rede |Get-AzureRmNetworkInterface -Name "myNIC" -ResourceGroupName $myResourceGroup<BR><BR>Obtém informações sobre um adaptador de rede específico. |
| Obter configuração de IP de saudação de uma interface de rede |[Get-AzureRmNetworkInterfaceIPConfig](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermnetworkinterfaceipconfig) -Name "myNICIP" -NetworkInterface $nic<BR><BR>Obtém informações sobre a configuração de IP Olá Olá especificado da interface de rede. valor de saudação $nic representa o objeto de saudação retornado por Get-AzureRmNetworkInterface. |

## <a name="manage-network-resources"></a>Gerenciar recursos de rede

| Tarefa | Command |
| ---- | ------- |
| Adicionar uma rede virtual de tooa de sub-rede |[Add-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig) -AddressPrefix XX.X.X.X/XX -Name "mySubnet1" -VirtualNetwork $vnet<BR><BR>Adiciona uma tooan de sub-rede virtual rede existente. valor de saudação $vnet representa o objeto de saudação retornado por Get-AzureRmVirtualNetwork. |
| Excluir uma rede virtual |[Remove-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/module/azurerm.network/remove-azurermvirtualnetwork) -Name "myVNet" -ResourceGroupName $myResourceGroup<BR><BR>Remove a rede virtual especificado do hello saudação do grupo de recursos. |
| Excluir um adaptador de rede |[Remove-AzureRmNetworkInterface](https://docs.microsoft.com/powershell/module/azurerm.network/remove-azurermnetworkinterface) -Name "myNIC" -ResourceGroupName $myResourceGroup<BR><BR>Remove a interface de rede especificada Olá Olá do grupo de recursos. |
| Excluir um balanceador de carga |[Remove-AzureRmLoadBalancer](https://docs.microsoft.com/powershell/module/azurerm.network/remove-azurermloadbalancer) -Name "myLoadBalancer" -ResourceGroupName $myResourceGroup<BR><BR>Olá remove especificado balanceador de carga de saudação do grupo de recursos. |
| Excluir um endereço IP público |[Remove-AzureRmPublicIpAddress](https://docs.microsoft.com/powershell/module/azurerm.network/remove-azurermpublicipaddress)-Name "myIPAddress" -ResourceGroupName $myResourceGroup<BR><BR>Olá remove especificado endereço IP público do grupo de recursos de saudação. |

## <a name="next-steps"></a>Próximas etapas
* Interface de rede do uso Olá recém criado quando você [criar uma VM](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Saiba mais sobre como você pode [criar uma VM com várias interfaces de rede](../../virtual-network/virtual-networks-multiple-nics.md).

