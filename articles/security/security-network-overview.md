---
title: "aaaNetwork requisitos no Azure e conceitos de segurança | Microsoft Docs"
description: " Este artigo torna mais fácil para você toounderstand o Microsoft Azure tem toooffer na área de saudação de segurança de rede. Oferecemos básicas explicações para os conceitos básicos de segurança de rede e os requisitos e obter informações sobre o Azure tem toooffer em cada uma dessas áreas. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: bedf411a-0781-47b9-9742-d524cf3dbfc1
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: terrylan
ms.openlocfilehash: 87d336064b880ddcf90ae4fcb79b7823367682b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-network-security-overview"></a>Azure Network Security Overview (Visão geral da segurança de rede do Azure)
Microsoft Azure inclui um toosupport robusta de infraestrutura de rede de seu aplicativo e os requisitos de conectividade do serviço. Conectividade de rede é possível entre os recursos localizados no Azure, entre locais e hospedado do Azure, recursos e tooand de saudação à Internet e o Azure.

Olá objetivo deste artigo é toomake mais fácil para você toounderstand o Microsoft Azure tem toooffer na área de saudação da segurança de rede. Aqui, fornecemos explicações básicas sobre os principais requisitos e conceitos de segurança de rede. Nós também fornecemos informações para você no Azure tem toooffer em cada uma dessas áreas, bem como links toohelp obter uma compreensão mais profunda das áreas de interesse.

Este artigo de visão geral de segurança de rede do Azure enfoca Olá áreas a seguir:

* Rede do Azure
* Controle de acesso à rede
* Acesso remoto seguro e conectividade entre instalações
* Disponibilidade
* Resolução de nomes
* Arquitetura do DMZ
* Monitoramento e detecção de ameaças


## <a name="azure-networking"></a>Rede do Azure
As máquinas virtuais precisam de conectividade de rede. toosupport esse requisito, o Azure requer toobe de máquinas virtuais conectada tooan rede Virtual do Azure. Uma rede Virtual do Azure é um constructo lógico criado com base em malha de rede do Azure física hello. Cada Rede Virtual do Azure lógica é isolada das todas as outras Redes Virtuais do Azure. Isso ajuda a garantir que o tráfego de rede em suas implantações não é os clientes do Microsoft Azure tooother acessível.

Saiba mais:

* [Visão geral da Rede Virtual](../virtual-network/virtual-networks-overview.md)


## <a name="network-access-control"></a>Controle de acesso à rede
Controle de acesso de rede é o ato de saudação de limitar tooand de conectividade de dispositivos específicos ou sub-redes em uma rede Virtual do Azure. meta de saudação do controle de acesso de rede é acessar toolimit tooyour as máquinas virtuais e os usuários tooapproved de serviços e dispositivos. Controles de acesso baseados em permitir ou negar decisões para conexões tooand de sua máquina virtual ou serviço.

O Azure dá suporte a vários tipos de controle de acesso à rede como:

* Controle de camada de rede
* Controle de rota e túnel forçado
* Dispositivos de segurança de rede virtual

### <a name="network-layer-control"></a>Controle de camada de rede
Qualquer implantação segura requer alguma medida de controle de acesso à rede. meta de saudação do controle de acesso de rede é toorestrict máquina virtual toohello necessário os sistemas de comunicação e que outras tentativas de comunicação estão bloqueadas.

Se você precisar de controle de acesso no nível de rede básica (com base no endereço IP e Olá TCP ou protocolos UDP), você pode usar grupos de segurança de rede. Um grupo de segurança de rede (NSG) é um pacote com monitoração de estado básico firewall de filtragem e permite que você toocontrol acesso com base em um [5-tupla](https://www.techopedia.com/definition/28190/5-tuple). Os NSGs não fornecem inspeção da camada de aplicativo nem controles de acesso autenticado.

Saiba mais:

* [Grupos de segurança de rede](../virtual-network/virtual-networks-nsg.md)

### <a name="route-control-and-forced-tunneling"></a>Controle de rota e túnel forçado
Olá capacidade toocontrol comportamento de roteamento em suas redes virtuais do Azure é um recurso de controle de acesso e segurança críticas de rede. Se o roteamento está configurado incorretamente, aplicativos e serviços hospedados em sua máquina virtual podem conectar dispositivos toounauthorized incluindo sistemas de propriedade e operada por invasores.

Rede do Azure oferece suporte ao comportamento de roteamento do hello capacidade toocustomize Olá para o tráfego de rede em suas redes virtuais do Azure. Isso permite que você tooalter saudação padrão roteamento entradas da tabela em sua rede Virtual do Azure. O controle do comportamento de roteamento ajuda a garantir que todo o tráfego de determinado dispositivo ou grupo de dispositivos entra ou sai da rede virtual por meio de um local específico.

Por exemplo, você pode ter um dispositivo de segurança de rede virtual em sua Rede Virtual do Azure. Você deseja toomake-se de que todos os tooand de tráfego de rede Virtual do Azure passa por esse dispositivo de segurança virtual. É possível fazer isso configurando as [Rotas Definidas pelo Usuário](../virtual-network/virtual-networks-udr-overview.md) no Azure.

[Encapsulamento forçado](https://www.petri.com/azure-forced-tunneling) é um mecanismo que você pode usar tooensure seus serviços não são permitidos tooinitiate toodevices uma conexão em Olá da Internet. Observe que isso é diferente de aceitar conexões de entrada e, em seguida, responder toothem. Servidores web front-end precisam toorequests toorespond de hosts da Internet, e para que o tráfego originado de Internet é permitido servidores da web de entrada toothese e Olá web são permitidas toorespond.

O que você não deseja tooallow é um servidor de front-end web tooinitiate uma solicitação de saída. Essas solicitações podem representar um risco de segurança porque essas conexões podem ser usado toodownload malware. Mesmo se você desejar que eles front-end servidores tooinitiate saída solicitações toohello da Internet, você pode querer tooforce-los toogo por meio do seu local proxies da web para que você pode tirar proveito da URL de filtragem e log.

Em vez disso, você desejaria toouse forçado túnel tooprevent isso. Quando você habilita o túnel forçado, todas as conexões toohello Internet são forçadas por meio de seu gateway local. É possível configurar o túnel forçado utilizando as Rotas Definidas pelo Usuário.

Saiba mais:

* [O que são Rotas Definidas pelo Usuário e Encaminhamento de IP](../virtual-network/virtual-networks-udr-overview.md)

### <a name="virtual-network-security-appliances"></a>Dispositivos de segurança de rede virtual
Enquanto o túnel forçado, rotas definidas pelo usuário e grupos de segurança de rede fornecem um nível de segurança em camadas de transporte e de rede de saudação do hello [modelo OSI](https://en.wikipedia.org/wiki/OSI_model), pode haver ocasiões em que você deseja tooenable segurança em níveis mais altos de rede hello.

Por exemplo, seus requisitos de segurança podem incluir:

* Autenticação e autorização antes de permitir acesso tooyour aplicativo
* Detecção de intrusões e resposta a intrusões
* Inspeção da camada do aplicativo para os protocolos de nível alto
* Filtragem de URL
* Antimalware e antivírus no nível de rede
* Proteção contra bots
* Controle de acesso de aplicativo
* Proteção DDoS adicional (acima Olá proteção fornecida Olá DDoS malha do Azure em si)

É possível acessar esses recursos avançados de segurança de rede por meio de uma solução de parceiros do Azure. Você pode encontrar hello mais recentes soluções de segurança de rede de parceiro do Azure, visitando Olá [Azure Marketplace](https://azure.microsoft.com/marketplace/) e a pesquisa de "segurança" e "segurança de rede".

## <a name="secure-remote-access-and-cross-premises-connectivity"></a>Acesso remoto seguro e conectividade entre instalações
Instalação, configuração e gerenciamento de recursos do Azure precisa toobe feita remotamente. Além disso, você pode desejar toodeploy [TI híbrida](http://social.technet.microsoft.com/wiki/contents/articles/18120.hybrid-cloud-infrastructure-design-considerations.aspx) soluções que têm componentes locais e na nuvem pública do Azure de saudação. Esses cenários exigem o acesso remoto seguro.

Rede do Azure dá suporte a saudação os seguintes cenários de acesso remoto:

* Conecte-se de estações de trabalho individuais tooan rede Virtual do Azure
* Conecte-se a sua rede de local tooan rede Virtual do Azure com uma VPN
* Conecte-se a sua rede de local tooan rede Virtual do Azure com uma conexão WAN dedicada
* Conectar redes virtuais do Azure tooeach outros

### <a name="connect-individual-workstations-tooan-azure-virtual-network"></a>Conecte-se de estações de trabalho individuais tooan rede Virtual do Azure
Pode haver ocasiões em que você deseja tooenable individuais desenvolvedores ou operações equipe toomanage máquinas virtuais e serviços no Azure. Por exemplo, você precisa acessar a máquina de virtual tooa em uma rede Virtual do Azure e sua política de segurança não permitir que o acesso remoto RDP ou SSH tooindividual máquinas virtuais. Nesse caso, você pode usar uma conexão VPN ponto a site.

Olá conexão VPN usa Olá ponto a site [SSTP VPN](https://technet.microsoft.com/library/cc731352.aspx) protocolo tooenable você tooset se uma conexão privada e segura entre o usuário hello e hello rede Virtual do Azure. Após o estabelecimento de conexão de VPN Olá Olá será capaz de tooRDP ou SSH sobre Olá VPN link em qualquer máquina virtual hello (supondo que hello usuário pode autenticar e é autorizado) de rede Virtual do Azure.

Saiba mais:

* [Configurar um tooa de Conexão de ponto para Site de rede Virtual usando o PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

### <a name="connect-your-on-premises-network-tooan-azure-virtual-network-with-a-vpn"></a>Conecte-se a sua rede local tooan rede Virtual do Azure com uma VPN
Você talvez queira tooconnect sua toda a rede corporativa, ou partes dele, tooan rede Virtual do Azure. Isso é comum em cenários de TI híbrida, em que as empresas [estendem seu data center local para o Azure](https://gallery.technet.microsoft.com/Datacenter-extension-687b1d84). Em muitos casos, as empresas hospedarão algumas partes de um serviço no Azure e outras localmente, por exemplo, quando uma solução inclui servidores Web front-end no Azure e bancos de dados back-end localmente. Esses tipos de conexões “entre instalações” também tornam o gerenciamento dos recursos localizados no Azure mais seguros e possibilitam cenários como a extensão dos controladores de domínio do Active Directory para o Azure.

Uma maneira tooaccomplish trata toouse um [VPN site a site](https://www.techopedia.com/definition/30747/site-to-site-vpn). diferença de saudação entre uma VPN site a site e uma VPN ponto a site é uma VPN ponto a site se conecta tooan um único dispositivo Rede Virtual do Azure, enquanto uma VPN site a site se conecta a uma rede Virtual do Azure de tooan de toda a rede (por exemplo, sua rede local) . Tooan de VPNs site a site rede Virtual do Azure use Olá altamente seguro IPsec túnel VPN protocolo em modo.

Saiba mais:

* [Criar uma VNet do Gerenciador de recursos com uma conexão de VPN site a site usando Olá Portal do Azure](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [Planejamento e design para o Gateway de VPN](../vpn-gateway/vpn-gateway-plan-design.md)

### <a name="connect-your-on-premises-network-tooan-azure-virtual-network-with-a-dedicated-wan-link"></a>Conectar-se a sua rede Virtual do Azure de tooan de rede local com um Link de WAN dedicado
As conexões VPN ponto a site e site a site são eficazes para habilitar a conectividade entre instalações. No entanto, algumas organizações considerar Olá toohave seguintes desvantagens:

* Conexões VPN de mover dados Olá Internet – isso expõe esses problemas de segurança de toopotential conexões envolvidos na movimentação de dados em uma rede pública. Além disso, a confiabilidade e a disponibilidade de conexões com a Internet não podem ser garantidas.
* Conexões de VPN tooAzure redes virtuais pode ser considerado restrita para alguns aplicativos e fins, como eles max out a cerca de 200 Mbps de largura de banda.

As organizações que precisam Olá nível mais alto de segurança e disponibilidade para suas conexões entre locais normalmente usar links WAN dedicados tooconnect tooremote sites. O Azure fornece que Olá capacidade toouse um link WAN dedicado que você pode usar tooconnect tooan de rede seu local na rede Virtual do Azure. Isso é habilitado por meio da Azure ExpressRoute.

Saiba mais:

* [Visão Geral Técnica do ExpressRoute](../expressroute/expressroute-introduction.md)

### <a name="connect-azure-virtual-networks-tooeach-other"></a>Conectar redes virtuais do Azure tooEach outros
É possível que você toouse várias redes virtuais do Azure para suas implantações. Há muitas razões pelas quais você poderia fazer isso. Pode ter um dos motivos Olá gerenciamento toosimplify; outra pode ser por motivos de segurança. Independentemente de motivação hello ou lógica para colocar recursos em diferentes redes virtuais do Azure, pode haver ocasiões em que você deseja recursos em cada Olá redes tooconnect uns com os outros.

Uma opção seria para serviços em um tooservices tooconnect de rede Virtual do Azure em outra rede Virtual do Azure por "loop volta" por meio de saudação à Internet. conexão Olá seria Iniciar em uma rede Virtual do Azure, percorrer Olá Internet e vir toohello destino rede Virtual do Azure. Esta opção apresenta problemas Olá conexão toohello segurança inerente tooany comunicação baseado na Internet.

Uma opção melhor seria toocreate um Azure Virtual VPN de site a site de rede de Virtual de rede para o Azure. Esta rede Virtual do Azure Virtual Network para o Azure usa VPN site a site Olá mesmo [modo de túnel IPsec](https://technet.microsoft.com/library/cc786385.aspx) protocolo como as conexão de VPN site a site entre locais Olá mencionado acima.

Olá vantagem usando um Azure Virtual VPN de site a site de rede de Virtual de rede para o Azure é que conexão de VPN Olá estabelecido pela Olá malha de rede do Azure, em vez de conectar-se via Olá da Internet. Isso fornece a você uma camada extra de segurança em comparação com VPNs site toosite que se conectam pela Internet de saudação.

Saiba mais:

* [Configurar uma conexão de rede virtual com rede virtual usando o PowerShell e o Azure Resource Manager](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

## <a name="availability"></a>Disponibilidade
A disponibilidade é um componente fundamental de qualquer programa de segurança. Se seus sistemas e usuários não podem acessar o que eles precisam tooaccess sobre Olá de rede, hello serviço pode ser considerado comprometidos. O Azure tem tecnologias de rede que Olá suporte a mecanismos de alta disponibilidade a seguir:

* Balanceamento de carga baseado em HTTP
* Balanceamento de carga no nível de rede
* Balanceamento de carga global

Balanceamento de carga é um mecanismo projetado tooequally distribuir conexões entre vários dispositivos. Olá objetivos de balanceamento de carga são:

* Aumentar a disponibilidade – quando você carregar o saldo conexões em vários dispositivos, um ou mais dos dispositivos Olá podem se tornar indisponível e serviços de saudação em execução no hello restantes dispositivos on-line podem continuar tooserve conteúdo de saudação do serviço de saudação
* Aumentar o desempenho – quando você carrega o saldo conexões em vários dispositivos, um único dispositivo não tem o processador de saudação tootake atingido. Em vez disso, Olá demandas de processamento e memória para que serve o conteúdo de saudação é distribuído em vários dispositivos.

### <a name="http-based-load-balancing"></a>Balanceamento de carga baseado em HTTP
Organizações que executam serviços baseados na web muitas vezes desejo toohave um balanceador de carga com base em HTTP na frente esses toohelp de serviços web garantir níveis adequados de desempenho e alta disponibilidade. Em contraste tootraditional baseados em rede balanceadores de carga, hello decisões de balanceamento de carga feitas por balanceadores de carga com base em HTTP são baseadas em características do protocolo de saudação HTTP, não em protocolos de camada de transporte e rede hello.

tooprovide você com base em HTTP balanceamento de carga para seus serviços baseados na web, o Azure fornece hello Azure Application Gateway. saudação de Gateway de aplicativo do Azure oferece suporte a:

* Com base em HTTP balanceamento de carga – decisões de balanceamento de carga são feitas com base no protocolo toohello característica especial HTTP
* Afinidade de sessão baseada em cookie – esse recurso torna-se de que as conexões estabelecidas tooone dos servidores de saudação por trás do balanceador de carga que permanece intacta entre servidor e cliente hello. Isso assegura a estabilidade das transações.
* Descarregamento SSL – quando uma conexão de cliente é estabelecida com o balanceador de carga hello, que sessão entre o cliente hello e balanceador de carga de saudação é criptografado usando Olá HTTPS (SSL /) protocolo. No entanto, no desempenho de tooincrease ordem, você tem conexão de saudação do hello opção toohave entre balanceador de carga de saudação e o servidor de web de saudação atrás de protocolo hello HTTP (sem criptografia) do uso de Balanceador de carga hello. Isso é chamado tooas "descarregamento SSL" porque os servidores de web hello por trás do balanceador de carga de saudação não enfrentar sobrecarga do processador Olá envolvida com a criptografia e, portanto, devem ser capaz de tooservice solicitações mais rapidamente.
* URL de roteamento baseado em conteúdo – este recurso torna possível para decisões de toomake de Balanceador de carga de saudação em onde tooforward conexões com base na URL de destino de saudação. Isso oferece muito mais flexibilidade do que as soluções que tomam decisões de balanceamento de carga de acordo com os endereços IP.

Saiba mais:

* [Visão geral do Gateway de Aplicativo](../application-gateway/application-gateway-introduction.md)

### <a name="network-level-load-balancing"></a>Balanceamento de carga no nível de rede
Em contraste com base em tooHTTP balanceamento de carga e balanceamento de carga nível da rede torna com base no endereço IP e porta (TCP ou UDP) números de decisões de balanceamento de carga.
Você pode obter benefícios de saudação do nível balanceamento de carga no Azure usando Olá balanceador de carga do Azure. Algumas características principais de saudação balanceador de carga do Azure incluem:

* Balanceamento de carga no nível de rede de acordo com o endereço IP e números de porta
* Suporte para qualquer protocolo de camada de aplicativo
* Balanceamento de carga de máquinas virtuais de tooAzure e instâncias de função de serviços de nuvem
* Pode ser usado para aplicativos e máquinas virtuais para a Internet (balanceamento de carga externo) e não voltadas à Internet (balanceamento de carga interno)
* Ponto de extremidade de monitoramento, que é usado toodetermine se qualquer um dos serviços de saudação por trás do balanceador de carga Olá tornaram-se indisponível

Saiba mais:

* [Balanceador de carga para a Internet entre várias Máquinas Virtuais ou serviços](../load-balancer/load-balancer-internet-overview.md)
* [Visão geral do Balanceador de Carga Interno](../load-balancer/load-balancer-internal-overview.md)

### <a name="global-load-balancing"></a>Balanceamento de carga global
Algumas empresas desejará mais alto o nível de disponibilidade Olá possíveis. Uma maneira tooreach que esse objetivo é toohost aplicativos globalmente distribuídas datacenters. Quando um aplicativo é hospedado em data centers localizados em todo o mundo Olá, é possível para um toobecome toda a região geopolíticas disponível e ainda ter o aplicativo hello até e em execução.

Além disso toohello vantagens de disponibilidade que você obtém por hospedar aplicativos em data centers globalmente distribuídos, você também pode obter benefícios de desempenho. Esses benefícios de desempenho podem ser obtidos por meio de um mecanismo que direciona solicitações de saudação serviço toohello data center mais próximo toohello dispositivo que está fazendo a solicitação de saudação.

O balanceamento de carga global pode proporcionar essas duas vantagens. No Azure, você pode obter benefícios de saudação global de balanceamento de carga usando o Azure Traffic Manager.

Saiba mais:

* [O que é o Gerenciador de Tráfego?](../traffic-manager/traffic-manager-overview.md)


## <a name="name-resolution"></a>Resolução de nomes
Resolução de nomes é uma função crítica para todos os serviços hospedados no Azure. De uma perspectiva de segurança, comprometimento de função de resolução de nome hello pode levar a solicitações de redirecionamento de invasor tooan do site do invasor tooan seus sites. Uma resolução de nomes segura é um requisito de todos os serviços hospedados na nuvem.

Há dois tipos de resolução de nome que é necessário tooaddress:

* Resolução de nomes interna – usada pelos serviços nas Redes Virtuais do Azure, nas redes locais ou em ambas. Nomes usados para resolução de nome interno não são acessíveis pela Internet da saudação. Para uma melhor segurança, é importante que seu esquema de resolução de nome interno não é acessível tooexternal usuários.
* Resolução de nome externa – usada por pessoas e dispositivos fora das redes locais e das Redes Virtuais do Azure. Esses são os nomes de saudação que estão visível toohello da Internet e serviços em nuvem usado toodirect conexão tooyour.

Para a resolução de nomes interna, você tem duas opções:

* Um servidor DNS da Rede Virtual do Azure – ao criar uma nova Rede Virtual do Azure, um servidor DNS é criado para você. Esse servidor DNS pode resolver nomes de Olá Olá máquinas localizados nessa rede Virtual do Azure. O servidor DNS não é configurável e é gerenciado pelo Gerenciador de malha do Azure hello, tornando uma solução de resolução de nome seguro.
* Traga seu próprio servidor DNS, você tem a opção de saudação de colocar um servidor DNS de sua escolha na sua rede Virtual do Azure. Esse servidor DNS pode ser que um Active Directory integrado servidor DNS ou uma solução de servidor DNS dedicada fornecido por um parceiro do Azure, que pode ser obtido hello Azure Marketplace.

Saiba mais:

* [Visão geral da Rede Virtual](../virtual-network/virtual-networks-overview.md)
* [Gerenciar servidores DNS usados por uma rede virtual (VNet)](../virtual-network/virtual-network-manage-network.md#dns-servers)

Para a resolução DNS externa, você tem duas opções:

* Hospedar seu próprio servidor DNS externo localmente
* Hospedar seu próprio servidor DNS externo com um provedor de serviços

Muitas organizações de grande porte hospedarão seus próprios servidores DNS localmente. Eles podem fazer isso porque eles têm Olá rede experiência e presença global toodo assim.

Na maioria dos casos, é melhor toohost a resolução de nome DNS de serviços com um provedor de serviços. Esses provedores de serviço tem conhecimento de rede hello e presença global tooensure muito alta disponibilidade para os serviços de resolução de nome. A disponibilidade é essencial para serviços de DNS, porque se a resolução de nome de serviços falhará, ninguém poderá ser capaz de tooreach seu para serviços de Internet.

Azure fornece alta disponibilidade e alto desempenho solução DNS externa no formulário de saudação do DNS do Azure. Essa solução de resolução de nome externo se beneficia da infraestrutura de DNS do Azure em todo o mundo hello. Ele permite toohost seu domínio no Azure usando Olá mesmo credenciais, APIs, ferramentas e cobrança como outros serviços do Azure. Como parte do Azure, ele também herda controles de alta segurança Olá incorporados Olá plataforma.

Saiba mais:

* [Visão geral do DNS do Azure](../dns/dns-overview.md)

## <a name="dmz-architecture"></a>Arquitetura do DMZ
Muitas empresas usam DMZs toosegment seu toocreate redes uma zona de buffer entre hello Internet e seus serviços. parte do DMZ de saudação da rede Olá é considerada uma zona de baixa segurança e não ativos de alto valor são colocados no segmento da rede. Normalmente, você verá dispositivos de segurança de rede que têm uma interface de rede no segmento de saudação DMZ e outra interface conectada tooa rede com máquinas virtuais e serviços que aceitam conexões de entrada de saudação à Internet.

Há diversas variações de design de rede de Perímetro e Olá decisão toodeploy uma rede de Perímetro e, em seguida, o tipo de rede de Perímetro toouse se você decidir toouse, baseia-se nos seus requisitos de segurança de rede.

Saiba mais:

* [Segurança de rede e Serviços de Nuvem da Microsoft](../best-practices-network-security.md)


## <a name="monitoring-and-threat-detection"></a>Monitoramento e detecção de ameaças

O Azure fornece recursos toohelp você nesta área chave com início detecção, monitoramento e Olá capacidade revisão e toocollect tráfego de rede.

### <a name="azure-network-watcher"></a>Observador de Rede do Azure
Observador de rede do Azure inclui um grande número de recursos para ajudar a solucionar problemas, bem como para fornecer um novo conjunto de ferramentas tooassist com identificação de saudação de problemas de segurança.

[Exibição de grupo de segurança ](/network-watcher/network-watcher-security-group-view-overview.md) ajuda a conformidade de segurança e auditoria de máquinas virtuais e pode ser usado tooperform auditorias programáticas comparando as políticas de linhas de base de Olá definidas pelas regras de tooeffective sua organização para cada uma das suas VMs. Isso pode ajudar a identificar qualquer descompasso de configuração.

[Captura de pacote](/network-watcher/network-watcher-packet-capture-overview.md) permite que você toocapture tooand de tráfego de rede da máquina virtual de saudação. Além de ajudar, permitindo que as estatísticas de rede toocollect e Olá solução de problemas do aplicativo de captura de pacote de problemas pode ser inestimável na investigação de saudação de invasões de rede. Você também pode usar essa funcionalidade em conjunto com funções do Azure capturas de rede de toostart na resposta toospecific Azure alertas.

Para obter mais informações sobre o observador de rede do Azure e como toostart testar algumas das funcionalidades de saudação em seus laboratórios dar uma olhada em hello [visão geral do monitoramento de observador de rede do Azure](/network-watcher/network-watcher-monitoring-overview.md)

>[!NOTE]
Observador de rede do Azure ainda está em visualização pública para que ele não pode ter Olá mesmo nível de disponibilidade e confiabilidade como os serviços são, em geral, versão de disponibilidade. Determinados recursos podem não ter suporte, podem ter restrição e podem não estar disponíveis em todos os locais do Azure. Para notificações mais recentes de Olá em disponibilidade e o status do serviço, verifique Olá [página atualizações do Azure](https://azure.microsoft.com/updates/?product=network-watcher)

### <a name="azure-security-center"></a>Central de Segurança do Azure
Central de segurança ajuda a evitar, detectar e responder toothreats e fornece que maior visibilidade e controle, segurança de saudação de seus recursos do Azure. Ela permite o gerenciamento de políticas e o monitoramento da segurança integrada entre suas assinaturas do Azure, ajuda a detectar ameaças que poderiam passar despercebidas e funciona com um grande conjunto de soluções de segurança.

A Central de Segurança do Azure ajuda a otimizar e a monitorar a segurança da rede:

* Fornecendo recomendações de segurança de rede
* Monitoramento de estado de saudação da sua configuração de segurança de rede
* Alerta de toonetwork com base em ameaças ambas nos níveis de rede e o ponto de extremidade Olá

Saiba mais:

* [Introdução tooAzure Central de segurança](../security-center/security-center-intro.md)


### <a name="logging"></a>Registro em log
O log em um nível de rede é uma função essencial em qualquer cenário de segurança de rede. No Azure, você pode registrar informações obtidas de nível de rede tooget de grupos de segurança de rede informações de registro. Com o log do NSG, você obtém informações dos seguintes:

* [Logs de atividade](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) – esses logs são usado tooview todas as operações enviada tooyour Azure assinaturas. Esses logs são habilitados por padrão e podem ser usados em Olá portal do Azure. Eles eram anteriormente conhecidos como "Logs de auditoria" ou "Logs operacionais".
* Logs de eventos – esses logs fornecem informações sobre quais regras do NSG foram aplicadas.
* Logs do contador – esses logs permitem a você saber quantas vezes cada regra NSG foi aplicada toodeny ou permitam o tráfego.

Você também pode usar [Microsoft Power BI](https://powerbi.microsoft.com/what-is-power-bi/), uma visualização de dados poderosa ferramenta tooview e analisar esses logs.

Saiba mais:

* [Análise de logs para NSGs (grupos de segurança de rede)](../virtual-network/virtual-network-nsg-manage-log.md)
