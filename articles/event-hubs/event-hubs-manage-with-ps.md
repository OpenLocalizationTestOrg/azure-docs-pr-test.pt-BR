---
title: recursos de Hubs de eventos do Azure aaaUse PowerShell toomanage | Microsoft Docs
description: "Usar toocreate de módulo do PowerShell e gerenciar os Hubs de eventos"
services: event-hubs
documentationcenter: .NET
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: d79cb307c2b4a031d059ce6ca67117ffc0b4600b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomanage-event-hubs-resources"></a><span data-ttu-id="f72f6-103">Usar recursos de Hubs de eventos do PowerShell toomanage</span><span class="sxs-lookup"><span data-stu-id="f72f6-103">Use PowerShell toomanage Event Hubs resources</span></span>

<span data-ttu-id="f72f6-104">Microsoft Azure PowerShell é um ambiente de script que você pode usar toocontrol e automatizar a implantação de saudação e o gerenciamento de serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="f72f6-104">Microsoft Azure PowerShell is a scripting environment that you can use toocontrol and automate hello deployment and management of Azure services.</span></span> <span data-ttu-id="f72f6-105">Este artigo descreve como Olá toouse [módulo PowerShell do Gerenciador de recursos de Hubs de evento](/powershell/module/azurerm.eventhub) tooprovision e gerenciar entidades de Hubs de eventos (namespaces, os hubs de eventos individuais e grupos de consumidores) usando um console local do PowerShell do Azure ou script.</span><span class="sxs-lookup"><span data-stu-id="f72f6-105">This article describes how toouse hello [Event Hubs Resource Manager PowerShell module](/powershell/module/azurerm.eventhub) tooprovision and manage Event Hubs entities (namespaces, individual event hubs, and consumer groups) using a local Azure PowerShell console or script.</span></span>

<span data-ttu-id="f72f6-106">Também é possível gerenciar recursos dos Hubs de Eventos usando modelos do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f72f6-106">You can also manage Event Hubs resources using Azure Resource Manager templates.</span></span> <span data-ttu-id="f72f6-107">Para obter mais informações, consulte o artigo Olá [criar um namespace de Hubs de eventos com o grupo de consumidor e hub de eventos usando um modelo do Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub.md).</span><span class="sxs-lookup"><span data-stu-id="f72f6-107">For more information, see hello article [Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f72f6-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f72f6-108">Prerequisites</span></span>

<span data-ttu-id="f72f6-109">Antes de começar, você precisará seguir hello:</span><span class="sxs-lookup"><span data-stu-id="f72f6-109">Before you begin, you'll need hello following:</span></span>

* <span data-ttu-id="f72f6-110">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="f72f6-110">An Azure subscription.</span></span> <span data-ttu-id="f72f6-111">Para saber mais sobre como adquirir uma assinatura, confira [Opções de compra][purchase options], [ofertas para membros][member offers] ou [conta gratuita][free account].</span><span class="sxs-lookup"><span data-stu-id="f72f6-111">For more information about obtaining a subscription, see [purchase options][purchase options], [member offers][member offers], or [free account][free account].</span></span>
* <span data-ttu-id="f72f6-112">Um computador com o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="f72f6-112">A computer with Azure PowerShell.</span></span> <span data-ttu-id="f72f6-113">Para obter instruções, consulte [Introdução aos cmdlets do Azure PowerShell](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="f72f6-113">For instructions, see [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps).</span></span>
* <span data-ttu-id="f72f6-114">Uma compreensão geral dos scripts do PowerShell, pacotes do NuGet e saudação do .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="f72f6-114">A general understanding of PowerShell scripts, NuGet packages, and hello .NET Framework.</span></span>

## <a name="get-started"></a><span data-ttu-id="f72f6-115">Introdução</span><span class="sxs-lookup"><span data-stu-id="f72f6-115">Get started</span></span>

<span data-ttu-id="f72f6-116">Olá primeira etapa é toouse PowerShell toolog em tooyour conta do Azure e assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="f72f6-116">hello first step is toouse PowerShell toolog in tooyour Azure account and Azure subscription.</span></span> <span data-ttu-id="f72f6-117">Siga as instruções de saudação em [Introdução aos cmdlets do PowerShell do Azure](/powershell/azure/get-started-azureps) toolog em tooyour conta do Azure, em seguida, recuperar e acessar recursos de saudação em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="f72f6-117">Follow hello instructions in [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps) toolog in tooyour Azure account, then retrieve and access hello resources in your Azure subscription.</span></span>

## <a name="provision-an-event-hubs-namespace"></a><span data-ttu-id="f72f6-118">Provisionar um namespace dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="f72f6-118">Provision an Event Hubs namespace</span></span>

<span data-ttu-id="f72f6-119">Ao trabalhar com namespaces de Hubs de eventos, você pode usar o hello [Get-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace), [New-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace), [AzureRmEventHubNamespace remover](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace) , e [AzureRmEventHubNamespace conjunto](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace) cmdlets.</span><span class="sxs-lookup"><span data-stu-id="f72f6-119">When working with Event Hubs namespaces, you can use hello [Get-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace), [New-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace), [Remove-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace), and [Set-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace) cmdlets.</span></span>

<span data-ttu-id="f72f6-120">Este exemplo cria algumas variáveis locais no script hello; `$Namespace` e `$Location`.</span><span class="sxs-lookup"><span data-stu-id="f72f6-120">This example creates a few local variables in hello script; `$Namespace` and `$Location`.</span></span>

* <span data-ttu-id="f72f6-121">`$Namespace`é o nome de saudação do namespace de Hubs de eventos de saudação com a qual queremos toowork.</span><span class="sxs-lookup"><span data-stu-id="f72f6-121">`$Namespace` is hello name of hello Event Hubs namespace with which we want toowork.</span></span>
* <span data-ttu-id="f72f6-122">`$Location`identifica Olá data center em que podemos provisionará Olá namespace.</span><span class="sxs-lookup"><span data-stu-id="f72f6-122">`$Location` identifies hello data center in which will we provision hello namespace.</span></span>
* <span data-ttu-id="f72f6-123">`$CurrentNamespace`armazena o namespace de referência Olá recuperar (ou criar).</span><span class="sxs-lookup"><span data-stu-id="f72f6-123">`$CurrentNamespace` stores hello reference namespace that we retrieve (or create).</span></span>

<span data-ttu-id="f72f6-124">Em um script real, `$Namespace` e `$Location` podem ser passados como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="f72f6-124">In an actual script, `$Namespace` and `$Location` can be passed as parameters.</span></span>

<span data-ttu-id="f72f6-125">Esta parte do script Olá Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="f72f6-125">This part of hello script does hello following:</span></span>

1. <span data-ttu-id="f72f6-126">Tentativas tooretrieve um namespace de Hubs de eventos com hello nome especificado.</span><span class="sxs-lookup"><span data-stu-id="f72f6-126">Attempts tooretrieve an Event Hubs namespace with hello specified name.</span></span>
2. <span data-ttu-id="f72f6-127">Se Olá namespace for encontrado, ele informa o que foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="f72f6-127">If hello namespace is found, it reports what was found.</span></span>
3. <span data-ttu-id="f72f6-128">Se Olá namespace não for encontrado, ele cria Olá namespace e recupera Olá recém-criado namespace.</span><span class="sxs-lookup"><span data-stu-id="f72f6-128">If hello namespace is not found, it creates hello namespace and then retrieves hello newly created namespace.</span></span>

    ```powershell
    # Query toosee if hello namespace currently exists
    $CurrentNamespace = Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
   
    # Check if hello namespace already exists or needs toobe created
    if ($CurrentNamespace)
    {
        Write-Host "hello namespace $Namespace already exists in hello $Location region:"
        # Report what was found
        Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "hello $Namespace namespace does not exist."
        Write-Host "Creating hello $Namespace namespace in hello $Location region..."
        New-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
        Write-Host "hello $Namespace namespace in Resource Group $ResGrpName in hello $Location region has been successfully created."
    }
    ```

## <a name="create-an-event-hub"></a><span data-ttu-id="f72f6-129">Criar um Hub de Evento</span><span class="sxs-lookup"><span data-stu-id="f72f6-129">Create an event hub</span></span>

<span data-ttu-id="f72f6-130">toocreate um hub de eventos, execute uma verificação de namespace usando o script hello na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="f72f6-130">toocreate an event hub, perform a namespace check using hello script in hello previous section.</span></span> <span data-ttu-id="f72f6-131">Em seguida, use Olá [AzureRmEventHub novo](/powershell/module/azurerm.eventhub/new-azurermeventhub) hub de eventos do cmdlet toocreate hello:</span><span class="sxs-lookup"><span data-stu-id="f72f6-131">Then, use hello [New-AzureRmEventHub](/powershell/module/azurerm.eventhub/new-azurermeventhub) cmdlet toocreate hello event hub:</span></span>

```powershell
# Check if event hub already exists
$CurrentEH = Get-AzureRMEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName

if($CurrentEH)
{
    Write-Host "hello event hub $EventHubName already exists in hello $Location region:"
    # Report what was found
    Get-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
}
else
{
    Write-Host "hello $EventHubName event hub does not exist."
    Write-Host "Creating hello $EventHubName event hub in hello $Location region..."
    New-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -Location $Location -MessageRetentionInDays 3
    $CurrentEH = Get-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
    Write-Host "hello $EventHubName event hub in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

### <a name="create-a-consumer-group"></a><span data-ttu-id="f72f6-132">Criar um grupo de consumidores</span><span class="sxs-lookup"><span data-stu-id="f72f6-132">Create a consumer group</span></span>

<span data-ttu-id="f72f6-133">toocreate um grupo de consumidor dentro de um hub de eventos, executar Olá namespace e o evento de hub verificações usando scripts de saudação na seção anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="f72f6-133">toocreate a consumer group within an event hub, perform hello namespace and event hub checks using hello scripts in hello previous section.</span></span> <span data-ttu-id="f72f6-134">Em seguida, use Olá [AzureRmEventHubConsumerGroup novo](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup) grupo de consumidores do cmdlet toocreate Olá no hub de eventos de saudação.</span><span class="sxs-lookup"><span data-stu-id="f72f6-134">Then, use hello [New-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup) cmdlet toocreate hello consumer group within hello event hub.</span></span> <span data-ttu-id="f72f6-135">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="f72f6-135">For example:</span></span>

```powershell
# Check if consumer group already exists
$CurrentCG = Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -ErrorAction Ignore

if($CurrentCG)
{
    Write-Host "hello consumer group $ConsumerGroupName in event hub $EventHubName already exists in hello $Location region:"
    # Report what was found
    Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
}
else
{
    Write-Host "hello $ConsumerGroupName consumer group does not exist."
    Write-Host "Creating hello $ConsumerGroupName consumer group in hello $Location region..."
    New-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
    $CurrentCG = Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
    Write-Host "hello $ConsumerGroupName consumer group in event hub $EventHubName in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

#### <a name="set-user-metadata"></a><span data-ttu-id="f72f6-136">Definir metadados do usuário</span><span class="sxs-lookup"><span data-stu-id="f72f6-136">Set user metadata</span></span>

<span data-ttu-id="f72f6-137">Depois de executar scripts de saudação em Olá anterior seções, você pode usar o hello [AzureRmEventHubConsumerGroup conjunto](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup) propriedades de saudação do cmdlet tooupdate de um grupo de consumidores, como no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="f72f6-137">After executing hello scripts in hello preceding sections, you can use hello [Set-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup) cmdlet tooupdate hello properties of a consumer group, as in hello following example:</span></span>

```powershell
# Set some user metadata on hello CG
Write-Host "Setting hello UserMetadata field too'Testing'"
Set-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -UserMetadata "Testing"
# Show result
Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
```

## <a name="remove-event-hub"></a><span data-ttu-id="f72f6-138">Remover hub de eventos</span><span class="sxs-lookup"><span data-stu-id="f72f6-138">Remove event hub</span></span>

<span data-ttu-id="f72f6-139">hubs de eventos de saudação tooremove criado, você pode usar o hello `Remove-*` cmdlets, como no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="f72f6-139">tooremove hello event hubs you created, you can use hello `Remove-*` cmdlets, as in hello following example:</span></span>

```powershell
# Clean up
Remove-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
Remove-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
Remove-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
```

## <a name="next-steps"></a><span data-ttu-id="f72f6-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f72f6-140">Next steps</span></span>

- <span data-ttu-id="f72f6-141">Consulte a documentação completa de módulo evento Hubs Gerenciador de recursos do PowerShell Olá [aqui](/powershell/module/azurerm.eventhub).</span><span class="sxs-lookup"><span data-stu-id="f72f6-141">See hello complete Event Hubs Resource Manager PowerShell module documentation [here](/powershell/module/azurerm.eventhub).</span></span> <span data-ttu-id="f72f6-142">Esta página lista todos os cmdlets disponíveis.</span><span class="sxs-lookup"><span data-stu-id="f72f6-142">This page lists all available cmdlets.</span></span>
- <span data-ttu-id="f72f6-143">Para obter informações sobre como usar modelos do Azure Resource Manager, consulte o artigo Olá [criar um namespace de Hubs de eventos com o grupo de consumidor e hub de eventos usando um modelo do Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub.md).</span><span class="sxs-lookup"><span data-stu-id="f72f6-143">For information about using Azure Resource Manager templates, see hello article [Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub.md).</span></span>
- <span data-ttu-id="f72f6-144">Informações sobre [Bibliotecas de gerenciamento .NET dos Hubs de Eventos](event-hubs-management-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="f72f6-144">Information about [Event Hubs .NET management libraries](event-hubs-management-libraries.md).</span></span>

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
