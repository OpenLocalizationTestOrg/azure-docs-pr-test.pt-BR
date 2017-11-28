---
title: Induzir o Chaos em clusters do Service Fabric | Microsoft Docs
description: "Como usar as APIs de serviço de Injeção de falhas e análise de cluster para gerenciar o Chaos no cluster."
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
ms.openlocfilehash: 3b3b93bc9ec5ecdcfc289e5b62e84de6aa4172ed
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="induce-controlled-chaos-in-service-fabric-clusters"></a><span data-ttu-id="6b9ec-103">Induzir o Controlled Chaos em clusters do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6b9ec-103">Induce controlled Chaos in Service Fabric clusters</span></span>
<span data-ttu-id="6b9ec-104">Os sistemas distribuídos em larga escala, como as infraestruturas de nuvem, não são confiáveis por natureza.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-104">Large-scale distributed systems like cloud infrastructures are inherently unreliable.</span></span> <span data-ttu-id="6b9ec-105">O Azure Service Fabric permite aos desenvolvedores escrever serviços distribuídos confiáveis sobre uma infraestrutura não confiável.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-105">Azure Service Fabric enables developers to write reliable distributed services on top of an unreliable infrastructure.</span></span> <span data-ttu-id="6b9ec-106">Para gravar serviços distribuídos robustos sobre uma infraestrutura não confiável, os desenvolvedores precisam poder testar a estabilidade de seus serviços enquanto a infraestrutura subjacente não confiável está passando por transições de estado complicadas devido a falhas.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-106">To write robust distributed services on top of an unreliable infrastructure, developers need to be able to test the stability of their services while the underlying unreliable infrastructure is going through complicated state transitions due to faults.</span></span>

<span data-ttu-id="6b9ec-107">O [Serviço de Injeção de Falhas e Análise de Cluster](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-testability-overview) (também conhecido como Serviço de Análise de Falhas) fornece aos desenvolvedores a capacidade de induzir falhas para testar os serviços.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-107">The [Fault Injection and Cluster Analysis Service](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-testability-overview) (also known as the Fault Analysis Service) gives developers the ability to induce faults to test their services.</span></span> <span data-ttu-id="6b9ec-108">Essas falhas simuladas direcionadas, como [reiniciar uma partição](https://docs.microsoft.com/en-us/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps), podem ajudar a praticar as transições de estado mais comuns.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-108">These targeted simulated faults, like [restarting a partition](https://docs.microsoft.com/en-us/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps), can help exercise the most common state transitions.</span></span> <span data-ttu-id="6b9ec-109">No entanto, as falhas simuladas direcionadas são tendenciosas por definição e, portanto, podem ignorar bugs que aparecem apenas em uma sequência de transições de estado complicada, longa e difícil de prever.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-109">However targeted simulated faults are biased by definition and thus may miss bugs that show up only in hard-to-predict, long and complicated sequence of state transitions.</span></span> <span data-ttu-id="6b9ec-110">Para um teste imparcial, você pode usar o Chaos.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-110">For an unbiased testing, you can use Chaos.</span></span>

<span data-ttu-id="6b9ec-111">O Chaos simula falhas intercaladas periódicas (amigáveis e não amigáveis) em todo o cluster durante longos períodos de tempo.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-111">Chaos simulates periodic, interleaved faults (both graceful and ungraceful) throughout the cluster over extended periods of time.</span></span> <span data-ttu-id="6b9ec-112">Depois que tiver configurado o Chaos com a taxa e o tipo de falhas, você pode iniciar o Chaos pela API do PowerShell ou C# para começar a gerar falhas no cluster e nos serviços.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-112">Once you have configured Chaos with the rate and the kind of faults, you can start Chaos through C# or Powershell API to start generating faults in the cluster and in your services.</span></span> <span data-ttu-id="6b9ec-113">Você pode configurar o Chaos para ser executado por um período especificado (por exemplo, por uma hora), após o qual o Chaos para automaticamente ou pode chamar a API StopChaos (C# ou PowerShell) para pará-lo a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-113">You can configure Chaos to run for a specified time period (for example, for one hour), after which Chaos stops automatically, or you can call StopChaos API (C# or Powershell) to stop it at any time.</span></span>

> [!NOTE]
> <span data-ttu-id="6b9ec-114">Em sua forma atual, o Chaos induz apenas falhas seguras, o que significa que, na ausência de falhas externas, uma perda de quórum ou uma perda de dados nunca ocorrerá.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-114">In its current form, Chaos induces only safe faults, which implies that in the absence of external faults a quorum loss, or data loss never occurs.</span></span>
>

<span data-ttu-id="6b9ec-115">Enquanto o Chaos estiver em execução, ele produzirá eventos diferentes que capturam o estado da execução no momento.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-115">While Chaos is running, it produces different events that capture the state of the run at the moment.</span></span> <span data-ttu-id="6b9ec-116">Por exemplo, um ExecutingFaultsEvent contém todas as falhas que o Chaos decidiu executar na iteração.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-116">For example, an ExecutingFaultsEvent contains all the faults that Chaos has decided to execute in that iteration.</span></span> <span data-ttu-id="6b9ec-117">Um ValidationFailedEvent contém os detalhes de uma falha de validação (problemas de integridade ou estabilidade) encontrada durante a validação do cluster.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-117">A ValidationFailedEvent contains the details of a validation failure (health or stability issues) that was found during the validation of the cluster.</span></span> <span data-ttu-id="6b9ec-118">Você pode invocar a API GetChaosReport (C# ou PowerShell) para obter o relatório de execuções do Chaos.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-118">You can invoke the GetChaosReport API (C# or Powershell) to get the report of Chaos runs.</span></span> <span data-ttu-id="6b9ec-119">Esses eventos são persistidos em um [dicionário confiável](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-reliable-collections), que tem uma política de truncamento determinada por duas configurações: **MaxStoredChaosEventCount** (o valor padrão é 25000) e **StoredActionCleanupIntervalInSeconds** (o valor padrão é 3600).</span><span class="sxs-lookup"><span data-stu-id="6b9ec-119">These events get persisted in a [reliable dictionary](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-reliable-collections), which has a truncation policy dictated by two configurations: **MaxStoredChaosEventCount** (default value is 25000) and **StoredActionCleanupIntervalInSeconds** (default value is 3600).</span></span> <span data-ttu-id="6b9ec-120">Todas as verificações do Chaos *StoredActionCleanupIntervalInSeconds* e todos os eventos *MaxStoredChaosEventCount*, exceto os mais recentes, são limpos do dicionário confiável.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-120">Every *StoredActionCleanupIntervalInSeconds* Chaos checks and all but the most recent *MaxStoredChaosEventCount* events, are purged from the reliable dictionary.</span></span>

## <a name="faults-induced-in-chaos"></a><span data-ttu-id="6b9ec-121">Falhas induzidas no Chaos</span><span class="sxs-lookup"><span data-stu-id="6b9ec-121">Faults induced in Chaos</span></span>
<span data-ttu-id="6b9ec-122">O Chaos gera falhas em todo o cluster do Service Fabric e compacta as falhas vistas em meses ou anos em poucas horas.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-122">Chaos generates faults across the entire Service Fabric cluster and compresses faults that are seen in months or years into a few hours.</span></span> <span data-ttu-id="6b9ec-123">A combinação de falhas intercaladas com a alta taxa de falhas localiza casos específicos que de outra forma seriam ignorados.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-123">The combination of interleaved faults with the high fault rate finds corner cases that may otherwise be missed.</span></span> <span data-ttu-id="6b9ec-124">Esse exercício do Chaos leva a uma melhoria significativa na qualidade do código do serviço.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-124">This exercise of Chaos leads to a significant improvement in the code quality of the service.</span></span>

<span data-ttu-id="6b9ec-125">O Chaos induz falhas a partir das seguintes categorias:</span><span class="sxs-lookup"><span data-stu-id="6b9ec-125">Chaos induces faults from the following categories:</span></span>

* <span data-ttu-id="6b9ec-126">Reiniciar um nó</span><span class="sxs-lookup"><span data-stu-id="6b9ec-126">Restart a node</span></span>
* <span data-ttu-id="6b9ec-127">Reiniciar um pacote de códigos implantado</span><span class="sxs-lookup"><span data-stu-id="6b9ec-127">Restart a deployed code package</span></span>
* <span data-ttu-id="6b9ec-128">Remover uma réplica</span><span class="sxs-lookup"><span data-stu-id="6b9ec-128">Remove a replica</span></span>
* <span data-ttu-id="6b9ec-129">Reiniciar uma réplica</span><span class="sxs-lookup"><span data-stu-id="6b9ec-129">Restart a replica</span></span>
* <span data-ttu-id="6b9ec-130">Mover uma réplica primária (configurável)</span><span class="sxs-lookup"><span data-stu-id="6b9ec-130">Move a primary replica (configurable)</span></span>
* <span data-ttu-id="6b9ec-131">Mover uma réplica secundária (configurável)</span><span class="sxs-lookup"><span data-stu-id="6b9ec-131">Move a secondary replica (configurable)</span></span>

<span data-ttu-id="6b9ec-132">O Chaos é executado em várias iterações.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-132">Chaos runs in multiple iterations.</span></span> <span data-ttu-id="6b9ec-133">Cada iteração é composta por falhas e validações de cluster para o período especificado.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-133">Each iteration consists of faults and cluster validation for the specified period.</span></span> <span data-ttu-id="6b9ec-134">Você pode configurar o tempo gasto para o cluster se estabilizar e a validação de êxito.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-134">You can configure the time spent for the cluster to stabilize and for validation to succeed.</span></span> <span data-ttu-id="6b9ec-135">Se uma falha for encontrada na validação do cluster, o Chaos gerará e persistirá um ValidationFailedEvent com o carimbo de data/hora UTC e os detalhes da falha.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-135">If a failure is found in cluster validation, Chaos generates and persists a ValidationFailedEvent with the UTC timestamp and the failure details.</span></span> <span data-ttu-id="6b9ec-136">Por exemplo, considere uma instância do Chaos, definida para ser executada por uma hora com, no máximo, três falhas simultâneas.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-136">For example, consider an instance of Chaos that is set to run for an hour with a maximum of three concurrent faults.</span></span> <span data-ttu-id="6b9ec-137">O Chaos induz três falhas e valida a integridade do cluster.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-137">Chaos induces three faults, and then validates the cluster health.</span></span> <span data-ttu-id="6b9ec-138">Ele itera através da etapa anterior até que seja explicitamente interrompido por meio da API StopChaosAsync ou após uma hora.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-138">It iterates through the previous step until it is explicitly stopped through the StopChaosAsync API or one-hour passes.</span></span> <span data-ttu-id="6b9ec-139">Se o cluster se tornar não íntegro em qualquer iteração (ou seja, não se estabilizar dentro do MaxClusterStabilizationTimeout repassado), o Chaos gerará um ValidationFailedEvent.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-139">If the cluster becomes unhealthy in any iteration (that is, it does not stabilize within the passed-in MaxClusterStabilizationTimeout), Chaos generates a ValidationFailedEvent.</span></span> <span data-ttu-id="6b9ec-140">Esse evento indica que algo deu errado e pode precisar de mais investigação.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-140">This event indicates that something has gone wrong and might need further investigation.</span></span>

<span data-ttu-id="6b9ec-141">Para obter quais falhas o Chaos induziu, você pode usar a API GetChaosReport (PowerShell ou C#).</span><span class="sxs-lookup"><span data-stu-id="6b9ec-141">To get which faults Chaos induced, you can use GetChaosReport API (powershell or C#).</span></span> <span data-ttu-id="6b9ec-142">A API obtém o próximo segmento do relatório do Chaos com base no token de continuação repassado ou no intervalo repassado.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-142">The API gets the next segment of the Chaos report based on the passed-in continuation token or the passed-in time-range.</span></span> <span data-ttu-id="6b9ec-143">Você pode especificar o ContinuationToken para obter o próximo segmento do relatório do Chaos ou especificar o intervalo por meio de StartTimeUtc e EndTimeUtc, mas não pode especificar o ContinuationToken e o intervalo de tempo na mesma chamada.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-143">You can either specify the ContinuationToken to get the next segment of the Chaos report or you can specify the time-range through StartTimeUtc and EndTimeUtc, but you cannot specify both the ContinuationToken and the time-range in the same call.</span></span> <span data-ttu-id="6b9ec-144">Quando há mais de 100 eventos do Chaos, o relatório do Chaos é retornado em segmentos, em que um segmento contém no máximo 100 eventos do Chaos.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-144">When there are more than 100 Chaos events, the Chaos report is returned in segments where a segment contains no more than 100 Chaos events.</span></span>

## <a name="important-configuration-options"></a><span data-ttu-id="6b9ec-145">Opções de configuração importantes</span><span class="sxs-lookup"><span data-stu-id="6b9ec-145">Important configuration options</span></span>
* <span data-ttu-id="6b9ec-146">**TimeToRun**: tempo total durante o qual o Chaos é executado antes de ser finalizado com êxito.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-146">**TimeToRun**: Total time that Chaos runs before it finishes with success.</span></span> <span data-ttu-id="6b9ec-147">Você pode interromper o Chaos antes que ele seja executado pelo período de TimeToRun usando a API StopChaos.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-147">You can stop Chaos before it has run for the TimeToRun period through the StopChaos API.</span></span>

* <span data-ttu-id="6b9ec-148">**MaxClusterStabilizationTimeout**: a quantidade máxima de tempo de espera para que o cluster se torne íntegro antes de produzir um ValidationFailedEvent.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-148">**MaxClusterStabilizationTimeout**: The maximum amount of time to wait for the cluster to become healthy before producing a ValidationFailedEvent.</span></span> <span data-ttu-id="6b9ec-149">Essa espera serve para reduzir a carga no cluster enquanto ele está se recuperando.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-149">This wait is to reduce the load on the cluster while it is recovering.</span></span> <span data-ttu-id="6b9ec-150">As verificações executadas são:</span><span class="sxs-lookup"><span data-stu-id="6b9ec-150">The checks performed are:</span></span>
  * <span data-ttu-id="6b9ec-151">Se a integridade do cluster está OK</span><span class="sxs-lookup"><span data-stu-id="6b9ec-151">If the cluster health is OK</span></span>
  * <span data-ttu-id="6b9ec-152">Se a integridade do serviço está OK</span><span class="sxs-lookup"><span data-stu-id="6b9ec-152">If the service health is OK</span></span>
  * <span data-ttu-id="6b9ec-153">Se o tamanho do conjunto de réplicas de destino é obtido para a partição de serviço</span><span class="sxs-lookup"><span data-stu-id="6b9ec-153">If the target replica set size is achieved for the service partition</span></span>
  * <span data-ttu-id="6b9ec-154">Não há réplicas InBuild</span><span class="sxs-lookup"><span data-stu-id="6b9ec-154">That no InBuild replicas exist</span></span>
* <span data-ttu-id="6b9ec-155">**MaxConcurrentFaults**: o número máximo de falhas simultâneas induzidas em cada iteração.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-155">**MaxConcurrentFaults**: The maximum number of concurrent faults that are induced in each iteration.</span></span> <span data-ttu-id="6b9ec-156">Quanto maior o número, mais agressivo o Chaos é e os failovers e as combinações de transição de estado pelos quais o cluster passa também são mais complexas.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-156">The higher the number, the more aggressive Chaos is and the failovers and the state transition combinations that the cluster goes through are also more complex.</span></span> 

> [!NOTE]
> <span data-ttu-id="6b9ec-157">Independentemente de quão alto um valor de *MaxConcurrentFaults* está, o Chaos garante, na ausência de falhas externas, que não há perda de quorum ou perda de dados.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-157">Regardless how high a value *MaxConcurrentFaults* has, Chaos guarantees - in the absence of external faults - there is no quorum loss or data loss.</span></span>
>

* <span data-ttu-id="6b9ec-158">**EnableMoveReplicaFaults**: habilita ou desabilita as falhas que causam a movimentação das réplicas primárias ou secundárias.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-158">**EnableMoveReplicaFaults**: Enables or disables the faults that cause the primary or secondary replicas to move.</span></span> <span data-ttu-id="6b9ec-159">Essas falhas estão desabilitadas por padrão.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-159">These faults are disabled by default.</span></span>
* <span data-ttu-id="6b9ec-160">**WaitTimeBetweenIterations**: a quantidade de tempo de espera entre as iterações.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-160">**WaitTimeBetweenIterations**: The amount of time to wait between iterations.</span></span> <span data-ttu-id="6b9ec-161">Ou seja, a quantidade de tempo que pela qual o Chaos fará uma pausa após ter executado uma rodada de falhas e ter concluído a validação correspondente da integridade do cluster.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-161">That is, the amount of time Chaos will pause after having executed a round of faults and having finished the corresponding validation of the health of the cluster.</span></span> <span data-ttu-id="6b9ec-162">Quanto maior o valor, menor é a taxa de injeção de falhas média.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-162">The higher the value, the lower is the average fault injection rate.</span></span>
* <span data-ttu-id="6b9ec-163">**WaitTimeBetweenFaults**: o tempo de espera entre as duas falhas consecutivas em uma única iteração.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-163">**WaitTimeBetweenFaults**: The amount of time to wait between two consecutive faults in a single iteration.</span></span> <span data-ttu-id="6b9ec-164">Quanto maior o valor, menor a simultaneidade (ou a sobreposição entre) de falhas.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-164">The higher the value, the lower the concurrency of (or the overlap between) faults.</span></span>
* <span data-ttu-id="6b9ec-165">**ClusterHealthPolicy**: a política de integridade do cluster é usada para validar a integridade do cluster entre iterações do Chaos.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-165">**ClusterHealthPolicy**: Cluster health policy is used to validate the health of the cluster in between Chaos iterations.</span></span> <span data-ttu-id="6b9ec-166">Se a integridade do cluster estiver em erro ou se ocorrer uma exceção inesperada durante a execução de falhas, o Chaos aguardará 30 minutos antes da próxima verificação de integridade, para fornecer ao cluster algum tempo para se recuperar.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-166">If the cluster health is in error or if an unexpected exception happens during fault execution, Chaos will wait for 30 minutes before the next health-check - to provide the cluster with some time to recuperate.</span></span>
* <span data-ttu-id="6b9ec-167">**Contexto**: uma coleção pares chave/valor do tipo (cadeia de caracteres, cadeia de caracteres).</span><span class="sxs-lookup"><span data-stu-id="6b9ec-167">**Context**: A collection of (string, string) type key-value pairs.</span></span> <span data-ttu-id="6b9ec-168">O mapa pode ser usado para registrar informações sobre a execução do Chaos.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-168">The map can be used to record information about the Chaos run.</span></span> <span data-ttu-id="6b9ec-169">Não pode haver mais de 100 desses pares e cada cadeia de caracteres (chave ou valor) pode ter no máximo 4095 caracteres.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-169">There cannot be more than 100 such pairs and each string (key or value) can be at most 4095 characters long.</span></span> <span data-ttu-id="6b9ec-170">Esse mapa é definido pelo iniciador da execução do Chaos para armazenar opcionalmente o contexto sobre a execução específica.</span><span class="sxs-lookup"><span data-stu-id="6b9ec-170">This map is set by the starter of the Chaos run to optionally store the context about the specific run.</span></span>

## <a name="how-to-run-chaos"></a><span data-ttu-id="6b9ec-171">Como executar o Chaos</span><span class="sxs-lookup"><span data-stu-id="6b9ec-171">How to run Chaos</span></span>

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
                Console.WriteLine("An instance of Chaos is already running in the cluster.");
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
                // If a StoppedEvent is found, exit the loop.
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
