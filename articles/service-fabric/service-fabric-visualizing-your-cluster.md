---
title: Visualizar seu cluster usando o Service Fabric Explorer | Microsoft Docs
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
ms.openlocfilehash: 789793a7f50170188d688881a9178546c3074018
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="visualize-your-cluster-with-service-fabric-explorer"></a><span data-ttu-id="4aa7d-103">Visualizando o cluster com o Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="4aa7d-103">Visualize your cluster with Service Fabric Explorer</span></span>
<span data-ttu-id="4aa7d-104">O Explorador do Service Fabric é uma ferramenta baseada na Web para inspecionar e gerenciar aplicativos e nós em um cluster do Service Fabric do Azure.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-104">Service Fabric Explorer is a web-based tool for inspecting and managing applications and nodes in an Azure Service Fabric cluster.</span></span> <span data-ttu-id="4aa7d-105">O Explorador do Service Fabric é hospedado diretamente dentro do cluster para estar sempre disponível, independentemente de onde o cluster estiver sendo executado.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-105">Service Fabric Explorer is hosted directly within the cluster, so it is always available, regardless of where your cluster is running.</span></span>

## <a name="video-tutorial"></a><span data-ttu-id="4aa7d-106">Tutorial em vídeo</span><span class="sxs-lookup"><span data-stu-id="4aa7d-106">Video tutorial</span></span>

<span data-ttu-id="4aa7d-107">Para saber como usar o Service Fabric Explorer, assista ao seguinte vídeo da Microsoft Virtual Academy:</span><span class="sxs-lookup"><span data-stu-id="4aa7d-107">To learn how to use Service Fabric Explorer, watch the following Microsoft Virtual Academy video:</span></span>

[<center><img src="./media/service-fabric-visualizing-your-cluster/SfxVideo.png" WIDTH="360" HEIGHT="244"></center>](https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=bBTFg46yC_9806218965)

## <a name="connect-to-service-fabric-explorer"></a><span data-ttu-id="4aa7d-108">Conectar ao Explorador do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4aa7d-108">Connect to Service Fabric Explorer</span></span>
<span data-ttu-id="4aa7d-109">Se você seguiu as instruções para [preparar o seu ambiente de desenvolvimento](service-fabric-get-started.md), pode inicializar o Explorador do Service Fabric no cluster local navegando para http://localhost:19080/Explorer.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-109">If you have followed the instructions to [prepare your development environment](service-fabric-get-started.md), you can launch Service Fabric Explorer on your local cluster by navigating to http://localhost:19080/Explorer.</span></span>

## <a name="understand-the-service-fabric-explorer-layout"></a><span data-ttu-id="4aa7d-110">Entender o layout do Explorador do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4aa7d-110">Understand the Service Fabric Explorer layout</span></span>
<span data-ttu-id="4aa7d-111">Você pode navegar pelo Explorador do Service Fabric usando a árvore à esquerda.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-111">You can navigate through Service Fabric Explorer by using the tree on the left.</span></span> <span data-ttu-id="4aa7d-112">Na raiz da árvore, o painel do cluster fornece uma visão geral do cluster, incluindo um resumo do aplicativo e a integridade do nó.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-112">At the root of the tree, the cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span>

![Painel de clusters do Explorador do Service Fabric][sfx-cluster-dashboard]

### <a name="view-the-clusters-layout"></a><span data-ttu-id="4aa7d-114">Exibir o layout do cluster</span><span class="sxs-lookup"><span data-stu-id="4aa7d-114">View the cluster's layout</span></span>
<span data-ttu-id="4aa7d-115">Nós em um cluster do Service Fabric são colocados em uma grade bidimensional de domínios de falha e domínios de atualização.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-115">Nodes in a Service Fabric cluster are placed across a two-dimensional grid of fault domains and upgrade domains.</span></span> <span data-ttu-id="4aa7d-116">Esse posicionamento garante que seus aplicativos permaneçam disponíveis na presença de falhas de hardware e atualizações de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-116">This placement ensures that your applications remain available in the presence of hardware failures and application upgrades.</span></span> <span data-ttu-id="4aa7d-117">Você pode exibir o layout do cluster atual usando o mapa de clusters.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-117">You can view how the current cluster is laid out by using the cluster map.</span></span>

![Mapa de clusters do Explorador do Service Fabric][sfx-cluster-map]

### <a name="view-applications-and-services"></a><span data-ttu-id="4aa7d-119">Exibir aplicativos e serviços</span><span class="sxs-lookup"><span data-stu-id="4aa7d-119">View applications and services</span></span>
<span data-ttu-id="4aa7d-120">O cluster contém duas subárvores: uma para aplicativos e outra para nós.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-120">The cluster contains two subtrees: one for applications and another for nodes.</span></span>

<span data-ttu-id="4aa7d-121">Você pode usar a exibição de aplicativos para navegar pela hierarquia lógica do Service Fabric: aplicativos, serviços, partições e réplicas.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-121">You can use the application view to navigate through Service Fabric's logical hierarchy: applications, services, partitions, and replicas.</span></span>

<span data-ttu-id="4aa7d-122">No exemplo abaixo, o aplicativo **MyApp** é composto por dois serviços, **MyStatefulService** e **WebService**.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-122">In the example below, the application **MyApp** consists of two services, **MyStatefulService** and **WebService**.</span></span> <span data-ttu-id="4aa7d-123">Como o **MyStatefulService** tem monitoração de estado, ele inclui uma partição com uma réplica principal e duas secundárias.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-123">Since **MyStatefulService** is stateful, it includes a partition with one primary and two secondary replicas.</span></span> <span data-ttu-id="4aa7d-124">Por outro lado, o WebSvcService é sem monitoração de estado e contém uma única instância.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-124">By contrast, WebSvcService is stateless and contains a single instance.</span></span>

![Exibição do aplicativo do Explorador do Service Fabric][sfx-application-tree]

<span data-ttu-id="4aa7d-126">Em cada nível da árvore, o painel principal mostra informações pertinentes sobre o item.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-126">At each level of the tree, the main pane shows pertinent information about the item.</span></span> <span data-ttu-id="4aa7d-127">Por exemplo, você pode ver o status de integridade e a versão de um serviço específico.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-127">For example, you can see the health status and version for a particular service.</span></span>

![Painel essencial do Explorador do Service Fabric][sfx-service-essentials]

### <a name="view-the-clusters-nodes"></a><span data-ttu-id="4aa7d-129">Exibir os nós do cluster</span><span class="sxs-lookup"><span data-stu-id="4aa7d-129">View the cluster's nodes</span></span>
<span data-ttu-id="4aa7d-130">A exibição de nós mostra o layout físico do cluster.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-130">The node view shows the physical layout of the cluster.</span></span> <span data-ttu-id="4aa7d-131">Para um nó específico, você pode inspecionar quais aplicativos têm código implantado naquele nó.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-131">For a given node, you can inspect which applications have code deployed on that node.</span></span> <span data-ttu-id="4aa7d-132">Mais especificamente, você pode ver quais réplicas estão sendo executadas lá atualmente.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-132">More specifically, you can see which replicas are currently running there.</span></span>

## <a name="actions"></a><span data-ttu-id="4aa7d-133">Ações</span><span class="sxs-lookup"><span data-stu-id="4aa7d-133">Actions</span></span>
<span data-ttu-id="4aa7d-134">O Explorador do Service Fabric oferece uma maneira rápida de invocar ações em nós, aplicativos e serviços no cluster.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-134">Service Fabric Explorer offers a quick way to invoke actions on nodes, applications, and services within your cluster.</span></span>

<span data-ttu-id="4aa7d-135">Por exemplo, para excluir uma instância do aplicativo, escolha o aplicativo na árvore à esquerda e escolha **Ações** > **Excluir Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-135">For example, to delete an application instance, choose the application from the tree on the left, and then choose **Actions** > **Delete Application**.</span></span>

![Excluir um aplicativo no Explorador do Service Fabric][sfx-delete-application]

> [!TIP]
> <span data-ttu-id="4aa7d-137">Você pode executar as mesmas ações clicando nas reticências ao lado de cada elemento.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-137">You can perform the same actions by clicking the ellipsis next to each element.</span></span>
>
>

<span data-ttu-id="4aa7d-138">A tabela a seguir lista as ações disponíveis para cada entidade:</span><span class="sxs-lookup"><span data-stu-id="4aa7d-138">The following table lists the actions available for each entity:</span></span>

| <span data-ttu-id="4aa7d-139">**Entidade**</span><span class="sxs-lookup"><span data-stu-id="4aa7d-139">**Entity**</span></span> | <span data-ttu-id="4aa7d-140">**Ação**</span><span class="sxs-lookup"><span data-stu-id="4aa7d-140">**Action**</span></span> | <span data-ttu-id="4aa7d-141">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="4aa7d-141">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4aa7d-142">Tipo de aplicativo</span><span class="sxs-lookup"><span data-stu-id="4aa7d-142">Application type</span></span> |<span data-ttu-id="4aa7d-143">Remover o provisionamento de tipo</span><span class="sxs-lookup"><span data-stu-id="4aa7d-143">Unprovision type</span></span> |<span data-ttu-id="4aa7d-144">Remover o pacote de aplicativos do repositório de imagens do cluster.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-144">Removes the application package from the cluster's image store.</span></span> <span data-ttu-id="4aa7d-145">Requer que todos os aplicativos desse tipo sejam removidos em primeiro lugar.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-145">Requires all applications of that type to be removed first.</span></span> |
| <span data-ttu-id="4aa7d-146">Aplicativo</span><span class="sxs-lookup"><span data-stu-id="4aa7d-146">Application</span></span> |<span data-ttu-id="4aa7d-147">Excluir Aplicativo</span><span class="sxs-lookup"><span data-stu-id="4aa7d-147">Delete Application</span></span> |<span data-ttu-id="4aa7d-148">Exclua o aplicativo, incluindo todos os seus serviços e o estado (se houver).</span><span class="sxs-lookup"><span data-stu-id="4aa7d-148">Delete the application, including all its services and their state (if any).</span></span> |
| <span data-ttu-id="4aa7d-149">O Barramento de</span><span class="sxs-lookup"><span data-stu-id="4aa7d-149">Service</span></span> |<span data-ttu-id="4aa7d-150">Excluir serviço</span><span class="sxs-lookup"><span data-stu-id="4aa7d-150">Delete Service</span></span> |<span data-ttu-id="4aa7d-151">Exclua o serviço e seu estado (se houver).</span><span class="sxs-lookup"><span data-stu-id="4aa7d-151">Delete the service and its state (if any).</span></span> |
| <span data-ttu-id="4aa7d-152">Nó</span><span class="sxs-lookup"><span data-stu-id="4aa7d-152">Node</span></span> |<span data-ttu-id="4aa7d-153">Ativar</span><span class="sxs-lookup"><span data-stu-id="4aa7d-153">Activate</span></span> |<span data-ttu-id="4aa7d-154">Ative o nó.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-154">Activate the node.</span></span> |
| <span data-ttu-id="4aa7d-155">Nó</span><span class="sxs-lookup"><span data-stu-id="4aa7d-155">Node</span></span> | <span data-ttu-id="4aa7d-156">Desativar (pausa)</span><span class="sxs-lookup"><span data-stu-id="4aa7d-156">Deactivate (pause)</span></span> | <span data-ttu-id="4aa7d-157">Pause o nó em seu estado atual.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-157">Pause the node in its current state.</span></span> <span data-ttu-id="4aa7d-158">Os serviços continuam sendo executados, mas o Service Fabric não move nada dele ou para ele proativamente, exceto se for necessário para impedir uma interrupção ou inconsistência de dados.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-158">Services continue to run but Service Fabric does not proactively move anything onto or off it unless it is required to prevent an outage or data inconsistency.</span></span> <span data-ttu-id="4aa7d-159">Essa ação normalmente é usada para habilitar serviços de depuração em um nó específico a fim de garantir que não sejam movidos durante a inspeção.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-159">This action is typically used to enable debugging services on a specific node to ensure that they do not move during inspection.</span></span> | |
| <span data-ttu-id="4aa7d-160">Nó</span><span class="sxs-lookup"><span data-stu-id="4aa7d-160">Node</span></span> | <span data-ttu-id="4aa7d-161">Desativar (reiniciar)</span><span class="sxs-lookup"><span data-stu-id="4aa7d-161">Deactivate (restart)</span></span> | <span data-ttu-id="4aa7d-162">Mova todos os serviços na memória de um nó com segurança e feche os serviços persistentes.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-162">Safely move all in-memory services off a node and close persistent services.</span></span> <span data-ttu-id="4aa7d-163">Normalmente usado quando os processos de host ou o computador precisam ser reiniciados.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-163">Typically used when the host processes or machine need to be restarted.</span></span> | |
| <span data-ttu-id="4aa7d-164">Nó</span><span class="sxs-lookup"><span data-stu-id="4aa7d-164">Node</span></span> | <span data-ttu-id="4aa7d-165">Desativar (remover dados)</span><span class="sxs-lookup"><span data-stu-id="4aa7d-165">Deactivate (remove data)</span></span> | <span data-ttu-id="4aa7d-166">Feche com segurança todos os serviços em execução no nó após a criação de réplicas de reposição suficientes.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-166">Safely close all services running on the node after building sufficient spare replicas.</span></span> <span data-ttu-id="4aa7d-167">Normalmente usado quando um nó (ou pelo menos seu armazenamento) é desabilitado permanentemente.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-167">Typically used when a node (or at least its storage) is being permanently taken out of commission.</span></span> | |
| <span data-ttu-id="4aa7d-168">Nó</span><span class="sxs-lookup"><span data-stu-id="4aa7d-168">Node</span></span> | <span data-ttu-id="4aa7d-169">Remover o estado do nó</span><span class="sxs-lookup"><span data-stu-id="4aa7d-169">Remove node state</span></span> | <span data-ttu-id="4aa7d-170">Remova o conhecimento das réplicas do nó do cluster.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-170">Remove knowledge of a node's replicas from the cluster.</span></span> <span data-ttu-id="4aa7d-171">Normalmente usado quando um nó com falha já é considerado irrecuperável.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-171">Typically used when an already failed node is deemed unrecoverable.</span></span> | |
| <span data-ttu-id="4aa7d-172">Nó</span><span class="sxs-lookup"><span data-stu-id="4aa7d-172">Node</span></span> | <span data-ttu-id="4aa7d-173">Reiniciar</span><span class="sxs-lookup"><span data-stu-id="4aa7d-173">Restart</span></span> | <span data-ttu-id="4aa7d-174">Simule a falha de nó reiniciando o nó.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-174">Simulate a node failure by restarting the node.</span></span> <span data-ttu-id="4aa7d-175">Mais informações podem ser obtidas [aqui](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps)</span><span class="sxs-lookup"><span data-stu-id="4aa7d-175">More information [here](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps)</span></span> | |

<span data-ttu-id="4aa7d-176">Como muitas ações são destrutivas, talvez seja necessário confirmar sua intenção antes que a ação seja concluída.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-176">Since many actions are destructive, you may be asked to confirm your intent before the action is completed.</span></span>

> [!TIP]
> <span data-ttu-id="4aa7d-177">Todas as ações que podem ser executadas usando o Explorador do Service Fabric também podem ser executadas usando o PowerShell ou uma API REST para habilitar a automação.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-177">Every action that can be performed through Service Fabric Explorer can also be performed through PowerShell or a REST API, to enable automation.</span></span>
>
>

<span data-ttu-id="4aa7d-178">Você também pode usar o Service Fabric Explorer para criar instâncias de aplicativo para um determinado tipo e versão de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-178">You can also use Service Fabric Explorer to create application instances for a given application type and version.</span></span> <span data-ttu-id="4aa7d-179">Escolha o tipo de aplicativo no modo de exibição de árvore, clique no link **Create app instance (Criar instância de aplicativo)** ao lado da versão desejada no painel da direita.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-179">Choose the application type in the tree view, then click the **Create app instance** link next to the version you'd like in the right pane.</span></span>

![Criar uma instância de aplicativo no Service Fabric Explorer][sfx-create-app-instance]

> [!NOTE]
> <span data-ttu-id="4aa7d-181">Instâncias de aplicativos criadas por meio do Service Fabric Explorer no momento não podem ser parametrizadas.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-181">Application instances created through Service Fabric Explorer cannot currently be parameterized.</span></span> <span data-ttu-id="4aa7d-182">Elas são criadas usando os valores de parâmetro padrão.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-182">They are created using default parameter values.</span></span>
>
>

## <a name="connect-to-a-remote-service-fabric-cluster"></a><span data-ttu-id="4aa7d-183">Conectar a um cluster remoto do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4aa7d-183">Connect to a remote Service Fabric cluster</span></span>
<span data-ttu-id="4aa7d-184">Conhecendo o ponto de extremidade do cluster e com permissões suficientes, você pode acessar o Service Fabric Explorer de qualquer navegador.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-184">If you know the cluster's endpoint and have sufficient permissions you can access Service Fabric Explorer from any browser.</span></span> <span data-ttu-id="4aa7d-185">Isso porque o Service Fabric Explorer é apenas outro serviço executado no cluster.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-185">This is because Service Fabric Explorer is just another service that runs in the cluster.</span></span>

### <a name="discover-the-service-fabric-explorer-endpoint-for-a-remote-cluster"></a><span data-ttu-id="4aa7d-186">Descobrir o ponto de extremidade do Explorador do Service Fabric para um cluster remoto</span><span class="sxs-lookup"><span data-stu-id="4aa7d-186">Discover the Service Fabric Explorer endpoint for a remote cluster</span></span>
<span data-ttu-id="4aa7d-187">A fim de acessar o Service Fabric Explorer para um determinado cluster, aponte o navegador para:</span><span class="sxs-lookup"><span data-stu-id="4aa7d-187">To reach Service Fabric Explorer for a given cluster, point your browser to:</span></span>

<span data-ttu-id="4aa7d-188">http://&lt;your-cluster-endpoint&gt;:19080/Explorer</span><span class="sxs-lookup"><span data-stu-id="4aa7d-188">http://&lt;your-cluster-endpoint&gt;:19080/Explorer</span></span>

<span data-ttu-id="4aa7d-189">Para clusters do Azure, a URL completa também está disponível no painel de noções básicas do cluster do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-189">For Azure clusters, the full URL is also available in the cluster essentials pane of the Azure portal.</span></span>

### <a name="connect-to-a-secure-cluster"></a><span data-ttu-id="4aa7d-190">Conectar a um cluster seguro</span><span class="sxs-lookup"><span data-stu-id="4aa7d-190">Connect to a secure cluster</span></span>
<span data-ttu-id="4aa7d-191">Você pode controlar o acesso do cliente ao cluster do Service Fabric com certificados ou usando o AAD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="4aa7d-191">You can control client access to your Service Fabric cluster either with certificates or using Azure Active Directory (AAD).</span></span>

<span data-ttu-id="4aa7d-192">Se você tentar se conectar ao Service Fabric Explorer em um cluster seguro, dependendo da configuração do cluster, será preciso apresentar um certificado de cliente ou fazer logon usando o AAD.</span><span class="sxs-lookup"><span data-stu-id="4aa7d-192">If you attempt to connect to Service Fabric Explorer on a secure cluster, then depending on the cluster's configuration you'll be required to present a client certificate or log in using AAD.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4aa7d-193">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4aa7d-193">Next steps</span></span>
* [<span data-ttu-id="4aa7d-194">Visão geral da Possibilidade de Teste</span><span class="sxs-lookup"><span data-stu-id="4aa7d-194">Testability overview</span></span>](service-fabric-testability-overview.md)
* [<span data-ttu-id="4aa7d-195">Gerenciando aplicativos da Malha do Serviço no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4aa7d-195">Managing your Service Fabric applications in Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)
* [<span data-ttu-id="4aa7d-196">Implantação de aplicativos de Malha do Serviço usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="4aa7d-196">Service Fabric application deployment using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)

<!--Image references-->
[sfx-cluster-dashboard]: ./media/service-fabric-visualizing-your-cluster/SfxClusterDashboard.png
[sfx-cluster-map]: ./media/service-fabric-visualizing-your-cluster/SfxClusterMap.png
[sfx-application-tree]: ./media/service-fabric-visualizing-your-cluster/SfxApplicationTree.png
[sfx-service-essentials]: ./media/service-fabric-visualizing-your-cluster/SfxServiceEssentials.png
[sfx-delete-application]: ./media/service-fabric-visualizing-your-cluster/SfxDeleteApplication.png
[sfx-create-app-instance]: ./media/service-fabric-visualizing-your-cluster/SfxCreateAppInstance.png
