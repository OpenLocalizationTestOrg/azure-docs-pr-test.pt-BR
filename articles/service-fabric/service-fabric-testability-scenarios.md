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
# <a name="testability-scenarios"></a><span data-ttu-id="6f55c-103">Cenários da possibilidade de teste</span><span class="sxs-lookup"><span data-stu-id="6f55c-103">Testability scenarios</span></span>
<span data-ttu-id="6f55c-104">Sistemas grandes distribuídos como infraestruturas de nuvem não são confiáveis por natureza.</span><span class="sxs-lookup"><span data-stu-id="6f55c-104">Large distributed systems like cloud infrastructures are inherently unreliable.</span></span> <span data-ttu-id="6f55c-105">Azure Service Fabric oferece aos desenvolvedores Olá capacidade toowrite serviços toorun sobre infraestruturas não confiáveis.</span><span class="sxs-lookup"><span data-stu-id="6f55c-105">Azure Service Fabric gives developers hello ability toowrite services toorun on top of unreliable infrastructures.</span></span> <span data-ttu-id="6f55c-106">Em serviços de alta qualidade toowrite ordem, os desenvolvedores precisam tooinduce capaz de toobe tal estabilidade de saudação tootest infraestrutura confiável de seus serviços.</span><span class="sxs-lookup"><span data-stu-id="6f55c-106">In order toowrite high-quality services, developers need toobe able tooinduce such unreliable infrastructure tootest hello stability of their services.</span></span>

<span data-ttu-id="6f55c-107">Olá falhas Analysis Services oferece aos desenvolvedores serviços tootest ações de falhas do hello capacidade tooinduce na presença de saudação de falhas.</span><span class="sxs-lookup"><span data-stu-id="6f55c-107">hello Fault Analysis Service gives developers hello ability tooinduce fault actions tootest services in hello presence of failures.</span></span> <span data-ttu-id="6f55c-108">No entanto, falhas simuladas direcionadas não o levarão tão longe.</span><span class="sxs-lookup"><span data-stu-id="6f55c-108">However, targeted simulated faults will get you only so far.</span></span> <span data-ttu-id="6f55c-109">Olá tootake testes Além disso, você pode usar os cenários de teste de saudação do Service Fabric: um caos de teste e um teste de failover.</span><span class="sxs-lookup"><span data-stu-id="6f55c-109">tootake hello testing further, you can use hello test scenarios in Service Fabric: a chaos test and a failover test.</span></span> <span data-ttu-id="6f55c-110">Esses cenários simular contínuas falhas intercaladas normais e anormais em todo o cluster Olá por longos períodos de tempo.</span><span class="sxs-lookup"><span data-stu-id="6f55c-110">These scenarios simulate continuous interleaved faults, both graceful and ungraceful, throughout hello cluster over extended periods of time.</span></span> <span data-ttu-id="6f55c-111">Após um teste está configurado com taxa de saudação e tipo de falhas, ele pode ser iniciado por meio de APIs de c# ou PowerShell, toogenerate falhas no cluster hello e seu serviço.</span><span class="sxs-lookup"><span data-stu-id="6f55c-111">Once a test is configured with hello rate and kind of faults, it can be started through either C# APIs or PowerShell, toogenerate faults in hello cluster and your service.</span></span>

> [!WARNING]
> <span data-ttu-id="6f55c-112">ChaosTestScenario está sendo substituído por um Chaos baseado em serviço mais resiliente.</span><span class="sxs-lookup"><span data-stu-id="6f55c-112">ChaosTestScenario is being replaced by a more resilient, service-based Chaos.</span></span> <span data-ttu-id="6f55c-113">Consulte o artigo novo toohello [controlados caos](service-fabric-controlled-chaos.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="6f55c-113">Please refer toohello new article [Controlled Chaos](service-fabric-controlled-chaos.md) for more details.</span></span>
> 
> 

## <a name="chaos-test"></a><span data-ttu-id="6f55c-114">Teste de caos</span><span class="sxs-lookup"><span data-stu-id="6f55c-114">Chaos test</span></span>
<span data-ttu-id="6f55c-115">cenário de caos Hello gera falhas em cluster do Service Fabric inteira de saudação.</span><span class="sxs-lookup"><span data-stu-id="6f55c-115">hello chaos scenario generates faults across hello entire Service Fabric cluster.</span></span> <span data-ttu-id="6f55c-116">cenário de saudação compacta falhas geralmente vistas em meses ou anos tooa algumas horas.</span><span class="sxs-lookup"><span data-stu-id="6f55c-116">hello scenario compresses faults generally seen in months or years tooa few hours.</span></span> <span data-ttu-id="6f55c-117">combinação de saudação de falhas intercaladas com taxa de falhas de alta Olá encontra casos de canto que são perdidos caso contrário.</span><span class="sxs-lookup"><span data-stu-id="6f55c-117">hello combination of interleaved faults with hello high fault rate finds corner cases that are otherwise missed.</span></span> <span data-ttu-id="6f55c-118">Isso leva a melhoria significativa tooa na qualidade do código de saudação do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="6f55c-118">This leads tooa significant improvement in hello code quality of hello service.</span></span>

### <a name="faults-simulated-in-hello-chaos-test"></a><span data-ttu-id="6f55c-119">Falhas simuladas no teste de caos Olá</span><span class="sxs-lookup"><span data-stu-id="6f55c-119">Faults simulated in hello chaos test</span></span>
* <span data-ttu-id="6f55c-120">Reiniciar um nó</span><span class="sxs-lookup"><span data-stu-id="6f55c-120">Restart a node</span></span>
* <span data-ttu-id="6f55c-121">Reiniciar um pacote de códigos implantado</span><span class="sxs-lookup"><span data-stu-id="6f55c-121">Restart a deployed code package</span></span>
* <span data-ttu-id="6f55c-122">Remover uma réplica</span><span class="sxs-lookup"><span data-stu-id="6f55c-122">Remove a replica</span></span>
* <span data-ttu-id="6f55c-123">Reiniciar uma réplica</span><span class="sxs-lookup"><span data-stu-id="6f55c-123">Restart a replica</span></span>
* <span data-ttu-id="6f55c-124">Mover uma réplica primária (opcional)</span><span class="sxs-lookup"><span data-stu-id="6f55c-124">Move a primary replica (optional)</span></span>
* <span data-ttu-id="6f55c-125">Mover uma réplica secundária (opcional)</span><span class="sxs-lookup"><span data-stu-id="6f55c-125">Move a secondary replica (optional)</span></span>

<span data-ttu-id="6f55c-126">teste de caos Olá executa várias iterações de falhas e validações de cluster de saudação especificado o período de tempo.</span><span class="sxs-lookup"><span data-stu-id="6f55c-126">hello chaos test runs multiple iterations of faults and cluster validations for hello specified period of time.</span></span> <span data-ttu-id="6f55c-127">Olá tempo para Olá cluster toostabilize e validação toosucceed também é configurável.</span><span class="sxs-lookup"><span data-stu-id="6f55c-127">hello time spent for hello cluster toostabilize and for validation toosucceed is also configurable.</span></span> <span data-ttu-id="6f55c-128">cenário de saudação falha quando você atinge uma única falha na validação de cluster.</span><span class="sxs-lookup"><span data-stu-id="6f55c-128">hello scenario fails when you hit a single failure in cluster validation.</span></span>

<span data-ttu-id="6f55c-129">Por exemplo, considere que um teste definido toorun por uma hora com um máximo de três falhas simultâneas.</span><span class="sxs-lookup"><span data-stu-id="6f55c-129">For example, consider a test set toorun for one hour with a maximum of three concurrent faults.</span></span> <span data-ttu-id="6f55c-130">teste de saudação induzir três falhas e validar a integridade do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="6f55c-130">hello test will induce three faults, and then validate hello cluster health.</span></span> <span data-ttu-id="6f55c-131">teste Olá irá iterar por meio da etapa anterior Olá até que o cluster de saudação se tornará não íntegro ou passa de uma hora.</span><span class="sxs-lookup"><span data-stu-id="6f55c-131">hello test will iterate through hello previous step till hello cluster becomes unhealthy or one hour passes.</span></span> <span data-ttu-id="6f55c-132">Se o cluster de saudação se tornará não íntegro em qualquer iteração, ou seja, não estável dentro de um tempo configurado, Olá teste falha com uma exceção.</span><span class="sxs-lookup"><span data-stu-id="6f55c-132">If hello cluster becomes unhealthy in any iteration, i.e. it does not stabilize within a configured time, hello test will fail with an exception.</span></span> <span data-ttu-id="6f55c-133">Essa exceção indica que algo deu errado e precisa de mais investigação.</span><span class="sxs-lookup"><span data-stu-id="6f55c-133">This exception indicates that something has gone wrong and needs further investigation.</span></span>

<span data-ttu-id="6f55c-134">Em sua forma atual, mecanismo de geração Olá falha no teste de caos Olá induz falhas apenas seguras.</span><span class="sxs-lookup"><span data-stu-id="6f55c-134">In its current form, hello fault generation engine in hello chaos test induces only safe faults.</span></span> <span data-ttu-id="6f55c-135">Isso significa que na ausência de saudação de falhas externas, uma quorum ou perda de dados nunca ocorrerão.</span><span class="sxs-lookup"><span data-stu-id="6f55c-135">This means that in hello absence of external faults, a quorum or data loss will never occur.</span></span>

### <a name="important-configuration-options"></a><span data-ttu-id="6f55c-136">Opções de configuração importantes</span><span class="sxs-lookup"><span data-stu-id="6f55c-136">Important configuration options</span></span>
* <span data-ttu-id="6f55c-137">**TimeToRun**: tempo Total de teste Olá será executado antes de concluir com êxito.</span><span class="sxs-lookup"><span data-stu-id="6f55c-137">**TimeToRun**: Total time that hello test will run before finishing with success.</span></span> <span data-ttu-id="6f55c-138">teste de saudação pode concluir anterior em vez de uma falha de validação.</span><span class="sxs-lookup"><span data-stu-id="6f55c-138">hello test can finish earlier in lieu of a validation failure.</span></span>
* <span data-ttu-id="6f55c-139">**MaxClusterStabilizationTimeout**: quantidade máxima de tempo toowait para Olá cluster toobecome Íntegro antes da falha de teste de saudação.</span><span class="sxs-lookup"><span data-stu-id="6f55c-139">**MaxClusterStabilizationTimeout**: Maximum amount of time toowait for hello cluster toobecome healthy before failing hello test.</span></span> <span data-ttu-id="6f55c-140">Hello verificações executadas são se a integridade do cluster é Okey, a integridade do serviço é Okey, hello tamanho do conjunto de réplica de destino é obtido para partição de serviço hello e nenhum réplicas InBuild existem.</span><span class="sxs-lookup"><span data-stu-id="6f55c-140">hello checks performed are whether cluster health is OK, service health is OK, hello target replica set size is achieved for hello service partition, and no InBuild replicas exist.</span></span>
* <span data-ttu-id="6f55c-141">**MaxConcurrentFaults**: número máximo de falhas simultâneas induzidas em cada iteração.</span><span class="sxs-lookup"><span data-stu-id="6f55c-141">**MaxConcurrentFaults**: Maximum number of concurrent faults induced in each iteration.</span></span> <span data-ttu-id="6f55c-142">Olá número mais alto de hello, Olá mais agressiva teste hello, portanto, resultando em failovers mais complexas e combinações de transição.</span><span class="sxs-lookup"><span data-stu-id="6f55c-142">hello higher hello number, hello more aggressive hello test, hence resulting in more complex failovers and transition combinations.</span></span> <span data-ttu-id="6f55c-143">teste de saudação garante que na ausência de falhas externas não haverá uma perda de quorum ou os dados, independentemente de quão alto essa configuração é.</span><span class="sxs-lookup"><span data-stu-id="6f55c-143">hello test guarantees that in absence of external faults there will not be a quorum or data loss, irrespective of how high this configuration is.</span></span>
* <span data-ttu-id="6f55c-144">**EnableMoveReplicaFaults**: habilita ou desabilita a falhas de saudação que estão causando mover Olá Olá réplicas primárias ou secundárias.</span><span class="sxs-lookup"><span data-stu-id="6f55c-144">**EnableMoveReplicaFaults**: Enables or disables hello faults that are causing hello move of hello primary or secondary replicas.</span></span> <span data-ttu-id="6f55c-145">Essas falhas estão desabilitadas por padrão.</span><span class="sxs-lookup"><span data-stu-id="6f55c-145">These faults are disabled by default.</span></span>
* <span data-ttu-id="6f55c-146">**WaitTimeBetweenIterations**: quantidade de tempo toowait entre as iterações, ou seja, depois uma rodada de falhas e validação correspondente.</span><span class="sxs-lookup"><span data-stu-id="6f55c-146">**WaitTimeBetweenIterations**: Amount of time toowait between iterations, i.e. after a round of faults and corresponding validation.</span></span>

### <a name="how-toorun-hello-chaos-test"></a><span data-ttu-id="6f55c-147">Como testar caos de saudação toorun</span><span class="sxs-lookup"><span data-stu-id="6f55c-147">How toorun hello chaos test</span></span>
<span data-ttu-id="6f55c-148">Exemplo de C#</span><span class="sxs-lookup"><span data-stu-id="6f55c-148">C# sample</span></span>

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

<span data-ttu-id="6f55c-149">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6f55c-149">PowerShell</span></span>

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```


## <a name="failover-test"></a><span data-ttu-id="6f55c-150">Teste de failover</span><span class="sxs-lookup"><span data-stu-id="6f55c-150">Failover test</span></span>
<span data-ttu-id="6f55c-151">cenário de teste de failover de saudação é uma versão do cenário de teste de caos Olá que tem como alvo uma partição de serviço específico.</span><span class="sxs-lookup"><span data-stu-id="6f55c-151">hello failover test scenario is a version of hello chaos test scenario that targets a specific service partition.</span></span> <span data-ttu-id="6f55c-152">Ele testa o efeito de saudação de failover em uma partição de serviço específico, deixando Olá outros serviços afetados.</span><span class="sxs-lookup"><span data-stu-id="6f55c-152">It tests hello effect of failover on a specific service partition while leaving hello other services unaffected.</span></span> <span data-ttu-id="6f55c-153">Depois que ele é configurado com informações de partição de destino hello e outros parâmetros, ele é executado como uma ferramenta de cliente que usa APIs do c# ou PowerShell falhas de toogenerate para uma partição de serviço.</span><span class="sxs-lookup"><span data-stu-id="6f55c-153">Once it's configured with hello target partition information and other parameters, it runs as a client-side tool that uses either C# APIs or PowerShell toogenerate faults for a service partition.</span></span> <span data-ttu-id="6f55c-154">cenário Olá itera por meio de uma sequência de falhas simuladas e validação de serviço, enquanto a lógica de negócios é executado no hello lado tooprovide uma carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="6f55c-154">hello scenario iterates through a sequence of simulated faults and service validation while your business logic runs on hello side tooprovide a workload.</span></span> <span data-ttu-id="6f55c-155">Uma falha na validação do serviço indica um problema que precisa de mais investigação.</span><span class="sxs-lookup"><span data-stu-id="6f55c-155">A failure in service validation indicates an issue that needs further investigation.</span></span>

### <a name="faults-simulated-in-hello-failover-test"></a><span data-ttu-id="6f55c-156">Falhas simuladas no teste de failover Olá</span><span class="sxs-lookup"><span data-stu-id="6f55c-156">Faults simulated in hello failover test</span></span>
* <span data-ttu-id="6f55c-157">Reiniciar um pacote de código implantado onde a partição hello está hospedada</span><span class="sxs-lookup"><span data-stu-id="6f55c-157">Restart a deployed code package where hello partition is hosted</span></span>
* <span data-ttu-id="6f55c-158">Remover uma réplica primária/secundária ou uma instância sem estado</span><span class="sxs-lookup"><span data-stu-id="6f55c-158">Remove a primary/secondary replica or stateless instance</span></span>
* <span data-ttu-id="6f55c-159">Reiniciar uma réplica primária secundária (se o serviço persistir)</span><span class="sxs-lookup"><span data-stu-id="6f55c-159">Restart a primary secondary replica (if a persisted service)</span></span>
* <span data-ttu-id="6f55c-160">Mover uma réplica primária</span><span class="sxs-lookup"><span data-stu-id="6f55c-160">Move a primary replica</span></span>
* <span data-ttu-id="6f55c-161">Mover uma réplica secundária</span><span class="sxs-lookup"><span data-stu-id="6f55c-161">Move a secondary replica</span></span>
* <span data-ttu-id="6f55c-162">Reinicie a partição Olá</span><span class="sxs-lookup"><span data-stu-id="6f55c-162">Restart hello partition</span></span>

<span data-ttu-id="6f55c-163">teste de failover Olá induzir a uma falha escolhida e executa validação no hello serviço tooensure sua estabilidade.</span><span class="sxs-lookup"><span data-stu-id="6f55c-163">hello failover test induces a chosen fault and then runs validation on hello service tooensure its stability.</span></span> <span data-ttu-id="6f55c-164">teste de failover Olá induz somente uma falha em uma hora, como contrário toopossible várias falhas no teste de caos hello.</span><span class="sxs-lookup"><span data-stu-id="6f55c-164">hello failover test induces only one fault at a time, as opposed toopossible multiple faults in hello chaos test.</span></span> <span data-ttu-id="6f55c-165">Se a partição de serviço Olá não estabilizar no tempo limite de saudação configurada após cada falha, o teste de saudação falhará.</span><span class="sxs-lookup"><span data-stu-id="6f55c-165">If hello service partition does not stabilize within hello configured timeout after each fault, hello test fails.</span></span> <span data-ttu-id="6f55c-166">teste de saudação induz somente falhas de seguras.</span><span class="sxs-lookup"><span data-stu-id="6f55c-166">hello test induces only safe faults.</span></span> <span data-ttu-id="6f55c-167">Isso significa que, na ausência de falhas externas, não ocorre uma perda de quorum ou dados.</span><span class="sxs-lookup"><span data-stu-id="6f55c-167">This means that in absence of external failures, a quorum or data loss will not occur.</span></span>

### <a name="important-configuration-options"></a><span data-ttu-id="6f55c-168">Opções de configuração importantes</span><span class="sxs-lookup"><span data-stu-id="6f55c-168">Important configuration options</span></span>
* <span data-ttu-id="6f55c-169">**PartitionSelector**: objeto de seletor que especifica a partição de saudação que precisa toobe direcionado.</span><span class="sxs-lookup"><span data-stu-id="6f55c-169">**PartitionSelector**: Selector object that specifies hello partition that needs toobe targeted.</span></span>
* <span data-ttu-id="6f55c-170">**TimeToRun**: tempo Total de teste Olá será executado antes de concluir.</span><span class="sxs-lookup"><span data-stu-id="6f55c-170">**TimeToRun**: Total time that hello test will run before finishing.</span></span>
* <span data-ttu-id="6f55c-171">**MaxServiceStabilizationTimeout**: quantidade máxima de tempo toowait para Olá cluster toobecome Íntegro antes da falha de teste de saudação.</span><span class="sxs-lookup"><span data-stu-id="6f55c-171">**MaxServiceStabilizationTimeout**: Maximum amount of time toowait for hello cluster toobecome healthy before failing hello test.</span></span> <span data-ttu-id="6f55c-172">Hello verificações executadas são se a integridade do serviço é Okey, hello tamanho do conjunto de réplica de destino é obtido para todas as partições e nenhum réplicas InBuild existem.</span><span class="sxs-lookup"><span data-stu-id="6f55c-172">hello checks performed are whether service health is OK, hello target replica set size is achieved for all partitions, and no InBuild replicas exist.</span></span>
* <span data-ttu-id="6f55c-173">**WaitTimeBetweenFaults**: quantidade de tempo toowait entre cada ciclo de falha e validação.</span><span class="sxs-lookup"><span data-stu-id="6f55c-173">**WaitTimeBetweenFaults**: Amount of time toowait between every fault and validation cycle.</span></span>

### <a name="how-toorun-hello-failover-test"></a><span data-ttu-id="6f55c-174">Como testar o failover de saudação toorun</span><span class="sxs-lookup"><span data-stu-id="6f55c-174">How toorun hello failover test</span></span>
<span data-ttu-id="6f55c-175">**C#**</span><span class="sxs-lookup"><span data-stu-id="6f55c-175">**C#**</span></span>

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


<span data-ttu-id="6f55c-176">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="6f55c-176">**PowerShell**</span></span>

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/SampleApp/SampleService"

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindSingleton
```
