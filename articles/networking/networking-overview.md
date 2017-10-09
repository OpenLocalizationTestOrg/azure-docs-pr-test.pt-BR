---
title: rede aaaAzure | Microsoft Docs
description: "Saiba sobre os recursos e serviços de rede do Azure."
services: networking
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: jdial
ms.openlocfilehash: 18945d139427f2e65138c0fd223e663fa46e9211
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking"></a>Rede do Azure

O Azure fornece uma variedade de recursos de rede que podem ser usados juntos ou separadamente. Clique em qualquer Olá funcionalidades principais toolearn mais sobre eles a seguir:
- [Conectividade entre os recursos do Azure](#connectivity): recursos de conectar o Azure juntos em uma rede virtual privada, segura na nuvem hello.
- [Conectividade com a Internet](#internet-connectivity): comunicar tooand de recursos do Azure por meio de saudação à Internet.
- [Conectividade local](#on-premises-connectivity): conectar-se um tooAzure recursos da rede de local por meio de uma rede virtual privada (VPN) pela Internet de hello, ou por meio de uma conexão dedicada tooAzure.
- [Direção do tráfego e balanceamento de carga](#load-balancing): Olá de carga balancear o tráfego tooservers no mesmo local e direcione o tráfego tooservers em diferentes locais.
- [Segurança](#security): filtre o tráfego de rede entre sub-redes ou VMs (máquinas virtuais) da rede.
- [Roteamento](#routing): use o roteamento padrão ou controle totalmente o roteamento entre seus recursos do Azure e recursos locais.
- [Capacidade de gerenciamento](#manageability): monitore e gerencie os recursos de rede do Azure.
- [Ferramentas de implantação e configuração](#tools): usar um portal baseado na web ou ferramentas de linha de comando de plataforma cruzada toodeploy e configurar os recursos de rede.

## <a name="Connectivity"></a>Conectividade entre recursos do Azure

Os recursos do Azure, as Máquinas Virtuais, os Serviços de Nuvem, os Conjuntos de Dimensionamento de Máquinas Virtuais e os Ambientes do Serviço de Aplicativo do Azure, podem se comunicar entre si de forma privada por meio de uma VNet (rede virtual) do Azure. Uma rede virtual é uma isolamento lógico de saudação nuvem do Azure dedicado tooyour [assinatura](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fnetworking%2ftoc.json). É possível implementar várias VNets dentro de cada assinatura e [região](https://azure.microsoft.com/regions) do Azure. Cada VNet é isolada de outras VNets. Para cada VNet, você pode:

- Especificar um espaço de endereço IP privado personalizado usando endereços públicos e privados (RFC 1918). Azure atribui recursos conectados toohello VNet um endereço IP privado de espaço de endereço Olá que você atribuir.
- Olá rede virtual em uma ou mais sub-redes de segmento e alocar uma parte da sub-rede de tooeach espaço do endereço de rede virtual hello.
- Usar a resolução de nomes fornecida pelo Azure ou especifique seu próprio servidor DNS para uso por recursos conectado tooa VNet.

toolearn mais sobre o serviço de rede Virtual do Azure hello, ler Olá [visão geral da rede Virtual](../virtual-network/virtual-networks-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo. Você pode se conectar a VNets tooeach outras, permitindo que recursos conectados tooeither VNet toocommunicate uns com os outros em VNets. Você pode usar um ou ambos Olá opções tooconnect VNets tooeach outros a seguir:

- **Emparelhamento:** habilita recursos conectado toodifferent VNets do Azure em Olá mesmo toocommunicate região do Azure com o outro. Olá largura de banda e latência entre Olá VNets é Olá mesmo que recursos Olá toohello conectado mesma rede virtual. toolearn mais sobre o emparelhamento, ler Olá [visão geral emparelhamento de rede Virtual](../virtual-network/virtual-network-peering-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.
- **Gateway VPN:** habilita recursos conectado toodifferent VNets do Azure em diferentes regiões do Azure toocommunicate entre si. O tráfego entre as VNets flui por meio de um Gateway de VPN do Azure. Entre os VNets é toohello limitada largura de banda do gateway de saudação. toolearn mais sobre a conexão VNets com um Gateway de VPN, ler Olá [configurar uma conexão de rede virtual a rede entre regiões](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.

## <a name="internet-connectivity"></a>Conectividade com a Internet

Todos os recursos do Azure, tooa conectado VNet ter conectividade de saída toohello da Internet por padrão. endereço IP privado de saudação do recurso de saudação é o endereço de rede de origem convertido endereço IP público de tooa (SNAT) por Olá infraestrutura do Azure. toolearn mais sobre a conectividade da Internet de saída, ler Olá [Noções básicas sobre conexões de saída no Azure](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.

toocommunicate tooAzure recursos de saudação da Internet ou toocommunicate toohello saída Internet sem SNAT, um recurso deve ser atribuída um endereço IP público de entrada. toolearn mais informações sobre endereços IP públicos, ler Olá [endereços IP públicos](../virtual-network/virtual-network-public-ip-address.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.

## <a name="on-premises-connectivity"></a>Conectividade local

Você pode acessar os recursos de sua VNet com segurança por meio de uma conexão VPN ou de uma conexão privada direta. toosend o tráfego de rede entre sua rede virtual do Azure e sua rede local, você deve criar um gateway de rede virtual. Você define configurações para o tipo de saudação de toocreate Olá gateway de conexão que você quer, VPN ou rota expressa.

Você pode conectar seu tooa de rede local VNet usando qualquer combinação de saudação as opções a seguir:

**Ponto a site (VPN sobre SSTP)**

Olá figura abaixo mostra as conexões de toosite separado do ponto entre vários computadores e uma rede virtual:

![Point-to-site](./media/networking-overview/point-to-site.png)

Essa conexão é estabelecida entre um único computador e uma VNet. Esse tipo de conexão é ótimo se você estiver apenas começando com o Azure, ou para os desenvolvedores, porque ele requer pouca ou nenhuma alterações tooyour rede. Ele também é conveniente quando você está se conectando de um local remoto, como uma conferência ou sua casa. Conexões ponto a site são geralmente associadas a uma conexão site a site por meio de saudação mesmo gateway de rede virtual. conexão Olá usa a comunicação de tooprovide criptografado de protocolo SSTP Olá Olá Internet entre o computador hello e Olá VNet. latência de saudação para uma VPN ponto a site é imprevisível, desde que o tráfego de saudação atravessa Olá Internet.

**Site a site (túnel VPN IPsec/IKE)**

![Site a site](./media/networking-overview/site-to-site.png)

Essa conexão é estabelecida entre o dispositivo VPN local e um Gateway de VPN do Azure. Esse tipo de conexão permite que qualquer recurso local que você autorize Olá tooaccess VNet. conexão de saudação é uma VPN IPSec/IKE que fornece comunicação criptografada sobre Olá Internet entre o dispositivo local e o gateway de VPN do Azure hello. Você pode se conectar a vários toohello de sites no local mesmo gateway VPN. Olá dispositivo VPN em cada site deve ter um endereço IP externamente voltados ao público que não estiver por trás de um NAT. ao local latência de saudação para uma conexão site a site é imprevisível, desde que o tráfego de saudação atravessa Olá Internet.

**ExpressRoute (conexão privada dedicada)**

![ExpressRoute](./media/networking-overview/expressroute.png)

Esse tipo de conexão é estabelecida entre sua rede e o Azure, por meio de um parceiro do ExpressRoute. Essa conexão é privada. O tráfego não atravessa Olá da Internet. latência de saudação para uma conexão de rota expressa é previsível, desde que o tráfego não atravessam a saudação da Internet. O ExpressRoute pode ser combinado a uma conexão site a site.

toolearn mais informações sobre todos os Olá conexão opções anteriores, leia Olá [diagramas de topologia de Conexão](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.

## <a name="load-balancing"></a>Direção do tráfego e balanceamento de carga

O Microsoft Azure fornece vários serviços para gerenciar a forma como o tráfego de rede é distribuído e como sua carga é balanceada. Você pode usar qualquer um dos Olá recursos a seguir separadamente ou em conjunto:

**Balanceamento de carga DNS**

saudação de serviço do Azure Traffic Manager fornece balanceamento de carga global do DNS. Gerenciador de tráfego responde tooclients com o endereço IP de saudação de um ponto de extremidade íntegro, com base em uma saudação métodos de roteamento a seguir:
- **Geográfico:** os clientes são direcionados a pontos de extremidade toospecific (Azure, externo ou aninhado) com base na qual localização geográfica sua consulta DNS se origina. Esse método habilita cenários em que conhecer a região geográfica do cliente e roteá-lo com base nisso, é importante. Os exemplos incluem conformidade com normas de soberania de dados, localização de conteúdo e experiência do usuário, bem como medição do tráfego de diferentes regiões.
- **Desempenho:** endereço IP de saudação retornado toohello cliente é o cliente de toohello "mais próximo" hello. ponto de extremidade 'mais próximo' Hello não é necessariamente mais próximo, conforme medido pela distância geográfica. Em vez disso, este método determina o ponto de extremidade mais próximo Olá medindo a latência de rede. Gerenciador de tráfego mantém um horário da Internet latência tabela tootrack Olá ida e volta entre os intervalos de endereços IP e cada data center do Azure.
- **Prioridade:** tráfego é direcionado toohello primário (prioridade mais alta-). Se o ponto de extremidade Olá primário não estiver disponível, o Gerenciador de tráfego rotas Olá segundo ponto de extremidade do tráfego toohello. Se ambos os pontos de extremidade primário e secundário Olá não estiverem disponíveis, o tráfego de saudação vai toohello em terceiro lugar, e assim por diante. Disponibilidade do ponto de extremidade de saudação é com base no status de saudação configurada (habilitado ou desabilitado) e Olá monitoramento de ponto de extremidade em andamento.
- **Round-robin ponderado:** para cada solicitação, o Gerenciador de Tráfego escolhe aleatoriamente um ponto de extremidade disponível. probabilidade de saudação de escolher um ponto de extremidade baseia-se em Olá pesos atribuídos tooall pontos de extremidade disponíveis. Mesmo usando Olá peso em todos os resultados de pontos de extremidade em um mesmo a distribuição de tráfego. Usando pesos superior ou inferiores em pontos de extremidade específicos faz com que esses toobe de pontos de extremidade mais ou menos frequente retornados em respostas DNS de saudação.

Olá figura abaixo mostra uma solicitação para um aplicativo direcionado de web tooa ponto de extremidade do aplicativo Web. Os pontos de extremidade também podem ser outros serviços do Azure, como VMs e serviços de nuvem.

![Gerenciador de Tráfego](./media/networking-overview/traffic-manager.png)

Olá se conecta diretamente toothat de ponto de extremidade. O Azure Traffic Manager detecta quando um ponto de extremidade não está íntegro e, em seguida, redireciona os clientes tooa diferentes Íntegro ponto de extremidade. toolearn mais sobre o Gerenciador de tráfego, ler Olá [visão geral do Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.

**Balanceamento de carga do aplicativo**

Olá serviço de Gateway de aplicativo do Azure fornece o controlador de entrega de aplicativos (ADC) como um serviço. Application Gateway oferece diversos recursos de balanceamento de carga de camada 7 (HTTP/HTTPS) para seus aplicativos, incluindo um aplicativo web firewall tooprotect seus aplicativos web de vulnerabilidades e explorações. Application Gateway também permite que você produtividade de farm da web toooptimize descarregando gateway de aplicativo de toohello de terminação SSL de uso intensivo de CPU. 

Outros recursos de roteamento de camada 7 incluem round-robin distribuição de tráfego de entrada, a afinidade de sessão baseada em cookie, roteamento baseado no caminho de URL e Olá capacidade toohost vários sites por trás de um gateway de aplicativo único. O Gateway de Aplicativo pode ser configurado como um gateway voltado para a Internet, um gateway apenas interno ou uma combinação de ambos. O Gateway de Aplicativo é totalmente gerenciado pelo Azure, escalonável e altamente disponível. Ele fornece um conjunto avançado de recursos de log e diagnósticos para melhor capacidade de gerenciamento. toolearn mais sobre o Application Gateway, ler Olá [visão geral do Application Gateway](../application-gateway/application-gateway-introduction.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.

Olá imagem a seguir mostra URL de roteamento com o Application Gateway baseadas em caminhos:

![Gateway de Aplicativo](./media/networking-overview/application-gateway.png)

**Balanceamento de carga de rede**

Olá balanceador de carga do Azure oferece alto desempenho e baixa latência camada 4 balanceamento de carga para todos os protocolos TCP e UDP. Ele gerencia conexões de entrada e saída. Você pode configurar pontos de extremidade com balanceamento de carga públicos e internos. Você pode definir regras toomap destinos de pool de tooback a fim de conexões de entrada usando TCP e HTTP de investigação de integridade opções toomanage disponibilidade do serviço. toolearn mais sobre o balanceador de carga, ler Olá [visão geral do balanceador de carga](../load-balancer/load-balancer-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.

Olá figura abaixo mostra um aplicativo de várias camado para a Internet que utiliza a ambos os balanceadores de carga interno e externo:

![Balanceador de carga](./media/networking-overview/load-balancer.png)

## <a name="security"></a>Segurança

Você pode filtrar o tráfego tooand de recursos do Azure usando Olá as opções a seguir:

- **Rede:** você pode implementar toofilter de grupos (NSGs) de segurança de rede do Azure de entrada e saída de tráfego tooAzure recursos. Cada NSG contém uma ou mais regras de entrada e saída. Cada regra especifica os endereços IP de origem hello, endereços IP de destino, porta e protocolo que o tráfego é filtrado com. Os NSGs podem ser aplicadas tooindividual sub-redes e VMs individuais. toolearn mais sobre os NSGs, ler Olá [visão geral de grupos de segurança de rede](../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.
- **Aplicativo:** usando um Gateway de Aplicativo com o firewall do aplicativo Web, você pode proteger seus aplicativos Web contra vulnerabilidades e explorações. Exemplos comuns são ataques de injeção SQL, scripts entre sites e cabeçalhos mal formados. O gateway de aplicativo filtra esse tráfego e o impede de chegar a seus servidores Web. Você é capaz de tooconfigure quais regras que devem ser habilitados. as diretivas de negociação SSL de tooconfigure capacidade Olá é fornecida tooallow certas políticas toobe desabilitado. toolearn mais sobre o firewall do aplicativo web hello, ler Olá [firewall do aplicativo Web](../application-gateway/application-gateway-web-application-firewall-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.

Se você precisar de funcionalidade de rede Azure não forneça ou deseja usar locais de aplicativos de rede toouse, você pode implementar produtos Olá em máquinas virtuais e conectá-los tooyour VNet. Olá [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/category/networking?page=1&subcategories=appliances) contém várias VMs diferentes pré-configuradas com aplicativos de rede, você pode usar no momento. Essas VMs pré-configurados são geralmente referidos tooas as soluções de virtualização de rede (NVA). As NVAs estão disponíveis com aplicativos como otimização de WAN e firewall.

## <a name="routing"></a>Roteamento

O Azure cria padrão tabelas de rotas que habilitam recursos tooany conectado sub-rede em qualquer toocommunicate VNet entre si. Você pode implementar uma ou ambas Olá seguintes tipos de rotas toooverride hello Azure cria as rotas padrão:
- **Definido pelo usuário:** você pode criar tabelas de rota personalizados com rotas que controlam onde o tráfego é roteado toofor cada sub-rede. toolearn mais sobre as rotas definidas pelo usuário, ler Olá [rotas definidas pelo usuário](../virtual-network/virtual-networks-udr-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.
- **(BGP) Border gateway protocol:** se você se conectar a sua rede de local de tooyour de rede virtual usando uma conexão de Gateway de VPN do Azure, ou rota expressa, você pode propagar rotas BGP tooyour VNets. O BGP é Olá protocolo de roteamento padrão usado em Olá tooexchange roteamento e acessibilidade informações da Internet entre duas ou mais redes. Quando usados no contexto de saudação de redes virtuais do Azure, BGP habilita Olá Gateways de VPN do Azure e os dispositivos VPN local, chamado BGP correspondentes ou vizinhos, tooexchange "roteia" que informam os dois gateways sobre acessibilidade para os prefixos e a disponibilidade de saudação toogo por meio de gateways de saudação ou roteadores envolvidos. BGP também pode habilitar o roteamento de tráfego entre várias redes propagando rotas aprende um gateway BGP de um tooall de par BGP outros pares de BGP. toolearn mais sobre o BGP, consulte Olá [BGP visão geral de Gateways de VPN do Azure](../vpn-gateway/vpn-gateway-bgp-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.

## <a name="manageability"></a>Capacidade de gerenciamento

O Azure fornece o seguinte Olá ferramentas toomonitor e gerenciar a rede:
- **Logs de atividade:** recursos do Azure todos os tem registros de atividades que fornecem informações sobre as operações executadas colocar, status de operações e quem iniciou a operação de saudação. toolearn mais sobre os logs de atividade, ler Olá [visão geral dos logs de atividades](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.
- **Logs de diagnóstico:** periódica e espontâneas eventos são criados por recursos de rede e registrados em contas de armazenamento do Azure, enviados tooan Hub de eventos do Azure ou enviados tooAzure análise de Log. Logs de diagnóstico fornecem integridade de toohello de informações de um recurso. Os logs de diagnóstico são fornecidos para o Balanceador de Carga (voltado para a Internet), Grupos de Segurança de Rede, rotas e o Gateway de Aplicativo. toolearn mais informações sobre logs de diagnóstico, ler Olá [visão geral de logs de diagnóstico](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.
- **Métricas:** as métricas são contadores e medidas de desempenho coletados durante um período. Métricas podem ser usados tootrigger alertas com base nos limites. Atualmente, as métricas estão disponíveis para o Gateway de Aplicativo. toolearn mais informações sobre métricas, ler Olá [visão geral das métricas](../monitoring-and-diagnostics/monitoring-overview-metrics.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.
- **Solução de problemas:** informações de solução de problemas pode ser acessada diretamente no hello portal do Azure. informações de saudação ajuda a diagnosticar problemas comuns de rota expressa, Gateway de VPN, Application Gateway, os Logs de segurança de rede, rotas, DNS, balanceador de carga e Gerenciador de tráfego.
- **RBAC (controle de acesso baseado em função):** controle quem pode criar e gerenciar recursos de rede com o RBAC (controle de acesso baseado em função). Saiba mais sobre o RBAC lendo Olá [Introdução ao RBAC](../active-directory/role-based-access-control-what-is.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo. 
- **Captura de pacote:** Olá observador de rede do Azure fornece serviço Olá toorun de capacidade de captura de um pacote em uma máquina virtual por meio de uma extensão em Olá VM. Essa funcionalidade está disponível para VMs Linux e Windows. toolearn mais informações sobre captura de pacote, ler Olá [visão geral de captura de pacote](../network-watcher/network-watcher-packet-capture-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.
- **Verifique se os fluxos IP:** observador de rede permite que você tooverify IP fluxos entre uma VM do Azure e um recurso remoto toodetermine se os pacotes são permitidas ou negadas. Esse recurso fornece aos administradores a capacidade de saudação tooquickly diagnosticar problemas de conectividade. toolearn mais sobre como o IP tooverify flui ler Olá [fluxo IP verificar a visão geral](../network-watcher/network-watcher-ip-flow-verify-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.
- **Solucionar problemas de conectividade VPN:** Olá capacidade de solução de problemas VPN do observador de rede fornece Olá capacidade tooquery uma conexão ou o gateway e verificar a integridade de saudação de recursos de saudação. toolearn mais sobre como solucionar problemas de conexões de VPN, ler Olá [visão geral de solução de problemas de conectividade VPN](../network-watcher/network-watcher-troubleshoot-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.
- **Exibir a topologia de rede:** exibir uma representação gráfica dos recursos de rede de saudação em uma rede virtual com o observador de rede. mais sobre a exibição de topologia de rede, leia a saudação de toolearn [visão geral da topologia](../network-watcher/network-watcher-topology-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.

## <a name="tools"></a>Ferramentas de implantação e configuração

Você pode implantar e configurar recursos de rede do Azure com qualquer Olá ferramentas a seguir:

- **Portal do Azure:** uma interface gráfica do usuário que é executada em um navegador. Olá abrir [portal do Azure](http://portal.azure.com).
- **Azure PowerShell:** ferramentas de linha de comando para gerenciar o Azure de computadores Windows. Saiba mais sobre o Azure PowerShell por leitura Olá [visão geral do Azure PowerShell](/powershell/azure/overview?view=azurermps-3.8.0?toc=%2fazure%2fnetworking%2ftoc.json) artigo.
- **CLI (interface de linha de comando) do Azure:** ferramentas de linha de comando para gerenciar o Azure de computadores Windows, Linux ou macOS. Saiba mais sobre Olá CLI do Azure por leitura Olá [visão geral da CLI do Azure](/cli/azure/get-started-with-azure-cli?toc=%2fazure%2fnetworking%2ftoc.json) artigo.
- **Modelos do Gerenciador de recursos do Azure:** um arquivo (em formato JSON) que define a infraestrutura de saudação e a configuração de uma solução do Azure. Usando um modelo, você pode implantar a solução repetidamente em todo seu ciclo de vida e com a confiança de que seus recursos serão implantados em um estado consistente. toolearn mais sobre a criação de modelos, ler Olá [práticas recomendadas para a criação de modelos](../azure-resource-manager/resource-manager-template-best-practices.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo. Modelos podem ser implantados com hello portal do Azure, CLI ou o PowerShell. tooget iniciado imediatamente, com modelos de implantar uma saudação muitos modelos pré-configurados em Olá [modelos de início rápido do Azure](https://azure.microsoft.com/resources/templates/?term=network) biblioteca. 

## <a name="pricing"></a>Preços

Alguns dos hello Azure serviços de rede têm um encargo, enquanto outras são gratuitas. Saudação de exibição [rede Virtual](https://azure.microsoft.com/pricing/details/virtual-network), [Gateway VPN](https://azure.microsoft.com/pricing/details/vpn-gateway), [Application Gateway](https://azure.microsoft.com/en-us/pricing/details/application-gateway/), [balanceador de carga](https://azure.microsoft.com/pricing/details/load-balancer), [doobservadorderede](https://azure.microsoft.com/pricing/details/network-watcher), [DNS](https://azure.microsoft.com/pricing/details/dns), [Traffic Manager](https://azure.microsoft.com/pricing/details/traffic-manager) e [ExpressRoute](https://azure.microsoft.com/pricing/details/expressroute) preços páginas para obter mais informações.

## <a name="next-steps"></a>Próximas etapas

- Criar sua primeira NET e conectar alguns tooit de VMs, concluindo as etapas Olá Olá [criar sua primeira rede virtual](../virtual-network/virtual-network-get-started-vnet-subnet.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.
- Conectar-se a sua rede virtual de tooa do computador completando as etapas de saudação do hello [configurar uma conexão ponto a site](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.
- Servidores da Internet toopublic do tráfego de balanceamento de carga completando as etapas de saudação do hello [criar um balanceador de carga para a Internet](../load-balancer/load-balancer-get-started-internet-portal.md?toc=%2fazure%2fnetworking%2ftoc.json) artigo.
