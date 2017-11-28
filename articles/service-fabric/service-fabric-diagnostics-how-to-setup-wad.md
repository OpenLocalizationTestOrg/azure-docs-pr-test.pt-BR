---
title: "Coletar logs usando o Diagnóstico do Azure | Microsoft Docs"
description: "Este artigo descreve como configurar o Diagnóstico do Azure para coletar logs de um cluster do Service Fabric em execução no Azure."
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
ms.openlocfilehash: 190a8a393f2e7d74a792db4efa81f94a18b02221
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="collect-logs-by-using-azure-diagnostics"></a><span data-ttu-id="ba63e-103">Coletar logs usando o Diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="ba63e-103">Collect logs by using Azure Diagnostics</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ba63e-104">Windows</span><span class="sxs-lookup"><span data-stu-id="ba63e-104">Windows</span></span>](service-fabric-diagnostics-how-to-setup-wad.md)
> * [<span data-ttu-id="ba63e-105">Linux</span><span class="sxs-lookup"><span data-stu-id="ba63e-105">Linux</span></span>](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

<span data-ttu-id="ba63e-106">Quando você estiver executando um cluster de Service Fabric do Azure, é uma boa ideia coletar os logs de todos os nós em um local central.</span><span class="sxs-lookup"><span data-stu-id="ba63e-106">When you're running an Azure Service Fabric cluster, it's a good idea to collect the logs from all the nodes in a central location.</span></span> <span data-ttu-id="ba63e-107">Ter os logs em um local central ajuda a analisar e solucionar problemas no cluster ou nos aplicativos e serviços em execução nesse cluster.</span><span class="sxs-lookup"><span data-stu-id="ba63e-107">Having the logs in a central location helps you analyze and troubleshoot issues in your cluster, or issues in the applications and services running in that cluster.</span></span>

<span data-ttu-id="ba63e-108">Uma forma de carregar e coletar logs é usar a extensão de Diagnóstico do Azure, que carrega os logs no Armazenamento do Azure, no Application Insights do Azure ou nos Hubs de Eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="ba63e-108">One way to upload and collect logs is to use the Azure Diagnostics extension, which uploads logs to Azure Storage, Azure Application Insights, or Azure Event Hubs.</span></span> <span data-ttu-id="ba63e-109">Os logs não são tão úteis diretamente no armazenamento ou em Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="ba63e-109">The logs are not that useful directly in storage or in Event Hubs.</span></span> <span data-ttu-id="ba63e-110">Mas você pode usar um processo externo para ler os eventos do armazenamento e colocá-los em um produto, como o [Log Analytics](../log-analytics/log-analytics-service-fabric.md) ou em outra solução de análise de log.</span><span class="sxs-lookup"><span data-stu-id="ba63e-110">But you can use an external process to read the events from storage and place them in a product such as [Log Analytics](../log-analytics/log-analytics-service-fabric.md) or another log-parsing solution.</span></span> <span data-ttu-id="ba63e-111">O [Application Insights do Azure](https://azure.microsoft.com/services/application-insights/) apresenta um serviço abrangente interno de pesquisa e análise de logs.</span><span class="sxs-lookup"><span data-stu-id="ba63e-111">[Azure Application Insights](https://azure.microsoft.com/services/application-insights/) comes with a comprehensive log search and analytics service built-in.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba63e-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ba63e-112">Prerequisites</span></span>
<span data-ttu-id="ba63e-113">Você pode usar essas ferramentas para executar algumas das operações neste documento:</span><span class="sxs-lookup"><span data-stu-id="ba63e-113">You use these tools to perform some of the operations in this document:</span></span>

* <span data-ttu-id="ba63e-114">[Diagnóstico do Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) (relacionado aos Serviços de Nuvem do Azure, mas tem boas informações e exemplos)</span><span class="sxs-lookup"><span data-stu-id="ba63e-114">[Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) (related to Azure Cloud Services but has good information and examples)</span></span>
* [<span data-ttu-id="ba63e-115">Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="ba63e-115">Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="ba63e-116">PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="ba63e-116">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="ba63e-117">Cliente do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ba63e-117">Azure Resource Manager client</span></span>](https://github.com/projectkudu/ARMClient)
* [<span data-ttu-id="ba63e-118">Modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ba63e-118">Azure Resource Manager template</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-sources-that-you-might-want-to-collect"></a><span data-ttu-id="ba63e-119">Fontes de log que você talvez queira coletar</span><span class="sxs-lookup"><span data-stu-id="ba63e-119">Log sources that you might want to collect</span></span>
* <span data-ttu-id="ba63e-120">**Logs do Service Fabric:** emitidos pela plataforma para canais de ETW (Rastreamento de Eventos para Windows) e EventSource padrão.</span><span class="sxs-lookup"><span data-stu-id="ba63e-120">**Service Fabric logs**: Emitted from the platform to standard Event Tracing for Windows (ETW) and EventSource channels.</span></span> <span data-ttu-id="ba63e-121">Os logs podem ser de vários tipos:</span><span class="sxs-lookup"><span data-stu-id="ba63e-121">Logs can be one of several types:</span></span>
  * <span data-ttu-id="ba63e-122">Eventos operacionais: logs para operações executadas pela plataforma do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ba63e-122">Operational events: Logs for operations that the Service Fabric platform performs.</span></span> <span data-ttu-id="ba63e-123">Os exemplos incluem criação de aplicativos e serviços, alterações de estado do nó e informações de atualização.</span><span class="sxs-lookup"><span data-stu-id="ba63e-123">Examples include creation of applications and services, node state changes, and upgrade information.</span></span>
  * [<span data-ttu-id="ba63e-124">Eventos do modelo de programação Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="ba63e-124">Reliable Actors programming model events</span></span>](service-fabric-reliable-actors-diagnostics.md)
  * [<span data-ttu-id="ba63e-125">Eventos do modelo de programação Reliable Services</span><span class="sxs-lookup"><span data-stu-id="ba63e-125">Reliable Services programming model events</span></span>](service-fabric-reliable-services-diagnostics.md)
* <span data-ttu-id="ba63e-126">**Eventos do aplicativo:** eventos emitidos do código de serviços e escritos usando a classe auxiliar EventSource fornecida nos modelos do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ba63e-126">**Application events**: Events emitted from your service's code and written out by using the EventSource helper class provided in the Visual Studio templates.</span></span> <span data-ttu-id="ba63e-127">Para obter mais informações sobre como gravar logs de seu aplicativo, consulte [Monitorar e diagnosticar serviços em uma configuração de desenvolvimento do computador local](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="ba63e-127">For more information on how to write logs from your application, see [Monitor and diagnose services in a local machine development setup](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>

## <a name="deploy-the-diagnostics-extension"></a><span data-ttu-id="ba63e-128">Implantar a extensão de Diagnóstico</span><span class="sxs-lookup"><span data-stu-id="ba63e-128">Deploy the Diagnostics extension</span></span>
<span data-ttu-id="ba63e-129">A primeira etapa para coletar logs será implantar a extensão Diagnóstico em cada uma das VMs no cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ba63e-129">The first step in collecting logs is to deploy the Diagnostics extension on each of the VMs in the Service Fabric cluster.</span></span> <span data-ttu-id="ba63e-130">A extensão de Diagnóstico coleta logs em cada VM e os carrega para a conta de armazenamento especificada.</span><span class="sxs-lookup"><span data-stu-id="ba63e-130">The Diagnostics extension collects logs on each VM and uploads them to the storage account that you specify.</span></span> <span data-ttu-id="ba63e-131">As etapas variam um pouco com base em seu uso do Portal do Azure ou do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ba63e-131">The steps vary a little based on whether you use the Azure portal or Azure Resource Manager.</span></span> <span data-ttu-id="ba63e-132">As etapas também variam com base em se a implantação faz parte da criação do cluster ou é para um cluster que já existe.</span><span class="sxs-lookup"><span data-stu-id="ba63e-132">The steps also vary based on whether the deployment is part of cluster creation or is for a cluster that already exists.</span></span> <span data-ttu-id="ba63e-133">Vejamos as etapas para cada cenário.</span><span class="sxs-lookup"><span data-stu-id="ba63e-133">Let's look at the steps for each scenario.</span></span>

### <a name="deploy-the-diagnostics-extension-as-part-of-cluster-creation-through-the-portal"></a><span data-ttu-id="ba63e-134">Implantar a extensão de Diagnóstico como parte da criação de cluster por meio do portal</span><span class="sxs-lookup"><span data-stu-id="ba63e-134">Deploy the Diagnostics extension as part of cluster creation through the portal</span></span>
<span data-ttu-id="ba63e-135">Para implantar a extensão de Diagnóstico nas VMs no cluster como parte da criação do cluster, você usa o painel de configurações de Diagnóstico mostrado na imagem abaixo.</span><span class="sxs-lookup"><span data-stu-id="ba63e-135">To deploy the Diagnostics extension to the VMs in the cluster as part of cluster creation, you use the Diagnostics settings panel shown in the following image.</span></span> <span data-ttu-id="ba63e-136">Para habilitar a coleta de eventos de Reliable Actors ou Reliable Services, certifique-se de que o diagnóstico esteja definido como **Ativado** (a configuração padrão).</span><span class="sxs-lookup"><span data-stu-id="ba63e-136">To enable Reliable Actors or Reliable Services event collection, ensure that Diagnostics is set to **On** (the default setting).</span></span> <span data-ttu-id="ba63e-137">Depois de criar o cluster, você não poderá alterar essas configurações por meio do portal.</span><span class="sxs-lookup"><span data-stu-id="ba63e-137">After you create the cluster, you can't change these settings by using the portal.</span></span>

![Configuração de Diagnóstico do Azure no portal para a criação do cluster](./media/service-fabric-diagnostics-how-to-setup-wad/portal-cluster-creation-diagnostics-setting.png)

<span data-ttu-id="ba63e-139">A equipe de suporte do Azure *requer* os logs de suporte para ajudar a resolver as solicitações de suporte que você criar.</span><span class="sxs-lookup"><span data-stu-id="ba63e-139">The Azure support team *requires* support logs to help resolve any support requests that you create.</span></span> <span data-ttu-id="ba63e-140">Esses logs são coletados em tempo real e são armazenados em uma das contas de armazenamento criadas no grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ba63e-140">These logs are collected in real time and are stored in one of the storage accounts created in the resource group.</span></span> <span data-ttu-id="ba63e-141">As definições de Diagnóstico configuram eventos de nível de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ba63e-141">The Diagnostics settings configure application-level events.</span></span> <span data-ttu-id="ba63e-142">Esses eventos incluem eventos de [Reliable Actors](service-fabric-reliable-actors-diagnostics.md), eventos de [Reliable Services](service-fabric-reliable-services-diagnostics.md) e alguns eventos de Service Fabric no nível de sistema a serem armazenados no Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="ba63e-142">These events include [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) events, [Reliable Services](service-fabric-reliable-services-diagnostics.md) events, and some system-level Service Fabric events to be stored in Azure Storage.</span></span>

<span data-ttu-id="ba63e-143">Os produtos como a [Elasticsearch](https://www.elastic.co/guide/index.html), ou seu próprio processo, podem obter os eventos na conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ba63e-143">Products such as [Elasticsearch](https://www.elastic.co/guide/index.html) or your own process can get the events from the storage account.</span></span> <span data-ttu-id="ba63e-144">Atualmente, não há nenhuma maneira de filtrar ou limpar os eventos que são enviados para a tabela.</span><span class="sxs-lookup"><span data-stu-id="ba63e-144">There is currently no way to filter or groom the events that are sent to the table.</span></span> <span data-ttu-id="ba63e-145">Se você não implantar um processo para remover eventos da tabela, a tabela continuará crescendo.</span><span class="sxs-lookup"><span data-stu-id="ba63e-145">If you don't implement a process to remove events from the table, the table will continue to grow.</span></span>

<span data-ttu-id="ba63e-146">Ao criar um cluster usando o portal, é altamente recomendável que você baixe o modelo **antes de clicar em OK** para criar o cluster.</span><span class="sxs-lookup"><span data-stu-id="ba63e-146">When you're creating a cluster by using the portal, we highly recommend that you download the template **before you click OK** to create the cluster.</span></span> <span data-ttu-id="ba63e-147">Para obter detalhes, confira [Setup a Service Fabric cluster by using an Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) (Configurar um cluster do Service Fabric usando um modelo do Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="ba63e-147">For details, refer to [Set up a Service Fabric cluster by using an Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="ba63e-148">Você precisará do modelo para fazer alterações posteriormente, porque não é possível fazer algumas alterações usando o portal.</span><span class="sxs-lookup"><span data-stu-id="ba63e-148">You'll need the template to make changes later, because you can't make some changes by using the portal.</span></span>

<span data-ttu-id="ba63e-149">Você pode exportar modelos por meio do portal usando as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="ba63e-149">You can export templates from the portal by using the following steps.</span></span> <span data-ttu-id="ba63e-150">No entanto, esses modelos podem ser mais difíceis de usar porque podem ter valores nulos em que estão faltando informações necessárias.</span><span class="sxs-lookup"><span data-stu-id="ba63e-150">However, these templates can be more difficult to use because they might have null values that are missing required information.</span></span>

1. <span data-ttu-id="ba63e-151">Abra seu grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ba63e-151">Open your resource group.</span></span>
2. <span data-ttu-id="ba63e-152">Selecione **Configurações** para exibir o painel Configurações.</span><span class="sxs-lookup"><span data-stu-id="ba63e-152">Select **Settings** to display the settings panel.</span></span>
3. <span data-ttu-id="ba63e-153">Selecione **Implantações** para exibir o painel de histórico de implantação.</span><span class="sxs-lookup"><span data-stu-id="ba63e-153">Select **Deployments** to display the deployment history panel.</span></span>
4. <span data-ttu-id="ba63e-154">Selecione uma implantação para exibir os detalhes da implantação.</span><span class="sxs-lookup"><span data-stu-id="ba63e-154">Select a deployment to display the details of the deployment.</span></span>
5. <span data-ttu-id="ba63e-155">Selecione **Exportar Modelo** para exibir o painel de modelo.</span><span class="sxs-lookup"><span data-stu-id="ba63e-155">Select **Export Template** to display the template panel.</span></span>
6. <span data-ttu-id="ba63e-156">Selecione **Salvar no arquivo** para exportar um arquivo .zip contendo os arquivos de modelo, parâmetro e do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ba63e-156">Select **Save to file** to export a .zip file that contains the template, parameter, and PowerShell files.</span></span>

<span data-ttu-id="ba63e-157">Depois de exportar os arquivos, é necessário fazer uma modificação.</span><span class="sxs-lookup"><span data-stu-id="ba63e-157">After you export the files, you need to make a modification.</span></span> <span data-ttu-id="ba63e-158">Edite o arquivo parameters.json e remova o elemento **adminPassword**.</span><span class="sxs-lookup"><span data-stu-id="ba63e-158">Edit the parameters.json file and remove the **adminPassword** element.</span></span> <span data-ttu-id="ba63e-159">Isso fará com que a senha seja solicitada quando o script de implantação for executado.</span><span class="sxs-lookup"><span data-stu-id="ba63e-159">This will cause a prompt for the password when the deployment script is run.</span></span> <span data-ttu-id="ba63e-160">Ao executar o script de implantação, você pode precisar corrigir os valores de parâmetro nulo.</span><span class="sxs-lookup"><span data-stu-id="ba63e-160">When you're running the deployment script, you might have to fix null parameter values.</span></span>

<span data-ttu-id="ba63e-161">Para usar o modelo baixado para atualizar uma configuração:</span><span class="sxs-lookup"><span data-stu-id="ba63e-161">To use the downloaded template to update a configuration:</span></span>

1. <span data-ttu-id="ba63e-162">Extraia o conteúdo para uma pasta no computador local.</span><span class="sxs-lookup"><span data-stu-id="ba63e-162">Extract the contents to a folder on your local computer.</span></span>
2. <span data-ttu-id="ba63e-163">Modifique o conteúdo para refletir a nova configuração.</span><span class="sxs-lookup"><span data-stu-id="ba63e-163">Modify the contents to reflect the new configuration.</span></span>
3. <span data-ttu-id="ba63e-164">Inicie o PowerShell e altere para a pasta para a qual você extraiu o conteúdo.</span><span class="sxs-lookup"><span data-stu-id="ba63e-164">Start PowerShell and change to the folder where you extracted the content.</span></span>
4. <span data-ttu-id="ba63e-165">Execute **deploy.ps1** e preencha a ID da assinatura, o nome do grupo de recursos (use o mesmo nome para atualizar a configuração) e um nome exclusivo da implantação.</span><span class="sxs-lookup"><span data-stu-id="ba63e-165">Run **deploy.ps1** and fill in the subscription ID, the resource group name (use the same name to update the configuration), and a unique deployment name.</span></span>

### <a name="deploy-the-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a><span data-ttu-id="ba63e-166">Implantar a extensão de diagnóstico como parte da criação de cluster usando o Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="ba63e-166">Deploy the Diagnostics extension as part of cluster creation by using Azure Resource Manager</span></span>
<span data-ttu-id="ba63e-167">Para criar um cluster usando o Resource Manager, você precisa adicionar a configuração de Diagnóstico JSON para o modelo do Resource Manager completo do cluster antes de criar o cluster.</span><span class="sxs-lookup"><span data-stu-id="ba63e-167">To create a cluster by using Resource Manager, you need to add the Diagnostics configuration JSON to the full cluster Resource Manager template before you create the cluster.</span></span> <span data-ttu-id="ba63e-168">Fornecemos um exemplo de modelo de Gerenciador de Recursos de cluster de cinco VMs com configuração de Diagnóstico adicionada a ele como parte dos exemplos do modelo de Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="ba63e-168">We provide a sample five-VM cluster Resource Manager template with Diagnostics configuration added to it as part of our Resource Manager template samples.</span></span> <span data-ttu-id="ba63e-169">Você pode vê-lo nesse local na Galeria de exemplos do Azure: [cluster cinco nós com exemplo de modelo do Gerenciador de Recursos de Diagnóstico](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype).</span><span class="sxs-lookup"><span data-stu-id="ba63e-169">You can see it at this location in the Azure Samples gallery: [Five-node cluster with Diagnostics Resource Manager template sample](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype).</span></span>

<span data-ttu-id="ba63e-170">Para ver a configuração do Diagnóstico no modelo do Resource Manager, abra o arquivo azuredeploy.json e pesquise **IaaSDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="ba63e-170">To see the Diagnostics setting in the Resource Manager template, open the azuredeploy.json file and search for **IaaSDiagnostics**.</span></span> <span data-ttu-id="ba63e-171">Para criar um cluster usando este modelo, selecione o botão **Implantar no Azure** disponível no link anterior.</span><span class="sxs-lookup"><span data-stu-id="ba63e-171">To create a cluster by using this template, select the **Deploy to Azure** button available at the previous link.</span></span>

<span data-ttu-id="ba63e-172">Como alternativa você pode baixar o exemplo de Gerenciador de Recursos, fazer suas alterações e criar um cluster com o modelo modificado usando o comando `New-AzureRmResourceGroupDeployment` em uma janela do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ba63e-172">Alternatively, you can download the Resource Manager sample, make changes to it, and create a cluster with the modified template by using the `New-AzureRmResourceGroupDeployment` command in an Azure PowerShell window.</span></span> <span data-ttu-id="ba63e-173">Consulte no código a seguir para ver os parâmetros que você passa para o comando.</span><span class="sxs-lookup"><span data-stu-id="ba63e-173">See the following code for the parameters that you pass in to the command.</span></span> <span data-ttu-id="ba63e-174">Para obter informações detalhadas sobre como implantar um grupo de recursos usando o PowerShell, consulte o artigo [Deploy a resource group with the Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md) (Implantar o grupo de recursos com o modelo do Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="ba63e-174">For detailed information on how to deploy a resource group by using PowerShell, see the article [Deploy a resource group with the Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

```powershell

New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -Name $deploymentName -TemplateFile $pathToARMConfigJsonFile -TemplateParameterFile $pathToParameterFile –Verbose
```

### <a name="deploy-the-diagnostics-extension-to-an-existing-cluster"></a><span data-ttu-id="ba63e-175">Implantar a extensão de diagnóstico em um cluster existente</span><span class="sxs-lookup"><span data-stu-id="ba63e-175">Deploy the Diagnostics extension to an existing cluster</span></span>
<span data-ttu-id="ba63e-176">Se você tiver um cluster existente que não tenha o Diagnóstico implantado ou se você quiser modificar uma configuração existente, você poderá adicioná-lo ou atualizá-lo.</span><span class="sxs-lookup"><span data-stu-id="ba63e-176">If you have an existing cluster that doesn't have Diagnostics deployed, or if you want to modify an existing configuration, you can add or update it.</span></span> <span data-ttu-id="ba63e-177">Modifique o modelo do Resource Manager usado para criar o cluster existente ou baixe o modelo do portal, conforme descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ba63e-177">Modify the Resource Manager template that's used to create the existing cluster or download the template from the portal as described earlier.</span></span> <span data-ttu-id="ba63e-178">Modifique o arquivo template.json executando as seguintes tarefas.</span><span class="sxs-lookup"><span data-stu-id="ba63e-178">Modify the template.json file by performing the following tasks.</span></span>

<span data-ttu-id="ba63e-179">Adicione um novo recurso de armazenamento ao modelo, adicionando à seção de recursos.</span><span class="sxs-lookup"><span data-stu-id="ba63e-179">Add a new storage resource to the template by adding to the resources section.</span></span>

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

 <span data-ttu-id="ba63e-180">Em seguida, adicione à seção de parâmetros logo após as definições da conta de armazenamento, entre `supportLogStorageAccountName` e `vmNodeType0Name`.</span><span class="sxs-lookup"><span data-stu-id="ba63e-180">Next, add to the parameters section just after the storage account definitions, between `supportLogStorageAccountName` and `vmNodeType0Name`.</span></span> <span data-ttu-id="ba63e-181">Substitua o texto do espaço reservado *nome da conta de armazenamento aqui* pelo nome da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ba63e-181">Replace the placeholder text *storage account name goes here* with the name of the storage account.</span></span>

```json
    "applicationDiagnosticsStorageAccountType": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "Replication option for the application diagnostics storage account"
      }
    },
    "applicationDiagnosticsStorageAccountName": {
      "type": "string",
      "defaultValue": "storage account name goes here",
      "metadata": {
        "description": "Name for the storage account that contains application diagnostics data from the cluster"
      }
    },
```
<span data-ttu-id="ba63e-182">Em seguida, atualize a seção `VirtualMachineProfile` do arquivo template.json adicionando o conteúdo a seguir dentro da matriz extensions.</span><span class="sxs-lookup"><span data-stu-id="ba63e-182">Then, update the `VirtualMachineProfile` section of the template.json file by adding the following code within the extensions array.</span></span> <span data-ttu-id="ba63e-183">Adicione uma vírgula no início ou no fim, dependendo de onde será inserido.</span><span class="sxs-lookup"><span data-stu-id="ba63e-183">Be sure to add a comma at the beginning or the end, depending on where it's inserted.</span></span>

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

<span data-ttu-id="ba63e-184">Após modificar o arquivo template.json conforme descrito, republique o modelo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ba63e-184">After you modify the template.json file as described, republish the Resource Manager template.</span></span> <span data-ttu-id="ba63e-185">Se o modelo tiver sido exportado, a execução do arquivo deploy.ps1 republicará o modelo.</span><span class="sxs-lookup"><span data-stu-id="ba63e-185">If the template was exported, running the deploy.ps1 file republishes the template.</span></span> <span data-ttu-id="ba63e-186">Após implantar, verifique se o status de **ProvisioningState** é **Com êxito**.</span><span class="sxs-lookup"><span data-stu-id="ba63e-186">After you deploy, ensure that **ProvisioningState** is **Succeeded**.</span></span>

## <a name="update-diagnostics-to-collect-health-and-load-events"></a><span data-ttu-id="ba63e-187">Atualizar o diagnóstico para coletar eventos de integridade e de carga</span><span class="sxs-lookup"><span data-stu-id="ba63e-187">Update diagnostics to collect health and load events</span></span>

<span data-ttu-id="ba63e-188">Começando com a versão 5.4 do Service Fabric, eventos de métrica de carga e integridade estão disponíveis para coleta.</span><span class="sxs-lookup"><span data-stu-id="ba63e-188">Starting with the 5.4 release of Service Fabric, health and load metric events are available for collection.</span></span> <span data-ttu-id="ba63e-189">Esses eventos refletir os eventos gerados pelo sistema ou seu código usando a integridade ou APIs de relatórios de carga como [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) ou [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span><span class="sxs-lookup"><span data-stu-id="ba63e-189">These events reflect events generated by the system or your code by using the health or load reporting APIs such as [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) or [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span></span> <span data-ttu-id="ba63e-190">Isso permite agregar e exibir a integridade do sistema ao longo do tempo e para alertas com base em eventos de integridade ou de carga.</span><span class="sxs-lookup"><span data-stu-id="ba63e-190">This allows for aggregating and viewing system health over time and for alerting based on health or load events.</span></span> <span data-ttu-id="ba63e-191">Para exibir esses eventos no Visualizador de Eventos de Diagnóstico do Visual Studio, adicione "Microsoft-ServiceFabric:4:0x4000000000000008" à lista de provedores de ETW.</span><span class="sxs-lookup"><span data-stu-id="ba63e-191">To view these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000008" to the list of ETW providers.</span></span>

<span data-ttu-id="ba63e-192">Para coletar os eventos, modificar o modelo do Resource Manager para incluir</span><span class="sxs-lookup"><span data-stu-id="ba63e-192">To collect the events, modify the resource manager template to include</span></span>

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

## <a name="update-diagnostics-to-collect-and-upload-logs-from-new-eventsource-channels"></a><span data-ttu-id="ba63e-193">Atualizar o Diagnóstico para coletar e carregar os logs de novos canais EventSource</span><span class="sxs-lookup"><span data-stu-id="ba63e-193">Update Diagnostics to collect and upload logs from new EventSource channels</span></span>
<span data-ttu-id="ba63e-194">Para atualizar o Diagnóstico para coletar logs de novos canais de EventSource que representam um novo aplicativo que você está prestes a implantar, basta executar as mesmas etapas da [seção acima](#deploywadarm) para configurar o Diagnóstico para um cluster existente.</span><span class="sxs-lookup"><span data-stu-id="ba63e-194">To update Diagnostics to collect logs from new EventSource channels that represent a new application that you're about to deploy, perform the same steps as in the [previous section](#deploywadarm) for setup of Diagnostics for an existing cluster.</span></span>

<span data-ttu-id="ba63e-195">Atualize a seção `EtwEventSourceProviderConfiguration` no arquivo template.json para adicionar entradas para novos canais de EventSource antes de aplicar a atualização de configuração usando o comando `New-AzureRmResourceGroupDeployment` do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ba63e-195">Update the `EtwEventSourceProviderConfiguration` section in the template.json file to add entries for the new EventSource channels before you apply the configuration update by using the `New-AzureRmResourceGroupDeployment` PowerShell command.</span></span> <span data-ttu-id="ba63e-196">O nome da origem do evento é definido como parte do seu código no arquivo Visual Studio-generated ServiceEventSource.cs.</span><span class="sxs-lookup"><span data-stu-id="ba63e-196">The name of the event source is defined as part of your code in the Visual Studio-generated ServiceEventSource.cs file.</span></span>

<span data-ttu-id="ba63e-197">Por exemplo, se a origem do evento for denominada My-Eventsource, adicione o seguinte código para colocar os eventos de My-Eventsource em uma tabela chamada MyDestinationTableName.</span><span class="sxs-lookup"><span data-stu-id="ba63e-197">For example, if your event source is named My-Eventsource, add the following code to place the events from My-Eventsource into a table named MyDestinationTableName.</span></span>

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

<span data-ttu-id="ba63e-198">Para coletar contadores de desempenho ou logs de eventos, modifique o modelo do Resource Manager usando os exemplos fornecidos em [Criar uma máquina virtual do Windows com monitoramento e diagnóstico usando um modelo do Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ba63e-198">To collect performance counters or event logs, modify the Resource Manager template by using the examples provided in [Create a Windows virtual machine with monitoring and diagnostics by using an Azure Resource Manager template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="ba63e-199">Em seguira, republique o modelo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ba63e-199">Then, republish the Resource Manager template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba63e-200">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ba63e-200">Next steps</span></span>
<span data-ttu-id="ba63e-201">Para compreender com mais detalhes quais eventos você deve analisar enquanto soluciona problemas, consulte os eventos de diagnóstico para [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) e [Reliable Services](service-fabric-reliable-services-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="ba63e-201">To understand in more detail what events you should look for while troubleshooting issues, see the diagnostic events emitted for [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) and [Reliable Services](service-fabric-reliable-services-diagnostics.md).</span></span>

## <a name="related-articles"></a><span data-ttu-id="ba63e-202">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="ba63e-202">Related articles</span></span>
* [<span data-ttu-id="ba63e-203">Aprenda a coletar contadores de desempenho ou logs usando a extensão de Diagnóstico</span><span class="sxs-lookup"><span data-stu-id="ba63e-203">Learn how to collect performance counters or logs by using the Diagnostics extension</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="ba63e-204">Solução do Service Fabric no Log Analytics</span><span class="sxs-lookup"><span data-stu-id="ba63e-204">Service Fabric solution in Log Analytics</span></span>](../log-analytics/log-analytics-service-fabric.md)

