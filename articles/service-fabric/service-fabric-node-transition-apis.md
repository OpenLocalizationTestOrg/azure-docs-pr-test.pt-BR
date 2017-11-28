---
title: "aaaStart e parar tootest de nós de cluster do Azure microservices | Microsoft Docs"
description: "Saiba como toouse falha injeção tootest um aplicativo do Service Fabric Iniciando e interrompendo nós de cluster."
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
ms.openlocfilehash: 7d3f5147328e6233a67533fbfb2a525aa5fc060e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replacing-hello-start-node-and-stop-node-apis-with-hello-node-transition-api"></a><span data-ttu-id="88a93-103">Substituindo hello nó iniciar e parar nó APIs com hello API de transição do nó</span><span class="sxs-lookup"><span data-stu-id="88a93-103">Replacing hello Start Node and Stop node APIs with hello Node Transition API</span></span>

## <a name="what-do-hello-stop-node-and-start-node-apis-do"></a><span data-ttu-id="88a93-104">O que Olá nó parar e iniciar o nó pelas APIs?</span><span class="sxs-lookup"><span data-stu-id="88a93-104">What do hello Stop Node and Start Node APIs do?</span></span>

<span data-ttu-id="88a93-105">Olá parar API de nó (gerenciados: [StopNodeAsync()][stopnode], PowerShell: [Stop ServiceFabricNode][stopnodeps]) para de um nó de malha do serviço.</span><span class="sxs-lookup"><span data-stu-id="88a93-105">hello Stop Node API (managed: [StopNodeAsync()][stopnode], PowerShell: [Stop-ServiceFabricNode][stopnodeps]) stops a Service Fabric node.</span></span>  <span data-ttu-id="88a93-106">Um nó de malha do serviço é o processo, não uma VM ou máquina – Olá VM ou máquina ainda será executado.</span><span class="sxs-lookup"><span data-stu-id="88a93-106">A Service Fabric node is process, not a VM or machine – hello VM or machine will still be running.</span></span>  <span data-ttu-id="88a93-107">Restante de saudação do documento hello "nó" significa que o nó de malha do serviço.</span><span class="sxs-lookup"><span data-stu-id="88a93-107">For hello rest of hello document "node" will mean Service Fabric node.</span></span>  <span data-ttu-id="88a93-108">Parada de um nó coloca-o em um *interrompido* estado em que ele não é um membro do cluster hello e não é possível hospedar serviços, assim, simulando uma *para baixo* nó.</span><span class="sxs-lookup"><span data-stu-id="88a93-108">Stopping a node puts it into a *stopped* state where it is not a member of hello cluster and cannot host services, thus simulating a *down* node.</span></span>  <span data-ttu-id="88a93-109">Isso é útil para injetar falhas em Olá sistema tootest seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="88a93-109">This is useful for injecting faults into hello system tootest your application.</span></span>  <span data-ttu-id="88a93-110">Olá iniciar API de nó (gerenciados: [StartNodeAsync()][startnode], PowerShell: [início ServiceFabricNode][startnodeps]]) reverte Olá parar a API de nó,  o que leva Olá nó tooa back o estado normal.</span><span class="sxs-lookup"><span data-stu-id="88a93-110">hello Start Node API (managed: [StartNodeAsync()][startnode], PowerShell: [Start-ServiceFabricNode][startnodeps]]) reverses hello Stop Node API,  which brings hello node back tooa normal state.</span></span>

## <a name="why-are-we-replacing-these"></a><span data-ttu-id="88a93-111">Por que os estamos substituindo?</span><span class="sxs-lookup"><span data-stu-id="88a93-111">Why are we replacing these?</span></span>

<span data-ttu-id="88a93-112">Conforme descrito anteriormente, um *interrompido* nó de malha do serviço é um nó de destino intencionalmente usando Olá parar API de nó.</span><span class="sxs-lookup"><span data-stu-id="88a93-112">As described earlier, a *stopped* Service Fabric node is a node intentionally targeted using hello Stop Node API.</span></span>  <span data-ttu-id="88a93-113">Um *para baixo* nó é um nó que está inativo por qualquer outro motivo (por exemplo, Olá VM ou máquina está desativado).</span><span class="sxs-lookup"><span data-stu-id="88a93-113">A *down* node is a node that is down for any other reason (e.g. hello VM or machine is off).</span></span>  <span data-ttu-id="88a93-114">Com hello parar API de nó, sistema Olá não expõe informações toodifferentiate entre *interrompido* nós e *para baixo* nós.</span><span class="sxs-lookup"><span data-stu-id="88a93-114">With hello Stop Node API, hello system does not expose information toodifferentiate between *stopped* nodes and *down* nodes.</span></span>

<span data-ttu-id="88a93-115">Além disso, alguns erros retornados por essas APIs não são mais tão descritivos quanto poderiam ser.</span><span class="sxs-lookup"><span data-stu-id="88a93-115">In addition, some errors returned by these APIs are not as descriptive as they could be.</span></span>  <span data-ttu-id="88a93-116">Por exemplo, chamar hello parar API de nó em uma já *interrompido* nó retornará Erro Olá *InvalidAddress*.</span><span class="sxs-lookup"><span data-stu-id="88a93-116">For example, invoking hello Stop Node API on an already *stopped* node will return hello error *InvalidAddress*.</span></span>  <span data-ttu-id="88a93-117">Essa experiência poderia ser melhorada.</span><span class="sxs-lookup"><span data-stu-id="88a93-117">This experience could be improved.</span></span>

<span data-ttu-id="88a93-118">Além disso, duração Olá que parou um nó é "infinita" até Olá que API do nó de início é invocado.</span><span class="sxs-lookup"><span data-stu-id="88a93-118">Also, hello duration a node is stopped for is “infinite” until hello Start Node API is invoked.</span></span>  <span data-ttu-id="88a93-119">Descobrimos que isso pode causar problemas e pode ser propenso a erros.</span><span class="sxs-lookup"><span data-stu-id="88a93-119">We’ve found this can cause problems and may be error-prone.</span></span>  <span data-ttu-id="88a93-120">Por exemplo, vimos problemas em que um usuário chamado hello parar API de nó em um nó e, em seguida, esquecer.</span><span class="sxs-lookup"><span data-stu-id="88a93-120">For example, we’ve seen problems where a user invoked hello Stop Node API on a node and then forgot about it.</span></span>  <span data-ttu-id="88a93-121">Posteriormente, é claro se o nó de saudação foi *para baixo* ou *interrompido*.</span><span class="sxs-lookup"><span data-stu-id="88a93-121">Later, it was unclear if hello node was *down* or *stopped*.</span></span>


## <a name="introducing-hello-node-transition-apis"></a><span data-ttu-id="88a93-122">Introdução ao Olá APIs de transição do nó</span><span class="sxs-lookup"><span data-stu-id="88a93-122">Introducing hello Node Transition APIs</span></span>

<span data-ttu-id="88a93-123">Abordamos esses problemas acima em um novo conjunto de APIs.</span><span class="sxs-lookup"><span data-stu-id="88a93-123">We’ve addressed these issues above in a new set of APIs.</span></span>  <span data-ttu-id="88a93-124">Olá nova API de transição de nó (gerenciados: [StartNodeTransitionAsync()][snt]) pode ser usado tootransition um tooa de nó do Service Fabric *interrompido* estado ou tootransition-lo de um *interrompido* tooa de estado normal de backup do estado.</span><span class="sxs-lookup"><span data-stu-id="88a93-124">hello new Node Transition API (managed: [StartNodeTransitionAsync()][snt]) may be used tootransition a Service Fabric node tooa *stopped* state, or tootransition it from a *stopped* state tooa normal up state.</span></span>  <span data-ttu-id="88a93-125">Observe que hello "Start" no nome de saudação do hello API não se refere a toostarting um nó.</span><span class="sxs-lookup"><span data-stu-id="88a93-125">Please note that hello “Start” in hello name of hello API does not refer toostarting a node.</span></span>  <span data-ttu-id="88a93-126">Refere-se uma operação assíncrona que o sistema Olá executará tootransition Olá nó tooeither de toobeginning *interrompido* ou estado foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="88a93-126">It refers toobeginning an asynchronous operation that hello system will execute tootransition hello node tooeither *stopped* or started state.</span></span>

<span data-ttu-id="88a93-127">**Uso**</span><span class="sxs-lookup"><span data-stu-id="88a93-127">**Usage**</span></span>

<span data-ttu-id="88a93-128">Se Olá API de transição de nó não gerará uma exceção quando invocado, em seguida, Olá sistema aceitou a operação assíncrona hello e executará a ele.</span><span class="sxs-lookup"><span data-stu-id="88a93-128">If hello Node Transition API does not throw an exception when invoked, then hello system has accepted hello asynchronous operation, and will execute it.</span></span>  <span data-ttu-id="88a93-129">Uma chamada bem-sucedida não implica a conclusão da operação de saudação ainda.</span><span class="sxs-lookup"><span data-stu-id="88a93-129">A successful call does not imply hello operation is finished yet.</span></span>  <span data-ttu-id="88a93-130">informações de tooget sobre Olá atual estado da operação hello, Olá chamada de API de progresso do nó de transição (gerenciados: [GetNodeTransitionProgressAsync()][gntp]) com o guid de saudação usada ao chamar o nó API de transição para esta operação.</span><span class="sxs-lookup"><span data-stu-id="88a93-130">tooget information about hello current state of hello operation, call hello Node Transition Progress API (managed: [GetNodeTransitionProgressAsync()][gntp]) with hello guid used when invoking Node Transition API for this operation.</span></span>  <span data-ttu-id="88a93-131">Olá nó transição andamento API retorna um objeto de NodeTransitionProgress.</span><span class="sxs-lookup"><span data-stu-id="88a93-131">hello Node Transition Progress API returns an NodeTransitionProgress object.</span></span>  <span data-ttu-id="88a93-132">A propriedade do objeto estado Especifica o estado atual de saudação da operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="88a93-132">This object’s State property specifies hello current state of hello operation.</span></span>  <span data-ttu-id="88a93-133">Se o estado de saudação é "Running", em seguida, Olá operação está em execução.</span><span class="sxs-lookup"><span data-stu-id="88a93-133">If hello state is “Running” then hello operation is executing.</span></span>  <span data-ttu-id="88a93-134">Se ela for concluída, a operação de saudação concluída sem erros.</span><span class="sxs-lookup"><span data-stu-id="88a93-134">If it is Completed, hello operation finished without error.</span></span>  <span data-ttu-id="88a93-135">Se estiver com defeito, houve um problema ao executar a operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="88a93-135">If it is Faulted, there was a problem executing hello operation.</span></span>  <span data-ttu-id="88a93-136">Exceção da propriedade de resultado Olá propriedade indicará quais Olá emitir era.</span><span class="sxs-lookup"><span data-stu-id="88a93-136">hello Result property’s Exception property will indicate what hello issue was.</span></span>  <span data-ttu-id="88a93-137">Consulte https://docs.microsoft.com/dotnet/api/system.fabric.testcommandprogressstate para obter mais informações sobre a propriedade State de saudação e a seção de "Exemplo de uso" hello abaixo para obter exemplos de código.</span><span class="sxs-lookup"><span data-stu-id="88a93-137">See https://docs.microsoft.com/dotnet/api/system.fabric.testcommandprogressstate for more information about hello State property, and hello “Sample Usage” section below for code examples.</span></span>


<span data-ttu-id="88a93-138">**Diferenciar entre um nó de parada e um nó para baixo** se um nó é *interrompido* usando Olá API de transição de nó, saída de saudação de uma consulta de nó (gerenciados: [GetNodeListAsync()] [ nodequery], PowerShell: [Get-ServiceFabricNode][nodequeryps]) mostrará que este nó tem um *IsStopped* valor da propriedade true.</span><span class="sxs-lookup"><span data-stu-id="88a93-138">**Differentiating between a stopped node and a down node** If a node is *stopped* using hello Node Transition API, hello output of a node query (managed: [GetNodeListAsync()][nodequery], PowerShell: [Get-ServiceFabricNode][nodequeryps]) will show that this node has an *IsStopped* property value of true.</span></span>  <span data-ttu-id="88a93-139">Observe que isso é diferente do valor Olá Olá *NodeStatus* propriedade dirá *para baixo*.</span><span class="sxs-lookup"><span data-stu-id="88a93-139">Note this is different from hello value of hello *NodeStatus* property, which will say *Down*.</span></span>  <span data-ttu-id="88a93-140">Se hello *NodeStatus* propriedade tem um valor de *para baixo*, mas *IsStopped* é false, e em seguida, o nó de saudação não foi parado usando Olá API de transição de nó e é  *Para baixo* devido a algum outro motivo.</span><span class="sxs-lookup"><span data-stu-id="88a93-140">If hello *NodeStatus* property has a value of *Down*, but *IsStopped* is false, then hello node was not stopped using hello Node Transition API, and is *Down* due some other reason.</span></span>  <span data-ttu-id="88a93-141">Se hello *IsStopped* propriedade é true e hello *NodeStatus* é de propriedade *para baixo*, e foi parado usando Olá API de transição do nó.</span><span class="sxs-lookup"><span data-stu-id="88a93-141">If hello *IsStopped* property is true, and hello *NodeStatus* property is *Down*, then it was stopped using hello Node Transition API.</span></span>

<span data-ttu-id="88a93-142">Iniciando um *interrompido* nó usando Olá nó transição API retornará-toofunction como membro do cluster de saudação normal novamente.</span><span class="sxs-lookup"><span data-stu-id="88a93-142">Starting a *stopped* node using hello Node Transition API will return it toofunction as a normal member of hello cluster again.</span></span>  <span data-ttu-id="88a93-143">Olá saída da consulta de nó Olá API mostrará *IsStopped* como false, e *NodeStatus* como algo que não é para baixo (por exemplo, para cima).</span><span class="sxs-lookup"><span data-stu-id="88a93-143">hello output of hello node query API will show *IsStopped* as false, and *NodeStatus* as something that is not Down (e.g. Up).</span></span>


<span data-ttu-id="88a93-144">**Limitado a duração** ao usar o hello nó transição API toostop um nó, parâmetros, uma saudação necessários *stopNodeDurationInSeconds*, representa Olá a quantidade de tempo no nó de saudação tookeep segundos  *interrompido*.</span><span class="sxs-lookup"><span data-stu-id="88a93-144">**Limited Duration** When using hello Node Transition API toostop a node, one of hello required parameters, *stopNodeDurationInSeconds*, represents hello amount of time in seconds tookeep hello node *stopped*.</span></span>  <span data-ttu-id="88a93-145">Esse valor deve estar no intervalo, que tem um mínimo de 600 e 14400 máximo permitida de saudação.</span><span class="sxs-lookup"><span data-stu-id="88a93-145">This value must be in hello allowed range, which has a minimum of 600, and a maximum of 14400.</span></span>  <span data-ttu-id="88a93-146">Após esse tempo expirar, nó Olá será reiniciado com o estado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="88a93-146">After this time expires, hello node will restart itself into Up state automatically.</span></span>  <span data-ttu-id="88a93-147">Consulte tooSample 1 abaixo para obter um exemplo de uso.</span><span class="sxs-lookup"><span data-stu-id="88a93-147">Refer tooSample 1 below for an example of usage.</span></span>

> [!WARNING]
> <span data-ttu-id="88a93-148">Evitar a mistura de APIs de transição de nó e Olá nó parar e iniciar APIs de nó.</span><span class="sxs-lookup"><span data-stu-id="88a93-148">Avoid mixing Node Transition APIs and hello Stop Node and Start Node APIs.</span></span>  <span data-ttu-id="88a93-149">recomendação de saudação é muito usar apenas a API de transição do nó hello.</span><span class="sxs-lookup"><span data-stu-id="88a93-149">hello recommendation is too use hello Node Transition API only.</span></span>  <span data-ttu-id="88a93-150">> Se um nó já foi interrompido usando Olá parar de API do nó, ele deve ser iniciado usando Olá iniciar nó API primeiro antes de usar o hello > APIs de transição do nó.</span><span class="sxs-lookup"><span data-stu-id="88a93-150">> If a node has been already been stopped using hello Stop Node API, it should be started using hello Start Node API first before using hello > Node Transition APIs.</span></span>

> [!WARNING]
> <span data-ttu-id="88a93-151">Várias APIs de transição de nó não não possível fazer chamadas em Olá mesmo nó em paralelo.</span><span class="sxs-lookup"><span data-stu-id="88a93-151">Multiple Node Transition APIs calls cannot be made on hello same node in parallel.</span></span>  <span data-ttu-id="88a93-152">Em tal situação, Olá API de transição de nó será > lançar um FabricException com um valor de propriedade ErrorCode de NodeTransitionInProgress.</span><span class="sxs-lookup"><span data-stu-id="88a93-152">In such a situation, hello Node Transition API will    > throw a FabricException with an ErrorCode property value of NodeTransitionInProgress.</span></span>  <span data-ttu-id="88a93-153">Depois que tiver uma transição de nó em um nó específico > foi iniciado, você deve aguardar até que a operação Olá atinge um estado terminal (ForceCancelled ou com falha, concluído) antes de iniciar uma > transição novos no hello mesmo nó.</span><span class="sxs-lookup"><span data-stu-id="88a93-153">Once a node transition on a specific node has  > been started, you should wait until hello operation reaches a terminal state (Completed, Faulted, or ForceCancelled) before starting a  > new transition on hello same node.</span></span>  <span data-ttu-id="88a93-154">São permitidas chamadas de transição de nó paralelas em nós diferentes.</span><span class="sxs-lookup"><span data-stu-id="88a93-154">Parallel node transition calls on different nodes are allowed.</span></span>


#### <a name="sample-usage"></a><span data-ttu-id="88a93-155">Exemplo de uso</span><span class="sxs-lookup"><span data-stu-id="88a93-155">Sample Usage</span></span>


<span data-ttu-id="88a93-156">**Exemplo 1** -Olá usos de exemplo a seguir Olá nó transição API toostop um nó.</span><span class="sxs-lookup"><span data-stu-id="88a93-156">**Sample 1** - hello following sample uses hello Node Transition API toostop a node.</span></span>

```csharp
        // Helper function tooget information about a node
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
                        // Inspect hello progress object's Result.Exception.HResult tooget hello error code.
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
            // Uses hello GetNodeListAsync() API tooget information about hello target node
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
                    // Invoke StartNodeTransitionAsync with hello NodeStopDescription from above, which will stop hello target node.  Retry transient errors.
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

<span data-ttu-id="88a93-157">**Exemplo 2** - Olá seguindo o exemplo inicia um *interrompido* nó.</span><span class="sxs-lookup"><span data-stu-id="88a93-157">**Sample 2** - hello following sample starts a *stopped* node.</span></span>  <span data-ttu-id="88a93-158">Ele usa alguns métodos auxiliares do primeiro exemplo de saudação.</span><span class="sxs-lookup"><span data-stu-id="88a93-158">It uses some helper methods from hello first sample.</span></span>

```csharp
        static async Task StartNodeAsync(FabricClient fc, string nodeName)
        {
            // Uses hello GetNodeListAsync() API tooget information about hello target node
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
                    // Invoke StartNodeTransitionAsync with hello NodeStartDescription from above, which will start hello target stopped node.  Retry transient errors.
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

<span data-ttu-id="88a93-159">**Exemplo 3** - Olá exemplo a seguir mostra o uso incorreto.</span><span class="sxs-lookup"><span data-stu-id="88a93-159">**Sample 3** - hello following sample shows incorrect usage.</span></span>  <span data-ttu-id="88a93-160">Esse uso está incorreto porque Olá *stopDurationInSeconds* é maior que o intervalo permitida de saudação.</span><span class="sxs-lookup"><span data-stu-id="88a93-160">This usage is incorrect because hello *stopDurationInSeconds* it provides is greater than hello allowed range.</span></span>  <span data-ttu-id="88a93-161">Como StartNodeTransitionAsync() falhará com um erro fatal, operação Olá não foi aceito e API de progresso de saudação não deve ser chamado.</span><span class="sxs-lookup"><span data-stu-id="88a93-161">Since StartNodeTransitionAsync() will fail with a fatal error, hello operation was not accepted, and hello progress API should not be called.</span></span>  <span data-ttu-id="88a93-162">Este exemplo usa alguns métodos auxiliares do primeiro exemplo de saudação.</span><span class="sxs-lookup"><span data-stu-id="88a93-162">This sample uses some helper methods from hello first sample.</span></span>

```csharp
        static async Task StopNodeWithOutOfRangeDurationAsync(FabricClient fc, string nodeName)
        {
            Node n = GetNodeInfo(fc, nodeName);

            Guid guid = Guid.NewGuid();

            // Use an out of range value for stopDurationInSeconds toodemonstrate error
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

<span data-ttu-id="88a93-163">**Exemplo 4** - Olá exemplo a seguir mostra as informações de erro de saudação que serão retornadas de saudação nó transição andamento API quando operação Olá iniciada pelo Olá API de transição do nó é aceito, mas falha posteriormente durante a execução.</span><span class="sxs-lookup"><span data-stu-id="88a93-163">**Sample 4** - hello following sample shows hello error information that will be returned from hello Node Transition Progress API when hello operation initiated by hello Node Transition API is accepted, but fails later while executing.</span></span>  <span data-ttu-id="88a93-164">No caso de Olá falha porque Olá nó transição API tentativas toostart um nó que não existe.</span><span class="sxs-lookup"><span data-stu-id="88a93-164">In hello case, it fails because hello Node Transition API attempts toostart a node that does not exist.</span></span>  <span data-ttu-id="88a93-165">Este exemplo usa alguns métodos auxiliares do primeiro exemplo de saudação.</span><span class="sxs-lookup"><span data-stu-id="88a93-165">This sample uses some helper methods from hello first sample.</span></span>

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
                    // Invoke StartNodeTransitionAsync with hello NodeStartDescription from above, which will start hello target stopped node.  Retry transient errors.
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

            // Now call StartNodeTransitionProgressAsync() until hello desired state is reached.  In this case, it will end up in hello Faulted state since hello node does not exist.
            // When StartNodeTransitionProgressAsync()'s returned progress object has a State if Faulted, inspect hello progress object's Result.Exception.HResult tooget hello error code.
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
