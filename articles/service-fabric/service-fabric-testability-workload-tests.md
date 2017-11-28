---
title: "Simular falhas nos microsserviços do Azure | Microsoft Docs"
description: "Como fortalecer seus serviços contra falhas normais/anormais."
services: service-fabric
documentationcenter: .net
author: anmolah
manager: timlt
editor: 
ms.assetid: 44af01f0-ed73-4c31-8ac0-d9d65b4ad2d6
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: anmola
ms.openlocfilehash: 7ec671c23e101d0f7401bd4656fb201111602cad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="simulate-failures-during-service-workloads"></a><span data-ttu-id="08e07-103">Simular falhas durante cargas de trabalho de serviço</span><span class="sxs-lookup"><span data-stu-id="08e07-103">Simulate failures during service workloads</span></span>
<span data-ttu-id="08e07-104">Os cenários de possibilidade de teste no Service Fabric do Azure isentam os desenvolvedores da preocupação com o tratamento de falhas individuais.</span><span class="sxs-lookup"><span data-stu-id="08e07-104">The testability scenarios in Azure Service Fabric enable developers to not worry about dealing with individual faults.</span></span> <span data-ttu-id="08e07-105">No entanto, há cenários em que uma intercalação explícita das falhas e da carga de trabalho do cliente pode ser necessária.</span><span class="sxs-lookup"><span data-stu-id="08e07-105">There are scenarios, however, where an explicit interleaving of client workload and failures might be needed.</span></span> <span data-ttu-id="08e07-106">A intercalação das falhas e da carga de trabalho do cliente garante que o serviço realmente execute alguma ação quando a falha acontece.</span><span class="sxs-lookup"><span data-stu-id="08e07-106">The interleaving of client workload and faults ensures that the service is actually performing some action when failure happens.</span></span> <span data-ttu-id="08e07-107">Dado o nível de controle que a possibilidade de teste fornece, elas podem estar em pontos precisos da execução da carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="08e07-107">Given the level of control that testability provides, these could be at precise points of the workload execution.</span></span> <span data-ttu-id="08e07-108">Essa indução de falhas em diferentes estados no aplicativo pode encontrar bugs e melhorar a qualidade.</span><span class="sxs-lookup"><span data-stu-id="08e07-108">This induction of faults at different states in the application can find bugs and improve quality.</span></span>

## <a name="sample-custom-scenario"></a><span data-ttu-id="08e07-109">Exemplo de cenário personalizado</span><span class="sxs-lookup"><span data-stu-id="08e07-109">Sample custom scenario</span></span>
<span data-ttu-id="08e07-110">Esse teste mostra um cenário que intercala a carga de trabalho de negócios com [falhas normais e anormais](service-fabric-testability-actions.md#graceful-vs-ungraceful-fault-actions).</span><span class="sxs-lookup"><span data-stu-id="08e07-110">This test shows a scenario that interleaves the business workload with [graceful and ungraceful failures](service-fabric-testability-actions.md#graceful-vs-ungraceful-fault-actions).</span></span> <span data-ttu-id="08e07-111">As falhas devem ser induzidas durante as operações ou cálculos do serviço para obter melhores resultados.</span><span class="sxs-lookup"><span data-stu-id="08e07-111">The faults should be induced in the middle of service operations or compute for best results.</span></span>

<span data-ttu-id="08e07-112">Vamos examinar um exemplo de um serviço que expõe quatro cargas de trabalho: A, B, C e D. Cada uma corresponde a um conjunto de fluxos de trabalho que pode ser computação, armazenamento ou uma combinação.</span><span class="sxs-lookup"><span data-stu-id="08e07-112">Let's walk through an example of a service that exposes four workloads: A, B, C, and D. Each corresponds to a set of workflows and could be compute, storage, or a mix.</span></span> <span data-ttu-id="08e07-113">Para simplificar, vamos abstrair as cargas de trabalho de nosso exemplo.</span><span class="sxs-lookup"><span data-stu-id="08e07-113">For the sake of simplicity, we will abstract out the workloads in our example.</span></span> <span data-ttu-id="08e07-114">As diferentes falhas executadas neste exemplo são:</span><span class="sxs-lookup"><span data-stu-id="08e07-114">The different faults executed in this example are:</span></span>

* <span data-ttu-id="08e07-115">RestartNode: falha anormal para simular uma reinicialização do computador.</span><span class="sxs-lookup"><span data-stu-id="08e07-115">RestartNode: Ungraceful fault to simulate a machine restart.</span></span>
* <span data-ttu-id="08e07-116">RestartDeployedCodePackage: falha anormal para simular uma falha do processo de host de serviço.</span><span class="sxs-lookup"><span data-stu-id="08e07-116">RestartDeployedCodePackage: Ungraceful fault to simulate service host process crashes.</span></span>
* <span data-ttu-id="08e07-117">RemoveReplica: falha normal para simular remoção de réplica.</span><span class="sxs-lookup"><span data-stu-id="08e07-117">RemoveReplica: Graceful fault to simulate replica removal.</span></span>
* <span data-ttu-id="08e07-118">MovePrimary: falha normal para simular movimentações de réplica disparadas pelo balanceador de carga do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="08e07-118">MovePrimary: Graceful fault to simulate replica moves triggered by the Service Fabric load balancer.</span></span>

```csharp
// Add a reference to System.Fabric.Testability.dll and System.Fabric.dll.

using System;
using System.Fabric;
using System.Fabric.Testability.Scenario;
using System.Threading;
using System.Threading.Tasks;

class Test
{
    public static int Main(string[] args)
    {
        // Replace these strings with the actual version for your cluster and application.
        string clusterConnection = "localhost:19000";
        Uri applicationName = new Uri("fabric:/samples/PersistentToDoListApp");
        Uri serviceName = new Uri("fabric:/samples/PersistentToDoListApp/PersistentToDoListService");

        Console.WriteLine("Starting Workload Test...");
        try
        {
            RunTestAsync(clusterConnection, applicationName, serviceName).Wait();
        }
        catch (AggregateException ae)
        {
            Console.WriteLine("Workload Test failed: ");
            foreach (Exception ex in ae.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("Workload Test completed successfully.");
        return 0;
    }

    public enum ServiceWorkloads
    {
        A,
        B,
        C,
        D
    }

    public enum ServiceFabricFaults
    {
        RestartNode,
        RestartCodePackage,
        RemoveReplica,
        MovePrimary,
    }

    public static async Task RunTestAsync(string clusterConnection, Uri applicationName, Uri serviceName)
    {
        // Create FabricClient with connection and security information here.
        FabricClient fabricClient = new FabricClient(clusterConnection);
        // Maximum time to wait for a service to stabilize.
        TimeSpan maxServiceStabilizationTime = TimeSpan.FromSeconds(120);

        // How many loops of faults you want to execute.
        uint testLoopCount = 20;
        Random random = new Random();

        for (var i = 0; i < testLoopCount; ++i)
        {
            var workload = SelectRandomValue<ServiceWorkloads>(random);
            // Start the workload.
            var workloadTask = RunWorkloadAsync(workload);

            // While the task is running, induce faults into the service. They can be ungraceful faults like
            // RestartNode and RestartDeployedCodePackage or graceful faults like RemoveReplica or MovePrimary.
            var fault = SelectRandomValue<ServiceFabricFaults>(random);

            // Create a replica selector, which will select a primary replica from the given service to test.
            var replicaSelector = ReplicaSelector.PrimaryOf(PartitionSelector.RandomOf(serviceName));
            // Run the selected random fault.
            await RunFaultAsync(applicationName, fault, replicaSelector, fabricClient);
            // Validate the health and stability of the service.
            await fabricClient.ServiceManager.ValidateServiceAsync(serviceName, maxServiceStabilizationTime);

            // Wait for the workload to finish successfully.
            await workloadTask;
        }
    }

    private static async Task RunFaultAsync(Uri applicationName, ServiceFabricFaults fault, ReplicaSelector selector, FabricClient client)
    {
        switch (fault)
        {
            case ServiceFabricFaults.RestartNode:
                await client.ClusterManager.RestartNodeAsync(selector, CompletionMode.Verify);
                break;
            case ServiceFabricFaults.RestartCodePackage:
                await client.ApplicationManager.RestartDeployedCodePackageAsync(applicationName, selector, CompletionMode.Verify);
                break;
            case ServiceFabricFaults.RemoveReplica:
                await client.ServiceManager.RemoveReplicaAsync(selector, CompletionMode.Verify, false);
                break;
            case ServiceFabricFaults.MovePrimary:
                await client.ServiceManager.MovePrimaryAsync(selector.PartitionSelector);
                break;
        }
    }

    private static Task RunWorkloadAsync(ServiceWorkloads workload)
    {
        throw new NotImplementedException();
        // This is where you trigger and complete your service workload.
        // Note that the faults induced while your service workload is running will
        // fault the primary service. Hence, you will need to reconnect to complete or check
        // the status of the workload.
    }

    private static T SelectRandomValue<T>(Random random)
    {
        Array values = Enum.GetValues(typeof(T));
        T workload = (T)values.GetValue(random.Next(values.Length));
        return workload;
    }
}
```
