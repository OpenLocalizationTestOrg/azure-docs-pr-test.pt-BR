---
title: "Olá aaaPlanning capacidade de cluster do Service Fabric | Microsoft Docs"
description: "Considerações de planejamento de capacidade de cluster do Service Fabric. Níveis de confiabilidade, durabilidade e nodetypes"
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 4c584f4a-cb1f-400c-b61f-1f797f11c982
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: chackdan
ms.openlocfilehash: 83272ce7fefe698eef755cf66493c2874cc3b120
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-cluster-capacity-planning-considerations"></a>Considerações de planejamento de capacidade de cluster do Service Fabric
Para qualquer implantação de produção, o planejamento de capacidade é uma etapa importante. Aqui estão alguns dos itens de saudação que você tenha tooconsider como parte desse processo.

* sua necessidades de cluster toostart out com tipos de número de saudação do nó
* Propriedades de saudação de cada tipo de nó (tamanho, primário, da internet, número de VMs, etc.)
* características de confiabilidade e durabilidade de saudação do cluster de saudação

Vamos examinar rapidamente cada um desses itens.

## <a name="hello-number-of-node-types-your-cluster-needs-toostart-out-with"></a>sua necessidades de cluster toostart out com tipos de número de saudação do nó
Primeiro, é necessário toofigure qual cluster Olá você está criando irá toobe usado para e que tipos de aplicativos que você está planejando toodeploy para este cluster. Se você não estiver claro no propósito de saudação do cluster de saudação, você provavelmente ainda não pronto do processo de planejamento de capacidade de saudação tooenter.

Estabelece o número de saudação de tipos de nós de com que cluster precisa toostart out.  Cada tipo de nó é mapeado tooa conjunto de escala de máquina Virtual. Cada tipo de nó pode ser escalado verticalmente para cima ou para baixo de forma independente, tem conjuntos diferentes de portas abertas e pode ter métricas de capacidade diferente. Portanto decisão de saudação do número de saudação de tipos de nós essencialmente resume toohello considerações a seguir:

* Seu aplicativo tem vários serviços, e qualquer um deles é necessário toobe pública ou voltados à internet? Os aplicativos típicos contêm um serviço de gateway de front-end que recebe entrada de um cliente e um ou mais serviços back-end que se comunicam com serviços de front-end de saudação. Nesse caso, você acaba tendo pelo menos dois tipos de nó.
* Os serviços (que compõem o aplicativo) têm necessidades de infraestrutura diferentes, como maior RAM ou mais ciclos de CPU? Por exemplo, suponhamos que esse aplicativo hello que você deseja toodeploy contém um serviço front-end e um serviço back-end. Olá serviço front-end pode executar em VMs menores (tamanhos de VM como D2) que tem portas abertas toohello internet.  Olá back-end, no entanto, toorun de computação intensiva e necessidades em VMs maior (com tamanhos de VM como D4, D6, D15) que não são internet enfrentados pelo serviço.
  
  Neste exemplo, embora você possa decidir tooput todos os serviços em um tipo de nó de Olá, é recomendável que você coloque-os em um cluster com dois tipos de nó.  Isso permite que propriedades de para cada nó tipo toohave distintos, como conectividade com a internet ou o tamanho da VM. número de saudação de VMs pode ser dimensionado independentemente, e também.  
* Desde que você não pode prever o futuro hello, vá com fatos que você conhece e decidir sobre o número de saudação de tipos de nós que seus aplicativos precisam toostart com. Você sempre pode adicionar ou remover tipos de nós posteriormente. Um cluster do Service Fabric deve ter pelo menos um tipo de nó.

## <a name="hello-properties-of-each-node-type"></a>Propriedades de saudação de cada tipo de nó
Olá **tipo de nó** podem ser vistos como equivalentes tooroles em serviços de nuvem. Tipos de nós definem tamanhos de VM hello, número de saudação de VMs e suas propriedades. Cada tipo de nó definido em um cluster do Service Fabric está configurado como um conjunto de dimensionamento de máquinas virtuais separado. Conjunto de escalas da máquina virtual é um recurso de computação do Azure, você pode usar toodeploy e gerenciar uma coleção de máquinas virtuais como um conjunto. Sendo definidos como conjuntos de dimensionamento de máquinas virtuais distintos, cada tipo de nó pode ser escalado verticalmente ou horizontalmente de forma independente, ter diferentes conjuntos de portas abertas e ter métricas de capacidade diferentes.

Leitura [neste documento](service-fabric-cluster-nodetypes.md) para obter mais detalhes sobre a relação de saudação do conjunto de escalas da máquina Nodetypes toovirtual, como tooRDP em uma das instâncias de hello, abrir novas portas etc.

O cluster pode ter mais de um tipo de nó, mas o tipo de nó primário hello (Olá a primeira alteração que você definir no portal de saudação) deve ter pelo menos cinco VMs para clusters usados para cargas de trabalho de produção (ou pelo menos três VMs para clusters de teste). Se você estiver criando um cluster de saudação usando um modelo do Gerenciador de recursos, em seguida, procure **primário** atributo na definição de tipo de nó de saudação. tipo de nó primário Olá é tipo de nó de saudação onde os serviços do sistema do Service Fabric são colocados.  

### <a name="primary-node-type"></a>Tipo de nó primário
Para um cluster com vários tipos de nó, você precisa toochoose um deles toobe primário. Aqui estão as características de saudação de um tipo de nó primário:

* Olá **tamanho mínimo de VMs** para o tipo de nó primário Olá é determinado pelo Olá **a camada de durabilidade** você escolher. saudação padrão da camada de durabilidade de saudação é Bronze. Role para baixo para obter detalhes sobre qual camada de durabilidade Olá é e valores hello pode demorar.  
* Olá **número mínimo de VMs** para o tipo de nó primário Olá é determinado pelo Olá **camada de confiabilidade** você escolher. saudação padrão da camada de confiabilidade de saudação é prata. Role para baixo para obter detalhes sobre qual camada de confiabilidade Olá é e valores hello pode demorar. 


* Serviços de sistema do Service Fabric Hello (por exemplo, serviço de Gerenciador de Cluster de saudação ou serviço de repositório de imagem) são colocados no tipo de nó primário hello e a confiabilidade de saudação caso e durabilidade de cluster Olá é determinada pela camada de valor e durabilidade de camada de confiabilidade do hello valor selecionado para o tipo de nó primário hello.

![Captura de tela de um cluster com dois tipos de nó ][SystemServices]

### <a name="non-primary-node-type"></a>Tipo de nó não primário
Para um cluster com vários tipos de nós, há um tipo de nó primário e rest Olá deles não primário. Aqui estão as características de saudação de um tipo de nó não primário:

* tamanho mínimo de saudação de VMs para esse tipo de nó é determinado pela camada de durabilidade de saudação que você escolher. saudação padrão da camada de durabilidade de saudação é Bronze. Role para baixo para obter detalhes sobre qual camada de durabilidade Olá é e valores hello pode demorar.  
* número mínimo de saudação de VMs para esse tipo de nó pode ser um. No entanto, você deve escolher esse número com base no número de saudação de réplicas de saudação/serviços de aplicativo que deseja toorun nesse tipo de nó. número de saudação de VMs em um tipo de nó pode ser aumentado após ter implantado o cluster hello.

## <a name="hello-durability-characteristics-of-hello-cluster"></a>características de durabilidade de saudação do cluster de saudação
a camada de durabilidade Olá é usado tooindicate toohello sistema Olá privilégios suas VMs com a infraestrutura do Azure subjacente de saudação. Em tipo de nó primário hello, esse privilégio permite Service Fabric toopause qualquer solicitação de infraestrutura de nível de VM (por exemplo, uma reinicialização da VM, recriação de imagem de VM ou migração de VM) que afetam os requisitos de quorum Olá para serviços do sistema hello e seus serviços com monitoração de estado. Em tipos de nó principal não hello, esse privilégio permite Service Fabric toopause quaisquer solicitações de nível de infraestrutura VM como reinicialização da VM, a nova imagem de VM, a migração de VM etc., que afetam os requisitos de quorum Olá para seus serviços com monitoração de estado em execução.

Este privilégio é expresso em Olá valores a seguir:

* Ouro - infraestrutura Olá trabalhos podem ser pausados por um período de duas horas por UD. A durabilidade ouro pode ser habilitada apenas em skus de VM de nó completo como D15_V2, G5 etc.
* Prata - Olá infraestrutura trabalhos pode ser pausado por um período de 10 minutos por UD e está disponíveis em todas as VMs padrão de núcleo único e acima.
* Bronze - sem privilégios. Esse é o padrão de saudação. Use esse nível de durabilidade somente para Tipos de nós que executam _somente_ cargas de trabalho sem estado. 

> [!WARNING]
> NodeTypes executados com durabilidade Bronze não têm _nenhum privilégio_. Isso significa que trabalhos de infraestrutura que afetam sus cargas de trabalho sem estado não serão interrompidas ou atrasadas. É possível que tais trabalhos ainda possam afetar suas cargas de trabalho, causando tempo de inatividade ou outros problemas. Para qualquer tipo de carga de trabalho de produção, é recomendável a execução com pelo menos o nível Prata. 
> 

Obter o nível de durabilidade toochoose para cada um dos tipos de nós. Você pode escolher um nível de durabilidade de ouro toohave de um tipo de nó ou prata e outros Olá ter Bronze Olá mesmo cluster. **Você deve manter um número mínimo de 5 nós de qualquer tipo de nó que tem uma durabilidade de ouro ou prata**. 

**Vantagens de usar os níveis de durabilidade Ouro ou Prata**
 
1. Reduz o número de saudação de etapas necessárias em uma operação de escala (ou seja, a desativação do nó e remover ServiceFabricNodeState é chamado automaticamente)
2. Reduz o risco de saudação de perda de dados devido a operações de infraestrutura do Azure ou tooa iniciada pelo cliente no local SKU de VM a operação de alteração.
     
**Desvantagens de usar os níveis de durabilidade Ouro ou Prata**
 
1. Implantações tooyour conjunto de escala de máquinas virtuais e outros recursos do Azure relacionados) podem ser atrasados, podem atingir o tempo limite ou podem ser bloqueados inteiramente por problemas no cluster ou no nível de infraestrutura de saudação. 
2. Aumenta Olá inúmeros [eventos de ciclo de vida de réplica](service-fabric-reliable-services-advanced-usage.md#stateful-service-replica-lifecycle ) (por exemplo, trocas primárias) devido tooautomated desativações de nó durante as operações de infraestrutura do Azure.

### <a name="recommendations-on-when-toouse-silver-or-gold-durability-levels"></a>Recomendações sobre quando toouse níveis de durabilidade Prata ou ouro

Use Prata ou ouro durabilidade para nó todos os tipos de monitoração de estado que host serviços você esperar no tooscale (reduzir a contagem de instâncias VM) com frequência, e você prefere que operações de implantação atrasado em favor simplificando essas operações de escala. cenários de expansão de saudação (adicionar instâncias de máquinas virtuais) não são reproduzidos em sua escolha de camada de durabilidade hello, em escala única.

### <a name="operational-recommendations-for-hello-node-type-that-you-have-set-toosilver-or-gold-durability-level"></a>Recomendações operacionais para o nó de saudação tipo que você definiu a durabilidade toosilver ou ouro nível.

1. Manter o cluster e os aplicativos de integridade em todos os momentos e certifique-se de que os aplicativos respondem tooall [eventos de ciclo de vida de réplica de serviço](service-fabric-reliable-services-advanced-usage.md#stateful-service-replica-lifecycle) (como a réplica de compilação está preso) de maneira oportuna.
2. Adotar toomake mais segura de maneiras uma alteração de SKU de VM (escala para cima/baixo): alterando Olá SKU de VM de um conjunto de escala de máquina Virtual é inerentemente uma operação não segura e isso devem ser evitados se possível. Este é o processo de saudação você pode seguir os problemas comuns de tooavoid.
    - **Para não primário nodetypes:** é recomendável que você cria novo conjunto de escala de máquina Virtual, modifique Olá posicionamento restrição tooinclude Olá novo conjunto de escala de máquinas virtuais/nó tipo de serviço e, em seguida, reduzir Olá antigo conjunto de escala de máquinas virtuais too0 de contagem de instância, um nó por vez (Isso é toomake-se de que a remoção de nós de saudação não afetam os confiabilidade de saudação do cluster Olá).
    - **Para nodetype primário Olá:** nossa recomendação é que você não altere o SKU de VM do tipo de nó primário hello. Se Olá razão para novo SKU hello é capacidade, recomendamos adicionar mais instâncias ou se possível, crie um novo cluster. Se você não tem escolha, fazer modificações toohello tooreflect de definição de modelo de conjunto de escala de máquina Virtual Olá SKU de novo. Se seu cluster tem apenas um nodetype, em seguida, certifique-se de que todos os seus aplicativos com monitoração de estado respondam tooall [eventos de ciclo de vida de réplica de serviço](service-fabric-reliable-services-advanced-usage.md#stateful-service-replica-lifecycle) (como a réplica de compilação está preso), de maneira oportuna e que a réplica de serviço recriar duração é menos de cinco minutos (para o nível de durabilidade prata). 


> [!WARNING]
> Olá alterar tamanho da SKU de VM para conjuntos de escala de VM não está em execução, pelo menos, Prata durabilidade não é recomendados. Alterar o Tamanho de SKU da VM é uma operação de infraestrutura no local com destruição de dados. Sem pelo menos um pouco toodelay capacidade ou o monitor dessa alteração, é possível que operação Olá pode causar perda de serviços com monitoração de estado ou outros problemas operacionais imprevistas, mesmo para cargas de trabalho sem monitoração de estado. 
> 
    
3. Mantenha uma contagem mínima de cinco nós para qualquer Conjunto de Dimensionamento de Máquinas Virtuais com MR habilitado
4. Não exclua instâncias de VM aleatórias; sempre reduza verticalmente o recurso Conjunto de Dimensionamento de Máquinas Virtuais. exclusão de saudação aleatórias de instâncias de VM tem o potencial de criação desequilíbrios na instância VM Olá espalhadas por UD e FD. Esse desequilíbrio pode afetar adversamente Olá sistemas capacidade tooproperly o balanceamento de carga entre réplicas de serviço/instâncias de serviço hello.
6. Se usar o dimensionamento automático, em seguida, defina regras de hello, de modo que a escala (remoção de instâncias VM) são feitas somente um nó por vez. Redução de mais de uma instância em um momento não é segura.
7. Se a redução de um tipo de nó primário, você deve nunca reduzi-lo mais do que permite que o nível de confiabilidade hello.


## <a name="hello-reliability-characteristics-of-hello-cluster"></a>características de confiabilidade de saudação do cluster de saudação
Olá camada de confiabilidade é usada número de saudação do tooset de réplicas Olá dos serviços do sistema que você deseja toorun neste cluster no tipo de nó primário hello. Olá mais número Olá de réplicas, hello mais confiável Olá serviços do sistema estejam em seu cluster.  

camada de confiabilidade Olá pode assumir Olá valores a seguir:

* Platinum - execução Olá serviços do sistema com uma contagem de conjunto de réplica de destino de 9
* Ouro - execução Olá serviços do sistema com uma contagem de conjunto de réplica de destino de 7
* Silver - executar Olá serviços do sistema com uma contagem de conjunto de réplica de destino de 5 
* Bronze - execução Olá serviços do sistema com uma contagem de conjunto de réplica de destino de 3

> [!NOTE]
> camada de confiabilidade Olá que você escolher determina o número mínimo de saudação de nós de que seu tipo de nó primário deve ter. 
> 
> 


### <a name="recommendations-for-hello-reliability-tier"></a>Recomendações para a camada de confiabilidade de saudação.

 Quando você aumentar ou diminuir o tamanho de saudação do cluster (soma de saudação de instâncias VM em todos os tipos de nó), você deve atualizar a confiabilidade de saudação do cluster de uma camada tooanother. Isso dispara Olá cluster atualizações necessárias toochange Olá sistema serviços réplica Definir contagem. Aguarde Olá atualização em andamento toocomplete antes de fazer quaisquer outra alterações toohello cluster, como a adição de nós.  Você pode monitorar o progresso de saudação de atualização de saudação no Service Fabric Explorer ou executando [ServiceFabricClusterUpgrade Get](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)

Aqui está a recomendação Olá sobre como escolher o nível de confiabilidade de saudação.

| **Tamanho do cluster** | **Camada de confiabilidade** |
| --- | --- |
| 1 |Não especifique Olá parâmetro da camada de confiabilidade, calcula o sistema Olá |
| 3 |Bronze |
| 5 ou 6|Silver |
| 7 ou 8 |Gold |
| 9 e superior |Platinum |




## <a name="primary-node-type---capacity-guidance"></a>Tipo de nó Primário - Diretrizes de Capacidade

Este é um guia de saudação para o planejamento de capacidade de tipo de nó primário Olá

1. **Número de VM instâncias toorun qualquer carga de trabalho de produção no Azure:** você deve especificar um tamanho de tipo de nó primário mínimo de 5. 
2. **Instâncias de VM toorun cargas de trabalho de teste no Azure** você pode especificar um tamanho de tipo de nó primário mínimo de 1 ou 3. Olá um cluster de nó, é executado com uma configuração especial e, portanto, não há suporte para a escala fora do cluster. um cluster de nó, Hello tem não confiabilidade e, portanto em seu modelo do Gerenciador de recursos, você tooremove ou não especifique que a configuração (não definindo o valor de configuração de saudação não é suficiente). Se você configurar o cluster de um nó de saudação configurar por meio do portal e configuração de saudação é feita automaticamente. Não há suporte para clusters de 1 e 3 nós para executar cargas de trabalho de produção. 
3. **SKU de VM:** tipo de nó primário é onde os serviços do sistema Olá executados, para Olá SKU de VM você escolher para, deve levar em Olá de conta geral pico de carga você planejar tooplace em cluster hello. Aqui está um tooillustrate analogia quero dizer aqui - opinião do tipo de nó primário hello como os "pulmões", é o que fornece dados de tooyour oxigênio e então se cérebro Olá não obtém suficiente oxigênio, seu corpo será prejudicado. 

Desde que as necessidades de capacidade de saudação de um cluster é determinado pela carga de trabalho planejar toorun em cluster hello, não é possível fornecer você com diretrizes qualitativa para sua carga de trabalho específica, mas, aqui é Olá diretrizes amplas toohelp que você a começar

Para cargas de trabalho de produção 


- Olá recomendado que é de SKU de VM D3 padrão ou D3_V2 padrão ou equivalente, com um mínimo de 14 GB de SSD local.
- uso de saudação mínimo com suporte SKU de VM é D1 padrão ou D1_V2 padrão ou equivalente, com um mínimo de 14 GB de SSD local. 
- As SKUs de VM de núcleo parcial como a Standard A0 não têm suporte para cargas de trabalho de produção.
- A SKU Standard A1 não tem suporte para cargas de trabalho de produção por motivos de desempenho.


## <a name="non-primary-node-type---capacity-guidance-for-stateful-workloads"></a>O tipo de nó Não Principal - Diretrizes de Capacidade para cargas de trabalho com monitoração de estado

Este guia é para cargas de trabalho com monitoração de estado usando o Service fabric [coleções confiáveis ou reliable Actors](service-fabric-choose-framework.md) que você está executando no tipo de nó não primário hello.


**Número de instâncias de VM:** para as cargas de trabalho de produção com monitoração de estado, é recomendável que você as execute com uma contagem de réplica mínima e de destino de 5. Isso significa que no estado estável, você fica com uma réplica (de um conjunto de réplicas) em cada domínio de falha e em cada domínio de atualização. conceito de camada de confiabilidade todo Olá para o tipo de nó primário Olá é uma maneira toospecify essa configuração para serviços do sistema. Olá assim mesmo consideração se aplica a serviços com monitoração de estado tooyour também.

Portanto para cargas de trabalho de produção, tamanho do tipo mínimo recomendado não - nó primário Olá for 5, se você estiver executando cargas de trabalho com monitoração de estado nele.


**SKU de VM:** isso é Olá tipo de nó em que estiver executando os serviços do aplicativo, para Olá SKU de VM escolha para ele, deve levar em conta Olá picos de carga você planejar tooplace em cada nó. Olá necessidades de capacidade de nodetype Olá, é determinado pela carga de trabalho que planejar toorun em cluster hello, portanto não é possível fornecer você com diretrizes qualitativa para sua carga de trabalho específica, mas, aqui é Olá diretrizes amplas toohelp que você a começar

Para cargas de trabalho de produção 

- Olá recomendado que é de SKU de VM D3 padrão ou D3_V2 padrão ou equivalente, com um mínimo de 14 GB de SSD local.
- uso de saudação mínimo com suporte SKU de VM é D1 padrão ou D1_V2 padrão ou equivalente, com um mínimo de 14 GB de SSD local. 
- As SKUs de VM de núcleo parcial como a Standard A0 não têm suporte para cargas de trabalho de produção.
- Especificamente, a SKU Standard A1 não tem suporte para cargas de trabalho de produção por motivos de desempenho.


## <a name="non-primary-node-type---capacity-guidance-for-stateless-workloads"></a>O tipo de nó Não Principal - Diretrizes de Capacidade para cargas de trabalho sem monitoração de estado

Este guia de cargas de trabalho sem monitoração de estado que você está executando em Olá não primário nodetype.

**Número de instâncias VM:** para produção as cargas de trabalho sem monitoração de estado, o tamanho do tipo de nó não primário Olá mínima com suporte é 2. Isso permite toorun você duas sem monitoração de estado instâncias de seu aplicativo e permitindo que o serviço toosurvive Olá perda de uma instância de VM. 

> [!NOTE]
> Se o cluster está em execução em uma versão do fabric de serviço menor 5.6, devido a defeito tooa em hello tempo de execução (esse problema é corrigido no 5.6), redução de um tooless de tipo de nó não primário que 5, resulta a ativação não íntegro, até que você chamar a integridade de cluster [ Remover ServiceFabricNodeState cmd](https://docs.microsoft.com/powershell/servicefabric/vlatest/Remove-ServiceFabricNodeState) com o nome de nó apropriado hello. Leia [Sair ou entrar no cluster do Service Fabric](service-fabric-cluster-scale-up-down.md) para obter mais detalhes
> 
>

**SKU de VM:** isso é Olá tipo de nó em que estiver executando os serviços do aplicativo, para Olá SKU de VM escolha para ele, deve levar em conta Olá picos de carga você planejar tooplace em cada nó. Olá necessidades de capacidade de nodetype Olá, é determinado pela carga de trabalho que planejar toorun em cluster hello, portanto não é possível fornecer você com diretrizes qualitativa para sua carga de trabalho específica, mas, aqui é Olá diretrizes amplas toohelp que você a começar

Para cargas de trabalho de produção 


- Olá recomendado que é de SKU de VM D3 padrão ou D3_V2 padrão ou equivalente. 
- uso de saudação mínimo com suporte SKU de VM é D1 padrão ou D1_V2 padrão ou equivalente. 
- As SKUs de VM de núcleo parcial como a Standard A0 não têm suporte para cargas de trabalho de produção.
- A SKU Standard A1 não tem suporte para cargas de trabalho de produção por motivos de desempenho.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="next-steps"></a>Próximas etapas
Depois de concluir o planejamento de capacidade e configurar um cluster, leia Olá seguinte:

* [Segurança do Cluster do Service Fabric](service-fabric-cluster-security.md)
* [Introdução ao modelo de Integridade do Service Fabric](service-fabric-health-introduction.md)
* [Relação de escala de máquina tooVirtual Nodetypes definida](service-fabric-cluster-nodetypes.md)

<!--Image references-->
[SystemServices]: ./media/service-fabric-cluster-capacity/SystemServices.png
