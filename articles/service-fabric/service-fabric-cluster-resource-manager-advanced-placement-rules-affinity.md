---
title: aaaService Gerenciador de recursos de Cluster de malha - afinidade | Microsoft Docs
description: "Visão geral da configuração de afinidade para os Serviços do Service Fabric"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 678073e1-d08d-46c4-a811-826e70aba6c4
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 7dc9b6d9c18d9d615d39cff7de9d7cba1c040474
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-and-using-service-affinity-in-service-fabric"></a>Configurando e usando a afinidade de serviço no Service Fabric
Afinidade é um controle que é fornecido principalmente toohelp facilidade Olá transição de aplicativos monolíticos maiores em nuvem e microservices Olá. Ele também é usado como uma otimização para melhorar o desempenho de saudação de serviços, embora assim pode ter efeitos colaterais.

Digamos que você está colocando um aplicativo maior, ou que não foi projetado apenas com microservices em mente, tooService malha (ou qualquer ambiente distribuído). Esse tipo de transição é comum. Iniciar levantar Olá todo app no ambiente Olá, empacotá-la e tornando-se de que ele está funcionando normalmente. Em seguida, iniciar dividi-los em diferentes serviços menores do que todos os falar tooeach outros.

Finalmente, você pode achar que o aplicativo hello está apresentando alguns problemas. problemas de saudação geralmente se encaixam em uma dessas categorias:

1. Algum componente X no aplicativo monolítico Olá tinha uma dependência não documentada no componente Y e é ativada apenas esses componentes em serviços separados. Desde que esses serviços estão em execução em diferentes nós de cluster de saudação, eles são desfeitos.
2. Esses componentes se comunicam por meio de (pipes nomeados locais | memória compartilhada | arquivos no disco) e o que realmente precisam toobe capaz de toowrite tooa compartilhado local recursos por motivos de desempenho no momento. Talvez essa forte dependência seja removida mais tarde.
3. Tudo está bem, mas acontece que esses dois componentes são, na prática, verborrágicos/dependentes do desempenho. Quando eles são movidos para serviços separados, o desempenho do aplicativo geral despenca ou a latência aumenta. Como resultado, hello geral do aplicativo não atende às expectativas.

Nesses casos, não quiser toolose nosso trabalho refatoração e não quiser toogo toohello back monolito. última condição de saudação ainda pode ser desejável como uma otimização simples. No entanto, até que podemos pode recriar Olá componentes toowork naturalmente como serviços (ou podemos resolver as expectativas de desempenho de saudação alguma outra forma), vamos tooneed algum sentido de localidade.

Quais toodo? Bem, você poderia tentar ativar a afinidade.

## <a name="how-tooconfigure-affinity"></a>Como tooconfigure afinidade
tooset a afinidade, você definir uma relação de afinidade entre dois serviços diferentes. Você pode pensar na afinidade como se estivesse "apontando" um serviço para outro e dizendo "Este serviço só pode ser executado quando esse serviço estiver em execução". Às vezes, nos referimos tooaffinity como uma relação pai/filho (onde você apontar filho Olá pai Olá). Afinidade assegura que as réplicas de saudação ou instâncias de um serviço são colocadas em Olá mesmo nós como o de outro serviço.

```csharp
ServiceCorrelationDescription affinityDescription = new ServiceCorrelationDescription();
affinityDescription.Scheme = ServiceCorrelationScheme.Affinity;
affinityDescription.ServiceName = new Uri("fabric:/otherApplication/parentService");
serviceDescription.Correlations.Add(affinityDescription);
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

> [!NOTE]
> Um serviço filho só pode participar de uma única relação de afinidade. Se você quisesse Olá filho toobe relacionado tootwo pai serviços ao mesmo tempo, você tem duas opções:
> - Inverter relações hello (tiver parentService1 e parentService2 ponto no serviço de filho atual Olá), ou
> - Designar um dos pais hello como um hub por convenção e ter todos os serviços de ponto de serviço. 
>
> Olá resultante comportamento de posicionamento no cluster Olá deve ser Olá mesmo.
>

## <a name="different-affinity-options"></a>Diferentes opções de afinidade
A afinidade é representada por meio de um dos vários esquemas de correlação e tem dois modos diferentes. Olá o modo mais comum de afinidade é o que chamamos de NonAlignedAffinity. Em NonAlignedAffinity, Olá réplicas ou instâncias de serviços diferentes Olá são colocadas em Olá mesmo nós. Olá, outro modo é AlignedAffinity. A Afinidade Alinhada é útil apenas com serviços com estado. Configuração de monitoração de estado dois serviços toohave alinhado afinidade assegura que primárias Olá desses serviços são colocadas em Olá mesmo nós de cada outro. Ele também faz com que cada par de secundários para esses serviços toobe colocada em Olá mesmo nós. Também é possível (embora menos comum) tooconfigure NonAlignedAffinity para serviços com monitoração de estado. Para NonAlignedAffinity, diferentes réplicas de saudação do hello dois serviços com monitoração de estado será executado no hello nós mesmos, mas seus primárias poderiam acabar em nós diferentes.

<center>
![Modos de afinidade e seus efeitos][Image1]
</center>

### <a name="best-effort-desired-state"></a>Estado desejado de melhor esforço
Uma relação de afinidade é considerada um melhor esforço. Ele não fornece Olá mesmas garantias de confiabilidade, em execução no hello mesmo processo executável faz ou de colocação. Serviços de saudação em um relacionamento de afinidade são fundamentalmente diferentes entidades que podem falhar e ser movidas independentemente. Uma relação de afinidade também pode ser interrompida, embora essas interrupções sejam temporárias. Por exemplo, as limitações de capacidade podem significar que apenas alguns dos objetos de serviço de saudação na relação de afinidade Olá podem se ajustar em um determinado nó. Nesses casos, embora não exista uma relação de afinidade no lugar, ele não pode ser imposto vencimento toohello outras restrições. Se for possível toodo assim, violação Olá será corrigida automaticamente mais tarde.

### <a name="chains-vs-stars"></a>Cadeias vs. estrelas
Hoje Olá Gerenciador de recursos de Cluster não é capaz de toomodel cadeias de relações de afinidade. Isso significa que um serviço filho em um relacionamento de afinidade não pode ser pai em outro relacionamento de afinidade. Se você quiser toomodel esse tipo de relação, você tem efetivamente toomodel-lo como uma estrela, em vez de uma cadeia. toomove de estrela de tooa uma cadeia, filho na extremidade inferior Olá seria pai do filho do pai toohello primeiro. Dependendo da organização de saudação de seus serviços, você pode ter toodo esse procedimento várias vezes. Se não houver nenhum serviço pai natural, você pode ter toocreate um que funciona como um espaço reservado. Dependendo dos requisitos, talvez você queira toolook em [grupos de aplicativos](service-fabric-cluster-resource-manager-application-groups.md).

<center>
![Cadeias vs. Estrelas no hello contexto de relações de afinidade][Image2]
</center>

Outro toonote coisa sobre relações de afinidade de hoje é que eles são direcionais. Isso significa que a regra afinidade Olá impõe somente criança Olá colocada com pai hello. Ela não garante que pai hello está localizado com filho hello. Também é importante toonote que Olá relacionamento de afinidade não pode ser perfeito ou instantaneamente imposta como serviços diferentes com diferentes ciclos de vida e podem falhar e mover independentemente. Por exemplo, digamos que pai Olá repentinamente Falha ao nó tooanother porque ele falhou. Olá Gerenciador de recursos de Cluster e o identificador de Gerenciador de Failover Olá failover em primeiro lugar, como manter os serviços de hello, consistente e disponível é a prioridade de saudação. Após a conclusão do failover Olá, relação de afinidade Olá for interrompida, mas Olá Gerenciador de recursos de Cluster considera que tudo está bem até que observa que filho Olá não é localizado com pai hello. Esses tipos de verificações são executados periodicamente. Mais informações sobre como Olá Gerenciador de recursos de Cluster avalia as restrições estão disponíveis em [neste artigo](service-fabric-cluster-resource-manager-management-integration.md#constraint-types), e [este](service-fabric-cluster-resource-manager-balancing.md) fala mais sobre como tooconfigure Olá cadência na qual essas restrições são avaliada.   


### <a name="partitioning-support"></a>Suporte ao particionamento
Olá coisa final toonotice sobre a afinidade é que relações de afinidade não há suporte para onde o pai de saudação é particionada. Serviços pai particionados podem vir a ter suporte, mas atualmente isso não é permitido.

## <a name="next-steps"></a>Próximas etapas
- Para saber mais sobre como configurar os serviços, [Saiba mais sobre como configurar serviços](service-fabric-cluster-resource-manager-configure-services.md)
- toolimit serviços tooa um conjunto pequeno de máquinas ou agregação carga Olá de serviços, use [grupos de aplicativos](service-fabric-cluster-resource-manager-application-groups.md)

[Image1]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-affinity/cluster-resrouce-manager-affinity-modes.png
[Image2]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-affinity/cluster-resource-manager-chains-vs-stars.png