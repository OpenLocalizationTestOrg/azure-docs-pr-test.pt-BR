---
title: "Agregação de Eventos do Azure Service Fabric com Diagnóstico do Windows Azure | Microsoft Docs"
description: "Saiba mais sobre a agregação e coleta de eventos utilizando o WAD para monitoramento e diagnóstico de clusters do Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/17/2017
ms.author: dekapur
ms.openlocfilehash: 5773361fdec4cb8ee54fa2856f6aa969d5dac4e9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="event-aggregation-and-collection-using-windows-azure-diagnostics"></a><span data-ttu-id="05a77-103">Coleta e agregação de eventos utilizando o Diagnóstico do Windows Azure</span><span class="sxs-lookup"><span data-stu-id="05a77-103">Event aggregation and collection using Windows Azure Diagnostics</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="05a77-104">Windows</span><span class="sxs-lookup"><span data-stu-id="05a77-104">Windows</span></span>](service-fabric-diagnostics-event-aggregation-wad.md)
> * [<span data-ttu-id="05a77-105">Linux</span><span class="sxs-lookup"><span data-stu-id="05a77-105">Linux</span></span>](service-fabric-diagnostics-event-aggregation-lad.md)
>
>

<span data-ttu-id="05a77-106">Quando você estiver executando um cluster de Service Fabric do Azure, é uma boa ideia coletar os logs de todos os nós em um local central.</span><span class="sxs-lookup"><span data-stu-id="05a77-106">When you're running an Azure Service Fabric cluster, it's a good idea to collect the logs from all the nodes in a central location.</span></span> <span data-ttu-id="05a77-107">Ter os logs em um local central ajuda a analisar e solucionar problemas no cluster ou nos aplicativos e serviços em execução nesse cluster.</span><span class="sxs-lookup"><span data-stu-id="05a77-107">Having the logs in a central location helps you analyze and troubleshoot issues in your cluster, or issues in the applications and services running in that cluster.</span></span>

<span data-ttu-id="05a77-108">Uma maneira de fazer upload e coletar logs é utilizar a extensão WAD (Diagnóstico do Windows Azure) que faz upload dos logs no Armazenamento do Azure e, além disso, possui a opção de enviar os logs para o Azure Application Insights ou Hubs de Evento.</span><span class="sxs-lookup"><span data-stu-id="05a77-108">One way to upload and collect logs is to use the Windows Azure Diagnostics (WAD) extension, which uploads logs to Azure Storage, and also has the option to send logs to Azure Application Insights or Event Hubs.</span></span> <span data-ttu-id="05a77-109">Também é possível utilizar um processo externo para ler os eventos do armazenamento e colocá-los em um produto da plataforma de análise, como [OMS Log Analytics](../log-analytics/log-analytics-service-fabric.md) ou outra solução de análise de logs.</span><span class="sxs-lookup"><span data-stu-id="05a77-109">You can also use an external process to read the events from storage and place them in an analysis platform product, such as [OMS Log Analytics](../log-analytics/log-analytics-service-fabric.md) or another log-parsing solution.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05a77-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="05a77-110">Prerequisites</span></span>
<span data-ttu-id="05a77-111">Essas ferramentas são usadas para executar algumas das operações neste documento:</span><span class="sxs-lookup"><span data-stu-id="05a77-111">These tools are used to perform some of the operations in this document:</span></span>

* <span data-ttu-id="05a77-112">[Diagnóstico do Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) (relacionado aos Serviços de Nuvem do Azure, mas tem boas informações e exemplos)</span><span class="sxs-lookup"><span data-stu-id="05a77-112">[Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) (related to Azure Cloud Services but has good information and examples)</span></span>
* [<span data-ttu-id="05a77-113">Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="05a77-113">Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="05a77-114">PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="05a77-114">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="05a77-115">Cliente do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="05a77-115">Azure Resource Manager client</span></span>](https://github.com/projectkudu/ARMClient)
* [<span data-ttu-id="05a77-116">Modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="05a77-116">Azure Resource Manager template</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-and-event-sources"></a><span data-ttu-id="05a77-117">Origem do evento e log</span><span class="sxs-lookup"><span data-stu-id="05a77-117">Log and event sources</span></span>

### <a name="service-fabric-platform-events"></a><span data-ttu-id="05a77-118">Eventos de plataforma do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="05a77-118">Service Fabric platform events</span></span>
<span data-ttu-id="05a77-119">Conforme discutido [neste artigo](service-fabric-diagnostics-event-generation-infra.md), o Service Fabric estabelece alguns canais de registro prontos, dos quais os seguintes canais facilmente são configurados com o WAD para enviar dados de monitoramento e diagnóstico para uma tabela de armazenamento ou outro lugar:</span><span class="sxs-lookup"><span data-stu-id="05a77-119">As discussed in [this article](service-fabric-diagnostics-event-generation-infra.md), Service Fabric sets you up with a few out-of-the-box logging channels, of which the following channels are easily configured with WAD to send monitoring and diagnostics data to a storage table or elsewhere:</span></span>
  * <span data-ttu-id="05a77-120">Eventos operacionais: operações de nível superior que a plataforma do Service Fabric executa.</span><span class="sxs-lookup"><span data-stu-id="05a77-120">Operational events: higher-level operations that the Service Fabric platform performs.</span></span> <span data-ttu-id="05a77-121">Os exemplos incluem criação de aplicativos e serviços, alterações de estado do nó e informações de atualização.</span><span class="sxs-lookup"><span data-stu-id="05a77-121">Examples include creation of applications and services, node state changes, and upgrade information.</span></span> <span data-ttu-id="05a77-122">Eles são emitidos como eventos de Rastreamento de Eventos para Windows (ETW)</span><span class="sxs-lookup"><span data-stu-id="05a77-122">These are emitted as Event Tracing for Windows (ETW) logs</span></span>
  * [<span data-ttu-id="05a77-123">Eventos do modelo de programação Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="05a77-123">Reliable Actors programming model events</span></span>](service-fabric-reliable-actors-diagnostics.md)
  * [<span data-ttu-id="05a77-124">Eventos do modelo de programação Reliable Services</span><span class="sxs-lookup"><span data-stu-id="05a77-124">Reliable Services programming model events</span></span>](service-fabric-reliable-services-diagnostics.md)

### <a name="application-events"></a><span data-ttu-id="05a77-125">Eventos de aplicativo</span><span class="sxs-lookup"><span data-stu-id="05a77-125">Application events</span></span>
 <span data-ttu-id="05a77-126">Os eventos emitidos a partir do código de serviços e aplicativos, e gravados usando a classe auxiliar EventSource fornecida nos modelos do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="05a77-126">Events emitted from your applications' and services' code and written out by using the EventSource helper class provided in the Visual Studio templates.</span></span> <span data-ttu-id="05a77-127">Para obter mais informações sobre como gravar logs EventSource do seu aplicativo, consulte [Monitorar e diagnosticar serviços em uma configuração de desenvolvimento do computador local](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="05a77-127">For more information on how to write EventSource logs from your application, see [Monitor and diagnose services in a local machine development setup](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>

## <a name="deploy-the-diagnostics-extension"></a><span data-ttu-id="05a77-128">Implantar a extensão de Diagnóstico</span><span class="sxs-lookup"><span data-stu-id="05a77-128">Deploy the Diagnostics extension</span></span>
<span data-ttu-id="05a77-129">A primeira etapa para coletar logs será implantar a extensão Diagnóstico em cada uma das VMs no cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="05a77-129">The first step in collecting logs is to deploy the Diagnostics extension on each of the VMs in the Service Fabric cluster.</span></span> <span data-ttu-id="05a77-130">A extensão de Diagnóstico coleta logs em cada VM e os carrega para a conta de armazenamento especificada.</span><span class="sxs-lookup"><span data-stu-id="05a77-130">The Diagnostics extension collects logs on each VM and uploads them to the storage account that you specify.</span></span> <span data-ttu-id="05a77-131">As etapas variam um pouco com base em seu uso do Portal do Azure ou do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="05a77-131">The steps vary a little based on whether you use the Azure portal or Azure Resource Manager.</span></span> <span data-ttu-id="05a77-132">As etapas também variam com base em se a implantação faz parte da criação do cluster ou é para um cluster que já existe.</span><span class="sxs-lookup"><span data-stu-id="05a77-132">The steps also vary based on whether the deployment is part of cluster creation or is for a cluster that already exists.</span></span> <span data-ttu-id="05a77-133">Vejamos as etapas para cada cenário.</span><span class="sxs-lookup"><span data-stu-id="05a77-133">Let's look at the steps for each scenario.</span></span>

### <a name="deploy-the-diagnostics-extension-as-part-of-cluster-creation-through-azure-portal"></a><span data-ttu-id="05a77-134">Implantar a extensão de Diagnóstico como parte da criação de cluster por meio do portal do Azure</span><span class="sxs-lookup"><span data-stu-id="05a77-134">Deploy the Diagnostics extension as part of cluster creation through Azure portal</span></span>
<span data-ttu-id="05a77-135">Para implantar a extensão de Diagnóstico nas VMs do cluster como parte da criação do cluster, você usa o painel de configurações de Diagnóstico mostrado na imagem a seguir - certifique-se de que esse Diagnóstico foi definido como **Habilitado** (a configuração padrão).</span><span class="sxs-lookup"><span data-stu-id="05a77-135">To deploy the Diagnostics extension to the VMs in the cluster as part of cluster creation, you use the Diagnostics settings panel shown in the following image - ensure that Diagnostics is set to **On** (the default setting).</span></span> <span data-ttu-id="05a77-136">Depois de criar o cluster, você não poderá alterar essas configurações por meio do portal.</span><span class="sxs-lookup"><span data-stu-id="05a77-136">After you create the cluster, you can't change these settings by using the portal.</span></span>

![Configuração de Diagnóstico do Azure no portal para a criação do cluster](media/service-fabric-diagnostics-event-aggregation-wad/azure-enable-diagnostics.png)

<span data-ttu-id="05a77-138">Ao criar um cluster usando o portal, é altamente recomendável que você baixe o modelo **antes de clicar em OK** para criar o cluster.</span><span class="sxs-lookup"><span data-stu-id="05a77-138">When you're creating a cluster by using the portal, we highly recommend that you download the template **before you click OK** to create the cluster.</span></span> <span data-ttu-id="05a77-139">Para obter detalhes, confira [Setup a Service Fabric cluster by using an Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) (Configurar um cluster do Service Fabric usando um modelo do Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="05a77-139">For details, refer to [Set up a Service Fabric cluster by using an Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="05a77-140">Você precisará do modelo para fazer alterações posteriormente, porque não é possível fazer algumas alterações usando o portal.</span><span class="sxs-lookup"><span data-stu-id="05a77-140">You'll need the template to make changes later, because you can't make some changes by using the portal.</span></span>

### <a name="deploy-the-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a><span data-ttu-id="05a77-141">Implantar a extensão de diagnóstico como parte da criação de cluster usando o Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="05a77-141">Deploy the Diagnostics extension as part of cluster creation by using Azure Resource Manager</span></span>
<span data-ttu-id="05a77-142">Para criar um cluster usando o Resource Manager, você precisa adicionar a configuração de Diagnóstico JSON para o modelo do Resource Manager completo do cluster antes de criar o cluster.</span><span class="sxs-lookup"><span data-stu-id="05a77-142">To create a cluster by using Resource Manager, you need to add the Diagnostics configuration JSON to the full cluster Resource Manager template before you create the cluster.</span></span> <span data-ttu-id="05a77-143">Fornecemos um exemplo de modelo de Gerenciador de Recursos de cluster de cinco VMs com configuração de Diagnóstico adicionada a ele como parte dos exemplos do modelo de Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="05a77-143">We provide a sample five-VM cluster Resource Manager template with Diagnostics configuration added to it as part of our Resource Manager template samples.</span></span> <span data-ttu-id="05a77-144">Você pode vê-lo nesse local na Galeria de exemplos do Azure: [cluster cinco nós com exemplo de modelo do Gerenciador de Recursos de Diagnóstico](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad).</span><span class="sxs-lookup"><span data-stu-id="05a77-144">You can see it at this location in the Azure Samples gallery: [Five-node cluster with Diagnostics Resource Manager template sample](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad).</span></span>

<span data-ttu-id="05a77-145">Para ver a configuração do Diagnóstico no modelo do Resource Manager, abra o arquivo azuredeploy.json e pesquise **IaaSDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="05a77-145">To see the Diagnostics setting in the Resource Manager template, open the azuredeploy.json file and search for **IaaSDiagnostics**.</span></span> <span data-ttu-id="05a77-146">Para criar um cluster usando este modelo, selecione o botão **Implantar no Azure** disponível no link anterior.</span><span class="sxs-lookup"><span data-stu-id="05a77-146">To create a cluster by using this template, select the **Deploy to Azure** button available at the previous link.</span></span>

<span data-ttu-id="05a77-147">Como alternativa você pode baixar o exemplo de Gerenciador de Recursos, fazer suas alterações e criar um cluster com o modelo modificado usando o comando `New-AzureRmResourceGroupDeployment` em uma janela do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="05a77-147">Alternatively, you can download the Resource Manager sample, make changes to it, and create a cluster with the modified template by using the `New-AzureRmResourceGroupDeployment` command in an Azure PowerShell window.</span></span> <span data-ttu-id="05a77-148">Consulte no código a seguir para ver os parâmetros que você passa para o comando.</span><span class="sxs-lookup"><span data-stu-id="05a77-148">See the following code for the parameters that you pass in to the command.</span></span> <span data-ttu-id="05a77-149">Para obter informações detalhadas sobre como implantar um grupo de recursos usando o PowerShell, consulte o artigo [Deploy a resource group with the Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md) (Implantar o grupo de recursos com o modelo do Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="05a77-149">For detailed information on how to deploy a resource group by using PowerShell, see the article [Deploy a resource group with the Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

### <a name="deploy-the-diagnostics-extension-to-an-existing-cluster"></a><span data-ttu-id="05a77-150">Implantar a extensão de diagnóstico em um cluster existente</span><span class="sxs-lookup"><span data-stu-id="05a77-150">Deploy the Diagnostics extension to an existing cluster</span></span>
<span data-ttu-id="05a77-151">Se você tiver um cluster existente que não tenha o Diagnóstico implantado ou se você quiser modificar uma configuração existente, você poderá adicioná-lo ou atualizá-lo.</span><span class="sxs-lookup"><span data-stu-id="05a77-151">If you have an existing cluster that doesn't have Diagnostics deployed, or if you want to modify an existing configuration, you can add or update it.</span></span> <span data-ttu-id="05a77-152">Modifique o modelo do Resource Manager usado para criar o cluster existente ou baixe o modelo do portal, conforme descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="05a77-152">Modify the Resource Manager template that's used to create the existing cluster or download the template from the portal as described earlier.</span></span> <span data-ttu-id="05a77-153">Modifique o arquivo template.json executando as seguintes tarefas.</span><span class="sxs-lookup"><span data-stu-id="05a77-153">Modify the template.json file by performing the following tasks.</span></span>

<span data-ttu-id="05a77-154">Adicione um novo recurso de armazenamento ao modelo, adicionando à seção de recursos.</span><span class="sxs-lookup"><span data-stu-id="05a77-154">Add a new storage resource to the template by adding to the resources section.</span></span>

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

 <span data-ttu-id="05a77-155">Em seguida, adicione à seção de parâmetros logo após as definições da conta de armazenamento, entre `supportLogStorageAccountName` e `vmNodeType0Name`.</span><span class="sxs-lookup"><span data-stu-id="05a77-155">Next, add to the parameters section just after the storage account definitions, between `supportLogStorageAccountName` and `vmNodeType0Name`.</span></span> <span data-ttu-id="05a77-156">Substitua o texto do espaço reservado *nome da conta de armazenamento aqui* pelo nome da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="05a77-156">Replace the placeholder text *storage account name goes here* with the name of the storage account.</span></span>

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
<span data-ttu-id="05a77-157">Em seguida, atualize a seção `VirtualMachineProfile` do arquivo template.json adicionando o conteúdo a seguir dentro da matriz extensions.</span><span class="sxs-lookup"><span data-stu-id="05a77-157">Then, update the `VirtualMachineProfile` section of the template.json file by adding the following code within the extensions array.</span></span> <span data-ttu-id="05a77-158">Adicione uma vírgula no início ou no fim, dependendo de onde será inserido.</span><span class="sxs-lookup"><span data-stu-id="05a77-158">Be sure to add a comma at the beginning or the end, depending on where it's inserted.</span></span>

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

<span data-ttu-id="05a77-159">Após modificar o arquivo template.json conforme descrito, republique o modelo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="05a77-159">After you modify the template.json file as described, republish the Resource Manager template.</span></span> <span data-ttu-id="05a77-160">Se o modelo tiver sido exportado, a execução do arquivo deploy.ps1 republicará o modelo.</span><span class="sxs-lookup"><span data-stu-id="05a77-160">If the template was exported, running the deploy.ps1 file republishes the template.</span></span> <span data-ttu-id="05a77-161">Após implantar, verifique se o status de **ProvisioningState** é **Com êxito**.</span><span class="sxs-lookup"><span data-stu-id="05a77-161">After you deploy, ensure that **ProvisioningState** is **Succeeded**.</span></span>

## <a name="collect-health-and-load-events"></a><span data-ttu-id="05a77-162">Coletar eventos de integridade e de carga</span><span class="sxs-lookup"><span data-stu-id="05a77-162">Collect health and load events</span></span>

<span data-ttu-id="05a77-163">Começando com a versão 5.4 do Service Fabric, eventos de métrica de carga e integridade estão disponíveis para coleta.</span><span class="sxs-lookup"><span data-stu-id="05a77-163">Starting with the 5.4 release of Service Fabric, health and load metric events are available for collection.</span></span> <span data-ttu-id="05a77-164">Esses eventos refletir os eventos gerados pelo sistema ou seu código usando a integridade ou APIs de relatórios de carga como [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) ou [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span><span class="sxs-lookup"><span data-stu-id="05a77-164">These events reflect events generated by the system or your code by using the health or load reporting APIs such as [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) or [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span></span> <span data-ttu-id="05a77-165">Isso permite agregar e exibir a integridade do sistema ao longo do tempo e para alertas com base em eventos de integridade ou de carga.</span><span class="sxs-lookup"><span data-stu-id="05a77-165">This allows for aggregating and viewing system health over time and for alerting based on health or load events.</span></span> <span data-ttu-id="05a77-166">Para exibir esses eventos no Visualizador de Eventos de Diagnóstico do Visual Studio, adicione "Microsoft-ServiceFabric:4:0x4000000000000008" à lista de provedores de ETW.</span><span class="sxs-lookup"><span data-stu-id="05a77-166">To view these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000008" to the list of ETW providers.</span></span>

<span data-ttu-id="05a77-167">Para coletar os eventos, modifique o modelo do Resource Manager para incluir</span><span class="sxs-lookup"><span data-stu-id="05a77-167">To collect the events, modify the Resource Manager template to include</span></span>

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

## <a name="collect-reverse-proxy-events"></a><span data-ttu-id="05a77-168">Coletar eventos de proxy reverso</span><span class="sxs-lookup"><span data-stu-id="05a77-168">Collect reverse proxy events</span></span>

<span data-ttu-id="05a77-169">A partir da versão 5.7 do Service Fabric, os eventos de [proxy reverso](service-fabric-reverseproxy.md) estão disponíveis para coleta.</span><span class="sxs-lookup"><span data-stu-id="05a77-169">Starting with the 5.7 release of Service Fabric, [reverse proxy](service-fabric-reverseproxy.md) events are available for collection.</span></span>
<span data-ttu-id="05a77-170">O proxy reverso emite eventos em dois canais, um que contém eventos de erro refletindo falhas e o outro que contém eventos detalhados sobre todas as solicitações de processamento de solicitações processados no proxy reverso.</span><span class="sxs-lookup"><span data-stu-id="05a77-170">Reverse proxy emits events into two channels, one containing error events reflecting request processing failures and the other one containing verbose events about all the requests processed at the reverse proxy.</span></span> 

1. <span data-ttu-id="05a77-171">Coletar eventos de erro: para exibir esses eventos no Visualizador de Eventos de Diagnóstico do Visual Studio, adicione "Microsoft-ServiceFabric:4:0x4000000000000010" à lista de provedores de ETW.</span><span class="sxs-lookup"><span data-stu-id="05a77-171">Collect error events: To view these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000010" to the list of ETW providers.</span></span>
<span data-ttu-id="05a77-172">Para coletar os eventos de clusters do Azure, modifique o modelo do Resource Manager para incluir</span><span class="sxs-lookup"><span data-stu-id="05a77-172">To collect the events from Azure clusters, modify the Resource Manager template to include</span></span>

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387920",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```

2. <span data-ttu-id="05a77-173">Coletar todos os eventos de processamento de solicitação: no Visualizador de Eventos de Diagnóstico no Visual Studio, atualize a entrada Microsoft-ServiceFabric na lista de provedores do ETW para "Microsoft-ServiceFabric:4:0x4000000000000020".</span><span class="sxs-lookup"><span data-stu-id="05a77-173">Collect all request processing events: In Visual Studio's Diagnostic Event Viewer, update the Microsoft-ServiceFabric entry in the ETW provider list to "Microsoft-ServiceFabric:4:0x4000000000000020".</span></span>
<span data-ttu-id="05a77-174">Para clusters do Azure Service Fabric, modifique o modelo do resource manager para incluir</span><span class="sxs-lookup"><span data-stu-id="05a77-174">For Azure Service Fabric clusters, modify the resource manager template to include</span></span>

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387936",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```
> <span data-ttu-id="05a77-175">É recomendável habilitar criteriosamente a coleta de eventos deste canal pois isso coleta todo o tráfego por meio do proxy reverso e pode consumir rapidamente a capacidade de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="05a77-175">It is recommended to judiciously enable collecting events from this channel as this collects all traffic through the reverse proxy and can quickly consume storage capacity.</span></span>

<span data-ttu-id="05a77-176">Para os clusters de Azure Service Fabric, os eventos de todos os nós são coletados e agregados em SystemEventTable.</span><span class="sxs-lookup"><span data-stu-id="05a77-176">For Azure Service Fabric clusters, the events from all the nodes are collected and aggregated in the SystemEventTable.</span></span>
<span data-ttu-id="05a77-177">Para obter a solução de problemas dos eventos de proxy reverso, veja o [guia de diagnóstico de proxy reverso](service-fabric-reverse-proxy-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="05a77-177">For detailed troubleshooting of the reverse proxy events, refer the [reverse proxy diagnostics guide](service-fabric-reverse-proxy-diagnostics.md).</span></span>

## <a name="collect-from-new-eventsource-channels"></a><span data-ttu-id="05a77-178">Coletar a partir de novos canais EventSource</span><span class="sxs-lookup"><span data-stu-id="05a77-178">Collect from new EventSource channels</span></span>

<span data-ttu-id="05a77-179">Para atualizar o Diagnóstico para coletar logs a partir de novos canais EventSource que representam um novo aplicativo que você está prestes a implantar, execute as mesmas etapas anteriores para configurar o Diagnóstico para um cluster existente.</span><span class="sxs-lookup"><span data-stu-id="05a77-179">To update Diagnostics to collect logs from new EventSource channels that represent a new application that you're about to deploy, perform the same steps as previously described for the setup of Diagnostics for an existing cluster.</span></span>

<span data-ttu-id="05a77-180">Atualize a seção `EtwEventSourceProviderConfiguration` no arquivo template.json para adicionar entradas para novos canais de EventSource antes de aplicar a atualização de configuração usando o comando `New-AzureRmResourceGroupDeployment` do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="05a77-180">Update the `EtwEventSourceProviderConfiguration` section in the template.json file to add entries for the new EventSource channels before you apply the configuration update by using the `New-AzureRmResourceGroupDeployment` PowerShell command.</span></span> <span data-ttu-id="05a77-181">O nome da origem do evento é definido como parte do seu código no arquivo Visual Studio-generated ServiceEventSource.cs.</span><span class="sxs-lookup"><span data-stu-id="05a77-181">The name of the event source is defined as part of your code in the Visual Studio-generated ServiceEventSource.cs file.</span></span>

<span data-ttu-id="05a77-182">Por exemplo, se a origem do evento for denominada My-Eventsource, adicione o seguinte código para colocar os eventos de My-Eventsource em uma tabela chamada MyDestinationTableName.</span><span class="sxs-lookup"><span data-stu-id="05a77-182">For example, if your event source is named My-Eventsource, add the following code to place the events from My-Eventsource into a table named MyDestinationTableName.</span></span>

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

<span data-ttu-id="05a77-183">Para coletar contadores de desempenho ou logs de eventos, modifique o modelo do Resource Manager usando os exemplos fornecidos em [Criar uma máquina virtual do Windows com monitoramento e diagnóstico usando um modelo do Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="05a77-183">To collect performance counters or event logs, modify the Resource Manager template by using the examples provided in [Create a Windows virtual machine with monitoring and diagnostics by using an Azure Resource Manager template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="05a77-184">Em seguira, republique o modelo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="05a77-184">Then, republish the Resource Manager template.</span></span>

## <a name="collect-performance-counters"></a><span data-ttu-id="05a77-185">Coletar contadores de desempenho</span><span class="sxs-lookup"><span data-stu-id="05a77-185">Collect Performance Counters</span></span>

<span data-ttu-id="05a77-186">Para coletar métricas de desempenho do seu cluster, adicione os contadores de desempenho para o "WadCfg > DiagnosticMonitorConfiguration" no modelo do Resource Manager para o cluster.</span><span class="sxs-lookup"><span data-stu-id="05a77-186">To collect performance metrics from your cluster, add the performance counters to your "WadCfg > DiagnosticMonitorConfiguration" in the Resource Manager template for your cluster.</span></span> <span data-ttu-id="05a77-187">Consulte [Contadores de desempenho do Service Fabric](service-fabric-diagnostics-event-generation-perf.md) para contadores de desempenho que recomendamos para coleta.</span><span class="sxs-lookup"><span data-stu-id="05a77-187">See [Service Fabric Performance Counters](service-fabric-diagnostics-event-generation-perf.md) for performance counters that we recommend collecting.</span></span>

<span data-ttu-id="05a77-188">Por exemplo, aqui vamos definir um contador de desempenho, amostras a cada 15 segundos (isso pode ser alterado e segue o formato de "PT\<time>\<unit>", por exemplo, o PT3M seria a amostra em intervalos de três minutos) e transferências para a tabela de armazenamento apropriada a cada um minuto.</span><span class="sxs-lookup"><span data-stu-id="05a77-188">For example, here we set one performance counter, sampled every 15 seconds (this can be changed and follows the format of "PT\<time>\<unit>", for example, PT3M would sample at three minute intervals), and transferred to the appropriate storage table every one minute.</span></span>

  ```json
  "PerformanceCounters": {
      "scheduledTransferPeriod": "PT1M",
      "PerformanceCounterConfiguration": [
          {
              "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
              "sampleRate": "PT15S",
              "unit": "Percent",
              "annotation": [
              ],
              "sinks": ""
          }
      ]
  }
  ```
  
<span data-ttu-id="05a77-189">Se você estiver usando um coletor do Application Insights, conforme descrito na seção abaixo e deseja que essas métricas sejam exibidas no Application Insights, certifique-se de adicionar o nome do coletor na seção "coletores", como mostrado acima.</span><span class="sxs-lookup"><span data-stu-id="05a77-189">If you are using an Application Insights sink, as described in the section below, and want these metrics to show up in Application Insights, then make sure to add the sink name in the "sinks" section as shown above.</span></span> <span data-ttu-id="05a77-190">Além disso, considere a criação de uma tabela separada para enviar seus Contadores de desempenho, para que eles não fiquem cheios de dados provenientes de outros canais de log que você habilitou.</span><span class="sxs-lookup"><span data-stu-id="05a77-190">Additionally, consider creating a separate table to send your Performance Counters to, so they don't crowd out the data coming from the other logging channels you have enabled.</span></span>


## <a name="send-logs-to-application-insights"></a><span data-ttu-id="05a77-191">Enviar logs para o Application Insights</span><span class="sxs-lookup"><span data-stu-id="05a77-191">Send logs to Application Insights</span></span>

<span data-ttu-id="05a77-192">Enviar dados de monitoramento e diagnóstico para o Application Insights (AI) pode ser feito como parte da configuração do WAD.</span><span class="sxs-lookup"><span data-stu-id="05a77-192">Sending monitoring and diagnostics data to Application Insights (AI) can be done as part of the WAD configuration.</span></span> <span data-ttu-id="05a77-193">Se você decidir usar o AI para visualização e análise de eventos, leia [Visualização e análise de eventos com o Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) para configurar um coletor do AI como parte do "WadCfg".</span><span class="sxs-lookup"><span data-stu-id="05a77-193">If you decide to use AI for event analysis and visualization, read [Event Analysis and Visualization with Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) to set up an AI Sink as part of your "WadCfg".</span></span>

## <a name="next-steps"></a><span data-ttu-id="05a77-194">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="05a77-194">Next steps</span></span>

<span data-ttu-id="05a77-195">Depois de configurar corretamente o diagnóstico do Azure, você verá os dados nas Tabelas de armazenamento dos logs do ETW e EventSource.</span><span class="sxs-lookup"><span data-stu-id="05a77-195">Once you have correctly configured Azure diagnostics, you will see data in your Storage tables from the ETW and EventSource logs.</span></span> <span data-ttu-id="05a77-196">Se você optar por usar o OMS, Kibana ou qualquer outra plataforma de análise e visualização de dados que não foi configurada diretamente no modelo do Resource Manager , certifique-se de configurar a plataforma de sua escolha para ler os dados dessas tabelas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="05a77-196">If you choose to use OMS, Kibana, or any other data analytics and visualization platform that is not directly configured in the Resource Manager template, make sure to set up the platform of your choice to read in the data from these storage tables.</span></span> <span data-ttu-id="05a77-197">Fazer isso para OMS é relativamente simples e é explicado em [Análise de eventos e logs no OMS](service-fabric-diagnostics-event-analysis-oms.md).</span><span class="sxs-lookup"><span data-stu-id="05a77-197">Doing this for OMS is relatively trivial, and is explained in [Event and log analysis through OMS](service-fabric-diagnostics-event-analysis-oms.md).</span></span> <span data-ttu-id="05a77-198">O Application Insights é um pouco diferente nesse sentido, pois ele pode ser configurado como parte da configuração da extensão de diagnóstico, então consulte o [artigo apropriado](service-fabric-diagnostics-event-analysis-appinsights.md) se optar por usar o AI.</span><span class="sxs-lookup"><span data-stu-id="05a77-198">Application Insights is a bit of a special case in this sense, since it can be configured as part of the Diagnostics extension configuration, so refer to the [appropriate article](service-fabric-diagnostics-event-analysis-appinsights.md) if you choose to use AI.</span></span>

>[!NOTE]
><span data-ttu-id="05a77-199">Atualmente, não há nenhuma maneira de filtrar ou limpar os eventos que são enviados para a tabela.</span><span class="sxs-lookup"><span data-stu-id="05a77-199">There is currently no way to filter or groom the events that are sent to the table.</span></span> <span data-ttu-id="05a77-200">Se você não implantar um processo para remover eventos da tabela, a tabela continuará crescendo.</span><span class="sxs-lookup"><span data-stu-id="05a77-200">If you don't implement a process to remove events from the table, the table will continue to grow.</span></span> <span data-ttu-id="05a77-201">Atualmente, há um exemplo de um serviço de limpeza de dados em execução no [exemplo Watchdog](https://github.com/Azure-Samples/service-fabric-watchdog-service), e é recomendável que você grave um para você mesmo, a menos que haja uma boa razão para armazenar logs além de um período de 30 ou 90 dias.</span><span class="sxs-lookup"><span data-stu-id="05a77-201">Currently, there is an example of a data grooming service running in the [Watchdog sample](https://github.com/Azure-Samples/service-fabric-watchdog-service), and it is recommended that you write one for yourself as well, unless there is a good reason for you to store logs beyond a 30 or 90 day timeframe.</span></span>

* [<span data-ttu-id="05a77-202">Aprenda a coletar contadores de desempenho ou logs usando a extensão de Diagnóstico</span><span class="sxs-lookup"><span data-stu-id="05a77-202">Learn how to collect performance counters or logs by using the Diagnostics extension</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="05a77-203">Visualização e Análise de Eventos com o Application Insights</span><span class="sxs-lookup"><span data-stu-id="05a77-203">Event Analysis and Visualization with Application Insights</span></span>](service-fabric-diagnostics-event-analysis-appinsights.md)
* [<span data-ttu-id="05a77-204">Visualização e Análise de Eventos com o OMS</span><span class="sxs-lookup"><span data-stu-id="05a77-204">Event Analysis and Visualization with OMS</span></span>](service-fabric-diagnostics-event-analysis-oms.md)