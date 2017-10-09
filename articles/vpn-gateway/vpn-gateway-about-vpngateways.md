---
title: "Visão geral de Gateway VPN: Criar conexões de VPN entre locais de redes virtuais tooAzure | Microsoft Docs"
description: "Esta visão geral Gateway de VPN explica Olá maneiras tooconnect tooAzure redes virtuais usando uma conexão VPN sobre Olá da Internet. Diagramas de configurações de conexão básica estão incluídos."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 2358dd5a-cd76-42c3-baf3-2f35aadc64c8
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/05/2017
ms.author: cherylmc
ms.openlocfilehash: 899270734270632a5b12d56021c924e977725a7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="about-vpn-gateway"></a>Sobre o Gateway de VPN

Um gateway de VPN é um tipo de gateway de rede virtual que envia o tráfego criptografado em uma conexão pública tooan local. Você também pode usar o tráfego de toosend criptografado de gateways VPN entre redes virtuais do Azure pela rede da Microsoft hello. toosend criptografado o tráfego de rede entre sua rede virtual do Azure e seu site local, você deve criar um gateway de VPN para sua rede virtual.

Cada rede virtual pode ter apenas um gateway VPN, no entanto, você pode criar várias toohello de conexões mesmo gateway VPN. Um exemplo disso é uma configuração de conexão de vários sites. Quando você cria várias toohello de conexões mesmo gateway VPN, todos os túneis VPN, incluindo VPNs ponto a Site, compartilhamento Olá largura de banda disponível para o gateway de saudação.

### <a name="whatis"></a>O que é um gateway da rede virtual?

Um gateway de rede virtual é composto de dois ou mais máquinas virtuais que são implantados sub-rede específica de tooa chamado hello GatewaySubnet. Olá VMs que estão localizados em Olá GatewaySubnet são criados quando você criar o gateway de rede virtual hello. VMs de gateway de rede virtual são tabelas de roteamento configurado toocontain e gateway de toohello específicas de serviços. Não seja possível configurar Olá VMs que fazem parte do gateway de rede virtual hello e você nunca deve implantar recursos adicionais toohello GatewaySubnet.

Quando você criar um gateway de rede virtual usando o tipo de gateway Olá 'Vpn', ele cria um tipo específico de gateway de rede virtual que criptografa o tráfego; um gateway VPN. Um gateway de VPN pode demorar até too45 toocreate de minutos. Isso ocorre porque Olá VMs de gateway VPN Olá estão sendo implantado toohello GatewaySubnet e configurado com configurações de saudação que você especificou. Olá SKU de Gateway que você seleciona determina Olá avançado como VMs são.

## <a name="gwsku"></a>SKUs do Gateway

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

## <a name="configuring"></a>Configurando um Gateway de VPN

Uma conexão de gateway VPN conta com vários recursos que são configurados com definições específicas. A maioria dos recursos de saudação pode ser configurada separadamente, embora eles devem ser configurados em uma determinada ordem, em alguns casos.

### <a name="settings"></a>Configurações

configurações de saudação que você escolheu para cada recurso são crítico toocreating uma conexão bem-sucedida. Para obter informações sobre os recursos individuais e as configurações do Gateway de VPN, consulte [Sobre as configurações do Gateway de VPN](vpn-gateway-about-vpn-gateway-settings.md). artigo Olá contém informações toohelp entender os tipos de gateway, tipos de VPN, tipos de conexão, sub-redes de gateway, gateways de rede local e várias outras configurações de recursos que podem ser tooconsider.

### <a name="tools"></a>Ferramentas de implantação

Você pode começar a criar e configurar recursos usando uma ferramenta de configuração, como Olá portal do Azure. Posteriormente, você pode decidir tooswitch tooanother ferramenta, como o PowerShell, tooconfigure obter recursos adicionais, ou modificar recursos existentes, quando aplicável. No momento, você não pode configurar cada recurso e a configuração de recurso no hello portal do Azure. instruções de saudação nos artigos Olá para cada topologia de conexão especifiquem quando uma ferramenta de configuração específica é necessária. 

### <a name="models"></a>Modelo de implantação

Quando você configura um gateway de VPN, etapas Olá executadas dependem Olá implantação modelo usado toocreate sua rede virtual. Por exemplo, se você criou sua rede virtual usando o modelo de implantação clássico Olá, use as diretrizes de saudação e instruções para implantação clássica Olá toocreate de modelo e configurar suas configurações de gateway VPN. Para obter mais informações sobre os modelos de implantação, consulte [Noções básicas sobre o Resource Manager e os modelos de implantação clássicos](../azure-resource-manager/resource-manager-deployment-model.md).

## <a name="diagrams"></a>Diagramas de topologia de conexão

É importante tooknow que configurações diferentes estão disponíveis para conexões de gateway VPN. É necessário toodetermine qual configuração que melhor atenda às suas necessidades. Nas seções de saudação abaixo, você pode exibir diagramas de topologia e informações sobre Olá conexões VPN de gateway a seguir: Olá seções a seguir contêm tabelas que listam:

* Modelo de implantação disponível
* Ferramentas de configuração disponíveis
* Links que levam diretamente tooan artigo, se disponível

Use Olá descrições e diagramas toohelp Olá selecione conexão topologia toomatch seus requisitos. Olá diagramas mostram Olá topologias de linha de base principal, mas é possível toobuild configurações mais complexas usando diagramas de saudação como uma diretriz.

## <a name="s2smulti"></a>Site a Site e Vários Sites (túnel VPN IPsec/IKE)

### <a name="S2S"></a>Site a site

Uma conexão de gateway VPN Site a Site (S2S) é uma conexão por túnel VPN IPsec/IKE (IKEv1 ou IKEv2). Uma conexão S2S requer uma VPN de dispositivos localizado localmente que tem um tooit de endereço atribuído de IP público e não estiver localizado atrás de um NAT. As conexões S2S podem ser usadas para configurações entre instalações e híbridas.   

![Exemplo de conexão Site a Site do Gateway de VPN do Azure](./media/vpn-gateway-about-vpngateways/vpngateway-site-to-site-connection-diagram.png)

### <a name="Multi"></a>Vários Sites

Esse tipo de conexão é uma variação de hello conexão Site a Site. Criar mais de uma conexão de VPN do gateway de rede virtual, conectar normalmente toomultiple sites locais. Ao trabalhar com várias conexões, você deve usar um tipo de VPN baseado em rota (conhecido como gateway dinâmico ao trabalhar com redes virtuais clássicas). Como cada rede virtual pode ter um gateway VPN, todas as conexões por meio do gateway de saudação compartilham largura de banda disponível hello. Isso é geralmente chamado de conexão com "vários sites".

![Exemplo de conexão Multissite do Gateway de VPN do Azure](./media/vpn-gateway-about-vpngateways/vpngateway-multisite-connection-diagram.png)

### <a name="deployment-models-and-methods-for-site-to-site-and-multi-site"></a>Modelos de implantação e métodos para Site a Site e Vários Sites

[!INCLUDE [vpn-gateway-table-site-to-site](../../includes/vpn-gateway-table-site-to-site-include.md)]

## <a name="P2S"></a>Ponto a Site (VPN sobre SSTP)

Um gateway VPN ponto a Site (P2S) permite criar uma rede virtual de tooyour de conexão segura de um computador cliente individual. Conexões VPN Site a ponto são úteis quando você deseja tooconnect tooyour VNet de um local remoto, como quando você está comunicando em casa ou em uma conferência. Uma VPN de P2S também é toouse uma solução útil em vez de uma VPN Site a Site quando você tiver apenas alguns clientes que precisam de tooconnect tooa VNet. 

Ao contrário das conexões S2S, as conexões P2S não exigem um endereço IP público local ou um dispositivo VPN. Conexões de P2S podem ser usadas com S2S conexões por meio de Olá mesmo gateway VPN, desde que todos os requisitos de configuração de Olá para ambas as conexões são compatíveis.

Usa P2S Olá SSTP Secure Socket Tunneling Protocol (), que é um protocolo VPN baseada em SSL. Uma conexão VPN de P2S é estabelecido pela iniciá-lo do computador do cliente de saudação.

![Exemplo de conexão Ponto de Site do Gateway de VPN do Azure](./media/vpn-gateway-about-vpngateways/vpngateway-point-to-site-connection-diagram.png)

### <a name="deployment-models-and-methods-for-point-to-site"></a>Modelos de implantação e métodos para Ponto a Site

[!INCLUDE [vpn-gateway-table-point-to-site](../../includes/vpn-gateway-table-point-to-site-include.md)]

## <a name="V2V"></a>Conexões de VNet para VNet (túnel VPN IPsec/IKE)

Conectar uma rede virtual tooanother VPN (rede virtual a rede) é semelhante tooconnecting uma VNet tooan no site local. Ambos os tipos de conectividade usam um gateway VPN tooprovide um túnel seguro usando IPsec/IKE. Você pode até combinar a comunicação VNet a VNet com as configurações de conexão de vários sites. Isso permite estabelecer topologias de rede que combinam conectividade entre instalações a conectividade de rede intervirtual.

Olá VNets que você se conectar pode ser:

* em Olá mesmas ou em diferentes regiões
* em Olá iguais ou diferentes assinaturas 
* em Olá modelos de implantação igual ou diferente

![Exemplo de conexão de tooVNet de rede virtual de Gateway de VPN do Azure](./media/vpn-gateway-about-vpngateways/vpngateway-vnet-to-vnet-connection-diagram.png)

### <a name="connections-between-deployment-models"></a>Conexões entre os modelos de implantação

Atualmente, o Azure tem dois modelos de implantação: o clássico e o Resource Manager. Se você já usa o Azure há algum tempo, provavelmente terá as VMs do Azure e as funções de instância em execução em uma Rede Virtual clássica. Suas VMs e instâncias de função mais recentes podem estar em execução em uma Rede Virtual criada no Resource Manager. Você pode criar uma conexão entre Olá VNets tooallow recursos Olá toocommunicate de uma rede virtual diretamente com os recursos em outro.

### <a name="vnet-peering"></a>Emparelhamento VNet

Você pode ser capaz de toouse emparelhamento toocreate sua conexão de rede virtual como sua rede virtual atende a certos requisitos. O emparelhamento de Rede Virtual não usa um gateway de rede virtual. Para obter mais informações, consulte [Emparelhamento da VNet](../virtual-network/virtual-network-peering-overview.md).

### <a name="deployment-models-and-methods-for-vnet-to-vnet"></a>Modelos de implantação e métodos para VNet a VNet

[!INCLUDE [vpn-gateway-table-vnet-to-vnet](../../includes/vpn-gateway-table-vnet-to-vnet-include.md)]

## <a name="ExpressRoute"></a>ExpressRoute (conexão privada dedicada)

O Microsoft Azure ExpressRoute permite estender suas redes locais no hello nuvem da Microsoft em uma conexão privada dedicada facilitada por um provedor de conectividade. Com o ExpressRoute, você pode estabelecer serviços de nuvem de tooMicrosoft de conexões, como o Microsoft Azure, Office 365 e CRM Online. A conectividade pode ocorrer de uma rede “qualquer para qualquer” (VPN IP), uma rede Ethernet ponto a ponto ou uma conexão cruzada virtual por meio de um provedor de conectividade em uma colocalização.

Conexões de rota expressa não passam pela Olá Internet pública. Isso permite toooffer de conexões de rota expressa mais confiabilidade, velocidades mais rápidas, latências menores e maior segurança que as conexões típicas pela Internet da saudação.

Uma conexão ExpressRoute não usa um gateway de VPN, embora ela use um gateway de rede virtual como parte de sua configuração necessária. Em uma conexão de rota expressa, o gateway de rede virtual Olá é configurado com o tipo de gateway Olá 'Rota expressa', em vez de 'Vpn'. Para obter mais informações sobre a rota expressa, consulte Olá [visão geral técnica do ExpressRoute](../expressroute/expressroute-introduction.md).

## <a name="coexisting"></a>Conexões coexistentes Site a Site e de ExpressRoute

Rota expressa é uma conexão direta, dedicada de sua WAN (não por Olá Internet pública) tooMicrosoft serviços, incluindo o Azure. Tráfego de VPN site a Site viajam criptografadas Olá Internet pública. Sendo tooconfigure capaz de conexões VPN Site a Site e ExpressRoute para a mesma rede virtual hello tem várias vantagens.

Você pode configurar uma VPN Site a Site como um caminho de failover segura para o ExpressRoute ou usar VPNs Site a Site tooconnect toosites que não fazem parte de sua rede, mas que são conectados por meio de rota expressa. Observe que essa configuração requer dois gateways de rede virtual para Olá mesma rede virtual, um usando Olá 'Vpn' do tipo de gateway e Olá outros usando o tipo de gateway Olá 'ExpressRoute'.

![Exemplos de conexões coexistentes do ExpressRoute e do Gateway de VPN](./media/vpn-gateway-about-vpngateways/expressroute-vpngateway-coexisting-connections-diagram.png)

### <a name="deployment-models-and-methods-for-s2s-and-expressroute"></a>Modelos de implantação e métodos para S2S e ExpressRoute

[!INCLUDE [vpn-gateway-table-coexist](../../includes/vpn-gateway-table-coexist-include.md)]

## <a name="pricing"></a>Preços

[!INCLUDE [vpn-gateway-about-pricing-include](../../includes/vpn-gateway-about-pricing-include.md)]

Para saber mais sobre as SKUs de gateway para Gateway de VPN, veja [SKUs de Gateway](vpn-gateway-about-vpn-gateway-settings.md#gwsku).

## <a name="faq"></a>Perguntas frequentes

Para perguntas frequentes sobre o gateway de VPN, consulte Olá [perguntas frequentes sobre o Gateway de VPN](vpn-gateway-vpn-faq.md).

## <a name="next-steps"></a>Próximas etapas

- Planeje sua configuração de gateway VPN. Confira [Planejamento e design do Gateway de VPN](vpn-gateway-plan-design.md).
- Saudação de exibição [perguntas frequentes sobre o Gateway de VPN](vpn-gateway-vpn-faq.md) para obter informações adicionais.
- Saudação de exibição [assinatura e limites de serviço](../azure-subscription-service-limits.md#networking-limits).
- Saiba mais sobre alguns dos Olá outra chave [recursos de rede](../networking/networking-overview.md) do Azure.
