---
title: "Planejamento e design de conexões entre locais: Gateway de VPN do Azure | Microsoft Docs"
description: "Saiba mais sobre o planejamento e design de Gateway de VPN para conexões entre locais, híbridas e VNet a VNet"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: d5aaab83-4e74-4484-8bf0-cc465811e757
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/27/2017
ms.author: cherylmc
ms.openlocfilehash: 3d4587ba31d163384212eca88a7e2c0ba8f3b21f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="planning-and-design-for-vpn-gateway"></a>Planejamento e design para o Gateway de VPN

Planejar e projetar suas conexões entre redes virtuais e entre locais pode ser simples ou complicado, dependendo das suas necessidades de rede. Este artigo traz considerações básicas de design e planejamento.

## <a name="planning"></a>Planejamento

### <a name="compare"></a>Opções de conectividade entre locais

Se você quiser tooconnect local sites com segurança de rede virtual tooa, assim que toodo de três maneiras diferentes: Site a Site, ponto a Site e ExpressRoute. Compare as conexões entre locais diferentes Olá disponíveis. opção de saudação pode depender de várias considerações, como:

* Que tipo de taxa de transferência sua solução exige?
* Você deseja toocommunicate sobre Olá Internet pública, por meio de VPN segura, ou em uma conexão privada?
* Você tem um público toouse disponível de endereço IP?
* Você está planejando toouse um dispositivo VPN? Nesse caso, é compatível?
* Você está conectando apenas alguns computadores ou deseja ter uma conexão persistente para o seu site?
* O tipo de gateway VPN é necessário para a solução de saudação deseja toocreate?
* Qual SKU de gateway você deve usar?

### <a name="planningtable"></a>Tabela de planejamento

Olá a tabela a seguir pode ajudá-lo a decidir hello, a melhor opção de conectividade para sua solução.

[!INCLUDE [vpn-gateway-cross-premises](../../includes/vpn-gateway-cross-premises-include.md)]

### <a name="gwsku"></a>SKUs do Gateway

[!INCLUDE [vpn-gateway-table-gwtype-aggtput](../../includes/vpn-gateway-table-gwtype-aggtput-include.md)]

### <a name="wf"></a>Fluxo de trabalho

Olá lista a seguir descreve Olá fluxo de trabalho comuns de conectividade de nuvem:

1. Design e o plano de que seu endereço de saudação conectividade topologia e lista de espaços para todas as redes deseja tooconnect.
2. Crie uma rede virtual do Azure. 
3. Crie um gateway VPN para rede virtual hello.
4. Criar e configurar redes de tooon locais de conexões ou outras redes virtuais (conforme necessário).
5. Crie e configure uma conexão Ponto a Site para o gateway de VPN do Azure (conforme necessário).

## <a name="design"></a>Design
### <a name="topologies"></a>Topologias de conexão

Iniciar examinando diagramas Olá Olá [sobre o Gateway de VPN](vpn-gateway-about-vpngateways.md) artigo. artigo Olá contém diagramas básicos, modelos de implantação de saudação para cada topologia, Olá disponíveis ferramentas de implantação e você pode usar toodeploy sua configuração.

### <a name="designbasics"></a>Noções básicas sobre design

Olá seções a seguir discutem Noções básicas sobre o gateway VPN hello. 

#### <a name="servicelimits"></a>Limites dos serviços de rede

Percorra Olá tabelas tooview [limites de serviços de rede para](../azure-subscription-service-limits.md#networking-limits). limites de saudação listados podem afetar seu design.

#### <a name="subnets"></a>Sobre sub-redes

Quando estiver criando conexões, você precisa considerar os intervalos de sub-rede. Não pode haver sobreposição dos intervalos de endereço de sub-rede. Uma sub-rede sobreposta é quando um local de rede ou local virtual contém Olá contém mesmo espaço de endereço que Olá outro local. Isso significa que você precisa seus engenheiros de rede para sua toocarve de redes locais local um intervalo para você toouse para o IP do Azure/sub-redes de espaço de endereçamento. É necessário espaço de endereço que não está sendo usado na rede do local no local de saudação.

Também é importante evitar a sobreposição de sub-redes quando você estiver trabalhando com conexões VNet a VNet. Se a sobreposição de suas sub-redes e um endereço IP existe na enviando hello e o destino VNets, conexões de rede virtual a rede falharem. Azure não pode rotear Olá dados toohello outra VNet como endereço de destino Olá faz parte do hello envio de rede virtual.

Os Gateways de VPN precisam de uma sub-rede específica, chamada sub-rede de gateway. Todas as sub-redes de gateway devem ser nomeadas GatewaySubnet toowork corretamente. Verifique se não tooname sua sub-rede de gateway outro nome e não implantar VMs ou qualquer outra transação sub-rede de gateway toohello. Consulte [Sub-redes de gateway](vpn-gateway-about-vpn-gateway-settings.md#gwsub).

#### <a name="local"></a>Sobre gateways de rede local

Normalmente, o gateway de rede local Olá refere-se tooyour no local. No modelo de implantação clássico hello, gateway de rede local Olá é chamado tooas um Site de rede Local. Quando você configurar um gateway de rede local, dê a ele um nome, especifique o endereço IP público de saudação do dispositivo VPN local hello e especificar prefixos de endereço de saudação que estejam no local de local de saudação. Azure examina os prefixos de endereço de destino Olá para o tráfego de rede, consulta configuração Olá que você especificou para o gateway de rede local hello e encaminha pacotes adequadamente. Você pode modificar os prefixos de endereço Olá conforme necessário. Para saber mais, confira [Gateways de rede local](vpn-gateway-about-vpn-gateway-settings.md#lng).

#### <a name="gwtype"></a>Sobre tipos de gateway

Selecionar tipo de gateway correto Olá para a sua topologia é crítico. Se você selecionar o tipo errado Olá, o gateway não funcionará corretamente. tipo de gateway Olá Especifica como o próprio gateway Olá se conecta e é uma configuração necessária para o modelo de implantação do Gerenciador de recursos de saudação.

tipos de gateway Olá são:

* Vpn
* ExpressRoute

#### <a name="connectiontype"></a>Sobre tipos de conexão

Cada configuração exige um tipo específico de conexão. tipos de conexão de saudação são:

* IPsec
* Vnet2Vnet
* ExpressRoute
* VPNClient

#### <a name="vpntype"></a>Sobre tipos de VPN

Cada configuração requer um tipo específico de VPN. Se você estiver combinando duas configurações, como a criação de uma conexão Site a Site e um toohello de conexão de ponto para Site mesma rede virtual, você deve usar um tipo VPN que atenda a ambos os requisitos de conexão.

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

Olá tabelas a seguir mostram o tipo de VPN hello como ele mapeia tooeach configuração de conexão. Verifique Olá-se de que tipo VPN para a sua configuração de saudação do gateway correspondências que você deseja toocreate. 

[!INCLUDE [vpn-gateway-table-vpntype](../../includes/vpn-gateway-table-vpntype-include.md)]

### <a name="devices"></a>Dispositivos de VPN e conexões Site a Site

conexão tooconfigure uma Site a Site, independentemente do modelo de implantação, você precisa Olá itens a seguir:

* Um dispositivo VPN que é compatível com os gateways de VPN do Azure
* Um endereço IP IPv4 público que não está protegido por um NAT

Você precisa de experiência toohave configurar seu dispositivo VPN ou que alguém que possa configurar dispositivo Olá para você.

[!INCLUDE [vpn-gateway-configure-vpn-device-rm](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

### <a name="forcedtunnel"></a>Considere a possibilidade de roteamento de túnel forçado

Para a maioria das configurações, é possível configurar o túnel forçado. Forçado permite redirecionar ou "forçar" todos os direcionado à Internet tráfego tooyour back local através de um túnel VPN Site a Site para inspeção e auditoria de túnel. Esse é um requisito crítico de segurança para a maioria das políticas de TI empresariais. 

Sem o túnel forçado, o tráfego direcionado à Internet de suas VMs no Azure sempre percorrerá da infraestrutura de rede do Azure diretamente out toohello Internet, sem Olá opção tooallow você tráfego de saudação tooinspect ou auditoria. Acesso não autorizado pode levar a divulgação de tooinformation ou outros tipos de violações de segurança.

Uma conexão de túnel forçado pode ser configurada em ambos os modelos de implantação e usando ferramentas diferentes. Para obter mais informações, consulte [Configurar o túnel forçado](vpn-gateway-forced-tunneling-rm.md).

**Diagrama do túnel forçado**

![Diagrama de túnel forçado do Gateway de VPN do Azure](./media/vpn-gateway-plan-design/forced-tunneling-diagram.png)

## <a name="next-steps"></a>Próximas etapas

Consulte Olá [perguntas frequentes sobre o Gateway de VPN](vpn-gateway-vpn-faq.md) e [sobre o Gateway de VPN](vpn-gateway-about-vpngateways.md) artigos para mais toohelp de informações você com seu design.

Para obter mais informações sobre configurações de gateway específicas, consulte [Sobre as configurações de Gateway de VPN](vpn-gateway-about-vpn-gateway-settings.md).