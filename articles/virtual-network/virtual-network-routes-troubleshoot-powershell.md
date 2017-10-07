---
title: rotas aaaTroubleshoot - PowerShell | Microsoft Docs
description: "Saiba como tootroubleshoot roteia no modelo de implantação do Azure Resource Manager hello usando o PowerShell do Azure."
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: bf7dc5e7-9399-460e-8e0d-8992dbed98a6
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 7a07806df5c1d0caee921187e6ad29f6755ab535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-routes-using-azure-powershell"></a>Solucionar problemas de rotas usando o Azure PowerShell
> [!div class="op_single_selector"]
> * [Portal do Azure](virtual-network-routes-troubleshoot-portal.md)
> * [PowerShell](virtual-network-routes-troubleshoot-powershell.md)
> 
> 

Se você estiver enfrentando tooor de problemas de conectividade de rede de sua máquina Virtual (VM) do Azure, rotas podem estar afetando os fluxos de tráfego VM. Este artigo fornece uma visão geral dos recursos de diagnóstico para rotas toohelp solucionar outros problemas.

As tabelas de rotas são associadas a sub-redes e estão em vigor em todas as NICs (interfaces de rede) nessa sub-rede. Olá seguintes tipos de rotas pode ser aplicado tooeach interface de rede:

* **Rotas de sistema:** por padrão, cada sub-rede criada em uma VNet (rede virtual) do Azure tem tabelas de rotas de sistema que possibilitam o tráfego da VNet, o tráfego local por meio de gateways de VPN e o tráfego da Internet. Também existem rotas de sistema para VNets emparelhadas.
* **Rotas de BGP:** propagadas toonetwork interfaces por meio de rota expressa ou conexões VPN site a site. Saiba mais sobre o roteamento de BGP lendo Olá [BGP com gateways de VPN](../vpn-gateway/vpn-gateway-bgp-overview.md) e [visão geral do ExpressRoute](../expressroute/expressroute-introduction.md) artigos.
* **Rotas definidas pelo usuário (UDR):** se você estiver usando dispositivos de rede virtual ou são forçados túnel de tráfego tooan no local de rede por meio de uma VPN site a site, você pode ter definido pelo usuário rotas (UDRs) associadas com sua tabela de rotas de sub-rede. Se você não estiver familiarizado com UDRs, leia Olá [rotas definidas pelo usuário](virtual-networks-udr-overview.md#user-defined-routes) artigo.

Com hello várias rotas que podem ser aplicadas tooa interface de rede, pode ser difícil toodetermine quais rotas agregação entrarão em vigor. toohelp solucionar problemas de conectividade de rede VM, você pode exibir todas as rotas efetivas de saudação para uma interface de rede no modelo de implantação do Azure Resource Manager hello.

## <a name="using-effective-routes-tootroubleshoot-vm-traffic-flow"></a>Usando o fluxo de tráfego VM rotas efetivas tootroubleshoot
Este artigo usa Olá cenário a seguir como um tooillustrate de exemplo como tootroubleshoot Olá efetiva roteia para uma interface de rede:

Uma VM (*VM1*) conectados a redes de toohello (*VNet1*, prefixo: 10.9.0.0/16) falha tooconnect tooa VM(VM3) em uma rede virtual peered recentemente (*VNet3*, prefixo 10.10.0.0/16). Não há nenhum UDRs ou BGP roteia toohello interface conectada da rede aplicado tooVM1-NIC1 VM, apenas as rotas de sistema são aplicadas.

Este artigo explica como Olá toodetermine causa da falha de conexão hello, usando o recurso de rotas efetiva no modelo de implantação do gerenciamento de recursos do Azure.
Enquanto o exemplo hello usa apenas as rotas de sistema, Olá mesmas etapas pode ser usada toodetermine falhas de conexão de entrada e saída em qualquer tipo de rota.

> [!NOTE]
> Se sua VM tem mais de uma NIC anexada, verifique rotas efetivas para cada Olá tooand de problemas de conectividade NICs toodiagnose rede de uma VM.
> 
> 

### <a name="view-effective-routes-for-a-virtual-machine"></a>Exibir rotas em vigor para uma máquina virtual
toosee Olá agregação rotas que são aplicada tooa VM, Olá concluir as etapas a seguir:

### <a name="view-effective-routes-for-a-network-interface"></a>Exibir rotas em vigor para um adaptador de rede
toosee Olá agregação rotas que são aplicadas tooa interface de rede, Olá concluir as etapas a seguir:

1. Inicie um tooAzure de logon e de sessão do PowerShell do Azure. Se você não estiver familiarizado com o PowerShell do Azure, leia Olá [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) artigo.
2. comando a seguir Hello retorna todos os interface de rede de tooa rotas aplicadas denominado *VM1 NIC1* no grupo de recursos de saudação *RG1*.
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > Se você não souber o nome de saudação de uma interface de rede, digite Olá nomes de saudação do comando tooretrieve de todas as interfaces de rede em um recurso group.* a seguir
   > 
   > 
   
       Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name
   
   Olá saída a seguir procura saída toohello semelhante cada saudação de sub-rede rota aplicada toohello A que NIC está conectada:
   
       Name :
       State : Active
       AddressPrefix : {10.9.0.0/16}
       NextHopType : VNetLocal
       NextHopIpAddress : {}
   
       Name :
       State : Active
       AddressPrefix : {0.0.0.0/16}
       NextHopType : Internet
       NextHopIpAddress : {}
   
   Observe o seguinte Olá na saída de hello:
   
   * **Nome**: nome da rota efetiva Olá pode ser vazio, a menos que explicitamente especificado, para rotas definidas pelo usuário. 
   * **Estado**: indica o estado da rota efetiva hello. Os valores possíveis são “Active” ou “Invalid”
   * **AddressPrefixes**: Especifica o prefixo do endereço de saudação da rota efetiva Olá na notação CIDR. 
   * **nextHopType**: indica o próximo salto Olá Olá considerando a rota. Os valores possíveis são *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering* ou *Null*. Um valor *Null* para **nextHopType** em uma UDR pode indicar uma rota inválida. Por exemplo, se **nextHopType** é *VirtualAppliance* e solução de virtualização de rede do hello VM não está em um estado de execução/provisionado. Se **nextHopType** é *o VPNGateway* e há um gateway provisionado/em execução no hello VNet fornecido, rota Olá pode se tornar inválida.
   * **NextHopIpAddress**: Especifica o endereço IP de saudação do próximo salto de saudação da rota efetiva hello.
   
   Olá comando a seguir retorna as rotas de saudação em uma tabela tooview mais fácil:
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1 | Format-Table
   
   Olá saída a seguir está algumas das Olá saída recebida para o cenário de saudação descrito anteriormente:
   
       Name State AddressPrefix NextHopType NextHopIpAddress
       ---- ----- ------------- ----------- ----------------
       Active {10.9.0.0/16} VnetLocal {}
       Active {0.0.0.0/0} Internet {}
3. Não há nenhuma rota listada toohello *WestUS VNet3* VNet (prefixo 10.10.0.0/16)** de *WestUS VNet1* (prefixo 10.9.0.0/16) na saída de saudação da etapa anterior hello. Conforme mostrado na figura abaixo de saudação, Olá link de emparelhamento VNet com hello *WestUS VNet3* rede virtual está em Olá *Disconnected* estado.
   
    ![](./media/virtual-network-routes-troubleshoot-portal/image4.png)
   
    link de bi-direcional Olá Olá emparelhamento é interrompida, que explica por que VM1 não pôde se conectar tooVM3 em Olá *WestUS VNet3* VNet. Configure um link de emparelhamento de VNet bidirecional novamente para as VNets *WestUS-VNet1* e *WestUS-VNet3*. saída de Hello retornada depois que o link de emparelhamento de rede virtual Olá é estabelecida corretamente a seguinte:
   
        Name State AddressPrefix NextHopType NextHopIpAddress
        ---- ----- ------------- ----------- ----------------
        Active {10.9.0.0/16} VnetLocal {}
        Active {10.10.0.0/16} VNetPeering {}
        Active {0.0.0.0/0} Internet {}
   
    Depois de determinar o problema hello, você pode adicionar, remover, ou alterar as rotas e tabelas de rota. Digite hello após o comando toosee uma lista de saudação comandos usados toodo assim:
   
        Get-Help *-AzureRmRouteConfig

## <a name="considerations"></a>Considerações
Alguns tookeep coisas em mente ao examinar a lista de saudação de rotas retornado:

* O roteamento é baseado no LPM (Correspondência de Prefixo Mais Longo) entre UDRs, rotas BGP e do sistema. Se houver mais de uma rota com hello mesmo LPM corresponder, então uma rota é selecionada com base em sua origem no hello ordem a seguir:
  
  * Rota definida pelo usuário
  * Rota BGP
  * Rota do sistema (padrão)
    
    Com rotas efetivas, você pode ver apenas as rotas efetivas que são LPM correspondência com base em todas as rotas do hello disponível. Mostrando como rotas hello, na verdade, são avaliadas para uma NIC determinada, isso torna muito mais fácil rotas de tootroubleshoot específicas que podem afetar a conectividade de sua VM.
* Se você tiver UDRs e está enviando o dispositivo virtual de rede tooa do tráfego NVA (), com *VirtualAppliance* como **nextHopType**, verifique se o encaminhamento de IP está habilitado no tráfego de recebimento Olá Olá NVA ou os pacotes são descartados. 
* Se o túnel forçado estiver habilitado, todo o tráfego de saída do Internet será roteado tooon local. RDP/SSH de Internet tooyour que VM pode não funcionar com essa configuração, dependendo de como Olá local trata esse tráfego. 
  O túnel forçado pode ser habilitado:
  * Se você estiver usando a VPN site a site, definindo uma UDR (rota definida pelo usuário) com nextHopType como Gateway de VPN
  * Se uma rota padrão é anunciada por meio do BGP
* Para a rede virtual emparelhamento tráfego toowork corretamente, uma rota de sistema com **nextHopType** *VNetPeering* deve existir para Olá emparelhadas intervalo de prefixo da rede virtual. Se tal uma rota não existir e Olá emparelhamento VNet link é Okey:
  * Aguarde alguns segundos e tente novamente se for um link de emparelhamento recém-estabelecido. Ocasionalmente, leva mais rotas de toopropagate interfaces de rede Olá tooall em uma sub-rede.
  * Regras de grupo de segurança de rede (NSG) podem estar afetando Olá fluxos de tráfego. Para obter mais informações, consulte Olá [solucionar problemas de grupos de segurança de rede](virtual-network-nsg-troubleshoot-powershell.md) artigo.

