---
title: "Aplicativo de orquestração de patch do Azure Service Fabric | Microsoft Docs"
description: "Aplicativo para automatizar a aplicação de patch do sistema operacional em um cluster do Service Fabric."
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
ms.openlocfilehash: 2c5842822e347113e388d570f6ae603a313944d6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="patch-the-windows-operating-system-in-your-service-fabric-cluster"></a><span data-ttu-id="42474-103">Patch do sistema operacional Windows em seu cluster do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="42474-103">Patch the Windows operating system in your Service Fabric cluster</span></span>

<span data-ttu-id="42474-104">O aplicativo de orquestração de patch é um aplicativo do Azure Service Fabric que automatiza a aplicação de patches do sistema operacional em um cluster do Service Fabric no Azure sem tempo de inatividade.</span><span class="sxs-lookup"><span data-stu-id="42474-104">The patch orchestration application is an Azure Service Fabric application that automates operating system patching on a Service Fabric cluster on Azure without downtime.</span></span>

<span data-ttu-id="42474-105">O aplicativo de orquestração de patch fornece o seguinte:</span><span class="sxs-lookup"><span data-stu-id="42474-105">The patch orchestration app provides the following:</span></span>

- <span data-ttu-id="42474-106">**Instalação da atualização automática do sistema operacional**.</span><span class="sxs-lookup"><span data-stu-id="42474-106">**Automatic operating system update installation**.</span></span> <span data-ttu-id="42474-107">Atualizações do sistema operacional são baixadas e instaladas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="42474-107">Operating system updates are automatically downloaded and installed.</span></span> <span data-ttu-id="42474-108">Nós de cluster são reiniciados conforme necessário, sem tempo de inatividade do cluster.</span><span class="sxs-lookup"><span data-stu-id="42474-108">Cluster nodes are rebooted as needed without cluster downtime.</span></span>

- <span data-ttu-id="42474-109">**Aplicação de patch com suporte a cluster e integração de integridade**.</span><span class="sxs-lookup"><span data-stu-id="42474-109">**Cluster-aware patching and health integration**.</span></span> <span data-ttu-id="42474-110">Durante a aplicação de atualizações, o aplicativo de orquestração de patch monitora a integridade dos nós de cluster.</span><span class="sxs-lookup"><span data-stu-id="42474-110">While applying updates, the patch orchestration app monitors the health of the cluster nodes.</span></span> <span data-ttu-id="42474-111">Os nós de cluster fazem upgrade de um nó ou um domínio de atualização por vez.</span><span class="sxs-lookup"><span data-stu-id="42474-111">Cluster nodes are upgraded one node at a time or one upgrade domain at a time.</span></span> <span data-ttu-id="42474-112">Se a integridade do cluster falhar devido ao processo de aplicação de patch, a aplicação de patch será interrompida para evitar agravar o problema.</span><span class="sxs-lookup"><span data-stu-id="42474-112">If the health of the cluster goes down due to the patching process, patching is stopped to prevent aggravating the problem.</span></span>

## <a name="internal-details-of-the-app"></a><span data-ttu-id="42474-113">Detalhes internos do aplicativo</span><span class="sxs-lookup"><span data-stu-id="42474-113">Internal details of the app</span></span>

<span data-ttu-id="42474-114">O aplicativo de orquestração de patch é composto dos seguintes subcomponentes:</span><span class="sxs-lookup"><span data-stu-id="42474-114">The patch orchestration app is composed of the following subcomponents:</span></span>

- <span data-ttu-id="42474-115">**Serviço de Coordenador**: este serviço com estado é responsável por:</span><span class="sxs-lookup"><span data-stu-id="42474-115">**Coordinator Service**: This stateful service is responsible for:</span></span>
    - <span data-ttu-id="42474-116">Coordenar o trabalho do Windows Update em todo o cluster.</span><span class="sxs-lookup"><span data-stu-id="42474-116">Coordinating the Windows Update job on the entire cluster.</span></span>
    - <span data-ttu-id="42474-117">Armazenar o resultado das operações concluídas do Windows Update.</span><span class="sxs-lookup"><span data-stu-id="42474-117">Storing the result of completed Windows Update operations.</span></span>
- <span data-ttu-id="42474-118">**Serviço de Agente do Nó**: é um serviço sem estado, executado em todos os nós de cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="42474-118">**Node Agent Service**: This stateless service runs on all Service Fabric cluster nodes.</span></span> <span data-ttu-id="42474-119">O serviço é responsável por:</span><span class="sxs-lookup"><span data-stu-id="42474-119">The service is responsible for:</span></span>
    - <span data-ttu-id="42474-120">Inicialização de NTService do Agente do Nó.</span><span class="sxs-lookup"><span data-stu-id="42474-120">Bootstrapping the Node Agent NTService.</span></span>
    - <span data-ttu-id="42474-121">Monitoramento do NTService do Agente do Nó.</span><span class="sxs-lookup"><span data-stu-id="42474-121">Monitoring the Node Agent NTService.</span></span>
- <span data-ttu-id="42474-122">**NTService do Agente do Nó**: este serviço Windows NT é executado em um privilégio de nível superior (SISTEMA).</span><span class="sxs-lookup"><span data-stu-id="42474-122">**Node Agent NTService**: This Windows NT service runs at a higher-level privilege (SYSTEM).</span></span> <span data-ttu-id="42474-123">Em comparação, o Serviço de Agente do Nó e o Serviço de Coordenador são executados em um nível inferior de privilégio (SERVIÇO DE REDE).</span><span class="sxs-lookup"><span data-stu-id="42474-123">In contrast, the Node Agent Service and the Coordinator Service run at a lower-level privilege (NETWORK SERVICE).</span></span> <span data-ttu-id="42474-124">O serviço é responsável por executar os seguintes trabalhos do Windows Update em todos os nós de cluster:</span><span class="sxs-lookup"><span data-stu-id="42474-124">The service is responsible for performing the following Windows Update jobs on all the cluster nodes:</span></span>
    - <span data-ttu-id="42474-125">Desabilitar o Windows Update automático no nó.</span><span class="sxs-lookup"><span data-stu-id="42474-125">Disabling automatic Windows Update on the node.</span></span>
    - <span data-ttu-id="42474-126">Baixar e instalar o Windows Update de acordo com a política que o usuário forneceu.</span><span class="sxs-lookup"><span data-stu-id="42474-126">Downloading and installing Windows Update according to the policy the user has provided.</span></span>
    - <span data-ttu-id="42474-127">Reiniciar o computador após a instalação do Windows Update.</span><span class="sxs-lookup"><span data-stu-id="42474-127">Restarting the machine post Windows Update installation.</span></span>
    - <span data-ttu-id="42474-128">Carregar os resultados das atualizações do Windows para o Serviço do Coordenador.</span><span class="sxs-lookup"><span data-stu-id="42474-128">Uploading the results of Windows updates to the Coordinator Service.</span></span>
    - <span data-ttu-id="42474-129">Relatórios de integridade de relatórios no caso de falha na operação após esgotar todas as novas tentativas.</span><span class="sxs-lookup"><span data-stu-id="42474-129">Reporting health reports in case an operation has failed after exhausting all retries.</span></span>

> [!NOTE]
> <span data-ttu-id="42474-130">O aplicativo de orquestração de patch usa o serviço do sistema do gerenciador de reparo do Service Fabric para habilitar ou desabilitar o nó e executar as verificações de integridade.</span><span class="sxs-lookup"><span data-stu-id="42474-130">The patch orchestration app uses the Service Fabric repair manager system service to disable or enable the node and perform health checks.</span></span> <span data-ttu-id="42474-131">A tarefa de reparo criada pelo aplicativo de orquestração de patch rastreia o progresso do Windows Update para cada nó.</span><span class="sxs-lookup"><span data-stu-id="42474-131">The repair task created by the patch orchestration app tracks the Windows Update progress for each node.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42474-132">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="42474-132">Prerequisites</span></span>

### <a name="minimum-supported-service-fabric-runtime-version"></a><span data-ttu-id="42474-133">Versão de tempo de execução do Service Fabric com suporte mínimo</span><span class="sxs-lookup"><span data-stu-id="42474-133">Minimum supported Service Fabric runtime version</span></span>

#### <a name="azure-clusters"></a><span data-ttu-id="42474-134">Clusters do Azure</span><span class="sxs-lookup"><span data-stu-id="42474-134">Azure clusters</span></span>
<span data-ttu-id="42474-135">O aplicativo de orquestração de patch deve ser executado nos clusters do Azure que têm a versão de tempo de execução v5.5 ou posterior do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="42474-135">The patch orchestration app must be run on Azure clusters that have Service Fabric runtime version v5.5 or later.</span></span>

#### <a name="standalone-on-premises-clusters"></a><span data-ttu-id="42474-136">Clusters locais autônomos</span><span class="sxs-lookup"><span data-stu-id="42474-136">Standalone on-premises Clusters</span></span>
<span data-ttu-id="42474-137">O aplicativo de orquestração de patch deve ser executado nos clusters autônomos que têm a versão de tempo de execução v5.6 ou posterior do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="42474-137">The patch orchestration app must be run on Standalone clusters that have Service Fabric runtime version v5.6 or later.</span></span>

### <a name="enable-the-repair-manager-service-if-its-not-running-already"></a><span data-ttu-id="42474-138">Habilite o serviço do gerenciador de reparo (se ainda não estiver em execução)</span><span class="sxs-lookup"><span data-stu-id="42474-138">Enable the repair manager service (if it's not running already)</span></span>

<span data-ttu-id="42474-139">O aplicativo de orquestração de patch exige que o serviço do sistema do gerenciador de reparo esteja habilitado no cluster.</span><span class="sxs-lookup"><span data-stu-id="42474-139">The patch orchestration app requires the repair manager system service to be enabled on the cluster.</span></span>

#### <a name="azure-clusters"></a><span data-ttu-id="42474-140">Clusters do Azure</span><span class="sxs-lookup"><span data-stu-id="42474-140">Azure clusters</span></span>

<span data-ttu-id="42474-141">Clusters do Azure na camada de durabilidade prata têm o serviço do gerenciador de reparo habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="42474-141">Azure clusters in the silver durability tier have the repair manager service enabled by default.</span></span> <span data-ttu-id="42474-142">Clusters do Azure na camada de durabilidade ouro podem ou não ter o serviço do gerenciador de reparo habilitado, dependendo de quando esses clusters foram criados.</span><span class="sxs-lookup"><span data-stu-id="42474-142">Azure clusters in the gold durability tier might or might not have the repair manager service enabled, depending on when those clusters were created.</span></span> <span data-ttu-id="42474-143">Cluster do Azure na camada de durabilidade bronze, por padrão, não têm o serviço do gerenciador de reparo habilitado.</span><span class="sxs-lookup"><span data-stu-id="42474-143">Azure clusters in the bronze durability tier, by default, do not have the repair manager service enabled.</span></span> <span data-ttu-id="42474-144">Se o serviço já está habilitado, você pode ver ele em execução na seção de serviços do sistema no Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="42474-144">If the service is already enabled, you can see it running in the system services section in the Service Fabric Explorer.</span></span>

##### <a name="azure-portal"></a><span data-ttu-id="42474-145">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="42474-145">Azure portal</span></span>
<span data-ttu-id="42474-146">Você pode habilitar o Gerenciador de reparo do portal do Azure no momento da configuração do cluster.</span><span class="sxs-lookup"><span data-stu-id="42474-146">You can enable repair manager from Azure portal at the time of setting up of cluster.</span></span> <span data-ttu-id="42474-147">Selecione a opção `Include Repair Manager` em `Add on features` no momento da configuração de Cluster.</span><span class="sxs-lookup"><span data-stu-id="42474-147">Select `Include Repair Manager` option under `Add on features` at the time of Cluster configuration.</span></span>
<span data-ttu-id="42474-148">![Imagem do Gerenciador de reparo de habilitação do portal do Azure](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)</span><span class="sxs-lookup"><span data-stu-id="42474-148">![Image of Enabling Repair Manager from Azure portal](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)</span></span>

##### <a name="azure-resource-manager-template"></a><span data-ttu-id="42474-149">Modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="42474-149">Azure Resource Manager template</span></span>
<span data-ttu-id="42474-150">Como alternativa, você pode usar o [modelo do Azure Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) para habilitar o serviço do gerenciador de reparo em clusters novos e existentes do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="42474-150">Alternatively you can use the [Azure Resource Manager template](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) to enable the repair manager service on new and existing Service Fabric clusters.</span></span> <span data-ttu-id="42474-151">Obtenha o modelo para o cluster que você deseja implantar.</span><span class="sxs-lookup"><span data-stu-id="42474-151">Get the template for the cluster that you want to deploy.</span></span> <span data-ttu-id="42474-152">Você pode usar os modelos de exemplo ou criar um modelo do Resource Manager personalizado.</span><span class="sxs-lookup"><span data-stu-id="42474-152">You can either use the sample templates or create a custom Resource Manager template.</span></span> 

<span data-ttu-id="42474-153">Para habilitar o serviço de Gerenciador de reparo usando [modelo do Azure Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):</span><span class="sxs-lookup"><span data-stu-id="42474-153">To enable the repair manager service using [Azure Resource Manager template](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):</span></span>

1. <span data-ttu-id="42474-154">Primeiro, verifique se a `apiversion` está definida como `2017-07-01-preview` para o recurso `Microsoft.ServiceFabric/clusters`, conforme mostrado no trecho a seguir.</span><span class="sxs-lookup"><span data-stu-id="42474-154">First check that the `apiversion` is set to `2017-07-01-preview` for the `Microsoft.ServiceFabric/clusters` resource, as shown in the following snippet.</span></span> <span data-ttu-id="42474-155">Se for diferente, você precisará atualizar a `apiVersion` para o valor `2017-07-01-preview`:</span><span class="sxs-lookup"><span data-stu-id="42474-155">If it is different, then you need to update the `apiVersion` to the value `2017-07-01-preview`:</span></span>

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. <span data-ttu-id="42474-156">Agora habilite o serviço do gerenciador de reparo adicionando a seguinte seção `addonFeatures` após a seção `fabricSettings`:</span><span class="sxs-lookup"><span data-stu-id="42474-156">Now enable the repair manager service by adding the following `addonFeatures` section after the `fabricSettings` section:</span></span>

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. <span data-ttu-id="42474-157">Depois de atualizar o modelo de cluster com essas alterações, aplique-as e permita a conclusão do upgrade.</span><span class="sxs-lookup"><span data-stu-id="42474-157">After you have updated your cluster template with these changes, apply them and let the upgrade finish.</span></span> <span data-ttu-id="42474-158">Agora você pode ver o serviço do sistema do gerenciador de reparo em execução no cluster.</span><span class="sxs-lookup"><span data-stu-id="42474-158">You can now see the repair manager system service running in your cluster.</span></span> <span data-ttu-id="42474-159">Ele é chamado de `fabric:/System/RepairManagerService` na seção de serviços do sistema no Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="42474-159">It is called `fabric:/System/RepairManagerService` in the system services section in the Service Fabric Explorer.</span></span> 

### <a name="standalone-on-premises-clusters"></a><span data-ttu-id="42474-160">Clusters locais autônomos</span><span class="sxs-lookup"><span data-stu-id="42474-160">Standalone on-premises clusters</span></span>

<span data-ttu-id="42474-161">Você pode usar as [Definições de configuração para o cluster autônomo do Windows](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) para habilitar o serviço do gerenciador de reparo em clusters novos e existentes do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="42474-161">You can use the [Configuration settings for standalone Windows cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) to enable the repair manager service on new and existing Service Fabric cluster.</span></span>

<span data-ttu-id="42474-162">Para habilitar o serviço do gerenciador de reparo:</span><span class="sxs-lookup"><span data-stu-id="42474-162">To enable the repair manager service:</span></span>

1. <span data-ttu-id="42474-163">Primeiro verifique se o `apiversion` nas [Configurações de cluster geral](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) está definido como `04-2017` ou superior:</span><span class="sxs-lookup"><span data-stu-id="42474-163">First check that the `apiversion` in [General cluster configurations](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) is set to `04-2017` or higher:</span></span>

    ```json
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "04-2017",
        ...
    }
    ```

2. <span data-ttu-id="42474-164">Agora habilite o serviço do gerenciador de reparo adicionando a seguinte seção `addonFeaturres` após a seção `fabricSettings`, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="42474-164">Now enable repair manager service by adding the following `addonFeaturres` section after the `fabricSettings` section as shown below:</span></span>

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. <span data-ttu-id="42474-165">Atualize o manifesto do cluster com essas alterações, usando o manifesto do cluster atualizado [crie um novo cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) ou [atualize a configuração do cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration).</span><span class="sxs-lookup"><span data-stu-id="42474-165">Update your cluster manifest with these changes, using the updated cluster manifest [create a new cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) or [upgrade the cluster configuration](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration).</span></span> <span data-ttu-id="42474-166">Com o cluster em execução com o manifesto do cluster atualizado, agora você poderá ver o serviço do sistema do gerenciador de reparo em execução no seu cluster, que é chamado de `fabric:/System/RepairManagerService`, sob a seção de serviços do sistema no Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="42474-166">Once the cluster is running with updated cluster manifest, you can now see the repair manager system service running in your cluster, which is called `fabric:/System/RepairManagerService`, under system services section in the Service Fabric explorer.</span></span>

### <a name="disable-automatic-windows-update-on-all-nodes"></a><span data-ttu-id="42474-167">Desabilite o Windows Update automático em todos os nós</span><span class="sxs-lookup"><span data-stu-id="42474-167">Disable automatic Windows Update on all nodes</span></span>

<span data-ttu-id="42474-168">As atualizações automáticas do Windows podem causar a perda de disponibilidade porque vários nós de cluster podem ser reiniciados ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="42474-168">Automatic Windows updates might lead to availability loss because multiple cluster nodes can restart at the same time.</span></span> <span data-ttu-id="42474-169">O aplicativo de orquestração de patch, por padrão tenta desabilitar o Windows Update automático em cada nó de cluster.</span><span class="sxs-lookup"><span data-stu-id="42474-169">The patch orchestration app, by default, tries to disable the automatic Windows Update on each cluster node.</span></span> <span data-ttu-id="42474-170">No entanto, se as configurações forem gerenciadas pela política de grupo ou administrador, é recomendável configurar a política do Windows Update explicitamente como "Notificar antes de baixar".</span><span class="sxs-lookup"><span data-stu-id="42474-170">However, if the settings are managed by an administrator or group policy, we recommend setting the Windows Update policy to “Notify before Download” explicitly.</span></span>

### <a name="optional-enable-azure-diagnostics"></a><span data-ttu-id="42474-171">Opcional: habilitar o Diagnóstico do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="42474-171">Optional: Enable Azure Diagnostics</span></span>

<span data-ttu-id="42474-172">Clusters que executam a versão de tempo de execução do Service Fabric `5.6.220.9494` e acima de logs de aplicativo de orquestração patch coletar como parte da malha do serviço de logs.</span><span class="sxs-lookup"><span data-stu-id="42474-172">Clusters running Service Fabric runtime version `5.6.220.9494` and above collect patch orchestration app logs as part of Service Fabric logs.</span></span>
<span data-ttu-id="42474-173">Você pode ignorar esta etapa se o cluster está em execução na versão de tempo de execução do Service Fabric `5.6.220.9494` e acima.</span><span class="sxs-lookup"><span data-stu-id="42474-173">You can skip this step if your cluster is running on Service Fabric runtime version `5.6.220.9494` and above.</span></span>

<span data-ttu-id="42474-174">Para clusters que executam a versão de tempo de execução do Service Fabric menor `5.6.220.9494`, logs do aplicativo de orquestração de patch são coletados localmente em cada um de nós do cluster.</span><span class="sxs-lookup"><span data-stu-id="42474-174">For clusters running Service Fabric runtime version less than `5.6.220.9494`, logs for the patch orchestration app are collected locally on each of the cluster nodes.</span></span>
<span data-ttu-id="42474-175">É recomendável que você configure o diagnóstico do Azure para carregar os logs de todos os nós em um local central.</span><span class="sxs-lookup"><span data-stu-id="42474-175">We recommend that you configure Azure Diagnostics to upload logs from all nodes to a central location.</span></span>

<span data-ttu-id="42474-176">Para obter mais informações sobre o Diagnóstico do Microsoft Azure, consulte [Coletar logs usando o Diagnóstico do Microsoft Azure](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad).</span><span class="sxs-lookup"><span data-stu-id="42474-176">For information on enabling Azure Diagnostics, see [Collect logs by using Azure Diagnostics](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad).</span></span>

<span data-ttu-id="42474-177">Os logs para o aplicativo de orquestração de patch serão gerados nas seguintes IDs de provedor fixas:</span><span class="sxs-lookup"><span data-stu-id="42474-177">Logs for the patch orchestration app are generated on the following fixed provider IDs:</span></span>

- <span data-ttu-id="42474-178">e39b723c-590c-4090-abb0-11e3e6616346</span><span class="sxs-lookup"><span data-stu-id="42474-178">e39b723c-590c-4090-abb0-11e3e6616346</span></span>
- <span data-ttu-id="42474-179">fc0028ff-bfdc-499f-80dc-ed922c52c5e9</span><span class="sxs-lookup"><span data-stu-id="42474-179">fc0028ff-bfdc-499f-80dc-ed922c52c5e9</span></span>
- <span data-ttu-id="42474-180">24afa313-0d3b-4c7c-b485-1047fd964b60</span><span class="sxs-lookup"><span data-stu-id="42474-180">24afa313-0d3b-4c7c-b485-1047fd964b60</span></span>
- <span data-ttu-id="42474-181">05dc046c-60e9-4ef7-965e-91660adffa68</span><span class="sxs-lookup"><span data-stu-id="42474-181">05dc046c-60e9-4ef7-965e-91660adffa68</span></span>

<span data-ttu-id="42474-182">No modelo do Resource Manager acesse a seção `EtwEventSourceProviderConfiguration` em `WadCfg` e adicione as seguintes entradas:</span><span class="sxs-lookup"><span data-stu-id="42474-182">In Resource Manager template goto `EtwEventSourceProviderConfiguration` section under `WadCfg` and add the following entries:</span></span>

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
> <span data-ttu-id="42474-183">Se o cluster do Service Fabric tiver vários tipos de nó, a seção anterior deve ser adicionada para todas as seções `WadCfg`.</span><span class="sxs-lookup"><span data-stu-id="42474-183">If your Service Fabric cluster has multiple node types, then the previous section must be added for all the `WadCfg` sections.</span></span>

## <a name="download-the-app-package"></a><span data-ttu-id="42474-184">Baixar o pacote do aplicativo</span><span class="sxs-lookup"><span data-stu-id="42474-184">Download the app package</span></span>

<span data-ttu-id="42474-185">Baixe o aplicativo usando o [link para download](https://go.microsoft.com/fwlink/P/?linkid=849590).</span><span class="sxs-lookup"><span data-stu-id="42474-185">Download the application from the [download link](https://go.microsoft.com/fwlink/P/?linkid=849590).</span></span>

## <a name="configure-the-app"></a><span data-ttu-id="42474-186">Configurar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="42474-186">Configure the app</span></span>

<span data-ttu-id="42474-187">O comportamento do aplicativo de orquestração de patch pode ser configurado para atender às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="42474-187">The behavior of the patch orchestration app can be configured to meet your needs.</span></span> <span data-ttu-id="42474-188">Substitua os valores padrão passando o parâmetro de aplicativo durante a criação ou atualização do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="42474-188">Override the default values by passing in the application parameter during application creation or update.</span></span> <span data-ttu-id="42474-189">Parâmetros do aplicativo podem ser fornecidos especificando `ApplicationParameter` aos cmdlets `Start-ServiceFabricApplicationUpgrade` ou `New-ServiceFabricApplication`.</span><span class="sxs-lookup"><span data-stu-id="42474-189">Application parameters can be provided by specifying `ApplicationParameter` to the `Start-ServiceFabricApplicationUpgrade` or `New-ServiceFabricApplication` cmdlets.</span></span>

|<span data-ttu-id="42474-190">**Parâmetro**</span><span class="sxs-lookup"><span data-stu-id="42474-190">**Parameter**</span></span>        |<span data-ttu-id="42474-191">**Tipo**</span><span class="sxs-lookup"><span data-stu-id="42474-191">**Type**</span></span>                          | <span data-ttu-id="42474-192">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="42474-192">**Details**</span></span>|
|:-|-|-|
|<span data-ttu-id="42474-193">MaxResultsToCache</span><span class="sxs-lookup"><span data-stu-id="42474-193">MaxResultsToCache</span></span>    |<span data-ttu-id="42474-194">long</span><span class="sxs-lookup"><span data-stu-id="42474-194">Long</span></span>                              | <span data-ttu-id="42474-195">Número máximo de resultados do Windows Update, que devem ser armazenados em cache.</span><span class="sxs-lookup"><span data-stu-id="42474-195">Maximum number of Windows Update results, which should be cached.</span></span> <br><span data-ttu-id="42474-196">O valor padrão é 3000, supondo que o:</span><span class="sxs-lookup"><span data-stu-id="42474-196">Default value is 3000 assuming the:</span></span> <br> <span data-ttu-id="42474-197">- Número de nós é 20.</span><span class="sxs-lookup"><span data-stu-id="42474-197">- Number of nodes is 20.</span></span> <br> <span data-ttu-id="42474-198">- Número de atualizações acontecendo em um nó por mês seja de cinco.</span><span class="sxs-lookup"><span data-stu-id="42474-198">- Number of updates happening on a node per month is five.</span></span> <br> <span data-ttu-id="42474-199">– Número de resultados por operação possa ser de 10.</span><span class="sxs-lookup"><span data-stu-id="42474-199">- Number of results per operation can be 10.</span></span> <br> <span data-ttu-id="42474-200">- Resultados para os últimos três meses devem ser armazenados.</span><span class="sxs-lookup"><span data-stu-id="42474-200">- Results for the past three months should be stored.</span></span> |
|<span data-ttu-id="42474-201">TaskApprovalPolicy</span><span class="sxs-lookup"><span data-stu-id="42474-201">TaskApprovalPolicy</span></span>   |<span data-ttu-id="42474-202">Enum</span><span class="sxs-lookup"><span data-stu-id="42474-202">Enum</span></span> <br> <span data-ttu-id="42474-203">{ NodeWise, UpgradeDomainWise }</span><span class="sxs-lookup"><span data-stu-id="42474-203">{ NodeWise, UpgradeDomainWise }</span></span>                          |<span data-ttu-id="42474-204">A TaskApprovalPolicy indica a política a ser usada pelo Serviço do Coordinator para instalar atualizações do Windows em todos os nós de cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="42474-204">TaskApprovalPolicy indicates the policy that is to be used by the Coordinator Service to install Windows updates across the Service Fabric cluster nodes.</span></span><br>                         <span data-ttu-id="42474-205">Valores permitidos são:</span><span class="sxs-lookup"><span data-stu-id="42474-205">Allowed values are:</span></span> <br>                                                           <span data-ttu-id="42474-206"><b>NodeWise</b>.</span><span class="sxs-lookup"><span data-stu-id="42474-206"><b>NodeWise</b>.</span></span> <span data-ttu-id="42474-207">O Windows Update é instalado em um nó por vez.</span><span class="sxs-lookup"><span data-stu-id="42474-207">Windows Update is installed one node at a time.</span></span> <br>                                                           <span data-ttu-id="42474-208"><b>UpgradeDomainWise</b>.</span><span class="sxs-lookup"><span data-stu-id="42474-208"><b>UpgradeDomainWise</b>.</span></span> <span data-ttu-id="42474-209">O Windows Update é instalado em um domínio de atualização por vez.</span><span class="sxs-lookup"><span data-stu-id="42474-209">Windows Update is installed one upgrade domain at a time.</span></span> <span data-ttu-id="42474-210">(No máximo, todos os nós que pertencem a um domínio de atualização podem ir para o Windows Update.)</span><span class="sxs-lookup"><span data-stu-id="42474-210">(At the maximum, all the nodes belonging to an upgrade domain can go for Windows Update.)</span></span>
|<span data-ttu-id="42474-211">LogsDiskQuotaInMB</span><span class="sxs-lookup"><span data-stu-id="42474-211">LogsDiskQuotaInMB</span></span>   |<span data-ttu-id="42474-212">long</span><span class="sxs-lookup"><span data-stu-id="42474-212">Long</span></span>  <br> <span data-ttu-id="42474-213">(Padrão: 1024)</span><span class="sxs-lookup"><span data-stu-id="42474-213">(Default: 1024)</span></span>               |<span data-ttu-id="42474-214">Tamanho máximo dos logs do aplicativo de orquestração de patch em MB, que pode ser mantido localmente no nó.</span><span class="sxs-lookup"><span data-stu-id="42474-214">Maximum size of patch orchestration app logs in MB, which can be persisted locally on nodes.</span></span>
| <span data-ttu-id="42474-215">WUQuery</span><span class="sxs-lookup"><span data-stu-id="42474-215">WUQuery</span></span>               | <span data-ttu-id="42474-216">string</span><span class="sxs-lookup"><span data-stu-id="42474-216">string</span></span><br><span data-ttu-id="42474-217">(Padrão: "IsInstalled=0")</span><span class="sxs-lookup"><span data-stu-id="42474-217">(Default: "IsInstalled=0")</span></span>                | <span data-ttu-id="42474-218">Consulta para obter atualizações do Windows.</span><span class="sxs-lookup"><span data-stu-id="42474-218">Query to get Windows updates.</span></span> <span data-ttu-id="42474-219">Para obter mais informações, consulte [WuQuery.](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx)</span><span class="sxs-lookup"><span data-stu-id="42474-219">For more information, see [WuQuery.](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx)</span></span>
| <span data-ttu-id="42474-220">InstallWindowsOSOnlyUpdates</span><span class="sxs-lookup"><span data-stu-id="42474-220">InstallWindowsOSOnlyUpdates</span></span> | <span data-ttu-id="42474-221">Bool</span><span class="sxs-lookup"><span data-stu-id="42474-221">Bool</span></span> <br> <span data-ttu-id="42474-222">(padrão: True)</span><span class="sxs-lookup"><span data-stu-id="42474-222">(default: True)</span></span>                 | <span data-ttu-id="42474-223">Esse sinalizador permite a instalação das atualizações do sistema operacional Windows.</span><span class="sxs-lookup"><span data-stu-id="42474-223">This flag allows Windows operating system updates to be installed.</span></span>            |
| <span data-ttu-id="42474-224">WUOperationTimeOutInMinutes</span><span class="sxs-lookup"><span data-stu-id="42474-224">WUOperationTimeOutInMinutes</span></span> | <span data-ttu-id="42474-225">int</span><span class="sxs-lookup"><span data-stu-id="42474-225">Int</span></span> <br><span data-ttu-id="42474-226">(Padrão: 90)</span><span class="sxs-lookup"><span data-stu-id="42474-226">(Default: 90)</span></span>                   | <span data-ttu-id="42474-227">Especifica o tempo limite para qualquer operação do Windows Update (pesquisar, baixar ou instalar).</span><span class="sxs-lookup"><span data-stu-id="42474-227">Specifies the timeout for any Windows Update operation (search or download or install).</span></span> <span data-ttu-id="42474-228">Se a operação não for concluída dentro do tempo limite especificado, ela será anulada.</span><span class="sxs-lookup"><span data-stu-id="42474-228">If the operation is not completed within the specified timeout, it is aborted.</span></span>       |
| <span data-ttu-id="42474-229">WURescheduleCount</span><span class="sxs-lookup"><span data-stu-id="42474-229">WURescheduleCount</span></span>     | <span data-ttu-id="42474-230">int</span><span class="sxs-lookup"><span data-stu-id="42474-230">Int</span></span> <br> <span data-ttu-id="42474-231">(Padrão: 5)</span><span class="sxs-lookup"><span data-stu-id="42474-231">(Default: 5)</span></span>                  | <span data-ttu-id="42474-232">O número máximo de vezes que o serviço reagendaria o Windows Update no caso de falha persistente na operação.</span><span class="sxs-lookup"><span data-stu-id="42474-232">The maximum number of times the service reschedules the Windows update in case an operation fails persistently.</span></span>          |
| <span data-ttu-id="42474-233">WURescheduleTimeInMinutes</span><span class="sxs-lookup"><span data-stu-id="42474-233">WURescheduleTimeInMinutes</span></span> | <span data-ttu-id="42474-234">int</span><span class="sxs-lookup"><span data-stu-id="42474-234">Int</span></span> <br><span data-ttu-id="42474-235">(Padrão: 30)</span><span class="sxs-lookup"><span data-stu-id="42474-235">(Default: 30)</span></span> | <span data-ttu-id="42474-236">O intervalo ao qual o serviço reagendaria o Windows Update no caso de persistência da falha.</span><span class="sxs-lookup"><span data-stu-id="42474-236">The interval at which the service reschedules the Windows update in case failure persists.</span></span> |
| <span data-ttu-id="42474-237">WUFrequency</span><span class="sxs-lookup"><span data-stu-id="42474-237">WUFrequency</span></span>           | <span data-ttu-id="42474-238">Cadeia de caracteres separada por vírgula (padrão: "Semanalmente, quarta-feira, 7:00:00")</span><span class="sxs-lookup"><span data-stu-id="42474-238">Comma-separated string (Default: "Weekly, Wednesday, 7:00:00")</span></span>     | <span data-ttu-id="42474-239">A frequência para a instalação do Windows Update.</span><span class="sxs-lookup"><span data-stu-id="42474-239">The frequency for installing Windows Update.</span></span> <span data-ttu-id="42474-240">O formato e os valores possíveis são:</span><span class="sxs-lookup"><span data-stu-id="42474-240">The format and possible values are:</span></span> <br><span data-ttu-id="42474-241">-   Mensal, DD, HH:MM:SS, por exemplo, Mensal, 5, 12:22:32.</span><span class="sxs-lookup"><span data-stu-id="42474-241">-   Monthly, DD,HH:MM:SS, for example, Monthly, 5,12:22:32.</span></span> <br> <span data-ttu-id="42474-242">-   Semanal, DIA, HH:MM:SS, por exemplo, Semanal, terça-feira, 12:22:32.</span><span class="sxs-lookup"><span data-stu-id="42474-242">-   Weekly, DAY,HH:MM:SS, for example, Weekly, Tuesday, 12:22:32.</span></span>  <br> <span data-ttu-id="42474-243">-   Diário, HH:MM:SS, por exemplo, Diário, 12:22:32.</span><span class="sxs-lookup"><span data-stu-id="42474-243">-   Daily, HH:MM:SS, for example, Daily, 12:22:32.</span></span>  <br> <span data-ttu-id="42474-244">-  Nenhum indica que o Windows Update não deve ser executado.</span><span class="sxs-lookup"><span data-stu-id="42474-244">-  None indicates that Windows Update shouldn't be done.</span></span>  <br><br> <span data-ttu-id="42474-245">Observe que todos os horários estão em UTC.</span><span class="sxs-lookup"><span data-stu-id="42474-245">Note that all the times are in UTC.</span></span>|
| <span data-ttu-id="42474-246">AcceptWindowsUpdateEula</span><span class="sxs-lookup"><span data-stu-id="42474-246">AcceptWindowsUpdateEula</span></span> | <span data-ttu-id="42474-247">Bool</span><span class="sxs-lookup"><span data-stu-id="42474-247">Bool</span></span> <br><span data-ttu-id="42474-248">(Padrão: true)</span><span class="sxs-lookup"><span data-stu-id="42474-248">(Default: true)</span></span> | <span data-ttu-id="42474-249">Ao definir esse sinalizador, o aplicativo aceita o Contrato de licença do usuário final para o Windows Update em nome do proprietário do computador.</span><span class="sxs-lookup"><span data-stu-id="42474-249">By setting this flag, the application accepts the End-User License Agreement for Windows Update on behalf of the owner of the machine.</span></span>              |

> [!TIP]
> <span data-ttu-id="42474-250">Se você quiser que o Windows Update seja executado imediatamente, defina `WUFrequency` em relação ao tempo de implantação do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="42474-250">If you want Windows Update to happen immediately, set `WUFrequency` relative to the application deployment time.</span></span> <span data-ttu-id="42474-251">Por exemplo, suponha que você tem um cluster de teste de cinco nós e planeja implantar o aplicativo em torno de 5:00 PM UTC.</span><span class="sxs-lookup"><span data-stu-id="42474-251">For example, suppose that you have a five-node test cluster and plan to deploy the app at around 5:00 PM UTC.</span></span> <span data-ttu-id="42474-252">Se você considera que o upgrade ou implantação do aplicativo leva 30 minutos no máximo, defina a WUFrequency como "Diariamente, 17:30:00".</span><span class="sxs-lookup"><span data-stu-id="42474-252">If you assume that the application upgrade or deployment takes 30 minutes at the maximum, set the WUFrequency as "Daily, 17:30:00."</span></span>

## <a name="deploy-the-app"></a><span data-ttu-id="42474-253">Implantar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="42474-253">Deploy the app</span></span>

1. <span data-ttu-id="42474-254">Conclua todas as etapas necessárias para preparar o cluster.</span><span class="sxs-lookup"><span data-stu-id="42474-254">Finish all the prerequisite steps to prepare the cluster.</span></span>
2. <span data-ttu-id="42474-255">Implante o aplicativo de orquestração de patch como qualquer outro aplicativo do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="42474-255">Deploy the patch orchestration app like any other Service Fabric app.</span></span> <span data-ttu-id="42474-256">Você pode implantar o aplicativo usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="42474-256">You can deploy the app by using PowerShell.</span></span> <span data-ttu-id="42474-257">Siga as etapas em [Implantar e remover aplicativos usando o PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span><span class="sxs-lookup"><span data-stu-id="42474-257">Follow the steps in [Deploy and remove applications using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span></span>
3. <span data-ttu-id="42474-258">Para configurar o aplicativo no momento da implantação, passe o `ApplicationParamater` para o cmdlet `New-ServiceFabricApplication`.</span><span class="sxs-lookup"><span data-stu-id="42474-258">To configure the application at the time of deployment, pass the `ApplicationParamater` to the `New-ServiceFabricApplication` cmdlet.</span></span> <span data-ttu-id="42474-259">Para sua conveniência, fornecemos o script Deploy.ps1 juntamente com o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="42474-259">For your convenience, we’ve provided the script Deploy.ps1 along with the application.</span></span> <span data-ttu-id="42474-260">Para usar o script:</span><span class="sxs-lookup"><span data-stu-id="42474-260">To use the script:</span></span>

    - <span data-ttu-id="42474-261">Conectar a um cluster do Service Fabric usando `Connect-ServiceFabricCluster`.</span><span class="sxs-lookup"><span data-stu-id="42474-261">Connect to a Service Fabric cluster by using `Connect-ServiceFabricCluster`.</span></span>
    - <span data-ttu-id="42474-262">Execute o script do PowerShell Deploy.ps1 com o valor `ApplicationParameter` apropriado.</span><span class="sxs-lookup"><span data-stu-id="42474-262">Execute the PowerShell script Deploy.ps1 with the appropriate `ApplicationParameter` value.</span></span>

> [!NOTE]
> <span data-ttu-id="42474-263">Mantenha a pasta de scripts e de aplicativos PatchOrchestrationApplication no mesmo diretório.</span><span class="sxs-lookup"><span data-stu-id="42474-263">Keep the script and the application folder PatchOrchestrationApplication in the same directory.</span></span>

## <a name="upgrade-the-app"></a><span data-ttu-id="42474-264">Upgrade do aplicativo</span><span class="sxs-lookup"><span data-stu-id="42474-264">Upgrade the app</span></span>

<span data-ttu-id="42474-265">Para fazer upgrade de um aplicativo de orquestração de patch existente usando o PowerShell, execute as etapas em [Upgrade do aplicativo do Service Fabric usando o PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell).</span><span class="sxs-lookup"><span data-stu-id="42474-265">To upgrade an existing patch orchestration app by using PowerShell, follow the steps in [Service Fabric application upgrade using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell).</span></span>

## <a name="remove-the-app"></a><span data-ttu-id="42474-266">Remover o aplicativo</span><span class="sxs-lookup"><span data-stu-id="42474-266">Remove the app</span></span>

<span data-ttu-id="42474-267">Para remover o aplicativo, siga as etapas em [Implantar e remover aplicativos usando o PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span><span class="sxs-lookup"><span data-stu-id="42474-267">To remove the application, follow the steps in [Deploy and remove applications using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span></span>

<span data-ttu-id="42474-268">Para sua conveniência, fornecemos o script Undeploy.ps1 juntamente com o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="42474-268">For your convenience, we've provided the script Undeploy.ps1 along with the application.</span></span> <span data-ttu-id="42474-269">Para usar o script:</span><span class="sxs-lookup"><span data-stu-id="42474-269">To use the script:</span></span>

  - <span data-ttu-id="42474-270">Conectar a um cluster do Service Fabric usando ```Connect-ServiceFabricCluster```.</span><span class="sxs-lookup"><span data-stu-id="42474-270">Connect to a Service Fabric cluster by using ```Connect-ServiceFabricCluster```.</span></span>

  - <span data-ttu-id="42474-271">Execute o script do PowerShell Undeploy.ps1.</span><span class="sxs-lookup"><span data-stu-id="42474-271">Execute the PowerShell script Undeploy.ps1.</span></span>

> [!NOTE]
> <span data-ttu-id="42474-272">Mantenha a pasta de scripts e de aplicativos PatchOrchestrationApplication no mesmo diretório.</span><span class="sxs-lookup"><span data-stu-id="42474-272">Keep the script and the application folder PatchOrchestrationApplication in the same directory.</span></span>

## <a name="view-the-windows-update-results"></a><span data-ttu-id="42474-273">Exibir os resultados do Windows Update</span><span class="sxs-lookup"><span data-stu-id="42474-273">View the Windows Update results</span></span>

<span data-ttu-id="42474-274">O aplicativo de orquestração de patch expõe as APIs REST para exibir os resultados históricos do usuário.</span><span class="sxs-lookup"><span data-stu-id="42474-274">The patch orchestration app exposes REST APIs to display the historical results to the user.</span></span> <span data-ttu-id="42474-275">Um exemplo de resultado JSON:</span><span class="sxs-lookup"><span data-stu-id="42474-275">An example of the result JSON:</span></span>
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
            "Description": "A security issue has been identified in a Microsoft software product that could affect your system. You can help protect your system by installing this update from Microsoft. For a complete listing of the issues that are included in this update, see the associated Microsoft Knowledge Base article. After you install this update, you may have to restart your system.",
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
<span data-ttu-id="42474-276">Se nenhuma atualização estiver agendada ainda, o resultado JSON estará vazio.</span><span class="sxs-lookup"><span data-stu-id="42474-276">If no update is scheduled yet, the result JSON is empty.</span></span>

<span data-ttu-id="42474-277">Faça logon no cluster para consultar os resultados do Windows Update.</span><span class="sxs-lookup"><span data-stu-id="42474-277">Log in to the cluster to query Windows Update results.</span></span> <span data-ttu-id="42474-278">Em seguida, descubra o endereço de réplica para o primário do Serviço do Coordenador e pressione a URL do navegador: http://&lt;REPLICA-IP&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1/GetWindowsUpdateResults.</span><span class="sxs-lookup"><span data-stu-id="42474-278">Then find out the replica address for the primary of the Coordinator Service, and hit the URL from the browser: http://&lt;REPLICA-IP&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1/GetWindowsUpdateResults.</span></span>

<span data-ttu-id="42474-279">O ponto de extremidade REST para o Serviço do Coordenador tem uma porta dinâmica.</span><span class="sxs-lookup"><span data-stu-id="42474-279">The REST endpoint for the Coordinator Service has a dynamic port.</span></span> <span data-ttu-id="42474-280">Para verificar a URL exata, consulte o Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="42474-280">To check the exact URL, refer to the Service Fabric Explorer.</span></span> <span data-ttu-id="42474-281">Por exemplo, os resultados estão disponíveis em `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`.</span><span class="sxs-lookup"><span data-stu-id="42474-281">For example, the results are available at `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`.</span></span>

![Imagem do ponto de extremidade REST](media/service-fabric-patch-orchestration-application/Rest_Endpoint.png)


<span data-ttu-id="42474-283">Se o proxy reverso estiver habilitado no cluster, você pode acessar a URL de fora do cluster também.</span><span class="sxs-lookup"><span data-stu-id="42474-283">If the reverse proxy is enabled on the cluster, you can access the URL from outside of the cluster as well.</span></span>
<span data-ttu-id="42474-284">O ponto de extremidade que precisa ser atingido é http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults.</span><span class="sxs-lookup"><span data-stu-id="42474-284">The endpoint that needs to be hit is http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults.</span></span>

<span data-ttu-id="42474-285">Para habilitar o proxy reverso no cluster, siga as etapas em [Proxy reverso no Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy).</span><span class="sxs-lookup"><span data-stu-id="42474-285">To enable the reverse proxy on the cluster, follow the steps in [Reverse proxy in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy).</span></span> 

> 
> [!WARNING]
> <span data-ttu-id="42474-286">Depois que o proxy reverso estiver configurado, todos os microsserviços do cluster que exponham um ponto de extremidade HTTP serão endereçáveis de fora do cluster.</span><span class="sxs-lookup"><span data-stu-id="42474-286">After the reverse proxy is configured, all micro services in the cluster that expose an HTTP endpoint are addressable from outside the cluster.</span></span>

## <a name="diagnosticshealth-events"></a><span data-ttu-id="42474-287">Eventos de diagnóstico/integridade</span><span class="sxs-lookup"><span data-stu-id="42474-287">Diagnostics/health events</span></span>

### <a name="collect-patch-orchestration-app-logs"></a><span data-ttu-id="42474-288">Colete logs do aplicativo de orquestração de patch</span><span class="sxs-lookup"><span data-stu-id="42474-288">Collect patch orchestration app logs</span></span>

<span data-ttu-id="42474-289">Os logs do aplicativo de orquestração de patch são coletados como parte dos logs do Service Fabric a partir da versão de tempo de execução `5.6.220.9494` e superior.</span><span class="sxs-lookup"><span data-stu-id="42474-289">Patch orchestration app logs are collected as part of Service Fabric logs from runtime version `5.6.220.9494` and above.</span></span>
<span data-ttu-id="42474-290">Para clusters que executam a versão de tempo de execução do Service Fabric anteriores à `5.6.220.9494`, os logs podem ser coletados usando um dos métodos a seguir.</span><span class="sxs-lookup"><span data-stu-id="42474-290">For clusters running Service Fabric runtime version less than `5.6.220.9494`, logs can be collected by using one of the following methods.</span></span>

#### <a name="locally-on-each-node"></a><span data-ttu-id="42474-291">Localmente em cada nó</span><span class="sxs-lookup"><span data-stu-id="42474-291">Locally on each node</span></span>

<span data-ttu-id="42474-292">Logs são coletados localmente em cada nó de cluster do Service Fabric se a versão de tempo de execução do Service Fabric é menor que `5.6.220.9494`.</span><span class="sxs-lookup"><span data-stu-id="42474-292">Logs are collected locally on each Service Fabric cluster node if Service Fabric runtime version is less than `5.6.220.9494`.</span></span> <span data-ttu-id="42474-293">O local para acessar os logs é \[Service Fabric\_Instalação\_Unidade\]:\\PatchOrchestrationApplication\\logs.</span><span class="sxs-lookup"><span data-stu-id="42474-293">The location to access the logs is \[Service Fabric\_Installation\_Drive\]:\\PatchOrchestrationApplication\\logs.</span></span>

<span data-ttu-id="42474-294">Por exemplo, se o Service Fabric for instalado na unidade D, o caminho será D:\\PatchOrchestrationApplication\\logs.</span><span class="sxs-lookup"><span data-stu-id="42474-294">For example, if Service Fabric is installed on drive D, the path is D:\\PatchOrchestrationApplication\\logs.</span></span>

#### <a name="central-location"></a><span data-ttu-id="42474-295">Local central</span><span class="sxs-lookup"><span data-stu-id="42474-295">Central location</span></span>

<span data-ttu-id="42474-296">Se o Diagnóstico do Microsoft Azure estiver configurado como parte das etapas de pré-requisitos, os logs para o aplicativo de orquestração de patch estarão disponíveis no Armazenamento do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="42474-296">If Azure Diagnostics is configured as part of prerequisite steps, logs for the patch orchestration app are available in Azure Storage.</span></span>

### <a name="health-reports"></a><span data-ttu-id="42474-297">Relatórios de integridade</span><span class="sxs-lookup"><span data-stu-id="42474-297">Health reports</span></span>

<span data-ttu-id="42474-298">O aplicativo de orquestração de patch também publica relatórios de integridade em relação ao Serviço do Coordinator ou ao Serviço de Agente do Nó nos seguintes casos:</span><span class="sxs-lookup"><span data-stu-id="42474-298">The patch orchestration app also publishes health reports against the Coordinator Service or the Node Agent Service in the following cases:</span></span>

#### <a name="a-windows-update-operation-failed"></a><span data-ttu-id="42474-299">Uma falha na operação do Windows Update</span><span class="sxs-lookup"><span data-stu-id="42474-299">A Windows Update operation failed</span></span>

<span data-ttu-id="42474-300">Se uma operação do Windows Update falhar em um nó, um relatório de integridade em relação ao Serviço de Agente do Nó será gerado.</span><span class="sxs-lookup"><span data-stu-id="42474-300">If a Windows Update operation fails on a node, a health report is generated against the Node Agent Service.</span></span> <span data-ttu-id="42474-301">Detalhes do relatório de integridade contêm o nome do nó problemático.</span><span class="sxs-lookup"><span data-stu-id="42474-301">Details of the health report contain the problematic node name.</span></span>

<span data-ttu-id="42474-302">Após a aplicação de pach ser concluída com sucesso no nó problemático, o relatório é apagado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="42474-302">After patching is successfully completed on the problematic node, the report is automatically cleared.</span></span>

#### <a name="the-node-agent-ntservice-is-down"></a><span data-ttu-id="42474-303">O NTService do Agente do Nó está inativo</span><span class="sxs-lookup"><span data-stu-id="42474-303">The Node Agent NTService is down</span></span>

<span data-ttu-id="42474-304">Se o NTService do Agente do Nó estiver inativo em um nó, o relatório de integridade no nível de aviso será gerado no Serviço de Agente do Nó.</span><span class="sxs-lookup"><span data-stu-id="42474-304">If the Node Agent NTService is down on a node, a warning-level health report is generated against the Node Agent Service.</span></span>

#### <a name="the-repair-manager-service-is-not-enabled"></a><span data-ttu-id="42474-305">O serviço do gerenciador de reparo não está habilitado</span><span class="sxs-lookup"><span data-stu-id="42474-305">The repair manager service is not enabled</span></span>

<span data-ttu-id="42474-306">Se o serviço do gerenciador de reparo não for encontrado no cluster, um relatório de integridade no nível de aviso será gerado para o Serviço do Coordinator.</span><span class="sxs-lookup"><span data-stu-id="42474-306">If the repair manager service is not found on the cluster, a warning-level health report is generated for the Coordinator Service.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="42474-307">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="42474-307">Frequently asked questions</span></span>

<span data-ttu-id="42474-308">P.</span><span class="sxs-lookup"><span data-stu-id="42474-308">Q.</span></span> <span data-ttu-id="42474-309">**Por que consigo ver meu cluster em um estado de erro quando o aplicativo de orquestração de patch está em execução?**</span><span class="sxs-lookup"><span data-stu-id="42474-309">**Why do I see my cluster in an error state when the patch orchestration app is running?**</span></span>

<span data-ttu-id="42474-310">R.</span><span class="sxs-lookup"><span data-stu-id="42474-310">A.</span></span> <span data-ttu-id="42474-311">Durante o processo de instalação, o aplicativo de orquestração de patch desabilita ou reinicia os nós, isso pode resultar em redução temporária da integridade do cluster.</span><span class="sxs-lookup"><span data-stu-id="42474-311">During the installation process, the patch orchestration app disables or restarts nodes, which can temporarily result in the health of the cluster going down.</span></span>

<span data-ttu-id="42474-312">Com base na política para o aplicativo, um nó pode ficar inativo durante uma operação de aplicação de patch *ou* todo um domínio de atualização pode ficar inativo ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="42474-312">Based on the policy for the application, either one node can go down during a patching operation *or* an entire upgrade domain can go down simultaneously.</span></span>

<span data-ttu-id="42474-313">Até o fim da instalação do Windows Update, os nós serão reabilitados após a reinicialização.</span><span class="sxs-lookup"><span data-stu-id="42474-313">By the end of the Windows Update installation, the nodes are reenabled post restart.</span></span>

<span data-ttu-id="42474-314">No exemplo a seguir, o cluster veio de um estado de erro temporário porque dois nós estavam inativos e a política MaxPercentageUnhealthNodes foi violada.</span><span class="sxs-lookup"><span data-stu-id="42474-314">In the following example, the cluster went to an error state temporarily because two nodes were down and the MaxPercentageUnhealthNodes policy was violated.</span></span> <span data-ttu-id="42474-315">O erro é temporário até que a operação de aplicação de patch esteja em andamento.</span><span class="sxs-lookup"><span data-stu-id="42474-315">The error is temporary until the patching operation is ongoing.</span></span>

![Imagem do cluster não íntegro](media/service-fabric-patch-orchestration-application/MaxPercentage_causing_unhealthy_cluster.png)

<span data-ttu-id="42474-317">Caso o problema persista, consulte a seção de Solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="42474-317">If the issue persists, refer to the Troubleshooting section.</span></span>

<span data-ttu-id="42474-318">P.</span><span class="sxs-lookup"><span data-stu-id="42474-318">Q.</span></span> <span data-ttu-id="42474-319">**O aplicativo de orquestração de patch está em estado de aviso**</span><span class="sxs-lookup"><span data-stu-id="42474-319">**Patch orchestration app is in warning state**</span></span>

<span data-ttu-id="42474-320">R.</span><span class="sxs-lookup"><span data-stu-id="42474-320">A.</span></span> <span data-ttu-id="42474-321">Verifique para ver se um relatório de integridade publicado em relação ao aplicativo é a causa raiz.</span><span class="sxs-lookup"><span data-stu-id="42474-321">Check to see if a health report posted against the application is the root cause.</span></span> <span data-ttu-id="42474-322">Geralmente, o aviso contém detalhes do problema.</span><span class="sxs-lookup"><span data-stu-id="42474-322">Usually, the warning contains details of the problem.</span></span> <span data-ttu-id="42474-323">Se o problema for transitório, o aplicativo deve esperar recuperar-se automaticamente desse estado.</span><span class="sxs-lookup"><span data-stu-id="42474-323">If the issue is transient, the application is expected to auto-recover from this state.</span></span>

<span data-ttu-id="42474-324">P.</span><span class="sxs-lookup"><span data-stu-id="42474-324">Q.</span></span> <span data-ttu-id="42474-325">**O que fazer se o cluster não está íntegro e preciso fazer uma atualização urgente do sistema operacional?**</span><span class="sxs-lookup"><span data-stu-id="42474-325">**What can I do if my cluster is unhealthy and I need to do an urgent operating system update?**</span></span>

<span data-ttu-id="42474-326">R.</span><span class="sxs-lookup"><span data-stu-id="42474-326">A.</span></span> <span data-ttu-id="42474-327">O aplicativo de orquestração de patch não instala atualizações enquanto o cluster não está íntegro.</span><span class="sxs-lookup"><span data-stu-id="42474-327">The patch orchestration app does not install updates while the cluster is unhealthy.</span></span> <span data-ttu-id="42474-328">Tente colocar o cluster em um estado íntegro para desbloquear o fluxo de trabalho do aplicativo de orquestração de patch.</span><span class="sxs-lookup"><span data-stu-id="42474-328">Try to bring your cluster to a healthy state to unblock the patch orchestration app workflow.</span></span>

<span data-ttu-id="42474-329">P.</span><span class="sxs-lookup"><span data-stu-id="42474-329">Q.</span></span> <span data-ttu-id="42474-330">**Por que a execução da aplicação de patch nos clusters leva tanto tempo?**</span><span class="sxs-lookup"><span data-stu-id="42474-330">**Why does patching across clusters take so long to run?**</span></span>

<span data-ttu-id="42474-331">R.</span><span class="sxs-lookup"><span data-stu-id="42474-331">A.</span></span> <span data-ttu-id="42474-332">O tempo que o aplicativo de orquestração de patch leva depende principalmente dos seguintes fatores:</span><span class="sxs-lookup"><span data-stu-id="42474-332">The time needed by the patch orchestration app is mostly dependent on the following factors:</span></span>

- <span data-ttu-id="42474-333">A política do Serviço do Coordinator.</span><span class="sxs-lookup"><span data-stu-id="42474-333">The policy of the Coordinator Service.</span></span> 
  - <span data-ttu-id="42474-334">A política padrão, `NodeWise`, resulta na aplicação de patch em apenas um nó por vez.</span><span class="sxs-lookup"><span data-stu-id="42474-334">The default policy, `NodeWise`, results in patching only one node at a time.</span></span> <span data-ttu-id="42474-335">Especialmente no caso de clusters maiores, é recomendável que você use a política `UpgradeDomainWise` para alcançar a aplicação de patch em clusters mais rápida.</span><span class="sxs-lookup"><span data-stu-id="42474-335">Especially in the case of bigger clusters, we recommend that you use the `UpgradeDomainWise` policy to achieve faster patching across clusters.</span></span>
- <span data-ttu-id="42474-336">O número de atualizações disponíveis para baixar e instalar.</span><span class="sxs-lookup"><span data-stu-id="42474-336">The number of updates available for download and installation.</span></span> 
- <span data-ttu-id="42474-337">O tempo médio necessário para baixar e instalar uma atualização, que não deve exceder alguma horas.</span><span class="sxs-lookup"><span data-stu-id="42474-337">The average time needed to download and install an update, which should not exceed a couple of hours.</span></span>
- <span data-ttu-id="42474-338">O desempenho da VM e largura da banda de rede.</span><span class="sxs-lookup"><span data-stu-id="42474-338">The performance of the VM and network bandwidth.</span></span>

<span data-ttu-id="42474-339">P.</span><span class="sxs-lookup"><span data-stu-id="42474-339">Q.</span></span> <span data-ttu-id="42474-340">**Por que vejo algumas atualizações no Windows Update resultados obtidos por meio da api REST, mas não sob o histórico do Windows Update no computador?**</span><span class="sxs-lookup"><span data-stu-id="42474-340">**Why do I see some updates in Windows Update results obtained via REST api's, but not under the Windows Update history on machine?**</span></span>

<span data-ttu-id="42474-341">R.</span><span class="sxs-lookup"><span data-stu-id="42474-341">A.</span></span> <span data-ttu-id="42474-342">Algumas atualizações de produto precisam ser verificadas no seu respectivo histórico de atualização/aplicação de patch.</span><span class="sxs-lookup"><span data-stu-id="42474-342">Some product updates need to be checked in their respective update/patch history.</span></span> <span data-ttu-id="42474-343">Por exemplo: Atualizações do Windows Defender não aparecem no histórico do Windows Update no Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="42474-343">Eg: Windows Defender updates do not show up in Windows Update history on Windows Server 2016.</span></span>

## <a name="disclaimers"></a><span data-ttu-id="42474-344">Avisos de Isenção de Responsabilidade</span><span class="sxs-lookup"><span data-stu-id="42474-344">Disclaimers</span></span>

- <span data-ttu-id="42474-345">O aplicativo de orquestração de patch aceita o Contrato de licença do usuário final do Windows Update em nome do usuário.</span><span class="sxs-lookup"><span data-stu-id="42474-345">The patch orchestration app accepts the End-User License Agreement of Windows Update on behalf of the user.</span></span> <span data-ttu-id="42474-346">A definição opcionalmente pode ser desativada na configuração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="42474-346">Optionally, the setting can be turned off in the configuration of the application.</span></span>

- <span data-ttu-id="42474-347">O aplicativo de orquestração de patch coleta a telemetria para acompanhar o uso e o desempenho.</span><span class="sxs-lookup"><span data-stu-id="42474-347">The patch orchestration app collects telemetry to track usage and performance.</span></span> <span data-ttu-id="42474-348">A telemetria do aplicativo segue a definição da configuração de telemetria do tempo de execução do Service Fabric (ativada por padrão).</span><span class="sxs-lookup"><span data-stu-id="42474-348">The application’s telemetry follows the setting of the Service Fabric runtime’s telemetry setting (which is on by default).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="42474-349">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="42474-349">Troubleshooting</span></span>

### <a name="a-node-is-not-coming-back-to-up-state"></a><span data-ttu-id="42474-350">O nó não volta para o estado ativo</span><span class="sxs-lookup"><span data-stu-id="42474-350">A node is not coming back to up state</span></span>

<span data-ttu-id="42474-351">**O nó pode estar paralisado em um estado de desabilitação porque**:</span><span class="sxs-lookup"><span data-stu-id="42474-351">**The node might be stuck in a disabling state because**:</span></span>

<span data-ttu-id="42474-352">Uma verificação de segurança está pendente.</span><span class="sxs-lookup"><span data-stu-id="42474-352">A safety check is pending.</span></span> <span data-ttu-id="42474-353">Para corrigir essa situação, verifique se há nós suficientes disponíveis em um estado íntegro.</span><span class="sxs-lookup"><span data-stu-id="42474-353">To remedy this situation, ensure that enough nodes are available in a healthy state.</span></span>

<span data-ttu-id="42474-354">**O nó pode estar paralisado em um estado desabilitado porque**:</span><span class="sxs-lookup"><span data-stu-id="42474-354">**The node might be stuck in a disabled state because**:</span></span>

- <span data-ttu-id="42474-355">O nó foi desabilitado manualmente.</span><span class="sxs-lookup"><span data-stu-id="42474-355">The node was disabled manually.</span></span>
- <span data-ttu-id="42474-356">O nó foi desabilitado devido a um trabalho de infraestrutura do Azure em andamento.</span><span class="sxs-lookup"><span data-stu-id="42474-356">The node was disabled due to an ongoing Azure infrastructure job.</span></span>
- <span data-ttu-id="42474-357">O nó foi desabilitado temporariamente pelo aplicativo de orquestração de patch para aplicar o patch ao nó.</span><span class="sxs-lookup"><span data-stu-id="42474-357">The node was disabled temporarily by the patch orchestration app to patch the node.</span></span>

<span data-ttu-id="42474-358">**O nó pode estar paralisado em um estado inativo porque**:</span><span class="sxs-lookup"><span data-stu-id="42474-358">**The node might be stuck in a down state because**:</span></span>

- <span data-ttu-id="42474-359">O nó foi colocado no estado inativo manualmente.</span><span class="sxs-lookup"><span data-stu-id="42474-359">The node was put in a down state manually.</span></span>
- <span data-ttu-id="42474-360">O nó está passando por uma reinicialização (que pode ser disparada pelo aplicativo de orquestração de patch).</span><span class="sxs-lookup"><span data-stu-id="42474-360">The node is undergoing a restart (which might be triggered by the patch orchestration app).</span></span>
- <span data-ttu-id="42474-361">O nó está inativo devido a problemas de conectividade de rede ou VM/computador com defeito.</span><span class="sxs-lookup"><span data-stu-id="42474-361">The node is down due to a faulty VM or machine or network connectivity issues.</span></span>

### <a name="updates-were-skipped-on-some-nodes"></a><span data-ttu-id="42474-362">As atualizações foram ignoradas em alguns nós</span><span class="sxs-lookup"><span data-stu-id="42474-362">Updates were skipped on some nodes</span></span>

<span data-ttu-id="42474-363">O aplicativo de orquestração de patch tenta instalar o Windows Update de acordo com a política de reagendamento.</span><span class="sxs-lookup"><span data-stu-id="42474-363">The patch orchestration app tries to install a Windows update according to the rescheduling policy.</span></span> <span data-ttu-id="42474-364">O serviço tenta recuperar o nó e ignorar a atualização de acordo com a política do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="42474-364">The service tries to recover the node and skip the update according to the application policy.</span></span>

<span data-ttu-id="42474-365">Nesse caso, será gerado um relatório de integridade no nível de aviso em relação ao Serviço de Agente do Nó.</span><span class="sxs-lookup"><span data-stu-id="42474-365">In such a case, a warning-level health report is generated against the Node Agent Service.</span></span> <span data-ttu-id="42474-366">O resultado para o Windows Update também contém o possível motivo da falha.</span><span class="sxs-lookup"><span data-stu-id="42474-366">The result for Windows Update also contains the possible reason for the failure.</span></span>

### <a name="the-health-of-the-cluster-goes-to-error-while-the-update-installs"></a><span data-ttu-id="42474-367">A integridade do cluster entrou em estado de erro enquanto a atualização é instalada</span><span class="sxs-lookup"><span data-stu-id="42474-367">The health of the cluster goes to error while the update installs</span></span>

<span data-ttu-id="42474-368">Uma atualização do Windows com falha pode reduzir a integridade de um aplicativo ou cluster em um nó ou domínio de atualização específico.</span><span class="sxs-lookup"><span data-stu-id="42474-368">A faulty Windows update can bring down the health of an application or cluster on a particular node or upgrade domain.</span></span> <span data-ttu-id="42474-369">O aplicativo de orquestração de patch interrompe qualquer operação subsequente do Windows Update até que o cluster esteja íntegro novamente.</span><span class="sxs-lookup"><span data-stu-id="42474-369">The patch orchestration app discontinues any subsequent Windows Update operation until the cluster is healthy again.</span></span>

<span data-ttu-id="42474-370">Um administrador deve intervir e determinar por que o aplicativo ou cluster se tornou não íntegro devido ao Windows Update.</span><span class="sxs-lookup"><span data-stu-id="42474-370">An administrator must intervene and determine why the application or cluster became unhealthy due to Windows Update.</span></span>

## <a name="release-notes-"></a><span data-ttu-id="42474-371">Notas de Versão:</span><span class="sxs-lookup"><span data-stu-id="42474-371">Release Notes :</span></span>

### <a name="version-110"></a><span data-ttu-id="42474-372">Version 1.1.0</span><span class="sxs-lookup"><span data-stu-id="42474-372">Version 1.1.0</span></span>
- <span data-ttu-id="42474-373">Versão pública</span><span class="sxs-lookup"><span data-stu-id="42474-373">Public release</span></span>

### <a name="version-111"></a><span data-ttu-id="42474-374">Versão 1.1.1</span><span class="sxs-lookup"><span data-stu-id="42474-374">Version 1.1.1</span></span>
- <span data-ttu-id="42474-375">Correção de bug no SetupEntryPoint de NodeAgentService que impediu a instalação de NodeAgentNTService.</span><span class="sxs-lookup"><span data-stu-id="42474-375">Fixed a bug in SetupEntryPoint of NodeAgentService that prevented installation of NodeAgentNTService.</span></span>

### <a name="version-120-latest"></a><span data-ttu-id="42474-376">Versão 1.2.0 (mais recente)</span><span class="sxs-lookup"><span data-stu-id="42474-376">Version 1.2.0 (Latest)</span></span>

- <span data-ttu-id="42474-377">Correções de bugs em torno do fluxo de trabalho de reinício do sistema.</span><span class="sxs-lookup"><span data-stu-id="42474-377">Bug fixes around system restart workflow.</span></span>
- <span data-ttu-id="42474-378">Correção de bug na criação de tarefas RM devido à qual integridade seleção durante a preparação de tarefas de reparo não estava acontecendo conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="42474-378">Bug fix in creation of RM tasks due to which health check during preparing repair tasks wasn't happening as expected.</span></span>
- <span data-ttu-id="42474-379">Alterado o modo de inicialização para o serviço windows POANodeSvc de auto para delayed-auto.</span><span class="sxs-lookup"><span data-stu-id="42474-379">Changed the startup mode for windows service POANodeSvc from auto to delayed-auto.</span></span>
