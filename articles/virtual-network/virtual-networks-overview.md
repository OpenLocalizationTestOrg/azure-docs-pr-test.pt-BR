---
title: aaaAzure rede Virtual | Microsoft Docs
description: Saiba mais sobre os conceitos e recursos da Rede Virtual do Azure.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 9633de4b-a867-4ddf-be3c-a332edf02e24
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/23/2017
ms.author: jdial
ms.openlocfilehash: 55ae6a131d882ad893aeffcaa4127bc47beda552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-network"></a>Rede Virtual do Azure

Olá ativa do serviço de rede Virtual do Azure toosecurely você se conectar a recursos do Azure tooeach outros com redes virtuais (VNets). Uma rede virtual é uma representação de sua própria rede na nuvem hello. Uma rede virtual é uma isolamento lógico de saudação nuvem do Azure dedicado tooyour assinatura. Você também pode se conectar a rede de local de tooyour VNets. Olá a imagem a seguir mostra alguns dos recursos de saudação do hello serviço de rede Virtual do Azure:

![Diagrama de rede](./media/virtual-networks-overview/virtual-network-overview.png)

toolearn mais sobre Olá seguindo os recursos de rede Virtual do Azure, clique em recurso hello:
- **[Isolamento:](#isolation)** as VNets são isoladas umas das outras. Você pode criar VNets separadas para o desenvolvimento, teste e produção Olá que use blocos de endereços CIDR mesmo. Por outro lado, você pode criar várias VNets que usam blocos de endereço CIDR diferentes e conectam as redes. Você pode segmentar uma VNet em várias sub-redes. O Azure fornece resolução de nome interno para VMs e instâncias de função de serviços de nuvem conectados tooa VNet. Opcionalmente, você pode configurar uma rede virtual toouse seus próprios servidores DNS, em vez de usar a resolução de nome interno do Azure.
- **[Conectividade com a Internet:](#internet)**  instâncias de função de todas as máquinas virtuais (VM) do Azure e serviços de nuvem tiver conectado tooa VNet acessam toohello da Internet, por padrão. Você também pode habilitar recursos de toospecific de acesso de entrada, conforme necessário.
- **[Conectividade de recursos do Azure:](#within-vnet)**  recursos do Azure, como serviços de nuvem e máquinas virtuais podem ser conectado toohello mesma rede virtual. recursos de saudação podem se conectar a outros tooeach usando privada endereços IP, mesmo que eles estejam em sub-redes diferentes. O Azure fornece o roteamento padrão entre sub-redes, VNets e redes locais, para que você não tem tooconfigure e gerencie rotas.
- **[Conectividade de rede virtual:](#connect-vnets)**  VNets pode ser conectado tooeach outras, permitindo que recursos conectado tooany VNet toocommunicate com qualquer recurso em qualquer outra VNet.
- **[Conectividade local:](#connect-on-premises)**  VNets podem ser redes locais tooon conectados por meio de conexões de rede privada entre sua rede e o Azure, ou uma conexão de VPN site a site over Olá da Internet.
- **[Filtragem de tráfego:](#filtering)** o tráfego de rede de instâncias de função de VMs e do Serviços de Nuvem pode ser filtrado na entrada e na saída pelo endereço IP e porta de origem, endereço IP e porta de destino e protocolo.
- **[Roteamento:](#routing)** opcionalmente, você pode substituir o roteamento padrão do Azure configurando suas próprias rotas ou usando rotas BGP por meio de um gateway de rede.

## <a name = "isolation"></a>Isolamento e segmentação de rede

É possível implementar várias VNets dentro de cada [assinatura](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) e [região](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#region) do Azure. Cada VNet é isolada de outras VNets. Para cada VNet, você pode:
- Especificar um espaço de endereço IP privado personalizado usando endereços públicos e privados (RFC 1918). Azure atribui recursos conectados toohello VNet um endereço IP privado de espaço de endereço Olá que você atribuir.
- Olá rede virtual em uma ou mais sub-redes de segmento e alocar uma parte da sub-rede de tooeach espaço do endereço de rede virtual hello.
- Usar a resolução de nomes fornecida pelo Azure ou especifique seu próprio servidor DNS para uso por recursos conectado tooa VNet. toolearn mais informações sobre resolução de nomes em VNets, ler Olá [resolução de nomes para VMs e serviços de nuvem](virtual-networks-name-resolution-for-vms-and-role-instances.md) artigo.

## <a name = "internet"></a>Conecte-se toohello da Internet
Todos os recursos tooa conectado VNet ter conectividade de saída toohello da Internet por padrão. endereço IP privado de saudação do recurso de saudação é o endereço de rede de origem convertido endereço IP público de tooa (SNAT) por Olá infraestrutura do Azure. toolearn mais sobre a conectividade da Internet de saída, ler Olá [Noções básicas sobre conexões de saída no Azure](..\load-balancer\load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json#standalone-vm-with-no-instance-level-public-ip-address) artigo. Você pode alterar a conectividade do saudação padrão Implementando o roteamento personalizado e filtragem.

toocommunicate tooAzure recursos de saudação da Internet ou toocommunicate toohello saída Internet sem SNAT, um recurso deve ser atribuída um endereço IP público de entrada. toolearn mais informações sobre endereços IP públicos, ler Olá [endereços IP públicos](virtual-network-public-ip-address.md) artigo.

## <a name="within-vnet"></a>Conectar recursos do Azure
Você pode se conectar a vários recursos do Azure tooa VNet, como máquinas virtuais (VM), os serviços de nuvem, ambientes de serviço de aplicativo e conjuntos de escala de máquina Virtual. VMs se conectar a sub-rede tooa dentro de uma rede virtual por meio de uma interface de rede (NIC). toolearn mais sobre NICs, ler Olá [interfaces de rede](virtual-network-network-interface.md) artigo.

## <a name="connect-vnets"></a>Conectar redes virtuais

Você pode se conectar a VNets tooeach outras, permitindo que recursos conectados tooeither VNet toocommunicate uns com os outros em VNets. Você pode usar um ou ambos Olá opções tooconnect VNets tooeach outros a seguir:
- **Emparelhamento:** habilita recursos conectado toodifferent VNets do Azure em Olá mesmo toocommunicate local do Azure com o outro. Olá largura de banda e latência entre Olá VNets é Olá mesmo que recursos Olá toohello conectado mesma rede virtual. toolearn mais sobre o emparelhamento, ler Olá [emparelhamento de rede Virtual](virtual-network-peering-overview.md) artigo.
- **Conexão de rede virtual a rede:** habilita recursos conectado toodifferent VNet do Azure em Olá iguais ou diferentes locais do Azure. Ao contrário do emparelhamento, a largura de banda é limitada entre as VNets, pois o tráfego deve fluir por um Gateway de VPN do Azure. toolearn mais sobre como conectar VNets com uma conexão de rede virtual a rede, ler Olá [configurar uma conexão de rede virtual a rede](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artigo.

## <a name="connect-on-premises"></a>Conecte-se a rede de local de tooan

Você pode conectar seu tooa de rede local VNet usando qualquer combinação de saudação as opções a seguir:
- **Rede privada virtual (VPN) site a ponto:** estabelecido entre um único computador tooyour conectado rede Olá VNet. Esse tipo de conexão é ótimo se você estiver apenas começando com o Azure, ou para os desenvolvedores, porque ele requer pouca ou nenhuma alterações tooyour rede. conexão Olá usa a comunicação de tooprovide criptografado de protocolo SSTP Olá Olá Internet entre Olá PC e hello VNet. latência de saudação para uma VPN ponto a site é imprevisível, desde que o tráfego de saudação atravessa Olá Internet.
- **VPN site a site:** estabelecida entre o dispositivo VPN e um Gateway de VPN do Azure. Esse tipo de conexão permite que qualquer recurso local autorizar tooaccess uma rede virtual. conexão de saudação é uma VPN IPSec/IKE que fornece comunicação criptografada sobre Olá Internet entre o dispositivo local e o gateway de VPN do Azure hello. latência de saudação para uma conexão site a site é imprevisível, desde que o tráfego de saudação atravessa Olá Internet.
- **Azure ExpressRoute:** estabelecida entre sua rede e o Azure, por meio de um parceiro de ExpressRoute. Essa conexão é privada. O tráfego não atravessa Olá da Internet. latência de saudação para uma conexão de rota expressa é previsível, desde que o tráfego não atravessam a saudação da Internet.

toolearn mais informações sobre todos os Olá conexão opções anteriores, leia Olá [diagramas de topologia de Conexão](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#diagrams) artigo.

## <a name="filtering"></a>Filtrar o tráfego de rede
Você pode filtrar o tráfego de rede entre sub-redes usando um ou ambos Olá as opções a seguir:
- **Rede (NSG) de grupos de segurança:** cada NSG pode conter várias regras de segurança de entrada e saída que permitem que você toofilter tráfego por endereço IP de origem e de destino, porta e protocolo. Você pode aplicar um tooeach NSG NIC em uma VM. Você também pode aplicar uma sub-rede do NSG toohello uma NIC ou outros recursos do Azure, está conectado. toolearn mais sobre os NSGs, ler Olá [grupos de segurança de rede](virtual-networks-nsg.md) artigo.
- **NVA (Solução de virtualização de rede):** NVA um é uma VM que executa um software responsável por uma função de rede, como um firewall. Exibir uma lista de NVAs disponíveis no hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/category/networking?page=1&subcategories=appliances). Também há NVAs que fornecem otimização de WAN e outras funções de tráfego de rede. As NVAs são usadas normalmente com rotas BGP ou definidas pelo usuário. Você também pode usar um tráfego de toofilter NVA entre VNets.

## <a name="routing"></a>Rotear o tráfego de rede

O Azure cria tabelas de rotas que habilitam recursos tooany conectado sub-rede em qualquer toocommunicate VNet entre si, por padrão. Você pode implementar uma ou ambas Olá toooverride opções a seguir hello Azure cria as rotas padrão:
- **Rotas definidas pelo usuário:** você pode criar tabelas de rota personalizados com rotas que controlam onde o tráfego é roteado toofor cada sub-rede. toolearn mais sobre as rotas definidas pelo usuário, ler Olá [rotas definidas pelo usuário](virtual-networks-udr-overview.md) artigo.
- **Rotas de BGP:** se você se conectar a sua rede de local de tooyour de rede virtual usando uma conexão de Gateway de VPN do Azure, ou rota expressa, você pode propagar rotas BGP tooyour VNets.

## <a name="pricing"></a>Preços

Não há cobrança pelas redes virtuais, sub-redes, tabelas de rotas ou grupos de segurança de rede. Uso de largura de banda de Internet de saída, endereços IP públicos, emparelhamento de rede virtual, Gateways de VPN e ExpressRoute têm suas próprias estruturas de preços. Saudação de exibição [rede Virtual](https://azure.microsoft.com/pricing/details/virtual-network), [Gateway VPN](https://azure.microsoft.com/pricing/details/vpn-gateway), e [ExpressRoute](https://azure.microsoft.com/pricing/details/expressroute) preços páginas para obter mais informações.

## <a name="faq"></a>Perguntas frequentes

tooreview perguntas frequentes sobre rede Virtual, consulte Olá [perguntas Frequentes de rede Virtual](virtual-networks-faq.md) artigo.


## <a name="next-steps"></a>Próximas etapas

- Criar sua primeira NET e conectar alguns tooit de VMs, concluindo as etapas Olá Olá [criar sua primeira rede virtual](virtual-network-get-started-vnet-subnet.md) artigo.
- Criar uma conexão ponto a site de tooa VNet completando as etapas de saudação do hello [configurar uma conexão ponto a site](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artigo.
- Saiba mais sobre alguns dos Olá outra chave [recursos de rede](../networking/networking-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json) do Azure.
