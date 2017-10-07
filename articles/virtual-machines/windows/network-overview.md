---
title: "aaaVirtual redes e máquinas virtuais do Windows no Azure | Microsoft Docs"
description: "Saiba mais sobre o sistema de rede relacionado toohello Noções básicas sobre a criação de máquinas virtuais do Windows no Azure."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 5493e9f7-7d45-4e98-be9a-657a53708746
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: e28a4782f9f6c69f6101e45dbb560ccd694a1e07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-networks-and-windows-virtual-machines-in-azure"></a>Redes virtuais e máquinas virtuais do Windows no Azure 

Ao criar uma VM (máquina virtual) do Azure, você deve criar uma [VNet](../../virtual-network/virtual-networks-overview.md) (rede virtual) ou usar uma VNet existente. Você também precisa toodecide como suas VMs são pretendido toobe acessado em Olá VNet. É importante muito[plano antes de criar recursos](../../virtual-network/virtual-network-vnet-plan-design-arm.md) e certifique-se de que entendeu Olá [limites de recursos de rede](../../azure-subscription-service-limits.md#networking-limits).

Em Olá figura a seguir, as VMs são representadas como servidores web e servidores de banco de dados. Cada conjunto de máquinas virtuais são atribuídos a sub-redes tooseparate Olá VNet.

![rede virtual do Azure](./media/network-overview/vnetoverview.png)

Você pode criar uma rede virtual antes de criar uma máquina virtual ou você pode criar redes de saudação ao criar uma VM. Você deve criar uma rede virtual por conta própria ou ela será criada quando você criar uma VM.

Criar esses recursos toosupport comunicação com uma VM:

- Interfaces de rede
- Endereços IP
- Rede virtual e sub-redes

Além de recursos básicos de toothose, você também deve considerar esses recursos opcionais:

- Grupos de segurança de rede
- Balanceadores de carga 

## <a name="network-interfaces"></a>Interfaces de rede

Um [interface de rede (NIC)](../../virtual-network/virtual-network-network-interface.md) é interconexão de saudação entre uma máquina virtual e uma rede virtual (VNet). Uma máquina virtual deve ter pelo menos um NIC, mas pode ter mais de um, dependendo de tamanho de saudação do hello VM que você criou. Saiba mais sobre para quantas NICs cada tamanho de VM dá suporte em [Tamanhos das máquinas virtuais no Azure](sizes.md). 

Se você quiser toocreate uma VM com mais de uma NIC, você deve criar hello VM com pelo menos dois.  Após a criação, você pode adicionar NICs adicionais toohello número suportado pelo tamanho da VM Olá, mas não é possível adicionar tooa de NICs adicional VM criada somente com um, independentemente de quantos NICs Olá tamanho da VM oferece suporte. 

Se Olá VM for adicionada tooan conjunto de disponibilidade, todas as VMs no conjunto de disponibilidade Olá devem ter uma ou várias NICs. Máquinas virtuais com mais de um NIC não são necessárias toohave Olá mesmo número de NICs, mas eles devem ter pelo menos dois.

Cada tooa NIC conectada VM deve existir no hello mesmo local e assinatura como Olá VM. Cada NIC deve ser conectado tooa VNet que existe no hello mesmo local do Azure e assinatura como Olá NIC. Depois que uma NIC é criada, você pode alterar a sub-rede hello que está conectado ao, mas você não pode alterar Olá rede virtual está conectado ao.  Cada NIC conectada tooa que VM é atribuída a um endereço MAC que não são alterados até Olá VM é excluída.

Esta tabela lista os métodos de saudação que você pode usar toocreate uma interface de rede.

| Método | Descrição |
| ------ | ----------- |
| Portal do Azure | Quando você cria uma máquina virtual no hello portal do Azure, uma interface de rede é criada automaticamente para você (você não pode usar uma NIC que você cria separadamente). portal de saudação cria uma VM com apenas uma placa de rede. Se você quiser toocreate uma VM com mais de uma NIC, você deve criá-lo com um método diferente. |
| [PowerShell do Azure](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) | Use [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) com hello **- PublicIpAddressId** parâmetro tooprovide Olá identificador de endereço IP público Olá que você criou anteriormente. |
| [CLI do Azure](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md) | tooprovide Olá identificador de IP público Olá endereço que você use criado anteriormente, [nic da rede az criar](https://docs.microsoft.com/cli/azure/network/nic#create) com hello **– endereço ip público** parâmetro. |
| [Modelo](../../virtual-network/virtual-network-deploy-multinic-arm-template.md) | Use [Interface de rede em uma rede Virtual com endereço IP público](https://github.com/Azure/azure-quickstart-templates/tree/master/101-nic-publicip-dns-vnet) como um guia para a implantação de uma interface de rede usando um modelo. |

## <a name="ip-addresses"></a>Endereços IP 

Você pode atribuir esses tipos de [endereços IP](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) tooa NIC no Azure:

- **Endereços IP públicos** -usado toocommunicate de entrada e saída (sem conversão de endereços de rede (NAT)) com hello Internet e outros recursos do Azure não conectado tooa VNet. Atribuir um tooa de endereço IP público NIC é opcional. Endereços IP públicos têm um custo nominal, e há um número máximo que pode ser usado por assinatura.
- **Endereços IP privados** - usado para comunicação em uma rede virtual, sua rede local e Olá Internet (NAT). Você deve atribuir pelo menos um privada IP endereço tooa VM. toolearn mais sobre NAT no Azure, leia [Noções básicas sobre conexões de saída no Azure](../../load-balancer/load-balancer-outbound-connections.md).

Você pode atribuir tooVMs de endereços IP públicos ou balanceadores de carga para a internet. Você pode atribuir tooVMs de endereços IP privados e balanceadores de carga interno. Você atribui tooa de endereços IP usando uma interface de rede VM.

Há dois métodos em que um endereço IP é alocado tooa recurso - dinâmico ou estático. método de alocação saudação padrão é dinâmico, onde não é possível alocar um endereço IP quando ele é criado. Em vez disso, o endereço IP de saudação é alocado quando você cria uma máquina virtual ou iniciar uma VM parada. endereço IP de saudação é liberado quando você interromper ou excluir Olá VM. 

endereço IP de saudação tooensure para Olá VM permanece Olá mesmo, você pode definir o método de alocação hello explicitamente toostatic. Nesse caso, um endereço IP é atribuído imediatamente. Ele é liberado apenas quando você excluir Olá VM ou alterar seu toodynamic de método de alocação.
    
Esta tabela lista os métodos de saudação que você pode usar um endereço IP de toocreate.

| Método | Descrição |
| ------ | ----------- |
| [Portal do Azure](../../virtual-network/virtual-network-deploy-static-pip-arm-portal.md) | Por padrão, os endereços IP públicos são dinâmicos e Olá endereço associado toothem pode ser alterada quando Olá VM for interrompida ou excluída. tooguarantee que Olá VM sempre usa Olá mesmo endereço IP público, crie um endereço IP público estático. Por padrão, o portal de saudação atribui um tooa de endereço IP de privada dinâmico NIC ao criar uma VM. Você pode alterar esse toostatic depois Olá que VM é criada.|
| [PowerShell do Azure](../../virtual-network/virtual-network-deploy-static-pip-arm-ps.md) | Você usa [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) com hello **- AllocationMethod** parâmetro como dinâmico ou estático. |
| [CLI do Azure](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md) | Você usa [criar az rede ip público](https://docs.microsoft.com/cli/azure/network/public-ip#create) com hello **-método de alocação** parâmetro como dinâmico ou estático. |
| [Modelo](../../virtual-network/virtual-network-deploy-static-pip-arm-template.md) | Use [Interface de rede em uma rede Virtual com endereço IP público](https://github.com/Azure/azure-quickstart-templates/tree/master/101-nic-publicip-dns-vnet) como um guia para implantar um IP público de endereço usando um modelo. |

Depois de criar um endereço IP público, você pode associá-lo com uma VM atribuindo a ele tooa NIC.

## <a name="virtual-network-and-subnets"></a>Rede virtual e sub-redes

Uma sub-rede é um intervalo de endereços IP em redes de saudação. Você pode dividir a VNet em várias sub-redes para fins de organização e segurança. Cada NIC em uma VM é sub-rede tooone conectado em uma VNet. NICs toosubnets conectado (igual ou diferente) dentro de uma rede virtual podem se comunicar uns com os outros sem qualquer configuração adicional.

Quando você configura uma rede virtual, você pode especificar topologia hello, incluindo sub-redes e espaços de endereço disponível hello. Se Olá VNet toobe conectado tooother VNets ou local redes, você deve selecionar intervalos de endereços que não se sobrepõem. endereços IP Hello são particulares e não podem ser acessados de Olá Internet, que é válida somente para endereços IP não routeable hello como 10.0.0.0/8, 172.16.0.0/12 ou 192.168.0.0/16. Agora, o Azure trata qualquer intervalo de endereços como parte da saudação privada VNet espaço de endereço IP que só está acessível no hello VNet, dentro do VNets interconectadas e em sua localização no local. 

Se você trabalha em uma organização que outra pessoa é responsável por redes internas hello, você deve conversar toothat pessoa antes de selecionar o espaço de endereço. Verifique se não há nenhuma sobreposição e informe espaço Olá desejado toouse para que eles não tentam toouse Olá mesmo intervalo de endereços IP. 

Por padrão, não há nenhum limite de segurança entre sub-redes, para que as VMs em cada uma dessas sub-redes podem falar tooone outro. No entanto, você pode configurar grupos de segurança de rede (NSGs), que permitem que você tooand de fluxo de tráfego toocontrol Olá de sub-redes e tooand de VMs. 

Esta tabela lista os métodos de saudação que você pode usar toocreate uma rede virtual e sub-redes.   

| Método | Descrição |
| ------ | ----------- |
| [Portal do Azure](../../virtual-network/virtual-networks-create-vnet-arm-pportal.md) | Se você permitir que o Azure criar uma rede virtual, quando você cria uma máquina virtual, o nome de saudação é uma combinação de nome do grupo de recursos de saudação contém Olá VNet e **- vnet**. espaço de endereço Olá 10.0.0.0/24, Olá necessária subrede nome é **padrão**, e o intervalo de endereços de sub-rede Olá é 10.0.0.0/24. |
| [PowerShell do Azure](../../virtual-network/virtual-networks-create-vnet-arm-ps.md) | Você usa [New-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmVirtualNetworkSubnetConfig) e [AzureRmVirtualNetwork novo](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmVirtualNetwork) toocreate uma sub-rede e uma rede virtual. Você também pode usar [adicionar AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig) tooadd tooan uma sub-rede VNet existente. |
| [CLI do Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md) | Olá sub-rede e Olá redes são criadas no hello mesmo tempo. Forneça um **– nome da sub-rede** parâmetro muito[criar redes de rede az](https://docs.microsoft.com/cli/azure/network/vnet#create) com o nome da sub-rede hello. |
| [Modelo](../../virtual-network/virtual-networks-create-vnet-arm-template-click.md) | Olá toocreate de maneira mais fácil uma rede virtual e sub-redes é toodownload um modelo existente, como [rede Virtual com duas sub-redes](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets)e modificá-lo para suas necessidades. |

## <a name="network-security-groups"></a>Grupos de segurança de rede

Um [o grupo de segurança de rede (NSG)](../../virtual-network/virtual-networks-nsg.md) contém uma lista de regras de lista de controle de acesso (ACL) que permitem ou negam toosubnets de tráfego de rede, NICs ou ambos. Os NSGs podem ser associados a sub-redes ou NICs conectados tooa sub-rede. Quando um NSG está associado uma sub-rede, regras de ACL Olá aplicam tooall Olá VMs na sub-rede. Além disso, o tráfego tooan NIC individual pode ser restringido associando um NSG diretamente tooa NIC.

Os NSGs contêm dois conjuntos de regras: entrada e saída. prioridade de saudação para uma regra deve ser exclusiva em cada conjunto. Cada regra tem propriedades de protocolo, origem e intervalos de porta de destino, prefixos de endereço, direção de tráfego, prioridade e tipo de acesso. 

Todos os NSGs contêm um conjunto de regras padrão. as regras de saudação padrão não podem ser excluídas, mas porque eles recebem a prioridade mais baixa hello, elas podem ser substituídas pelas regras de saudação que você criar. 

Quando você associa um tooa NSG NIC, regras de acesso de rede Olá no hello NSG são NIC toothat somente aplicada. Se um NSG é aplicado tooa única NIC em uma VM multi-NIC, ele não afeta o tráfego toohello outros NICs. Você pode associar diferentes NSGs tooa NIC (ou máquina virtual, dependendo do modelo de implantação de saudação) e Olá sub-rede que uma NIC ou a VM está associada a. Prioridade é fornecida com base na direção de saudação do tráfego.

Certifique-se muito[plano](../../virtual-network/virtual-networks-nsg.md#planning) seus NSGs ao planejar suas máquinas virtuais e redes.

Esta tabela lista os métodos de saudação que você pode usar toocreate um grupo de segurança de rede.

| Método | Descrição |
| ------ | ----------- |
| [Portal do Azure](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md) | Quando você cria uma máquina virtual no hello portal do Azure, um NSG é criado automaticamente e associadas toohello NIC Olá portal cria. nome de saudação do hello NSG é uma combinação de nome de saudação do hello VM e **- nsg**. Este NSG contém uma regra de entrada com uma prioridade de 1000, tooRDP do conjunto de serviço, Olá tooTCP de conjunto de protocolo, porta definida too3389 e ação definida tooAllow. Se você quiser tooallow qualquer outro tráfego de entrada toohello VM, você deve adicionar regras adicionais toohello NSG. |
| [PowerShell do Azure](../../virtual-network/virtual-networks-create-nsg-arm-ps.md) | Use [AzureRmNetworkSecurityRuleConfig novo](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmNetworkSecurityRuleConfig) e fornecer informações de regra de saudação necessária. Use [AzureRmNetworkSecurityGroup novo](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmNetworkSecurityGroup) toocreate Olá NSG. Use [AzureRmVirtualNetworkSubnetConfig conjunto](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/Set-AzureRmVirtualNetworkSubnetConfig) tooconfigure Olá NSG para a sub-rede de saudação. Use [AzureRmVirtualNetwork conjunto](/powershell/module/azurerm.network/set-azurermvirtualnetwork) tooadd Olá NSG toohello VNet. |
| [CLI do Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md) | Use [criar az rede nsg](https://docs.microsoft.com/cli/azure/network/nsg#create) tooinitially criar hello NSG. Use [criar regra de nsg rede az](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) tooadd regras toohello NSG. Use [atualização de sub-rede da rede virtual de rede az](https://docs.microsoft.com/en-us/cli/azure/network/vnet/subnet#update) subrede tooadd Olá NSG toohello. |
| [Modelo](../../virtual-network/virtual-networks-create-nsg-arm-template.md) | Use [Criar um grupo de segurança de rede](https://github.com/Azure/azure-quickstart-templates/tree/master/101-security-group-create) como um guia para a implantação de um grupo de segurança de rede usando um modelo. |

## <a name="load-balancers"></a>Balanceadores de carga

[O balanceador de carga do Azure](../../load-balancer/load-balancer-overview.md) fornece tooyour aplicativos de alto desempenho de disponibilidade e rede. Um balanceador de carga pode ser configurado de maneira muito[equilibrar o tráfego da Internet](../../load-balancer/load-balancer-internet-overview.md) tooVMs ou [equilibrar o tráfego entre VMs em uma rede virtual](../../load-balancer/load-balancer-internal-overview.md). Um balanceador de carga também pode equilibrar o tráfego entre computadores locais e VMs em uma rede entre locais ou encaminhar o tráfego externo tooa VM específica.

Olá carga balanceador mapas de entrada e saída do tráfego entre Olá público endereço IP e porta no balanceador de carga hello e Olá endereço IP e porta de Olá VM.

Ao criar um balanceador de carga, você também deve considerar estes elementos de configuração:

- **Configuração de IP front-end** – um balanceador de carga pode incluir um ou mais endereços IP front-end, também conhecidos como VIPs (IPs virtuais). Esses endereços IP servem como entrada para o tráfego de saudação.
- **Pool de endereços de back-end** – endereços IP que estão associados com a carga de toowhich NIC Olá é distribuído.
- **Regras NAT** -define como o tráfego passa pela Olá front-end e IP distribuídos toohello back-end.
- **Regras de Balanceador de carga** -mapeia uma determinada IP de front-end e um conjunto de tooa de combinação de porta de combinação de porta e endereços IP de back-end. Um balanceador de carga único pode ter várias regras de balanceamento de carga. Cada regra é uma combinação de um IP de front-end e IP de porta e back-end e porta associada a VMs.
- **[Testes](../../load-balancer/load-balancer-custom-probe-overview.md)**  -monitores Olá integridade das VMs. Quando um teste falha toorespond, balanceador de carga hello interrompe o envio de novos toohello de conexões VM não íntegro. as conexões existentes Olá não são afetadas e novas conexões são enviadas toohealthy VMs.

Esta tabela lista os métodos de saudação que você pode usar toocreate um balanceador de carga para a internet.

| Método | Descrição |
| ------ | ----------- |
| Portal do Azure | No momento não é possível criar um balanceador de carga de voltados à internet usando Olá portal do Azure. |
| [PowerShell do Azure](../../load-balancer/load-balancer-get-started-internet-arm-ps.md) | tooprovide Olá identificador de IP público Olá endereço que você use criado anteriormente, [New-AzureRmLoadBalancerFrontendIpConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerFrontendIpConfig) com hello **- PublicIpAddress** parâmetro. Use [AzureRmLoadBalancerBackendAddressPoolConfig novo](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerBackendAddressPoolConfig) toocreate configuração de saudação do pool de endereços de back-end de saudação. Use [AzureRmLoadBalancerInboundNatRuleConfig novo](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerInboundNatRuleConfig) toocreate associadas a configuração IP de front-end Olá que você criou as regras de NAT de entrada. Use [AzureRmLoadBalancerProbeConfig novo](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerProbeConfig) toocreate Olá testes que você precisa. Use [AzureRmLoadBalancerRuleConfig novo](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerRuleConfig) toocreate configuração de Balanceador de carga de saudação. Use [AzureRmLoadBalancer novo](/powershell/module/azurerm.network/new-azurermloadbalancer) toocreate balanceador de carga de saudação.|
| [CLI do Azure](../../load-balancer/load-balancer-get-started-internet-arm-cli.md) | Use [criar de balanceamento de carga de rede az](https://docs.microsoft.com/cli/azure/network/lb#create) toocreate configuração de Balanceador de carga inicial de saudação. Use [ip de front-end de balanceamento de carga de rede de az criar](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) tooadd Olá endereço IP público que você criou anteriormente. Use [Criar pool de endereços de balanceamento de carga de rede de az](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) tooadd configuração de saudação do pool de endereços de back-end de saudação. Use [az rede lb--regra de entrada nat criar](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) tooadd as regras de NAT. Use [criar regra de balanceamento de carga de rede az](https://docs.microsoft.com/cli/azure/network/lb/rule#create) tooadd regras de Balanceador de carga de saudação. Use [criar investigação de balanceamento de carga de rede az](https://docs.microsoft.com/cli/azure/network/lb/probe#create) tooadd Olá investigações. |
| [Modelo](../../load-balancer/load-balancer-get-started-internet-arm-template.md) | Use [2 VMs em um balanceador de carga e configure as regras NAT em Olá LB](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-natrules) como um guia para implantar um balanceador de carga usando um modelo. |
    
Esta tabela lista os métodos de saudação que você pode usar toocreate um balanceador de carga interno.

| Método | Descrição |
| ------ | ----------- |
| Portal do Azure | No momento não é possível criar um balanceador de carga interno usando Olá portal do Azure. |
| [PowerShell do Azure](../../load-balancer/load-balancer-get-started-ilb-arm-ps.md) | tooprovide um endereço IP privado na sub-rede hello, use [New-AzureRmLoadBalancerFrontendIpConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerFrontendIpConfig) com hello **- PrivateIpAddress** parâmetro. Use [AzureRmLoadBalancerBackendAddressPoolConfig novo](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerBackendAddressPoolConfig) toocreate configuração de saudação do pool de endereços de back-end de saudação. Use [AzureRmLoadBalancerInboundNatRuleConfig novo](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerInboundNatRuleConfig) toocreate associadas a configuração IP de front-end Olá que você criou as regras de NAT de entrada. Use [AzureRmLoadBalancerProbeConfig novo](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerProbeConfig) toocreate Olá testes que você precisa. Use [AzureRmLoadBalancerRuleConfig novo](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerRuleConfig) toocreate configuração de Balanceador de carga de saudação. Use [AzureRmLoadBalancer novo](/powershell/module/azurerm.network/new-azurermloadbalancer) toocreate balanceador de carga de saudação.|
| [CLI do Azure](../../load-balancer/load-balancer-get-started-ilb-arm-cli.md) | Saudação de uso [criar de balanceamento de carga de rede az](https://docs.microsoft.com/cli/azure/network/lb#create) configuração de Balanceador de carga inicial de saudação do comando toocreate. toodefine Olá endereço IP privado, use [ip de front-end de balanceamento de carga de rede de az criar](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) com hello **– endereço de ip privado** parâmetro. Use [Criar pool de endereços de balanceamento de carga de rede de az](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) tooadd configuração de saudação do pool de endereços de back-end de saudação. Use [az rede lb--regra de entrada nat criar](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) tooadd as regras de NAT. Use [criar regra de balanceamento de carga de rede az](https://docs.microsoft.com/cli/azure/network/lb/rule#create) tooadd regras de Balanceador de carga de saudação. Use [criar investigação de balanceamento de carga de rede az](https://docs.microsoft.com/cli/azure/network/lb/probe#create) tooadd Olá investigações.|
| [Modelo](../../load-balancer/load-balancer-get-started-ilb-arm-template.md) | Use [2 VMs em um balanceador de carga e configure as regras NAT em Olá LB](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer) como um guia para implantar um balanceador de carga usando um modelo. |

## <a name="vms"></a>VMs

Máquinas virtuais podem ser criados em Olá mesmo VNet e eles podem se conectar a outros tooeach usando endereços IP privado. Eles podem se conectar mesmo que eles estejam em sub-redes diferentes sem Olá necessidade tooconfigure um gateway ou usem endereços IP públicos. tooput VMs em uma rede virtual, que você cria Olá rede virtual e, em seguida, ao criar cada VM, você atribuí-lo toohello rede virtual e sub-rede. As VMs adquirem suas configurações de rede durante a implantação ou a inicialização.  

Um endereço IP é atribuído às VMs quando elas são implantadas. Se você implantar várias VMs em uma rede virtual ou sub-rede, endereços IP serão atribuídos quando elas forem inicializadas. Um endereço IP dinâmico (DIP) é o endereço IP interno Olá associado a uma VM. Você pode alocar uma tooa DIP estático VM. Se você alocar um DIP estático, você deve considerar o uso de tooavoid uma sub-rede específica que acidentalmente reutilizando um DIP estático para outra VM.  

Se você criar uma máquina virtual e mais tarde quiser toomigrate-lo em uma rede virtual, não é uma alteração de configuração simples. Você deve reimplantar Olá VM em Olá VNet. Olá tooredeploy de maneira mais fácil é toodelete Olá VM, mas não todos os discos anexados tooit e, em seguida, recrie Olá VM usando Olá discos originais no hello VNet. 

Esta tabela lista os métodos de saudação que você pode usar toocreate uma VM em uma rede virtual.

| Método | Descrição |
| ------ | ----------- |
| [Portal do Azure](../virtual-machines-windows-hero-tutorial.md) | Usa Olá configurações de rede padrão que foram previamente mencionados toocreate uma VM com uma única placa de rede. toocreate uma VM com várias placas de rede, você deve usar um método diferente. |
| [PowerShell do Azure](../virtual-machines-windows-ps-create.md) | Inclui o uso de saudação do [AzureRmVMNetworkInterface adicionar](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) tooadd Olá NIC que você criou anteriormente toohello configuração da VM. |
| [Modelo](ps-template.md) | Use [Implantação muito simples de uma VM do Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) como um guia para implantar uma VM usando um modelo. |

## <a name="next-steps"></a>Próximas etapas

- Saiba como tooconfigure [rotas definidas pelo usuário e encaminhamento de IP](../../virtual-network/virtual-networks-udr-overview.md). 
- Saiba como tooconfigure [VNet tooVNet conexões](../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).
- Saiba como muito[solucionar rotas](../../virtual-network/virtual-network-routes-troubleshoot-portal.md).
