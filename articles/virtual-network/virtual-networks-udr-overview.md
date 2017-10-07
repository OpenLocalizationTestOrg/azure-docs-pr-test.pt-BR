---
title: rotas definidas aaaUser e encaminhamento de IP no Azure | Microsoft Docs
description: "Saiba como rotas definidas pelo usuário do tooconfigure (UDR) e o encaminhamento IP tooforward tráfego toonetwork de dispositivos virtuais no Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: c39076c4-11b7-4b46-a904-817503c4b486
ms.service: virtual-network
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f1f1d46166d5a7c776f472b7ade1354d943ece10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="user-defined-routes-and-ip-forwarding"></a>Encaminhamento IP e rotas definidas pelo usuário

Quando você adiciona máquinas virtuais (VMs) tooa VPN (rede virtual) no Azure, você observará que Olá VMs são capaz de toocommunicate entre si pela rede hello, automaticamente. Não é necessário toospecify um gateway, embora Olá VMs estiverem em sub-redes diferentes. Olá mesmo é verdadeiro para comunicação de saudação VMs toohello Internet pública e rede de local tooyour mesmo quando uma conexão híbrida do Azure tooyour possui datacenter estiver presente.

Este fluxo de comunicação é possível porque o Azure usa uma série de sistema rotas toodefine como fluxos de tráfego IP. Rotas de sistema controlam o fluxo de saudação de comunicação no hello os seguintes cenários:

* No hello na mesma sub-rede.
* De tooanother uma sub-rede dentro de uma rede virtual.
* De VMs toohello da Internet.
* De uma rede virtual tooanother redes por meio de um gateway de VPN.
* De uma rede virtual tooanother VNet a VNet emparelhamento (encadeamento de serviço).
* De uma rede tooyour no local de rede virtual por meio de um gateway de VPN.

Olá figura a seguir mostra uma configuração simples com uma rede virtual, duas sub-redes e algumas VMs, juntamente com hello rotas de sistema que permitem tooflow de tráfego IP.

![Rotas de sistema no Azure](./media/virtual-networks-udr-overview/Figure1.png)

Embora o uso de saudação de rotas do sistema facilita tráfego automaticamente para sua implantação, há casos em que você quer toocontrol Olá roteamento de pacotes por meio de um dispositivo virtual. Você pode então crie rotas definidas pelo usuário que especificar próximo salto Olá para pacotes que fluem de dispositivo virtual do tooa sub-rede específica toogo tooyour em vez disso, e habilitando IP encaminhamento para Olá VM em execução como dispositivo virtual hello.

Olá figura abaixo mostra um exemplo de rotas definidas pelo usuário e encaminhamento tooforce pacotes IP enviada tooone sub-rede do outro toogo por meio de um dispositivo virtual em uma sub-rede de terceiro.

![Rotas de sistema no Azure](./media/virtual-networks-udr-overview/Figure2.png)

> [!IMPORTANT]
> Rotas definidas pelo usuário são aplicada tootraffic deixando uma sub-rede de qualquer recurso (como interfaces de rede conectados tooVMs) na sub-rede hello. Não é possível criar rotas toospecify como tráfego entra em uma sub-rede de saudação da Internet, por exemplo. dispositivo Olá estiverem encaminhando tráfego toocannot estar no hello mesma sub-rede em que o tráfego de saudação se origina. Sempre crie uma sub-rede separada para seus dispositivos. 
> 
> 

## <a name="route-resource"></a>Recurso de rota
Os pacotes são roteados por uma rede TCP/IP com base em uma tabela de rotas definida em cada nó na rede física hello. Uma tabela de rotas é que uma coleção de rotas individuais usadas toodecide onde tooforward pacotes com base no destino Olá endereço IP. Uma rota consiste nas seguintes hello:

| Propriedade | Descrição | Restrições | Considerações |
| --- | --- | --- | --- |
| Prefixo de Endereço |Olá destino CIDR toowhich Olá rota se aplica, como 10.1.0.0/16. |Deve ser um intervalo CIDR válido que representa os endereços Olá Internet pública, a rede virtual do Azure ou o datacenter local. |Verifique se Olá **prefixo de endereço** não tem endereço Olá Olá **próximo salto**, caso contrário, seus pacotes entrará em um loop indo de próximo salto do hello fonte toohello sem atinja destino de saudação. |
| Tipo do próximo salto |tipo de saudação do pacote de saudação do nó do Azure deve ser enviado para. |Deve ser um Olá valores a seguir: <br/> **Rede Virtual**. Representa a rede virtual local de saudação. Por exemplo, se você tiver duas sub-redes, 10.1.0.0/16 e 10.2.0.0/16 na mesma rede virtual de hello, rota Olá para cada sub-rede na tabela de rotas Olá terá um valor próximo salto *rede Virtual*. <br/> **Gateway de Rede Virtual**. Representa um Gateway de VPN S2S do Azure. <br/> **Internet**. Representa o gateway de Internet padrão Olá fornecido pelo Olá infraestrutura do Azure. <br/> **Dispositivo Virtual**. Representa um dispositivo virtual que você adicionou tooyour rede virtual do Azure. <br/> **Nenhum**. Representa um buraco negro. Pacotes encaminhados de buraco negro tooa não serão encaminhados em todos os. |Considere o uso de **dispositivo Virtual** toodirect tooa VM ou o balanceador de carga do Azure endereço IP interno de tráfego.  Esse tipo permite a especificação de saudação de um endereço IP, conforme descrito abaixo. Considere o uso de um **nenhum** digite pacotes toostop tooa fluxo fornecido de destino. |
| Endereço do próximo salto |próximo endereço de salto Olá contém o endereço IP de saudação pacotes devem ser encaminhados. Valores do próximo salto somente são permitidos em rotas onde é o tipo de próximo salto Olá *dispositivo Virtual*. |Deve ser um endereço IP que é acessível em Olá rede Virtual onde Olá rota definida pelo usuário é aplicada, sem passar por um **Gateway de rede Virtual**. endereço IP Hello tem toobe Olá mesmo Virtual de rede quando ela é aplicada, ou em uma rede Virtual peered. |Se o endereço IP hello representa uma máquina virtual, certifique-se de habilitar [encaminhamento IP](#IP-forwarding) no Azure para Olá VM. Se hello IP endereço representa Olá endereço IP interno do balanceador de carga do Azure, verifique se você tem uma regra para cada porta de balanceamento de carga correspondente você deseja balancear tooload.|

No Azure PowerShell alguns dos valores de "NextHopType" hello têm nomes diferentes:

* A Rede Virtual é VnetLocal
* O Gateway de Rede Virtual é VirtualNetworkGateway
* O Dispositivo Virtual é VirtualAppliance
* A Internet é Internet
* Nenhum é None

### <a name="system-routes"></a>Rotas do sistema
Cada sub-rede criada em uma rede virtual é associado automaticamente uma tabela de rota que contém Olá regras de rota do sistema a seguir:

* **Regra de VNet local**: essa regra é criada automaticamente para todas as sub-redes em uma rede virtual. Especifica que há um link direto entre VMs Olá no hello rede virtual e não não próximo salto intermediário.
* **Regra local**: esta regra aplica-se o intervalo de endereços do tooall o tráfego destinado toohello local e usa o gateway VPN como destino do hello próximo salto.
* **Regra de Internet**: essa regra trata todos os toohello de tráfego destinado Internet pública (prefixo de endereço 0.0.0.0/0) e o gateway de internet de infraestrutura usa hello como saudação do próximo salto para todo o tráfego destinado toohello da Internet.

### <a name="user-defined-routes"></a>Rotas definidas pelo usuário
Para a maioria dos ambientes, precisará apenas rotas de sistema Olá já definidas pelo Azure. No entanto, você pode precisar toocreate uma tabela de rota e adicione uma ou mais rotas em casos específicos, como:

* Força toohello encapsulamento da Internet por meio de sua rede local.
* Uso de dispositivos virtuais em seu ambiente do Azure.

Em cenários de saudação acima, será necessário toocreate uma tabela de rota e adicionar tooit de rotas definidas pelo usuário. Você pode ter várias tabelas de rota e hello mesma tabela de rota pode ser associado tooone ou mais sub-redes. E cada sub-rede só pode ser a tabela de rota único tooa associado. Todas as VMs e serviços de nuvem em uma sub-rede usam Olá rota tabela associada toothat sub-rede.

Sub-redes dependem de rotas do sistema até que uma tabela de rotas é sub-rede toohello associado. Quando existe uma associação, o roteamento é feito com base em LPM (Correspondência de Prefixo mais Longo) entre as rotas definidas pelo usuário e as rotas de sistema. Se houver mais de uma rota com hello LPM mesmo corresponde então uma rota é selecionada com base em sua origem no hello ordem a seguir:

1. Rota definida pelo usuário
2. Rota BGP (quando o ExpressRoute é usado)
3. Rota de sistema

toolearn como usuário toocreate definidos rotas, consulte [como tooCreate rotas e habilitar o encaminhamento de IP no Azure](virtual-network-create-udr-arm-template.md).

> [!IMPORTANT]
> Rotas definidas pelo usuário são apenas aplicado tooAzure VMs e serviços em nuvem. Por exemplo, se você quiser tooadd um dispositivo virtual firewall entre sua rede local e o Azure, você terá toocreate uma rota definida pelo usuário para as tabelas de rota do Azure que encaminha todo o tráfego direcionado toohello de espaço de endereço de local toohello virtual dispositivo. Você também pode adicionar que um usuário definido rota (UDR) toohello GatewaySubnet tooforward todo o tráfego de tooAzure local por meio do dispositivo virtual hello. Isso é uma adição recente.
> 
> 

### <a name="bgp-routes"></a>Rotas BGP
Se você tiver uma conexão de rota expressa entre sua rede local e o Azure, você pode habilitar as rotas BGP toopropagate na sua tooAzure de rede local. Essas rotas BGP são usadas em Olá mesma forma que as rotas de sistema e usuário definidas rotas em cada sub-rede do Azure. Para obter mais informações, consulte [Introdução ao ExpressRoute](../expressroute/expressroute-introduction.md).

> [!IMPORTANT]
> Você pode configurar sua força de toouse do ambiente do Azure túnel por meio de sua rede local, criando uma rota definida pelo usuário para a sub-rede 0.0.0.0/0 que utiliza o gateway VPN hello como Olá próximo nó. No entanto, isso só funcionará se você estiver usando um gateway de VPN, não o ExpressRoute. Para o ExpressRoute, o túnel à força é configurado por meio do BGP.
> 
> 

## <a name="ip-forwarding"></a>Encaminhamento IP
Conforme descrito acima, uma saudação motivos principais pelos quais toocreate uma rota definida pelo usuário é dispositivo virtual do tooa tooforward tráfego. Um dispositivo virtual é nada mais que uma VM que executa um tráfego de rede do aplicativo usado toohandle de alguma forma, como um firewall ou um dispositivo NAT.

Este dispositivo virtual que VM deve ser capaz de tooreceive tráfego de entrada que é não resolvidos tooitself. tooallow um tráfego de tooreceive VM endereçado tooother destinos, você deve habilitar o encaminhamento IP para Olá VM. Este é um Azure configuração, não é uma configuração no sistema de operacional convidado hello.

## <a name="next-steps"></a>Próximas etapas
* Saiba como muito[criar rotas no modelo de implantação do Gerenciador de recursos de saudação](virtual-network-create-udr-arm-template.md) e associá-los toosubnets. 
* Saiba como muito[criar rotas no modelo de implantação clássico Olá](virtual-network-create-udr-classic-ps.md) e associá-los toosubnets.

