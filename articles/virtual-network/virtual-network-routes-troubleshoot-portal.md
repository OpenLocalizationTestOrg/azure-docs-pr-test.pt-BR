---
title: rotas aaaTroubleshoot - Portal | Microsoft Docs
description: "Saiba como rotas tootroubleshoot hello Azure Resource Manager implantação modelo usando Olá Portal do Azure."
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: bdd8b6dc-02fb-4057-bb23-8289caa9de89
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 579bae91ef3200852032b3953d3cc5d26deada86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-routes-using-hello-azure-portal"></a>Solucionar problemas de rotas usando Olá Portal do Azure
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

1. Logon toohello portal do Azure em https://portal.azure.com.
2. Clique em **mais serviços**, em seguida, clique em **máquinas virtuais** na lista de saudação que aparece.
3. Selecione tootroubleshoot uma VM na lista de saudação que é exibido e uma folha VM com opções é exibida.
4. Clique em **Diagnosticar e resolver problemas** e selecione um problema comum. Neste exemplo, **toomy VM do Windows não consigo conectar** está selecionado.

    ![](./media/virtual-network-routes-troubleshoot-portal/image1.png)
5. Etapas aparecem em problema hello, conforme mostrado na figura abaixo de saudação:

    ![](./media/virtual-network-routes-troubleshoot-portal/image2.png)

    Clique em *rotas efetivas* na lista de saudação de etapas recomendadas.
6. Olá **rotas efetivas** folha é exibida, conforme mostrado na figura abaixo de saudação:

    ![](./media/virtual-network-routes-troubleshoot-portal/image3.png)

    Se sua VM tiver apenas um NIC, ele será selecionado por padrão. Se você tiver mais de uma NIC, selecione NIC Olá para o qual você deseja rotas efetivas do tooview hello.

   > [!NOTE]
   > Se hello VM associado hello NIC não está no estado de execução, rotas efetivas não serão exibidas. Somente hello 200 primeiros rotas efetivas são mostradas no portal de saudação. Para a lista completa de saudação, clique em **baixar**. Você pode filtrar ainda mais sobre os resultados de saudação do hello baixado. csv.
   >
   >

    Observe o seguinte Olá na saída de hello:

   * **Origem**: indica o tipo de saudação da rota. Rotas de sistema são mostradas como *Default*, UDRs são mostradas como *User* e as rotas de gateway (estáticas ou BGP) são mostradas como *VPNGateway*.
   * **Estado**: indica o estado da rota efetiva hello. Os valores possíveis são *Active* ou *Invalid*.
   * **AddressPrefixes**: Especifica o prefixo do endereço de saudação da rota efetiva Olá na notação CIDR.
   * **nextHopType**: indica o próximo salto Olá Olá considerando a rota. Os valores possíveis são *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering* ou *Null*. Um valor *Null* para **nextHopType** em uma UDR pode indicar uma rota inválida. Por exemplo, se **nextHopType** é *VirtualAppliance* e solução de virtualização de rede do hello VM não está em um estado de execução/provisionado. Se **nextHopType** é *o VPNGateway* e há um gateway provisionado/em execução no hello VNet fornecido, rota Olá pode se tornar inválida.
7. Não há nenhuma rota listada toohello *WestUS VNET3* VNet (prefixo 10.10.0.0/16) de saudação *WestUS VNet1* (prefixo 10.9.0.0/16) na imagem de saudação na etapa anterior hello. Nas Olá figura abaixo, link emparelhamento hello está sendo Olá *Disconnected* estado:

    ![](./media/virtual-network-routes-troubleshoot-portal/image4.png)

    link de bi-direcional Olá Olá emparelhamento é interrompida, que explica por que VM1 não pôde se conectar tooVM3 em Olá *WestUS VNet3* VNet.
8. Olá imagem a seguir mostra as rotas de saudação depois de estabelecer um link de emparelhamento de bi-direcional hello:

    ![](./media/virtual-network-routes-troubleshoot-portal/image5.png)

Para cenários de solução de problemas mais para avaliação de rota e de túnel forçado, leia Olá [considerações](virtual-network-routes-troubleshoot-portal.md#considerations) deste artigo.

### <a name="view-effective-routes-for-a-network-interface"></a>Exibir rotas em vigor para um adaptador de rede
Se o fluxo do tráfego de rede for afetado para um NIC (adaptador de rede) específico, você poderá ver uma lista completa de rotas em vigor em um NIC diretamente. toosee Olá agregação rotas que são aplicada tooa NIC, Olá concluir as etapas a seguir:

1. Logon toohello portal do Azure em https://portal.azure.com.
2. Clique em **Mais serviços** e, em seguida, clique em **Interfaces de rede**
3. Pesquisar lista Olá para o nome de saudação de uma NIC ou selecioná-lo na lista de saudação que é exibida. Neste exemplo, **VM1-NIC1** foi selecionada.
4. Selecione **rotas efetivas** em Olá **interface de rede** folha, conforme mostrado na figura abaixo de saudação:

       ![](./media/virtual-network-routes-troubleshoot-portal/image6.png)

    Olá **escopo** interface de rede toohello padrões selecionado.

      ![](./media/virtual-network-routes-troubleshoot-portal/image7.png)

### <a name="view-effective-routes-for-a-route-table"></a>Exibir rotas em vigor para uma tabela de rotas
Ao modificar as rotas definidas pelo usuário (UDRs) em uma tabela de rota, talvez você queira tooreview impacto de saudação de rotas Olá que está sendo adicionado em uma VM específica. Uma tabela de rotas pode ser associada a qualquer número de sub-redes. Agora você pode exibir todas as rotas efetivas de Olá para todos os Olá NICs de uma tabela de rota em questão é aplicada, sem ter que tooswitch o contexto da saudação dada folha da tabela de rota.

Neste exemplo, uma UDR (*UDRoute*) é especificada em uma tabela de rotas (*UDRouteTable*). Essa rota envia todo o tráfego de Internet de *Subnet1* em Olá *WestUS VNet1* VNet, por meio de um dispositivo de rede virtual NVA (), em *Subnet2* de Olá mesma rede virtual. rota de saudação é mostrada no hello figura abaixo:

![](./media/virtual-network-routes-troubleshoot-portal/image8.png)

rotas agregada do hello toosee uma tabela de rota, Olá concluir as etapas a seguir:

1. Logon toohello portal do Azure em https://portal.azure.com.
2. Clique em **Mais serviços** e, em seguida, clique em **Tabelas de rotas**
3. A lista de tabela de rotas Olá Olá pesquisa que você deseja toosee rotas de agregação para e selecioná-lo. Neste exemplo, **UDRouteTable** foi selecionado. Uma folha para a tabela de rotas Olá selecionado é exibida, conforme mostrado na figura abaixo de saudação:

    ![](./media/virtual-network-routes-troubleshoot-portal/image9.png)
4. Selecione **rotas efetivas** em Olá **tabela de rotas** folha. Olá **escopo** está definida toohello tabela de rota selecionada.
5. Uma tabela de rota pode ser aplicado toomultiple sub-redes. Selecione Olá **sub-rede** deseja tooreview da lista de saudação. Neste exemplo, a **Subnet1** foi selecionada.
6. Selecione um **Adaptador de rede**. Todas as NICs conectados toohello selecionado está listada. Neste exemplo, **VM1-NIC1** foi selecionada.

    ![](./media/virtual-network-routes-troubleshoot-portal/image10.png)

   > [!NOTE]
   > Se Olá NIC não está associado uma VM em execução, nenhuma rotas efetivas serão mostradas.
   >
   >

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
  * Regras de grupo de segurança de rede (NSG) podem estar afetando Olá fluxos de tráfego. Para obter mais informações, consulte Olá [solucionar problemas de grupos de segurança de rede](virtual-network-nsg-troubleshoot-portal.md) artigo.
