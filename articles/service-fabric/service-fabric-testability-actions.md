---
title: "Simular falhas nos microsserviços do Azure | Microsoft Docs"
description: "Este artigo fala sobre as ações da Possibilidade de Teste encontradas na Malha de Serviço do Microsoft Azure."
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
ms.openlocfilehash: c8ddc7732999ae555323bebaef60aa34c8f2ec17
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="testability-actions"></a><span data-ttu-id="4e4dc-103">Ações da Possibilidade de Teste</span><span class="sxs-lookup"><span data-stu-id="4e4dc-103">Testability actions</span></span>
<span data-ttu-id="4e4dc-104">Para simular uma infraestrutura não confiável, o Service Fabric do Azure fornece a você, o desenvolvedor, maneiras de simular várias falhas e transições de estado reais.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-104">In order to simulate an unreliable infrastructure, Azure Service Fabric provides you, the developer, with ways to simulate various real-world failures and state transitions.</span></span> <span data-ttu-id="4e4dc-105">Elas são expostas como ações de possibilidade de teste.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-105">These are exposed as testability actions.</span></span> <span data-ttu-id="4e4dc-106">As ações são as APIs de nível baixo que causam uma injeção de falha específica, transição de estado ou validação.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-106">The actions are the low-level APIs that cause a specific fault injection, state transition, or validation.</span></span> <span data-ttu-id="4e4dc-107">Ao combinar essas ações, você pode criar cenários de teste abrangentes para seus serviços.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-107">By combining these actions, you can write comprehensive test scenarios for your services.</span></span>

<span data-ttu-id="4e4dc-108">O Service Fabric fornece alguns cenários comuns de teste compostos por essas ações.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-108">Service Fabric provides some common test scenarios composed of these actions.</span></span> <span data-ttu-id="4e4dc-109">É altamente recomendável utilizar esses cenários internos, que são escolhidos cuidadosamente para testar transições de estado comuns e casos de falha.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-109">We highly recommend that you utilize these built-in scenarios, which are carefully chosen to test common state transitions and failure cases.</span></span> <span data-ttu-id="4e4dc-110">No entanto, as ações podem ser usadas para criar cenários de teste personalizados quando você desejar adicionar cobertura para cenários que ainda não estão cobertos pelos cenários internos ou personalizados sob medida para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-110">However, actions can be used to create custom test scenarios when you want to add coverage for scenarios that are not covered by the built-in scenarios yet or that are custom tailored for your application.</span></span>

<span data-ttu-id="4e4dc-111">As implementações das ações em C# são encontradas no assembly System.Fabric.dll.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-111">C# implementations of the actions are found in the System.Fabric.dll assembly.</span></span> <span data-ttu-id="4e4dc-112">O módulo Service Fabric PowerShell é encontrado no assembly Microsoft.ServiceFabric.Powershell.dll.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-112">The System Fabric PowerShell module is found in the Microsoft.ServiceFabric.Powershell.dll assembly.</span></span> <span data-ttu-id="4e4dc-113">Como parte da instalação em tempo de execução, o módulo do PowerShell ServiceFabric é instalado para fins de facilidade de uso.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-113">As part of runtime installation, the ServiceFabric PowerShell module is installed to allow for ease of use.</span></span>

## <a name="graceful-vs-ungraceful-fault-actions"></a><span data-ttu-id="4e4dc-114">Ações de falha normais x anormais</span><span class="sxs-lookup"><span data-stu-id="4e4dc-114">Graceful vs. ungraceful fault actions</span></span>
<span data-ttu-id="4e4dc-115">As ações da Possibilidade de Teste são classificadas em dois blocos principais:</span><span class="sxs-lookup"><span data-stu-id="4e4dc-115">Testability actions are classified into two major buckets:</span></span>

* <span data-ttu-id="4e4dc-116">Falhas anormais: simulam falhas como reinicializações de máquina e panes de processo.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-116">Ungraceful faults: These faults simulate failures like machine restarts and process crashes.</span></span> <span data-ttu-id="4e4dc-117">No caso dessas falhas, o contexto de execução do processo é interrompido abruptamente.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-117">In such cases of failures, the execution context of process stops abruptly.</span></span> <span data-ttu-id="4e4dc-118">Isso significa que nenhuma limpeza de estado pode ser executada antes de o aplicativo ser iniciado novamente.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-118">This means no cleanup of the state can run before the application starts up again.</span></span>
* <span data-ttu-id="4e4dc-119">Falhas normais: simulam ações normais como movimentações de réplica e remoções acionadas pelo balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-119">Graceful faults: These faults simulate graceful actions like replica moves and drops triggered by load balancing.</span></span> <span data-ttu-id="4e4dc-120">Nesses casos, o serviço recebe uma notificação de fechamento e pode limpar o estado antes de sair.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-120">In such cases, the service gets a notification of the close and can clean up the state before exiting.</span></span>

<span data-ttu-id="4e4dc-121">Para validação de melhor qualidade, execute a carga de trabalho de serviço e comercial enquanto estiver induzindo várias falhas normais e anormais.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-121">For better quality validation, run the service and business workload while inducing various graceful and ungraceful faults.</span></span> <span data-ttu-id="4e4dc-122">Falhas anormais utilizam cenários em que o processo de serviço é interrompido abruptamente no meio de algum fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-122">Ungraceful faults exercise scenarios where the service process abruptly exits in the middle of some workflow.</span></span> <span data-ttu-id="4e4dc-123">Isso testa o caminho de recuperação assim que a réplica do serviço é restaurada pelo Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-123">This tests  the recovery path once the service replica is restored by Service Fabric.</span></span> <span data-ttu-id="4e4dc-124">Isso ajudará na consistência dos dados de teste e a verificar se o estado do serviço é mantido corretamente após as falhas.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-124">This will help test data consistency and whether the service state is maintained correctly after failures.</span></span> <span data-ttu-id="4e4dc-125">O outro conjunto de falhas (falhas normais) testa se o serviço reage corretamente à movimentação das réplicas pelo Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-125">The other set of failures (the graceful failures) test that the service correctly reacts to replicas being moved around by Service Fabric.</span></span> <span data-ttu-id="4e4dc-126">Isso testa o tratamento de cancelamento no método RunAsync.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-126">This tests handling of cancellation in the RunAsync method.</span></span> <span data-ttu-id="4e4dc-127">O serviço precisa verificar se o token de cancelamento que está sendo definido salva seu estado e encerra o método RunAsync corretamente.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-127">The service needs to check for the cancellation token being set, correctly save its state, and exit the RunAsync method.</span></span>

## <a name="testability-actions-list"></a><span data-ttu-id="4e4dc-128">Lista de ações da Possibilidade de Teste</span><span class="sxs-lookup"><span data-stu-id="4e4dc-128">Testability actions list</span></span>
| <span data-ttu-id="4e4dc-129">Ação</span><span class="sxs-lookup"><span data-stu-id="4e4dc-129">Action</span></span> | <span data-ttu-id="4e4dc-130">Descrição</span><span class="sxs-lookup"><span data-stu-id="4e4dc-130">Description</span></span> | <span data-ttu-id="4e4dc-131">API gerenciada</span><span class="sxs-lookup"><span data-stu-id="4e4dc-131">Managed API</span></span> | <span data-ttu-id="4e4dc-132">Cmdlet do Powershell</span><span class="sxs-lookup"><span data-stu-id="4e4dc-132">PowerShell cmdlet</span></span> | <span data-ttu-id="4e4dc-133">Falhas normais/anormais</span><span class="sxs-lookup"><span data-stu-id="4e4dc-133">Graceful/ungraceful faults</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="4e4dc-134">CleanTestState</span><span class="sxs-lookup"><span data-stu-id="4e4dc-134">CleanTestState</span></span> |<span data-ttu-id="4e4dc-135">Remove todo o estado de teste do cluster em caso de desligamento repentino do driver de teste.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-135">Removes all the test state from the cluster in case of a bad shutdown of the test driver.</span></span> |<span data-ttu-id="4e4dc-136">CleanTestStateAsync</span><span class="sxs-lookup"><span data-stu-id="4e4dc-136">CleanTestStateAsync</span></span> |<span data-ttu-id="4e4dc-137">Remove-ServiceFabricTestState</span><span class="sxs-lookup"><span data-stu-id="4e4dc-137">Remove-ServiceFabricTestState</span></span> |<span data-ttu-id="4e4dc-138">Não aplicável</span><span class="sxs-lookup"><span data-stu-id="4e4dc-138">Not applicable</span></span> |
| <span data-ttu-id="4e4dc-139">InvokeDataLoss</span><span class="sxs-lookup"><span data-stu-id="4e4dc-139">InvokeDataLoss</span></span> |<span data-ttu-id="4e4dc-140">Induz a perda de dados em uma partição de serviço.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-140">Induces data loss into a service partition.</span></span> |<span data-ttu-id="4e4dc-141">InvokeDataLossAsync</span><span class="sxs-lookup"><span data-stu-id="4e4dc-141">InvokeDataLossAsync</span></span> |<span data-ttu-id="4e4dc-142">Invoke-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="4e4dc-142">Invoke-ServiceFabricPartitionDataLoss</span></span> |<span data-ttu-id="4e4dc-143">Normal</span><span class="sxs-lookup"><span data-stu-id="4e4dc-143">Graceful</span></span> |
| <span data-ttu-id="4e4dc-144">InvokeQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="4e4dc-144">InvokeQuorumLoss</span></span> |<span data-ttu-id="4e4dc-145">Coloca uma determinada partição de serviço com estado na perda de quórum.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-145">Puts a given stateful service partition into quorum loss.</span></span> |<span data-ttu-id="4e4dc-146">InvokeQuorumLossAsync</span><span class="sxs-lookup"><span data-stu-id="4e4dc-146">InvokeQuorumLossAsync</span></span> |<span data-ttu-id="4e4dc-147">Invoke-ServiceFabricQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="4e4dc-147">Invoke-ServiceFabricQuorumLoss</span></span> |<span data-ttu-id="4e4dc-148">Normal</span><span class="sxs-lookup"><span data-stu-id="4e4dc-148">Graceful</span></span> |
| <span data-ttu-id="4e4dc-149">Mover primária</span><span class="sxs-lookup"><span data-stu-id="4e4dc-149">Move Primary</span></span> |<span data-ttu-id="4e4dc-150">Move a réplica primária especificada do serviço com estado para o nó de cluster especificado.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-150">Moves the specified primary replica of a stateful service to the specified cluster node.</span></span> |<span data-ttu-id="4e4dc-151">MovePrimaryAsync</span><span class="sxs-lookup"><span data-stu-id="4e4dc-151">MovePrimaryAsync</span></span> |<span data-ttu-id="4e4dc-152">Move-ServiceFabricPrimaryReplica</span><span class="sxs-lookup"><span data-stu-id="4e4dc-152">Move-ServiceFabricPrimaryReplica</span></span> |<span data-ttu-id="4e4dc-153">Normal</span><span class="sxs-lookup"><span data-stu-id="4e4dc-153">Graceful</span></span> |
| <span data-ttu-id="4e4dc-154">Mover secundária</span><span class="sxs-lookup"><span data-stu-id="4e4dc-154">Move Secondary</span></span> |<span data-ttu-id="4e4dc-155">Move a réplica secundária atual de um serviço com  estado para outro nó de cluster.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-155">Moves the current secondary replica of a stateful service to a different cluster node.</span></span> |<span data-ttu-id="4e4dc-156">MoveSecondaryAsync</span><span class="sxs-lookup"><span data-stu-id="4e4dc-156">MoveSecondaryAsync</span></span> |<span data-ttu-id="4e4dc-157">Move-ServiceFabricSecondaryReplica</span><span class="sxs-lookup"><span data-stu-id="4e4dc-157">Move-ServiceFabricSecondaryReplica</span></span> |<span data-ttu-id="4e4dc-158">Normal</span><span class="sxs-lookup"><span data-stu-id="4e4dc-158">Graceful</span></span> |
| <span data-ttu-id="4e4dc-159">RemoveReplica</span><span class="sxs-lookup"><span data-stu-id="4e4dc-159">RemoveReplica</span></span> |<span data-ttu-id="4e4dc-160">Simula uma falha de réplica removendo uma réplica de um cluster.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-160">Simulates a replica failure by removing a replica from a cluster.</span></span> <span data-ttu-id="4e4dc-161">Isso fecha a réplica e faz a transição dela para a função “Nenhum”, removendo todo o seu estado do cluster.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-161">This will close the replica and will transition it to role 'None', removing all of its state from the cluster.</span></span> |<span data-ttu-id="4e4dc-162">RemoveReplicaAsync</span><span class="sxs-lookup"><span data-stu-id="4e4dc-162">RemoveReplicaAsync</span></span> |<span data-ttu-id="4e4dc-163">Remove-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="4e4dc-163">Remove-ServiceFabricReplica</span></span> |<span data-ttu-id="4e4dc-164">Normal</span><span class="sxs-lookup"><span data-stu-id="4e4dc-164">Graceful</span></span> |
| <span data-ttu-id="4e4dc-165">RestartDeployedCodePackage</span><span class="sxs-lookup"><span data-stu-id="4e4dc-165">RestartDeployedCodePackage</span></span> |<span data-ttu-id="4e4dc-166">Simula uma falha de processo do pacote de códigos reiniciando um pacote de códigos implantado em um nó em um cluster.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-166">Simulates a code package process failure by restarting a code package deployed on a node in a cluster.</span></span> <span data-ttu-id="4e4dc-167">Isso anula o processo do pacote de códigos, o que reiniciará todas as réplicas de serviço do usuário hospedadas nesse processo.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-167">This aborts the code package process, which will restart all the user service replicas hosted in that process.</span></span> |<span data-ttu-id="4e4dc-168">RestartDeployedCodePackageAsync</span><span class="sxs-lookup"><span data-stu-id="4e4dc-168">RestartDeployedCodePackageAsync</span></span> |<span data-ttu-id="4e4dc-169">Restart-ServiceFabricDeployedCodePackage</span><span class="sxs-lookup"><span data-stu-id="4e4dc-169">Restart-ServiceFabricDeployedCodePackage</span></span> |<span data-ttu-id="4e4dc-170">Anormais</span><span class="sxs-lookup"><span data-stu-id="4e4dc-170">Ungraceful</span></span> |
| <span data-ttu-id="4e4dc-171">RestartNode</span><span class="sxs-lookup"><span data-stu-id="4e4dc-171">RestartNode</span></span> |<span data-ttu-id="4e4dc-172">Simula uma falha de nó de cluster da Malha de Serviço reinicializando um nó.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-172">Simulates a Service Fabric cluster node failure by restarting a node.</span></span> |<span data-ttu-id="4e4dc-173">RestartNodeAsync</span><span class="sxs-lookup"><span data-stu-id="4e4dc-173">RestartNodeAsync</span></span> |<span data-ttu-id="4e4dc-174">Restart-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="4e4dc-174">Restart-ServiceFabricNode</span></span> |<span data-ttu-id="4e4dc-175">Anormais</span><span class="sxs-lookup"><span data-stu-id="4e4dc-175">Ungraceful</span></span> |
| <span data-ttu-id="4e4dc-176">RestartPartition</span><span class="sxs-lookup"><span data-stu-id="4e4dc-176">RestartPartition</span></span> |<span data-ttu-id="4e4dc-177">Simula um cenário de blecaute do datacenter ou cluster reiniciando algumas ou todas as réplicas de uma partição.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-177">Simulates a datacenter blackout or cluster blackout scenario by restarting some or all replicas of a partition.</span></span> |<span data-ttu-id="4e4dc-178">RestartPartitionAsync</span><span class="sxs-lookup"><span data-stu-id="4e4dc-178">RestartPartitionAsync</span></span> |<span data-ttu-id="4e4dc-179">Restart-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="4e4dc-179">Restart-ServiceFabricPartition</span></span> |<span data-ttu-id="4e4dc-180">Normal</span><span class="sxs-lookup"><span data-stu-id="4e4dc-180">Graceful</span></span> |
| <span data-ttu-id="4e4dc-181">RestartReplica</span><span class="sxs-lookup"><span data-stu-id="4e4dc-181">RestartReplica</span></span> |<span data-ttu-id="4e4dc-182">Simula uma falha de réplica reiniciando uma réplica persistente em um cluster, fechando a réplica e reabrindo-a.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-182">Simulates a replica failure by restarting a persisted replica in a cluster, closing the replica and then reopening it.</span></span> |<span data-ttu-id="4e4dc-183">RestartReplicaAsync</span><span class="sxs-lookup"><span data-stu-id="4e4dc-183">RestartReplicaAsync</span></span> |<span data-ttu-id="4e4dc-184">Restart-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="4e4dc-184">Restart-ServiceFabricReplica</span></span> |<span data-ttu-id="4e4dc-185">Normal</span><span class="sxs-lookup"><span data-stu-id="4e4dc-185">Graceful</span></span> |
| <span data-ttu-id="4e4dc-186">StartNode</span><span class="sxs-lookup"><span data-stu-id="4e4dc-186">StartNode</span></span> |<span data-ttu-id="4e4dc-187">Inicia um nó em um cluster que já foi interrompido.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-187">Starts a node in a cluster that is already stopped.</span></span> |<span data-ttu-id="4e4dc-188">StartNodeAsync</span><span class="sxs-lookup"><span data-stu-id="4e4dc-188">StartNodeAsync</span></span> |<span data-ttu-id="4e4dc-189">Start-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="4e4dc-189">Start-ServiceFabricNode</span></span> |<span data-ttu-id="4e4dc-190">Não aplicável</span><span class="sxs-lookup"><span data-stu-id="4e4dc-190">Not applicable</span></span> |
| <span data-ttu-id="4e4dc-191">StopNode</span><span class="sxs-lookup"><span data-stu-id="4e4dc-191">StopNode</span></span> |<span data-ttu-id="4e4dc-192">Simula uma falha de nó interrompendo um nó em um cluster.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-192">Simulates a node failure by stopping a node in a cluster.</span></span> <span data-ttu-id="4e4dc-193">O nó permanecerá inativo até que StartNode seja chamado.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-193">The node will stay down until StartNode is called.</span></span> |<span data-ttu-id="4e4dc-194">StopNodeAsync</span><span class="sxs-lookup"><span data-stu-id="4e4dc-194">StopNodeAsync</span></span> |<span data-ttu-id="4e4dc-195">Stop-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="4e4dc-195">Stop-ServiceFabricNode</span></span> |<span data-ttu-id="4e4dc-196">Anormais</span><span class="sxs-lookup"><span data-stu-id="4e4dc-196">Ungraceful</span></span> |
| <span data-ttu-id="4e4dc-197">ValidateApplication</span><span class="sxs-lookup"><span data-stu-id="4e4dc-197">ValidateApplication</span></span> |<span data-ttu-id="4e4dc-198">Valida a disponibilidade e a integridade de todos os serviços da Malha de Serviço em um aplicativo, geralmente depois de induzir alguma falha no sistema.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-198">Validates the availability and health of all Service Fabric services within an application, usually after inducing some fault into the system.</span></span> |<span data-ttu-id="4e4dc-199">ValidateApplicationAsync</span><span class="sxs-lookup"><span data-stu-id="4e4dc-199">ValidateApplicationAsync</span></span> |<span data-ttu-id="4e4dc-200">Test-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="4e4dc-200">Test-ServiceFabricApplication</span></span> |<span data-ttu-id="4e4dc-201">Não aplicável</span><span class="sxs-lookup"><span data-stu-id="4e4dc-201">Not applicable</span></span> |
| <span data-ttu-id="4e4dc-202">ValidateService</span><span class="sxs-lookup"><span data-stu-id="4e4dc-202">ValidateService</span></span> |<span data-ttu-id="4e4dc-203">Valida a disponibilidade e a integridade de um serviço da Malha de Serviço, geralmente depois de induzir alguma falha no sistema.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-203">Validates the availability and health of a Service Fabric service, usually after inducing some fault into the system.</span></span> |<span data-ttu-id="4e4dc-204">ValidateServiceAsync</span><span class="sxs-lookup"><span data-stu-id="4e4dc-204">ValidateServiceAsync</span></span> |<span data-ttu-id="4e4dc-205">Test-ServiceFabricService</span><span class="sxs-lookup"><span data-stu-id="4e4dc-205">Test-ServiceFabricService</span></span> |<span data-ttu-id="4e4dc-206">Não aplicável</span><span class="sxs-lookup"><span data-stu-id="4e4dc-206">Not applicable</span></span> |

## <a name="running-a-testability-action-using-powershell"></a><span data-ttu-id="4e4dc-207">Executando uma ação de possibilidade de teste usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e4dc-207">Running a testability action using PowerShell</span></span>
<span data-ttu-id="4e4dc-208">Este tutorial mostra como executar uma ação de possibilidade de teste com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-208">This tutorial shows you how to run a testability action by using PowerShell.</span></span> <span data-ttu-id="4e4dc-209">Você aprenderá a executar uma ação da possibilidade de teste em um cluster local (one-box) ou em um cluster do Azure.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-209">You will learn how to run a testability action against a local (one-box) cluster or an Azure cluster.</span></span> <span data-ttu-id="4e4dc-210">Microsoft.Fabric.Powershell.dll – o módulo Service Fabric PowerShell – é instalado automaticamente quando você instala o Microsoft Service Fabric MSI.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-210">Microsoft.Fabric.Powershell.dll--the Service Fabric PowerShell module--is installed automatically when you install the Microsoft Service Fabric MSI.</span></span> <span data-ttu-id="4e4dc-211">O módulo é carregado automaticamente quando você abre um prompt do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-211">The module is loaded automatically when you open a PowerShell prompt.</span></span>

<span data-ttu-id="4e4dc-212">Segmentos do tutorial:</span><span class="sxs-lookup"><span data-stu-id="4e4dc-212">Tutorial segments:</span></span>

* [<span data-ttu-id="4e4dc-213">Executar uma ação em um cluster one-box</span><span class="sxs-lookup"><span data-stu-id="4e4dc-213">Run an action against a one-box cluster</span></span>](#run-an-action-against-a-one-box-cluster)
* [<span data-ttu-id="4e4dc-214">Executar uma ação em um cluster do Azure</span><span class="sxs-lookup"><span data-stu-id="4e4dc-214">Run an action against an Azure cluster</span></span>](#run-an-action-against-an-azure-cluster)

### <a name="run-an-action-against-a-one-box-cluster"></a><span data-ttu-id="4e4dc-215">Executar uma ação em um cluster one-box</span><span class="sxs-lookup"><span data-stu-id="4e4dc-215">Run an action against a one-box cluster</span></span>
<span data-ttu-id="4e4dc-216">Para executar uma ação da Possibilidade Teste em um cluster local, primeiramente, conecte-se ao cluster e abra o prompt do PowerShell no modo de administrador.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-216">To run a testability action against a local cluster, first connect to the cluster and open the PowerShell prompt in administrator mode.</span></span> <span data-ttu-id="4e4dc-217">Vejamos a ação **Restart-ServiceFabricNode** .</span><span class="sxs-lookup"><span data-stu-id="4e4dc-217">Let us look at the **Restart-ServiceFabricNode** action.</span></span>

```powershell
Restart-ServiceFabricNode -NodeName Node1 -CompletionMode DoNotVerify
```

<span data-ttu-id="4e4dc-218">Aqui, a ação **Restart-ServiceFabricNode** está sendo executada em um nó chamado "Node1".</span><span class="sxs-lookup"><span data-stu-id="4e4dc-218">Here the action **Restart-ServiceFabricNode** is being run on a node named "Node1".</span></span> <span data-ttu-id="4e4dc-219">O modo de preenchimento especifica que ela não deve verificar se a ação de reinicialização do nó foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-219">The completion mode specifies that it should not verify whether the restart-node action actually succeeded.</span></span> <span data-ttu-id="4e4dc-220">Especificar o modo de preenchimento como "Verify" fará com que ele verifique se a ação de reinicialização foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-220">Specifying the completion mode as "Verify" will cause it to verify whether the restart action actually succeeded.</span></span> <span data-ttu-id="4e4dc-221">Em vez de especificar o nó diretamente por seu nome, você pode especificá-lo por meio de uma chave de partição e pelo tipo de réplica, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="4e4dc-221">Instead of directly specifying the node by its name, you can specify it via a partition key and the kind of replica, as follows:</span></span>

```powershell
Restart-ServiceFabricNode -ReplicaKindPrimary  -PartitionKindNamed -PartitionKey Partition3 -CompletionMode Verify
```


```powershell
$connection = "localhost:19000"
$nodeName = "Node1"

Connect-ServiceFabricCluster $connection
Restart-ServiceFabricNode -NodeName $nodeName -CompletionMode DoNotVerify
```

<span data-ttu-id="4e4dc-222">**Restart-ServiceFabricNode** deve ser usada para reiniciar um nó da Malha de Serviço em um cluster.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-222">**Restart-ServiceFabricNode** should be used to restart a Service Fabric node in a cluster.</span></span> <span data-ttu-id="4e4dc-223">Isso encerrará o processo Fabric.exe, que reiniciará todo o serviço do sistema e as réplicas de serviço do usuário hospedadas nesse nó.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-223">This will stop the Fabric.exe process, which will restart all of the system service and user service replicas hosted on that node.</span></span> <span data-ttu-id="4e4dc-224">Usar essa API para testar seu serviço ajuda a descobrir bugs ao longo dos caminhos de recuperação de failover.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-224">Using this API to test your service helps uncover bugs along the failover recovery paths.</span></span> <span data-ttu-id="4e4dc-225">Ela ajuda a simular falhas de nó no cluster.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-225">It helps simulate node failures in the cluster.</span></span>

<span data-ttu-id="4e4dc-226">A captura de tela a seguir mostra o comando **Restart-ServiceFabricNode** da possibilidade de teste em ação.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-226">The following screenshot shows the **Restart-ServiceFabricNode** testability command in action.</span></span>

![](media/service-fabric-testability-actions/Restart-ServiceFabricNode.png)

<span data-ttu-id="4e4dc-227">A saída do primeiro **Get-ServiceFabricNode** (um cmdlet do módulo do PowerShell do Service Fabric) mostra que o cluster local tem cinco nós: Node.1 para Node.5.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-227">The output of the first **Get-ServiceFabricNode** (a cmdlet from the Service Fabric PowerShell module) shows that the local cluster has five nodes: Node.1 to Node.5.</span></span> <span data-ttu-id="4e4dc-228">Depois que a ação da possibilidade de teste (cmdlet) **Restart-ServiceFabricNode** for executada no nó, denominado Node.4, poderemos ver o tempo de atividade do nó redefinido.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-228">After the testability action (cmdlet) **Restart-ServiceFabricNode** is executed on the node, named Node.4, we see that the node's uptime has been reset.</span></span>

### <a name="run-an-action-against-an-azure-cluster"></a><span data-ttu-id="4e4dc-229">Executar uma ação em um cluster do Azure</span><span class="sxs-lookup"><span data-stu-id="4e4dc-229">Run an action against an Azure cluster</span></span>
<span data-ttu-id="4e4dc-230">Executar uma ação da possibilidade de teste (usando o PowerShell) em um cluster do Azure é semelhante ao executar a ação em um cluster local.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-230">Running a testability action (by using PowerShell) against an Azure cluster is similar to running the action against a local cluster.</span></span> <span data-ttu-id="4e4dc-231">A única diferença é que, antes de executar a ação, em vez de conectar-se ao cluster local, você precisa se conectar ao cluster do Azure pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-231">The only difference is that before you can run the action, instead of connecting to the local cluster, you need to connect to the Azure cluster first.</span></span>

## <a name="running-a-testability-action-using-c35"></a><span data-ttu-id="4e4dc-232">Executando uma ação de possibilidade de teste usando o C&#35;</span><span class="sxs-lookup"><span data-stu-id="4e4dc-232">Running a testability action using C&#35;</span></span>
<span data-ttu-id="4e4dc-233">Para executar uma ação da possibilidade de teste usando C#, você precisa se conectar ao cluster usando o FabricClient.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-233">To run a testability action by using C#, first you need to connect to the cluster by using FabricClient.</span></span> <span data-ttu-id="4e4dc-234">Em seguida, obtenha os parâmetros necessários para executar a ação.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-234">Then obtain the parameters needed to run the action.</span></span> <span data-ttu-id="4e4dc-235">Parâmetros diferentes podem ser usados para executar a mesma ação.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-235">Different parameters can be used to run the same action.</span></span>
<span data-ttu-id="4e4dc-236">Uma maneira de executar a ação RestartServiceFabricNode é usando as informações do nó (nome do nó e id da instância do nó) no cluster.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-236">Looking at the RestartServiceFabricNode action, one way to run it is by using the node information (node name and node instance ID) in the cluster.</span></span>

```csharp
RestartNodeAsync(nodeName, nodeInstanceId, completeMode, operationTimeout, CancellationToken.None)
```

<span data-ttu-id="4e4dc-237">Explicação do parâmetro:</span><span class="sxs-lookup"><span data-stu-id="4e4dc-237">Parameter explanation:</span></span>

* <span data-ttu-id="4e4dc-238">**CompleteMode** especifica que o modo não deve verificar se a ação de reinicialização de fato foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-238">**CompleteMode** specifies that the mode should not verify whether the restart action actually succeeded.</span></span> <span data-ttu-id="4e4dc-239">Especificar o modo de preenchimento como "Verify" fará com que ele verifique se a ação de reinicialização foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-239">Specifying the completion mode as "Verify" will cause it to verify whether the restart action actually succeeded.</span></span>  
* <span data-ttu-id="4e4dc-240">**OperationTimeout** define a quantidade de tempo para conclusão da operação antes que uma exceção TimeoutException seja lançada.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-240">**OperationTimeout** sets the amount of time for the operation to finish before a TimeoutException exception is thrown.</span></span>
* <span data-ttu-id="4e4dc-241">**CancellationToken** permite que uma chamada pendente seja cancelada.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-241">**CancellationToken** enables a pending call to be canceled.</span></span>

<span data-ttu-id="4e4dc-242">Em vez de especificar o nó diretamente por seu nome, você pode especificá-lo por meio de uma chave de partição e pelo tipo de réplica.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-242">Instead of directly specifying the node by its name, you can specify it via a partition key and the kind of replica.</span></span>

<span data-ttu-id="4e4dc-243">Para obter mais informações, consulte [PartitionSelector e ReplicaSelector](#partition_replica_selector).</span><span class="sxs-lookup"><span data-stu-id="4e4dc-243">For further information, see [PartitionSelector and ReplicaSelector](#partition_replica_selector).</span></span>

```csharp
// Add a reference to System.Fabric.Testability.dll and System.Fabric.dll
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
            //Restart the node by using ReplicaSelector
            RestartNodeAsync(clusterConnection, serviceName).Wait();

            //Another way to restart node is by using nodeName and nodeInstanceId
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

## <a name="partitionselector-and-replicaselector"></a><span data-ttu-id="4e4dc-244">PartitionSelector e ReplicaSelector</span><span class="sxs-lookup"><span data-stu-id="4e4dc-244">PartitionSelector and ReplicaSelector</span></span>
### <a name="partitionselector"></a><span data-ttu-id="4e4dc-245">PartitionSelector</span><span class="sxs-lookup"><span data-stu-id="4e4dc-245">PartitionSelector</span></span>
<span data-ttu-id="4e4dc-246">PartitionSelector é um auxiliar exposto na possibilidade de teste e é usado para selecionar uma partição específica na qual executar qualquer uma das ações da possibilidade de teste.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-246">PartitionSelector is a helper exposed in testability and is used to select a specific partition on which to perform any of the testability actions.</span></span> <span data-ttu-id="4e4dc-247">Ele pode ser usado para selecionar uma partição específica se a ID da partição for conhecida.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-247">It can be used to select a specific partition if the partition ID is known beforehand.</span></span> <span data-ttu-id="4e4dc-248">Ou você pode fornecer a chave de partição e a operação resolverá a ID da partição internamente.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-248">Or, you can provide the partition key and the operation will resolve the partition ID internally.</span></span> <span data-ttu-id="4e4dc-249">Você também tem a opção de selecionar uma partição aleatória.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-249">You also have the option of selecting a random partition.</span></span>

<span data-ttu-id="4e4dc-250">Para usar esse auxiliar, crie o objeto PartitionSelector e selecione a partição usando um dos métodos Select *.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-250">To use this helper, create the PartitionSelector object and select the partition by using one of the Select* methods.</span></span> <span data-ttu-id="4e4dc-251">Em seguida, passe o objeto PartitionSelector para a API que precisa dele.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-251">Then pass in the PartitionSelector object to the API that requires it.</span></span> <span data-ttu-id="4e4dc-252">Se nenhuma opção for selecionada, ela será padronizada para partição aleatória.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-252">If no option is selected, it defaults to a random partition.</span></span>

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

### <a name="replicaselector"></a><span data-ttu-id="4e4dc-253">ReplicaSelector</span><span class="sxs-lookup"><span data-stu-id="4e4dc-253">ReplicaSelector</span></span>
<span data-ttu-id="4e4dc-254">ReplicaSelector é um auxiliar exposto na possibilidade de teste usado para ajudar a selecionar uma réplica na qual executar qualquer uma das ações da possibilidade de teste.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-254">ReplicaSelector is a helper exposed in testability and is used to help select a replica on which to perform any of the testability actions.</span></span> <span data-ttu-id="4e4dc-255">Ele pode ser usado para selecionar uma réplica específica se a ID da réplica já for conhecida.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-255">It can be used to select a specific replica if the replica ID is known beforehand.</span></span> <span data-ttu-id="4e4dc-256">Além disso, você tem a opção de selecionar uma réplica primária ou uma secundária aleatória.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-256">In addition, you have the option of selecting a primary replica or a random secondary.</span></span> <span data-ttu-id="4e4dc-257">ReplicaSelector deriva de PartitionSelector, de modo que você precisa selecionar a réplica e a partição nas quais deseja executar a operação da possibilidade de teste.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-257">ReplicaSelector derives from PartitionSelector, so you need to select both the replica and the partition on which you wish to perform the testability operation.</span></span>

<span data-ttu-id="4e4dc-258">Para usar esse auxiliar, crie um objeto ReplicaSelector e defina a maneira como deseja selecionar a réplica e a partição.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-258">To use this helper, create a ReplicaSelector object and set the way you want to select the replica and the partition.</span></span> <span data-ttu-id="4e4dc-259">Em seguida, passe-o para a API que o exige.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-259">You can then pass it into the API that requires it.</span></span> <span data-ttu-id="4e4dc-260">Se nenhuma opção for selecionada, ela será padronizada para uma réplica ou partição aleatória.</span><span class="sxs-lookup"><span data-stu-id="4e4dc-260">If no option is selected, it defaults to a random replica and random partition.</span></span>

```csharp
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);
long replicaId = 130559876481875498;

// Select a random replica
ReplicaSelector randomReplicaSelector = ReplicaSelector.RandomOf(partitionSelector);

// Select the primary replica
ReplicaSelector primaryReplicaSelector = ReplicaSelector.PrimaryOf(partitionSelector);

// Select the replica by ID
ReplicaSelector replicaByIdSelector = ReplicaSelector.ReplicaIdOf(partitionSelector, replicaId);

// Select a random secondary replica
ReplicaSelector secondaryReplicaSelector = ReplicaSelector.RandomSecondaryOf(partitionSelector);
```

## <a name="next-steps"></a><span data-ttu-id="4e4dc-261">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4e4dc-261">Next steps</span></span>
* [<span data-ttu-id="4e4dc-262">Cenários da possibilidade de teste</span><span class="sxs-lookup"><span data-stu-id="4e4dc-262">Testability scenarios</span></span>](service-fabric-testability-scenarios.md)
* <span data-ttu-id="4e4dc-263">Como testar seu serviço</span><span class="sxs-lookup"><span data-stu-id="4e4dc-263">How to test your service</span></span>
  * [<span data-ttu-id="4e4dc-264">Simular falhas durante cargas de trabalho de serviço</span><span class="sxs-lookup"><span data-stu-id="4e4dc-264">Simulate failures during service workloads</span></span>](service-fabric-testability-workload-tests.md)
  * [<span data-ttu-id="4e4dc-265">Falhas de comunicação entre serviços</span><span class="sxs-lookup"><span data-stu-id="4e4dc-265">Service-to-service communication failures</span></span>](service-fabric-testability-scenarios-service-communication.md)

