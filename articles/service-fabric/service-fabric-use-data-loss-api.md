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
# <a name="how-tooinvoke-data-loss-on-services"></a><span data-ttu-id="83df9-103">Como tooInvoke perda de dados nos serviços</span><span class="sxs-lookup"><span data-stu-id="83df9-103">How tooInvoke Data Loss on Services</span></span>
> [!WARNING]
> <span data-ttu-id="83df9-104">Este documento descreve como toocause perda de dados em seus serviços e deve ser usada com cuidado.</span><span class="sxs-lookup"><span data-stu-id="83df9-104">This document describe how toocause data loss in your services, and should be used with care.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="83df9-105">Introdução</span><span class="sxs-lookup"><span data-stu-id="83df9-105">Introduction</span></span>
<span data-ttu-id="83df9-106">Você pode invocar a perda de dados em uma partição do serviço do Service Fabric chamando StartPartitionDataLossAsync().</span><span class="sxs-lookup"><span data-stu-id="83df9-106">You can invoke data loss on a partition of your Service Fabric Service by calling StartPartitionDataLossAsync().</span></span>  <span data-ttu-id="83df9-107">Essa api usa Olá injeção de falha e o serviço de análise tooperform Olá trabalho toocause dados perda condições.</span><span class="sxs-lookup"><span data-stu-id="83df9-107">This api uses hello Fault Injection and Analysis Service tooperform hello work toocause data loss conditions.</span></span>

## <a name="using-hello-fault-injection-and-analysis-service"></a><span data-ttu-id="83df9-108">Usando o serviço de análise e Olá injeção de falha</span><span class="sxs-lookup"><span data-stu-id="83df9-108">Using hello Fault Injection and Analysis Service</span></span>
<span data-ttu-id="83df9-109">Olá injeção de falha e o serviço de análise atualmente suporta Olá APIs no gráfico de saudação abaixo a seguir.</span><span class="sxs-lookup"><span data-stu-id="83df9-109">hello Fault Injection and Analysis Service currently supports hello following APIs in hello chart below.</span></span>  <span data-ttu-id="83df9-110">Olá direita do gráfico de saudação mostra Olá cmdlet do PowerShell correspondente.</span><span class="sxs-lookup"><span data-stu-id="83df9-110">hello right side of hello chart shows hello corresponding PowerShell cmdlet.</span></span>  <span data-ttu-id="83df9-111">Consulte toohello documentação do msdn sobre cada API para obter mais informações sobre cada um deles.</span><span class="sxs-lookup"><span data-stu-id="83df9-111">Please refer toohello msdn documentation on each API for more information on each one.</span></span>

| <span data-ttu-id="83df9-112">API do C#</span><span class="sxs-lookup"><span data-stu-id="83df9-112">C# API</span></span> | <span data-ttu-id="83df9-113">Cmdlet do PowerShell</span><span class="sxs-lookup"><span data-stu-id="83df9-113">PowerShell Cmdlet</span></span> |
| --- | ---:|
| <span data-ttu-id="83df9-114">[StartPartitionDataLossAsync][dl]</span><span class="sxs-lookup"><span data-stu-id="83df9-114">[StartPartitionDataLossAsync][dl]</span></span> |<span data-ttu-id="83df9-115">[Start-ServiceFabricPartitionDataLoss][psdl]</span><span class="sxs-lookup"><span data-stu-id="83df9-115">[Start-ServiceFabricPartitionDataLoss][psdl]</span></span> |
| <span data-ttu-id="83df9-116">[StartPartitionQuorumLossAsync][ql]</span><span class="sxs-lookup"><span data-stu-id="83df9-116">[StartPartitionQuorumLossAsync][ql]</span></span> |<span data-ttu-id="83df9-117">[Start-ServiceFabricPartitionQuorumLoss][psql]</span><span class="sxs-lookup"><span data-stu-id="83df9-117">[Start-ServiceFabricPartitionQuorumLoss][psql]</span></span> |
| <span data-ttu-id="83df9-118">[StartPartitionRestartAsync][rp]</span><span class="sxs-lookup"><span data-stu-id="83df9-118">[StartPartitionRestartAsync][rp]</span></span> |<span data-ttu-id="83df9-119">[Start-ServiceFabricPartitionRestart][psrp]</span><span class="sxs-lookup"><span data-stu-id="83df9-119">[Start-ServiceFabricPartitionRestart][psrp]</span></span> |

## <a name="conceptual-overview-of-running-a-command"></a><span data-ttu-id="83df9-120">Visão geral conceitual de execução de um comando</span><span class="sxs-lookup"><span data-stu-id="83df9-120">Conceptual Overview of Running a Command</span></span>
<span data-ttu-id="83df9-121">Olá injeção de falha e o Analysis Services usa um modelo assíncrono onde iniciar Olá comando com uma API, chamado tooas hello "Start" API neste documento, e, em seguida, verificações de progresso Olá desse comando usando uma API de "GetProgress" até que ele atingiu um terminal estado, ou até que você cancele-o.</span><span class="sxs-lookup"><span data-stu-id="83df9-121">hello Fault Injection and Analysis Service uses an asynchronous model where you start hello command with one API, referred tooas hello “Start” API in this document, then checks hello progress of this command using a “GetProgress” API until it has reached a terminal state, or until you cancel it.</span></span>
<span data-ttu-id="83df9-122">toostart um comando, chamada hello "Iniciar" API para API correspondente hello.</span><span class="sxs-lookup"><span data-stu-id="83df9-122">toostart a command, call hello “Start” API for hello corresponding API.</span></span>  <span data-ttu-id="83df9-123">Essa API retorna quando hello injeção de falha e o serviço de análise aceitou a solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="83df9-123">This API returns when hello Fault Injection and Analysis Service has accepted hello request.</span></span>  <span data-ttu-id="83df9-124">No entanto, ela não indica o quanto um comando foi executado, nem mesmo se ele já foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="83df9-124">However, it does not indicate how far a command has run, or even if it has started yet.</span></span>  <span data-ttu-id="83df9-125">Em andamento toocheck da ordem de um comando, chame hello "GetProgress" que corresponde a API de "Início" toohello anteriormente chamada de API.</span><span class="sxs-lookup"><span data-stu-id="83df9-125">In order toocheck progress of a command, call hello “GetProgress” API that corresponds toohello “Start” API previously called.</span></span>  <span data-ttu-id="83df9-126">Olá "GetProgress" API retorna um objeto que indica o status atual de saudação do comando hello dentro de sua propriedade de estado.</span><span class="sxs-lookup"><span data-stu-id="83df9-126">hello “GetProgress” API will return an object indicating hello current status of hello command inside its State property.</span></span>  <span data-ttu-id="83df9-127">Um comando é executado indefinidamente até:</span><span class="sxs-lookup"><span data-stu-id="83df9-127">A command runs indefinitely until:</span></span>

1. <span data-ttu-id="83df9-128">Que seja concluído com êxito.</span><span class="sxs-lookup"><span data-stu-id="83df9-128">It completes successfully.</span></span>  <span data-ttu-id="83df9-129">Se você chamar "GetProgress" nesse caso, estado do objeto de andamento Olá será concluído.</span><span class="sxs-lookup"><span data-stu-id="83df9-129">If you call “GetProgress” on it in this case, hello progress object’s State will be Completed.</span></span>
2. <span data-ttu-id="83df9-130">Que ele encontre um erro fatal.</span><span class="sxs-lookup"><span data-stu-id="83df9-130">It encounters a fatal error.</span></span>  <span data-ttu-id="83df9-131">Se você chamar "GetProgress" nesse caso, estado do objeto do hello andamento será interrompido.</span><span class="sxs-lookup"><span data-stu-id="83df9-131">If you call “GetProgress” on it in this case, hello progress object’s State will be Faulted</span></span>
3. <span data-ttu-id="83df9-132">Cancelá-lo por meio de saudação [CancelTestCommandAsync] [ cancel] API, ou [Stop ServiceFabricTestCommand] [ cancelps] cmdlet do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="83df9-132">You cancel it through hello [CancelTestCommandAsync][cancel] API, or [Stop-ServiceFabricTestCommand][cancelps] PowerShell cmdlet.</span></span>  <span data-ttu-id="83df9-133">Se você chamar "GetProgress" nesse caso, hello estado do objeto de progresso será cancelado ou ForceCancelled, dependendo de uma API de toothat do argumento.</span><span class="sxs-lookup"><span data-stu-id="83df9-133">If you call “GetProgress” on it in this case, hello progress object’s State will be either Cancelled or ForceCancelled, depending on an argument toothat API.</span></span>  <span data-ttu-id="83df9-134">Consulte a documentação de saudação para [CancelTestCommandAsync] [ cancel] para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="83df9-134">See hello documentation for [CancelTestCommandAsync][cancel] for more details.</span></span>

## <a name="details-of-running-a-command"></a><span data-ttu-id="83df9-135">Detalhes da execução de um comando</span><span class="sxs-lookup"><span data-stu-id="83df9-135">Details of Running a Command</span></span>
<span data-ttu-id="83df9-136">Em ordem toostart um comando, chame hello API iniciar com argumentos Olá esperado.</span><span class="sxs-lookup"><span data-stu-id="83df9-136">In order toostart a command, call hello Start API with hello expected arguments.</span></span>  <span data-ttu-id="83df9-137">Todas as APIs Start têm um argumento GUID chamado operationId.</span><span class="sxs-lookup"><span data-stu-id="83df9-137">All Start APIs have a Guid argument named operationId.</span></span>  <span data-ttu-id="83df9-138">Você deve manter o controle de argumento de operationId hello, pois ele é usado tootrack andamento desse comando.</span><span class="sxs-lookup"><span data-stu-id="83df9-138">You should keep track of hello operationId argument, since it is used tootrack progress of this command.</span></span>  <span data-ttu-id="83df9-139">Isso deve ser passado para hello "GetProgress" API em andamento de tootrack de ordem do comando hello.</span><span class="sxs-lookup"><span data-stu-id="83df9-139">This must be passed into hello “GetProgress” API in order tootrack progress of hello command.</span></span>  <span data-ttu-id="83df9-140">ID da operação Olá deve ser exclusivo.</span><span class="sxs-lookup"><span data-stu-id="83df9-140">hello operationId must be unique.</span></span>

<span data-ttu-id="83df9-141">Depois de chamar com êxito Olá API Iniciar, Olá GetProgress API deve ser chamado em um loop até que hello retornadas andamento propriedade de estado do objeto é concluída.</span><span class="sxs-lookup"><span data-stu-id="83df9-141">After successfully calling hello Start API, hello GetProgress API should be called in a loop until hello returned progress object’s State property is Completed.</span></span>  <span data-ttu-id="83df9-142">Todas as [FabricTransientException’s][fte] e OperationCanceledException’s devem ser recuperadas.</span><span class="sxs-lookup"><span data-stu-id="83df9-142">All [FabricTransientException’s][fte] and OperationCanceledException’s should be retried.</span></span>
<span data-ttu-id="83df9-143">Quando o comando Olá atingiu um estado terminal (concluído, com falha ou cancelamento), Olá retornado de propriedade do resultado do objeto de andamento terá informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="83df9-143">When hello command has reached a terminal state (Completed, Faulted, or Cancelled), hello returned progress object’s Result property will have additional information.</span></span>  <span data-ttu-id="83df9-144">Se o estado de saudação for concluído, Result.SelectedPartition.PartitionId contém id de partição Olá que foi selecionado.</span><span class="sxs-lookup"><span data-stu-id="83df9-144">If hello state is Completed, Result.SelectedPartition.PartitionId will contain hello partition id that was selected.</span></span>  <span data-ttu-id="83df9-145">Result.Exception será nulo.</span><span class="sxs-lookup"><span data-stu-id="83df9-145">Result.Exception will be null.</span></span>  <span data-ttu-id="83df9-146">Se o estado de saudação está com defeito, Result.Exception terá Olá Olá do motivo injeção de falha e Analysis Services com defeito Olá comando.</span><span class="sxs-lookup"><span data-stu-id="83df9-146">If hello state is Faulted, Result.Exception will have hello reason hello Fault Injection and Analysis Service faulted hello command.</span></span>  <span data-ttu-id="83df9-147">Result.SelectedPartition.PartitionId tem uma id de partição Olá que foi selecionado.</span><span class="sxs-lookup"><span data-stu-id="83df9-147">Result.SelectedPartition.PartitionId will have hello partition id that was selected.</span></span>  <span data-ttu-id="83df9-148">Em algumas situações, comando Olá pode não ter continuavam suficiente toochoose uma partição.</span><span class="sxs-lookup"><span data-stu-id="83df9-148">In some situations, hello command may not have proceeded far enough toochoose a partition.</span></span>  <span data-ttu-id="83df9-149">Nesse caso, a saudação PartitionId será 0.</span><span class="sxs-lookup"><span data-stu-id="83df9-149">In that case, hello PartitionId will be 0.</span></span>  <span data-ttu-id="83df9-150">Se o estado de saudação é cancelado, Result.Exception será nulo.</span><span class="sxs-lookup"><span data-stu-id="83df9-150">If hello state is Cancelled, Result.Exception will be null.</span></span>  <span data-ttu-id="83df9-151">Como Olá caso com falha, Result.SelectedPartition.PartitionId tem uma id de partição de saudação foi escolhido, mas se o comando Olá não tenha transcorrido suficiente toodo assim, ela será 0.</span><span class="sxs-lookup"><span data-stu-id="83df9-151">Like hello Faulted case, Result.SelectedPartition.PartitionId will have hello partition id that was chosen, but if hello command has not proceeded far enough toodo so, it will be 0.</span></span>  <span data-ttu-id="83df9-152">Consulte também toohello exemplo abaixo.</span><span class="sxs-lookup"><span data-stu-id="83df9-152">Please also refer toohello sample below.</span></span>

<span data-ttu-id="83df9-153">código de exemplo Hello abaixo mostra como toostart, em seguida, verificar o andamento em caso de perda de dados de toocause um comando em uma partição específica.</span><span class="sxs-lookup"><span data-stu-id="83df9-153">hello sample code below shows how toostart then check progress on a command toocause data loss on a specific partition.</span></span>

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

<span data-ttu-id="83df9-154">exemplo Hello abaixo mostra como toouse Olá PartitionSelector toochoose uma partição aleatória de um serviço especificado:</span><span class="sxs-lookup"><span data-stu-id="83df9-154">hello sample below shows how toouse hello PartitionSelector toochoose a random partition of a specified service:</span></span>

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

## <a name="history-and-truncation"></a><span data-ttu-id="83df9-155">Histórico e truncamento</span><span class="sxs-lookup"><span data-stu-id="83df9-155">History and Truncation</span></span>
<span data-ttu-id="83df9-156">Depois que um comando atingir um estado terminal, seus metadados permanecem no hello injeção de falha e serviço de análise para uma determinada hora, antes de ser removido toosave espaço.</span><span class="sxs-lookup"><span data-stu-id="83df9-156">After a command has reached a terminal state, its metadata will remain in hello Fault Injection and Analysis Service for a certain time, before it will be removed toosave space.</span></span>  <span data-ttu-id="83df9-157">Se "GetProgress" for chamado usando Olá ID da operação de um comando após ele ter sido removido, ele retornará um FabricException com um código de erro de KeyNotFound.</span><span class="sxs-lookup"><span data-stu-id="83df9-157">If “GetProgress” is called using hello operationId of a command after it has been removed, it will return a FabricException with an ErrorCode of KeyNotFound.</span></span>

[dl]: https://msdn.microsoft.com/library/azure/mt693569.aspx
[ql]: https://msdn.microsoft.com/library/azure/mt693558.aspx
[rp]: https://msdn.microsoft.com/library/azure/mt645056.aspx
[psdl]: https://msdn.microsoft.com/library/mt697573.aspx
[psql]: https://msdn.microsoft.com/library/mt697557.aspx
[psrp]: https://msdn.microsoft.com/library/mt697560.aspx
[cancel]: https://msdn.microsoft.com/library/azure/mt668910.aspx
[cancelps]: https://msdn.microsoft.com/library/mt697566.aspx
[fte]: https://msdn.microsoft.com/library/azure/system.fabric.fabrictransientexception.aspx
