---
title: aaaCommon perguntas sobre o Microsoft Azure Service Fabric | Microsoft Docs
description: Perguntas frequentes e respostas sobre o Service Fabric
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: 
ms.assetid: 5a179703-ff0c-4b8e-98cd-377253295d12
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: chackdan
ms.openlocfilehash: 4cbe92d2a03f7a1ea5d077807fdc982288220a7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="commonly-asked-service-fabric-questions"></a>Perguntas frequentes sobre o Service Fabric

Há muitas perguntas frequentes sobre o que o Service Fabric pode fazer e como ele deve ser usado. Este documento aborda muitas dessas perguntas comuns e suas respostas.

## <a name="cluster-setup-and-management"></a>Gerenciamento e instalação de cluster

### <a name="can-i-create-a-cluster-that-spans-multiple-azure-regions-or-my-own-datacenters"></a>É possível criar um cluster que abranja várias regiões do Azure ou meus próprios data centers?

Sim. 

Central de saudação tecnologia de clustering de malha do serviço pode ser usado toocombine máquinas em execução em qualquer lugar no mundo Olá, desde que eles têm conectividade rede tooeach outros. No entanto, criar e executar um cluster desse tipo pode ser complicado.

Se você estiver interessado nesse cenário, recomendamos que você tooget em contato por meio de saudação [lista de problemas do serviço de malha Github](https://github.com/azure/service-fabric-issues) ou por meio de seu representante de suporte na orientação adicional do tooobtain de ordem. equipe do Service Fabric Hello está funcionando esclarecimento adicional tooprovide, diretrizes e recomendações para este cenário. 

Tooconsider algumas coisas: 

1. Olá recurso de cluster do Service Fabric no Azure é regional hoje, como escala de máquinas virtuais Olá define esse cluster Olá se baseia no. Isso significa que, em caso de saudação de uma falha regional, você poderá perder o cluster de saudação do hello capacidade toomanage por meio de saudação do Azure Resource Manager ou Olá Portal do Azure. Isso pode ocorrer mesmo que o cluster Olá permanece em execução e será capaz de toointeract com eles diretamente. Além disso, Azure atualmente não oferecem Olá capacidade toohave uma única rede virtual que pode ser usada em regiões. Isso significa que um cluster de várias regiões do Azure requer o [endereços IP públicos para cada máquina virtual Olá conjuntos de escala de VM](../virtual-machine-scale-sets/virtual-machine-scale-sets-networking.md#public-ipv4-per-virtual-machine) ou [Gateways de VPN do Azure](../vpn-gateway/vpn-gateway-about-vpngateways.md). Essas opções de rede tem impactos diferentes no design de aplicativo de grau toosome de custos e desempenho, análise cuidadosa e planejamento é necessária antes de manter um ambiente desse tipo.
2. Hello manutenção, gerenciamento e monitoramento desses computadores podem se tornar complicadas, especialmente quando distribuída em _tipos_ dos ambientes, tais como entre provedores de nuvem diferentes ou entre recursos locais e o Azure . Deve ter cuidado tooensure que atualiza, monitoramento, gerenciamento e diagnóstico é entendido para cluster hello e aplicativos de saudação antes de executar cargas de trabalho de produção em um ambiente desse tipo. Se você já tiver bastante experiência solucionando esses problemas no Azure ou em seus próprios data centers, é provável que as mesmas soluções possam ser aplicadas ao desenvolver ou executar seu cluster do Service Fabric. 

### <a name="do-service-fabric-nodes-automatically-receive-os-updates"></a>Os nós do Service Fabric recebem as atualizações do sistema operacional automaticamente?

Não hoje, mas isso também é uma solicitação comum Azure pretenda toodeliver.

Olá provisório, temos [fornecido a um aplicativo](service-fabric-patch-orchestration-application.md) que sistemas operacionais de saudação sob os nós do Service Fabric permaneça corrigido e o toodate.

Olá desafio atualizações do sistema operacional é que eles geralmente requerem uma reinicialização da máquina hello, o que resulta em perda de disponibilidade temporário. Por si só, que não é um problema, desde que o Service Fabric redirecionará automaticamente o tráfego para os nós de tooother de serviços. No entanto, se as atualizações do sistema operacional não são coordenadas cluster hello, há o potencial de saudação que muitos nós ficarem inativos ao mesmo tempo. Essas reinicializações simultâneas podem causar a perda de disponibilidade completa para um serviço ou, pelo menos, para uma partição específica (para um serviço com estado).

Olá futuro, planejamos política de atualização toosupport um sistema operacional que é totalmente automatizada e coordenada entre domínios de atualização, garantindo que a disponibilidade é mantida apesar reinicializações e outras falhas inesperadas.

### <a name="can-i-use-large-virtual-machine-scale-sets-in-my-sf-cluster"></a>Posso usar grandes conjuntos de dimensionamento de máquinas virtuais no meu cluster do SF? 

**Resposta curta** – Não. 

**Tempo de resposta** - embora Olá grandes conjuntos de escala de máquina Virtual que você tooscale uma escala de máquina virtual definido até 1000 instâncias de VM, isso é feito pelo uso de saudação do posicionamento grupos (páginas). Domínios de falha (FDs) e domínios de atualização (UDs) só são consistentes dentro de um serviço do posicionamento grupo malha usa FDs e UDs toomake decisões de posicionamento de suas instâncias de serviço/réplicas do serviço. Como FDs hello e UDs são comparáveis somente dentro de um grupo de posicionamento SF não pode usá-lo. Por exemplo, se VM1 no PG1 com uma topologia de FD = 0 e VM9 em PG2 com uma topologia de FD = 4, isso não significa que VM1 e VM2 em dois Racks de Hardware diferente, portanto, SF não é possível usar valores hello FD em decisões de posicionamento neste caso toomake.

Há outros problemas com conjuntos de escala de máquina virtual grande, como suporte ao balanceamento de carga de falta de saudação de nível 4. Consulte toofor [detalhes em grande escala conjuntos](../virtual-machine-scale-sets/virtual-machine-scale-sets-placement-groups.md)



### <a name="what-is-hello-minimum-size-of-a-service-fabric-cluster-why-cant-it-be-smaller"></a>O que é o tamanho mínimo de saudação de um cluster do Service Fabric? Por que ele não pode ser menor?

tamanho mínimo com suporte de saudação para um cluster do Service Fabric executando cargas de trabalho de produção é de cinco nós. Para cenários de desenvolvimento/teste, oferecemos suporte para três clusters de nó.

Esses mínimos existem porque o cluster do Service Fabric Olá executa um conjunto de serviços de monitoração de estado do sistema, incluindo o Gerenciador de failover de saudação e o serviço de nomeação de saudação. Esses serviços, que acompanham os serviços que foram implantados toohello cluster e onde estão hospedados no momento, dependem de consistência forte. Consistência de alta segurança, por sua vez, depende de saudação capacidade tooacquire um *quorum* para qualquer atualização determinada toohello estado dos serviços, onde um quorum representa uma maioria estrita de réplicas de saudação (N/2 + 1) para um determinado serviço.

Com esse plano de fundo, vamos examinar algumas configurações de cluster possíveis:

**Um nó**: essa opção não fornece alta disponibilidade como perda de saudação de único nó Olá por qualquer motivo significa perda de saudação do cluster inteiro hello.

**Dois nós**: um quorum para um serviço implantado entre dois nós (N = 2) é 2 (2/2 + 1 = 2). Quando uma única réplica for perdida, é impossível toocreate um quorum. Como a execução de uma atualização de serviço requer desativar temporariamente uma réplica, essa não é uma configuração útil.

**Três nós**: com três nós (N = 3), Olá requisito toocreate um quorum ainda é dois nós (2/3 + 1 = 2). Isso significa que você pode perder um nó individual e ainda manter o quorum.

configuração de cluster de nó três Olá há suporte para desenvolvimento e teste porque você pode executar atualizações e sobreviver a falhas de nós individuais, com segurança, contanto que não ocorram simultaneamente. Para cargas de trabalho de produção, você deve ser resiliente toosuch uma falha simultânea, portanto, cinco nós são necessário.

### <a name="can-i-turn-off-my-cluster-at-nightweekends-toosave-costs"></a>Posso desativar o cluster em custos de toosave noite/finais de semana?

Em geral, não. Serviço de malha armazena o estado em discos locais, efêmeros, que significa que, se Olá máquina de virtual é movida tooa outro host, Olá dados não são movidos com ele. Em operação normal, que não é um problema de como o novo nó de saudação é colocado toodate por outros nós. No entanto, se você parar todos os nós e reiniciá-los mais tarde, há a possibilidade de significativa que a maioria de nós Olá Iniciar em novos hosts e faça Olá sistema não é possível toorecover.

Se você quiser toocreate clusters para testar seu aplicativo antes da implantação, é recomendável criar dinamicamente desses clusters como parte de sua [integração contínua/contínua pipeline de implantação](service-fabric-set-up-continuous-integration.md).


### <a name="how-do-i-upgrade-my-operating-system-for-example-from-windows-server-2012-toowindows-server-2016"></a>Como faço para atualizar meu sistema operacional (por exemplo, do Windows Server 2012 tooWindows Server 2016)

Enquanto estamos trabalhando em uma experiência aprimorada, atualmente, você é responsável pela atualização de saudação. Você deve atualizar a imagem Olá SO Olá uma máquina virtual de cluster de máquinas virtuais de saudação por vez. 

## <a name="container-support"></a>Suporte a contêiner

### <a name="why-are-my-containers-that-are-deployed-toosf-unable-tooresolve-dns-addresses"></a>Por que são Meus contêineres que são implantados tooSF não é possível tooresolve DNS endereços?

Esse problema foi relatado em clusters que estão na versão 5.6.204.9494 

**Mitigação** : siga [neste documento](service-fabric-dnsservice.md) tooenable Olá DNS serviço serviço de malha em seu cluster.

**Corrigir** : versão de cluster tooa atualização com suporte que é maior do que 5.6.204.9494, quando ele estiver disponível. Se o cluster for definido tooautomatic atualizações, cluster Olá atualizará automaticamente versão toohello com essa correção do problema.

  
## <a name="application-design"></a>Design do aplicativo

### <a name="whats-hello-best-way-tooquery-data-across-partitions-of-a-reliable-collection"></a>O que é Olá melhor tooquery dados em partições de um conjunto confiável?

Coleções confiáveis são tipicamente [particionada](service-fabric-concepts-partitioning.md) tooenable expansão para maior produtividade e desempenho. Isso significa que o estado de saudação para um determinado serviço pode ser disseminado por 10 ou 100 máquinas. tooperform operações em que conjunto de dados completo, você tem algumas opções:

- Crie um serviço que consulta todas as partições de outro toopull de serviço nos dados Olá necessário.
- Criar um serviço que possa receber dados de todas as partições de outro serviço.
- Periodicamente enviar por push dados de cada repositório externo de tooan do serviço. Essa abordagem só é apropriada se consultas Olá que você está executando não fazem parte de sua lógica de negócios principal.


### <a name="whats-hello-best-way-tooquery-data-across-my-actors"></a>O que é Olá melhor tooquery dados em meu atores?

Atores são unidades independentes de toobe projetado de estado e computação, portanto, não é recomendável tooperform consultas amplo do estado de ator em tempo de execução. Se você tiver uma necessidade tooquery em conjunto completo de saudação do estado ator, você deve considerar o:

- Substituindo os serviços de ator com serviços confiáveis com monitoração de estado, que Olá número da rede solicitações toogather todos os dados de número de saudação do número de toohello de atores de partições em seu serviço.
- Criando o envio de tooperiodically atores seu repositório externo do estado tooan para consultar mais fácil. Como acima, essa abordagem é somente viável se consultas Olá que estiver executando não são necessárias para o comportamento de tempo de execução.

### <a name="how-much-data-can-i-store-in-a-reliable-collection"></a>Quantos dados posso armazenar em uma Coleção Confiável?

Serviços confiáveis geralmente são particionados para que quantidade hello, você pode armazenar é limitada apenas pelo número de Olá das máquinas que você tem em cluster hello e quantidade de saudação de memória disponível nessas máquinas.

Por exemplo, suponha que você tem uma coleção confiável em um serviço com 100 partições e 3 réplicas, armazenando objetos com 1kb de tamanho, em média. Agora, suponha que você tem um cluster de 10 máquinas com 16 gb de memória por máquina. Para simplificar e toobe muito conservadora, suponha que Olá sistema operacional e serviços do sistema, tempo de execução do Service Fabric Olá e seus serviços consumam 6gb de que, deixando 10gb disponíveis por máquina ou 100gb para o cluster de saudação.

Tendo em mente que cada objeto deve ser armazenado três vezes (uma primária e duas réplicas), você teria memória suficiente para cerca de 35 milhões de objetos na sua coleção ao operar com capacidade total. No entanto, recomendamos que está sendo toohello resilientes a perda simultâneas de um domínio de falha e um domínio de atualização, que representa o cerca de 1/3 da capacidade e reduziria Olá número tooroughly 23 milhões.

Observe que esse cálculo também pressupõe que:

- Essa distribuição Olá de dados em partições Olá é aproximadamente uniforme ou que você estiver relatando toohello de métricas de carga Gerenciador de recursos de Cluster. Por padrão, o Service Fabric balanceará a carga com base na contagem de réplicas. Em nosso exemplo acima, que deve colocar 10 réplicas primárias e 20 réplicas secundárias em cada nó no cluster hello. Que funciona bem para a carga será distribuída igualmente entre partições hello. Se o carregamento não é par, você deve relate carga para que hello Gerenciador de recursos pode pacote menores réplicas juntos e permite maior tooconsume de réplicas mais memória em um nó individual.

- Olá confiável serviço em questão é apenas um estado armazenando Olá cluster hello. Como você pode implantar um cluster de tooa vários serviços, é necessário toobe atento recursos Olá que cada precisarão toorun e gerenciar seu estado.

- Esse cluster Olá em si não é ampliação ou redução. Se você adicionar mais máquinas, o Service Fabric será reequilibrar sua capacidade adicional do réplicas tooleverage Olá até que o número de saudação de máquinas ultrapassa o número de saudação de partições em seu serviço, desde que uma réplica individual não pode abranger máquinas. Por outro lado, se você reduzir o tamanho de saudação do cluster Olá removendo máquinas, suas réplicas serão compactadas mais rigidamente e têm menos capacidade geral.

### <a name="how-much-data-can-i-store-in-an-actor"></a>Quantos dados posso armazenar em um ator?

Assim como acontece com serviços confiáveis, quantidade de saudação de dados que você pode armazenar em um serviço de ator só é limitada pelo Olá espaço total em disco e memória disponível em nós de saudação do cluster. No entanto, os atores individuais são mais efetivos quando são usada tooencapsulate uma pequena quantidade de lógica de negócios de estado e associado. Como regra geral, um ator individual deve ter um estado que seja medido em quilobytes.

## <a name="other-questions"></a>Outras perguntas

### <a name="how-does-service-fabric-relate-toocontainers"></a>Como o Service Fabric se relacionam toocontainers?

Contêineres oferecem serviços de toopackage uma maneira simples e suas dependências, de modo que eles executar consistentemente em todos os ambientes e podem funcionar de maneira isolada em um único computador. Service Fabric oferece uma maneira toodeploy e gerenciar serviços, incluindo [serviços que foram compactados em um contêiner](service-fabric-containers-overview.md).

### <a name="are-you-planning-tooopen-source-service-fabric"></a>Você está planejando tooopen fonte do Service Fabric

Estamos pretende serviços confiáveis do tooopen fonte hello e estruturas de atores confiável no GitHub e aceitará projetos de toothose contribuições da comunidade. Siga Olá [Service Fabric blog](https://blogs.msdn.microsoft.com/azureservicefabric/) para obter mais detalhes conforme eles estão anunciados.

Olá estão atualmente não há planos tooopen fonte Olá Service Fabric tempo de execução.

## <a name="next-steps"></a>Próximas etapas

- [Saiba mais sobre os principais conceitos do Service Fabric e práticas recomendadas](https://mva.microsoft.com/en-us/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965)
