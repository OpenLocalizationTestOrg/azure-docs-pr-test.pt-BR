---
title: "aaaCollect logs usando o diagnóstico do Azure | Microsoft Docs"
description: "Este artigo descreve como tooset o diagnóstico do Azure toocollect logs de um cluster de malha do serviço em execução no Azure."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 9f7e1fa5-6543-4efd-b53f-39510f18df56
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: afbcfbe972b1847ef33bf0539b4398794b1bd56b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-logs-by-using-azure-diagnostics"></a><span data-ttu-id="2ab12-103">Coletar logs usando o Diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="2ab12-103">Collect logs by using Azure Diagnostics</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2ab12-104">Windows</span><span class="sxs-lookup"><span data-stu-id="2ab12-104">Windows</span></span>](service-fabric-diagnostics-how-to-setup-wad.md)
> * [<span data-ttu-id="2ab12-105">Linux</span><span class="sxs-lookup"><span data-stu-id="2ab12-105">Linux</span></span>](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

<span data-ttu-id="2ab12-106">Quando você estiver executando um cluster do Service Fabric do Azure, é logs de Olá de toocollect uma boa ideia de todos os nós de saudação em um local central.</span><span class="sxs-lookup"><span data-stu-id="2ab12-106">When you're running an Azure Service Fabric cluster, it's a good idea toocollect hello logs from all hello nodes in a central location.</span></span> <span data-ttu-id="2ab12-107">Ter Olá logs em um local central ajuda a analisar e solucionar problemas no seu cluster, ou em aplicativos de saudação e serviços em execução no cluster.</span><span class="sxs-lookup"><span data-stu-id="2ab12-107">Having hello logs in a central location helps you analyze and troubleshoot issues in your cluster, or issues in hello applications and services running in that cluster.</span></span>

<span data-ttu-id="2ab12-108">Tooupload uma forma e coletar logs é a extensão de diagnóstico do Azure Olá toouse, quais carregamentos logs tooAzure armazenamento, informações de aplicativo do Azure ou Hubs de eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="2ab12-108">One way tooupload and collect logs is toouse hello Azure Diagnostics extension, which uploads logs tooAzure Storage, Azure Application Insights, or Azure Event Hubs.</span></span> <span data-ttu-id="2ab12-109">Olá logs não são úteis diretamente no armazenamento ou em Hubs de eventos.</span><span class="sxs-lookup"><span data-stu-id="2ab12-109">hello logs are not that useful directly in storage or in Event Hubs.</span></span> <span data-ttu-id="2ab12-110">Mas você pode usar um processo externo tooread Olá de eventos do armazenamento e colocá-los em um produto como [análise de Log](../log-analytics/log-analytics-service-fabric.md) ou outra solução de análise de log.</span><span class="sxs-lookup"><span data-stu-id="2ab12-110">But you can use an external process tooread hello events from storage and place them in a product such as [Log Analytics](../log-analytics/log-analytics-service-fabric.md) or another log-parsing solution.</span></span> <span data-ttu-id="2ab12-111">O [Application Insights do Azure](https://azure.microsoft.com/services/application-insights/) apresenta um serviço abrangente interno de pesquisa e análise de logs.</span><span class="sxs-lookup"><span data-stu-id="2ab12-111">[Azure Application Insights](https://azure.microsoft.com/services/application-insights/) comes with a comprehensive log search and analytics service built-in.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ab12-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2ab12-112">Prerequisites</span></span>
<span data-ttu-id="2ab12-113">Use essas ferramentas tooperform algumas das operações de saudação neste documento:</span><span class="sxs-lookup"><span data-stu-id="2ab12-113">You use these tools tooperform some of hello operations in this document:</span></span>

* <span data-ttu-id="2ab12-114">[Diagnóstico do Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) (relacionado tooAzure serviços de nuvem, mas tem boas informações e exemplos)</span><span class="sxs-lookup"><span data-stu-id="2ab12-114">[Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) (related tooAzure Cloud Services but has good information and examples)</span></span>
* [<span data-ttu-id="2ab12-115">Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="2ab12-115">Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="2ab12-116">PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="2ab12-116">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="2ab12-117">Cliente do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2ab12-117">Azure Resource Manager client</span></span>](https://github.com/projectkudu/ARMClient)
* [<span data-ttu-id="2ab12-118">Modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2ab12-118">Azure Resource Manager template</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-sources-that-you-might-want-toocollect"></a><span data-ttu-id="2ab12-119">Fontes de log que convém toocollect</span><span class="sxs-lookup"><span data-stu-id="2ab12-119">Log sources that you might want toocollect</span></span>
* <span data-ttu-id="2ab12-120">**Logs do Service Fabric**: emitido de canais de rastreamento de eventos para Windows (ETW) e EventSource de toostandard de plataforma do hello.</span><span class="sxs-lookup"><span data-stu-id="2ab12-120">**Service Fabric logs**: Emitted from hello platform toostandard Event Tracing for Windows (ETW) and EventSource channels.</span></span> <span data-ttu-id="2ab12-121">Os logs podem ser de vários tipos:</span><span class="sxs-lookup"><span data-stu-id="2ab12-121">Logs can be one of several types:</span></span>
  * <span data-ttu-id="2ab12-122">Eventos operacionais: Logs de operações que Olá executa a plataforma do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2ab12-122">Operational events: Logs for operations that hello Service Fabric platform performs.</span></span> <span data-ttu-id="2ab12-123">Os exemplos incluem criação de aplicativos e serviços, alterações de estado do nó e informações de atualização.</span><span class="sxs-lookup"><span data-stu-id="2ab12-123">Examples include creation of applications and services, node state changes, and upgrade information.</span></span>
  * [<span data-ttu-id="2ab12-124">Eventos do modelo de programação Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="2ab12-124">Reliable Actors programming model events</span></span>](service-fabric-reliable-actors-diagnostics.md)
  * [<span data-ttu-id="2ab12-125">Eventos do modelo de programação Reliable Services</span><span class="sxs-lookup"><span data-stu-id="2ab12-125">Reliable Services programming model events</span></span>](service-fabric-reliable-services-diagnostics.md)
* <span data-ttu-id="2ab12-126">**Eventos de aplicativo**: eventos emitidas a partir de código do serviço e gravadas usando Olá EventSource auxiliar classe fornecido em modelos do Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="2ab12-126">**Application events**: Events emitted from your service's code and written out by using hello EventSource helper class provided in hello Visual Studio templates.</span></span> <span data-ttu-id="2ab12-127">Para obter mais informações sobre como toowrite logs de seu aplicativo, consulte [monitorar e diagnosticar os serviços em uma instalação de desenvolvimento do computador local](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="2ab12-127">For more information on how toowrite logs from your application, see [Monitor and diagnose services in a local machine development setup](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>

## <a name="deploy-hello-diagnostics-extension"></a><span data-ttu-id="2ab12-128">Implantar a extensão de diagnóstico Olá</span><span class="sxs-lookup"><span data-stu-id="2ab12-128">Deploy hello Diagnostics extension</span></span>
<span data-ttu-id="2ab12-129">Olá primeira etapa na coleta de logs é extensão de diagnóstico Olá toodeploy em cada uma das VMs Olá no cluster do Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="2ab12-129">hello first step in collecting logs is toodeploy hello Diagnostics extension on each of hello VMs in hello Service Fabric cluster.</span></span> <span data-ttu-id="2ab12-130">Olá extensão de diagnóstico coleta logs em cada VM e os carrega toohello conta de armazenamento que você especificar.</span><span class="sxs-lookup"><span data-stu-id="2ab12-130">hello Diagnostics extension collects logs on each VM and uploads them toohello storage account that you specify.</span></span> <span data-ttu-id="2ab12-131">etapas de saudação variam um pouco com base em se você usar Olá portal do Azure ou o Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="2ab12-131">hello steps vary a little based on whether you use hello Azure portal or Azure Resource Manager.</span></span> <span data-ttu-id="2ab12-132">etapas de saudação também variam com base na implantação Olá faz parte da criação do cluster ou para um cluster que já existe.</span><span class="sxs-lookup"><span data-stu-id="2ab12-132">hello steps also vary based on whether hello deployment is part of cluster creation or is for a cluster that already exists.</span></span> <span data-ttu-id="2ab12-133">Vamos dar uma olhada em etapas Olá para cada cenário.</span><span class="sxs-lookup"><span data-stu-id="2ab12-133">Let's look at hello steps for each scenario.</span></span>

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-through-hello-portal"></a><span data-ttu-id="2ab12-134">Implantar a extensão de diagnóstico hello como parte da criação de cluster por meio do portal Olá</span><span class="sxs-lookup"><span data-stu-id="2ab12-134">Deploy hello Diagnostics extension as part of cluster creation through hello portal</span></span>
<span data-ttu-id="2ab12-135">toodeploy Olá diagnóstico extensão toohello VMs no cluster hello como parte da criação do cluster, você usar o painel de configurações de diagnóstico Olá Olá a imagem a seguir mostrada.</span><span class="sxs-lookup"><span data-stu-id="2ab12-135">toodeploy hello Diagnostics extension toohello VMs in hello cluster as part of cluster creation, you use hello Diagnostics settings panel shown in hello following image.</span></span> <span data-ttu-id="2ab12-136">tooenable Reliable Actors ou serviços confiáveis coleta de eventos, verifique se o diagnóstico está definido muito**em** (Olá a configuração padrão).</span><span class="sxs-lookup"><span data-stu-id="2ab12-136">tooenable Reliable Actors or Reliable Services event collection, ensure that Diagnostics is set too**On** (hello default setting).</span></span> <span data-ttu-id="2ab12-137">Depois de criar o cluster hello, você não pode alterar essas configurações usando o portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ab12-137">After you create hello cluster, you can't change these settings by using hello portal.</span></span>

![Configurações de diagnóstico do Azure no portal de saudação para criação de cluster](./media/service-fabric-diagnostics-how-to-setup-wad/portal-cluster-creation-diagnostics-setting.png)

<span data-ttu-id="2ab12-139">Olá a equipe de suporte do Azure *requer* suporte logs toohelp resolver as solicitações de suporte que você criar.</span><span class="sxs-lookup"><span data-stu-id="2ab12-139">hello Azure support team *requires* support logs toohelp resolve any support requests that you create.</span></span> <span data-ttu-id="2ab12-140">Esses logs são coletados em tempo real e são armazenados em uma saudação contas de armazenamento criadas no grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ab12-140">These logs are collected in real time and are stored in one of hello storage accounts created in hello resource group.</span></span> <span data-ttu-id="2ab12-141">as configurações de diagnóstico Olá configuram eventos em nível de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2ab12-141">hello Diagnostics settings configure application-level events.</span></span> <span data-ttu-id="2ab12-142">Esses eventos incluem [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) eventos, [serviços confiáveis](service-fabric-reliable-services-diagnostics.md) eventos e alguns toobe de eventos do nível de sistema do Service Fabric no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="2ab12-142">These events include [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) events, [Reliable Services](service-fabric-reliable-services-diagnostics.md) events, and some system-level Service Fabric events toobe stored in Azure Storage.</span></span>

<span data-ttu-id="2ab12-143">Produtos como [Elasticsearch](https://www.elastic.co/guide/index.html) ou seu próprio processo pode obter eventos Olá Olá da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2ab12-143">Products such as [Elasticsearch](https://www.elastic.co/guide/index.html) or your own process can get hello events from hello storage account.</span></span> <span data-ttu-id="2ab12-144">Atualmente, não há nenhuma maneira toofilter ou limpar Olá eventos enviados toohello tabela.</span><span class="sxs-lookup"><span data-stu-id="2ab12-144">There is currently no way toofilter or groom hello events that are sent toohello table.</span></span> <span data-ttu-id="2ab12-145">Se você não implementa um tooremove de processar eventos de tabela hello, tabela Olá continuará toogrow.</span><span class="sxs-lookup"><span data-stu-id="2ab12-145">If you don't implement a process tooremove events from hello table, hello table will continue toogrow.</span></span>

<span data-ttu-id="2ab12-146">Quando você estiver criando um cluster usando o portal de Olá, é altamente recomendável que você baixe o modelo de saudação **antes de clicar em Okey** toocreate cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ab12-146">When you're creating a cluster by using hello portal, we highly recommend that you download hello template **before you click OK** toocreate hello cluster.</span></span> <span data-ttu-id="2ab12-147">Para obter detalhes, consulte muito[configurar um cluster do Service Fabric usando um modelo do Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="2ab12-147">For details, refer too[Set up a Service Fabric cluster by using an Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="2ab12-148">Será necessário toomake alterações do modelo de hello mais tarde, porque você não pode fazer algumas alterações usando o portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ab12-148">You'll need hello template toomake changes later, because you can't make some changes by using hello portal.</span></span>

<span data-ttu-id="2ab12-149">Você pode exportar modelos do portal Olá Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="2ab12-149">You can export templates from hello portal by using hello following steps.</span></span> <span data-ttu-id="2ab12-150">No entanto, esses modelos podem ser mais difícil toouse porque eles podem ter valores nulos que estão faltando informações necessárias.</span><span class="sxs-lookup"><span data-stu-id="2ab12-150">However, these templates can be more difficult toouse because they might have null values that are missing required information.</span></span>

1. <span data-ttu-id="2ab12-151">Abra seu grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2ab12-151">Open your resource group.</span></span>
2. <span data-ttu-id="2ab12-152">Selecione **configurações** toodisplay painel de configurações de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ab12-152">Select **Settings** toodisplay hello settings panel.</span></span>
3. <span data-ttu-id="2ab12-153">Selecione **implantações** toodisplay painel de histórico de implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ab12-153">Select **Deployments** toodisplay hello deployment history panel.</span></span>
4. <span data-ttu-id="2ab12-154">Selecione detalhes implantação toodisplay Olá de implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ab12-154">Select a deployment toodisplay hello details of hello deployment.</span></span>
5. <span data-ttu-id="2ab12-155">Selecione **exportar modelo** toodisplay painel de modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ab12-155">Select **Export Template** toodisplay hello template panel.</span></span>
6. <span data-ttu-id="2ab12-156">Selecione **salvar toofile** tooexport um arquivo. zip que contém o modelo de hello, parâmetro e arquivos do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2ab12-156">Select **Save toofile** tooexport a .zip file that contains hello template, parameter, and PowerShell files.</span></span>

<span data-ttu-id="2ab12-157">Depois de exportar arquivos Olá, é necessário toomake uma modificação.</span><span class="sxs-lookup"><span data-stu-id="2ab12-157">After you export hello files, you need toomake a modification.</span></span> <span data-ttu-id="2ab12-158">Editar o arquivo de parameters.json hello e remover Olá **adminPassword** elemento.</span><span class="sxs-lookup"><span data-stu-id="2ab12-158">Edit hello parameters.json file and remove hello **adminPassword** element.</span></span> <span data-ttu-id="2ab12-159">Isso fará com que um prompt de senha hello quando Olá script de implantação é executado.</span><span class="sxs-lookup"><span data-stu-id="2ab12-159">This will cause a prompt for hello password when hello deployment script is run.</span></span> <span data-ttu-id="2ab12-160">Quando você estiver executando o script de implantação hello, você pode ter valores de parâmetro nulo toofix.</span><span class="sxs-lookup"><span data-stu-id="2ab12-160">When you're running hello deployment script, you might have toofix null parameter values.</span></span>

<span data-ttu-id="2ab12-161">Olá toouse baixado modelo tooupdate uma configuração:</span><span class="sxs-lookup"><span data-stu-id="2ab12-161">toouse hello downloaded template tooupdate a configuration:</span></span>

1. <span data-ttu-id="2ab12-162">Extraia a pasta de tooa Olá conteúdo no computador local.</span><span class="sxs-lookup"><span data-stu-id="2ab12-162">Extract hello contents tooa folder on your local computer.</span></span>
2. <span data-ttu-id="2ab12-163">Modificar Olá conteúdo tooreflect Olá nova configuração.</span><span class="sxs-lookup"><span data-stu-id="2ab12-163">Modify hello contents tooreflect hello new configuration.</span></span>
3. <span data-ttu-id="2ab12-164">Inicie o PowerShell e alterar pasta toohello onde você extraiu o conteúdo de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ab12-164">Start PowerShell and change toohello folder where you extracted hello content.</span></span>
4. <span data-ttu-id="2ab12-165">Executar **deploy.ps1** e preencha a ID da assinatura Olá, nome do grupo de recursos de saudação (use Olá mesma configuração do nome tooupdate Olá) e um nome de implantação exclusiva.</span><span class="sxs-lookup"><span data-stu-id="2ab12-165">Run **deploy.ps1** and fill in hello subscription ID, hello resource group name (use hello same name tooupdate hello configuration), and a unique deployment name.</span></span>

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a><span data-ttu-id="2ab12-166">Implantar a extensão de diagnóstico hello como parte da criação de cluster usando o Gerenciador de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="2ab12-166">Deploy hello Diagnostics extension as part of cluster creation by using Azure Resource Manager</span></span>
<span data-ttu-id="2ab12-167">toocreate um cluster usando o Gerenciador de recursos, é necessário tooadd Olá diagnóstico JSON toohello completo do cluster Resource Manager modelo de configuração antes de criar o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ab12-167">toocreate a cluster by using Resource Manager, you need tooadd hello Diagnostics configuration JSON toohello full cluster Resource Manager template before you create hello cluster.</span></span> <span data-ttu-id="2ab12-168">Fornecemos um modelo de Gerenciador de recursos de cluster de cinco VM de exemplo com a configuração de diagnóstico adicionada tooit como parte de nossos exemplos de modelo do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="2ab12-168">We provide a sample five-VM cluster Resource Manager template with Diagnostics configuration added tooit as part of our Resource Manager template samples.</span></span> <span data-ttu-id="2ab12-169">Você pode vê-lo nesse local na Galeria de exemplos do Azure Olá: [cluster de cinco nós com exemplo de modelo do Gerenciador de recursos de diagnóstico](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype).</span><span class="sxs-lookup"><span data-stu-id="2ab12-169">You can see it at this location in hello Azure Samples gallery: [Five-node cluster with Diagnostics Resource Manager template sample](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype).</span></span>

<span data-ttu-id="2ab12-170">configuração de diagnóstico de Olá toosee no modelo do Gerenciador de recursos de saudação, arquivo de azuredeploy.json Olá aberto e procure **IaaSDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="2ab12-170">toosee hello Diagnostics setting in hello Resource Manager template, open hello azuredeploy.json file and search for **IaaSDiagnostics**.</span></span> <span data-ttu-id="2ab12-171">toocreate um cluster usando esse modelo, selecione Olá **implantar tooAzure** disponíveis no link anterior de saudação do botão.</span><span class="sxs-lookup"><span data-stu-id="2ab12-171">toocreate a cluster by using this template, select hello **Deploy tooAzure** button available at hello previous link.</span></span>

<span data-ttu-id="2ab12-172">Como alternativa, você pode baixar o exemplo do Gerenciador de recursos de hello, fazer alterações tooit e criar um cluster com o modelo modificado hello usando Olá `New-AzureRmResourceGroupDeployment` comando em uma janela do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="2ab12-172">Alternatively, you can download hello Resource Manager sample, make changes tooit, and create a cluster with hello modified template by using hello `New-AzureRmResourceGroupDeployment` command in an Azure PowerShell window.</span></span> <span data-ttu-id="2ab12-173">Consulte Olá código para hello parâmetros que você passa no toohello comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="2ab12-173">See hello following code for hello parameters that you pass in toohello command.</span></span> <span data-ttu-id="2ab12-174">Para obter informações detalhadas sobre como toodeploy um recurso de grupo usando o PowerShell, consulte o artigo Olá [implantar um grupo de recursos com o modelo do Azure Resource Manager Olá](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="2ab12-174">For detailed information on how toodeploy a resource group by using PowerShell, see hello article [Deploy a resource group with hello Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

```powershell

New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -Name $deploymentName -TemplateFile $pathToARMConfigJsonFile -TemplateParameterFile $pathToParameterFile –Verbose
```

### <a name="deploy-hello-diagnostics-extension-tooan-existing-cluster"></a><span data-ttu-id="2ab12-175">Implantar um cluster existente do hello diagnóstico extensão tooan</span><span class="sxs-lookup"><span data-stu-id="2ab12-175">Deploy hello Diagnostics extension tooan existing cluster</span></span>
<span data-ttu-id="2ab12-176">Se você tiver um cluster existente que não tem o diagnóstico de implantado, ou se você quiser toomodify uma configuração existente, você pode adicionar ou atualizá-lo.</span><span class="sxs-lookup"><span data-stu-id="2ab12-176">If you have an existing cluster that doesn't have Diagnostics deployed, or if you want toomodify an existing configuration, you can add or update it.</span></span> <span data-ttu-id="2ab12-177">Modificar o modelo do Gerenciador de recursos de saudação que é usado toocreate Olá existente cluster ou baixar o modelo de saudação do portal Olá conforme descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2ab12-177">Modify hello Resource Manager template that's used toocreate hello existing cluster or download hello template from hello portal as described earlier.</span></span> <span data-ttu-id="2ab12-178">Modificar o arquivo de template.json de saudação executando Olá tarefas a seguir.</span><span class="sxs-lookup"><span data-stu-id="2ab12-178">Modify hello template.json file by performing hello following tasks.</span></span>

<span data-ttu-id="2ab12-179">Adicione um novo modelo de toohello de recursos de armazenamento adicionando toohello seção de recursos.</span><span class="sxs-lookup"><span data-stu-id="2ab12-179">Add a new storage resource toohello template by adding toohello resources section.</span></span>

```json
{
  "apiVersion": "2015-05-01-preview",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[parameters('applicationDiagnosticsStorageAccountName')]",
  "location": "[parameters('computeLocation')]",
  "properties": {
    "accountType": "[parameters('applicationDiagnosticsStorageAccountType')]"
  },
  "tags": {
    "resourceType": "Service Fabric",
    "clusterName": "[parameters('clusterName')]"
  }
},
```

 <span data-ttu-id="2ab12-180">Em seguida, adicione a seção parâmetros toohello depois de definições de conta de armazenamento hello, entre `supportLogStorageAccountName` e `vmNodeType0Name`.</span><span class="sxs-lookup"><span data-stu-id="2ab12-180">Next, add toohello parameters section just after hello storage account definitions, between `supportLogStorageAccountName` and `vmNodeType0Name`.</span></span> <span data-ttu-id="2ab12-181">Substitua o texto do espaço reservado Olá *o nome de conta de armazenamento aqui* com nome Olá Olá da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2ab12-181">Replace hello placeholder text *storage account name goes here* with hello name of hello storage account.</span></span>

```json
    "applicationDiagnosticsStorageAccountType": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "Replication option for hello application diagnostics storage account"
      }
    },
    "applicationDiagnosticsStorageAccountName": {
      "type": "string",
      "defaultValue": "storage account name goes here",
      "metadata": {
        "description": "Name for hello storage account that contains application diagnostics data from hello cluster"
      }
    },
```
<span data-ttu-id="2ab12-182">Em seguida, atualizar Olá `VirtualMachineProfile` seção do arquivo de template.json Olá adicionando Olá código dentro do conjunto de extensões de saudação a seguir.</span><span class="sxs-lookup"><span data-stu-id="2ab12-182">Then, update hello `VirtualMachineProfile` section of hello template.json file by adding hello following code within hello extensions array.</span></span> <span data-ttu-id="2ab12-183">Ser tooadd se uma vírgula no início de saudação ou no final de hello, dependendo de onde será inserido.</span><span class="sxs-lookup"><span data-stu-id="2ab12-183">Be sure tooadd a comma at hello beginning or hello end, depending on where it's inserted.</span></span>

```json
{
    "name": "[concat(parameters('vmNodeType0Name'),'_Microsoft.Insights.VMDiagnosticsSettings')]",
    "properties": {
        "type": "IaaSDiagnostics",
        "autoUpgradeMinorVersion": true,
        "protectedSettings": {
        "storageAccountName": "[parameters('applicationDiagnosticsStorageAccountName')]",
        "storageAccountKey": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('applicationDiagnosticsStorageAccountName')),'2015-05-01-preview').key1]",
        "storageAccountEndPoint": "https://core.windows.net/"
        },
        "publisher": "Microsoft.Azure.Diagnostics",
        "settings": {
        "WadCfg": {
            "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": "50000",
            "EtwProviders": {
                "EtwEventSourceProviderConfiguration": [
                {
                    "provider": "Microsoft-ServiceFabric-Actors",
                    "scheduledTransferKeywordFilter": "1",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableActorEventTable"
                    }
                },
                {
                    "provider": "Microsoft-ServiceFabric-Services",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableServiceEventTable"
                    }
                }
                ],
                "EtwManifestProviderConfiguration": [
                {
                    "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
                    "scheduledTransferLogLevelFilter": "Information",
                    "scheduledTransferKeywordFilter": "4611686018427387904",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricSystemEventTable"
                    }
                }
                ]
            }
            }
        },
        "StorageAccount": "[parameters('applicationDiagnosticsStorageAccountName')]"
        },
        "typeHandlerVersion": "1.5"
    }
}
```

<span data-ttu-id="2ab12-184">Depois de modificar o arquivo de template.json Olá conforme descrito, republicar o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ab12-184">After you modify hello template.json file as described, republish hello Resource Manager template.</span></span> <span data-ttu-id="2ab12-185">Se o modelo de saudação foi exportado, executando o arquivo hello deploy.ps1 republica modelo hello.</span><span class="sxs-lookup"><span data-stu-id="2ab12-185">If hello template was exported, running hello deploy.ps1 file republishes hello template.</span></span> <span data-ttu-id="2ab12-186">Após implantar, verifique se o status de **ProvisioningState** é **Com êxito**.</span><span class="sxs-lookup"><span data-stu-id="2ab12-186">After you deploy, ensure that **ProvisioningState** is **Succeeded**.</span></span>

## <a name="update-diagnostics-toocollect-health-and-load-events"></a><span data-ttu-id="2ab12-187">Atualizar diagnóstico toocollect eventos de integridade e de carga</span><span class="sxs-lookup"><span data-stu-id="2ab12-187">Update diagnostics toocollect health and load events</span></span>

<span data-ttu-id="2ab12-188">A partir da versão de hello 5.4 da malha do serviço, eventos de métrica de integridade e de carga estão disponíveis para coleção.</span><span class="sxs-lookup"><span data-stu-id="2ab12-188">Starting with hello 5.4 release of Service Fabric, health and load metric events are available for collection.</span></span> <span data-ttu-id="2ab12-189">Esses eventos refletir os eventos gerados pelo sistema hello ou seu código usando a integridade de saudação ou carregar relatórios APIs como [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) ou [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span><span class="sxs-lookup"><span data-stu-id="2ab12-189">These events reflect events generated by hello system or your code by using hello health or load reporting APIs such as [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) or [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span></span> <span data-ttu-id="2ab12-190">Isso permite agregar e exibir a integridade do sistema ao longo do tempo e para alertas com base em eventos de integridade ou de carga.</span><span class="sxs-lookup"><span data-stu-id="2ab12-190">This allows for aggregating and viewing system health over time and for alerting based on health or load events.</span></span> <span data-ttu-id="2ab12-191">tooview adicionar esses eventos no Visualizador de eventos diagnóstico do Visual Studio "Microsoft-ServiceFabric:4:0x4000000000000008" toohello lista de provedores do ETW.</span><span class="sxs-lookup"><span data-stu-id="2ab12-191">tooview these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000008" toohello list of ETW providers.</span></span>

<span data-ttu-id="2ab12-192">eventos de saudação toocollect, modificar Olá tooinclude de modelo de Gerenciador de recursos</span><span class="sxs-lookup"><span data-stu-id="2ab12-192">toocollect hello events, modify hello resource manager template tooinclude</span></span>

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387912",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```

## <a name="update-diagnostics-toocollect-and-upload-logs-from-new-eventsource-channels"></a><span data-ttu-id="2ab12-193">Atualizar toocollect de diagnóstico e carregar os logs de novos canais de EventSource</span><span class="sxs-lookup"><span data-stu-id="2ab12-193">Update Diagnostics toocollect and upload logs from new EventSource channels</span></span>
<span data-ttu-id="2ab12-194">logs de toocollect tooupdate diagnóstico de novos canais de EventSource que representam um novo aplicativo que você está prestes a toodeploy, executar Olá mesmo etapas como Olá [seção anterior](#deploywadarm) para configuração de diagnóstico para um existente cluster.</span><span class="sxs-lookup"><span data-stu-id="2ab12-194">tooupdate Diagnostics toocollect logs from new EventSource channels that represent a new application that you're about toodeploy, perform hello same steps as in hello [previous section](#deploywadarm) for setup of Diagnostics for an existing cluster.</span></span>

<span data-ttu-id="2ab12-195">Atualizar Olá `EtwEventSourceProviderConfiguration` seção nas entradas de tooadd Olá template.json arquivo hello novos EventSource canais antes de aplicar a configuração de saudação atualizar usando Olá `New-AzureRmResourceGroupDeployment` comando do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2ab12-195">Update hello `EtwEventSourceProviderConfiguration` section in hello template.json file tooadd entries for hello new EventSource channels before you apply hello configuration update by using hello `New-AzureRmResourceGroupDeployment` PowerShell command.</span></span> <span data-ttu-id="2ab12-196">nome de saudação da origem de eventos de saudação é definido como parte do seu código no arquivo do hello ServiceEventSource.cs gerado pelo Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2ab12-196">hello name of hello event source is defined as part of your code in hello Visual Studio-generated ServiceEventSource.cs file.</span></span>

<span data-ttu-id="2ab12-197">Por exemplo, se a origem do evento é denominada Meu Eventsource, adicione Olá após eventos de saudação do código tooplace do meu Eventsource em uma tabela nomeada MyDestinationTableName.</span><span class="sxs-lookup"><span data-stu-id="2ab12-197">For example, if your event source is named My-Eventsource, add hello following code tooplace hello events from My-Eventsource into a table named MyDestinationTableName.</span></span>

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

<span data-ttu-id="2ab12-198">contadores de desempenho de toocollect ou logs de eventos, modificar o modelo de Gerenciador de recursos de saudação usando exemplos Olá fornecidos [criar uma máquina virtual do Windows com o monitoramento e diagnóstico usando um modelo do Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2ab12-198">toocollect performance counters or event logs, modify hello Resource Manager template by using hello examples provided in [Create a Windows virtual machine with monitoring and diagnostics by using an Azure Resource Manager template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="2ab12-199">Em seguida, republicar o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ab12-199">Then, republish hello Resource Manager template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ab12-200">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2ab12-200">Next steps</span></span>
<span data-ttu-id="2ab12-201">toounderstand mais detalhadamente os eventos que você deve procurar na solução de problemas, consulte os eventos de diagnóstico Olá emitidos para [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) e [serviços confiáveis](service-fabric-reliable-services-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="2ab12-201">toounderstand in more detail what events you should look for while troubleshooting issues, see hello diagnostic events emitted for [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) and [Reliable Services](service-fabric-reliable-services-diagnostics.md).</span></span>

## <a name="related-articles"></a><span data-ttu-id="2ab12-202">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="2ab12-202">Related articles</span></span>
* [<span data-ttu-id="2ab12-203">Saiba como os contadores de desempenho de toocollect ou logs usando Olá extensão de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="2ab12-203">Learn how toocollect performance counters or logs by using hello Diagnostics extension</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="2ab12-204">Solução do Service Fabric no Log Analytics</span><span class="sxs-lookup"><span data-stu-id="2ab12-204">Service Fabric solution in Log Analytics</span></span>](../log-analytics/log-analytics-service-fabric.md)

