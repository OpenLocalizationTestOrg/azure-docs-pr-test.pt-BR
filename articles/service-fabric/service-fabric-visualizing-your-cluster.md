---
title: aaaVisualizing o cluster usando o Gerenciador do Service Fabric | Microsoft Docs
description: "O Explorador do Service Fabric é uma ferramenta baseada na Web para inspecionar e gerenciar aplicativos em nuvem e nós em um cluster do Service Fabric do Microsoft Azure."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: c875b993-b4eb-494b-94b5-e02f5eddbd6a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: ryanwi
ms.openlocfilehash: 73adc4fc254cf6b949b4419b02a046cee3f6a83d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-your-cluster-with-service-fabric-explorer"></a><span data-ttu-id="dce40-103">Visualizando o cluster com o Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="dce40-103">Visualize your cluster with Service Fabric Explorer</span></span>
<span data-ttu-id="dce40-104">O Explorador do Service Fabric é uma ferramenta baseada na Web para inspecionar e gerenciar aplicativos e nós em um cluster do Service Fabric do Azure.</span><span class="sxs-lookup"><span data-stu-id="dce40-104">Service Fabric Explorer is a web-based tool for inspecting and managing applications and nodes in an Azure Service Fabric cluster.</span></span> <span data-ttu-id="dce40-105">Gerenciador do Service Fabric está hospedado diretamente no cluster hello, para que ele estará sempre disponível, independentemente de onde o cluster está em execução.</span><span class="sxs-lookup"><span data-stu-id="dce40-105">Service Fabric Explorer is hosted directly within hello cluster, so it is always available, regardless of where your cluster is running.</span></span>

## <a name="video-tutorial"></a><span data-ttu-id="dce40-106">Tutorial em vídeo</span><span class="sxs-lookup"><span data-stu-id="dce40-106">Video tutorial</span></span>

<span data-ttu-id="dce40-107">toolearn como toouse Service Fabric Explorer, assista Olá vídeo Microsoft Virtual Academy a seguir:</span><span class="sxs-lookup"><span data-stu-id="dce40-107">toolearn how toouse Service Fabric Explorer, watch hello following Microsoft Virtual Academy video:</span></span>

[<center><img src="./media/service-fabric-visualizing-your-cluster/SfxVideo.png" WIDTH="360" HEIGHT="244"></center>](https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=bBTFg46yC_9806218965)

## <a name="connect-tooservice-fabric-explorer"></a><span data-ttu-id="dce40-108">Conecte-se tooService Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="dce40-108">Connect tooService Fabric Explorer</span></span>
<span data-ttu-id="dce40-109">Se você seguiu as instruções de saudação muito[preparar seu ambiente de desenvolvimento](service-fabric-get-started.md), você pode iniciar o Gerenciador do Service Fabric no cluster local navegando toohttp://localhost:19080 / Explorer.</span><span class="sxs-lookup"><span data-stu-id="dce40-109">If you have followed hello instructions too[prepare your development environment](service-fabric-get-started.md), you can launch Service Fabric Explorer on your local cluster by navigating toohttp://localhost:19080/Explorer.</span></span>

## <a name="understand-hello-service-fabric-explorer-layout"></a><span data-ttu-id="dce40-110">Entender o layout do Service Fabric Explorer Olá</span><span class="sxs-lookup"><span data-stu-id="dce40-110">Understand hello Service Fabric Explorer layout</span></span>
<span data-ttu-id="dce40-111">Você pode navegar por meio do Gerenciador do Service Fabric usando árvore Olá Olá esquerda.</span><span class="sxs-lookup"><span data-stu-id="dce40-111">You can navigate through Service Fabric Explorer by using hello tree on hello left.</span></span> <span data-ttu-id="dce40-112">Na raiz de saudação da árvore Olá, painel de cluster de saudação fornece uma visão geral do cluster, incluindo um resumo do aplicativo e a integridade do nó.</span><span class="sxs-lookup"><span data-stu-id="dce40-112">At hello root of hello tree, hello cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span>

![Painel de clusters do Explorador do Service Fabric][sfx-cluster-dashboard]

### <a name="view-hello-clusters-layout"></a><span data-ttu-id="dce40-114">Exibir o layout do cluster Olá</span><span class="sxs-lookup"><span data-stu-id="dce40-114">View hello cluster's layout</span></span>
<span data-ttu-id="dce40-115">Nós em um cluster do Service Fabric são colocados em uma grade bidimensional de domínios de falha e domínios de atualização.</span><span class="sxs-lookup"><span data-stu-id="dce40-115">Nodes in a Service Fabric cluster are placed across a two-dimensional grid of fault domains and upgrade domains.</span></span> <span data-ttu-id="dce40-116">Esse posicionamento garante que os aplicativos permanecem disponíveis na presença de saudação de falhas de hardware e atualizações de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dce40-116">This placement ensures that your applications remain available in hello presence of hardware failures and application upgrades.</span></span> <span data-ttu-id="dce40-117">Você pode exibir como o cluster atual Olá é distribuído usando o mapa de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="dce40-117">You can view how hello current cluster is laid out by using hello cluster map.</span></span>

![Mapa de clusters do Explorador do Service Fabric][sfx-cluster-map]

### <a name="view-applications-and-services"></a><span data-ttu-id="dce40-119">Exibir aplicativos e serviços</span><span class="sxs-lookup"><span data-stu-id="dce40-119">View applications and services</span></span>
<span data-ttu-id="dce40-120">cluster Olá contém duas subárvores: um para aplicativos e outra para nós.</span><span class="sxs-lookup"><span data-stu-id="dce40-120">hello cluster contains two subtrees: one for applications and another for nodes.</span></span>

<span data-ttu-id="dce40-121">Você pode usar o hello aplicativo exibição toonavigate a hierarquia lógica da malha do serviço: aplicativos, serviços, partições e réplicas.</span><span class="sxs-lookup"><span data-stu-id="dce40-121">You can use hello application view toonavigate through Service Fabric's logical hierarchy: applications, services, partitions, and replicas.</span></span>

<span data-ttu-id="dce40-122">O exemplo hello abaixo, Olá aplicativo **MyApp** consiste em dois serviços, **MyStatefulService** e **WebService**.</span><span class="sxs-lookup"><span data-stu-id="dce40-122">In hello example below, hello application **MyApp** consists of two services, **MyStatefulService** and **WebService**.</span></span> <span data-ttu-id="dce40-123">Como o **MyStatefulService** tem monitoração de estado, ele inclui uma partição com uma réplica principal e duas secundárias.</span><span class="sxs-lookup"><span data-stu-id="dce40-123">Since **MyStatefulService** is stateful, it includes a partition with one primary and two secondary replicas.</span></span> <span data-ttu-id="dce40-124">Por outro lado, o WebSvcService é sem monitoração de estado e contém uma única instância.</span><span class="sxs-lookup"><span data-stu-id="dce40-124">By contrast, WebSvcService is stateless and contains a single instance.</span></span>

![Exibição do aplicativo do Explorador do Service Fabric][sfx-application-tree]

<span data-ttu-id="dce40-126">Em cada nível da árvore de hello, painel principal Olá mostra informações pertinentes sobre o item de saudação.</span><span class="sxs-lookup"><span data-stu-id="dce40-126">At each level of hello tree, hello main pane shows pertinent information about hello item.</span></span> <span data-ttu-id="dce40-127">Por exemplo, você pode ver o status de integridade de saudação e versão para um serviço específico.</span><span class="sxs-lookup"><span data-stu-id="dce40-127">For example, you can see hello health status and version for a particular service.</span></span>

![Painel essencial do Explorador do Service Fabric][sfx-service-essentials]

### <a name="view-hello-clusters-nodes"></a><span data-ttu-id="dce40-129">Visualizar os nós do cluster Olá</span><span class="sxs-lookup"><span data-stu-id="dce40-129">View hello cluster's nodes</span></span>
<span data-ttu-id="dce40-130">exibição do nó de saudação mostra o layout físico de saudação do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="dce40-130">hello node view shows hello physical layout of hello cluster.</span></span> <span data-ttu-id="dce40-131">Para um nó específico, você pode inspecionar quais aplicativos têm código implantado naquele nó.</span><span class="sxs-lookup"><span data-stu-id="dce40-131">For a given node, you can inspect which applications have code deployed on that node.</span></span> <span data-ttu-id="dce40-132">Mais especificamente, você pode ver quais réplicas estão sendo executadas lá atualmente.</span><span class="sxs-lookup"><span data-stu-id="dce40-132">More specifically, you can see which replicas are currently running there.</span></span>

## <a name="actions"></a><span data-ttu-id="dce40-133">Ações</span><span class="sxs-lookup"><span data-stu-id="dce40-133">Actions</span></span>
<span data-ttu-id="dce40-134">Service Fabric Explorer oferece uma maneira rápida de tooinvoke ações em nós, aplicativos e serviços em cluster.</span><span class="sxs-lookup"><span data-stu-id="dce40-134">Service Fabric Explorer offers a quick way tooinvoke actions on nodes, applications, and services within your cluster.</span></span>

<span data-ttu-id="dce40-135">Por exemplo, toodelete uma instância de aplicativo, escolha o aplicativo hello da árvore Olá Olá esquerda e, em seguida, escolha **ações** > **excluir aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="dce40-135">For example, toodelete an application instance, choose hello application from hello tree on hello left, and then choose **Actions** > **Delete Application**.</span></span>

![Excluir um aplicativo no Explorador do Service Fabric][sfx-delete-application]

> [!TIP]
> <span data-ttu-id="dce40-137">Você pode executar Olá ações clicando Olá reticências próximo tooeach elemento.</span><span class="sxs-lookup"><span data-stu-id="dce40-137">You can perform hello same actions by clicking hello ellipsis next tooeach element.</span></span>
>
>

<span data-ttu-id="dce40-138">Olá tabela a seguir lista as ações de saudação disponíveis para cada entidade:</span><span class="sxs-lookup"><span data-stu-id="dce40-138">hello following table lists hello actions available for each entity:</span></span>

| <span data-ttu-id="dce40-139">**Entidade**</span><span class="sxs-lookup"><span data-stu-id="dce40-139">**Entity**</span></span> | <span data-ttu-id="dce40-140">**Ação**</span><span class="sxs-lookup"><span data-stu-id="dce40-140">**Action**</span></span> | <span data-ttu-id="dce40-141">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="dce40-141">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dce40-142">Tipo de aplicativo</span><span class="sxs-lookup"><span data-stu-id="dce40-142">Application type</span></span> |<span data-ttu-id="dce40-143">Remover o provisionamento de tipo</span><span class="sxs-lookup"><span data-stu-id="dce40-143">Unprovision type</span></span> |<span data-ttu-id="dce40-144">Remove o pacote de aplicativo de saudação do cluster de saudação repositório de imagens.</span><span class="sxs-lookup"><span data-stu-id="dce40-144">Removes hello application package from hello cluster's image store.</span></span> <span data-ttu-id="dce40-145">Requer que todos os aplicativos de que toobe tipo removido primeiro.</span><span class="sxs-lookup"><span data-stu-id="dce40-145">Requires all applications of that type toobe removed first.</span></span> |
| <span data-ttu-id="dce40-146">Aplicativo</span><span class="sxs-lookup"><span data-stu-id="dce40-146">Application</span></span> |<span data-ttu-id="dce40-147">Excluir Aplicativo</span><span class="sxs-lookup"><span data-stu-id="dce40-147">Delete Application</span></span> |<span data-ttu-id="dce40-148">Exclua aplicativo hello, incluindo todos os seus serviços e seus estados (se houver).</span><span class="sxs-lookup"><span data-stu-id="dce40-148">Delete hello application, including all its services and their state (if any).</span></span> |
| <span data-ttu-id="dce40-149">O Barramento de</span><span class="sxs-lookup"><span data-stu-id="dce40-149">Service</span></span> |<span data-ttu-id="dce40-150">Excluir serviço</span><span class="sxs-lookup"><span data-stu-id="dce40-150">Delete Service</span></span> |<span data-ttu-id="dce40-151">Exclua serviço hello e seu estado (se houver).</span><span class="sxs-lookup"><span data-stu-id="dce40-151">Delete hello service and its state (if any).</span></span> |
| <span data-ttu-id="dce40-152">Nó</span><span class="sxs-lookup"><span data-stu-id="dce40-152">Node</span></span> |<span data-ttu-id="dce40-153">Ativar</span><span class="sxs-lookup"><span data-stu-id="dce40-153">Activate</span></span> |<span data-ttu-id="dce40-154">Ative nó hello.</span><span class="sxs-lookup"><span data-stu-id="dce40-154">Activate hello node.</span></span> |
| <span data-ttu-id="dce40-155">Nó</span><span class="sxs-lookup"><span data-stu-id="dce40-155">Node</span></span> | <span data-ttu-id="dce40-156">Desativar (pausa)</span><span class="sxs-lookup"><span data-stu-id="dce40-156">Deactivate (pause)</span></span> | <span data-ttu-id="dce40-157">Pausa no nó Olá em seu estado atual.</span><span class="sxs-lookup"><span data-stu-id="dce40-157">Pause hello node in its current state.</span></span> <span data-ttu-id="dce40-158">Serviços continuam toorun mas Service Fabric não proativamente mover tudo para ou dela, a menos que ele é necessário tooprevent uma interrupção ou inconsistência de dados.</span><span class="sxs-lookup"><span data-stu-id="dce40-158">Services continue toorun but Service Fabric does not proactively move anything onto or off it unless it is required tooprevent an outage or data inconsistency.</span></span> <span data-ttu-id="dce40-159">Esta ação é normalmente usada tooenable depurando serviços em tooensure um nó específico que eles não serão movidos durante a inspeção.</span><span class="sxs-lookup"><span data-stu-id="dce40-159">This action is typically used tooenable debugging services on a specific node tooensure that they do not move during inspection.</span></span> | |
| <span data-ttu-id="dce40-160">Nó</span><span class="sxs-lookup"><span data-stu-id="dce40-160">Node</span></span> | <span data-ttu-id="dce40-161">Desativar (reiniciar)</span><span class="sxs-lookup"><span data-stu-id="dce40-161">Deactivate (restart)</span></span> | <span data-ttu-id="dce40-162">Mova todos os serviços na memória de um nó com segurança e feche os serviços persistentes.</span><span class="sxs-lookup"><span data-stu-id="dce40-162">Safely move all in-memory services off a node and close persistent services.</span></span> <span data-ttu-id="dce40-163">Geralmente usado quando os processos de host hello ou máquina necessidade toobe reiniciado.</span><span class="sxs-lookup"><span data-stu-id="dce40-163">Typically used when hello host processes or machine need toobe restarted.</span></span> | |
| <span data-ttu-id="dce40-164">Nó</span><span class="sxs-lookup"><span data-stu-id="dce40-164">Node</span></span> | <span data-ttu-id="dce40-165">Desativar (remover dados)</span><span class="sxs-lookup"><span data-stu-id="dce40-165">Deactivate (remove data)</span></span> | <span data-ttu-id="dce40-166">Feche com segurança todos os serviços em execução no nó Olá após a criação de réplicas de reposição suficientes.</span><span class="sxs-lookup"><span data-stu-id="dce40-166">Safely close all services running on hello node after building sufficient spare replicas.</span></span> <span data-ttu-id="dce40-167">Normalmente usado quando um nó (ou pelo menos seu armazenamento) é desabilitado permanentemente.</span><span class="sxs-lookup"><span data-stu-id="dce40-167">Typically used when a node (or at least its storage) is being permanently taken out of commission.</span></span> | |
| <span data-ttu-id="dce40-168">Nó</span><span class="sxs-lookup"><span data-stu-id="dce40-168">Node</span></span> | <span data-ttu-id="dce40-169">Remover o estado do nó</span><span class="sxs-lookup"><span data-stu-id="dce40-169">Remove node state</span></span> | <span data-ttu-id="dce40-170">Remova dados de conhecimento das réplicas de um nó de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="dce40-170">Remove knowledge of a node's replicas from hello cluster.</span></span> <span data-ttu-id="dce40-171">Normalmente usado quando um nó com falha já é considerado irrecuperável.</span><span class="sxs-lookup"><span data-stu-id="dce40-171">Typically used when an already failed node is deemed unrecoverable.</span></span> | |
| <span data-ttu-id="dce40-172">Nó</span><span class="sxs-lookup"><span data-stu-id="dce40-172">Node</span></span> | <span data-ttu-id="dce40-173">Reiniciar</span><span class="sxs-lookup"><span data-stu-id="dce40-173">Restart</span></span> | <span data-ttu-id="dce40-174">Simule uma falha de nó, reiniciando nó hello.</span><span class="sxs-lookup"><span data-stu-id="dce40-174">Simulate a node failure by restarting hello node.</span></span> <span data-ttu-id="dce40-175">Mais informações podem ser obtidas [aqui](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps)</span><span class="sxs-lookup"><span data-stu-id="dce40-175">More information [here](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps)</span></span> | |

<span data-ttu-id="dce40-176">Como muitas ações são destrutivas, talvez seja solicitado tooconfirm sua intenção antes da conclusão da ação de saudação.</span><span class="sxs-lookup"><span data-stu-id="dce40-176">Since many actions are destructive, you may be asked tooconfirm your intent before hello action is completed.</span></span>

> [!TIP]
> <span data-ttu-id="dce40-177">Todas as ações que podem ser executadas por meio do Gerenciador do Service Fabric também podem ser executadas por meio do PowerShell ou uma API REST, tooenable automação.</span><span class="sxs-lookup"><span data-stu-id="dce40-177">Every action that can be performed through Service Fabric Explorer can also be performed through PowerShell or a REST API, tooenable automation.</span></span>
>
>

<span data-ttu-id="dce40-178">Você também pode usar instâncias de aplicativos do Service Fabric Explorer toocreate para um tipo determinado aplicativo e a versão.</span><span class="sxs-lookup"><span data-stu-id="dce40-178">You can also use Service Fabric Explorer toocreate application instances for a given application type and version.</span></span> <span data-ttu-id="dce40-179">Escolha o tipo de aplicativo de Olá Olá na exibição em árvore, clique em Olá **criar instância de aplicativo** versão toohello próximo link no painel direito da saudação.</span><span class="sxs-lookup"><span data-stu-id="dce40-179">Choose hello application type in hello tree view, then click hello **Create app instance** link next toohello version you'd like in hello right pane.</span></span>

![Criar uma instância de aplicativo no Service Fabric Explorer][sfx-create-app-instance]

> [!NOTE]
> <span data-ttu-id="dce40-181">Instâncias de aplicativos criadas por meio do Service Fabric Explorer no momento não podem ser parametrizadas.</span><span class="sxs-lookup"><span data-stu-id="dce40-181">Application instances created through Service Fabric Explorer cannot currently be parameterized.</span></span> <span data-ttu-id="dce40-182">Elas são criadas usando os valores de parâmetro padrão.</span><span class="sxs-lookup"><span data-stu-id="dce40-182">They are created using default parameter values.</span></span>
>
>

## <a name="connect-tooa-remote-service-fabric-cluster"></a><span data-ttu-id="dce40-183">Conecte-se o cluster de malha do serviço remoto tooa</span><span class="sxs-lookup"><span data-stu-id="dce40-183">Connect tooa remote Service Fabric cluster</span></span>
<span data-ttu-id="dce40-184">Se você souber o ponto de extremidade do cluster hello e tem permissões suficientes, você pode acessar Service Fabric Explorer em qualquer navegador.</span><span class="sxs-lookup"><span data-stu-id="dce40-184">If you know hello cluster's endpoint and have sufficient permissions you can access Service Fabric Explorer from any browser.</span></span> <span data-ttu-id="dce40-185">Isso ocorre porque o Service Fabric Explorer é apenas outro serviço que é executado no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="dce40-185">This is because Service Fabric Explorer is just another service that runs in hello cluster.</span></span>

### <a name="discover-hello-service-fabric-explorer-endpoint-for-a-remote-cluster"></a><span data-ttu-id="dce40-186">Descobrir ponto de extremidade do hello Service Fabric Explorer para um cluster remoto</span><span class="sxs-lookup"><span data-stu-id="dce40-186">Discover hello Service Fabric Explorer endpoint for a remote cluster</span></span>
<span data-ttu-id="dce40-187">tooreach Service Fabric Explorer para um determinado cluster, aponte seu navegador para:</span><span class="sxs-lookup"><span data-stu-id="dce40-187">tooreach Service Fabric Explorer for a given cluster, point your browser to:</span></span>

<span data-ttu-id="dce40-188">http://&lt;your-cluster-endpoint&gt;:19080/Explorer</span><span class="sxs-lookup"><span data-stu-id="dce40-188">http://&lt;your-cluster-endpoint&gt;:19080/Explorer</span></span>

<span data-ttu-id="dce40-189">Para clusters do Azure, Olá a URL completa também está disponível no painel de essentials de cluster de saudação do hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="dce40-189">For Azure clusters, hello full URL is also available in hello cluster essentials pane of hello Azure portal.</span></span>

### <a name="connect-tooa-secure-cluster"></a><span data-ttu-id="dce40-190">Conecte-se o cluster seguro tooa</span><span class="sxs-lookup"><span data-stu-id="dce40-190">Connect tooa secure cluster</span></span>
<span data-ttu-id="dce40-191">Você pode controlar o cliente tooyour Service Fabric cluster de acesso com certificados ou usando o Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="dce40-191">You can control client access tooyour Service Fabric cluster either with certificates or using Azure Active Directory (AAD).</span></span>

<span data-ttu-id="dce40-192">Se você tentar tooconnect tooService Fabric Explorer em um cluster seguro, dependendo da configuração do cluster de saudação você vai ser toopresent necessário um certificado de cliente ou faça logon usando o AAD.</span><span class="sxs-lookup"><span data-stu-id="dce40-192">If you attempt tooconnect tooService Fabric Explorer on a secure cluster, then depending on hello cluster's configuration you'll be required toopresent a client certificate or log in using AAD.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dce40-193">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dce40-193">Next steps</span></span>
* [<span data-ttu-id="dce40-194">Visão geral da Possibilidade de Teste</span><span class="sxs-lookup"><span data-stu-id="dce40-194">Testability overview</span></span>](service-fabric-testability-overview.md)
* [<span data-ttu-id="dce40-195">Gerenciando aplicativos da Malha do Serviço no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dce40-195">Managing your Service Fabric applications in Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)
* [<span data-ttu-id="dce40-196">Implantação de aplicativos de Malha do Serviço usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="dce40-196">Service Fabric application deployment using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)

<!--Image references-->
[sfx-cluster-dashboard]: ./media/service-fabric-visualizing-your-cluster/SfxClusterDashboard.png
[sfx-cluster-map]: ./media/service-fabric-visualizing-your-cluster/SfxClusterMap.png
[sfx-application-tree]: ./media/service-fabric-visualizing-your-cluster/SfxApplicationTree.png
[sfx-service-essentials]: ./media/service-fabric-visualizing-your-cluster/SfxServiceEssentials.png
[sfx-delete-application]: ./media/service-fabric-visualizing-your-cluster/SfxDeleteApplication.png
[sfx-create-app-instance]: ./media/service-fabric-visualizing-your-cluster/SfxCreateAppInstance.png
