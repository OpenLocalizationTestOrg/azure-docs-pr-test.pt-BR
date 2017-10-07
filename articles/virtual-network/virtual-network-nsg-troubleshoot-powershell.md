---
title: "aaaTroubleshoot grupos de segurança de rede - PowerShell | Microsoft Docs"
description: "Saiba como grupos de segurança de rede tootroubleshoot na implantação do Azure Resource Manager Olá modelo usando o PowerShell do Azure."
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 4c732bb7-5cb1-40af-9e6d-a2a307c2a9c4
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 95fd60fa72cf6d17fa990e3c3eb7d980878f7c15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-network-security-groups-using-azure-powershell"></a>Solucionar problemas de grupos de segurança de rede usando o Azure PowerShell
> [!div class="op_single_selector"]
> * [Portal do Azure](virtual-network-nsg-troubleshoot-portal.md)
> * [PowerShell](virtual-network-nsg-troubleshoot-powershell.md)
> 
> 

Se configurado os grupos de segurança de rede (NSGs) em sua máquina virtual (VM) e estão com problemas de conectividade VM, este artigo fornece uma visão geral dos recursos de diagnóstico para os NSGs toohelp solucionar outros problemas.

Os NSGs permitem que você toocontrol tipos de saudação do tráfego de fluxo para dentro e fora de suas máquinas virtuais (VMs). Os NSGs podem ser aplicadas toosubnets em uma rede Virtual do Azure (VNet), interfaces de rede (NIC) ou ambos. Olá efetivo regras aplicadas tooa NIC são uma agregação das regras de saudação que existem no hello NSGs aplicados tooa NIC e hello sub-rede está conectado ao. As regras nesses NSGs podem, às vezes, entrar em conflito umas com as outras e afetar a conectividade de rede de uma VM.  

Você pode exibir todas as regras de segurança efetiva de saudação do seus NSGs aplicados ao NICs da VM. Este artigo mostra como problemas de conectividade VM tootroubleshoot usando essas regras em Olá modelo de implantação do Gerenciador de recursos do Azure. Se você não estiver familiarizado com conceitos de rede virtual e NSG, leia Olá [rede Virtual](virtual-networks-overview.md) e [grupos de segurança de rede](virtual-networks-nsg.md) artigos de visão geral.

## <a name="using-effective-security-rules-tootroubleshoot-vm-traffic-flow"></a>Usando o fluxo de tráfego VM de tootroubleshoot de regras de segurança efetiva
cenário de saudação que segue é um exemplo de um problema de conexão comum:

Uma VM denominada *VM1* faz parte de uma sub-rede denominada *Subnet1* em uma VNet denominada *WestUS-VNet1*. Toohello de tooconnect uma tentativa de VM usando o RDP usando a porta TCP 3389 falhará. Os NSGs são aplicados em ambos os Olá NIC *VM1 NIC1* e Olá sub-rede *Subnet1*. TooTCP porta 3389 do tráfego é permitida em Olá associado à interface de rede de saudação do NSG *VM1 NIC1*, no entanto, porta 3389 ocorre uma falha da tooVM1 ping do TCP.

Embora este exemplo usa a porta TCP 3389, Olá seguintes etapas pode ser usada toodetermine falhas de conexão de entrada e saída em qualquer porta.

## <a name="detailed-troubleshooting-steps"></a>Etapas de solução de problemas detalhadas
Concluir Olá seguindo as etapas tootroubleshoot NSGs para uma VM:

1. Inicie um tooAzure de logon e de sessão do PowerShell do Azure. Se você não estiver familiarizado com o uso do PowerShell do Azure, leia Olá [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) artigo.
2. Digite hello tooreturn aplicação de todas as regras NSG tooa NIC chamada do comando a seguir *VM1 NIC1* no grupo de recursos de saudação *RG1*:
   
        Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > Se você não souber o nome de saudação de uma NIC, digite Olá nomes de saudação do comando tooretrieve de todas as NICs de um grupo de recursos a seguir: 
   > 
   > `Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name`
   > 
   > 
   
    Olá, texto a seguir é um exemplo de saída de regras efetivo hello retornada para Olá *VM1 NIC1* NIC:
   
        NetworkSecurityGroup   : {
                                   "Id": "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkSecurityGroups/VM1-NIC1-NSG"
                                 }
        Association            : {
                                   "NetworkInterface": {
                                     "Id": "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkInterfaces/VM1-NIC1"
                                   }
                                 }
        EffectiveSecurityRules : [
                                 {
                                 "Name": "securityRules/allowRDP",
                                 "Protocol": "Tcp",
                                 "SourcePortRange": "0-65535",
                                 "DestinationPortRange": "3389-3389",
                                 "SourceAddressPrefix": "Internet",
                                 "DestinationAddressPrefix": "0.0.0.0/0",
                                 "ExpandedSourceAddressPrefix": [… ],
                                 "ExpandedDestinationAddressPrefix": [],
                                 "Access": "Allow",
                                 "Priority": 1000,
                                 "Direction": "Inbound"
                                 },
                                 {
                                 "Name": "defaultSecurityRules/AllowVnetInBound",
                                 "Protocol": "All",
                                 "SourcePortRange": "0-65535",
                                 "DestinationPortRange": "0-65535",
                                 "SourceAddressPrefix": "VirtualNetwork",
                                 "DestinationAddressPrefix": "VirtualNetwork",
                                 "ExpandedSourceAddressPrefix": [
                                  "10.9.0.0/16",
                                  "168.63.129.16/32",
                                  "10.0.0.0/16",
                                  "10.1.0.0/16"
                                  ],
                                 "ExpandedDestinationAddressPrefix": [
                                  "10.9.0.0/16",
                                  "168.63.129.16/32",
                                  "10.0.0.0/16",
                                  "10.1.0.0/16"
                                  ],
                                  "Access": "Allow",
                                  "Priority": 65000,
                                  "Direction": "Inbound"
                                  },…
                         ]
   
        NetworkSecurityGroup   : {
                                   "Id": 
                                 "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkSecurityGroups/Subnet1-NSG"
                                 }
        Association            : {
                                   "Subnet": {
                                     "Id": 
                                 "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/virtualNetworks/WestUS-VNet1/subnets/Subnet1"
                                 }
                                 }
        EffectiveSecurityRules : [
                                 {
                                "Name": "securityRules/denyRDP",
                                "Protocol": "Tcp",
                                "SourcePortRange": "0-65535",
                                "DestinationPortRange": "3389-3389",
                                "SourceAddressPrefix": "Internet",
                                "DestinationAddressPrefix": "0.0.0.0/0",
                                "ExpandedSourceAddressPrefix": [
                                   ... ],
                                "ExpandedDestinationAddressPrefix": [],
                                "Access": "Deny",
                                "Priority": 1000,
                                "Direction": "Inbound"
                                },
                                {
                                "Name": "defaultSecurityRules/AllowVnetInBound",
                                "Protocol": "All",
                                "SourcePortRange": "0-65535",
                                "DestinationPortRange": "0-65535",
                                "SourceAddressPrefix": "VirtualNetwork",
                                "DestinationAddressPrefix": "VirtualNetwork",
                                "ExpandedSourceAddressPrefix": [
                                "10.9.0.0/16",
                                "168.63.129.16/32",
                                "10.0.0.0/16",
                                "10.1.0.0/16"
                                ],
                                "ExpandedDestinationAddressPrefix": [
                                "10.9.0.0/16",
                                "168.63.129.16/32",
                                "10.0.0.0/16",
                                "10.1.0.0/16"
                                ],
                                "Access": "Allow",
                                "Priority": 65000,
                                "Direction": "Inbound"
                                },...
                                ]
   
    Observe Olá informações na saída de hello a seguir:
   
   * Há duas seções **NetworkSecurityGroup**: uma é associada a uma sub-rede (*Subnet1*) e a outra é associada a uma NIC (*VM1-NIC1*). Neste exemplo, um NSG foi tooeach aplicado.
   * **Associação** mostra que o recurso de saudação (subrede ou NIC) um determinado NSG está associado. Se Olá recurso NSG é desassociado/movido imediatamente antes de executar esse comando, você pode precisar toowait alguns segundos para Olá tooreflect de alteração na saída do comando hello. 
   * Olá nomes de regras que são precedidos de *defaultSecurityRules*: quando um NSG é criado, várias regras de segurança padrão são criadas com ela. Regras padrão não podem ser removidas, mas podem ser substituídas por regras com prioridade mais alta.
     Saudação de leitura [visão geral do NSG](virtual-networks-nsg.md#default-rules) artigo toolearn mais sobre o NSG padrão de regras de segurança.
   * **ExpandedAddressPrefix** expande os prefixos de endereço Olá para marcas de padrão NSG. As marcações representam vários prefixos de endereço. Expansão de marcas Olá pode ser útil ao solucionar problemas de conectividade VM de prefixos de endereço específico. Por exemplo, com o emparelhamento de rede virtual, a marca VIRTUAL_NETWORK expande tooshow emparelhadas prefixos de rede virtual na saída de saudação anterior.
     
     > [!NOTE]
     > Olá regras efetivo do comando apenas mostra se um NSG está associado uma sub-rede, uma NIC ou ambos. Uma VM pode ter várias NICs com diferentes NSGs aplicados. Ao solucionar o problema, execute o comando de saudação para cada NIC.
     > 
     > 
3. tooease filtragem maior número de regras do NSG, digite Olá comandos tootroubleshoot ainda mais a seguir: 
   
        $NSGs = Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
        $NSGs.EffectiveSecurityRules | Sort-Object Direction, Access, Priority | Out-GridView
   
    Um filtro para o tráfego RDP (porta TCP 3389), é aplicada a exibição de grade toohello, conforme mostrado na figura abaixo de saudação:
   
    ![Lista de regras](./media/virtual-network-nsg-troubleshoot-powershell/rules.png)
4. Como você pode ver no modo de exibição de grade hello, há dois permitirem e negar regras para RDP. Olá, saída da etapa 2 mostra que Olá *DenyRDP* a regra está em Olá NSG aplicada toohello sub-rede. Para regras de entrada, os NSGs aplicados toohello sub-rede são processadas primeiro. Se uma correspondência for encontrada, a interface de rede do hello NSG aplicada toohello não foi processada. Nesse caso, Olá *DenyRDP* blocos de regra da sub-rede Olá RDP toohello VM (**VM1**).
   
   > [!NOTE]
   > Uma VM pode ter várias NICs e anexado tooit. Cada um pode ser conectado tooa outra sub-rede. Como comandos de saudação nas etapas anteriores Olá são executados em relação a uma NIC, é importante tooensure que você especificar Olá NIC estiver com falha de conectividade de saudação em. Se você não tiver certeza, você também pode executar comandos de saudação em relação a cada toohello NIC conectada VM.
   > 
   > 
5. tooRDP na VM1, alteração Olá *negar RDP (3389)* regra muito*permitir RDP(3389)* em Olá **Subnet1 NSG** NSG. Confirme que a porta TCP 3389 esteja aberta abrindo uma conexão de RDP toohello VM ou usando a ferramenta de PsPing hello. Você pode aprender mais sobre PsPing ao ler Olá [PsPing página de download](https://technet.microsoft.com/sysinternals/psping.aspx)
   
    Você pode ou remove as regras de um NSG usando informações de saudação da saída Olá Olá comando a seguir:
   
        Get-Help *-AzureRmNetworkSecurityRuleConfig

## <a name="considerations"></a>Considerações
Considere Olá pontos a seguir ao solucionar problemas de conectividade:

* As regras NSG padrão bloqueará o acesso de entrada de saudação à internet e permitir VNet o tráfego de entrada. As regras devem ser adicionadas explicitamente tooallow acesso de entrada da Internet, conforme necessário.
* Se não houver nenhuma regra de segurança NSG causando toofail de conectividade de rede da VM, problema de saudação pode ser devido a:
  * Software de firewall em execução no sistema operacional da VM Olá
  * Rotas configuradas para soluções de virtualização ou tráfego local. Tráfego de Internet pode ser redirecionado tooon local por meio de túnel forçado. Uma conexão de RDP/SSH de saudação Internet tooyour VM pode não funcionar com essa configuração, dependendo de como o hardware de rede local Olá lida com esse tráfego. Saudação de leitura [rotas de solução de problemas](virtual-network-routes-troubleshoot-powershell.md) artigo toolearn como toodiagnose encaminhar os problemas que podem estar impedindo Olá fluxo do tráfego do hello VM. 
* Se você tiver emparelhadas VNets, por padrão, Olá marca VIRTUAL_NETWORK expandirá automaticamente tooinclude prefixos para emparelhadas VNets. Você pode exibir esses prefixos no hello **ExpandedAddressPrefix** listar, tootroubleshoot qualquer tooVNet relacionados problemas emparelhamento de conectividade. 
* Regras de segurança efetiva são mostradas apenas se houver que um NSG associado da VM Olá NIC e ou uma sub-rede. 
* Se não há nenhum NSGs associados Olá NIC ou sub-rede e tiver um endereço IP público atribuído tooyour VM, todas as portas será abertas para acesso de entrada e saído. Se Olá VM tem um endereço IP público, aplicar os NSGs toohello NIC ou sub-rede é recomendável.  

