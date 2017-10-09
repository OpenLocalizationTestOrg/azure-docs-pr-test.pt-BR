---
title: "clusters de caos na malha do serviço aaaInduce | Microsoft Docs"
description: "Usando a injeção de falha e as APIs de serviço de análise de Cluster toomanage caos em cluster hello."
services: service-fabric
documentationcenter: .net
author: motanv
manager: anmola
editor: motanv
ms.assetid: 2bd13443-3478-4382-9a5a-1f6c6b32bfc9
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: motanv
ms.openlocfilehash: 7e87cae22645fc4ba52e258471d8f3a4ffdb1cce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="induce-controlled-chaos-in-service-fabric-clusters"></a><span data-ttu-id="5a325-103">Induzir o Controlled Chaos em clusters do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="5a325-103">Induce controlled Chaos in Service Fabric clusters</span></span>
<span data-ttu-id="5a325-104">Os sistemas distribuídos em larga escala, como as infraestruturas de nuvem, não são confiáveis por natureza.</span><span class="sxs-lookup"><span data-stu-id="5a325-104">Large-scale distributed systems like cloud infrastructures are inherently unreliable.</span></span> <span data-ttu-id="5a325-105">Malha do Azure do serviço permite que desenvolvedores toowrite confiável serviços distribuídos em uma infraestrutura não confiável.</span><span class="sxs-lookup"><span data-stu-id="5a325-105">Azure Service Fabric enables developers toowrite reliable distributed services on top of an unreliable infrastructure.</span></span> <span data-ttu-id="5a325-106">toowrite serviços distribuídos robusto sobre uma infraestrutura não confiável, os desenvolvedores precisam estabilidade de saudação toobe tootest capaz de seus serviços enquanto Olá subjacente infraestrutura confiável está passando por transições de estado complicado toofaults vencimento.</span><span class="sxs-lookup"><span data-stu-id="5a325-106">toowrite robust distributed services on top of an unreliable infrastructure, developers need toobe able tootest hello stability of their services while hello underlying unreliable infrastructure is going through complicated state transitions due toofaults.</span></span>

<span data-ttu-id="5a325-107">Olá [injeção de falha e o serviço de análise de Cluster](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-testability-overview) (também conhecido como Olá falhas Analysis Service) permite que os desenvolvedores Olá tooinduce falhas tootest seus serviços.</span><span class="sxs-lookup"><span data-stu-id="5a325-107">hello [Fault Injection and Cluster Analysis Service](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-testability-overview) (also known as hello Fault Analysis Service) gives developers hello ability tooinduce faults tootest their services.</span></span> <span data-ttu-id="5a325-108">Esses direcionados simulados falhas, como [reiniciar uma partição](https://docs.microsoft.com/en-us/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps), pode ajudar o exercício transições de estado hello mais comuns.</span><span class="sxs-lookup"><span data-stu-id="5a325-108">These targeted simulated faults, like [restarting a partition](https://docs.microsoft.com/en-us/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps), can help exercise hello most common state transitions.</span></span> <span data-ttu-id="5a325-109">No entanto, as falhas simuladas direcionadas são tendenciosas por definição e, portanto, podem ignorar bugs que aparecem apenas em uma sequência de transições de estado complicada, longa e difícil de prever.</span><span class="sxs-lookup"><span data-stu-id="5a325-109">However targeted simulated faults are biased by definition and thus may miss bugs that show up only in hard-to-predict, long and complicated sequence of state transitions.</span></span> <span data-ttu-id="5a325-110">Para um teste imparcial, você pode usar o Chaos.</span><span class="sxs-lookup"><span data-stu-id="5a325-110">For an unbiased testing, you can use Chaos.</span></span>

<span data-ttu-id="5a325-111">Caos simula falhas periódicas, intercaladas (normais e anormais) em todo o cluster Olá por longos períodos de tempo.</span><span class="sxs-lookup"><span data-stu-id="5a325-111">Chaos simulates periodic, interleaved faults (both graceful and ungraceful) throughout hello cluster over extended periods of time.</span></span> <span data-ttu-id="5a325-112">Depois que você configurou caos com taxa de saudação e tipo de saudação de falhas, você pode iniciar caos por meio do c# ou Powershell API toostart gerar falhas no cluster hello e nos serviços.</span><span class="sxs-lookup"><span data-stu-id="5a325-112">Once you have configured Chaos with hello rate and hello kind of faults, you can start Chaos through C# or Powershell API toostart generating faults in hello cluster and in your services.</span></span> <span data-ttu-id="5a325-113">Você pode configurar caos toorun por um período de tempo especificado (por exemplo, para uma hora), após o qual caos interrompe automaticamente, ou você pode chamar a API StopChaos (c# ou Powershell) toostop-lo a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="5a325-113">You can configure Chaos toorun for a specified time period (for example, for one hour), after which Chaos stops automatically, or you can call StopChaos API (C# or Powershell) toostop it at any time.</span></span>

> [!NOTE]
> <span data-ttu-id="5a325-114">Em sua forma atual, caos induz falhas apenas seguras, que implica que na ausência de saudação de falhas externas de uma perda de quorum, ou perda de dados nunca ocorre.</span><span class="sxs-lookup"><span data-stu-id="5a325-114">In its current form, Chaos induces only safe faults, which implies that in hello absence of external faults a quorum loss, or data loss never occurs.</span></span>
>

<span data-ttu-id="5a325-115">Durante a execução caos, ele gera eventos diferentes que capturam o estado de saudação do hello executado no momento da saudação.</span><span class="sxs-lookup"><span data-stu-id="5a325-115">While Chaos is running, it produces different events that capture hello state of hello run at hello moment.</span></span> <span data-ttu-id="5a325-116">Por exemplo, um ExecutingFaultsEvent contém todas as falhas de saudação que caos decidiu tooexecute na iteração.</span><span class="sxs-lookup"><span data-stu-id="5a325-116">For example, an ExecutingFaultsEvent contains all hello faults that Chaos has decided tooexecute in that iteration.</span></span> <span data-ttu-id="5a325-117">Um ValidationFailedEvent contém detalhes de saudação de uma falha de validação (problemas de integridade ou de estabilidade) que foi encontrado durante a validação de saudação do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="5a325-117">A ValidationFailedEvent contains hello details of a validation failure (health or stability issues) that was found during hello validation of hello cluster.</span></span> <span data-ttu-id="5a325-118">Você pode chamar o relatório de saudação do Olá GetChaosReport API (c# ou Powershell) tooget de execuções de caos.</span><span class="sxs-lookup"><span data-stu-id="5a325-118">You can invoke hello GetChaosReport API (C# or Powershell) tooget hello report of Chaos runs.</span></span> <span data-ttu-id="5a325-119">Esses eventos são persistidos em um [dicionário confiável](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-reliable-collections), que tem uma política de truncamento determinada por duas configurações: **MaxStoredChaosEventCount** (o valor padrão é 25000) e **StoredActionCleanupIntervalInSeconds** (o valor padrão é 3600).</span><span class="sxs-lookup"><span data-stu-id="5a325-119">These events get persisted in a [reliable dictionary](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-reliable-collections), which has a truncation policy dictated by two configurations: **MaxStoredChaosEventCount** (default value is 25000) and **StoredActionCleanupIntervalInSeconds** (default value is 3600).</span></span> <span data-ttu-id="5a325-120">Cada *StoredActionCleanupIntervalInSeconds* verificações caos e todos os mas hello mais recente *MaxStoredChaosEventCount* eventos, são removidos do dicionário de saudação confiável.</span><span class="sxs-lookup"><span data-stu-id="5a325-120">Every *StoredActionCleanupIntervalInSeconds* Chaos checks and all but hello most recent *MaxStoredChaosEventCount* events, are purged from hello reliable dictionary.</span></span>

## <a name="faults-induced-in-chaos"></a><span data-ttu-id="5a325-121">Falhas induzidas no Chaos</span><span class="sxs-lookup"><span data-stu-id="5a325-121">Faults induced in Chaos</span></span>
<span data-ttu-id="5a325-122">Caos gera falhas em inteiras de cluster do Service Fabric hello e compacta falhas que são vistas em meses ou anos em algumas horas.</span><span class="sxs-lookup"><span data-stu-id="5a325-122">Chaos generates faults across hello entire Service Fabric cluster and compresses faults that are seen in months or years into a few hours.</span></span> <span data-ttu-id="5a325-123">combinação de saudação de falhas intercaladas com taxa de falhas de alta Olá encontra casos de canto que poderão ser perdidos caso contrário.</span><span class="sxs-lookup"><span data-stu-id="5a325-123">hello combination of interleaved faults with hello high fault rate finds corner cases that may otherwise be missed.</span></span> <span data-ttu-id="5a325-124">Este exercício de caos leva tooa um aprimoramento significativo na qualidade do código de saudação do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="5a325-124">This exercise of Chaos leads tooa significant improvement in hello code quality of hello service.</span></span>

<span data-ttu-id="5a325-125">Caos induzir a falhas de saudação categorias a seguir:</span><span class="sxs-lookup"><span data-stu-id="5a325-125">Chaos induces faults from hello following categories:</span></span>

* <span data-ttu-id="5a325-126">Reiniciar um nó</span><span class="sxs-lookup"><span data-stu-id="5a325-126">Restart a node</span></span>
* <span data-ttu-id="5a325-127">Reiniciar um pacote de códigos implantado</span><span class="sxs-lookup"><span data-stu-id="5a325-127">Restart a deployed code package</span></span>
* <span data-ttu-id="5a325-128">Remover uma réplica</span><span class="sxs-lookup"><span data-stu-id="5a325-128">Remove a replica</span></span>
* <span data-ttu-id="5a325-129">Reiniciar uma réplica</span><span class="sxs-lookup"><span data-stu-id="5a325-129">Restart a replica</span></span>
* <span data-ttu-id="5a325-130">Mover uma réplica primária (configurável)</span><span class="sxs-lookup"><span data-stu-id="5a325-130">Move a primary replica (configurable)</span></span>
* <span data-ttu-id="5a325-131">Mover uma réplica secundária (configurável)</span><span class="sxs-lookup"><span data-stu-id="5a325-131">Move a secondary replica (configurable)</span></span>

<span data-ttu-id="5a325-132">O Chaos é executado em várias iterações.</span><span class="sxs-lookup"><span data-stu-id="5a325-132">Chaos runs in multiple iterations.</span></span> <span data-ttu-id="5a325-133">Cada iteração consiste em falhas e período de validação de cluster para Olá especificado.</span><span class="sxs-lookup"><span data-stu-id="5a325-133">Each iteration consists of faults and cluster validation for hello specified period.</span></span> <span data-ttu-id="5a325-134">Você pode configurar o tempo de saudação gasto para Olá cluster toostabilize e toosucceed de validação.</span><span class="sxs-lookup"><span data-stu-id="5a325-134">You can configure hello time spent for hello cluster toostabilize and for validation toosucceed.</span></span> <span data-ttu-id="5a325-135">Se for encontrada uma falha na validação de cluster, caos gera e persistir um ValidationFailedEvent com carimbo de hora de UTC hello e detalhes da falha hello.</span><span class="sxs-lookup"><span data-stu-id="5a325-135">If a failure is found in cluster validation, Chaos generates and persists a ValidationFailedEvent with hello UTC timestamp and hello failure details.</span></span> <span data-ttu-id="5a325-136">Por exemplo, considere uma instância de caos definida toorun para uma hora com um máximo de três falhas simultâneas.</span><span class="sxs-lookup"><span data-stu-id="5a325-136">For example, consider an instance of Chaos that is set toorun for an hour with a maximum of three concurrent faults.</span></span> <span data-ttu-id="5a325-137">Caos induzir três falhas e, em seguida, valida a integridade do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="5a325-137">Chaos induces three faults, and then validates hello cluster health.</span></span> <span data-ttu-id="5a325-138">Ele itera Olá anterior passa etapa até que seja explicitamente interrompido por meio de saudação StopChaosAsync API ou uma hora.</span><span class="sxs-lookup"><span data-stu-id="5a325-138">It iterates through hello previous step until it is explicitly stopped through hello StopChaosAsync API or one-hour passes.</span></span> <span data-ttu-id="5a325-139">Se o cluster de saudação se tornará não íntegro em qualquer iteração (ou seja, ele não estabilizar em Olá passado no MaxClusterStabilizationTimeout), caos gera um ValidationFailedEvent.</span><span class="sxs-lookup"><span data-stu-id="5a325-139">If hello cluster becomes unhealthy in any iteration (that is, it does not stabilize within hello passed-in MaxClusterStabilizationTimeout), Chaos generates a ValidationFailedEvent.</span></span> <span data-ttu-id="5a325-140">Esse evento indica que algo deu errado e pode precisar de mais investigação.</span><span class="sxs-lookup"><span data-stu-id="5a325-140">This event indicates that something has gone wrong and might need further investigation.</span></span>

<span data-ttu-id="5a325-141">tooget que falhas de caos induzido, você pode usar a API GetChaosReport (powershell ou c#).</span><span class="sxs-lookup"><span data-stu-id="5a325-141">tooget which faults Chaos induced, you can use GetChaosReport API (powershell or C#).</span></span> <span data-ttu-id="5a325-142">Olá API obtém o próximo segmento de saudação do hello caos relatório com base em token de continuação passado hello ou Olá passado no intervalo de tempo.</span><span class="sxs-lookup"><span data-stu-id="5a325-142">hello API gets hello next segment of hello Chaos report based on hello passed-in continuation token or hello passed-in time-range.</span></span> <span data-ttu-id="5a325-143">Você pode especificar Olá ContinuationToken tooget Olá próximo segmento de relatório de caos hello ou você pode especificar Olá-intervalo de tempo por meio de StartTimeUtc e EndTimeUtc, mas você não pode especificar Olá ContinuationToken e o intervalo de tempo de saudação em Olá mesma chamada.</span><span class="sxs-lookup"><span data-stu-id="5a325-143">You can either specify hello ContinuationToken tooget hello next segment of hello Chaos report or you can specify hello time-range through StartTimeUtc and EndTimeUtc, but you cannot specify both hello ContinuationToken and hello time-range in hello same call.</span></span> <span data-ttu-id="5a325-144">Quando há mais de 100 eventos caos, Olá relatório caos é retornado em segmentos onde um segmento contém eventos de caos não mais do que 100.</span><span class="sxs-lookup"><span data-stu-id="5a325-144">When there are more than 100 Chaos events, hello Chaos report is returned in segments where a segment contains no more than 100 Chaos events.</span></span>

## <a name="important-configuration-options"></a><span data-ttu-id="5a325-145">Opções de configuração importantes</span><span class="sxs-lookup"><span data-stu-id="5a325-145">Important configuration options</span></span>
* <span data-ttu-id="5a325-146">**TimeToRun**: tempo total durante o qual o Chaos é executado antes de ser finalizado com êxito.</span><span class="sxs-lookup"><span data-stu-id="5a325-146">**TimeToRun**: Total time that Chaos runs before it finishes with success.</span></span> <span data-ttu-id="5a325-147">Você pode interromper caos antes que ele tenha executado por período de TimeToRun Olá Olá StopChaos API.</span><span class="sxs-lookup"><span data-stu-id="5a325-147">You can stop Chaos before it has run for hello TimeToRun period through hello StopChaos API.</span></span>

* <span data-ttu-id="5a325-148">**MaxClusterStabilizationTimeout**: quantidade máxima de saudação do tempo toowait para Olá cluster toobecome Íntegro antes de produzir um ValidationFailedEvent.</span><span class="sxs-lookup"><span data-stu-id="5a325-148">**MaxClusterStabilizationTimeout**: hello maximum amount of time toowait for hello cluster toobecome healthy before producing a ValidationFailedEvent.</span></span> <span data-ttu-id="5a325-149">Essa espera é tooreduce Olá carga no cluster Olá enquanto está recuperando.</span><span class="sxs-lookup"><span data-stu-id="5a325-149">This wait is tooreduce hello load on hello cluster while it is recovering.</span></span> <span data-ttu-id="5a325-150">Olá verificações realizadas são:</span><span class="sxs-lookup"><span data-stu-id="5a325-150">hello checks performed are:</span></span>
  * <span data-ttu-id="5a325-151">Se a integridade do cluster Olá é Okey</span><span class="sxs-lookup"><span data-stu-id="5a325-151">If hello cluster health is OK</span></span>
  * <span data-ttu-id="5a325-152">Se a integridade do serviço Olá é Okey</span><span class="sxs-lookup"><span data-stu-id="5a325-152">If hello service health is OK</span></span>
  * <span data-ttu-id="5a325-153">Se o tamanho do conjunto de réplicas de destino de saudação é obtida para a partição de serviço Olá</span><span class="sxs-lookup"><span data-stu-id="5a325-153">If hello target replica set size is achieved for hello service partition</span></span>
  * <span data-ttu-id="5a325-154">Não há réplicas InBuild</span><span class="sxs-lookup"><span data-stu-id="5a325-154">That no InBuild replicas exist</span></span>
* <span data-ttu-id="5a325-155">**MaxConcurrentFaults**: Olá número máximo de falhas simultâneas que são induzidos em cada iteração.</span><span class="sxs-lookup"><span data-stu-id="5a325-155">**MaxConcurrentFaults**: hello maximum number of concurrent faults that are induced in each iteration.</span></span> <span data-ttu-id="5a325-156">número mais alto de Olá Olá, hello mais agressiva é caos e Olá failovers e hello estado transição combinações Olá cluster passa por também são mais complexos.</span><span class="sxs-lookup"><span data-stu-id="5a325-156">hello higher hello number, hello more aggressive Chaos is and hello failovers and hello state transition combinations that hello cluster goes through are also more complex.</span></span> 

> [!NOTE]
> <span data-ttu-id="5a325-157">Independentemente um valor alto como *MaxConcurrentFaults* tem caos garante - na ausência de saudação de falhas externas - não há perda de quorum ou perda de dados.</span><span class="sxs-lookup"><span data-stu-id="5a325-157">Regardless how high a value *MaxConcurrentFaults* has, Chaos guarantees - in hello absence of external faults - there is no quorum loss or data loss.</span></span>
>

* <span data-ttu-id="5a325-158">**EnableMoveReplicaFaults**: habilita ou desabilita a falhas de saudação que provocam Olá réplicas primárias ou secundárias toomove.</span><span class="sxs-lookup"><span data-stu-id="5a325-158">**EnableMoveReplicaFaults**: Enables or disables hello faults that cause hello primary or secondary replicas toomove.</span></span> <span data-ttu-id="5a325-159">Essas falhas estão desabilitadas por padrão.</span><span class="sxs-lookup"><span data-stu-id="5a325-159">These faults are disabled by default.</span></span>
* <span data-ttu-id="5a325-160">**WaitTimeBetweenIterations**: quantidade de saudação do toowait de tempo entre as iterações.</span><span class="sxs-lookup"><span data-stu-id="5a325-160">**WaitTimeBetweenIterations**: hello amount of time toowait between iterations.</span></span> <span data-ttu-id="5a325-161">Ou seja, Olá que caos fará uma pausa após ter executado uma rodada de falhas e ter concluído a validação correspondente Olá de integridade de saudação do cluster de saudação do tempo.</span><span class="sxs-lookup"><span data-stu-id="5a325-161">That is, hello amount of time Chaos will pause after having executed a round of faults and having finished hello corresponding validation of hello health of hello cluster.</span></span> <span data-ttu-id="5a325-162">Olá valor mais alto do hello, Olá inferior é a taxa de injeção de média de falhas de saudação.</span><span class="sxs-lookup"><span data-stu-id="5a325-162">hello higher hello value, hello lower is hello average fault injection rate.</span></span>
* <span data-ttu-id="5a325-163">**WaitTimeBetweenFaults**: quantidade de saudação do toowait de tempo entre duas falhas consecutivas em uma única iteração.</span><span class="sxs-lookup"><span data-stu-id="5a325-163">**WaitTimeBetweenFaults**: hello amount of time toowait between two consecutive faults in a single iteration.</span></span> <span data-ttu-id="5a325-164">Olá valor mais alto de hello, Olá inferior simultaneidade de saudação do (ou Olá sobreposição entre) falhas.</span><span class="sxs-lookup"><span data-stu-id="5a325-164">hello higher hello value, hello lower hello concurrency of (or hello overlap between) faults.</span></span>
* <span data-ttu-id="5a325-165">**ClusterHealthPolicy**: política de integridade do Cluster é toovalidate usado Olá integridade de cluster Olá entre iterações de caos.</span><span class="sxs-lookup"><span data-stu-id="5a325-165">**ClusterHealthPolicy**: Cluster health policy is used toovalidate hello health of hello cluster in between Chaos iterations.</span></span> <span data-ttu-id="5a325-166">Se a integridade do cluster Olá é um erro ou se ocorrer uma exceção inesperada durante a execução de falhas, caos aguardará 30 minutos antes de saudação próxima verificação de integridade - cluster de saudação tooprovide com toorecuperate algum tempo.</span><span class="sxs-lookup"><span data-stu-id="5a325-166">If hello cluster health is in error or if an unexpected exception happens during fault execution, Chaos will wait for 30 minutes before hello next health-check - tooprovide hello cluster with some time toorecuperate.</span></span>
* <span data-ttu-id="5a325-167">**Contexto**: uma coleção pares chave/valor do tipo (cadeia de caracteres, cadeia de caracteres).</span><span class="sxs-lookup"><span data-stu-id="5a325-167">**Context**: A collection of (string, string) type key-value pairs.</span></span> <span data-ttu-id="5a325-168">mapa de saudação pode ser usado toorecord saber Olá caos executar.</span><span class="sxs-lookup"><span data-stu-id="5a325-168">hello map can be used toorecord information about hello Chaos run.</span></span> <span data-ttu-id="5a325-169">Não pode haver mais de 100 desses pares e cada cadeia de caracteres (chave ou valor) pode ter no máximo 4095 caracteres.</span><span class="sxs-lookup"><span data-stu-id="5a325-169">There cannot be more than 100 such pairs and each string (key or value) can be at most 4095 characters long.</span></span> <span data-ttu-id="5a325-170">Este mapa é definido pelo inicializador de saudação do contexto de saudação de repositório Olá caos executar toooptionally sobre Olá específico execute.</span><span class="sxs-lookup"><span data-stu-id="5a325-170">This map is set by hello starter of hello Chaos run toooptionally store hello context about hello specific run.</span></span>

## <a name="how-toorun-chaos"></a><span data-ttu-id="5a325-171">Como toorun caos</span><span class="sxs-lookup"><span data-stu-id="5a325-171">How toorun Chaos</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Threading.Tasks;
using System.Fabric;

using System.Diagnostics;
using System.Fabric.Chaos.DataStructures;

class Program
{
    private class ChaosEventComparer : IEqualityComparer<ChaosEvent>
    {
        public bool Equals(ChaosEvent x, ChaosEvent y)
        {
            return x.TimeStampUtc.Equals(y.TimeStampUtc);
        }

        public int GetHashCode(ChaosEvent obj)
        {
            return obj.TimeStampUtc.GetHashCode();
        }
    }

    static void Main(string[] args)
    {
        var clusterConnectionString = "localhost:19000";
        using (var client = new FabricClient(clusterConnectionString))
        {
            var startTimeUtc = DateTime.UtcNow;
            var stabilizationTimeout = TimeSpan.FromSeconds(30.0);
            var timeToRun = TimeSpan.FromMinutes(60.0);
            var maxConcurrentFaults = 3;

            var parameters = new ChaosParameters(
                stabilizationTimeout,
                maxConcurrentFaults,
                true, /* EnableMoveReplicaFault */
                timeToRun);

            try
            {
                client.TestManager.StartChaosAsync(parameters).GetAwaiter().GetResult();
            }
            catch (FabricChaosAlreadyRunningException)
            {
                Console.WriteLine("An instance of Chaos is already running in hello cluster.");
            }

            var filter = new ChaosReportFilter(startTimeUtc, DateTime.MaxValue);

            var eventSet = new HashSet<ChaosEvent>(new ChaosEventComparer());

            while (true)
            {
                var report = client.TestManager.GetChaosReportAsync(filter).GetAwaiter().GetResult();

                foreach (var chaosEvent in report.History)
                {
                    if (eventSet.Add(chaosEvent))
                    {
                        Console.WriteLine(chaosEvent);
                    }
                }

                // When Chaos stops, a StoppedEvent is created.
                // If a StoppedEvent is found, exit hello loop.
                var lastEvent = report.History.LastOrDefault();

                if (lastEvent is StoppedEvent)
                {
                    break;
                }

                Task.Delay(TimeSpan.FromSeconds(1.0)).GetAwaiter().GetResult();
            }
        }
    }
}
```

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

$events = @{}
$now = [System.DateTime]::UtcNow

Start-ServiceFabricChaos -TimeToRunMinute $timeToRun -MaxConcurrentFaults $concurrentFaults -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec

while($true)
{
    $stopped = $false
    $report = Get-ServiceFabricChaosReport -StartTimeUtc $now -EndTimeUtc ([System.DateTime]::MaxValue)

    foreach ($e in $report.History) {

        if(-Not ($events.Contains($e.TimeStampUtc.Ticks)))
        {
            $events.Add($e.TimeStampUtc.Ticks, $e)
            if($e -is [System.Fabric.Chaos.DataStructures.ValidationFailedEvent])
            {
                Write-Host -BackgroundColor White -ForegroundColor Red $e
            }
            else
            {
                if($e -is [System.Fabric.Chaos.DataStructures.StoppedEvent])
                {
                    $stopped = $true
                }

                Write-Host $e
            }
        }
    }

    if($stopped -eq $true)
    {
        break
    }

    Start-Sleep -Seconds 1
}

Stop-ServiceFabricChaos
```
