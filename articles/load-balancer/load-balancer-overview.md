---
title: "Visão geral do balanceador de carga aaaAzure | Microsoft Docs"
description: "Visão geral dos recursos do Balanceador de Carga do Azure, arquitetura e implementação. Saiba como funciona o balanceador de carga hello e aproveitá-lo na nuvem hello."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
ms.assetid: 0f313dc0-f007-4cee-b2b9-f542357925a3
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 2376a02f7cbbbed6a90f216419c0c3d30f594272
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-load-balancer-overview"></a>Visão geral do Balanceador de Carga do Azure

O balanceador de carga do Azure fornece tooyour aplicativos de alto desempenho de disponibilidade e rede. É um balanceador de carga do tipo Camada 4 (TCP, UDP) que distribui o tráfego de entrada entre as instâncias de serviço íntegras definidas em um conjunto de balanceadores de carga.

O Azure Load Balancer pode ser configurado para:

* Balancear cargas de entrada da Internet tráfego toovirtual máquinas. Essa configuração é conhecida como [balanceamento de carga voltada para a Internet](load-balancer-internet-overview.md).
* Balanceie o tráfego de carga entre as máquinas virtuais em uma rede virtual, entre as máquinas virtuais nos serviços de nuvem ou entre os computadores locais e as máquinas virtuais em uma rede virtual entre as instalações. Essa configuração é conhecida como [balanceamento de carga interno](load-balancer-internal-overview.md).
* Encaminhar o tráfego externo tooa específico de máquina virtual.

Todos os recursos em nuvem Olá necessário um toobe de endereço IP público de saudação à Internet. infraestrutura de nuvem Olá no Azure usa endereços IP não roteável para seus recursos. O Azure usa a conversão de endereços de rede (NAT) com IP endereços toocommunicate toohello Internet pública.

## <a name="azure-deployment-models"></a>Modelos de implantação do Azure

É importante toounderstand Olá diferenças hello clássico do Azure e o Gerenciador de recursos de [modelos de implantação](../azure-resource-manager/resource-manager-deployment-model.md). O Azure Load Balancer está configurado de forma diferente em cada modelo.

### <a name="azure-classic-deployment-model"></a>modelo de implantação clássico do Azure

Máquinas virtuais implantadas em um limite de serviço de nuvem podem ser agrupado toouse um balanceador de carga. Neste modelo um endereço IP público e um nome de domínio totalmente qualificado, (FQDN) são atribuídos tooa serviço de nuvem. o balanceador de carga Olá porta tradução e balanceamento de carga de tráfego de rede hello usando o endereço IP público de Olá Olá serviço de nuvem.

O tráfego de balanceamento de carga é definido por pontos de extremidade. Pontos de extremidade de conversão de porta têm uma relação um para um entre a porta atribuída público saudação do endereço IP público de saudação e a porta local de Olá atribuído toohello serviço em uma máquina virtual específica. Pontos de extremidade de balanceamento de carga têm uma relação um-para-muitos entre o endereço IP público de saudação e Olá local portas atribuídas toohello serviços em máquinas virtuais de saudação no serviço de nuvem hello.

![Balanceador de carga do Azure no modelo de implantação clássico Olá](./media/load-balancer-overview/asm-lb.png)

Figura 1 - balanceador de carga do Azure no modelo de implantação clássico Olá

rótulo de endereço IP público Olá que Olá usos do balanceador de carga para esse modelo de implantação do domínio de saudação é \<nome do serviço de nuvem\>. cloudapp.net. Olá gráfico a seguir mostra Olá balanceador de carga do Azure neste modelo.

### <a name="azure-resource-manager-deployment-model"></a>modelo de implantação do Azure Resource Manager

No modelo de implantação do Gerenciador de recursos de saudação há toocreate sem necessidade de um serviço de nuvem. Balanceador de carga de saudação é criado tooexplicitly rotear o tráfego entre várias máquinas virtuais.

Um endereço IP público é um recurso individual que tem um rótulo de domínio (nome DNS). endereço IP público de saudação é associado ao recurso de Balanceador de carga hello. Regras de Balanceador de carga e regras de NAT de entrada usam endereço IP público de saudação conforme Olá ponto de extremidade de Internet para recursos de saudação que está recebendo o tráfego de balanceamento de carga de rede.

Um endereço IP público ou privado é atribuído a máquina de virtual de tooa toohello rede interface recursos anexado. Depois que uma interface de rede é adicionada um pool de endereços IP de back-end do balanceador de carga tooa, o balanceador de carga de saudação é toosend capaz de balanceamento de carga de tráfego de rede com base em regras Olá com balanceamento de carga que são criadas.

Olá gráfico a seguir mostra Olá balanceador de carga do Azure neste modelo:

![Azure Load Balancer no Gerenciador de Recursos](./media/load-balancer-overview/arm-lb.png)

Figura 2 – Azure Load Balancer no Resource Manager

o balanceador de carga Olá pode ser gerenciado por meio do Gerenciador de recursos com base em modelos, APIs e ferramentas. toolearn mais sobre o Gerenciador de recursos, consulte Olá [visão geral do Gerenciador de recursos](../azure-resource-manager/resource-group-overview.md).

## <a name="load-balancer-features"></a>Recursos do balanceador de carga

* Distribuição baseada em hash

    O Balanceador de Carga do Azure usa um algoritmo de distribuição baseado em hash. Por padrão, ele usa um hash tupla 5 composto de IP de origem, porta de origem, IP de destino, porta de destino e servidores do protocolo tipo toomap tráfego tooavailable. Ele fornece permanência somente *dentro* de uma sessão de transporte. Pacotes em Olá mesma sessão TCP ou UDP será direcionado toohello mesmo instância por trás do ponto de extremidade com balanceamento de carga do hello. Quando o cliente Olá fecha e reabre a conexão de saudação ou inicia uma nova sessão de Olá mesmo IP de origem, as alterações de porta de origem hello. Isso pode causar Olá tráfego toogo tooa ponto de extremidade diferente em um datacenter diferente.

    Para obter mais detalhes, consulte [Modo de distribuição do balanceador de carga](load-balancer-distribution-mode.md). Olá gráfico a seguir mostra a distribuição de baseadas em hash de saudação:

    ![Distribuição baseada em hash](./media/load-balancer-overview/load-balancer-distribution.png)

    Figura 3 – Distribuição baseada em hash

* Encaminhamento de porta

    O Balanceador de Carga do Azure oferece-lhe controle sobre como a comunicação de entrada é gerenciada. Essa comunicação inclui o tráfego iniciado de hosts da Internet ou de máquinas virtuais em outros serviços de nuvem ou redes virtuais. Esse controle é representado por um ponto de extremidade (também chamado de ponto de extremidade de entrada).

    Um ponto de extremidade de entrada escuta em uma porta pública e encaminha o tráfego de porta interna tooan. Você pode mapear Olá mesmo portas para um ponto de extremidade interno ou externo ou usar uma porta diferente para eles. Por exemplo, você pode ter um tooport de toolisten do web server configurado 81 enquanto o mapeamento de ponto de extremidade público Olá é a porta 80. a criação de um ponto de extremidade público Olá dispara a criação de saudação de uma instância do balanceador de carga.

    Quando criado usando hello portal do Azure, o portal de saudação cria automaticamente pontos de extremidade toohello máquina virtual Olá protocolo de área de trabalho remota (RDP) e o tráfego da sessão remoto do Windows PowerShell. Você pode usar esses pontos de extremidade tooremotely administrar Olá VM por meio de saudação da Internet.

* Reconfiguração automática

    O Balanceador de Carga do Azure reconfigura-se instantaneamente quando você aumenta ou diminui as instâncias. Por exemplo, essa reconfiguração ocorre quando você aumenta Olá contagem de instâncias para funções web/de trabalho em um serviço de nuvem ou quando você adiciona máquinas virtuais adicionais em Olá mesmo com balanceamento de carga definido.

* Monitoramento do serviço

    Balanceador de carga do Azure pode investigação de integridade de saudação do hello várias instâncias do servidor. Quando um teste falha toorespond, balanceador de carga hello para enviar novas conexões instâncias não íntegras toohello. As conexões existentes não são afetadas.

    Existem três tipos de investigação com suporte:

    + **Investigação de agente convidado (na plataforma como um serviço de máquinas virtuais somente):** balanceador de carga Olá utiliza o agente convidado Olá em máquina virtual de saudação. Olá agente convidado escuta e responde com uma resposta HTTP 200 Okey somente quando hello instância está no estado pronto do hello (ou seja, Olá instância não está em um estado como ocupado, Reciclando ou parando). Se o agente de saudação falhar toorespond com um Okey de 200 HTTP, marcas de Balanceador de carga Olá Olá instância como sem resposta e deixa de enviar a instância de toothat de tráfego. o balanceador de carga Olá continua a instância de saudação do tooping. Se o agente de convidado Olá responder com HTTP 200, o balanceador de carga Olá enviará instância de toothat tráfego novamente. Quando você estiver usando uma função web, o código do site será executado normalmente em w3wp.exe, que não é monitorada por Olá malha do Azure ou o agente convidado. Isso significa que falhas no w3wp.exe (por exemplo, respostas HTTP 500) não será relatado toohello agente de convidado e o balanceador de carga Olá não saberá tootake essa instância fora de rotação.
    + **Investigação personalizada de HTTP:** essa investigação substituições da investigação saudação padrão (agente de convidado). Você pode usá-lo toocreate sua integridade do lógica personalizada toodetermine Olá Olá da instância de função. o balanceador de carga Olá regularmente será teste seu ponto de extremidade (cada 15 segundos, por padrão). instância de saudação é considerada toobe em rotação se ele responde com um ACK TCP ou HTTP 200 dentro do período de tempo limite da saudação (padrão de 31 segundos). Isso é útil para implementar seus próprio instâncias de tooremove lógica da rotação do balanceador de carga hello. Por exemplo, você pode configurar Olá instância tooreturn um status de não-200 se instância Olá estiver acima de 90% da CPU. Para funções da web que usam w3wp.exe, você também obtém automática de monitoramento do seu site, como falhas no código do site da Web retornam um teste de toohello do status de 200 não.
    + **Investigação personalizada de TCP:** esse teste depende de porta de investigação de tooa definido de estabelecimento do TCP sessão bem-sucedida.

    Para obter mais informações, consulte Olá [esquema LoadBalancerProbe](https://msdn.microsoft.com/library/azure/jj151530.aspx).

* NAT de Origem

    Todos os toohello de tráfego de saída Internet que se origina de seu serviço sofre NAT (SNAT) de origem usando Olá mesmo endereço VIP como Olá tráfego de entrada. A SNAT fornece benefícios importantes:

    + Ele permite fácil atualização e recuperação de desastres de serviços, como Olá que VIP pode ser dinamicamente mapeado tooanother instância do serviço de saudação.
    + Facilita o gerenciamento de ACL (lista de controle de acesso). ACLs expressadas em termos de VIPs não mudam à medida que os serviços são escalados verticalmente ou reimplantados.

    configuração de Balanceador de carga Olá suporta cone completo NAT para UDP. Cone completo NAT é um tipo de NAT onde a porta Olá permite conexões de entrada de qualquer host externo (na solicitação de saída tooan de resposta).

    Para cada conexão de saída nova que inicia uma máquina virtual, uma porta de saída também é alocada pelo Balanceador de carga de saudação. host externo Olá vê o tráfego com uma porta virtual alocada pelo VIP IP. Para cenários que exigem um grande número de conexões de saída, é recomendável toouse [IP público de nível de instância](../virtual-network/virtual-networks-instance-level-public-ip.md) endereços para que VMs Olá tenham um endereço IP de saída dedicado para SNAT. Isso reduz o risco de saudação do esgotamento de porta.

    Consulte [conexões de saída](load-balancer-outbound-connections.md) para obter mais detalhes sobre esse tópico.

### <a name="support-for-multiple-load-balanced-ip-addresses-for-virtual-machines"></a>Suporte para vários endereços IP com balanceamento de carga para máquinas virtuais
Você pode atribuir mais de um balanceamento de carga público tooa conjunto de endereços IP de máquinas virtuais. Com essa capacidade, você pode hospedar vários sites SSL e/ou em vários ouvintes de grupo de disponibilidade do AlwaysOn do SQL Server no mesmo conjunto de máquinas virtuais de saudação. Para obter mais informações, consulte [Vários VIPs por serviço de nuvem](load-balancer-multivip.md).

[!INCLUDE [load-balancer-compare-tm-ag-lb-include.md](../../includes/load-balancer-compare-tm-ag-lb-include.md)]

## <a name="limitations"></a>Limitações

Pools de back-end do Load Balancer podem conter qualquer SKU de VM exceto camada Básica.

## <a name="next-steps"></a>Próximas etapas

- Saiba mais sobre o [balanceador de carga para a Internet](load-balancer-internet-overview.md)

- Saiba mais sobre a [Visão geral do balanceador de carga interno](load-balancer-internal-overview.md)

- Criar um [balanceador de carga para a Internet](load-balancer-get-started-internet-portal.md)

- Saiba mais sobre alguns dos Olá outra chave [recursos de rede](../networking/networking-overview.md) do Azure

