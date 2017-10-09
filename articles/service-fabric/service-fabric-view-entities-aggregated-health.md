---
title: entidades do Azure Service Fabric aaaHow tooview agregado de integridade | Microsoft Docs
description: Descreve como tooquery, exibir e avaliar a integridade agregada de entidades do Azure Service Fabric, por meio de consultas de integridade e consultas gerais.
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: fa34c52d-3a74-4b90-b045-ad67afa43fe5
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: oanapl
ms.openlocfilehash: add810551cac26d2b4ff81b57d94ddd780c2cc2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="view-service-fabric-health-reports"></a>Como exibir relatórios de integridade do Service Fabric
O Azure Service Fabric apresenta um [modelo de integridade](service-fabric-health-introduction.md) com entidades de integridade nas quais os componentes do sistema e watchdogs podem relatar condições locais que estão monitorando. Olá [repositório de integridade](service-fabric-health-introduction.md#health-store) agrega todos os toodetermine de dados de integridade se entidades estão íntegros.

cluster de saudação é preenchida automaticamente com os relatórios de integridade enviados pelos componentes do sistema hello. Leia mais em [relatórios de integridade do sistema de uso do tootroubleshoot](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).

Serviço de malha fornece várias maneiras tooget Olá agregado integridade de entidades de saudação:

* [Gerenciador de Malha do Serviço](service-fabric-visualizing-your-cluster.md) ou outras ferramentas de visualização
* Consultas de integridade (por meio do PowerShell, da API ou de REST)
* Geral consultas que retornam uma lista de entidades que têm integridade como uma das propriedades de saudação (por meio do PowerShell, API ou REST)

toodemonstrate essas opções, vamos usar um cluster local com cinco nós e hello [fabric: / aplicativo WordCount](http://aka.ms/servicefabric-wordcountapp). Olá **fabric: / WordCount** aplicativo contém dois serviços de padrão, um serviço com monitoração de estado do tipo `WordCountServiceType`e um serviço sem monitoração de estado do tipo `WordCountWebServiceType`. Alterei Olá `ApplicationManifest.xml` toorequire sete réplicas de destino para o serviço com monitoração de estado hello e uma partição. Porque há apenas cinco nós no cluster hello, componentes do sistema Olá relatam um aviso na partição de serviço Olá porque ele está abaixo da contagem de destino hello.

```xml
<Service Name="WordCountService">
<<<<<<< HEAD
    <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="3">
      <UniformInt64Partition PartitionCount="1" LowKey="1" HighKey="26" />
    </StatefulService>
=======
  <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="2">
    <UniformInt64Partition PartitionCount="[WordCountService_PartitionCount]" LowKey="1" HighKey="26" />
  </StatefulService>
>>>>>>> 5e84dbdd8e45a5d6b36f435a550b7433b873bf11
</Service>
```

## <a name="health-in-service-fabric-explorer"></a>Integridade no Gerenciador da Malha do Serviço
Service Fabric Explorer fornece uma exibição visual de cluster hello. Na imagem de saudação abaixo, você pode ver que:

* Olá aplicativo **fabric: / WordCount** é vermelho (erro) porque ele tem um evento de erro relatado pelo **MyWatchdog** para a propriedade Olá **disponibilidade**.
* Um de seus serviços, **fabric:/WordCount/WordCountService** está amarelo (em aviso). Olá serviço está configurado com sete réplicas e cluster Olá tem cinco nós, duas repicas não pode ser colocados. Embora não seja mostrado aqui, partição de serviço Olá estiver amarela devido a um relatório do sistema de `System.FM` dizendo que `Partition is below target replica or instance count`. gatilhos de partição amarelo Olá Olá serviço amarelo.
* cluster de saudação é vermelho devido ao aplicativo hello vermelho.

avaliação de saudação usa políticas de padrão de manifesto do cluster hello e o manifesto do aplicativo. Elas são políticas rígidas e não toleram falhas.

Exibição do cluster Olá Service Fabric Explorer de:

![Exibição de cluster Olá com Gerenciador do Service Fabric.][1]

[1]: ./media/service-fabric-view-entities-aggregated-health/servicefabric-explorer-cluster-health.png


> [!NOTE]
> Leia mais sobre o [Gerenciador da Malha do Serviço](service-fabric-visualizing-your-cluster.md).
>
>

## <a name="health-queries"></a>Consultas de integridade
Malha do serviço expõe consultas de integridade para cada Olá suportada [tipos de entidade](service-fabric-health-introduction.md#health-entities-and-hierarchy). Eles podem ser acessados por meio de saudação API, usando métodos em [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), cmdlets do PowerShell e REST. Essas consultas retornam informações de integridade completa sobre entidade Olá: Olá agregado estado de integridade, eventos de integridade de entidade, os estados de integridade filho (quando aplicável), avaliações não íntegras (quando a entidade de saudação não está íntegra) e estatísticas de integridade de filhos (quando aplicável).

> [!NOTE]
> Uma entidade de integridade é retornada quando está completamente populada no repositório de integridade de saudação. entidade Olá deve ser ativo (não excluído) e ter um relatório do sistema. Suas entidades pai na cadeia de hierarquia Olá também devem ter os relatórios do sistema. Se alguma dessas condições não forem atendidas, integridade Olá consultas retornam um [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) com [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` que mostra por que a entidade Olá não é retornada.
>
>

consultas de integridade Olá devem passar no identificador da entidade hello, dependendo do tipo de entidade hello. consultas de saudação aceitam parâmetros de política de integridade opcional. Se nenhuma política de integridade forem especificada, Olá [políticas de integridade](service-fabric-health-introduction.md#health-policies) do manifesto de cluster ou o aplicativo hello são usadas para avaliação. Se os manifestos de saudação não contém uma definição para políticas de integridade, diretivas de integridade saudação padrão são usadas para avaliação. diretivas de integridade padrão Olá não tolerar falhas. consultas de saudação também aceitam filtros para retornar somente os filhos parciais ou eventos – Olá aqueles que respeitam Olá filtros especificados. Outro filtro permite a exclusão de estatísticas de filhos de saudação.

> [!NOTE]
> Olá filtros de saída são aplicados no lado do servidor de saudação, para que o tamanho de resposta de mensagem de saudação é reduzido. É recomendável que você use filtros de saída Olá toolimit Olá dados retornam, em vez de aplicam filtros no lado do cliente de saudação.
>
>

A integridade da entidade contém:

* Olá estado de integridade agregado da entidade de saudação. Calculado pelo repositório de integridade de saudação com base em relatórios de integridade de entidade, filho estados de integridade (quando aplicável) e políticas de integridade. Leia mais sobre [Avaliação de integridade da entidade](service-fabric-health-introduction.md#health-evaluation).  
* eventos de integridade Olá na entidade hello.
* coleção de saudação de estados de integridade de todos os filhos de entidades de saudação que podem ter filhos. estados de integridade de saudação contêm os identificadores de entidade e Olá estado de integridade agregada. tooget toda a integridade de um filho, chame integridade de consulta Olá Olá filho tipo de entidade e passe no identificador de filho hello.
* avaliações não íntegras de saudação toohello esse ponto de relatório que disparado estado Olá da entidade de saudação se Olá entidade não está íntegra. avaliações de saudação são recursivas, contendo as avaliações de integridade do hello filhos que disparou o estado de integridade atual. Por exemplo, um watchdog relatou um erro em uma réplica. integridade do aplicativo Hello mostra uma avaliação não íntegro devido tooan de serviço não íntegro; serviço de saudação não está íntegro devido a partição tooa com erro; partição de saudação não está íntegra devido a réplica tooa com erro; réplica de saudação não está íntegra toohello relatório de integridade de erro de watchdog de conclusão.
* estatísticas de integridade Olá para todos os tipos de filhos de entidades de saudação que têm filhos. Por exemplo, a integridade do cluster mostra o número total de saudação de aplicativos, serviços, partições, as réplicas e implantado entidades no cluster hello. Integridade do serviço mostra o número total de saudação de partições e réplicas em Olá especificado serviço.

## <a name="get-cluster-health"></a>Obter integridade do cluster
Retorna Olá integridade da entidade de cluster hello e contém Olá estados de integridade de aplicativos e nós (filhos do cluster Olá). Entrada:

* Política de integridade de cluster Olá [opcional] usado tooevaluate nós de Olá Olá eventos e clusters.
* Mapa de política de integridade de aplicativo hello [opcional], com as políticas de integridade Olá usado diretivas do manifesto de aplicativo toooverride hello.
* [Opcional] Filtros de eventos, nós e aplicativos que especificam quais entradas são de interesse e devem ser retornadas no resultado da saudação (por exemplo, apenas os erros ou avisos e erros). Todos os eventos, nós e aplicativos são usados tooevaluate Olá agregado da entidade integridade, independentemente de filtro de saudação.
* [Opcional] Filtre tooexclude estatísticas de integridade.
* [Opcional] Filtrar tooinclude fabric: / estatísticas de integridade do sistema em Olá estatísticas de integridade. Aplicável somente quando as estatísticas de integridade de saudação não são excluídas. Por padrão, estatísticas de integridade de saudação incluem somente as estatísticas para aplicativos de usuário e o aplicativo de sistema do hello.

### <a name="api"></a>API
tooget integridade de cluster, crie um `FabricClient` e chamada hello [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) método no seu **HealthManager**.

Olá, chamada a seguir obtém a integridade do cluster hello:

```csharp
ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync();
```

Olá código a seguir obtém a integridade do cluster hello usando uma política de integridade de cluster personalizado e filtros para nós e aplicativos. Especifica estatísticas de integridade Olá incluem malha Olá: / estatísticas do sistema. Ele cria [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), que contém informações de entrada hello.

```csharp
var policy = new ClusterHealthPolicy()
{
    MaxPercentUnhealthyNodes = 20
};
var nodesFilter = new NodeHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error | HealthStateFilter.Warning
};
var applicationsFilter = new ApplicationHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error
};
var healthStatisticsFilter = new ClusterHealthStatisticsFilter()
{
    ExcludeHealthStatistics = false,
    IncludeSystemApplicationHealthStatistics = true
};
var queryDescription = new ClusterHealthQueryDescription()
{
    HealthPolicy = policy,
    ApplicationsFilter = applicationsFilter,
    NodesFilter = nodesFilter,
    HealthStatisticsFilter = healthStatisticsFilter
};

ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
integridade de cluster de saudação do Hello cmdlet tooget [Get-ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth). Primeiro, conecte o cluster toohello usando Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.

Olá estado do cluster de saudação é cinco nós, o aplicativo do sistema hello e fabric: / WordCount configurado conforme descrito.

Olá cmdlet a seguir obtém a integridade do cluster usando diretivas de integridade padrão. Olá estado de integridade agregada é um aviso, porque Olá fabric: / aplicativo WordCount estiver em um aviso. Observe como o avaliações não íntegras Olá fornecem detalhes sobre condições de saudação que disparou Olá agregado de integridade.

```xml
PS D:\ServiceFabric> Get-ServiceFabricClusterHealth


AggregatedHealthState   : Warning
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Warning'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                          
                          
NodeHealthStates        : 
                          NodeName              : _Node_4
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_3
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_2
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_1
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_0
                          AggregatedHealthState : Ok
                          
ApplicationHealthStates : 
                          ApplicationName       : fabric:/System
                          AggregatedHealthState : Ok
                          
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Warning
                          
HealthEvents            : None
HealthStatistics        : 
                          Node                  : 5 Ok, 0 Warning, 0 Error
                          Replica               : 6 Ok, 0 Warning, 0 Error
                          Partition             : 1 Ok, 1 Warning, 0 Error
                          Service               : 1 Ok, 1 Warning, 0 Error
                          DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                          DeployedApplication   : 5 Ok, 0 Warning, 0 Error
                          Application           : 0 Ok, 1 Warning, 0 Error
```

Olá seguinte cmdlet do PowerShell obtém Olá integridade de cluster hello usando uma política de aplicativo personalizado. Ele filtra somente aplicativos de tooget de resultados e nós em erro ou aviso. Como resultado nenhum nó é retornado, pois todos estão íntegros. Olá somente fabric: / aplicativo WordCount respeita o filtro de aplicativos de saudação. Porque a política personalizada de saudação especifica tooconsider avisos como erros de malha Olá: / aplicativo WordCount, o aplicativo hello é avaliado como em erro, e então é cluster hello.

```powershell
PS D:\ServiceFabric> $appHealthPolicy = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicy
$appHealthPolicy.ConsiderWarningAsError = $true
$appHealthPolicyMap = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicyMap
$appUri1 = New-Object -TypeName System.Uri -ArgumentList "fabric:/WordCount"
$appHealthPolicyMap.Add($appUri1, $appHealthPolicy)
Get-ServiceFabricClusterHealth -ApplicationHealthPolicyMap $appHealthPolicyMap -ApplicationsFilter "Warning,Error" -NodesFilter "Warning,Error" -ExcludeHealthStatistics


AggregatedHealthState   : Error
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Error'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                          
                          
NodeHealthStates        : None
ApplicationHealthStates : 
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Error
                          
HealthEvents            : None
```

### <a name="rest"></a>REST
Você pode obter a integridade do cluster com um [solicitação GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) ou um [solicitação POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) que inclui as políticas de integridade descritas no corpo de saudação.

## <a name="get-node-health"></a>Obter integridade do nó
Retorna Olá integridade de uma entidade de nó e contém eventos de integridade de saudação relatados no nó de saudação. Entrada:

* Nome do nó Olá [obrigatório] que identifica o nó de saudação.
* Configurações de política de integridade de cluster [opcional] Olá usado tooevaluate integridade.
* [Opcional] Os filtros de eventos que especifiquem as entradas são de interesse e devem ser retornados no resultado da saudação (por exemplo, apenas os erros ou avisos e erros). Todos os eventos são usados tooevaluate Olá agregado da entidade integridade, independentemente de filtro de saudação.

### <a name="api"></a>API
integridade do nó tooget por meio de saudação API, crie um `FabricClient` e chamada hello [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) método no seu HealthManager.

Olá código a seguir obtém integridade do nó Olá para o nome do nó especificado hello:

```csharp
NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(nodeName);
```

Olá código a seguir obtém integridade do nó Olá para Olá especificado o nome do nó e passa no filtro de eventos e uma política personalizada por meio de [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):

```csharp
var queryDescription = new NodeHealthQueryDescription(nodeName)
{
    HealthPolicy = new ClusterHealthPolicy() {  ConsiderWarningAsError = true },
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.Warning },
};

NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
integridade do nó do Hello cmdlet tooget Olá [Get-ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth). Primeiro, conecte o cluster toohello usando Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.
Olá cmdlet a seguir obtém a integridade do nó hello usando diretivas de integridade padrão:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNodeHealth _Node_1


NodeName              : _Node_1
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 3
                        SentAt                : 7/13/2017 4:39:23 PM
                        ReceivedAt            : 7/13/2017 4:40:47 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 4:40:47 PM, LastWarning = 1/1/0001 12:00:00 AM
```

Olá cmdlet a seguir obtém Olá integridade de todos os nós no cluster hello:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNode | Get-ServiceFabricNodeHealth | select NodeName, AggregatedHealthState | ft -AutoSize

NodeName AggregatedHealthState
-------- ---------------------
_Node_4                     Ok
_Node_3                     Ok
_Node_2                     Ok
_Node_1                     Ok
_Node_0                     Ok
```

### <a name="rest"></a>REST
Você pode obter a integridade do nó com um [solicitação GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) ou um [solicitação POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) que inclui as políticas de integridade descritas no corpo de saudação.

## <a name="get-application-health"></a>Obter integridade do aplicativo
Retorna a integridade de uma entidade de aplicativo hello. Ele contém os estados de integridade de saudação do aplicativo hello implantado e filhos de serviço. Entrada:

* Olá [obrigatório] nome do aplicativo (URI) que identifica o aplicativo hello.
* Política de integridade de aplicativo hello [opcional] usado diretivas do manifesto de aplicativo toooverride hello.
* [Opcional] Os filtros de eventos, serviços e aplicativos implantados que especificam quais entradas são de interesse e devem ser retornados no resultado da saudação (por exemplo, apenas os erros ou avisos e erros). Todos os eventos, serviços e aplicativos implantados são usados tooevaluate Olá agregado da entidade integridade, independentemente de filtro de saudação.
* [Opcional] Estatísticas de integridade de saudação tooexclude de filtro. Se não for especificado, as estatísticas de integridade de saudação incluem okey hello, de aviso e de contagem de erros para todos os filhos do aplicativo: serviços, partições, réplicas, aplicativos implantados e pacotes de serviço implantados.

### <a name="api"></a>API
integridade do aplicativo tooget, criar um `FabricClient` e chamada hello [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) método no seu HealthManager.

Olá, código a seguir obtém Olá integridade de aplicativo para o nome do aplicativo especificado hello (URI):

```csharp
ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(applicationName);
```

Olá código a seguir obtém Olá aplicativo integridade para o nome do aplicativo especificado hello (URI), com filtros e políticas personalizadas especificado via [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).

```csharp
HealthStateFilter warningAndErrors = HealthStateFilter.Error | HealthStateFilter.Warning;
var serviceTypePolicy = new ServiceTypeHealthPolicy()
{
    MaxPercentUnhealthyPartitionsPerService = 0,
    MaxPercentUnhealthyReplicasPerPartition = 5,
    MaxPercentUnhealthyServices = 0,
};
var policy = new ApplicationHealthPolicy()
{
    ConsiderWarningAsError = false,
    DefaultServiceTypeHealthPolicy = serviceTypePolicy,
    MaxPercentUnhealthyDeployedApplications = 0,
};

var queryDescription = new ApplicationHealthQueryDescription(applicationName)
{
    HealthPolicy = policy,
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = warningAndErrors },
    ServicesFilter = new ServiceHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
    DeployedApplicationsFilter = new DeployedApplicationHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
};

ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
integridade do aplicativo Hello cmdlet tooget Olá é [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps). Primeiro, conecte o cluster toohello usando Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.

Hello, cmdlet a seguir retorna integridade de saudação do hello **fabric: / WordCount** aplicativo:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Warning
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountWebService
                                  AggregatedHealthState : Ok
                                  
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Warning
                                  
DeployedApplicationHealthStates : 
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_4
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_3
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_0
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_2
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_1
                                  AggregatedHealthState : Ok
                                  
HealthEvents                    : 
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 282
                                  SentAt                : 7/13/2017 5:57:05 PM
                                  ReceivedAt            : 7/13/2017 5:57:05 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 7/13/2017 5:57:05 PM, LastWarning = 1/1/0001 12:00:00 AM
                                  
HealthStatistics                : 
                                  Replica               : 6 Ok, 0 Warning, 0 Error
                                  Partition             : 1 Ok, 1 Warning, 0 Error
                                  Service               : 1 Ok, 1 Warning, 0 Error
                                  DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                                  DeployedApplication   : 5 Ok, 0 Warning, 0 Error
```

Olá seguindo os passos de cmdlet do PowerShell em políticas personalizadas. Ele também filtra filhos e eventos.

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth -ApplicationName fabric:/WordCount -ConsiderWarningAsError $true -ServicesFilter Error -EventsFilter Error -DeployedApplicationsFilter Error -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Error
                                  
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

### <a name="rest"></a>REST
Você pode obter a integridade do aplicativo com um [solicitação GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) ou um [solicitação POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) que inclui as políticas de integridade descritas no corpo de saudação.

## <a name="get-service-health"></a>Obter integridade do serviço
Retorna a integridade de saudação de uma entidade de serviço. Ele contém Olá estados de integridade de partição. Entrada:

* Olá [obrigatório] nome do serviço (URI) que identifica o serviço de saudação.
* Política de integridade de aplicativo hello [opcional] usado diretiva do manifesto de aplicativo toooverride hello.
* [Opcional] Filtros de eventos e partições que especificam quais entradas são de interesse e devem ser retornadas no resultado da saudação (por exemplo, apenas os erros ou avisos e erros). Todos os eventos e as partições são usadas tooevaluate Olá agregado da entidade integridade, independentemente de filtro de saudação.
* [Opcional] Filtre tooexclude estatísticas de integridade. Se não for especificado, Olá integridade estatísticas Mostrar Olá okey, aviso e erro de contagem de todas as partições e réplicas do serviço de saudação.

### <a name="api"></a>API
integridade do serviço tooget por meio de saudação API, crie um `FabricClient` e chamada hello [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) método no seu HealthManager.

Olá, exemplo a seguir obtém Olá integridade de um serviço com o nome de serviço especificado (URI):

```charp
ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(serviceName);
```

Olá, código a seguir obtém Olá a integridade do serviço para nome de serviço especificado da saudação (URI), especificando filtros e uma política personalizada por meio de [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):

```csharp
var queryDescription = new ServiceHealthQueryDescription(serviceName)
{
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.All },
    PartitionsFilter = new PartitionHealthStatesFilter() { HealthStateFilterValue = HealthStateFilter.Error },
};

ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
integridade do serviço do Hello cmdlet tooget Olá [Get-ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth). Primeiro, conecte o cluster toohello usando Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.

Olá cmdlet a seguir obtém a integridade do serviço hello usando diretivas de integridade padrão:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricServiceHealth -ServiceName fabric:/WordCount/WordCountService


ServiceName           : fabric:/WordCount/WordCountService
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                        
                        Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                        
                            Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
PartitionHealthStates : 
                        PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                        AggregatedHealthState : Warning
                        
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 15
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
                        Partition             : 0 Ok, 1 Warning, 0 Error
```

### <a name="rest"></a>REST
Você pode obter a integridade do serviço com um [solicitação GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) ou um [solicitação POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) que inclui as políticas de integridade descritas no corpo de saudação.

## <a name="get-partition-health"></a>Obter integridade da partição
Retorna a integridade de saudação de uma entidade de partição. Ele contém Olá estados de integridade de réplica. Entrada:

* Partição de saudação [obrigatório] ID (GUID) que identifica a partição de saudação.
* Política de integridade de aplicativo hello [opcional] usado diretiva do manifesto de aplicativo toooverride hello.
* [Opcional] Filtros de eventos e as réplicas que especificam quais entradas são de interesse e devem ser retornadas no resultado da saudação (por exemplo, apenas os erros ou avisos e erros). Todos os eventos e as réplicas são usadas tooevaluate Olá agregado da entidade integridade, independentemente de filtro de saudação.
* [Opcional] Filtre tooexclude estatísticas de integridade. Se não for especificado, as estatísticas de integridade de Olá mostram quantas réplicas estão em okey, aviso e erro estados.

### <a name="api"></a>API
integridade da partição tooget por meio de saudação API, crie um `FabricClient` e chamada hello [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) método no seu HealthManager. criar parâmetros opcionais de toospecify, [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).

```csharp
PartitionHealth partitionHealth = await fabricClient.HealthManager.GetPartitionHealthAsync(partitionId);
```

### <a name="powershell"></a>PowerShell
integridade da partição Olá Olá cmdlet tooget é [Get-ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth). Primeiro, conecte o cluster toohello usando Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.

Olá, cmdlet a seguir obtém Olá integridade de todas as partições de saudação **fabric: / WordCount/WordCountService** serviço e filtra os estados de integridade da réplica:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth -ReplicasFilter None

PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 72
                        SentAt                : 7/13/2017 5:57:29 PM
                        ReceivedAt            : 7/13/2017 5:57:48 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        fabric:/WordCount/WordCountService 7 2 af2e3e44-a8f8-45ac-9f31-4093eb897600
                          N/P RD _Node_2 Up 131444422260002646
                          N/S RD _Node_4 Up 131444422293113678
                          N/S RD _Node_3 Up 131444422293113679
                          N/S RD _Node_1 Up 131444422293118720
                          N/S RD _Node_0 Up 131444422293118721
                          (Showing 5 out of 5 replicas. Total available replicas: 5.)
                        
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Ok->Warning = 7/13/2017 5:57:48 PM, LastError = 1/1/0001 12:00:00 AM
                        
                        SourceId              : System.PLB
                        Property              : ServiceReplicaUnplacedHealth_Secondary_af2e3e44-a8f8-45ac-9f31-4093eb897600
                        HealthState           : Warning
                        SequenceNumber        : 131444445174851664
                        SentAt                : 7/13/2017 6:35:17 PM
                        ReceivedAt            : 7/13/2017 6:35:18 PM
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
                        FaultDomain:fd:/1 NodeName:_Node_1 NodeType:NodeType1 UpgradeDomain:1 UpgradeDomain: ud:/1 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/0 NodeName:_Node_0 NodeType:NodeType0 UpgradeDomain:0 UpgradeDomain: ud:/0 Deactivation Intent/Status: None/None
                        
                        Existing Primary Replica -- Nodes with Partition's Existing Primary Replica or Secondary Replicas:
                        --
                        FaultDomain:fd:/2 NodeName:_Node_2 NodeType:NodeType2 UpgradeDomain:2 UpgradeDomain: ud:/2 Deactivation Intent/Status: None/None
                        
                        
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/13/2017 5:57:48 PM, LastOk = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a>REST
Você pode obter a integridade da partição com um [solicitação GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) ou um [solicitação POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) que inclui as políticas de integridade descritas no corpo de saudação.

## <a name="get-replica-health"></a>Obter integridade da réplica
Retorna a integridade de saudação de uma réplica de serviço com monitoração de estado ou uma instância de serviço sem monitoração de estado. Entrada:

* [Obrigatório] Olá partição ID (GUID) e réplica ID que identifica réplica hello.
* Parâmetros de política de integridade de aplicativo hello [opcional] usado diretivas do manifesto de aplicativo toooverride hello.
* [Opcional] Os filtros de eventos que especifiquem as entradas são de interesse e devem ser retornados no resultado da saudação (por exemplo, apenas os erros ou avisos e erros). Todos os eventos são usados tooevaluate Olá agregado da entidade integridade, independentemente de filtro de saudação.

### <a name="api"></a>API
integridade da réplica Olá tooget por meio de saudação API, crie um `FabricClient` e chamada hello [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) método no seu HealthManager. use parâmetros avançados de toospecify [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).

```csharp
ReplicaHealth replicaHealth = await fabricClient.HealthManager.GetReplicaHealthAsync(partitionId, replicaId);
```

### <a name="powershell"></a>PowerShell
integridade da réplica Olá Olá cmdlet tooget é [Get-ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth). Primeiro, conecte o cluster toohello usando Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.

Olá, cmdlet a seguir obtém Olá integridade da réplica primária de saudação para todas as partições do serviço de saudação:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a>REST
Você pode obter a integridade da réplica com um [solicitação GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) ou um [solicitação POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) que inclui as políticas de integridade descritas no corpo de saudação.

## <a name="get-deployed-application-health"></a>Obter integridade do aplicativo implantado
Retorna Olá integridade de um aplicativo implantado em uma entidade do nó. Ele contém os estados de integridade de pacote de serviço Olá implantado. Entrada:

* Nome do aplicativo hello [obrigatório] (URI) e o nome de nó (string) que identificam Olá implantado o aplicativo.
* Política de integridade de aplicativo hello [opcional] usado diretivas do manifesto de aplicativo toooverride hello.
* [Opcional] Os filtros de eventos e pacotes de serviço implantado que especificam quais entradas são de interesse e devem ser retornados no resultado da saudação (por exemplo, apenas os erros ou avisos e erros). Todos os eventos e pacotes de serviços implantados são usados tooevaluate Olá agregado da entidade integridade, independentemente de filtro de saudação.
* [Opcional] Filtre tooexclude estatísticas de integridade. Se não for especificado, o hello estatísticas de integridade mostram o número de saudação de pacotes de serviço implantado nos Estados de integridade okey, aviso e erro.

### <a name="api"></a>API
integridade de saudação tooget de um aplicativo implantado em um nó por meio de saudação API, crie um `FabricClient` e chamada hello [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) método no seu HealthManager. parâmetros opcionais de toospecify, use [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).

```csharp
DeployedApplicationHealth health = await fabricClient.HealthManager.GetDeployedApplicationHealthAsync(
    new DeployedApplicationHealthQueryDescription(applicationName, nodeName));
```

### <a name="powershell"></a>PowerShell
Olá cmdlet tooget Olá implantado integridade do aplicativo é [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps). Primeiro, conecte o cluster toohello usando Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet. toofind limite em que um aplicativo é implantado, execute [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) e examinar Olá implantado filhos do aplicativo.

Hello, cmdlet a seguir obtém Olá integridade de saudação **fabric: / WordCount** aplicativo implantado em **_Node_2**.

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplicationHealth -ApplicationName fabric:/WordCount -NodeName _Node_0


ApplicationName                    : fabric:/WordCount
NodeName                           : _Node_0
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates : 
                                     ServiceManifestName   : WordCountServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
                                     ServiceManifestName   : WordCountWebServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
HealthEvents                       : 
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 131444422261848308
                                     SentAt                : 7/13/2017 5:57:06 PM
                                     ReceivedAt            : 7/13/2017 5:57:17 PM
                                     TTL                   : Infinite
                                     Description           : hello application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/13/2017 5:57:17 PM, LastWarning = 1/1/0001 12:00:00 AM
                                     
HealthStatistics                   : 
                                     DeployedServicePackage : 2 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a>REST
Você pode obter a integridade do aplicativo implantado com um [solicitação GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) ou um [solicitação POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) que inclui as políticas de integridade descritas no corpo de saudação.

## <a name="get-deployed-service-package-health"></a>Obter integridade do pacote de serviço implantado
Retorna Olá integridade de uma entidade de pacote de serviço implantado. Entrada:

* Nome do aplicativo hello [obrigatório] (URI), nome do nó (string) e o nome manifesto do serviço (string) que identificam Olá implantadas pacote de serviço.
* Política de integridade de aplicativo hello [opcional] usado diretiva do manifesto de aplicativo toooverride hello.
* [Opcional] Os filtros de eventos que especifiquem as entradas são de interesse e devem ser retornados no resultado da saudação (por exemplo, apenas os erros ou avisos e erros). Todos os eventos são usados tooevaluate Olá agregado da entidade integridade, independentemente de filtro de saudação.

### <a name="api"></a>API
integridade de saudação tooget de um pacote de serviço implantado por meio de saudação API, crie um `FabricClient` e chamada hello [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) método no seu HealthManager. parâmetros opcionais de toospecify, use [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).

```csharp
DeployedServicePackageHealth health = await fabricClient.HealthManager.GetDeployedServicePackageHealthAsync(
    new DeployedServicePackageHealthQueryDescription(applicationName, nodeName, serviceManifestName));
```

### <a name="powershell"></a>PowerShell
Olá integridade do pacote de serviço do cmdlet tooget Olá implantado é [Get-ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth). Primeiro, conecte o cluster toohello usando Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet. executar toosee onde um aplicativo é implantado, [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) e analisar os aplicativos implantado de saudação. toosee que os pacotes de serviço estão em um aplicativo, procure no hello implantado filhos de pacote de serviço em Olá [ServiceFabricDeployedApplicationHealth Get](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) saída.

Hello, cmdlet a seguir obtém Olá integridade de saudação **WordCountServicePkg** pacote de serviço do hello **fabric: / WordCount** aplicativo implantado em **_Node_2**. Olá entidade tem **System.Hosting** relatórios de ativação bem-sucedida do pacote de serviço e o ponto de entrada e o registro bem-sucedido do tipo de serviço.

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplication -ApplicationName fabric:/WordCount -NodeName _Node_2 | Get-ServiceFabricDeployedServicePackageHealth -ServiceManifestName WordCountServicePkg


ApplicationName            : fabric:/WordCount
ServiceManifestName        : WordCountServicePkg
ServicePackageActivationId : 
NodeName                   : _Node_2
AggregatedHealthState      : Ok
HealthEvents               : 
                             SourceId              : System.Hosting
                             Property              : Activation
                             HealthState           : Ok
                             SequenceNumber        : 131444422267693359
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : hello ServicePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : CodePackageActivation:Code:EntryPoint
                             HealthState           : Ok
                             SequenceNumber        : 131444422267903345
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : hello CodePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : ServiceTypeRegistration:WordCountServiceType
                             HealthState           : Ok
                             SequenceNumber        : 131444422272458374
                             SentAt                : 7/13/2017 5:57:07 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : hello ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a>REST
Você pode obter a integridade do pacote de serviço implantado com um [solicitação GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) ou um [solicitação POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) que inclui as políticas de integridade descritas no corpo de saudação.

## <a name="health-chunk-queries"></a>Consultas de integridade em blocos
consultas de parte de integridade de saudação podem retornar os filhos de cluster de vários níveis (recursivamente), por filtros de entrada. Ele dá suporte a filtros avançados que permitem que uma grande flexibilidade na escolha de filhos Olá toobe retornado. filtros de saudação podem especificar filhos por identificador exclusivo da saudação ou outros identificadores de grupo e/ou os estados de integridade. Por padrão, nenhum filho é incluído, como comandos toohealth contrário que incluem sempre o primeiro nível filhos.

Olá [consultas de integridade](service-fabric-view-entities-aggregated-health.md#health-queries) retorno filhos apenas de primeiro nível de saudação especificado entidade por filtros necessários. tooget Olá filhos filhos hello, você deve chamar APIs de integridade adicional para cada entidade de interesse. Da mesma forma, integridade de saudação tooget de entidades específicas, você deve chamar integridade de uma API para cada entidade desejada. Olá parte consulta filtragem avançada permite que você toorequest vários itens de interesse em uma consulta, reduzindo o tamanho de mensagem de saudação e número de saudação de mensagens.

valor de saudação de consulta de parte de saudação é que você pode obter o estado de integridade para mais entidades de cluster (potencialmente todos os cluster entidades começando na raiz necessário) em uma chamada. Você pode expressar uma consulta de integridade complexa da seguinte maneira:

* Retorne apenas os aplicativos com erro e, para esses aplicativos, inclua todos os serviços em aviso|erro. Para os serviços retornados, inclua todas as partições.
* Retorne apenas integridade de saudação de quatro aplicativos, especificado por seus nomes.
* Retorne apenas integridade de saudação de aplicativos de um tipo de aplicativo desejado.
* Retorne todas as entidades implantadas em um nó. Retorna todos os aplicativos, implantados todos os aplicativos no nó especificado hello e todos os pacotes de serviço Olá implantado naquele nó.
* Retorna todas as réplicas com erro. Retorna todos os aplicativos, serviços, partições e somente réplicas com erro.
* Retorna todos os aplicativos. Para um serviço específico, inclua todas as partições.

Atualmente, consulta de parte de integridade de saudação é exposta somente para a entidade de cluster hello. Ela retorna uma parte da integridade do cluster, que contém:

* estado de integridade do cluster agregado Hello.
* Olá integridade estado parte lista de nós que respeitar os filtros de entrada.
* Olá integridade estado parte lista de aplicativos que respeitar os filtros de entrada. Cada bloco de estado de integridade do aplicativo contém uma lista de partes com todos os serviços que respeitam os filtros de entrada e uma lista de partes com todos os aplicativos implantados que respeita filtros hello. Mesmo para os filhos de saudação de serviços e aplicativos implantados. Dessa forma, todas as entidades no cluster Olá podem ser potencialmente retornadas se solicitado, de maneira hierárquica.

### <a name="cluster-health-chunk-query"></a>Consulta em bloco sobre a integridade do cluster
Retorna Olá integridade da entidade de cluster hello e contém partes de estado de integridade hierárquica Olá dos filhos necessários. Entrada:

* Política de integridade de cluster Olá [opcional] usado tooevaluate nós de Olá Olá eventos e clusters.
* Mapa de política de integridade de aplicativo hello [opcional], com as políticas de integridade Olá usado diretivas do manifesto de aplicativo toooverride hello.
* [Opcional] Os filtros para nós e os aplicativos que especificam quais entradas são de interesse e devem ser retornados no resultado de saudação. filtros de saudação são tooan específico/grupo de entidades de entidades ou são aplicáveis tooall entidades nesse nível. saudação de filtros pode conter um filtro geral e/ou filtros para entidades de granularidade toofine identificadores específicos retornados pela consulta hello. Se estiver vazio, os filhos de saudação não são retornados por padrão.
  Leia mais sobre filtros de saudação [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) e [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter). Olá aplicativo filtros pode recursivamente especificar filtros avançados para filhos.

resultados de fragmento de saudação incluem filhos Olá respeitam os filtros de saudação.

No momento, a consulta de parte de saudação não retorna avaliações não íntegras ou eventos de entidade. Essas informações adicionais podem ser obtidas usando a consulta de integridade do cluster existente hello.

### <a name="api"></a>API
integridade do cluster tooget parte, crie um `FabricClient` e chamada hello [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) método no seu **HealthManager**. Você pode passar de [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) toodescribe diretivas de integridade e filtros avançados.

Olá código a seguir obtém o fragmento de integridade do cluster com filtros avançados.

```csharp
var queryDescription = new ClusterHealthChunkQueryDescription();
queryDescription.ApplicationFilters.Add(new ApplicationHealthStateFilter()
    {
        // Return applications only if they are in error
        HealthStateFilter = HealthStateFilter.Error
    });

// Return all replicas
var wordCountServiceReplicaFilter = new ReplicaHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };

// Return all replicas and all partitions
var wordCountServicePartitionFilter = new PartitionHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };
wordCountServicePartitionFilter.ReplicaFilters.Add(wordCountServiceReplicaFilter);

// For specific service, return all partitions and all replicas
var wordCountServiceFilter = new ServiceHealthStateFilter()
{
    ServiceNameFilter = new Uri("fabric:/WordCount/WordCountService"),
};
wordCountServiceFilter.PartitionFilters.Add(wordCountServicePartitionFilter);

// Application filter: for specific application, return no services except hello ones of interest
var wordCountApplicationFilter = new ApplicationHealthStateFilter()
    {
        // Always return fabric:/WordCount application
        ApplicationNameFilter = new Uri("fabric:/WordCount"),
    };
wordCountApplicationFilter.ServiceFilters.Add(wordCountServiceFilter);

queryDescription.ApplicationFilters.Add(wordCountApplicationFilter);

var result = await fabricClient.HealthManager.GetClusterHealthChunkAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
integridade de cluster de saudação do Hello cmdlet tooget [Get-ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk). Primeiro, conecte o cluster toohello usando Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.

Olá código a seguir obtém nós apenas se estiverem em erro, exceto de um nó específico, que sempre deve ser retornado.

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$nodeFilter1 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{HealthStateFilter=$errorFilter}
$nodeFilter2 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{NodeNameFilter="_Node_1";HealthStateFilter=$allFilter}
# Create node filter list that will be passed in hello cmdlet
$nodeFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.NodeHealthStateFilter]
$nodeFilters.Add($nodeFilter1)
$nodeFilters.Add($nodeFilter2)

Get-ServiceFabricClusterHealthChunk -NodeFilters $nodeFilters


HealthState                  : Warning
NodeHealthStateChunks        : 
                               TotalCount            : 1
                               
                               NodeName              : _Node_1
                               HealthState           : Ok
                               
ApplicationHealthStateChunks : None
```

Olá cmdlet a seguir obtém a parte do cluster com filtros de aplicativo.

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

# All replicas
$replicaFilter = New-Object System.Fabric.Health.ReplicaHealthStateFilter -Property @{HealthStateFilter=$allFilter}

# All partitions
$partitionFilter = New-Object System.Fabric.Health.PartitionHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$partitionFilter.ReplicaFilters.Add($replicaFilter)

# For WordCountService, return all partitions and all replicas
$svcFilter1 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{ServiceNameFilter="fabric:/WordCount/WordCountService"}
$svcFilter1.PartitionFilters.Add($partitionFilter)

$svcFilter2 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{HealthStateFilter=$errorFilter}

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{ApplicationNameFilter="fabric:/WordCount"}
$appFilter.ServiceFilters.Add($svcFilter1)
$appFilter.ServiceFilters.Add($svcFilter2)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)

Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 1
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               ServiceHealthStateChunks : 
                                TotalCount            : 1
                               
                                ServiceName           : fabric:/WordCount/WordCountService
                                HealthState           : Error
                                PartitionHealthStateChunks : 
                                    TotalCount            : 1
                               
                                    PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                                    HealthState           : Error
                                    ReplicaHealthStateChunks : 
                                        TotalCount            : 5
                               
                                        ReplicaOrInstanceId   : 131444422293118720
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293118721
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113678
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113679
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422260002646
                                        HealthState           : Error
```

Olá cmdlet a seguir retorna implantadas todas as entidades em um nó.

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$dspFilter = New-Object System.Fabric.Health.DeployedServicePackageHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$daFilter =  New-Object System.Fabric.Health.DeployedApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter;NodeNameFilter="_Node_2"}
$daFilter.DeployedServicePackageFilters.Add($dspFilter)

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$appFilter.DeployedApplicationFilters.Add($daFilter)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)
Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 2
                               
                               ApplicationName       : fabric:/System
                               HealthState           : Ok
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : FAS
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
                               
                               
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : WordCountServicePkg
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
```

### <a name="rest"></a>REST
Você pode obter parte de integridade de cluster com um [solicitação GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) ou um [solicitação POST](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) que inclui políticas de integridade e descritos no corpo de saudação de filtros avançados.

## <a name="general-queries"></a>Consultas gerais
As consultas gerais retornam a lista de entidades do Service Fabric de um tipo especificado. Eles são expostos por meio da API de saudação (por meio de métodos de saudação em **FabricClient.QueryManager**), cmdlets do PowerShell e REST. Essas consultas agregam subconsultas de vários componentes. Um deles é hello [repositório de integridade](service-fabric-health-introduction.md#health-store), que preenche Olá agregado estado de integridade para cada resultado da consulta.  

> [!NOTE]
> Consultas gerais retornam Olá agregado estado de integridade da entidade hello e não contêm dados de integridade avançados. Se uma entidade não está íntegra, você pode acompanhar com integridade consultas tooget todas as suas informações de integridade, incluindo eventos, estados de integridade do filho e avaliações não íntegras.
>
>

Se consultas gerais retornam um estado de integridade desconhecido para uma entidade, é possível que repositório integridade Olá não tem dados completos sobre entidade hello. Também é possível que um repositório de integridade toohello subconsulta não foi bem-sucedida (por exemplo, ocorreu um erro de comunicação ou armazenamento de integridade Olá foi restringido). O acompanhamento com uma consulta de integridade de entidade hello. Se a subconsulta Olá encontrou erros transitórios, como problemas de rede, poderá ter êxito, esta consulta de acompanhamento. Ele pode também fornecer mais detalhes do repositório de integridade Olá sobre por que a entidade Olá não está exposta.

Olá consultas que contêm **HealthState** para entidades são:

* Lista de nós: retorna nós de lista de Olá Olá cluster (via paginada).
  * API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)
  * PowerShell: Get-ServiceFabricNode
* Lista de aplicativos: lista de saudação retorna de aplicativos em cluster hello (via paginada).
  * API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)
  * PowerShell: Get-ServiceFabricApplication
* Lista de serviços: lista de saudação do retorna de serviços em um aplicativo (via paginada).
  * API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)
  * PowerShell: Get-ServiceFabricService
* Lista de partição: lista de saudação retorna de partições em um serviço (via paginada).
  * API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)
  * PowerShell: Get-ServiceFabricPartition
* Lista de réplica: lista de saudação retorna das réplicas de uma partição (via paginada).
  * API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)
  * PowerShell: Get-ServiceFabricReplica
* Implantado a lista de aplicativos: lista de saudação retorna dos aplicativos implantados em um nó.
  * API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)
  * PowerShell: Get-ServiceFabricDeployedApplication
* Implantado a lista de pacotes de serviço: lista de saudação retorna de pacotes de serviço em um aplicativo implantado.
  * API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)
  * PowerShell: Get-ServiceFabricDeployedApplication

> [!NOTE]
> Algumas consultas Olá retornam resultados paginados. retorno dessas consultas Hello é uma lista derivada [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1). Se os resultados de saudação não se ajustar a uma mensagem, apenas uma página será retornada e um ContinuationToken que controla qual enumeração foi interrompida. Continue toocall Olá mesma consulta e passar o token de continuação Olá Olá anterior tooget próximos de resultados da consulta.
>
>

### <a name="examples"></a>Exemplos
Olá código a seguir obtém aplicativos problemáticos Olá no cluster hello:

```csharp
var applications = fabricClient.QueryManager.GetApplicationListAsync().Result.Where(
  app => app.HealthState == HealthState.Error);
```

Hello seguir obtém os detalhes do aplicativo hello para a malha de saudação: / aplicativo WordCount. Observe que o estado de integridade é de aviso.

```powershell
PS C:\> Get-ServiceFabricApplication -ApplicationName fabric:/WordCount

ApplicationName        : fabric:/WordCount
ApplicationTypeName    : WordCount
ApplicationTypeVersion : 1.0.0
ApplicationStatus      : Ready
HealthState            : Warning
ApplicationParameters  : { "WordCountWebService_InstanceCount" = "1";
                         "_WFDebugParams_" = "[{"ServiceManifestName":"WordCountWebServicePkg","CodePackageName":"Code","EntryPointType":"Main","Debug
                         ExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {74f7e5d5-71a9-47e2-a8cd-1878ec4734f1} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"},{"ServiceManifestName":"WordCountServicePkg","CodeP
                         ackageName":"Code","EntryPointType":"Main","DebugExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {2ab462e6-e0d1-4fda-a844-972f561fe751} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"}]" }
```

Olá, cmdlet a seguir obtém Olá serviços com um estado de integridade de erro:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplication | Get-ServiceFabricService | where {$_.HealthState -eq "Error"}


ServiceName            : fabric:/WordCount/WordCountService
ServiceKind            : Stateful
ServiceTypeName        : WordCountServiceType
IsServiceGroup         : False
ServiceManifestVersion : 1.0.0
HasPersistedState      : True
ServiceStatus          : Active
HealthState            : Error
```

## <a name="cluster-and-application-upgrades"></a>Atualização de cluster e aplicativo
Durante uma atualização monitorada do cluster hello e do aplicativo, o Service Fabric verifica tooensure de integridade que tudo permaneça íntegro. Se uma entidade não está íntegra, conforme avaliado usando políticas de integridade configurado, o upgrade Olá aplica próxima ação do políticas específicas de atualização toodetermine hello. atualização Olá pode ser pausado tooallow interação do usuário (como corrigir as condições de erro ou alteração de políticas), ou ele pode automaticamente reverter toohello versão anterior de BOM.

Durante uma *cluster* atualização, você pode obter o status de atualização de cluster hello. status de atualização de saudação inclui avaliações não íntegras, quais toowhat ponto não está íntegro no cluster hello. Se Olá atualização é revertida devido a problemas de toohealth, status da atualização Olá lembra motivos não íntegro do último hello. Essas informações podem ajudar os administradores a investigar o que deu errado atualização Olá revertida ou interrompido.

Da mesma forma, durante um *aplicativo* atualização, qualquer avaliações não íntegras estão contidas no status de atualização de aplicativo hello.

Hello a seguir mostra o status de atualização de aplicativo do Olá para uma malha modificada: / aplicativo WordCount. Um watchdog relatou um erro em uma de suas réplicas. atualização de Hello está sendo porque as verificações de integridade de saudação não for respeitadas.

```powershell
PS C:\> Get-ServiceFabricApplicationUpgrade fabric:/WordCount

ApplicationName               : fabric:/WordCount
ApplicationTypeName           : WordCount
TargetApplicationTypeVersion  : 1.0.0.0
ApplicationParameters         : {}
StartTimestampUtc             : 4/21/2017 5:23:26 PM
FailureTimestampUtc           : 4/21/2017 5:23:37 PM
FailureReason                 : HealthCheck
UpgradeState                  : RollingBackInProgress
UpgradeDuration               : 00:00:23
CurrentUpgradeDomainDuration  : 00:00:00
CurrentUpgradeDomainProgress  : UD1

                                NodeName            : _Node_1
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_2
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_3
                                UpgradePhase        : PreUpgradeSafetyCheck
                                PendingSafetyChecks :
                                EnsurePartitionQuorum - PartitionId: 30db5be6-4e20-4698-8185-4bd7ca744020
NextUpgradeDomain             : UD2
UpgradeDomainsStatus          : { "UD1" = "Completed";
                                "UD2" = "Pending";
                                "UD3" = "Pending";
                                "UD4" = "Pending" }
UnhealthyEvaluations          :
                                Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.

                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.

                                      Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                      Unhealthy partition: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b', AggregatedHealthState='Error'.

                                          Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.

                                          Unhealthy replica: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b',
                                  ReplicaOrInstanceId='131031502346844058', AggregatedHealthState='Error'.

                                              Error event: SourceId='DiskWatcher', Property='Disk'.

UpgradeKind                   : Rolling
RollingUpgradeMode            : UnmonitoredAuto
ForceRestart                  : False
UpgradeReplicaSetCheckTimeout : 00:15:00
```

Leia mais sobre Olá [atualização do aplicativo do Service Fabric](service-fabric-application-upgrade.md).

## <a name="use-health-evaluations-tootroubleshoot"></a>Usar tootroubleshoot de avaliações de integridade
Sempre que houver um problema com o cluster de saudação ou um aplicativo, examine Olá toopinpoint de integridade de cluster ou o aplicativo que está errado. avaliações não íntegras Olá fornecem detalhes sobre Olá disparada atual estado não íntegro. Se você precisar, você pode fazer drill down em filho não íntegros entidades tooidentify Olá causas.

Por exemplo, pense em um aplicativo não íntegro porque há um relatório de erros em uma de suas réplicas. Olá seguinte cmdlet do Powershell mostra avaliações não íntegras hello:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount -EventsFilter None -ServicesFilter None -DeployedApplicationsFilter None -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.
                                  
                                        Unhealthy replica: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', ReplicaOrInstanceId='131444422260002646', AggregatedHealthState='Error'.
                                  
                                            Error event: SourceId='MyWatchdog', Property='Memory'.
                                  
ServiceHealthStates             : None
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

Você pode examinar Olá réplica tooget obter mais informações:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricReplicaHealth -ReplicaOrInstanceId 131444422260002646 -PartitionId af2e3e44-a8f8-45ac-9f31-4093eb897600


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Error
UnhealthyEvaluations  : 
                        Error event: SourceId='MyWatchdog', Property='Memory'.
                        
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
                        SourceId              : MyWatchdog
                        Property              : Memory
                        HealthState           : Error
                        SequenceNumber        : 131444451657749403
                        SentAt                : 7/13/2017 6:46:05 PM
                        ReceivedAt            : 7/13/2017 6:46:05 PM
                        TTL                   : Infinite
                        Description           : 
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Warning->Error = 7/13/2017 6:46:05 PM, LastOk = 1/1/0001 12:00:00 AM
```

> [!NOTE]
> Olá, avaliações não íntegras Mostrar Olá primeiro motivo Olá entidade é avaliado toocurrent estado de integridade. Pode haver vários outros eventos que disparam esse estado, mas elas não são refletidas em avaliações de saudação. tooget obter mais informações, busca detalhada toofigure de entidades de integridade Olá todos os relatórios de não-íntegro Olá cluster hello.
>
>

## <a name="next-steps"></a>Próximas etapas
[Usar tootroubleshoot de relatórios de integridade do sistema](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[Adicionar relatórios de integridade personalizados do Service Fabric](service-fabric-report-health.md)

[Como tooreport e verificação de integridade do serviço](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[Monitorar e diagnosticar serviços localmente](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Atualização de aplicativos do Service Fabric](service-fabric-application-upgrade.md)
