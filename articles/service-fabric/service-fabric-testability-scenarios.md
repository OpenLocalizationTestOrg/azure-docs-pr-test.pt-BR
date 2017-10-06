---
title: testes de aaaCreate caos e failover para o Azure microservices | Microsoft Docs
description: "Usando Olá Service Fabric failover e teste de caos falhas de tooinduce de cenários de teste e verifique se confiabilidade Olá dos seus serviços."
services: service-fabric
documentationcenter: .net
author: motanv
manager: rsinha
editor: toddabel
ms.assetid: 8eee7e89-404a-4605-8f00-7e4d4fb17553
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: motanv
ms.openlocfilehash: 1cac4f9e0e4a6c8416d5220d1537b5110decd1f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="testability-scenarios"></a>Cenários da possibilidade de teste
Sistemas grandes distribuídos como infraestruturas de nuvem não são confiáveis por natureza. Azure Service Fabric oferece aos desenvolvedores Olá capacidade toowrite serviços toorun sobre infraestruturas não confiáveis. Em serviços de alta qualidade toowrite ordem, os desenvolvedores precisam tooinduce capaz de toobe tal estabilidade de saudação tootest infraestrutura confiável de seus serviços.

Olá falhas Analysis Services oferece aos desenvolvedores serviços tootest ações de falhas do hello capacidade tooinduce na presença de saudação de falhas. No entanto, falhas simuladas direcionadas não o levarão tão longe. Olá tootake testes Além disso, você pode usar os cenários de teste de saudação do Service Fabric: um caos de teste e um teste de failover. Esses cenários simular contínuas falhas intercaladas normais e anormais em todo o cluster Olá por longos períodos de tempo. Após um teste está configurado com taxa de saudação e tipo de falhas, ele pode ser iniciado por meio de APIs de c# ou PowerShell, toogenerate falhas no cluster hello e seu serviço.

> [!WARNING]
> ChaosTestScenario está sendo substituído por um Chaos baseado em serviço mais resiliente. Consulte o artigo novo toohello [controlados caos](service-fabric-controlled-chaos.md) para obter mais detalhes.
> 
> 

## <a name="chaos-test"></a>Teste de caos
cenário de caos Hello gera falhas em cluster do Service Fabric inteira de saudação. cenário de saudação compacta falhas geralmente vistas em meses ou anos tooa algumas horas. combinação de saudação de falhas intercaladas com taxa de falhas de alta Olá encontra casos de canto que são perdidos caso contrário. Isso leva a melhoria significativa tooa na qualidade do código de saudação do serviço de saudação.

### <a name="faults-simulated-in-hello-chaos-test"></a>Falhas simuladas no teste de caos Olá
* Reiniciar um nó
* Reiniciar um pacote de códigos implantado
* Remover uma réplica
* Reiniciar uma réplica
* Mover uma réplica primária (opcional)
* Mover uma réplica secundária (opcional)

teste de caos Olá executa várias iterações de falhas e validações de cluster de saudação especificado o período de tempo. Olá tempo para Olá cluster toostabilize e validação toosucceed também é configurável. cenário de saudação falha quando você atinge uma única falha na validação de cluster.

Por exemplo, considere que um teste definido toorun por uma hora com um máximo de três falhas simultâneas. teste de saudação induzir três falhas e validar a integridade do cluster hello. teste Olá irá iterar por meio da etapa anterior Olá até que o cluster de saudação se tornará não íntegro ou passa de uma hora. Se o cluster de saudação se tornará não íntegro em qualquer iteração, ou seja, não estável dentro de um tempo configurado, Olá teste falha com uma exceção. Essa exceção indica que algo deu errado e precisa de mais investigação.

Em sua forma atual, mecanismo de geração Olá falha no teste de caos Olá induz falhas apenas seguras. Isso significa que na ausência de saudação de falhas externas, uma quorum ou perda de dados nunca ocorrerão.

### <a name="important-configuration-options"></a>Opções de configuração importantes
* **TimeToRun**: tempo Total de teste Olá será executado antes de concluir com êxito. teste de saudação pode concluir anterior em vez de uma falha de validação.
* **MaxClusterStabilizationTimeout**: quantidade máxima de tempo toowait para Olá cluster toobecome Íntegro antes da falha de teste de saudação. Hello verificações executadas são se a integridade do cluster é Okey, a integridade do serviço é Okey, hello tamanho do conjunto de réplica de destino é obtido para partição de serviço hello e nenhum réplicas InBuild existem.
* **MaxConcurrentFaults**: número máximo de falhas simultâneas induzidas em cada iteração. Olá número mais alto de hello, Olá mais agressiva teste hello, portanto, resultando em failovers mais complexas e combinações de transição. teste de saudação garante que na ausência de falhas externas não haverá uma perda de quorum ou os dados, independentemente de quão alto essa configuração é.
* **EnableMoveReplicaFaults**: habilita ou desabilita a falhas de saudação que estão causando mover Olá Olá réplicas primárias ou secundárias. Essas falhas estão desabilitadas por padrão.
* **WaitTimeBetweenIterations**: quantidade de tempo toowait entre as iterações, ou seja, depois uma rodada de falhas e validação correspondente.

### <a name="how-toorun-hello-chaos-test"></a>Como testar caos de saudação toorun
Exemplo de C#

```csharp
using System;
using System.Fabric;
using System.Fabric.Testability.Scenario;
using System.Threading;
using System.Threading.Tasks;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";

        Console.WriteLine("Starting Chaos Test Scenario...");
        try
        {
            RunChaosTestScenarioAsync(clusterConnection).Wait();
        }
        catch (AggregateException ae)
        {
            Console.WriteLine("Chaos Test Scenario did not complete: ");
            foreach (Exception ex in ae.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("Chaos Test Scenario completed.");
        return 0;
    }

    static async Task RunChaosTestScenarioAsync(string clusterConnection)
    {
        TimeSpan maxClusterStabilizationTimeout = TimeSpan.FromSeconds(180);
        uint maxConcurrentFaults = 3;
        bool enableMoveReplicaFaults = true;

        // Create FabricClient with connection and security information here.
        FabricClient fabricClient = new FabricClient(clusterConnection);

        // hello chaos test scenario should run at least 60 minutes or until it fails.
        TimeSpan timeToRun = TimeSpan.FromMinutes(60);
        ChaosTestScenarioParameters scenarioParameters = new ChaosTestScenarioParameters(
          maxClusterStabilizationTimeout,
          maxConcurrentFaults,
          enableMoveReplicaFaults,
          timeToRun);

        // Other related parameters:
        // Pause between two iterations for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenIterations = TimeSpan.FromSeconds(30);
        // Pause between concurrent actions for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenFaults = TimeSpan.FromSeconds(10);

        // Create hello scenario class and execute it asynchronously.
        ChaosTestScenario chaosScenario = new ChaosTestScenario(fabricClient, scenarioParameters);

        try
        {
            await chaosScenario.ExecuteAsync(CancellationToken.None);
        }
        catch (AggregateException ae)
        {
            throw ae.InnerException;
        }
    }
}
```

PowerShell

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```


## <a name="failover-test"></a>Teste de failover
cenário de teste de failover de saudação é uma versão do cenário de teste de caos Olá que tem como alvo uma partição de serviço específico. Ele testa o efeito de saudação de failover em uma partição de serviço específico, deixando Olá outros serviços afetados. Depois que ele é configurado com informações de partição de destino hello e outros parâmetros, ele é executado como uma ferramenta de cliente que usa APIs do c# ou PowerShell falhas de toogenerate para uma partição de serviço. cenário Olá itera por meio de uma sequência de falhas simuladas e validação de serviço, enquanto a lógica de negócios é executado no hello lado tooprovide uma carga de trabalho. Uma falha na validação do serviço indica um problema que precisa de mais investigação.

### <a name="faults-simulated-in-hello-failover-test"></a>Falhas simuladas no teste de failover Olá
* Reiniciar um pacote de código implantado onde a partição hello está hospedada
* Remover uma réplica primária/secundária ou uma instância sem estado
* Reiniciar uma réplica primária secundária (se o serviço persistir)
* Mover uma réplica primária
* Mover uma réplica secundária
* Reinicie a partição Olá

teste de failover Olá induzir a uma falha escolhida e executa validação no hello serviço tooensure sua estabilidade. teste de failover Olá induz somente uma falha em uma hora, como contrário toopossible várias falhas no teste de caos hello. Se a partição de serviço Olá não estabilizar no tempo limite de saudação configurada após cada falha, o teste de saudação falhará. teste de saudação induz somente falhas de seguras. Isso significa que, na ausência de falhas externas, não ocorre uma perda de quorum ou dados.

### <a name="important-configuration-options"></a>Opções de configuração importantes
* **PartitionSelector**: objeto de seletor que especifica a partição de saudação que precisa toobe direcionado.
* **TimeToRun**: tempo Total de teste Olá será executado antes de concluir.
* **MaxServiceStabilizationTimeout**: quantidade máxima de tempo toowait para Olá cluster toobecome Íntegro antes da falha de teste de saudação. Hello verificações executadas são se a integridade do serviço é Okey, hello tamanho do conjunto de réplica de destino é obtido para todas as partições e nenhum réplicas InBuild existem.
* **WaitTimeBetweenFaults**: quantidade de tempo toowait entre cada ciclo de falha e validação.

### <a name="how-toorun-hello-failover-test"></a>Como testar o failover de saudação toorun
**C#**

```csharp
using System;
using System.Fabric;
using System.Fabric.Testability.Scenario;
using System.Threading;
using System.Threading.Tasks;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";
        Uri serviceName = new Uri("fabric:/samples/PersistentToDoListApp/PersistentToDoListService");

        Console.WriteLine("Starting Chaos Test Scenario...");
        try
        {
            RunFailoverTestScenarioAsync(clusterConnection, serviceName).Wait();
        }
        catch (AggregateException ae)
        {
            Console.WriteLine("Chaos Test Scenario did not complete: ");
            foreach (Exception ex in ae.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("Chaos Test Scenario completed.");
        return 0;
    }

    static async Task RunFailoverTestScenarioAsync(string clusterConnection, Uri serviceName)
    {
        TimeSpan maxServiceStabilizationTimeout = TimeSpan.FromSeconds(180);
        PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);

        // Create FabricClient with connection and security information here.
        FabricClient fabricClient = new FabricClient(clusterConnection);

        // hello chaos test scenario should run at least 60 minutes or until it fails.
        TimeSpan timeToRun = TimeSpan.FromMinutes(60);
        FailoverTestScenarioParameters scenarioParameters = new FailoverTestScenarioParameters(
          randomPartitionSelector,
          timeToRun,
          maxServiceStabilizationTimeout);

        // Other related parameters:
        // Pause between two iterations for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenIterations = TimeSpan.FromSeconds(30);
        // Pause between concurrent actions for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenFaults = TimeSpan.FromSeconds(10);

        // Create hello scenario class and execute it asynchronously.
        FailoverTestScenario failoverScenario = new FailoverTestScenario(fabricClient, scenarioParameters);

        try
        {
            await failoverScenario.ExecuteAsync(CancellationToken.None);
        }
        catch (AggregateException ae)
        {
            throw ae.InnerException;
        }
    }
}
```


**PowerShell**

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/SampleApp/SampleService"

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindSingleton
```
