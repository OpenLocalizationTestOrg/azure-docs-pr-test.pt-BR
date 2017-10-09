---
title: "aaaAzure agregação de eventos do serviço de malha com o diagnóstico do Windows Azure | Microsoft Docs"
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
ms.openlocfilehash: 4827ce66620e61c5b4a8682db55952333113188a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-windows-azure-diagnostics"></a><span data-ttu-id="e3d01-103">Coleta e agregação de eventos utilizando o Diagnóstico do Windows Azure</span><span class="sxs-lookup"><span data-stu-id="e3d01-103">Event aggregation and collection using Windows Azure Diagnostics</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e3d01-104">Windows</span><span class="sxs-lookup"><span data-stu-id="e3d01-104">Windows</span></span>](service-fabric-diagnostics-event-aggregation-wad.md)
> * [<span data-ttu-id="e3d01-105">Linux</span><span class="sxs-lookup"><span data-stu-id="e3d01-105">Linux</span></span>](service-fabric-diagnostics-event-aggregation-lad.md)
>
>

<span data-ttu-id="e3d01-106">Quando você estiver executando um cluster do Service Fabric do Azure, é logs de Olá de toocollect uma boa ideia de todos os nós de saudação em um local central.</span><span class="sxs-lookup"><span data-stu-id="e3d01-106">When you're running an Azure Service Fabric cluster, it's a good idea toocollect hello logs from all hello nodes in a central location.</span></span> <span data-ttu-id="e3d01-107">Ter Olá logs em um local central ajuda a analisar e solucionar problemas no seu cluster, ou em aplicativos de saudação e serviços em execução no cluster.</span><span class="sxs-lookup"><span data-stu-id="e3d01-107">Having hello logs in a central location helps you analyze and troubleshoot issues in your cluster, or issues in hello applications and services running in that cluster.</span></span>

<span data-ttu-id="e3d01-108">Tooupload uma forma e coletar logs é extensão de Windows Azure WAD (Diagnóstico) de saudação toouse, que carrega logs tooAzure armazenamento e também tem Olá opção toosend logs tooAzure Application Insights ou Hubs de eventos.</span><span class="sxs-lookup"><span data-stu-id="e3d01-108">One way tooupload and collect logs is toouse hello Windows Azure Diagnostics (WAD) extension, which uploads logs tooAzure Storage, and also has hello option toosend logs tooAzure Application Insights or Event Hubs.</span></span> <span data-ttu-id="e3d01-109">Você também pode usar um processo externo tooread Olá de eventos do armazenamento e colocá-los em um produto de plataforma de análise, como [análise de logs do OMS](../log-analytics/log-analytics-service-fabric.md) ou outra solução de análise de log.</span><span class="sxs-lookup"><span data-stu-id="e3d01-109">You can also use an external process tooread hello events from storage and place them in an analysis platform product, such as [OMS Log Analytics](../log-analytics/log-analytics-service-fabric.md) or another log-parsing solution.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e3d01-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e3d01-110">Prerequisites</span></span>
<span data-ttu-id="e3d01-111">Essas ferramentas são usada tooperform algumas das operações de saudação neste documento:</span><span class="sxs-lookup"><span data-stu-id="e3d01-111">These tools are used tooperform some of hello operations in this document:</span></span>

* <span data-ttu-id="e3d01-112">[Diagnóstico do Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) (relacionado tooAzure serviços de nuvem, mas tem boas informações e exemplos)</span><span class="sxs-lookup"><span data-stu-id="e3d01-112">[Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) (related tooAzure Cloud Services but has good information and examples)</span></span>
* [<span data-ttu-id="e3d01-113">Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="e3d01-113">Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="e3d01-114">PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="e3d01-114">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="e3d01-115">Cliente do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e3d01-115">Azure Resource Manager client</span></span>](https://github.com/projectkudu/ARMClient)
* [<span data-ttu-id="e3d01-116">Modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e3d01-116">Azure Resource Manager template</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-and-event-sources"></a><span data-ttu-id="e3d01-117">Origem do evento e log</span><span class="sxs-lookup"><span data-stu-id="e3d01-117">Log and event sources</span></span>

### <a name="service-fabric-platform-events"></a><span data-ttu-id="e3d01-118">Eventos de plataforma do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e3d01-118">Service Fabric platform events</span></span>
<span data-ttu-id="e3d01-119">Conforme discutido em [neste artigo](service-fabric-diagnostics-event-generation-infra.md)Service Fabric configura você com alguns canais de registro de fora da caixa, do qual Olá canais a seguir facilmente configurados com WAD toosend monitoramento e diagnóstico tooa armazenamento tabela de dados ou em outro lugar:</span><span class="sxs-lookup"><span data-stu-id="e3d01-119">As discussed in [this article](service-fabric-diagnostics-event-generation-infra.md), Service Fabric sets you up with a few out-of-the-box logging channels, of which hello following channels are easily configured with WAD toosend monitoring and diagnostics data tooa storage table or elsewhere:</span></span>
  * <span data-ttu-id="e3d01-120">Eventos operacionais: operações de nível mais alto que Olá executa a plataforma do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e3d01-120">Operational events: higher-level operations that hello Service Fabric platform performs.</span></span> <span data-ttu-id="e3d01-121">Os exemplos incluem criação de aplicativos e serviços, alterações de estado do nó e informações de atualização.</span><span class="sxs-lookup"><span data-stu-id="e3d01-121">Examples include creation of applications and services, node state changes, and upgrade information.</span></span> <span data-ttu-id="e3d01-122">Eles são emitidos como eventos de Rastreamento de Eventos para Windows (ETW)</span><span class="sxs-lookup"><span data-stu-id="e3d01-122">These are emitted as Event Tracing for Windows (ETW) logs</span></span>
  * [<span data-ttu-id="e3d01-123">Eventos do modelo de programação Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="e3d01-123">Reliable Actors programming model events</span></span>](service-fabric-reliable-actors-diagnostics.md)
  * [<span data-ttu-id="e3d01-124">Eventos do modelo de programação Reliable Services</span><span class="sxs-lookup"><span data-stu-id="e3d01-124">Reliable Services programming model events</span></span>](service-fabric-reliable-services-diagnostics.md)

### <a name="application-events"></a><span data-ttu-id="e3d01-125">Eventos de aplicativo</span><span class="sxs-lookup"><span data-stu-id="e3d01-125">Application events</span></span>
 <span data-ttu-id="e3d01-126">Eventos emitidas a partir de seus aplicativos e serviços de código e gravadas usando a classe de auxiliar de EventSource Olá fornecidas Olá modelos do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e3d01-126">Events emitted from your applications' and services' code and written out by using hello EventSource helper class provided in hello Visual Studio templates.</span></span> <span data-ttu-id="e3d01-127">Para obter mais informações sobre como toowrite EventSource logs de seu aplicativo, consulte [monitorar e diagnosticar os serviços em uma instalação de desenvolvimento do computador local](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="e3d01-127">For more information on how toowrite EventSource logs from your application, see [Monitor and diagnose services in a local machine development setup](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>

## <a name="deploy-hello-diagnostics-extension"></a><span data-ttu-id="e3d01-128">Implantar a extensão de diagnóstico Olá</span><span class="sxs-lookup"><span data-stu-id="e3d01-128">Deploy hello Diagnostics extension</span></span>
<span data-ttu-id="e3d01-129">Olá primeira etapa na coleta de logs é extensão de diagnóstico Olá toodeploy em cada uma das VMs Olá no cluster do Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="e3d01-129">hello first step in collecting logs is toodeploy hello Diagnostics extension on each of hello VMs in hello Service Fabric cluster.</span></span> <span data-ttu-id="e3d01-130">Olá extensão de diagnóstico coleta logs em cada VM e os carrega toohello conta de armazenamento que você especificar.</span><span class="sxs-lookup"><span data-stu-id="e3d01-130">hello Diagnostics extension collects logs on each VM and uploads them toohello storage account that you specify.</span></span> <span data-ttu-id="e3d01-131">etapas de saudação variam um pouco com base em se você usar Olá portal do Azure ou o Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3d01-131">hello steps vary a little based on whether you use hello Azure portal or Azure Resource Manager.</span></span> <span data-ttu-id="e3d01-132">etapas de saudação também variam com base na implantação Olá faz parte da criação do cluster ou para um cluster que já existe.</span><span class="sxs-lookup"><span data-stu-id="e3d01-132">hello steps also vary based on whether hello deployment is part of cluster creation or is for a cluster that already exists.</span></span> <span data-ttu-id="e3d01-133">Vamos dar uma olhada em etapas Olá para cada cenário.</span><span class="sxs-lookup"><span data-stu-id="e3d01-133">Let's look at hello steps for each scenario.</span></span>

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-through-azure-portal"></a><span data-ttu-id="e3d01-134">Implantar a extensão de diagnóstico hello como parte da criação de cluster por meio do portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e3d01-134">Deploy hello Diagnostics extension as part of cluster creation through Azure portal</span></span>
<span data-ttu-id="e3d01-135">toodeploy Olá diagnóstico extensão toohello VMs no cluster hello como parte da criação do cluster, que você usar o painel de configurações de diagnóstico Olá mostrado na seguinte Olá imagem - Verifique se o diagnóstico está definido muito**em** (Olá a configuração padrão) .</span><span class="sxs-lookup"><span data-stu-id="e3d01-135">toodeploy hello Diagnostics extension toohello VMs in hello cluster as part of cluster creation, you use hello Diagnostics settings panel shown in hello following image - ensure that Diagnostics is set too**On** (hello default setting).</span></span> <span data-ttu-id="e3d01-136">Depois de criar o cluster hello, você não pode alterar essas configurações usando o portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3d01-136">After you create hello cluster, you can't change these settings by using hello portal.</span></span>

![Configurações de diagnóstico do Azure no portal de saudação para criação de cluster](media/service-fabric-diagnostics-event-aggregation-wad/azure-enable-diagnostics.png)

<span data-ttu-id="e3d01-138">Quando você estiver criando um cluster usando o portal de Olá, é altamente recomendável que você baixe o modelo de saudação **antes de clicar em Okey** toocreate cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3d01-138">When you're creating a cluster by using hello portal, we highly recommend that you download hello template **before you click OK** toocreate hello cluster.</span></span> <span data-ttu-id="e3d01-139">Para obter detalhes, consulte muito[configurar um cluster do Service Fabric usando um modelo do Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="e3d01-139">For details, refer too[Set up a Service Fabric cluster by using an Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="e3d01-140">Será necessário toomake alterações do modelo de hello mais tarde, porque você não pode fazer algumas alterações usando o portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3d01-140">You'll need hello template toomake changes later, because you can't make some changes by using hello portal.</span></span>

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a><span data-ttu-id="e3d01-141">Implantar a extensão de diagnóstico hello como parte da criação de cluster usando o Gerenciador de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="e3d01-141">Deploy hello Diagnostics extension as part of cluster creation by using Azure Resource Manager</span></span>
<span data-ttu-id="e3d01-142">toocreate um cluster usando o Gerenciador de recursos, é necessário tooadd Olá diagnóstico JSON toohello completo do cluster Resource Manager modelo de configuração antes de criar o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3d01-142">toocreate a cluster by using Resource Manager, you need tooadd hello Diagnostics configuration JSON toohello full cluster Resource Manager template before you create hello cluster.</span></span> <span data-ttu-id="e3d01-143">Fornecemos um modelo de Gerenciador de recursos de cluster de cinco VM de exemplo com a configuração de diagnóstico adicionada tooit como parte de nossos exemplos de modelo do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="e3d01-143">We provide a sample five-VM cluster Resource Manager template with Diagnostics configuration added tooit as part of our Resource Manager template samples.</span></span> <span data-ttu-id="e3d01-144">Você pode vê-lo nesse local na Galeria de exemplos do Azure Olá: [cluster de cinco nós com exemplo de modelo do Gerenciador de recursos de diagnóstico](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad).</span><span class="sxs-lookup"><span data-stu-id="e3d01-144">You can see it at this location in hello Azure Samples gallery: [Five-node cluster with Diagnostics Resource Manager template sample](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad).</span></span>

<span data-ttu-id="e3d01-145">configuração de diagnóstico de Olá toosee no modelo do Gerenciador de recursos de saudação, arquivo de azuredeploy.json Olá aberto e procure **IaaSDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="e3d01-145">toosee hello Diagnostics setting in hello Resource Manager template, open hello azuredeploy.json file and search for **IaaSDiagnostics**.</span></span> <span data-ttu-id="e3d01-146">toocreate um cluster usando esse modelo, selecione Olá **implantar tooAzure** disponíveis no link anterior de saudação do botão.</span><span class="sxs-lookup"><span data-stu-id="e3d01-146">toocreate a cluster by using this template, select hello **Deploy tooAzure** button available at hello previous link.</span></span>

<span data-ttu-id="e3d01-147">Como alternativa, você pode baixar o exemplo do Gerenciador de recursos de hello, fazer alterações tooit e criar um cluster com o modelo modificado hello usando Olá `New-AzureRmResourceGroupDeployment` comando em uma janela do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3d01-147">Alternatively, you can download hello Resource Manager sample, make changes tooit, and create a cluster with hello modified template by using hello `New-AzureRmResourceGroupDeployment` command in an Azure PowerShell window.</span></span> <span data-ttu-id="e3d01-148">Consulte Olá código para hello parâmetros que você passa no toohello comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="e3d01-148">See hello following code for hello parameters that you pass in toohello command.</span></span> <span data-ttu-id="e3d01-149">Para obter informações detalhadas sobre como toodeploy um recurso de grupo usando o PowerShell, consulte o artigo Olá [implantar um grupo de recursos com o modelo do Azure Resource Manager Olá](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="e3d01-149">For detailed information on how toodeploy a resource group by using PowerShell, see hello article [Deploy a resource group with hello Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

### <a name="deploy-hello-diagnostics-extension-tooan-existing-cluster"></a><span data-ttu-id="e3d01-150">Implantar um cluster existente do hello diagnóstico extensão tooan</span><span class="sxs-lookup"><span data-stu-id="e3d01-150">Deploy hello Diagnostics extension tooan existing cluster</span></span>
<span data-ttu-id="e3d01-151">Se você tiver um cluster existente que não tem o diagnóstico de implantado, ou se você quiser toomodify uma configuração existente, você pode adicionar ou atualizá-lo.</span><span class="sxs-lookup"><span data-stu-id="e3d01-151">If you have an existing cluster that doesn't have Diagnostics deployed, or if you want toomodify an existing configuration, you can add or update it.</span></span> <span data-ttu-id="e3d01-152">Modificar o modelo do Gerenciador de recursos de saudação que é usado toocreate Olá existente cluster ou baixar o modelo de saudação do portal Olá conforme descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e3d01-152">Modify hello Resource Manager template that's used toocreate hello existing cluster or download hello template from hello portal as described earlier.</span></span> <span data-ttu-id="e3d01-153">Modificar o arquivo de template.json de saudação executando Olá tarefas a seguir.</span><span class="sxs-lookup"><span data-stu-id="e3d01-153">Modify hello template.json file by performing hello following tasks.</span></span>

<span data-ttu-id="e3d01-154">Adicione um novo modelo de toohello de recursos de armazenamento adicionando toohello seção de recursos.</span><span class="sxs-lookup"><span data-stu-id="e3d01-154">Add a new storage resource toohello template by adding toohello resources section.</span></span>

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

 <span data-ttu-id="e3d01-155">Em seguida, adicione a seção parâmetros toohello depois de definições de conta de armazenamento hello, entre `supportLogStorageAccountName` e `vmNodeType0Name`.</span><span class="sxs-lookup"><span data-stu-id="e3d01-155">Next, add toohello parameters section just after hello storage account definitions, between `supportLogStorageAccountName` and `vmNodeType0Name`.</span></span> <span data-ttu-id="e3d01-156">Substitua o texto do espaço reservado Olá *o nome de conta de armazenamento aqui* com nome Olá Olá da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e3d01-156">Replace hello placeholder text *storage account name goes here* with hello name of hello storage account.</span></span>

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
<span data-ttu-id="e3d01-157">Em seguida, atualizar Olá `VirtualMachineProfile` seção do arquivo de template.json Olá adicionando Olá código dentro do conjunto de extensões de saudação a seguir.</span><span class="sxs-lookup"><span data-stu-id="e3d01-157">Then, update hello `VirtualMachineProfile` section of hello template.json file by adding hello following code within hello extensions array.</span></span> <span data-ttu-id="e3d01-158">Ser tooadd se uma vírgula no início de saudação ou no final de hello, dependendo de onde será inserido.</span><span class="sxs-lookup"><span data-stu-id="e3d01-158">Be sure tooadd a comma at hello beginning or hello end, depending on where it's inserted.</span></span>

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

<span data-ttu-id="e3d01-159">Depois de modificar o arquivo de template.json Olá conforme descrito, republicar o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3d01-159">After you modify hello template.json file as described, republish hello Resource Manager template.</span></span> <span data-ttu-id="e3d01-160">Se o modelo de saudação foi exportado, executando o arquivo hello deploy.ps1 republica modelo hello.</span><span class="sxs-lookup"><span data-stu-id="e3d01-160">If hello template was exported, running hello deploy.ps1 file republishes hello template.</span></span> <span data-ttu-id="e3d01-161">Após implantar, verifique se o status de **ProvisioningState** é **Com êxito**.</span><span class="sxs-lookup"><span data-stu-id="e3d01-161">After you deploy, ensure that **ProvisioningState** is **Succeeded**.</span></span>

## <a name="collect-health-and-load-events"></a><span data-ttu-id="e3d01-162">Coletar eventos de integridade e de carga</span><span class="sxs-lookup"><span data-stu-id="e3d01-162">Collect health and load events</span></span>

<span data-ttu-id="e3d01-163">A partir da versão de hello 5.4 da malha do serviço, eventos de métrica de integridade e de carga estão disponíveis para coleção.</span><span class="sxs-lookup"><span data-stu-id="e3d01-163">Starting with hello 5.4 release of Service Fabric, health and load metric events are available for collection.</span></span> <span data-ttu-id="e3d01-164">Esses eventos refletir os eventos gerados pelo sistema hello ou seu código usando a integridade de saudação ou carregar relatórios APIs como [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) ou [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span><span class="sxs-lookup"><span data-stu-id="e3d01-164">These events reflect events generated by hello system or your code by using hello health or load reporting APIs such as [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) or [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span></span> <span data-ttu-id="e3d01-165">Isso permite agregar e exibir a integridade do sistema ao longo do tempo e para alertas com base em eventos de integridade ou de carga.</span><span class="sxs-lookup"><span data-stu-id="e3d01-165">This allows for aggregating and viewing system health over time and for alerting based on health or load events.</span></span> <span data-ttu-id="e3d01-166">tooview adicionar esses eventos no Visualizador de eventos diagnóstico do Visual Studio "Microsoft-ServiceFabric:4:0x4000000000000008" toohello lista de provedores do ETW.</span><span class="sxs-lookup"><span data-stu-id="e3d01-166">tooview these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000008" toohello list of ETW providers.</span></span>

<span data-ttu-id="e3d01-167">eventos de saudação toocollect, modificar tooinclude de modelo do Gerenciador de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="e3d01-167">toocollect hello events, modify hello Resource Manager template tooinclude</span></span>

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

## <a name="collect-reverse-proxy-events"></a><span data-ttu-id="e3d01-168">Coletar eventos de proxy reverso</span><span class="sxs-lookup"><span data-stu-id="e3d01-168">Collect reverse proxy events</span></span>

<span data-ttu-id="e3d01-169">Versão de hello 5.7 do Service Fabric [proxy reverso](service-fabric-reverseproxy.md) eventos estão disponíveis para a coleção.</span><span class="sxs-lookup"><span data-stu-id="e3d01-169">Starting with hello 5.7 release of Service Fabric, [reverse proxy](service-fabric-reverseproxy.md) events are available for collection.</span></span>
<span data-ttu-id="e3d01-170">Proxy reverso emite eventos em dois canais, um erro que contém eventos refletindo falhas de processamento de solicitação e Olá outros uma que contém eventos detalhados sobre todas as solicitações de saudação processados no proxy reverso hello.</span><span class="sxs-lookup"><span data-stu-id="e3d01-170">Reverse proxy emits events into two channels, one containing error events reflecting request processing failures and hello other one containing verbose events about all hello requests processed at hello reverse proxy.</span></span> 

1. <span data-ttu-id="e3d01-171">Coletar eventos de erro: tooview adicionar esses eventos no Visualizador de eventos diagnóstico do Visual Studio "Microsoft-ServiceFabric:4:0x4000000000000010" toohello lista de provedores do ETW.</span><span class="sxs-lookup"><span data-stu-id="e3d01-171">Collect error events: tooview these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000010" toohello list of ETW providers.</span></span>
<span data-ttu-id="e3d01-172">eventos de saudação toocollect de clusters do Azure, modifique tooinclude de modelo do Gerenciador de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="e3d01-172">toocollect hello events from Azure clusters, modify hello Resource Manager template tooinclude</span></span>

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

2. <span data-ttu-id="e3d01-173">Coletar todos os eventos de processamento de solicitação: visualizador no Visual Studio de eventos diagnóstico, entrada hello ServiceFabric do Microsoft update Olá lista de provedor ETW muito "Microsoft-ServiceFabric:4:0x4000000000000020".</span><span class="sxs-lookup"><span data-stu-id="e3d01-173">Collect all request processing events: In Visual Studio's Diagnostic Event Viewer, update hello Microsoft-ServiceFabric entry in hello ETW provider list too"Microsoft-ServiceFabric:4:0x4000000000000020".</span></span>
<span data-ttu-id="e3d01-174">Para clusters de malha do serviço do Azure, modifique Olá tooinclude de modelo de Gerenciador de recursos</span><span class="sxs-lookup"><span data-stu-id="e3d01-174">For Azure Service Fabric clusters, modify hello resource manager template tooinclude</span></span>

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
> <span data-ttu-id="e3d01-175">É recomendável toojudiciously habilitar coleta de eventos deste canal como isso coleta todo o tráfego por meio do proxy reverso hello e pode consumir rapidamente a capacidade de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e3d01-175">It is recommended toojudiciously enable collecting events from this channel as this collects all traffic through hello reverse proxy and can quickly consume storage capacity.</span></span>

<span data-ttu-id="e3d01-176">Para clusters de malha do serviço do Azure, os eventos de saudação de todos os nós de saudação são coletados e agregados em Olá SystemEventTable.</span><span class="sxs-lookup"><span data-stu-id="e3d01-176">For Azure Service Fabric clusters, hello events from all hello nodes are collected and aggregated in hello SystemEventTable.</span></span>
<span data-ttu-id="e3d01-177">Para obter a solução de problemas de eventos de proxy reverso hello, consulte Olá [guia de diagnóstico de proxy reverso](service-fabric-reverse-proxy-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="e3d01-177">For detailed troubleshooting of hello reverse proxy events, refer hello [reverse proxy diagnostics guide](service-fabric-reverse-proxy-diagnostics.md).</span></span>

## <a name="collect-from-new-eventsource-channels"></a><span data-ttu-id="e3d01-178">Coletar a partir de novos canais EventSource</span><span class="sxs-lookup"><span data-stu-id="e3d01-178">Collect from new EventSource channels</span></span>

<span data-ttu-id="e3d01-179">logs de toocollect tooupdate diagnóstico de novos canais de EventSource que representam um novo aplicativo que você está prestes a toodeploy, executar Olá mesmas etapas conforme descritas anteriormente para a configuração de saudação do diagnóstico para um cluster existente.</span><span class="sxs-lookup"><span data-stu-id="e3d01-179">tooupdate Diagnostics toocollect logs from new EventSource channels that represent a new application that you're about toodeploy, perform hello same steps as previously described for hello setup of Diagnostics for an existing cluster.</span></span>

<span data-ttu-id="e3d01-180">Atualizar Olá `EtwEventSourceProviderConfiguration` seção nas entradas de tooadd Olá template.json arquivo hello novos EventSource canais antes de aplicar a configuração de saudação atualizar usando Olá `New-AzureRmResourceGroupDeployment` comando do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e3d01-180">Update hello `EtwEventSourceProviderConfiguration` section in hello template.json file tooadd entries for hello new EventSource channels before you apply hello configuration update by using hello `New-AzureRmResourceGroupDeployment` PowerShell command.</span></span> <span data-ttu-id="e3d01-181">nome de saudação da origem de eventos de saudação é definido como parte do seu código no arquivo do hello ServiceEventSource.cs gerado pelo Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e3d01-181">hello name of hello event source is defined as part of your code in hello Visual Studio-generated ServiceEventSource.cs file.</span></span>

<span data-ttu-id="e3d01-182">Por exemplo, se a origem do evento é denominada Meu Eventsource, adicione Olá após eventos de saudação do código tooplace do meu Eventsource em uma tabela nomeada MyDestinationTableName.</span><span class="sxs-lookup"><span data-stu-id="e3d01-182">For example, if your event source is named My-Eventsource, add hello following code tooplace hello events from My-Eventsource into a table named MyDestinationTableName.</span></span>

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

<span data-ttu-id="e3d01-183">contadores de desempenho de toocollect ou logs de eventos, modificar o modelo de Gerenciador de recursos de saudação usando exemplos Olá fornecidos [criar uma máquina virtual do Windows com o monitoramento e diagnóstico usando um modelo do Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e3d01-183">toocollect performance counters or event logs, modify hello Resource Manager template by using hello examples provided in [Create a Windows virtual machine with monitoring and diagnostics by using an Azure Resource Manager template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="e3d01-184">Em seguida, republicar o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3d01-184">Then, republish hello Resource Manager template.</span></span>

## <a name="collect-performance-counters"></a><span data-ttu-id="e3d01-185">Coletar contadores de desempenho</span><span class="sxs-lookup"><span data-stu-id="e3d01-185">Collect Performance Counters</span></span>

<span data-ttu-id="e3d01-186">toocollect métricas de desempenho do seu cluster, adicione tooyour de contadores de desempenho do hello "WadCfg > DiagnosticMonitorConfiguration" no modelo do Gerenciador de recursos de saudação para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="e3d01-186">toocollect performance metrics from your cluster, add hello performance counters tooyour "WadCfg > DiagnosticMonitorConfiguration" in hello Resource Manager template for your cluster.</span></span> <span data-ttu-id="e3d01-187">Consulte [Contadores de desempenho do Service Fabric](service-fabric-diagnostics-event-generation-perf.md) para contadores de desempenho que recomendamos para coleta.</span><span class="sxs-lookup"><span data-stu-id="e3d01-187">See [Service Fabric Performance Counters](service-fabric-diagnostics-event-generation-perf.md) for performance counters that we recommend collecting.</span></span>

<span data-ttu-id="e3d01-188">Por exemplo, aqui vamos definir um contador de desempenho, a cada 15 segundos de amostra (Isso pode ser alterado e segue Olá formato de "PT\<tempo >\<unidade >", por exemplo, PT3M seria amostragem em três minutos) e transferida toohello tabela de armazenamento apropriado cada um minuto.</span><span class="sxs-lookup"><span data-stu-id="e3d01-188">For example, here we set one performance counter, sampled every 15 seconds (this can be changed and follows hello format of "PT\<time>\<unit>", for example, PT3M would sample at three minute intervals), and transferred toohello appropriate storage table every one minute.</span></span>

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
  
<span data-ttu-id="e3d01-189">Se você estiver usando um coletor do Application Insights, conforme descrito na seção de saudação abaixo e deseja tooshow essas métricas para cima no Application Insights, faça-se de nome de coletor de saudação tooadd na seção de "coletores" hello como mostrado acima.</span><span class="sxs-lookup"><span data-stu-id="e3d01-189">If you are using an Application Insights sink, as described in hello section below, and want these metrics tooshow up in Application Insights, then make sure tooadd hello sink name in hello "sinks" section as shown above.</span></span> <span data-ttu-id="e3d01-190">Além disso, considere a criação de uma tabela separada toosend seus contadores de desempenho, para que eles não prejudique out Olá dados provenientes do hello outros canais de registro que você tiver habilitado.</span><span class="sxs-lookup"><span data-stu-id="e3d01-190">Additionally, consider creating a separate table toosend your Performance Counters to, so they don't crowd out hello data coming from hello other logging channels you have enabled.</span></span>


## <a name="send-logs-tooapplication-insights"></a><span data-ttu-id="e3d01-191">Enviar logs tooApplication Insights</span><span class="sxs-lookup"><span data-stu-id="e3d01-191">Send logs tooApplication Insights</span></span>

<span data-ttu-id="e3d01-192">Enviar dados de monitoramento e diagnóstico tooApplication Insights (AI) pode ser feito como parte da configuração do WAD hello.</span><span class="sxs-lookup"><span data-stu-id="e3d01-192">Sending monitoring and diagnostics data tooApplication Insights (AI) can be done as part of hello WAD configuration.</span></span> <span data-ttu-id="e3d01-193">Se você decidir toouse AI para visualização e análise de eventos, leia [visualização com o Application Insights e análise de eventos](service-fabric-diagnostics-event-analysis-appinsights.md) tooset a um coletor AI como parte da "WadCfg".</span><span class="sxs-lookup"><span data-stu-id="e3d01-193">If you decide toouse AI for event analysis and visualization, read [Event Analysis and Visualization with Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) tooset up an AI Sink as part of your "WadCfg".</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3d01-194">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e3d01-194">Next steps</span></span>

<span data-ttu-id="e3d01-195">Depois que você configurou corretamente o diagnóstico do Azure, você verá os dados nas tabelas de armazenamento dos logs de EventSource e Olá ETW.</span><span class="sxs-lookup"><span data-stu-id="e3d01-195">Once you have correctly configured Azure diagnostics, you will see data in your Storage tables from hello ETW and EventSource logs.</span></span> <span data-ttu-id="e3d01-196">Se você escolher toouse OMS, Kibana, ou outros dados análise e visualização de plataforma que não é configurada diretamente no modelo do Gerenciador de recursos de saudação, verifique tooset-se de que a plataforma de saudação do tooread sua escolha nos dados Olá dessas tabelas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e3d01-196">If you choose toouse OMS, Kibana, or any other data analytics and visualization platform that is not directly configured in hello Resource Manager template, make sure tooset up hello platform of your choice tooread in hello data from these storage tables.</span></span> <span data-ttu-id="e3d01-197">Fazer isso para OMS é relativamente simples e é explicado em [Análise de eventos e logs no OMS](service-fabric-diagnostics-event-analysis-oms.md).</span><span class="sxs-lookup"><span data-stu-id="e3d01-197">Doing this for OMS is relatively trivial, and is explained in [Event and log analysis through OMS](service-fabric-diagnostics-event-analysis-oms.md).</span></span> <span data-ttu-id="e3d01-198">O Application Insights é um pouco de um caso especial nesse sentido, pois ele pode ser configurado como parte da configuração de extensão de diagnóstico hello, então consulte toohello [apropriado](service-fabric-diagnostics-event-analysis-appinsights.md) se você escolher toouse AI.</span><span class="sxs-lookup"><span data-stu-id="e3d01-198">Application Insights is a bit of a special case in this sense, since it can be configured as part of hello Diagnostics extension configuration, so refer toohello [appropriate article](service-fabric-diagnostics-event-analysis-appinsights.md) if you choose toouse AI.</span></span>

>[!NOTE]
><span data-ttu-id="e3d01-199">Atualmente, não há nenhuma maneira toofilter ou limpar Olá eventos enviados toohello tabela.</span><span class="sxs-lookup"><span data-stu-id="e3d01-199">There is currently no way toofilter or groom hello events that are sent toohello table.</span></span> <span data-ttu-id="e3d01-200">Se você não implementa um tooremove de processar eventos de tabela hello, tabela Olá continuará toogrow.</span><span class="sxs-lookup"><span data-stu-id="e3d01-200">If you don't implement a process tooremove events from hello table, hello table will continue toogrow.</span></span> <span data-ttu-id="e3d01-201">Atualmente, há um exemplo de um serviço de manutenção de dados em execução no hello [exemplo Watchdog](https://github.com/Azure-Samples/service-fabric-watchdog-service), e é recomendável que você escreva uma para você mesmo assim, a menos que haja uma boa razão para você toostore logs além de um período de 30 ou 90 dias.</span><span class="sxs-lookup"><span data-stu-id="e3d01-201">Currently, there is an example of a data grooming service running in hello [Watchdog sample](https://github.com/Azure-Samples/service-fabric-watchdog-service), and it is recommended that you write one for yourself as well, unless there is a good reason for you toostore logs beyond a 30 or 90 day timeframe.</span></span>

* [<span data-ttu-id="e3d01-202">Saiba como os contadores de desempenho de toocollect ou logs usando Olá extensão de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="e3d01-202">Learn how toocollect performance counters or logs by using hello Diagnostics extension</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="e3d01-203">Visualização e Análise de Eventos com o Application Insights</span><span class="sxs-lookup"><span data-stu-id="e3d01-203">Event Analysis and Visualization with Application Insights</span></span>](service-fabric-diagnostics-event-analysis-appinsights.md)
* [<span data-ttu-id="e3d01-204">Visualização e Análise de Eventos com o OMS</span><span class="sxs-lookup"><span data-stu-id="e3d01-204">Event Analysis and Visualization with OMS</span></span>](service-fabric-diagnostics-event-analysis-oms.md)