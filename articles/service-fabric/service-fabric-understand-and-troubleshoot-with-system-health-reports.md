---
title: "aaaTroubleshoot com relatórios de integridade do sistema | Microsoft Docs"
description: "Descreve os relatórios de integridade Olá enviados pelos componentes do Azure Service Fabric e seu uso para solução de problemas de cluster ou problemas de aplicativos."
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
ms.openlocfilehash: c77a6cdd0440ce5d354cd8760f40151f674a3529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-system-health-reports-tootroubleshoot"></a>Usar tootroubleshoot de relatórios de integridade do sistema
Relatório do Azure Service Fabric componentes imediato saudação em todas as entidades no cluster hello. Olá [repositório de integridade](service-fabric-health-introduction.md#health-store) cria e exclui entidades com base em relatórios de saudação do sistema. Ele também os organiza em uma hierarquia que captura interações de entidade.

> [!NOTE]
> conceitos relacionados à integridade toounderstand, leia mais em [modelo de integridade da malha do serviço](service-fabric-health-introduction.md).
> 
> 

Os relatórios de integridade do sistema fornecem visibilidade da funcionalidade do cluster e de aplicativos e sinalizam problemas por meio da integridade. Para aplicativos e serviços, relatórios de integridade do sistema, verifique se que entidades foram implementadas e estão funcionando corretamente da saudação perspectiva do Service Fabric. relatórios de saudação não fornecem nenhum monitoramento de integridade de lógica de negócios de saudação do serviço hello ou detecção de processos travados. Serviços de usuário podem enriquecer os dados de integridade de saudação com lógica de tootheir específicos de informações.

> [!NOTE]
> Relatórios de integridade watchdogs são visíveis apenas *depois* componentes do sistema Olá criam uma entidade. Quando uma entidade é excluída, o repositório de integridade Olá exclui automaticamente todos os relatórios de integridade associados a ele. Olá mesmo é verdadeiro quando é criada uma nova instância da entidade de saudação (por exemplo, uma nova instância de réplica com monitoração de estado de serviço persistente é criada). Todos os relatórios associados a instância antiga Olá são excluídos e limpos do repositório de saudação.
> 
> 

Olá relatórios de componente do sistema são identificados pela origem hello, que inicia com hello "**System.**" prefixo. Watchdogs não podem usar o hello mesmo prefixo para suas fontes, como relatórios com parâmetros inválidos são rejeitados.
Vamos examinar alguns relatórios toounderstand que faz com que elas e como toocorrect Olá possíveis problemas que eles representam.

> [!NOTE]
> Service Fabric continua tooadd relatórios sobre as condições de interesse que melhorar a visibilidade sobre o que está acontecendo no aplicativo e o cluster de saudação. Os relatórios existentes também podem ser aprimorados com mais detalhes toohelp solucionar problema hello mais rapidamente.
> 
> 

## <a name="cluster-system-health-reports"></a>Relatórios de integridade do sistema de cluster
entidade de integridade do cluster Olá é criada automaticamente no repositório de integridade de saudação. Se tudo funcionar corretamente, ele não terá um relatório do sistema.

### <a name="neighborhood-loss"></a>Perda de ambiente
**System.Federation** relata um erro quando detecta uma perda de ambiente. relatório de saudação for de nós individuais e Olá a ID do nó está incluída no nome da propriedade hello. Se um ambiente é perdido no anel de malha do serviço inteiro hello, normalmente, haverá dois eventos (ambos os lados do relatório de intervalo de saudação). Se houver mais perdas de ambiente, haverá mais eventos.

relatório de Olá Especifica o tempo limite de concessão global hello como tempo de saudação toolive. relatório de saudação é reenviado cada metade da duração de tempo de vida de saudação de como condição Olá permanece ativa. evento de saudação é removido automaticamente quando ela expirar. Remova ao comportamento expirado garante que relatório Olá é limpos do repositório de integridade Olá corretamente, mesmo se o nó reporting hello está inativo.

* **SourceId**: System.Federation
* **Propriedade**: começa com **Ambiente** e inclui informações sobre o nó
* **Próximas etapas**: investigar por que o ambiente de saudação for perdido (por exemplo, verificar Olá comunicação entre nós de cluster).

## <a name="node-system-health-reports"></a>Relatórios de integridade do sistema de nó
**System.FM**, que representa o serviço de Gerenciador de Failover hello, Olá autoridade que gerencia informações sobre nós de cluster. Cada nó deve ter um relatório de System.FM mostrando seu estado. entidades de nó Olá são removidas quando o estado do nó Olá é removido (consulte [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).

### <a name="node-updown"></a>Nó ativo/inativo
System.FM informa como Okey ao nó Olá une anel hello (estiver em execução). Ele relata um erro ao nó Olá entregas de anel hello (ele estiver inativo, seja para atualizar ou simplesmente porque ele falhou). hierarquia de integridade Olá criada pelo repositório de integridade Olá age em entidades implantadas em correlação com relatórios de nó System.FM. Ele considera nó Olá virtual pai de todas as entidades implantados. entidades Olá implantado nesse nó são expostas por meio de consultas se o nó Olá é relatada como backup por System.FM, com hello mesmo a instância como instância Olá associada com entidades de saudação. Ao System.FM relatórios a nó hello está desligado ou reiniciado (uma nova instância), repositório de integridade Olá limpa automaticamente entidades Olá implantado que podem existir somente Olá para baixo de nó ou na instância anterior de saudação do nó de saudação.

* **SourceId**: System.FM
* **Propriedade**: Estado
* **Próximas etapas**: se o nó de saudação está inativo para uma atualização, ele deve voltar depois que ele foi atualizado. Nesse caso, o estado de integridade de saudação deve alternar tooOK back. Se o nó de saudação não voltar ou falhar, problema de saudação precisa de mais investigação.

Olá exemplo a seguir mostra Olá System.FM evento com um estado de integridade de Okey para o nó de:

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
**System.FabricNode** relata um aviso quando certificados usados por nó Olá estão prestes a expirar. Há três certificados por nó: **Certificate_cluster**, **Certificate_server** e **Certificate_default_client**. Quando a expiração de saudação é pelo menos duas semanas, o estado de integridade de relatório de saudação é Okey. Quando a expiração Olá estiver dentro de duas semanas, o tipo de relatório de saudação é um aviso. TTL desses eventos é infinito, e eles são removidos quando sai de um nó de cluster hello.

* **SourceId**: System.FabricNode
* **Propriedade**: começa com **certificado** e contém mais informações sobre o tipo de certificado Olá
* **Próximas etapas**: atualizar certificados de saudação se eles estiverem perto da expiração.

### <a name="load-capacity-violation"></a>Violação da capacidade de carga
Olá balanceador de carga de malha do serviço relata um aviso quando detecta uma violação de capacidade do nó.

* **SourceId**: System.PLB
* **Propriedade**: começa com **Capacity**
* **Próximas etapas**: seleção fornecido capacidade atual de métricas e exibição Olá no nó de saudação.

## <a name="application-system-health-reports"></a>Relatórios de integridade do sistema de aplicativo
**System.CM**, que representa o serviço de Gerenciador de Cluster de hello, Olá autoridade que gerencia informações sobre um aplicativo.

### <a name="state"></a>Estado
System.CM informa como Okey quando o aplicativo hello foi criado ou atualizado. Ele informa repositório de integridade hello quando o aplicativo hello foi excluído, para que ele pode ser removido do repositório.

* **SourceId**: System.CM
* **Propriedade**: Estado
* **Próximas etapas**: se o aplicativo hello foi criado ou atualizado, ele deve incluir o relatório de integridade do Gerenciador de Cluster de saudação. Caso contrário, verifique o estado de saudação do aplicativo hello emitindo uma consulta (por exemplo, Olá cmdlet do PowerShell **ServiceFabricApplication de Get - ApplicationName *applicationName***).

Olá exemplo a seguir mostra o evento de estado Olá em hello **fabric: / WordCount** aplicativo:

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
**System.FM**, que representa o serviço de Gerenciador de Failover hello, Olá autoridade que gerencia informações sobre os serviços.

### <a name="state"></a>Estado
System.FM informa como Okey quando Olá serviço foi criado. Ele exclui entidade saudação do repositório de integridade hello quando o serviço de saudação foi excluído.

* **SourceId**: System.FM
* **Propriedade**: Estado

Olá exemplo a seguir mostra o evento de estado Olá no serviço de saudação **fabric: / WordCount/WordCountWebService**:

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
**System.PLB** relata um erro quando detecta que um toobe serviço correlacionada com outro serviço de atualização cria uma cadeia de afinidade. relatório de saudação é limpo quando ocorre a atualização bem-sucedida.

* **SourceId**: System.PLB
* **Propriedade**: ServiceDescription
* **Próximas etapas**: seleção Olá correlacionados descrições de serviços.

## <a name="partition-system-health-reports"></a>Relatórios de integridade do sistema de partição
**System.FM**, que representa o serviço de Gerenciador de Failover hello, Olá autoridade que gerencia informações sobre partições de serviço.

### <a name="state"></a>Estado
System.FM informa como Okey quando a partição Olá foi criada e está íntegra. Ele exclui entidade saudação do repositório de integridade hello quando Olá partição será excluída.

Se a partição Olá está abaixo da contagem de réplica mínimo hello, ele relata um erro. Se Olá partição não está abaixo da contagem de réplica mínimo hello, mas está abaixo da contagem de réplica de destino hello, ele relata um aviso. Se a partição de saudação está em perda de quorum, System.FM relata um erro.

Outros eventos importantes incluem um aviso quando a reconfiguração de saudação leva mais tempo do que o esperado e quando a compilação Olá demora mais do que o esperado. tempos de saudação esperado para compilação hello e reconfiguração são configuráveis com base em cenários de serviço. Por exemplo, se um serviço tem um terabyte de estado, como o banco de dados SQL, compilação Olá leva mais tempo do que para um serviço com uma pequena quantidade de estado.

* **SourceId**: System.FM
* **Propriedade**: Estado
* **Próximas etapas**: se o estado de integridade de saudação não for Okey, é possível que algumas réplicas não foram criado, aberto ou promovida tooprimary ou secundário corretamente. Em muitos casos, Olá principal causa é um bug de serviço no hello aberta ou na implementação de função de alteração.

saudação de exemplo a seguir mostra uma partição íntegra:

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

Olá exemplo a seguir mostra a integridade saudação de uma partição que está abaixo da contagem de réplica de destino. Olá próxima etapa é tooget Olá descrição da partição, que mostra como estiver configurado: **MinReplicaSetSize** é três e **TargetReplicaSetSize** é sete. Em seguida, obter o número de Olá de nós no cluster Olá: cinco. Portanto nesse caso, duas réplicas não podem ser armazenadas porque o número de destino de saudação de réplicas é maior do que o número de saudação de nós disponíveis.

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
                        Description           : hello Load Balancer was unable toofind a placement for one or more of hello Service's Replicas:
                        Secondary replica could not be placed due toohello following constraints and properties:  
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
**System.PLB** relata um aviso se detectar uma violação de restrição de réplica e não puder posicionar todas as réplicas da partição. detalhes do relatório Olá mostram quais restrições e propriedades de evitar que o posicionamento de réplica de saudação.

* **SourceId**: System.PLB
* **Propriedade**: começa com **ReplicaConstraintViolation**

## <a name="replica-system-health-reports"></a>Relatórios de integridade do sistema de réplica
**System.RA**, que representa o componente do agente de reconfiguração Olá, é a autoridade de saudação para estado da réplica hello.

### <a name="state"></a>Estado
**System.RA** relata Okey quando Olá réplica foi criada.

* **SourceId**: System.RA
* **Propriedade**: Estado

saudação de exemplo a seguir mostra uma réplica íntegra:

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
Descrição de saudação deste relatório de integridade contém a hora de início da saudação (Coordinated Universal Time) quando chamada Olá API foi chamada.

**System.RA** relata um aviso se a réplica de saudação abrir demora mais do que o período Olá configurado (padrão: 30 minutos). Se Olá API afeta a disponibilidade do serviço, o relatório de saudação é emitido muito mais rápido (um intervalo configurável, com um padrão de 30 segundos). medida de tempo de saudação inclui tempo Olá para o replicador de saudação aberto e o serviço de Olá aberto. Olá tooOK de alterações de propriedade se abrir Olá completa.

* **SourceId**: System.RA
* **Propriedade**: **ReplicaOpenStatus**
* **Próximas etapas**: se o estado de integridade de saudação não for Okey, investigue por que a réplica de saudação abrir demora mais do que esperado.

### <a name="slow-service-api-call"></a>Chamada à API para serviço lento
**System.RAP** e **System.Replicator** relatar um aviso se um código de serviço chamada toohello usuário demora mais do que o tempo de saudação configurado. Aviso de saudação é limpo quando Olá chamada é concluída.

* **SourceId**: System.RAP ou System.Replicator
* **Propriedade**: nome de saudação da API lenta hello. Descrição de saudação fornece mais detalhes sobre a saudação de tempo Olá API foi pendente.
* **Próximas etapas**: investigar por que a chamada de saudação demora mais do que esperado.

saudação de exemplo a seguir mostra uma partição em perda de quorum e Olá investigação etapas feitas toofigure o motivo. Uma das réplicas de saudação tem um estado de integridade de aviso, para que você obtenha sua integridade. Ele mostra que operação de serviço Olá leva mais tempo do que o esperado, um evento relatado pelo System.RAP. Depois que essas informações são recebidas, o hello próxima etapa é toolook no código de serviço hello e investigar existe. Nesse caso, Olá **RunAsync** implementação de serviço com monitoração de estado Olá lança uma exceção sem tratamento. réplicas de saudação são Reciclando, talvez você não veja todas as réplicas em estado de aviso de saudação. Você pode tentar novamente obter estado de integridade de saudação e examinar as diferenças na ID de réplica hello. Em certos casos, repetições Olá podem fornecer pistas.

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

Quando você inicia o aplicativo com defeito hello sob depurador Olá, o windows de eventos de diagnóstico de saudação mostram exceção de saudação do RunAsync:

![Eventos de diagnóstico do Visual Studio 2015: falha de RunAsync em fabric:/HelloWorldStatefulApplication.][1]

Eventos de diagnóstico do Visual Studio 2015: falha de RunAsync em **fabric:/HelloWorldStatefulApplication**.

[1]: ./media/service-fabric-understand-and-troubleshoot-with-system-health-reports/servicefabric-health-vs-runasync-exception.png


### <a name="replication-queue-full"></a>Fila de replicação cheia
**System.Replicator** relata um aviso quando a fila de replicação hello está cheia. Em Olá primário, fila de replicação normalmente fica cheio porque uma ou mais réplicas secundárias são operações tooacknowledge lenta. Em Olá secundário, isso geralmente acontece quando o serviço hello está lenta tooapply Olá operações. Aviso de saudação é limpo quando a fila de saudação não esteja mais cheio.

* **SourceId**: System.Replicator
* **Propriedade**: **PrimaryReplicationQueueStatus** ou **SecondaryReplicationQueueStatus**, dependendo da função de réplica Olá

### <a name="slow-naming-operations"></a>Operações de Nomeação lentas
**System.NamingService** relata a integridade na réplica primária quando uma operação de nomenclatura demora mais do que o aceitável. Exemplos de operações de Nomeação: [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) ou [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync). Mais métodos podem ser encontrados em FabricClient, por exemplo, em [métodos de gerenciamento do serviço](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) ou [métodos de gerenciamento de propriedade](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).

> [!NOTE]
> Olá Naming service resolve local tooa do serviço de nomes de cluster hello e permite que propriedades e nomes de serviço toomanage de usuários. É um serviço persistentes particionado pelo Service Fabric. Uma das partições Olá representa Olá proprietário da autoridade, que contém metadados sobre todos os nomes de serviço de malha e serviços. nomes de Service Fabric do Hello são mapeadas toodifferent partições, chamadas partições do proprietário do nome, portanto, o serviço de saudação extensível. Leia mais sobre o [Serviço de nomeação](service-fabric-architecture.md).
> 
> 

Quando uma operação de nomenclatura leva mais tempo do que o esperado, operação Olá será sinalizada com um relatório de aviso em Olá *réplica primária do hello nomear a partição de serviço que serve a operação de saudação*. Se a operação de saudação for concluída com êxito, hello aviso está desmarcado. Se a conclusão da operação de saudação com um erro, o relatório de integridade Olá inclui detalhes sobre o erro hello.

* **SourceId**: System.NamingService
* **Propriedade**: começa com o prefixo **Duration_** e identifica a operação lenta hello e o nome de malha do serviço Olá quais Olá operação é aplicada. Por exemplo, se criar um serviço na malha de nome: / MyApp/MyService leva muito tempo, a propriedade de saudação é Duration_AOCreateService.fabric:/MyApp/MyService. Função de toohello sol pontos de saudação partição de nomenclatura para o nome e a operação.
* **Próximas etapas**: seleção por Olá nomenclatura operação falha. Cada operação pode ter causas raiz diferentes. Por exemplo, excluir o serviço pode estar preso em um nó, porque o host de aplicativo hello fica falhando em um nó devido tooa bug de usuário no código de serviço de saudação.

saudação de exemplo a seguir mostra uma operação de criação do serviço. operação de saudação demorou mais do que a duração de saudação configurada. AO tentar novamente e envia tooNO de trabalho. Nenhuma operação última Olá concluída com tempo limite. Nesse caso, hello mesma réplica é a principal para Olá sol e nenhuma função.

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
                        Description           : hello AOCreateService started at 2016-04-29 20:39:08.677 is taking longer than 30.000.
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
                        Description           : hello NOCreateService started at 2016-04-29 20:39:08.689 completed with FABRIC_E_TIMEOUT in more than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM
```

## <a name="deployedapplication-system-health-reports"></a>Relatórios de integridade do sistema DeployedApplication
**System.Hosting** é Olá autoridade em entidades implantadas.

### <a name="activation"></a>Ativação
System.Hosting informa como Okey quando um aplicativo foi ativado com êxito no nó de saudação. Caso contrário, ele relata um erro.

* **SourceId**: System.Hosting
* **Propriedade**: ativação, incluindo a versão de distribuição Olá
* **Próximas etapas**: se o aplicativo hello não está íntegro, investigar por que a ativação de saudação falhou.

saudação de ativação bem-sucedida do exemplo mostra a seguir:

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
                                     Description           : hello application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a>Baixar
**System.Hosting** relata um erro se o download do pacote de aplicativo hello falhar.

* **SourceId**: System.Hosting
* **Propriedade**: **Download:*RolloutVersion***
* **Próximas etapas**: investigar por que o download de saudação falhou no nó de saudação.

## <a name="deployedservicepackage-system-health-reports"></a>Relatórios de integridade do sistema DeployedServicePackage
**System.Hosting** é Olá autoridade em entidades implantadas.

### <a name="service-package-activation"></a>Ativação do pacote de serviço
System.Hosting informa como Okey se a ativação do pacote de serviço Olá no nó de saudação for bem-sucedida. Caso contrário, ele relata um erro.

* **SourceId**: System.Hosting
* **Propriedade**: ativação
* **Próximas etapas**: investigar por que a ativação de saudação falhou.

### <a name="code-package-activation"></a>Ativação do pacote de códigos
**System.Hosting** informa como Okey para cada pacote de código se saudação de ativação é bem-sucedida. Se a ativação Olá falhar, ele relata um aviso como configurado. Se **CodePackage** falhar tooactivate ou termina com um erro maior Olá configurado **CodePackageHealthErrorThreshold**, hospedagem relata um erro. Se um pacote de serviço contiver vários pacotes de código, um relatório de ativação será gerado para cada um.

* **SourceId**: System.Hosting
* **Propriedade**: prefixo de saudação usa **CodePackageActivation** e contém o nome de saudação do pacote de códigos hello e ponto de entrada hello como  **CodePackageActivation:* CodePackageName*:*SetupEntryPoint/EntryPoint** * (por exemplo, **CodePackageActivation:Code:SetupEntryPoint**)

### <a name="service-type-registration"></a>Registro do tipo de serviço
**System.Hosting** informa como Okey se o tipo de serviço Olá foi registrado com êxito. Ele relata um erro se Olá registro não foi feito no tempo (configurado usando **ServiceTypeRegistrationTimeout**). Se Olá runtime estiver fechada, o tipo de serviço Olá é cancelar o registro do nó de saudação e hospedagem relata um aviso.

* **SourceId**: System.Hosting
* **Propriedade**: prefixo de saudação usa **ServiceTypeRegistration** e contém o nome do tipo de serviço de saudação (por exemplo, **ServiceTypeRegistration:FileStoreServiceType**)

saudação de exemplo a seguir mostra um pacote de serviço implantado Íntegro:

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
                             Description           : hello ServicePackage was activated successfully.
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
                             Description           : hello CodePackage was activated successfully.
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
                             Description           : hello ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a>Baixar
**System.Hosting** relata um erro se o download do pacote de serviço Olá falhar.

* **SourceId**: System.Hosting
* **Propriedade**: **Download:*RolloutVersion***
* **Próximas etapas**: investigar por que o download de saudação falhou no nó de saudação.

### <a name="upgrade-validation"></a>Validação da atualização
**System.Hosting** relata um erro se houver falha na validação durante a atualização de saudação ou se hello atualização falha no nó de saudação.

* **SourceId**: System.Hosting
* **Propriedade**: prefixo de saudação usa **FabricUpgradeValidation** e contém a versão de atualização de saudação
* **Descrição**: pontos toohello erro

## <a name="next-steps"></a>Próximas etapas
[Como exibir relatórios de integridade do Service Fabric](service-fabric-view-entities-aggregated-health.md)

[Como tooreport e verificação de integridade do serviço](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[Monitorar e diagnosticar serviços localmente](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Atualização de aplicativos do Service Fabric](service-fabric-application-upgrade.md)

