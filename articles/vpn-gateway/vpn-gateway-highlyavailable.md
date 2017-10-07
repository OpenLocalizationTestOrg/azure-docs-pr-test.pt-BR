---
title: "aaaOverview de configurações de alta disponibilidade com Gateways de VPN do Azure | Microsoft Docs"
description: "Este artigo fornece uma visão geral das opções de configuração de alta disponibilidade usando os Gateways de VPN do Azure."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: a8bfc955-de49-4172-95ac-5257e262d7ea
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/24/2016
ms.author: yushwang
ms.openlocfilehash: 316293b9ac79645bf9bb9e89fbc4aa8f3eacd209
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="highly-available-cross-premises-and-vnet-to-vnet-connectivity"></a>Conectividade Altamente Disponível entre os Locais e VNet com VNet
Este artigo fornece uma visão geral das opções de configuração Altamente Disponível para sua conectividade entre os locais e VNet com VNet usando os gateways de VPN.

## <a name = "activestandby"></a>Sobre a redundância do gateway de VPN do Azure
Cada gateway de VPN do Azure consiste em duas instâncias em uma configuração ativa e em espera. Para qualquer manutenção planejada ou não planejado de interrupção que ocorre em instância ativa do toohello, instância em espera Olá seria assumir (failover) automaticamente e retomar Olá VPN S2S ou conexões de rede virtual a rede. Alterar Olá fará com que uma breve interrupção. Manutenção planejada, conectividade de saudação deve ser restaurada em 10 segundos too15. Para problemas não planejados, recuperação de conexão Olá será mais longa, sobre too1 minuto 1 e meia minutos no pior caso de saudação. Para o gateway de toohello de conexões de cliente VPN P2S, conexões de P2S hello serão desconectados e usuários Olá precisará tooreconnect de máquinas de clientes de saudação.

![Ativa/Em Espera](./media/vpn-gateway-highlyavailable/active-standby.png)

## <a name="highly-available-cross-premises-connectivity"></a>Conectividade Altamente Disponível entre os Locais
tooprovide melhor disponibilidade para seu cruzada local conexões, há duas opções disponíveis:

* Vários dispositivos VPN locais
* Gateway de VPN do Azure ativo
* Combinação dos dois

### <a name = "activeactiveonprem"></a>Vários dispositivos VPN locais
Você pode usar vários dispositivos VPN do gateway VPN do Azure local rede tooconnect tooyour, conforme mostrado no diagrama a seguir de saudação:

![Vários VPNs Locais](./media/vpn-gateway-highlyavailable/multiple-onprem-vpns.png)

Essa configuração fornece vários túneis ativos de saudação mesmo Azure gateway tooyour local dispositivos VPN em Olá mesmo local. Há alguns requisitos e restrições:

1. É necessário toocreate várias conexões VPN S2S do seu tooAzure de dispositivos VPN. Quando você se conectar vários dispositivos VPN Olá mesmo local de rede tooAzure, é necessário toocreate um gateway de rede local para cada dispositivo VPN e uma conexão de seu gateway de rede local do toohello de gateway VPN do Azure.
2. gateways de rede local Olá correspondente tooyour dispositivos VPN devem ter endereços IP públicos exclusivos no hello "GatewayIpAddress" propriedade.
3. O BGP é necessário para esta configuração. Cada gateway de rede local que representa um dispositivo VPN deve ter um endereço IP de par BGP exclusivo especificado na propriedade de "BgpPeerIpAddress" hello.
4. campo de propriedade Olá AddressPrefix em cada gateway de rede local não deve se sobrepor. Você deverá especificar hello "BgpPeerIpAddress" /32 formato CIDR no campo de AddressPrefix hello, por exemplo, 10.200.200.254/32.
5. Você deve usar o BGP tooadvertise Olá prefixos mesmo gateway de VPN do Azure tooyour prefixos de rede do mesmo local de saudação e tráfego hello será encaminhado por esses túneis simultaneamente.
6. Cada conexão é contado em número máximo de saudação de túneis para o gateway de VPN do Azure, 10 para Basic e Standard SKUs e 30 HighPerformance SKU. 

Nessa configuração, gateway de VPN do Azure Olá ainda está em modo de espera ativa, Olá assim mesmo comportamento de failover e breves interrupções ainda ocorrerá conforme descrito [acima](#activestandby). Mas essa configuração protege contra falhas ou interrupções na rede local e nos dispositivos VPN.

### <a name="active-active-azure-vpn-gateway"></a>Gateway de VPN do Azure ativo
Agora você pode criar um gateway de VPN do Azure em uma configuração ativo-ativo, onde ambas as instâncias de gateway Olá que VMs estabelecerá que túneis de VPN S2S tooyour dispositivo VPN local, como Olá mostrado a seguir diagrama:

![Ativo-ativo](./media/vpn-gateway-highlyavailable/active-active.png)

Nessa configuração, cada instância de gateway do Azure terá um endereço IP público exclusivo e cada estabelecerá um IPsec/IKE S2S VPN túnel tooyour no dispositivo VPN local especificado no seu gateway de rede local e a conexão. Observe que os dois encapsulamentos VPN são, na verdade, parte da saudação mesma conexão. Você ainda será necessário tooconfigure seu tooaccept de dispositivo VPN local ou estabelecer duas VPN S2S túneis toothose dois VPN do Azure gateway endereços IP públicos.

Como são instâncias de gateway do Azure Olá na configuração ativa-ativa, tráfego de saudação do tooyour sua rede virtual do Azure local rede será roteada por ambos os túneis simultaneamente, mesmo se o dispositivo VPN local pode favorecer um túnel sobre Olá outros. Observe que Olá mesmo fluxo TCP ou UDP sempre percorrerá Olá mesmo caminho ou túnel, a menos que um evento de manutenção acontece em uma das instâncias de saudação.

Quando um evento não planejado ou manutenção planejada acontece tooone instância de gateway, túnel IPsec de saudação do tooyour instância local do dispositivo VPN será desconectado. Olá rotas correspondentes em seus dispositivos VPN devem ser removidas ou retiradas automaticamente para que o tráfego de saudação será alternado pela toohello outros túnel IPsec ativo. Em Olá do lado do Azure, comutador hello sobre ocorrerá automaticamente da saudação afetada toohello active instância.

### <a name="dual-redundancy-active-active-vpn-gateways-for-both-azure-and-on-premises-networks"></a>Dupla redundância: gateways VPN ativos para redes locais e do Azure
opção mais confiável de saudação é gateways de ativo-ativo Olá toocombine na sua rede e o Azure, conforme mostrado no diagrama de saudação abaixo.

![Dupla Redundância](./media/vpn-gateway-highlyavailable/dual-redundancy.png)

Aqui você cria e configurar o gateway de VPN do Azure Olá em uma configuração ativo-ativo e cria dois gateways de rede local e duas conexões para seus dois locais dispositivos VPN conforme descrito acima. resultado de saudação é uma conectividade de malha completa de 4 túneis IPsec entre sua rede virtual do Azure e sua rede local.

Todos os gateways e túneis estão ativos de saudação do lado do Azure, para que o tráfego de saudação distribuídos entre todos os 4 túneis simultaneamente, embora cada TCP ou UDP de fluxo será novamente siga Olá túnel mesmo ou Olá de caminho do lado do Azure. Embora distribuindo tráfego hello, você poderá ver um pouco melhor taxa de transferência por túneis do IPsec hello, Olá principal objetivo dessa configuração é para alta disponibilidade. E devido toohello natureza estatística de propagação de Olá, é difícil tooprovide Olá medida no tráfego de aplicativo diferentes condições afetam a taxa de transferência agregada hello.

Essa topologia exigirá dois gateways de rede local e o par de saudação toosupport duas conexões de dispositivos VPN no local e o BGP é necessário tooallow Olá duas conexões toohello mesma rede local. Esses requisitos são Olá mesmo como Olá [acima](#activeactiveonprem). 

## <a name="highly-available-vnet-to-vnet-connectivity-through-azure-vpn-gateways"></a>Conectividade de VNet com VNet de Alta Disponibilidade através de Gateways VPN do Azure
Olá mesma configuração ativo-ativo também pode aplicar tooAzure conexões de rede virtual a rede. Você pode criar gateways VPN ativa para ambas as redes virtuais e conectá-los juntos tooform Olá mesmo completa de malha conectividade de 4 túneis entre hello dois VNets, conforme mostrado no hello diagrama abaixo:

![VNet a VNet](./media/vpn-gateway-highlyavailable/vnet-to-vnet.png)

Isso garante que sempre há um par de túneis entre duas redes virtuais Olá para qualquer evento de manutenção planejada, mantendo a disponibilidade ainda melhor. Embora hello mesma topologia para conectividade entre locais requer duas conexões, topologia de rede virtual a rede Olá mostrada acima será necessário somente uma conexão para cada gateway. Além disso, o BGP é opcional, a menos que o roteamento de tráfego em Olá conexão de rede virtual a rede é necessário.

## <a name="next-steps"></a>Próximas etapas
Consulte [Gateways de VPN configuração ativa-ativa para conexões de rede virtual a rede e entre locais](vpn-gateway-activeactive-rm-powershell.md) para conexões de rede virtual a rede e etapas tooconfigure ativo-ativo entre locais.

