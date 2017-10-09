---
title: aaaSet um cluster do Azure Service Fabric | Microsoft Docs
description: "Guia de início rápido - criar um cluster do Service Fabric do Windows ou Linux no Azure."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: ryanwi
ms.openlocfilehash: 13c60e293d19d607bb41ee4859706508c219a833
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-cluster-on-azure"></a><span data-ttu-id="e047a-103">Criar seu primeiro cluster do Service Fabric no Azure</span><span class="sxs-lookup"><span data-stu-id="e047a-103">Create your first Service Fabric cluster on Azure</span></span>
<span data-ttu-id="e047a-104">Um [cluster do Service Fabric](service-fabric-deploy-anywhere.md) é um conjunto de máquinas físicas ou virtuais conectadas em rede, no qual os microsserviços são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="e047a-104">A [Service Fabric cluster](service-fabric-deploy-anywhere.md) is a network-connected set of virtual or physical machines into which your microservices are deployed and managed.</span></span> <span data-ttu-id="e047a-105">Este guia de início rápido ajuda toocreate um cluster de cinco nós, em execução no Windows ou Linux, a saudação [Azure PowerShell](https://msdn.microsoft.com/library/dn135248) ou [portal do Azure](http://portal.azure.com) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="e047a-105">This quickstart helps you toocreate a five-node cluster, running on either Windows or Linux, through hello [Azure PowerShell](https://msdn.microsoft.com/library/dn135248) or [Azure portal](http://portal.azure.com) in just a few minutes.</span></span>  

<span data-ttu-id="e047a-106">Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="e047a-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>


## <a name="use-hello-azure-portal"></a><span data-ttu-id="e047a-107">Use Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e047a-107">Use hello Azure portal</span></span>

<span data-ttu-id="e047a-108">Faça logon no toohello portal do Azure em [http://portal.azure.com](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e047a-108">Log in toohello Azure portal at [http://portal.azure.com](http://portal.azure.com).</span></span>

### <a name="create-hello-cluster"></a><span data-ttu-id="e047a-109">Criar cluster Olá</span><span class="sxs-lookup"><span data-stu-id="e047a-109">Create hello cluster</span></span>

1. <span data-ttu-id="e047a-110">Clique em Olá **novo** botão localizado no canto superior esquerdo de saudação do hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e047a-110">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>
2. <span data-ttu-id="e047a-111">Selecione **de computação** de saudação **novo** folha e, em seguida, selecione **Cluster do Service Fabric** de saudação **de computação** folha.</span><span class="sxs-lookup"><span data-stu-id="e047a-111">Select **Compute** from hello **New** blade and then select **Service Fabric Cluster** from hello **Compute** blade.</span></span>
3. <span data-ttu-id="e047a-112">Preenchimento de saudação do Service Fabric **Noções básicas sobre** formulário.</span><span class="sxs-lookup"><span data-stu-id="e047a-112">Fill out hello Service Fabric **Basics** form.</span></span> <span data-ttu-id="e047a-113">Para **sistema operacional**, selecione a versão de saudação do Windows ou Linux que você deseja Olá toorun de nós de cluster.</span><span class="sxs-lookup"><span data-stu-id="e047a-113">For **Operating system**, select hello version of Windows or Linux you want hello cluster nodes toorun.</span></span> <span data-ttu-id="e047a-114">nome de usuário de saudação e a senha digitada aqui é toolog usada na máquina virtual de toohello.</span><span class="sxs-lookup"><span data-stu-id="e047a-114">hello user name and password entered here is used toolog in toohello virtual machine.</span></span> <span data-ttu-id="e047a-115">Para **Grupo de Recursos**, crie um novo.</span><span class="sxs-lookup"><span data-stu-id="e047a-115">For **Resource group**, create a new one.</span></span> <span data-ttu-id="e047a-116">Um grupo de recursos é um contêiner lógico no qual os recursos do Azure são criados e gerenciados coletivamente.</span><span class="sxs-lookup"><span data-stu-id="e047a-116">A resource group is a logical container into which Azure resources are created and collectively managed.</span></span> <span data-ttu-id="e047a-117">Ao concluir, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="e047a-117">When complete, click **OK**.</span></span>

    ![Saída da instalação do cluster][cluster-setup-basics]

4. <span data-ttu-id="e047a-119">Preencha Olá **configuração de Cluster** formulário.</span><span class="sxs-lookup"><span data-stu-id="e047a-119">Fill out hello **Cluster configuration** form.</span></span>  <span data-ttu-id="e047a-120">Em **Contagem do tipo de nó**, digite "1".</span><span class="sxs-lookup"><span data-stu-id="e047a-120">For **Node type count**, enter "1".</span></span>

5. <span data-ttu-id="e047a-121">Selecione **1 (primário) do tipo de nó** e o preenchimento Olá **configuração do tipo de nó** formulário.</span><span class="sxs-lookup"><span data-stu-id="e047a-121">Select **Node type 1 (Primary)** and fill out hello **Node type configuration** form.</span></span>  <span data-ttu-id="e047a-122">Insira um nome de tipo de nó e defina Olá [a camada de durabilidade](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) muito "Bronze".</span><span class="sxs-lookup"><span data-stu-id="e047a-122">Enter a node type name and set hello [Durability tier](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) too"Bronze."</span></span>  <span data-ttu-id="e047a-123">Selecione um tamanho de VM.</span><span class="sxs-lookup"><span data-stu-id="e047a-123">Select a VM size.</span></span>

    <span data-ttu-id="e047a-124">Tipos de nós definem tamanho da VM hello, número de VMs, pontos de extremidade personalizados e outras configurações para Olá VMs desse tipo.</span><span class="sxs-lookup"><span data-stu-id="e047a-124">Node types define hello VM size, number of VMs, custom endpoints, and other settings for hello VMs of that type.</span></span> <span data-ttu-id="e047a-125">Cada tipo de nó definido é configurado como um conjunto de escala de máquina virtual separada, que é usado toodeploy e máquinas virtuais gerenciadas como um conjunto.</span><span class="sxs-lookup"><span data-stu-id="e047a-125">Each node type defined is set up as a separate virtual machine scale set, which is used toodeploy and managed virtual machines as a set.</span></span> <span data-ttu-id="e047a-126">Cada tipo de nó pode ser dimensionado para cima ou para baixo de forma independente, tem conjuntos diferentes de portas abertas e pode ter métricas de capacidade diferentes.</span><span class="sxs-lookup"><span data-stu-id="e047a-126">Each node type can be scaled up or down independently, have different sets of ports open, and can have different capacity metrics.</span></span>  <span data-ttu-id="e047a-127">Olá primeiro ou primário, tipo de nó é onde os serviços do sistema do Service Fabric hospedados e devem ter cinco ou mais VMs.</span><span class="sxs-lookup"><span data-stu-id="e047a-127">hello first, or primary, node type is where Service Fabric system services are hosted and must have five or more VMs.</span></span>

    <span data-ttu-id="e047a-128">Para qualquer implantação de produção, o [planejamento da capacidade](service-fabric-cluster-capacity.md) é uma etapa importante.</span><span class="sxs-lookup"><span data-stu-id="e047a-128">For any production deployment, [capacity planning](service-fabric-cluster-capacity.md) is an important step.</span></span>  <span data-ttu-id="e047a-129">Para esse início rápido, no entanto, você não está executando aplicativos, portanto, escolha um tamanho de VM *DS1_v2 Padrão*.</span><span class="sxs-lookup"><span data-stu-id="e047a-129">For this quick start, however, you aren't running applications so select a *DS1_v2 Standard* VM size.</span></span>  <span data-ttu-id="e047a-130">Selecione "Prata" hello [camada de confiabilidade](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) e capacidade de 5 do conjunto de uma escala de inicial da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e047a-130">Select "Silver" for hello [reliability tier](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) and an initial virtual machine scale set capacity of 5.</span></span>  

    <span data-ttu-id="e047a-131">Pontos de extremidade personalizados abrem portas no balanceador de carga do Azure Olá para que você pode se conectar com aplicativos em execução no cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="e047a-131">Custom endpoints open up ports in hello Azure load balancer so that you can connect with applications running on hello cluster.</span></span>  <span data-ttu-id="e047a-132">Insira "80, 8172" tooopen as portas 80 e 8172.</span><span class="sxs-lookup"><span data-stu-id="e047a-132">Enter "80, 8172" tooopen up ports 80 and 8172.</span></span>

    <span data-ttu-id="e047a-133">Não verificar Olá **definir configurações avançadas** caixa, que é usada para personalizar os pontos de extremidade de gerenciamento de TCP/HTTP, intervalos de porta de aplicativo, [restrições de posicionamento](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints), e [capacidade propriedades](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="e047a-133">Do not check hello **Configure advanced settings** box, which is used for customizing TCP/HTTP management endpoints, application port ranges, [placement constraints](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints), and [capacity properties](service-fabric-cluster-resource-manager-metrics.md).</span></span>    

    <span data-ttu-id="e047a-134">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="e047a-134">Select **OK**.</span></span>

6. <span data-ttu-id="e047a-135">Em Olá **configuração de Cluster** formulário, defina **diagnóstico** muito**em**.</span><span class="sxs-lookup"><span data-stu-id="e047a-135">In hello **Cluster configuration** form, set **Diagnostics** too**On**.</span></span>  <span data-ttu-id="e047a-136">Para este guia de início rápido, você não precisa tooenter qualquer [configuração de malha](service-fabric-cluster-fabric-settings.md) propriedades.</span><span class="sxs-lookup"><span data-stu-id="e047a-136">For this quickstart, you do not need tooenter any [fabric setting](service-fabric-cluster-fabric-settings.md) properties.</span></span>  <span data-ttu-id="e047a-137">Em **versão do Fabric**, selecione **automáticas** modo de atualização para que a Microsoft atualiza automaticamente a versão de saudação do código-malha Olá executando Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="e047a-137">In **Fabric version**, select **Automatic** upgrade mode so that Microsoft automatically updates hello version of hello fabric code running hello cluster.</span></span>  <span data-ttu-id="e047a-138">Definir o modo de saudação muito**Manual** se você quiser muito[escolher uma versão com suporte](service-fabric-cluster-upgrade.md) tooupgrade para.</span><span class="sxs-lookup"><span data-stu-id="e047a-138">Set hello mode too**Manual** if you want too[choose a supported version](service-fabric-cluster-upgrade.md) tooupgrade to.</span></span> 

    ![Configuração do tipo de nó][node-type-config]

    <span data-ttu-id="e047a-140">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="e047a-140">Select **OK**.</span></span>

7. <span data-ttu-id="e047a-141">Preencha Olá **segurança** formulário.</span><span class="sxs-lookup"><span data-stu-id="e047a-141">Fill out hello **Security** form.</span></span>  <span data-ttu-id="e047a-142">Para esse início rápido, selecione **Não seguro**.</span><span class="sxs-lookup"><span data-stu-id="e047a-142">For this quick start select **Unsecure**.</span></span>  <span data-ttu-id="e047a-143">É altamente recomendável toocreate um cluster seguro para cargas de trabalho de produção, no entanto, já que qualquer pessoa pode conectar-se o cluster não segura tooan anonimamente e executar operações de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="e047a-143">It is highly recommended toocreate a secure cluster for production workloads, however, since anyone can anonymously connect tooan unsecure cluster and perform management operations.</span></span>  

    <span data-ttu-id="e047a-144">Os certificados são usados em Service Fabric tooprovide toosecure de autenticação e criptografia vários aspectos de um cluster e seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="e047a-144">Certificates are used in Service Fabric tooprovide authentication and encryption toosecure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="e047a-145">Para obter mais informações sobre como os certificados são usados no Service Fabric, consulte [Cenários de segurança do cluster do Service Fabric](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="e047a-145">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios](service-fabric-cluster-security.md).</span></span>  <span data-ttu-id="e047a-146">usando o Active Directory do Azure ou tooset certificados para segurança de aplicativo de autenticação de usuário tooenable [criar um cluster de um modelo do Gerenciador de recursos](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="e047a-146">tooenable user authentication using Azure Active Directory or tooset up certificates for application security, [create a cluster from a Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span>

    <span data-ttu-id="e047a-147">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="e047a-147">Select **OK**.</span></span>

8. <span data-ttu-id="e047a-148">Saudação de revisão resumida.</span><span class="sxs-lookup"><span data-stu-id="e047a-148">Review hello summary.</span></span>  <span data-ttu-id="e047a-149">Se você gostaria que toodownload um modelo do Gerenciador de recursos criado a partir de configurações de saudação inserido, selecione **baixar modelo e parâmetros de**.</span><span class="sxs-lookup"><span data-stu-id="e047a-149">If you'd like toodownload a Resource Manager template built from hello settings you entered, select **Download template and parameters**.</span></span>  <span data-ttu-id="e047a-150">Selecione **criar** toocreate cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="e047a-150">Select **Create** toocreate hello cluster.</span></span>

    <span data-ttu-id="e047a-151">Você pode ver o progresso da criação da saudação em notificações de saudação.</span><span class="sxs-lookup"><span data-stu-id="e047a-151">You can see hello creation progress in hello notifications.</span></span> <span data-ttu-id="e047a-152">(Clique ícone de sino"hello" próximo a barra de status de saudação do superior de saudação à direita da tela). Se você clicou **Pin tooStartboard** durante a criação de cluster hello, você verá **implantação de Cluster do Service Fabric** fixado toohello **iniciar** quadro.</span><span class="sxs-lookup"><span data-stu-id="e047a-152">(Click hello "Bell" icon near hello status bar at hello upper right of your screen.) If you clicked **Pin tooStartboard** while creating hello cluster, you see **Deploying Service Fabric Cluster** pinned toohello **Start** board.</span></span>

### <a name="view-cluster-status"></a><span data-ttu-id="e047a-153">Exibir o status do cluster</span><span class="sxs-lookup"><span data-stu-id="e047a-153">View cluster status</span></span>
<span data-ttu-id="e047a-154">Quando o cluster é criado, você pode inspecionar o seu cluster em Olá **visão geral** folha no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="e047a-154">Once your cluster is created, you can inspect your cluster in hello **Overview** blade in hello portal.</span></span> <span data-ttu-id="e047a-155">Agora você pode ver detalhes de saudação do cluster no painel hello, incluindo o ponto de extremidade do cluster Olá público e um link de tooService Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="e047a-155">You can now see hello details of your cluster in hello dashboard, including hello cluster's public endpoint and a link tooService Fabric Explorer.</span></span>

![Status do cluster][cluster-status]

### <a name="visualize-hello-cluster-using-service-fabric-explorer"></a><span data-ttu-id="e047a-157">Visualizar cluster hello usando o Gerenciador do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e047a-157">Visualize hello cluster using Service Fabric explorer</span></span>
<span data-ttu-id="e047a-158">O [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) é uma boa ferramenta para visualizar o cluster e gerenciar os aplicativos.</span><span class="sxs-lookup"><span data-stu-id="e047a-158">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a good tool for visualizing your cluster and managing applications.</span></span>  <span data-ttu-id="e047a-159">Gerenciador do Service Fabric é um serviço que é executado no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="e047a-159">Service Fabric Explorer is a service that runs in hello cluster.</span></span>  <span data-ttu-id="e047a-160">Acessá-lo usando um navegador da web clicando Olá **Service Fabric Explorer** link de cluster Olá **visão geral** página no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="e047a-160">Access it using a web browser by clicking hello **Service Fabric Explorer** link of hello cluster **Overview** page in hello portal.</span></span>  <span data-ttu-id="e047a-161">Você também pode inserir o endereço de saudação diretamente no navegador Olá: [http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)</span><span class="sxs-lookup"><span data-stu-id="e047a-161">You can also enter hello address directly into hello browser: [http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)</span></span>

<span data-ttu-id="e047a-162">painel do cluster Olá fornece uma visão geral do cluster, incluindo um resumo do aplicativo e a integridade do nó.</span><span class="sxs-lookup"><span data-stu-id="e047a-162">hello cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span> <span data-ttu-id="e047a-163">exibição do nó de saudação mostra o layout físico de saudação do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="e047a-163">hello node view shows hello physical layout of hello cluster.</span></span> <span data-ttu-id="e047a-164">Para um nó específico, você pode inspecionar quais aplicativos têm código implantado naquele nó.</span><span class="sxs-lookup"><span data-stu-id="e047a-164">For a given node, you can inspect which applications have code deployed on that node.</span></span>

![Service Fabric Explorer][service-fabric-explorer]

### <a name="connect-toohello-cluster-using-powershell"></a><span data-ttu-id="e047a-166">Conecte-se o cluster toohello usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="e047a-166">Connect toohello cluster using PowerShell</span></span>
<span data-ttu-id="e047a-167">Verifique se que esse cluster hello está em execução ao se conectar usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e047a-167">Verify that hello cluster is running by connecting using PowerShell.</span></span>  <span data-ttu-id="e047a-168">Olá ServiceFabric do PowerShell é instalado com o hello [SDK do Service Fabric](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e047a-168">hello ServiceFabric PowerShell module is installed with hello [Service Fabric SDK](service-fabric-get-started.md).</span></span>  <span data-ttu-id="e047a-169">Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet estabelece um cluster de toohello de conexão.</span><span class="sxs-lookup"><span data-stu-id="e047a-169">hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet establishes a connection toohello cluster.</span></span>   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint quickstartcluster.westus2.cloudapp.azure.com:19000
```
<span data-ttu-id="e047a-170">Consulte [conectar tooa segura cluster](service-fabric-connect-to-secure-cluster.md) para obter outros exemplos de cluster de tooa conexão.</span><span class="sxs-lookup"><span data-stu-id="e047a-170">See [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md) for other examples of connecting tooa cluster.</span></span> <span data-ttu-id="e047a-171">Depois de cluster toohello conexão, use Olá [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) toodisplay cmdlet uma lista de nós no hello cluster e informações de status para cada nó.</span><span class="sxs-lookup"><span data-stu-id="e047a-171">After connecting toohello cluster, use hello [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet toodisplay a list of nodes in hello cluster and status information for each node.</span></span> <span data-ttu-id="e047a-172">**HealthState** deve ser *OK* para cada nó.</span><span class="sxs-lookup"><span data-stu-id="e047a-172">**HealthState** should be *OK* for each node.</span></span>

```powershell
PS C:\Users\sfuser> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName     IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- --------     --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     _nodetype1_2 10.0.0.6        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_1 10.0.0.5        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_0 10.0.0.4        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_4 10.0.0.8        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_3 10.0.0.7        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
```

### <a name="remove-hello-cluster"></a><span data-ttu-id="e047a-173">Remover cluster Olá</span><span class="sxs-lookup"><span data-stu-id="e047a-173">Remove hello cluster</span></span>
<span data-ttu-id="e047a-174">Um cluster do Service Fabric é composto por outros recursos do Azure além de recurso de cluster toohello propriamente dito.</span><span class="sxs-lookup"><span data-stu-id="e047a-174">A Service Fabric cluster is made up of other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="e047a-175">Para toocompletely exclua um cluster do Service Fabric também é necessário toodelete que todos Olá recursos que é formado.</span><span class="sxs-lookup"><span data-stu-id="e047a-175">So toocompletely delete a Service Fabric cluster you also need toodelete all hello resources it is made of.</span></span> <span data-ttu-id="e047a-176">cluster do Hello mais simples maneira toodelete hello e todos os recursos de saudação consome é o grupo de recursos de saudação do toodelete.</span><span class="sxs-lookup"><span data-stu-id="e047a-176">hello simplest way toodelete hello cluster and all hello resources it consumes is toodelete hello resource group.</span></span> <span data-ttu-id="e047a-177">Para outros toodelete de maneiras que um cluster ou toodelete alguns (mas não todos) recursos de saudação em um grupo de recursos, consulte [excluir um cluster](service-fabric-cluster-delete.md)</span><span class="sxs-lookup"><span data-stu-id="e047a-177">For other ways toodelete a cluster or toodelete some (but not all) hello resources in a resource group, see [Delete a cluster](service-fabric-cluster-delete.md)</span></span>

<span data-ttu-id="e047a-178">Exclua um grupo de recursos em Olá portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="e047a-178">Delete a resource group in hello Azure portal:</span></span>
1. <span data-ttu-id="e047a-179">Navegue cluster do Service Fabric toohello toodelete desejado.</span><span class="sxs-lookup"><span data-stu-id="e047a-179">Navigate toohello Service Fabric cluster you want toodelete.</span></span>
2. <span data-ttu-id="e047a-180">Clique em Olá **grupo de recursos** nome na página de recursos básicos de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="e047a-180">Click hello **Resource Group** name on hello cluster essentials page.</span></span>
3. <span data-ttu-id="e047a-181">Em Olá **princípios básicos de grupo de recursos** , clique em **excluir grupo de recursos** e siga as instruções de saudação que página toocomplete Olá a exclusão do grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="e047a-181">In hello **Resource Group Essentials** page, click **Delete resource group** and follow hello instructions on that page toocomplete hello deletion of hello resource group.</span></span>
    <span data-ttu-id="e047a-182">![Excluir grupo de recursos de saudação][cluster-delete]</span><span class="sxs-lookup"><span data-stu-id="e047a-182">![Delete hello resource group][cluster-delete]</span></span>


## <a name="use-azure-powershell-toodeploy-a-secure-cluster"></a><span data-ttu-id="e047a-183">Usar o Azure Powershell toodeploy um cluster seguro</span><span class="sxs-lookup"><span data-stu-id="e047a-183">Use Azure Powershell toodeploy a secure cluster</span></span>
1. <span data-ttu-id="e047a-184">Baixar Olá [Azure Powershell versão 4.0 ou superior do módulo](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) em seu computador.</span><span class="sxs-lookup"><span data-stu-id="e047a-184">Download hello [Azure Powershell module version 4.0 or higher](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) on your machine.</span></span>

2. <span data-ttu-id="e047a-185">Abra uma janela do Windows PowerShell, Olá executar comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="e047a-185">Open a Windows PowerShell window, Run hello following command.</span></span> 
    
    ```powershell

    Get-Command -Module AzureRM.ServiceFabric 
    ```

    <span data-ttu-id="e047a-186">Você verá uma saída semelhante toohello a seguir.</span><span class="sxs-lookup"><span data-stu-id="e047a-186">You should see an output similar toohello following.</span></span>

    ![ps-list][ps-list]

3. <span data-ttu-id="e047a-188">Logon tooAzure e selecione Olá assinatura toowhich toocreate Olá pelo cluster</span><span class="sxs-lookup"><span data-stu-id="e047a-188">Login tooAzure and Select hello subscription toowhich you want toocreate hello cluster</span></span>

    ```powershell

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionId "Subcription ID" 
    ```

4. <span data-ttu-id="e047a-189">Olá execução toonow de comando a seguir criar um cluster seguro.</span><span class="sxs-lookup"><span data-stu-id="e047a-189">Run hello following command toonow create a secure cluster.</span></span> <span data-ttu-id="e047a-190">Não se esqueça de parâmetros de saudação toocustomize.</span><span class="sxs-lookup"><span data-stu-id="e047a-190">Do not forget toocustomize hello parameters.</span></span> 

    ```powershell
    $certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
    $RDPpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force 
    $RDPuser="vmadmin"
    $RGname="mycluster" # this is also hello name of your cluster
    $clusterloc="SouthCentralUS"
    $subname="$RGname.$clusterloc.cloudapp.azure.com"
    $certfolder="c:\mycertificates\"
    $clustersize=1 # can take values 1, 3-99

    New-AzureRmServiceFabricCluster -ResourceGroupName $RGname -Location $clusterloc -ClusterSize $clustersize -VmUserName $RDPuser -VmPassword $RDPpwd -CertificateSubjectName $subname -CertificatePassword $certpwd -CertificateOutputFolder $certfolder
    ```

    <span data-ttu-id="e047a-191">comando Olá pode levar de 10 minutos too30 minutos toocomplete, no final de saudação do mesmo, você deve obter uma saída semelhante toohello a seguir.</span><span class="sxs-lookup"><span data-stu-id="e047a-191">hello command can take anywhere from 10 minutes too30 minutes toocomplete, at hello end of it, you should get an output similar toohello following.</span></span> <span data-ttu-id="e047a-192">saída de Hello tem informações sobre o certificado hello, Olá KeyVault onde ele foi carregado, e Olá pasta local em que o certificado de saudação é copiado.</span><span class="sxs-lookup"><span data-stu-id="e047a-192">hello output has information about hello certificate, hello KeyVault where it was uploaded to, and hello local folder where hello certificate is copied.</span></span> 

    ![ps-out][ps-out]

5. <span data-ttu-id="e047a-194">Copiar saída inteiro hello e salvar o arquivo de texto tooa conforme necessário toorefer tooit.</span><span class="sxs-lookup"><span data-stu-id="e047a-194">Copy hello entire output and save tooa text file as we need toorefer tooit.</span></span> <span data-ttu-id="e047a-195">Anote Olá informações a seguir da saída de hello.</span><span class="sxs-lookup"><span data-stu-id="e047a-195">Make a note of hello following information from hello output.</span></span> 

    - <span data-ttu-id="e047a-196">**CertificateSavedLocalPath** : c:\mycertificates\mycluster20170504141137.pfx</span><span class="sxs-lookup"><span data-stu-id="e047a-196">**CertificateSavedLocalPath** : c:\mycertificates\mycluster20170504141137.pfx</span></span>
    - <span data-ttu-id="e047a-197">**CertificateThumbprint** : C4C1E541AD512B8065280292A8BA6079C3F26F10</span><span class="sxs-lookup"><span data-stu-id="e047a-197">**CertificateThumbprint** : C4C1E541AD512B8065280292A8BA6079C3F26F10</span></span>
    - <span data-ttu-id="e047a-198">**ManagementEndpoint** : https://mycluster.southcentralus.cloudapp.azure.com:19080</span><span class="sxs-lookup"><span data-stu-id="e047a-198">**ManagementEndpoint** : https://mycluster.southcentralus.cloudapp.azure.com:19080</span></span>
    - <span data-ttu-id="e047a-199">**ClientConnectionEndpointPort** : 19000</span><span class="sxs-lookup"><span data-stu-id="e047a-199">**ClientConnectionEndpointPort** : 19000</span></span>

### <a name="install-hello-certificate-on-your-local-machine"></a><span data-ttu-id="e047a-200">Instalar o certificado de saudação em seu computador local</span><span class="sxs-lookup"><span data-stu-id="e047a-200">Install hello certificate on your local machine</span></span>
  
<span data-ttu-id="e047a-201">tooconnect toohello cluster, você precisa de tooinstall Olá certificado no repositório de pessoal (Meu) de saudação do usuário atual Olá.</span><span class="sxs-lookup"><span data-stu-id="e047a-201">tooconnect toohello cluster, you need tooinstall hello certificate into hello Personal (My) store of hello current user.</span></span> 

<span data-ttu-id="e047a-202">Saudação de execução do PowerShell a seguir</span><span class="sxs-lookup"><span data-stu-id="e047a-202">Run hello following PowerShell</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\hello name of hello cert.pfx `
        -Password (ConvertTo-SecureString -String certpwd -AsPlainText -Force)
```

<span data-ttu-id="e047a-203">Agora você está pronto tooconnect tooyour segura cluster.</span><span class="sxs-lookup"><span data-stu-id="e047a-203">You are now ready tooconnect tooyour secure cluster.</span></span>

### <a name="connect-tooa-secure-cluster"></a><span data-ttu-id="e047a-204">Conecte-se o cluster seguro tooa</span><span class="sxs-lookup"><span data-stu-id="e047a-204">Connect tooa secure cluster</span></span> 

<span data-ttu-id="e047a-205">Execute Olá cluster seguro do PowerShell comando tooconnect tooa a seguir.</span><span class="sxs-lookup"><span data-stu-id="e047a-205">Run hello following PowerShell command tooconnect tooa secure cluster.</span></span> <span data-ttu-id="e047a-206">detalhes do certificado Olá devem corresponder a um certificado que foi usado tooset cluster hello.</span><span class="sxs-lookup"><span data-stu-id="e047a-206">hello certificate details must match a certificate that was used tooset up hello cluster.</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```


<span data-ttu-id="e047a-207">Olá Olá do exemplo mostra a seguir concluída parâmetros:</span><span class="sxs-lookup"><span data-stu-id="e047a-207">hello following example shows hello completed parameters:</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mycluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="e047a-208">Execute Olá toocheck de comando que você está conectado a seguir e Olá cluster está íntegro.</span><span class="sxs-lookup"><span data-stu-id="e047a-208">Run hello following command toocheck that you are connected and hello cluster is healthy.</span></span>

```powershell

Get-ServiceFabricClusterHealth

```
### <a name="publish-your-apps-tooyour-cluster-from-visual-studio"></a><span data-ttu-id="e047a-209">Publicar seu cluster tooyour de aplicativos do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e047a-209">Publish your apps tooyour cluster from Visual Studio</span></span>

<span data-ttu-id="e047a-210">Agora que você configurou um cluster do Azure, você pode publicar seu tooit de aplicativos do Visual Studio pelo seguinte Olá [publicar tooan cluster](service-fabric-publish-app-remote-cluster.md) documento.</span><span class="sxs-lookup"><span data-stu-id="e047a-210">Now that you have set up an Azure cluster, you can publish your applications tooit from Visual Studio by following hello [Publish tooan cluster](service-fabric-publish-app-remote-cluster.md) document.</span></span> 

### <a name="remove-hello-cluster"></a><span data-ttu-id="e047a-211">Remover cluster Olá</span><span class="sxs-lookup"><span data-stu-id="e047a-211">Remove hello cluster</span></span>
<span data-ttu-id="e047a-212">Um cluster é composto por outros recursos do Azure além de recurso de cluster toohello propriamente dito.</span><span class="sxs-lookup"><span data-stu-id="e047a-212">A cluster is made up of other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="e047a-213">cluster do Hello mais simples maneira toodelete hello e todos os recursos de saudação consome é o grupo de recursos de saudação do toodelete.</span><span class="sxs-lookup"><span data-stu-id="e047a-213">hello simplest way toodelete hello cluster and all hello resources it consumes is toodelete hello resource group.</span></span> 

```powershell

Remove-AzureRmResourceGroup -Name $RGname -Force

```

## <a name="next-steps"></a><span data-ttu-id="e047a-214">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e047a-214">Next steps</span></span>
<span data-ttu-id="e047a-215">Agora que você configurou um cluster de desenvolvimento, tente o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="e047a-215">Now that you have set up a development cluster, try hello following:</span></span>
* [<span data-ttu-id="e047a-216">Criar um cluster seguro no portal de saudação</span><span class="sxs-lookup"><span data-stu-id="e047a-216">Create a secure cluster in hello portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="e047a-217">Criar um cluster a partir de um modelo</span><span class="sxs-lookup"><span data-stu-id="e047a-217">Create a cluster from a template</span></span>](service-fabric-cluster-creation-via-arm.md) 
* [<span data-ttu-id="e047a-218">Implantar aplicativos usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="e047a-218">Deploy apps using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)


[cluster-setup-basics]: ./media/service-fabric-get-started-azure-cluster/basics.png
[node-type-config]: ./media/service-fabric-get-started-azure-cluster/nodetypeconfig.png
[cluster-status]: ./media/service-fabric-get-started-azure-cluster/clusterstatus.png
[service-fabric-explorer]: ./media/service-fabric-get-started-azure-cluster/sfx.png
[cluster-delete]: ./media/service-fabric-get-started-azure-cluster/delete.png
[ps-list]: ./media/service-fabric-get-started-azure-cluster/pslist.PNG
[ps-out]: ./media/service-fabric-get-started-azure-cluster/psout.PNG
