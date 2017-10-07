---
title: "recursos de barramento de serviço do Azure aaaUse PowerShell toomanage | Microsoft Docs"
description: "Usar toocreate de módulo do PowerShell e gerenciar recursos do barramento de serviço"
services: service-bus-messaging
documentationcenter: .NET
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/06/2017
ms.author: sethm
ms.openlocfilehash: 737044def913c5798e7e05fc4f1aeece76c8f4dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomanage-service-bus-resources"></a><span data-ttu-id="e53ae-103">Usar recursos de barramento de serviço do PowerShell toomanage</span><span class="sxs-lookup"><span data-stu-id="e53ae-103">Use PowerShell toomanage Service Bus resources</span></span>

<span data-ttu-id="e53ae-104">Microsoft Azure PowerShell é um ambiente de script que você pode usar toocontrol e automatizar a implantação de saudação e o gerenciamento de serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="e53ae-104">Microsoft Azure PowerShell is a scripting environment that you can use toocontrol and automate hello deployment and management of Azure services.</span></span> <span data-ttu-id="e53ae-105">Este artigo descreve como Olá toouse [módulo PowerShell do Gerenciador de recursos do barramento de serviço](/powershell/module/azurerm.servicebus) tooprovision e gerenciar entidades do barramento de serviço (namespaces, filas, tópicos e assinaturas) usando um console local do PowerShell do Azure ou script.</span><span class="sxs-lookup"><span data-stu-id="e53ae-105">This article describes how toouse hello [Service Bus Resource Manager PowerShell module](/powershell/module/azurerm.servicebus) tooprovision and manage Service Bus entities (namespaces, queues, topics, and subscriptions) using a local Azure PowerShell console or script.</span></span>

<span data-ttu-id="e53ae-106">Também é possível gerenciar entidades do Barramento de Serviço usando modelos do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e53ae-106">You can also manage Service Bus entities using Azure Resource Manager templates.</span></span> <span data-ttu-id="e53ae-107">Para obter mais informações, consulte o artigo Olá [recursos de barramento de serviço criar usando modelos do Azure Resource Manager](service-bus-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e53ae-107">For more information, see hello article [Create Service Bus resources using Azure Resource Manager templates](service-bus-resource-manager-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e53ae-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e53ae-108">Prerequisites</span></span>

<span data-ttu-id="e53ae-109">Antes de começar, você precisará seguir hello:</span><span class="sxs-lookup"><span data-stu-id="e53ae-109">Before you begin, you'll need hello following:</span></span>

* <span data-ttu-id="e53ae-110">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="e53ae-110">An Azure subscription.</span></span> <span data-ttu-id="e53ae-111">Para saber mais sobre como adquirir uma assinatura, confira [Opções de compra][purchase options], [ofertas para membros][member offers] ou [conta gratuita][free account].</span><span class="sxs-lookup"><span data-stu-id="e53ae-111">For more information about obtaining a subscription, see [purchase options][purchase options], [member offers][member offers], or [free account][free account].</span></span>
* <span data-ttu-id="e53ae-112">Um computador com o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="e53ae-112">A computer with Azure PowerShell.</span></span> <span data-ttu-id="e53ae-113">Para obter instruções, consulte [Introdução aos cmdlets do Azure PowerShell](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="e53ae-113">For instructions, see [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps).</span></span>
* <span data-ttu-id="e53ae-114">Uma compreensão geral dos scripts do PowerShell, pacotes do NuGet e saudação do .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="e53ae-114">A general understanding of PowerShell scripts, NuGet packages, and hello .NET Framework.</span></span>

## <a name="get-started"></a><span data-ttu-id="e53ae-115">Introdução</span><span class="sxs-lookup"><span data-stu-id="e53ae-115">Get started</span></span>

<span data-ttu-id="e53ae-116">Olá primeira etapa é toouse PowerShell toolog em tooyour conta do Azure e assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="e53ae-116">hello first step is toouse PowerShell toolog in tooyour Azure account and Azure subscription.</span></span> <span data-ttu-id="e53ae-117">Siga as instruções de saudação em [Introdução aos cmdlets do PowerShell do Azure](/powershell/azure/get-started-azureps) toolog tooyour conta do Azure e recuperar e acessar recursos de saudação em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="e53ae-117">Follow hello instructions in [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps) toolog in tooyour Azure account, and retrieve and access hello resources in your Azure subscription.</span></span>

## <a name="provision-a-service-bus-namespace"></a><span data-ttu-id="e53ae-118">Provisionar um namespace do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="e53ae-118">Provision a Service Bus namespace</span></span>

<span data-ttu-id="e53ae-119">Ao trabalhar com namespaces de barramento de serviço, você pode usar o hello [Get-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [New-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace), e [AzureRmServiceBusNamespace conjunto](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) cmdlets.</span><span class="sxs-lookup"><span data-stu-id="e53ae-119">When working with Service Bus namespaces, you can use hello [Get-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [New-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace), and [Set-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) cmdlets.</span></span>

<span data-ttu-id="e53ae-120">Este exemplo cria algumas variáveis locais no script hello; `$Namespace` e `$Location`.</span><span class="sxs-lookup"><span data-stu-id="e53ae-120">This example creates a few local variables in hello script; `$Namespace` and `$Location`.</span></span>

* <span data-ttu-id="e53ae-121">`$Namespace`é o nome de saudação do namespace de barramento de serviço Olá com a qual queremos toowork.</span><span class="sxs-lookup"><span data-stu-id="e53ae-121">`$Namespace` is hello name of hello Service Bus namespace with which we want toowork.</span></span>
* <span data-ttu-id="e53ae-122">`$Location`identifica Olá data center em que podemos provisionará Olá namespace.</span><span class="sxs-lookup"><span data-stu-id="e53ae-122">`$Location` identifies hello data center in which will we provision hello namespace.</span></span>
* <span data-ttu-id="e53ae-123">`$CurrentNamespace`armazena o namespace de referência Olá recuperar (ou criar).</span><span class="sxs-lookup"><span data-stu-id="e53ae-123">`$CurrentNamespace` stores hello reference namespace that we retrieve (or create).</span></span>

<span data-ttu-id="e53ae-124">Em um script real, `$Namespace` e `$Location` podem ser passados como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="e53ae-124">In an actual script, `$Namespace` and `$Location` can be passed as parameters.</span></span>

<span data-ttu-id="e53ae-125">Esta parte do script Olá Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="e53ae-125">This part of hello script does hello following:</span></span>

1. <span data-ttu-id="e53ae-126">Tentativas tooretrieve um namespace de barramento de serviço com hello nome especificado.</span><span class="sxs-lookup"><span data-stu-id="e53ae-126">Attempts tooretrieve a Service Bus namespace with hello specified name.</span></span>
2. <span data-ttu-id="e53ae-127">Se Olá namespace for encontrado, ele informa o que foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="e53ae-127">If hello namespace is found, it reports what was found.</span></span>
3. <span data-ttu-id="e53ae-128">Se Olá namespace não for encontrado, ele cria Olá namespace e recupera Olá recém-criado namespace.</span><span class="sxs-lookup"><span data-stu-id="e53ae-128">If hello namespace is not found, it creates hello namespace and then retrieves hello newly created namespace.</span></span>
   
    ``` powershell
    # Query toosee if hello namespace currently exists
    $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
   
    # Check if hello namespace already exists or needs toobe created
    if ($CurrentNamespace)
    {
        Write-Host "hello namespace $Namespace already exists in hello $Location region:"
        # Report what was found
        Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "hello $Namespace namespace does not exist."
        Write-Host "Creating hello $Namespace namespace in hello $Location region..."
        New-AzureRmServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
        Write-Host "hello $Namespace namespace in Resource Group $ResGrpName in hello $Location region has been successfully created."
                
    }
    ```

### <a name="create-a-namespace-authorization-rule"></a><span data-ttu-id="e53ae-129">Criar uma regra de autorização de namespace</span><span class="sxs-lookup"><span data-stu-id="e53ae-129">Create a namespace authorization rule</span></span>

<span data-ttu-id="e53ae-130">Olá exemplo a seguir mostra como regras de autorização de namespace toomanage usando Olá [New-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [Conjunto AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule), e [AzureRmServiceBusNamespaceAuthorizationRule remover cmdlets](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule).</span><span class="sxs-lookup"><span data-stu-id="e53ae-130">hello following example shows how toomanage namespace authorization rules using hello [New-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [Set-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule), and [Remove-AzureRmServiceBusNamespaceAuthorizationRule cmdlets](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule).</span></span>

```powershell
# Query toosee if rule exists
$CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

# Check if hello rule already exists or needs toobe created
if ($CurrentRule)
{
    Write-Host "hello $AuthRule rule already exists for hello namespace $Namespace."
}
else
{
    Write-Host "hello $AuthRule rule does not exist."
    Write-Host "Creating hello $AuthRule rule for hello $Namespace namespace..."
    New-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule -Rights @("Listen","Send")
    $CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
    Write-Host "hello $AuthRule rule for hello $Namespace namespace has been successfully created."

    Write-Host "Setting rights on hello namespace"
    $authRuleObj = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

    Write-Host "Remove Send rights"
    $authRuleObj.Rights.Remove("Send")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj

    Write-Host "Add Send and Manage rights toohello namespace"
    $authRuleObj.Rights.Add("Send")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj
    $authRuleObj.Rights.Add("Manage")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj

    Write-Host "Show value of primary key"
    $CurrentKey = Get-AzureRmServiceBusNamespaceKey -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
        
    Write-Host "Remove this authorization rule"
    Remove-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
}
```

## <a name="create-a-queue"></a><span data-ttu-id="e53ae-131">Criar uma fila</span><span class="sxs-lookup"><span data-stu-id="e53ae-131">Create a queue</span></span>

<span data-ttu-id="e53ae-132">toocreate uma fila ou tópico, execute uma verificação de namespace usando o script hello na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="e53ae-132">toocreate a queue or topic, perform a namespace check using hello script in hello previous section.</span></span> <span data-ttu-id="e53ae-133">Em seguida, crie uma fila de saudação:</span><span class="sxs-lookup"><span data-stu-id="e53ae-133">Then, create hello queue:</span></span>

```powershell
# Check if queue already exists
$CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName

if($CurrentQ)
{
    Write-Host "hello queue $QueueName already exists in hello $Location region:"
}
else
{
    Write-Host "hello $QueueName queue does not exist."
    Write-Host "Creating hello $QueueName queue in hello $Location region..."
    New-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -EnablePartitioning $True
    $CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName
    Write-Host "hello $QueueName queue in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

### <a name="modify-queue-properties"></a><span data-ttu-id="e53ae-134">Modificar propriedades da fila</span><span class="sxs-lookup"><span data-stu-id="e53ae-134">Modify queue properties</span></span>

<span data-ttu-id="e53ae-135">Depois de executar o script de saudação em Olá anterior seção, você pode usar o hello [AzureRmServiceBusQueue conjunto](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) propriedades de saudação do cmdlet tooupdate de uma fila, como no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="e53ae-135">After executing hello script in hello preceding section, you can use hello [Set-AzureRmServiceBusQueue](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) cmdlet tooupdate hello properties of a queue, as in hello following example:</span></span>

```powershell
$CurrentQ.DeadLetteringOnMessageExpiration = $True
$CurrentQ.MaxDeliveryCount = 7
$CurrentQ.MaxSizeInMegabytes = 2048
$CurrentQ.EnableExpress = $True

Set-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -QueueObj $CurrentQ
```

## <a name="provisioning-other-service-bus-entities"></a><span data-ttu-id="e53ae-136">Provisionamento de outras entidades do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="e53ae-136">Provisioning other Service Bus entities</span></span>

<span data-ttu-id="e53ae-137">Você pode usar o hello [módulo PowerShell do barramento de serviço](/powershell/module/azurerm.servicebus) tooprovision outras entidades, como tópicos e assinaturas.</span><span class="sxs-lookup"><span data-stu-id="e53ae-137">You can use hello [Service Bus PowerShell module](/powershell/module/azurerm.servicebus) tooprovision other entities, such as topics and subscriptions.</span></span> <span data-ttu-id="e53ae-138">Esses cmdlets são sintaticamente semelhantes cmdlets de criação de fila toohello demonstrado na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="e53ae-138">These cmdlets are syntactically similar toohello queue creation cmdlets demonstrated in hello previous section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e53ae-139">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e53ae-139">Next steps</span></span>

- <span data-ttu-id="e53ae-140">Consulte a documentação completa de módulo PowerShell Gerenciador de recursos do barramento de serviço Olá [aqui](/powershell/module/azurerm.servicebus).</span><span class="sxs-lookup"><span data-stu-id="e53ae-140">See hello complete Service Bus Resource Manager PowerShell module documentation [here](/powershell/module/azurerm.servicebus).</span></span> <span data-ttu-id="e53ae-141">Esta página lista todos os cmdlets disponíveis.</span><span class="sxs-lookup"><span data-stu-id="e53ae-141">This page lists all available cmdlets.</span></span>
- <span data-ttu-id="e53ae-142">Para obter informações sobre como usar modelos do Azure Resource Manager, consulte o artigo Olá [recursos de barramento de serviço criar usando modelos do Azure Resource Manager](service-bus-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e53ae-142">For information about using Azure Resource Manager templates, see hello article [Create Service Bus resources using Azure Resource Manager templates](service-bus-resource-manager-overview.md).</span></span>
- <span data-ttu-id="e53ae-143">Informações sobre [Bibliotecas de gerenciamento .NET do Barramento de Serviço](service-bus-management-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="e53ae-143">Information about [Service Bus .NET management libraries](service-bus-management-libraries.md).</span></span>

<span data-ttu-id="e53ae-144">Há algumas formas alternativas toomanage entidades do barramento de serviço, conforme descrito nessas postagens de blog:</span><span class="sxs-lookup"><span data-stu-id="e53ae-144">There are some alternate ways toomanage Service Bus entities, as described in these blog posts:</span></span>

* [<span data-ttu-id="e53ae-145">Como toocreate Service Bus filas, tópicos e assinaturas usando um script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="e53ae-145">How toocreate Service Bus queues, topics and subscriptions using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [<span data-ttu-id="e53ae-146">Como toocreate um Namespace de barramento de serviço e um Hub de eventos usando um script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="e53ae-146">How toocreate a Service Bus Namespace and an Event Hub using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)
* [<span data-ttu-id="e53ae-147">Scripts do PowerShell do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="e53ae-147">Service Bus PowerShell Scripts</span></span>](https://code.msdn.microsoft.com/Service-Bus-PowerShell-a46b7059)

<!--Anchors-->

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
