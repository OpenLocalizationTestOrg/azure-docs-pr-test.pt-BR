---
title: falhas de aaaSimulate em microservices do Azure | Microsoft Docs
description: "Este artigo fala sobre ações de capacidade de teste de saudação encontradas no Microsoft Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: motanv
manager: timlt
editor: toddabel
ms.assetid: ed53ca5c-4d5e-4b48-93c9-e386f32d8b7a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: motanv;heeldin
ms.openlocfilehash: 5bdda1c0c5a40b243ab956c4791afd52e11c4089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="testability-actions"></a>Ações da Possibilidade de Teste
Em ordem toosimulate uma infraestrutura não confiável, Azure Service Fabric fornece, desenvolvedor hello, com modos toosimulate várias falhas do mundo real e as transições de estado. Elas são expostas como ações de possibilidade de teste. ações de saudação são Olá APIs de baixo nível que causam uma injeção de falha específico, a transição de estado ou a validação. Ao combinar essas ações, você pode criar cenários de teste abrangentes para seus serviços.

O Service Fabric fornece alguns cenários comuns de teste compostos por essas ações. É altamente recomendável que você utiliza esses cenários internos, que são escolhidos com cuidado as transições de estado comum tootest e casos de falha. No entanto, as ações podem ser cenários de teste personalizada toocreate usado quando você desejar tooadd cobertura para cenários que não são cobertas por cenários internos Olá ainda ou que são personalizados personalizadas para seu aplicativo.

C# implementações das ações de saudação são encontradas em Olá System.Fabric.dll assembly. módulo do PowerShell de malha do sistema Olá encontra-se em Olá Microsoft.ServiceFabric.Powershell.dll assembly. Como parte da instalação do tempo de execução, Olá módulo ServiceFabric do PowerShell é instalado tooallow para facilidade de uso.

## <a name="graceful-vs-ungraceful-fault-actions"></a>Ações de falha normais x anormais
As ações da Possibilidade de Teste são classificadas em dois blocos principais:

* Falhas anormais: simulam falhas como reinicializações de máquina e panes de processo. No caso de falhas, o contexto de execução de saudação do processo para abruptamente. Isso significa que nenhuma limpeza do estado de saudação pode ser executado antes que o aplicativo hello for iniciado novamente.
* Falhas normais: simulam ações normais como movimentações de réplica e remoções acionadas pelo balanceamento de carga. Nesses casos, o serviço de saudação recebe uma notificação de saudação fechar e pode limpar o estado de saudação antes de sair.

Para validação de melhor qualidade, executar o serviço de saudação e carga de trabalho de negócios ao induzindo várias falhas normais e anormais. Falhas anormais exercitam cenários em que o processo de serviço Olá abruptamente encerrada no meio de saudação de fluxos de trabalho. Isso testa o caminho de recuperação hello quando réplicas do serviço Olá for restaurada pela malha do serviço. Isso ajudará a consistência dos dados e se o estado do serviço Olá é mantido corretamente após falhas de teste. Hello outro conjunto de falhas (saudação normal de falhas) de teste que o serviço Olá reage corretamente tooreplicas seja movido pela malha do serviço. Isso testa o tratamento de cancelamento no método de RunAsync hello. serviço de saudação precisa toocheck Olá cancelamento token que está sendo definido corretamente salvar seu estado e sair do método de RunAsync hello.

## <a name="testability-actions-list"></a>Lista de ações da Possibilidade de Teste
| Ação | Descrição | API gerenciada | Cmdlet do Powershell | Falhas normais/anormais |
| --- | --- | --- | --- | --- |
| CleanTestState |Remove todos os estados de teste de saudação do cluster Olá no caso de um desligamento incorreto do driver de teste de saudação. |CleanTestStateAsync |Remove-ServiceFabricTestState |Não aplicável |
| InvokeDataLoss |Induz a perda de dados em uma partição de serviço. |InvokeDataLossAsync |Invoke-ServiceFabricPartitionDataLoss |Normal |
| InvokeQuorumLoss |Coloca uma determinada partição de serviço com estado na perda de quórum. |InvokeQuorumLossAsync |Invoke-ServiceFabricQuorumLoss |Normal |
| Mover primária |Olá move especificado a réplica primária de um nó de cluster especificado toohello serviço com monitoração de estado. |MovePrimaryAsync |Move-ServiceFabricPrimaryReplica |Normal |
| Mover secundária |Move a réplica secundária atual de saudação de um nó de cluster diferente de tooa de serviço com monitoração de estado. |MoveSecondaryAsync |Move-ServiceFabricSecondaryReplica |Normal |
| RemoveReplica |Simula uma falha de réplica removendo uma réplica de um cluster. Isso fechará réplica hello e mudará toorole 'None', removendo todos os seus estados de cluster hello. |RemoveReplicaAsync |Remove-ServiceFabricReplica |Normal |
| RestartDeployedCodePackage |Simula uma falha de processo do pacote de códigos reiniciando um pacote de códigos implantado em um nó em um cluster. Isso anula o processo de pacote de código hello, que irá reiniciar todas as réplicas de serviço do usuário Olá hospedadas no processo. |RestartDeployedCodePackageAsync |Restart-ServiceFabricDeployedCodePackage |Anormais |
| RestartNode |Simula uma falha de nó de cluster da Malha de Serviço reinicializando um nó. |RestartNodeAsync |Restart-ServiceFabricNode |Anormais |
| RestartPartition |Simula um cenário de blecaute do datacenter ou cluster reiniciando algumas ou todas as réplicas de uma partição. |RestartPartitionAsync |Restart-ServiceFabricPartition |Normal |
| RestartReplica |Simule uma falha de réplica reiniciando uma réplica persistente em um cluster, fechando réplica hello e, em seguida, abri-la. |RestartReplicaAsync |Restart-ServiceFabricReplica |Normal |
| StartNode |Inicia um nó em um cluster que já foi interrompido. |StartNodeAsync |Start-ServiceFabricNode |Não aplicável |
| StopNode |Simula uma falha de nó interrompendo um nó em um cluster. nó de saudação permanecerá inativo até StartNode é chamado. |StopNodeAsync |Stop-ServiceFabricNode |Anormais |
| ValidateApplication |Valida a disponibilidade de saudação e a integridade de todos os serviços do Service Fabric dentro de um aplicativo, geralmente após induzindo algumas falhas no sistema de saudação. |ValidateApplicationAsync |Test-ServiceFabricApplication |Não aplicável |
| ValidateService |Valida a disponibilidade hello e a integridade de um serviço de malha do serviço, geralmente após induzindo algumas falhas no sistema de saudação. |ValidateServiceAsync |Test-ServiceFabricService |Não aplicável |

## <a name="running-a-testability-action-using-powershell"></a>Executando uma ação de possibilidade de teste usando o PowerShell
Este tutorial mostra como toorun uma ação de capacidade de teste usando o PowerShell. Você aprenderá como toorun uma ação de capacidade de teste em um cluster (caixa) local ou em um cluster do Azure. Microsoft.Fabric.Powershell.dll – hello módulo PowerShell do Service Fabric – é instalado automaticamente quando você instala o hello MSI do Microsoft Service Fabric. módulo Olá é carregado automaticamente quando você abrir um prompt do PowerShell.

Segmentos do tutorial:

* [Executar uma ação em um cluster one-box](#run-an-action-against-a-one-box-cluster)
* [Executar uma ação em um cluster do Azure](#run-an-action-against-an-azure-cluster)

### <a name="run-an-action-against-a-one-box-cluster"></a>Executar uma ação em um cluster one-box
toorun uma ação de capacidade de teste em um cluster local, conecte-se primeiro toohello cluster e o prompt do PowerShell Olá aberto no modo de administrador. Vamos dar uma olhada em Olá **ServiceFabricNode reinicialização** ação.

```powershell
Restart-ServiceFabricNode -NodeName Node1 -CompletionMode DoNotVerify
```

Olá aqui ação **ServiceFabricNode reinicialização** está sendo executado em um nó denominado "Node1". modo de conclusão de saudação especifica que ele não deve verificar se ação de reinicialização do nó Olá teve êxito realmente. Modo de preenchimento Olá especificando como "Verificar" fará com que ele tooverify se a ação de reinicialização Olá foi bem-sucedida. Em vez de especificar diretamente o nó Olá por seu nome, você pode especificá-lo por meio de um tipo de chave e hello de partição da réplica, da seguinte maneira:

```powershell
Restart-ServiceFabricNode -ReplicaKindPrimary  -PartitionKindNamed -PartitionKey Partition3 -CompletionMode Verify
```


```powershell
$connection = "localhost:19000"
$nodeName = "Node1"

Connect-ServiceFabricCluster $connection
Restart-ServiceFabricNode -NodeName $nodeName -CompletionMode DoNotVerify
```

**Reinicialização ServiceFabricNode** deve ser usado toorestart um nó de malha do serviço em um cluster. Isso interromperá o processo de Fabric.exe hello, que irá reiniciar todas Olá system service e o usuário serviço réplicas hospedadas naquele nó. Usando essa API tootest seu serviço ajuda a revelar bugs em caminhos de recuperação de failover de saudação. Ele ajuda a simular falhas de nó no cluster hello.

Olá, seguinte captura de tela mostra Olá **ServiceFabricNode reinicialização** comando de capacidade de teste em ação.

![](media/service-fabric-testability-actions/Restart-ServiceFabricNode.png)

saudação de saída de hello primeiro **Get-ServiceFabricNode** (um cmdlet do módulo do PowerShell do Service Fabric Olá) mostra o cluster local Olá tem cinco nós: Node.1 tooNode.5. Após a ação de capacidade de teste de saudação (cmdlet) **ServiceFabricNode reinicialização** é executado no nó hello, denominado Node.4, podemos ver tempo de atividade do nó Olá foi redefinido.

### <a name="run-an-action-against-an-azure-cluster"></a>Executar uma ação em um cluster do Azure
Executar uma ação de capacidade de teste (usando o PowerShell) em um cluster do Azure é a ação de saudação de toorunning semelhante em um cluster local. Olá somente a diferença é que, antes de executar a ação de hello, em vez de conectar toohello de cluster local, você precisa tooconnect toohello Azure cluster primeiro.

## <a name="running-a-testability-action-using-c35"></a>Executando uma ação de possibilidade de teste usando o C&#35;
toorun uma ação de capacidade de teste usando c#, primeiro é necessário tooconnect toohello cluster usando FabricClient. Em seguida, obter Olá parâmetros necessários toorun Olá ação. Parâmetros diferentes podem ser usados toorun Olá a mesma ação.
Olhando Olá RestartServiceFabricNode ação, toorun unidirecional usando informações de nó da saudação (nome de nó e ID de instância do nó) no cluster hello.

```csharp
RestartNodeAsync(nodeName, nodeInstanceId, completeMode, operationTimeout, CancellationToken.None)
```

Explicação do parâmetro:

* **CompleteMode** Especifica que o modo de saudação não deve verificar se ação de reinicialização Olá teve êxito realmente. Modo de preenchimento Olá especificando como "Verificar" fará com que ele tooverify se a ação de reinicialização Olá foi bem-sucedida.  
* **OperationTimeout** conjuntos Olá quantidade de tempo da saudação operação toofinish antes de uma exceção TimeoutException é lançada.
* **CancellationToken** permite que um toobe pendente chamada cancelada.

Em vez de especificar diretamente o nó Olá por seu nome, você pode especificar isso por meio de um tipo de chave e hello de partição de réplica.

Para obter mais informações, consulte [PartitionSelector e ReplicaSelector](#partition_replica_selector).

```csharp
// Add a reference tooSystem.Fabric.Testability.dll and System.Fabric.dll
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Fabric.Testability;
using System.Fabric;
using System.Threading;
using System.Numerics;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";
        Uri serviceName = new Uri("fabric:/samples/PersistentToDoListApp/PersistentToDoListService");
        string nodeName = "N0040";
        BigInteger nodeInstanceId = 130743013389060139;

        Console.WriteLine("Starting RestartNode test");
        try
        {
            //Restart hello node by using ReplicaSelector
            RestartNodeAsync(clusterConnection, serviceName).Wait();

            //Another way toorestart node is by using nodeName and nodeInstanceId
            RestartNodeAsync(clusterConnection, nodeName, nodeInstanceId).Wait();
        }
        catch (AggregateException exAgg)
        {
            Console.WriteLine("RestartNode did not complete: ");
            foreach (Exception ex in exAgg.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("RestartNode completed.");
        return 0;
    }

    static async Task RestartNodeAsync(string clusterConnection, Uri serviceName)
    {
        PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);
        ReplicaSelector primaryofReplicaSelector = ReplicaSelector.PrimaryOf(randomPartitionSelector);

        // Create FabricClient with connection and security information here
        FabricClient fabricclient = new FabricClient(clusterConnection);
        await fabricclient.FaultManager.RestartNodeAsync(primaryofReplicaSelector, CompletionMode.Verify);
    }

    static async Task RestartNodeAsync(string clusterConnection, string nodeName, BigInteger nodeInstanceId)
    {
        // Create FabricClient with connection and security information here
        FabricClient fabricclient = new FabricClient(clusterConnection);
        await fabricclient.FaultManager.RestartNodeAsync(nodeName, nodeInstanceId, CompletionMode.Verify);
    }
}
```

## <a name="partitionselector-and-replicaselector"></a>PartitionSelector e ReplicaSelector
### <a name="partitionselector"></a>PartitionSelector
PartitionSelector é um auxiliar exposto na capacidade de teste e é tooselect usado uma determinada partição no qual tooperform qualquer uma das ações de capacidade de teste de saudação. Pode ser usado tooselect uma partição específica se a ID de partição Olá é conhecido com antecedência. Ou, você pode fornecer a chave de partição hello e operação Olá resolverá o ID de partição Olá internamente. Você também tem a opção de saudação do selecionando uma partição aleatória.

toouse este auxiliar, criar hello PartitionSelector objeto e selecione partição hello usando um dos métodos de saudação Select *. Em seguida, passe Olá PartitionSelector objeto toohello API que exija isso. Se nenhuma opção for selecionada, será padronizado partição aleatória tooa.

```csharp
Uri serviceName = new Uri("fabric:/samples/InMemoryToDoListApp/InMemoryToDoListService");
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
string partitionName = "Partition1";
Int64 partitionKeyUniformInt64 = 1;

// Select a random partition
PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);

// Select a partition based on ID
PartitionSelector partitionSelectorById = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);

// Select a partition based on name
PartitionSelector namedPartitionSelector = PartitionSelector.PartitionKeyOf(serviceName, partitionName);

// Select a partition based on partition key
PartitionSelector uniformIntPartitionSelector = PartitionSelector.PartitionKeyOf(serviceName, partitionKeyUniformInt64);
```

### <a name="replicaselector"></a>ReplicaSelector
ReplicaSelector é um auxiliar exposto na capacidade de teste e é usado toohelp selecione uma réplica na qual tooperform qualquer uma das ações de capacidade de teste de saudação. Pode ser usado tooselect uma réplica específica se a ID da réplica Olá é conhecido com antecedência. Além disso, você tem opção de saudação da seleção de uma réplica primária ou um secundário aleatório. ReplicaSelector deriva PartitionSelector, portanto, você precisa tooselect ambos Olá hello e réplica de partição no qual você deseja tooperform operação de capacidade de teste de saudação.

toouse este auxiliar, crie um objeto de ReplicaSelector e definido como Olá desejar partição de réplica e Olá Olá tooselect. Você pode passá-lo em Olá API que exija isso. Se nenhuma opção for selecionada, o padrão é réplica aleatório tooa e partição aleatória.

```csharp
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);
long replicaId = 130559876481875498;

// Select a random replica
ReplicaSelector randomReplicaSelector = ReplicaSelector.RandomOf(partitionSelector);

// Select hello primary replica
ReplicaSelector primaryReplicaSelector = ReplicaSelector.PrimaryOf(partitionSelector);

// Select hello replica by ID
ReplicaSelector replicaByIdSelector = ReplicaSelector.ReplicaIdOf(partitionSelector, replicaId);

// Select a random secondary replica
ReplicaSelector secondaryReplicaSelector = ReplicaSelector.RandomSecondaryOf(partitionSelector);
```

## <a name="next-steps"></a>Próximas etapas
* [Cenários da possibilidade de teste](service-fabric-testability-scenarios.md)
* Como tootest seu serviço
  * [Simular falhas durante cargas de trabalho de serviço](service-fabric-testability-workload-tests.md)
  * [Falhas de comunicação entre serviços](service-fabric-testability-scenarios-service-communication.md)

