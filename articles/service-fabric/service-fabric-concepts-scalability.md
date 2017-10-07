---
title: "aaaScalability de serviços do Service Fabric | Microsoft Docs"
description: "Descreve como os serviços do Service Fabric tooscale"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: ed324f23-242f-47b7-af1a-e55c839e7d5d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 5af06f8f71ad5dee32ba115b922842684867e654
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-in-service-fabric"></a>Dimensionamento no Service Fabric
Malha do serviço do Azure torna aplicativos escalonáveis toobuild fácil por meio do gerenciamento de serviços hello, partições e réplicas em nós de saudação de um cluster. Executando várias cargas de trabalho Olá mesmo hardware habilita utilização máxima dos recursos, mas também fornece flexibilidade em termos de como você escolhe tooscale suas cargas de trabalho. 

O dimensionamento no Service Fabric é feito várias maneiras diferentes:

1. Dimensionamento criando ou removendo instâncias de serviço sem estado
2. Dimensionamento criando ou removendo novos serviços nomeados
3. Dimensionamento criando ou removendo novas instâncias de aplicativos nomeados
4. Dimensionamento usando serviços particionados
5. Dimensionamento adicionando e removendo nós do cluster Olá 
6. Dimensionamento usando métricas do Gerenciador de Recursos de Cluster

## <a name="scaling-by-creating-or-removing-stateless-service-instances"></a>Dimensionamento criando ou removendo instâncias de serviço sem estado
Uma saudação tooscale mais simples de maneiras dentro do Service Fabric funciona com serviços sem monitoração de estado. Quando você cria um serviço sem monitoração de estado, você obtém uma chance toodefine um `InstanceCount`. `InstanceCount`define quantas cópias em execução de código do serviço são criadas quando o serviço de saudação é iniciado. Digamos que, por exemplo, há 100 nós no cluster de saudação. Digamos também que um serviço seja criado com um `InstanceCount` igual a 10. Durante a execução, as 10 cópias em execução de código Olá podem todos se tornar muito ocupadas (ou podem não estar ocupadas suficiente). Uma maneira tooscale essa carga de trabalho é o número de saudação do toochange de instâncias. Por exemplo, alguma parte do código de monitoramento ou gerenciamento pode alterar número de saudação existentes de instâncias too50 ou too5, dependendo se a carga de trabalho Olá precisa tooscale in ou out Olá com base na carga. 

C#:

```csharp
StatelessServiceUpdateDescription updateDescription = new StatelessServiceUpdateDescription(); 
updateDescription.InstanceCount = 50;
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/app/service"), updateDescription);
```

Powershell:

```posh
Update-ServiceFabricService -Stateless -ServiceName $serviceName -InstanceCount 50
```
### <a name="using-dynamic-instance-count"></a>Usando a Contagem de Instâncias Dinâmica
Especificamente para serviços sem monitoração de estado, o Service Fabric oferece uma contagem de instâncias de saudação de toochange de forma automática. Isso permite Olá serviço tooscale dinamicamente com número de saudação de nós que estão disponíveis. Olá tooopt de maneira em que esse comportamento é a contagem de instâncias de saudação tooset = -1. InstanceCount = -1 é uma instrução tooService malha que diz "Executar esse serviço sem monitoração de estado em todos os nós". Se Olá número de nós é alterado, o Service Fabric altera automaticamente Olá toomatch de contagem de instância, garantindo que hello está sendo executado em todos os nós válido. 

C#:

```csharp
StatelessServiceDescription serviceDescription = new StatelessServiceDescription();
//Set other service properties necessary for creation....
serviceDescription.InstanceCount = -1;
await fc.ServiceManager.CreateServiceAsync(serviceDescription);
```

Powershell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName -Stateless -PartitionSchemeSingleton -InstanceCount "-1"
```

## <a name="scaling-by-creating-or-removing-new-named-services"></a>Dimensionamento criando ou removendo novos serviços nomeados
Uma instância de serviço nomeado é uma instância específica de um tipo de serviço (consulte [ciclo de vida do aplicativo do Service Fabric](service-fabric-application-lifecycle.md)) em algumas instâncias de aplicativo nomeada em cluster hello. 

Novas instâncias de serviço nomeadas podem ser criadas (ou removidas) conforme os serviços ficarem mais ou menos ocupados. Isso permite que solicitações toobe disseminadas por mais instâncias de serviço, geralmente permitindo a carga em toodecrease de serviços existentes. Ao criar serviços, Olá Gerenciador de recursos de Cluster do serviço de malha coloca serviços Olá no cluster de saudação de maneira distribuída. decisões exata Olá são administradas por Olá [métricas](service-fabric-cluster-resource-manager-metrics.md) no cluster hello e outras regras de posicionamento. Serviços podem ser criados de várias maneiras diferentes, mas hello mais comuns são por meio de ações administrativas como alguém chamar [ `New-ServiceFabricService` ](https://docs.microsoft.com/en-us/powershell/module/servicefabric/new-servicefabricservice?view=azureservicefabricps), ou chamando código [ `CreateServiceAsync` ](https://docs.microsoft.com/en-us/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync?view=azure-dotnet). `CreateServiceAsync`pode até mesmo ser chamado de dentro de outros serviços em execução no cluster de saudação.

A criação de serviços de forma dinâmica pode ser usada em todo tipo de cenário e é um padrão comum. Por exemplo, considere um serviço com estado que representa um fluxo de trabalho específico. Chamadas que representa o trabalho vai tooshow toothis serviço e esse serviço é contínuo tooexecute Olá etapas toothat fluxo de trabalho e o registro de progresso. 

Como você faria essa escala de serviço específico? Olá serviço pode ser multilocatário de alguma forma e aceitar as chamadas e iniciar as etapas para muitas instâncias diferentes do hello mesmo fluxo de trabalho ao mesmo tempo. No entanto, que pode tornar Olá código mais complexo, pois agora tem tooworry sobre muitas instâncias diferentes do hello mesmo fluxo de trabalho, todas as em diferentes estágios e de clientes diferentes. Além disso, tratamento de vários fluxos de trabalho no hello ao mesmo tempo não resolve Olá problema de escala. Isso ocorre porque, em algum momento, esse serviço consumirá toofit um número excessivo de recursos em um computador específico. Muitos serviços não criados para esse padrão em primeiro lugar de saudação ter dificuldade devido afunilamento inerente toosome ou lentidão no seu código. Esses tipos de problemas de fazer com que o serviço de saudação não toowork bem quando o número de saudação de fluxos de trabalho simultâneos está controlando obtém maior.  

Uma solução é toocreate uma instância desse serviço para cada instância diferente do fluxo de trabalho Olá deseja tootrack. Este é um ótimo padrão e funciona se o serviço de saudação é com ou sem estado. Para este toowork padrão, há geralmente outro serviço que atua como um "serviço de Gerenciador de carga de trabalho". trabalho de saudação do serviço é tooreceive solicitações e tooroute esses serviços de tooother solicitações. Gerenciador de saudação pode criar dinamicamente uma instância de serviço de carga de trabalho hello quando ele recebe a mensagem de saudação e passar nos serviços de toothose solicitações. serviço de Gerenciador de saudação também pode receber retornos de chamada quando um serviço de fluxo de trabalho concluir seu trabalho. Quando o Gerenciador de saudação recebe esses retornos de chamada ele pode excluir essa instância do serviço de fluxo de trabalho de saudação ou deixá-lo se mais chamadas são esperadas. 

Versões avançadas desse tipo de Gerenciador podem até mesmo criar pools de serviços de saudação que ele gerencia. pool de saudação ajuda a garantir que, quando uma nova solicitação chega ele não tem toowait para Olá serviço toospin. Em vez disso, Gerenciador de saudação pode apenas escolher um serviço de fluxo de trabalho que não está ocupado no momento do pool de saudação ou rotear aleatoriamente. Manter um pool de serviços disponíveis faz novas solicitações de manipulação mais rapidamente, pois é menos provável que a solicitação Olá tenha toowait para um novo toobe de serviço girado para cima. A criação de novos serviços é rápida, mas não é gratuita ou instantânea. pool de saudação ajuda a minimizar Olá tempo solicitação Olá tem toowait antes que estão sendo atendidas. Você verá esse gerenciador e pool padrão geralmente quando os tempos de resposta mais importam hello. Solicitação de enfileiramento de mensagens de saudação e criar serviço Olá no plano de fundo de saudação e _, em seguida,_ transmiti-lo em também é um padrão de Gerenciador populares, como é criar e excluir serviços com base em algum controle da quantidade de saudação do trabalho desse serviço no momento tem pendente. 

## <a name="scaling-by-creating-or-removing-new-named-application-instances"></a>Dimensionamento criando ou removendo novas instâncias de aplicativos nomeados
Criar e excluir instâncias de todo o aplicativo são padrão toohello semelhante de criação e exclusão de serviços. Para esse padrão, há alguns service manager que está fazendo a decisão de saudação com base nas solicitações de saudação que está vendo e informações hello está recebendo do hello outros serviços dentro do cluster de saudação. 

Quando a criação de uma nova instância de aplicativo nomeada deve ser usada em vez da criação de uma nova instância de serviço nomeada em algum aplicativo já existente? Há alguns casos:

  * nova instância do aplicativo Hello é para um cliente cujo código precisa toorun em alguma identidade específica ou configurações de segurança.
    * Serviço de malha permite definir toorun de pacotes de código diferente em identidades específicas. Em ordem toolaunch hello mesmo pacote de código em identidades diferentes, ativações Olá necessário toooccur em instâncias de aplicativo diferente. Considere um caso em que você tem as cargas de trabalho de um cliente existente implantadas. Eles podem estar em execução sob uma identidade específica para que possa monitorar e controlar seus tooother acessar recursos, como bancos de dados remotos ou outros sistemas. Nesse caso, quando se inscreve um novo cliente, provavelmente você não precisa tooactivate seu código em Olá mesmo contexto (espaço de processo). Enquanto você poderia, isso dificulta o tooact de código de serviço no contexto de saudação de uma identidade específica. Normalmente, você precisa ter mais código de gerenciamento de identidade, isolamento e segurança. Em vez de usar diferentes denominada serviço instâncias dentro Olá a mesma instância de aplicativo e, portanto, Olá mesmo espaço de processo, você pode usar diferentes instâncias nomeadas do aplicativo de malha do serviço. Isso torna mais fácil contextos de identidade diferentes toodefine.
  * nova instância do aplicativo Hello também serve como um meio de configuração
    * Por padrão, todos Olá chamado instâncias do serviço de um tipo de serviço específico em uma instância do aplicativo serão executado no mesmo processo em um determinado nó de saudação. Isso significa que, embora você possa configurar cada instância de serviço de forma diferente, fazer isso é complicado. Serviços devem ter alguns token usarem toolook a sua configuração dentro de um pacote de configuração. Geralmente, isso é apenas o nome do serviço de saudação. Isso funciona bem, mas associa nomes de toohello configuração Olá Olá individuais nomeado de instâncias de serviço na instância do aplicativo. Isso pode ser confuso e toomanage rígido desde a configuração normalmente é um artefato de tempo de design com valores específicos de instância de aplicativo. Criar mais serviços sempre significa que atualizações de aplicativo mais informações de saudação toochange dentro de pacotes de configuração de saudação ou toodeploy novas para que os novos serviços de saudação podem procurar suas informações específicas. Geralmente é mais fácil toocreate uma nova instância de aplicativo nomeada. Em seguida, você pode usar tooset de parâmetros do aplicativo hello qualquer configuração é necessária para os serviços de saudação. Dessa forma, todos os serviços de saudação que são criados dentro desse denominado instância do aplicativo pode herdar as definições de configuração específico. Por exemplo, em vez de ter um único arquivo de configuração com configurações de saudação e personalizações de cada cliente, como segredos ou por limites de recursos de cliente, você em vez disso, teria uma instância de aplicativo diferente para cada cliente com essas configurações substituído. 
  * novo aplicativo de saudação serve como um limite de atualização
    * Dentro do Service Fabric, instâncias de aplicativo nomeadas diferentes servem como limites de atualização. Uma atualização de uma instância nomeada do aplicativo não terá impacto sobre código Olá outra instância de aplicativo nomeada em execução. Olá diferentes aplicativos terminarão executando versões diferentes do mesmo código de saudação em Olá mesmos nós. Isso pode ser um fator quando precisar toomake uma decisão de escala, porque você pode escolher que se o novo código de saudação deve seguir Olá mesmo atualiza como outro serviço ou não. Por exemplo, digamos que uma chamada chega ao serviço de Gerenciador de saudação que é responsável por dimensionar cargas de trabalho de um determinado cliente, criando e excluindo serviços dinamicamente. Nesse caso, no entanto, chamada hello é para uma carga de trabalho associada com um _novo_ ao cliente. A maioria dos clientes como sendo isolados uns dos outros não apenas por motivos de segurança e configuração de saudação listados anteriormente, mas porque ele oferece mais flexibilidade em termos de executando versões específicas do software hello e escolhendo quando eles atualizado. Você também pode criar uma nova instância de aplicativo e criar serviço Olá existe simplesmente toofurther partição Olá quantidade de seus serviços de qualquer uma atualização afeta. Instâncias de aplicativo separadas proporcionam maior granularidade ao fazer atualizações de aplicativo e também habilitam testes A/B e implantações de verde/azul. 
  * instância de aplicativo existente Hello está cheio
    * No Service Fabric [capacidade de aplicativo](service-fabric-cluster-resource-manager-application-groups.md) é um conceito que você pode usar a quantidade de saudação toocontrol de recursos disponíveis para instâncias de determinado aplicativo. Por exemplo, você pode decidir que um determinado serviço precisa toohave outra instância criada na ordem tooscale. No entanto, essa instância de aplicativo está sem capacidade para uma determinada métrica. Se este cliente específico ou a carga de trabalho deve ainda receber mais recursos, em seguida, você pode aumentar capacidade de saudação existente para o aplicativo ou criar um novo aplicativo. 

## <a name="scaling-at-hello-partition-level"></a>Dimensionamento no nível da partição Olá
O Service Fabric permite o particionamento. O particionamento divide um serviço em várias seções lógicas e físicas, e cada uma delas funciona de forma independente. Isso é útil com os serviços com monitoração de estado, pois nenhum conjunto de réplicas tem toohandle todas as chamadas de saudação e manipular todos os estados de saudação ao mesmo tempo. Olá [visão geral de particionamento](service-fabric-concepts-partitioning.md) fornece informações sobre tipos de saudação dos esquemas de particionamentos que têm suporte. réplicas de saudação de cada partição são disseminadas por nós de saudação em um cluster, distribuindo a carga do serviço e garantindo que nenhum serviço hello como um todo ou qualquer partição tem um ponto único de falha. 

Considere um serviço que usa um esquema de particionamento de intervalo com uma chave baixa de 0, uma chave alta de 99 e uma contagem de partições de 4. Em um cluster de três nós, o serviço Olá pode ser disposto com quatro réplicas que compartilham recursos de saudação em cada nó, conforme mostrado aqui:

<center>
![Layout de partição com três nós](./media/service-fabric-concepts-scalability/layout-three-nodes.png)
</center>

Se você aumentar o número de saudação de nós, Service Fabric moverá algumas das réplicas existentes Olá existe. Por exemplo, digamos que toofour aumenta o número Olá de nós e réplicas Olá redistribuídas. Agora que o serviço de saudação agora tem três réplicas em execução em cada nó, cada que pertencem a partições toodifferent. Isso permite melhor utilização de recursos desde que o novo nó de saudação não está frio. Normalmente, ele também melhora o desempenho porque cada serviço tem mais tooit disponíveis de recursos.

<center>
![Layout de partição com quatro nós](./media/service-fabric-concepts-scalability/layout-four-nodes.png)
</center>

## <a name="scaling-by-using-hello-service-fabric-cluster-resource-manager-and-metrics"></a>Dimensionamento usando hello Gerenciador de recursos de Cluster do serviço de malha e métricas
[Métricas](service-fabric-cluster-resource-manager-metrics.md) são como serviços express seu consumo de recursos tooService malha. Uso de métricas fornece Olá Gerenciador de recursos de Cluster tooreorganize uma oportunidade e otimizar o layout de saudação do cluster hello. Por exemplo, pode haver muitos recursos em cluster hello, mas eles não podem ser alocados toohello serviços que estão atualmente fazendo o trabalho. Uso de métricas permite Olá tooreorganize do Gerenciador de recursos de Cluster Olá cluster tooensure serviços têm acesso toohello os recursos disponíveis. 


## <a name="scaling-by-adding-and-removing-nodes-from-hello-cluster"></a>Dimensionamento adicionando e removendo nós do cluster Olá 
Outra opção para dimensionar com o Service Fabric é toochange tamanho de saudação do cluster hello. Alterando o tamanho de saudação do cluster Olá significa adicionar ou remover nós de um ou mais tipos de nós de saudação em cluster hello. Por exemplo, considere um caso onde todos os nós de saudação em cluster Olá são dinâmicos. Isso significa que os recursos do cluster Olá quase todo consumida. Nesse caso, o cluster adicionando mais toohello de nós é Olá melhor maneira tooscale. Depois de ingressar em novos nós de Olá Olá Olá de cluster o Gerenciador de recursos de Cluster do serviço de malha move toothem de serviços, resultando em carga total menor em nós existentes Olá. Para serviços sem estado com contagem de instâncias = -1, mais instâncias de serviço são criadas automaticamente. Isso permite que alguns toomove chamadas de saudação nós toohello novos nós de existentes. 

Adicionando e removendo nós toohello cluster pode ser feito por meio do módulo de serviço malha do Azure Resource Manager PowerShell hello.

```posh
Add-AzureRmServiceFabricNode -ResourceGroupName $resourceGroupName -Name $clusterResourceName -NodeType $nodeTypeName  -NumberOfNodesToAdd 5 
Remove-AzureRmServiceFabricNode -ResourceGroupName $resourceGroupName -Name $clusterResourceName -NodeType $nodeTypeName -NumberOfNodesToRemove 5
```

## <a name="putting-it-all-together"></a>Juntando as peças
Vamos todas as ideias de saudação que discutimos aqui e se comunicar por meio de um exemplo. Considere Olá serviço a seguir: toobuild um serviço que atua como um catálogo de endereços está tentando manter em toonames e informações de contato. 

À direita com antecedência você tem um monte de tooscale de perguntas relacionadas: quantos usuários está você vai toohave? Quantos contatos cada usuário armazenará? Quando você estiver aguardando seu serviço para hello primeira vez que é difícil tentar toofigure isso tudo. Digamos que você fosse toogo com um único serviço estático com uma contagem de partição específica. consequências de saudação de separação Olá incorreto de contagem de partições pode causar problemas de escala toohave mais tarde. Da mesma forma, mesmo que você escolher contagem direita hello, que talvez você não tenha todas as informações de saudação é necessário. Por exemplo, também tiver toodecide tamanho de saudação do cluster de saudação com antecedência, em termos de número de saudação de nós e seus tamanhos. É geralmente rígido toopredict quantos recursos de um serviço será tooconsume durante sua vida útil. Ele também pode ser tooknow rígido à frente do padrão de tráfego do hello tempo serviço Olá realmente vê. Por exemplo, pessoas talvez adicionar e remover seus contatos somente primeira coisa manhã hello, ou talvez ele é distribuído uniformemente longo de saudação do dia de saudação. Com base em isso que talvez seja necessário tooscale sair e entrar dinamicamente. Talvez você pode aprender toopredict quando você vai tooneed tooscale sair e entrar, mas de qualquer forma provavelmente ficará toochanging tooneed tooreact o consumo de recursos por seu serviço. Isso pode envolver alterando o tamanho de saudação do cluster de saudação em ordem tooprovide mais recursos ao uso dos recursos existentes a reorganização não é suficiente. 

Mas por que mesmo tente toopick um esquema de partição única saída para todos os usuários? Por que limite tooone serviço e um cluster estático? situação real Olá é geralmente mais dinâmica. 

Ao compilar para escala, considere a possibilidade de saudação padrão dinâmico a seguir. Talvez seja necessário tooadapt-tooyour situação:

1. Em vez de tentar toopick um esquema de particionamento para qualquer pessoa no futuro, crie um serviço"manager".
2. trabalho de saudação do serviço de Gerenciador de saudação é toolook as informações do cliente ao se inscreverem para seu serviço. Dependendo de informações serviço de Gerenciador de saudação criar uma instância do seu _real_ serviço de armazenamento de contato _apenas para esse cliente_. Se eles exigem configuração específica, isolamento ou atualizações, você também pode decidir toospin uma instância de aplicativo para este cliente. 

Esse padrão de criação dinâmica traz muitos benefícios:

  - Você não está tentando a contagem de partição correta de saudação tooguess para todos os usuários com antecedência ou criar um único serviço que é infinitamente escalonável em seu próprio. 
  - Diferentes usuários não têm Olá toohave mesma partição contagem, contagem de réplica, restrições de posicionamento, métricas, carrega padrão, nomes de serviço, configurações de dns ou qualquer Olá outras propriedades especificadas no serviço de saudação ou nível de aplicativo. 
  - Você obtém uma maior segmentação de dados. Cada cliente tem sua própria cópia do serviço de saudação
    - Cada serviço de cliente pode ser configurado de forma diferente e pode ter mais ou menos recursos, com mais ou menos partições ou réplicas, conforme a necessidade baseada na escala esperada.
      - Por exemplo, digamos que Prezado cliente paga camada "Ouro" hello - poderem mais réplicas ou contagem de partição maior e potencialmente recursos dedicados tootheir serviços por meio de capacidades de métricas e aplicativo.
      - Ou eles fornecido informações indicando o número de saudação de contatos precisavam foram "Pequeno" – eles obtém somente algumas partições, ou ainda podem ser inseridos em um pool de serviços compartilhados com outros clientes.
  - Você não estiver executando várias instâncias de serviço ou réplicas enquanto você aguarda para clientes tooshow backup
  - Se um cliente nunca deixa, remova as informações de seu serviço é tão simple quanto com o Gerenciador de saudação excluir esse serviço ou aplicativo que ele criou.

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre os conceitos de malha do serviço, consulte Olá artigos a seguir:

* [Disponibilidade dos serviços de malha do serviço](service-fabric-availability-services.md)
* [Particionando serviços da Malha do Serviço](service-fabric-concepts-partitioning.md)
