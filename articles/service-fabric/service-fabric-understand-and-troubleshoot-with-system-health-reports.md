---
title: "Solucionar problemas com relatórios de integridade do sistema | Microsoft Docs"
description: "Descreve os relatórios de integridade enviados por componentes do Service Fabric do Azure e seu uso para solucionar problemas de cluster ou de aplicativos."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: 52574ea7-eb37-47e0-a20a-101539177625
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: oanapl
ms.openlocfilehash: 54e20146b2f1e0ca6153b66319be70c6f7c2fb59
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="use-system-health-reports-to-troubleshoot"></a>Usar relatórios de integridade do sistema para solução de problemas
Os componentes do Service Fabric apresentam relatórios de integridade prontos para uso sobre todas as entidades. O [repositório de integridade](service-fabric-health-introduction.md#health-store) cria e exclui entidades baseado nos relatórios do sistema. Ele também os organiza em uma hierarquia que captura interações de entidade.

> [!NOTE]
> Leia mais sobre o [Modelo de Integridade do Service Fabric](service-fabric-health-introduction.md)para entender os conceitos relacionados à integridade.
> 
> 

Os relatórios de integridade do sistema fornecem visibilidade da funcionalidade do cluster e de aplicativos e sinalizam problemas por meio da integridade. Para aplicativos e serviços, os relatórios de integridade do sistema verificam se as entidades são implementadas e estão se comportando corretamente da perspectiva do Service Fabric. Os relatórios não fornecem monitoramento de integridade da lógica de negócios do serviço nem detecção de processos travados. Os serviços de usuário podem enriquecer os dados de integridade com informações específicas à respectiva lógica.

> [!NOTE]
> Os relatórios de integridade dos watchdogs ficam visíveis somente *depois* que os componentes do sistema criam uma entidade. Quando uma entidade é excluída, o repositório de integridade exclui automaticamente todos os relatórios de integridade associados a ela. O mesmo acontece quando uma nova instância da entidade é criada (por exemplo, uma nova instância de réplica do serviço com estado persistente é criada). Todos os relatórios associados à instância antiga são excluídos e removidos do repositório.
> 
> 

Os relatórios de componentes do sistema são identificados por sua origem, que começa com o prefixo "**System.**" prefixo. Os watchdogs não podem usar o mesmo prefixo para suas origens, pois os relatórios com parâmetros inválidos são rejeitados.
Vamos examinar alguns relatórios do sistema para entender o que os dispara e como corrigir possíveis problemas que eles representam.

> [!NOTE]
> O Service Fabric continua adicionando relatórios sobre condições de interesse que melhoram a visibilidade do que está acontecendo no cluster e no aplicativo. Os relatórios existentes também podem ser aprimorados com mais detalhes para ajudar a solucionar o problema mais rapidamente.
> 
> 

## <a name="cluster-system-health-reports"></a>Relatórios de integridade do sistema de cluster
A entidade de integridade do cluster é criada automaticamente no repositório de integridade. Se tudo funcionar corretamente, ele não terá um relatório do sistema.

### <a name="neighborhood-loss"></a>Perda de ambiente
**System.Federation** relata um erro quando detecta uma perda de ambiente. O relatório tem origem em nós individuais e a ID do nó é incluída no nome da propriedade. Caso haja uma perda de ambiente em todo o anel do Service Fabric, geralmente podemos esperar dois eventos (ambos os lados da lacuna serão relatados). Se houver mais perdas de ambiente, haverá mais eventos.

O relatório especifica o tempo limite de concessão global como o tempo de vida útil. O relatório é enviado novamente a cada metade da duração do tempo de vida útil, desde que a condição permaneça ativa. O evento é removido automaticamente quando expira. Remover o comportamento expirado garante que o relatório será removido do repositório de integridade corretamente, mesmo que o nó de relatório esteja inativo.

* **SourceId**: System.Federation
* **Propriedade**: começa com **Ambiente** e inclui informações sobre o nó
* **Próximas etapas**: investigue por que o ambiente foi perdido (por exemplo, verifique a comunicação entre os nós do cluster).

## <a name="node-system-health-reports"></a>Relatórios de integridade do sistema de nó
**System.FM**, que representa o serviço Gerenciador de Failover, é a autoridade que gerencia informações sobre nós de cluster. Cada nó deve ter um relatório de System.FM mostrando seu estado. As entidades de nó são removidas quando o estado do nó é removido (veja [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).

### <a name="node-updown"></a>Nó ativo/inativo
System.FM relata OK quando o nó ingressa no anel (está em execução). Ele relata um erro quando o nó é removido do anel (ele está desativado, seja para atualização ou simplesmente porque falhou). A hierarquia de integridade criada pelo repositório de integridade age nas entidades implantadas em correlação com relatórios de nó do System.FM. Ela considera o nó como um pai virtual de todas as entidades implantadas. As entidades implantadas nesse nó serão expostas por meio de consultas se o nó for reportado como ativo pelo System.FM, com a mesma instância que aquela associada às entidades. Quando System.FM relata o nó inativo ou reiniciado (nova instância), o repositório de integridade remove automaticamente as entidades implantadas que podem existir apenas no nó inativo ou na instância anterior do nó.

* **SourceId**: System.FM
* **Propriedade**: Estado
* **Próximas etapas**: se o nó estiver inativo para uma atualização, ele deverá aparecer novamente depois que for atualizado. Nesse caso, o estado de integridade deve ser alternado de volta para OK. Se o nó não voltar ou falhar, será preciso investigar mais.

O exemplo a seguir mostra o evento System.FM com estado de integridade OK para o nó ativo:

```powershell
PS C:\> Get-ServiceFabricNodeHealth  _Node_0

NodeName              : _Node_0
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 8
                        SentAt                : 7/14/2017 4:54:51 PM
                        ReceivedAt            : 7/14/2017 4:55:14 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```


### <a name="certificate-expiration"></a>Expiração de certificado
**System.FabricNode** relata um aviso quando os certificados usados pelo nó estão prestes a expirar. Há três certificados por nó: **Certificate_cluster**, **Certificate_server** e **Certificate_default_client**. Quando falta pelo menos duas semanas para expirar, o estado de integridade do relatório é OK. Quando a expiração é dentro de duas semanas, o tipo de relatório é um aviso. O tempo de vida útil desses eventos é infinito; eles são removidos quando um nó deixa o cluster.

* **SourceId**: System.FabricNode
* **Propriedade**: começa com **Certificate** e contém mais informações sobre o tipo de certificado
* **Próximas etapas**: atualize os certificados se eles estiverem prestes a expirar.

### <a name="load-capacity-violation"></a>Violação da capacidade de carga
O Service Fabric Load Balancer relata um aviso quando detecta uma violação da capacidade do nó.

* **SourceId**: System.PLB
* **Propriedade**: começa com **Capacity**
* **Próximas etapas**: verifique as métricas fornecidas e exiba a capacidade atual do nó.

## <a name="application-system-health-reports"></a>Relatórios de integridade do sistema de aplicativo
**System.CM**, que representa o serviço do Gerenciador de Cluster, é a autoridade que gerencia as informações sobre um aplicativo.

### <a name="state"></a>Estado
System.CM relata OK quando o aplicativo é criado ou atualizado. Ele informa ao repositório de integridade quando o aplicativo é excluído para que este possa ser removido do repositório.

* **SourceId**: System.CM
* **Propriedade**: Estado
* **Próximas etapas**: se o aplicativo tiver sido criado ou atualizado, ele deverá incluir o relatório de integridade do Gerenciador de Cluster. Caso contrário, verifique o estado do aplicativo emitindo uma consulta (por exemplo, o cmdlet **Get-ServiceFabricApplication -ApplicationName *applicationName*** do PowerShell).

O exemplo a seguir mostra o evento de estado no aplicativo **fabric:/WordCount** :

```powershell
PS C:\> Get-ServiceFabricApplicationHealth fabric:/WordCount -ServicesFilter None -DeployedApplicationsFilter None -ExcludeHealthStatistics

ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Ok
ServiceHealthStates             : None
DeployedApplicationHealthStates : None
HealthEvents                    : 
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 282
                                  SentAt                : 7/13/2017 5:57:05 PM
                                  ReceivedAt            : 7/14/2017 4:55:10 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 7/13/2017 5:57:05 PM, LastWarning = 1/1/0001 12:00:00 AM
```

## <a name="service-system-health-reports"></a>Relatórios de integridade do sistema de serviço
**System.FM**, que representa o serviço do Gerenciador de Failover, é a autoridade que gerencia as informações sobre serviços.

### <a name="state"></a>Estado
System.FM relata OK quando o serviço é criado. Ele exclui a entidade do repositório de integridade quando o serviço é excluído.

* **SourceId**: System.FM
* **Propriedade**: Estado

O exemplo a seguir mostra o evento de estado no serviço **fabric:/WordCount/WordCountWebService**:

```powershell
PS C:\> Get-ServiceFabricServiceHealth fabric:/WordCount/WordCountWebService -ExcludeHealthStatistics


ServiceName           : fabric:/WordCount/WordCountWebService
AggregatedHealthState : Ok
PartitionHealthStates : 
                        PartitionId           : 8bbcd03a-3a53-47ec-a5f1-9b77f73c53b2
                        AggregatedHealthState : Ok
                        
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 14
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/14/2017 4:55:10 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="service-correlation-error"></a>Erro de correlação de serviço
**System.PLB** relata um erro ao detectar que a atualização de um serviço a ser correlacionado com outro serviço cria uma cadeia de afinidade. O relatório é limpo quando a atualização é bem-sucedida.

* **SourceId**: System.PLB
* **Propriedade**: ServiceDescription
* **Próximas etapas**: verifique as descrições de serviços correlacionadas.

## <a name="partition-system-health-reports"></a>Relatórios de integridade do sistema de partição
**System.FM**, que representa o serviço do Gerenciador de Failover, é a autoridade que gerencia as informações sobre partições de serviço.

### <a name="state"></a>Estado
System.FM relata OK quando a partição é criada e está íntegra. Ele exclui a entidade do repositório de integridade quando a partição é excluída.

Se a partição estiver abaixo da contagem mínima de réplica, ela relatará um erro. Se a partição não estiver abaixo da contagem mínima de réplica, mas estiver abaixo da contagem de réplica de destino, ele relatará um aviso. Se a partição estiver na perda de quórum, o System.FM relatará um erro.

Outros eventos importantes incluem avisos quando a reconfiguração demorar mais que o esperado e quando a compilação demorar mais que o esperado. Os tempos esperados para compilação ou reconfiguração podem ser configurados baseados nos cenários de serviço. Por exemplo, se um serviço tem um terabyte de estado, como o Banco de Dados SQL, criá-lo demora mais do que demoraria para um serviço com uma pequena quantidade de estado.

* **SourceId**: System.FM
* **Propriedade**: Estado
* **Próximas etapas**: se o estado de integridade não está OK, é possível que algumas réplicas não tenham sido criadas, abertas ou promovidas para o primário ou secundário corretamente. Em muitos casos, a causa raiz é um bug de serviço na implementação da função de abertura ou de alteração.

O exemplo a seguir mostra uma partição íntegra:

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountWebService | Get-ServiceFabricPartitionHealth -ExcludeHealthStatistics -ReplicasFilter None

PartitionId           : 8bbcd03a-3a53-47ec-a5f1-9b77f73c53b2
AggregatedHealthState : Ok
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 70
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/14/2017 4:55:10 PM
                        TTL                   : Infinite
                        Description           : Partition is healthy.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

O exemplo a seguir mostra a integridade de uma partição que está abaixo da contagem de réplica de destino. A etapa seguinte é obter a descrição da partição, que mostra como ela é configurada: **MinReplicaSetSize** é três e **TargetReplicaSetSize** é sete. Em seguida, obtenha o número de nós no cluster: cinco. Nesse caso, portanto, duas réplicas não podem ser colocadas porque o número de réplicas de destino é maior do que o número de nós disponíveis.

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth -ReplicasFilter None -ExcludeHealthStatistics


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 123
                        SentAt                : 7/14/2017 4:55:39 PM
                        ReceivedAt            : 7/14/2017 4:55:44 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        fabric:/WordCount/WordCountService 7 2 af2e3e44-a8f8-45ac-9f31-4093eb897600
                          N/S RD _Node_2 Up 131444422260002646
                          N/S RD _Node_4 Up 131444422293113678
                          N/S RD _Node_3 Up 131444422293113679
                          N/S RD _Node_1 Up 131444422293118720
                          N/P RD _Node_0 Up 131444422293118721
                          (Showing 5 out of 5 replicas. Total available replicas: 5.)
                        
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/14/2017 4:55:44 PM, LastOk = 1/1/0001 12:00:00 AM
                        
                        SourceId              : System.PLB
                        Property              : ServiceReplicaUnplacedHealth_Secondary_af2e3e44-a8f8-45ac-9f31-4093eb897600
                        HealthState           : Warning
                        SequenceNumber        : 131445250939703027
                        SentAt                : 7/14/2017 4:58:13 PM
                        ReceivedAt            : 7/14/2017 4:58:14 PM
                        TTL                   : 00:01:05
                        Description           : The Load Balancer was unable to find a placement for one or more of the Service's Replicas:
                        Secondary replica could not be placed due to the following constraints and properties:  
                        TargetReplicaSetSize: 7
                        Placement Constraint: N/A
                        Parent Service: N/A
                        
                        Constraint Elimination Sequence:
                        Existing Secondary Replicas eliminated 4 possible node(s) for placement -- 1/5 node(s) remain.
                        Existing Primary Replica eliminated 1 possible node(s) for placement -- 0/5 node(s) remain.
                        
                        Nodes Eliminated By Constraints:
                        
                        Existing Secondary Replicas -- Nodes with Partition's Existing Secondary Replicas/Instances:
                        --
                        FaultDomain:fd:/4 NodeName:_Node_4 NodeType:NodeType4 UpgradeDomain:4 UpgradeDomain: ud:/4 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/3 NodeName:_Node_3 NodeType:NodeType3 UpgradeDomain:3 UpgradeDomain: ud:/3 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/2 NodeName:_Node_2 NodeType:NodeType2 UpgradeDomain:2 UpgradeDomain: ud:/2 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/1 NodeName:_Node_1 NodeType:NodeType1 UpgradeDomain:1 UpgradeDomain: ud:/1 Deactivation Intent/Status: None/None
                        
                        Existing Primary Replica -- Nodes with Partition's Existing Primary Replica or Secondary Replicas:
                        --
                        FaultDomain:fd:/0 NodeName:_Node_0 NodeType:NodeType0 UpgradeDomain:0 UpgradeDomain: ud:/0 Deactivation Intent/Status: None/None
                        
                        
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/14/2017 4:56:14 PM, LastOk = 1/1/0001 12:00:00 AM

PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | select MinReplicaSetSize,TargetReplicaSetSize

MinReplicaSetSize TargetReplicaSetSize
----------------- --------------------
                2                    7                        

PS C:\> @(Get-ServiceFabricNode).Count
5
```

### <a name="replica-constraint-violation"></a>Violação da restrição de réplica
**System.PLB** relata um aviso se detectar uma violação de restrição de réplica e não puder posicionar todas as réplicas da partição. Os detalhes do relatório mostram quais restrições e propriedades impedem o posicionamento da réplica.

* **SourceId**: System.PLB
* **Propriedade**: começa com **ReplicaConstraintViolation**

## <a name="replica-system-health-reports"></a>Relatórios de integridade do sistema de réplica
**System.RA**, que representa o componente do agente de reconfiguração, é a autoridade do estado da réplica.

### <a name="state"></a>Estado
**System.RA** relata OK quando a réplica é criada.

* **SourceId**: System.RA
* **Propriedade**: Estado

O exemplo a seguir mostra uma réplica íntegra:

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth

PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422293118721
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131445248920273536
                        SentAt                : 7/14/2017 4:54:52 PM
                        ReceivedAt            : 7/14/2017 4:55:13 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_0
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/14/2017 4:55:13 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="replica-open-status"></a>Status aberto da réplica
A descrição desse relatório de integridade contém a hora de início (UTC) da chamada à API invocada.

**System.RA** relatará um aviso se a réplica aberta demorar mais que o período configurado (padrão: 30 minutos). Quando a API afeta a disponibilidade do serviço, o relatório é emitido muito mais rapidamente (intervalo configurável, padrão de 30 segundos). O tempo medido inclui o tempo necessário para abrir o replicador e abrir o serviço. A propriedade muda para OK quando a abertura é concluída.

* **SourceId**: System.RA
* **Propriedade**: **ReplicaOpenStatus**
* **Próximas etapas**: se o estado de integridade não estiver OK, investigue o motivo pelo qual a réplica aberta demora mais que o esperado.

### <a name="slow-service-api-call"></a>Chamada à API para serviço lento
**System.RAP** e **System.Replicator** relatarão um aviso se uma chamada para o código do serviço do usuário demorar mais que o tempo configurado. Esse status é removido quando a chamada é concluída.

* **SourceId**: System.RAP ou System.Replicator
* **Propriedade**: o nome da API lenta. A descrição fornece mais detalhes sobre o tempo em que a API esteve pendente.
* **Próximas etapas**: investigue o motivo pelo qual a chamada demora mais que o esperado.

O exemplo a seguir mostra uma partição na perda de quórum e as etapas de investigação realizadas para entender o motivo. Uma das réplicas tem o estado de integridade de aviso; portanto, obtemos sua integridade. Ele mostra que a operação do serviço demora mais que o esperado, um evento relatado por System.RAP. Depois que a informação é recebida, a próxima etapa será examinar o código de serviço e investigá-lo. Nesse caso, a implementação de **RunAsync** do serviço com estado gera uma exceção sem tratamento. As réplicas são recicladas, de modo que você não pode ver nenhuma réplica no estado de aviso. Você pode tentar novamente obter o estado de integridade e examinar as diferenças na ID de réplica. Em alguns casos, as novas tentativas podem lhe dar pistas.

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/HelloWorldStatefulApplication/HelloWorldStateful | Get-ServiceFabricPartitionHealth -ExcludeHealthStatistics

PartitionId           : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
AggregatedHealthState : Error
UnhealthyEvaluations  :
                        Error event: SourceId='System.FM', Property='State'.

ReplicaHealthStates   :
                        ReplicaId             : 130743748372546446
                        AggregatedHealthState : Ok

                        ReplicaId             : 130743746168084332
                        AggregatedHealthState : Ok

                        ReplicaId             : 130743746195428808
                        AggregatedHealthState : Warning

                        ReplicaId             : 130743746195428807
                        AggregatedHealthState : Ok

HealthEvents          :
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Error
                        SequenceNumber        : 182
                        SentAt                : 4/24/2015 7:00:17 PM
                        ReceivedAt            : 4/24/2015 7:00:31 PM
                        TTL                   : Infinite
                        Description           : Partition is in quorum loss.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Warning->Error = 4/24/2015 6:51:31 PM

PS C:\> Get-ServiceFabricPartition fabric:/HelloWorldStatefulApplication/HelloWorldStateful

PartitionId            : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
PartitionKind          : Int64Range
PartitionLowKey        : -9223372036854775808
PartitionHighKey       : 9223372036854775807
PartitionStatus        : InQuorumLoss
LastQuorumLossDuration : 00:00:13
MinReplicaSetSize      : 3
TargetReplicaSetSize   : 3
HealthState            : Error
DataLossNumber         : 130743746152927699
ConfigurationNumber    : 227633266688

PS C:\> Get-ServiceFabricReplica 72a0fb3e-53ec-44f2-9983-2f272aca3e38 130743746195428808

ReplicaId           : 130743746195428808
ReplicaAddress      : PartitionId: 72a0fb3e-53ec-44f2-9983-2f272aca3e38, ReplicaId: 130743746195428808
ReplicaRole         : Primary
NodeName            : Node.3
ReplicaStatus       : Ready
LastInBuildDuration : 00:00:01
HealthState         : Warning

PS C:\> Get-ServiceFabricReplicaHealth 72a0fb3e-53ec-44f2-9983-2f272aca3e38 130743746195428808

PartitionId           : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
ReplicaId             : 130743746195428808
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.RAP', Property='ServiceOpenOperationDuration', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 130743756170185892
                        SentAt                : 4/24/2015 7:00:17 PM
                        ReceivedAt            : 4/24/2015 7:00:33 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/24/2015 7:00:33 PM

                        SourceId              : System.RAP
                        Property              : ServiceOpenOperationDuration
                        HealthState           : Warning
                        SequenceNumber        : 130743756399407044
                        SentAt                : 4/24/2015 7:00:39 PM
                        ReceivedAt            : 4/24/2015 7:00:59 PM
                        TTL                   : Infinite
                        Description           : Start Time (UTC): 2015-04-24 19:00:17.019
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Warning = 4/24/2015 7:00:59 PM
```

Ao iniciar o aplicativo com defeito no depurador, as janelas Eventos de Diagnóstico mostram a exceção lançada por RunAsync:

![Eventos de diagnóstico do Visual Studio 2015: falha de RunAsync em fabric:/HelloWorldStatefulApplication.][1]

Eventos de diagnóstico do Visual Studio 2015: falha de RunAsync em **fabric:/HelloWorldStatefulApplication**.

[1]: ./media/service-fabric-understand-and-troubleshoot-with-system-health-reports/servicefabric-health-vs-runasync-exception.png


### <a name="replication-queue-full"></a>Fila de replicação cheia
**System.Replicator** relata um aviso quando a fila de replicação está cheia. Na réplica primária, a fila de replicação normalmente fica cheia porque uma ou mais réplicas secundárias são lentas confirmar as operações. No local secundário, isso geralmente acontece quando o serviço está lento para aplicar as operações. O aviso será removido quando a fila não estiver mais cheia.

* **SourceId**: System.Replicator
* **Propriedade**: **PrimaryReplicationQueueStatus** ou **SecondaryReplicationQueueStatus**, dependendo da função da réplica

### <a name="slow-naming-operations"></a>Operações de Nomeação lentas
**System.NamingService** relata a integridade na réplica primária quando uma operação de nomenclatura demora mais do que o aceitável. Exemplos de operações de Nomeação: [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) ou [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync). Mais métodos podem ser encontrados em FabricClient, por exemplo, em [métodos de gerenciamento do serviço](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) ou [métodos de gerenciamento de propriedade](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).

> [!NOTE]
> O serviço de nomenclatura resolve nomes de serviço para um local no cluster e permite aos usuários gerenciar propriedades e nomes de serviço. É um serviço persistentes particionado pelo Service Fabric. Uma das partições representa o proprietário da autoridade, que contém metadados sobre todos os nomes e serviços do Service Fabric. Os nomes do Service Fabric são mapeados para partições diferentes, chamadas de partições de Proprietário de Nome, assim, o serviço é extensível. Leia mais sobre o [Serviço de nomeação](service-fabric-architecture.md).
> 
> 

Quando uma operação de nomeação leva mais tempo do que o esperado, a operação é sinalizada com um relatório de Aviso na *réplica primária da partição de serviço de nomeação que atende à operação*. Se a operação for concluída com êxito, o Aviso será limpo. Se a operação for concluída com um erro, o relatório de integridade incluirá detalhes sobre o erro.

* **SourceId**: System.NamingService
* **Propriedade**: começa com o prefixo **Duration_** e identifica a operação lenta e o nome do Service Fabric em que a operação é aplicada. Por exemplo, se a criação de um serviço em name fabric: /MyApp/MyService levar muito tempo, a propriedade será Duration_AOCreateService.fabric:/MyApp/MyService. AO aponta para a função da partição de nomeação para esse nome e a operação.
* **Próximas etapas**: verifique por que a operação de nomeação falha. Cada operação pode ter causas raiz diferentes. Por exemplo, a exclusão de serviço pode estar bloqueado em um nó porque o host do aplicativo falha em um nó devido a um bug de usuário no código de serviço.

O exemplo a seguir mostra uma operação de criação de serviço. A operação demorou mais do que a duração configurada. AO tenta novamente e envia o trabalho para NO. NO concluiu a última operação com Tempo limite. Nesse caso, a mesma réplica é primária para as funções AO e NO.

```powershell
PartitionId           : 00000000-0000-0000-0000-000000001000
ReplicaId             : 131064359253133577
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.NamingService', Property='Duration_AOCreateService.fabric:/MyApp/MyService', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131064359308715535
                        SentAt                : 4/29/2016 8:38:50 PM
                        ReceivedAt            : 4/29/2016 8:39:08 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 4/29/2016 8:39:08 PM, LastWarning = 1/1/0001 12:00:00 AM

                        SourceId              : System.NamingService
                        Property              : Duration_AOCreateService.fabric:/MyApp/MyService
                        HealthState           : Warning
                        SequenceNumber        : 131064359526778775
                        SentAt                : 4/29/2016 8:39:12 PM
                        ReceivedAt            : 4/29/2016 8:39:38 PM
                        TTL                   : 00:05:00
                        Description           : The AOCreateService started at 2016-04-29 20:39:08.677 is taking longer than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM

                        SourceId              : System.NamingService
                        Property              : Duration_NOCreateService.fabric:/MyApp/MyService
                        HealthState           : Warning
                        SequenceNumber        : 131064360657607311
                        SentAt                : 4/29/2016 8:41:05 PM
                        ReceivedAt            : 4/29/2016 8:41:08 PM
                        TTL                   : 00:00:15
                        Description           : The NOCreateService started at 2016-04-29 20:39:08.689 completed with FABRIC_E_TIMEOUT in more than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM
```

## <a name="deployedapplication-system-health-reports"></a>Relatórios de integridade do sistema DeployedApplication
**System.Hosting** é a autoridade nas entidades implantadas.

### <a name="activation"></a>Ativação
System.Hosting relata OK quando um aplicativo é ativado com êxito no nó. Caso contrário, ele relata um erro.

* **SourceId**: System.Hosting
* **Propriedade**: ativação, incluindo a versão de distribuição
* **Próximas etapas**: se o aplicativo não estiver íntegro, investigue o motivo pelo qual a ativação falhou.

O exemplo a seguir mostra uma ativação bem-sucedida:

```powershell
PS C:\> Get-ServiceFabricDeployedApplicationHealth -NodeName _Node_1 -ApplicationName fabric:/WordCount -ExcludeHealthStatistics

ApplicationName                    : fabric:/WordCount
NodeName                           : _Node_1
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates : 
                                     ServiceManifestName   : WordCountServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_1
                                     AggregatedHealthState : Ok
                                     
HealthEvents                       : 
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 131445249083836329
                                     SentAt                : 7/14/2017 4:55:08 PM
                                     ReceivedAt            : 7/14/2017 4:55:14 PM
                                     TTL                   : Infinite
                                     Description           : The application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a>Baixar
**System.Hosting** relatará um erro se o download do pacote de aplicativos falhar.

* **SourceId**: System.Hosting
* **Propriedade**: **Download:*RolloutVersion***
* **Próximas etapas**: investigue o motivo pelo qual o download falhou no nó.

## <a name="deployedservicepackage-system-health-reports"></a>Relatórios de integridade do sistema DeployedServicePackage
**System.Hosting** é a autoridade nas entidades implantadas.

### <a name="service-package-activation"></a>Ativação do pacote de serviço
System.Hosting relatará OK se a ativação do pacote de serviço no nó for bem-sucedida. Caso contrário, ele relata um erro.

* **SourceId**: System.Hosting
* **Propriedade**: ativação
* **Próximas etapas**: investigue o motivo pelo qual a ativação falhou.

### <a name="code-package-activation"></a>Ativação do pacote de códigos
**System.Hosting** relatará OK para cada pacote de códigos se a ativação for bem-sucedida. Se houver falha na ativação, ele relatará um aviso conforme configurado. Se **CodePackage** falhar em ativar ou terminar com um erro maior que o **CodePackageHealthErrorThreshold** configurado, a hospedagem relatará um erro. Se um pacote de serviço contiver vários pacotes de código, um relatório de ativação será gerado para cada um.

* **SourceId**: System.Hosting
* **Propriedade**: usa o prefixo **CodePackageActivation** e contém o nome do pacote de códigos e o ponto de entrada como **CodePackageActivation:*CodePackageName*:*SetupEntryPoint/EntryPoint*** (por exemplo, **CodePackageActivation:Code:SetupEntryPoint**)

### <a name="service-type-registration"></a>Registro do tipo de serviço
**System.Hosting** relatará OK se o tipo de serviço for registrado com êxito. Ele relatará um erro se o registro não foi feito pontualmente (conforme configurado usando **ServiceTypeRegistrationTimeout**). Se o tempo de execução estiver fechado, o tipo de serviço não estará registrado no nó e Hospedagem relatará um aviso.

* **SourceId**: System.Hosting
* **Propriedade**: usa o prefixo **ServiceTypeRegistration** e contém o nome do tipo de serviço (por exemplo, **ServiceTypeRegistration:FileStoreServiceType**)

O exemplo a seguir mostra um pacote de serviço íntegro implantado:

```powershell
PS C:\> Get-ServiceFabricDeployedServicePackageHealth -NodeName _Node_1 -ApplicationName fabric:/WordCount -ServiceManifestName WordCountServicePkg


ApplicationName            : fabric:/WordCount
ServiceManifestName        : WordCountServicePkg
ServicePackageActivationId : 
NodeName                   : _Node_1
AggregatedHealthState      : Ok
HealthEvents               : 
                             SourceId              : System.Hosting
                             Property              : Activation
                             HealthState           : Ok
                             SequenceNumber        : 131445249084026346
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : The ServicePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : CodePackageActivation:Code:EntryPoint
                             HealthState           : Ok
                             SequenceNumber        : 131445249084306362
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : The CodePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : ServiceTypeRegistration:WordCountServiceType
                             HealthState           : Ok
                             SequenceNumber        : 131445249088096842
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : The ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a>Baixar
**System.Hosting** relatará um erro se o download do pacote de serviço falhar.

* **SourceId**: System.Hosting
* **Propriedade**: **Download:*RolloutVersion***
* **Próximas etapas**: investigue o motivo pelo qual o download falhou no nó.

### <a name="upgrade-validation"></a>Validação da atualização
**System.Hosting** relatará um erro se a validação durante a atualização falhar ou se a atualização falhar no nó.

* **SourceId**: System.Hosting
* **Propriedade**: usa o prefixo **FabricUpgradeValidation** e contém a versão de atualização
* **Descrição**: aponta para o erro encontrado

## <a name="next-steps"></a>Próximas etapas
[Como exibir relatórios de integridade do Service Fabric](service-fabric-view-entities-aggregated-health.md)

[Como relatar e verificar a integridade do serviço](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[Monitorar e diagnosticar serviços localmente](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Atualização de aplicativos do Service Fabric](service-fabric-application-upgrade.md)

