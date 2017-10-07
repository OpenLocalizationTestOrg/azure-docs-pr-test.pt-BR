---
title: "arquitetura de serviço aaaReliable | Microsoft Docs"
description: "Visão geral da arquitetura do serviço confiável Olá para serviços com e sem monitoração de estado"
services: service-fabric
documentationcenter: .net
author: AlanWarwick
manager: timlt
editor: vturecek
ms.assetid: af002ae6-7f6d-4769-b049-82aa1ba0891b
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/30/2016
ms.author: alanwar
redirect_url: /azure/service-fabric/service-fabric-reliable-services-introduction
ms.openlocfilehash: d2d0ec9600275ae248ab7717be269cc7204a1e4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="architecture-for-stateful-and-stateless-reliable-services"></a>Arquitetura de Reliable Services com e sem estado
Um serviço confiável do Service Fabric do Azure pode ser com ou sem estado. Cada tipo de serviço é executado em uma arquitetura específica. Essas arquiteturas são descritas neste artigo.
Consulte Olá [visão geral do serviço confiável](service-fabric-reliable-services-introduction.md) para obter mais informações sobre as diferenças de saudação entre serviços com e sem monitoração de estado.

## <a name="stateful-reliable-services"></a>Serviços Confiáveis com estado
### <a name="architecture-of-a-stateful-service"></a>Arquitetura de um serviço com estado
![Diagrama da arquitetura de um serviço com estado](./media/service-fabric-reliable-services-platform-architecture/reliable-stateful-service-architecture.png)

### <a name="stateful-reliable-service"></a>Serviço Confiável com estado
Um serviço confiável com monitoração de estado podem derivar Olá StatefulService ou classe StatefulServiceBase. Ambas essas classes base são fornecidas pelo Service Fabric. Eles oferecem vários níveis de suporte e abstração para Olá toointerface de serviço com monitoração de estado com a malha do serviço – e tooparticipate como um serviço em cluster do Service Fabric hello.

StatefulService deriva de StatefulServiceBase. StatefulServiceBase oferece serviços mais flexibilidade, mas requer mais compreensão dos recursos internos de saudação do Service Fabric.
Consulte Olá [visão geral do serviço confiável](service-fabric-reliable-services-introduction.md) e [o uso avançado de serviço confiável](service-fabric-reliable-services-advanced-usage.md) para mais informações sobre especificações de saudação de escrever serviços usando classes de StatefulService e StatefulServiceBase Olá .

Ambas as classes base gerenciam o tempo de vida de saudação e a função da implementação do serviço de saudação. implementação do serviço Olá pode substituir métodos virtuais de qualquer classe de base se implementação do serviço Olá tiver toodo de trabalho esses pontos Olá serviço implementação do ciclo de vida – ou se ele deseja toocreate um objeto de ouvinte de comunicação. Observe que embora uma implementação de serviço pode implementar seu próprio objeto de ouvinte de comunicação expor ICommunicationListener, no diagrama acima, a saudação Olá comunicação ouvinte é implementado pela malha do serviço – como Olá a implementação de serviço usa um ouvinte de comunicação que é implementado pela malha do serviço.

Um serviço confiável com monitoração de estado usa Olá estado confiável manager tootake aproveitar coleções confiáveis. Coleções confiáveis são estruturas de dados locais que são altamente disponível toohello service--que é, eles estão sempre disponíveis, independentemente de failovers de serviço. Cada tipo de coleção confiável é implementado por um provedor de estado confiável.
Para obter mais informações sobre coleções confiáveis, consulte Olá [visão geral das coleções confiável](service-fabric-reliable-services-reliable-collections.md).

### <a name="reliable-state-manager-and-state-providers"></a>Provedores e gerenciador de estado confiáveis
Gerenciador de estado confiável de saudação é objeto Olá que gerencia o estado confiável de provedores. Ele tem Olá funcionalidade toocreate, excluir, enumerar e certifique-se de que os provedores de estado confiável de saudação são persistentes e altamente disponível. Uma instância do provedor de estado confiável representa uma instância de uma estrutura de dados persistente e altamente disponível, como um dicionário ou uma fila.

Cada provedor de estado confiável expõe uma interface que é usada por um toointeract com monitoração de estado do serviço com o provedor de estado confiável de saudação. Por exemplo, IReliableDictionary é toointerface usado com o dicionário de confiável hello, enquanto IReliableQueue é toointerface usado com fila confiável hello. Todos os provedores de estado confiável implementam a interface de IReliableState de saudação.

Gerenciador de estado confiável de saudação tem uma interface denominada IReliableStateManager, que permite acesso tooit de um serviço com monitoração de estado. Provedores de estado de tooreliable interfaces são retornados por meio de IReliableStateManager.

Gerenciador de estado confiável de saudação usa uma arquitetura de plug-in para que os novos tipos de coleções confiáveis podem ser conectados dinamicamente.

dicionário confiável Hello e fila confiável são criados após a implementação de saudação de um repositório de diferencial de alto desempenho, com controle de versão.

### <a name="transactional-replicator"></a>Replicator transacional
componente do replicador transacional Olá é responsável por garantir que o estado de saudação de um serviço (ou seja, o estado de Olá no Gerenciador de estado confiável de saudação e coleções confiável Olá) é consistente em todas as réplicas que executam o serviço de saudação. Ele também garante que o estado de saudação é persistido no log de saudação. Olá interfaces do Gerenciador de estado confiável com o replicador transacional do hello através de um mecanismo privado.

replicador transacional Olá usa um estado de toocommunicate de protocolo de rede com outras réplicas da instância de serviço Olá para que todas as réplicas tenham informações atualizadas.

replicador transacional Olá usa informações de estado de toopersist um log para que as informações de estado de saudação sobrevive processo ou falhas de nó. log do Hello interface toohello é através de um mecanismo privado.

### <a name="log"></a>Registro
componente de log Olá fornece um armazenamento persistente de alto desempenho que pode ser otimizado para gravar toospinning ou discos de estado sólido.  design de saudação do log de saudação é para o armazenamento persistente de hello (ou seja, discos rígidos) toobe toohello local nós que estiver executando o serviço de monitoração de estado de saudação. Isso permite que as latências de baixas e alta taxa de transferência, como armazenamento persistente tooremote comparados, que não é um nó de toohello local.

componente de log Olá usa vários arquivos de log. Há um arquivo log todo o nó compartilhada usada por todas as réplicas como ele pode fornecer Olá menor latência e taxa de transferência mais alta para armazenar dados de estado. Por padrão, log compartilhado Olá é colocado no diretório de trabalho do nó de malha do serviço hello, mas também pode ser configurado toobe colocado em outro local, idealmente em um disco reservado para somente log compartilhado hello. Cada réplica para o serviço de saudação também tem um arquivo de log dedicado e log dedicado Olá é colocado no diretório de trabalho do serviço de saudação. Não há nenhum mecanismo tooconfigure Olá dedicado log toobe, colocado em um local diferente.

log compartilhado Olá é uma área de transição para obter informações de estado da réplica hello, durante a saudação o arquivo de log dedicado é destino final hello, onde ele é mantido. Nesse design, informações de estado de saudação é o primeiro arquivo de log compartilhados toohello escrito e movidos toohello arquivos de log dedicado no plano de fundo Olá lentamente. Dessa forma, hello gravação toohello compartilhado log teria Olá menor latência e taxa de transferência mais alta que permite que o progresso do serviço de saudação toomake mais rapidamente.

Lê e grava o log compartilhado toohello são feitas por meio do espaço de toopreallocated de e/s direto no disco de Olá Olá compartilhado arquivo de log. tooallow um ótimo uso de espaço em disco na unidade de saudação com logs dedicados, Olá dedicado é criado como um arquivo esparso do NTFS. Observe que isso permitirá que o excesso de provisionamento de espaço em disco e Olá SO mostrará os arquivos de log de saudação dedicado com muito mais espaço em disco que é realmente usada.

Além de um log de toohello de interface mínima do modo de usuário, o log de saudação é gravado como um driver de modo kernel. Ao ser executado como um driver de modo kernel, log Olá pode fornecer desempenho mais alto de saudação serviços tooall usá-lo.

Para obter mais informações sobre como configurar o log de hello, consulte [configuração com monitoração de estado confiável dos serviços](service-fabric-reliable-services-configuration.md).

## <a name="stateless-reliable-service"></a>Serviço Confiável sem estado
### <a name="architecture-of-a-stateless-service"></a>Arquitetura de um serviço sem estado
![Diagrama da arquitetura de um serviço sem estado](./media/service-fabric-reliable-services-platform-architecture/reliable-stateless-service-architecture.png)

### <a name="stateless-reliable-service"></a>Serviço Confiável sem estado
Implementações de serviço sem monitoração de estado derivam Olá StatelessService ou classe StatelessServiceBase. Olá classe StatelessServiceBase permite mais flexibilidade que Olá StatelessService classe.
Ambas as classes base gerenciam o tempo de vida de saudação e a função de um serviço.

implementação do serviço Olá pode substituir métodos virtuais de qualquer classe de base se serviço Olá tiver trabalho toodo os pontos no ciclo de vida de serviço hello – ou se ele deseja toocreate um objeto de ouvinte de comunicação. Observe que, embora o serviço Olá pode implementar seu próprio objeto de ouvinte de comunicação expor ICommunicationListener, no diagrama acima, a saudação ouvinte de comunicação de saudação é implementada pela malha do serviço, pois essa implementação de serviço usa uma comunicação ouvinte que é implementado pela malha do serviço.

Consulte Olá [visão geral do serviço confiável](service-fabric-reliable-services-introduction.md) e [o uso avançado de serviço confiável](service-fabric-reliable-services-advanced-usage.md) para mais informações sobre especificações de saudação de escrever serviços usando classes de StatelessService e StatelessServiceBase Olá .

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre a Malha de Serviços, consulte:

[Visão geral de Reliable Services](service-fabric-reliable-services-introduction.md)

[Início rápido](service-fabric-reliable-services-quick-start.md)

[Visão geral das coleções confiáveis](service-fabric-reliable-services-reliable-collections.md)

[Uso avançado de Reliable Services](service-fabric-reliable-services-advanced-usage.md)

[Configuração de Reliable Services](service-fabric-reliable-services-configuration.md)  

