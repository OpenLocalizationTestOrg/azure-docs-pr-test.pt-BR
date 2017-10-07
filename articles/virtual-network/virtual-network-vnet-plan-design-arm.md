---
title: aaaAzure rede Virtual (VNet) guia de Design e plano | Microsoft Docs
description: Saiba como tooplan e design de redes virtuais no Azure com base nos seus requisitos de isolamento, conectividade e local.
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 3a4a9aea-7608-4d2e-bb3c-40de2e537200
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/08/2016
ms.author: jdial
ms.openlocfilehash: f3ffadf8cf254f64b1f86b44f90315d2bc679f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="plan-and-design-azure-virtual-networks"></a>Planejar e projetar redes virtuais do Azure
Criar um tooexperiment VNet com é muito fácil, mas é provável, você implantará múltiplas VNets sobre necessidades de produção de hello tempo toosupport da sua organização. Com algum planejamento e design, você será capaz de toodeploy VNets e conectar Olá recursos que você precisa com mais eficiência. Se você não estiver familiarizado com VNets, é recomendável que você [saber mais sobre VNets](virtual-networks-overview.md) e [como toodeploy](virtual-networks-create-vnet-arm-pportal.md) um antes de continuar.

## <a name="plan"></a>Plano
Uma compreensão completa de assinaturas do Azure, regiões e recursos de rede é essencial para o sucesso. Você pode usar a lista de saudação das considerações a seguir como um ponto de partida. Depois de entender essas considerações, você pode definir requisitos de saudação para seu design de rede.

### <a name="considerations"></a>Considerações
Antes de responder Olá abaixo de perguntas de planejamento, considere o seguinte de saudação:

* Tudo que você cria no Azure é composto de um ou mais recursos. Uma máquina virtual (VM) é um recurso, Olá adaptador interface de rede (NIC) usado por uma máquina virtual é um recurso de endereço IP público Olá usado por uma NIC é um recurso, Olá VNet Olá NIC é um recurso de toois conectado.
* Criar recursos dentro de uma [Região do Azure](https://azure.microsoft.com/regions/#services) e assinatura. Recursos apenas podem ser conectados tooa rede virtual existente no hello mesmo recurso de saudação de região e assinatura está em.
* Você pode se conectar a redes virtuais tooeach outros usando:
    * **[Emparelhamento de rede virtual](virtual-network-peering-overview.md)**: redes virtuais Olá devem existir no hello mesma região do Azure. Largura de banda entre os recursos em redes virtuais emparelhadas é Olá mesmo que recursos Olá toohello conectado mesma rede virtual.
    * **Um Azure [Gateway VPN](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)**: redes virtuais Olá podem existir em Olá iguais, ou em regiões diferentes do Azure. Largura de banda entre os recursos em redes virtuais conectadas por meio de um Gateway de VPN é limitada pela largura de banda Olá Olá Gateway VPN.
* Você pode se conectar a rede de local de tooyour VNets usando um Olá [opções de conectividade](../vpn-gateway/vpn-gateway-about-vpngateways.md#s2smulti) disponíveis no Azure.
* Recursos diferentes podem ser agrupados em [grupos de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups), tornando mais fácil recursos de saudação toomanage como uma unidade. Um grupo de recursos pode conter recursos de várias regiões, como recursos de saudação pertencer toohello mesma assinatura.

### <a name="define-requirements"></a>Definir requisitos
Use perguntas de saudação abaixo como ponto de partida para o design de rede do Azure.    

1. O que os locais do Azure você vai usar toohost VNets?
2. Você precisa tooprovide comunicação entre esses locais do Azure?
3. Você precisa tooprovide comunicação entre o Azure VNet(s) e datacenter(s) seu local?
4. Quantas VMs de IaaS (Infraestrutura como serviço), funções de serviços de nuvem e aplicativos Web são necessários para sua solução?
5. Você precisa de tráfego de tooisolate com base em grupos de máquinas virtuais (servidores de web ou seja, front-end e servidores de banco de dados de back-end)?
6. Você precisa de fluxo de tráfego toocontrol usando dispositivos virtuais?
7. Fazer os usuários a necessidade para diferentes conjuntos de permissões toodifferent recursos do Azure?

### <a name="understand-vnet-and-subnet-properties"></a>Entender as propriedades de rede virtual e sub-rede
Os recursos de rede virtual e sub-redes ajudam a definir um limite de segurança para cargas de trabalho em execução no Azure. Uma VNet é caracterizada por uma coleção de espaços de endereços, definidos como blocos CIDR.

> [!NOTE]
> Os administradores de rede estão familiarizados com a notação CIDR. Se não estiver familiarizado com o CIDR, [saiba mais sobre ele](http://whatismyipaddress.com/cidr).
>
>

VNets conter Olá propriedades a seguir.

| Propriedade | Descrição | Restrições |
| --- | --- | --- |
| **name** |Nome da VNet |Cadeia de caracteres too80. Pode conter letras, números, sublinhados, pontos ou hifens. Deve começar com uma letra ou número. Deve terminar com uma letra, número ou sublinhado. Pode contém letras maiúsculas ou minúsculas. |
| **local** |Local do Azure (também chamado tooas região). |Deve ser um dos Olá locais do Azure válidos. |
| **addressSpace** |Coleção de prefixos de endereço que compõem a saudação rede virtual na notação CIDR. |Deve ser uma matriz de blocos de endereços CIDR válidos, incluindo intervalos de endereços IP públicos. |
| **sub-redes** |Coleção de sub-redes que compõem a saudação VNet |Consulte a tabela de propriedades de subrede de saudação abaixo. |
| **dhcpOptions** |Objeto que contém uma única propriedade necessária denominada **dnsServers**. | |
| **dnsServers** |Matriz de servidores DNS usados por Olá VNet. Se nenhum servidor for especificado, a resolução de nome interno do Azure será usada. |Deve ser uma matriz de servidores de DNS too10, pelo endereço IP. |

Uma sub-rede é um recurso filho de uma VNet e ajuda a definir segmentos de espaços de endereços em um bloco CIDR, usando prefixos de endereços IP. As NICs podem ser adicionadas toosubnets e tooVMs conectado, fornecendo conectividade para várias cargas de trabalho.

Subredes contêm Olá propriedades a seguir.

| Propriedade | Descrição | Restrições |
| --- | --- | --- |
| **name** |Nome da sub-rede |Cadeia de caracteres too80. Pode conter letras, números, sublinhados, pontos ou hifens. Deve começar com uma letra ou número. Deve terminar com uma letra, número ou sublinhado. Pode contém letras maiúsculas ou minúsculas. |
| **local** |Local do Azure (também chamado tooas região). |Deve ser um dos Olá locais do Azure válidos. |
| **addressPrefix** |Prefixo de endereço único que compõem a sub-rede de saudação na notação CIDR |Deve ser um único bloco CIDR que faz parte de um dos espaços de endereço da rede virtual hello. |
| **networkSecurityGroup** |Subrede toohello NSG aplicado | |
| **routeTable** |Tabela de rotas aplicado toohello sub-rede | |
| **ipConfigurations** |Coleção de objetos de configuração de IP usado pelo NICs conectados toohello sub-rede | |

### <a name="name-resolution"></a>Resolução de nomes
Por padrão, usa sua VNet [resolução de nomes fornecida pelo Azure](virtual-networks-name-resolution-for-vms-and-role-instances.md) tooresolve nomes no hello rede virtual e no hello Internet pública. No entanto, se você conectar seus centros de dados VNets tooyour local, você precisa tooprovide [seu próprio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md) tooresolve nomes entre suas redes.  

### <a name="limits"></a>limites
Examine os limites de rede de saudação do hello [Azure limita](../azure-subscription-service-limits.md#networking-limits) tooensure artigo que seu design não entra em conflito com qualquer um dos limites de saudação. Alguns limites podem ser aumentados abrindo um tíquete de suporte.

### <a name="role-based-access-control-rbac"></a>RBAC (Controle de Acesso Baseado em Função)
Você pode usar [RBAC do Azure](../active-directory/role-based-access-built-in-roles.md) toocontrol nível de saudação do acesso de usuários diferentes pode ter recursos toodifferent no Azure. Dessa forma, que você pode separar trabalho Olá pela sua equipe de acordo com suas necessidades.

Como distante como redes virtuais são preocupada, os usuários Olá **rede Colaborador** função tem controle total sobre os recursos de rede virtual do Azure Resource Manager. Da mesma forma, os usuários em Olá **Colaborador clássico de rede** função tem controle total sobre os recursos de rede virtual clássica.

> [!NOTE]
> Você também pode [criar suas próprias funções](../active-directory/role-based-access-control-configure.md) tooseparate suas necessidades administrativas.
>
>

## <a name="design"></a>Design
Depois que você souber respostas Olá perguntas toohello Olá [planejar](#Plan) seção, examine o seguinte Olá antes de definir seus VNets.

### <a name="number-of-subscriptions-and-vnets"></a>Número de assinaturas e redes virtuais
Considere a criação de múltiplas VNets em Olá os seguintes cenários:

* **Máquinas virtuais que precisam toobe colocada em diferentes locais do Azure**. As redes virtuais no Azure são regionais. Eles não podem abranger locais. Portanto você precisa de pelo menos uma VNet para cada local do Azure que deseja toohost VMs.
* **Cargas de trabalho que precisam toobe completamente isolada uma da outra**. Você pode criar VNets separadas, Olá que use até mesmo espaços de endereço IP, tooisolate cargas de trabalho diferentes uns dos outros.

Tenha em mente que os limites de saudação que consulte acima são por região por assinatura. Isso significa que você pode usar vários limite de saudação tooincrease assinaturas de recursos, que você pode manter no Azure. Você pode usar uma VPN site a site ou um circuito de rota expressa, tooconnect VNets em assinaturas diferentes.

### <a name="subscription-and-vnet-design-patterns"></a>Assinatura e padrões de design de rede virtual
Olá tabela a seguir mostra alguns padrões comuns de design para o uso de assinaturas e VNets.

| Cenário | Diagrama | Prós | Contras |
| --- | --- | --- | --- |
| Assinatura única, duas redes virtuais por aplicativo |![Assinatura única](./media/virtual-network-vnet-plan-design-arm/figure1.png) |Toomanage apenas uma assinatura. |Número máximo de VNets por região do Azure. Você precisa de mais inscrições depois disso. Saudação de revisão [Azure limita](../azure-subscription-service-limits.md#networking-limits) artigo para obter detalhes. |
| Uma assinatura por aplicativo, duas redes virtuais por aplicativo |![Assinatura única](./media/virtual-network-vnet-plan-design-arm/figure2.png) |Usa apenas duas redes virtuais por assinatura. |Toomanage mais difícil quando há muitos aplicativos. |
| Uma assinatura por unidade de negócios, duas redes virtuais por aplicativo. |![Assinatura única](./media/virtual-network-vnet-plan-design-arm/figure3.png) |Equilíbrio entre o número de assinaturas e as redes virtuais. |Número máximo de VNets por unidade de negócios (assinatura). Saudação de revisão [Azure limita](../azure-subscription-service-limits.md#networking-limits) artigo para obter detalhes. |
| Uma assinatura por unidade de negócios, duas redes virtuais por grupo de aplicativos. |![Assinatura única](./media/virtual-network-vnet-plan-design-arm/figure4.png) |Equilíbrio entre o número de assinaturas e as redes virtuais. |Os aplicativos devem ser isolados usando sub-redes e NSGs. |

### <a name="number-of-subnets"></a>Número de sub-redes
Você deve considerar várias sub-redes em uma rede virtual no hello os seguintes cenários:

* **Não há endereços IP particulares para todas as NICs em uma sub-rede**. Se o seu espaço de endereço de sub-rede não contém endereços IP suficientes para o número de saudação de NICs na sub-rede hello, será necessário toocreate várias sub-redes. Tenha em mente que o Azure reservará 5 endereços IP privados de cada sub-rede que não podem ser usados: Olá primeiro e último endereços do espaço de endereço da saudação (para o endereço de sub-rede hello e multicast) e 3 endereços toobe usado internamente (para fins DHCP e DNS).
* **Segurança**. Você pode usar grupos de tooseparate subredes de máquinas virtuais entre si para cargas de trabalho que tem uma multi-camada de estrutura e aplicar diferentes [(NSGs) de grupos de segurança de rede](virtual-networks-nsg.md#subnets) para essas sub-redes.
* **Conectividade híbrida**. Você pode usar gateways de VPN e circuitos ExpressRoute muito[conectar](../vpn-gateway/vpn-gateway-about-vpngateways.md#s2smulti) tooone seus VNets outro, e tooyour data center local. Gateways de VPN e circuitos ExpressRoute exigem uma sub-rede de seu próprios toobe criado.
* **Dispositivos virtuais**. Você pode usar um dispositivo virtual, como um firewall, acelerador de WAN ou gateway de VPN em uma rede virtual do Azure. Quando você fizer isso, é preciso muito[rotear o tráfego](virtual-networks-udr-overview.md) toothose appliances e isolá-los em sua própria sub-rede.

### <a name="subnet-and-nsg-design-patterns"></a>Padrões de design de sub-rede e NSG
Olá tabela a seguir mostra alguns padrões comuns de design para o uso de sub-redes.

| Cenário | Diagrama | Prós | Contras |
| --- | --- | --- | --- |
| Sub-rede única, NSGs por camada de aplicativo, por aplicativo |![Sub-rede única](./media/virtual-network-vnet-plan-design-arm/figure5.png) |Apenas um toomanage de sub-rede. |Vários tooisolate necessário de NSGs cada aplicativo. |
| Uma sub-rede por aplicativo, NSGs por camada de aplicativo |![Sub-rede por aplicativo](./media/virtual-network-vnet-plan-design-arm/figure6.png) |Menos toomanage de NSGs. |Toomanage de várias sub-redes. |
| Uma sub-rede por camada de aplicativo, NSGs por aplicativo. |![Sub-rede por camada](./media/virtual-network-vnet-plan-design-arm/figure7.png) |Equilíbrio entre o número de sub-redes e de NSGs. |Número máximo de NSGs por assinatura. Saudação de revisão [Azure limita](../azure-subscription-service-limits.md#networking-limits) artigo para obter detalhes. |
| Uma sub-rede por camada de aplicativo, por aplicativo, NSGs por sub-rede |![Sub-rede por camada por aplicativo](./media/virtual-network-vnet-plan-design-arm/figure8.png) |Possivelmente menor número de NSGs. |Toomanage de várias sub-redes. |

## <a name="sample-design"></a>Projeto de amostra
aplicativo de hello tooillustrate de informações de saudação neste artigo, considere Olá cenário a seguir.

Você trabalha para uma empresa que tem 2 datacenters na América do Norte e dois datacenters na Europa. Você identificou 6 voltado para aplicativos de cliente diferentes mantidas por 2 diferentes unidades de negócios que você deseja tooAzure toomigrate como um piloto. arquitetura básica de saudação para aplicativos de saudação são da seguinte maneira:

* App1, App2, App3 e App4 são aplicativos Web hospedados em servidores Linux executando o Ubuntu. Cada aplicativo conecta o servidor de aplicativo separado de tooa que hospeda os serviços RESTful em servidores Linux. os serviços RESTful Olá conecte-se o banco de dados do MySQL tooa back-end.
* App5 e App6 são aplicativos Web hospedados em servidores Windows que executam o Windows Server 2012 R2. Cada aplicativo se conecta a dados do SQL Server de back-end tooa.
* Atualmente, todos os aplicativos são hospedados em um dos centros de dados da empresa Olá na América do Norte.
* centros de dados local Olá usam espaço de endereço de 10.0.0.0/8 de saudação.

É necessário toodesign uma solução de rede virtual que atenda Olá requisitos a seguir:

* Cada unidade de negócios não será afetada por consumo de recursos de outras unidades de negócios.
* Você deve minimizar a quantidade de saudação de sub-redes e VNets toomake gerenciamento mais fácil.
* Cada unidade de negócios deve ter uma única rede virtual de teste/desenvolvimento usada para todos os aplicativos.
* Cada aplicativo é hospedado em 2 datacenters diferentes do Azure por continente (América do Norte e Europa).
* Cada aplicativo é completamente isolado do outro.
* Cada aplicativo pode ser acessado por clientes via Olá Internet usando HTTP.
* Cada aplicativo pode ser acessado por usuários conectados toohello local datacenters usando um túnel criptografado.
* Data centers de Conexão local tooon devem usar dispositivos VPN existentes.
* Olá grupo rede da empresa deve ter controle total sobre a configuração da rede virtual hello.
* Os desenvolvedores em cada unidade de negócios só devem ser capaz de toodeploy VMs tooexisting sub-redes.
* Todos os aplicativos serão migrados como eles são tooAzure (comparação de precisão e shift).
* bancos de dados de saudação em cada local devem replicar tooother Azure locais de uma vez por dia.
* Cada aplicativo deve usar 5 servidores web de front-end, 2 servidores de aplicativos (quando necessário) e 2 servidores de banco de dados.

### <a name="plan"></a>Plano
Você deve iniciar seu design de planejamento ao responder pergunta Olá Olá [definir requisitos](#Define-requirements) seção conforme mostrado abaixo.

1. O que os locais do Azure você vai usar toohost VNets?

    2 locais na América do Norte e 2 locais na Europa. Você deve escolher aqueles com base no local físico de saudação de seus data centers existentes para o local. Dessa forma a sua conexão de seu tooAzure locais físicos terá uma latência melhor.
2. Você precisa tooprovide comunicação entre esses locais do Azure?

    Sim. Como bancos de dados Olá devem ser replicadas tooall locais.
3. Você precisa tooprovide comunicação entre o VNet(s) do Azure e seu data center local?

    Sim. Desde que os usuários conectados toohello centros de dados de local devem ser capaz de tooaccess aplicativos de saudação por meio de um túnel criptografado.
4. Quantas VMs de IaaS você precisa para sua solução?

    200 VMs de IaaS. App1, App2, App3 e App4 exigem 5 servidores Web cada, 2 servidores de aplicativos cada e 2 servidores de banco de dados cada. Isso é um total de 9 VMs de IaaS por aplicativos ou 36 VMs de IaaS. App5 e App6 exigem 5 servidores web e 2 servidores de banco de dados cada. Isso é um total de 7 VMs de IaaS por aplicativos ou 14 VMs de IaaS. Portanto, você precisa de 50 VMs de IaaS para todos os aplicativos em cada região do Azure. Já que precisamos toouse 4 regiões, haverá 200 VMs de IaaS.

    Você também precisará tooprovide servidores DNS em cada rede virtual, ou em seu nome de tooresolve de centros de dados local entre suas VMs de IaaS do Azure e sua rede local.
5. Você precisa de tráfego de tooisolate com base em grupos de máquinas virtuais (servidores de web ou seja, front-end e servidores de banco de dados de back-end)?

    Sim. Cada aplicativo deve ser completamente isolado um do outro, e cada camada do aplicativo também deve ser isolada.
6. Você precisa de fluxo de tráfego toocontrol usando dispositivos virtuais?

    Não. Dispositivos virtuais podem ser usado tooprovide mais controlam sobre o fluxo de tráfego, incluindo o log mais detalhado do plano de dados.
7. Fazer os usuários a necessidade para diferentes conjuntos de permissões toodifferent recursos do Azure?

    Sim. Olá rede equipe precisa de controle total sobre configurações de rede virtual hello, enquanto os desenvolvedores só devem ser capaz de toodeploy suas VMs existentes toopre sub-redes.

### <a name="design"></a>Design
Você deve seguir o design Olá especificando os NSGs, VNets, sub-redes e assinaturas. Discutiremos NSGs aqui, mas você deve saber mais sobre [NSGs](virtual-networks-nsg.md) antes de concluir o design.

**Número de assinaturas e redes virtuais**

Olá requisitos a seguir é relacionadas toosubscriptions e VNets:

* Cada unidade de negócios não será afetada por consumo de recursos de outras unidades de negócios.
* Você deve minimizar a quantidade de saudação de sub-redes e VNets.
* Cada unidade de negócios deve ter uma única rede virtual de teste/desenvolvimento usada para todos os aplicativos.
* Cada aplicativo é hospedado em 2 datacenters diferentes do Azure por continente (América do Norte e Europa).

De acordo com esses requisitos, é necessário ter uma assinatura para cada unidade de negócios. Dessa forma, o consumo de recursos de uma unidade de negócios não contará até os limites para outras unidades de negócios. E desde que você quiser toominimize Olá número de VNets, você deve considerar o uso Olá **uma assinatura por unidade de negócios, dois VNets por grupo de aplicativos** padrão, conforme mostrado abaixo.

![Assinatura única](./media/virtual-network-vnet-plan-design-arm/figure9.png)

Também é necessário um espaço de endereço de saudação toospecify para cada rede virtual. Desde que você precisa conectividade entre hello centros de dados locais e hello regiões do Azure, espaço de endereço Olá usado para VNets do Azure não podem conflitar com rede de local de saudação e espaço de endereço de saudação usado por cada rede virtual não deve conflitar com outras VNets existentes. Você pode usar os espaços de endereço Olá na tabela Olá abaixo toosatisfy esses requisitos.  

| **Assinatura** | **Rede virtual** | **Região do Azure** | **Espaço de endereço** |
| --- | --- | --- | --- |
| BU1 |ProdBU1US1 |Oeste dos EUA |172.16.0.0/16 |
| BU1 |ProdBU1US2 |Leste dos EUA |172.17.0.0/16 |
| BU1 |ProdBU1EU1 |Norte da Europa |172.18.0.0/16 |
| BU1 |ProdBU1EU2 |Europa Ocidental |172.19.0.0/16 |
| BU1 |TestDevBU1 |Oeste dos EUA |172.20.0.0/16 |
| BU2 |TestDevBU2 |Oeste dos EUA |172.21.0.0/16 |
| BU2 |ProdBU2US1 |Oeste dos EUA |172.22.0.0/16 |
| BU2 |ProdBU2US2 |Leste dos EUA |172.23.0.0/16 |
| BU2 |ProdBU2EU1 |Norte da Europa |172.24.0.0/16 |
| BU2 |ProdBU2EU2 |Europa Ocidental |172.25.0.0/16 |

**Número de sub-redes e NSGs**

Olá requisitos a seguir é relacionadas toosubnets e NSGs:

* Você deve minimizar a quantidade de saudação de sub-redes e VNets.
* Cada aplicativo é completamente isolado do outro.
* Cada aplicativo pode ser acessado por clientes via Olá Internet usando HTTP.
* Cada aplicativo pode ser acessado por usuários conectados toohello local datacenters usando um túnel criptografado.
* Data centers de Conexão local tooon devem usar dispositivos VPN existentes.
* bancos de dados de saudação em cada local devem replicar tooother Azure locais de uma vez por dia.

Com base nesses requisitos, você poderia usar uma sub-rede por camada de aplicativo e usar os NSGs toofilter tráfego por aplicativo. Dessa forma, você só tem 3 sub-redes em cada rede virtual (front-end, camada de aplicativo e a camada de dados) e um NSG por aplicativo por sub-rede. Nesse caso, você deve considerar o uso de saudação **uma sub-rede por camada de aplicativo, os NSGs por aplicativo** padrão de design. Olá a figura abaixo mostra o uso de Olá Olá do padrão de design que representa a saudação **ProdBU1US1** VNet.

![Uma sub-rede por camada, um NSG por aplicativo por camada](./media/virtual-network-vnet-plan-design-arm/figure11.png)

No entanto, você também precisa toocreate uma sub-rede extra para conectividade VPN Olá entre Olá VNets e seus centros de dados local. E você precisar de espaço de endereço de Olá toospecify para cada sub-rede. Olá figura a seguir mostra um exemplo de solução para **ProdBU1US1** VNet. Você deve replicar esse cenário para cada rede virtual. Cada cor representa um aplicativo diferente.

![Rede virtual de exemplo](./media/virtual-network-vnet-plan-design-arm/figure10.png)

**Controle de Acesso**

Olá, requisitos a seguir estão relacionadas tooaccess controle:

* Olá grupo rede da empresa deve ter controle total sobre a configuração da rede virtual hello.
* Os desenvolvedores em cada unidade de negócios só devem ser capaz de toodeploy VMs tooexisting sub-redes.

Com base nesses requisitos, você pode adicionar usuários de Olá, equipe toohello interna do sistema de rede **rede Colaborador** função em cada assinatura; e criar uma função personalizada para Olá os desenvolvedores de aplicativos em cada assinatura fornecendo eles direitos tooadd VMs tooexisting subredes.

## <a name="next-steps"></a>Próximas etapas
* [Implantar uma rede virtual](virtual-networks-create-vnet-arm-template-click.md) com base em um cenário.
* Entender como muito[balancear a carga](../load-balancer/load-balancer-overview.md) VMs de IaaS e [gerenciar o roteamento por várias regiões do Azure](../traffic-manager/traffic-manager-overview.md).
* Saiba mais sobre [NSGs e como tooplan e design](virtual-networks-nsg.md) uma solução NSG.
* Saiba mais sobre os [Locais cruzados e opções de conectividade de rede virtual](../vpn-gateway/vpn-gateway-about-vpngateways.md#s2smulti).
