---
title: "Iniciar e interromper nós de cluster para testar os microsserviços do Azure |Microsoft Docs"
description: "Saiba como usar a injeção de falha para testar um aplicativo do Service Fabric iniciando e interrompendo nós de cluster."
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
ms.date: 6/12/2017
ms.author: lemai
ms.openlocfilehash: 850fbc0c74811ec942292da64064dec867cd1b9e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="replacing-the-start-node-and-stop-node-apis-with-the-node-transition-api"></a><span data-ttu-id="ee497-103">Substituir as APIs de Nó de Início e Nó de Parada pela API de Nó de Transição</span><span class="sxs-lookup"><span data-stu-id="ee497-103">Replacing the Start Node and Stop node APIs with the Node Transition API</span></span>

## <a name="what-do-the-stop-node-and-start-node-apis-do"></a><span data-ttu-id="ee497-104">O que as APIs de Nó de Parada e de Início fazem?</span><span class="sxs-lookup"><span data-stu-id="ee497-104">What do the Stop Node and Start Node APIs do?</span></span>

<span data-ttu-id="ee497-105">A API de Nó de Parada (gerenciada: [StopNodeAsync()][stopnode], PowerShell: [Stop-ServiceFabricNode][stopnodeps]) interrompe um nó do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ee497-105">The Stop Node API (managed: [StopNodeAsync()][stopnode], PowerShell: [Stop-ServiceFabricNode][stopnodeps]) stops a Service Fabric node.</span></span>  <span data-ttu-id="ee497-106">Um nó de Service Fabric é o processo e não uma VM ou máquina: a VM ou a máquina ainda estará em execução.</span><span class="sxs-lookup"><span data-stu-id="ee497-106">A Service Fabric node is process, not a VM or machine – the VM or machine will still be running.</span></span>  <span data-ttu-id="ee497-107">No restante do documento, "nó" significa um nó do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ee497-107">For the rest of the document "node" will mean Service Fabric node.</span></span>  <span data-ttu-id="ee497-108">Parar um nó coloca-o em um estado *parado* em que ele não é membro do cluster e não pode hospedar serviços, simulando assim um nó *inoperante*.</span><span class="sxs-lookup"><span data-stu-id="ee497-108">Stopping a node puts it into a *stopped* state where it is not a member of the cluster and cannot host services, thus simulating a *down* node.</span></span>  <span data-ttu-id="ee497-109">Isso é útil para injetar falhas no sistema para testar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ee497-109">This is useful for injecting faults into the system to test your application.</span></span>  <span data-ttu-id="ee497-110">A API de Nó de Início (gerenciada: [StartNodeAsync()][startnode], PowerShell: [Start-ServiceFabricNode][startnodeps]]) inverte a API de Nó de Parada, o que coloca o nó de volta em um estado normal.</span><span class="sxs-lookup"><span data-stu-id="ee497-110">The Start Node API (managed: [StartNodeAsync()][startnode], PowerShell: [Start-ServiceFabricNode][startnodeps]]) reverses the Stop Node API,  which brings the node back to a normal state.</span></span>

## <a name="why-are-we-replacing-these"></a><span data-ttu-id="ee497-111">Por que os estamos substituindo?</span><span class="sxs-lookup"><span data-stu-id="ee497-111">Why are we replacing these?</span></span>

<span data-ttu-id="ee497-112">Conforme descrito anteriormente, um nó *parado* do Service Fabric é um nó direcionado intencionalmente usando a API de Nó de Parada.</span><span class="sxs-lookup"><span data-stu-id="ee497-112">As described earlier, a *stopped* Service Fabric node is a node intentionally targeted using the Stop Node API.</span></span>  <span data-ttu-id="ee497-113">Um nó *inoperante* é um nó que está inativo por qualquer motivo (por exemplo, a VM ou a máquina está desativada).</span><span class="sxs-lookup"><span data-stu-id="ee497-113">A *down* node is a node that is down for any other reason (e.g. the VM or machine is off).</span></span>  <span data-ttu-id="ee497-114">Com a API de Nó de Parada, o sistema não expõe informações para diferenciar entre nós *parados* e nós *inoperantes*.</span><span class="sxs-lookup"><span data-stu-id="ee497-114">With the Stop Node API, the system does not expose information to differentiate between *stopped* nodes and *down* nodes.</span></span>

<span data-ttu-id="ee497-115">Além disso, alguns erros retornados por essas APIs não são mais tão descritivos quanto poderiam ser.</span><span class="sxs-lookup"><span data-stu-id="ee497-115">In addition, some errors returned by these APIs are not as descriptive as they could be.</span></span>  <span data-ttu-id="ee497-116">Por exemplo, se for invocada a API de Nó de Parada em um nó já *parado*, isso retornará o erro *InvalidAddress*.</span><span class="sxs-lookup"><span data-stu-id="ee497-116">For example, invoking the Stop Node API on an already *stopped* node will return the error *InvalidAddress*.</span></span>  <span data-ttu-id="ee497-117">Essa experiência poderia ser melhorada.</span><span class="sxs-lookup"><span data-stu-id="ee497-117">This experience could be improved.</span></span>

<span data-ttu-id="ee497-118">Além disso, a duração pela qual um nó é interrompido é "infinita" até que a API de Nó de Início seja invocada.</span><span class="sxs-lookup"><span data-stu-id="ee497-118">Also, the duration a node is stopped for is “infinite” until the Start Node API is invoked.</span></span>  <span data-ttu-id="ee497-119">Descobrimos que isso pode causar problemas e pode ser propenso a erros.</span><span class="sxs-lookup"><span data-stu-id="ee497-119">We’ve found this can cause problems and may be error-prone.</span></span>  <span data-ttu-id="ee497-120">Por exemplo, houve problemas em que um usuário invocou a API de Nó de Parada em um nó e depois se esqueceu.</span><span class="sxs-lookup"><span data-stu-id="ee497-120">For example, we’ve seen problems where a user invoked the Stop Node API on a node and then forgot about it.</span></span>  <span data-ttu-id="ee497-121">Posteriormente, não estava claro se o nó estava *inoperante* ou *parado*.</span><span class="sxs-lookup"><span data-stu-id="ee497-121">Later, it was unclear if the node was *down* or *stopped*.</span></span>


## <a name="introducing-the-node-transition-apis"></a><span data-ttu-id="ee497-122">Introdução às APIs de Transição de Nó</span><span class="sxs-lookup"><span data-stu-id="ee497-122">Introducing the Node Transition APIs</span></span>

<span data-ttu-id="ee497-123">Abordamos esses problemas acima em um novo conjunto de APIs.</span><span class="sxs-lookup"><span data-stu-id="ee497-123">We’ve addressed these issues above in a new set of APIs.</span></span>  <span data-ttu-id="ee497-124">A nova API de Transição de Nó (gerenciada: [StartNodeTransitionAsync()][snt]) pode ser usada para fazer a transição de um nó do Service Fabric para um estado *parado* ou para fazer a transição de um estado *parado* para um estado ativo normal.</span><span class="sxs-lookup"><span data-stu-id="ee497-124">The new Node Transition API (managed: [StartNodeTransitionAsync()][snt]) may be used to transition a Service Fabric node to a *stopped* state, or to transition it from a *stopped* state to a normal up state.</span></span>  <span data-ttu-id="ee497-125">Observe que "Start" no nome da API não se refere a iniciar um nó.</span><span class="sxs-lookup"><span data-stu-id="ee497-125">Please note that the “Start” in the name of the API does not refer to starting a node.</span></span>  <span data-ttu-id="ee497-126">Isso se refere a iniciar uma operação assíncrona que o sistema executará para fazer a transição do nó como estado *parado* ou iniciado.</span><span class="sxs-lookup"><span data-stu-id="ee497-126">It refers to beginning an asynchronous operation that the system will execute to transition the node to either *stopped* or started state.</span></span>

<span data-ttu-id="ee497-127">**Uso**</span><span class="sxs-lookup"><span data-stu-id="ee497-127">**Usage**</span></span>

<span data-ttu-id="ee497-128">Se a API de Transição de Nó não lançar uma exceção quando invocada, o sistema aceitou a operação assíncrona e a executará.</span><span class="sxs-lookup"><span data-stu-id="ee497-128">If the Node Transition API does not throw an exception when invoked, then the system has accepted the asynchronous operation, and will execute it.</span></span>  <span data-ttu-id="ee497-129">Uma chamada bem-sucedida não implica que a operação já foi concluída.</span><span class="sxs-lookup"><span data-stu-id="ee497-129">A successful call does not imply the operation is finished yet.</span></span>  <span data-ttu-id="ee497-130">Para obter informações sobre o estado atual da operação, chame a API de Progresso de Transição de Nó (gerenciada: [GetNodeTransitionProgressAsync()][gntp]) com o guid usado ao invocar a API de Transição de Nó para essa operação.</span><span class="sxs-lookup"><span data-stu-id="ee497-130">To get information about the current state of the operation, call the Node Transition Progress API (managed: [GetNodeTransitionProgressAsync()][gntp]) with the guid used when invoking Node Transition API for this operation.</span></span>  <span data-ttu-id="ee497-131">A API de Progresso de Transição de Nó retorna um objeto NodeTransitionProgress.</span><span class="sxs-lookup"><span data-stu-id="ee497-131">The Node Transition Progress API returns an NodeTransitionProgress object.</span></span>  <span data-ttu-id="ee497-132">A propriedade do objeto State especifica o estado atual da operação.</span><span class="sxs-lookup"><span data-stu-id="ee497-132">This object’s State property specifies the current state of the operation.</span></span>  <span data-ttu-id="ee497-133">Se o estado for "Em Execução", a operação está em execução.</span><span class="sxs-lookup"><span data-stu-id="ee497-133">If the state is “Running” then the operation is executing.</span></span>  <span data-ttu-id="ee497-134">Se for Concluído, a operação foi concluída sem erros.</span><span class="sxs-lookup"><span data-stu-id="ee497-134">If it is Completed, the operation finished without error.</span></span>  <span data-ttu-id="ee497-135">Se for Falha, houve um problema ao executar a operação.</span><span class="sxs-lookup"><span data-stu-id="ee497-135">If it is Faulted, there was a problem executing the operation.</span></span>  <span data-ttu-id="ee497-136">A propriedade Exception da propriedade Result indicará qual foi o problema.</span><span class="sxs-lookup"><span data-stu-id="ee497-136">The Result property’s Exception property will indicate what the issue was.</span></span>  <span data-ttu-id="ee497-137">Confira https://docs.microsoft.com/dotnet/api/system.fabric.testcommandprogressstate para obter mais informações sobre a propriedade State e a seção "Exemplo de uso" abaixo para obter exemplos de código.</span><span class="sxs-lookup"><span data-stu-id="ee497-137">See https://docs.microsoft.com/dotnet/api/system.fabric.testcommandprogressstate for more information about the State property, and the “Sample Usage” section below for code examples.</span></span>


<span data-ttu-id="ee497-138">**Diferenciar entre um nó parado e um nó inoperante** Se um nó for *parado* usando a API de Transição de Nó, a saída de uma consulta de nó (gerenciada: [GetNodeListAsync()][nodequery], PowerShell: [Get-ServiceFabricNode][nodequeryps]) mostrará que este nó tem um valor de propriedade *IsStopped* de true.</span><span class="sxs-lookup"><span data-stu-id="ee497-138">**Differentiating between a stopped node and a down node** If a node is *stopped* using the Node Transition API, the output of a node query (managed: [GetNodeListAsync()][nodequery], PowerShell: [Get-ServiceFabricNode][nodequeryps]) will show that this node has an *IsStopped* property value of true.</span></span>  <span data-ttu-id="ee497-139">Observe que isso é diferente do valor da propriedade *NodeStatus*, que indicará *Down*.</span><span class="sxs-lookup"><span data-stu-id="ee497-139">Note this is different from the value of the *NodeStatus* property, which will say *Down*.</span></span>  <span data-ttu-id="ee497-140">Se a propriedade *NodeStatus* tiver o valor *Down*, mas *IsStopped* for false, o nó não foi interrompido usando a API de Transição de Nó e está *Down* devido a algum outro motivo.</span><span class="sxs-lookup"><span data-stu-id="ee497-140">If the *NodeStatus* property has a value of *Down*, but *IsStopped* is false, then the node was not stopped using the Node Transition API, and is *Down* due some other reason.</span></span>  <span data-ttu-id="ee497-141">Se a propriedade *IsStopped* for true e a propriedade *NodeStatus* for *Down*, ele foi interrompido usando a API de Transição de Nó.</span><span class="sxs-lookup"><span data-stu-id="ee497-141">If the *IsStopped* property is true, and the *NodeStatus* property is *Down*, then it was stopped using the Node Transition API.</span></span>

<span data-ttu-id="ee497-142">Iniciar um nó *parado* usando a API de Transição de Nó o retornará para o funcionamento como um membro normal do cluster novamente.</span><span class="sxs-lookup"><span data-stu-id="ee497-142">Starting a *stopped* node using the Node Transition API will return it to function as a normal member of the cluster again.</span></span>  <span data-ttu-id="ee497-143">A saída da API de consulta de nó mostrará *IsStopped* como false e *NodeStatus* como algo diferente de Down (por exemplo, Up).</span><span class="sxs-lookup"><span data-stu-id="ee497-143">The output of the node query API will show *IsStopped* as false, and *NodeStatus* as something that is not Down (e.g. Up).</span></span>


<span data-ttu-id="ee497-144">**Duração limitada** Ao usar a API de Transição de Nó para um nó, um dos parâmetros necessários, *stopNodeDurationInSeconds*, representa a quantidade de tempo em segundos para manter o nó *parado*.</span><span class="sxs-lookup"><span data-stu-id="ee497-144">**Limited Duration** When using the Node Transition API to stop a node, one of the required parameters, *stopNodeDurationInSeconds*, represents the amount of time in seconds to keep the node *stopped*.</span></span>  <span data-ttu-id="ee497-145">Esse valor deve estar no intervalo permitido, que tem um mínimo de 600 e um máximo de 14400.</span><span class="sxs-lookup"><span data-stu-id="ee497-145">This value must be in the allowed range, which has a minimum of 600, and a maximum of 14400.</span></span>  <span data-ttu-id="ee497-146">Depois que esse tempo expirar, o nó será reiniciado com estado Operante automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ee497-146">After this time expires, the node will restart itself into Up state automatically.</span></span>  <span data-ttu-id="ee497-147">Confira o exemplo 1 abaixo para obter um exemplo de uso.</span><span class="sxs-lookup"><span data-stu-id="ee497-147">Refer to Sample 1 below for an example of usage.</span></span>

> [!WARNING]
> <span data-ttu-id="ee497-148">Evite misturar APIs de Transição de Nó e APIs de Nó de Parada e Nó de Início.</span><span class="sxs-lookup"><span data-stu-id="ee497-148">Avoid mixing Node Transition APIs and the Stop Node and Start Node APIs.</span></span>  <span data-ttu-id="ee497-149">A recomendação é usar somente a API de Transição de Nó.</span><span class="sxs-lookup"><span data-stu-id="ee497-149">The recommendation is to  use the Node Transition API only.</span></span>  <span data-ttu-id="ee497-150">> Se um nó já foi interrompido usando a API de Nó de Parada, ele deve ser iniciado usando a API de Nó de Início antes de usar as > APIs de Transição de Nó.</span><span class="sxs-lookup"><span data-stu-id="ee497-150">> If a node has been already been stopped using the Stop Node API, it should be started using the Start Node API first before using the > Node Transition APIs.</span></span>

> [!WARNING]
> <span data-ttu-id="ee497-151">Não é possível fazer várias chamadas de APIs de Transição de Nó no mesmo nó em paralelo.</span><span class="sxs-lookup"><span data-stu-id="ee497-151">Multiple Node Transition APIs calls cannot be made on the same node in parallel.</span></span>  <span data-ttu-id="ee497-152">Nessa situação, a API de Transição de Nó > lançará um FabricException com um valor de propriedade ErrorCode de NodeTransitionInProgress.</span><span class="sxs-lookup"><span data-stu-id="ee497-152">In such a situation, the Node Transition API will    > throw a FabricException with an ErrorCode property value of NodeTransitionInProgress.</span></span>  <span data-ttu-id="ee497-153">Depois que uma transição de nó em um nó específico > tiver sido iniciada, você deverá aguardar até que a operação atinja um estado terminal (Concluído, Falha ou ForceCancelled) antes de iniciar uma > nova transição no mesmo nó.</span><span class="sxs-lookup"><span data-stu-id="ee497-153">Once a node transition on a specific node has  > been started, you should wait until the operation reaches a terminal state (Completed, Faulted, or ForceCancelled) before starting a  > new transition on the same node.</span></span>  <span data-ttu-id="ee497-154">São permitidas chamadas de transição de nó paralelas em nós diferentes.</span><span class="sxs-lookup"><span data-stu-id="ee497-154">Parallel node transition calls on different nodes are allowed.</span></span>


#### <a name="sample-usage"></a><span data-ttu-id="ee497-155">Exemplo de uso</span><span class="sxs-lookup"><span data-stu-id="ee497-155">Sample Usage</span></span>


<span data-ttu-id="ee497-156">**Exemplo 1** - o exemplo a seguir usa a API de Transição de Nó para parar um nó.</span><span class="sxs-lookup"><span data-stu-id="ee497-156">**Sample 1** - The following sample uses the Node Transition API to stop a node.</span></span>

```csharp
        // Helper function to get information about a node
        static Node GetNodeInfo(FabricClient fc, string node)
        {
            NodeList n = null;
            while (n == null)
            {
                n = fc.QueryManager.GetNodeListAsync(node).GetAwaiter().GetResult();
                Task.Delay(TimeSpan.FromSeconds(1)).GetAwaiter();
            };

            return n.FirstOrDefault();
        }

        static async Task WaitForStateAsync(FabricClient fc, Guid operationId, TestCommandProgressState targetState)
        {
            NodeTransitionProgress progress = null;

            do
            {
                bool exceptionObserved = false;
                try
                {
                    progress = await fc.TestManager.GetNodeTransitionProgressAsync(operationId, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                }
                catch (OperationCanceledException oce)
                {
                    Console.WriteLine("Caught exception '{0}'", oce);
                    exceptionObserved = true;
                }
                catch (FabricTransientException fte)
                {
                    Console.WriteLine("Caught exception '{0}'", fte);
                    exceptionObserved = true;
                }

                if (!exceptionObserved)
                {
                    Console.WriteLine("Current state of operation '{0}': {1}", operationId, progress.State);

                    if (progress.State == TestCommandProgressState.Faulted)
                    {
                        // Inspect the progress object's Result.Exception.HResult to get the error code.
                        Console.WriteLine("'{0}' failed with: {1}, HResult: {2}", operationId, progress.Result.Exception, progress.Result.Exception.HResult);

                        // ...additional logic as required
                    }

                    if (progress.State == targetState)
                    {
                        Console.WriteLine("Target state '{0}' has been reached", targetState);
                        break;
                    }
                }

                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);
            }
            while (true);
        }

        static async Task StopNodeAsync(FabricClient fc, string nodeName, int durationInSeconds)
        {
            // Uses the GetNodeListAsync() API to get information about the target node
            Node n = GetNodeInfo(fc, nodeName);

            // Create a Guid
            Guid guid = Guid.NewGuid();

            // Create a NodeStopDescription object, which will be used as a parameter into StartNodeTransition
            NodeStopDescription description = new NodeStopDescription(guid, n.NodeName, n.NodeInstanceId, durationInSeconds);

            bool wasSuccessful = false;

            do
            {
                try
                {
                    // Invoke StartNodeTransitionAsync with the NodeStopDescription from above, which will stop the target node.  Retry transient errors.
                    await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                    wasSuccessful = true;
                }
                catch (OperationCanceledException oce)
                {
                    // This is retryable
                }
                catch (FabricTransientException fte)
                {
                    // This is retryable
                }

                // Backoff
                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);
            }
            while (!wasSuccessful);

            // Now call StartNodeTransitionProgressAsync() until hte desired state is reached.
            await WaitForStateAsync(fc, guid, TestCommandProgressState.Completed).ConfigureAwait(false);
        }
```

<span data-ttu-id="ee497-157">**Exemplo 2** - o exemplo a seguir inicia um nó *parado*.</span><span class="sxs-lookup"><span data-stu-id="ee497-157">**Sample 2** - The following sample starts a *stopped* node.</span></span>  <span data-ttu-id="ee497-158">Ele usa alguns métodos auxiliares do primeiro exemplo.</span><span class="sxs-lookup"><span data-stu-id="ee497-158">It uses some helper methods from the first sample.</span></span>

```csharp
        static async Task StartNodeAsync(FabricClient fc, string nodeName)
        {
            // Uses the GetNodeListAsync() API to get information about the target node
            Node n = GetNodeInfo(fc, nodeName);

            Guid guid = Guid.NewGuid();
            BigInteger nodeInstanceId = n.NodeInstanceId;

            // Create a NodeStartDescription object, which will be used as a parameter into StartNodeTransition
            NodeStartDescription description = new NodeStartDescription(guid, n.NodeName, nodeInstanceId);

            bool wasSuccessful = false;

            do
            {
                try
                {
                    // Invoke StartNodeTransitionAsync with the NodeStartDescription from above, which will start the target stopped node.  Retry transient errors.
                    await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                    wasSuccessful = true;
                }
                catch (OperationCanceledException oce)
                {
                    Console.WriteLine("Caught exception '{0}'", oce);
                }
                catch (FabricTransientException fte)
                {
                    Console.WriteLine("Caught exception '{0}'", fte);
                }

                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);

            }
            while (!wasSuccessful);

            // Now call StartNodeTransitionProgressAsync() until hte desired state is reached.
            await WaitForStateAsync(fc, guid, TestCommandProgressState.Completed).ConfigureAwait(false);
        }
```

<span data-ttu-id="ee497-159">**Exemplo 3** - o exemplo a seguir mostra o uso incorreto.</span><span class="sxs-lookup"><span data-stu-id="ee497-159">**Sample 3** - The following sample shows incorrect usage.</span></span>  <span data-ttu-id="ee497-160">Esse uso é incorreto porque *stopDurationInSeconds* é maior do que o intervalo permitido.</span><span class="sxs-lookup"><span data-stu-id="ee497-160">This usage is incorrect because the *stopDurationInSeconds* it provides is greater than the allowed range.</span></span>  <span data-ttu-id="ee497-161">Como StartNodeTransitionAsync() falhará com um erro fatal, a operação não foi aceita, e a API de progresso não deverá ser chamada.</span><span class="sxs-lookup"><span data-stu-id="ee497-161">Since StartNodeTransitionAsync() will fail with a fatal error, the operation was not accepted, and the progress API should not be called.</span></span>  <span data-ttu-id="ee497-162">Este exemplo usa alguns métodos auxiliares do primeiro exemplo.</span><span class="sxs-lookup"><span data-stu-id="ee497-162">This sample uses some helper methods from the first sample.</span></span>

```csharp
        static async Task StopNodeWithOutOfRangeDurationAsync(FabricClient fc, string nodeName)
        {
            Node n = GetNodeInfo(fc, nodeName);

            Guid guid = Guid.NewGuid();

            // Use an out of range value for stopDurationInSeconds to demonstrate error
            NodeStopDescription description = new NodeStopDescription(guid, n.NodeName, n.NodeInstanceId, 99999);

            try
            {
                await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
            }

            catch (FabricException e)
            {
                Console.WriteLine("Caught {0}", e);
                Console.WriteLine("ErrorCode {0}", e.ErrorCode);
                // Output:
                // Caught System.Fabric.FabricException: System.Runtime.InteropServices.COMException (-2147017629)
                // StopDurationInSeconds is out of range ---> System.Runtime.InteropServices.COMException: Exception from HRESULT: 0x80071C63
                // << Parts of exception omitted>>
                //
                // ErrorCode InvalidDuration
            }
        }
```

<span data-ttu-id="ee497-163">**Exemplo 4** - o exemplo a seguir mostra as informações de erro que serão retornadas da API de Progresso de Transição de Nó quando a operação iniciada pela API de Transição de Nó for aceita, mas falhar posteriormente durante a execução.</span><span class="sxs-lookup"><span data-stu-id="ee497-163">**Sample 4** - The following sample shows the error information that will be returned from the Node Transition Progress API when the operation initiated by the Node Transition API is accepted, but fails later while executing.</span></span>  <span data-ttu-id="ee497-164">Nesse caso, ele falhará porque a API de Transição de Nó tenta iniciar um nó que não existe.</span><span class="sxs-lookup"><span data-stu-id="ee497-164">In the case, it fails because the Node Transition API attempts to start a node that does not exist.</span></span>  <span data-ttu-id="ee497-165">Este exemplo usa alguns métodos auxiliares do primeiro exemplo.</span><span class="sxs-lookup"><span data-stu-id="ee497-165">This sample uses some helper methods from the first sample.</span></span>

```csharp
        static async Task StartNodeWithNonexistentNodeAsync(FabricClient fc)
        {
            Guid guid = Guid.NewGuid();
            BigInteger nodeInstanceId = 12345;

            // Intentionally use a nonexistent node
            NodeStartDescription description = new NodeStartDescription(guid, "NonexistentNode", nodeInstanceId);

            bool wasSuccessful = false;

            do
            {
                try
                {
                    // Invoke StartNodeTransitionAsync with the NodeStartDescription from above, which will start the target stopped node.  Retry transient errors.
                    await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                    wasSuccessful = true;
                }
                catch (OperationCanceledException oce)
                {
                    Console.WriteLine("Caught exception '{0}'", oce);
                }
                catch (FabricTransientException fte)
                {
                    Console.WriteLine("Caught exception '{0}'", fte);
                }

                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);

            }
            while (!wasSuccessful);

            // Now call StartNodeTransitionProgressAsync() until the desired state is reached.  In this case, it will end up in the Faulted state since the node does not exist.
            // When StartNodeTransitionProgressAsync()'s returned progress object has a State if Faulted, inspect the progress object's Result.Exception.HResult to get the error code.
            // In this case, it will be NodeNotFound.
            await WaitForStateAsync(fc, guid, TestCommandProgressState.Faulted).ConfigureAwait(false);
        }
```

[stopnode]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.faultmanagementclient?redirectedfrom=MSDN#System_Fabric_FabricClient_FaultManagementClient_StopNodeAsync_System_String_System_Numerics_BigInteger_System_Fabric_CompletionMode_
[stopnodeps]: https://msdn.microsoft.com/library/mt125982.aspx
[startnode]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.faultmanagementclient?redirectedfrom=MSDN#System_Fabric_FabricClient_FaultManagementClient_StartNodeAsync_System_String_System_Numerics_BigInteger_System_String_System_Int32_System_Fabric_CompletionMode_System_Threading_CancellationToken_
[startnodeps]: https://msdn.microsoft.com/library/mt163520.aspx
[nodequery]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient#System_Fabric_FabricClient_QueryClient_GetNodeListAsync_System_String_
[nodequeryps]: https://docs.microsoft.com/powershell/servicefabric/vlatest/Get-ServiceFabricNode?redirectedfrom=msdn
[snt]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.testmanagementclient#System_Fabric_FabricClient_TestManagementClient_StartNodeTransitionAsync_System_Fabric_Description_NodeTransitionDescription_System_TimeSpan_System_Threading_CancellationToken_
[gntp]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.testmanagementclient#System_Fabric_FabricClient_TestManagementClient_GetNodeTransitionProgressAsync_System_Guid_System_TimeSpan_System_Threading_CancellationToken_
