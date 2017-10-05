---
title: "Criar testes de caos e failover para os microsserviços do Azure | Microsoft Docs"
description: "Usando os cenários de testes de caos e failover do Service Fabric para induzir falhas e verificar a confiabilidade de seus serviços."
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
ms.openlocfilehash: d06026c750e01ad5825338a78d9af331265f434a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="testability-scenarios"></a><span data-ttu-id="04000-103">Cenários da possibilidade de teste</span><span class="sxs-lookup"><span data-stu-id="04000-103">Testability scenarios</span></span>
<span data-ttu-id="04000-104">Sistemas grandes distribuídos como infraestruturas de nuvem não são confiáveis por natureza.</span><span class="sxs-lookup"><span data-stu-id="04000-104">Large distributed systems like cloud infrastructures are inherently unreliable.</span></span> <span data-ttu-id="04000-105">O Service Fabric do Azure permite aos desenvolvedores gravar os serviços para serem executados em infraestruturas não confiáveis.</span><span class="sxs-lookup"><span data-stu-id="04000-105">Azure Service Fabric gives developers the ability to write services to run on top of unreliable infrastructures.</span></span> <span data-ttu-id="04000-106">Para gravar serviços de alta qualidade, os desenvolvedores precisam ser capazes de induzir essa infraestrutura não confiável a testar a estabilidade dos seus serviços.</span><span class="sxs-lookup"><span data-stu-id="04000-106">In order to write high-quality services, developers need to be able to induce such unreliable infrastructure to test the stability of their services.</span></span>

<span data-ttu-id="04000-107">O serviço Análise de Falhas fornece aos desenvolvedores a capacidade de induzir ações de falha para testar serviços em caso de falhas.</span><span class="sxs-lookup"><span data-stu-id="04000-107">The Fault Analysis Service gives developers the ability to induce fault actions to test services in the presence of failures.</span></span> <span data-ttu-id="04000-108">No entanto, falhas simuladas direcionadas não o levarão tão longe.</span><span class="sxs-lookup"><span data-stu-id="04000-108">However, targeted simulated faults will get you only so far.</span></span> <span data-ttu-id="04000-109">Para fazer mais testes, você pode usar os cenários de teste no Service Fabric: um teste de caos e um de failover.</span><span class="sxs-lookup"><span data-stu-id="04000-109">To take the testing further, you can use the test scenarios in Service Fabric: a chaos test and a failover test.</span></span> <span data-ttu-id="04000-110">Esses cenários simulam falhas intercaladas contínuas, amigáveis e não amigáveis, em todo o cluster por longos períodos de tempo.</span><span class="sxs-lookup"><span data-stu-id="04000-110">These scenarios simulate continuous interleaved faults, both graceful and ungraceful, throughout the cluster over extended periods of time.</span></span> <span data-ttu-id="04000-111">Quando um teste é configurado com a taxa e o tipo de falha, ele pode ser iniciado por meio de APIs do C# ou do PowerShell para gerar falhas no cluster e no serviço.</span><span class="sxs-lookup"><span data-stu-id="04000-111">Once a test is configured with the rate and kind of faults, it can be started through either C# APIs or PowerShell, to generate faults in the cluster and your service.</span></span>

> [!WARNING]
> <span data-ttu-id="04000-112">ChaosTestScenario está sendo substituído por um Chaos baseado em serviço mais resiliente.</span><span class="sxs-lookup"><span data-stu-id="04000-112">ChaosTestScenario is being replaced by a more resilient, service-based Chaos.</span></span> <span data-ttu-id="04000-113">Confira o novo artigo [Controlled Chaos](service-fabric-controlled-chaos.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="04000-113">Please refer to the new article [Controlled Chaos](service-fabric-controlled-chaos.md) for more details.</span></span>
> 
> 

## <a name="chaos-test"></a><span data-ttu-id="04000-114">Teste de caos</span><span class="sxs-lookup"><span data-stu-id="04000-114">Chaos test</span></span>
<span data-ttu-id="04000-115">O cenário de caos gera falhas em todo o cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="04000-115">The chaos scenario generates faults across the entire Service Fabric cluster.</span></span> <span data-ttu-id="04000-116">O cenário compacta falhas geralmente vistas em meses ou em anos em apenas algumas horas.</span><span class="sxs-lookup"><span data-stu-id="04000-116">The scenario compresses faults generally seen in months or years to a few hours.</span></span> <span data-ttu-id="04000-117">A combinação de falhas intercaladas com a alta taxa de falhas localiza casos específicos que de outra forma seriam ignorados.</span><span class="sxs-lookup"><span data-stu-id="04000-117">The combination of interleaved faults with the high fault rate finds corner cases that are otherwise missed.</span></span> <span data-ttu-id="04000-118">Isso leva a uma melhoria significativa na qualidade do código do serviço.</span><span class="sxs-lookup"><span data-stu-id="04000-118">This leads to a significant improvement in the code quality of the service.</span></span>

### <a name="faults-simulated-in-the-chaos-test"></a><span data-ttu-id="04000-119">Falhas simuladas no teste de caos</span><span class="sxs-lookup"><span data-stu-id="04000-119">Faults simulated in the chaos test</span></span>
* <span data-ttu-id="04000-120">Reiniciar um nó</span><span class="sxs-lookup"><span data-stu-id="04000-120">Restart a node</span></span>
* <span data-ttu-id="04000-121">Reiniciar um pacote de códigos implantado</span><span class="sxs-lookup"><span data-stu-id="04000-121">Restart a deployed code package</span></span>
* <span data-ttu-id="04000-122">Remover uma réplica</span><span class="sxs-lookup"><span data-stu-id="04000-122">Remove a replica</span></span>
* <span data-ttu-id="04000-123">Reiniciar uma réplica</span><span class="sxs-lookup"><span data-stu-id="04000-123">Restart a replica</span></span>
* <span data-ttu-id="04000-124">Mover uma réplica primária (opcional)</span><span class="sxs-lookup"><span data-stu-id="04000-124">Move a primary replica (optional)</span></span>
* <span data-ttu-id="04000-125">Mover uma réplica secundária (opcional)</span><span class="sxs-lookup"><span data-stu-id="04000-125">Move a secondary replica (optional)</span></span>

<span data-ttu-id="04000-126">O teste de caos executa várias iterações de falhas e validações de cluster durante o período de tempo especificado.</span><span class="sxs-lookup"><span data-stu-id="04000-126">The chaos test runs multiple iterations of faults and cluster validations for the specified period of time.</span></span> <span data-ttu-id="04000-127">O tempo gasto para o cluster se estabilizar e a validação de êxito também são configuráveis.</span><span class="sxs-lookup"><span data-stu-id="04000-127">The time spent for the cluster to stabilize and for validation to succeed is also configurable.</span></span> <span data-ttu-id="04000-128">O cenário falha quando nos deparamos com uma única falha na validação do cluster.</span><span class="sxs-lookup"><span data-stu-id="04000-128">The scenario fails when you hit a single failure in cluster validation.</span></span>

<span data-ttu-id="04000-129">Por exemplo, considere um teste definido para ser executado por uma hora com um máximo de três falhas simultâneas.</span><span class="sxs-lookup"><span data-stu-id="04000-129">For example, consider a test set to run for one hour with a maximum of three concurrent faults.</span></span> <span data-ttu-id="04000-130">O teste induzirá três falhas e validará a integridade do cluster.</span><span class="sxs-lookup"><span data-stu-id="04000-130">The test will induce three faults, and then validate the cluster health.</span></span> <span data-ttu-id="04000-131">O teste será iterado por meio da etapa anterior até que o cluster perca a integridade ou tenha decorrido uma hora.</span><span class="sxs-lookup"><span data-stu-id="04000-131">The test will iterate through the previous step till the cluster becomes unhealthy or one hour passes.</span></span> <span data-ttu-id="04000-132">Se o cluster se tornar não íntegro em qualquer iteração, ou seja, não se estabilizar em um tempo configurado, o teste falhará com uma exceção.</span><span class="sxs-lookup"><span data-stu-id="04000-132">If the cluster becomes unhealthy in any iteration, i.e. it does not stabilize within a configured time, the test will fail with an exception.</span></span> <span data-ttu-id="04000-133">Essa exceção indica que algo deu errado e precisa de mais investigação.</span><span class="sxs-lookup"><span data-stu-id="04000-133">This exception indicates that something has gone wrong and needs further investigation.</span></span>

<span data-ttu-id="04000-134">Em sua forma atual, o mecanismo de geração de falha no teste de caos induz somente a falhas seguras.</span><span class="sxs-lookup"><span data-stu-id="04000-134">In its current form, the fault generation engine in the chaos test induces only safe faults.</span></span> <span data-ttu-id="04000-135">Isso significa que, na ausência de falhas externas, uma perda de quorum ou dados nunca ocorrerá.</span><span class="sxs-lookup"><span data-stu-id="04000-135">This means that in the absence of external faults, a quorum or data loss will never occur.</span></span>

### <a name="important-configuration-options"></a><span data-ttu-id="04000-136">Opções de configuração importantes</span><span class="sxs-lookup"><span data-stu-id="04000-136">Important configuration options</span></span>
* <span data-ttu-id="04000-137">**TimeToRun**: tempo total em que o teste será executado antes de ser finalizado com êxito.</span><span class="sxs-lookup"><span data-stu-id="04000-137">**TimeToRun**: Total time that the test will run before finishing with success.</span></span> <span data-ttu-id="04000-138">O teste pode ser finalizado antes, no lugar de uma falha de validação.</span><span class="sxs-lookup"><span data-stu-id="04000-138">The test can finish earlier in lieu of a validation failure.</span></span>
* <span data-ttu-id="04000-139">**MaxClusterStabilizationTimeout**: a quantidade máxima de tempo de espera para que o cluster se torne íntegro antes de falhar no teste.</span><span class="sxs-lookup"><span data-stu-id="04000-139">**MaxClusterStabilizationTimeout**: Maximum amount of time to wait for the cluster to become healthy before failing the test.</span></span> <span data-ttu-id="04000-140">As verificações executadas são as seguintes: se a integridade do cluster está OK, se a integridade do serviço está OK, se o tamanho do conjunto de réplicas de destino foi atingido para a partição de serviço e se não existe réplica do InBuild.</span><span class="sxs-lookup"><span data-stu-id="04000-140">The checks performed are whether cluster health is OK, service health is OK, the target replica set size is achieved for the service partition, and no InBuild replicas exist.</span></span>
* <span data-ttu-id="04000-141">**MaxConcurrentFaults**: número máximo de falhas simultâneas induzidas em cada iteração.</span><span class="sxs-lookup"><span data-stu-id="04000-141">**MaxConcurrentFaults**: Maximum number of concurrent faults induced in each iteration.</span></span> <span data-ttu-id="04000-142">Quanto maior o número, mais agressivo o teste, resultando em failovers mais complexos e combinações de transição.</span><span class="sxs-lookup"><span data-stu-id="04000-142">The higher the number, the more aggressive the test, hence resulting in more complex failovers and transition combinations.</span></span> <span data-ttu-id="04000-143">O teste garante que, na ausência de falhas externas, não haverá uma perda de quorum ou de dados, independentemente de quão alta essa configuração está.</span><span class="sxs-lookup"><span data-stu-id="04000-143">The test guarantees that in absence of external faults there will not be a quorum or data loss, irrespective of how high this configuration is.</span></span>
* <span data-ttu-id="04000-144">**EnableMoveReplicaFaults**: habilita ou desabilita as falhas que estão causando a movimentação das réplicas primárias ou secundárias.</span><span class="sxs-lookup"><span data-stu-id="04000-144">**EnableMoveReplicaFaults**: Enables or disables the faults that are causing the move of the primary or secondary replicas.</span></span> <span data-ttu-id="04000-145">Essas falhas estão desabilitadas por padrão.</span><span class="sxs-lookup"><span data-stu-id="04000-145">These faults are disabled by default.</span></span>
* <span data-ttu-id="04000-146">**WaitTimeBetweenIterations**: tempo de espera entre as iterações, isto é, após uma rodada de falhas e a validação correspondente.</span><span class="sxs-lookup"><span data-stu-id="04000-146">**WaitTimeBetweenIterations**: Amount of time to wait between iterations, i.e. after a round of faults and corresponding validation.</span></span>

### <a name="how-to-run-the-chaos-test"></a><span data-ttu-id="04000-147">Como executar o teste de caos</span><span class="sxs-lookup"><span data-stu-id="04000-147">How to run the chaos test</span></span>
<span data-ttu-id="04000-148">Exemplo de C#</span><span class="sxs-lookup"><span data-stu-id="04000-148">C# sample</span></span>

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

        // The chaos test scenario should run at least 60 minutes or until it fails.
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

        // Create the scenario class and execute it asynchronously.
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

<span data-ttu-id="04000-149">PowerShell</span><span class="sxs-lookup"><span data-stu-id="04000-149">PowerShell</span></span>

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```


## <a name="failover-test"></a><span data-ttu-id="04000-150">Teste de failover</span><span class="sxs-lookup"><span data-stu-id="04000-150">Failover test</span></span>
<span data-ttu-id="04000-151">O cenário do teste de failover é uma versão do cenário de teste de caos que visa uma partição de serviço específica.</span><span class="sxs-lookup"><span data-stu-id="04000-151">The failover test scenario is a version of the chaos test scenario that targets a specific service partition.</span></span> <span data-ttu-id="04000-152">Ele testa o efeito de failover em uma partição de serviço específica, sem afetar os outros serviços.</span><span class="sxs-lookup"><span data-stu-id="04000-152">It tests the effect of failover on a specific service partition while leaving the other services unaffected.</span></span> <span data-ttu-id="04000-153">Quando configurado com as informações de partição de destino e outros parâmetros, ele é executado como uma ferramenta do lado do cliente que usa as APIs do C# ou o PowerShell para gerar falhas para uma partição de serviço.</span><span class="sxs-lookup"><span data-stu-id="04000-153">Once it's configured with the target partition information and other parameters, it runs as a client-side tool that uses either C# APIs or PowerShell to generate faults for a service partition.</span></span> <span data-ttu-id="04000-154">O cenário é iterado por meio de uma sequência de falhas simuladas e validação de serviço enquanto a lógica de negócios é executada ao lado para fornecer uma carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="04000-154">The scenario iterates through a sequence of simulated faults and service validation while your business logic runs on the side to provide a workload.</span></span> <span data-ttu-id="04000-155">Uma falha na validação do serviço indica um problema que precisa de mais investigação.</span><span class="sxs-lookup"><span data-stu-id="04000-155">A failure in service validation indicates an issue that needs further investigation.</span></span>

### <a name="faults-simulated-in-the-failover-test"></a><span data-ttu-id="04000-156">Falhas simuladas no teste de failover</span><span class="sxs-lookup"><span data-stu-id="04000-156">Faults simulated in the failover test</span></span>
* <span data-ttu-id="04000-157">Reiniciar um pacote de códigos implantado onde a partição está hospedada</span><span class="sxs-lookup"><span data-stu-id="04000-157">Restart a deployed code package where the partition is hosted</span></span>
* <span data-ttu-id="04000-158">Remover uma réplica primária/secundária ou uma instância sem estado</span><span class="sxs-lookup"><span data-stu-id="04000-158">Remove a primary/secondary replica or stateless instance</span></span>
* <span data-ttu-id="04000-159">Reiniciar uma réplica primária secundária (se o serviço persistir)</span><span class="sxs-lookup"><span data-stu-id="04000-159">Restart a primary secondary replica (if a persisted service)</span></span>
* <span data-ttu-id="04000-160">Mover uma réplica primária</span><span class="sxs-lookup"><span data-stu-id="04000-160">Move a primary replica</span></span>
* <span data-ttu-id="04000-161">Mover uma réplica secundária</span><span class="sxs-lookup"><span data-stu-id="04000-161">Move a secondary replica</span></span>
* <span data-ttu-id="04000-162">Reiniciar a partição</span><span class="sxs-lookup"><span data-stu-id="04000-162">Restart the partition</span></span>

<span data-ttu-id="04000-163">O teste de failover induz a uma falha escolhida e depois executa a validação no serviço para assegurar sua estabilidade.</span><span class="sxs-lookup"><span data-stu-id="04000-163">The failover test induces a chosen fault and then runs validation on the service to ensure its stability.</span></span> <span data-ttu-id="04000-164">O teste de failover induz apenas a uma falha de cada vez, em vez de possíveis várias falhas no teste de caos.</span><span class="sxs-lookup"><span data-stu-id="04000-164">The failover test induces only one fault at a time, as opposed to possible multiple faults in the chaos test.</span></span> <span data-ttu-id="04000-165">Se a partição de serviço não estabilizar no tempo limite configurado após cada falha, o teste falhará.</span><span class="sxs-lookup"><span data-stu-id="04000-165">If the service partition does not stabilize within the configured timeout after each fault, the test fails.</span></span> <span data-ttu-id="04000-166">O teste induz apenas a falhas seguras.</span><span class="sxs-lookup"><span data-stu-id="04000-166">The test induces only safe faults.</span></span> <span data-ttu-id="04000-167">Isso significa que, na ausência de falhas externas, não ocorre uma perda de quorum ou dados.</span><span class="sxs-lookup"><span data-stu-id="04000-167">This means that in absence of external failures, a quorum or data loss will not occur.</span></span>

### <a name="important-configuration-options"></a><span data-ttu-id="04000-168">Opções de configuração importantes</span><span class="sxs-lookup"><span data-stu-id="04000-168">Important configuration options</span></span>
* <span data-ttu-id="04000-169">**PartitionSelector**: objeto seletor que especifica a partição que precisa ser direcionada.</span><span class="sxs-lookup"><span data-stu-id="04000-169">**PartitionSelector**: Selector object that specifies the partition that needs to be targeted.</span></span>
* <span data-ttu-id="04000-170">**TimeToRun**: tempo total pelo qual o teste será executado antes da finalização.</span><span class="sxs-lookup"><span data-stu-id="04000-170">**TimeToRun**: Total time that the test will run before finishing.</span></span>
* <span data-ttu-id="04000-171">**MaxServiceStabilizationTimeout**: a quantidade máxima de tempo de espera para que o cluster se torne íntegro antes da falha no teste.</span><span class="sxs-lookup"><span data-stu-id="04000-171">**MaxServiceStabilizationTimeout**: Maximum amount of time to wait for the cluster to become healthy before failing the test.</span></span> <span data-ttu-id="04000-172">As verificações executadas são as seguintes: se a integridade do serviço está OK, se o tamanho do conjunto de réplicas de destino foi atingido para todas as partições e se não existe réplica do InBuild.</span><span class="sxs-lookup"><span data-stu-id="04000-172">The checks performed are whether service health is OK, the target replica set size is achieved for all partitions, and no InBuild replicas exist.</span></span>
* <span data-ttu-id="04000-173">**WaitTimeBetweenFaults**: tempo de espera entre cada ciclo de falha e validação.</span><span class="sxs-lookup"><span data-stu-id="04000-173">**WaitTimeBetweenFaults**: Amount of time to wait between every fault and validation cycle.</span></span>

### <a name="how-to-run-the-failover-test"></a><span data-ttu-id="04000-174">Como executar o teste de failover</span><span class="sxs-lookup"><span data-stu-id="04000-174">How to run the failover test</span></span>
<span data-ttu-id="04000-175">**C#**</span><span class="sxs-lookup"><span data-stu-id="04000-175">**C#**</span></span>

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

        // The chaos test scenario should run at least 60 minutes or until it fails.
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

        // Create the scenario class and execute it asynchronously.
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


<span data-ttu-id="04000-176">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="04000-176">**PowerShell**</span></span>

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/SampleApp/SampleService"

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindSingleton
```
