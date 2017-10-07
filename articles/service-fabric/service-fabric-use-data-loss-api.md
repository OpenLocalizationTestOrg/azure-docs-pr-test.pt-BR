---
title: "aaaHow tooInvoke perda de dados nos serviços de malha do serviço | Microsoft Docs"
description: "Descreve como toouse Olá perda de dados api"
services: service-fabric
documentationcenter: .net
author: LMWF
manager: rsinha
editor: 
ms.assetid: f4e70f6f-cad9-4a3e-9655-009b4db09c6d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 09/19/2016
ms.author: lemai
redirect_url: /azure/service-fabric/service-fabric-testability-overview
ms.openlocfilehash: 014c7ebfd2c42d79a5fe1802ecc3fa0c1f26f9d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinvoke-data-loss-on-services"></a>Como tooInvoke perda de dados nos serviços
> [!WARNING]
> Este documento descreve como toocause perda de dados em seus serviços e deve ser usada com cuidado.
> 
> 

## <a name="introduction"></a>Introdução
Você pode invocar a perda de dados em uma partição do serviço do Service Fabric chamando StartPartitionDataLossAsync().  Essa api usa Olá injeção de falha e o serviço de análise tooperform Olá trabalho toocause dados perda condições.

## <a name="using-hello-fault-injection-and-analysis-service"></a>Usando o serviço de análise e Olá injeção de falha
Olá injeção de falha e o serviço de análise atualmente suporta Olá APIs no gráfico de saudação abaixo a seguir.  Olá direita do gráfico de saudação mostra Olá cmdlet do PowerShell correspondente.  Consulte toohello documentação do msdn sobre cada API para obter mais informações sobre cada um deles.

| API do C# | Cmdlet do PowerShell |
| --- | ---:|
| [StartPartitionDataLossAsync][dl] |[Start-ServiceFabricPartitionDataLoss][psdl] |
| [StartPartitionQuorumLossAsync][ql] |[Start-ServiceFabricPartitionQuorumLoss][psql] |
| [StartPartitionRestartAsync][rp] |[Start-ServiceFabricPartitionRestart][psrp] |

## <a name="conceptual-overview-of-running-a-command"></a>Visão geral conceitual de execução de um comando
Olá injeção de falha e o Analysis Services usa um modelo assíncrono onde iniciar Olá comando com uma API, chamado tooas hello "Start" API neste documento, e, em seguida, verificações de progresso Olá desse comando usando uma API de "GetProgress" até que ele atingiu um terminal estado, ou até que você cancele-o.
toostart um comando, chamada hello "Iniciar" API para API correspondente hello.  Essa API retorna quando hello injeção de falha e o serviço de análise aceitou a solicitação de saudação.  No entanto, ela não indica o quanto um comando foi executado, nem mesmo se ele já foi iniciado.  Em andamento toocheck da ordem de um comando, chame hello "GetProgress" que corresponde a API de "Início" toohello anteriormente chamada de API.  Olá "GetProgress" API retorna um objeto que indica o status atual de saudação do comando hello dentro de sua propriedade de estado.  Um comando é executado indefinidamente até:

1. Que seja concluído com êxito.  Se você chamar "GetProgress" nesse caso, estado do objeto de andamento Olá será concluído.
2. Que ele encontre um erro fatal.  Se você chamar "GetProgress" nesse caso, estado do objeto do hello andamento será interrompido.
3. Cancelá-lo por meio de saudação [CancelTestCommandAsync] [ cancel] API, ou [Stop ServiceFabricTestCommand] [ cancelps] cmdlet do PowerShell.  Se você chamar "GetProgress" nesse caso, hello estado do objeto de progresso será cancelado ou ForceCancelled, dependendo de uma API de toothat do argumento.  Consulte a documentação de saudação para [CancelTestCommandAsync] [ cancel] para obter mais detalhes.

## <a name="details-of-running-a-command"></a>Detalhes da execução de um comando
Em ordem toostart um comando, chame hello API iniciar com argumentos Olá esperado.  Todas as APIs Start têm um argumento GUID chamado operationId.  Você deve manter o controle de argumento de operationId hello, pois ele é usado tootrack andamento desse comando.  Isso deve ser passado para hello "GetProgress" API em andamento de tootrack de ordem do comando hello.  ID da operação Olá deve ser exclusivo.

Depois de chamar com êxito Olá API Iniciar, Olá GetProgress API deve ser chamado em um loop até que hello retornadas andamento propriedade de estado do objeto é concluída.  Todas as [FabricTransientException’s][fte] e OperationCanceledException’s devem ser recuperadas.
Quando o comando Olá atingiu um estado terminal (concluído, com falha ou cancelamento), Olá retornado de propriedade do resultado do objeto de andamento terá informações adicionais.  Se o estado de saudação for concluído, Result.SelectedPartition.PartitionId contém id de partição Olá que foi selecionado.  Result.Exception será nulo.  Se o estado de saudação está com defeito, Result.Exception terá Olá Olá do motivo injeção de falha e Analysis Services com defeito Olá comando.  Result.SelectedPartition.PartitionId tem uma id de partição Olá que foi selecionado.  Em algumas situações, comando Olá pode não ter continuavam suficiente toochoose uma partição.  Nesse caso, a saudação PartitionId será 0.  Se o estado de saudação é cancelado, Result.Exception será nulo.  Como Olá caso com falha, Result.SelectedPartition.PartitionId tem uma id de partição de saudação foi escolhido, mas se o comando Olá não tenha transcorrido suficiente toodo assim, ela será 0.  Consulte também toohello exemplo abaixo.

código de exemplo Hello abaixo mostra como toostart, em seguida, verificar o andamento em caso de perda de dados de toocause um comando em uma partição específica.

```csharp
    static async Task PerformDataLossSample()
    {
        // Create a unique operation id for hello command below
        Guid operationId = Guid.NewGuid();

        // Note: Use hello appropriate overload for your configuration
        FabricClient fabricClient = new FabricClient();

        // hello name of hello target service
        Uri targetServiceName = new Uri("fabric:/MyService");

        // hello id of hello target partition inside hello target service
        Guid targetPartitionId = new Guid("00000000-0000-0000-0000-000002233445");

        PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(targetServiceName, targetPartitionId);

        // Start hello command.  Retry OperationCanceledException and all FabricTransientException's.  Note when StartPartitionDataLossAsync completes
        // successfully it only means hello Fault Injection and Analysis Service has saved hello intent tooperform this work.  It does not say anything about hello progress
        // of hello command.
        while (true)
        {
            try
            {
                await fabricClient.TestManager.StartPartitionDataLossAsync(operationId, partitionSelector, DataLossMode.FullDataLoss).ConfigureAwait(false);
                break;
            }
            catch (OperationCanceledException)
            {
            }
            catch (FabricTransientException)
            {
            }

            await Task.Delay(TimeSpan.FromSeconds(1.0d)).ConfigureAwait(false);
        }

        PartitionDataLossProgress progress = null;

        // Poll hello progress using GetPartitionDataLossProgressAsync until it is either Completed or Faulted.  In this example, we're assuming
        // hello command won't be cancelled.        

        while (true)
        {
            try
            {
                progress = await fabricClient.TestManager.GetPartitionDataLossProgressAsync(operationId).ConfigureAwait(false);
            }
            catch (OperationCanceledException)
            {
                continue;
            }
            catch (FabricTransientException)
            {
                continue;
            }

            if (progress.State == TestCommandProgressState.Completed)
            {
                Console.WriteLine("Command '{0}' completed successfully", operationId);

                // In a terminal state .Result.SelectedPartition.PartitionId will have hello chosen partition
                Console.WriteLine("  Printing selected partition='{0}'", progress.Result.SelectedPartition.PartitionId);
                break;
            }
            else if (progress.State == TestCommandProgressState.Faulted)
            {
                // If State is Faulted, hello progress object's Result property's Exception property will have hello reason why.
                Console.WriteLine("Command '{0}' failed with '{1}'", operationId, progress.Result.Exception);
                break;
            }
            else
            {
                Console.WriteLine("Command '{0}' is currently Running", operationId);
            }

            await Task.Delay(TimeSpan.FromSeconds(5.0d)).ConfigureAwait(false);
        }
    }
```

exemplo Hello abaixo mostra como toouse Olá PartitionSelector toochoose uma partição aleatória de um serviço especificado:

```csharp
    static async Task PerformDataLossUseSelectorSample()
    {
        // Create a unique operation id for hello command below
        Guid operationId = Guid.NewGuid();

        // Note: Use hello appropriate overload for your configuration
        FabricClient fabricClient = new FabricClient();

        // hello name of hello target service
        Uri targetServiceName = new Uri("fabric:/SampleService ");

        // Use a PartitionSelector that will have hello Fault Injection and Analysis Service choose a random partition of “targetServiceName”
        PartitionSelector partitionSelector = PartitionSelector.RandomOf(targetServiceName);

        // Start hello command.  Retry OperationCanceledException and all FabricTransientException's.  Note when StartPartitionDataLossAsync completes
        // successfully it only means hello Fault Injection and Analysis Service has saved hello intent tooperform this work.  It does not say anything about hello progress
        // of hello command.
        while (true)
        {
            try
            {
                await fabricClient.TestManager.StartPartitionDataLossAsync(operationId, partitionSelector, DataLossMode.FullDataLoss).ConfigureAwait(false);
                break;
            }
            catch (OperationCanceledException)
            {
            }
            catch (FabricTransientException)
            {
            }
            catch (Exception e)
            {
                Console.WriteLine("Unexpected exception '{0}'", e);
                throw;
            }

            await Task.Delay(TimeSpan.FromSeconds(1.0d)).ConfigureAwait(false);
        }

        PartitionDataLossProgress progress = null;

        // Poll hello progress using GetPartitionDataLossProgressAsync until it is either Completed or Faulted.  In this example, we're assuming
        // hello command won't be cancelled.

        while (true)
        {
            try
            {
                progress = await fabricClient.TestManager.GetPartitionDataLossProgressAsync(operationId).ConfigureAwait(false);
            }
            catch (OperationCanceledException)
            {
                continue;
            }
            catch (FabricTransientException)
            {
                continue;
            }

            if (progress.State == TestCommandProgressState.Completed)
            {
                Console.WriteLine("Command '{0}' completed successfully", operationId);

                Console.WriteLine("Printing progress.Result:");
                Console.WriteLine("  Printing selected partition='{0}'", progress.Result.SelectedPartition.PartitionId);

                break;
            }
            else if (progress.State == TestCommandProgressState.Faulted)
            {
                // If State is Faulted, hello progress object's Result property's Exception property will have hello reason why.
                Console.WriteLine("Command '{0}' failed with '{1}', SelectedPartition {2}", operationId, progress.Result.Exception, progress.Result.SelectedPartition);
                break;
            }
            else
            {
                Console.WriteLine("Command '{0}' is currently Running", operationId);
            }

            await Task.Delay(TimeSpan.FromSeconds(1.0d)).ConfigureAwait(false);
        }
    }
```

## <a name="history-and-truncation"></a>Histórico e truncamento
Depois que um comando atingir um estado terminal, seus metadados permanecem no hello injeção de falha e serviço de análise para uma determinada hora, antes de ser removido toosave espaço.  Se "GetProgress" for chamado usando Olá ID da operação de um comando após ele ter sido removido, ele retornará um FabricException com um código de erro de KeyNotFound.

[dl]: https://msdn.microsoft.com/library/azure/mt693569.aspx
[ql]: https://msdn.microsoft.com/library/azure/mt693558.aspx
[rp]: https://msdn.microsoft.com/library/azure/mt645056.aspx
[psdl]: https://msdn.microsoft.com/library/mt697573.aspx
[psql]: https://msdn.microsoft.com/library/mt697557.aspx
[psrp]: https://msdn.microsoft.com/library/mt697560.aspx
[cancel]: https://msdn.microsoft.com/library/azure/mt668910.aspx
[cancelps]: https://msdn.microsoft.com/library/mt697566.aspx
[fte]: https://msdn.microsoft.com/library/azure/system.fabric.fabrictransientexception.aspx
