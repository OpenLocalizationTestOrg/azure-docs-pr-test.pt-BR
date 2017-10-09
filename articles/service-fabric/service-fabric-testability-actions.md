---
title: falhas de aaaSimulate em microservices do Azure | Microsoft Docs
description: "Este artigo fala sobre ações de capacidade de teste de saudação encontradas no Microsoft Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: motanv
manager: timlt
editor: toddabel
ms.assetid: ed53ca5c-4d5e-4b48-93c9-e386f32d8b7a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: motanv;heeldin
ms.openlocfilehash: 5bdda1c0c5a40b243ab956c4791afd52e11c4089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="testability-actions"></a><span data-ttu-id="8c54e-103">Ações da Possibilidade de Teste</span><span class="sxs-lookup"><span data-stu-id="8c54e-103">Testability actions</span></span>
<span data-ttu-id="8c54e-104">Em ordem toosimulate uma infraestrutura não confiável, Azure Service Fabric fornece, desenvolvedor hello, com modos toosimulate várias falhas do mundo real e as transições de estado.</span><span class="sxs-lookup"><span data-stu-id="8c54e-104">In order toosimulate an unreliable infrastructure, Azure Service Fabric provides you, hello developer, with ways toosimulate various real-world failures and state transitions.</span></span> <span data-ttu-id="8c54e-105">Elas são expostas como ações de possibilidade de teste.</span><span class="sxs-lookup"><span data-stu-id="8c54e-105">These are exposed as testability actions.</span></span> <span data-ttu-id="8c54e-106">ações de saudação são Olá APIs de baixo nível que causam uma injeção de falha específico, a transição de estado ou a validação.</span><span class="sxs-lookup"><span data-stu-id="8c54e-106">hello actions are hello low-level APIs that cause a specific fault injection, state transition, or validation.</span></span> <span data-ttu-id="8c54e-107">Ao combinar essas ações, você pode criar cenários de teste abrangentes para seus serviços.</span><span class="sxs-lookup"><span data-stu-id="8c54e-107">By combining these actions, you can write comprehensive test scenarios for your services.</span></span>

<span data-ttu-id="8c54e-108">O Service Fabric fornece alguns cenários comuns de teste compostos por essas ações.</span><span class="sxs-lookup"><span data-stu-id="8c54e-108">Service Fabric provides some common test scenarios composed of these actions.</span></span> <span data-ttu-id="8c54e-109">É altamente recomendável que você utiliza esses cenários internos, que são escolhidos com cuidado as transições de estado comum tootest e casos de falha.</span><span class="sxs-lookup"><span data-stu-id="8c54e-109">We highly recommend that you utilize these built-in scenarios, which are carefully chosen tootest common state transitions and failure cases.</span></span> <span data-ttu-id="8c54e-110">No entanto, as ações podem ser cenários de teste personalizada toocreate usado quando você desejar tooadd cobertura para cenários que não são cobertas por cenários internos Olá ainda ou que são personalizados personalizadas para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8c54e-110">However, actions can be used toocreate custom test scenarios when you want tooadd coverage for scenarios that are not covered by hello built-in scenarios yet or that are custom tailored for your application.</span></span>

<span data-ttu-id="8c54e-111">C# implementações das ações de saudação são encontradas em Olá System.Fabric.dll assembly.</span><span class="sxs-lookup"><span data-stu-id="8c54e-111">C# implementations of hello actions are found in hello System.Fabric.dll assembly.</span></span> <span data-ttu-id="8c54e-112">módulo do PowerShell de malha do sistema Olá encontra-se em Olá Microsoft.ServiceFabric.Powershell.dll assembly.</span><span class="sxs-lookup"><span data-stu-id="8c54e-112">hello System Fabric PowerShell module is found in hello Microsoft.ServiceFabric.Powershell.dll assembly.</span></span> <span data-ttu-id="8c54e-113">Como parte da instalação do tempo de execução, Olá módulo ServiceFabric do PowerShell é instalado tooallow para facilidade de uso.</span><span class="sxs-lookup"><span data-stu-id="8c54e-113">As part of runtime installation, hello ServiceFabric PowerShell module is installed tooallow for ease of use.</span></span>

## <a name="graceful-vs-ungraceful-fault-actions"></a><span data-ttu-id="8c54e-114">Ações de falha normais x anormais</span><span class="sxs-lookup"><span data-stu-id="8c54e-114">Graceful vs. ungraceful fault actions</span></span>
<span data-ttu-id="8c54e-115">As ações da Possibilidade de Teste são classificadas em dois blocos principais:</span><span class="sxs-lookup"><span data-stu-id="8c54e-115">Testability actions are classified into two major buckets:</span></span>

* <span data-ttu-id="8c54e-116">Falhas anormais: simulam falhas como reinicializações de máquina e panes de processo.</span><span class="sxs-lookup"><span data-stu-id="8c54e-116">Ungraceful faults: These faults simulate failures like machine restarts and process crashes.</span></span> <span data-ttu-id="8c54e-117">No caso de falhas, o contexto de execução de saudação do processo para abruptamente.</span><span class="sxs-lookup"><span data-stu-id="8c54e-117">In such cases of failures, hello execution context of process stops abruptly.</span></span> <span data-ttu-id="8c54e-118">Isso significa que nenhuma limpeza do estado de saudação pode ser executado antes que o aplicativo hello for iniciado novamente.</span><span class="sxs-lookup"><span data-stu-id="8c54e-118">This means no cleanup of hello state can run before hello application starts up again.</span></span>
* <span data-ttu-id="8c54e-119">Falhas normais: simulam ações normais como movimentações de réplica e remoções acionadas pelo balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="8c54e-119">Graceful faults: These faults simulate graceful actions like replica moves and drops triggered by load balancing.</span></span> <span data-ttu-id="8c54e-120">Nesses casos, o serviço de saudação recebe uma notificação de saudação fechar e pode limpar o estado de saudação antes de sair.</span><span class="sxs-lookup"><span data-stu-id="8c54e-120">In such cases, hello service gets a notification of hello close and can clean up hello state before exiting.</span></span>

<span data-ttu-id="8c54e-121">Para validação de melhor qualidade, executar o serviço de saudação e carga de trabalho de negócios ao induzindo várias falhas normais e anormais.</span><span class="sxs-lookup"><span data-stu-id="8c54e-121">For better quality validation, run hello service and business workload while inducing various graceful and ungraceful faults.</span></span> <span data-ttu-id="8c54e-122">Falhas anormais exercitam cenários em que o processo de serviço Olá abruptamente encerrada no meio de saudação de fluxos de trabalho.</span><span class="sxs-lookup"><span data-stu-id="8c54e-122">Ungraceful faults exercise scenarios where hello service process abruptly exits in hello middle of some workflow.</span></span> <span data-ttu-id="8c54e-123">Isso testa o caminho de recuperação hello quando réplicas do serviço Olá for restaurada pela malha do serviço.</span><span class="sxs-lookup"><span data-stu-id="8c54e-123">This tests  hello recovery path once hello service replica is restored by Service Fabric.</span></span> <span data-ttu-id="8c54e-124">Isso ajudará a consistência dos dados e se o estado do serviço Olá é mantido corretamente após falhas de teste.</span><span class="sxs-lookup"><span data-stu-id="8c54e-124">This will help test data consistency and whether hello service state is maintained correctly after failures.</span></span> <span data-ttu-id="8c54e-125">Hello outro conjunto de falhas (saudação normal de falhas) de teste que o serviço Olá reage corretamente tooreplicas seja movido pela malha do serviço.</span><span class="sxs-lookup"><span data-stu-id="8c54e-125">hello other set of failures (hello graceful failures) test that hello service correctly reacts tooreplicas being moved around by Service Fabric.</span></span> <span data-ttu-id="8c54e-126">Isso testa o tratamento de cancelamento no método de RunAsync hello.</span><span class="sxs-lookup"><span data-stu-id="8c54e-126">This tests handling of cancellation in hello RunAsync method.</span></span> <span data-ttu-id="8c54e-127">serviço de saudação precisa toocheck Olá cancelamento token que está sendo definido corretamente salvar seu estado e sair do método de RunAsync hello.</span><span class="sxs-lookup"><span data-stu-id="8c54e-127">hello service needs toocheck for hello cancellation token being set, correctly save its state, and exit hello RunAsync method.</span></span>

## <a name="testability-actions-list"></a><span data-ttu-id="8c54e-128">Lista de ações da Possibilidade de Teste</span><span class="sxs-lookup"><span data-stu-id="8c54e-128">Testability actions list</span></span>
| <span data-ttu-id="8c54e-129">Ação</span><span class="sxs-lookup"><span data-stu-id="8c54e-129">Action</span></span> | <span data-ttu-id="8c54e-130">Descrição</span><span class="sxs-lookup"><span data-stu-id="8c54e-130">Description</span></span> | <span data-ttu-id="8c54e-131">API gerenciada</span><span class="sxs-lookup"><span data-stu-id="8c54e-131">Managed API</span></span> | <span data-ttu-id="8c54e-132">Cmdlet do Powershell</span><span class="sxs-lookup"><span data-stu-id="8c54e-132">PowerShell cmdlet</span></span> | <span data-ttu-id="8c54e-133">Falhas normais/anormais</span><span class="sxs-lookup"><span data-stu-id="8c54e-133">Graceful/ungraceful faults</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="8c54e-134">CleanTestState</span><span class="sxs-lookup"><span data-stu-id="8c54e-134">CleanTestState</span></span> |<span data-ttu-id="8c54e-135">Remove todos os estados de teste de saudação do cluster Olá no caso de um desligamento incorreto do driver de teste de saudação.</span><span class="sxs-lookup"><span data-stu-id="8c54e-135">Removes all hello test state from hello cluster in case of a bad shutdown of hello test driver.</span></span> |<span data-ttu-id="8c54e-136">CleanTestStateAsync</span><span class="sxs-lookup"><span data-stu-id="8c54e-136">CleanTestStateAsync</span></span> |<span data-ttu-id="8c54e-137">Remove-ServiceFabricTestState</span><span class="sxs-lookup"><span data-stu-id="8c54e-137">Remove-ServiceFabricTestState</span></span> |<span data-ttu-id="8c54e-138">Não aplicável</span><span class="sxs-lookup"><span data-stu-id="8c54e-138">Not applicable</span></span> |
| <span data-ttu-id="8c54e-139">InvokeDataLoss</span><span class="sxs-lookup"><span data-stu-id="8c54e-139">InvokeDataLoss</span></span> |<span data-ttu-id="8c54e-140">Induz a perda de dados em uma partição de serviço.</span><span class="sxs-lookup"><span data-stu-id="8c54e-140">Induces data loss into a service partition.</span></span> |<span data-ttu-id="8c54e-141">InvokeDataLossAsync</span><span class="sxs-lookup"><span data-stu-id="8c54e-141">InvokeDataLossAsync</span></span> |<span data-ttu-id="8c54e-142">Invoke-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="8c54e-142">Invoke-ServiceFabricPartitionDataLoss</span></span> |<span data-ttu-id="8c54e-143">Normal</span><span class="sxs-lookup"><span data-stu-id="8c54e-143">Graceful</span></span> |
| <span data-ttu-id="8c54e-144">InvokeQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="8c54e-144">InvokeQuorumLoss</span></span> |<span data-ttu-id="8c54e-145">Coloca uma determinada partição de serviço com estado na perda de quórum.</span><span class="sxs-lookup"><span data-stu-id="8c54e-145">Puts a given stateful service partition into quorum loss.</span></span> |<span data-ttu-id="8c54e-146">InvokeQuorumLossAsync</span><span class="sxs-lookup"><span data-stu-id="8c54e-146">InvokeQuorumLossAsync</span></span> |<span data-ttu-id="8c54e-147">Invoke-ServiceFabricQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="8c54e-147">Invoke-ServiceFabricQuorumLoss</span></span> |<span data-ttu-id="8c54e-148">Normal</span><span class="sxs-lookup"><span data-stu-id="8c54e-148">Graceful</span></span> |
| <span data-ttu-id="8c54e-149">Mover primária</span><span class="sxs-lookup"><span data-stu-id="8c54e-149">Move Primary</span></span> |<span data-ttu-id="8c54e-150">Olá move especificado a réplica primária de um nó de cluster especificado toohello serviço com monitoração de estado.</span><span class="sxs-lookup"><span data-stu-id="8c54e-150">Moves hello specified primary replica of a stateful service toohello specified cluster node.</span></span> |<span data-ttu-id="8c54e-151">MovePrimaryAsync</span><span class="sxs-lookup"><span data-stu-id="8c54e-151">MovePrimaryAsync</span></span> |<span data-ttu-id="8c54e-152">Move-ServiceFabricPrimaryReplica</span><span class="sxs-lookup"><span data-stu-id="8c54e-152">Move-ServiceFabricPrimaryReplica</span></span> |<span data-ttu-id="8c54e-153">Normal</span><span class="sxs-lookup"><span data-stu-id="8c54e-153">Graceful</span></span> |
| <span data-ttu-id="8c54e-154">Mover secundária</span><span class="sxs-lookup"><span data-stu-id="8c54e-154">Move Secondary</span></span> |<span data-ttu-id="8c54e-155">Move a réplica secundária atual de saudação de um nó de cluster diferente de tooa de serviço com monitoração de estado.</span><span class="sxs-lookup"><span data-stu-id="8c54e-155">Moves hello current secondary replica of a stateful service tooa different cluster node.</span></span> |<span data-ttu-id="8c54e-156">MoveSecondaryAsync</span><span class="sxs-lookup"><span data-stu-id="8c54e-156">MoveSecondaryAsync</span></span> |<span data-ttu-id="8c54e-157">Move-ServiceFabricSecondaryReplica</span><span class="sxs-lookup"><span data-stu-id="8c54e-157">Move-ServiceFabricSecondaryReplica</span></span> |<span data-ttu-id="8c54e-158">Normal</span><span class="sxs-lookup"><span data-stu-id="8c54e-158">Graceful</span></span> |
| <span data-ttu-id="8c54e-159">RemoveReplica</span><span class="sxs-lookup"><span data-stu-id="8c54e-159">RemoveReplica</span></span> |<span data-ttu-id="8c54e-160">Simula uma falha de réplica removendo uma réplica de um cluster.</span><span class="sxs-lookup"><span data-stu-id="8c54e-160">Simulates a replica failure by removing a replica from a cluster.</span></span> <span data-ttu-id="8c54e-161">Isso fechará réplica hello e mudará toorole 'None', removendo todos os seus estados de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="8c54e-161">This will close hello replica and will transition it toorole 'None', removing all of its state from hello cluster.</span></span> |<span data-ttu-id="8c54e-162">RemoveReplicaAsync</span><span class="sxs-lookup"><span data-stu-id="8c54e-162">RemoveReplicaAsync</span></span> |<span data-ttu-id="8c54e-163">Remove-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="8c54e-163">Remove-ServiceFabricReplica</span></span> |<span data-ttu-id="8c54e-164">Normal</span><span class="sxs-lookup"><span data-stu-id="8c54e-164">Graceful</span></span> |
| <span data-ttu-id="8c54e-165">RestartDeployedCodePackage</span><span class="sxs-lookup"><span data-stu-id="8c54e-165">RestartDeployedCodePackage</span></span> |<span data-ttu-id="8c54e-166">Simula uma falha de processo do pacote de códigos reiniciando um pacote de códigos implantado em um nó em um cluster.</span><span class="sxs-lookup"><span data-stu-id="8c54e-166">Simulates a code package process failure by restarting a code package deployed on a node in a cluster.</span></span> <span data-ttu-id="8c54e-167">Isso anula o processo de pacote de código hello, que irá reiniciar todas as réplicas de serviço do usuário Olá hospedadas no processo.</span><span class="sxs-lookup"><span data-stu-id="8c54e-167">This aborts hello code package process, which will restart all hello user service replicas hosted in that process.</span></span> |<span data-ttu-id="8c54e-168">RestartDeployedCodePackageAsync</span><span class="sxs-lookup"><span data-stu-id="8c54e-168">RestartDeployedCodePackageAsync</span></span> |<span data-ttu-id="8c54e-169">Restart-ServiceFabricDeployedCodePackage</span><span class="sxs-lookup"><span data-stu-id="8c54e-169">Restart-ServiceFabricDeployedCodePackage</span></span> |<span data-ttu-id="8c54e-170">Anormais</span><span class="sxs-lookup"><span data-stu-id="8c54e-170">Ungraceful</span></span> |
| <span data-ttu-id="8c54e-171">RestartNode</span><span class="sxs-lookup"><span data-stu-id="8c54e-171">RestartNode</span></span> |<span data-ttu-id="8c54e-172">Simula uma falha de nó de cluster da Malha de Serviço reinicializando um nó.</span><span class="sxs-lookup"><span data-stu-id="8c54e-172">Simulates a Service Fabric cluster node failure by restarting a node.</span></span> |<span data-ttu-id="8c54e-173">RestartNodeAsync</span><span class="sxs-lookup"><span data-stu-id="8c54e-173">RestartNodeAsync</span></span> |<span data-ttu-id="8c54e-174">Restart-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="8c54e-174">Restart-ServiceFabricNode</span></span> |<span data-ttu-id="8c54e-175">Anormais</span><span class="sxs-lookup"><span data-stu-id="8c54e-175">Ungraceful</span></span> |
| <span data-ttu-id="8c54e-176">RestartPartition</span><span class="sxs-lookup"><span data-stu-id="8c54e-176">RestartPartition</span></span> |<span data-ttu-id="8c54e-177">Simula um cenário de blecaute do datacenter ou cluster reiniciando algumas ou todas as réplicas de uma partição.</span><span class="sxs-lookup"><span data-stu-id="8c54e-177">Simulates a datacenter blackout or cluster blackout scenario by restarting some or all replicas of a partition.</span></span> |<span data-ttu-id="8c54e-178">RestartPartitionAsync</span><span class="sxs-lookup"><span data-stu-id="8c54e-178">RestartPartitionAsync</span></span> |<span data-ttu-id="8c54e-179">Restart-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="8c54e-179">Restart-ServiceFabricPartition</span></span> |<span data-ttu-id="8c54e-180">Normal</span><span class="sxs-lookup"><span data-stu-id="8c54e-180">Graceful</span></span> |
| <span data-ttu-id="8c54e-181">RestartReplica</span><span class="sxs-lookup"><span data-stu-id="8c54e-181">RestartReplica</span></span> |<span data-ttu-id="8c54e-182">Simule uma falha de réplica reiniciando uma réplica persistente em um cluster, fechando réplica hello e, em seguida, abri-la.</span><span class="sxs-lookup"><span data-stu-id="8c54e-182">Simulates a replica failure by restarting a persisted replica in a cluster, closing hello replica and then reopening it.</span></span> |<span data-ttu-id="8c54e-183">RestartReplicaAsync</span><span class="sxs-lookup"><span data-stu-id="8c54e-183">RestartReplicaAsync</span></span> |<span data-ttu-id="8c54e-184">Restart-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="8c54e-184">Restart-ServiceFabricReplica</span></span> |<span data-ttu-id="8c54e-185">Normal</span><span class="sxs-lookup"><span data-stu-id="8c54e-185">Graceful</span></span> |
| <span data-ttu-id="8c54e-186">StartNode</span><span class="sxs-lookup"><span data-stu-id="8c54e-186">StartNode</span></span> |<span data-ttu-id="8c54e-187">Inicia um nó em um cluster que já foi interrompido.</span><span class="sxs-lookup"><span data-stu-id="8c54e-187">Starts a node in a cluster that is already stopped.</span></span> |<span data-ttu-id="8c54e-188">StartNodeAsync</span><span class="sxs-lookup"><span data-stu-id="8c54e-188">StartNodeAsync</span></span> |<span data-ttu-id="8c54e-189">Start-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="8c54e-189">Start-ServiceFabricNode</span></span> |<span data-ttu-id="8c54e-190">Não aplicável</span><span class="sxs-lookup"><span data-stu-id="8c54e-190">Not applicable</span></span> |
| <span data-ttu-id="8c54e-191">StopNode</span><span class="sxs-lookup"><span data-stu-id="8c54e-191">StopNode</span></span> |<span data-ttu-id="8c54e-192">Simula uma falha de nó interrompendo um nó em um cluster.</span><span class="sxs-lookup"><span data-stu-id="8c54e-192">Simulates a node failure by stopping a node in a cluster.</span></span> <span data-ttu-id="8c54e-193">nó de saudação permanecerá inativo até StartNode é chamado.</span><span class="sxs-lookup"><span data-stu-id="8c54e-193">hello node will stay down until StartNode is called.</span></span> |<span data-ttu-id="8c54e-194">StopNodeAsync</span><span class="sxs-lookup"><span data-stu-id="8c54e-194">StopNodeAsync</span></span> |<span data-ttu-id="8c54e-195">Stop-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="8c54e-195">Stop-ServiceFabricNode</span></span> |<span data-ttu-id="8c54e-196">Anormais</span><span class="sxs-lookup"><span data-stu-id="8c54e-196">Ungraceful</span></span> |
| <span data-ttu-id="8c54e-197">ValidateApplication</span><span class="sxs-lookup"><span data-stu-id="8c54e-197">ValidateApplication</span></span> |<span data-ttu-id="8c54e-198">Valida a disponibilidade de saudação e a integridade de todos os serviços do Service Fabric dentro de um aplicativo, geralmente após induzindo algumas falhas no sistema de saudação.</span><span class="sxs-lookup"><span data-stu-id="8c54e-198">Validates hello availability and health of all Service Fabric services within an application, usually after inducing some fault into hello system.</span></span> |<span data-ttu-id="8c54e-199">ValidateApplicationAsync</span><span class="sxs-lookup"><span data-stu-id="8c54e-199">ValidateApplicationAsync</span></span> |<span data-ttu-id="8c54e-200">Test-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="8c54e-200">Test-ServiceFabricApplication</span></span> |<span data-ttu-id="8c54e-201">Não aplicável</span><span class="sxs-lookup"><span data-stu-id="8c54e-201">Not applicable</span></span> |
| <span data-ttu-id="8c54e-202">ValidateService</span><span class="sxs-lookup"><span data-stu-id="8c54e-202">ValidateService</span></span> |<span data-ttu-id="8c54e-203">Valida a disponibilidade hello e a integridade de um serviço de malha do serviço, geralmente após induzindo algumas falhas no sistema de saudação.</span><span class="sxs-lookup"><span data-stu-id="8c54e-203">Validates hello availability and health of a Service Fabric service, usually after inducing some fault into hello system.</span></span> |<span data-ttu-id="8c54e-204">ValidateServiceAsync</span><span class="sxs-lookup"><span data-stu-id="8c54e-204">ValidateServiceAsync</span></span> |<span data-ttu-id="8c54e-205">Test-ServiceFabricService</span><span class="sxs-lookup"><span data-stu-id="8c54e-205">Test-ServiceFabricService</span></span> |<span data-ttu-id="8c54e-206">Não aplicável</span><span class="sxs-lookup"><span data-stu-id="8c54e-206">Not applicable</span></span> |

## <a name="running-a-testability-action-using-powershell"></a><span data-ttu-id="8c54e-207">Executando uma ação de possibilidade de teste usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c54e-207">Running a testability action using PowerShell</span></span>
<span data-ttu-id="8c54e-208">Este tutorial mostra como toorun uma ação de capacidade de teste usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8c54e-208">This tutorial shows you how toorun a testability action by using PowerShell.</span></span> <span data-ttu-id="8c54e-209">Você aprenderá como toorun uma ação de capacidade de teste em um cluster (caixa) local ou em um cluster do Azure.</span><span class="sxs-lookup"><span data-stu-id="8c54e-209">You will learn how toorun a testability action against a local (one-box) cluster or an Azure cluster.</span></span> <span data-ttu-id="8c54e-210">Microsoft.Fabric.Powershell.dll – hello módulo PowerShell do Service Fabric – é instalado automaticamente quando você instala o hello MSI do Microsoft Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8c54e-210">Microsoft.Fabric.Powershell.dll--hello Service Fabric PowerShell module--is installed automatically when you install hello Microsoft Service Fabric MSI.</span></span> <span data-ttu-id="8c54e-211">módulo Olá é carregado automaticamente quando você abrir um prompt do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8c54e-211">hello module is loaded automatically when you open a PowerShell prompt.</span></span>

<span data-ttu-id="8c54e-212">Segmentos do tutorial:</span><span class="sxs-lookup"><span data-stu-id="8c54e-212">Tutorial segments:</span></span>

* [<span data-ttu-id="8c54e-213">Executar uma ação em um cluster one-box</span><span class="sxs-lookup"><span data-stu-id="8c54e-213">Run an action against a one-box cluster</span></span>](#run-an-action-against-a-one-box-cluster)
* [<span data-ttu-id="8c54e-214">Executar uma ação em um cluster do Azure</span><span class="sxs-lookup"><span data-stu-id="8c54e-214">Run an action against an Azure cluster</span></span>](#run-an-action-against-an-azure-cluster)

### <a name="run-an-action-against-a-one-box-cluster"></a><span data-ttu-id="8c54e-215">Executar uma ação em um cluster one-box</span><span class="sxs-lookup"><span data-stu-id="8c54e-215">Run an action against a one-box cluster</span></span>
<span data-ttu-id="8c54e-216">toorun uma ação de capacidade de teste em um cluster local, conecte-se primeiro toohello cluster e o prompt do PowerShell Olá aberto no modo de administrador.</span><span class="sxs-lookup"><span data-stu-id="8c54e-216">toorun a testability action against a local cluster, first connect toohello cluster and open hello PowerShell prompt in administrator mode.</span></span> <span data-ttu-id="8c54e-217">Vamos dar uma olhada em Olá **ServiceFabricNode reinicialização** ação.</span><span class="sxs-lookup"><span data-stu-id="8c54e-217">Let us look at hello **Restart-ServiceFabricNode** action.</span></span>

```powershell
Restart-ServiceFabricNode -NodeName Node1 -CompletionMode DoNotVerify
```

<span data-ttu-id="8c54e-218">Olá aqui ação **ServiceFabricNode reinicialização** está sendo executado em um nó denominado "Node1".</span><span class="sxs-lookup"><span data-stu-id="8c54e-218">Here hello action **Restart-ServiceFabricNode** is being run on a node named "Node1".</span></span> <span data-ttu-id="8c54e-219">modo de conclusão de saudação especifica que ele não deve verificar se ação de reinicialização do nó Olá teve êxito realmente.</span><span class="sxs-lookup"><span data-stu-id="8c54e-219">hello completion mode specifies that it should not verify whether hello restart-node action actually succeeded.</span></span> <span data-ttu-id="8c54e-220">Modo de preenchimento Olá especificando como "Verificar" fará com que ele tooverify se a ação de reinicialização Olá foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="8c54e-220">Specifying hello completion mode as "Verify" will cause it tooverify whether hello restart action actually succeeded.</span></span> <span data-ttu-id="8c54e-221">Em vez de especificar diretamente o nó Olá por seu nome, você pode especificá-lo por meio de um tipo de chave e hello de partição da réplica, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="8c54e-221">Instead of directly specifying hello node by its name, you can specify it via a partition key and hello kind of replica, as follows:</span></span>

```powershell
Restart-ServiceFabricNode -ReplicaKindPrimary  -PartitionKindNamed -PartitionKey Partition3 -CompletionMode Verify
```


```powershell
$connection = "localhost:19000"
$nodeName = "Node1"

Connect-ServiceFabricCluster $connection
Restart-ServiceFabricNode -NodeName $nodeName -CompletionMode DoNotVerify
```

<span data-ttu-id="8c54e-222">**Reinicialização ServiceFabricNode** deve ser usado toorestart um nó de malha do serviço em um cluster.</span><span class="sxs-lookup"><span data-stu-id="8c54e-222">**Restart-ServiceFabricNode** should be used toorestart a Service Fabric node in a cluster.</span></span> <span data-ttu-id="8c54e-223">Isso interromperá o processo de Fabric.exe hello, que irá reiniciar todas Olá system service e o usuário serviço réplicas hospedadas naquele nó.</span><span class="sxs-lookup"><span data-stu-id="8c54e-223">This will stop hello Fabric.exe process, which will restart all of hello system service and user service replicas hosted on that node.</span></span> <span data-ttu-id="8c54e-224">Usando essa API tootest seu serviço ajuda a revelar bugs em caminhos de recuperação de failover de saudação.</span><span class="sxs-lookup"><span data-stu-id="8c54e-224">Using this API tootest your service helps uncover bugs along hello failover recovery paths.</span></span> <span data-ttu-id="8c54e-225">Ele ajuda a simular falhas de nó no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="8c54e-225">It helps simulate node failures in hello cluster.</span></span>

<span data-ttu-id="8c54e-226">Olá, seguinte captura de tela mostra Olá **ServiceFabricNode reinicialização** comando de capacidade de teste em ação.</span><span class="sxs-lookup"><span data-stu-id="8c54e-226">hello following screenshot shows hello **Restart-ServiceFabricNode** testability command in action.</span></span>

![](media/service-fabric-testability-actions/Restart-ServiceFabricNode.png)

<span data-ttu-id="8c54e-227">saudação de saída de hello primeiro **Get-ServiceFabricNode** (um cmdlet do módulo do PowerShell do Service Fabric Olá) mostra o cluster local Olá tem cinco nós: Node.1 tooNode.5.</span><span class="sxs-lookup"><span data-stu-id="8c54e-227">hello output of hello first **Get-ServiceFabricNode** (a cmdlet from hello Service Fabric PowerShell module) shows that hello local cluster has five nodes: Node.1 tooNode.5.</span></span> <span data-ttu-id="8c54e-228">Após a ação de capacidade de teste de saudação (cmdlet) **ServiceFabricNode reinicialização** é executado no nó hello, denominado Node.4, podemos ver tempo de atividade do nó Olá foi redefinido.</span><span class="sxs-lookup"><span data-stu-id="8c54e-228">After hello testability action (cmdlet) **Restart-ServiceFabricNode** is executed on hello node, named Node.4, we see that hello node's uptime has been reset.</span></span>

### <a name="run-an-action-against-an-azure-cluster"></a><span data-ttu-id="8c54e-229">Executar uma ação em um cluster do Azure</span><span class="sxs-lookup"><span data-stu-id="8c54e-229">Run an action against an Azure cluster</span></span>
<span data-ttu-id="8c54e-230">Executar uma ação de capacidade de teste (usando o PowerShell) em um cluster do Azure é a ação de saudação de toorunning semelhante em um cluster local.</span><span class="sxs-lookup"><span data-stu-id="8c54e-230">Running a testability action (by using PowerShell) against an Azure cluster is similar toorunning hello action against a local cluster.</span></span> <span data-ttu-id="8c54e-231">Olá somente a diferença é que, antes de executar a ação de hello, em vez de conectar toohello de cluster local, você precisa tooconnect toohello Azure cluster primeiro.</span><span class="sxs-lookup"><span data-stu-id="8c54e-231">hello only difference is that before you can run hello action, instead of connecting toohello local cluster, you need tooconnect toohello Azure cluster first.</span></span>

## <a name="running-a-testability-action-using-c35"></a><span data-ttu-id="8c54e-232">Executando uma ação de possibilidade de teste usando o C&#35;</span><span class="sxs-lookup"><span data-stu-id="8c54e-232">Running a testability action using C&#35;</span></span>
<span data-ttu-id="8c54e-233">toorun uma ação de capacidade de teste usando c#, primeiro é necessário tooconnect toohello cluster usando FabricClient.</span><span class="sxs-lookup"><span data-stu-id="8c54e-233">toorun a testability action by using C#, first you need tooconnect toohello cluster by using FabricClient.</span></span> <span data-ttu-id="8c54e-234">Em seguida, obter Olá parâmetros necessários toorun Olá ação.</span><span class="sxs-lookup"><span data-stu-id="8c54e-234">Then obtain hello parameters needed toorun hello action.</span></span> <span data-ttu-id="8c54e-235">Parâmetros diferentes podem ser usados toorun Olá a mesma ação.</span><span class="sxs-lookup"><span data-stu-id="8c54e-235">Different parameters can be used toorun hello same action.</span></span>
<span data-ttu-id="8c54e-236">Olhando Olá RestartServiceFabricNode ação, toorun unidirecional usando informações de nó da saudação (nome de nó e ID de instância do nó) no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="8c54e-236">Looking at hello RestartServiceFabricNode action, one way toorun it is by using hello node information (node name and node instance ID) in hello cluster.</span></span>

```csharp
RestartNodeAsync(nodeName, nodeInstanceId, completeMode, operationTimeout, CancellationToken.None)
```

<span data-ttu-id="8c54e-237">Explicação do parâmetro:</span><span class="sxs-lookup"><span data-stu-id="8c54e-237">Parameter explanation:</span></span>

* <span data-ttu-id="8c54e-238">**CompleteMode** Especifica que o modo de saudação não deve verificar se ação de reinicialização Olá teve êxito realmente.</span><span class="sxs-lookup"><span data-stu-id="8c54e-238">**CompleteMode** specifies that hello mode should not verify whether hello restart action actually succeeded.</span></span> <span data-ttu-id="8c54e-239">Modo de preenchimento Olá especificando como "Verificar" fará com que ele tooverify se a ação de reinicialização Olá foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="8c54e-239">Specifying hello completion mode as "Verify" will cause it tooverify whether hello restart action actually succeeded.</span></span>  
* <span data-ttu-id="8c54e-240">**OperationTimeout** conjuntos Olá quantidade de tempo da saudação operação toofinish antes de uma exceção TimeoutException é lançada.</span><span class="sxs-lookup"><span data-stu-id="8c54e-240">**OperationTimeout** sets hello amount of time for hello operation toofinish before a TimeoutException exception is thrown.</span></span>
* <span data-ttu-id="8c54e-241">**CancellationToken** permite que um toobe pendente chamada cancelada.</span><span class="sxs-lookup"><span data-stu-id="8c54e-241">**CancellationToken** enables a pending call toobe canceled.</span></span>

<span data-ttu-id="8c54e-242">Em vez de especificar diretamente o nó Olá por seu nome, você pode especificar isso por meio de um tipo de chave e hello de partição de réplica.</span><span class="sxs-lookup"><span data-stu-id="8c54e-242">Instead of directly specifying hello node by its name, you can specify it via a partition key and hello kind of replica.</span></span>

<span data-ttu-id="8c54e-243">Para obter mais informações, consulte [PartitionSelector e ReplicaSelector](#partition_replica_selector).</span><span class="sxs-lookup"><span data-stu-id="8c54e-243">For further information, see [PartitionSelector and ReplicaSelector](#partition_replica_selector).</span></span>

```csharp
// Add a reference tooSystem.Fabric.Testability.dll and System.Fabric.dll
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Fabric.Testability;
using System.Fabric;
using System.Threading;
using System.Numerics;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";
        Uri serviceName = new Uri("fabric:/samples/PersistentToDoListApp/PersistentToDoListService");
        string nodeName = "N0040";
        BigInteger nodeInstanceId = 130743013389060139;

        Console.WriteLine("Starting RestartNode test");
        try
        {
            //Restart hello node by using ReplicaSelector
            RestartNodeAsync(clusterConnection, serviceName).Wait();

            //Another way toorestart node is by using nodeName and nodeInstanceId
            RestartNodeAsync(clusterConnection, nodeName, nodeInstanceId).Wait();
        }
        catch (AggregateException exAgg)
        {
            Console.WriteLine("RestartNode did not complete: ");
            foreach (Exception ex in exAgg.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("RestartNode completed.");
        return 0;
    }

    static async Task RestartNodeAsync(string clusterConnection, Uri serviceName)
    {
        PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);
        ReplicaSelector primaryofReplicaSelector = ReplicaSelector.PrimaryOf(randomPartitionSelector);

        // Create FabricClient with connection and security information here
        FabricClient fabricclient = new FabricClient(clusterConnection);
        await fabricclient.FaultManager.RestartNodeAsync(primaryofReplicaSelector, CompletionMode.Verify);
    }

    static async Task RestartNodeAsync(string clusterConnection, string nodeName, BigInteger nodeInstanceId)
    {
        // Create FabricClient with connection and security information here
        FabricClient fabricclient = new FabricClient(clusterConnection);
        await fabricclient.FaultManager.RestartNodeAsync(nodeName, nodeInstanceId, CompletionMode.Verify);
    }
}
```

## <a name="partitionselector-and-replicaselector"></a><span data-ttu-id="8c54e-244">PartitionSelector e ReplicaSelector</span><span class="sxs-lookup"><span data-stu-id="8c54e-244">PartitionSelector and ReplicaSelector</span></span>
### <a name="partitionselector"></a><span data-ttu-id="8c54e-245">PartitionSelector</span><span class="sxs-lookup"><span data-stu-id="8c54e-245">PartitionSelector</span></span>
<span data-ttu-id="8c54e-246">PartitionSelector é um auxiliar exposto na capacidade de teste e é tooselect usado uma determinada partição no qual tooperform qualquer uma das ações de capacidade de teste de saudação.</span><span class="sxs-lookup"><span data-stu-id="8c54e-246">PartitionSelector is a helper exposed in testability and is used tooselect a specific partition on which tooperform any of hello testability actions.</span></span> <span data-ttu-id="8c54e-247">Pode ser usado tooselect uma partição específica se a ID de partição Olá é conhecido com antecedência.</span><span class="sxs-lookup"><span data-stu-id="8c54e-247">It can be used tooselect a specific partition if hello partition ID is known beforehand.</span></span> <span data-ttu-id="8c54e-248">Ou, você pode fornecer a chave de partição hello e operação Olá resolverá o ID de partição Olá internamente.</span><span class="sxs-lookup"><span data-stu-id="8c54e-248">Or, you can provide hello partition key and hello operation will resolve hello partition ID internally.</span></span> <span data-ttu-id="8c54e-249">Você também tem a opção de saudação do selecionando uma partição aleatória.</span><span class="sxs-lookup"><span data-stu-id="8c54e-249">You also have hello option of selecting a random partition.</span></span>

<span data-ttu-id="8c54e-250">toouse este auxiliar, criar hello PartitionSelector objeto e selecione partição hello usando um dos métodos de saudação Select *.</span><span class="sxs-lookup"><span data-stu-id="8c54e-250">toouse this helper, create hello PartitionSelector object and select hello partition by using one of hello Select* methods.</span></span> <span data-ttu-id="8c54e-251">Em seguida, passe Olá PartitionSelector objeto toohello API que exija isso.</span><span class="sxs-lookup"><span data-stu-id="8c54e-251">Then pass in hello PartitionSelector object toohello API that requires it.</span></span> <span data-ttu-id="8c54e-252">Se nenhuma opção for selecionada, será padronizado partição aleatória tooa.</span><span class="sxs-lookup"><span data-stu-id="8c54e-252">If no option is selected, it defaults tooa random partition.</span></span>

```csharp
Uri serviceName = new Uri("fabric:/samples/InMemoryToDoListApp/InMemoryToDoListService");
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
string partitionName = "Partition1";
Int64 partitionKeyUniformInt64 = 1;

// Select a random partition
PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);

// Select a partition based on ID
PartitionSelector partitionSelectorById = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);

// Select a partition based on name
PartitionSelector namedPartitionSelector = PartitionSelector.PartitionKeyOf(serviceName, partitionName);

// Select a partition based on partition key
PartitionSelector uniformIntPartitionSelector = PartitionSelector.PartitionKeyOf(serviceName, partitionKeyUniformInt64);
```

### <a name="replicaselector"></a><span data-ttu-id="8c54e-253">ReplicaSelector</span><span class="sxs-lookup"><span data-stu-id="8c54e-253">ReplicaSelector</span></span>
<span data-ttu-id="8c54e-254">ReplicaSelector é um auxiliar exposto na capacidade de teste e é usado toohelp selecione uma réplica na qual tooperform qualquer uma das ações de capacidade de teste de saudação.</span><span class="sxs-lookup"><span data-stu-id="8c54e-254">ReplicaSelector is a helper exposed in testability and is used toohelp select a replica on which tooperform any of hello testability actions.</span></span> <span data-ttu-id="8c54e-255">Pode ser usado tooselect uma réplica específica se a ID da réplica Olá é conhecido com antecedência.</span><span class="sxs-lookup"><span data-stu-id="8c54e-255">It can be used tooselect a specific replica if hello replica ID is known beforehand.</span></span> <span data-ttu-id="8c54e-256">Além disso, você tem opção de saudação da seleção de uma réplica primária ou um secundário aleatório.</span><span class="sxs-lookup"><span data-stu-id="8c54e-256">In addition, you have hello option of selecting a primary replica or a random secondary.</span></span> <span data-ttu-id="8c54e-257">ReplicaSelector deriva PartitionSelector, portanto, você precisa tooselect ambos Olá hello e réplica de partição no qual você deseja tooperform operação de capacidade de teste de saudação.</span><span class="sxs-lookup"><span data-stu-id="8c54e-257">ReplicaSelector derives from PartitionSelector, so you need tooselect both hello replica and hello partition on which you wish tooperform hello testability operation.</span></span>

<span data-ttu-id="8c54e-258">toouse este auxiliar, crie um objeto de ReplicaSelector e definido como Olá desejar partição de réplica e Olá Olá tooselect.</span><span class="sxs-lookup"><span data-stu-id="8c54e-258">toouse this helper, create a ReplicaSelector object and set hello way you want tooselect hello replica and hello partition.</span></span> <span data-ttu-id="8c54e-259">Você pode passá-lo em Olá API que exija isso.</span><span class="sxs-lookup"><span data-stu-id="8c54e-259">You can then pass it into hello API that requires it.</span></span> <span data-ttu-id="8c54e-260">Se nenhuma opção for selecionada, o padrão é réplica aleatório tooa e partição aleatória.</span><span class="sxs-lookup"><span data-stu-id="8c54e-260">If no option is selected, it defaults tooa random replica and random partition.</span></span>

```csharp
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);
long replicaId = 130559876481875498;

// Select a random replica
ReplicaSelector randomReplicaSelector = ReplicaSelector.RandomOf(partitionSelector);

// Select hello primary replica
ReplicaSelector primaryReplicaSelector = ReplicaSelector.PrimaryOf(partitionSelector);

// Select hello replica by ID
ReplicaSelector replicaByIdSelector = ReplicaSelector.ReplicaIdOf(partitionSelector, replicaId);

// Select a random secondary replica
ReplicaSelector secondaryReplicaSelector = ReplicaSelector.RandomSecondaryOf(partitionSelector);
```

## <a name="next-steps"></a><span data-ttu-id="8c54e-261">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8c54e-261">Next steps</span></span>
* [<span data-ttu-id="8c54e-262">Cenários da possibilidade de teste</span><span class="sxs-lookup"><span data-stu-id="8c54e-262">Testability scenarios</span></span>](service-fabric-testability-scenarios.md)
* <span data-ttu-id="8c54e-263">Como tootest seu serviço</span><span class="sxs-lookup"><span data-stu-id="8c54e-263">How tootest your service</span></span>
  * [<span data-ttu-id="8c54e-264">Simular falhas durante cargas de trabalho de serviço</span><span class="sxs-lookup"><span data-stu-id="8c54e-264">Simulate failures during service workloads</span></span>](service-fabric-testability-workload-tests.md)
  * [<span data-ttu-id="8c54e-265">Falhas de comunicação entre serviços</span><span class="sxs-lookup"><span data-stu-id="8c54e-265">Service-to-service communication failures</span></span>](service-fabric-testability-scenarios-service-communication.md)

