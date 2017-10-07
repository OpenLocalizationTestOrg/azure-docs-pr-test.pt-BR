---
title: "Práticas recomendadas de segurança de rede de aaaAzure | Microsoft Docs"
description: "Este artigo fornece um conjunto de práticas recomendadas de segurança de rede usando recursos internos do Azure."
services: security
documentationcenter: na
author: TomShinder
manager: swadhwa
editor: TomShinder
ms.assetid: 7f6aa45f-138f-4fde-a611-aaf7e8fe56d1
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/09/2017
ms.author: TomSh
ms.openlocfilehash: 5867dea358b4da65c65b3e52fcab7e687e981642
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-network-security-best-practices"></a>Práticas recomendadas de rede do Azure
Microsoft Azure permite que dispositivos de tooother em rede de máquinas virtuais e dispositivos tooconnect, colocando-os em redes virtuais do Azure. Uma rede Virtual do Azure é uma construção de rede virtual que permite que você tooconnect rede virtual interface cartões tooa virtual tooallow baseada em TCP/IP comunicações de rede entre os dispositivos de rede habilitada. Máquinas virtuais do Azure conectado tooan rede Virtual do Azure são toodevices tooconnect capaz em Olá mesma rede Virtual do Azure, redes virtuais diferentes do Azure, na saudação da Internet ou até mesmo em suas próprias redes locais.

Neste artigo, veremos uma coleção de práticas recomendadas de segurança de rede do Azure. Essas práticas recomendadas são derivadas da nossa experiência com a rede do Azure e experiências de saudação de clientes, como por conta própria.

Para cada prática recomendada, vamos explicar:

* A prática recomendada que Olá é
* Por que você deseja tooenable essa prática recomendada
* O que pode ser resultado de saudação se você não a prática recomendada de saudação tooenable
* Prática recomendada de toohello possíveis alternativas
* Como você pode aprender a prática recomendada de saudação tooenable

Este artigo de práticas recomendadas de segurança de rede do Azure baseia-se em uma opinião consenso e recursos da plataforma Azure e conjuntos de recursos, que existem em tempo de saudação que este artigo foi escrito. Tecnologias e opiniões alterar ao longo do tempo e este artigo será atualizado em um tooreflect regularmente essas alterações.

As práticas recomendadas de segurança de rede do Azure discutidas neste artigo incluem:

* Segmentar logicamente as sub-redes
* Controlar o comportamento de roteamento
* Habilitar o túnel forçado
* Usar dispositivos de rede virtual
* Implantar DMZs para zoneamento de segurança
* Evitar a exposição toohello Internet com links WAN dedicados
* Otimizar o desempenho e o tempo de atividade
* Usar o balanceamento de carga global
* Desabilitar acesso RDP tooAzure máquinas virtuais
* Habilitar a Central de Segurança do Azure
* Estender seu datacenter para o Azure

## <a name="logically-segment-subnets"></a>Segmentar logicamente as sub-redes
[Redes virtuais do Azure](https://azure.microsoft.com/documentation/services/virtual-network/) são semelhantes LAN tooa em sua rede local. Olá ideia por trás de uma rede Virtual do Azure é que você crie uma único IP endereço com base em espaço rede privada na qual você pode colocar todos os seus [máquinas virtuais do Azure](https://azure.microsoft.com/services/virtual-machines/). Olá privados espaços de endereço IP disponíveis estão em Olá A classe (10.0.0.0/8), classe B (172.16.0.0/12) e classe C (192.168.0.0/16) intervalos.

Toowhat semelhante é local, será necessário espaço de endereço maior toosegment Olá em sub-redes. Você pode usar [CIDR](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) com base em sub-redes toocreate princípios suas sub-redes.

Roteamento entre sub-redes acontecerá automaticamente e você não precisa configurar o toomanually tabelas de roteamento. No entanto, a configuração padrão de saudação é que não há nenhum controle de acesso de rede entre sub-redes Olá que criar em Olá rede Virtual do Azure. Em controles de acesso de ordem toocreate rede entre sub-redes, você precisará tooput algo entre sub-redes hello.

Uma das coisas Olá você pode usar tooaccomplish essa tarefa é um [grupo de segurança de rede](../virtual-network/virtual-networks-nsg.md) (NSG). Os NSGs são inspeção de pacotes com monitoração de estado simples dispositivos que usam Olá 5 tuplas (IP de origem hello, porta de origem, IP de destino, porta de destino e protocolo de camada 4) abordagem toocreate Permitir/Negar regras para o tráfego de rede. Você pode permitir ou negar o tráfego tooand do endereço IP único, tooand vários endereços IP ou até mesmo tooand de sub-redes inteiras.

Usando os NSGs de controle de acesso de rede entre sub-redes permite que você tooput recursos que pertencem a toohello mesma zona de segurança ou de função em suas próprias sub-redes. Pense, por exemplo, em um aplicativo de camada 3 simples que tenha uma camada da Web, uma camada lógica de aplicativo e uma camada de banco de dados. Você colocar máquinas virtuais que pertencem a tooeach esses níveis em suas próprias sub-redes. Em seguida, você pode usar NSGs toocontrol tráfego entre as sub-redes de saudação:

* Máquinas de virtuais de camada da Web só pode iniciar máquinas de lógica de aplicativo conexões toohello e só pode aceitar conexões da saudação da Internet
* Máquinas de virtuais de lógica de aplicativo só podem iniciar conexões com o nível de banco de dados e só pode aceitar conexões da camada da web de saudação
* Não é possível iniciar a conexão com qualquer coisa fora de sua própria sub-rede de máquinas de virtuais de camada de banco de dados e só pode aceitar conexões da camada de lógica de aplicativo hello

toolearn mais sobre grupos de segurança de rede e como você pode usá-los toologically segmento suas redes virtuais do Azure, leia o artigo de saudação [o que é um grupo de segurança de rede](../virtual-network/virtual-networks-nsg.md) (NSG).

## <a name="control-routing-behavior"></a>Controlar o comportamento de roteamento
Quando você colocar uma máquina virtual em uma rede Virtual do Azure, você perceberá que a máquina virtual Olá pode se conectar tooany outra máquina virtual em Olá mesma rede Virtual do Azure, mesmo se hello outras máquinas virtuais estiverem em sub-redes diferentes. motivo Olá por que isso é possível é que há uma coleção de rotas de sistema que são habilitados por padrão que permita esse tipo de comunicação. Essas rotas padrão permitem que máquinas virtuais em Olá mesmo conexões tooinitiate de rede Virtual do Azure entre si e com hello Internet (para comunicações de saída toohello Internet somente).

Enquanto as rotas de sistema do saudação padrão são úteis para muitos cenários de implantação, há horários de configuração de roteamento toocustomize Olá para suas implantações. Essas personalizações permitirá que você tooconfigure Olá próximo salto endereço tooreach destinos específicos.

É recomendável que você configure Rotas Definidas pelo Usuário ao implantar um dispositivo de segurança de rede virtual, sobre o qual falaremos em uma prática recomendada posterior.

> [!NOTE]
> Rotas definidas pelo usuário não são necessárias e rotas de sistema saudação padrão funciona na maioria dos casos.
>
>

Você pode aprender mais sobre as rotas definidas pelo usuário e como tooconfigure-los ao ler o artigo Olá [quais são rotas definidas pelo usuário e encaminhamento IP](../virtual-network/virtual-networks-udr-overview.md).

## <a name="enable-forced-tunneling"></a>Habilitar o túnel forçado
toobetter entender o túnel forçado, é útil toounderstand que "túnel dividido" é.
exemplo de Hello mais comuns de túnel dividido é visto com conexões VPN. Imagine que você estabeleça uma conexão VPN de sua rede corporativa do hotel sala tooyour. Esta conexão permite tooconnect tooresources em sua rede corporativa e vá tooresources de todas as comunicações em sua rede corporativa por meio de túnel VPN hello.

O que acontece quando você quiser tooresources tooconnect em Olá Internet? Quando criar um túnel dividido está habilitado, as conexões vá diretamente toohello Internet e não por meio de saudação VPN de túnel. Alguns especialistas em segurança considere esse toobe um risco em potencial e, portanto, recomendam que túnel dividido desabilitado e todas as conexões, os destinado a saudação da Internet e aqueles destinados a recursos corporativos, passar pelo túnel VPN hello. vantagem de saudação de fazer isso é que toohello conexões à Internet, em seguida, são impostos por meio de dispositivos de segurança de rede corporativa hello, que não seriam o caso de saudação se cliente VPN Olá conectado toohello Internet fora do túnel VPN hello.

Agora vamos colocar isso toovirtual máquinas de volta em uma rede Virtual do Azure. as rotas saudação padrão para uma rede Virtual do Azure permitem que máquinas virtuais tooinitiate tráfego toohello da Internet. Isso também pode representar um risco à segurança, como essas conexões de saída podem aumentar a superfície de ataque de saudação de uma máquina virtual e ser aproveitadas por invasores.
Por esse motivo, recomendamos que você habilite o túnel forçado em suas máquinas virtuais quando tiver conectividade entre locais entre sua Rede Virtual do Azure e sua rede local. Falaremos sobre a conectividade entre locais neste documento sobre práticas recomendadas de rede do Azure.

Se você não tiver uma conexão entre locais, verifique se você aproveitar os grupos de segurança de rede (discutido anteriormente) ou o Azure toohello rede virtual segurança dispositivos (discutido Avançar) tooprevent conexões de saída da Internet de sua Virtual do Azure Máquinas.

Saiba mais sobre toolearn túnel forçado e como tooenable, leia o artigo de saudação [configurar o túnel forçado usando o PowerShell e o Azure Resource Manager](../vpn-gateway/vpn-gateway-forced-tunneling-rm.md).

## <a name="use-virtual-network-appliances"></a>Usar dispositivos de rede virtual
Enquanto os grupos de segurança de rede e roteamento de definida pelo usuário podem fornecer uma certas medidas de segurança de rede no hello camadas de transporte e de rede de saudação [modelo OSI](https://en.wikipedia.org/wiki/OSI_model), serão toobe situações em que você deseja ou precisa tooenable segurança em níveis altos da pilha de saudação. Em tais situações, é recomendável que você implante dispositivos de segurança de rede virtual fornecidos por parceiros do Azure.

Os dispositivos de segurança de rede do Azure podem oferecer níveis consideravelmente aprimorados de segurança em relação ao que é fornecido pelos controles de nível de rede. Alguns dos recursos de segurança de rede Olá fornecidos por dispositivos de segurança de rede virtual incluem:

* Firewall
* Detecção de intrusão/prevenção contra intrusões
* Gerenciamento de vulnerabilidades
* Controle de aplicativo
* Detecção de anomalias baseada em rede
* Filtragem da Web
* Antivírus
* Proteção botnet

Se você precisar de um nível mais alto de segurança de rede que pode obter com controles de acesso no nível de rede, é recomendável que você investigue e implante os dispositivos de segurança de rede virtual do Azure.

toolearn sobre quais dispositivos de segurança de rede virtual do Azure estão disponíveis e seus recursos, visite Olá [Azure Marketplace](https://azure.microsoft.com/marketplace/) e procure "segurança" e "segurança de rede".

## <a name="deploy-dmzs-for-security-zoning"></a>Implantar DMZs para zoneamento de segurança
Uma rede de Perímetro ou "rede de perímetro" é físico ou segmento de rede lógica que é projetado tooprovide uma camada adicional de segurança entre seus ativos e saudação da Internet. intenção Olá Olá DMZ é tooplace especializado dispositivos de controle de acesso de rede na borda de saudação da rede Olá DMZ para que somente o tráfego desejado é permitido passar Olá dispositivo de segurança de rede e em sua rede Virtual do Azure.

DMZs são úteis porque você pode se concentrar o gerenciamento de controle de acesso de rede, monitorar, registro em log e relatórios em dispositivos de saudação na borda de saudação da sua rede Virtual do Azure. Aqui, você normalmente habilitaria a prevenção de DDoS, os sistemas de Detecção de Intrusão/Prevenção contra Intrusão (IDS/IPS), as regras e políticas de firewall, a filtragem da Web, a rede antimalware e muito mais. dispositivos de segurança de rede Olá ficam entre hello Internet e sua rede Virtual do Azure e tem uma interface em ambas as redes.

Embora esse seja o design básico de saudação de uma rede de Perímetro, existem muitos diferentes designs de rede de Perímetro, como em frente e verso, três adaptadores de rede, multihomed e outros.

É recomendável para todas as implantações de alta segurança que você considere a implantação de um nível de saudação do DMZ tooenhance de segurança de rede para os recursos do Azure.

mais sobre DMZs e como toodeploy-los no Azure, leia o artigo de saudação do toolearn [segurança de rede e serviços de nuvem da Microsoft](../best-practices-network-security.md).

## <a name="avoid-exposure-toohello-internet-with-dedicated-wan-links"></a>Evitar a exposição toohello Internet com links WAN dedicados
Muitas organizações escolheu rota de TI híbrida hello. Em TI híbrida, alguns dos ativos de informações da empresa Olá estão no Azure, enquanto outros permanecem no local. Em muitos caso,s alguns componentes de um serviço estarão em execução no Azure, enquanto outros componentes permanecem no local.

Em híbrida Olá cenário de TI, geralmente há algum tipo de conectividade entre locais. Isso entre locais conectividade permite Olá empresa tooconnect seu tooAzure de redes locais redes virtuais. Há duas soluções de conectividade entre locais disponíveis:

* VPN site a site
* ExpressRoute

A [VPN site a site](../vpn-gateway/vpn-gateway-site-to-site-create.md) representa uma conexão privada virtual entre sua rede local e uma Rede Virtual do Azure. Essa conexão é feita em Olá Internet e permite que você muito "encapsular" informações dentro de uma conexão criptografada entre sua rede e o Azure. A VPN site a site é uma tecnologia segura e madura implantada por empresas de todos os portes há décadas. A criptografia de túnel é realizada usando o [modo de túnel IPsec](https://technet.microsoft.com/library/cc786385.aspx).

Enquanto o VPN site a site é uma tecnologia estabelecida, confiável e confiável, tráfego de túnel Olá atravessar Olá da Internet. Além disso, a largura de banda é relativamente restrita tooa máximo sobre 200 Mbps.

Se você precisar de um nível excepcional de segurança ou de desempenho para as conexões entre locais, recomendamos que você use a Azure ExpressRoute para sua conectividade entre locais. O ExpressRoute é um link WAN dedicado entre seu local ou um provedor de hospedagem do Exchange. Como esta é uma conexão de telecomunicações, seus dados não passam pelo Olá da Internet e, portanto, é toohello não exposta possíveis riscos inerentes a comunicação com a Internet.

toolearn mais sobre como funciona a rota expressa do Azure e como toodeploy, leia o artigo de saudação [visão geral técnica do ExpressRoute](../expressroute/expressroute-introduction.md).

## <a name="optimize-uptime-and-performance"></a>Otimizar o desempenho e o tempo de atividade
Confidencialidade, integridade e disponibilidade (CIA) incluem triplo de saudação do modelo de segurança mais influente de hoje. Confidencialidade é sobre criptografia e a privacidade, a integridade é focado em garantir que dados não são alterados por pessoas não autorizadas, e a disponibilidade é focado em garantir que pessoas autorizadas são tooaccess capaz de obter informações de saudação que estão autorizados tooaccess. A falha em qualquer uma dessas áreas representa uma possível violação de segurança.

A disponibilidade pode ser pensada como relacionada a tempo de atividade e ao desempenho. Se um serviço estiver inativo, as informações não poderão ser acessadas. Se o desempenho é inadequado assim como dados de saudação toomake inutilizáveis, em seguida, pode consideramos Olá dados toobe inacessível. Portanto, de uma perspectiva de segurança, precisamos toodo qualquer possível toomake se nossos serviços tem o melhor tempo de atividade e desempenho.
Um método eficiente e popular usado tooenhance disponibilidade e o desempenho é toouse balanceamento de carga. O balanceamento de carga é um método de distribuição de tráfego de rede entre servidores que fazem parte de um serviço. Por exemplo, se você tiver servidores web front-end como parte de seu serviço, você pode usar o tráfego balanceamento de carga toodistribute Olá em vários servidores web front-end.

Essa distribuição de tráfego aumenta a disponibilidade porque se um dos servidores de web hello ficar indisponível, o balanceador de carga Olá parará de enviar server de toothat de tráfego e servidores de toohello de tráfego de redirecionamento que ainda estão online. Balanceamento de carga também ajuda a desempenho, pois hello processador, rede e sobrecarga de memória para atender solicitações são distribuídos em todos os servidores de balanceamento de carga de saudação.

É recomendável implantar o balanceamento de carga sempre que possível e conforme apropriado para seus serviços. Vamos abordá conveniência em Olá seções a seguir.
Em Olá nível de rede Virtual do Azure, o Azure fornece com três principais opções de balanceamento de carga:

* Balanceamento de carga baseado em HTTP
* Balanceamento de carga externo
* Balanceamento de carga interno

## <a name="http-based-load-balancing"></a>Balanceamento de carga baseado em HTTP
Balanceamento de carga com base em HTTP bases decisões sobre quais conexões de toosend do servidor usando as características do protocolo de saudação HTTP. O Azure tem um balanceador de carga HTTP que passa pelo nome de saudação do Application Gateway.

É recomendável que você use o Gateway de Aplicativo do Azure quando:

* Aplicativos que necessitam de solicitações de saudação mesmo tooreach de sessão de usuário/cliente Olá mesma máquina virtual de back-end. Exemplos disso são os aplicativos de carrinho de compras e servidores de email na Web.
* Aplicativos que deseja toofree web farms de servidores de terminação SSL sobrecarga, tirando proveito do Application Gateway [descarregamento SSL](https://f5.com/glossary/ssl-offloading) recurso.
* Aplicativos, como uma rede de fornecimento de conteúdo, que requerem várias solicitações HTTP na Olá mesmo toobe de conexão TCP de longa execução roteadas ou servidores de back-end toodifferent com balanceamento de carga.

toolearn mais sobre como funciona o Gateway de aplicativo do Azure e como você pode usá-lo em suas implantações, leia o artigo Olá [visão geral do Application Gateway](../application-gateway/application-gateway-introduction.md).

## <a name="external-load-balancing"></a>Balanceamento de carga externo
Balanceamento de carga externa ocorre quando as conexões de entrada da saudação Internet têm a carga balanceada entre os servidores localizados em uma rede Virtual do Azure. Hello Azure balanceador externo de carga pode fornecer esse recurso e é recomendável que você usá-lo quando não necessitar de sessões Autoadesivas hello ou descarregamento de SSL.

Em contraste com base em tooHTTP balanceamento de carga, Olá balanceador externo de carga usa informações em camadas de transporte e de rede de saudação do hello OSI modelo toomake decisões de rede no qual conexão do servidor tooload saldo para.

Recomendamos que você use balanceamento de carga externo sempre que houver [aplicativos sem monitoração de estado](http://whatis.techtarget.com/definition/stateless-app) aceitar solicitações de entrada de saudação à Internet.

toolearn mais sobre como funciona a saudação balanceador de carga externo do Azure e como implantá-lo, leia o artigo Olá [começar a criar um balanceador de carga voltados para Internet no Gerenciador de recursos usando o PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md).

## <a name="internal-load-balancing"></a>Balanceamento de carga interno
Balanceamento de carga interno é semelhante tooexternal balanceamento de carga e usa Olá mesmo mecanismo tooload saldo conexões toohello servidores por trás deles. Olá única diferença é que balanceador de carga Olá nesse caso está aceitando conexões de máquinas virtuais que não estão na Internet de saudação. Na maioria dos casos, as conexões de Olá aceitos para balanceamento de carga são iniciadas por dispositivos em uma rede Virtual do Azure.

É recomendável que você use para cenários que se beneficiam esse recurso, como quando você precisar tooload saldo conexões tooSQL servidores ou servidores web interno de balanceamento de carga interna.

toolearn mais sobre como funciona o balanceamento de carga interno do Azure e como implantá-lo, leia o artigo Olá [começar a criar um balanceador de carga interno usando o PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md#update-an-existing-load-balancer).

## <a name="use-global-load-balancing"></a>Usar o balanceamento de carga global
Possibilita de computação em nuvem pública toodeploy de aplicativos que têm componentes localizados em data centers em todo o Olá, mundo globalmente distribuídos. Isso é possível no Microsoft Azure devido a presença de datacenter global do tooAzure. Em contraste tecnologias de balanceamento de carga de toohello mencionado anteriormente, balanceamento de carga global torna possível toomake serviços disponível mesmo quando datacenters inteira podem se tornar indisponível.

Você pode obter esse tipo de balanceamento de carga global no Azure ao aproveitar as vantagens do [Gerenciador de Tráfego do Azure](https://azure.microsoft.com/documentation/services/traffic-manager/). O Traffic Manager faz é saldo tooload possíveis serviços tooyour de conexões com base na localização de saudação do usuário hello.

Por exemplo, se o usuário Olá faz um serviço de tooyour de solicitação da saudação da UE, conexão Olá é direcionado tooyour serviços localizados em um datacenter da Europa. Essa parte da Ajuda tooimprove desempenho de balanceamento de carga global do Gerenciador de tráfego como conexão toohello mais próximo de datacenter é mais rápida do que conectar toodatacenters que estão distantes.

No lado de disponibilidade hello, balanceamento de carga global garante que o serviço está disponível mesmo se um datacenter inteiro deve se tornar indisponível.

Por exemplo, se um datacenter do Azure deve se tornar indisponível devido a motivos tooenvironmental ou vencimento toooutages (tais como falhas de rede regional), conexões de serviço tooyour seja redirecionado toohello mais próximo do datacenter online. Esse balanceamento de carga global é realizado tirando proveito das políticas de DNS que você pode criar no Gerenciador de Tráfego.

É recomendável que você use o Gerenciador de tráfego para desenvolver qualquer solução de nuvem que tem um escopo amplamente distribuído por várias regiões e requer o nível mais alto de saudação de tempo de atividade possíveis.

toolearn mais sobre o Azure Traffic Manager e como toodeploy, leia o artigo de saudação [o que é o Gerenciador de tráfego](../traffic-manager/traffic-manager-overview.md).

## <a name="disable-rdpssh-access-tooazure-virtual-machines"></a>Desabilitar o acesso RDP/SSH tooAzure máquinas virtuais
É possível tooreach máquinas virtuais do Azure usando Olá [Remote Desktop Protocol](https://en.wikipedia.org/wiki/Remote_Desktop_Protocol) (RDP) e hello [Secure Shell](https://en.wikipedia.org/wiki/Secure_Shell) protocolos (SSH). Esses protocolos torná-lo em máquinas virtuais de toomanage possíveis de locais remotos e são padrão na computação do datacenter.

possível problema de segurança Olá com usando esses protocolos sobre Olá Internet é que os invasores podem usar vários [força bruta](https://en.wikipedia.org/wiki/Brute-force_attack) técnicas toogain acesso tooAzure máquinas virtuais. Depois que os invasores Olá obterem acesso, eles podem usar sua máquina virtual como um ponto de partida para comprometer outros computadores na sua rede Virtual do Azure ou mesmo ataques dispositivos de rede fora do Azure.

Por isso, recomendamos que você desabilite direto RDP e SSH acesso tooyour máquinas virtuais do Azure de saudação à Internet. Após direto RDP e SSH acessar de saudação que Internet está desabilitada, você tem outras opções que você pode usar tooaccess essas máquinas virtuais para o gerenciamento remoto:

* VPN ponto a site
* VPN site a site
* ExpressRoute

A [VPN ponto a site](../vpn-gateway/vpn-gateway-point-to-site-create.md) é outro termo para uma conexão de cliente/servidor de VPN de acesso remoto. Uma VPN ponto a site permite tooan de tooconnect um único usuário rede Virtual do Azure pela Internet da saudação. Após a conexão de ponto para site Olá é estabelecida, Olá será capaz de toouse RDP ou SSH, tooconnect tooany máquinas virtuais localizadas em Olá rede Virtual do Azure que Olá usuário conectado toovia ponto a site VPN. Isso pressupõe que o usuário Olá é autorizado tooreach essas máquinas virtuais.

VPN ponto a site é mais segura do que conexões diretas de RDP ou SSH como usuário Olá tem tooauthenticate duas vezes antes de conectar máquina virtual de tooa. Primeiro, Olá tooauthenticate de necessidades de usuário (e ser autorizado) conexão de VPN de ponto para site de saudação tooestablish; segundo, Olá tooauthenticate de necessidades de usuário (e ser autorizado) tooestablish Olá RDP ou SSH à sessão.

Um [VPN site a site](../vpn-gateway/vpn-gateway-site-to-site-create.md) se conecta a uma rede inteira do tooanother pela Olá da Internet. Você pode usar um tooconnect VPN site a site tooan de rede seu local na rede Virtual do Azure. Se você implantar uma VPN site a site, usuários em sua rede local será capaz de tooconnect toovirtual máquinas na rede Virtual do Azure usando Olá RDP ou protocolo SSH mais Olá conexão de VPN site a site e não requer tooallow direto RDP ou SSH acesso a saudação da Internet.

Você também pode usar um toohello do link WAN dedicado tooprovide funcionalidade semelhante VPN site a site. Olá principais diferenças são 1. link WAN dedicado Olá não atravessa Olá Internet e 2. os links WAN dedicados são geralmente mais estáveis e com maior desempenho. Azure fornece uma solução de link WAN dedicado na forma de saudação de [ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/).

## <a name="enable-azure-security-center"></a>Habilitar a Central de Segurança do Azure
Central de segurança do Azure ajuda a evitar, detectar e responder toothreats e fornece que maior visibilidade e controle, segurança de saudação de seus recursos do Azure. Ela permite o gerenciamento de políticas e o monitoramento da segurança integrada entre suas assinaturas do Azure, ajuda a detectar ameaças que poderiam passar despercebidas e funciona com uma enorme variedade de soluções de segurança.

A Central de Segurança do Azure ajuda a otimizar e a monitorar a segurança da rede:

* Fornecendo recomendações de segurança de rede
* Monitoramento de estado de saudação da sua configuração de segurança de rede
* Alerta de toonetwork com base em ameaças ambas nos níveis de rede e o ponto de extremidade Olá

É altamente recomendável que você habilite a Central de Segurança do Azure para todas as implantações do Azure.

mais informações sobre a Central de segurança do Azure e como tooenable para suas implantações, leia o artigo de saudação do toolearn [tooAzure Introdução a Central de segurança](../security-center/security-center-intro.md).

## <a name="securely-extend-your-datacenter-into-azure"></a>Estenda com segurança seu datacenter para o Azure
TI empresarial de muitas organizações analisando tooexpand nuvem Olá em vez de crescimento de seus datacenters locais. Essa expansão representa uma extensão da infra-estrutura de TI na nuvem pública hello. Ao aproveitar entre locais de opções de conectividade, é possível tootreat suas redes virtuais do Azure como qualquer outra sub-rede em seu local infraestrutura de rede.

No entanto, há muito planejamento e design que precisam toobe abordados primeiro. Isso é especialmente importante na área de saudação de segurança de rede. Uma saudação melhores maneiras toounderstand como abordar esse design é toosee um exemplo.

A Microsoft criou Olá [diagrama de arquitetura de referência de extensão do Datacenter](https://gallery.technet.microsoft.com/Datacenter-extension-687b1d84#content) e suporte toohelp colateral entender aparência tal uma extensão de datacenter. Isso fornece uma implementação de referência de exemplo que você pode usar tooplan e crie uma nuvem de toohello de extensão de datacenter corporativo seguro. É recomendável que você examine este documento tooget uma ideia dos componentes principais de saudação de uma solução segura.

toolearn mais informações sobre como toosecurely estender seu datacenter no Azure, consulte o vídeo Olá [tooMicrosoft estender seu Datacenter do Azure](https://www.youtube.com/watch?v=Th1oQQCb2KA).
