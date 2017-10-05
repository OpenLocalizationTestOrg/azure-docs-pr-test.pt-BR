---
title: "Como invocar a perda de dados nos serviços do Service Fabric | Microsoft Docs"
description: Descreve como usar a api de perda de dados
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
ms.openlocfilehash: 0c4791e56f84d0df38783a13c8d8c564fd25f55f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-invoke-data-loss-on-services"></a><span data-ttu-id="839bf-103">Como invocar a perda de dados nos serviços</span><span class="sxs-lookup"><span data-stu-id="839bf-103">How to Invoke Data Loss on Services</span></span>
> [!WARNING]
> <span data-ttu-id="839bf-104">Este documento descreve como fazer com que os dados em seus serviços se percam, devendo ser usado com cuidado.</span><span class="sxs-lookup"><span data-stu-id="839bf-104">This document describe how to cause data loss in your services, and should be used with care.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="839bf-105">Introdução</span><span class="sxs-lookup"><span data-stu-id="839bf-105">Introduction</span></span>
<span data-ttu-id="839bf-106">Você pode invocar a perda de dados em uma partição do serviço do Service Fabric chamando StartPartitionDataLossAsync().</span><span class="sxs-lookup"><span data-stu-id="839bf-106">You can invoke data loss on a partition of your Service Fabric Service by calling StartPartitionDataLossAsync().</span></span>  <span data-ttu-id="839bf-107">Essa api usa o Serviço de Análise e Injeção de Falha para executar o trabalho que causa as condições de perda de dados.</span><span class="sxs-lookup"><span data-stu-id="839bf-107">This api uses the Fault Injection and Analysis Service to perform the work to cause data loss conditions.</span></span>

## <a name="using-the-fault-injection-and-analysis-service"></a><span data-ttu-id="839bf-108">Usando o Serviço de Análise e Injeção de Falha</span><span class="sxs-lookup"><span data-stu-id="839bf-108">Using the Fault Injection and Analysis Service</span></span>
<span data-ttu-id="839bf-109">Atualmente, o Serviço de Análise e Injeção de Falha é compatível com as APIs do quadro abaixo.</span><span class="sxs-lookup"><span data-stu-id="839bf-109">The Fault Injection and Analysis Service currently supports the following APIs in the chart below.</span></span>  <span data-ttu-id="839bf-110">À direita, temos o cmdlet do PowerShell correspondente.</span><span class="sxs-lookup"><span data-stu-id="839bf-110">The right side of the chart shows the corresponding PowerShell cmdlet.</span></span>  <span data-ttu-id="839bf-111">Consulte a documentação do msdn em cada API para obter mais informações sobre cada uma.</span><span class="sxs-lookup"><span data-stu-id="839bf-111">Please refer to the msdn documentation on each API for more information on each one.</span></span>

| <span data-ttu-id="839bf-112">API do C#</span><span class="sxs-lookup"><span data-stu-id="839bf-112">C# API</span></span> | <span data-ttu-id="839bf-113">Cmdlet do PowerShell</span><span class="sxs-lookup"><span data-stu-id="839bf-113">PowerShell Cmdlet</span></span> |
| --- | ---:|
| <span data-ttu-id="839bf-114">[StartPartitionDataLossAsync][dl]</span><span class="sxs-lookup"><span data-stu-id="839bf-114">[StartPartitionDataLossAsync][dl]</span></span> |<span data-ttu-id="839bf-115">[Start-ServiceFabricPartitionDataLoss][psdl]</span><span class="sxs-lookup"><span data-stu-id="839bf-115">[Start-ServiceFabricPartitionDataLoss][psdl]</span></span> |
| <span data-ttu-id="839bf-116">[StartPartitionQuorumLossAsync][ql]</span><span class="sxs-lookup"><span data-stu-id="839bf-116">[StartPartitionQuorumLossAsync][ql]</span></span> |<span data-ttu-id="839bf-117">[Start-ServiceFabricPartitionQuorumLoss][psql]</span><span class="sxs-lookup"><span data-stu-id="839bf-117">[Start-ServiceFabricPartitionQuorumLoss][psql]</span></span> |
| <span data-ttu-id="839bf-118">[StartPartitionRestartAsync][rp]</span><span class="sxs-lookup"><span data-stu-id="839bf-118">[StartPartitionRestartAsync][rp]</span></span> |<span data-ttu-id="839bf-119">[Start-ServiceFabricPartitionRestart][psrp]</span><span class="sxs-lookup"><span data-stu-id="839bf-119">[Start-ServiceFabricPartitionRestart][psrp]</span></span> |

## <a name="conceptual-overview-of-running-a-command"></a><span data-ttu-id="839bf-120">Visão geral conceitual de execução de um comando</span><span class="sxs-lookup"><span data-stu-id="839bf-120">Conceptual Overview of Running a Command</span></span>
<span data-ttu-id="839bf-121">O Serviço Análise e Injeção de Falha usa um modelo assíncrono em que você inicia o comando com uma API, conhecida como a API "Start" neste documento, em seguida, verifica o progresso desse comando usando uma API "GetProgress" até que ela tenha atingido um estado terminal ou até que você a cancele.</span><span class="sxs-lookup"><span data-stu-id="839bf-121">The Fault Injection and Analysis Service uses an asynchronous model where you start the command with one API, referred to as the “Start” API in this document, then checks the progress of this command using a “GetProgress” API until it has reached a terminal state, or until you cancel it.</span></span>
<span data-ttu-id="839bf-122">Para iniciar um comando, chame a API "Start" da API correspondente.</span><span class="sxs-lookup"><span data-stu-id="839bf-122">To start a command, call the “Start” API for the corresponding API.</span></span>  <span data-ttu-id="839bf-123">Essa API retornará quando o Serviço de Análise e Injeção de Falha tiver aceitado a solicitação.</span><span class="sxs-lookup"><span data-stu-id="839bf-123">This API returns when the Fault Injection and Analysis Service has accepted the request.</span></span>  <span data-ttu-id="839bf-124">No entanto, ela não indica o quanto um comando foi executado, nem mesmo se ele já foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="839bf-124">However, it does not indicate how far a command has run, or even if it has started yet.</span></span>  <span data-ttu-id="839bf-125">Para verificar o andamento de um comando, chame a API "GetProgress" que corresponde à API "Start" chamada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="839bf-125">In order to check progress of a command, call the “GetProgress” API that corresponds to the “Start” API previously called.</span></span>  <span data-ttu-id="839bf-126">A API "GetProgress" retornará um objeto que indica o status atual do comando dentro de sua propriedade State.</span><span class="sxs-lookup"><span data-stu-id="839bf-126">The “GetProgress” API will return an object indicating the current status of the command inside its State property.</span></span>  <span data-ttu-id="839bf-127">Um comando é executado indefinidamente até:</span><span class="sxs-lookup"><span data-stu-id="839bf-127">A command runs indefinitely until:</span></span>

1. <span data-ttu-id="839bf-128">Que seja concluído com êxito.</span><span class="sxs-lookup"><span data-stu-id="839bf-128">It completes successfully.</span></span>  <span data-ttu-id="839bf-129">Se você chamar "GetProgress" dentro dele nesse caso, o estado do objeto de progresso será concluído.</span><span class="sxs-lookup"><span data-stu-id="839bf-129">If you call “GetProgress” on it in this case, the progress object’s State will be Completed.</span></span>
2. <span data-ttu-id="839bf-130">Que ele encontre um erro fatal.</span><span class="sxs-lookup"><span data-stu-id="839bf-130">It encounters a fatal error.</span></span>  <span data-ttu-id="839bf-131">Se você chamar "GetProgress" dentro dele nesse caso, a State do objeto de progresso será Faulted</span><span class="sxs-lookup"><span data-stu-id="839bf-131">If you call “GetProgress” on it in this case, the progress object’s State will be Faulted</span></span>
3. <span data-ttu-id="839bf-132">Você o cancela por meio da API [CancelTestCommandAsync][cancel] ou do cmdlet [Stop-ServiceFabricTestCommand][cancelps] do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="839bf-132">You cancel it through the [CancelTestCommandAsync][cancel] API, or [Stop-ServiceFabricTestCommand][cancelps] PowerShell cmdlet.</span></span>  <span data-ttu-id="839bf-133">Se você chamar "GetProgress" dentro dele nesse caso, a State do objeto de progresso será Cancelled ou ForceCancelled, dependendo de um argumento para essa API.</span><span class="sxs-lookup"><span data-stu-id="839bf-133">If you call “GetProgress” on it in this case, the progress object’s State will be either Cancelled or ForceCancelled, depending on an argument to that API.</span></span>  <span data-ttu-id="839bf-134">Confira a documentação de [CancelTestCommandAsync][cancel] para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="839bf-134">See the documentation for [CancelTestCommandAsync][cancel] for more details.</span></span>

## <a name="details-of-running-a-command"></a><span data-ttu-id="839bf-135">Detalhes da execução de um comando</span><span class="sxs-lookup"><span data-stu-id="839bf-135">Details of Running a Command</span></span>
<span data-ttu-id="839bf-136">Para iniciar um comando, chame a API Start com os argumentos esperados.</span><span class="sxs-lookup"><span data-stu-id="839bf-136">In order to start a command, call the Start API with the expected arguments.</span></span>  <span data-ttu-id="839bf-137">Todas as APIs Start têm um argumento GUID chamado operationId.</span><span class="sxs-lookup"><span data-stu-id="839bf-137">All Start APIs have a Guid argument named operationId.</span></span>  <span data-ttu-id="839bf-138">É preciso controlar o argumento operationId, uma vez que ele é usado para rastrear o progresso desse comando.</span><span class="sxs-lookup"><span data-stu-id="839bf-138">You should keep track of the operationId argument, since it is used to track progress of this command.</span></span>  <span data-ttu-id="839bf-139">Ele deve ser passado para a API "GetProgress" para rastrear o progresso do comando.</span><span class="sxs-lookup"><span data-stu-id="839bf-139">This must be passed into the “GetProgress” API in order to track progress of the command.</span></span>  <span data-ttu-id="839bf-140">A operationId deve ser exclusiva.</span><span class="sxs-lookup"><span data-stu-id="839bf-140">The operationId must be unique.</span></span>

<span data-ttu-id="839bf-141">Depois de chamar a API Start com êxito, a API GetProgress deverá ser chamada em um loop até que a propriedade State do objeto de progresso seja Completed.</span><span class="sxs-lookup"><span data-stu-id="839bf-141">After successfully calling the Start API, the GetProgress API should be called in a loop until the returned progress object’s State property is Completed.</span></span>  <span data-ttu-id="839bf-142">Todas as [FabricTransientException’s][fte] e OperationCanceledException’s devem ser recuperadas.</span><span class="sxs-lookup"><span data-stu-id="839bf-142">All [FabricTransientException’s][fte] and OperationCanceledException’s should be retried.</span></span>
<span data-ttu-id="839bf-143">Quando o comando tiver atingido um estado terminal (Completed, Faulted ou Cancelled), a propriedade Result do objeto de progresso retornado terá informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="839bf-143">When the command has reached a terminal state (Completed, Faulted, or Cancelled), the returned progress object’s Result property will have additional information.</span></span>  <span data-ttu-id="839bf-144">Se o estado for Completed, Result.SelectedPartition.PartitionId conterá a id da partição que foi selecionada.</span><span class="sxs-lookup"><span data-stu-id="839bf-144">If the state is Completed, Result.SelectedPartition.PartitionId will contain the partition id that was selected.</span></span>  <span data-ttu-id="839bf-145">Result.Exception será nulo.</span><span class="sxs-lookup"><span data-stu-id="839bf-145">Result.Exception will be null.</span></span>  <span data-ttu-id="839bf-146">Se o estado for Faulted, Result.Exception apresentará o motivo pelo qual o comando do Serviço de Análise e Injeção de Falha falhou.</span><span class="sxs-lookup"><span data-stu-id="839bf-146">If the state is Faulted, Result.Exception will have the reason the Fault Injection and Analysis Service faulted the command.</span></span>  <span data-ttu-id="839bf-147">Result.SelectedPartition.PartitionId terá a id da partição que foi selecionada.</span><span class="sxs-lookup"><span data-stu-id="839bf-147">Result.SelectedPartition.PartitionId will have the partition id that was selected.</span></span>  <span data-ttu-id="839bf-148">Em algumas situações, o comando pode não ser executado o suficiente para escolher uma partição.</span><span class="sxs-lookup"><span data-stu-id="839bf-148">In some situations, the command may not have proceeded far enough to choose a partition.</span></span>  <span data-ttu-id="839bf-149">Nesse caso, PartitionId será 0.</span><span class="sxs-lookup"><span data-stu-id="839bf-149">In that case, the PartitionId will be 0.</span></span>  <span data-ttu-id="839bf-150">Se o estado for Cancelled, Result.Exception será nulo.</span><span class="sxs-lookup"><span data-stu-id="839bf-150">If the state is Cancelled, Result.Exception will be null.</span></span>  <span data-ttu-id="839bf-151">Assim como no caso de Faulted, Result.SelectedPartition.PartitionId terá a id da partição que foi escolhida, mas se o comando não tiver prosseguido o suficiente para isso, será 0.</span><span class="sxs-lookup"><span data-stu-id="839bf-151">Like the Faulted case, Result.SelectedPartition.PartitionId will have the partition id that was chosen, but if the command has not proceeded far enough to do so, it will be 0.</span></span>  <span data-ttu-id="839bf-152">Veja também o exemplo abaixo.</span><span class="sxs-lookup"><span data-stu-id="839bf-152">Please also refer to the sample below.</span></span>

<span data-ttu-id="839bf-153">O código de exemplo abaixo mostra como iniciar e depois verificar o progresso em um comando para causar a perda de dados em uma partição específica.</span><span class="sxs-lookup"><span data-stu-id="839bf-153">The sample code below shows how to start then check progress on a command to cause data loss on a specific partition.</span></span>

```csharp
    static async Task PerformDataLossSample()
    {
        // Create a unique operation id for the command below
        Guid operationId = Guid.NewGuid();

        // Note: Use the appropriate overload for your configuration
        FabricClient fabricClient = new FabricClient();

        // The name of the target service
        Uri targetServiceName = new Uri("fabric:/MyService");

        // The id of the target partition inside the target service
        Guid targetPartitionId = new Guid("00000000-0000-0000-0000-000002233445");

        PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(targetServiceName, targetPartitionId);

        // Start the command.  Retry OperationCanceledException and all FabricTransientException's.  Note when StartPartitionDataLossAsync completes
        // successfully it only means the Fault Injection and Analysis Service has saved the intent to perform this work.  It does not say anything about the progress
        // of the command.
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

        // Poll the progress using GetPartitionDataLossProgressAsync until it is either Completed or Faulted.  In this example, we're assuming
        // the command won't be cancelled.        

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

                // In a terminal state .Result.SelectedPartition.PartitionId will have the chosen partition
                Console.WriteLine("  Printing selected partition='{0}'", progress.Result.SelectedPartition.PartitionId);
                break;
            }
            else if (progress.State == TestCommandProgressState.Faulted)
            {
                // If State is Faulted, the progress object's Result property's Exception property will have the reason why.
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

<span data-ttu-id="839bf-154">O exemplo abaixo mostra como usar PartitionSelector para escolher uma partição aleatória de um serviço especificado:</span><span class="sxs-lookup"><span data-stu-id="839bf-154">The sample below shows how to use the PartitionSelector to choose a random partition of a specified service:</span></span>

```csharp
    static async Task PerformDataLossUseSelectorSample()
    {
        // Create a unique operation id for the command below
        Guid operationId = Guid.NewGuid();

        // Note: Use the appropriate overload for your configuration
        FabricClient fabricClient = new FabricClient();

        // The name of the target service
        Uri targetServiceName = new Uri("fabric:/SampleService ");

        // Use a PartitionSelector that will have the Fault Injection and Analysis Service choose a random partition of “targetServiceName”
        PartitionSelector partitionSelector = PartitionSelector.RandomOf(targetServiceName);

        // Start the command.  Retry OperationCanceledException and all FabricTransientException's.  Note when StartPartitionDataLossAsync completes
        // successfully it only means the Fault Injection and Analysis Service has saved the intent to perform this work.  It does not say anything about the progress
        // of the command.
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

        // Poll the progress using GetPartitionDataLossProgressAsync until it is either Completed or Faulted.  In this example, we're assuming
        // the command won't be cancelled.

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
                // If State is Faulted, the progress object's Result property's Exception property will have the reason why.
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

## <a name="history-and-truncation"></a><span data-ttu-id="839bf-155">Histórico e truncamento</span><span class="sxs-lookup"><span data-stu-id="839bf-155">History and Truncation</span></span>
<span data-ttu-id="839bf-156">Depois que um comando tiver atingido um estado terminal, seus metadados permanecerão no Serviço de Análise e Injeção de Falha por um tempo determinado, antes de ser removido para economia de espaço.</span><span class="sxs-lookup"><span data-stu-id="839bf-156">After a command has reached a terminal state, its metadata will remain in the Fault Injection and Analysis Service for a certain time, before it will be removed to save space.</span></span>  <span data-ttu-id="839bf-157">Se "GetProgress" for chamado usando operationId de um comando depois que ele tiver sido removido, ele retornará uma FabricException com um ErrorCode de KeyNotFound.</span><span class="sxs-lookup"><span data-stu-id="839bf-157">If “GetProgress” is called using the operationId of a command after it has been removed, it will return a FabricException with an ErrorCode of KeyNotFound.</span></span>

[dl]: https://msdn.microsoft.com/library/azure/mt693569.aspx
[ql]: https://msdn.microsoft.com/library/azure/mt693558.aspx
[rp]: https://msdn.microsoft.com/library/azure/mt645056.aspx
[psdl]: https://msdn.microsoft.com/library/mt697573.aspx
[psql]: https://msdn.microsoft.com/library/mt697557.aspx
[psrp]: https://msdn.microsoft.com/library/mt697560.aspx
[cancel]: https://msdn.microsoft.com/library/azure/mt668910.aspx
[cancelps]: https://msdn.microsoft.com/library/mt697566.aspx
[fte]: https://msdn.microsoft.com/library/azure/system.fabric.fabrictransientexception.aspx
