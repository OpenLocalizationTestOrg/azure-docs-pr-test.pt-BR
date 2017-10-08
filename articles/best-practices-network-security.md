---
title: "práticas recomendadas de segurança de rede aaaAzure | Microsoft Docs"
description: "Aprenda a que saudação principais recursos disponíveis no Azure toohelp criam ambientes de rede segura"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: d169387a-1243-4867-a602-01d6f2d8a2a1
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: b851b2862428a8bd5e7525c85584fc1c14ffcabe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-cloud-services-and-network-security"></a>Segurança de rede e serviços em nuvem da Microsoft
Os serviços em nuvem da Microsoft entregam serviços e estrutura em larga escala, recursos de nível empresarial e várias opções de conectividade híbrida. Os clientes podem escolher tooaccess esses serviços por meio de saudação da Internet ou com o Azure ExpressRoute, que fornece conectividade de rede privada. plataforma do Microsoft Azure Olá permite aos clientes tooseamlessly estender sua infraestrutura em nuvem hello e compilar arquiteturas de várias camadas. Além disso, terceiros podem habilitar recursos avançados oferecendo serviços de segurança e soluções de virtualização. Este white paper fornece uma visão geral sobre segurança e problemas de arquitetura que os clientes devem considerar ao usar os serviços em nuvem da Microsoft acessados através do ExpressRoute. Ele também aborda a criação de serviços mais seguros em redes virtuais do Azure.

## <a name="fast-start"></a>Início rápido
Olá gráfico lógica a seguir pode direcionar você tooa exemplo específico de saudação muitas técnicas de segurança disponíveis com hello plataforma Windows Azure. Para referência rápida, localize o exemplo hello que melhor se encaixa em seu caso. Para obter explicações expandidas, continue lendo papel hello.
[![0]][0]

[Exemplo 1: Criar uma rede de perímetro (também conhecida como DMZ, zona desmilitarizada ou sub-rede filtrada) toohelp proteger aplicativos com grupos de segurança de rede (NSGs).](#example-1-build-a-perimeter-network-to-help-protect-applications-with-nsgs)</br>
[Exemplo 2: Criar um perímetro rede toohelp proteger aplicativos com um firewall e NSGs.](#example-2-build-a-perimeter-network-to-help-protect-applications-with-a-firewall-and-nsgs)</br>
[Exemplo 3: Criar um perímetro rede toohelp proteger redes com um firewall, a rota definida pelo usuário (UDR) e o NSG.](#example-3-build-a-perimeter-network-to-help-protect-networks-with-a-firewall-and-udr-and-nsg)</br>
[Exemplo 4: adicione uma conexão híbrida com uma VPN (rede privada virtual) site a site de solução de virtualização.](#example-4-add-a-hybrid-connection-with-a-site-to-site-virtual-appliance-vpn)</br>
[Exemplo 5: adicione uma conexão híbrida com um gateway de VPN site a site do Azure.](#example-5-add-a-hybrid-connection-with-a-site-to-site-azure-vpn-gateway)</br>
[Exemplo 6: adicione uma conexão híbrida com o ExpressRoute.](#example-6-add-a-hybrid-connection-with-expressroute)</br>
Exemplos para adicionar conexões entre redes virtuais, a alta disponibilidade e o encadeamento de serviço serão adicionados toothis documento durante saudação próximos meses.

## <a name="microsoft-compliance-and-infrastructure-protection"></a>Proteção de infraestrutura e conformidade da Microsoft
organizações toohelp obedecer nacional, regional, e requisitos específicos do setor que controlam a coleta de saudação e uso de dados de indivíduos, a Microsoft oferece mais de 40 certificações e attestations. Olá mais abrangente conjunto de qualquer provedor de serviços de nuvem.

Para obter mais informações, consulte as informações de conformidade Olá em Olá [Microsoft Trust Center][TrustCenter].

A Microsoft tem uma abordagem abrangente tooprotect infraestrutura necessária toorun hyper-escala global serviços de nuvem. Infraestrutura de nuvem da Microsoft inclui hardware, software, redes e administrativas e a equipe de operações, além de toohello físico data centers.

![2]

Essa abordagem fornece uma base mais segura para os clientes toodeploy seus serviços em nuvem da Microsoft de saudação. Olá próxima etapa é para clientes toodesign e criar um tooprotect de arquitetura de segurança desses serviços.

## <a name="traditional-security-architectures-and-perimeter-networks"></a>Arquiteturas de segurança tradicionais e redes de perímetro
Embora a Microsoft faz investimentos consideráveis para proteger a infraestrutura de nuvem Olá, os clientes também devem proteger os serviços de nuvem e grupos de recursos. Uma abordagem de várias camadas toosecurity fornece melhor defesa do hello. Uma zona de segurança de rede de perímetro protege recursos da rede interna de uma rede não confiável. Uma rede de perímetro refere-se toohello bordas ou partes da rede Olá estabelecidos entre hello da Internet e a infra-estrutura de TI da empresa Olá protegido.

Em redes corporativas típicas, infraestrutura básica de saudação muito proteção reforçada no perímetro hello, com várias camadas de dispositivos de segurança. limite de saudação de cada camada consiste em dispositivos e pontos de imposição de política. Cada camada pode incluir uma combinação de saudação dispositivos de segurança de rede a seguir: firewalls, prevenção dos (negação de serviço), a detecção de intrusão ou sistemas de proteção (IDS/IPS) e dispositivos VPN. Imposição de política pode assumir a forma de saudação de roteamento específico, listas de controle de acesso (ACLs) ou políticas de firewall. Olá primeira linha de defesa na rede hello, diretamente aceitar tráfego de entrada de saudação à Internet, é uma combinação desses mecanismos tooblock ataques e tráfego prejudicial permitindo ainda mais a solicitações legítimas em rede hello. Esse tráfego roteia tooresources diretamente na rede de perímetro hello. Esse recurso pode, em seguida, "falar" tooresources em rede hello, transiting limites de Avançar Olá para validação primeiro. camada de externo de saudação é chamada de rede de perímetro Olá porque essa parte da rede Olá toohello exposto à Internet, normalmente com alguma forma de proteção em ambos os lados. Olá figura a seguir mostra um exemplo de uma rede de perímetro de única sub-rede em uma rede corporativa, com dois limites de segurança.

![3]

Há muitos tooimplement de arquiteturas usadas com uma rede de perímetro. Essas arquiteturas podem variar de uma rede de perímetro de várias sub-redes de tooa de Balanceador de carga simples com diferentes mecanismos em tráfego de tooblock cada limite e proteger as camadas de hello mais profundas da rede corporativa hello. Como a rede de perímetro Olá é criada depende necessidades específicas de saudação da organização de saudação e sua tolerância ao risco geral.

Como os clientes mudam suas nuvens de toopublic de cargas de trabalho, é toosupport crítico de recursos semelhantes para arquitetura de rede de perímetro no Azure toomeet requisitos de conformidade e segurança. Este documento fornece diretrizes sobre como os clientes podem criar um ambiente de rede segura no Azure. Ele se concentra na rede de perímetro hello, mas também inclui uma discussão abrangente de muitos aspectos de segurança de rede. Esta discussão informá-Olá perguntas a seguir:

* Como é possível criar uma rede de perímetro no Azure?
* Quais são de rede de perímetro Olá recursos do Azure disponíveis toobuild Olá?
* Como cargas de trabalho de back-end podem ser protegidas?
* Como são toohello Internet comunicações controladas cargas de trabalho no Azure?
* Como as redes locais de saudação podem ser protegidas de implantações no Azure?
* Quando recursos de segurança nativos do Azure devem ser usados em vez de dispositivos ou serviços de terceiros?

Olá diagrama a seguir mostra várias camadas de segurança que Azure fornece toocustomers. Essas camadas são nativo em Olá plataforma do Azure e recursos definidos pelo cliente:

![4]

Entrada de saudação à Internet, DDoS Azure ajuda a proteger contra ataques em grande escala no Azure. Olá próxima camada é definida pelo cliente endereços IP públicos (pontos de extremidade), que são usado toodetermine tráfego que pode passar por rede virtual do hello nuvem serviço toohello. O isolamento de rede virtual nativa do Azure garante o isolamento completo de todas as outras redes e garante que o tráfego flua somente através de métodos e caminhos configurados pelo usuário. Esses caminhos e os métodos são próxima camada hello, onde os NSGs, UDR e dispositivos de rede virtual podem ser toocreate usada segurança limites tooprotect Olá implantações de aplicativos em rede Olá protegido.

Olá próxima seção fornece uma visão geral de redes virtuais do Azure. As redes virtuais do Azure são criadas por clientes e tratam-se daquilo a que as cargas de trabalho implantadas por esses clientes estão conectadas. Redes virtuais são a base de saudação de todos os recursos de segurança de rede Olá necessário tooestablish uma implantações de cliente de tooprotect da rede de perímetro no Azure.

## <a name="overview-of-azure-virtual-networks"></a>Visão geral das redes virtuais do Azure
Antes do tráfego da Internet pode obter toohello redes virtuais do Azure, há duas camadas de segurança inerentes toohello plataforma Windows Azure:

1.    **Proteção DDoS**: proteção DDoS é uma camada de saudação do Azure rede física que protege Olá plataforma do Azure em si contra ataques de baseado na Internet em larga escala. Esses ataques usam vários nós de "bot" toooverwhelm uma tentativa de um serviço de Internet. O Azure tem uma malha de proteção sólida contra DDoS em todas as conexões de entrada, saída e entre regiões do Azure. Essa camada de proteção DDoS sem atributos configuráveis do usuário e não é acessível toohello cliente. camada de proteção DDoS Olá protege o Azure como uma plataforma de ataques em grande escala, ele também monitora o tráfego de saída e tráfego de região do Azure entre. Usando dispositivos de rede virtual no hello VNet, camadas adicionais de resiliência podem ser configuradas pelo cliente Olá contra um ataque de escala menor que não trip proteção em nível de plataforma hello. Um exemplo de DDoS em ação; Se um endereço IP de com a internet foi atacados por um ataque de DDoS em larga escala, Azure detecte fontes Olá Olá ataques e limpar Olá afetada tráfego antes de que atingiu seu destino pretendido. Em quase todos os casos, hello atacado do ponto de extremidade não é afetado por ataque hello. Em Olá raros casos em que um ponto de extremidade é afetado, nenhum tráfego é afetado tooother pontos de extremidade, apenas Olá atacado ponto de extremidade. Assim, outros clientes e serviços não veem nenhum impacto vindo desse ataque. É crítico toonote que DDoS Azure só está procurando por ataques em larga escala. É possível que seu serviço específico pode ser sobrecarregado antes Olá plataforma proteção limites são excedidos. Por exemplo, um site da Web em um único servidor IIS A0 poderia ficar offline devido a um ataque de DDoS antes que a proteção contra DDoS no nível de plataforma do Azure registrasse uma ameaça.

2.  **Endereços IP públicos**: IP público endereços (habilitados por meio de pontos de extremidade de serviço, endereços IP públicos, Application Gateway e outros recursos do Azure que apresentam um público toohello internet roteadas tooyour recurso de endereço IP) permitem que os serviços de nuvem ou grupos de recurso toohave endereços de IP da Internet públicos e portas expostas. ponto de extremidade de saudação usa a conversão de endereço de rede (NAT) tooroute tráfego toohello interno endereço e porta no hello rede virtual do Azure. Esse caminho é a principal maneira Olá para toopass tráfego externo na rede virtual hello. endereços IP públicos de saudação são configurável toodetermine tráfego que é passado e como e onde ele é convertido em rede virtual toohello.

Depois que o tráfego chegue a rede virtual hello, há muitos recursos que entram em cena. Redes virtuais do Azure são Olá base para os clientes tooattach suas cargas de trabalho e onde básicos de segurança de nível de rede se aplica. É uma rede privada (uma sobreposição de rede virtual) no Azure para clientes com hello recursos e as características a seguir:

* **Isolamento de tráfego**: uma rede virtual é o limite de isolamento de tráfego Olá em Olá plataforma Windows Azure. Máquinas virtuais (VMs) em uma rede virtual não pode se comunicar diretamente tooVMs em uma rede virtual diferente, mesmo se as duas redes virtuais são criadas por Olá mesmo cliente. Isolamento é uma propriedade vital que garante que as VMs e as comunicações do cliente permaneçam privadas em uma rede virtual.

>[!NOTE]
>Isolamento de tráfego refere-se apenas tootraffic *entrada* rede virtual toohello. Pelo tráfego de saída padrão da saudação VNet toohello internet é permitida, mas pode ser evitado se desejado, os NSGs.
>
>

* **Topologia de multicamadas**: redes virtuais permitem que os clientes toodefine topologia de multicamadas alocando sub-redes e designar espaços de endereço separados para diferentes elementos ou "níveis" de suas cargas de trabalho. Esses agrupamentos lógicos e topologias habilitar política de acesso diferente de toodefine de clientes com base nos tipos de carga de trabalho hello e também controlam os fluxos de tráfego entre os níveis de saudação.
* **Conectividade entre locais**: os clientes podem estabelecer a conectividade entre locais entre uma rede virtual e vários sites locais ou outras redes virtuais no Azure. tooconstruct uma conexão, os clientes podem usar o emparelhamento de rede virtual, Gateways de VPN do Azure, soluções de virtualização de rede de terceiros ou rota expressa. O Azure dá suporte a VPNs site a site (S2S) usando protocolos padrão de IPsec/IKE e conectividade privada de ExpressRoute.
* **NSG** permite que os clientes toocreate regras (ACLs) no nível desejada de saudação de granularidade: subredes virtuais, VMs individuais ou interfaces de rede. Clientes podem controlar o acesso ao permitir ou negar a comunicação entre as cargas de trabalho de saudação em uma rede virtual, de sistemas de redes do cliente por meio da conectividade entre locais, ou direcionar comunicação na Internet.
* **UDR** e **encaminhamento IP** permitem que os clientes toodefine caminhos de comunicação de saudação entre níveis diferentes em uma rede virtual. Os clientes podem implantar firewall, IDS/IPS e outras soluções de virtualização, além de rotear o tráfego de rede por meio dessas soluções de segurança para a aplicação, auditoria e inspeção das políticas de limites de segurança.
* **Soluções de virtualização de rede** em hello Azure Marketplace: dispositivos de segurança, como firewalls, balanceadores de carga e IDS/IPS estão disponíveis em hello Azure Marketplace e Olá Galeria de imagens de VM. Os clientes podem implantar esses aplicativos em suas redes virtuais e, especificamente, no seu ambiente de rede segura do segurança limites (incluindo sub-redes de rede de perímetro Olá) toocomplete um várias camadas.

Com esses recursos e funções, um exemplo de como uma arquitetura de rede de perímetro pode ser criada no Azure é hello diagrama a seguir:

![5]

## <a name="perimeter-network-characteristics-and-requirements"></a>Requisitos e características da rede de perímetro
rede de perímetro Olá é Olá front-end da rede hello, comunicação de saudação Internet diretamente em uma interface. pacotes de entrada Hello devem fluir através de dispositivos de segurança hello, como firewall hello, IDS e IPS, antes de alcançar os servidores de back-end de saudação. Pacotes direcionado à Internet de cargas de trabalho Olá também podem fluir através de dispositivos de segurança Olá na rede de perímetro Olá para imposição de política, inspeção e auditoria, antes de sair da rede de saudação. Além disso, a rede de perímetro Olá pode hospedar gateways VPN entre locais entre redes virtuais do cliente e redes locais.

### <a name="perimeter-network-characteristics"></a>Características da rede de perímetro
Algumas das características de saudação de uma rede de perímetro boa referência figura anterior hello, são da seguinte maneira:

* Voltada para a Internet:
  * sub-rede de rede de perímetro Olá em si é voltado para a Internet, se comunicar diretamente com hello da Internet.
  * Endereços IP públicos, VIPs e/ou pontos de extremidade de serviço passam dispositivos e a rede front-end de toohello de tráfego de Internet.
  * O tráfego de entrada da saudação que Internet passa por meio de dispositivos de segurança antes de outros recursos na rede de front-end de saudação.
  * Se segurança de saída estiver habilitada, o tráfego passa por dispositivos de segurança, como etapa final do hello, antes de passar toohello da Internet.
* Rede protegida:
  * Há um caminho direto de infraestrutura básica do hello Internet toohello.
  * Infraestrutura de núcleo toohello canais deve percorrer dispositivos de segurança, como os NSGs, firewalls ou dispositivos VPN.
  * Outros dispositivos não devem ligar a infraestrutura básica de Internet e hello.
  * Dispositivos de segurança nos dois Olá voltado para a Internet e rede protegida hello, voltados para limites de rede de perímetro da saudação (por exemplo, Olá dois firewall ícones mostrados na figura anterior Olá), na verdade, pode ser um único dispositivo virtual com regras diferenciados ou interfaces de cada limite. Por exemplo, um dispositivo físico, separado logicamente, tratamento de carga para os limites de rede de perímetro Olá Olá.
* Outras práticas e restrições comuns:
  * As cargas de trabalho não devem armazenar informações essenciais aos negócios.
  * Implantações e acesso e atualização de configurações de rede tooperimeter são administradores de tooonly limitada autorizado.

### <a name="perimeter-network-requirements"></a>Requisitos de rede de perímetro
tooenable essas características, siga estas diretrizes sobre requisitos de rede virtual tooimplement uma rede de perímetro com êxito:

* **Arquitetura de sub-rede:** especifique Olá virtual rede, de modo que uma sub-rede inteira dedicada como rede de perímetro hello, separadas de outras sub-redes em Olá mesmo rede virtual. Essa separação garante que o tráfego entre a rede de perímetro hello e outros fluxos de camadas de sub-rede interna ou privada por meio de um firewall ou dispositivo virtual IDS/IPS hello.  Rotas definidas pelo usuário no limite de saudação sub-redes são necessárias tooforward este dispositivo virtual do toohello de tráfego.
* **NSG:** sub-rede de rede de perímetro Olá em si deve ser tooallow abrir comunicação com hello da Internet, mas isso não significa que os clientes devem ser ignorando os NSGs. Siga comuns segurança práticas toominimize Olá rede superfícies expostos toohello da Internet. Bloquear intervalos de endereço remoto Olá permitido implantações de saudação tooaccess ou protocolos de aplicativo específico hello e portas que estão abertas. Pode haver circunstâncias, porém, em que um bloqueio total não é possível. Por exemplo, se os clientes têm um site externo no Azure, rede de perímetro Olá deve permitir que as solicitações da web hello de endereços IP públicos, mas só deve abrir portas do aplicativo web hello: TCP na porta 80 e/ou TCP na porta 443.
* **Tabela de roteamento:** sub-rede de rede de perímetro Olá em si deve ser capaz de toocommunicate toohello Internet diretamente, mas não deve permitir a comunicação direta tooand de redes back Olá final ou no local sem passar por um firewall ou dispositivo de segurança.
* **Configuração de dispositivo de segurança:** tooroute e inspecionar os pacotes entre rede de perímetro hello e rest Olá de redes Olá protegido, Olá dispositivos de segurança, como firewall, IDS, e dispositivos IPS podem ser multihomed. Eles podem ter NICs separadas para a rede de perímetro hello e sub-redes de back-end de saudação. Olá NICs na rede de perímetro Olá se comuniquem diretamente tooand de saudação da Internet, com hello NSGs correspondentes e perímetro Olá tabela de roteamento de rede. NICs Olá a conexão de sub-redes de back-end toohello mais tem restringido os NSGs e tabelas de roteamento de sub-redes de back-end correspondente hello.
* **Funcionalidade do dispositivo de segurança:** dispositivos de segurança Olá implantados na rede de perímetro do hello normalmente executam Olá funcionalidade a seguir:
  * Firewall: Impor regras de firewall ou políticas de controle de acesso para as solicitações de entrada hello.
  * Detecção e prevenção de ameaças: detectando e reduzindo ataques mal-intencionados de saudação à Internet.
  * Auditoria e registro em log: mantém logs detalhados de auditoria e análise.
  * Proxy reverso: redirecionamento de entrada hello solicitações toohello correspondente servidores de back-end. Esse redirecionamento envolve o mapeamento e normalmente conversão de endereços de destino de saudação em dispositivos de front-end hello, firewalls, toohello endereços de servidor back-end.
  * Encaminhar proxy: fornecendo NAT e realizar a auditoria para comunicações iniciada a partir Olá toohello de rede virtual da Internet.
  * Roteador: Encaminhar o tráfego de entrada e de sub-rede cruzado dentro da rede virtual hello.
  * Dispositivo VPN: agindo como saudação entre locais gateways VPN para conectividade entre locais VPN entre redes de local de clientes e redes virtuais do Azure.
  * Servidor VPN: aceitar clientes VPN conectando redes virtuais tooAzure.

> [!TIP]
> Lembre-Olá separado de dois grupos a seguir: indivíduos Olá tooaccess Olá perímetro rede segurança engrenagem e hello pessoas autorizadas autorizadas como administradores de aplicativo de desenvolvimento, implantação ou operações. Manter esses grupos separados permite uma diferenciação de deveres e impede que uma única pessoa ignore controles de segurança de aplicativos e de rede.
>
>

### <a name="questions-toobe-asked-when-building-network-boundaries"></a>Toobe perguntas frequentes ao criar limites de rede
Nesta seção, a menos que especificamente mencionado, Olá termo "redes" refere-se tooprivate Azure redes virtuais criadas por um administrador de assinatura. termo de saudação não se refere a redes físicas subjacentes de toohello dentro do Azure.

Além disso, redes virtuais do Azure costumam ser usadas tooextend local tradicional redes. É possível tooincorporate site a site ou rota expressa híbrida soluções com arquiteturas de rede de perímetro de rede. Esse link híbrido é uma consideração importante na criação de limites de segurança de rede.

Olá seguintes três perguntas estão tooanswer crítico quando você estiver criando uma rede com uma rede de perímetro e vários limites de segurança.

#### <a name="1-how-many-boundaries-are-needed"></a>1) Quantos limites são necessários?
Olá primeiro ponto de decisão é toodecide quantos limites de segurança são necessários em um determinado cenário:

* Um único limite: uma na rede de perímetro front-end de saudação entre a rede virtual hello e hello Internet.
* Dois limites: um no hello lado de Internet da rede de perímetro do hello e outro entre sub-redes de rede de perímetro hello e sub-redes de back-end de saudação em Olá redes virtuais do Azure.
* Limites de três: um no lado de Internet de saudação da rede de perímetro hello, um entre a rede de perímetro hello e sub-redes de back-end e uma entre as sub-redes de back-end de saudação e rede de local de saudação.
* Limites de N: um número variável. Dependendo dos requisitos de segurança, não há nenhum toohello limitar o número de limites de segurança que podem ser aplicadas em uma determinada rede.

Hello número e tipo de limites necessários variam com base em risco tolerância e hello cenário específico uma empresa que está sendo implementado. Geralmente essa é uma decisão conjunta tomada por vários grupos dentro de uma organização, muitas vezes incluindo uma equipe de risco e conformidade, uma equipe de rede e plataforma e uma equipe de desenvolvimento de aplicativos. Pessoas com conhecimento de segurança, Olá dados envolvidos e tecnologias hello está sendo usadas devem ter uma diga nessa postura de segurança apropriadas decisão tooensure Olá para cada implementação.

> [!TIP]
> Use o menor número de saudação de limites que atender aos requisitos de segurança Olá uma situação. Com os limites de mais operações e solução de problemas podem ser mais difícil, bem como Olá gerenciamento sobrecarga envolvida ao gerenciamento Olá várias políticas de limites ao longo do tempo. No entanto, os limites insuficientes aumentam o risco. Localizando saldo de saudação é crítico.
>
>

![6]

Olá figura anterior mostra uma visão geral de uma rede de limite de segurança de três. limites de saudação são entre Olá perímetro e Olá Internet, hello Azure front-end e back-end subredes privadas e Olá sub-rede de back-end do Azure e rede Olá local corporativa.

#### <a name="2-where-are-hello-boundaries-located"></a>2) onde estão localizados os limites de Olá?
Depois que o número de saudação de limites é decidir, onde tooimplement-los é Olá próximo ponto de decisão. Geralmente, há três opções:

* Usar um serviço intermediário baseado na Internet (por exemplo, um firewall do aplicativo Web baseado em nuvem, que não é discutido neste documento)
* Usar recursos nativos e/ou soluções de virtualização de rede no Azure
* Usando dispositivos físicos na rede de local de saudação

Em redes puramente do Azure, opções de saudação são recursos nativos do Azure (por exemplo, balanceadores de carga do Azure) ou dispositivos de rede virtual do hello ecossistema de parceiros rico do Azure (por exemplo, firewalls de ponto de verificação).

Se for necessário um limite entre o Azure e uma rede local, dispositivos de segurança Olá podem residir em um dos lados da conexão hello (ou ambos os lados). Assim, uma decisão deve ser feita em equipamentos de segurança de tooplace Olá local.

Na figura anterior do hello, rede de Internet à perímetro hello e limites de frente para back-end de saudação contidos inteiramente no Azure em devem ser nativo recursos do Azure ou dispositivos de rede virtual. Dispositivos de segurança em Olá limite entre o Azure (sub-rede de back-end) e rede corporativa Olá poderia ser nos saudação do lado do Azure ou no lado do local de saudação ou até mesmo uma combinação de dispositivos em ambos os lados. Pode haver vantagens significativas e opção de tooeither desvantagens que deve ser considerada sério.

Por exemplo, usando a engrenagem de segurança física existente no hello local lado de rede tem a vantagem de saudação que nenhum novo engrenagem é necessária. Ele precisa apenas de reconfiguração. desvantagem Hello, no entanto, é que todo o tráfego deve volta provenientes do Azure toohello local rede toobe visto pelo mecanismo de segurança de saudação. Assim, o tráfego do Azure para o Azure pode incorrer em latência significativa e afetam a experiência de usuário e o desempenho do aplicativo, se ela foi forçada toohello Voltar no local de rede para a imposição de política de segurança.

#### <a name="3-how-are-hello-boundaries-implemented"></a>3) como os limites de saudação são implementados?
Cada limite de segurança provavelmente terão os requisitos de recurso diferente (por exemplo, IDS e regras de firewall no hello lado de Internet da rede de perímetro hello, mas apenas ACLs entre a rede de perímetro hello e sub-rede back-end). Decidir em qual dispositivo (ou quantos dispositivos) toouse depende Olá requisitos do cenário e segurança. Olá seção a seguir, exemplos de 1, 2 e 3 discutem algumas opções que podem ser usadas. Revisar os recursos de rede nativo do Azure hello e dispositivos de saudação disponíveis no Azure do ecossistema de parceiros Olá mostra Olá uma grande variedade de opções disponíveis toosolve praticamente qualquer cenário.

Outro ponto de decisão de implementação de chave é como tooconnect Olá local rede com o Azure. Você deve usar Olá gateway virtual do Azure ou um dispositivo de rede virtual? Essas opções são discutidas em maiores detalhes hello (exemplos 4, 5 e 6) da seção a seguir.

Além disso, o tráfego entre redes virtuais no Azure pode ser necessário. Esses cenários serão adicionados em Olá futuras.

Quando você souber respostas Olá toohello anterior perguntas, Olá [Fast Start](#fast-start) seção pode ajudar a identificar quais exemplos são mais apropriados para um determinado cenário.

## <a name="examples-building-security-boundaries-with-azure-virtual-networks"></a>Exemplos: criando limites de segurança com redes virtuais do Azure
### <a name="example-1-build-a-perimeter-network-toohelp-protect-applications-with-nsgs"></a>Exemplo 1 compilação um toohelp de rede de perímetro proteger aplicativos com os NSGs
[Fazer início tooFast](#fast-start) | [Detailed compilar instruções para este exemplo][Example1]

[![7]][7]

#### <a name="environment-description"></a>Descrição do ambiente
Neste exemplo, há uma assinatura que contém Olá recursos a seguir:

- Um único grupo de recursos
- Uma rede virtual com duas sub-redes: “FrontEnd” e “BackEnd”
- Um grupo de segurança de rede que é aplicada tooboth sub-redes
- Um servidor Windows que representa um servidor Web de aplicativos ("IIS01")
- Dois servidores Windows que representam servidores de back-end de aplicativos ("AppVM01", "AppVM02")
- Um servidor Windows que representa um servidor DNS ("DNS01")
- Um IP público associado Olá aplicativo servidor web

Para scripts e um modelo do Gerenciador de recursos do Azure, consulte Olá [compilação instruções detalhadas][Example1].

#### <a name="nsg-description"></a>Descrição de NSG
Neste exemplo, um grupo NSG é criado e então carregado com seis regras.

> [!TIP]
> Em geral, você deve criar suas regras específicas de "Permitir" primeiro, seguido por hello mais genérico "Negar" regras. Olá priorizada determina quais regras são avaliadas primeiro. Depois que o tráfego for encontrado uma regra específica de tooa tooapply, nenhuma regra adicional será avaliada. Regras NSG podem ser aplicados em um Olá direção de entrada ou saída (da perspectiva de saudação da sub-rede Olá).
>
>

Declarativamente, Olá regras a seguir está sendo compilado para o tráfego de entrada:

1. O tráfego interno de DNS (porta 53) é permitido.
2. O tráfego de RDP (porta 3389) do hello Internet tooany Máquina Virtual é permitido.
3. O tráfego HTTP (porta 80) Olá tooweb do servidor de Internet (IIS01) é permitido.
4. Qualquer tráfego (todas as portas) do IIS01 tooAppVM1 é permitido.
5. Qualquer tráfego (todas as portas) do hello Internet toohello toda rede virtual (ambas as sub-redes) foi negado.
6. Qualquer tráfego (todas as portas) de sub-rede de back-end de toohello Olá sub-rede front-end é negado.

A sub-rede de tooeach associada essas regras, se uma solicitação HTTP foi entrada do servidor web do hello Internet toohello, ambos regras 3 (Permitir) e 5 (Negar) seria aplicável. Mas como a regra 3 tem uma prioridade mais alta, apenas ela seria aplicável e a regra 5 não seria entram em cena. Assim você seria permitido a solicitação HTTP Olá toohello servidor de web. Se esse mesmo tráfego foi a tentativa de servidor de saudação DNS01 tooreach, regra 5 (Negar) seria Olá tooapply primeiro e o tráfego de Olá não deve ser permitido toopass toohello server. Regra de 6 (Negar) blocos Olá sub-rede front-end do falando toohello sub-rede de back-end (com exceção de tráfego permitido nas regras 1 e 4). Esse conjunto de regras protege a rede de back-end Olá no caso de um invasor comprometer o aplicativo da web hello no front-end hello. invasor Olá seria limitada acesso toohello back-end "protegido" rede (somente tooresources exposto no servidor de AppVM01 Olá).

Há uma regra de saída padrão que permite que o tráfego de saída toohello da Internet. Neste exemplo, permitiremos o tráfego de saída e não modificaremos quaisquer regras de saída. toolock tráfego em ambas as direções, roteamento definida pelo usuário é necessário (consulte o exemplo 3).

#### <a name="conclusion"></a>Conclusão
Este exemplo é uma maneira relativamente simple e direta de isolamento de sub-rede de back-end de saudação do tráfego de entrada. Para obter mais informações, consulte Olá [compilação instruções detalhadas][Example1]. Essas instruções incluem:

* Como toobuild desse perímetro rede com clássicos scripts do PowerShell.
* Como toobuild desse perímetro rede com um modelo do Gerenciador de recursos do Azure.
* Descrições detalhadas de cada comando NSG.
* Cenários de fluxo de tráfego detalhados mostrando como o tráfego é permitido ou negado em cada camada.


### <a name="example-2-build-a-perimeter-network-toohelp-protect-applications-with-a-firewall-and-nsgs"></a>Compilação do exemplo 2 um toohelp de rede de perímetro proteger aplicativos com um firewall e NSGs
[Fazer início tooFast](#fast-start) | [Detailed compilar instruções para este exemplo][Example2]

[![8]][8]

#### <a name="environment-description"></a>Descrição do ambiente
Neste exemplo, há uma assinatura que contém Olá recursos a seguir:

* Um único grupo de recursos
* Uma rede virtual com duas sub-redes: “FrontEnd” e “BackEnd”
* Um grupo de segurança de rede que é aplicada tooboth sub-redes
* Um dispositivo virtual de rede, neste caso, um firewall, conectado toohello front-end subrede
* Um servidor Windows que representa um servidor Web de aplicativos ("IIS01")
* Dois servidores Windows que representam servidores de back-end de aplicativos ("AppVM01", "AppVM02")
* Um servidor Windows que representa um servidor DNS ("DNS01")

Para scripts e um modelo do Gerenciador de recursos do Azure, consulte Olá [compilação instruções detalhadas][Example2].

#### <a name="nsg-description"></a>Descrição de NSG
Neste exemplo, um grupo NSG é criado e então carregado com seis regras.

> [!TIP]
> Em geral, você deve criar suas regras específicas de "Permitir" primeiro, seguido por hello mais genérico "Negar" regras. Olá priorizada determina quais regras são avaliadas primeiro. Depois que o tráfego for encontrado uma regra específica de tooa tooapply, nenhuma regra adicional será avaliada. Regras NSG podem ser aplicados em um Olá direção de entrada ou saída (da perspectiva de saudação da sub-rede Olá).
>
>

Declarativamente, Olá regras a seguir está sendo compilado para o tráfego de entrada:

1. O tráfego interno de DNS (porta 53) é permitido.
2. O tráfego de RDP (porta 3389) do hello Internet tooany Máquina Virtual é permitido.
3. Qualquer tráfego (todas as portas) toohello rede virtual appliance de Internet (firewall) é permitido.
4. Qualquer tráfego (todas as portas) do IIS01 tooAppVM1 é permitido.
5. Qualquer tráfego (todas as portas) do hello Internet toohello toda rede virtual (ambas as sub-redes) foi negado.
6. Qualquer tráfego (todas as portas) de sub-rede de back-end de toohello Olá sub-rede front-end é negado.

A sub-rede de tooeach associada essas regras, se uma solicitação HTTP foi entrada de firewall de toohello de saudação, ambos regras 3 (Permitir) e 5 (Negar) seria aplicável. Mas como a regra 3 tem uma prioridade mais alta, apenas ela seria aplicável e a regra 5 não seria entram em cena. Assim, você seria permitido a solicitação de Olá HTTP toohello firewall. Se esse mesmo tráfego foi a tentativa de servidor de saudação IIS01 tooreach, mesmo que ele está na sub-rede front-end hello, regra 5 (Negar) seria aplicada, e o tráfego de Olá não deve ser permitido toopass toohello server. Regra de 6 (Negar) blocos Olá sub-rede front-end do falando toohello sub-rede de back-end (com exceção de tráfego permitido nas regras 1 e 4). Esse conjunto de regras protege a rede de back-end Olá no caso de um invasor comprometer o aplicativo da web hello no front-end hello. invasor Olá seria limitada acesso toohello back-end "protegido" rede (somente tooresources exposto no servidor de AppVM01 Olá).

Há uma regra de saída padrão que permite que o tráfego de saída toohello da Internet. Neste exemplo, permitiremos o tráfego de saída e não modificaremos quaisquer regras de saída. toolock tráfego em ambas as direções, roteamento definida pelo usuário é necessário (consulte o exemplo 3).

#### <a name="firewall-rule-description"></a>Descrição da regra de firewall
No firewall hello, regras de encaminhamento devem ser criada. Como este exemplo somente o tráfego de Internet de entrada de rotas toohello firewall e, em seguida, toohello da web, apenas um servidor de encaminhamento de rede (NAT) de conversão de endereço regra é necessário.

regra de encaminhamento de saudação aceita qualquer endereço de origem de entrada que chega firewall Olá tentar tooreach HTTP (porta 80 ou 443 para HTTPS). Ela tem enviadas fora da interface local do firewall hello e redirecionado toohello web server com hello endereço IP do 10.0.1.5.

#### <a name="conclusion"></a>Conclusão
Este exemplo é uma maneira relativamente simples de proteger seu aplicativo com um firewall e o isolamento de sub-rede de back-end de saudação do tráfego de entrada. Para obter mais informações, consulte Olá [compilação instruções detalhadas][Example2]. Essas instruções incluem:

* Como toobuild desse perímetro rede com clássicos scripts do PowerShell.
* Como toobuild esse exemplo com um modelo do Gerenciador de recursos do Azure.
* Descrições detalhadas de cada comando NSG e regra de firewall.
* Cenários de fluxo de tráfego detalhados mostrando como o tráfego é permitido ou negado em cada camada.

### <a name="example-3-build-a-perimeter-network-toohelp-protect-networks-with-a-firewall-and-udr-and-nsg"></a>Exemplo 3 compilação um toohelp de rede de perímetro proteger redes com um firewall e UDR e NSG
[Fazer início tooFast](#fast-start) | [Detailed compilar instruções para este exemplo][Example3]

[![9]][9]

#### <a name="environment-description"></a>Descrição do ambiente
Neste exemplo, há uma assinatura que contém Olá recursos a seguir:

* Um único grupo de recursos
* Uma rede virtual com três sub-redes; “SecNet”, “FrontEnd” e “BackEnd”
* Um dispositivo virtual de rede, neste caso, um firewall, conectado toohello SecNet sub-rede
* Um servidor Windows que representa um servidor Web de aplicativos ("IIS01")
* Dois servidores Windows que representam servidores de back-end de aplicativos ("AppVM01", "AppVM02")
* Um servidor Windows que representa um servidor DNS ("DNS01")

Para scripts e um modelo do Gerenciador de recursos do Azure, consulte Olá [compilação instruções detalhadas][Example3].

#### <a name="udr-description"></a>Descrição de UDR
Por padrão, a saudação rotas de sistema a seguir é definida como:

        Effective routes :
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.0.0/16}     VNETLocal                            Active   Default    
         {0.0.0.0/0}       Internet                             Active   Default    
         {10.0.0.0/8}      Null                                 Active   Default    
         {100.64.0.0/10}   Null                                 Active   Default    
         {172.16.0.0/12}   Null                                 Active   Default    
         {192.168.0.0/16}  Null                                 Active   Default

Olá VNETLocal é sempre um ou mais prefixos de endereço definida que compõem a rede virtual Olá para essa rede específico (ou seja, ele muda de rede de toovirtual de rede virtual, dependendo de como cada rede virtual específico é definida). rotas de sistema restantes Olá são estáticas e padrão como indicado na tabela de saudação.

Neste exemplo, duas tabelas de roteamento são criados, um para as sub-redes de front-end e back-end de saudação. Cada tabela é carregada com rotas estáticas apropriadas para Olá recebe sub-rede. Neste exemplo, cada tabela tem três rotas que direcionam todo o tráfego (0.0.0.0/0) através do firewall da saudação (próximo salto = endereço IP do dispositivo Virtual):

1. O tráfego de sub-rede local com não próximo salto definido tooallow sub-rede local o tráfego toobypass Olá firewall.
2. Tráfego de rede virtual com um Próximo Salto definido como firewall. Este próximo salto substituições Olá regra padrão que permite tooroute de tráfego de rede virtual local diretamente.
3. Todos os tráfego restante (0/0) com o próximo nó definido como Olá firewall.

> [!TIP]
> Sem entrada de sub-rede local Olá no hello UDR quebras sub-rede local comunicações.
>
> * Em nosso exemplo, é essencial 10.0.1.0/24 apontando tooVNETLocal! Sem ele, deixando Olá Web Server (10.0.1.4) destinado tooanother local server 10.0.1.25 (por exemplo) do pacote falhará, pois eles serão enviados toohello NVA. Olá NVA será enviado toohello subrede e sub-rede Olá vai reenviar toohello NVA em um loop infinito.
> * a probabilidade de saudação de um loop de roteamento é normalmente mais alta em dispositivos com várias placas de rede que estão conectados tooseparate sub-redes, que é geralmente de dispositivos de local tradicional.
>
>

Após a criação de tabelas de roteamento hello, eles devem ser associadas tootheir sub-redes. Olá sub-rede front-end, tabela de roteamento, uma vez criado e associado a sub-rede toohello, seria semelhante esta saída:

        Effective routes :
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.1.0/24}     VNETLocal                            Active
         {10.0.0.0/16}     VirtualAppliance 10.0.0.4            Active    
         {0.0.0.0/0}       VirtualAppliance 10.0.0.4            Active

> [!NOTE]
> UDR agora podem ser toohello aplicados sub-rede do gateway no qual Olá rota expressa o circuito está conectado.
>
> Exemplos de como tooenable o perímetro da rede com a rede de site a site ou rota expressa são mostrados nos exemplos 3 e 4.
>
>

#### <a name="ip-forwarding-description"></a>Descrição de Encaminhamento IP
Encaminhamento de IP é um tooUDR de recurso complementar. Encaminhamento de IP é uma configuração em um dispositivo virtual que permite que ele tooreceive o tráfego endereçado não especificamente toohello dispositivo e, em seguida, encaminhe destino tráfego tooits ultimate.

Por exemplo, se AppVM01 faz uma solicitação ao servidor toohello DNS01, UDR seria rotear esse tráfego toohello firewall. Com o encaminhamento IP habilitado, tráfego Olá para o destino de DNS01 hello (10.0.2.4) é aceito pelo dispositivo hello (10.0.0.4) e, em seguida, encaminhado destino final de tooits (10.0.2.4). Sem o encaminhamento IP habilitada no firewall hello, tráfego seria não aceito pelo dispositivo Olá, embora a tabela de rotas Olá firewall hello como o próximo salto de saudação. toouse um dispositivo virtual, é crítico tooremember tooenable IP juntamente com UDR de encaminhamento.

#### <a name="nsg-description"></a>Descrição de NSG
Neste exemplo, um grupo NSG é criado e então carregado com uma única regra. Esse grupo, em seguida, é associado somente toohello front-end e back-end sub-redes (não Olá SecNet). Declarativamente Olá regra a seguir está sendo compilado:

* Qualquer tráfego (todas as portas) do hello Internet toohello toda rede virtual (todas as sub-redes) foi negado.

Embora NSGs sejam usados neste exemplo, seu principal objetivo será ser como uma segunda camada de defesa contra erros de configuração manual. Olá meta é tooblock todo o tráfego de entrada hello Internet tooeither Olá sub-redes de front-end ou back-end. Tráfego só deve fluir através do firewall do hello SecNet sub-rede toohello (e, se apropriado, em sub-redes toohello de front-end ou back-end). Além disso, com as regras UDR Olá em vigor, qualquer tráfego torná-lo em Olá front-end ou back-end subredes seria direcionado out toohello firewall (Obrigado tooUDR). firewall Olá veria esse tráfego como um fluxo assimétrico e ficaria o tráfego de saída hello. Assim, há três camadas de segurança protegendo sub-redes hello:

* Não há endereços IP públicos em nenhuma NIC de front-end ou back-end.
* NSGs negar o tráfego de saudação à Internet.
* Olá soltar assimétricas o tráfego de firewall.

Um ponto interessante sobre Olá NSG neste exemplo é que ele contém apenas uma regra, que é toodeny Internet tráfego toohello toda rede virtual, inclusive Olá segurança sub-rede. No entanto, como Olá que NSG só é associado toohello front-end e back-end sub-redes, a regra de saudação não são processadas no tráfego de entrada toohello sub-rede de segurança. Como resultado, o tráfego passa toohello sub-rede de segurança.

#### <a name="firewall-rules"></a>Regras de firewall
No firewall hello, regras de encaminhamento devem ser criada. Como bloqueio ou o encaminhamento de todas as entrada, saído e o tráfego de rede virtual entre firewall hello, várias regras de firewall são necessárias. Além disso, todo o tráfego de entrada atinge o endereço IP público de serviço de segurança hello (em portas diferentes), toobe processadas pelo firewall hello. Uma prática recomendada é fluxos de lógica de Olá toodiagram antes de configurar sub-redes hello e regras de firewall, tooavoid retrabalho mais tarde. Olá figura a seguir é uma exibição lógica de regras de firewall Olá para este exemplo:

![10]

> [!NOTE]
> Portas de gerenciamento de saudação com base na Olá usado do dispositivo de rede Virtual, variam. Neste exemplo, um Firewall NextGen Barracuda é mencionado e usa as portas 22, 801 e 807. Consulte Olá appliance fornecedor documentação toofind Olá exata portas usadas para o gerenciamento de dispositivo hello está sendo usado.
>
>

#### <a name="firewall-rules-description"></a>Descrição das regras de firewall
Olá anterior diagrama lógico, sub-rede de segurança Olá não é mostrado como o firewall Olá único recurso Olá nessa sub-rede. diagrama de saudação está mostrando as regras de firewall hello e como eles logicamente permitem ou negar fluxos de tráfego, não Olá roteados caminho real. Além disso, dois octetos do endereço IP local do Olá para facilitar a leitura mais fácil da última portas externas de saudação selecionadas para Olá tráfego RDP são portas intervalos superior (8014 – 8026) e foram selecionado tooloosely alinhada hello (por exemplo, o endereço do servidor local 10.0.1.4 está associado com a porta externa 8014). No entanto, todas as portas não conflitantes acima disso poderiam ser usadas.

Para este exemplo, precisamos de sete tipos de regras:

* Regras externas (para o tráfego de entrada):
  1. Regra de firewall de gerenciamento: uma regra de redirecionamento deste aplicativo permite tráfego toopass toohello as portas de gerenciamento do dispositivo virtual de rede hello.
  2. Regras RDP (para cada servidor do Windows): essas quatro regras (uma para cada servidor) permitem o gerenciamento de saudação servidores individuais via RDP. quatro regras RDP Olá também podem ser recolhidas em uma regra, dependendo de recursos Olá Olá rede da solução de virtualização que está sendo usado.
  3. Regras de tráfego do aplicativo: há dois essas regras, Olá primeiro para o tráfego da web front-end de hello e Olá segundo para o tráfego de back-end da saudação (por exemplo, servidor toodata camada da web). configuração de saudação dessas regras depende de arquitetura de rede de saudação (em que os servidores são colocados) e fluxos de tráfego (fluxos de tráfego que Olá direção e quais portas são usadas).
     * primeira regra de saudação permite que o servidor de aplicativos do hello aplicativo real tráfego tooreach hello. Enquanto hello outras regras permitirem gerenciamento e segurança, regras de tráfego do aplicativo são o que permitem que os tooaccess usuários ou serviços externos Olá aplicativos. Neste exemplo, há um único servidor Web na porta 80. Portanto, uma regra de firewall único de aplicativo redireciona IP externo do tráfego de entrada toohello, toohello web interno endereço IP de servidores. sessão de tráfego Olá redirecionado deve ser convertida por meio do servidor interno do NAT toohello.
     * segunda regra de saudação é Olá regra de back-end tooallow Olá servidor tootalk toohello AppVM01 servidor web (mas não AppVM02) por meio de qualquer porta.
* Regras internas (para tráfego entre redes virtuais)
  1. Regra de saída tooInternet: esta regra permitir o tráfego de qualquer rede toopass toohello selecionado redes. Geralmente, essa regra é uma regra padrão já está no firewall hello, mas em um estado desabilitado. Essa regra deve ser habilitada para esse exemplo.
  2. Regra DNS: essa regra permite que somente o DNS (porta 53) tráfego toopass toohello servidor DNS. Para esse ambiente, a maior parte do tráfego de saudação front-end toohello back-end está bloqueada. Essa regra permite especificamente DNS de qualquer sub-rede local.
  3. Regra de toosubnet de sub-rede: esta regra é tooallow qualquer servidor no servidor do hello sub-rede back-end tooconnect tooany na sub-rede front-end da saudação (mas não Olá inversa).
* Regra à prova de falhas (para o tráfego que não atende a qualquer um de saudação anterior):
  1. Negar todas as regras de tráfego: essa regra de negação sempre deve ter a regra final hello (em termos de prioridade), e como tal, se um fluxo de tráfego falhar toomatch qualquer Olá anterior regras serão descartados por essa regra. Essa regra é uma regra padrão e geralmente in-loco e ativa. Nenhuma modificação é geralmente necessários toothis regra.

> [!TIP]
> Em Olá qualquer porta segundo aplicativo tráfego regra, toosimplify neste exemplo, é permitida. Em um cenário real, intervalos de porta e endereço de mais específicos de Olá devem ser superfície de ataque de saudação tooreduce usada dessa regra.
>
>

Após a criação de regras anteriores Olá, é importante tooreview prioridade de saudação do tráfego de tooensure cada regra é permitida ou negada conforme desejado. Neste exemplo, as regras de saudação são em ordem de prioridade.

#### <a name="conclusion"></a>Conclusão
Este exemplo é um mais complexo, porém concluída de maneira de proteger e isolar a rede Olá de Olá exemplos anteriores. (Exemplo 2 protege apenas o aplicativo hello e exemplo 1 apenas isola sub-redes). Esse design permite monitorar o tráfego em ambas as direções e protege não apenas os servidores de aplicativo de entrada hello mas impõe a política de segurança de rede para todos os servidores na rede. Além disso, dependendo do dispositivo Olá usado, reconhecimento e o tráfego total de auditoria podem ser obtidos. Para obter mais informações, consulte Olá [compilação instruções detalhadas][Example3]. Essas instruções incluem:

* Como toobuild desse perímetro exemplo rede com clássicos scripts do PowerShell.
* Como toobuild esse exemplo com um modelo do Gerenciador de recursos do Azure.
* As descrições detalhadas de cada comando NSG, UDR e regra de firewall.
* Cenários de fluxo de tráfego detalhados mostrando como o tráfego é permitido ou negado em cada camada.

### <a name="example-4-add-a-hybrid-connection-with-a-site-to-site-virtual-appliance-vpn"></a>Exemplo 4: adicionar uma conexão híbrida com uma VPN de solução de virtualização site a site
[Fazer início tooFast](#fast-start) | Obter instruções de compilação disponível em breve

[![11]][11]

#### <a name="environment-description"></a>Descrição do ambiente
Rede híbrida usando um dispositivo de rede virtual (NVA) pode ser adicionado tooany dos tipos de rede de perímetro Olá descritos nos exemplos 1, 2 ou 3.

Conforme mostrado na figura anterior hello, uma conexão VPN sobre Olá Internet (site a site) é usado tooconnect um tooan de rede local a rede virtual do Azure por meio de uma NVA.

> [!NOTE]
> Se você usar o ExpressRoute com opção de emparelhamento público do Azure Olá habilitada, uma rota estática deve ser criada. Essa rota estática deve encaminhar toohello endereço de IP de VPN de NVA seu corporativo na Internet e não por meio de saudação conexão de rota expressa. Olá NAT necessário em Olá opção emparelhamento público de rota expressa do Azure pode interromper a sessão VPN hello.
>
>

Após a saudação VPN está em vigor, Olá NVA é hub central de saudação para todas as redes e sub-redes. regras de encaminhamento de firewall Olá determinam qual fluxos são permitidos, o tráfego são convertidas por meio de NAT, serão redirecionadas ou são descartados (mesmo para fluxos de tráfego entre a rede de local de saudação e Azure).

Fluxos de tráfego devem ser considerados com cuidado, como eles podem ser otimizados ou degradado, o padrão de design, dependendo da saudação específica caso de uso.

Usando o ambiente de saudação criado no exemplo 3 e, em seguida, adicionar uma conexão de rede do site a site VPN híbrida, produz Olá design a seguir:

[![12]][12]

Olá local roteador ou outro dispositivo de rede que é compatível com sua NVA para VPN, seria do cliente VPN hello. Esse dispositivo físico seria responsável por iniciar e manter a conexão de VPN Olá com seu NVA.

Logicamente toohello NVA, rede Olá parece quatro separado "zonas de segurança", com as regras de saudação na Olá NVA sendo Diretor de saudação primário do tráfego entre essas regiões:

![13]

#### <a name="conclusion"></a>Conclusão
adição de saudação de uma conexão de rede de híbrida VPN site a site tooan rede virtual do Azure pode estender a rede de local de saudação no Azure de forma segura. Usando uma conexão VPN, o tráfego é criptografado e roteia via Olá da Internet. Olá NVA neste exemplo fornece um local central tooenforce e gerenciar a política de segurança de saudação. Para obter mais informações, consulte Olá detalhada compilar instruções (em breve). Essas instruções incluem:

* Como toobuild desse perímetro exemplo rede com scripts do PowerShell.
* Como toobuild esse exemplo com um modelo do Gerenciador de recursos do Azure.
* Cenários de fluxo de tráfego detalhados mostrando como o tráfego flui através desse design.

### <a name="example-5-add-a-hybrid-connection-with-a-site-to-site-azure-vpn-gateway"></a>Exemplo 5: adicionar uma conexão híbrida com um gateway de VPN site a site do Azure
[Fazer início tooFast](#fast-start) | Obter instruções de compilação disponível em breve

[![14]][14]

#### <a name="environment-description"></a>Descrição do ambiente
Tipo de rede de perímetro tooeither descrito nos exemplos 1 ou 2 pode ser adicionado a rede híbrida usando um gateway de VPN do Azure.

Conforme mostrado na saudação anterior figura, uma conexão VPN sobre Olá Internet (site a site) é usado tooconnect um tooan de rede local a rede virtual do Azure por meio de um gateway VPN do Azure.

> [!NOTE]
> Se você usar o ExpressRoute com opção de emparelhamento público do Azure Olá habilitada, uma rota estática deve ser criada. Essa rota estática deve encaminhar toohello endereço de IP de VPN de NVA seu corporativo na Internet e não por meio de saudação WAN de rota expressa. Olá NAT necessário em Olá opção emparelhamento público de rota expressa do Azure pode interromper a sessão VPN hello.
>
>

Olá seguinte figura mostra Olá duas bordas de rede neste exemplo. Na borda da primeira hello, Olá NVA e NSGs controlam fluxos de tráfego para redes do Azure entre e entre o Azure e Olá da Internet. borda segundo Olá é o gateway de VPN do Azure hello, que é uma borda da rede isolada e separados entre local e o Azure.

Fluxos de tráfego devem ser considerados com cuidado, como eles podem ser otimizados ou degradado, o padrão de design, dependendo da saudação específica caso de uso.

Usando o ambiente de saudação criado no exemplo 1 e, em seguida, adicionar uma conexão de rede do site a site VPN híbrida, produz Olá design a seguir:

[![15]][15]

#### <a name="conclusion"></a>Conclusão
adição de saudação de uma conexão de rede de híbrida VPN site a site tooan rede virtual do Azure pode estender a rede de local de saudação no Azure de forma segura. Usando o gateway de VPN do Azure nativo Olá, o tráfego é criptografado IPSec e roteia via Olá da Internet. Além disso, usar o gateway de VPN do Azure Olá pode fornecer uma opção de baixo custo (nenhuma licença adicional de custo como com terceiros NVAs). Essa opção é mais econômica no exemplo 1, em que nenhuma NVA é usada. Para obter mais informações, consulte Olá detalhada compilar instruções (em breve). Essas instruções incluem:

* Como toobuild desse perímetro exemplo rede com scripts do PowerShell.
* Como toobuild esse exemplo com um modelo do Gerenciador de recursos do Azure.
* Cenários de fluxo de tráfego detalhados mostrando como o tráfego flui através desse design.

### <a name="example-6-add-a-hybrid-connection-with-expressroute"></a>Exemplo 6: adicione uma conexão híbrida com o ExpressRoute
[Fazer início tooFast](#fast-start) | Obter instruções de compilação disponível em breve

[![16]][16]

#### <a name="environment-description"></a>Descrição do ambiente
Rede híbrida usando uma rota expressa conexão emparelhamento particular pode ser adicionado o tipo de rede de perímetro tooeither descrito nos exemplos 1 ou 2.

Conforme mostrado na saudação anterior figura, emparelhamento privado da rota expressa fornece uma conexão direta entre sua rede local e hello rede virtual do Azure. Tráfego de trânsito somente rede de provedor de serviços de saudação e de rede do Microsoft Azure hello, nunca tocar saudação da Internet.

> [!TIP]
> Usando o ExpressRoute mantém o tráfego de rede corporativa desligada Olá da Internet. Ele também permite SLAs do seu provedor do ExpressRoute. Olá Gateway Azure pode passar o too10 Gbps com o ExpressRoute, enquanto com VPNs site a site, a taxa de transferência máxima do Gateway Azure Olá é 200 Mbps.
>
>

Conforme visto no diagrama a seguir de saudação, com hello essa opção ambiente agora tem duas bordas de rede. Olá NVA e NSG controle fluxos de tráfego para redes do Azure entre e entre o Azure e Olá Internet, enquanto o gateway de saudação é uma borda da rede isolada e separados entre local e o Azure.

Fluxos de tráfego devem ser considerados com cuidado, como eles podem ser otimizados ou degradado, o padrão de design, dependendo da saudação específica caso de uso.

Usando o ambiente de saudação criado no exemplo 1 e, em seguida, adicionar uma conexão de rede do ExpressRoute híbrida, produz Olá design a seguir:

[![17]][17]

#### <a name="conclusion"></a>Conclusão
adição de saudação de uma conexão de rede privada de rota expressa de emparelhamento pode estender a rede de local de saudação no Azure em uma latência de segura, inferior, superior executar de maneira. Além disso, o Gateway nativo do Azure, como neste exemplo, usando Olá oferece uma opção de baixo custo (não de licenciamento adicional como com terceiros NVAs). Para obter mais informações, consulte Olá detalhada compilar instruções (em breve). Essas instruções incluem:

* Como toobuild desse perímetro exemplo rede com scripts do PowerShell.
* Como toobuild esse exemplo com um modelo do Gerenciador de recursos do Azure.
* Cenários de fluxo de tráfego detalhados mostrando como o tráfego flui através desse design.

## <a name="references"></a>Referências
### <a name="helpful-websites-and-documentation"></a>Sites úteis e documentação
* Acesse o Azure com o Azure Resource Manager:
* Acessando o Azure com o PowerShell: [https://docs.microsoft.com/powershell/azureps-cmdlets-docs/](/powershell/azure/overview)
* Documentação de rede virtual: [https://docs.microsoft.com/azure/virtual-network/](https://docs.microsoft.com/azure/virtual-network/)
* Documentação do grupo de segurança de rede: [https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg](virtual-network/virtual-networks-nsg.md)
* Documentação do roteamento definido pelo usuário: [https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview](virtual-network/virtual-networks-udr-overview.md)
* Gateways virtuais do Azure: [https://docs.microsoft.com/azure/vpn-gateway/](https://docs.microsoft.com/azure/vpn-gateway/)
* VPNs Site a Site: [https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell](vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)
* Documentação de rota expressa (ser toocheck-se de seções de "Introdução" e "como" hello): [https://docs.microsoft.com/azure/expressroute/](https://docs.microsoft.com/azure/expressroute/)

<!--Image References-->
[0]: ./media/best-practices-network-security/flowchart.png "Fluxograma de opções de segurança"
[2]: ./media/best-practices-network-security/azuresecurityfeatures.png "Recursos de segurança do Azure"
[3]: ./media/best-practices-network-security/dmzcorporate.png "Uma DMZ em uma rede corporativa"
[4]: ./media/best-practices-network-security/azuresecurityarchitecture.png "Arquitetura de segurança do Azure"
[5]: ./media/best-practices-network-security/dmzazure.png "Uma DMZ em uma Rede Virtual do Azure"
[6]: ./media/best-practices-network-security/dmzhybrid.png "Rede híbrida com três limites de segurança"
[7]: ./media/best-practices-network-security/example1design.png "DMZ de entrada com NSG"
[8]: ./media/best-practices-network-security/example2design.png "DMZ de entrada com NVA e NSG"
[9]: ./media/best-practices-network-security/example3design.png "DMZ bidirecional com NVA, NSG e UDR"
[10]: ./media/best-practices-network-security/example3firewalllogical.png "exibição lógica de saudação regras de Firewall"
[11]: ./media/best-practices-network-security/example3designoptions.png "DMZ com rede híbrida conectada com NVA"
[12]: ./media/best-practices-network-security/example4designs2s.png "DMZ com NVA conectado usando VPN site a site"
[13]: ./media/best-practices-network-security/example4networklogical.png "Rede lógica da perspectiva de NVA"
[14]: ./media/best-practices-network-security/example5designoptions.png "DMZ com rede híbrida site a site conectada ao Gateway do Azure"
[15]: ./media/best-practices-network-security/example5designs2s.png "DMZ com Gateway do Azure usando VPN site a site"
[16]: ./media/best-practices-network-security/example6designoptions.png "DMZ com rede híbrida da ExpressRoute conectada ao Gateway do Azure"
[17]: ./media/best-practices-network-security/example6designexpressroute.png "DMZ com Gateway do Azure usando uma conexão ExpressRoute"

<!--Link References-->
[TrustCenter]: https://azure.microsoft.com/support/trust-center/compliance/
[Example1]: ./virtual-network/virtual-networks-dmz-nsg.md
[Example2]: ./virtual-network/virtual-networks-dmz-nsg-fw-asm.md
[Example3]: ./virtual-network/virtual-networks-dmz-nsg-fw-udr-asm.md
[Example4]: ./virtual-network/virtual-networks-hybrid-s2s-nva-asm.md
[Example5]: ./virtual-network/virtual-networks-hybrid-s2s-agw-asm.md
[Example6]: ./virtual-network/virtual-networks-hybrid-expressroute-asm.md
[Example7]: ./virtual-network/virtual-networks-vnet2vnet-direct-asm.md
[Example8]: ./virtual-network/virtual-networks-vnet2vnet-transit-asm.md
