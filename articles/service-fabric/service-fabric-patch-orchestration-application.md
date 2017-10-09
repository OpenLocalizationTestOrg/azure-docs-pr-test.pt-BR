---
title: "aaaAzure aplicativo de orquestração de patch do Service Fabric | Microsoft Docs"
description: Tooautomate aplicativo operacional patches do sistema em um cluster do Service Fabric.
services: service-fabric
documentationcenter: .net
author: novino
manager: timlt
editor: 
ms.assetid: de7dacf5-4038-434a-a265-5d0de80a9b1d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/9/2017
ms.author: nachandr
ms.openlocfilehash: fbb89aa2ea418181ee908a01850178c113c462fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="patch-hello-windows-operating-system-in-your-service-fabric-cluster"></a><span data-ttu-id="d7c4a-103">Patch do sistema de operacional do Windows hello no cluster do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d7c4a-103">Patch hello Windows operating system in your Service Fabric cluster</span></span>

<span data-ttu-id="d7c4a-104">aplicativo de orquestração de patch Hello é um aplicativo do Azure Service Fabric que automatiza o sistema operacional a aplicação de patch em um cluster do Service Fabric no Azure sem tempo de inatividade.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-104">hello patch orchestration application is an Azure Service Fabric application that automates operating system patching on a Service Fabric cluster on Azure without downtime.</span></span>

<span data-ttu-id="d7c4a-105">Olá patch orquestração aplicativo fornece a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="d7c4a-105">hello patch orchestration app provides hello following:</span></span>

- <span data-ttu-id="d7c4a-106">**Instalação da atualização automática do sistema operacional**.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-106">**Automatic operating system update installation**.</span></span> <span data-ttu-id="d7c4a-107">Atualizações do sistema operacional são baixadas e instaladas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-107">Operating system updates are automatically downloaded and installed.</span></span> <span data-ttu-id="d7c4a-108">Nós de cluster são reiniciados conforme necessário, sem tempo de inatividade do cluster.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-108">Cluster nodes are rebooted as needed without cluster downtime.</span></span>

- <span data-ttu-id="d7c4a-109">**Aplicação de patch com suporte a cluster e integração de integridade**.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-109">**Cluster-aware patching and health integration**.</span></span> <span data-ttu-id="d7c4a-110">Durante a aplicação de atualizações, Olá patch orquestração aplicativo monitora a integridade de Olá Olá de nós de cluster.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-110">While applying updates, hello patch orchestration app monitors hello health of hello cluster nodes.</span></span> <span data-ttu-id="d7c4a-111">Os nós de cluster fazem upgrade de um nó ou um domínio de atualização por vez.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-111">Cluster nodes are upgraded one node at a time or one upgrade domain at a time.</span></span> <span data-ttu-id="d7c4a-112">Se a integridade de saudação do cluster Olá falhar devido a processo de aplicação de patch toohello, aplicação de patch é interrompido tooprevent aggravating problema hello.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-112">If hello health of hello cluster goes down due toohello patching process, patching is stopped tooprevent aggravating hello problem.</span></span>

## <a name="internal-details-of-hello-app"></a><span data-ttu-id="d7c4a-113">Detalhes internos de aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="d7c4a-113">Internal details of hello app</span></span>

<span data-ttu-id="d7c4a-114">aplicativo de orquestração de patch Olá é composto de saudação subcomponentes a seguir:</span><span class="sxs-lookup"><span data-stu-id="d7c4a-114">hello patch orchestration app is composed of hello following subcomponents:</span></span>

- <span data-ttu-id="d7c4a-115">**Serviço de Coordenador**: este serviço com estado é responsável por:</span><span class="sxs-lookup"><span data-stu-id="d7c4a-115">**Coordinator Service**: This stateful service is responsible for:</span></span>
    - <span data-ttu-id="d7c4a-116">Coordenar o trabalho de atualização do Windows hello em todo o cluster hello.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-116">Coordinating hello Windows Update job on hello entire cluster.</span></span>
    - <span data-ttu-id="d7c4a-117">Armazena o resultado de saudação das operações concluídas do Windows Update.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-117">Storing hello result of completed Windows Update operations.</span></span>
- <span data-ttu-id="d7c4a-118">**Serviço de Agente do Nó**: é um serviço sem estado, executado em todos os nós de cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-118">**Node Agent Service**: This stateless service runs on all Service Fabric cluster nodes.</span></span> <span data-ttu-id="d7c4a-119">serviço de saudação é responsável por:</span><span class="sxs-lookup"><span data-stu-id="d7c4a-119">hello service is responsible for:</span></span>
    - <span data-ttu-id="d7c4a-120">Olá NTService de agente do nó de inicialização.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-120">Bootstrapping hello Node Agent NTService.</span></span>
    - <span data-ttu-id="d7c4a-121">Olá NTService do nó do agente de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-121">Monitoring hello Node Agent NTService.</span></span>
- <span data-ttu-id="d7c4a-122">**NTService do Agente do Nó**: este serviço Windows NT é executado em um privilégio de nível superior (SISTEMA).</span><span class="sxs-lookup"><span data-stu-id="d7c4a-122">**Node Agent NTService**: This Windows NT service runs at a higher-level privilege (SYSTEM).</span></span> <span data-ttu-id="d7c4a-123">Por outro lado, Olá nó serviço de agente e hello serviço Coordenador de execute em um nível mais baixo de privilégio (serviço de rede).</span><span class="sxs-lookup"><span data-stu-id="d7c4a-123">In contrast, hello Node Agent Service and hello Coordinator Service run at a lower-level privilege (NETWORK SERVICE).</span></span> <span data-ttu-id="d7c4a-124">serviço de saudação é responsável pela execução Olá trabalhos de atualização do Windows a seguir em todos os nós de cluster hello:</span><span class="sxs-lookup"><span data-stu-id="d7c4a-124">hello service is responsible for performing hello following Windows Update jobs on all hello cluster nodes:</span></span>
    - <span data-ttu-id="d7c4a-125">Desabilitar atualização automática do Windows no nó de saudação.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-125">Disabling automatic Windows Update on hello node.</span></span>
    - <span data-ttu-id="d7c4a-126">Baixando e instalando o Windows Update de acordo com o usuário de saudação do toohello política foi fornecido.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-126">Downloading and installing Windows Update according toohello policy hello user has provided.</span></span>
    - <span data-ttu-id="d7c4a-127">Postagem de máquina Olá reiniciar a instalação do Windows Update.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-127">Restarting hello machine post Windows Update installation.</span></span>
    - <span data-ttu-id="d7c4a-128">Carregando resultados de saudação do toohello de atualizações do Windows o serviço de coordenador.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-128">Uploading hello results of Windows updates toohello Coordinator Service.</span></span>
    - <span data-ttu-id="d7c4a-129">Relatórios de integridade de relatórios no caso de falha na operação após esgotar todas as novas tentativas.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-129">Reporting health reports in case an operation has failed after exhausting all retries.</span></span>

> [!NOTE]
> <span data-ttu-id="d7c4a-130">Olá patch orquestração aplicativo usa Olá Service Fabric reparar toodisable de serviço de sistema do Gerenciador ou habilitar nó hello e realiza verificações de integridade.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-130">hello patch orchestration app uses hello Service Fabric repair manager system service toodisable or enable hello node and perform health checks.</span></span> <span data-ttu-id="d7c4a-131">tarefa de reparo do Hello criada pelo Olá Olá patch orquestração aplicativo rastreia andamento da atualização do Windows para cada nó.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-131">hello repair task created by hello patch orchestration app tracks hello Windows Update progress for each node.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d7c4a-132">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d7c4a-132">Prerequisites</span></span>

### <a name="minimum-supported-service-fabric-runtime-version"></a><span data-ttu-id="d7c4a-133">Versão de tempo de execução do Service Fabric com suporte mínimo</span><span class="sxs-lookup"><span data-stu-id="d7c4a-133">Minimum supported Service Fabric runtime version</span></span>

#### <a name="azure-clusters"></a><span data-ttu-id="d7c4a-134">Clusters do Azure</span><span class="sxs-lookup"><span data-stu-id="d7c4a-134">Azure clusters</span></span>
<span data-ttu-id="d7c4a-135">Olá patch orquestração aplicativo deve ser executado no Azure clusters que têm v 5.5 do Service Fabric runtime versão ou posterior.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-135">hello patch orchestration app must be run on Azure clusters that have Service Fabric runtime version v5.5 or later.</span></span>

#### <a name="standalone-on-premises-clusters"></a><span data-ttu-id="d7c4a-136">Clusters locais autônomos</span><span class="sxs-lookup"><span data-stu-id="d7c4a-136">Standalone on-premises Clusters</span></span>
<span data-ttu-id="d7c4a-137">Olá patch orquestração aplicativo deve ser executado em clusters autônomo com v 5.6 de versão de tempo de execução do Service Fabric ou posterior.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-137">hello patch orchestration app must be run on Standalone clusters that have Service Fabric runtime version v5.6 or later.</span></span>

### <a name="enable-hello-repair-manager-service-if-its-not-running-already"></a><span data-ttu-id="d7c4a-138">Habilitar o serviço de Gerenciador de reparo do hello (se ele não está funcionando)</span><span class="sxs-lookup"><span data-stu-id="d7c4a-138">Enable hello repair manager service (if it's not running already)</span></span>

<span data-ttu-id="d7c4a-139">Olá patch orquestração aplicativo requer Olá reparo manager sistema serviço toobe habilitada no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-139">hello patch orchestration app requires hello repair manager system service toobe enabled on hello cluster.</span></span>

#### <a name="azure-clusters"></a><span data-ttu-id="d7c4a-140">Clusters do Azure</span><span class="sxs-lookup"><span data-stu-id="d7c4a-140">Azure clusters</span></span>

<span data-ttu-id="d7c4a-141">Clusters do Azure na camada de durabilidade prata Olá tem Olá reparar service manager habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-141">Azure clusters in hello silver durability tier have hello repair manager service enabled by default.</span></span> <span data-ttu-id="d7c4a-142">Clusters do Azure na camada de durabilidade gold Olá podem ou não podem ter o serviço de Gerenciador de reparo do hello habilitado, dependendo de quando os clusters foram criados.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-142">Azure clusters in hello gold durability tier might or might not have hello repair manager service enabled, depending on when those clusters were created.</span></span> <span data-ttu-id="d7c4a-143">Clusters do Azure na camada de durabilidade bronze hello, por padrão, não têm Olá reparar service manager habilitado.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-143">Azure clusters in hello bronze durability tier, by default, do not have hello repair manager service enabled.</span></span> <span data-ttu-id="d7c4a-144">Se o serviço de saudação já estiver habilitado, você pode ver em execução na seção de serviços de sistema Olá em Olá Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-144">If hello service is already enabled, you can see it running in hello system services section in hello Service Fabric Explorer.</span></span>

##### <a name="azure-portal"></a><span data-ttu-id="d7c4a-145">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d7c4a-145">Azure portal</span></span>
<span data-ttu-id="d7c4a-146">Você pode habilitar o Gerenciador de reparo do portal do Azure em tempo de saudação de configuração de cluster.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-146">You can enable repair manager from Azure portal at hello time of setting up of cluster.</span></span> <span data-ttu-id="d7c4a-147">Selecione `Include Repair Manager` opção em `Add on features` no tempo de saudação da configuração de Cluster.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-147">Select `Include Repair Manager` option under `Add on features` at hello time of Cluster configuration.</span></span>
<span data-ttu-id="d7c4a-148">![Imagem do Gerenciador de reparo de habilitação do portal do Azure](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)</span><span class="sxs-lookup"><span data-stu-id="d7c4a-148">![Image of Enabling Repair Manager from Azure portal](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)</span></span>

##### <a name="azure-resource-manager-template"></a><span data-ttu-id="d7c4a-149">Modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d7c4a-149">Azure Resource Manager template</span></span>
<span data-ttu-id="d7c4a-150">Como alternativa, você pode usar Olá [modelo do Azure Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) serviço de Gerenciador de reparo tooenable Olá em clusters de malha de serviço novos e existentes.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-150">Alternatively you can use hello [Azure Resource Manager template](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) tooenable hello repair manager service on new and existing Service Fabric clusters.</span></span> <span data-ttu-id="d7c4a-151">Obter modelo Olá cluster Olá que você deseja toodeploy.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-151">Get hello template for hello cluster that you want toodeploy.</span></span> <span data-ttu-id="d7c4a-152">Você pode usar modelos de exemplo hello ou criar um modelo personalizado do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-152">You can either use hello sample templates or create a custom Resource Manager template.</span></span> 

<span data-ttu-id="d7c4a-153">serviço tooenable Olá reparo Gerenciador usando [modelo do Azure Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):</span><span class="sxs-lookup"><span data-stu-id="d7c4a-153">tooenable hello repair manager service using [Azure Resource Manager template](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):</span></span>

1. <span data-ttu-id="d7c4a-154">Primeiro, verifique que Olá `apiversion` está definido muito`2017-07-01-preview` para Olá `Microsoft.ServiceFabric/clusters` recurso, conforme mostrado no hello trecho de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-154">First check that hello `apiversion` is set too`2017-07-01-preview` for hello `Microsoft.ServiceFabric/clusters` resource, as shown in hello following snippet.</span></span> <span data-ttu-id="d7c4a-155">Se ele for diferente, você precisará Olá tooupdate `apiVersion` toohello valor `2017-07-01-preview`:</span><span class="sxs-lookup"><span data-stu-id="d7c4a-155">If it is different, then you need tooupdate hello `apiVersion` toohello value `2017-07-01-preview`:</span></span>

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. <span data-ttu-id="d7c4a-156">Agora habilitar o serviço de Gerenciador de reparo do hello adicionando Olá seguintes `addonFeatures` seção após Olá `fabricSettings` seção:</span><span class="sxs-lookup"><span data-stu-id="d7c4a-156">Now enable hello repair manager service by adding hello following `addonFeatures` section after hello `fabricSettings` section:</span></span>

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. <span data-ttu-id="d7c4a-157">Depois de atualizar o modelo de cluster com essas alterações, aplicá-las e que a atualização de saudação concluir.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-157">After you have updated your cluster template with these changes, apply them and let hello upgrade finish.</span></span> <span data-ttu-id="d7c4a-158">Agora você pode ver o serviço do sistema Olá reparo manager em execução no cluster.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-158">You can now see hello repair manager system service running in your cluster.</span></span> <span data-ttu-id="d7c4a-159">Ele é chamado `fabric:/System/RepairManagerService` na seção de serviços de sistema Olá em Olá Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-159">It is called `fabric:/System/RepairManagerService` in hello system services section in hello Service Fabric Explorer.</span></span> 

### <a name="standalone-on-premises-clusters"></a><span data-ttu-id="d7c4a-160">Clusters locais autônomos</span><span class="sxs-lookup"><span data-stu-id="d7c4a-160">Standalone on-premises clusters</span></span>

<span data-ttu-id="d7c4a-161">Você pode usar o hello [definições de configuração para o cluster do Windows autônoma](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) serviço de Gerenciador de reparo tooenable Olá no cluster do Service Fabric novo e existente.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-161">You can use hello [Configuration settings for standalone Windows cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) tooenable hello repair manager service on new and existing Service Fabric cluster.</span></span>

<span data-ttu-id="d7c4a-162">serviço de Gerenciador de reparo do hello tooenable:</span><span class="sxs-lookup"><span data-stu-id="d7c4a-162">tooenable hello repair manager service:</span></span>

1. <span data-ttu-id="d7c4a-163">Primeiro, verifique que Olá `apiversion` na [configurações de cluster geral](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) está definido muito`04-2017` ou superior:</span><span class="sxs-lookup"><span data-stu-id="d7c4a-163">First check that hello `apiversion` in [General cluster configurations](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) is set too`04-2017` or higher:</span></span>

    ```json
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "04-2017",
        ...
    }
    ```

2. <span data-ttu-id="d7c4a-164">Agora ativar o serviço de Gerenciador de reparo adicionando Olá seguintes `addonFeaturres` seção após Olá `fabricSettings` seção conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="d7c4a-164">Now enable repair manager service by adding hello following `addonFeaturres` section after hello `fabricSettings` section as shown below:</span></span>

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. <span data-ttu-id="d7c4a-165">Atualizar o manifesto do cluster com essas alterações, usando o manifesto do cluster Olá atualizado [criar um novo cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) ou [configuração de cluster de atualização Olá](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration).</span><span class="sxs-lookup"><span data-stu-id="d7c4a-165">Update your cluster manifest with these changes, using hello updated cluster manifest [create a new cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) or [upgrade hello cluster configuration](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration).</span></span> <span data-ttu-id="d7c4a-166">Depois que o cluster hello está sendo executado com o manifesto de cluster atualizado, agora você pode ver em execução no seu cluster, que é chamado de serviço do sistema Olá reparo Gerenciador `fabric:/System/RepairManagerService`, em serviços de sistema seção no Gerenciador do Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-166">Once hello cluster is running with updated cluster manifest, you can now see hello repair manager system service running in your cluster, which is called `fabric:/System/RepairManagerService`, under system services section in hello Service Fabric explorer.</span></span>

### <a name="disable-automatic-windows-update-on-all-nodes"></a><span data-ttu-id="d7c4a-167">Desabilite o Windows Update automático em todos os nós</span><span class="sxs-lookup"><span data-stu-id="d7c4a-167">Disable automatic Windows Update on all nodes</span></span>

<span data-ttu-id="d7c4a-168">Atualizações automáticas do Windows podem causar perda de tooavailability porque vários nós de cluster podem reiniciar Olá mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-168">Automatic Windows updates might lead tooavailability loss because multiple cluster nodes can restart at hello same time.</span></span> <span data-ttu-id="d7c4a-169">aplicativo de orquestração de patch Hello, por padrão, as tentativas toodisable Olá atualização automática do Windows em cada nó de cluster.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-169">hello patch orchestration app, by default, tries toodisable hello automatic Windows Update on each cluster node.</span></span> <span data-ttu-id="d7c4a-170">No entanto, se as configurações de saudação são gerenciadas por um administrador ou a diretiva de grupo, é recomendável Olá configuração Windows Update política muito "notificar antes de baixar" explicitamente.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-170">However, if hello settings are managed by an administrator or group policy, we recommend setting hello Windows Update policy too“Notify before Download” explicitly.</span></span>

### <a name="optional-enable-azure-diagnostics"></a><span data-ttu-id="d7c4a-171">Opcional: habilitar o Diagnóstico do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="d7c4a-171">Optional: Enable Azure Diagnostics</span></span>

<span data-ttu-id="d7c4a-172">Clusters que executam a versão de tempo de execução do Service Fabric `5.6.220.9494` e acima de logs de aplicativo de orquestração patch coletar como parte da malha do serviço de logs.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-172">Clusters running Service Fabric runtime version `5.6.220.9494` and above collect patch orchestration app logs as part of Service Fabric logs.</span></span>
<span data-ttu-id="d7c4a-173">Você pode ignorar esta etapa se o cluster está em execução na versão de tempo de execução do Service Fabric `5.6.220.9494` e acima.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-173">You can skip this step if your cluster is running on Service Fabric runtime version `5.6.220.9494` and above.</span></span>

<span data-ttu-id="d7c4a-174">Para clusters que executam a versão de tempo de execução do Service Fabric menor `5.6.220.9494`, logs do aplicativo de orquestração de patch Olá são coletados localmente em cada um de nós de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-174">For clusters running Service Fabric runtime version less than `5.6.220.9494`, logs for hello patch orchestration app are collected locally on each of hello cluster nodes.</span></span>
<span data-ttu-id="d7c4a-175">É recomendável que você configurar logs de tooupload de diagnóstico do Azure de todos os local central tooa de nós.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-175">We recommend that you configure Azure Diagnostics tooupload logs from all nodes tooa central location.</span></span>

<span data-ttu-id="d7c4a-176">Para obter mais informações sobre o Diagnóstico do Microsoft Azure, consulte [Coletar logs usando o Diagnóstico do Microsoft Azure](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad).</span><span class="sxs-lookup"><span data-stu-id="d7c4a-176">For information on enabling Azure Diagnostics, see [Collect logs by using Azure Diagnostics](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad).</span></span>

<span data-ttu-id="d7c4a-177">Logs do aplicativo de orquestração de patch Olá são gerados no hello provedor fixa IDs a seguir:</span><span class="sxs-lookup"><span data-stu-id="d7c4a-177">Logs for hello patch orchestration app are generated on hello following fixed provider IDs:</span></span>

- <span data-ttu-id="d7c4a-178">e39b723c-590c-4090-abb0-11e3e6616346</span><span class="sxs-lookup"><span data-stu-id="d7c4a-178">e39b723c-590c-4090-abb0-11e3e6616346</span></span>
- <span data-ttu-id="d7c4a-179">fc0028ff-bfdc-499f-80dc-ed922c52c5e9</span><span class="sxs-lookup"><span data-stu-id="d7c4a-179">fc0028ff-bfdc-499f-80dc-ed922c52c5e9</span></span>
- <span data-ttu-id="d7c4a-180">24afa313-0d3b-4c7c-b485-1047fd964b60</span><span class="sxs-lookup"><span data-stu-id="d7c4a-180">24afa313-0d3b-4c7c-b485-1047fd964b60</span></span>
- <span data-ttu-id="d7c4a-181">05dc046c-60e9-4ef7-965e-91660adffa68</span><span class="sxs-lookup"><span data-stu-id="d7c4a-181">05dc046c-60e9-4ef7-965e-91660adffa68</span></span>

<span data-ttu-id="d7c4a-182">No Gerenciador de recursos modelo goto `EtwEventSourceProviderConfiguration` seção em `WadCfg` e adicione Olá entradas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d7c4a-182">In Resource Manager template goto `EtwEventSourceProviderConfiguration` section under `WadCfg` and add hello following entries:</span></span>

```json
  {
    "provider": "e39b723c-590c-4090-abb0-11e3e6616346",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
      "eventDestination": "PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "fc0028ff-bfdc-499f-80dc-ed922c52c5e9",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "24afa313-0d3b-4c7c-b485-1047fd964b60",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "05dc046c-60e9-4ef7-965e-91660adffa68",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  }
```

> [!NOTE]
> <span data-ttu-id="d7c4a-183">Se o cluster do Service Fabric tem vários tipos de nó, seção anterior Olá deve ser adicionada para Olá todos os `WadCfg` seções.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-183">If your Service Fabric cluster has multiple node types, then hello previous section must be added for all hello `WadCfg` sections.</span></span>

## <a name="download-hello-app-package"></a><span data-ttu-id="d7c4a-184">Baixe o pacote do aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="d7c4a-184">Download hello app package</span></span>

<span data-ttu-id="d7c4a-185">Baixar o aplicativo hello da saudação [link de download](https://go.microsoft.com/fwlink/P/?linkid=849590).</span><span class="sxs-lookup"><span data-stu-id="d7c4a-185">Download hello application from hello [download link](https://go.microsoft.com/fwlink/P/?linkid=849590).</span></span>

## <a name="configure-hello-app"></a><span data-ttu-id="d7c4a-186">Configurar aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="d7c4a-186">Configure hello app</span></span>

<span data-ttu-id="d7c4a-187">Olá o comportamento do aplicativo de orquestração de patch Olá pode ser configurado toomeet suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-187">hello behavior of hello patch orchestration app can be configured toomeet your needs.</span></span> <span data-ttu-id="d7c4a-188">Substitua valores de padrão de saudação pela passagem de parâmetro de saudação do aplicativo durante a criação do aplicativo ou atualização.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-188">Override hello default values by passing in hello application parameter during application creation or update.</span></span> <span data-ttu-id="d7c4a-189">Parâmetros do aplicativo podem ser fornecidos especificando `ApplicationParameter` toohello `Start-ServiceFabricApplicationUpgrade` ou `New-ServiceFabricApplication` cmdlets.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-189">Application parameters can be provided by specifying `ApplicationParameter` toohello `Start-ServiceFabricApplicationUpgrade` or `New-ServiceFabricApplication` cmdlets.</span></span>

|<span data-ttu-id="d7c4a-190">**Parâmetro**</span><span class="sxs-lookup"><span data-stu-id="d7c4a-190">**Parameter**</span></span>        |<span data-ttu-id="d7c4a-191">**Tipo**</span><span class="sxs-lookup"><span data-stu-id="d7c4a-191">**Type**</span></span>                          | <span data-ttu-id="d7c4a-192">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="d7c4a-192">**Details**</span></span>|
|:-|-|-|
|<span data-ttu-id="d7c4a-193">MaxResultsToCache</span><span class="sxs-lookup"><span data-stu-id="d7c4a-193">MaxResultsToCache</span></span>    |<span data-ttu-id="d7c4a-194">long</span><span class="sxs-lookup"><span data-stu-id="d7c4a-194">Long</span></span>                              | <span data-ttu-id="d7c4a-195">Número máximo de resultados do Windows Update, que devem ser armazenados em cache.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-195">Maximum number of Windows Update results, which should be cached.</span></span> <br><span data-ttu-id="d7c4a-196">O valor padrão é 3000, supondo que o:</span><span class="sxs-lookup"><span data-stu-id="d7c4a-196">Default value is 3000 assuming the:</span></span> <br> <span data-ttu-id="d7c4a-197">- Número de nós é 20.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-197">- Number of nodes is 20.</span></span> <br> <span data-ttu-id="d7c4a-198">- Número de atualizações acontecendo em um nó por mês seja de cinco.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-198">- Number of updates happening on a node per month is five.</span></span> <br> <span data-ttu-id="d7c4a-199">– Número de resultados por operação possa ser de 10.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-199">- Number of results per operation can be 10.</span></span> <br> <span data-ttu-id="d7c4a-200">-Resultados de saudação últimos três meses devem ser armazenados.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-200">- Results for hello past three months should be stored.</span></span> |
|<span data-ttu-id="d7c4a-201">TaskApprovalPolicy</span><span class="sxs-lookup"><span data-stu-id="d7c4a-201">TaskApprovalPolicy</span></span>   |<span data-ttu-id="d7c4a-202">Enum</span><span class="sxs-lookup"><span data-stu-id="d7c4a-202">Enum</span></span> <br> <span data-ttu-id="d7c4a-203">{ NodeWise, UpgradeDomainWise }</span><span class="sxs-lookup"><span data-stu-id="d7c4a-203">{ NodeWise, UpgradeDomainWise }</span></span>                          |<span data-ttu-id="d7c4a-204">TaskApprovalPolicy indica a diretiva de saudação toobe usada por atualizações do Windows hello serviço tooinstall em nós de cluster do Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-204">TaskApprovalPolicy indicates hello policy that is toobe used by hello Coordinator Service tooinstall Windows updates across hello Service Fabric cluster nodes.</span></span><br>                         <span data-ttu-id="d7c4a-205">Valores permitidos são:</span><span class="sxs-lookup"><span data-stu-id="d7c4a-205">Allowed values are:</span></span> <br>                                                           <span data-ttu-id="d7c4a-206"><b>NodeWise</b>.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-206"><b>NodeWise</b>.</span></span> <span data-ttu-id="d7c4a-207">O Windows Update é instalado em um nó por vez.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-207">Windows Update is installed one node at a time.</span></span> <br>                                                           <span data-ttu-id="d7c4a-208"><b>UpgradeDomainWise</b>.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-208"><b>UpgradeDomainWise</b>.</span></span> <span data-ttu-id="d7c4a-209">O Windows Update é instalado em um domínio de atualização por vez.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-209">Windows Update is installed one upgrade domain at a time.</span></span> <span data-ttu-id="d7c4a-210">(No máximo de hello, todos os nós de saudação pertencentes tooan domínio de atualização podem ir para o Windows Update).</span><span class="sxs-lookup"><span data-stu-id="d7c4a-210">(At hello maximum, all hello nodes belonging tooan upgrade domain can go for Windows Update.)</span></span>
|<span data-ttu-id="d7c4a-211">LogsDiskQuotaInMB</span><span class="sxs-lookup"><span data-stu-id="d7c4a-211">LogsDiskQuotaInMB</span></span>   |<span data-ttu-id="d7c4a-212">long</span><span class="sxs-lookup"><span data-stu-id="d7c4a-212">Long</span></span>  <br> <span data-ttu-id="d7c4a-213">(Padrão: 1024)</span><span class="sxs-lookup"><span data-stu-id="d7c4a-213">(Default: 1024)</span></span>               |<span data-ttu-id="d7c4a-214">Tamanho máximo dos logs do aplicativo de orquestração de patch em MB, que pode ser mantido localmente no nó.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-214">Maximum size of patch orchestration app logs in MB, which can be persisted locally on nodes.</span></span>
| <span data-ttu-id="d7c4a-215">WUQuery</span><span class="sxs-lookup"><span data-stu-id="d7c4a-215">WUQuery</span></span>               | <span data-ttu-id="d7c4a-216">string</span><span class="sxs-lookup"><span data-stu-id="d7c4a-216">string</span></span><br><span data-ttu-id="d7c4a-217">(Padrão: "IsInstalled=0")</span><span class="sxs-lookup"><span data-stu-id="d7c4a-217">(Default: "IsInstalled=0")</span></span>                | <span data-ttu-id="d7c4a-218">Consulta tooget atualizações do Windows.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-218">Query tooget Windows updates.</span></span> <span data-ttu-id="d7c4a-219">Para obter mais informações, consulte [WuQuery.](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx)</span><span class="sxs-lookup"><span data-stu-id="d7c4a-219">For more information, see [WuQuery.](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx)</span></span>
| <span data-ttu-id="d7c4a-220">InstallWindowsOSOnlyUpdates</span><span class="sxs-lookup"><span data-stu-id="d7c4a-220">InstallWindowsOSOnlyUpdates</span></span> | <span data-ttu-id="d7c4a-221">Bool</span><span class="sxs-lookup"><span data-stu-id="d7c4a-221">Bool</span></span> <br> <span data-ttu-id="d7c4a-222">(padrão: True)</span><span class="sxs-lookup"><span data-stu-id="d7c4a-222">(default: True)</span></span>                 | <span data-ttu-id="d7c4a-223">Esse sinalizador permite que o Windows operacional toobe de atualizações do sistema instalado.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-223">This flag allows Windows operating system updates toobe installed.</span></span>            |
| <span data-ttu-id="d7c4a-224">WUOperationTimeOutInMinutes</span><span class="sxs-lookup"><span data-stu-id="d7c4a-224">WUOperationTimeOutInMinutes</span></span> | <span data-ttu-id="d7c4a-225">int</span><span class="sxs-lookup"><span data-stu-id="d7c4a-225">Int</span></span> <br><span data-ttu-id="d7c4a-226">(Padrão: 90)</span><span class="sxs-lookup"><span data-stu-id="d7c4a-226">(Default: 90)</span></span>                   | <span data-ttu-id="d7c4a-227">Especifica o tempo limite de saudação para qualquer operação de atualização do Windows (Pesquisar ou baixar ou instalar).</span><span class="sxs-lookup"><span data-stu-id="d7c4a-227">Specifies hello timeout for any Windows Update operation (search or download or install).</span></span> <span data-ttu-id="d7c4a-228">Se a operação de saudação não foi concluída dentro de Olá tempo limite especificado, ele será anulado.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-228">If hello operation is not completed within hello specified timeout, it is aborted.</span></span>       |
| <span data-ttu-id="d7c4a-229">WURescheduleCount</span><span class="sxs-lookup"><span data-stu-id="d7c4a-229">WURescheduleCount</span></span>     | <span data-ttu-id="d7c4a-230">int</span><span class="sxs-lookup"><span data-stu-id="d7c4a-230">Int</span></span> <br> <span data-ttu-id="d7c4a-231">(Padrão: 5)</span><span class="sxs-lookup"><span data-stu-id="d7c4a-231">(Default: 5)</span></span>                  | <span data-ttu-id="d7c4a-232">o número de vezes que serviço Olá reagenda Olá máximo Olá Windows update no caso de uma operação falha de maneira persistente.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-232">hello maximum number of times hello service reschedules hello Windows update in case an operation fails persistently.</span></span>          |
| <span data-ttu-id="d7c4a-233">WURescheduleTimeInMinutes</span><span class="sxs-lookup"><span data-stu-id="d7c4a-233">WURescheduleTimeInMinutes</span></span> | <span data-ttu-id="d7c4a-234">int</span><span class="sxs-lookup"><span data-stu-id="d7c4a-234">Int</span></span> <br><span data-ttu-id="d7c4a-235">(Padrão: 30)</span><span class="sxs-lookup"><span data-stu-id="d7c4a-235">(Default: 30)</span></span> | <span data-ttu-id="d7c4a-236">intervalo de saudação em qual Olá serviço reagenda Olá Windows update no caso de falha persistir.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-236">hello interval at which hello service reschedules hello Windows update in case failure persists.</span></span> |
| <span data-ttu-id="d7c4a-237">WUFrequency</span><span class="sxs-lookup"><span data-stu-id="d7c4a-237">WUFrequency</span></span>           | <span data-ttu-id="d7c4a-238">Cadeia de caracteres separada por vírgula (padrão: "Semanalmente, quarta-feira, 7:00:00")</span><span class="sxs-lookup"><span data-stu-id="d7c4a-238">Comma-separated string (Default: "Weekly, Wednesday, 7:00:00")</span></span>     | <span data-ttu-id="d7c4a-239">frequência de saudação para instalar o Windows Update.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-239">hello frequency for installing Windows Update.</span></span> <span data-ttu-id="d7c4a-240">Olá formato e os valores possíveis são:</span><span class="sxs-lookup"><span data-stu-id="d7c4a-240">hello format and possible values are:</span></span> <br><span data-ttu-id="d7c4a-241">-   Mensal, DD, HH:MM:SS, por exemplo, Mensal, 5, 12:22:32.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-241">-   Monthly, DD,HH:MM:SS, for example, Monthly, 5,12:22:32.</span></span> <br> <span data-ttu-id="d7c4a-242">-   Semanal, DIA, HH:MM:SS, por exemplo, Semanal, terça-feira, 12:22:32.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-242">-   Weekly, DAY,HH:MM:SS, for example, Weekly, Tuesday, 12:22:32.</span></span>  <br> <span data-ttu-id="d7c4a-243">-   Diário, HH:MM:SS, por exemplo, Diário, 12:22:32.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-243">-   Daily, HH:MM:SS, for example, Daily, 12:22:32.</span></span>  <br> <span data-ttu-id="d7c4a-244">-  Nenhum indica que o Windows Update não deve ser executado.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-244">-  None indicates that Windows Update shouldn't be done.</span></span>  <br><br> <span data-ttu-id="d7c4a-245">Observe que todos os tempos de saudação estão em UTC.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-245">Note that all hello times are in UTC.</span></span>|
| <span data-ttu-id="d7c4a-246">AcceptWindowsUpdateEula</span><span class="sxs-lookup"><span data-stu-id="d7c4a-246">AcceptWindowsUpdateEula</span></span> | <span data-ttu-id="d7c4a-247">Bool</span><span class="sxs-lookup"><span data-stu-id="d7c4a-247">Bool</span></span> <br><span data-ttu-id="d7c4a-248">(Padrão: true)</span><span class="sxs-lookup"><span data-stu-id="d7c4a-248">(Default: true)</span></span> | <span data-ttu-id="d7c4a-249">Ao definir esse sinalizador, o aplicativo hello aceita saudação do usuário final licença contrato para o Windows Update em nome do proprietário de saudação da máquina de saudação.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-249">By setting this flag, hello application accepts hello End-User License Agreement for Windows Update on behalf of hello owner of hello machine.</span></span>              |

> [!TIP]
> <span data-ttu-id="d7c4a-250">Se você quiser Windows Update toohappen imediatamente, defina `WUFrequency` toohello relativo tempo de implantação de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-250">If you want Windows Update toohappen immediately, set `WUFrequency` relative toohello application deployment time.</span></span> <span data-ttu-id="d7c4a-251">Por exemplo, suponha que você tenha um aplicativo teste de nó de cinco cluster e planejar toodeploy Olá em cerca de 5:00 PM UTC.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-251">For example, suppose that you have a five-node test cluster and plan toodeploy hello app at around 5:00 PM UTC.</span></span> <span data-ttu-id="d7c4a-252">Se você presumir que a implantação ou atualização do aplicativo hello leva 30 minutos no Olá Olá máximo, defina WUFrequency como "Diariamente, 17:30:00."</span><span class="sxs-lookup"><span data-stu-id="d7c4a-252">If you assume that hello application upgrade or deployment takes 30 minutes at hello maximum, set hello WUFrequency as "Daily, 17:30:00."</span></span>

## <a name="deploy-hello-app"></a><span data-ttu-id="d7c4a-253">Implantar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="d7c4a-253">Deploy hello app</span></span>

1. <span data-ttu-id="d7c4a-254">Conclua todos os cluster de Olá Olá etapas de pré-requisito tooprepare.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-254">Finish all hello prerequisite steps tooprepare hello cluster.</span></span>
2. <span data-ttu-id="d7c4a-255">Implante o aplicativo de orquestração de patch de saudação como qualquer outro aplicativo de malha do serviço.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-255">Deploy hello patch orchestration app like any other Service Fabric app.</span></span> <span data-ttu-id="d7c4a-256">Você pode implantar o aplicativo hello usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-256">You can deploy hello app by using PowerShell.</span></span> <span data-ttu-id="d7c4a-257">Siga as etapas de saudação em [implantar e remover aplicativos usando o PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span><span class="sxs-lookup"><span data-stu-id="d7c4a-257">Follow hello steps in [Deploy and remove applications using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span></span>
3. <span data-ttu-id="d7c4a-258">aplicativo de Olá tooconfigure em tempo de saudação de implantação, passe Olá `ApplicationParamater` toohello `New-ServiceFabricApplication` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-258">tooconfigure hello application at hello time of deployment, pass hello `ApplicationParamater` toohello `New-ServiceFabricApplication` cmdlet.</span></span> <span data-ttu-id="d7c4a-259">Para sua conveniência, fornecemos script hello Deploy.ps1 juntamente com o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-259">For your convenience, we’ve provided hello script Deploy.ps1 along with hello application.</span></span> <span data-ttu-id="d7c4a-260">script de saudação toouse:</span><span class="sxs-lookup"><span data-stu-id="d7c4a-260">toouse hello script:</span></span>

    - <span data-ttu-id="d7c4a-261">Conecte-se o cluster do Service Fabric tooa usando `Connect-ServiceFabricCluster`.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-261">Connect tooa Service Fabric cluster by using `Connect-ServiceFabricCluster`.</span></span>
    - <span data-ttu-id="d7c4a-262">Executar script do PowerShell Olá Deploy.ps1 com hello apropriado `ApplicationParameter` valor.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-262">Execute hello PowerShell script Deploy.ps1 with hello appropriate `ApplicationParameter` value.</span></span>

> [!NOTE]
> <span data-ttu-id="d7c4a-263">Manter script hello e pasta de aplicativo hello PatchOrchestrationApplication em Olá mesmo diretório.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-263">Keep hello script and hello application folder PatchOrchestrationApplication in hello same directory.</span></span>

## <a name="upgrade-hello-app"></a><span data-ttu-id="d7c4a-264">Atualizar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="d7c4a-264">Upgrade hello app</span></span>

<span data-ttu-id="d7c4a-265">tooupgrade um aplicativo de orquestração de patch existente usando o PowerShell, execute as etapas de saudação em [atualização do aplicativo do Service Fabric usando o PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell).</span><span class="sxs-lookup"><span data-stu-id="d7c4a-265">tooupgrade an existing patch orchestration app by using PowerShell, follow hello steps in [Service Fabric application upgrade using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell).</span></span>

## <a name="remove-hello-app"></a><span data-ttu-id="d7c4a-266">Remover o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="d7c4a-266">Remove hello app</span></span>

<span data-ttu-id="d7c4a-267">aplicativo do tooremove hello, siga etapas de saudação em [implantar e remover aplicativos usando o PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span><span class="sxs-lookup"><span data-stu-id="d7c4a-267">tooremove hello application, follow hello steps in [Deploy and remove applications using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span></span>

<span data-ttu-id="d7c4a-268">Para sua conveniência, fornecemos script hello Undeploy.ps1 juntamente com o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-268">For your convenience, we've provided hello script Undeploy.ps1 along with hello application.</span></span> <span data-ttu-id="d7c4a-269">script de saudação toouse:</span><span class="sxs-lookup"><span data-stu-id="d7c4a-269">toouse hello script:</span></span>

  - <span data-ttu-id="d7c4a-270">Conecte-se o cluster do Service Fabric tooa usando ```Connect-ServiceFabricCluster```.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-270">Connect tooa Service Fabric cluster by using ```Connect-ServiceFabricCluster```.</span></span>

  - <span data-ttu-id="d7c4a-271">Execute o script do PowerShell Olá Undeploy.ps1.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-271">Execute hello PowerShell script Undeploy.ps1.</span></span>

> [!NOTE]
> <span data-ttu-id="d7c4a-272">Manter script hello e pasta de aplicativo hello PatchOrchestrationApplication em Olá mesmo diretório.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-272">Keep hello script and hello application folder PatchOrchestrationApplication in hello same directory.</span></span>

## <a name="view-hello-windows-update-results"></a><span data-ttu-id="d7c4a-273">Exibir resultados da atualização do Windows hello</span><span class="sxs-lookup"><span data-stu-id="d7c4a-273">View hello Windows Update results</span></span>

<span data-ttu-id="d7c4a-274">Olá patch orquestração aplicativo expõe o usuário de toohello APIs REST toodisplay Olá resultados históricos.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-274">hello patch orchestration app exposes REST APIs toodisplay hello historical results toohello user.</span></span> <span data-ttu-id="d7c4a-275">Um exemplo de resultado de saudação JSON:</span><span class="sxs-lookup"><span data-stu-id="d7c4a-275">An example of hello result JSON:</span></span>
```json
[
  {
    "NodeName": "_stg1vm_1",
    "WindowsUpdateOperationResults": [
      {
        "OperationResult": 0,
        "NodeName": "_stg1vm_1",
        "OperationTime": "2017-05-21T11:46:52.1953713Z",
        "UpdateDetails": [
          {
            "UpdateId": "7392acaf-6a85-427c-8a8d-058c25beb0d6",
            "Title": "Cumulative Security Update for Internet Explorer 11 for Windows Server 2012 R2 (KB3185319)",
            "Description": "A security issue has been identified in a Microsoft software product that could affect your system. You can help protect your system by installing this update from Microsoft. For a complete listing of hello issues that are included in this update, see hello associated Microsoft Knowledge Base article. After you install this update, you may have toorestart your system.",
            "ResultCode": 0
          }
        ],
        "OperationType": 1,
        "WindowsUpdateQuery": "IsInstalled=0",
        "WindowsUpdateFrequency": "Daily,10:00:00",
        "RebootRequired": false
      }
    ]
  },
  ...
]
```
<span data-ttu-id="d7c4a-276">Se nenhuma atualização estiver agendada ainda, o resultado de saudação JSON está vazio.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-276">If no update is scheduled yet, hello result JSON is empty.</span></span>

<span data-ttu-id="d7c4a-277">Registrar resultados em toohello cluster tooquery Windows Update.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-277">Log in toohello cluster tooquery Windows Update results.</span></span> <span data-ttu-id="d7c4a-278">Em seguida, descobrir Olá endereço de réplica para o primário Olá Olá serviço Coordenador de e pressione Olá URL do navegador de saudação: http://&lt;IP de réplica&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1 / GetWindowsUpdateResults.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-278">Then find out hello replica address for hello primary of hello Coordinator Service, and hit hello URL from hello browser: http://&lt;REPLICA-IP&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1/GetWindowsUpdateResults.</span></span>

<span data-ttu-id="d7c4a-279">Olá o ponto de extremidade REST para Olá serviço tem uma porta dinâmica.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-279">hello REST endpoint for hello Coordinator Service has a dynamic port.</span></span> <span data-ttu-id="d7c4a-280">toocheck Olá URL exata, consulte toohello Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-280">toocheck hello exact URL, refer toohello Service Fabric Explorer.</span></span> <span data-ttu-id="d7c4a-281">Por exemplo, os resultados de saudação estão disponíveis em `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-281">For example, hello results are available at `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`.</span></span>

![Imagem do ponto de extremidade REST](media/service-fabric-patch-orchestration-application/Rest_Endpoint.png)


<span data-ttu-id="d7c4a-283">Se o proxy reverso Olá estiver habilitado no cluster Olá, você pode acessar Olá a URL de fora do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-283">If hello reverse proxy is enabled on hello cluster, you can access hello URL from outside of hello cluster as well.</span></span>
<span data-ttu-id="d7c4a-284">Olá ponto de extremidade que precisa toobe ocorrências é http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-284">hello endpoint that needs toobe hit is http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults.</span></span>

<span data-ttu-id="d7c4a-285">proxy reverso do tooenable Olá no cluster hello, siga as etapas de saudação em [proxy no Azure Service Fabric reverso](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy).</span><span class="sxs-lookup"><span data-stu-id="d7c4a-285">tooenable hello reverse proxy on hello cluster, follow hello steps in [Reverse proxy in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy).</span></span> 

> 
> [!WARNING]
> <span data-ttu-id="d7c4a-286">Após a configuração de proxy reverso hello, todos os serviços em cluster Olá micro que expõem um ponto de extremidade HTTP são endereçáveis da fora Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-286">After hello reverse proxy is configured, all micro services in hello cluster that expose an HTTP endpoint are addressable from outside hello cluster.</span></span>

## <a name="diagnosticshealth-events"></a><span data-ttu-id="d7c4a-287">Eventos de diagnóstico/integridade</span><span class="sxs-lookup"><span data-stu-id="d7c4a-287">Diagnostics/health events</span></span>

### <a name="collect-patch-orchestration-app-logs"></a><span data-ttu-id="d7c4a-288">Colete logs do aplicativo de orquestração de patch</span><span class="sxs-lookup"><span data-stu-id="d7c4a-288">Collect patch orchestration app logs</span></span>

<span data-ttu-id="d7c4a-289">Os logs do aplicativo de orquestração de patch são coletados como parte dos logs do Service Fabric a partir da versão de tempo de execução `5.6.220.9494` e superior.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-289">Patch orchestration app logs are collected as part of Service Fabric logs from runtime version `5.6.220.9494` and above.</span></span>
<span data-ttu-id="d7c4a-290">Para clusters que executam a versão de tempo de execução do Service Fabric menor `5.6.220.9494`, logs podem ser coletados usando um dos métodos a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-290">For clusters running Service Fabric runtime version less than `5.6.220.9494`, logs can be collected by using one of hello following methods.</span></span>

#### <a name="locally-on-each-node"></a><span data-ttu-id="d7c4a-291">Localmente em cada nó</span><span class="sxs-lookup"><span data-stu-id="d7c4a-291">Locally on each node</span></span>

<span data-ttu-id="d7c4a-292">Logs são coletados localmente em cada nó de cluster do Service Fabric se a versão de tempo de execução do Service Fabric é menor que `5.6.220.9494`.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-292">Logs are collected locally on each Service Fabric cluster node if Service Fabric runtime version is less than `5.6.220.9494`.</span></span> <span data-ttu-id="d7c4a-293">Olá local tooaccess Olá logs é \[Service Fabric\_instalação\_unidade\]:\\PatchOrchestrationApplication\\logs.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-293">hello location tooaccess hello logs is \[Service Fabric\_Installation\_Drive\]:\\PatchOrchestrationApplication\\logs.</span></span>

<span data-ttu-id="d7c4a-294">Por exemplo, se o serviço de malha é instalada na unidade D, caminho de saudação é d:\\PatchOrchestrationApplication\\logs.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-294">For example, if Service Fabric is installed on drive D, hello path is D:\\PatchOrchestrationApplication\\logs.</span></span>

#### <a name="central-location"></a><span data-ttu-id="d7c4a-295">Local central</span><span class="sxs-lookup"><span data-stu-id="d7c4a-295">Central location</span></span>

<span data-ttu-id="d7c4a-296">Se o diagnóstico do Azure é configurado como parte das etapas de pré-requisito, logs do aplicativo de orquestração de patch Olá estão disponíveis no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-296">If Azure Diagnostics is configured as part of prerequisite steps, logs for hello patch orchestration app are available in Azure Storage.</span></span>

### <a name="health-reports"></a><span data-ttu-id="d7c4a-297">Relatórios de integridade</span><span class="sxs-lookup"><span data-stu-id="d7c4a-297">Health reports</span></span>

<span data-ttu-id="d7c4a-298">aplicativo de orquestração de patch Olá também publica relatórios de integridade em relação a saudação serviço coordenador ou Olá serviço de agente do nó no Olá casos a seguir:</span><span class="sxs-lookup"><span data-stu-id="d7c4a-298">hello patch orchestration app also publishes health reports against hello Coordinator Service or hello Node Agent Service in hello following cases:</span></span>

#### <a name="a-windows-update-operation-failed"></a><span data-ttu-id="d7c4a-299">Uma falha na operação do Windows Update</span><span class="sxs-lookup"><span data-stu-id="d7c4a-299">A Windows Update operation failed</span></span>

<span data-ttu-id="d7c4a-300">Se uma operação de atualização do Windows falhar em um nó, um relatório de integridade é gerado em relação a saudação serviço de agente do nó.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-300">If a Windows Update operation fails on a node, a health report is generated against hello Node Agent Service.</span></span> <span data-ttu-id="d7c4a-301">Detalhes do relatório de integridade de saudação contém nome de nó problemáticos de saudação.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-301">Details of hello health report contain hello problematic node name.</span></span>

<span data-ttu-id="d7c4a-302">Após a aplicação de patch é concluída com êxito no nó problemático hello, relatório Olá será desmarcado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-302">After patching is successfully completed on hello problematic node, hello report is automatically cleared.</span></span>

#### <a name="hello-node-agent-ntservice-is-down"></a><span data-ttu-id="d7c4a-303">Olá NTService de agente do nó está inoperante</span><span class="sxs-lookup"><span data-stu-id="d7c4a-303">hello Node Agent NTService is down</span></span>

<span data-ttu-id="d7c4a-304">Se Olá NTService de agente do nó estiver inativo em um nó, um relatório de integridade do nível de aviso é gerado em relação a saudação serviço de agente do nó.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-304">If hello Node Agent NTService is down on a node, a warning-level health report is generated against hello Node Agent Service.</span></span>

#### <a name="hello-repair-manager-service-is-not-enabled"></a><span data-ttu-id="d7c4a-305">serviço de Gerenciador de reparo do Hello não está habilitado</span><span class="sxs-lookup"><span data-stu-id="d7c4a-305">hello repair manager service is not enabled</span></span>

<span data-ttu-id="d7c4a-306">Se o serviço de Gerenciador de reparo do hello não foi encontrado no cluster hello, um relatório de integridade do nível de aviso é gerado para Olá serviço de coordenador.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-306">If hello repair manager service is not found on hello cluster, a warning-level health report is generated for hello Coordinator Service.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="d7c4a-307">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="d7c4a-307">Frequently asked questions</span></span>

<span data-ttu-id="d7c4a-308">P.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-308">Q.</span></span> <span data-ttu-id="d7c4a-309">**Por que vejo o cluster em um estado de erro quando Olá patch orquestração aplicativo está em execução?**</span><span class="sxs-lookup"><span data-stu-id="d7c4a-309">**Why do I see my cluster in an error state when hello patch orchestration app is running?**</span></span>

<span data-ttu-id="d7c4a-310">R.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-310">A.</span></span> <span data-ttu-id="d7c4a-311">Durante o processo de instalação hello, Olá patch orquestração aplicativo desabilita ou reinicia nós, o que podem resultar temporariamente a integridade de saudação do cluster Olá ficar inativo.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-311">During hello installation process, hello patch orchestration app disables or restarts nodes, which can temporarily result in hello health of hello cluster going down.</span></span>

<span data-ttu-id="d7c4a-312">Com base na política de saudação para o aplicativo hello, ou um nó pode ser reduzidos durante uma operação de aplicação de patch *ou* todo um domínio de atualização pode ser reduzidos simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-312">Based on hello policy for hello application, either one node can go down during a patching operation *or* an entire upgrade domain can go down simultaneously.</span></span>

<span data-ttu-id="d7c4a-313">Final de saudação do hello instalação do Windows Update, Olá nós são habilitados novamente após a reinicialização.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-313">By hello end of hello Windows Update installation, hello nodes are reenabled post restart.</span></span>

<span data-ttu-id="d7c4a-314">Em Olá exemplo a seguir, o cluster Olá entrou estado de erro tooan temporariamente porque dois nós foram para baixo e Olá MaxPercentageUnhealthNodes política foi violado.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-314">In hello following example, hello cluster went tooan error state temporarily because two nodes were down and hello MaxPercentageUnhealthNodes policy was violated.</span></span> <span data-ttu-id="d7c4a-315">Erro de saudação é temporário até Olá operação de patch está em andamento.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-315">hello error is temporary until hello patching operation is ongoing.</span></span>

![Imagem do cluster não íntegro](media/service-fabric-patch-orchestration-application/MaxPercentage_causing_unhealthy_cluster.png)

<span data-ttu-id="d7c4a-317">Se Olá problema persistir, consulte a seção de solução de problemas de toohello.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-317">If hello issue persists, refer toohello Troubleshooting section.</span></span>

<span data-ttu-id="d7c4a-318">P.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-318">Q.</span></span> <span data-ttu-id="d7c4a-319">**O aplicativo de orquestração de patch está em estado de aviso**</span><span class="sxs-lookup"><span data-stu-id="d7c4a-319">**Patch orchestration app is in warning state**</span></span>

<span data-ttu-id="d7c4a-320">R.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-320">A.</span></span> <span data-ttu-id="d7c4a-321">Verifique toosee se um relatório de integridade lançado contra o aplicativo hello causa hello.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-321">Check toosee if a health report posted against hello application is hello root cause.</span></span> <span data-ttu-id="d7c4a-322">Normalmente, o aviso de saudação contém detalhes do problema de saudação.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-322">Usually, hello warning contains details of hello problem.</span></span> <span data-ttu-id="d7c4a-323">Se o problema de saudação é transitório, o aplicativo hello é esperada tooauto recuperação desse estado.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-323">If hello issue is transient, hello application is expected tooauto-recover from this state.</span></span>

<span data-ttu-id="d7c4a-324">P.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-324">Q.</span></span> <span data-ttu-id="d7c4a-325">**O que fazer se o cluster está íntegro e precisa de uma atualização do sistema de operacional urgentes de toodo?**</span><span class="sxs-lookup"><span data-stu-id="d7c4a-325">**What can I do if my cluster is unhealthy and I need toodo an urgent operating system update?**</span></span>

<span data-ttu-id="d7c4a-326">R.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-326">A.</span></span> <span data-ttu-id="d7c4a-327">Olá patch orquestração aplicativo não instala atualizações ao cluster Olá não está íntegro.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-327">hello patch orchestration app does not install updates while hello cluster is unhealthy.</span></span> <span data-ttu-id="d7c4a-328">Tente toobring seu cluster tooa Íntegro toounblock Olá patch orquestração aplicativo fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-328">Try toobring your cluster tooa healthy state toounblock hello patch orchestration app workflow.</span></span>

<span data-ttu-id="d7c4a-329">P.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-329">Q.</span></span> <span data-ttu-id="d7c4a-330">**Por que a aplicação de patch em clusters leva muito tempo toorun?**</span><span class="sxs-lookup"><span data-stu-id="d7c4a-330">**Why does patching across clusters take so long toorun?**</span></span>

<span data-ttu-id="d7c4a-331">R.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-331">A.</span></span> <span data-ttu-id="d7c4a-332">tempo de saudação necessário pelo aplicativo de orquestração de patch Olá depende principalmente Olá fatores a seguir:</span><span class="sxs-lookup"><span data-stu-id="d7c4a-332">hello time needed by hello patch orchestration app is mostly dependent on hello following factors:</span></span>

- <span data-ttu-id="d7c4a-333">política de saudação do hello serviço coordenador.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-333">hello policy of hello Coordinator Service.</span></span> 
  - <span data-ttu-id="d7c4a-334">Olá política padrão, `NodeWise`, resulta na aplicação de patch apenas um nó por vez.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-334">hello default policy, `NodeWise`, results in patching only one node at a time.</span></span> <span data-ttu-id="d7c4a-335">Especialmente no caso de saudação de clusters maiores, é recomendável que você use Olá `UpgradeDomainWise` política tooachieve mais rápido de aplicação de patch em clusters.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-335">Especially in hello case of bigger clusters, we recommend that you use hello `UpgradeDomainWise` policy tooachieve faster patching across clusters.</span></span>
- <span data-ttu-id="d7c4a-336">número de saudação de atualizações disponíveis para download e instalação.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-336">hello number of updates available for download and installation.</span></span> 
- <span data-ttu-id="d7c4a-337">Olá toodownload tempo médio necessário e instalar uma atualização, que não deve exceder a algumas horas.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-337">hello average time needed toodownload and install an update, which should not exceed a couple of hours.</span></span>
- <span data-ttu-id="d7c4a-338">desempenho de saudação de largura de banda de rede e máquinas virtuais de saudação.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-338">hello performance of hello VM and network bandwidth.</span></span>

<span data-ttu-id="d7c4a-339">P.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-339">Q.</span></span> <span data-ttu-id="d7c4a-340">**Por que vejo algumas atualizações no Windows Update resultados obtidos por meio da api REST, mas não em Olá histórico do Windows Update no computador?**</span><span class="sxs-lookup"><span data-stu-id="d7c4a-340">**Why do I see some updates in Windows Update results obtained via REST api's, but not under hello Windows Update history on machine?**</span></span>

<span data-ttu-id="d7c4a-341">R.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-341">A.</span></span> <span data-ttu-id="d7c4a-342">Algumas atualizações do produto necessário toobe check-in de seu histórico de atualização/patch do respectivos.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-342">Some product updates need toobe checked in their respective update/patch history.</span></span> <span data-ttu-id="d7c4a-343">Por exemplo: Atualizações do Windows Defender não aparecem no histórico do Windows Update no Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-343">Eg: Windows Defender updates do not show up in Windows Update history on Windows Server 2016.</span></span>

## <a name="disclaimers"></a><span data-ttu-id="d7c4a-344">Avisos de Isenção de Responsabilidade</span><span class="sxs-lookup"><span data-stu-id="d7c4a-344">Disclaimers</span></span>

- <span data-ttu-id="d7c4a-345">aplicativo de orquestração de patch Olá aceita saudação do usuário final licença contrato do Windows Update em nome de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-345">hello patch orchestration app accepts hello End-User License Agreement of Windows Update on behalf of hello user.</span></span> <span data-ttu-id="d7c4a-346">Opcionalmente, configuração de saudação pode ser desativada na configuração de saudação do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-346">Optionally, hello setting can be turned off in hello configuration of hello application.</span></span>

- <span data-ttu-id="d7c4a-347">aplicativo de orquestração de patch Olá coleta telemetria tootrack uso e desempenho.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-347">hello patch orchestration app collects telemetry tootrack usage and performance.</span></span> <span data-ttu-id="d7c4a-348">Telemetria do aplicativo Hello segue a configuração de saudação da configuração de telemetria de saudação do Service Fabric runtime (que é ativado por padrão).</span><span class="sxs-lookup"><span data-stu-id="d7c4a-348">hello application’s telemetry follows hello setting of hello Service Fabric runtime’s telemetry setting (which is on by default).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="d7c4a-349">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="d7c4a-349">Troubleshooting</span></span>

### <a name="a-node-is-not-coming-back-tooup-state"></a><span data-ttu-id="d7c4a-350">Um nó não voltará tooup estado</span><span class="sxs-lookup"><span data-stu-id="d7c4a-350">A node is not coming back tooup state</span></span>

<span data-ttu-id="d7c4a-351">**nó de saudação pode estar paralisada em um estado de desabilitação porque**:</span><span class="sxs-lookup"><span data-stu-id="d7c4a-351">**hello node might be stuck in a disabling state because**:</span></span>

<span data-ttu-id="d7c4a-352">Uma verificação de segurança está pendente.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-352">A safety check is pending.</span></span> <span data-ttu-id="d7c4a-353">tooremedy nessa situação, certifique-se de que nós suficientes estejam disponíveis em um estado íntegro.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-353">tooremedy this situation, ensure that enough nodes are available in a healthy state.</span></span>

<span data-ttu-id="d7c4a-354">**nó de saudação pode estar paralisada em um estado desabilitado porque**:</span><span class="sxs-lookup"><span data-stu-id="d7c4a-354">**hello node might be stuck in a disabled state because**:</span></span>

- <span data-ttu-id="d7c4a-355">nó de saudação foi desativado manualmente.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-355">hello node was disabled manually.</span></span>
- <span data-ttu-id="d7c4a-356">nó de saudação foi desabilitada devido tooan trabalho de infraestrutura do Azure em andamento.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-356">hello node was disabled due tooan ongoing Azure infrastructure job.</span></span>
- <span data-ttu-id="d7c4a-357">nó Olá foi desativado temporariamente pelo nó de saudação toopatch do aplicativo de orquestração de patch hello.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-357">hello node was disabled temporarily by hello patch orchestration app toopatch hello node.</span></span>

<span data-ttu-id="d7c4a-358">**Olá nó pode estar paralisado em um estado inativo porque**:</span><span class="sxs-lookup"><span data-stu-id="d7c4a-358">**hello node might be stuck in a down state because**:</span></span>

- <span data-ttu-id="d7c4a-359">nó de saudação foi colocado em um estado inativo manualmente.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-359">hello node was put in a down state manually.</span></span>
- <span data-ttu-id="d7c4a-360">nó de saudação está passando por uma reinicialização (que pode ser disparada por aplicativo de orquestração de patch Olá).</span><span class="sxs-lookup"><span data-stu-id="d7c4a-360">hello node is undergoing a restart (which might be triggered by hello patch orchestration app).</span></span>
- <span data-ttu-id="d7c4a-361">nó de saudação está inoperante devido tooa defeituoso VM ou máquina ou rede problemas de conectividade.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-361">hello node is down due tooa faulty VM or machine or network connectivity issues.</span></span>

### <a name="updates-were-skipped-on-some-nodes"></a><span data-ttu-id="d7c4a-362">As atualizações foram ignoradas em alguns nós</span><span class="sxs-lookup"><span data-stu-id="d7c4a-362">Updates were skipped on some nodes</span></span>

<span data-ttu-id="d7c4a-363">Olá patch orquestração aplicativo tenta tooinstall uma acordo toohello reagendar diretiva do Windows update.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-363">hello patch orchestration app tries tooinstall a Windows update according toohello rescheduling policy.</span></span> <span data-ttu-id="d7c4a-364">serviço de Olá tenta nó de saudação toorecover e ignorar a política de aplicativo de toohello acordo do hello update.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-364">hello service tries toorecover hello node and skip hello update according toohello application policy.</span></span>

<span data-ttu-id="d7c4a-365">Nesse caso, um relatório de integridade do nível de aviso é gerado em relação a saudação serviço de agente do nó.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-365">In such a case, a warning-level health report is generated against hello Node Agent Service.</span></span> <span data-ttu-id="d7c4a-366">resultado de saudação para o Windows Update também contém um motivo possível para falha de Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-366">hello result for Windows Update also contains hello possible reason for hello failure.</span></span>

### <a name="hello-health-of-hello-cluster-goes-tooerror-while-hello-update-installs"></a><span data-ttu-id="d7c4a-367">integridade de saudação do cluster Olá vai tooerror enquanto a instalação da atualização de saudação</span><span class="sxs-lookup"><span data-stu-id="d7c4a-367">hello health of hello cluster goes tooerror while hello update installs</span></span>

<span data-ttu-id="d7c4a-368">Uma atualização com falha do Windows pode desativar a integridade de saudação de um aplicativo ou o cluster em um nó específico ou um domínio de atualização.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-368">A faulty Windows update can bring down hello health of an application or cluster on a particular node or upgrade domain.</span></span> <span data-ttu-id="d7c4a-369">Olá patch orquestração aplicativo interrompe qualquer operação subsequente do Windows Update até que o cluster Olá estiver íntegra novamente.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-369">hello patch orchestration app discontinues any subsequent Windows Update operation until hello cluster is healthy again.</span></span>

<span data-ttu-id="d7c4a-370">Um administrador deve intervir e determinar por que aplicativo hello ou cluster se tornou Íntegro devido tooWindows atualização.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-370">An administrator must intervene and determine why hello application or cluster became unhealthy due tooWindows Update.</span></span>

## <a name="release-notes-"></a><span data-ttu-id="d7c4a-371">Notas de Versão:</span><span class="sxs-lookup"><span data-stu-id="d7c4a-371">Release Notes :</span></span>

### <a name="version-110"></a><span data-ttu-id="d7c4a-372">Version 1.1.0</span><span class="sxs-lookup"><span data-stu-id="d7c4a-372">Version 1.1.0</span></span>
- <span data-ttu-id="d7c4a-373">Versão pública</span><span class="sxs-lookup"><span data-stu-id="d7c4a-373">Public release</span></span>

### <a name="version-111"></a><span data-ttu-id="d7c4a-374">Versão 1.1.1</span><span class="sxs-lookup"><span data-stu-id="d7c4a-374">Version 1.1.1</span></span>
- <span data-ttu-id="d7c4a-375">Correção de bug no SetupEntryPoint de NodeAgentService que impediu a instalação de NodeAgentNTService.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-375">Fixed a bug in SetupEntryPoint of NodeAgentService that prevented installation of NodeAgentNTService.</span></span>

### <a name="version-120-latest"></a><span data-ttu-id="d7c4a-376">Versão 1.2.0 (mais recente)</span><span class="sxs-lookup"><span data-stu-id="d7c4a-376">Version 1.2.0 (Latest)</span></span>

- <span data-ttu-id="d7c4a-377">Correções de bugs em torno do fluxo de trabalho de reinício do sistema.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-377">Bug fixes around system restart workflow.</span></span>
- <span data-ttu-id="d7c4a-378">Correção de bug na criação de tarefas do RM devido a verificação de integridade toowhich durante a preparação de tarefas de reparo não estava acontecendo conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-378">Bug fix in creation of RM tasks due toowhich health check during preparing repair tasks wasn't happening as expected.</span></span>
- <span data-ttu-id="d7c4a-379">Modo de inicialização alterada Olá para o serviço do windows POANodeSvc de auto toodelayed-auto.</span><span class="sxs-lookup"><span data-stu-id="d7c4a-379">Changed hello startup mode for windows service POANodeSvc from auto toodelayed-auto.</span></span>
