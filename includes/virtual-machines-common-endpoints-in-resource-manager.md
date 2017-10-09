pontos de extremidade do Hello abordagem tooAzure funciona um pouco diferente entre os modelos de implantação clássico e o Gerenciador de recursos de saudação. Modelo de implantação do Gerenciador de recursos de hello, agora você tem Olá flexibilidade toocreate filtros de rede que controlam o fluxo de saudação do tráfego dentro e fora de suas VMs. Esses filtros permitem que você os ambientes de rede complexos toocreate além de um ponto de extremidade simple, como no modelo de implantação clássico hello. Este artigo fornece uma visão geral dos Grupos de Segurança de Rede e como eles são diferentes da utilização de pontos de extremidade Clássicos, criando regras de filtragem e exemplos de cenários de implantação.

## <a name="overview-of-resource-manager-deployments"></a>Visão geral das implantações do Resource Manager
Pontos de extremidade no modelo de implantação clássico Olá são substituídos por grupos de segurança de rede e regras ACL (lista) de controle de acesso. As etapas rápidas para implementação de regras de ACL de Grupo de Segurança de Rede são:

* Criará um Grupo de Segurança de Rede.
* tooallow ou negar o tráfego, defina as regras de ACL de grupo de segurança de rede.
* Atribua sua interface de rede de tooa do grupo de segurança de rede ou sub-rede da rede virtual.

Se você está precisando tooalso executar encaminhamento de porta, você precisa tooplace um balanceador de carga na frente de sua VM e usa regras NAT. As etapas rápidas para implementar regras de NAT e um balanceador de carga seriam as seguintes:

* Criar um balanceador de carga.
* Criar um pool de back-end e adicione o pool de toohello de VMs.
* Defina regras de NAT para encaminhamento de porta Olá necessário.
* Atribua regras NAT tooyour VMs.

## <a name="network-security-group-overview"></a>Visão geral do Grupo de Segurança de Rede
Grupos de segurança de rede fornecem uma camada de segurança para você portas específicas tooallow e sub-redes tooaccess suas VMs. Você normalmente sempre tem um grupo de segurança de rede fornecendo essa camada de segurança entre suas máquinas virtuais e Olá fora do mundo. Grupos de segurança de rede podem ser aplicadas tooa sub-rede da rede virtual ou uma interface de rede específico para uma máquina virtual. Em vez de criar regras de ACL do ponto de extremidade, agora é possível criar regras de ACL de Grupo de Segurança de Rede. Essas regras ACL fornecem muito controle maior do que simplesmente criar um ponto de extremidade tooforward uma determinada porta. Para obter mais informações, confira [O que é um Grupo de Segurança de Rede?](../articles/virtual-network/virtual-networks-nsg.md)

> [!TIP]
> Você pode atribuir sub-redes de toomultiple de grupos de segurança de rede ou interfaces de rede. Não há mapeamento 1:1. Você pode criar um grupo de segurança de rede com um conjunto comum de regras de ACL e aplique toomultiple sub-redes ou interfaces de rede. Além disso, o grupo de segurança de rede pode ser tooresources aplicados em sua assinatura (com base em [controles de acesso com base em função](../articles/active-directory/role-based-access-control-what-is.md).

## <a name="load-balancers-overview"></a>Visão geral do balanceador de carga
No modelo de implantação clássico hello, o Azure seria executar todos os Olá conversão de endereço de rede (NAT) e porta encaminhamento de um serviço de nuvem para você. Ao criar um ponto de extremidade, você especificaria Olá porta externa tooexpose juntamente com hello porta interna toodirect tráfego. Os Grupos de Segurança de Rede por si só não executam essa mesma NAT e o encaminhamento de porta. 

tooallow você toocreate as regras de NAT para essa porta de encaminhamento, crie um balanceador de carga do Azure no seu grupo de recursos. Novamente, o balanceador de carga de saudação é granular suficiente tooonly aplicar toospecific VMs, se necessário. Hello Azure carga de trabalho de regras NAT de Balanceador junto com tooprovide de regras de ACL de grupo de segurança de rede muito mais flexibilidade e controle que era possível usar pontos de extremidade de serviço de nuvem. Para obter mais informações, consulte Olá [visão geral do balanceador de carga](../articles/load-balancer/load-balancer-overview.md).

## <a name="network-security-group-acl-rules"></a>Regras de ACL de Grupo de Segurança de Rede
As regras de ACL permitem que você defina o tráfego que pode fluir dentro e fora de sua VM com base em protocolos, intervalos de porta ou portas específicas. As regras são atribuídas tooindividual VMs ou sub-rede tooa. Olá captura de tela a seguir está um exemplo de regras ACL para um servidor da Web comuns:

![Lista de regras de ACL de Grupo de Segurança de Rede](./media/virtual-machines-common-endpoints-in-resource-manager/example-acl-rules.png)

Regras de ACL são aplicadas com base em uma métrica de prioridade que você especificar - valor mais alto de Olá Olá, prioridade inferior a Olá Olá. Cada grupo de segurança de rede tem três padrão as regras que são criadas toohandle fluxo de saudação do tráfego de rede do Azure, com uma explícita `DenyAllInbound` como regra final hello. Regras ACL padrão são fornecido um toonot de baixa prioridade interferir com as regras que você criar.

## <a name="assigning-network-security-groups"></a>Atribuição dos Grupos de Segurança de Rede
Você atribui uma sub-rede de tooa do grupo de segurança de rede ou uma interface de rede. Essa abordagem permite que você toobe como granular conforme necessário ao aplicar a ACL regras tooonly uma VM específica, ou certifique-se de um conjunto comum de ACL de regras são aplicada tooall VMs parte de uma sub-rede:

![Aplicar os NSGs toonetwork interfaces ou sub-redes](./media/virtual-machines-common-endpoints-in-resource-manager/apply-nsg-to-resources.png)

comportamento de saudação do grupo de segurança de rede de saudação não mudar dependendo do que está sendo atribuído a uma interface de rede ou sub-rede tooa. Um cenário de implantação comum tem Olá que grupo de segurança de rede atribuído tooa conformidade de tooensure de sub-rede da sub-rede de toothat anexado todas as VMs. Para obter mais informações, consulte [aplicar segurança de rede grupos tooresources](../articles/virtual-network/virtual-networks-nsg.md#associating-nsgs).

## <a name="default-behavior-of-network-security-groups"></a>Comportamento padrão dos Grupos de Segurança de Rede
Dependendo de como e quando você cria o grupo de segurança de rede, as regras padrão podem ser criadas para acesso RDP toopermit VMs do Windows na porta TCP 3389. Regras padrão para as VMs do Linux permitem o acesso SSH na porta TCP 22. Essas regras ACL automática são criadas em Olá condições a seguir:

* Se você criar uma VM do Windows por meio do portal hello e aceita o saudação padrão ação toocreate um grupo de segurança de rede, uma ACL regra tooallow a porta TCP 3389 (RDP) é criada.
* Se você criar uma VM do Linux por meio do portal hello e aceita o saudação padrão ação toocreate um grupo de segurança de rede, uma ACL regra tooallow a porta TCP 22 (SSH) é criada.

Em todas as outras condições, essas regras ACL padrão não são criadas. Você não pode se conectar tooyour VM sem criar hello regras de ACL apropriadas. Essas condições incluem hello ações comuns a seguir:

* Criando um grupo de segurança de rede por meio do portal hello como saudação de toocreating uma ação separada VM.
* Criação de um Grupo de Segurança de Rede por meio de programação no PowerShell, na CLI do Azure, APIs Rest etc.
* Criar uma VM e atribuí-la tooan existentes do grupo de segurança de rede que ainda não tem regra ACL apropriada Olá definida.

Olá todos os anteriores casos, é necessário toocreate regras de ACL para as conexões do VM tooallow Olá apropriada de gerenciamento remoto.

## <a name="default-behavior-of-a-vm-without-a-network-security-group"></a>Comportamento padrão de uma VM sem um Grupo de Segurança de Rede
Você pode criar uma VM sem criar um Grupo de Segurança de Rede. Nessas situações, você pode se conectar a tooyour VM usando o RDP ou SSH sem criar regras ACL. Da mesma forma, se você instalou um serviço Web na porta 80, esse serviço pode ser acessado automaticamente remotamente. Olá VM tem todas as portas abertas.

> [!NOTE]
> Você ainda precisa toohave um público tooa de endereço atribuído de IP VM para que conexões remotas. Não tem um grupo de segurança de rede para interface de rede ou sub-rede Olá não expõe o tráfego Olá VM tooany externo. ação de padrão de saudação ao criar uma VM por meio do portal Olá é toocreate um novo IP público. Para todas as outras formas de criação de uma VM, como o PowerShell, CLI do Azure ou o modelo do Resource Manager, um IP público não será criado automaticamente se não tiver sido solicitado explicitamente. ação de padrão de saudação por meio do portal Olá também é toocreate um grupo de segurança de rede. Essa ação padrão significa que você não deve terminar em uma situação com uma VM exposta sem uma rede de filtragem em vigor.

## <a name="understanding-load-balancers-and-nat-rules"></a>Noções básicas sobre regras de NAT e balanceadores de carga
No modelo de implantação clássico hello, você pode criar pontos de extremidade que também realizadas encaminhamento de porta. Quando você cria uma máquina virtual no modelo de implantação clássico hello, regras de ACL para RDP ou SSH seriam criadas automaticamente. Essas regras não exporá a porta TCP 3389 ou a porta TCP 22 respectivamente toohello fora do mundo. Em vez disso, uma porta TCP de grande valor estariam exposta que mapeia a porta interna apropriado de toohello. Você também pode criar suas próprias regras ACL de maneira semelhante, como expor um servidor Web em TCP porta toohello 4280 fora do mundo. Você pode ver essas regras ACL e mapeamentos de porta no hello captura de tela a seguir no portal clássico de saudação:

![Encaminhamento de porta com pontos de extremidade Clássicos](./media/virtual-machines-common-endpoints-in-resource-manager/classic-endpoints-port-forwarding.png)

Com os Grupos de Segurança de Rede, essa função de encaminhamento de porta é tratada por um balanceador de carga. Para obter mais informações, confira [balanceadores de carga no Azure](../articles/load-balancer/load-balancer-overview.md). Olá exemplo a seguir mostra um balanceador de carga com um NAT regra tooperform encaminhamento de porta TCP porta 4222 toohello interno a porta TCP 22 uma VM:

![Regras NAT do Balanceador de carga para encaminhamento de porta](./media/virtual-machines-common-endpoints-in-resource-manager/load-balancer-nat-rules.png)

> [!NOTE]
> Quando você implementa um balanceador de carga, você normalmente não atribuir Olá própria máquina virtual um endereço IP público. Em vez disso, o balanceador de carga Olá tem um tooit de endereço atribuído de IP público. Você ainda precisa toocreate seu grupo de segurança de rede e ACL regras toodefine Olá o fluxo de tráfego dentro e fora de sua VM. Olá, regras de NAT de Balanceador de carga são simplesmente toodefine quais portas são permitidas por meio do balanceador de carga hello e como obter distribuídos entre VMs de back-end hello. Como tal, você precisa toocreate uma regra NAT para tráfego tooflow pelo Balanceador de carga de saudação. saudação de tooreach de tráfego do tooallow Olá VM, criar uma regra de ACL de grupo de segurança de rede.
