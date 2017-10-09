---
title: "carga do Azure microsserviço aaaManage usando métricas | Microsoft Docs"
description: "Saiba mais sobre como as métricas de tooconfigure e usar no Service Fabric toomanage serviço consumo de recursos."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 0d622ea6-a7c7-4bef-886b-06e6b85a97fb
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 592dc749ce30683a1e439a702b7d0dc0a638276f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-resource-consumption-and-load-in-service-fabric-with-metrics"></a>Gerenciando o consumo e a carga de recursos no Service Fabric com métricas
*Métricas* recursos de saudação valoriza seus serviços e que é fornecido por nós de saudação no cluster de saudação. Uma métrica é algo que você deseja toomanage no desempenho de saudação tooimprove ou o monitor de ordem de seus serviços. Por exemplo, você pode observar tooknow de consumo de memória se o serviço está sobrecarregado. Outro uso é toofigure out se serviço Olá podia se mover em outro lugar em que a memória é que menos restrita em um desempenho melhor ordem tooget.

Itens como Memória, Disco e Uso de CPU são exemplos de métricas. Essas métricas são métricas físicas, recursos que correspondem a recursos de toophysical no nó de saudação que precisam toobe gerenciado. As métricas também podem ser (e normalmente são) métricas lógicas. Métricas lógicas são itens como "MyWorkQueueDepth", "MessagesToProcess" ou "TotalRecords". Métricas lógicas são definidas pelo aplicativo e indiretamente correspondem toosome consumo de recursos físicos. Métricas lógicas são comuns, como pode ser difícil toomeasure e relatórios de consumo de recursos físicos em uma base por serviço. complexidade de saudação de medir e suas próprias métricas físicas de relatórios também é porque o serviço de malha fornece algumas métricas padrão.

## <a name="default-metrics"></a>Métricas padrão
Digamos que você deseja tooget iniciado gravar e implantar seu serviço. Neste ponto, você não sabe quais recursos físicos ou lógicos serão consumidos. Sem problemas! Olá Gerenciador de recursos de Cluster do serviço de malha usa algumas métricas padrão quando não há outras métricas são especificadas. Eles são:

  - PrimaryCount - contagem de réplicas primárias no nó Olá 
  - ReplicaCount - contagem total de réplicas com monitoração de estado no nó Olá
  - Contagem - contagem de todos os objetos de serviço (com e sem monitoração) no nó Olá

| Métrica | Carga de Instância Sem Estado | Carga Secundária com Estado | Carga Primária com Estado |
| --- | --- | --- | --- |
| PrimaryCount |0 |0 |1 |
| ReplicaCount |0 |1 |1 |
| Contagem |1 |1 |1 |

Para cargas de trabalho básicas, métricas de padrão de saudação fornecem uma distribuição razoável de trabalho no cluster hello. Saudação de exemplo a seguir, vamos ver o que acontece quando criamos dois serviços e confiar na métrica padrão de saudação para balanceamento de. serviço primeiro Olá é um serviço com monitoração de estado com três partições e uma réplica de destino define tamanho de três. segundo serviço de saudação é um serviço sem monitoração de estado com uma partição e uma contagem de instâncias de três.

Veja o acontece:

<center>
![Layout de cluster com métricas padrão][Image1]
</center>

Toonote algumas coisas:
  - As réplicas primárias para o serviço com monitoração de estado Olá são distribuídas por vários nós
  - Réplicas para a mesma partição são em nós diferentes de saudação
  - número total de saudação do primários e secundários é distribuído no cluster Olá
  - número total de saudação de objetos de serviço é alocado igualmente em cada nó

Ótimo!

métrica de padrão de saudação funciona muito bem como de início. No entanto, as métricas padrão de saudação apenas realizará a você até o momento. Por exemplo: o que é a probabilidade de saudação que Olá particionamento esquema separado resultados na utilização perfeitamente até mesmo por todas as partições? O que é a chance de Olá Olá carga para um determinado serviço é constante ao longo do tempo ou até mesmo Olá mesmo por várias partições agora?

Você pode executar com apenas as métricas saudação padrão. No entanto, isso geralmente significa que a utilização do cluster é menor e mais irregular que o desejado. Isso ocorre porque as métricas padrão de saudação não adaptáveis e vamos supor que tudo o que é equivalente. Por exemplo, uma réplica primária está ocupada e não é ambos os contribuem métrica de PrimaryCount toohello "1". No pior caso de Olá, usando apenas as métricas saudação padrão também pode resultar em nós overscheduled, resultando em problemas de desempenho. Se você estiver interessado em obter hello mais fora do seu cluster e evitar problemas de desempenho, você precisa toouse personalizados de métricas e relatórios de carga dinâmico.

## <a name="custom-metrics"></a>Métricas personalizadas
Métricas são configuradas em uma base por--serviço-instância nomeada quando você está criando o serviço de saudação.

Qualquer métrica possui propriedades que a descrevem: um nome, um peso e uma carga padrão.

* Nome de métrica: nome de saudação da métrica de saudação. nome da métrica Olá é um identificador exclusivo para a métrica Olá no cluster de saudação do ponto de vista do Gerenciador de recursos de saudação.
* Peso: Peso da métrica define a importância essa métrica é relativo toohello outras métricas para esse serviço.
* Padrão de carga: carga de padrão de saudação é representada diferente dependendo se o serviço de saudação é com ou sem estado.
  * Para serviços sem estado cada métrica tem uma propriedade única chamada DeafultLoad
  * Para serviços com estado, você define:
    * PrimaryDefaultLoad: quantidade dessa métrica que esse serviço consome quando ele é primária padrão da saudação
    * SecondaryDefaultLoad: quantidade de padrão de saudação dessa métrica que esse serviço consome quando ele for um secundário

> [!NOTE]
> Se você definir métricas personalizadas e deseja too_also_ usar a métrica da saudação padrão, será necessário too_explicitly_ adicionar métricas de padrão de saudação fazer e definem os pesos e os valores para eles. Isso ocorre porque você deve definir a relação de saudação entre as métricas padrão de saudação e suas métricas personalizadas. Por exemplo, talvez você se preocupe mais com ConnectionCount ou WorkQueueDepth do que com a distribuição Principal. Por peso de saudação do padrão de saudação PrimaryCount métrica é alta, para que você deseja tooreduce-tooMedium quando você adiciona o tooensure de métricas que eles têm precedência.
>

### <a name="defining-metrics-for-your-service---an-example"></a>Definindo métricas para seu serviço - um exemplo
Vamos supor que você queira Olá a seguinte configuração:

  - O serviço relata uma métrica denominada “ConnectionCount”
  - Você deseja que as métricas do toouse saudação padrão 
  - Você fez algumas medições e sabe que normalmente uma réplica Primária desse serviço requer 20 unidades de “ConnectionCount”
  - As secundárias usam 5 unidades de "ConnectionCount"
  - Você sabe que "ConnectionCount" hello mais importante em termos de Gerenciando o desempenho de saudação do serviço específico
  - Você ainda deseja que as réplicas Principais sejam balanceadas. Balancear réplicas primárias geralmente é uma boa ideia. Isso ajuda a evitar a perda de saudação de algum nó ou falha de domínio afetam a maioria das réplicas primárias junto com ele. 
  - Caso contrário, as métricas padrão de saudação são permitidas

Aqui está o código de saudação que você escreve toocreate um serviço com essa configuração de métrica:

Código:

```csharp
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
StatefulServiceLoadMetricDescription connectionMetric = new StatefulServiceLoadMetricDescription();
connectionMetric.Name = "ConnectionCount";
connectionMetric.PrimaryDefaultLoad = 20;
connectionMetric.SecondaryDefaultLoad = 5;
connectionMetric.Weight = ServiceLoadMetricWeight.High;

StatefulServiceLoadMetricDescription primaryCountMetric = new StatefulServiceLoadMetricDescription();
primaryCountMetric.Name = "PrimaryCount";
primaryCountMetric.PrimaryDefaultLoad = 1;
primaryCountMetric.SecondaryDefaultLoad = 0;
primaryCountMetric.Weight = ServiceLoadMetricWeight.Medium;

StatefulServiceLoadMetricDescription replicaCountMetric = new StatefulServiceLoadMetricDescription();
replicaCountMetric.Name = "ReplicaCount";
replicaCountMetric.PrimaryDefaultLoad = 1;
replicaCountMetric.SecondaryDefaultLoad = 1;
replicaCountMetric.Weight = ServiceLoadMetricWeight.Low;

StatefulServiceLoadMetricDescription totalCountMetric = new StatefulServiceLoadMetricDescription();
totalCountMetric.Name = "Count";
totalCountMetric.PrimaryDefaultLoad = 1;
totalCountMetric.SecondaryDefaultLoad = 1;
totalCountMetric.Weight = ServiceLoadMetricWeight.Low;

serviceDescription.Metrics.Add(connectionMetric);
serviceDescription.Metrics.Add(primaryCountMetric);
serviceDescription.Metrics.Add(replicaCountMetric);
serviceDescription.Metrics.Add(totalCountMetric);

await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

Powershell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton –Metric @("ConnectionCount,High,20,5”,"PrimaryCount,Medium,1,0”,"ReplicaCount,Low,1,1”,"Count,Low,1,1”)
```

> [!NOTE]
> Olá acima exemplos e hello restante deste documento descrevem as métricas de gerenciamento em uma base por chamada-serviço. Também é possível toodefine métricas para os serviços no serviço de saudação _tipo_ nível. Isso é feito especificando-as em seus manifestos de serviço. Não é recomendável definir as métricas do nível de tipo por vários motivos. Olá primeiro motivo é que os nomes de métrica são frequentemente específico do ambiente. A menos que haja um contrato sólido em vigor, você não pode ter certeza de que métrica hello "Núcleos" em um ambiente não é "MiliCores" ou "Núcleos" em outros. Se suas métricas são definidas em seu manifesto, você precisará manifestos de novo toocreate por ambiente. Isso geralmente leva tooa proliferação de manifestos diferentes com apenas algumas diferenças, que podem levar a problemas de toomanagement.  
>
> Cargas de métricas normalmente são atribuídas por instância de serviço nomeada. Por exemplo, digamos que você criar uma instância de saudação do serviço para CustomerA que planeja toouse-pouco. Digamos que você também crie outra para ClienteB que tem uma carga de trabalho maior. Nesse caso, talvez seja conveniente padrão de saudação tootweak carrega para esses serviços. Se você tiver as métricas e carrega definida por meio de manifestos e você deseja toosupport neste cenário, requer diferentes aplicativos e tipos de serviço para cada cliente. valores de saudação definidos no momento da criação de serviço substituem as definidas no manifesto de hello, portanto você pode usar esse tooset Olá os padrões específicos. No entanto, isso faz com que valores hello declarados na correspondência de toonot manifestos Olá com que esses Olá serviço realmente é executado. Isso pode levar tooconfusion. 
>

Como um lembrete: se você quiser apenas as métricas do toouse saudação padrão, não precisa a coleção de métricas Olá tootouch em todos os ou fazer algo especial ao criar o serviço. métrica de padrão de saudação obter usada automaticamente quando não há outros são definidos. 

Agora, vamos percorrer cada uma dessas configurações mais detalhadamente e falar sobre o comportamento de saudação que ela influencia.

## <a name="load"></a>Carregar
Olá objetivo de definir métricas é toorepresent alguma carga. *Carga* é a quantidade de determinada métrica consumida por alguma instância de serviço ou réplica em determinado nó. A carga pode ser configurada em praticamente qualquer ponto. Por exemplo:

  - A carga pode ser definida quando um serviço é criado. Isso é chamado de _carga padrão_.
  - carrega informações de métrica Hello, incluindo padrão, para um serviço pode ser atualizado depois Olá serviço é criado. Isso é chamado de _atualização de um serviço_. 
  - Olá cargas para uma determinada partição podem ser redefinição toohello os valores padrão para o serviço. Isso é chamado de _redefinição da carga de partição_.
  - A carga pode ser relatada por objeto de serviço dinamicamente em tempo de execução. Isso é chamado de _relatório de carga_. 
  
Todas essas estratégias podem ser usadas em Olá mesmo de serviços por meio de seu ciclo de vida. 

## <a name="default-load"></a>Carga padrão
*Padrão de carga* é a quantidade de métrica Olá consome de cada objeto de serviço (instância sem monitoração de estado ou réplica com monitoração de estado) do serviço. Olá Gerenciador de recursos de Cluster usa esse número para carga de saudação do objeto de serviço Olá até receber outra informação, como um relatório de carga dinâmico. Para serviços mais simples, a carga de padrão de saudação é uma definição estática. carga de padrão de saudação nunca é atualizada e é usada pelo tempo de vida de saudação do serviço de saudação. Padrão carrega funciona bem para cenários em que certos valores de recursos dedicados toodifferent cargas de trabalho e não alteram de planejamento de capacidade simple.

> [!NOTE]
> Para obter mais informações sobre o gerenciamento de capacidade e definindo as capacidades para nós de saudação em seu cluster, consulte [neste artigo](service-fabric-cluster-resource-manager-cluster-description.md#capacity).
> 

Olá Gerenciador de recursos de Cluster permite toospecify services com monitoração de estado uma carga padrão diferente para seus primários e secundários. Serviços sem estado só podem especificar um valor que se aplica a instâncias de tooall. Para serviços com monitoração de estado, o carregamento de padrão de Olá para réplicas primária e secundária são normalmente diferente como réplicas diferentes tipos de trabalho em cada função. Por exemplo, primárias geralmente servem leituras e gravações e lidar com a maioria da carga de computação hello, enquanto secundários não. Geralmente a carga do saudação padrão para uma réplica primária é maior que o saudação padrão de carga para réplicas secundárias. números reais de saudação depende de suas próprias medidas.

## <a name="dynamic-load"></a>Carga dinâmica
Digamos que você esteja executando o serviço há algum tempo. Com o monitoramento, você observou que:

1. Algumas partições ou instâncias de determinado serviço consomem mais recursos do que outras
2. Alguns serviços têm carga que varia ao longo do tempo.

Há muitos itens que podem causar esses tipos de flutuações de carga. Por exemplo, serviços ou partições diferentes estão associadas com diferentes clientes com diferentes requisitos. Carga também pode alterar como valor de saudação do serviço de saudação do trabalho varia Olá longo do dia de saudação. Independentemente do motivo hello, normalmente há um número de único que você pode usar para padrão. Isso é especialmente verdadeiro se você quiser tooget Olá utilização mais fora do cluster de saudação. Qualquer valor que você escolher para o padrão de carga é errado alguns tempo de saudação. Padrão incorreto carrega resultam em Olá Gerenciador de recursos de Cluster de failover ou na alocação de recursos. Como resultado, você pode ter nós acima ou abaixo utilizados, embora Olá Gerenciador de recursos de Cluster considera cluster Olá é equilibrada. As cargas padrão ainda são válidas, pois fornecem algumas informações para o posicionamento inicial, mas não dão a visão completa das cargas de trabalho reais. tooaccurately captura alterações de requisitos de recursos, Olá Gerenciador de recursos de Cluster permite que cada tooupdate de objeto de serviço sua própria carga durante o tempo de execução. Isso é chamado de relatório dinâmico de carga.

Relatórios de carga dinâmico permitem tooadjust réplicas ou as instâncias sua carga de alocação/relatados de métricas em seu tempo de vida. Uma réplica de serviço ou uma instância inoperante e que não realizasse trabalho normalmente informaria que estava usando valores baixos de determinada métrica. Uma réplica ou instância ocupada relataria que está usando mais.

Carga por réplica ou instância de relatórios permite que Olá tooreorganize do Gerenciador de recursos de Cluster de objetos de serviço individual Olá Olá cluster. A reorganização de serviços Olá ajuda a garantir que eles obtenham recursos Olá que exigem. Serviços de ocupado efetivamente obtém muito "recuperar" recursos de outras réplicas ou as instâncias que estão atualmente frio ou fazer menos trabalho.

Em serviços confiáveis, carga de tooreport Olá código dinamicamente tem esta aparência:

Código:

```csharp
this.Partition.ReportLoad(new List<LoadMetric> { new LoadMetric("CurrentConnectionCount", 1234), new LoadMetric("metric1", 42) });
```

Um serviço pode relatar em qualquer uma das métricas de saudação definidas para ele no momento da criação. Se uma carga de relatórios de serviço para uma métrica que ele não está configurado toouse, o Service Fabric ignora esse relatório. Se houver outras métricas relatadas em Olá mesmo tempo que são válidos, esses relatórios são aceitas. Código de serviço pode medir e relatar todas Olá métricas sabe como, e operadores poderá especificar Olá configuração métrica toouse sem código de serviço toochange hello. 

### <a name="updating-a-services-metric-configuration"></a>Atualizando a configuração da métrica do serviço
lista de saudação de métricas associadas ao serviço de saudação e propriedades Olá dessas métricas podem ser atualizadas dinamicamente enquanto o serviço hello está ativo. Isso permite flexibilidade e a oportunidade de fazer experimentos. Alguns exemplos de quando isso é útil são:

  - ao desabilitar uma métrica com um relatório com bugs para um serviço específico
  - reconfigurar os pesos de saudação de métricas com base no comportamento desejado
  - habilitando uma métrica novo somente depois que o código de saudação já foi implantado e validado por meio de outros mecanismos
  - alterando o saudação padrão de carga para um serviço com base no consumo e comportamento observado

Olá principais APIs para alterar a configuração de métrica são `FabricClient.ServiceManagementClient.UpdateServiceAsync` em c# e `Update-ServiceFabricService` no PowerShell. Quaisquer informações que você especificar com essas APIs substituem Olá as informações de métrica existente para o serviço de saudação imediatamente. 

## <a name="mixing-default-load-values-and-dynamic-load-reports"></a>Combinando valores de carga padrão e relatórios de carga dinâmica
Padrão de carga e carrega dinâmica pode ser usadas para Olá mesmo serviço. Quando o serviço utiliza os relatórios de carga padrão e carga dinâmica carga padrão serve como uma estimativa até os relatórios dinâmicos serem gerados. Padrão de carga é bom porque oferece Olá Gerenciador de recursos de Cluster algo toowork com. saudação de carga de padrão permite Olá tooplace do Gerenciador de recursos de Cluster objetos de serviço de saudação em locais bom quando eles são criados. Se nenhuma informação de carga padrão for fornecida, o posicionamento dos serviços será efetivamente aleatório. Quando os relatórios de carga chegam mais tarde colocação aleatória inicial de saudação geralmente é incorreta e Olá Gerenciador de recursos de Cluster com os serviços de toomove.

Vamos conferir nosso exemplo anterior e ver o que acontece quando adicionamos algumas métricas personalizadas e relatórios dinâmicos de carga. Neste exemplo, usamos "MemoryInMb" como uma métrica de exemplo.

> [!NOTE]
> Memória é uma das métricas de sistema de saudação do Service Fabric pode [controlam recursos](service-fabric-resource-governance.md), e relatá-las é difícil normalmente. Não, na verdade, esperamos que você tooreport consumo de memória; A memória é usada como um toolearning ajuda sobre recursos de saudação do hello Gerenciador de recursos de Cluster.
>

Vamos supor que inicialmente criamos serviço com monitoração de estado Olá com hello comando a seguir:

Powershell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton –Metric @("MemoryInMb,High,21,11”,"PrimaryCount,Medium,1,0”,"ReplicaCount,Low,1,1”,"Count,Low,1,1”)
```

Como lembrete, essa sintaxe é ("MetricName, MetricWeight, PrimaryDefaultLoad, SecondaryDefaultLoad").

Vamos ver qual poderia ser a aparência de um layout de cluster:

<center>
![Cluster equilibrado com métricas padrão e personalizadas][Image2]
</center>

Algumas coisas que vale a pena observar:

* As réplicas secundárias dentro de uma partição podem ter cada uma a sua própria carga
* Geral métricas Olá aparência equilibradas. Para a memória, Olá taxa entre Olá máximo e mínimo de carga é 1,75 (nó Olá com hello mais carga é N3, Olá é menos N2 e 28/16 = 1,75).

Há algumas coisas que precisamos ainda tooexplain:

* O que determinou se uma taxa de 1,75 é razoável ou não? Como a saudação Gerenciador de recursos de Cluster saber se há ou se não houver mais toodo de trabalho?
* Quando o balanceamento acontece?
* O que significa que a memória foi ponderada como "Alta"?

## <a name="metric-weights"></a>Pesos de métrica
Controle Olá mesmo métricas em diferentes serviços é importante. Se a exibição global é o que permite Olá consumo de tootrack do Gerenciador de recursos de Cluster no cluster hello, equilibrar o consumo em nós e certifique-se de que nós não passam pela capacidade. No entanto, serviços podem ter diferentes modos de exibição como toohello importância da saudação mesma métrica. Além disso, em um cluster com várias métricas e muitos serviços, talvez não existam soluções perfeitamente equilibradas para todas as métricas. Como Olá Gerenciador de recursos de Cluster deve tratar essas situações?

Métricos pesos permitem Olá toodecide do Gerenciador de recursos de Cluster como toobalance Olá cluster quando não há nenhuma resposta perfeita. Métricos pesos também permitem que Olá toobalance do Gerenciador de recursos de Cluster serviços específicos diferente. As métricas podem ter quatro níveis de peso diferente: zero, baixa, média e alta. Uma métrica com um peso Zero não contribui em nada ao considerar se as coisas estão balanceadas ou não. No entanto, sua carga ainda contribuem toocapacity gerenciamento. Métricas com peso Zero ainda são úteis e costumam ser usadas como parte do monitoramento de desempenho e do comportamento de serviço. [Este artigo](service-fabric-diagnostics-event-generation-infra.md) fornece mais informações sobre o uso de Olá das métricas de monitoramento e diagnóstico dos seus serviços. 

Olá impacto real pesos de métrica diferentes no cluster Olá é que esse gerenciador de recursos de Cluster hello gera diferentes soluções. Métricos pesos informam Olá Gerenciador de recursos de Cluster que determinadas métricas são mais importantes do que outras pessoas. Quando não houver nenhum Olá solução perfeita Gerenciador de recursos de Cluster pode preferir soluções que equilibram Olá superior ponderada métricas melhor. Se um serviço achar que uma métrica específica não é importante, ele poderá considerar seu uso dessa métrica desequilibrado. Isso permite que outro tooget de serviço uma distribuição uniforme de alguns métrica que é importante tooit.

Vejamos um exemplo de alguns relatórios de carga e uma métrica diferente como pondera resulta em várias alocações no cluster hello. Neste exemplo, podemos ver que alternar peso relativo de saudação de métricas de saudação causa Olá toocreate do Gerenciador de recursos de Cluster de diferentes organizações de serviços.

<center>
![Exemplo de ponderação da métrica e seu impacto sobre as soluções de balanceamento][Image3]
</center>

Neste exemplo, há quatro serviços diferentes, todos relatando diferentes valores para duas métricas diferentes, Métrica A e Métrica B. Em um caso, todos os serviços de saudação definem MetricA é mais importante de hello (peso = alta) e MetricB como importantes (peso = baixo). Como resultado, podemos ver que Olá Gerenciador de recursos de Cluster coloca serviços Olá para que é melhor MetricA balanceada que MetricB. "Melhor equilibrada" significa que a Métrica A tem um desvio padrão menor que a Métrica B. No segundo caso de Olá, podemos reverter pesos métrica hello. Como resultado, Olá Gerenciador de recursos de Cluster troca serviços A e B toocome backup com uma alocação onde MetricB é mais equilibrada que MetricA.

> [!NOTE]
> Métricos pesos determinam como Olá Gerenciador de recursos de Cluster deve equilibrar, mas não quando balanceamento deve ocorrer. Para saber mais sobre balanceamento, leia [este artigo](service-fabric-cluster-resource-manager-balancing.md)
>

### <a name="global-metric-weights"></a>Pesos de métrica global
Digamos que Services define MetricA como alta de peso e ServiceB define o peso de saudação para MetricA tooLow ou Zero. O que é o peso real de saudação que acaba acostumar?

Há vários pesos que são rastreados para cada métrica. Peso primeiro Olá é hello definido para a métrica de saudação quando Olá serviço é criado. Olá, outros peso é um peso global, que é calculado automaticamente. Olá Gerenciador de recursos de Cluster usa esses níveis de importância quando soluções de pontuação. Considerar ambos os pesos é importante. Isso permite que Olá toobalance do Gerenciador de recursos de Cluster de cada serviço tooits acordos possuir prioridades e também como um todo é alocado corretamente, verifique se esse cluster hello.

O que aconteceria se Olá Gerenciador de recursos de Cluster não importa saldo global e local? Bem, é fácil tooconstruct soluções que são balanceados globalmente, mas que pode resultar no equilíbrio de recursos de baixo para serviços individuais. Em Olá exemplo a seguir, vamos examinar um serviço configurado com apenas as métricas saudação padrão e veja o que acontece quando somente o saldo global é considerado:

<center>
![Olá impacto de uma solução somente Global][Image4]
</center>

O exemplo de superior Olá com base apenas em equilíbrio global, Olá cluster como um todo é realmente equilibrado. Todos os nós têm Olá mesma contagem de primárias e Olá mesmo número total de réplicas. No entanto, se você observar o impacto real Olá essa alocação não é tão boa: perda de saudação de qualquer nó afeta uma carga de trabalho específica desproporcionalmente, porque usa todos os seus primários. Por exemplo, se primeiro nó de saudação falhar três cores primárias de saudação para Olá três diferentes partições de saudação serviço círculo todos seriam perdidos. Por outro lado, hello triângulo e serviços hexágono tem suas partições de perder uma réplica. Isso faz com que sem interrupção, diferente de ter toorecover Olá para baixo de réplica.

No exemplo de inferior hello, Olá Gerenciador de recursos de Cluster tenha distribuído réplicas Olá com base em ambos os equilíbrio de saudação global e por serviço. Ao calcular a pontuação de saudação da solução Olá ele fornece a maioria das soluções globais da saudação peso toohello e services tooindividual parte (configurável). Saldo global para uma métrica é calculado com base na média de saudação de pesos de métrica de saudação de cada serviço. Cada serviço é equilibrado acordo tooits próprio definido métrica pesos. Isso garante que serviços Olá são balanceados em si, de acordo com tootheir próprias necessidades. Como resultado, se hello mesmo primeiro nó falha Olá é distribuído entre todas as partições de todos os serviços. Olá impacto tooeach é Olá mesmo.

## <a name="next-steps"></a>Próximas etapas
- Para obter mais informações sobre a configuração de serviços, [Saiba mais sobre como configurar serviços](service-fabric-cluster-resource-manager-configure-services.md)(service-fabric-cluster-resource-manager-configure-services.md)
- Definir métricas de desfragmentação é carga tooconsolidate unidirecional em nós em vez de propagação de. toolearn como tooconfigure desfragmentação, consulte muito[neste artigo](service-fabric-cluster-resource-manager-defragmentation-metrics.md)
- toofind out sobre como Olá Gerenciador de recursos de Cluster gerencia e equilibra a carga no cluster hello, check-out artigo Olá em [balanceamento de carga](service-fabric-cluster-resource-manager-balancing.md)
- Desde o início de saudação e [obter uma introdução toohello Gerenciador de recursos de Cluster do serviço de malha](service-fabric-cluster-resource-manager-introduction.md)
- O custo de movimento é uma forma de sinalização toohello Gerenciador de recursos de Cluster que determinados serviços são toomove mais caro do que outros. toolearn mais sobre o custo de movimento, consulte muito[neste artigo](service-fabric-cluster-resource-manager-movement-cost.md)

[Image1]:./media/service-fabric-cluster-resource-manager-metrics/cluster-resource-manager-cluster-layout-with-default-metrics.png
[Image2]:./media/service-fabric-cluster-resource-manager-metrics/Service-Fabric-Resource-Manager-Dynamic-Load-Reports.png
[Image3]:./media/service-fabric-cluster-resource-manager-metrics/cluster-resource-manager-metric-weights-impact.png
[Image4]:./media/service-fabric-cluster-resource-manager-metrics/cluster-resource-manager-global-vs-local-balancing.png
