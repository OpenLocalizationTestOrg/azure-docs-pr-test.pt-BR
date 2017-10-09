---
title: "Segurança de rede de aaaAzure | Microsoft Docs"
description: "Saiba mais sobre os serviços que podem ser dimensionada para cima e automaticamente toomeet Olá às necessidades de seu aplicativo ou empresa e serviços de computação em nuvem que incluem uma ampla seleção de instâncias de computação."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/24/2017
ms.author: TomSh
ms.openlocfilehash: 7dae83bbe338a2727575447583a7fb773527dd59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-network-security"></a>Segurança de rede do Azure

Sabemos que a segurança é trabalho na nuvem hello e como é importante que você encontrar precisas e em tempo hábil de informações sobre a segurança do Azure. Um dos toouse de motivos melhor Azure Olá para seus aplicativos e serviços é tootake aproveitar amplo o conjunto de recursos e ferramentas de segurança do Azure. Essas ferramentas e recursos de ajudam tornam soluções seguras toocreate possíveis em Olá plataforma Windows Azure.

O Microsoft Azure fornece confidencialidade, integridade e disponibilidade dos dados do cliente, ao mesmo tempo que também permite uma responsabilidade transparente. toohelp entender melhor coleção de saudação de controles de segurança de rede implementado no Microsoft Azure da perspectiva do cliente hello, este artigo, "Segurança de rede do Azure", foi escrito tooprovide uma visão completa de segurança de rede Olá controles disponíveis com o Microsoft Azure.

Este artigo é destinado a tooinform sobre a ampla variedade de saudação da rede controles que você pode configurar a segurança de saudação tooenhance das soluções de saudação que implantar no Azure. Se você estiver interessado no que a Microsoft does toosecure malha de rede de saudação do Olá plataforma do Azure, consulte a seção de segurança do Azure Olá Olá [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/azure-security).

## <a name="azure-platform"></a>Plataforma do Azure

O Azure é uma plataforma de serviço de nuvem pública que dá suporte a uma ampla seleção de sistemas operacionais, linguagens de programação, estruturas, ferramentas, bancos de dados e dispositivos.  Ele pode executar contêineres do Linux com a integração com o Docker, criar aplicativos com JavaScript, Python, .NET, PHP, Java e Node.js e criar back-ends para dispositivos iOS, Android e Windows. Serviços de nuvem do Azure suporte Olá tecnologias mesmo milhões de desenvolvedores e profissionais de TI já contam e confiam.

Quando você construir ou migra ativos de TI para um provedor de serviços de nuvem pública, você depender de tooprotect de recursos da organização seus aplicativos e dados com hello controles hello e serviços oferecem toomanage segurança de saudação do seu baseado em nuvem ativos.

Infraestrutura do Azure foi projetada de saudação recurso tooapplications para hospedagem milhões de clientes simultaneamente, e fornece uma base confiável em que as empresas podem atender aos requisitos de segurança. Além disso, Azure fornece uma extensa coleção de toocontrol de capacidade de saudação e opções de segurança configuráveis-los para que você possa personalizar requisitos exclusivos de segurança toomeet Olá das implantações de sua organização.

## <a name="abstract"></a>Resumo

Os serviços de nuvem pública da Microsoft entregam serviços e estrutura em larga escala, recursos de nível empresarial e várias opções de conectividade híbrida. Você pode escolher tooaccess esses serviços por meio de saudação da Internet ou com o Azure ExpressRoute, que fornece conectividade de rede privada. plataforma do Microsoft Azure Olá permite tooseamlessly estender sua infraestrutura de nuvem hello e compilar arquiteturas de várias camadas. Além disso, terceiros podem habilitar recursos avançados oferecendo serviços de segurança e soluções de virtualização.

Os serviços de rede do Azure maximizam a flexibilidade, disponibilidade, resiliência, segurança e integridade por design. Este white paper fornece detalhes sobre as funções de rede de saudação do Azure e informações sobre como os clientes podem usar toohelp de recursos de segurança nativa do Azure protegem seus ativos de informações.

Olá objetivo públicos-alvo deste white paper incluem:

- Gerentes técnicos, administradores de rede e desenvolvedores que estão procurando soluções de segurança disponíveis e com suporte no Azure.

-   SMEs ou executivos de processo de negócios que desejam uma visão geral de tooget Olá tecnologias de rede do Azure e serviços que são relevantes em discussões sobre segurança de rede em Olá nuvem pública do Azure.

## <a name="azure-networking-big-picture"></a>Visão geral de rede do Azure
Microsoft Azure inclui um toosupport robusta de infraestrutura de rede de seu aplicativo e os requisitos de conectividade do serviço. Conectividade de rede é possível entre os recursos localizados no Azure, entre locais e hospedado do Azure, recursos e tooand de saudação à Internet e o Azure.

![Visão Geral de Rede do Azure](media/azure-network-security/azure-network-security-fig-1.png)

Olá [infra-estrutura de rede do Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-networking-guidelines) permite que você toosecurely se conectar a recursos do Azure tooeach outros com redes virtuais (VNets). Uma rede virtual é uma representação de sua própria rede na nuvem hello. Uma rede virtual é uma isolamento lógico de assinatura de tooyour de rede dedicada Olá nuvem do Azure. Você pode se conectar a redes de local de tooyour VNets.

Dá suporte ao Azure dedicado a rede local do link WAN conectividade tooyour e uma rede Virtual do Azure com [ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction). Olá link entre o Azure e seu site usa uma conexão dedicada que não passa pelo Olá Internet pública. Se seu aplicativo do Azure é executado em vários datacenters, você pode usar [Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) tooroute solicitações de usuários de forma inteligente entre instâncias do aplicativo hello. Você também pode rotear o tráfego tooservices não em execução no Azure, se eles são acessíveis de saudação à Internet.

## <a name="enterprise-view-of-azure-networking-components"></a>Exibição para empresa de componentes de rede do Azure
O Azure tem muitos componentes de rede que são relevantes toonetwork discussões de segurança. descrevemos esses componentes de rede e foco em segurança Olá emite toothem relacionado.

> [!Note]
> Nem todos os aspectos de rede do Azure são descritos –, abordamos apenas aqueles considerados toobe essencial planejar e projetar uma infraestrutura de rede segura em torno de seus serviços e aplicativos que você implanta no Azure.

Neste documento, Olá rosto seguirá recursos corporativos de rede do Azure:

-   Conectividade de rede básica

-   Conectividade Híbrida

-   Controles de Segurança

-   Validação de rede

### <a name="basic-network-connectivity"></a>Conectividade de rede básica

Olá [rede Virtual do Azure](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) permite que o serviço toosecurely você se conectar a recursos do Azure tooeach outros com redes virtuais (VNet). Uma rede virtual é uma representação de sua própria rede na nuvem hello. Uma rede virtual é uma isolamento lógico de saudação rede Azure infraestrutura dedicada tooyour assinatura. Você também pode conectar VNets tooeach outros e redes usando VPNs site a site local e dedicado tooyour [links WAN](https://docs.microsoft.com/azure/expressroute/expressroute-introduction).

![Conectividade de rede básica](media/azure-network-security/azure-network-security-fig-2.png)

Com hello Noções básicas sobre o que você use servidores de toohost de VMs no Azure, a pergunta Olá é como essas VMs se conectar a rede tooa. Olá resposta é que as VMs se conectar tooan [rede Virtual do Azure](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview).

Redes virtuais do Azure são como redes de saudação virtual use local com suas próprias soluções de plataforma de virtualização, como o Microsoft Hyper-V ou VMware.

#### <a name="intra-vnet-connectivity"></a>Conectividade entre VNets

Você pode se conectar a VNets tooeach outras, permitindo que recursos conectados tooeither VNet toocommunicate uns com os outros em VNets. Você pode usar um ou ambos Olá opções tooconnect VNets tooeach outros a seguir:

- **Emparelhamento:** habilita recursos conectado toodifferent VNets do Azure em Olá mesmo toocommunicate local do Azure com o outro. Olá largura de banda e latência entre Olá VNet é Olá mesmo que recursos Olá toohello conectado mesma rede virtual. toolearn mais sobre o emparelhamento, ler [emparelhamento de rede Virtual](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview).

 ![Emparelhamento](media/azure-network-security/azure-network-security-fig-3.png)

- **Conexão de rede virtual a rede:** habilita recursos conectado toodifferent VNet do Azure em Olá iguais ou diferentes locais do Azure. Ao contrário do emparelhamento, a largura de banda é limitada entre as VNets, pois o tráfego deve fluir por um Gateway de VPN do Azure.

![Conexão de VNet para VNet](media/azure-network-security/azure-network-security-fig-4.png)


toolearn mais sobre como conectar VNets com uma conexão de rede virtual a rede, ler Olá [definir um artigo de conexão de rede virtual a rede](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal?toc=%2fazure%2fvirtual-network%2ftoc.json).

#### <a name="azure-virtual-network-capabilities"></a>Recursos de rede virtual do Azure:

Como você pode ver, uma rede Virtual do Azure fornece máquinas virtuais tooconnect toohello rede para que eles possam se conectar a recursos de rede tooother de forma segura. No entanto, a conectividade básica está a partir de Olá apenas. Olá seguintes recursos de serviço de rede Virtual do Azure do hello expõem características de segurança Olá rede Virtual do Azure:

-   Isolamento

-   Conectividade com a Internet

-   Conectividade de recursos do Azure

-   Conectividade de VNet

-   Conectividade local

-   Filtragem de tráfego

-   Roteamento

**Isolamento**

As VNets são [isoladas](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) umas das outras. Você pode criar VNets separadas para o desenvolvimento, teste e produção que use Olá mesmo [CIDR](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) blocos de endereço. Por outro lado, você pode criar várias VNets que usam blocos de endereço CIDR diferentes e conectam as redes. Você pode segmentar uma VNet em várias sub-redes.

O Azure fornece resolução de nome interno para VMs e [serviços de nuvem](https://azure.microsoft.com/services/cloud-services/) instâncias de função conectado tooa VNet. Opcionalmente, você pode configurar uma rede virtual toouse seus próprios servidores DNS, em vez de usar a resolução de nome interno do Azure.

É possível implementar várias VNets dentro de cada [assinatura](https://docs.microsoft.com/azure/azure-glossary-cloud-terminology?toc=%2fazure%2fvirtual-network%2ftoc.json) e [região](https://docs.microsoft.com/azure/azure-glossary-cloud-terminology?toc=%2fazure%2fvirtual-network%2ftoc.json) do Azure. Cada VNet é isolada de outras VNets. Para cada VNet, você pode:

-   Especificar um espaço de endereço IP privado personalizado usando endereços públicos e privados (RFC 1918). Azure atribui um endereço IP privado recursos conectados toohello VNet saudação do espaço de endereços, você atribuir.

-   Olá rede virtual em uma ou mais sub-redes de segmento e alocar uma parte da sub-rede de tooeach espaço do endereço de rede virtual hello.

-   Usar a resolução de nomes fornecida pelo Azure ou especifique seu próprio servidor DNS para uso por recursos conectado tooa VNet. toolearn mais informações sobre resolução de nomes em VNets, ler Olá [resolução de nomes para VMs e serviços de nuvem](https://docs.microsoft.com/azure/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances).

**Conectividade com a Internet**

Todos os [máquinas virtuais (VM) do Azure](https://docs.microsoft.com/azure/virtual-machines/windows/) e instâncias de função de serviços de nuvem conectado tooa VNet têm acessam toohello da Internet, por padrão. Você também pode habilitar recursos de toospecific de acesso de entrada, conforme necessário. (VM) e instâncias de função de serviços de nuvem conectado tooa VNet têm acessam toohello da Internet, por padrão. Você também pode habilitar recursos de toospecific de acesso de entrada, conforme necessário.

Todos os recursos tooa conectado VNet ter conectividade de saída toohello da Internet por padrão. endereço IP privado de saudação do recurso de saudação é o endereço de rede de origem convertido endereço IP público de tooa (SNAT) por Olá infraestrutura do Azure. Você pode alterar a conectividade do saudação padrão Implementando o roteamento personalizado e filtragem. toolearn mais sobre a conectividade da Internet de saída, ler Olá [Noções básicas sobre conexões de saída no Azure](https://docs.microsoft.com/azure/load-balancer/load-balancer-outbound-connections?toc=%2fazure%2fvirtual-network%2ftoc.json).

toocommunicate tooAzure recursos de saudação da Internet ou toocommunicate toohello saída Internet sem SNAT, um recurso deve ser atribuída um endereço IP público de entrada. toolearn mais informações sobre endereços IP públicos, ler Olá [endereços IP públicos](https://docs.microsoft.com/azure/virtual-network/virtual-network-public-ip-address).

**Conectividade de recursos do Azure**

[Recursos do Azure](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) como serviços de nuvem e máquinas virtuais podem ser conectado toohello mesma rede virtual. recursos de saudação podem se conectar a outros tooeach usando privada endereços IP, mesmo que eles estejam em sub-redes diferentes. O Azure fornece o roteamento padrão entre sub-redes, VNets e redes locais, para que você não tem tooconfigure e gerencie rotas.

Você pode se conectar a vários recursos do Azure tooa VNet, como máquinas virtuais (VM), os serviços de nuvem, ambientes de serviço de aplicativo e conjuntos de escala de máquina Virtual. VMs se conectar a sub-rede tooa dentro de uma rede virtual por meio de uma interface de rede (NIC). toolearn mais sobre NICs, ler Olá [interfaces de rede](https://docs.microsoft.com/azure/virtual-network/virtual-network-network-interface).

**Conectividade de VNet**

[VNets](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) pode ser conectado tooeach outras, permitindo que recursos conectado tooany VNet toocommunicate com qualquer recurso em qualquer outra VNet.

Você pode se conectar a VNets tooeach outras, permitindo que recursos conectados tooeither VNet toocommunicate uns com os outros em VNets. Você pode usar um ou ambos Olá opções tooconnect VNets tooeach outros a seguir:

- **Emparelhamento:** habilita recursos conectado toodifferent VNets do Azure em Olá mesmo toocommunicate local do Azure com o outro. Olá largura de banda e latência entre Olá VNets é Olá mesmo como recursos de saudação foram conectado toohello mesmo VNet.toolearn mais sobre o emparelhamento, ler Olá [emparelhamento de rede Virtual](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview).

- **Conexão de rede virtual a rede:** habilita recursos conectado toodifferent VNet do Azure em Olá iguais ou diferentes locais do Azure. Ao contrário do emparelhamento, a largura de banda é limitada entre as VNets, pois o tráfego deve fluir por um Gateway de VPN do Azure. toolearn mais sobre como conectar VNets com uma conexão de rede virtual a rede. toolearn mais, leia Olá [configurar uma conexão de rede virtual a rede](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal?toc=%2fazure%2fvirtual-network%2ftoc.json) .

**Conectividade local**

VNets pode ser conectado muito[local](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) redes através de conexões de rede privada entre sua rede e o Azure ou por meio de uma conexão de VPN site a site sobre Olá da Internet.

Você pode conectar seu tooa de rede local VNet usando qualquer combinação de saudação as opções a seguir:

- **Rede privada virtual (VPN) site a ponto:** estabelecido entre um único computador tooyour conectado rede Olá VNet. Esse tipo de conexão é ótimo se você estiver apenas começando com o Azure, ou para os desenvolvedores, porque ele requer pouca ou nenhuma alterações tooyour rede. conexão Olá usa a comunicação de tooprovide criptografado de protocolo SSTP Olá Olá Internet entre Olá PC e hello VNet. latência de saudação para uma VPN ponto a site é imprevisível desde que o tráfego de saudação atravessa Olá Internet.

- **VPN site a site:** estabelecida entre o dispositivo VPN e um Gateway de VPN do Azure. Esse tipo de conexão permite que qualquer recurso local autorizar tooaccess uma rede virtual. conexão de saudação é uma VPN IPsec/IKE que fornece comunicação criptografada sobre Olá Internet entre o dispositivo local e o gateway de VPN do Azure hello. latência de saudação para uma conexão site a site é imprevisível desde que o tráfego de saudação atravessa Olá Internet.

- **Azure ExpressRoute:** estabelecida entre sua rede e o Azure, por meio de um parceiro de ExpressRoute. Essa conexão é privada. O tráfego não atravessa Olá da Internet. latência de saudação para uma conexão de rota expressa é previsível desde que o tráfego não atravessam a saudação da Internet. toolearn mais informações sobre todos os Olá conexão opções anteriores, leia Olá [diagramas de topologia de Conexão](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways?toc=%2fazure%2fvirtual-network%2ftoc.json).

**Filtragem de tráfego**

O [tráfego de rede](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) de instâncias de função de VMs e do Serviços de Nuvem pode ser filtrado na entrada e na saída pelo endereço IP e porta de origem, endereço IP e porta de destino e protocolo.

Você pode filtrar o tráfego de rede entre sub-redes usando um ou ambos Olá as opções a seguir:

- **Rede (NSG) de grupos de segurança:** cada NSG pode conter várias regras de segurança de entrada e saída que permitem que você toofilter tráfego por endereço IP de origem e de destino, porta e protocolo. Você pode aplicar um tooeach NSG NIC em uma VM. Você também pode aplicar uma sub-rede do NSG toohello uma NIC ou outros recursos do Azure, está conectado. toolearn mais sobre os NSGs, ler Olá [grupos de segurança de rede](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg).

- **Dispositivos de rede virtual:** uma um dispositivo de rede virtual é uma VM que executa um software responsável por uma função de rede, como um firewall. Exiba uma lista de NVAs disponíveis no hello Azure Marketplace. Também há NVAs que fornecem otimização de WAN e outras funções de tráfego de rede. As NVAs são usadas normalmente com rotas BGP ou definidas pelo usuário. Você também pode usar um tráfego de toofilter NVA entre VNets.

**Roteamento**

Opcionalmente, você pode substituir o roteamento padrão do Azure configurando suas próprias rotas ou usando rotas BGP por meio de um gateway de rede.

O Azure cria tabelas de rotas que habilitam recursos tooany conectado sub-rede em qualquer toocommunicate VNet entre si, por padrão. Você pode implementar uma ou ambas Olá toooverride opções a seguir hello Azure cria as rotas padrão:

- **Rotas definidas pelo usuário:** você pode criar tabelas de rota personalizados com rotas que controlam onde o tráfego é roteado toofor cada sub-rede. toolearn mais sobre as rotas definidas pelo usuário, ler Olá [rotas definidas pelo usuário](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview).

- **Rotas de BGP:** se você se conectar a sua rede de local de tooyour de rede virtual usando uma conexão de Gateway de VPN do Azure, ou rota expressa, você pode propagar rotas BGP tooyour VNets.

### <a name="hybrid-internet-connectivity-connect-tooan-on-premises-network"></a>Conectividade de internet híbrida: conectar-se a rede de local de tooan
Você pode conectar seu tooa de rede local VNet usando qualquer combinação de saudação as opções a seguir:

-   Conectividade com a Internet

-   VPN de ponto a site (VPN P2S)

-   VPN de site a site (VPN S2S)

-   ExpressRoute

#### <a name="internet-connectivity"></a>Conectividade com a Internet

Como o nome sugere, conectividade com a Internet disponibilizar suas cargas de trabalho de saudação à Internet, fazendo com que você expor tooworkloads diferentes pontos de extremidade públicos que residem dentro da rede virtual hello. Essas cargas de trabalho podem ser expostas usando [balanceador de carga para a Internet](https://docs.microsoft.com/azure/load-balancer/load-balancer-internet-overview) ou simplesmente atribuindo um IP público toohello VM de endereço. Dessa forma, é possível para qualquer coisa na Internet de saudação toobe tooreach capaz de máquina virtual, fornecido um firewall de host, [(NSG) de grupos de segurança de rede](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg), e [rotas definidas pelo usuário](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview) permitir que toohappen.

Nesse cenário, você pode expor um aplicativo que necessite toobe pública toohello Internet e ser tooit tooconnect capaz de em qualquer lugar ou locais específicos, dependendo da configuração de saudação das cargas de trabalho.

#### <a name="point-to-site-vpn-or-site-to-site-vpn"></a>VPN de ponto a site ou VPN de site a site
Esses dois cairá em Olá mesma categoria. Ambos precisam de sua rede virtual toohave um Gateway de VPN e você pode se conectar usando um cliente de VPN para sua estação de trabalho como parte de saudação do tooit [configuraçãopontoaSite](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) ou você pode configurar seu local [dedispositivoVPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpn-devices) toobe capaz de tooterminate uma VPN site a site. Dessa forma, dispositivos locais podem se conectar a tooresources em Olá VNet.

Uma configuração ponto a Site (P2S) permite criar uma conexão segura de uma rede virtual do computador tooa de clientes individuais. O P2S é uma conexão VPN sobre SSTP (Secure Socket Tunneling Protocol).

![VPN ponto a site](media/azure-network-security/azure-network-security-fig-5.png)

Conexões ponto a Site são úteis quando você deseja tooconnect tooyour VNet de um local remoto, como em casa ou em um centro de conferência, ou quando tiver apenas alguns clientes que precisam de rede virtual do tooconnect tooa.

As conexões ponto a site não exigem um dispositivo VPN ou um endereço IP voltado para o público. Estabelecer uma conexão de VPN de saudação do computador do cliente de saudação. Portanto, P2S não é recomendável maneira tooconnect tooAzure caso você precise de uma conexão persistente de vários dispositivos locais e computadores tooyour rede do Azure.

![VPN de site a site](media/azure-network-security/azure-network-security-fig-6.png)

> [!Note]
> Para obter mais informações sobre conexões ponto a Site, consulte Olá [ponto a Site FA v p](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-classic-azure-portal).

Uma conexão de gateway VPN Site a Site é usado tooconnect seu local de rede tooan rede virtual do Azure por um túnel VPN IPsec/IKE (IKEv1 ou IKEv2).

Esse tipo de conexão exige um VPN de dispositivos localizado localmente que tenha uma tooit de endereço atribuído de IP público externamente. Essa conexão é feita em Olá Internet e permite que você muito "encapsular" informações dentro de uma conexão criptografada entre sua rede e o Azure. A VPN site a site é uma tecnologia segura e madura implantada por empresas de todos os portes há décadas. A criptografia de túnel é realizada usando o [modo de túnel IPsec](https://technet.microsoft.com/library/cc786385.aspx).

Enquanto o VPN site a site é uma tecnologia estabelecida, confiável e confiável, tráfego de túnel Olá atravessar Olá da Internet. Além disso, a largura de banda é relativamente restrita tooa máximo cerca de 200 Mbps.

Se você precisar de um nível excepcional de segurança ou de desempenho para as conexões entre locais, recomendamos que você use a Azure ExpressRoute para sua conectividade entre locais. O ExpressRoute é um link WAN dedicado entre seu local ou um provedor de hospedagem do Exchange. Como esta é uma conexão de telecomunicações, seus dados não passam pelo Olá da Internet e, portanto, é toohello não exposta possíveis riscos inerentes a comunicação com a Internet.

> [!Note]
> Para obter mais informações sobre os gateways de VPN, veja [Sobre o gateway de VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways).

#### <a name="dedicated-wan-link"></a>Link WAN dedicado
O Microsoft Azure ExpressRoute permite estender suas redes locais no hello Azure sobre uma conexão privada dedicada facilitada por um provedor de conectividade.

Conexões de rota expressa não passam pela Olá Internet pública. Isso permite toooffer de conexões de rota expressa mais confiabilidade, velocidades mais rápidas, latências menores e maior segurança que as conexões típicas pela Internet da saudação.

![ Link WAN Dedicado](media/azure-network-security/azure-network-security-fig-7.png)

> [!Note]
> Para obter informações sobre como tooconnect seu tooMicrosoft de rede usando o ExpressRoute, consulte [modelos de conectividade de rota expressa](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways) e [visão geral técnica do ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction).

Como com opções de VPN site a site hello, rota expressa também permite que você tooresources tooconnect que não são necessariamente em apenas um VNet. Na verdade, dependendo da saudação SKU, você pode conectar too10 VNets. Se você tiver Olá [complemento premium](https://docs.microsoft.com/azure/expressroute/expressroute-faqs), conexões tooup too100 VNets são possíveis, dependendo da largura de banda. mais sobre o que esses tipos de conexões aparência, como, leitura de toolearn [diagramas de topologia de Conexão](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways?toc=%2fazure%2fvirtual-network%2ftoc.json).

### <a name="security-controls"></a>Controles de segurança
Uma Rede Virtual do Azure fornece uma rede segura e lógica que é isolada de outras redes virtuais e dá suporte a vários controles de segurança que você pode usar em suas redes locais. Os clientes criar sua própria estrutura usando: sub-redes — use seu próprio intervalo de endereços IP privado, configurar as tabelas de rota, grupos de segurança de rede de controle de acesso ACLs (listas), gateways e dispositivos virtuais toorun suas cargas de trabalho na nuvem hello.

Olá seguem controles de segurança, que você pode usar em suas redes virtuais do Azure:

-   Controles de Acesso à Rede

-   Rotas definidas pelo usuário

-   Solução de segurança de rede

-   Gateway de Aplicativo

-   Firewall do aplicativo Web do Azure

-   Controle de disponibilidade de rede

#### <a name="network-access-controls"></a>Controles de acesso à rede
Embora Olá rede Virtual do Azure (VNet) é a base de saudação do modelo de rede do Azure e fornece isolamento e proteção, Olá [grupos de segurança de rede (NSG)](https://blogs.msdn.microsoft.com/igorpag/2016/05/14/azure-network-security-groups-nsg-best-practices-and-lessons-learned/) são Olá ferramenta principal que você usar tooenforce e controle de tráfego de rede regras de nível de rede hello.

![ Controles de Acesso à Rede](media/azure-network-security/azure-network-security-fig-8.png)


Você pode controlar o acesso ao permitir ou negar a comunicação entre as cargas de trabalho de saudação em uma rede virtual, de sistemas de redes do cliente por meio da conectividade entre locais, ou direcionar comunicação na Internet.

No diagrama de hello, VNets e NSGs residam em uma camada específica na pilha de segurança geral do Azure hello, onde os NSGs, UDR e dispositivos de rede virtual podem ser toocreate usada segurança limites tooprotect Olá implantações de aplicativos em rede Olá protegido.

Os NSGs usam o tráfego de tooevaluate uma tupla 5 (e são usados nas regras de saudação que você configurar para Olá NSG):

-   [Endereço IP de origem e de destino](https://support.microsoft.com/help/969029/the-functionality-for-source-ip-address-selection-in-windows-server-2008-and-in-windows-vista-differs-from-the-corresponding-functionality-in-earlier-versions-of-windows)

-   [Porta de origem e de destino](https://technet.microsoft.com/library/dd197515)

-   Protocolo: [protocolo TCP](https://technet.microsoft.com/library/cc940037.aspx) ou [protocolo UDP](https://technet.microsoft.com/library/cc940034.aspx)

Isso significa que você pode controlar o acesso entre uma única VM e um grupo de VMs ou um único tooanother VM única VM, ou entre sub-redes inteiras. Novamente, tenha em mente que isso é simples uma filtragem de pacote com estado simples e não uma inspeção de pacote completa. Não há nenhuma capacidade IPS ou IDS de nível de rede ou de validação de protocolo em um Grupo de Segurança de Rede.

Um NSG vem com algumas regras internas às quais você deve estar atento. Estes são:

-   **Permitir todo o tráfego em uma rede virtual específico:** todas as VMs em hello uma mesma rede Virtual do Azure podem se comunicar uns com os outros.

-   **Permitir tooinbound de balanceamento de carga do Azure:** essa regra permite o tráfego de qualquer endereço de destino de tooany de endereço de origem para o balanceador de carga do Azure hello.

-   **Negar todas as entradas:** essa regra bloqueia todo o tráfego de fornecimento de saudação da Internet que você tem permissão explicitamente.

-   **Permitir que todos os toohello de saída de tráfego da Internet:** essa regra permite que máquinas virtuais tooinitiate conexões toohello da Internet. Se você não quiser que essas conexões iniciadas, precisar toocreate tooblock uma regra as conexões ou aplicar o túnel forçado.

#### <a name="system-routes-and-user-defined-routes"></a>Rotas de sistema e rotas definidas pelo usuário

Quando você adiciona máquinas virtuais (VMs) tooa VPN (rede virtual) no Azure, você observe que VMs Olá capaz de toocommunicate entre si pela rede hello, automaticamente. Não é necessário toospecify um gateway, embora Olá VMs estiverem em sub-redes diferentes.

Olá mesmo é verdadeiro para comunicação de saudação VMs toohello Internet pública e rede de local tooyour mesmo quando uma conexão híbrida do Azure tooyour possui datacenter estiver presente.

![Rotas do sistema](media/azure-network-security/azure-network-security-fig-9.png)

Este fluxo de comunicação é possível porque o Azure usa uma série de sistema rotas toodefine como fluxos de tráfego IP. Rotas de sistema controlam o fluxo de saudação de comunicação no hello os seguintes cenários:

-   No hello na mesma sub-rede.

-   De tooanother uma sub-rede dentro de uma rede virtual.

-   De VMs toohello da Internet.

-   De uma rede virtual tooanother redes por meio de um gateway de VPN.

-   De um tooanother VNet redes por meio de emparelhamento VNet ([encadeamento de serviço](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview)).

-   De uma rede tooyour no local de rede virtual por meio de um gateway de VPN.

Muitas empresas têm segurança rigorosa e políticas de requisitos de conformidade que exigem a inspeção do local de todos os tooenforce de pacotes de rede específico. O Azure fornece um mecanismo chamado [túnel forçado](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-forced-tunneling) que direciona o tráfego de saudação VMs locais tooon criando uma rota personalizada ou [Border Gateway Protocol (BGP)](https://docs.microsoft.com/windows-server/remote/remote-access/bgp/border-gateway-protocol-bgp) anúncios por meio de Rota expressa ou VPN.

O túnel forçado no Azure é configurado por meio de UDR (rotas de definidas pelo usuário) de rede virtual. Redirecionar o tráfego tooan local do site é expressa como um gateway de VPN do Azure toohello rota padrão.

Olá, seção a seguir lista limitação atual Olá da tabela de roteamento hello e rotas para uma rede Virtual do Azure:

-   Cada sub-rede de rede virtual tem uma tabela de roteamento interna do sistema. tabela de roteamento de sistema Olá tem Olá três grupos de rotas a seguir:

 -  **Rotas de rede virtual locais:** diretamente toohello VMs de destino na Olá mesma rede virtual

 - **Nas rotas locais:** toohello gateway de VPN do Azure

 -  **Rota padrão:** toohello diretamente da Internet. Pacotes destinados toohello endereços IP privados não cobertos por rotas Olá dois anterior são removidos.

-   Com o lançamento de saudação de rotas definidas pelo usuário, crie um tooadd de tabela de roteamento uma rota padrão e, em seguida, associar Olá roteamento tabela tooyour VNet sub-rede tooenable forçado túnel nessas sub-redes.

-   É necessário tooset "site padrão" entre a rede virtual de toohello conectado Olá de sites locais entre locais.

-   O túnel forçado deve ser associado a uma Rede Virtual que tem um gateway de VPN de roteamento dinâmico (e não um gateway estático).

- Túnel forçado do ExpressRoute não está configurado por meio desse mecanismo, mas em vez disso, é habilitado por anuncia uma rota padrão por meio de saudação ExpressRoute BGP sessões de emparelhamento.

> [!Note]
> Para obter mais informações, consulte Olá [documentação de rota expressa](https://azure.microsoft.com/documentation/services/expressroute/) para obter mais informações.

#### <a name="network-security-appliances"></a>Soluções de segurança de rede
Enquanto as rotas definidas pelo usuário e grupos de segurança de rede podem fornecer uma certas medidas de segurança de rede no hello camadas de transporte e de rede de saudação [modelo OSI](https://en.wikipedia.org/wiki/OSI_model), serão toobe situações onde deseja ou precisa tooenable segurança em níveis mais altos da pilha de rede hello. Em tais situações, é recomendável que você implante dispositivos de segurança de rede virtual fornecidos por parceiros do Azure.

![Soluções de segurança de rede](./media/azure-network-security/azure-network-security-fig-10.png)

Dispositivos de segurança de rede do Azure melhorar a segurança de rede virtual e funções de rede e elas estão disponíveis de vários fornecedores por meio de saudação [Azure Marketplace](https://azuremarketplace.microsoft.com). Esses dispositivos de segurança virtual podem ser implantado tooprovide:

-   Firewalls altamente disponíveis

-   Prevenção de intrusões

-   Detecção de intrusões

-   WAFs (firewalls de aplicativo Web)

-   Otimização WAN

-   Roteamento

-   Balanceamento de carga

-   VPN

-   Gerenciamento de certificados

-   Active Directory

-   Autenticação multifator

#### <a name="application-gateway"></a>Gateway de Aplicativo

O [Gateway de Aplicativo do Microsoft Azure](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) é uma solução de virtualização dedicada que fornece um ADC (controlador de entrega de aplicativos) como um serviço.

 ![Gateway de Aplicativo](./media/azure-network-security/azure-network-security-fig-11.png)

Application Gateway permite que você toooptimize web farm desempenho e disponibilidade descarregando CPU intensa SSL encerramento toohello application gateway (descarregamento de SSL). Ele também fornece outros recursos de roteamento de camada 7, incluindo:

-   Distribuição round robin do tráfego de entrada

-   Afinidade de sessão baseada em cookie

-   Visão geral do roteamento baseado em caminho de URL

-   Capacidade toohost vários sites por trás de um único Gateway de aplicativo


Um [firewall do aplicativo web (WAF)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) também é fornecido como parte do gateway de aplicativo hello. Isso fornece proteção tooweb aplicativos comuns de vulnerabilidades de web e explorações. O Gateway de Aplicativo pode ser configurado como um gateway voltado para a Internet, um gateway apenas interno ou uma combinação de ambos.

O WAF do Gateway de Aplicativo pode ser executado no modo de detecção ou de prevenção. É um caso de uso comum para administradores toorun no tráfego tooobserve do modo de detecção para padrões mal-intencionados. Depois de explorações potenciais forem detectadas, ativar o modo de tooprevention bloqueia o tráfego de entrada suspeito.

 ![Gateway de Aplicativo](./media/azure-network-security/azure-network-security-fig-12.png)

Além disso, WAF de Gateway de aplicativo ajuda a monitorar os aplicativos web contra ataques usando um log WAF em tempo real que são integrados com [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview) e [Central de segurança do Azure](https://azure.microsoft.com/services/security-center/) tootrack WAF alertas e monitorar facilmente as tendências.

Olá JSON formatado log vai diretamente conta de armazenamento toohello do cliente. Você tem controle total sobre esses logs e pode aplicar suas próprias políticas de retenção.

Você também pode ingerir esses logs em seu próprio sistema de análise usando a [Integração de Log do Azure](https://aka.ms/AzLog). Logs de WAF também são integradas [Operations Management Suite (OMS)](https://www.microsoft.com/cloud-platform/operations-management-suite) , você pode usar a análise de logs do OMS tooexecute sofisticado consultas refinadas.

#### <a name="azure-web-application-firewall-waf"></a>WAF (Firewall do aplicativo Web) do Azure

Aplicativos da Web estão cada vez mais destinos de ataques mal-intencionados que exploram vulnerabilidades conhecidas comuns, como injeção SQL, ataques de script entre sites e outros ataques que aparecem no hello [superior OWASP 10](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project). Evitar tais maliciosos no aplicativo hello exige manutenção rigorosa, aplicação de patch e monitoramento em vários níveis de topologia de aplicativo hello.

 ![WAF (Firewall do Aplicativo Web) do Azure](./media/azure-network-security/azure-network-security-fig-13.png)

Um [Firewall do aplicativo Web (WAF)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) centralizado pode proteger contra ataques da Web e simplifica o gerenciamento de segurança sem exigir nenhuma alteração de aplicativo.

Uma solução WAF também possa reagir de ameaça à segurança tooa mais rápida por uma vulnerabilidade conhecida em um local central em vez de proteção de cada um dos aplicativos web individuais de aplicação de patch. Os gateways de aplicativos existentes podem ser facilmente convertido tooa web aplicativo firewall habilitado application gateway.

#### <a name="network-availability-controls"></a>Controles de disponibilidade de rede

Há diferentes opções toodistribute o tráfego usando o Microsoft Azure. Essas opções funcionam de forma diferente uma da outra, com conjuntos diferentes de recursos e permitindo cenários diferentes. Cada uma pode ser usada isoladamente ou em combinação.

A seguir são Olá controles de disponibilidade de rede:

-   Azure Load Balancer

-   Gateway de Aplicativo

-   Gerenciador de Tráfego

**Azure Load Balancer**

Fornece tooyour aplicativos de alto desempenho de disponibilidade e rede. É um balanceador de carga do tipo Camada 4 (TCP, UDP) que distribui o tráfego de entrada entre as instâncias de serviço íntegras definidas em um conjunto de balanceadores de carga.

 ![Azure Load Balancer](media/azure-network-security/azure-network-security-fig-14.png)


O Azure Load Balancer pode ser configurado para:

-   Balancear cargas de entrada da Internet tráfego toovirtual máquinas. Essa configuração é conhecida como [balanceamento de carga voltada para a Internet](https://docs.microsoft.com/azure/load-balancer/load-balancer-internet-overview).

-   Balanceie o tráfego de carga entre as máquinas virtuais em uma rede virtual, entre as máquinas virtuais nos serviços de nuvem ou entre os computadores locais e as máquinas virtuais em uma rede virtual entre as instalações. Essa configuração é conhecida como [balanceamento de carga interno](https://docs.microsoft.com/azure/load-balancer/load-balancer-internal-overview).

-   Encaminhar o tráfego externo tooa específico de máquina virtual.

Todos os recursos em nuvem Olá necessário um toobe de endereço IP público de saudação à Internet. infraestrutura de nuvem Olá no Azure usa endereços IP não roteável para seus recursos. O Azure usa a conversão de endereços de rede (NAT) com IP endereços toocommunicate toohello Internet pública.

 **Gateway de Aplicativo**

 Application Gateway funciona na camada de aplicativo hello (camada 7 na pilha de referência de rede Olá OSI). Ele atua como um serviço de proxy reverso, encerrando a conexão de cliente hello e encaminhamento de solicitações de pontos de extremidade tooback-end.

 **Gerenciador de tráfego**

O Microsoft Azure Traffic Manager permite que você toocontrol distribuição de saudação do tráfego do usuário para pontos de extremidade de serviço em data centers diferentes. Os pontos de extremidade de serviço com suporte no Gerenciador de Tráfego incluem VMs do Azure, Aplicativos Web e serviços de nuvem. Você também pode usar o Gerenciador de Tráfego com pontos de extremidade externos e não do Azure.

O Traffic Manager usa Olá sistema DNS (Domain Name) toodirect cliente solicita toohello ponto de extremidade mais apropriado com base em um [o método de roteamento de tráfego](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-routing-methods) e a integridade de saudação de pontos de extremidade de saudação. O Traffic Manager fornece uma variedade de roteamento de tráfego métodos toosuit diferentes necessidades de aplicativo, integridade do ponto de extremidade [monitoramento](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-monitoring)e o failover automático. Gerenciador de tráfego é toofailure resiliente, incluindo Olá falha de toda a uma região do Azure.

O Azure Traffic Manager permite que você toocontrol distribuição de saudação do tráfego em seus pontos de extremidade do aplicativo. Um ponto de extremidade é qualquer serviço para a Internet hospedado dentro ou fora do Azure.

O Gerenciador de Tráfego oferece dois benefícios principais:

-   Distribuição do tráfego de acordo com o tooone de vários [métodos de roteamento de tráfego](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-routing-methods).

-   [Monitoramento contínuo de integridade do ponto de extremidade](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-monitoring) e failover automático quando os pontos de extremidade falharem.

Quando um cliente tenta tooconnect tooa serviço, ele precisa primeiro resolver nome DNS Olá Olá tooan IP do endereço do serviço. cliente Hello, em seguida, conecta-se o serviço de saudação do toothat IP endereço tooaccess. Pontos de extremidade com base nas regras de saudação do método de roteamento de tráfego de saudação do serviço do Traffic Manager usa DNS toodirect clientes toospecific. Os clientes se conectam diretamente toohello selecionado de ponto de extremidade. O Gerenciador de Tráfego não é um proxy nem um gateway. Gerenciador de tráfego não vê tráfego Olá entre cliente hello e serviço de saudação.

### <a name="azure-network-validation"></a>Validação de rede do Azure

Validação de rede do Azure é tooensure que Olá rede do Azure está funcionando conforme ela é configurada e validação pode ser feita usando Olá serviços e recursos disponíveis toomonitor Olá rede. Com o observador de rede do Azure, você pode acessar uma grande quantidade de log e os recursos de diagnóstico que capacitam você com informações toounderstand sua integridade e desempenho da rede. Esses recursos são acessíveis por meio do Portal, do Power Shell, da CLI, da API Rest e do SDK.

Segurança operacional Azure refere-se a serviços toohello, controles e toousers de recursos disponíveis para proteger seus dados, aplicativos e outros recursos do Microsoft Azure. Segurança operacionais do Azure é construída em uma estrutura que incorpora conhecimento Olá obtido por meio de uma diversos recursos que são exclusivo tooMicrosoft, incluindo Olá Microsoft Security Development Lifecycle (SDL), Olá Centro de resposta de segurança do Microsoft programa e conhecimento profundo do cenário de ameaças de segurança Olá cibernéticos.

-   [Azure Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview)

-   [Central de Segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-intro)

-   [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview)

-   [Observador de Rede do Azure](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview)

-   [Azure Storage Analytics](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics)

-   Gerenciador de Recursos do Azure

#### <a name="azure-resource-manager"></a>Azure Resource Manager

pessoas Hello e processos que operam Microsoft Azure são talvez recurso mais importante de segurança Olá da plataforma de saudação. Esta seção descreve recursos que ajudam a melhorar e manter a segurança, continuidade e privacidade da infraestrutura de datacenter global da Microsoft.

infraestrutura de saudação para seu aplicativo geralmente é composta de vários componentes – pode ser uma máquina virtual, conta de armazenamento e rede virtual, ou um aplicativo web, banco de dados, servidor de banco de dados e serviços de terceiros. Tais componentes não são vistos como entidades separadas, em vez disso, eles são mostrados como partes relacionadas e interdependentes de uma única entidade. Você deseja toodeploy, gerenciar e monitorá-los como um grupo. Gerenciador de recursos do Azure permite que você toowork com recursos de saudação em sua solução como um grupo.

Você pode implantar, atualizar ou excluir todos os recursos de saudação para sua solução em uma única operação coordenada. Usar um modelo para a implantação e esse modelo pode ser útil para ambientes diferentes, como teste, preparação e produção. Gerenciador de recursos fornece segurança, auditoria e marcação recursos toohelp gerenciar seus recursos após a implantação.

**benefícios de saudação do usando o Gerenciador de recursos**

O Gerenciador de Recursos fornece vários benefícios:

-   Você pode implantar, gerenciar e monitorar todos os recursos de saudação para sua solução como um grupo, em vez de manipular esses recursos individualmente.

-   Repetidamente, você pode implantar sua solução em todo o ciclo de vida de desenvolvimento hello e ter certeza de que seus recursos são implantados em um estado consistente.

-   Você pode gerenciar sua infraestrutura por meio de modelos declarativos em vez de scripts.

-   Você pode definir dependências de saudação entre os recursos, para que eles são implantados na ordem correta, Olá.

-   Você pode aplicar tooall serviços de controle de acesso no seu grupo de recursos como controle de acesso baseado em função (RBAC) nativamente é integrado à plataforma de gerenciamento de saudação.

-   Você pode aplicar marcas tooresources toologically organizar todos os recursos de saudação em sua assinatura.

-   Você pode esclarecer a cobrança da sua organização exibindo os custos para um grupo de recursos que compartilham a mesma marcação.

> [!Note]
> Gerenciador de recursos fornece um novo toodeploy de maneira e gerenciar suas soluções. Se você usou Olá modelo de implantação anterior e deseja toolearn sobre alterações hello, consulte [Noções básicas sobre o Gerenciador de recursos de implantação e implantação clássica](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-deployment-model).

## <a name="azure-network-logging-and-monitoring"></a>Registro em log e monitoramento de rede do Azure

O Azure oferece muitas toomonitor de ferramentas, evitar, detectar e responder a eventos de segurança toonetwork. Alguns dos hello mais poderosas ferramentas disponíveis tooyou nesta área incluem:

-   Observador de Rede

-   Monitoramento no nível do recurso de rede

-   Log Analytics

### <a name="network-watcher"></a>Observador de Rede

[Inspetor de rede](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) -baseada em cenário de monitoramento é fornecido com recursos de saudação do observador de rede. Esse serviço inclui a captura de pacotes, próximo salto, verificação do fluxo de IP, exibição do grupo de segurança e logs de fluxo de NSG. Monitoramento do nível do cenário fornece uma exibição de tooend final dos recursos de rede no monitoramento de recursos de rede do contraste tooindividual.

 ![Observador de Rede](./media/azure-network-security/azure-network-security-fig-15.png)

Observador de rede é um serviço regional que permite que você toomonitor e diagnosticar as condições em uma rede cenário nível, para e do Azure. Diagnóstico de rede e as ferramentas de visualização disponíveis com o observador de rede ajudarão-lo a entender, diagnosticar e obter a rede de tooyour insights no Azure.

Observador de rede atualmente tem Olá recursos a seguir:

#### <a name="topology"></a>Topologia

A [topologia](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-overview) retorna um gráfico de recursos de rede em uma rede virtual. gráfico de saudação mostra interconexão de saudação entre Olá recursos toorepresent Olá final tooend a conectividade de rede. No portal de saudação topologia retorna objetos de recurso de saudação em de acordo com a base de rede virtual. relações de saudação estão representadas por linhas entre os recursos de saudação fora da região do observador de rede hello, mesmo que no recurso Olá o grupo não será exibido. recursos Olá retornados na exibição de portal Olá são um subconjunto Olá de componentes de rede que são mostrados. lista completa de saudação de toosee de recursos de rede, você pode usar [PowerShell](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-powershell) ou [REST](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-rest).

Como os recursos são retornados conexão Olá entre eles são modeladas em duas relações.

- **Confinamento** – Exemplo: uma rede virtual contém uma sub-rede que contém um adaptador de rede.

- **Associados** – um adaptador de rede está associado a uma VM.

#### <a name="variable-packet-capture"></a>Captura de pacote variável

Inspetor de rede [captura de pacote variável](https://docs.microsoft.com/azure/network-watcher/network-watcher-packet-capture-overview) permite que você toocreate pacote captura sessões tootrack tooand de tráfego de uma máquina virtual. Captura de pacote ajuda toodiagnose anomalias na rede ambos os reativa e proactivity. Outros usos incluem a coleta de estatísticas de rede, obtenção de informações de invasões de rede, toodebug cliente-servidor comunicações e muito mais.

A captura de pacote é uma extensão de máquina virtual iniciada remotamente por meio do Observador de Rede. Esse recurso facilita a carga Olá da execução de uma captura de pacote manualmente na máquina virtual Olá desejado, o que economiza tempo. Captura de pacote pode ser acionada por meio do portal de saudação, o PowerShell, CLI ou API REST. Os alertas de Máquina Virtual são um exemplo de como a captura de pacote pode ser disparada.

#### <a name="ip-flow-verify"></a>Verificação de fluxo de IP

[Verifique se os fluxos IP](https://docs.microsoft.com/azure/network-watcher/network-watcher-ip-flow-verify-overview) verifica se um pacote é permitido ou negado tooor de uma máquina virtual com base nas informações de 5 tuplas. Essas informações consistem em direção, protocolo, IP local, IP remoto, porta local e porta remota. Se o pacote de saudação é negado por um grupo de segurança, nome de saudação de regra Olá negado pacote de saudação é retornado. Enquanto qualquer IP de origem ou de destino pode ser escolhido, esse recurso ajuda os administradores a diagnosticar rapidamente toohello ou problemas de conectividade de internet e de ou toohello ambiente de local.

A verificação de fluxo de IP é direcionada a um adaptador de rede de uma máquina virtual. Fluxo de tráfego é verificado com base em tooor de configurações de saudação configurada desta interface de rede. Esse recurso é útil para confirmar se uma regra em um grupo de segurança de rede está bloqueando tooor de tráfego de entrada ou de saída de uma máquina virtual.

#### <a name="next-hop"></a>Próximo salto

Determina a saudação [próximo salto](https://docs.microsoft.com/azure/network-watcher/network-watcher-next-hop-overview) para pacotes que está sendo direcionados no hello malha de rede do Azure, permitindo que você toodiagnose qualquer configurado incorretamente rotas definidas pelo usuário. O tráfego de uma VM é enviado tooa destino com base nas rotas efetiva de saudação associadas a uma NIC. Próximo salto obtém o tipo de próximo salto hello e endereço IP de um pacote de uma máquina virtual específica e a NIC. Isso ajuda a toodetermine se hello pacote está sendo direcionado toohello destino ou é holed de tráfego Olá sendo preto.

Próximo salto também retorna a tabela de rotas Olá associada próximo salto de saudação. Ao consultar um próximo salto se rota de saudação é definida como uma rota definida pelo usuário, essa rota será retornada. Caso contrário, o Próximo salto retornará a "Rota do Sistema".

#### <a name="security-group-view"></a>Exibição de grupo de segurança

Obtém as regras de segurança efetiva e aplicadas de Olá que são aplicadas em uma máquina virtual. Os grupos Segurança da Rede podem ser associados no nível da sub-rede ou no nível da NIC. Quando associado em um nível de sub-rede, ele se aplica a instâncias de VM Olá tooall na sub-rede hello. Rede [exibição de grupo de segurança](https://docs.microsoft.com/azure/network-watcher/network-watcher-security-group-view-overview) retorna todos os NSGs Olá configurado e regras associadas em um nível NIC e de sub-rede para uma máquina virtual fornece ideias sobre configuração de saudação. Além disso, as regras de segurança efetiva de saudação são retornadas para cada uma das NICs de saudação em uma VM. Usando a exibição Grupo de Segurança da Rede, você pode avaliar uma VM quanto às vulnerabilidades da rede, como as portas abertas. Você também pode validar se o grupo de segurança de rede está funcionando conforme o esperado com base em um [comparação entre hello configurado e Olá regras de segurança efetiva](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-auditing-powershell).

#### <a name="nsg-flow-logging"></a>Registro em log do fluxo NSG

 Fluxo de logs para grupos de segurança de rede permitem que você toocapture logs tootraffic relacionados que são permitidas ou negadas pelas regras de segurança de saudação no grupo de saudação. Olá fluxo é definido pelas informações de uma tupla 5 – IP de origem, IP de destino, porta de origem, porta de destino e protocolo.

[Logs de fluxo de grupo de segurança de rede](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview) são um recurso do observador de rede que permite que você tooview informações sobre o tráfego IP de entrada e saída por meio de um grupo de segurança de rede.

#### <a name="virtual-network-gateway-and-connection-troubleshooting"></a>Solução de problemas de conexão e do gateway de rede virtual

Observador de rede fornece vários recursos que diz respeito a toounderstanding seus recursos de rede no Azure. Um desses recursos é a solução de problemas de recursos. A [solução de problemas de recursos](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest) pode ser chamada pelo PowerShell, pela CLI ou pela API REST. Quando chamado, o observador de rede inspeciona a integridade de saudação de um gateway de rede Virtual ou uma Conexão e retorna suas descobertas.

Esta seção leva você através de saudação diversas tarefas de gerenciamento que estão atualmente disponíveis para solução de problemas de recursos.

-   [Solução de problemas de um gateway de rede virtual](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest)

-   [Como solucionar problemas de uma conexão](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest)

#### <a name="network-subscription-limits"></a>Limites de assinatura da rede

[Limites de assinatura de rede](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) fornecem detalhes de uso de saudação de cada um dos recursos de rede de saudação em uma assinatura em uma região com o número máximo de saudação de recursos disponíveis.

#### <a name="configuring-diagnostics-log"></a>Configurar o log de diagnóstico

O Observador de Rede fornece uma exibição dos [logs de diagnóstico](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview). Essa exibição contém todos os recursos de rede que oferecem suporte ao log de diagnóstico. Nessa exibição, você pode habilitar e desabilitar os recursos de rede de modo rápido e prático.

### <a name="network-resource-level-monitoring"></a>Monitoramento no nível do recurso da rede

Olá recursos a seguir está disponível para o monitoramento de nível de recursos:

#### <a name="audit-log"></a>Log de auditoria

Operações executadas como parte da configuração de saudação de redes são registradas. Esses logs de auditoria é essencial tooestablish vários conformidades. Esses logs podem ser exibidos no portal do Azure de saudação ou recuperados por meio de ferramentas da Microsoft, como o Power BI ou ferramentas de terceiros. Logs de auditoria estão disponíveis por meio do portal hello, PowerShell, CLI e API de Rest.

> [!Note]
> Para obter mais informações sobre os Logs de auditoria, consulte [Operações de auditoria com o Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-audit).
Os logs de auditoria estão disponíveis para as operações realizadas em todos os recursos da rede.


#### <a name="metrics"></a>Métricas

As métricas são medidas de desempenho e contadores coletados em um período de tempo. As métricas estão disponíveis atualmente para o Gateway de Aplicativo. As métricas podem ser usados tootrigger alertas com base no limite. Gateway de aplicativo do Azure por padrão monitora a integridade de saudação de todos os recursos em seu pool de back-end e automaticamente remove qualquer recurso considerado não íntegro do pool de saudação. Application Gateway continua instâncias não íntegras do toomonitor hello e os adiciona fazer toohello Íntegro pool de back-end quando estiverem disponíveis e responder toohealth testes. Gateway de aplicativo envia Olá investigações de integridade com hello mesma porta que é definida nas configurações de HTTP de back-end de saudação. Essa configuração garante que teste hello está testando Olá a mesma porta que os clientes usarão back-end do tooconnect toohello.

> [!Note]
> Consulte [Application Gateway Diagnostics](https://docs.microsoft.com/azure/application-gateway/application-gateway-probe-overview) tooview como métricas podem ser usados toocreate alertas.

#### <a name="diagnostic-logs"></a>Logs de diagnóstico

Eventos periódicos e espontâneas são criados pelos recursos de rede e registrados em contas de armazenamento, enviadas tooan Hub de eventos ou análise de Log. Esses logs fornecem informações sobre a integridade de saudação de um recurso. Esses logs podem ser visualizados em ferramentas como o Power BI e o Log Analytics. toolearn como logs de diagnóstico tooview, visite [análise de Log](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-networking-analytics).

Os logs de diagnóstico estão disponíveis para o [Balanceador de Carga](https://docs.microsoft.com/azure/load-balancer/load-balancer-monitor-log), [Grupos de Segurança da Rede](https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log), Rotas e [Gateway de Aplicativo](https://docs.microsoft.com/azure/application-gateway/application-gateway-diagnostics).

O Observador de Rede fornece uma exibição dos logs de diagnóstico. Essa exibição contém todos os recursos de rede que oferecem suporte ao log de diagnóstico. Nessa exibição, você pode habilitar e desabilitar os recursos de rede de modo rápido e prático.

### <a name="log-analytics"></a>Log Analytics

[Análise de log](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) é um serviço no [Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) que monitora o toomaintain de ambientes de nuvem e local sua disponibilidade e desempenho. Ele coleta dados gerados pelos recursos em seus ambientes de nuvem e locais e de outras análises de tooprovide ferramentas monitoramento em várias origens.

Análise de log oferece Olá soluções para monitorar suas redes a seguir:

-   Monitor de Desempenho de Rede (NPM)

-   Análise do Gateway de Aplicativo do Azure

-   Análise do Grupo de Segurança de Rede do Azure

#### <a name="network-performance-monitor-npm"></a>NPM (Monitor de Desempenho de Rede)
Olá [Monitor de desempenho de rede](https://docs.microsoft.com/azure/log-analytics/log-analytics-network-performance-monitor) solução de gerenciamento é uma solução que monitora a integridade de saudação, a disponibilidade e a acessibilidade de redes de monitoramento de rede.

É usado toomonitor conectividade entre:

-   nuvem pública e local

-   data centers e locais de usuário (filiais)

-   sub-redes hospeda várias camadas de um aplicativo de várias camadas.


#### <a name="azure-application-gateway-analytics-in-log-analytics"></a>Análise do Gateway de Aplicativo do Azure no Log Analytics

Olá logs a seguir têm suporte para Gateways de aplicativo:

-   ApplicationGatewayAccessLog

-   ApplicationGatewayPerformanceLog

-   ApplicationGatewayFirewallLog

Olá métricas a seguir têm suporte para Gateways de aplicativo:

-   Taxa de transferência de 5 minutos

#### <a name="azure-network-security-group-analytics-in-log-analytics"></a>Análise do Grupo de Segurança de Rede do Azure no Log Analytics

Olá seguintes logs têm suporte para [grupos de segurança de rede](https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log):

- **NetworkSecurityGroupEvent:** contém entradas para o NSG as regras são aplicadas tooVMs e funções de instância com base no endereço MAC. status Olá para essas regras são coletados a cada 60 segundos.

- **NetworkSecurityGroupRuleCounter:** contém entradas para quantas vezes cada NSG regra é aplicada toodeny ou permitir o tráfego.

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre a segurança lendo alguns dos tópicos detalhados sobre segurança:

-   [Análise de logs para NSGs (grupos de segurança de rede)](https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log)

-   [Rede inovações essa unidade Olá nuvem de interrupção](https://azure.microsoft.com/blog/networking-innovations-that-drive-the-cloud-disruption/)

-   [SONiC: Olá software comutador que alimenta Olá nuvem Global da Microsoft de rede](https://azure.microsoft.com/blog/sonic-the-networking-switch-software-that-powers-the-microsoft-global-cloud/)

-   [Como a Microsoft constrói a sua rede global rápida e confiável](https://azure.microsoft.com/blog/how-microsoft-builds-its-fast-and-reliable-global-network/)

-   [Esclarecendo a inovação de rede](https://azure.microsoft.com/blog/lighting-up-network-innovation/)
